---
title: Konfigurieren von SAM-R zum Aktivieren eines Erkennungsvorgangs für Lateral Movement-Pfade in Advanced Threat Analytics | Microsoft-Dokumentation
description: Informationen zum Konfigurieren von SAM-R zum Erkennen eines Lateral Movement-Pfads in Advanced Threat Analytics (ATA)
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 08/08/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 7597ed25-87f5-472c-a496-d5f205c9c391
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: bd47ebbe059014015b180ad568e4c519ba1b95b7
ms.sourcegitcommit: db35bae8354fa35644e9334bfc37b9ffbafdaacc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68862578"
---
# <a name="install-ata---step-9"></a>Installieren von ATA: Schritt 9

*Gilt für: Advanced Threat Analytics Version 1.9*

> [!div class="step-by-step"]
> [« Schritt 8 ](install-ata-step7.md)

> [!NOTE]
> Bevor Sie eine neue Richtlinie erzwingen, stellen Sie immer sicher, dass Ihre Umgebung sicher bleibt, ohne die Anwendungs Kompatibilität zu beeinträchtigen, indem Sie zunächst die vorgeschlagenen Änderungen im Überwachungsmodus aktivieren und überprüfen. 

## <a name="step-9-configure-sam-r-required-permissions"></a>Schritt 9: Konfigurieren von für SAM-R erforderliche Berechtigungen

Der Erkennungsvorgang für [Lateral Movement-Pfade](use-case-lateral-movement-path.md) ist abhängig von Abfragen, die lokale Administratoren auf bestimmten Computern ermitteln. Diese Abfragen werden mithilfe des SAMR-R-Protokolls über das in [Schritt 2: Verbinden mit AD erstellte ATA-Dienstkonto durchgeführt. Verbinden mit AD](install-ata-step2.md).
 
Wenn Sie sicherstellen möchten, dass Windows-Clients und -Server zulassen, dass der ATA-Dienst diesen SAM-R-Vorgang durchführt, muss die **Gruppenrichtlinie** geändert werden, damit das ATA-Dienstkonto zu den konfigurierten Konten hinzugefügt wird, die in der Richtlinie für den **Netzwerkzugriff** aufgeführt sind.

1. Finden der Richtlinie:

   - Richtlinienname: Netzwerkzugriff: Clients einschränken, die Remoteaufrufe an SAM ausführen dürfen
   - Speicherort: Computerkonfiguration, Windows-Einstellungen, Sicherheitseinstellungen, lokale Richtlinien, Sicherheitsoptionen
  
   ![Finden der Richtlinie](./media/samr-policy-location.png)

2. Fügen Sie den ATA-Dienst der Liste zulässiger Konten hinzu, die diese Aktion auf Ihren modernen Windows-Systemen durchführen können.
 
   ![Hinzufügen des Diensts](./media/samr-add-service.png)

3. Der **ATA-Dienst**, der bei der Installation erstellt wurde, weist nun die nötigen Berechtigungen auf, um SAM-R in der Umgebung auszuführen.

 Weitere Informationen zu SAM-R und dieser Gruppenrichtlinie finden Sie unter [Netzwerkzugriff: Clients einschränken, die Remoteaufrufe an SAM ausführen dürfen](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).


> [!div class="step-by-step"]
> [« Schritt 8 ](install-ata-step7.md)

## <a name="see-also"></a>Siehe auch
- [Handbuch für die ATA POC-Bereitstellung](http://aka.ms/atapoc)
- [Tool zur Bemessung von ATA-Gateways](http://aka.ms/atasizingtool)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Voraussetzungen für ATA](ata-prerequisites.md)
