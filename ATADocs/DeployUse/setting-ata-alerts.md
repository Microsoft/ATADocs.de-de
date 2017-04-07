---
title: Festlegen von Advanced Threat Analytics-Benachrichtigungen | Microsoft-Dokumentation
description: "Beschreibt, wie ATA-Warnungen festgelegt werden, damit Sie bei verdächtigen Aktivitäten benachrichtigt werden."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 06aa85cededdc3647aadaaca7d594ce3bbbb0723
ms.sourcegitcommit: 49e892a82275efa5146998764e850959f20d3216
translationtype: HT
---
*Gilt für: Advanced Threat Analytics Version 1.7*



# <a name="set-ata-notifications"></a>Festlegen von ATA-Benachrichtigungen
ATA kann Sie bei Erkennen einer verdächtigen Aktivität per E-Mail oder über ATA-Ereignisweiterleitung benachrichtigen und das Ereignis an den SIEM-/Syslog-Server weiterleiten. Bevor Sie auswählen, welche Benachrichtigungen Sie erhalten möchten, müssen Sie [Ihren E-Mail-Server und Ihren Syslog-Server einrichten](setting-syslog-email-server-settings.md).

> [!NOTE]
> -   E-Mail-Benachrichtigungen enthalten einen Link, mit denen der Benutzer direkt die erkannte verdächtige Aktivität aufrufen kann. Der Hostnamenteil des Links wird von der Einstellung für die ATA-Konsolen-URL auf der Seite „ATA Center“ übernommen. Standardmäßig ist die URL der ATA-Konsole die IP-Adresse, die während der Installation von ATA Center ausgewählt wurde.  Wenn Sie das Konfigurieren von E-Mail-Benachrichtigungen beabsichtigen, wird die Verwendung eines FQDN als URL der ATA-Konsole empfohlen.
> -   Benachrichtigungen werden von ATA Center entweder an den SMTP-Server oder an den Syslog-Server gesendet.

## <a name="mail-notifications"></a>E-Mail-Benachrichtigungen
Um E-Mail-Benachrichtigungen zu erhalten, legen Sie Folgendes fest:


1. Wählen Sie in der ATA-Konsole auf der Symbolleiste die Einstellungsoption aus, und wählen Sie dann **Konfiguration** aus.
![Symbol der ATA-Konfigurationseinstellungen](media/ATA-config-icon.JPG)

2. Wählen Sie **Einstellungen** im Abschnitt **Benachrichtigungen** aus.
3. Geben Sie unter **E-Mail-Empfänger** die Empfänger an, die die Benachrichtigungen per E-Mail erhalten sollen.
>    [!NOTE]
>   E-Mail-Benachrichtigungen über verdächtige Aktivitäten werden nur beim Erstellen der verdächtigen Aktivität gesendet.

4. Verwenden Sie die Optionen unter **Benachrichtigen, wenn:**, um auszuwählen, welche Benachrichtigungen gesendet werden sollen:
  - Neue verdächtige Aktivität ermittelt
  - Neues Integritätsproblem ermittelt
  - Neues Softwareupdate ist verfügbar

5. Klicken Sie auf **Speichern**.

![ATA mail notification settings image](media/ATA-mail-notification-settings-1.7.png)


## <a name="syslog-notification"></a>Syslog-Benachrichtigung

Um Syslog-Benachrichtigungen zu erhalten, legen Sie Folgendes fest:


1. Wählen Sie in der ATA-Konsole auf der Symbolleiste die Einstellungsoption aus, und wählen Sie dann **Konfiguration** aus.
![Symbol der ATA-Konfigurationseinstellungen](media/ATA-config-icon.JPG)

2. Wählen Sie **Einstellungen** im Abschnitt **Benachrichtigungen** aus.
3. Verwenden Sie die Optionen unter **Syslog-Benachrichtigungen**, um auszuwählen, welche Benachrichtigungen gesendet werden sollen:


    - Neue verdächtige Aktivität ermittelt
    - Vorhandene verdächtige Aktivität wurde aktualisiert
    - Neues Integritätsproblem ermittelt
5. Klicken Sie auf **Speichern**.

![Bild mit Einstellungen für ATA-Benachrichtigungen](media/ATA-syslog-notification-settings-1.7.png)




## <a name="see-also"></a>Weitere Informationen
[Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
