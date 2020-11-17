---
title: Neues in ATA Version 1.7
description: Listet Neuerungen sowie bekannte Probleme in ATA Version 1.7 auf
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 1/23/2017
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: be9ee613-4eb3-40f1-8973-e7f0a707ff57
ms.reviewer: ''
ms.suite: ems
ms.openlocfilehash: e8750b31bb8dec807202e0053df7cabad2850967
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2020
ms.locfileid: "94689478"
---
# <a name="whats-new-in-ata-version-17"></a>Neues in ATA Version 1.7

Die vorliegenden Anmerkungen zu dieser Version enthalten Informationen zu bekannten Problemen in dieser Version von Advanced Threat Analytics.

## <a name="whats-new-in-the-ata-17-update"></a>Neuerungen beim Update auf ATA 1.7
Das Update auf ATA 1.7 bietet Verbesserungen in folgenden Bereichen:

- Neue und aktualisierte Erkennung

- Rollenbasierte Zugriffssteuerung

- Unterstützung für Windows Server 2016 und Windows Server 2016 Core

- Verbesserungen der Benutzeroberfläche

- Kleinere Änderungen


### <a name="new--updated-detections"></a>Neue und aktualisierte Erkennung


- **Reconnaissance mithilfe von Verzeichnisdienstenumeration:** Im Rahmen dieser Phase der Reconnaissance sammeln Angreifer auf verschiedene Weise Informationen zu den Entitäten im Netzwerk. Die Verzeichnisdienstenumeration mit dem SAM-R-Protokoll ermöglicht es Angreifern, die Liste der Benutzer und Gruppen in einer Domäne zu erhalten und die Interaktion zwischen den verschiedenen Entitäten zu verstehen. 

- **Verbesserungen bei Pass-the-Hash-Angriffen:** Wir haben zusätzliche Verhaltensmodelle für Authentifizierungsmuster von Entitäten hinzugefügt, um die Pass-the-Hash-Erkennung zu verbessern. Dank dieser Modelle kann ATA das Verhalten von Entitäten verdächtigen NTLM-Authentifizierungen zuordnen und echte Pass-the-Hash-Angriffe vom Verhalten falsch-positiver Szenarien unterscheiden.

- **Verbesserungen bei Pass-the-Ticket-Angriffen:** Um hochentwickelte Attacken (allgemein, aber auch speziell Pass-the-Ticket-Angriffe) erfolgreich zu erkennen, muss die Korrelation zwischen einer IP-Adresse und dem Computerkonto präzise sein. Dies ist eine Herausforderung in Umgebungen, in denen IP-Adressen sich beabsichtigt schnell ändern, (z.B. Wi-Fi-Netzwerke und wenn mehrere virtuelle Maschinen einen gemeinsamen Host nutzen). Um diese Herausforderung zu überwinden und die Genauigkeit der Erkennung von Pass-the-Ticket-Angriffen zu verbessern, wurde der Mechanismus zur Auflösung des Netzwerknamens (Network Name Resolution; NNR) von ATA deutlich verbessert, um Fehlerquote zu reduzieren.

- **Verbesserungen bei ungewöhnlichem/nicht normalem Verhalten:** In ATA 1.7 wurden die NTLM-Authentifizierungsdaten als Datenquelle für nicht normales Verhalten hinzugefügt. Dazu decken die Algorithmen nun ein größeres Spektrum von Entitätsverhalten im Netzwerk ab. 

- **Verbesserungen bei der ungewöhnlichen Protokollimplementierung:** ATA erkennt nun die ungewöhnliche Protokollimplementierung im Kerberos-Protokoll, zusammen mit zusätzlichen Anomalien im NTLM-Protokoll. Diese neuen Kerberos-Anomalien werden gewöhnlicherweise für Overpass-the-Hash-Angriffe verwendet.


### <a name="infrastructure"></a>Infrastruktur

- **Rollenbasierte Zugriffskontrolle:** die Funktion für die rollenbasierte Zugriffskontrolle (Role-Based Access Control; RBAC) ATA 1.7 enthält drei Rollen: ATA Administrator, ATA Analyst und ATA Executive.

- **Unterstützung für Windows Server 2016 und Windows Server Core:** ATA 1.7 unterstützt die Bereitstellung von Lightweight-Gateways auf Domänencontrollern unter Windows Server 2008 R2 SP1 (ohne Server Core), Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 (mit Core, jedoch ohne Nano). Darüber hinaus unterstützt dieses Release Windows Server 2016 sowohl für die ATA Center- als auch die ATA-Gatewaykomponenten.

### <a name="user-experience"></a>Benutzererfahrung
- **Einfache Konfiguration:** Die ATA-Konfigurationsbenutzeroberfläche wurde in dieser Version neu gestaltet, um eine höhere Benutzerfreundlichkeit und eine bessere Unterstützung für Umgebungen mit mehreren ATA-Gateways zu gewährleisten. Mit diesem Release wird auch die Updateseite für das ATA-Gateway eingeführt, um die Verwaltung von automatische Updates für die verschiedenen Gateways zu erleichtern.

## <a name="known-issues"></a>Bekannte Probleme
In dieser Version bestehen die folgenden bekannten Probleme.

### <a name="gateway-automatic-update-may-fail"></a>Die automatische Aktualisierung des Gateways kann fehlschlagen.
**Symptome:** Das ATA-Gateway kann in einer Umgebung mit langsamen WAN-Verbindungen das Update-Timeout (100 Sekunden) erreichen. Updates können daraufhin nicht erfolgreich abgeschlossen werden.
In der ATA-Konsole zeigt das ATA-Gateway über längere Zeit den Status „Wird aktualisiert (Paket wird heruntergeladen)“ an und schlägt schließlich fehl.
**Problemumgehung:** Laden Sie das neueste ATA-Gateway-Paket aus der ATA-Konsole herunter, und aktualisieren das ATA-Gateway manuell, um dieses Problem zu umgehen.

> [!IMPORTANT]
>  Die automatische Erneuerung der von ATA verwendeten Zertifikate wird nicht unterstützt. Die Verwendung dieser Zertifikate kann dazu führen, dass ATA bei einer automatischen Erneuerung der Zertifikate nicht mehr funktioniert. 

### <a name="no-browser-support-for-jis-encoding"></a>Keine Browserunterstützung für JIS-Codierung
**Symptome:** Die ATA-Konsole funktioniert in Browsern mit JIS-Codierung möglicherweise nicht erwartungsgemäß. **Problemumgehung:** Ändern Sie die Codierung des Browsers zu Unicode UTF-8.
 
### <a name="dropped-port-mirror-traffic-when-using-vmware"></a>„Netzwerkdatenverkehr aus Portspiegelung gelöscht“ bei Verwendung von VMware

Die Warnung, dass Netzwerkdatenverkehr aus der Portspiegelung gelöscht wurde, wird ausgegeben, wenn ein Lightweight-Gateway auf VMware verwendet wird.

Wenn Sie Domänencontroller auf virtuellen VMware-Computern verwenden, wird möglicherweise die Warnung **Netzwerkverkehr aus Portspiegelung gelöscht** ausgegeben. Dies kann aufgrund von Konfigurationskonflikten in VMware auftreten. Um zu vermeiden, dass diese Warnung ausgegeben wird, können Sie überprüfen, ob auf dem virtuellen Computer die folgenden Einstellungen auf „0“ oder „deaktiviert“ festgelegt sind:  

- TsoEnable
- LargeSendOffload(IPv4)
- IPv4 TSO Offload

Deaktivieren Sie ebenso IPv4 Giant TSO Offload. Weitere Informationen finden Sie in der VMware-Dokumentation.

### <a name="automatic-gateway-update-fail-when-updating-to-17-update-1"></a>Fehler bei der automatischen Gatewayaktualisierung auf Version 1.7 Update 1

Beim Aktualisieren von ATA 1.7 auf ATA 1.7 Update 1 funktionieren sowohl der automatische ATA-Gatewayaktualisierungsprozess als auch die manuelle Installation des Gateways mithilfe des Gatewaypakets möglicherweise nicht wie erwartet.
Dieses Problem tritt auf, wenn das vom ATA-Center verwendete Zertifikat vor der Aktualisierung von ATA geändert wurde.
Um das Problem zu überprüfen, prüfen Sie das **Microsoft.Tri.Gateway.Updater.log** auf dem ATA-Gateway, und suchen Sie nach folgenden Ausnahmen: **System.Net.Http.HttpRequestException: Beim Senden der Anforderung ist ein Fehler aufgetreten. ---> System.Net.WebException: Die zugrunde liegende Verbindung wurde geschlossen: Unerwarteter Fehler beim Senden. ---> System.IdentityModel.Tokens.SecurityTokenValidationException: Fehler bei der Überprüfung des Zertifikatfingerabdrucks**

![Fehler bei der Aktualisierung des ATA-Gateways](media/17update_gatewaybug.png)

Um das Problem zu beheben, wechseln Sie nach dem Ändern des Zertifikats an einer Eingabeaufforderung mit erhöhten Rechten zum Speicherort **%ProgramFiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**, und führen Sie Folgendes aus:

1. Mongo.exe ATA (ATA muss groß geschrieben werden) 

1. CenterThumbprint=db.SystemProfile.find({_t:"CenterSystemProfile"}).toArray()[0].Configuration.SecretManagerConfiguration.CertificateThumbprint;

1. db.SystemProfile.update({_t:"ServiceSystemProfile"},{$set:{"Configuration.ManagementClientConfiguration.ServerCertificateThumbprint":CenterThumbprint}}, {multi: true})

### <a name="export-suspicious-activity-details-to-excel-may-fail"></a>Beim Export von Details über verdächtige Aktivität nach Excel tritt möglicherweise ein Fehler auf
Beim Versuch, Details über verdächtige Aktivität in eine Excel-Datei zu exportieren, tritt möglicherweise der folgende Fehler auf: *Error [BsonClassMapSerializer`1] System.FormatException: An error occurred while deserializing the Activity property of class Microsoft.Tri.Common.Data.NetworkActivities.SuspiciousActivityActivity: Element 'ResourceIdentifier' does not match any field or property of class Microsoft.Tri.Common.Data.EventActivities.NtlmEvent. ---> System.FormatException: Element 'ResourceIdentifier' does not match any field or property of class Microsoft.Tri.Common.Data.EventActivities.NtlmEvent.* (Fehler [BsonClassMapSerializer`1] System.FormatException: Fehler beim Deserialisieren der Aktivitätseigenschaft der Klasse Microsoft.Tri.Common.Data.NetworkActivities.SuspiciousActivityActivity: Das Element 'ResourceIdentifier' stimmt mit keinem Feld und keiner Eigenschaft der Klasse Microsoft.Tri.Common.Data.EventActivities.NtlmEvent überein. ---> System.FormatException: Das Element 'ResourceIdentifier' stimmt mit keinem Feld und keiner Eigenschaft der Klasse Microsoft.Tri.Common.Data.EventActivities.NtlmEvent überein.)

Um dieses Problem zu beheben, wechseln Sie an einer Eingabeaufforderung mit erhöhten Rechten zum Speicherort **%ProgramFiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**, und führen Sie folgende Befehle aus:
1. `Mongo.exe ATA` (ATA muss in Großbuchstaben angegeben werden)
2. `db.SuspiciousActivityActivity.update({ "Activity._t": "NtlmEvent" },{$unset: {"Activity.ResourceIdentifier": ""}}, {multi: true});`

## <a name="minor-changes"></a>Kleinere Änderungen

- ATA verwendet jetzt OWIN anstelle von IIS für die ATA-Konsole.
- Wenn der ATA Center-Dienst nicht verfügbar ist, können Sie nicht auf die ATA-Konsole zugreifen.
- Kurzfristige Lease-Subnetze sind aufgrund von Änderungen in der ATA NNR nicht mehr erforderlich.

## <a name="see-also"></a>Weitere Informationen
[Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Aktualisieren von ATA auf Version 1.7 – Migrationshandbuch](ata-update-1.7-migration-guide.md)

