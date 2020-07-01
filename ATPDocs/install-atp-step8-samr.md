---
title: Konfigurieren von SAM-R zum Aktivieren der Erkennung von Lateral Movement-Pfaden in Azure ATP
description: Erläutert das Konfigurieren von Azure ATP für das Ausführen von Remoteaufrufen an SAM
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 05/16/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: b09adce3-0fbc-40e3-a53f-31f57fe79ca3
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 76b38cfb407007b58436d7790b7e530026aa5215
ms.sourcegitcommit: c5b64066f28b5a97034c1b92908b1c5e3221a36d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/25/2020
ms.locfileid: "85365757"
---
# <a name="configure-azure-atp-to-make-remote-calls-to-sam"></a>Konfigurieren von Azure ATP für das Ausführen von Remoteaufrufen an SAM

Der Erkennungsvorgang für [Lateral Movement-Pfade](use-case-lateral-movement-path.md) von Azure ATP ist abhängig von Abfragen, die lokale Administratoren auf bestimmten Computern ermitteln. Diese Abfragen werden mithilfe des SAM-R-Protokolls über das während der Azure ATP-Installation in [Schritt 2 erstellte Azure ATP-Dienstkonto ausgeführt. Verbinden mit AD](install-atp-step2.md).

## <a name="configure-sam-r-required-permissions"></a>Konfigurieren von für SAM-R erforderliche Berechtigungen

Wenn Sie sicherstellen möchten, dass Windows-Clients und -Server zulassen, dass Ihr Azure ATP-Konto SAM-R durchführt, muss die **Gruppenrichtlinie** geändert werden, damit das Azure ATP-Dienstkonto zu den konfigurierten Konten hinzugefügt wird, die in der Richtlinie für den **Netzwerkzugriff** aufgeführt sind. Stellen Sie sicher, dass Gruppenrichtlinien auf alle Computer außer Domänencontroller angewendet werden.

> [!Note]
> Bevor Sie neue Richtlinien wie die zuvor erwähnte erzwingen, ist es wichtig, dass Sie die Sicherheit Ihrer Umgebung gewährleisten können und dass die Änderungen sich nicht auf die Anwendungskompatibilität auswirken. Aktivieren und überprüfen Sie daher zunächst die Kompatibilität vorgeschlagener Änderungen im Überwachungsmodus, bevor Sie Änderungen an Ihrer Produktionsumgebung vornehmen.

1. Finden der Richtlinie:

   - Richtlinienname: Netzwerkzugriff: Clients einschränken, die Remoteaufrufe an SAM ausführen dürfen
   - Speicherort: Computerkonfiguration, Windows-Einstellungen, Sicherheitseinstellungen, lokale Richtlinien, Sicherheitsoptionen

   ![Finden der Richtlinie](./media/samr-policy-location.png)

2. Fügen Sie den Azure ATP-Dienst der Liste von zulässigen Konten hinzu, die diese Aktion auf Ihren modernen Windows-Systemen durchführen können.

   ![Hinzufügen des Diensts](./media/samr-add-service.png)

3. Der **Azure ATP-Dienst**, der bei der Installation erstellt wurde, weist nun die nötigen Berechtigungen auf, um SAM-R in der Umgebung auszuführen.

Weitere Informationen zu SAM-R und dieser Gruppenrichtlinie, finden Sie unter [Netzwerkzugriff: Clients einschränken, die Remoteaufrufe an SAM ausführen dürfen](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).

## <a name="see-also"></a>Weitere Informationen

- [Investigating lateral movement path attacks with Azure ATP (Untersuchen von Lateral Movement-Pfaden mit Azure ATP)](use-case-lateral-movement-path.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
