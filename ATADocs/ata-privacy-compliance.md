---
title: Advanced Threat Analytics-Richtlinie für persönliche Daten
description: Dieser Artikel stellt Links zu Informationen bereit, wie Sie private Informationen und personenbezogene Daten aus ATA löschen.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 9/27/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1b2d185c-62cd-45f0-b0dd-687b51317f32
ms.reviewer: ophirp
ms.suite: ems
ms.openlocfilehash: ed811af8f046aff1249e30ac1c7c5585b07f9f88
ms.sourcegitcommit: fbb0768c392f9bccdd7e4adf0e9a0303c8d1922c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2020
ms.locfileid: "84774926"
---
# <a name="ata-data-security-and-privacy"></a>Sicherheit und Datenschutz für ATA

*Gilt für: Advanced Threat Analytics Version 1.9*

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

## <a name="searching-for-and-identifying-personal-data"></a>Suchen nach und Identifizieren von personenbezogenen Daten 

Alle entitätsbezogenen Daten in ATA stammen aus Active Directory (AD) und werden von dort aus zu ATA repliziert. Bei der Suche nach personenbezogenen Daten sollten Sie zuerst in AD nachsehen. 

Verwenden Sie die Suchleiste im ATA Center, um die identifizierbaren personenbezogenen Daten anzuzeigen, die in der Datenbank gespeichert sind. Benutzer können nach einem bestimmten Benutzer oder einem bestimmten Gerät suchen. Durch einen Klick auf die Entität wird die Profilseite des Benutzers oder des Geräts geöffnet. Das Profil bietet Ihnen umfassende Details zu der Entität, deren Versionsgeschichte und verknüpfte Netzwerkaktivität, die aus AD stammt. 

## <a name="updating-personal-data"></a>Aktualisieren personenbezogener Daten 

Personenbezogene Daten zu Benutzern und Entitäten in ATA stammen aus dem Objekt des Benutzers im AD Ihrer Organisation. Aus diesem Grund werden alle Änderungen am Benutzerprofil AD in ATA übernommen. 

## <a name="deleting-personal-data"></a>Löschen von personenbezogenen Daten 

Obwohl Daten in ATA repliziert sind und immer aus Active Directory aktualisiert werden, werden die Entitätsdaten in ATA zu Sicherheitszwecken beibehalten, wenn eine Entität in AD gelöscht wird. 

Gehen Sie folgendermaßen vor, um die benutzerspezifischen Daten dauerhaft aus der ATA-Datenbank zu löschen: 

1. [Laden Sie das Skript „MongoDB“ (gdpr.js) herunter.](https://aka.ms/ata-gdpr-script)  

2. Kopieren Sie das Skript in den ATA-Ordner (unter `"C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB`), und führen Sie den folgenden Befehl auf dem ATA Center-Computer aus: 

Verwenden Sie ATA-GDPR-Datenbankskripts, um Entitäten und Aktivitätsdaten von Entitäten zu löschen. Dies wird in den folgenden Abschnitten beschrieben.

### <a name="delete-entities"></a>Löschen von Entitäten

Diese Aktion löscht eine Entität endgültig aus der ATA-Datenbank. Wenn Sie diesen Befehl ausführen möchten, stellen Sie den Befehlsnamen `deleteAccount` und `SamName`, `UpnName` oder `GUID` für den Computer oder Benutzernamen bereit, die Sie löschen möchten. Beispiel: 

`"C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongo.exe" ATA --eval "var params='deleteAccount,admin1@contoso.com';" GDPR.js`

Durch das Ausführen wird die Entität mit dem UPN admin1@contoso.com zusammen mit allen der Entität zugeordneten Aktivitäten und Sicherheitswarnungen vollständig aus der Datenbank entfernt. 

### <a name="delete-entity-activity-data"></a>Löschen von Daten zur Entitätsaktivität

Diese Aktion löscht die Aktivitäten einer Entität endgültig aus der ATA-Datenbank. Alle Entitäten bleiben unverändert, aber ihre Aktivitäten und Sicherheitswarnungen werden für den angegebenen Zeitraum gelöscht. 

Geben Sie zum Ausführen dieses Befehls den Befehlsnamen `deleteOldData` und die Anzahl der Tage für die Daten an, die Sie in der Datenbank aufbewahren möchten. 

Beispiel: 

`"C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongo.exe" ATA --eval "var params='deleteOldData,30';" GDPR.js`

Dieses Skript entfernt die Daten aller Entitätsaktivitäten und Sicherheitswarnungen aus der Datenbank, die älter als 30 Tage sind. Es werden nur die Daten der letzten 30 Tage aufbewahrt.

## <a name="exporting-personal-data"></a>Exportieren von personenbezogenen Daten 

Da die entitätsbezogenen Daten in ATA aus AD stammen, wird nur eine Teilmenge der Daten in der ATA-Datenbank gespeichert. Aus diesem Grund sollten Sie die entitätsbezogenen Daten aus AD exportieren. 

Mit ATA können Sie alle sicherheitsrelevanten Informationen nach Excel exportieren, einschließlich personenbezogener Daten. 

 
## <a name="opt-out-of-system-generated-logs"></a>Deaktivieren von systemgenerierten Protokollen 

ATA sammelt anonymisierte systemgenerierte Protokolle zu jeder Bereitstellung und überträgt diese über HTTPS an die Microsoft-Server. Diese Daten werden von Microsoft zur Verbesserung von zukünftigen ATA-Versionen verwendet. 

Weitere Informationen finden Sie unter [Manage system-generated logs (Verwalten von systemgenerierten Protokollen)](manage-telemetry-settings.md).

So deaktivieren Sie die Datensammlung:

1. Melden Sie sich bei der ATA-Konsole an, klicken Sie auf der Symbolleiste auf die drei Punkte, und wählen Sie **Info** aus. 
2. Deaktivieren Sie das Kontrollkästchen für **Senden Sie uns Nutzungsinformationen, um uns bei der Verbesserung der Benutzerfreundlichkeit zu unterstützen**. 

## <a name="additional-resources"></a>Zusätzliche Ressourcen

- Informationen zur Vertrauensstellung und Konformität von ATA finden Sie im [Service Trust Portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted) und auf der Website zur [Microsoft 365-GDPR-Konformität](https://docs.microsoft.com/microsoft-365/compliance/compliance-solutions-overview).
