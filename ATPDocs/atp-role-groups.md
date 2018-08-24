---
title: Azure Advanced Threat Protection-Rollengruppen für die Zugriffsverwaltung | Microsoft-Dokumentation
description: 'Exemplarische Vorgehensweise: Arbeit mit Azure ATP-Rollengruppen.'
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/15/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a6b4f668533ab3169c10cfc9b194b8bd392db6d1
ms.sourcegitcommit: 121c49d559e71741136db1626455b065e8624ff9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2018
ms.locfileid: "41734516"
---
*Gilt für: Azure Advanced Threat Protection*




# <a name="azure-atp-role-groups"></a>Azure ATP-Rollengruppen

Azure ATP bietet eine rollenbasierte Sicherheit, um Daten gemäß den spezifischen Sicherheits- und Konformitätsanforderungen einer Organisation zu schützen. Azure ATP unterstützt drei separate Rollen: Administratoren, Benutzer und Betrachter. 

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

Rollengruppen erlauben die Zugriffsverwaltung für Azure ATP. Sie können durch Verwendung von Rollengruppen Aufgaben in Ihrem Sicherheitsteam aufteilen und nur so viel Zugriff gewähren, wie Benutzer für die Ausführung ihrer Arbeit benötigen. Dieser Artikel beschreibt die Zugriffsverwaltung sowie die Berechtigungen der einzelnen Azure ATP-Rollengruppen und hilft Ihnen bei der Einrichtung und Ausführung von Rollengruppen in ATP.

> [!NOTE]
> Sämtliche globalen Administratoren und Sicherheitsadministratoren für die Azure Active Directory-Version des Mandanten werden automatisch als Azure ATP-Administratoren angesehen.

## <a name="accessing-the-management-portal"></a>Zugreifen auf das Verwaltungsportal

Nur Azure AD-Benutzer mit den Verzeichnisrollen „globaler Administrator“ oder „Sicherheitsadministrator“ können auf das Verwaltungsportal (portal.atp.azure.com) zugreifen. Wenn Sie das Portal öffnen, können Sie Ihren Arbeitsbereich erstellen. Der Azure ATP-Dienst erstellt drei Sicherheitsgruppen in Ihrem Azure Active Directory-Mandanten: Administratoren, Benutzer, Viewer. 

> [!NOTE]
> Nur Benutzer, die zu der Azure AD-Sicherheitsgruppe für diesen Arbeitsbereich gehören sowie globale Administratoren und Sicherheitsadministratoren, können auf das Azure ATP-Arbeitsbereichsportal zugreifen.


## <a name="types-of-azure-atp-security-groups"></a>Typen von Azure ATP-Sicherheitsgruppen 

Azure ATP umfasst drei Typen von Sicherheitsgruppen: *Arbeitsbereichsname* von Azure ATP-Administratoren, *Arbeitsbereichsname* von Azure ATP-Benutzern und *Arbeitsbereichsname* von Azure ATP-Viewern. Die folgende Tabelle beschreibt den Zugriffstyp im Azure ATP-Arbeitsbereichsportal, der pro Rolle verfügbar ist. Je nachdem, welche Rolle Sie zuweisen, stehen verschiedene Anzeigen und Menüoptionen im Azure ATP-Arbeitsbereich nicht zur Verfügung:

|Aktivität |Azure ATP-Administratoren für *Arbeitsbereichsname*|Azure ATP-Benutzer für *Arbeitsbereichsname*|Azure ATP-Viewers für *Arbeitsbereichsname*|
|----|----|----|----|
|Anmeldung|Verfügbar|Verfügbar|Verfügbar|
|Ändern des Status von verdächtigen Aktivitäten|Verfügbar|Verfügbar|Nicht verfügbar|
|Freigeben/Exportieren von verdächtiger Aktivität über E-Mail/Abruflink|Verfügbar|Verfügbar|Verfügbar|
|Ändern des Status der Überwachung von Warnungen|Verfügbar|Nicht verfügbar|Nicht verfügbar|
|Aktualisieren der Azure ATP-Konfiguration|Verfügbar|Nicht verfügbar|Nicht verfügbar|
|Sensor: hinzufügen|Verfügbar|Nicht verfügbar|Nicht verfügbar|
|Sensor: löschen |Verfügbar|Nicht verfügbar|Nicht verfügbar|
|Überwachter DC – Hinzufügen |Verfügbar|Nicht verfügbar|Nicht verfügbar|
|Überwachter DC – Löschen|Verfügbar|Nicht verfügbar|Nicht verfügbar|
|Anzeigen von Warnungen und verdächtigen Aktivitäten|Verfügbar|Verfügbar|Verfügbar|


Wenn Benutzer versuchen, auf eine Seite zuzugreifen, die nicht für deren Rollengruppe verfügbar ist, werden sie auf eine Azure ATP-Seite weitergeleitet, die ihnen mitteilt, dass Sie für den Zugriff nicht autorisiert sind. 

## <a name="add-and-remove-users"></a>Hinzufügen und Entfernen von Benutzern 


Azure ATP verwendet Azure AD-Sicherheitsgruppen als eine Basis für Rollengruppen. Die Rollengruppen können über [https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/GroupsManagementMenuBlade/All%20groups](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/GroupsManagementMenuBlade/All%20groups) verwaltet werden. Nur Azure AD-Benutzer können zu Sicherheitsgruppen hinzugefügt bzw. aus ihnen entfernt werden. 

## <a name="see-also"></a>Weitere Informationen
- [Tool zur Bemessung von ATA-Gateways](http://aka.ms/aatpsizingtool)
- [ATA-Architektur](atp-architecture.md)
- [Installieren von ATA](install-atp-step1.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)

