---
title: Konformität, Vertrauensstellung, Datensicherheit und Datenschutz von Advanced Threat Analytics | Microsoft-Dokumentation
description: Stellt eine Liste von Links zu ATA-Ressourcen, Videos, ersten Schritten sowie zur Bereitstellung und zum Überblick für die Bereitschaft bereit.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/16/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1b2d185c-62cd-45f0-b0dd-687b51317f32
ms.reviewer: ophirp
ms.suite: ems
ms.openlocfilehash: dee55446c18ee9bc560045c94f9421840fc28fc2
ms.sourcegitcommit: 714a01edc9006b38d1163d03852dafc2a5fddb5f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2018
---
*Gilt für: Advanced Threat Analytics Version 1.9*

# <a name="ata-compliance-trust-data-security-and-privacy"></a>Konformität, Vertrauensstellung, Datensicherheit und Datenschutz von ATA 

Informationen zur Vertrauensstellung und Konformität von ATA finden Sie im [Service Trust Portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted) und auf der Website zur [Microsoft 365-GDPR-Konformität](https://docs.microsoft.com/microsoft-365/compliance/compliance-solutions-overview).

## <a name="searching-for-and-identifying-personal-data"></a>Suchen und Ermitteln von personenbezogenen Daten 

Alle entitätsbezogenen Daten in ATA stammen aus Active Directory (AD) und werden von dort aus zu ATA repliziert. Bei der Suche nach personenbezogenen Daten sollten Sie zuerst in AD nachsehen. 

Verwenden Sie die Suchleiste im ATA Center, um die identifizierbaren personenbezogenen Daten anzuzeigen, die in der Datenbank gespeichert sind. Benutzer können nach einem bestimmten Benutzer oder einem bestimmten Gerät suchen. Durch einen Klick auf die Entität wird die Profilseite des Benutzers oder des Geräts geöffnet. Das Profil bietet Ihnen umfassende Details zu der Entität, deren Versionsgeschichte und verknüpfte Netzwerkaktivität, die aus AD stammt. 

## <a name="updating-personal-data"></a>Aktualisieren von personenbezogenen Daten 

Personenbezogene Daten zu Benutzern und Entitäten in ATA stammen aus dem Objekt des Benutzers im AD Ihrer Organisation. Aus diesem Grund werden alle Änderungen am Benutzerprofil AD in ATA übernommen. 

## <a name="deleting-personal-data"></a>Löschen von personenbezogenen Daten 

Obwohl Daten in ATA repliziert sind und immer aus Active Directory aktualisiert werden, werden die Entitätsdaten in ATA zu Sicherheitszwecken beibehalten, wenn eine Entität in AD gelöscht wird. 

Gehen Sie folgendermaßen vor, um die benutzerspezifischen Daten dauerhaft aus der ATA-Datenbank zu löschen: 

1. [Laden Sie das Skript „MongoDB“ (gdpr.js) herunter.](https://aka.ms/ata-gdpr-script)  

2. Kopieren Sie das Skript auf den ATA Center-Computer, und führen Sie dort den folgenden Befehl aus: 

Verwenden Sie ATA-GDPR-Datenbankskripts, um Entitäten und Aktivitätsdaten von Entitäten zu löschen. Dies wird in den folgenden Abschnitten beschrieben.

### <a name="delete-entities"></a>Löschen von Einträgen

Diese Aktion löscht eine Entität endgültig aus der ATA-Datenbank. Wenn Sie diesen Befehl ausführen möchten, stellen Sie den Befehlsnamen `deleteAccount` und `SamName`, `UpnName` oder `GUID` für den Computer oder Benutzernamen bereit, die Sie löschen möchten. Beispiel: 

`C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongo.exe" ATA --eval “var params= deleteAccount,admin1@contoso.com;” GDPR.js `

Durch das Ausführen wird die Entität mit dem UPN admin1@contoso.com zusammen mit allen der Entität zugeordneten Aktivitäten und Sicherheitswarnungen vollständig aus der Datenbank entfernt. 

### <a name="delete-entity-activity-data"></a>Löschen von Daten zur Entitätsaktivität

Diese Aktion löscht die Aktivitäten einer Entität endgültig aus der ATA-Datenbank. Alle Entitäten bleiben unverändert, aber ihre Aktivitäten und Sicherheitswarnungen werden für den angegebenen Zeitraum gelöscht. 

Geben Sie zum Ausführen dieses Befehls den Befehlsnamen `deleteOldData` und die Anzahl der Tage für die Daten an, die Sie in der Datenbank aufbewahren möchten. 

Beispiel: 

`C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongo.exe" ATA --eval “var params= deleteOldData,30;” GDPR.js`

Dieses Skript entfernt die Daten aller Entitätsaktivitäten und Sicherheitswarnungen aus der Datenbank, die älter als 30 Tage sind. Es werden nur die Daten der letzten 30 Tage aufbewahrt.

## <a name="exporting-personal-data"></a>Exportieren von personenbezogenen Daten 

Da die entitätsbezogenen Daten in ATA aus AD stammen, wird nur eine Teilmenge der Daten in der ATA-Datenbank gespeichert. Aus diesem Grund sollten Sie die entitätsbezogenen Daten aus AD exportieren. 

Mit ATA können Sie alle sicherheitsrelevanten Informationen nach Excel exportieren, einschließlich personenbezogener Daten. 

 
## <a name="opt-out-of-telemetry"></a>Deaktivieren der Telemetrie 

ATA sammelt anonymisierte Telemetriedaten zu jeder Bereitstellung und überträgt diese über HTTPS an die Microsoft-Server. Diese Daten werden von Microsoft zur Verbesserung von zukünftigen ATA-Versionen verwendet. 

Weitere Informationen finden Sie unter [Verwalten von Telemetrieeinstellungen](manage-telemetry-settings.md).

So deaktivieren Sie das Erfassen von Daten:

1. Melden Sie sich bei der ATA-Konsole an, klicken Sie auf der Symbolleiste auf die drei Punkte, und wählen Sie **Info** aus. 
2. Deaktivieren Sie das Kontrollkästchen für **Senden Sie uns Nutzungsinformationen, um uns bei der Verbesserung der Benutzerfreundlichkeit zu unterstützen**. 

 

 

 

## <a name="additional-resources"></a>Zusätzliche Ressourcen

[Seite zu Microsoft Security Channel 9](https://channel9.msdn.com/Shows/Microsoft-Security/)

## <a name="community-resources"></a>Communityressourcen

[ATA-Blog](https://aka.ms/ATABlog)
[ATA-Community](https://aka.ms/ATACommunity)
[Feedback zu ATA](https://aka.ms/ATAUserVoice)