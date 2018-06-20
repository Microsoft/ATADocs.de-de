---
title: Neuerungen in ATA Version 1.8 | Microsoft-Dokumentation
description: Listet Neuerungen sowie bekannte Probleme in ATA 1.8 auf.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 9/03/2017
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 9592d413-df0e-4cec-8e03-be1ae00ba5dc
ms.reviewer: ''
ms.suite: ems
ms.openlocfilehash: 71e7f723d02b4e86f1799e5a92998363766de7a2
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/07/2017
ms.locfileid: "24019050"
---
# <a name="whats-new-in-ata-version-18"></a>Neuerungen in ATA 1.8

Die neueste Updateversion von ATA kann [aus dem Download Center heruntergeladen](https://www.microsoft.com/download/details.aspx?id=55536) werden. Die Vollversion kann aus dem [Evaluation Center](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics) heruntergeladen werden.

Die vorliegenden Anmerkungen zu dieser Version enthalten Informationen zu Updates, neuen Funktionen, Fehlerbehebungen und bekannten Problemen in dieser Version von Advanced Threat Analytics.



## <a name="new--updated-detections"></a>Neue und aktualisierte Erkennung

- Die Implementierung von ungewöhnlichen Protokollen wurde verbessert, sodass sie jetzt auch WannaCry-Schadprogramm erkennen kann.

- NEU! **Ungewöhnliche Modifizierungen von sensiblen Gruppen**: Im Rahmen der Rechteausweitungsphase modifizieren Angreifer Gruppen mit hohen Berechtigungen, um Zugriff auf sensible Ressourcen zu erhalten. ATA erkennt jetzt, wenn ungewöhnliche Änderungen in Gruppen mit erhöhten Berechtigungen vorgenommen werden.
- NEU! **Verdächtige fehlgeschlagene Authentifizierungen** (Brute Force-Verhalten): Angreifer wenden „rohe Gewalt“ bei der Anmeldung an, um Konten zu kompromittieren. ATA gibt jetzt eine Warnung aus, wenn es ungewöhnliche fehlgeschlagene Authentifizierungen erkennt.   

- **Versuchte Remoteausführung – WMI-Ausführung**: Angreifer können versuchen, die Kontrolle über Ihr Netzwerk zu erlangen, indem sie Code remote auf Ihrem Domänencontroller ausführen. Die Erkennung von remoten Ausführungsversuchen wurde in ATA verbessert, sodass es jetzt auch WMI-Methoden erkennt, die Code remote ausführen können.

- Reconnaissance mit Verzeichnisdienstabfragen: Diese Erkennung wurde verbessert, sodass Sie jetzt auch Abfragen einer einzelnen sensiblen Entität erfassen kann. Zudem wird durch diese Verbesserung die Zahl der falsch positiven Ergebnisse gesenkt, die in der vorherigen Version generiert wurden. Wenn Sie dies in Version 1.7 deaktiviert haben, wird dies durch die Installation von Version 1.8 automatisch aktiviert.

- Kerberos Golden Ticket-Aktivität: ATA 1.8 enthält eine zusätzliche Technik, um Golden Ticket-Attacken zu erkennen.
    - ATA erkennt jetzt verdächtige Aktivitäten, in denen die Lebensdauer des Golden Ticket abgelaufen ist. Wenn ein Kerberos-Ticket länger als die erlaubte Lebensdauer verwendet wird, erkennt ATA dies als verdächtige Aktivität, bei der ein Golden Ticket mit hoher Wahrscheinlichkeit erstellt wurde.
- Folgende Erkennungen wurden verbessert, um bekannte falsch positive Ergebnisse zu entfernen:  
    - Rechteausweitungserkennung (gefälschte PAC-Datei) 
    - Aktivität zur Herabstufung der Verschlüsselung (Skeleton Key)
    - Ungewöhnliche Protokollimplementierung
    - einer fehlerhaften Vertrauensstellung

## <a name="improved-triage-of-suspicious-activities"></a>Verbesserte Selektierung von verdächtigen Aktivitäten

-   NEU! Mit ATA 1.8 können Sie die folgenden Aktionen für verdächtige Aktivitäten während des Selektierungsprozesses ausführen: 
    - **Ausschluss von Entitäten**: Sie können Entitäten ausschließen, die keine weiteren verdächtigen Aktivitäten verursachen sollen, damit ATA keine Warnungen mehr ausgibt, wenn es gutartige richtig positive Aktivitäten erkennt (wie z.B. ein Administrator, der remoten Code ausführt oder das Erkennen von Sicherheitsscannern).
    - **Unterdrücken des Warnens vor wiederholten** verdächtigen Aktivitäten.
    - **Löschen verdächtiger Aktivitäten** auf der Angriffszeitachse
-   Der Prozess des Nachverfolgens von Warnungen zu verdächtiger Aktivität ist jetzt effizienter. Die Zeitachse für verdächtige Aktivitäten wurde umgestaltet. In ATA 1.8 können Sie sich deutlich mehr verdächtige Aktivitäten auf einem Bildschirm anschauen. Diese enthalten ausführlichere Informationen zwecks Selektierung und Untersuchung. 

## <a name="new-reports-to-help-you-investigate"></a>Neue Berichte, um Sie bei der Untersuchung zu unterstützen 
-   NEU! Der **Zusammenfassungsbericht** wurde hinzugefügt, damit Sie sich alle zusammengefassten Daten von ATA anschauen können, einschließlich verdächtiger Aktivitäten, Integritätsproblemen usw. Sie können sogar einen benutzerdefinierten Bericht definieren, der automatisch periodisch neu erstellt wird.
-   NEU! Der **Bericht zu sensiblen Gruppen** wurde hinzugefügt, damit Sie sich alle Änderungen an sensiblen Gruppen über einen bestimmten Zeitraum anschauen können.


## <a name="infrastructure-improvements"></a>Verbesserungen der Infrastruktur

-   Die Leistung von ATA Center wurde verbessert. In ATA 1.8 kann ATA Center per als 1 Mio. Pakete in der Sekunde behandeln.
-   Das ATA-Lightweight-Gateway kann jetzt Ereignisse lokal lesen, ohne die Ereignisweiterleitung zu konfigurieren.
-   Sie können jetzt E-Mails für Überwachungsbenachrichtigungen und verdächtige Aktivitäten getrennt konfigurieren.

## <a name="security-improvements"></a>Sicherheitsverbesserungen

-   NEU! **Einmalige Anmeldung für die Verwaltung von ATA** ATA unterstützt die in die Windows-Authentifizierung integrierte einmalige Anmeldung: wenn Sie sich schon bei Ihrem Computer angemeldet haben, verwenden ATA das Token, um Sie in der ATA-Konsole anzumelden. Sie können sich auch mit einer Smartcard anmelden. Stille Installationsskripts für das ATA-Gateway und das ATA-Lightweight-Gateway verwenden jetzt den Kontext des angemeldeten Benutzers, ohne Anmeldeinformationen eingeben zu müssen.
-   Berechtigungen für das lokale System wurden aus dem ATA-Gatewayprozess entfernt, damit Sie virtuelle Konten (nur in eigenständigen ATA-Gateways verfügbar), verwaltete Dienstkonten und gruppenverwaltete Dienstkonten verwenden können, um den ATA-Gatewayprozess auszuführen.   
-   Überwachungsprotokolle für ATA Center und Gateways wurden hinzugefügt, und alle Aktionen werden jetzt im Windows-Ereignisprotokoll erfasst.
-   Die Unterstützung für KSP-Zertifikate für ATA Center wurde hinzugefügt.

## <a name="additional-changes"></a>Weitere Änderungen

- Die Option zum Hinzufügen von Notizen wurde aus „Verdächtige Aktivitäten“ entfernt.
- Empfehlungen zur Abwehr verdächtiger Aktivitäten wurden aus der Zeitachse für verdächtige Aktivitäten entfernt.
- Ab ATA Version 1.8 verwalten die ATA-Gateways und Lightweight-Gateways ihre eigenen Zertifikate, sodass keine Administratorinteraktion für die Verwaltung nötig ist.

## <a name="known-issues"></a>Bekannte Probleme

> [!WARNING]
> Um diese bekannten Probleme zu verhindern, führen Sie ein Update oder eine Bereitstellung mit 1.8 Update 1 durch.

### <a name="ata-gateway-on-windows-server-core"></a>ATA-Gateway in Windows Server Core

**Symptome**: Das Aktualisieren eines ATA-Gateway auf 1.8 in Windows Server 2012 R2 Core mit .Net Framework 4.7 schlägt möglicherweise mit dem Fehler: *Microsoft Advanced Threat Analytics Gateway has stopped working* (Microsoft Advanced Threat Analytics-Gateway wird nicht mehr ausgeführt) fehl. 

![Fehler von Gateway Core](./media/gateway-core-error.png)

In Windows Server 2016 Core sehen Sie den Fehler möglicherweise nicht, aber der Vorgang schlägt fehl, wenn Sie versuchen, eine Installation durchzuführen, und die Ereignisse 1000 und 1001 (Prozessabsturz) werden im Anwendungsereignisprotokoll auf dem Server protokolliert.

**Beschreibung**: Es liegt ein Problem mit .NET Framework 4.7 vor, sodass Anwendungen, die WPF-Technologie (z.B. ATA) verwenden, beim Laden fehlschlagen. Weitere Informationen finden Sie unter [KB 4034015](https://support.microsoft.com/help/4034015/wpf-window-can-t-be-loaded-after-you-install-the-net-framework-4-7-on). 

**Problemumgehung**: Deinstallieren Sie .NET 4.7 ([KB 3186497](https://support.microsoft.com/help/3186497/the-net-framework-4-7-offline-installer-for-windows)), um die .NET Version zu .NET 4.6.2 wiederherzustellen, und aktualisieren Sie anschließend das ATA-Gateway auf Version 1.8. Nach dem Upgrade von ATA können Sie .NET 4.7 neu installieren.  Es wird ein Update zur Behebung dieses Problems in einer zukünftigen Version vorhanden sein.

### <a name="lightweight-gateway-event-log-permissions"></a>Berechtigungen für das Ereignisprotokoll des Lightweight-Gateway

**Symptome**: Beim Aktualisieren von ATA auf Version 1.8 können Apps oder Dienste, die vorher erteilte Zugriffsberechtigungen für das Sicherheitsereignisprotokoll hatten, die Berechtigungen verlieren. 

**Beschreibung**: Um das Bereitstellen von ATA zu erleichtern, greift ATA 1.8 direkt auf Ihr Sicherheitsereignisprotokoll zu, ohne die Konfiguration der Windows-Ereignisweiterleitung zu benötigen. Zur gleichen Zeit wird ATA als lokaler Dienst mit geringen Berechtigungen ausgeführt, um eine höhere Sicherheit zu gewährleisten. Der ATA-Dienst erteilt sich selbst Berechtigungen für das Sicherheitsereignisprotokoll, damit ATA die Ereignisse lesen kann. In diesem Fall können bereits erteilte Berechtigungen für andere Dienste deaktiviert werden.

**Problemumgehung**: Führen Sie das folgende Windows PowerShell-Skript aus. Dies entfernt die falsch hinzugefügten Berechtigungen in der Registrierung von ATA und fügt sie über eine andere API hinzu. Dies kann Berechtigungen für andere Apps wiederherstellen. Wenn dies nicht der Fall ist, müssen sie manuell wiederhergestellt werden. Es wird ein Update zur Behebung dieses Problems in einer zukünftigen Version vorhanden sein. 

       $ATADaclEntry = "(A;;0x1;;;S-1-5-80-1717699148-1527177629-2874996750-2971184233-2178472682)"
        try {
        $SecurityDescriptor = Get-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\Eventlog\Security -Name CustomSD
        $ATASddl = "O:BAG:SYD:" + $ATADaclEntry 
        if($SecurityDescriptor.CustomSD -eq $ATASddl) {
        Remove-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\Eventlog\Security -Name CustomSD
        }
    }
    catch
    {
    # registry key does not exist
    }

    $EventLogConfiguration = New-Object -TypeName System.Diagnostics.Eventing.Reader.EventLogConfiguration("Security")
    $EventLogConfiguration.SecurityDescriptor = $EventLogConfiguration.SecurityDescriptor + $ATADaclEntry

### <a name="proxy-interference"></a>Störungen des Proxy

**Symptome**: Nach dem Upgrade auf ATA 1.8 kann der ATA-Gatewaydienst möglicherweise nicht gestartet werden. Im ATA-Fehlerprotokoll wird möglicherweise die folgende Ausnahme angezeigt: *System.Net.Http.HttpRequestException: Fehler beim Senden der Anforderung.---> System.NET.WebException: Der Remoteserver hat einen Fehler zurückgegeben: (407) Proxyauthentifizierung erforderlich.*

**Beschreibung**: Ab ATA 1.8 kommuniziert das ATA-Gateway mit ATA Center über das HTTP-Protokoll. Wenn der Computer, auf dem Sie das ATA-Gateway installiert haben, einen Proxyserver für die Verbindung mit ATA Center verwendet, kann dies die Kommunikation unterbrechen. 

**Problemumgehung**: Deaktivieren Sie die Verwendung des Proxyservers auf dem Dienstkonto des ATA-Gateways. Es wird ein Update zur Behebung dieses Problems in einer zukünftigen Version vorhanden sein.

### <a name="report-settings-reset"></a>Zurücksetzen der Berichtseinstellungen

**Symptome**: Alle Einstellungen, die an den geplanten Berichten vorgenommen wurden, werden gelöscht, wenn Sie auf Version 1.8 Update 1 aktualisieren.

**Beschreibung**: Das Aktualisieren von Version 1.8 Update 1 von Version 1.8 setzt die Einstellungen für geplante Berichte zurück.

**Problemumgehung**: Bevor Sie auf Version 1.8 Update 1 aktualisieren, erstellen Sie eine Kopie der Berichtseinstellungen, und geben Sie diese erneut ein. Dies kann auch über ein Skript erfolgen. Weitere Informationen dazu finden Sie unter [Exportieren und Importieren der Advanced Threat Analytics-Konfiguration](ata-configuration-file.md).


## <a name="see-also"></a>Siehe auch
[Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Aktualisieren von ATA auf Version 1.8: Migrationshandbuch](ata-update-1.8-migration-guide.md)

