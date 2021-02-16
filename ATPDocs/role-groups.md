---
title: Microsoft Defender für Identitäts Rollen Gruppen für die Zugriffs Verwaltung
description: Führt Sie durch die Arbeit mit Microsoft Defender für Identitäts Rollen Gruppen.
ms.date: 02/27/2020
ms.topic: conceptual
ms.openlocfilehash: 9ff271c8f417d3f2c15e3e6809b62986a7825db4
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533357"
---
# <a name="microsoft-defender-for-identity-role-groups"></a>Microsoft Defender für Identitäts Rollen Gruppen

[!INCLUDE [Product long](includes/product-long.md)] bietet rollenbasierte Sicherheit, um Daten gemäß den spezifischen Sicherheits-und Konformitätsanforderungen eines Unternehmens zu schützen. [!INCLUDE [Product short](includes/product-short.md)] Unterstützung von drei separaten Rollen: Administratoren, Benutzer und Viewer.

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

Rollen Gruppen ermöglichen die Zugriffs Verwaltung für [!INCLUDE [Product short](includes/product-short.md)] . Sie können durch Verwendung von Rollengruppen Aufgaben in Ihrem Sicherheitsteam aufteilen und nur so viel Zugriff gewähren, wie Benutzer für die Ausführung ihrer Arbeit benötigen. Dieser Artikel erläutert die Zugriffs Verwaltung, die [!INCLUDE [Product short](includes/product-short.md)] Rollen Autorisierung und hilft Ihnen bei der Einrichtung und Ausführung von Rollen Gruppen in [!INCLUDE [Product short](includes/product-short.md)] .

> [!NOTE]
> Alle globalen Administratoren oder Sicherheits Administratoren für den Azure Active Directory des Mandanten werden automatisch als [!INCLUDE [Product short](includes/product-short.md)] Administrator angemeldet.

## <a name="accessing-the-defender-for-identity-portal"></a>Zugreifen auf das Defender für Identity-Portal

Der Zugriff auf das [!INCLUDE [Product short](includes/product-short.md)] Portal (Portal.ATP.Azure.com) kann nur von einem Azure AD Benutzer durchgeführt werden, der über die Verzeichnis Rolle "globaler Administrator" oder "Sicherheitsadministrator" verfügt. Nachdem Sie das Portal mit der erforderlichen Rolle eingegeben haben, können Sie die- [!INCLUDE [Product short](includes/product-short.md)] Instanz erstellen. [!INCLUDE [Product short](includes/product-short.md)] der-Dienst erstellt drei Sicherheitsgruppen in Ihrem Azure Active Directory-Mandanten: Administratoren, Benutzer, Viewer.

> [!NOTE]
> Der Zugriff auf das [!INCLUDE [Product short](includes/product-short.md)] Portal wird nur Benutzern innerhalb der [!INCLUDE [Product short](includes/product-short.md)] Sicherheitsgruppen innerhalb ihrer Azure Active Directory sowie der globalen und Sicherheits Administratoren des Mandanten gewährt.

## <a name="types-of-defender-for-identity-security-groups"></a>Typen von Defender für Identitäts Sicherheitsgruppen

[!INCLUDE [Product short](includes/product-short.md)] bietet drei Arten von Sicherheitsgruppen: Azure ATP *(Instanzname)* Administratoren, Azure ATP *(Instanzname)* Benutzer und Azure ATP-Viewer *(Instanzname)* . In der folgenden Tabelle wird der Zugriffstyp im Portal beschrieben, der [!INCLUDE [Product short](includes/product-short.md)] für die einzelnen Rollen verfügbar ist. Je nachdem, welche Rolle Sie zuweisen, sind verschiedene Bildschirme und Menü Optionen im [!INCLUDE [Product short](includes/product-short.md)] Portal für diese Benutzer wie folgt nicht verfügbar:

|Aktivität |Azure ATP *(Instanzname)* -Administratoren|Azure ATP *(Instanzname)* Benutzer|Azure ATP-Viewer *(Instanzname)*|
|----|----|----|----|
|Status von Integritäts Warnungen ändern|Verfügbar|Nicht verfügbar|Nicht verfügbar|
|Der Status der Sicherheitswarnungen wurde geändert (erneut öffnen, schließen, ausschließen, unterdrücken)|Verfügbar|Verfügbar|Nicht verfügbar|
|Löschen einer Instanz|Verfügbar|Nicht verfügbar|Nicht verfügbar|
|Herunterladen eines Berichts|Verfügbar|Verfügbar|Verfügbar|
|Anmelden|Verfügbar|Verfügbar|Verfügbar|
|Sicherheitswarnungen für Freigeben/Exportieren (über E-Mail, Link abrufen und Download von Details)|Verfügbar|Verfügbar|Verfügbar|
|Aktualisieren der [!INCLUDE [Product short](includes/product-short.md)] Konfiguration: Updates|Verfügbar|Nicht verfügbar|Nicht verfügbar|
|Aktualisieren der [!INCLUDE [Product short](includes/product-short.md)] Konfiguration: Entitäts Tags (sensitive und honeytoken)|Verfügbar|Verfügbar|Nicht verfügbar|
|Update [!INCLUDE [Product short](includes/product-short.md)] Konfiguration-Ausschlüsse|Verfügbar|Verfügbar|Nicht verfügbar|
|Aktualisieren der [!INCLUDE [Product short](includes/product-short.md)] Konfigurationssprache|Verfügbar|Verfügbar|Nicht verfügbar|
|Aktualisieren der [!INCLUDE [Product short](includes/product-short.md)] Konfiguration: Benachrichtigungen (e-Mail und syslog)|Verfügbar|Verfügbar|Nicht verfügbar|
|Aktualisieren der [!INCLUDE [Product short](includes/product-short.md)] Konfiguration: Vorschau Erkennungen|Verfügbar|Verfügbar|Nicht verfügbar|
|Aktualisieren der [!INCLUDE [Product short](includes/product-short.md)] Konfiguration-geplante Berichte|Verfügbar|Verfügbar|Nicht verfügbar|
|Aktualisieren der [!INCLUDE [Product short](includes/product-short.md)] Konfiguration: Datenquellen (Verzeichnisdienste, Siem, VPN, WD, ATP)|Verfügbar|Nicht verfügbar|Nicht verfügbar|
|Aktualisieren der [!INCLUDE [Product short](includes/product-short.md)] Konfiguration: Sensoren (Download, Schlüssel neu generieren, konfigurieren, löschen)|Verfügbar|Nicht verfügbar|Nicht verfügbar|
|Anzeigen von Entitätsprofilen und Sicherheitswarnungen|Verfügbar|Verfügbar|Verfügbar|

Wenn Benutzer versuchen, auf eine Seite zuzugreifen, die nicht für Ihre Rollen Gruppe verfügbar ist, werden Sie auf die Seite "nicht autorisiert" umgeleitet [!INCLUDE [Product short](includes/product-short.md)] .

## <a name="add-and-remove-users"></a>Hinzufügen und Entfernen von Benutzern

[!INCLUDE [Product short](includes/product-short.md)] verwendet Azure AD Sicherheitsgruppen als Grundlage für Rollen Gruppen. Die Rollen Gruppen können über die [Seite Gruppenverwaltung](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/GroupsManagementMenuBlade/All%20groups)verwaltet werden. Nur Azure AD-Benutzer können zu Sicherheitsgruppen hinzugefügt bzw. aus ihnen entfernt werden.

## <a name="see-also"></a>Weitere Informationen

- [[!INCLUDE [Product short](includes/product-short.md)]-Tool zur Größenanpassung](https://aka.ms/aatpsizingtool)
- [[!INCLUDE [Product short](includes/product-short.md)]-Architektur](architecture.md)
- [Installieren von [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
