---
# required metadata

title: Ändern der ATA-Konfiguration – Name des Netzwerkadapters für die Erfassung | Microsoft Advanced Threat Analytics
description: Beschreibt, wie der Name des Netzwerkadapters geändert wird, der als Netzwerkadapter für die Erfassung konfiguriert ist, ohne die Verbindung mit dem ATA-Gateway zu beenden.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 3225a81e-0395-43ca-9a48-0cbe7171e5de

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Ändern der ATA-Konfiguration – Name des Netzwerkadapters für die Erfassung

>[!div class="step-by-step"]
[« Domänenverbindungskennwort](modifying-ata-config-dcpassword.md)

## Ändern des Namens des ATA-Gateway-Netzwerkadapters für die Erfassung
Wenn Sie den Namen des Netzwerkadapters ändern, der aktuell als Netzwerkadapter für die Erfassung konfiguriert ist, wird der ATA-Gatewayserver nicht gestartet. Gehen Sie wie folgt vor, um den Namen zu ändern, ohne dass die Verbindung mit dem ATA-Gateway geändert wird:

1.  Heben Sie auf der Seite „ATA-Gatewaykonfiguration“ die Auswahl des Netzwerkadapters auf, den Sie umbenennen möchten, und wählen Sie stattdessen einen anderen Netzwerkadapter für die Erfassung aus. Dabei kann es sich um einen vorläufigen Netzwerkadapter oder auch um den Verwaltungsnetzwerkadapter handeln. In diesem Zeitraum wird der Datenverkehr des Domänencontrollers in ATA nicht mittels Portspiegelung erfasst. Speichern Sie die neue Konfiguration.

2.  Benennen Sie auf dem ATA-Gateway den Netzwerkadapter um. Öffnen Sie dazu die Systemsteuerung, und wählen Sie „Netzwerkverbindungen“ aus.

3.  Wechseln Sie dann wieder zur Seite „ATA-Gatewaykonfiguration“ der ATA-Konsole. Möglicherweise müssen Sie die Seite aktualisieren, damit der Netzwerkadapter mit dem neuen Namen in der Liste angezeigt wird. Heben Sie die Auswahl des in Schritt 1 ausgewählten Adapters auf, und wählen Sie dann den neu benannten Adapter aus. Speichern Sie abschließend die neue Konfiguration.

Wenn Sie den Netzwerkadapter nicht entsprechend den Schritten oben umbenennen, wird das ATA-Gateway nicht gestartet, und auf dem ATA-Gateway wird in der Protokolldatei „Microsoft.Tri.Gateway-Errors.log“ die folgende Fehlermeldung angezeigt. Im Beispiel unten steht **Capture** für den ursprünglichen von Ihnen festgelegten Namen des Netzwerkadapters.

`Error [NetworkListener] Microsoft.Tri.Infrastructure.ExtendedException: Unavailable network adapters [UnavailableCaptureNetworkAdapterNames=Capture]`

Um dieses Problem zu beheben, benennen Sie den Netzwerkadapter wieder in den Namen um, der beim Einrichten von ATA festgelegt war, und ändern Sie den Namen entsprechend den oben beschriebenen Schritten.

>[!div class="step-by-step"]
[« Domänenverbindungskennwort](modifying-ata-config-dcpassword.md)


## Siehe auch
- [Arbeiten mit der ATA-Konsole](/advanced-threat-analytics/understand/working-with-ata-console)
- [Installieren von ATA](install-ata.md)
- [Unterstützung finden Sie in unserem Forum.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


