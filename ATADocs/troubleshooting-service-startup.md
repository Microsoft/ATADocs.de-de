---
title: Behandeln von Problemen beim Starten von Advanced Threat Analytics | Microsoft-Dokumentation
description: Beschreibt, wie Sie häufige Fehler beim Starten von ATA beheben können
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 5a65285c-d1de-4025-9bb4-ef9c20b13cfa
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 21afd487fbf15b3fc1f5d618e0e6b98d50d07cae
ms.sourcegitcommit: f37127601166216e57e56611f85dd783c291114c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/24/2019
ms.locfileid: "54839562"
---
# <a name="troubleshooting-service-startup"></a>Problembehandlung beim Starten eines Diensts

*Gilt für: Advanced Threat Analytics Version 1.9*

## <a name="troubleshooting-ata-center-service-startup"></a>Problembehandlung beim Starten des ATA Center-Diensts

Wenn ATA Center nicht gestartet wird, führen Sie das folgende Verfahren zur Fehlerbehebung durch:

1.  Führen Sie den folgenden Windows PowerShell-Befehl aus: `Get-Service Pla | Select Status`,
    um sicherzustellen, dass der Leistungsindikatordienst ausgeführt wird. Wenn es nicht funktioniert, liegt das Problem bei der Plattform, und Sie müssen sicherstellen, dass der Dienst wieder ausgeführt werden kann.
2.  Wenn er ausgeführt wurde, versuchen Sie einen Neustart, und beobachten Sie, ob das Problem behoben wird: `Restart-Service Pla`
3.  Versuchen Sie, manuell einen neuen Datensammler zu erstellen (einer reicht aus, auch nur um z.B. CPUs von Computern zu sammeln).
Wenn er gestartet werden kann, ist die Plattform wahrscheinlich in Ordnung. Andernfalls liegt noch immer ein Plattformproblem vor.

4.  Versuchen Sie, den ATA-Datensammler über eine Eingabeaufforderung mit erhöhten Rechten manuell zu erstellen. Führen Sie dazu folgende Befehle aus:

        sc stop ATACenter
        logman stop "Microsoft ATA Center"
        logman export "Microsoft ATA Center" -xml c:\center.xml
        logman delete "Microsoft ATA Center"
        logman import "Microsoft ATA Center" -xml c:\center.xml
        logman start "Microsoft ATA Center"
        sc start ATACenter

## <a name="troubleshooting-ata-lightweight-gateway-startup"></a>Problembehandlung beim Starten des ATA-Lightweight-Gateways

**Symptom**

Ihr ATA-Gateway startet nicht, und es wird folgende Fehlermeldung ausgegeben:<br></br>
*System.Net.Http.HttpRequestException: Der Antwortstatuscode gibt keinen Erfolg an: 500 (Interner Serverfehler)*

**Beschreibung**

Der Grund ist folgender: Im Rahmen des Installationsprozesses des Lightweight-Gateways weist ATA einen CPU-Schwellenwert zu. Das Lightweight-Gateway kann diese zugewiesene CPU mit einem Puffer von 15% nutzen. Wenn Sie manuell einen Schwellenwert mit dem Registrierungsschlüssel festgelegt haben, verhindert dieser Konflikt das Starten des Lightweight-Gateways. 

**Lösung**

1. Wenn sich unter dem Registrierungsschlüssel ein DWORD-Wert mit dem Namen **Disable Performance Counters** befindet, achten Sie darauf, dass dieser auf **0**: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\PerfOS\Performance\` festgelegt ist.
    `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\PerfProc\Performance`
 
2. Starten Sie dann den PLA-Dienst neu. Das ATA-Lightweight-Gateway erkennt die Änderung automatisch und startet den Dienst neu.


## <a name="see-also"></a>Weitere Informationen
- [Voraussetzungen für ATA](ata-prerequisites.md)
- [ATA-Kapazitätsplanung](ata-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-collection.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
