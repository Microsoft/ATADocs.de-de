---
title: Festlegen von ATA-Benachrichtigungen | Microsoft Advanced Threat Analytics
description: "Beschreibt, wie ATA-Warnungen festgelegt werden, damit Sie bei verdächtigen Aktivitäten benachrichtigt werden."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: a32799b68d9a8b2949033ab5d1fc5910cff71258


---

# Festlegen von ATA-Benachrichtigungen
ATA kann Sie bei Erkennen einer verdächtigen Aktivität per E-Mail oder über ATA-Ereignisweiterleitung benachrichtigen und das Ereignis an den SIEM-/Syslog-Server weiterleiten. Bevor Sie auswählen, welche Benachrichtigungen Sie erhalten möchten, müssen Sie [Ihren E-Mail-Server und Ihren Syslog-Server einrichten](setting-syslog-email-server-settings.md).

> [!NOTE]
> -   E-Mail-Benachrichtigungen enthalten einen Link, mit denen der Benutzer direkt die erkannte verdächtige Aktivität aufrufen kann. Der Hostnamenteil des Links wird von der Einstellung für die ATA-Konsolen-URL auf der Seite „ATA Center“ übernommen. Standardmäßig ist die URL der ATA-Konsole die IP-Adresse, die während der Installation von ATA Center ausgewählt wurde.  Wenn Sie das Konfigurieren von E-Mail-Benachrichtigungen beabsichtigen, wird die Verwendung eines FQDN als URL der ATA-Konsole empfohlen.
> -   Benachrichtigungen werden von ATA Center entweder an den SMTP-Server oder an den Syslog-Server gesendet.

Um E-Mail-Benachrichtigungen zu erhalten, legen Sie Folgendes fest:


1. Wählen Sie in der ATA-Konsole auf der Symbolleiste die Einstellungsoption aus, und wählen Sie dann **Konfiguration** aus.
![Symbol der ATA-Konfigurationseinstellungen](media/ATA-config-icon.JPG)

2. Wählen Sie **Benachrichtigungen** aus.
3. Verwenden Sie die Optionen unter **E-Mail-Benachrichtigungen**, um auszuwählen, welche Benachrichtigungen gesendet werden sollen:


    - Neue verdächtige Aktivität ermittelt
    - Neues Integritätsproblem ermittelt
    - Neues Softwareupdate ist verfügbar

4. Geben Sie die Empfänger an, die die Benachrichtigungen per E-Mail erhalten sollen.

    [!Hinweis:] E-Mail-Benachrichtigungen über verdächtige Aktivitäten werden nur beim Erstellen der verdächtigen Aktivität gesendet.


5. Klicken Sie auf **Speichern**.

Um Syslog-Benachrichtigungen zu erhalten, legen Sie Folgendes fest:


1. Wählen Sie in der ATA-Konsole auf der Symbolleiste die Einstellungsoption aus, und wählen Sie dann **Konfiguration** aus.
![Symbol der ATA-Konfigurationseinstellungen](media/ATA-config-icon.JPG)

2. Wählen Sie **Benachrichtigungen** aus.
3. Verwenden Sie die Optionen unter **Syslog-Benachrichtigungen**, um auszuwählen, welche Benachrichtigungen gesendet werden sollen:


    - Neue verdächtige Aktivität ermittelt
    - Vorhandene verdächtige Aktivität wurde aktualisiert
    - Neues Integritätsproblem ermittelt
5. Klicken Sie auf **Speichern**.
![Bild mit Einstellungen für ATA-Benachrichtigungen](media/ATA-notification-settings.png)




## Weitere Informationen
[Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jun16_HO4-->


