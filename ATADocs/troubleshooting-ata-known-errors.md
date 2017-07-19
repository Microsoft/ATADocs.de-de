---
title: Behandlung von bekannten Problemen bei ATA | Microsoft-Dokumentation
description: "Beschreibt, wie sie bekannte Probleme in Advanced Threat Analytics (ATA) behandeln können"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/3/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 0ded0dd064f0327f6e52f15081e2b9dce14f982b
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
*Gilt für: Advanced Threat Analytics Version 1.8*



# <a name="troubleshooting-ata-known-issues"></a>Behandlung von bekannten Problemen bei ATA

In diesem Abschnitt sind mögliche Fehler, die es in den Bereitstellungen von ATA geben kann, und die Schritte zu deren Behebung aufgeführt.

## <a name="ata-gateway-and-lightweight-gateway-errors"></a>Fehler im ATA-Gateway und Lightweight-Gateway

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
|System.IO.IOException: Fehler bei der Authentifizierung, da die Gegenseite den Transportstream geschlossen hat.|TLS 1.0 ist auf dem ATA-Gateway deaktiviert, .NET ist aber für die Verwendung von TLS 1.2 eingerichtet.|Verwenden Sie eine der folgenden Optionen: </br> TLS 1.0 auf dem ATA-Gateway aktivieren </br>Aktivieren Sie TLS 1.2 in .NET, indem Sie die Registrierungsschlüssel wie folgt für die Verwendung der Standardwerte des Betriebssystems für LLS und TLS einrichten: `[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001` </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`|
|System.TypeLoadException: Could not load type 'Microsoft.Opn.Runtime.Values.BinaryValueBufferManager' from assembly 'Microsoft.Opn.Runtime, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' (System.TypeLoadException: Der Typ „Microsoft.Opn.Runtime.Values.BinaryValueBufferManager“ konnte nicht aus der Assembly „Microsoft.Opn.Runtime, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35“ geladen werden.)|Das ATA-Gateway konnte erforderliche Analysedateien nicht laden.|Überprüfen Sie, ob die Microsoft-Nachrichtenanalyse aktuell installiert ist. Die Nachrichtenanalyse wird nicht für die Installation mit dem ATA-Gateway bzw. Lightweight-Gateway unterstützt. Deinstallieren Sie die Nachrichtenanalyse und starten Sie den Gatewaydienst neu.|
|Die Warnung, dass Netzwerkdatenverkehr aus der Portspiegelung gelöscht wurde, wird ausgegeben, wenn ein Lightweight-Gateway auf VMware verwendet wird.|Wenn Sie Domänencontroller auf virtuellen VMware-Computern verwenden, wird möglicherweise die Warnung **Netzwerkdatenverkehr aus Portspiegelung gelöscht** ausgegeben. Dies kann aufgrund von Konfigurationskonflikten in VMware auftreten. |Um zu vermeiden, dass diese Warnung ausgegeben wird, können Sie überprüfen, ob die folgenden Einstellungen auf „0“ oder „deaktiviert“ festgelegt sind: TsoEnable, LargeSendOffload, IPv4, TSO Offload. Deaktivieren Sie ebenso IPv4 Giant TSO Offload. Weitere Informationen finden Sie in der VMware-Dokumentation.|


## <a name="deployment-errors"></a>Bereitstellungsfehler
|Fehler|Beschreibung|Lösung|
|-------------|----------|---------|
|Fehler bei der Installation von .NET Framework 4.6.1. Fehlernummer ist 0x800713ec.|Die erforderlichen Komponenten für .NET Framework 4.6.1 sind nicht auf dem Server installiert. |Stellen Sie vor der Installation von ATA sicher, dass die Windows-Updates [KB2919442](https://www.microsoft.com/download/details.aspx?id=42135) und [KB2919355](https://support.microsoft.com/kb/2919355) auf dem Server installiert sind.|
|System.Threading.Tasks.TaskCanceledException: A task was canceled (System.Threading.Tasks.TaskCanceledException: Eine Aufgabe wurde abgebrochen)|Zeitüberschreitung während des Bereitstellungsvorgangs, da ATA Center nicht erreicht werden konnte.|1.    Überprüfen Sie Ihre Netzwerkverbindung zu ATA Center, indem Sie mithilfe der IP-Adresse dahin navigieren. <br></br>2.    Überprüfen Sie die Proxy- oder Firewallkonfiguration.|
|System.Net.Http.HttpRequestException: An error occurred while sending the request. (System.Net.Http.HttpRequestException: Fehler beim Senden der Anfrage.) ---> System.Net.WebException: Der Remoteserver hat einen Fehler ausgegeben: (407) Proxyauthentifizierung erforderlich.|Zeitüberschreitung während des Bereitstellungsvorgangs, da ATA Center aufgrund einer Proxyfehlkonfiguration nicht erreicht werden konnte.|Deaktivieren Sie die Proxykonfiguration vor der Bereitstellung, aktivieren Sie dann die Proxykonfiguration erneut. Alternativ können Sie eine Ausnahme im Proxy konfigurieren.|
|Es wurde kein Datenverkehr vom Domänencontroller empfangen, doch es wurden Überwachungswarnungen beobachtet.|    Es wurde kein Datenverkehr von einem Domänencontroller empfangen, der Portspiegelung über ein ATA-Gateway verwendet.|Deaktivieren Sie diese Funktionen auf dem verwendeten NIC auf dem ATA-Gateway unter **Erweiterte Einstellungen**:<br></br>Empfang zusammengeführter Segmente (IPv4)<br></br>Empfang zusammengeführter Segmente (IPv6)|





## <a name="see-also"></a>Siehe auch
- [Voraussetzungen für ATA](ata-prerequisites.md)
- [ATA-Kapazitätsplanung](ata-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-collection.md#configuring-windows-event-forwarding)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
