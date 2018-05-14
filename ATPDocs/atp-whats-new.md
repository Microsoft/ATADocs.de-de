---
title: Neuerungen in Azure ATP | Microsoft-Dokumentation
description: Beschreibt die neuesten Releases von Azure ATP und enthält Informationen zu den Neuerungen in den einzelnen Version.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/8/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 7d0f33db-2513-4146-a395-290e001f4199
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6d794e2d30b51d78bd3e4af76d8bd4a48b2d413f
ms.sourcegitcommit: 8472f3f46fc90da7471cd1065cdb2f6a1d5a9f69
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/08/2018
---
*Gilt für: Azure Advanced Threat Protection*


# <a name="whats-new-in-azure-atp"></a>Neuerungen in Azure ATP 



## <a name="azure-atp-release-231"></a>Azure ATP Release 2.31

Veröffentlicht: 6.Mai 2018
 
- Verbesserungen wurden für die Namensauflösung hinzugefügt. Als Teil dieses Aufwands kann der Sensor zusätzlich zur aktiven RPC- und NetBIOS-Auflösung ein TSL Client Hello-Paket an den Port des RDP-Endpunkts (3389) übergeben. 
- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme. 

## <a name="azure-atp-release-230"></a>Azure ATP Release 2.30

Veröffentlicht: 29. April 2018
 
- Verdächtige Aktivitäten zur Herabstufung der Verschlüsselung enthalten jetzt einen Beweisabschnitt, der die von Azure ATP erkannten Symptome beschreibt, auf denen der Verdacht basiert, dass eine Aktivität zur Herabstufung der Verschlüsselung stattgefunden hat. 
-   Azure ATP verwendet jetzt den Azure Email Orchestrator für alle von Azure ATP gesendeten E-Mail-Nachrichten einschließlich verdächtiger Aktivitäten, Überwachungswarnungen und Berichte. Sie werden feststellen, dass diese E-Mail-Benachrichtigungen jetzt im Interesse der Benutzerfreundlichkeit ein konsistentes Format aufweisen, und Excel-Dateien werden mit der E-Mail verknüpft, die von der Konsole heruntergeladen werden können.
 
 

## <a name="azure-atp-release-229"></a>Azure ATP-Version 2.29

Veröffentlicht: 22. April 2018
 
- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme. 
 
 
## <a name="azure-atp-release-228"></a>Azure ATP-Version 2.28

Veröffentlicht: 15. April 2018
 
-   Benutzer, die Mitglieder der Rollengruppen für Azure ATP-Benutzer und anzeigende Azure ATP-Benutzer sind, sind jetzt berechtigt, Überwachungswarnungen anzuzeigen.
- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme. 


## <a name="azure-atp-release-227"></a>Azure ATP-Version 2.27

Veröffentlicht: 8. April 2018

- Sie haben jetzt die Möglichkeit, Benutzerfeedback über die obere Navigationsleiste bereitzustellen. Durch Klicken auf das Smileysymbol in der Menüleiste können Sie eine E-Mail mit Ihrem Feedback an das Azure Advanced Threat Protection-Team senden.

- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme. 
 

## <a name="azure-atp-release-226"></a>Azure ATP-Version 2.26

Veröffentlicht: 25. März 2018

- Wenn Azure ATP Sie über eine verdächtige Aktivität informiert, die Sie als gutartig positiv identifizieren (eine legitime Aktion, die keine verdächtige Aktivität ist), haben Sie die Möglichkeit, Computer und IP-Adressen für weitere Erkennungen auszuschließen. Hierzu zählen: Herabstufen der Verschlüsselung, LDAP-Brute-Force, gefälschte PAC, Brute-Force und Pass-the-Hash.
-   Die Leistung des Azure ATP-Sensors wurde verbessert.
-   Eine neue Region für die Bereitstellung eines Arbeitsbereichs wurde hinzugefügt. Sie können ab sofort auch einen Arbeitsbereich in Asien bereitstellen. 


## <a name="azure-atp-release-225"></a>Azure ATP Version 2.25

Veröffentlicht: 18. März 2018

- Die mehrstufige Authentifizierung (Multi-factor authentication, MFA) wird jetzt von Azure ATP unterstützt. Mandanten, die MFA verwenden, können jetzt auf das Azure ATP-Portal zugreifen.
- Azure ATP verfügt jetzt über die Seite [**Systemstatus**](https://health.atp.azure.com/), auf der Sie Informationen dazu erhalten, ob das Portal zum Verwalten des Arbeitsbereichs aktiv ist und funktioniert, ob Probleme bei Ermittlungsvorgängen auftreten und ob der Sensor Datenverkehr an die Cloud senden kann. Sie können über die Menüleiste in Azure ATP auf den **Systemstatus** zugreifen.


## <a name="azure-atp-release-224"></a>Azure ATP Version 2.24

Veröffentlicht: 11. März 2018

**Neue und aktualisierte Erkennungen**
  - Erstellung verdächtiger Dienste – Angreifer versuchen, verdächtige Dienste in Ihrem Netzwerk auszuführen. Azure ATP gibt jetzt eine Warnung aus, wenn erkannt wird, dass jemand an einem bestimmten Computer einen neuen Dienst ausführt, der verdächtig erscheint. Diese Erkennung basiert auf Ereignissen (nicht auf Datenverkehr) und wird auf jedem Domänencontroller in Ihrem Netzwerk ausgelöst, der das Ereignis 7045 an Azure ATP weiterleitet. Weitere Informationen finden Sie im [Leitfaden zu verdächtigen Aktivitäten](suspicious-activity-guide.md).

**Verbesserte Untersuchung**
  - Azure ATP enthält ein erweitertes [Entitätsprofil](entity-profiles.md). Über das Entitätsprofil erhalten Sie eine Plattform, die auf eine detaillierte Untersuchung von Benutzeraktivitäten ausgerichtet ist. Zu diesen gehören u.a die verwendeten Ressourcen und Computer. Über das Entitätsprofil erhalten Sie Verzeichnisdaten, und Sie haben die Möglichkeit, potenzielle Lateral Movement-Pfade zu oder von der Entität zu identifizieren, wodurch Sie mehr über die potenziellen Sicherheitsverletzungen in Ihrer Organisation erfahren können.

  - ATP ermöglicht es Ihnen, Entitäten manuell als *vertraulich* zu kennzeichnen, um die Erkennung und Überwachung zu verbessern. Diese Kennzeichnung hat Auswirkungen auf viele Azure ATP-Vorgänge zum Erkennen von verdächtigen Diensten, wie z.B. die Vorgänge zum Erkennen von Änderungen sensibler Gruppen und [Lateral Movement-Pfaden](use-case-lateral-movement-path.md), die sensible Entitäten verwenden.

**Neue Berichte, um Sie bei Untersuchungen zu unterstützen**
  - Mithilfe des [Berichts zu Kennwörtern im Klartextformat](reports.md) können Sie erkennen, wenn Dienste Kontoanmeldeinformationen im Nur-Text-Format gesendet werden. Durch diese Funktion können Sie Dienste untersuchen und die Sicherheitsstufe Ihres Netzwerks verbessern. Der Bericht ersetzt die Klartextwarnungen über verdächtige Aktivität.
  - In [Lateral Movement-Pfaden zu sensiblen Konten](reports.md) werden die sensiblen Konten aufgeführt, die über Lateral Movement-Pfade zur Verfügung gestellt werden. Um die Angriffsfläche zu minimieren, kann so die Anzahl dieser Pfade verringert und die Sicherheit Ihres Netzwerks erhöht werden. Indem Lateral Movement-Vorgänge verhindert werden, können sich Angreifer nicht zwischen Benutzern und Computern in Ihrem Netzwerk bewegen, bis sie auf den Jackpot in Sachen virtuelle Sicherheit stoßen: die sensiblen Anmeldeinformationen Ihres Administratorkontos.

- Sie können jetzt einfach über den in einer Warnung über verdächtige Aktivität enthaltenen Link auf die Dokumentation zugreifen, um [Schritte, die Sie durchführen können](suspicious-activity-guide.md) anzuzeigen. 

**Leistungsverbesserungen**
 -  Die Azure ATP-Sensorinfrastruktur wurde bezüglich der Leistung verbessert: Die aggregierte Datenverkehrsansicht ermöglicht Optimierungen der CPU- und Paketpipeline und verwendet Sockets zu Domänencontrollern erneut, um SSL-Sitzungen zum DC zu minimieren.

## <a name="see-also"></a>Weitere Informationen
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Azure ATP capacity planning (Azure ATP-Kapazitätsplanung)](atp-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)