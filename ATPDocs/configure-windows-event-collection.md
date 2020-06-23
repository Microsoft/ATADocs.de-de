---
title: Konfigurieren der Windows-Ereignissammlung in Azure Advanced Threat Protection
description: In diesem Schritt bei der ATP-Installation konfigurieren Sie die Windows-Ereignissammlung.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 02/19/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 88692d1a-45a3-4d54-a549-4b5bba6c037b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: adf5901307430fec54d4f3a625df3a5a1a47fe15
ms.sourcegitcommit: fbb0768c392f9bccdd7e4adf0e9a0303c8d1922c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2020
ms.locfileid: "84772614"
---
# <a name="configure-windows-event-collection"></a>Konfigurieren der Windows-Ereignissammlung

Um die Funktionen zum Erkennen von Bedrohungen zu verbessern, benötigt Azure Advanced Threat Protection (Azure ATP) die folgenden Windows-Ereignisse: 4776, 4732, 4733, 4728, 4729, 4756, 4757, 7045 und 8004. Diese Ereignisse können entweder automatisch vom Azure ATP-Sensor gelesen oder, falls dieser nicht bereitgestellt wurde, an den eigenständigen Azure ATP-Sensor weitergeleitet werden. Dazu gibt es zwei Möglichkeiten: die [Konfiguration des eigenständigen Azure ATP-Sensors](configure-event-forwarding.md), sodass dieser auf SIEM-Ereignisse lauscht, oder die [Konfiguration der Windows-Ereignisweiterleitung](configure-event-forwarding.md).

> [!NOTE]
>
> - Eigenständige Azure ATP-Server unterstützen nicht die Erstellung von Protokolleinträgen für Ereignisablaufverfolgung für Windows (Event Tracing for Windows, ETW), die Daten für mehrere Erkennungen bereitstellen. Zur vollständigen Abdeckung Ihrer Umgebung empfiehlt es sich, den Azure ATP-Sensor bereitzustellen.
> - Es ist wichtig, vor dem Aktivieren der Ereignissammlung die [Überwachungsrichtlinien](atp-advanced-audit-policy.md) zu überprüfen und zu verifizieren, um sicherzustellen, dass die Domänencontroller ordnungsgemäß für die Aufzeichnung der erforderlichen Ereignisse konfiguriert sind.

Zusätzlich zum Sammeln und Analysieren des Netzwerkverkehrs zu und von den Domänencontrollern kann Azure ATP Windows-Ereignisse heranziehen, um Erkennungen weiter zu verbessern. Azure ATP verwendet die Windows-Ereignisse 4776 und 8004 für NTLM, um verschiedene Erkennungen zu verbessern. Die Ereignisse 4732, 4733, 4728, 4729, 4756, 4757, 7045 und 8004 dienen dazu, die Erkennung von Änderungen an vertraulichen Gruppen und die Diensterstellung zu verbessern. Dies kann aus dem SIEM-Agent heraus erfolgen oder indem Sie die Windows-Ereignisweiterleitung von Ihrem Domänencontroller aus einrichten. Die gesammelten Ereignisse versorgen Azure ATP mit zusätzlichen Informationen, die nicht über den Datenverkehr des Domänencontrollers verfügbar sind.

> [!NOTE]
> Gruppenrichtlinien zum Sammeln des Windows-Ereignisses 8004 auf Domänenebene dürfen **nur** auf Domänencontroller angewendet werden.

## <a name="ntlm-authentication-using-windows-event-8004"></a>NTLM-Authentifizierung mithilfe des Windows-Ereignisses 8004

So konfigurieren Sie die Windows-Ereignis 8004-Sammlung:

1. Navigieren Sie zu: Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\Sicherheitsoptionen
2. Konfigurieren oder erstellen Sie eine **Gruppenrichtlinie auf Domänenebene**, die wie folgt auf die Domänencontroller in jeder Domäne angewendet wird:
   - Netzwerksicherheit: Beschränken von NTLM: Ausgehender NTLM-Datenverkehr zu Remoteservern = **Alle überwachen**
   - Netzwerksicherheit: Beschränken von NTLM: NTLM-Authentifizierung in dieser Domäne überwachen = **Alle aktivieren**
   - Netzwerksicherheit: Beschränken von NTLM: Eingehenden NTLM-Datenverkehr überwachen = **Überwachung für alle Konten aktivieren**

Bei der Analyse des Windows-Ereignisses 8004 durch den Azure ATP-Sensor werden Azure ATP-NTLM-Authentifizierungsaktivitäten durch die Daten ergänzt, auf die auf dem Server zugegriffen wird.

## <a name="see-also"></a>Weitere Informationen

- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](https://aka.ms/aatpsizingtool)
- [Referenz zum Azure ATP-SIEM-Protokoll](cef-format-sa.md)
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
