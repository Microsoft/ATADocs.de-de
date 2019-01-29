---
title: Konfigurieren von SAM-R zum Aktivieren eines Erkennungsvorgangs für Lateral Movement-Pfade in Azure ATP | Microsoft-Dokumentation
description: Erläutert das Konfigurieren von Azure ATP für das Ausführen von Remoteaufrufen an SAM
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/02/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: b09adce3-0fbc-40e3-a53f-31f57fe79ca3
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4b0cdf2bd9294a2acb70bb8c3ce5e2e55e480f23
ms.sourcegitcommit: f37127601166216e57e56611f85dd783c291114c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/24/2019
ms.locfileid: "54839671"
---
# <a name="configure-azure-atp-to-make-remote-calls-to-sam"></a>Konfigurieren von Azure ATP für das Ausführen von Remoteaufrufen an SAM
Der Erkennungsvorgang für [Lateral Movement-Pfade](use-case-lateral-movement-path.md) von Azure ATP ist abhängig von Abfragen, die lokale Administratoren auf bestimmten Computern ermitteln. Diese Abfragen werden mithilfe des SAM-R-Protokolls über das während der Azure ATP-Installation in [Schritt 2 erstellte Azure ATP-Dienstkonto ausgeführt. Verbinden mit AD](install-atp-step2.md).

## <a name="configure-sam-r-required-permissions"></a>Konfigurieren von für SAM-R erforderliche Berechtigungen
Wenn Sie sicherstellen möchten, dass Windows-Clients und -Server zulassen, dass Ihr Azure ATP-Konto SAM-R durchführt, muss die **Gruppenrichtlinie** geändert werden, damit das Azure ATP-Dienstkonto zu den konfigurierten Konten hinzugefügt wird, die in der Richtlinie für den **Netzwerkzugriff** aufgeführt sind.

1. Finden der Richtlinie:

   - Richtlinienname: Netzwerkzugriff: Clients einschränken, die Remoteaufrufe an SAM ausführen dürfen
   - Speicherort: Computerkonfiguration, Windows-Einstellungen, Sicherheitseinstellungen, lokale Richtlinien, Sicherheitsoptionen
  
   ![Finden der Richtlinie](./media/samr-policy-location.png)

2. Fügen Sie den Azure ATP-Dienst der Liste von zulässigen Konten hinzu, die diese Aktion auf Ihren modernen Windows-Systemen durchführen können.
 
   ![Hinzufügen des Diensts](./media/samr-add-service.png)

3. Der **Azure ATP-Dienst**, der bei der Installation erstellt wurde, weist nun die nötigen Berechtigungen auf, um SAM-R in der Umgebung auszuführen.

> [!NOTE]
> Stellen Sie vor der Erzwingung neuer Richtlinien sicher, dass Ihre Umgebung weiterhin geschützt ist, ohne dass Ihre Anwendungskompatibilität beeinträchtigt wird, indem Sie den Überwachungsmodus aktivieren und die vorgeschlagenen Änderungen im Überwachungsmodus überprüfen.

Weitere Informationen zu SAM-R und dieser Gruppenrichtlinie, finden Sie unter [Netzwerkzugriff: Clients einschränken, die Remoteaufrufe an SAM ausführen dürfen](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).



## <a name="see-also"></a>Weitere Informationen
- [Investigating lateral movement path attacks with Azure ATP (Untersuchen von Lateral Movement-Pfaden mit Azure ATP)](use-case-lateral-movement-path.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)