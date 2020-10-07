---
title: Azure Advanced Threat Protection Rollen Gruppen für die Zugriffs Verwaltung
description: 'Exemplarische Vorgehensweise: Arbeit mit Azure ATP-Rollengruppen.'
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 02/27/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d66d5c5af5721d94cb834307bb5a5ebee28848fc
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2020
ms.locfileid: "90910022"
---
# <a name="azure-atp-role-groups"></a>Azure ATP-Rollengruppen

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Azure ATP bietet eine rollenbasierte Sicherheit, um Daten gemäß den spezifischen Sicherheits- und Konformitätsanforderungen einer Organisation zu schützen. Azure ATP unterstützt drei separate Rollen: Administratoren, Benutzer und Betrachter.

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

Rollengruppen erlauben die Zugriffsverwaltung für Azure ATP. Sie können durch Verwendung von Rollengruppen Aufgaben in Ihrem Sicherheitsteam aufteilen und nur so viel Zugriff gewähren, wie Benutzer für die Ausführung ihrer Arbeit benötigen. Dieser Artikel beschreibt die Zugriffsverwaltung sowie die Berechtigungen der einzelnen Azure ATP-Rollengruppen und hilft Ihnen bei der Einrichtung und Ausführung von Rollengruppen in Azure ATP.

> [!NOTE]
> Sämtliche globalen Administratoren und Sicherheitsadministratoren für die Azure Active Directory-Version des Mandanten werden automatisch als Azure ATP-Administratoren angesehen.

## <a name="accessing-the-azure-atp-portal"></a>Zugreifen auf das Azure ATP-Portal

Nur Azure AD-Benutzer mit den Verzeichnisrollen „globaler Administrator“ oder „Sicherheitsadministrator“ können auf das Azure ATP-Portal (portal.atp.azure.com) zugreifen. Nachdem Sie das Portal mit der erforderlichen Rolle aufgerufen haben, können Sie Ihre Azure ATP-Instanz erstellen. Der Azure ATP-Dienst erstellt drei Sicherheitsgruppen in Ihrem Azure Active Directory-Mandanten: Administratoren, Benutzer, Viewer.

> [!NOTE]
> Nur Benutzer, die zu der Azure ATP-Sicherheitsgruppe in Ihrem Azure Active Directory gehören sowie globale und Sicherheitsadministratoren des Mandanten, können auf das Azure ATP-Portal zugreifen.

## <a name="types-of-azure-atp-security-groups"></a>Typen von Azure ATP-Sicherheitsgruppen

Azure ATP stellt drei Typen von Sicherheitsgruppen bereit: *Instanzname* von Azure ATP-Administratoren, *Instanzname* von Azure ATP-Benutzern und *Instanzname* von Azure ATP-Viewern. Die folgende Tabelle beschreibt den Zugriffstyp im Azure ATP-Portal, der für jede Rolle verfügbar ist. Je nachdem, welche Rolle Sie zuweisen, stehen verschiedene Anzeigen und Menüoptionen im Azure ATP-Portal für folgende Benutzer nicht zur Verfügung:

|Aktivität |Azure ATP *(Instanzname)* -Administratoren|Azure ATP *(Instanzname)* Benutzer|Azure ATP-Viewer *(Instanzname)*|
|----|----|----|----|
|Status von Integritäts Warnungen ändern|Verfügbar|Nicht verfügbar|Nicht verfügbar|
|Der Status der Sicherheitswarnungen wurde geändert (erneut öffnen, schließen, ausschließen, unterdrücken)|Verfügbar|Verfügbar|Nicht verfügbar|
|Löschen einer Instanz|Verfügbar|Nicht verfügbar|Nicht verfügbar|
|Herunterladen eines Berichts|Verfügbar|Verfügbar|Verfügbar|
|Anmelden|Verfügbar|Verfügbar|Verfügbar|
|Sicherheitswarnungen für Freigeben/Exportieren (über E-Mail, Link abrufen und Download von Details)|Verfügbar|Verfügbar|Verfügbar|
|Aktualisieren der Azure ATP-Konfiguration: Updates|Verfügbar|Nicht verfügbar|Nicht verfügbar|
|Aktualisieren der Azure ATP-Konfiguration: Entitätstags (vertraulich und Honeytoken)|Verfügbar|Verfügbar|Nicht verfügbar|
|Aktualisieren der Azure ATP-Konfiguration: Ausschlüsse|Verfügbar|Verfügbar|Nicht verfügbar|
|Aktualisieren der Azure ATP-Konfiguration: Sprache|Verfügbar|Verfügbar|Nicht verfügbar|
|Aktualisieren der Azure ATP-Konfiguration: Benachrichtigungen (E-Mail und Syslog)|Verfügbar|Verfügbar|Nicht verfügbar|
|Aktualisieren der Azure ATP-Konfiguration: Vorschau von Erkennungen|Verfügbar|Verfügbar|Nicht verfügbar|
|Aktualisieren der Azure ATP-Konfiguration: geplante Berichte|Verfügbar|Verfügbar|Nicht verfügbar|
|Aktualisieren der Azure ATP-Konfiguration: Datenquellen (Verzeichnisdienste, SIEM, VPN WD-ATP)|Verfügbar|Nicht verfügbar|Nicht verfügbar|
|Aktualisieren der Azure ATP-Konfiguration: Sensoren (Download, Schlüssel neu generieren, konfigurieren, löschen)|Verfügbar|Nicht verfügbar|Nicht verfügbar|
|Anzeigen von Entitätsprofilen und Sicherheitswarnungen|Verfügbar|Verfügbar|Verfügbar|

Wenn Benutzer versuchen, auf eine Seite zuzugreifen, die nicht für deren Rollengruppe verfügbar ist, werden sie auf eine Azure ATP-Seite weitergeleitet, die ihnen mitteilt, dass Sie für den Zugriff nicht autorisiert sind.

## <a name="add-and-remove-users"></a>Hinzufügen und Entfernen von Benutzern

Azure ATP verwendet Azure AD-Sicherheitsgruppen als eine Basis für Rollengruppen. Die Rollen Gruppen können von verwaltet werden [https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/GroupsManagementMenuBlade/All%20groups](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/GroupsManagementMenuBlade/All%20groups) . Nur Azure AD-Benutzer können zu Sicherheitsgruppen hinzugefügt bzw. aus ihnen entfernt werden.

## <a name="see-also"></a>Weitere Informationen

- [ATP-Tool zur Größenanpassung](https://aka.ms/aatpsizingtool)
- [ATP-Architektur](architecture.md)
- [Install Azure ATP (Installieren von Azure ATP)](install-step1.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)