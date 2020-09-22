---
title: Problembehandlung beim Starten von Advanced Threat Analytics-Dienst
description: Beschreibt, wie Sie häufige Fehler beim Starten von ATA beheben können
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 5a65285c-d1de-4025-9bb4-ef9c20b13cfa
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: d4e5dda205aba4737e074853f22659c6e74a98d5
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2020
ms.locfileid: "90910734"
---
# <a name="troubleshooting-service-startup"></a>Problembehandlung beim Starten eines Diensts

[!INCLUDE [Banner for top of topics](includes/banner.md)]

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="troubleshooting-ata-center-service-startup"></a>Problembehandlung beim Starten des ATA Center-Diensts

Wenn ATA Center nicht gestartet wird, führen Sie das folgende Verfahren zur Fehlerbehebung durch:

1. Führen Sie den folgenden Windows PowerShell-Befehl aus: `Get-Service Pla | Select Status`,
   um sicherzustellen, dass der Leistungsindikatordienst ausgeführt wird. Wenn es nicht funktioniert, liegt das Problem bei der Plattform, und Sie müssen sicherstellen, dass der Dienst wieder ausgeführt werden kann.
1. Wenn er ausgeführt wurde, versuchen Sie, ihn neu zu starten, und überprüfen Sie, ob das Problem behoben wird:  `Restart-Service Pla`
1. Versuchen Sie, manuell einen neuen Datensammler zu erstellen (einer reicht aus, auch nur um z.B. CPUs von Computern zu sammeln).
Wenn er gestartet werden kann, ist die Plattform wahrscheinlich in Ordnung. Andernfalls liegt noch immer ein Plattformproblem vor.

1. Versuchen Sie, den ATA-Datensammler über eine Eingabeaufforderung mit erhöhten Rechten manuell zu erstellen. Führen Sie dazu folgende Befehle aus:

```dos
sc stop ATACenter
logman stop "Microsoft ATA Center"
logman export "Microsoft ATA Center" -xml c:\center.xml
logman delete "Microsoft ATA Center"
logman import "Microsoft ATA Center" -xml c:\center.xml
logman start "Microsoft ATA Center"
sc start ATACenter
```

## <a name="troubleshooting-ata-lightweight-gateway-startup"></a>Problembehandlung beim Starten des ATA-Lightweight-Gateways

**Symptom**

Ihr ATA-Gateway startet nicht, und es wird folgende Fehlermeldung ausgegeben:<br></br>
*System.Net.Http.HttpRequestException: Der Antwortstatuscode gibt keinen Erfolg an: 500 (Interner Serverfehler).*

**Beschreibung**

Der Grund ist folgender: Im Rahmen des Installationsprozesses des Lightweight-Gateways weist ATA einen CPU-Schwellenwert zu. Das Lightweight-Gateway kann diese zugewiesene CPU mit einem Puffer von 15% nutzen. Wenn Sie manuell einen Schwellenwert mit dem Registrierungsschlüssel festgelegt haben, verhindert dieser Konflikt das Starten des Lightweight-Gateways. 

**Lösung**

1. Wenn unter den Registrierungs Schlüsseln ein DWORD-Wert mit dem Namen **Leistungsindikatoren deaktivieren** vorhanden ist, stellen Sie sicher, dass der Wert auf **0**festgelegt ist:

```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\PerfOS\Performance\
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\PerfProc\Performance
```

1. Starten Sie dann den PLA-Dienst neu. Das ATA-Lightweight-Gateway erkennt die Änderung automatisch und startet den Dienst neu.

## <a name="see-also"></a>Weitere Informationen

- [ATA-Voraussetzungen](ata-prerequisites.md)
- [ATA-Kapazitätsplanung](ata-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-collection.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
