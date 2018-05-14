---
title: Untersuchen von Benutzern und Computern mit Azure ATP | Microsoft-Dokumentation
description: Dieser Artikel beschreibt, wie verdächtige Aktivitäten, die von Benutzern ausgeführt werden, sowie Entitäten, Computer oder Geräte mithilfe von Azure Advanced Threat Protection (ATP) untersucht werden können.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/6/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4ef4151a311dd5b076737cba9f3c7aa7454a32a7
ms.sourcegitcommit: 39a1ddeb6c9dd0817f92870b711627350b7f6f03
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/08/2018
---
*Gilt für: Azure Advanced Threat Protection Version 1.9*



# <a name="investigate-an-entity-with-azure-atp"></a>Untersuchen einer Entität mit Azure ATP

In diesem Artikel wird der Prozess zum Untersuchen von Entitäten beschrieben, nachdem verdächtige Aktivitäten mit Azure Advanced Threat Protection (ATP) erkannt wurden. Nachdem eine verdächtige Aktivität in der Zeitleiste angezeigt wurde, können Sie die in der Aktivität betroffene Entität detailliert anzeigen und die folgenden Parameter und Details verwenden, um zu erfahren, was passiert ist und was Sie tun müssen, um das Risiko einzuschränken.

## <a name="look-at-the-entity-profile"></a>Anzeigen des Entitätsprofils

Über das Entitätsprofil erhalten Sie eine umfassende Entitätsseite, die für eine detaillierte Untersuchung von Benutzern, Computern, Geräten und Ressourcen, auf die sie zugreifen können, sowie auf deren Verlauf, ausgerichtet ist. Die Profilseite nutzt den neuen logischen Aktivitätenübersetzer von Azure ATP, der eine Gruppe von Aktivitäten (für bis zu eine Minute zusammengefasst) überprüfen und diese in genau eine logische Aktivität gruppieren kann, um die tatsächlichen Aktivitäten der Benutzer zu verdeutlichen.

Wenn Sie auf die Profilseite einer Entität zugreifen möchten, klicken Sie auf der Zeitachse der verdächtigen Aktivität auf den Namen der Entität, z.B. den Benutzernamen. Sie können auch eine Miniversion des Entitätsprofils auf der Seite der verdächtigen Aktivität anzeigen, indem Sie mit der Maus auf den Entitätsnamen zeigen.

Über das Entitätsprofil können Sie Entitätsaktivitäten sowie Verzeichnisdaten und Lateral Movement-Pfade für die Entität anzeigen. Weitere Informationen finden Sie unter [Untersuchen von Entitätsprofilen](entity-profiles.md).

## <a name="check-entity-tags"></a>Überprüfen von Entitätstags

Azure ATP zieht Tags aus Active Directory, damit Sie eine einzelne Schnittstelle für die Überwachung Ihrer Active Directory-Benutzer und -Entitäten erhalten. Diese Tags stellen Informationen zu der Entität von Active Directory für Sie bereit, einschließlich:
- Partiell: Dieser Benutzer, Computer oder diese Gruppe wurde von der Domäne nicht synchronisiert und wurde über einen globalen Katalog partiell aufgelöst. Einige Attribute sind nicht verfügbar.
- Nicht aufgelöst: Dieser Computer wurde nicht zu einer gültigen Entität in der Active Directory-Struktur aufgelöst. Es sind keine Verzeichnisinformationen verfügbar.
- Gelöscht: Die Entität wurde aus Active Directory gelöscht.
- Deaktiviert: Die Entität wurde in Active Directory deaktiviert.
- Gesperrt: Für die Entität wurde mehrmals ein falsches Kennwort eingegeben, und sie wurde gesperrt.
- Abgelaufen: Die Entität ist in Active Directory abgelaufen.
- Neu: Die Entität wurde vor weniger als 30 Tagen erstellt.

## <a name="look-at-the-user-access-control-flags"></a>Anzeigen der Flags für die Benutzerzugriffssteuerung

Die Flags für die Benutzerzugriffssteuerung werden ebenfalls von Active Directory importiert. Azure ATP enthält 10 Flags, die für die Untersuchung gültig sind: 
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

Über Azure ATP erfahren Sie, ob diese Flags in Azure Active Directory aktiviert oder deaktiviert sind. Bunte Symbole weisen darauf hin, dass das Flag in Active Directory aktiviert ist. Im Beispiel unten ist nur **Konto deaktiviert** in Active Directory aktiviert.

 ![Flags für die Benutzerzugriffssteuerung](./media/user-access-flags.png)

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

## <a name="be-aware-of-lateral-movement-paths"></a>Bedenken von Lateral Movement-Pfaden

Azure ATP kann Ihnen dabei helfen, Angriffe mit Lateral Movement-Pfaden zu verhindern. Lateral Movement bedeutet, dass ein Angreifer proaktiv nicht-sensible Konten benutzt, um Zugriff auf sensible Konten zu erhalten.

Wenn ein Lateral Movement-Pfad für eine Entität existiert, können Sie auf der Seite des Entiätsprofils auf die Registerkarte **Lateral Movement-Pfade** klicken. Das angezeigte Diagramm stellt Ihnen eine Übersicht der möglichen Pfade zu Ihrem sensiblen Benutzer bereit. 

Weitere Informationen finden Sie unter [Untersuchen von Angriffen mit Lateral Movement-Pfaden mit Azure ATP](use-case-lateral-movement-path.md).


## <a name="is-it-a-honeytoken-entity"></a>Handelt es sich um eine Honeytoken-Entität?

Bevor Sie mit Ihrer Untersuchung fortfahren, ist es wichtig, zu wissen, ob die Entität ein Honeytoken ist. Der Einfachheit halber ermöglicht Azure ATP die Markierung von Konten und Entitäten als Honeytoken. Während der Untersuchung wird dann beim Öffnen des Entitätsprofils oder Miniprofils der Honeytokenbadge angezeigt, um Sie zu warnen, dass die Aktivität, die Sie sich gerade ansehen, von einem Konto durchgeführt wurde, das Sie als Honeytoken markiert haben.


    
## <a name="see-also"></a>Siehe auch

- [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)