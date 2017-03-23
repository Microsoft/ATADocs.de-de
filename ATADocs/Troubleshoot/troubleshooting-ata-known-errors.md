---
title: Behandeln von Problemen im Advanced Threat Analytics-Fehlerprotokoll | Microsoft-Dokumentation
description: "Beschreibt, wie Sie übliche Fehler in ATA beheben können"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/14/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 0c72b14a042e473c0cd59811db63ecafc4ec02d4
ms.sourcegitcommit: f18c0841d85e54eca940c8cbf226938b3c2bc80f
translationtype: HT
---
*Gilt für: Advanced Threat Analytics Version 1.7*



# <a name="troubleshooting-the-ata-error-log"></a>Behandeln von Problemen im ATA-Fehlerprotokoll

In diesem Abschnitt sind mögliche Fehler, die es in den Bereitstellungen von ATA geben kann, und die Schritte zu deren Behebung aufgeführt.

## <a name="ata-gateway-errors"></a>ATA-Gateway-Fehler

|Fehler|Beschreibung|Lösung|
|-------------|----------|---------|
|System.DirectoryServices.Protocols.LdapException: Lokaler Fehler.|Die ATA-Gateway konnte sich nicht beim Domänencontroller authentifizieren.|1. Vergewissern Sie sich, dass der DNS-Eintrag des Domänencontrollers im DNS-Server ordnungsgemäß konfiguriert ist. <br>2. Vergewissern Sie sich, dass die Zeit des ATA-Gateways mit der Zeit des Domänencontrollers synchronisiert ist.|
|System.IdentityModel.Tokens.SecurityTokenValidationException: Die Zertifikatkette kann nicht überprüft werden.|Das ATA-Gateway konnte das Zertifikat von ATA Center nicht überprüfen.|1. Vergewissern Sie sich, dass das Zertifikat der Stammzertifizierungsstelle im Zertifikatspeicher für vertrauenswürdige Zertifikate auf dem ATA-Gateway installiert ist. <br>2. Überprüfen Sie, ob die Zertifikatsperrliste (Certificate Revocation List, CRL) verfügbar ist und ob die Überprüfung auf Zertifikatssperrung ausgeführt werden kann.|
|Microsoft.Common.ExtendedException: Erstellungszeit konnte nicht analysiert werden.|Das ATA-Gateway konnte Syslog-Meldungen, die vom SIEM weitergeleitet wurden, nicht analysieren.|Stellen Sie sicher, dass das SIEM so konfiguriert ist, dass es die Meldungen in einem der Formate weiterleitet, die von ATA unterstützt werden.|
|System.ServiceModel.FaultException: Fehler beim Überprüfen der Sicherheit für die Nachricht.|Die ATA-Gateway konnte sich nicht bei ATA Center authentifizieren.|Vergewissern Sie sich, dass die Zeit des ATA-Gateways mit der Zeit von ATA-Center synchronisiert ist.|
|System.ServiceModel.EndpointNotFoundException: Es konnte keine Verbindung mit net.tcp://center.ip.addr:443/IEntityReceiver hergestellt werden.|Das ATA-Gateway konnte keine Verbindung mit ATA Center herstellen.|Vergewissern Sie sich, dass die Netzwerkeinstellungen richtig sind und dass die Verbindung zwischen dem ATA-Gateway und ATA Center aktiv ist.|
|System.DirectoryServices.Protocols.LdapException: Der LDAP-Server ist nicht verfügbar.|Das ATA-Gateway konnte den Domänencontroller nicht über das LDAP-Protokoll abfragen.|1. Vergewissern Sie sich, dass das Benutzerkonto, das von ATA zum Herstellen einer Verbindung mit der Active Directory-Domäne verwendet wird, vollen Lesezugriff auf alle Objekte in der Active Directory-Struktur hat. <br>2. Stellen Sie sicher, dass der Domänencontroller nicht so eingestellt ist, dass er LDAP-Abfragen von dem Benutzerkonto ablehnt, das von ATA verwendet wird.|
|Microsoft.Tri.Infrastructure.ContractException: Vertragsausnahme|Die ATA-Gateway konnte die Konfiguration von ATA Center nicht synchronisieren.|Schließen Sie die Konfiguration des ATA-Gateways in der ATA-Konsole ab.|
|System.Reflection.ReflectionTypeLoadException: Mindestens ein angeforderter Typ kann nicht geladen werden. Weitere Informationen erhalten Sie durch Abrufen der LoaderExceptions-Eigenschaft.|Auf dem ATA-Gateway ist die Nachrichtenanalyse installiert.| Deinstallieren Sie die Nachrichtenanalyse.|
|Fehler [Layout] System.OutOfMemoryException: Ausnahme vom Typ „System.OutOfMemoryException“ ausgelöst.|Auf dem ATA-Gateway ist nicht genügend Arbeitsspeicher verfügbar.|Erhöhen Sie die Arbeitsspeicherkapazität auf dem Domänencontroller.|
|Fehler beim Start von Live-Consumer  ---> Microsoft.Opn.Runtime.Monitoring.MessageSessionException: Der PEFNDIS-Ereignisanbieter ist nicht bereit.|PEF (Nachrichtenanalyse) wurde nicht ordnungsgemäß installiert.|Wenn Sie Hyper-V verwenden, versuchen Sie, die Hyper-V-Integrationsdienste zu aktualisieren. Kontaktieren Sie alternativ den Support für eine Problemumgehung.|
|Installationsfehler: 0x80070652|Auf Ihrem Computer stehen weitere Installationen aus.|Warten Sie, bis die anderen Installationen abgeschlossen sind, und starten Sie den Computer gegebenenfalls neu.|
|System.InvalidOperationException: Die Instanz „Microsoft.Tri.Gateway“ existiert nicht in der angegebenen Kategorie.|Die PIDs wurden für Prozessnamen im ATA-Gateway aktiviert.|Verwenden Sie [KB281884](https://support.microsoft.com/en-us/kb/281884), um die PIDs in den Prozessnamen zu deaktivieren.|
|System.InvalidOperationException: Die Kategorie ist nicht vorhanden.|Möglicherweise wurden die Leistungsindikatoren in der Registrierung deaktiviert.|Verwenden Sie [KB2554336](https://support.microsoft.com/en-us/kb/2554336), um die Leistungsindikatoren neu zu erstellen.|
|System.ApplicationException: Die ETW-Sitzung „MMA-ETW-Livecapture-a4f595bd-f567-49a7-b963-20fa4e370329“ kann nicht gestartet werden.|In der HOSTS-Datei existiert ein Hosteintrag, der auf den Kurznamen des Computers verweist.|Entfernen Sie den Hosteintrag aus „C:\Windows\System32\drivers\etc\HOSTS“, oder ändern Sie ihn in einen eindeutigen Domänennamen um.|
|System.IO.IOException: Fehler bei der Authentifizierung, da die Gegenseite den Transportstream geschlossen hat.|TLS 1.0 ist auf dem ATA-Gateway deaktiviert, .NET ist aber für die Verwendung von TLS 1.2 eingerichtet.|Verwenden Sie eine der folgenden Optionen: </br> TLS 1.0 auf dem ATA-Gateway aktivieren </br>Aktivieren Sie TLS 1.2 in .NET, indem Sie die Registrierungsschlüssel wie folgt für die Verwendung der Standardwerte des Betriebssystems für LLS und TLS einrichten: `[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001` </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"`|



## <a name="ata-lightweight-gateway-errors"></a>Fehler bei ATA-Lightweight-Gateways

**Fehler**: Beim Verwenden eines Lightweight-Gateways unter VMware wird eine Warnung ausgegeben, dass Datenverkehr aus einer Portspiegelung gelöscht wird.

**Beschreibung**: Wenn Sie Domänencontroller auf virtuellen VMware-Computern verwenden, wird möglicherweise die Warnung **Netzwerkdatenverkehr aus Portspiegelung gelöscht** ausgegeben. Dies kann aufgrund von Konfigurationskonflikten in VMware auftreten. 
**Lösung**: Um diese Warnungen zu vermeiden, überprüfen Sie, ob die folgenden Einstellungen auf „0“ oder „deaktiviert“ festgelegt sind: TsoEnable, LargeSendOffload, IPv4, TSO Offload. Deaktivieren Sie ebenso IPv4 Giant TSO Offload. Weitere Informationen finden Sie in der VMware-Dokumentation.


## <a name="ata-iis-errors-not-applicable-for-ata-v17-and-above"></a>ATA-IIS-Fehler (gilt nicht für ATA Version&1;.7 und höher)
|Fehler|Beschreibung|Lösung|
|-------------|----------|---------|
|HTTP-Fehler 500.19 – Interner Serverfehler|Das IIS URL Rewrite-Modul konnte nicht ordnungsgemäß installiert werden.|Deinstallieren Sie das IIS URL Rewrite-Modul, und installieren Sie es dann erneut.<br>[Laden Sie das IIS URL Rewrite-Modul herunter](http://go.microsoft.com/fwlink/?LinkID=615137)|

## <a name="deployment-errors"></a>Bereitstellungsfehler
|Fehler|Beschreibung|Lösung|
|-------------|----------|---------|
|Fehler bei der Installation von .NET Framework 4.6.1. Fehlernummer ist 0x800713ec.|Die erforderlichen Komponenten für .NET Framework 4.6.1 sind nicht auf dem Server installiert. |Stellen Sie vor der Installation von ATA sicher, dass die Windows-Updates [KB2919442](https://www.microsoft.com/download/details.aspx?id=42135) und [KB2919355](https://support.microsoft.com/kb/2919355) auf dem Server installiert sind.|

![Bild zu ATA-.NET-Installationsfehler](media/netinstallerror.png)


## <a name="see-also"></a>Weitere Informationen
- [Voraussetzungen für ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA-Kapazitätsplanung](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Konfigurieren der Ereignissammlung](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurieren der Windows-Ereignisweiterleitung](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
