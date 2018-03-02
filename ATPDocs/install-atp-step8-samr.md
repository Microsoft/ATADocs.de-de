---
title: "Konfigurieren von SAM-R zum Aktivieren eines Erkennungsvorgangs für Lateral Movement-Pfade in Azure ATP | Microsoft-Dokumentation"
description: Informationen zum Konfigurieren von SAM-R zum Aktivieren eines Lateral Movement-Pfads in Azure ATP
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: b09adce3-0fbc-40e3-a53f-31f57fe79ca3
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 0e2ac4fb68fb1429610a0416582c871c9ae704df
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/21/2018
---
*Gilt für: Azure Advanced Threat Protection*

# <a name="install-azure-atp---step-8"></a>Installieren von Azure ATP: Schritt 8

>[!div class="step-by-step"]
[« Schritt 7 ](install-atp-step7.md)

## <a name="step-8-configure-sam-r-required-permissions"></a>Schritt 8: Konfigurieren von für SAM-R erforderliche Berechtigungen

Der Erkennungsvorgang für [Lateral Movement-Pfade](use-case-lateral-movement-path.md) ist abhängig von Abfragen, die lokale Administratoren auf bestimmten Computern ermitteln. Diese Abfragen werden mithilfe des SAMR-R-Protokolls über das in [Schritt 2: Verbinden mit AD](install-atp-step2.md) erstellte Azure ATP-Dienstkonto durchgeführt .
 
Sie müssen eine Änderung an der Gruppenrichtlinie vornehmen, um sicherzustellen, dass Windows-Clients und -Server zulassen, dass das Azure ATP-Dienstkonto diesen SAM-R-Vorgang durchführt.

1. Finden der Richtlinie:

 - Richtlinienname: Netzwerkzugriff – Schränken Sie die Zahl der Clients ein, die Remoteaufrufe an SAM durchführen dürfen.
 - Speicherort: Computerkonfiguration, Windows-Einstellungen, Sicherheitseinstellungen, lokale Richtlinien, Sicherheitsoptionen
  
  ![Finden der Richtlinie](./media/samr-policy-location.png)

2. Fügen Sie den Azure ATP-Dienst der Liste von zulässigen Konten hinzu, die diese Aktion auf Ihren modernen Windows-Systemen durchführen können.
 
  ![Hinzufügen des Diensts](./media/samr-add-service.png)

3. Der **Azure ATP-Dienst**, der bei der Installation erstellt wurde, weist nun die nötigen Berechtigungen auf, um SAMR in der Umgebung auszuführen.

Weitere Informationen zu SAM-R und dieser Gruppenrichtlinie finden Sie unter [Network access: Restrict clients allowed to make remote calls to SAM (Netzwerkzugriff: Einschränken der Clients, die Remoteaufrufe an SAM durchführen dürfen)](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).


>[!div class="step-by-step"]
[« Schritt 7 ](install-atp-step7.md)



## <a name="see-also"></a>Weitere Informationen
- [Investigating lateral movement path attacks with Azure ATP (Untersuchen von Lateral Movement-Pfaden mit Azure ATP)](use-case-lateral-movement-path.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)