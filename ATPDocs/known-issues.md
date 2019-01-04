---
title: 'Azure ATP: Bekannte Probleme| Microsoft-Dokumentation'
description: In diesem Artikel werden die aktuell bekannten Probleme bei Azure ATP beschrieben.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/17/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: feea1982-ba23-48be-a468-98d2586cf840
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 59da5e27433ba4ce38e05d4e723f763cf48ca23d
ms.sourcegitcommit: c3ee9495b9d4db985783dcabcc4fa77c7c8eaed4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/17/2018
ms.locfileid: "53454477"
---
*Gilt für: Azure Advanced Threat Protection*

# <a name="azure-atp-known-issues"></a>Azure ATP: Bekannte Probleme

Azure ATP weist gelegentlich technische oder funktionelle Einschränkungen auf, die die Verwendung von Azure ATP-Diensten in Ihrer Organisation einschränken oder verändern können. Die aktuell bekannten Einschränkungen, die weder eine bekannte Problemumgehung noch den Status „In Bearbeitung“ ohne eine bestimmte Aktualisierungszeit aufweisen, sind im Folgenden beschrieben. 

Informationen zur Umgehung bekannter Probleme bei Azure ATP finden Sie unter [Behandlung von bekannten Problemen bei Azure ATP](troubleshooting-atp-known-issues.md). Rufen Sie das [Azure ATP-Integritätscenter](atp-health-center.md) auf, um den Status Ihres Azure ATP-Mandanten zu überprüfen. 

## <a name="suspected-brute-force-attack-ldap-security-alert-display"></a>Sicherheitswarnungsanzeige für Suspected Brute Force attack (LDAP) (Verdacht auf einen Brute-Force-Angriff (LDAP))
> [!div class="mx-tableFixed"] 

|Problem|Status|
|----|----|
Die Sicherheitswarnung für den *Verdacht auf einen Brute-Force-Angriff (LDAP)* wird nicht immer wie erwartet angezeigt. In bestimmten Szenarien wird die Warnungsbeschreibung nicht in der richtigen Reihenfolge angezeigt.| Es wird derzeit an einer Lösung für dieses Problem gearbeitet.| 

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

## <a name="closed-issues"></a>Abgeschlossene Probleme

Diese Gruppe von bekannten Problemen wird jetzt geschlossen. Überprüfen Sie zur Referenz die Versionsnummer für diesen Fix.   
### <a name="remote-code-execution-attempts-using-remote-powershell-commands-or-scripts-are-not-detected-when-using-windows-server-2016---v257-december-2-2018"></a>Wenn Sie versuchen, mit Remote-PowerShell-Befehlen und -Skripts Code remote auszuführen, werden diese in Windows Server 2016 – v.2.57 nicht erkannt (2. Dezember 2018).
> [!div class="mx-tableFixed"]  
|Problem|Status|
|----|----|
|Wenn Sie versuchen, mit Remote-PowerShell-Befehlen Code remote auszuführen, werden diese derzeit nicht auf Sensorcomputern unter Windows Server 2016 erkannt. Verwandte Erkennungen und daraus resultierende Warnungen sind nicht verfügbar.|Es wird derzeit an einer Lösung für dieses Problem gearbeitet, damit Windows Server 2016 von WinRM unterstützt wird.|

## <a name="see-also"></a>Weitere Informationen

- [Behandlung von bekannten Problemen bei Azure ATP](troubleshooting-atp-known-issues.md)
- [Behandlung von bekannten Problemen bei Azure ATP mithilfe von ATP-Protokollen](troubleshooting-atp-using-logs.md)
- [Neuerungen in Azure ATP](atp-whats-new.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)