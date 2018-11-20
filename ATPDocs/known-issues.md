---
title: 'Azure ATP: Bekannte Probleme| Microsoft-Dokumentation'
description: In diesem Artikel werden die aktuell bekannten Probleme bei Azure ATP beschrieben.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 11/12/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: feea1982-ba23-48be-a468-98d2586cf840
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: c1c5aa0359ac0d24d2bf3fc3033986657c3fc897
ms.sourcegitcommit: 2afc1486b40431f442d51a53df06e289796de87e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/12/2018
ms.locfileid: "51561427"
---
*Gilt für: Azure Advanced Threat Protection*

# <a name="azure-atp-known-issues"></a>Azure ATP: Bekannte Probleme

Azure ATP weist gelegentlich technische oder funktionelle Einschränkungen auf, die die Verwendung von Azure ATP-Diensten in Ihrer Organisation einschränken oder verändern können. Die aktuell bekannten Einschränkungen, die weder eine bekannte Problemumgehung noch den Status „In Bearbeitung“ ohne eine bestimmte Aktualisierungszeit aufweisen, sind im Folgenden beschrieben. 

Informationen zur Umgehung bekannter Probleme bei Azure ATP finden Sie unter [Behandlung von bekannten Problemen bei Azure ATP](troubleshooting-atp-known-issues.md). Rufen Sie das [Azure ATP-Integritätscenter](atp-health-center.md) auf, um den Status Ihres Azure ATP-Mandanten zu überprüfen. 

## <a name="winrm-not-supported-using-windows-server-2016"></a>Keine Unterstützung von Windows Server 2016 durch WinRM
> [!div class="mx-tableFixed"]  
|Problem|Status|
|----|----|
|Windows Server 2016 wird derzeit nicht von WinRM unterstützt. Die zugehörige Erkennung und daraus resultierenden Warnungen (versuchte Remotecodeausführungen) sind nicht für Computer mit Windows Server 2016 verfügbar.|Es wird derzeit an einer Lösung für dieses Problem gearbeitet, damit Windows Server 2016 von WinRM unterstützt wird.|

## <a name="ad-groups-with-more-than-1000-members-have-limited-detail-sync"></a>Eingeschränkte Detailsynchronisierung bei AD-Gruppen mit mehr als 1000 Mitgliedern
> [!div class="mx-tableFixed"]  
|Problem|Status|
|----|----|
|Azure ATP unterstützt keine Detailsynchronisierung von Entitäten in AD-Gruppen mit mehr als 1000 Mitgliedern pro Gruppe. Beim Untersuchen von Entitäten in Gruppen mit mehr als 1000 Mitgliedern können bei manchen Entitäten Fehler beim Synchronisieren oder Anzeigen von Details auftreten.|Technische Einschränkungen. Keine bekannte Lösung.|

## <a name="report-downloads-cannot-contain-more-than-100000-entries"></a>Keine Berichtsdownloads mit mehr als 100.000 Einträgen
> [!div class="mx-tableFixed"]  
|Problem|Status|
|----|----|
|Azure ATP unterstützt keine Berichtsdownloads mit mehr als 100.000 Einträgen pro Bericht. Die Berichte werden unvollständig gerendert, wenn mehr als 100.000 Einträge enthalten sind.|Technische Einschränkungen. Keine bekannte Lösung.|

## <a name="see-also"></a>Weitere Informationen

- [Behandlung von bekannten Problemen bei Azure ATP](troubleshooting-atp-known-issues.md)
- [Behandlung von bekannten Problemen bei Azure ATP mithilfe von ATP-Protokollen](troubleshooting-atp-using-logs.md)
- [Neuerungen in Azure ATP](atp-whats-new.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)