---
title: Einrichten von Azure Advanced Threat Protection-Benachrichtigungen | Microsoft-Dokumentation
description: Beschreibt, wie Azure ATP-Warnungen festgelegt werden, damit Sie bei verdächtigen Aktivitäten benachrichtigt werden.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 4308f03e-b2a7-4e38-a750-540ff94faa81
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: c3fc5adbb700c4b8df66c243a655cf98aacc79af
ms.sourcegitcommit: 9f02f0f6669b25f39b616bb0885bb55b8c4f050b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/19/2018
ms.locfileid: "46362424"
---
*Gilt für: Azure Advanced Threat Protection*


# <a name="set-azure-atp-notifications"></a>Festlegen von Azure ATP-Benachrichtigungen

Azure ATP kann Sie per E-Mail darüber benachrichtigen, wenn eine verdächtige Aktivität oder eine Integritätswarnung ermittelt wird. 

Legen Sie folgende Parameter fest, damit Benachrichtigungen an eine bestimmte E-Mail-Adresse gesendet werden:


1. Klicken Sie im Azure ATP-Arbeitsbereichsportal in der Symbolleiste erst auf die Einstellungsoption und dann auf **Konfiguration**.

![Symbol der Azure ATP-Konfigurationseinstellungen](media/atp-config-menu.png)

2. Klicken Sie auf **Benachrichtigungen**.
3. Geben Sie unter **E-Mail-Benachrichtigungen** an, wann Benachrichtigungen via E-Mail gesendet werden sollen: entweder für neue Warnungen (verdächtige Aktivitäten) oder neue Integritätsprobleme. 
 
 >  [!NOTE]
 >   E-Mail-Benachrichtigungen über verdächtige Aktivitäten werden nur beim Erstellen der verdächtigen Aktivität gesendet.
 
4. Klicken Sie auf **Speichern**.

 ![Azure ATP-Benachrichtigungen](media/atp-notifications.png)



## <a name="see-also"></a>Weitere Informationen

- [Konfigurieren der Ereignissammlung](configure-event-collection.md)

- [Set Syslog settings (Einrichten der Syslog-Einstellungen)](setting-syslog.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)
