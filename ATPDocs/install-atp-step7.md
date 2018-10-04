---
title: 'Installieren von Azure Advanced Threat Protection: Schritt 7 | Microsoft-Dokumentation'
description: Im letzten Schritt der Installation von Azure ATP konfigurieren Sie den Honeytoken-Benutzer.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/2/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 1ad5e923-9bbd-4f56-839a-b11a9f387d4b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 9252e47978a4adc0e2059a3111b362ff2b042daf
ms.sourcegitcommit: b283bf66e63d76e6dba4564a229e804792794c6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/29/2018
ms.locfileid: "47453798"
---
*Gilt für: Azure Advanced Threat Protection*



# <a name="install-azure-atp---step-7"></a>Installieren von Azure ATP: Schritt 7

> [!div class="step-by-step"]
> [« Schritt 6](install-atp-step6-vpn.md)
> [Schritt 8 »](install-atp-step8-samr.md)

## <a name="step-7-configure-detection-exclusions-and-honeytoken-accounts"></a>Schritt 7: Konfigurieren von Ausschlüssen von Erkennungen und Honeytokenkonten

Azure ATP ermöglicht den Ausschluss bestimmter IP-Adressen oder Benutzer aus einer Reihe von Erkennungen. 

Angenommen, ein **DNS-Reconnaissance-Ausschluss** könnte eine Sicherheitsprüfung sein, die DNS als Überprüfungsmechanismus verwendet. Der Ausschluss hilft Azure ATP, Überprüfungen dieser Art zu ignorieren.  

Azure ATP ermöglicht auch die Konfiguration von Honeytokenkonten, die als Traps für böswillige Akteure verwendet werden. Jede Authentifizierung, die diesen (normalerweise ruhenden) Honeytokenkonten zugeordnet ist, löst eine Warnung aus.

Dazu führen Sie folgende Schritte aus:

1.  Klicken Sie im Azure ATP-Arbeitsbereichsportal zuerst auf das Symbol „Einstellungen“ und dann auf **Konfiguration**.

    ![Azure ATP-Konfigurationseinstellungen](media/atp-config-menu.png)

2.  Klicken Sie unter **Erkennung** auf **Entitätstag**.

3. Geben Sie unter **Honeytokenkonten** den Kontonamen des Honeytokens ein, und klicken Sie auf das **+**-Zeichen. Das Honeytoken-Kontenfeld kann gesucht werden und zeigt automatisch Entitäten in Ihrem Netzwerk an. Klicken Sie auf **Speichern**.

   ![Honeytoken](media/honeytoken-sensitive.png)

4. Klicken Sie auf **Ausschlüsse**. Geben Sie für jeden Bedrohungstyp ein Benutzerkonto oder eine IP-Adresse ein, das/die von der Erkennung ausgeschlossen werden soll. 
5. Klicken Sie auf das *Plus*-Zeichen. Das Feld **Entität hinzufügen** (Benutzer oder Computer) kann durchsucht werden und wird automatisch mit Entitäten in Ihrem Netzwerk gefüllt. Weitere Informationen finden Sie unter [Excluding entities from detections (Ausschließen von Entitäten von Erkennungen)](excluding-entities-from-detections.md) und im [Handbuch zu verdächtigen Aktivitäten](suspicious-activity-guide.md).

   ![Ausschlüsse](media/exclusions.png)

6.  Klicken Sie auf **Speichern**.


Damit haben Sie Azure Advanced Threat Protection erfolgreich bereitgestellt.

Sie können nun die Angriffszeitleiste auf erkannte verdächtige Aktivitäten prüfen sowie nach Benutzern oder Computern suchen und deren Profile anzeigen.

Azure ATP startet sofort die automatische Überprüfung auf verdächtige Aktivitäten. Einige Erkennungen wie Abnormal Group Modification (ungewöhnliche Gruppenänderungen) erfordern eine Lernphase und sind nicht unmittelbar nach der Azure ATP-Bereitstellung verfügbar.



> [!div class="step-by-step"]
> [« Schritt 6](install-atp-step6-vpn.md)
> [Schritt 8 »](install-atp-step8-samr.md)

## <a name="see-also"></a>Weitere Informationen
- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](http://aka.ms/aatpsizingtool)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)
