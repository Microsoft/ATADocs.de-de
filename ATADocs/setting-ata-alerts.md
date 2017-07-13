---
title: Festlegen von Advanced Threat Analytics-Benachrichtigungen | Microsoft-Dokumentation
description: "Beschreibt, wie ATA-Warnungen festgelegt werden, damit Sie bei verdächtigen Aktivitäten benachrichtigt werden."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/12/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: cc7f5d2e75076b1f684ad76daca9ceb35e0d30e3
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/30/2017
---
*Gilt für: Advanced Threat Analytics Version 1.8*



# Festlegen von ATA-Benachrichtigungen
<a id="set-ata-notifications" class="xliff"></a>
ATA kann Sie bei Erkennen einer verdächtigen Aktivität per E-Mail oder über ATA-Ereignisweiterleitung benachrichtigen und das Ereignis an den SIEM-/Syslog-Server weiterleiten. Bevor Sie auswählen, welche Benachrichtigungen Sie erhalten möchten, müssen Sie [Ihren E-Mail-Server und Ihren Syslog-Server einrichten](setting-syslog-email-server-settings.md).

> [!NOTE]
> -   E-Mail-Benachrichtigungen enthalten einen Link, mit denen der Benutzer direkt die erkannte verdächtige Aktivität aufrufen kann. Der Hostnamenteil des Links wird von der Einstellung für die ATA-Konsolen-URL auf der Seite „ATA Center“ übernommen. Standardmäßig ist die URL der ATA-Konsole die IP-Adresse, die während der Installation von ATA Center ausgewählt wurde.  Wenn Sie das Konfigurieren von E-Mail-Benachrichtigungen beabsichtigen, wird die Verwendung eines FQDN als URL der ATA-Konsole empfohlen.
> -   Benachrichtigungen werden von ATA Center entweder an den SMTP-Server oder an den Syslog-Server gesendet.


Um Benachrichtigungen zu erhalten, legen Sie Folgendes fest:


1. Wählen Sie in der ATA-Konsole auf der Symbolleiste die Einstellungsoption aus, und wählen Sie dann **Konfiguration** aus.

![Symbol der ATA-Konfigurationseinstellungen](media/ATA-config-icon.png)

2. Wählen Sie im Abschnitt **Benachrichtigungen und Berichte** die Option **Benachrichtigung** aus.
3. Geben Sie unter **E-Mail-Benachrichtigungen** an, welche Benachrichtigungen via E-Mail gesendet werden sollen – neue verdächtige Aktivitäten oder neue Integritätsprobleme. Sie können eine separate E-Mail-Adresse festlegen, an die die verdächtigen Aktivitäten und die Integritätswarnungen gesendet werden, damit z.B. verdächtige Aktivitätsbenachrichtigungen an Ihren Sicherheitsanalysten und Ihre Integritätswarnungsbenachrichtigungen an Ihren IT-Administrator gesendet werden können.
>   [!NOTE]
>   E-Mail-Benachrichtigungen über verdächtige Aktivitäten werden nur beim Erstellen der verdächtigen Aktivität gesendet.
3. Geben Sie unter **Syslog-Benachrichtigungen** an, welche Benachrichtigungen an Ihren Syslog-Server gesendet werden sollen: neue verdächtige Aktivitäten, aktualisierte verdächtige Aktivitäten und neue Integritätsprobleme.
5. Klicken Sie auf **Speichern**.

![ATA mail notification settings image](media/ata-mail-notification-settings.png)




## Weitere Informationen
<a id="see-also" class="xliff"></a>
[Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
