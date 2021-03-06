---
title: Behandlung von bekannten Problemen bei ATA | Microsoft-Dokumentation
description: Beschreibt, wie sie bekannte Probleme in Advanced Threat Analytics (ATA) behandeln können
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 01/12/2021
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: b49e2b10713f23c4256a7236bfa7162189c6e43b
ms.sourcegitcommit: 373151a0e86e4933c5cb7c8f17c4d386356c98dd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/12/2021
ms.locfileid: "98114968"
---
# <a name="troubleshooting-ata-known-issues"></a>Behandlung von bekannten Problemen bei ATA

[!INCLUDE [Banner for top of topics](includes/banner.md)]

In diesem Abschnitt sind mögliche Fehler, die es in den Bereitstellungen von ATA geben kann, und die Schritte zu deren Behebung aufgeführt.

## <a name="ata-gateway-and-lightweight-gateway-errors"></a>Fehler im ATA-Gateway und Lightweight-Gateway

> [!div class="mx-tableFixed"]
>
> |Fehler|BESCHREIBUNG|Lösung|
> |-------------|----------|---------|
> |System.DirectoryServices.Protocols.LdapException: Lokaler Fehler.|Die ATA-Gateway konnte sich nicht beim Domänencontroller authentifizieren.|1. Vergewissern Sie sich, dass der DNS-Datensatz des Domänen Controllers ordnungsgemäß auf dem DNS-Server konfiguriert ist. <br>2. Überprüfen Sie, ob die Zeit des ATA-Gateways mit der Zeit des Domänen Controllers synchronisiert ist.|
> |System.IdentityModel.Tokens.SecurityTokenValidationException: Die Zertifikatkette kann nicht überprüft werden.|Das ATA-Gateway konnte das Zertifikat von ATA Center nicht überprüfen.|1. Überprüfen Sie, ob das Zertifikat der Stamm Zertifizierungsstelle im Zertifikat Speicher der vertrauenswürdigen Zertifizierungsstelle auf dem ATA-Gateway installiert ist.<br>2. Überprüfen Sie, ob die Zertifikat Sperr Liste verfügbar ist und dass die Zertifikats Sperr Überprüfung ausgeführt werden kann.|
> |Microsoft.Common.ExtendedException: Erstellungszeit konnte nicht analysiert werden.|Das ATA-Gateway konnte Syslog-Meldungen, die vom SIEM weitergeleitet wurden, nicht analysieren.|Stellen Sie sicher, dass das SIEM so konfiguriert ist, dass es die Meldungen in einem der Formate weiterleitet, die von ATA unterstützt werden.|
> |System.ServiceModel.FaultException: Fehler beim Überprüfen der Sicherheit für die Nachricht.|Die ATA-Gateway konnte sich nicht bei ATA Center authentifizieren.|Vergewissern Sie sich, dass die Zeit des ATA-Gateways mit der Zeit von ATA-Center synchronisiert ist.|
> |System.ServiceModel.EndpointNotFoundException: Es konnte keine Verbindung mit net.tcp://center.ip.addr:443/IEntityReceiver hergestellt werden.|Das ATA-Gateway konnte keine Verbindung mit ATA Center herstellen.|Vergewissern Sie sich, dass die Netzwerkeinstellungen richtig sind und dass die Verbindung zwischen dem ATA-Gateway und ATA Center aktiv ist.|
> |System.DirectoryServices.Protocols.LdapException: Der LDAP-Server ist nicht verfügbar.|Das ATA-Gateway konnte den Domänencontroller nicht über das LDAP-Protokoll abfragen.|1. Überprüfen Sie, ob das Benutzerkonto, das von ATA verwendet wird, um eine Verbindung mit der Active Directory Domäne herzustellen, Lesezugriff auf alle Objekte in der Active Directory Struktur hat.<br>2. Stellen Sie sicher, dass der Domänen Controller nicht festgeschrieben wurde, um LDAP-Abfragen für das von ATA verwendete Benutzerkonto zu verhindern.|
> |Microsoft.Tri.Infrastructure.ContractException: Vertragsausnahme|Die ATA-Gateway konnte die Konfiguration von ATA Center nicht synchronisieren.|Schließen Sie die Konfiguration des ATA-Gateways in der ATA-Konsole ab.|
> |System.Reflection.ReflectionTypeLoadException: Mindestens ein angeforderter Typ kann nicht geladen werden. Weitere Informationen erhalten Sie durch Abrufen der LoaderExceptions-Eigenschaft.|Auf dem ATA-Gateway ist die Nachrichtenanalyse installiert.| Deinstallieren Sie die Nachrichtenanalyse.|
> |Fehler [Layout] System.OutOfMemoryException: Ausnahme vom Typ „System.OutOfMemoryException“ ausgelöst.|Auf dem ATA-Gateway ist nicht genügend Arbeitsspeicher verfügbar.|Erhöhen Sie die Arbeitsspeicherkapazität auf dem Domänencontroller.|
> |Fehler beim Start von Live-Consumer  ---> Microsoft.Opn.Runtime.Monitoring.MessageSessionException: Der PEFNDIS-Ereignisanbieter ist nicht bereit.|PEF (Nachrichtenanalyse) wurde nicht ordnungsgemäß installiert.|Wenn Sie Hyper-V verwenden, versuchen Sie, die Hyper-V-Integrationsdienste zu aktualisieren. Kontaktieren Sie alternativ den Support für eine Problemumgehung.|
> |Installationsfehler: 0x80070652|Auf Ihrem Computer stehen weitere Installationen aus.|Warten Sie, bis die anderen Installationen abgeschlossen sind, und starten Sie den Computer gegebenenfalls neu.|
> |System.InvalidOperationException: Die Instanz „Microsoft.Tri.Gateway“ existiert nicht in der angegebenen Kategorie.|Die PIDs wurden für Prozessnamen im ATA-Gateway aktiviert.|Weitere Informationen finden Sie unter [behandeln doppelter Instanznamen](/windows/win32/perfctrs/handling-duplicate-instance-names) zum Deaktivieren von PIDs in Prozessnamen|
> System. InvalidOperationException: die Kategorie ist nicht vorhanden.|Möglicherweise wurden die Leistungsindikatoren in der Registrierung deaktiviert.|Verwenden Sie [KB2554336](https://support.microsoft.com/kb/2554336), um die Leistungsindikatoren neu zu erstellen.|
> |System.ApplicationException: Die ETW-Sitzung „MMA-ETW-Livecapture-a4f595bd-f567-49a7-b963-20fa4e370329“ kann nicht gestartet werden.|In der HOSTS-Datei existiert ein Hosteintrag, der auf den Kurznamen des Computers verweist.|Entfernen Sie den Hosteintrag aus „C:\Windows\System32\drivers\etc\HOSTS“, oder ändern Sie ihn in einen eindeutigen Domänennamen um.|
> |System. IO. IOException: bei der Authentifizierung ist ein Fehler aufgetreten, da die Remote Seite den Transportstream geschlossen hat oder keinen sicheren SSL/TLS-Kanal erstellen konnte.|TLS 1.0 ist auf dem ATA-Gateway deaktiviert, .NET ist aber für die Verwendung von TLS 1.2 eingerichtet.|Aktivieren Sie TLS 1,2 für .net, indem Sie die Registrierungsschlüssel wie folgt so festlegen, dass die Betriebssystem Standardwerte für SSL und TLS verwendet werden:<br></br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`</br> `[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`</br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SchUseStrongCrypto"=dword:00000001` </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] " SchUseStrongCrypto"=dword:00000001`|
> |System.TypeLoadException: Could not load type 'Microsoft.Opn.Runtime.Values.BinaryValueBufferManager' from assembly 'Microsoft.Opn.Runtime, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' (System.TypeLoadException: Der Typ „Microsoft.Opn.Runtime.Values.BinaryValueBufferManager“ konnte nicht aus der Assembly „Microsoft.Opn.Runtime, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35“ geladen werden.)|Das ATA-Gateway konnte erforderliche Analysedateien nicht laden.|Überprüfen Sie, ob die Microsoft-Nachrichtenanalyse aktuell installiert ist. Die Nachrichtenanalyse wird nicht für die Installation mit dem ATA-Gateway bzw. Lightweight-Gateway unterstützt. Deinstallieren Sie die Nachrichtenanalyse und starten Sie den Gatewaydienst neu.|
> |System.Net.WebException: Der Remoteserver hat einen Fehler ausgegeben: (407) Proxyauthentifizierung erforderlich|Die Kommunikation des ATA-Gateways mit dem ATA Center wurde durch einen Proxyserver unterbrochen.|Deaktivieren Sie den Proxy auf dem Computer des ATA-Gateways. <br></br>Beachten Sie, dass Proxyeinstellungen pro Konto gelten können.|
> |System.IO.DirectoryNotFoundException: Das System kann den angegebenen Pfad nicht finden. (Ausnahme von HRESULT: 0x80070003)|Mindestens einer der erforderlichen Dienste zur Ausführung von ATA konnte nicht gestartet werden.|Starten Sie die folgenden Dienste: <br></br>Leistungsprotokolle und -warnungen (PLA), Taskplaner (Zeitplan).|
> |System.Net.WebException: The remote server returned an error: (403) Forbidden (System.Net.WebException: Der Remoteserver hat einen Fehler zurückgegeben: (403) Verboten)|Das ATA-Gateway oder das Lightweight-Gateway konnte keine HTTP-Verbindung herstellen, da ATA Center nicht vertrauenswürdig ist.|Fügen Sie den NetBIOS-Namen und den FQDN von ATA Center der Liste vertrauenswürdiger Websites hinzu, und löschen Sie den Cache in Internet Explorer (oder den Namen von ATA Center, wie in der Konfiguration angegeben, wenn sich der konfigurierte von NetBIOS/FQDN unterscheidet).|
> |System.Net.Http.HttpRequestException: PostAsync fehlerhaft [requestTypeName=StopNetEventSessionRequest]|ATA Gateway oder ATA Lightweight Gateway kann aufgrund eines WMI-Problems nicht die ETW-Sitzung, die Netzwerkdatenverkehr erfasst, beenden und starten.|Befolgen Sie die Anweisungen unter [WMI: Neuerstellen des WMI-Repositorys](https://blogs.technet.microsoft.com/askperf/2009/04/13/wmi-rebuilding-the-wmi-repository/), um das WMI-Problem zu beheben.|
> |System.Net.Sockets.SocketException: Es wurde versucht, über durch die Zugriffsberechtigungen verbotene Wege auf einen Socket zuzugreifen.|Eine andere Anwendung verwendet Port 514 auf dem ATA-Gateway.|Verwenden Sie `netstat -o`, um festzulegen, durch welchen Vorgang der Port benutzt werden soll.|

## <a name="deployment-errors"></a>Bereitstellungsfehler

> [!div class="mx-tableFixed"]
>
> |Fehler|BESCHREIBUNG|Lösung|
> |-------------|----------|---------|
> |Fehler bei der Installation von .NET Framework 4.6.1. Fehlernummer ist 0x800713ec.|Die erforderlichen Komponenten für .NET Framework 4.6.1 sind nicht auf dem Server installiert. |Stellen Sie vor der Installation von ATA sicher, dass die Windows-Updates [KB2919442](https://www.microsoft.com/download/details.aspx?id=42135) und [KB2919355](https://support.microsoft.com/kb/2919355) auf dem Server installiert sind.|
> |System.Threading.Tasks.TaskCanceledException: A task was canceled (System.Threading.Tasks.TaskCanceledException: Eine Aufgabe wurde abgebrochen)|Zeitüberschreitung während des Bereitstellungsvorgangs, da ATA Center nicht erreicht werden konnte.|1. Überprüfen Sie die Netzwerk Konnektivität mit ATA Center, indem Sie die zugehörige IP-Adresse verwenden. <br></br>2. Überprüfen Sie die Proxy-oder Firewallkonfiguration.|
> |System.Net.Http.HttpRequestException: Fehler beim Senden der Anforderung. ---> System.Net.WebException: Der Remoteserver hat einen Fehler ausgegeben: (407) Proxyauthentifizierung erforderlich.|Zeitüberschreitung während des Bereitstellungsvorgangs, da ATA Center aufgrund einer Proxyfehlkonfiguration nicht erreicht werden konnte.|Deaktivieren Sie die Proxykonfiguration vor der Bereitstellung, aktivieren Sie dann die Proxykonfiguration erneut. Alternativ können Sie eine Ausnahme im Proxy konfigurieren.|
> |System.Net.Sockets.SocketException: Eine vorhandene Verbindung wurde vom Remotehost geschlossen.||Aktivieren Sie TLS 1,2 für .net, indem Sie die Registrierungsschlüssel wie folgt so festlegen, dass die Betriebssystem Standardwerte für SSL und TLS verwendet werden:<br></br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`</br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`</br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SchUseStrongCrypto"=dword:00000001` </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] "SchUseStrongCrypto"=dword:00000001`|
> |Fehler [ \\ [] deploymentmodel [ \\ ]] Fehler bei der Verwaltungs Authentifizierung [ \\ [] currentlyloggedonuser = <domain> \\ <username> Status = failedauthentication Exception = [ \\ ]]|Der Bereitstellungsprozess für das ATA-Gateway oder das ATA-Lightweight-Gateway konnte in ATA Center nicht erfolgreich authentifiziert werden.|Öffnen Sie auf dem Computer, auf dem der fehlerhafte Bereitstellungsprozess ausgeführt wurde, einen Browser, und versuchen Sie, die ATA-Konsole zu erreichen. </br>Wenn dies nicht möglich ist, starten Sie die Problembehandlung, um zu ermitteln, warum der Browser sich nicht in ATA Center authentifizieren kann. </br>Überprüfen Sie Folgendes: </br>Proxykonfiguration</br>Netzwerkprobleme</br>Gruppenrichtlinieneinstellungen für die Authentifizierung auf diesem Computer, die sich von den Einstellungen in ATA Center unterscheiden|
> | Error [\\[]DeploymentModel[\\]] Failed management authentication (Fehler bei der Verwaltungsauthentifizierung)|Fehler bei der Validierung des Center-Zertifikats|Das Zertifikat für ATA Center erfordert möglicherweise für die Überprüfung eine Internetverbindung. Stellen Sie sicher, dass Ihr Gatewaydienst über die ordnungsgemäße Proxykonfiguration verfügt, um die Verbindung und Überprüfung zu ermöglichen.|
> | Beim Bereitstellen des Centers und Auswählen eines Zertifikats wird der Fehler "nicht unterstützt" gemeldet.|Dies kann der Fall sein, wenn entweder das ausgewählte Zertifikat nicht den Anforderungen entspricht oder der private Schlüssel des Zertifikats nicht zugänglich ist.|Stellen Sie sicher, dass Sie die Bereitstellung mit erhöhten Rechten (**als Administrator ausführen**) ausführen und dass das ausgewählte Zertifikat die [Anforderungen](ata-prerequisites.md#certificates)erfüllt.|

## <a name="ata-center-errors"></a>ATA Center-Fehler

> [!div class="mx-tableFixed"]
>
> |Fehler|BESCHREIBUNG|Lösung|
> |-------------|----------|---------|
> |System.Security.Cryptography.CryptographicException: Zugriff verweigert.|ATA Center konnte das ausgestellte Zertifikat nicht für die Entschlüsselung verwenden. Dies liegt höchstwahrscheinlich daran, dass ein Zertifikat verwendet wurde, dessen KeySpec- bzw. KeyNumber-Wert auf „Signature“ (AT\\_SIGNATURE) festgelegt wurde, statt KeyExchange (AT\\_KEYEXCHANGE) zu verwenden. Dies wird für die Entschlüsselung nicht unterstützt.|1. stoppt den ATA Center-Dienst. <br></br>2. löschen Sie das ATA Center-Zertifikat aus dem Zertifikat Speicher des Centers. (Stellen Sie vor dem Löschen sicher, dass Sie das Zertifikat mit dem privaten Schlüssel in einer PFX-Datei gesichert haben.) <br></br>3. Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, und führen Sie certutil-importpfx "centercertificate. pfx" unter \\ _KEYEXCHANGE <br></br>4. Starten Sie den ATA Center-Dienst. <br></br>5. Überprüfen Sie, ob alles jetzt erwartungsgemäß funktioniert.|

## <a name="ata-gateway-and-lightweight-gateway-issues"></a>Probleme im ATA-Gateway und Lightweight-Gateway

> [!div class="mx-tableFixed"]
>
> |Problem|BESCHREIBUNG|Lösung|
> |-------------|----------|---------|
> |Es wurde kein Datenverkehr vom Domänen Controller empfangen, aber es werden Integritäts Warnungen beobachtet.|Es wurde kein Datenverkehr von einem Domänencontroller empfangen, der Portspiegelung über ein ATA-Gateway verwendet.|Deaktivieren Sie diese Funktionen auf der ATA-Gateway-Erfassungs-NIC unter **Erweiterte Einstellungen**:<br></br>Empfang zusammengeführter Segmente (IPv4)<br></br>Empfang zusammengeführter Segmente (IPv6)|
> |Diese Integritäts Warnung wird angezeigt: ein Teil des Netzwerk Datenverkehrs wird nicht analysiert.|Wenn Sie über ein ATA-Gateway oder ein Lightweight-Gateway auf virtuellen VMware-Computern verfügen, erhalten Sie möglicherweise die folgende Integritäts Warnung. Dies tritt aufgrund von Konfigurationskonflikten in VMware auf.|Legen Sie die folgenden Einstellungen in der NIC-Konfiguration der VM auf 0 (null) oder Deaktiviert fest: TsoEnable, LargeSendOffload, TSO Offload, Giant TSO Offload|

## <a name="multi-processor-group-mode"></a>Modus „Mehrere Prozessorgruppen“

Für Windows-Betriebssysteme 2008R2 und 2012 wird das ATA-Gateway im Modus für **mehrere Prozessor Gruppen** nicht unterstützt.

Mögliche Problemumgehungen:

- Wenn Hyperthreading aktiviert ist, schalten Sie es aus. Dadurch kann die Anzahl logischer Kerne möglicherweise weit genug reduziert werden, sodass eine Ausführung im Modus **Mehrere Prozessorgruppen** nicht notwendig ist.

- Wenn Ihr Computer weniger als 64 logische Kerne aufweist und auf einem HP-Host ausgeführt wird, können Sie möglicherweise die BIOS-Einstellung **NUMA Group Size Optimization** vom Standardwert **Clustered** in **Flat** ändern.

## <a name="see-also"></a>Weitere Informationen

- [ATA-Voraussetzungen](ata-prerequisites.md)
- [ATA-Kapazitätsplanung](ata-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-collection.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
