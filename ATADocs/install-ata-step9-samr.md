---
title: Konfigurieren von SAM-R zum Aktivieren eines Erkennungsvorgangs für Lateral Movement-Pfade in Advanced Threat Analytics | Microsoft-Dokumentation
description: Informationen zum Konfigurieren von SAM-R zum Erkennen eines Lateral Movement-Pfads in Advanced Threat Analytics (ATA)
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 7597ed25-87f5-472c-a496-d5f205c9c391
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a49478698adea15637698f4c715cdd34a9a601c4
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/22/2018
---
*Gilt für: Advanced Threat Analytics Version 1.9*

# <a name="install-ata---step-9"></a>Installieren von ATA: Schritt 9

>[!div class="step-by-step"]
[« Schritt 8 ](install-ata-step7.md)

## <a name="step-9-configure-sam-r-required-permissions"></a>Schritt 9: Konfigurieren von für SAM-R erforderliche Berechtigungen

Der Erkennungsvorgang für [Lateral Movement-Pfade](use-case-lateral-movement-path.md) ist abhängig von Abfragen, die lokale Administratoren auf bestimmten Computern ermitteln. Diese Abfragen werden mithilfe des SAMR-R-Protokolls über das in [Schritt 2: Verbinden mit AD](install-ata-step2.md) erstellte ATA-Dienstkonto durchgeführt. .
 
Sie müssen eine Änderung an der Gruppenrichtlinie vornehmen, um sicherzustellen, dass Windows-Clients und -Server zulassen, dass das ATA-Dienstkonto diesen SAM-R-Vorgang durchführt.

1. Finden der Richtlinie:

 - Richtlinienname: Netzwerkzugriff – Schränken Sie die Zahl der Clients ein, die Remoteaufrufe an SAM durchführen dürfen.
 - Speicherort: Computerkonfiguration, Windows-Einstellungen, Sicherheitseinstellungen, lokale Richtlinien, Sicherheitsoptionen
  
  ![Finden der Richtlinie](./media/samr-policy-location.png)

2. Fügen Sie den ATA-Dienst der Liste zulässiger Konten hinzu, die diese Aktion auf Ihren modernen Windows-Systemen durchführen können.
 
  ![Hinzufügen des Diensts](./media/samr-add-service.png)

3. Der **ATA-Dienst**, der bei der Installation erstellt wurde, weist nun die nötigen Berechtigungen auf, um SAM-R in der Umgebung auszuführen.

Weitere Informationen zu SAM-R und dieser Gruppenrichtlinie finden Sie unter [Network access: Restrict clients allowed to make remote calls to SAM (Netzwerkzugriff: Einschränken der Clients, die Remoteaufrufe an SAM durchführen dürfen)](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).


>[!div class="step-by-step"]
[« Schritt 8 ](install-ata-step7.md)

## <a name="see-also"></a>Weitere Informationen
- [Handbuch für die ATA POC-Bereitstellung](http://aka.ms/atapoc)
- [Tool zur Bemessung von ATA-Gateways](http://aka.ms/atasizingtool)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Voraussetzungen für ATA](ata-prerequisites.md)
