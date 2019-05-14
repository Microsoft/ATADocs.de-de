---
title: 'Azure Advanced Threat Protection: Konfigurieren des Ausschlusses von Erkennungen und von Honeytokenkonten | Microsoft-Dokumentation'
description: Konfigurieren des Ausschlusses von Erkennungen und von Honeytoken-Benutzern
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 12/02/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 1ad5e923-9bbd-4f56-839a-b11a9f387d4b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 0fdf6b312c51949a1a104336518cc55f924020aa
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2019
ms.locfileid: "65197150"
---
# <a name="configure-detection-exclusions-and-honeytoken-accounts"></a>Konfigurieren von Ausschlüssen von Erkennungen und Honeytokenkonten

Azure ATP ermöglicht den Ausschluss bestimmter IP-Adressen oder Benutzer aus einer Reihe von Erkennungen. 

Angenommen, ein **DNS-Reconnaissance-Ausschluss** könnte eine Sicherheitsprüfung sein, die DNS als Überprüfungsmechanismus verwendet. Der Ausschluss hilft Azure ATP, Überprüfungen dieser Art zu ignorieren.  

Azure ATP ermöglicht auch die Konfiguration von Honeytokenkonten, die als Traps für böswillige Akteure verwendet werden. Jede Authentifizierung, die diesen (normalerweise ruhenden) Honeytokenkonten zugeordnet ist, löst eine Warnung aus.

Dazu führen Sie folgende Schritte aus:

1.  Klicken Sie im Azure ATP-Portal zuerst auf das Symbol „Einstellungen“ und dann auf **Konfiguration**.

    ![Azure ATP-Konfigurationseinstellungen](media/atp-config-menu.png)

2.  Klicken Sie unter **Erkennung** auf **Entitätstag**.

3. Geben Sie unter **Honeytokenkonten** den Kontonamen des Honeytokens ein, und klicken Sie auf das **+**-Zeichen. Das Honeytoken-Kontenfeld kann gesucht werden und zeigt automatisch Entitäten in Ihrem Netzwerk an. Klicken Sie auf **Speichern**.

   ![Honeytoken](media/honeytoken-sensitive.png)

4. Klicken Sie auf **Ausschlüsse**. Geben Sie für jeden Bedrohungstyp ein Benutzerkonto oder eine IP-Adresse ein, das/die von der Erkennung ausgeschlossen werden soll. 
5. Klicken Sie auf das *Plus*-Zeichen. Das Feld **Entität hinzufügen** (Benutzer oder Computer) kann durchsucht werden und wird automatisch mit Entitäten in Ihrem Netzwerk gefüllt. Weitere Informationen finden Sie unter [Ausschließen von Entitäten von Erkennungen](excluding-entities-from-detections.md) und im [Handbuch zu Sicherheitswarnungen](suspicious-activity-guide.md).

   ![Ausschlüsse](media/exclusions.png)

6.  Klicken Sie auf **Speichern**.


Damit haben Sie Azure Advanced Threat Protection erfolgreich bereitgestellt.

Sie können nun die Angriffszeitleiste auf erkannte Sicherheitswarnungen prüfen sowie nach Benutzern oder Computern suchen und deren Profile anzeigen.

Azure ATP-Überprüfung wird sofort gestartet. Einige Erkennungen wie Abnormal Group Modification (ungewöhnliche Gruppenänderungen) erfordern eine Lernphase und sind nicht unmittelbar nach der Azure ATP-Bereitstellung verfügbar.


## <a name="see-also"></a>Weitere Informationen
- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](http://aka.ms/aatpsizingtool)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
