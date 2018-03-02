---
title: 'Installieren von Azure Advanced Threat Protection: Schritt 7 | Microsoft-Dokumentation'
description: Im letzten Schritt der Installation von Azure ATP konfigurieren Sie den Honeytoken-Benutzer.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 1ad5e923-9bbd-4f56-839a-b11a9f387d4b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: bef13d0f4799a4483eda6604a8ed96befaa13508
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/21/2018
---
*Gilt für: Azure Advanced Threat Protection*



# <a name="install-azure-atp---step-7"></a>Installieren von Azure ATP: Schritt 7

>[!div class="step-by-step"]
[« Schritt 6](install-atp-step6-vpn.md)
[Schritt 8 »](install-atp-step8-samr.md)

## <a name="step-7-configure-detection-exclusions-and-honeytoken-user"></a>Schritt 7: Konfigurieren von Ausschlüssen von Erkennungen und Honeytoken-Benutzern

Azure ATP ermöglicht den Ausschluss bestimmter IP-Adressen oder Benutzer aus einer Reihe von Erkennungen. 

Angenommen, ein **DNS-Reconnaissance-Ausschluss** könnte eine Sicherheitsprüfung sein, die DNS als Überprüfungsmechanismus verwendet. Der Ausschluss hilft Azure ATP, Überprüfungen dieser Art zu ignorieren.  

Azure ATP ermöglicht auch die Konfiguration eines Honeytoken-Benutzers, der als ein Trap für böswillige Teilnehmer verwendet wird. Jede Authentifizierung, die Ihrem (normalerweise ruhenden) Konto zugeordnet ist, löst eine Warnung aus.

Führen Sie zur Konfiguration die folgenden Schritte aus:

1.  Klicken Sie im Azure ATP-Arbeitsbereichsportal zuerst auf das Symbol „Einstellungen“ und dann auf **Konfiguration**.

    ![Azure ATP-Konfigurationseinstellungen](media/atp-config-menu.png)

2.  Klicken Sie unter **Erkennung** auf **Entitätstag**.

3. Geben Sie unter **Honeytokenkonten** den Kontonamen des Honeytokens ein, und klicken Sie auf das **+**-Zeichen. Das Honeytoken-Kontenfeld kann gesucht werden und zeigt automatisch Entitäten in Ihrem Netzwerk an. Klicken Sie auf **Speichern**.

   ![Honeytoken](media/honeytoken-sensitive.png)

4. Klicken Sie auf **Ausschlüsse**. Geben Sie für jeden Bedrohungstyp ein Benutzerkonto oder eine IP-Adresse ein, das/die von der Erkennung dieser Bedrohungen ausgeschlossen werden soll, und klicken Sie auf das *Pluszeichen*. Das Feld **Entität hinzufügen** (Benutzer oder Computer) kann durchsucht werden und wird automatisch mit Entitäten in Ihrem Netzwerk gefüllt. Weitere Informationen finden Sie unter [Excluding entities from detections (Ausschließen von Entitäten von Erkennungen)](excluding-entities-from-detections.md) und im [Handbuch zu verdächtigen Aktivitäten](suspicious-activity-guide.md).

   ![Ausschlüsse](media/exclusions.png)

5.  Klicken Sie auf **Speichern**.


Damit haben Sie Azure Advanced Threat Protection erfolgreich bereitgestellt.

Sie können nun die Angriffszeitleiste auf erkannte verdächtige Aktivitäten prüfen sowie nach Benutzern oder Computern suchen und deren Profile anzeigen.

Azure ATP startet sofort die automatische Überprüfung auf verdächtige Aktivitäten. Einige Erkennungen wie Abnormal Group Modification (ungewöhnliche Gruppenänderungen) erfordern eine Lernphase und sind nicht unmittelbar nach der Bereitstellung von Azure ATP verfügbar.



>[!div class="step-by-step"]
[« Schritt 6](install-atp-step6-vpn.md)
[Schritt 8 »](install-atp-step8-samr.md)

## <a name="see-also"></a>Weitere Informationen
- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](http://aka.ms/aatpsizingtool)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)
