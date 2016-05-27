---
# required metadata

title: Neuerungen in ATA 1.4 | Microsoft Advanced Threat Analytics
description: Listet Neuerungen sowie bekannte Probleme in ATA 1.4 auf.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: cbea47f9-34c1-42b6-ae9e-6a472b49e1a5

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Neuerungen in ATA 1.4
Die vorliegenden Anmerkungen zu dieser Version enthalten Informationen zu bekannten Problemen in Version 1.4 von Advanced Threat Analytics.

## Neuerungen in dieser Version

-   Unterstützung für die Windows-Ereignisweiterleitung (Windows Event Forwarding, WEF), um Ereignisse direkt von den Domänencontrollern an das ATA-Gateway zu senden.

-   Verbesserungen der Pass-the-Hash-Erkennung für Unternehmensressourcen durch Kombination von DPI (Deep Packet Inspection, ausführliche Paketüberprüfung) und Windows-Ereignisprotokollen.

-   Verbesserungen für die Unterstützung von nicht in eine Domäne eingebundenen Geräten und Nicht-Windows-Geräten in Bezug auf Erkennung und Sichtbarkeit.

-   Leistungsverbesserungen zur Unterstützung einer größeren Menge an Datenverkehr pro ATA-Gateway.

-   Leistungsverbesserungen zur Unterstützung einer größeren Anzahl von ATA-Gateways pro ATA Center.

-   Ein neuer automatischer Namensauflösungsprozess wurde hinzugefügt, der Computernamen und IP-Adressen einander zuordnet. Diese einzigartige Funktion spart kostbare Zeit bei der Untersuchung und liefert belastbare Informationen für Sicherheitsanalysten.

-   Verbesserte Möglichkeit zum Erfassen von Benutzereingaben, um den Erkennungsprozess automatisch zu optimieren.

-   Automatische Erkennung für NAT-Geräte.

-   Automatisches Failover, wenn die Domänencontroller nicht erreichbar sind.

-   Die Überwachung der Systemintegrität und Benachrichtigungen zur Systemintegrität liefern nun den Gesamtintegritätsstatus der Bereitstellung sowie bestimmte Probleme im Zusammenhang mit der Konfiguration und der Konnektivität.

-   Sichtbarkeit der Stand- und Speicherorte von Entitäten.

-   Unterstützung mehrerer Domänen.

-   Unterstützung von Domänen mit einfacher Bezeichnung (Single Label Domains, SLD).

-   Unterstützung des Änderns von IP-Adresse und Zertifikat der ATA-Gateways und von ATA Center.

-   Telemetrie zur Verbesserung der Benutzerfreundlichkeit.

## Bekannte Probleme
In dieser Version bestehen die folgenden bekannten Probleme.

### Software zur Netzwerkerfassung
Auf dem ATA-Gateway ist die einzige unterstützte Software zur Netzwerkerfassung, die Sie installieren können, [Microsoft Netzwerkmonitor 3.4](http://www.microsoft.com/en-us/download/details.aspx?id=4865). Installieren Sie nicht Microsoft Message Analyzer oder eine andere Software zur Netzwerkerfassung. Die Installation anderer Software führt dazu, dass das ATA-Gateway nicht mehr ordnungsgemäß funktioniert.

### Installation über ZIP-Datei
Stellen Sie beim Installieren des ATA-Gateways sicher, dass Sie die Dateien aus der ZIP-Datei in ein lokales Verzeichnis extrahieren und von dort aus installieren. Installieren Sie das ATA-Gateway nicht direkt aus der ZIP-Datei, da andernfalls die Installation fehlschlägt.

### Deinstallieren früherer Versionen von ATA
Wenn Sie eine frühere Version von ATA, eine öffentliche Vorschauversion oder eine private Vorschauversion installiert haben, müssen Sie ATA Center und die ATA-Gateways deinstallieren, bevor Sie diese Version von ATA installieren.

Darüber hinaus müssen Sie die Datenbankdateien und die Protokolldateien löschen. Die Datenbanken aus früheren Versionen von ATA sind nicht kompatibel mit der GA-Version von ATA.

Wenn Sie versuchen, ATA Center oder das ATA-Gateway zu deinstallieren, und die ATA-Installation anstelle der Deinstallation geöffnet wird, müssen Sie den folgenden Registrierungsschlüssel hinzufügen und ATA anschließend erneut deinstallieren.

**ATA Center**

-   HKLM\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center

-   Fügen Sie einen neuen Zeichenfolgenwert mit dem Namen `InstallationPath` und dem Wert `C:\Program Files\Microsoft Advanced Threat Analytics\Center` hinzu. Dies ist der Standardinstallationsordner. Wenn Sie den Installationsordner geändert haben, geben Sie den Pfad ein, in dem ATA installiert ist.

    ![Registrierungs-Editor mit ATA Center-Installationspfad](media/ATA-uninstall-center-bug.jpg)

**ATA-Gateway**

-   HKLM\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Gateway

-   Fügen Sie einen neuen Zeichenfolgenwert mit dem Namen `InstallationPath` und dem Wert `C:\Program Files\Microsoft Advanced Threat Analytics\Gateway` hinzu. Dies ist der Standardinstallationsordner.  Wenn Sie den Installationsordner geändert haben, geben Sie den Pfad ein, in dem ATA installiert ist.

    ![Registrierungs-Editor mit ATA-Gateway-Installationspfad](media/ATA-GW-uninstall-bug.jpg)

Löschen Sie nach dem Deinstallieren den Installationsordner in ATA Center und auf dem ATA-Gateway.  Wenn Sie die Datenbank in einem separaten Ordner installiert haben, löschen Sie den Datenbankordner in ATA Center.

### Integritätswarnung – getrenntes ATA-Gateway
Wenn Sie über mehrere ATA-Gateways verfügen und Warnungen erhalten, dass das ATA-Gateway getrennt ist, funktioniert die automatische Auflösung nur auf einem der Gateways, sodass die übrigen im Status „Offen“ verbleiben. Sie müssen manuell bestätigen, dass das ATA-Gateway in Betrieb ist und der Dienst ausgeführt wird, und die Warnung manuell auflösen.

### KB auf Virtualisierungshost
Installieren Sie KB3047154 nicht auf einem Virtualisierungshost. Dies kann dazu führen, dass die Portspiegelung nicht mehr ordnungsgemäß ausgeführt wird.

## Weitere Informationen

[Aktualisieren von ATA auf Version 1.6 – Migrationshandbuch](ata-update-1.6-migration-guide.md)

[Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)

<!--HONumber=May16_HO3-->


