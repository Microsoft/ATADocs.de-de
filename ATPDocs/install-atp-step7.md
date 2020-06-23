---
title: 'Azure Advanced Threat Protection: Konfigurieren des Ausschlusses von Erkennungen und von Honeytokenkonten'
description: Konfigurieren des Ausschlusses von Erkennungen und von Honeytoken-Benutzern
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/22/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 1ad5e923-9bbd-4f56-839a-b11a9f387d4b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 9ded53464c9247ce08533c6ba4c3758ff6f9f6b6
ms.sourcegitcommit: fbb0768c392f9bccdd7e4adf0e9a0303c8d1922c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2020
ms.locfileid: "84772223"
---
# <a name="configure-detection-exclusions-and-honeytoken-accounts"></a>Konfigurieren von Ausschlüssen von Erkennungen und Honeytokenkonten

Azure ATP ermöglicht den Ausschluss bestimmter IP-Adressen oder Benutzer aus einer Reihe von Erkennungen. 

Angenommen, ein **DNS-Reconnaissance-Ausschluss** könnte eine Sicherheitsprüfung sein, die DNS als Überprüfungsmechanismus verwendet. Der Ausschluss hilft Azure ATP, Überprüfungen dieser Art zu ignorieren.  

Azure ATP ermöglicht auch die Konfiguration von Honeytokenkonten, die als Traps für böswillige Akteure verwendet werden. Jede Authentifizierung, die diesen (normalerweise ruhenden) Honeytokenkonten zugeordnet ist, löst eine Warnung aus.

Dazu führen Sie folgende Schritte aus:

1.  Klicken Sie im Azure ATP-Portal zuerst auf das Symbol „Einstellungen“ und dann auf **Konfiguration**.

    ![Azure ATP-Konfigurationseinstellungen](media/atp-config-menu.png)

2.  Klicken Sie unter **Erkennung** auf **Entitätstag**.

3. Geben Sie unter **Honeytokenkonten** den Kontonamen des Honeytokens ein, und klicken Sie auf das **+** -Zeichen. Das Honeytoken-Kontenfeld kann gesucht werden und zeigt automatisch Entitäten in Ihrem Netzwerk an. Klicken Sie auf **Speichern**.

   ![Honeytoken](media/honeytoken-sensitive.png)

4. Klicken Sie auf **Ausschlüsse**. Geben Sie für jeden Bedrohungstyp ein Benutzerkonto oder eine IP-Adresse ein, das/die von der Erkennung ausgeschlossen werden soll. 
5. Klicken Sie auf das *Plus*-Zeichen. Das Feld **Entität hinzufügen** (Benutzer oder Computer) kann durchsucht werden und wird automatisch mit Entitäten in Ihrem Netzwerk gefüllt. Weitere Informationen finden Sie unter [Ausschließen von Entitäten von Erkennungen](excluding-entities-from-detections.md) und im [Handbuch zu Sicherheitswarnungen](suspicious-activity-guide.md).

   ![Ausschlüsse](media/exclusions.png)

6.  Klicken Sie auf **Speichern**.


Damit haben Sie Azure Advanced Threat Protection erfolgreich bereitgestellt.

Sie können nun die Angriffszeitleiste auf Sicherheitswarnungen prüfen, die aus erkannten Aktivitäten generiert wurden, sowie nach Benutzern oder Computern suchen und deren Profile anzeigen.

Azure ATP-Überprüfung wird sofort gestartet. Einige Erkennungen – z. B. [Verdächtige Hinzufügungen zu vertraulichen Gruppen](atp-domain-dominance-alerts.md#suspicious-additions-to-sensitive-groups-external-id-2024) erfordern einen Lernzeitraum und sind nicht sofort nach der Bereitstellung von Azure ATP verfügbar. Der Lernzeitraum für jede Warnung wird im detaillierten [Leitfaden für Sicherheitswarnungen](suspicious-activity-guide.md) aufgeführt. 


## <a name="see-also"></a>Weitere Informationen:
- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](https://aka.ms/aatpsizingtool)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Voraussetzungen für Azure ATP](atp-prerequisites.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
