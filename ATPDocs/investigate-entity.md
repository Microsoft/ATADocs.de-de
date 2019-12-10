---
title: Untersuchen von Benutzern und Computern mit Azure ATP | Microsoft-Dokumentation
description: Dieser Artikel beschreibt, wie verdächtige Aktivitäten, die von Benutzern ausgeführt werden, sowie Entitäten, Computer oder Geräte mithilfe von Azure Advanced Threat Protection (ATP) untersucht werden können.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/15/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6144f9f35e8ee3b7cec4b7522fe03a6a3e8673b0
ms.sourcegitcommit: 6dd002b5a34f230aaada55a6f6178c2f9e1584d9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2019
ms.locfileid: "71004749"
---
# <a name="tutorial-investigate-an-entity"></a>Tutorial: Untersuchen einer Entität

> [!NOTE]
> Die auf dieser Seite erläuterten Azure ATP-Features sind auch über das neue [Portal](https://portal.cloudappsecurity.com) zugänglich.

In diesem Tutorial erfahren Sie, wie Sie mit verdächtigen Aktivitäten in Verbindung stehende Objekte untersuchen können, die von Azure Advanced Threat Protection (ATP) erkannt werden. Nachdem eine Sicherheitswarnung in der Zeitleiste angezeigt wurde, können Sie einen Drilldown für die von der Warnung betroffene Entität durchführen und anhand der folgenden Parameter und Details herausfinden, was passiert ist und welche Schritte zur Risikominderung erforderlich sind.

> [!div class="checklist"]
> * Überprüfen des Entitätsprofils
> * Überprüfen von Entitätstags
> * Überprüfen der Flags für die Benutzerkontensteuerung
> * Gegenprüfung mit Windows Defender
> * Beachten der vertraulichen Benutzer und Gruppen
> * Überprüfen potenzieller Lateral Movement-Pfade
> * Überprüfen des Honeytoken-Status

## <a name="check-the-entity-profile"></a>Überprüfen des Entitätsprofils

Das Entitätsprofil bietet eine umfassende Entitätsseite, die für eine detaillierte Untersuchung von Benutzern, Computern, Geräten und Ressourcen, auf die sie zugreifen können, sowie auf deren Verlauf, ausgerichtet ist. Die Profilseite nutzt den neuen logischen Aktivitätenübersetzer von Azure ATP, der eine Gruppe von Aktivitäten (für bis zu eine Minute zusammengefasst) überprüfen und diese in genau eine logische Aktivität gruppieren kann, um die tatsächlichen Aktivitäten der Benutzer zu verdeutlichen.

Wenn Sie auf die Profilseite einer Entität zugreifen möchten, klicken Sie auf der Zeitachse der Sicherheitswarnung auf den Namen der Entität, z.B. einen Benutzernamen. Sie können auch eine Miniversion des Entitätsprofils auf der Seite der Sicherheitswarnung anzeigen, indem Sie mit der Maus auf den Entitätsnamen zeigen.

Über das Entitätsprofil können Sie Entitätsaktivitäten sowie Verzeichnisdaten und [Lateral Movement-Pfade](use-case-lateral-movement-path.md) für die Entität anzeigen. Weitere Informationen zu Entitäten finden Sie unter [Grundlegendes zu Entitätsprofilen](entity-profiles.md).

## <a name="check-entity-tags"></a>Überprüfen von Entitätstags

Azure ATP zieht Tags aus Active Directory, damit Sie eine einzelne Schnittstelle für die Überwachung Ihrer Active Directory-Benutzer und -Entitäten erhalten. Diese Tags stellen Informationen zu der Entität von Active Directory für Sie bereit, einschließlich:
- Teilweise: Dieser Benutzer, Computer oder diese Gruppe wurde von der Domäne nicht synchronisiert und über einen globalen Katalog teilweise aufgelöst. Einige Attribute sind nicht verfügbar.
- Nicht aufgelöst: Dieser Computer wurde nicht zu einer gültigen Entität in der Active Directory-Struktur aufgelöst. Es sind keine Verzeichnisinformationen verfügbar.
- Gelöscht: Die Entität wurde aus Active Directory gelöscht.
- Deaktiviert: Die Entität wurde in Active Directory deaktiviert.
- Gesperrt: Für die Entität wurde mehrmals ein falsches Kennwort eingegeben, und sie wurde gesperrt.
- Abgelaufen: Die Entität ist in Active Directory abgelaufen.
- Neu: Die Entität wurde vor weniger als 30 Tagen erstellt.

## <a name="check-user-account-control-flags"></a>Überprüfen der Flags für die Benutzerkontensteuerung

Die Flags für die Benutzerkontensteuerung werden ebenfalls von Active Directory importiert. Azure ATP-Entitätsverzeichnisdaten enthalten 10 Flags, die für die Untersuchung gültig sind: 
- Kennwort läuft nie ab
- Gilt für die Delegierung
- Smartcard erforderlich
- Kennwort abgelaufen
- Ein leeres Kennwort ist zulässig.
- Nur-Text-Kennwort gespeichert
- Kann nicht delegiert werden
- Nur DES-Verschlüsselung
- Kerberos-Vorauthentifizierung nicht erforderlich
- Konto deaktiviert 

Über Azure ATP erfahren Sie, ob diese Flags in Azure Active Directory aktiviert oder deaktiviert sind. Farbige Symbole und die entsprechende Umschaltfläche zeigen den Status der einzelnen Flags an. Im folgenden Beispiel ist nur **Kennwort läuft nie ab** in Active Directory aktiviert.

 ![Flags für die Benutzerkontensteuerung](./media/user-access-flags.png)

## <a name="cross-check-with-windows-defender"></a>Gegenprüfung mit Windows Defender

Um Ihnen produktübergreifende Einblicke zu gewähren, stellt Ihr Entitätsprofil Entitäten bereit, die Warnungen in Windows Defender mit einem Badge öffnen. Dieses Badge informiert Sie darüber, über wie viele offene Warnungen die Entität in Windows Defender verfügt und was der Schweregrad ist. Klicken Sie auf den Badge, um direkt zu den Warnungen zu wechseln, die dieser Entität in Windows Defender zugeordnet sind.


## <a name="keep-an-eye-on-sensitive-users-and-groups"></a>Beachten der vertraulichen Benutzer und Gruppen

Azure ATP importiert Benutzer- und Gruppeninformationen von Azure Active Directory, wodurch Sie identifizieren können, welche Benutzer automatisch als vertraulich eingestuft werden, da sie Mitglieder der folgenden Gruppen in Active Directory sind:

-   Administratoren
-   Hauptbenutzer
-   Konten-Operatoren
-   Server-Operatoren
-   Druck-Operatoren
-   Sicherungsoperatoren
-   Replikatoren
-   Remotedesktopbenutzer 
-   Netzwerkkonfigurations-Operatoren 
-   Eingehende Gesamtstruktur-Vertrauensstellung
-   Domänen-Admins
-   Domänencontroller
-   Gruppenrichtlinienersteller-Besitzer 
-   Schreibgeschützte Domänencontroller 
-   Schreibgeschützte Domänencontroller der Organisation 
-   Schema-Admins 
-   Organisations-Admins

Zusätzlich können Sie Entitäten **manuell markieren**, um darauf hinzuweisen, dass Sie in Azure ATP vertraulich sind. Dies ist wichtig, da einige Azure ATP-Erkennungsvorgänge, wie die Vorgänge zum Erkennen von Änderungen sensibler Gruppen und von Lateral Movement-Pfaden, sich auf den Vertraulichkeitsstatus der Entität verlassen. Wenn Sie zusätzliche Benutzer und Gruppen als sensibel markieren, z.B. Vorstandsmitglieder, leitende Angestellte und Verkaufsleiter, erkennt Azure ATP diese als sensibel an. Weitere Informationen finden Sie unter [Arbeiten mit sensiblen Konten](sensitive-accounts.md).

## <a name="review-lateral-movement-paths"></a>Überprüfen von Lateral Movement-Pfaden

Azure ATP kann Ihnen dabei helfen, Angriffe mit Lateral Movement-Pfaden zu verhindern. Lateral Movement bedeutet, dass ein Angreifer proaktiv nicht-sensible Konten benutzt, um Zugriff auf sensible Konten zu erhalten.

Wenn ein Lateral Movement-Pfad für eine Entität existiert, können Sie auf der Seite des Entiätsprofils auf die Registerkarte **Lateral Movement-Pfade** klicken. Das angezeigte Diagramm stellt Ihnen eine Übersicht der möglichen Pfade zu Ihrem sensiblen Benutzer bereit. 

Weitere Informationen finden Sie unter [Untersuchen von Angriffen mit Lateral Movement-Pfaden mit Azure ATP](use-case-lateral-movement-path.md).

## <a name="check-honeytoken-status"></a>Überprüfen des Honeytoken-Status

Bevor Sie mit Ihrer Untersuchung fortfahren, ist es wichtig, zu wissen, ob die Entität ein Honeytoken ist. Sie können Konten und Entitäten als Honeytoken in Azure ATP markieren. Wenn Sie das Entitäts- oder Miniprofil eines Kontos oder einer Entität öffnen, das bzw. die Sie als Honeytoken markiert haben, wird der Honeytokenbadge angezeigt. Der Honeytokenbadge warnt bei der Überprüfung, dass die unter Überprüfung stehende Aktivität von einem Konto ausgeführt wurde, das Sie als Honeytoken markiert haben.

## <a name="see-also"></a>Siehe auch

- [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
