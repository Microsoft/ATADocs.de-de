---
title: Azure Advanced Threat Protection-Rollengruppen für die Zugriffsverwaltung | Microsoft-Dokumentation
description: 'Exemplarische Vorgehensweise: Arbeit mit Azure ATP-Rollengruppen.'
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/07/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7ae3f0adca3137664f0a89c15e8feee71d0cd915
ms.sourcegitcommit: c4978be196e0039c7a5d5887bec4cbc5c01d64f9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/07/2018
ms.locfileid: "48848612"
---
*Gilt für: Azure Advanced Threat Protection*




# <a name="azure-atp-role-groups"></a>Azure ATP-Rollengruppen

Azure ATP bietet eine rollenbasierte Sicherheit, um Daten gemäß den spezifischen Sicherheits- und Konformitätsanforderungen einer Organisation zu schützen. Azure ATP unterstützt drei separate Rollen: Administratoren, Benutzer und Betrachter. 

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

Rollengruppen erlauben die Zugriffsverwaltung für Azure ATP. Sie können durch Verwendung von Rollengruppen Aufgaben in Ihrem Sicherheitsteam aufteilen und nur so viel Zugriff gewähren, wie Benutzer für die Ausführung ihrer Arbeit benötigen. Dieser Artikel beschreibt die Zugriffsverwaltung sowie die Berechtigungen der einzelnen Azure ATP-Rollengruppen und hilft Ihnen bei der Einrichtung und Ausführung von Rollengruppen in Azure ATP.

> [!NOTE]
> Sämtliche globalen Administratoren und Sicherheitsadministratoren für die Azure Active Directory-Version des Mandanten werden automatisch als Azure ATP-Administratoren angesehen.

## <a name="accessing-the-azure-atp-portal"></a>Zugreifen auf das Azure ATP-Portal

Nur Azure AD-Benutzer mit den Verzeichnisrollen „globaler Administrator“ oder „Sicherheitsadministrator“ können auf das Azure ATP-Portal (portal.atp.azure.com) zugreifen. Wenn Sie das Portal öffnen, können Sie Ihren Arbeitsbereich erstellen. Der Azure ATP-Dienst erstellt drei Sicherheitsgruppen in Ihrem Azure Active Directory-Mandanten: Administratoren, Benutzer, Viewer. 

> [!NOTE]
> Nur Benutzer, die zu der Azure ATP-Sicherheitsgruppe in Ihrem Azure Active Directory gehören sowie globale Administratoren und Sicherheitsadministratoren des Mandanten, können auf das Azure ATP-Portal zugreifen.


## <a name="types-of-azure-atp-security-groups"></a>Typen von Azure ATP-Sicherheitsgruppen 

Azure ATP stellt drei Typen von Sicherheitsgruppen bereit: *Arbeitsbereichsname* von Azure ATP-Administratoren, *Arbeitsbereichsname* von Azure ATP-Benutzern und *Arbeitsbereichsname* von Azure ATP-Viewern. Die folgende Tabelle beschreibt den Zugriffstyp im Azure ATP-Portal, der für jede Rolle verfügbar ist. Je nachdem, welche Rolle Sie zuweisen, stehen verschiedene Anzeigen und Menüoptionen im Azure ATP-Portal für folgende Benutzer nicht zur Verfügung:

|Aktivität |Azure ATP-Administratoren für *Arbeitsbereichsname*|Azure ATP-Benutzer für *Arbeitsbereichsname*|Azure ATP-Viewers für *Arbeitsbereichsname*|
|----|----|----|----|
|Anmeldung|Verfügbar|Verfügbar|Verfügbar|
|Der Status der Sicherheitswarnungen wurde geändert (erneut öffnen, schließen, ausschließen, unterdrücken)|Verfügbar|Verfügbar|Nicht verfügbar|
|Sicherheitswarnungen für Freigeben/Exportieren (über E-Mail, Link abrufen und Download von Details)|Verfügbar|Verfügbar|Verfügbar|
|Herunterladen eines Berichts|Verfügbar|Verfügbar|Verfügbar|
|Ändern des Status der Überwachung von Warnungen|Verfügbar|Nicht verfügbar|Nicht verfügbar|
|Aktualisieren der Azure ATP-Konfiguration: Sensoren (Download, Schlüssel neu generieren, konfigurieren, löschen)|Verfügbar|Nicht verfügbar|Nicht verfügbar|
|Aktualisieren der Azure ATP-Konfiguration: Datenquellen (Verzeichnisdienste, SIEM, VPN WD-ATP)|Verfügbar|Nicht verfügbar|Nicht verfügbar|
|Aktualisieren der Azure ATP-Konfiguration: Updates|Verfügbar|Nicht verfügbar|Nicht verfügbar|
|Aktualisieren der Azure ATP-Konfiguration: geplante Berichte|Verfügbar|Verfügbar|Nicht verfügbar|
|Aktualisieren der Azure ATP-Konfiguration: Entitätstags (vertraulich und Honeytoken)|Verfügbar|Verfügbar|Nicht verfügbar|
|Aktualisieren der Azure ATP-Konfiguration: Ausschlüsse|Verfügbar|Verfügbar|Nicht verfügbar|
|Aktualisieren der Azure ATP-Konfiguration: Sprache|Verfügbar|Verfügbar|Nicht verfügbar|
|Aktualisieren der Azure ATP-Konfiguration: Benachrichtigungen (E-Mail und Syslog)|Verfügbar|Verfügbar|Nicht verfügbar|
|Aktualisieren der Azure ATP-Konfiguration: Vorschau von Erkennungen|Verfügbar|Verfügbar|Nicht verfügbar|
|Anzeigen von Entitätsprofilen und Sicherheitswarnungen|Verfügbar|Verfügbar|Verfügbar|


Wenn Benutzer versuchen, auf eine Seite zuzugreifen, die nicht für deren Rollengruppe verfügbar ist, werden sie auf eine Azure ATP-Seite weitergeleitet, die ihnen mitteilt, dass Sie für den Zugriff nicht autorisiert sind. 

## <a name="add-and-remove-users"></a>Hinzufügen und Entfernen von Benutzern 


Azure ATP verwendet Azure AD-Sicherheitsgruppen als eine Basis für Rollengruppen. Die Rollengruppen können über [https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/GroupsManagementMenuBlade/All%20groups](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/GroupsManagementMenuBlade/All%20groups) verwaltet werden. Nur Azure AD-Benutzer können zu Sicherheitsgruppen hinzugefügt bzw. aus ihnen entfernt werden. 

## <a name="see-also"></a>Weitere Informationen
- [ATP-Tool zur Größenanpassung](http://aka.ms/aatpsizingtool)
- [ATP-Architektur](atp-architecture.md)
- [Install Azure ATP (Installieren von Azure ATP)](install-atp-step1.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)

