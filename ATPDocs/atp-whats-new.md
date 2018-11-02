---
title: Neuerungen in Azure ATP | Microsoft-Dokumentation
description: Beschreibt die neuesten Releases von Azure ATP und enthält Informationen zu den Neuerungen in den einzelnen Version.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/21/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 7d0f33db-2513-4146-a395-290e001f4199
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: bf620fd9eb3ee750f19a4fe69aa3efea16b9385a
ms.sourcegitcommit: 59ed430fa0cd8ac34a70609026ec5fc2f5972f57
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/21/2018
ms.locfileid: "49480666"
---
*Gilt für: Azure Advanced Threat Protection*

# <a name="whats-new-in-azure-atp"></a>Neuerungen in Azure ATP 

## <a name="azure-atp-release-251"></a>Azure ATP, Release 2.5.1
Veröffentlicht: 21. Oktober 2018

- Sie können die Integration von **WD-ATP** über den Bildschirm [Konfiguration](integrate-wd-atp.md#how-to-integrate-azure-atp-with-windows-defender-atp) im Azure ATP-Portal aktivieren oder deaktivieren. (Hierfür muss der Azure ATP-Benutzer ein globaler Administrator oder ein Sicherheitsadministrator im AAD-Mandanten sein.)

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-250"></a>Azure ATP Release 2.50
Veröffentlicht: 14. Oktober 2018
- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme.


## <a name="azure-atp-release-249"></a>Azure ATP Release 2.49
Veröffentlicht: 7. Oktober 2018
-   **Neue Erkennungen: Verdächtige DNS-Kommunikation** (Vorschauversion)<br>Neue Erkennungen, die hinzugefügt wurden, und vor verdächtigen DNS-Kommunikationsangriffen schützen:

    -   Diese Erkennung hilft dabei, Angriffe gegen das DNS-Protokoll zu erkennen: In den meisten Organisationen wird das DNS-Protokoll nicht überwacht und nur selten vor böswilligen Angriffen blockiert. Dadurch kann ein Angreifer auf einem kompromittierten Computer das DNS-Protokoll missbrauchen. Böswillige Kommunikation über DNS kann zur Datenexfiltration, Befehls- und Führungssystemeinschränkung und/oder zur Umgehung von Netzwerkeinschränkungen führen.

- **Neue Funktionen** <br>Die Azure ATP-**Benutzerrolle** wurde mit den folgenden Funktionen verbessert:
  - Der Status der Sicherheitswarnungen wurde geändert (erneut öffnen, schließen, ausschließen, unterdrücken)
  - Geplante Berichte wurden festgelegt
  - Entitätstags (vertraulich und Honeytoken) wurden festgelegt.
  - Ausschluss von Erkennung
  - Sprache ändern
  - Benachrichtigung über E-Mail oder Syslog wurden festgelegt


- Ein temporärer Anstieg von Sicherheitswarnungen des Typs **Reconnaissance mithilfe von Verzeichnisdienstabfragen**, die am 16.9.2018 aufgetreten sind, wurden identifiziert und gelöst. 

- Diese Version enthält darüber hinaus Fehlerbehebungen und Verbesserungen für mehrere Probleme.


## <a name="azure-atp-release-248"></a>Azure ATP Release 2.48
Veröffentlicht: 16. September 2018
- **Sicherheitswarnung:** Reconnaissance mithilfe von Verzeichnisdienstabfragen

  Diese Sicherheitswarnung enthält nun verbesserte Infografiken und Beweise. 

- **Ausschließen von Entitäten von der Erkennung** 

  Sie können Entitäten nun aus den folgenden Erkennungen ausschließen, um die Anzahl falsch positiver Ergebnisse zu reduzieren: 
  - Verdächtige VPN-Verbindung (Benutzerausschluss)
  - Verdächtige Heraufstufung zu Domänencontrollern (potenzieller DcShadow-Angriff)
  - Verdächtige Replikationsanforderung (potenzieller DcShadow-Angriff)

- Diese Version enthält darüber hinaus Fehlerbehebungen und Verbesserungen für mehrere Probleme.


## <a name="azure-atp-release-247"></a>Azure ATP Release 2.47
Veröffentlicht: 2. September 2018

- **Überprüfung der erweiterten Überwachungsrichtlinie von Azure ATP**
 
Azure Advanced Threat Protection überprüft jetzt die in Ihrem Domänencontroller vorhandenen erweiterten Überwachungsrichtlinien und empfiehlt Richtlinienänderungen, um die maximale Serviceabdeckung durch Azure ATP für Ihre Organisation zu garantieren. 

**Mit dieser Überprüfung können Sie nun folgende Aktionen ausführen:**
  -  fehlende Ereignisse in Ihren Windows-Ereignisprotokollen identifizieren, die derzeit von der Abdeckung durch Azure ATP ausgeschlossen sind
  -  ideale Einstellungen überprüfen und Änderungen basierend auf den bereitgestellten Empfehlungen für die Integritätswarnung durchführen
  -  zudem wird eine einzelne aggregierte Integritätswarnung für alle Ihre Domänencontroller ausgegeben, einschließlich Vorschlägen für die Wartung (falls benötigt).

Überprüfen Sie, wie [erweiterte Überwachungsrichtlinien konfiguriert werden](atp-advanced-audit-policy.md), um sicherzustellen, dass Ihr System ordnungsgemäß konfiguriert ist. 
- Diese Version enthält darüber hinaus Fehlerbehebungen und Verbesserungen für mehrere Probleme.

## <a name="azure-atp-release-246"></a>Azure ATP Release 2.46

Veröffentlicht: 26. August 2018

- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme.

## <a name="azure-atp-release-245"></a>Azure ATP Release 2.45

Veröffentlicht: 19. August 2018

- **Azure ATP verfügt nun über die Event Trace for Windows (ETW) als zusätzliche Datenquelle**  <br> Die Ereignisablaufverfolgung für Windows (Event Tracing for Windows, ETW) wurde neben dem vorhandenen Netzwerkverkehr und den Windows-Ereignissen als zusätzliche Datenquelle hinzugefügt. Die ETW bietet zusätzlich die Erkennung von verdächtigen Aktivitäten wie den Folgenden: Verdächtige Heraufstufung zu Domänencontroller und verdächtige Domänencontroller-Replikationsanforderungen (beide stellen potenzielle DcShadow-Angriffe dar). <br>
Nur die auf Domänencontrollern installierten ATP-Sensoren unterstützen die Erkennung basierend auf der ETW. Die Erkennung der auf ETW basierenden Ereignissenke wird nicht von eigenständigen ATP-Sensoren unterstützt. <br>  

- **Vier neue Erkennungen ab sofort allgemein verfügbar** <br>
  - Verdächtige VPN-Verbindung
  - Kerberos Golden Ticket – nicht vorhandenes Konto 
  - Erkennung verdächtiger Heraufstufungen zu Domänencontrollern (potenzieller DcShadow-Angriff) – Erkennung basierend auf der ETW, nur bei ATP-Sensoren verfügbar 
  - Verdächtige Domänencontroller-Replikationsanforderung (potenzieller DcShadow-Angriff) – Erkennung basierend auf der ETW, nur bei ATP-Sensoren verfügbar

- Diese Version enthält darüber hinaus Fehlerbehebungen und Verbesserungen für mehrere Probleme.


## <a name="azure-atp-release-244"></a>Azure ATP Release 2.44

Veröffentlicht: 12. August 2018

- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme.
- Die auf dem Sensorcomputer erstellten Protokolldateien enthalten nicht mehr das Protokoll „Ausnahmestatistik“.


## <a name="azure-atp-release-243"></a>Azure ATP Release 2.43

Veröffentlicht: 5. August 2018

- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme.



## <a name="azure-atp-release-242"></a>Azure ATP Release 2.42

Veröffentlicht: 29. Juli 2018

- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme. 


## <a name="azure-atp-release-241"></a>Azure ATP Release 2.41

Veröffentlicht: 22. Juli 2018

- **Unterstützung für mehrere Azure ATP-Gesamtstrukturen wird schrittweise eingeführt (Vorschau)** <br> Azure ATP kann jetzt Organisationen mit mehreren Gesamtstrukturen unterstützen, wodurch Sie die Möglichkeit erhalten, Aktivitäten und Profilbenutzer in allen Gesamtstrukturen zu überwachen. Diese neue Funktionalität ermöglicht Ihnen Folgendes:

  - Sie können Aktivitäten, die von Benutzern in mehreren Gesamtstrukturen ausgeführt werden, in einer zentralen Konsole im Blick behalten und untersuchen.
  - Durch erweiterte Active Directory-Integration und -Kontoauflösung lassen sich falsch positive Ergebnisse besser erkennen und reduzieren.
  - Sie profitieren von besseren Überwachungswarnungen und -berichten für eine organisationsübergreifende Übersicht.


-   **Neue Erkennungsoptionen: DCShadow**<br>Zwei neue Erkennungsfunktionen helfen Ihnen beim Schutz vor DCShadow-Angriffen (Domain Controller Shadow):

    -   Verdächtige Hochstufung zu Domänencontrollern (potenzieller DCShadow-Angriff): Diese Funktion hilft bei der Erkennung von Angriffen, bei denen ein Computer die Identität eines Domänencontrollers annimmt und dann versucht, die Replikation zu verwenden, um Änderungen an andere Domänencontroller in Ihrer Domäne zu verteilen.

    -   Verdächtige Replikationsanforderung (potenzieller DCShadow-Angriff): Diese Funktion hilft beim Schutz vor Angriffen, bei denen versucht wird, Computer, die keine Domänencontroller sind, zu Domänencontrollern hochzustufen, um Verzeichnisobjekte zu ändern.

-   **Verbesserte Informationen zu Verschlüsselungsdowngrades**<br>Die Erkennung von Verschlüsselungsdowngrades bietet jetzt mehr Informationen zum Typ des erkannten Angriffs: Overpass-the-Hash, Golden Ticket und Skeleton Key. Darüber hinaus wurden diese Warnungen aggregiert, um die Untersuchung zu vereinfachen.
- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme. 



## <a name="azure-atp-release-240"></a>Azure ATP Release 2.40

Veröffentlicht: 15. Juli 2018

- Die Pass-the-Ticket-Erkennung enthält jetzt auf der Seite „Warnungsdetails“ einen Beweisabschnitt. Dort werden zusätzliche Informationen zu einer Warnung angezeigt.

- Benutzerzugriffssteuerungs-Flags, die im Profil eines Benutzers unter den Verzeichnisdaten zu finden sind, enthalten jetzt eine Legende, um zu verdeutlichen, welche Attribute aktiviert und welche deaktiviert sind.  

## <a name="azure-atp-release-239"></a>Azure ATP Release 2.39

Veröffentlicht: 5. Juli 2018
-   **Neue hinzugefügte Erkennung: Kerberos Golden Ticket – nichtvorhandenes Konto** (Vorschauversion)<br>Mit dieser neuen Erkennung können Sie Ihre Organisation vor Angriffen schützen, in denen ein Golden Ticket für ein Konto erstellt wird, das in Ihrer Domäne nicht existiert. Weitere Informationen finden Sie im [Azure Advanced Threat Protection-Handbuch zu verdächtigen Aktivitäten](suspicious-activity-guide.md#golden-ticket).

- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme. 


## <a name="azure-atp-release-238"></a>Azure ATP Release 2.38

Veröffentlicht: 1. Juli 2018

- Diese Version enthält Fehlerbehebungen und Verbesserungen für verschiedene Probleme sowie Erweiterungen des Azure ATP-Portals.

## <a name="azure-atp-release-237"></a>Azure ATP Release 2.37

Veröffentlicht: 24. Juni 2018

- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme. 

## <a name="azure-atp-release-236"></a>Azure ATP Release 2.36

Veröffentlicht: 17. Juni 2018

- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme. 


## <a name="azure-atp-release-235"></a>Azure ATP Release 2.35

Veröffentlicht am 10. Juni 2018
 
- **Vorschauversionen neuer Erkennungen**<br></br>Ab jetzt nutzt Azure ATP seine Funktion als Clouddienst – für den neue Features in kürzeren Zyklen bereitgestellt werden können –und bietet Ihnen so schnell wie möglich neue Erkennungen. Diese neuen Erkennungen werden als „Vorschauversion“ markiert, wenn sie das erste Mal veröffentlicht werden. In der Regel wechselt eine neue Erkennung innerhalb weniger Wochen von der Vorschauversion zu einer allgemein verfügbaren Version. Es werden standardmäßig Vorschauversionen neuer Erkennungen angezeigt. Weitere Informationen zum Deaktivieren dieser Standardeinstellung finden Sie unter [Preview Detections (Vorschauversionen neuer Erkennungen)](working-with-suspicious-activities.md#preview-detections).
 
- **Erkennung verdächtiger VPNs**<br></br>Mit dieser Vorschauversion wird eine Vorschauversion für eine Erkennung verdächtiger VPNs eingeführt. Azure ATP speichert Informationen zum VPN-Verhalten des Benutzers, einschließlich der Computer, auf denen die Benutzer angemeldet sind, und der Orte, von denen die Benutzer eine Verbindung herstellen. Sie erhalten eine Warnung, wenn nicht das erwartete Verhalten eintritt. Weitere Informationen finden Sie unter [Suspicious VPN detection (Erkennung verdächtiger VPNs)](suspicious-activity-guide.md#suspicious-vpn-detection).

- **Delayed update** (Verzögertes Update)<br></br>Sie haben jetzt die Möglichkeit auszuwählen, dass Azure ATP-Sensoren bei jedem Update von Azure ATP erst später aktualisiert werden. Sie können für jeden einzelnen Sensor die Option **Delayed update** (Verzögertes Update) auswählen, sodass das Update erst 24 Stunden nach dem Update des Azure ATP-Clouddiensts ausgeführt wird. Durch dieses Feature können Sie das Update für bestimmte Testsensoren ausprobieren und Ihre Produktionssensoren erst später aktualisieren. Wenn bei dem ersten Updatezyklus ein Problem auftritt, erstellen Sie ein Supportticket. Weitere Informationen finden Sie unter [Aktualisieren von Azure ATP-Sensoren](sensor-update.md).

- **Aktualisierte Erkennung für ungewöhnliche Protokollimplementierungen**<br></br>Mithilfe der Erkennung für ungewöhnliche Protokollimplementierungen können jetzt mehr Informationen bereitgestellt werden. Sie können jetzt sehen, welches potenzielle Angriffstool Azure ATP verdächtigt, auf Ihrem Netzwerk zu arbeiten. Weitere Informationen finden Sie im [Leitfaden zu verdächtigen Aktivitäten](suspicious-activity-guide.md).
 
- **Warnung bei veralteten Sensoren**<br></br>Azure ATP umfasst eine neue Überwachungswarnung, über die Sie informiert werden, wenn es bereits drei neue Versionen eines Sensors gibt und noch kein Update ausgeführt wurde. Wenn Ihnen diese Warnung angezeigt wird, sollten Sie den Sensor aktualisieren oder prüfen, warum der Sensor nicht automatisch aktualisiert wird. Wenn die Warnung wiederholt auftritt, deinstallieren Sie den Sensor und installieren Sie ihn erneut.

- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme. 

## <a name="azure-atp-release-234"></a>Azure ATP Release 2.34

Veröffentlicht: 3. Juni 2018
 
- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme. 

 
## <a name="azure-atp-release-233"></a>Azure ATP Release 2.33

Veröffentlicht: 27. Mai 2018

- Feature der Vorschauversion: Azure ATP unterstützt jetzt neue Sprachen und 13 neue Gebietsschemas:
    - Tschechisch
    - Ungarisch
    - Italienisch
    - Koreanisch
    - Niederländisch
    - Polnisch
    - Portugiesisch (Brasilien)
    - Portugiesisch (Portugal)
    - Russische Föderation
    - Schwedisch
    - Türkisch
    - Chinesisch (China)
    - Chinesisch (Taiwan)



## <a name="azure-atp-release-232"></a>Azure ATP Release 2.32

Veröffentlicht: 13. Mai 2018
 
- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme. 

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
- [Was ist Azure Advanced Threat Protection?](what-is-atp.md)
- [Häufig gestellte Fragen](atp-technical-faq.md)
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Azure ATP-Kapazitätsplanung](atp-capacity-planning.md) (configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)