---
title: Einrichten von Azure Advanced Threat Protection-Benachrichtigungen | Microsoft-Dokumentation
description: Beschreibt, wie Azure ATP-Sicherheitswarnungen festgelegt werden, damit Sie bei verdächtigen Aktivitäten benachrichtigt werden.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 10/04/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 4308f03e-b2a7-4e38-a750-540ff94faa81
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 39b1c0835402ff4ff688a28451fd7505f2cd364c
ms.sourcegitcommit: 9673eb49729a06d3a25d52c0f43c76ac61b9cf89
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/12/2020
ms.locfileid: "75906138"
---
# <a name="set-azure-atp-notifications"></a>Festlegen von Azure ATP-Benachrichtigungen

Azure ATP kann Sie darüber benachrichtigen, wenn eine verdächtige Aktivität oder eine Integritätswarnung ermittelt wird, und gibt eine Sicherheitswarnung oder Integritätswarnung per E-Mail aus. 

Legen Sie folgende Parameter fest, damit Benachrichtigungen an eine bestimmte E-Mail-Adresse gesendet werden:


1. Klicken Sie im Azure ATP-Portal in der Symbolleiste erst auf die Einstellungsoption und dann auf **Konfiguration**.

   ![Symbol der Azure ATP-Konfigurationseinstellungen](media/atp-config-menu.png)

2. Klicken Sie auf **Benachrichtigungen**.
3. Geben Sie unter **E-Mail-Benachrichtigungen** an, wann Benachrichtigungen via E-Mail gesendet werden sollen: entweder für neue Warnungen (verdächtige Aktivitäten) oder neue Integritätsprobleme. 
 
   > [!NOTE]
   > E-Mail-Benachrichtigungen über verdächtige Aktivitäten werden nur beim Erstellen der verdächtigen Aktivität gesendet.
 
4. Klicken Sie auf **Speichern**.

   ![Azure ATP-Benachrichtigungen](media/atp-notifications.png)



## <a name="see-also"></a>Weitere Informationen

- [Konfigurieren der Ereignissammlung](configure-event-collection.md)

- [Set Syslog settings (Einrichten der Syslog-Einstellungen)](setting-syslog.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
