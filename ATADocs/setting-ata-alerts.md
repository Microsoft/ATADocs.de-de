---
title: Einrichten von Advanced Threat Analytics-Benachrichtigungen
description: Beschreibt, wie ATA-Warnungen festgelegt werden, damit Sie bei verdächtigen Aktivitäten benachrichtigt werden.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: e61436868e1d7bd441ab11e8f5d6b01869df4ed6
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88956022"
---
# <a name="set-ata-notifications"></a>Festlegen von ATA-Benachrichtigungen

*Gilt für: Advanced Threat Analytics Version 1.9*

ATA kann Sie bei Erkennen einer verdächtigen Aktivität per E-Mail oder über ATA-Ereignisweiterleitung benachrichtigen und das Ereignis an den SIEM-/Syslog-Server weiterleiten. Bevor Sie auswählen, welche Benachrichtigungen Sie erhalten möchten, müssen Sie [Ihren E-Mail-Server und Ihren Syslog-Server einrichten](setting-syslog-email-server-settings.md).

> [!NOTE]
> - E-Mail-Benachrichtigungen enthalten einen Link, mit denen der Benutzer direkt die erkannte verdächtige Aktivität aufrufen kann. Der Hostnamenteil des Links wird von der Einstellung für die ATA-Konsolen-URL auf der Seite „ATA Center“ übernommen. Standardmäßig ist die URL der ATA-Konsole die IP-Adresse, die während der Installation von ATA Center ausgewählt wurde. Wenn Sie E-Mail-Benachrichtigungen konfigurieren möchten, wird die Verwendung eines FQDN als URL der ATA-Konsole empfohlen.
> - Benachrichtigungen werden von ATA Center entweder an den SMTP-Server oder an den Syslog-Server gesendet.


Um Benachrichtigungen zu erhalten, legen Sie folgende Parameter fest:


1. Wählen Sie in der ATA-Konsole auf der Symbolleiste die Einstellungsoption aus, und wählen Sie dann **Konfiguration** aus.
    
    ![Symbol der ATA-Konfigurationseinstellungen](media/ATA-config-icon.png)
    
1. Wählen Sie im Abschnitt **Benachrichtigungen und Berichte** die Option **Benachrichtigung** aus.
1. Geben Sie unter **E-Mail-Benachrichtigungen** an, welche Benachrichtigungen via E-Mail gesendet werden sollen – neue verdächtige Aktivitäten oder neue Integritätsprobleme. Sie können eine separate E-Mail-Adresse festlegen, an die die verdächtigen Aktivitäten und die Integritätswarnungen gesendet werden, damit z.B. verdächtige Aktivitätsbenachrichtigungen an Ihren Sicherheitsanalysten und Ihre Integritätswarnungsbenachrichtigungen an Ihren IT-Administrator gesendet werden können.
    
    > [!NOTE]
    > E-Mail-Benachrichtigungen über verdächtige Aktivitäten werden nur beim Erstellen der verdächtigen Aktivität gesendet.

1. Geben Sie unter **syslog-Benachrichtigungen**an, welche Benachrichtigungen an Ihren Syslog-Server gesendet werden sollen: neue verdächtige Aktivitäten, aktualisierte verdächtige Aktivitäten und neue Integritäts Probleme.
1. Klicken Sie auf **Speichern**.
    
    ![ATA mail notification settings image](media/ata-mail-notification-settings.png)




## <a name="see-also"></a>Weitere Informationen
[Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
