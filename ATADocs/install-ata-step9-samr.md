---
title: Konfigurieren von Sam-R zum Aktivieren der Erkennung von Lateral Movement-Pfaden in Advanced Threat Analytics
description: Informationen zum Konfigurieren von SAM-R zum Erkennen eines Lateral Movement-Pfads in Advanced Threat Analytics (ATA)
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 09/08/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 7597ed25-87f5-472c-a496-d5f205c9c391
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: fa47a151ae8131039a5f7822acc5b541deb5c621
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2020
ms.locfileid: "79413977"
---
# <a name="install-ata---step-9"></a>Installieren von ATA: Schritt 9

*Gilt für: Advanced Threat Analytics Version 1.9*

> [!div class="step-by-step"]
> [« Schritt 8 ](install-ata-step7.md)

> [!NOTE]
> Bevor Sie eine neue Richtlinie erzwingen, stellen Sie immer sicher, dass Ihre Umgebung sicher bleibt, ohne die Anwendungs Kompatibilität zu beeinträchtigen, indem Sie zunächst die vorgeschlagenen Änderungen im Überwachungsmodus aktivieren und überprüfen. 

## <a name="step-9-configure-sam-r-required-permissions"></a>Schritt 9. Konfigurieren von für SAM-R erforderliche Berechtigungen

Der Erkennungsvorgang für [Lateral Movement-Pfade](use-case-lateral-movement-path.md) ist abhängig von Abfragen, die lokale Administratoren auf bestimmten Computern ermitteln. Diese Abfragen werden mithilfe des Sam-R-Protokolls über das in Schritt 2 erstellte ATA-Dienst Konto ausgeführt [. Verbindung mit AD herstellen](install-ata-step2.md).
 
Wenn Sie sicherstellen möchten, dass Windows-Clients und -Server zulassen, dass der ATA-Dienst diesen SAM-R-Vorgang durchführt, muss die **Gruppenrichtlinie** geändert werden, damit das ATA-Dienstkonto zu den konfigurierten Konten hinzugefügt wird, die in der Richtlinie für den **Netzwerkzugriff** aufgeführt sind. Diese Gruppenrichtlinie sollte für jedes Gerät in Ihrer Organisation angewendet werden. 

1. Finden der Richtlinie:

   - Richtlinienname: Netzwerkzugriff – Schränken Sie die Zahl der Clients ein, die Remoteaufrufe an SAM durchführen dürfen.
   - Speicherort: Computerkonfiguration, Windows-Einstellungen, Sicherheitseinstellungen, lokale Richtlinien, Sicherheitsoptionen
  
   ![Finden der Richtlinie](./media/samr-policy-location.png)

2. Fügen Sie den ATA-Dienst der Liste zulässiger Konten hinzu, die diese Aktion auf Ihren modernen Windows-Systemen durchführen können.
 
   ![Hinzufügen des Diensts](./media/samr-add-service.png)

3. Der **ATA-Dienst**, der bei der Installation erstellt wurde, weist nun die nötigen Berechtigungen auf, um SAM-R in der Umgebung auszuführen.

 Weitere Informationen zu SAM-R und der Gruppenrichtlinie finden Sie unter [Netzwerkzugriff: Einschränken der Clients, die Remoteaufrufe an SAM durchführen dürfen](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).


> [!div class="step-by-step"]
> [« Schritt 8 ](install-ata-step7.md)

## <a name="see-also"></a>Weitere Informationen:
- [Handbuch für die ATA POC-Bereitstellung](https://aka.ms/atapoc)
- [Tool zur Bemessung von ATA-Gateways](https://aka.ms/atasizingtool)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Voraussetzungen für ATA](ata-prerequisites.md)
