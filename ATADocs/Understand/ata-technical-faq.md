---
title: "Häufig gestellte Fragen zu ATA | Microsoft ATA"
description: "Liste häufig gestellter Fragen zu ATA und zugehörige Antworten"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: a7d378ec-68ed-4a7b-a0db-f5e439c3e852
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7d081a6e14adffc675de203001074c3435cce6b2
ms.openlocfilehash: 8896df26157f9da903e68ac7a1d21f7f80f95026


---
*Gilt für: Advanced Threat Analytics Version 1.7*

# Häufig gestellte Fragen zu ATA
Dieser Artikel enthält eine Reihe häufig gestellter Fragen zu ATA sowie Hintergrundwissen und Antworten.


## Wie wird ATA lizenziert?
Weitere Informationen zur Lizenzierung finden Sie unter [Bezugsquellen für Advanced Threat Analytics](https://www.microsoft.com/cloud-platform/advanced-threat-analytics-pricing).


## Das ATA-Gateway startet nicht. Wie sollte ich vorgehen?
Sehen Sie sich den letzten Fehlereintrag im aktuellen Fehlerprotokoll an (Installationsverzeichnis von ATA unter dem Ordner „Logs“).
## Wie kann ich ATA testen?
Sie können einen End-to-End-Test durchführen und verdächtige Aktivitäten simulieren. Führen Sie dazu eine der folgenden Aktionen aus:

1.  DNS-Reconnaissance durch Verwendung von „Nslookup.exe“
2.  Remoteausführung durch Verwendung von „psexec.exe“


Dies muss remote für den überwachten Domänencontroller und nicht über das ATA-Gateway ausgeführt werden.

## Wie kann ich die Windows-Ereignisweiterleitung überprüfen?
Sie können den folgenden Code in einer Datei ablegen und ihn dann über eine Eingabeaufforderung im Verzeichnis **\Programme\Microsoft Advanced Threat Analytics\Center\MongoDB\bin** wie folgt ausführen:

ATA-Dateiname mongo.exe

        db.getCollectionNames().forEach(function(collection) {
        if (collection.substring(0,10)=="NtlmEvent_") {
                if (db[collection].count() > 0) {
                                  print ("Found "+db[collection].count()+" NTLM events") 
                                }
                }
        });

## Funktioniert ATA mit verschlüsseltem Datenverkehr?
ATA stützt sich auf die Analyse mehrerer Netzwerkprotokolle sowie auf Ereignisse, die aus dem SIEM-Server oder über die Windows-Ereignisweiterleitung gesammelt wurden, sodass ATA wie gewohnt arbeitet und der Großteil der Erkennungen nicht betroffen ist, obwohl der verschlüsselte Datenverkehr nicht analysiert wird (z.B. LDAPS und IPSEC ESP).

## Funktioniert ATA mit Kerberos Armoring?
Die Aktivierung von Kerberos Armoring (auch als Flexible Authentication Secure Tunneling (FAST) bezeichnet) wird von ATA unterstützt. Einzige Ausnahme ist die Overpass-The-Hash-Erkennung, die nicht unterstützt wird.
## Wie viele ATA-Gateways benötige ich?

Die Anzahl der ATA-Gateways hängt von Ihrem Netzwerklayout, der Menge der Pakete und der Anzahl der Ereignisse ab, die von ATA erfasst werden. Lesen Sie den Abschnitt [Größenzuteilung für ATA Center](/advanced-threat-analytics/plan-design/ata-capacity-planning#ata-lightweight-gateway-sizing), um die genaue Anzahl zu ermitteln. 

## Wie viel Speicher benötige ich für ATA?
Für jeden ganzen Tag mit durchschnittlich 1000 Paketen/Sekunde sind 0,3 GB Speicher erforderlich.<br /><br />Weitere Informationen zur Dimensionierung von ATA Center finden Sie unter [ATA-Kapazitätsplanung](/advanced-threat-analytics/plan-design/ata-capacity-planning).


## Warum gelten bestimmte Konten als sensible Konten?
Dies ist der Fall, wenn ein Konto bestimmten Gruppen angehört, die als sensibel festgelegt sind (z. B. „Domänen-Admins“).

Um nachzuvollziehen, warum ein Konto ein sensibles Konto ist, können Sie seine Gruppenmitgliedschaft überprüfen, um festzustellen, welchen sensiblen Gruppen es angehört (die Gruppe, der das Konto angehört, kann auch wegen einer anderen Gruppe eine sensible Gruppe sein. Daher sollten Sie immer die höchste sensible Gruppe überprüfen).

## Wie kann ich einen virtuellen Domänencontroller mit ATA überwachen?
Die meisten virtuellen Domänencontroller können vom ATA-Lightweight-Gateway abgedeckt werden. Um festzustellen, ob das ATA-Lightweight-Gateway sich für Ihre Umgebung eignet, lesen Sie die Informationen unter [ATA-Kapazitätsplanung](/advanced-threat-analytics/plan-design/ata-capacity-planning).

Wenn ein virtueller Domänencontroller nicht durch das ATA-Lightweight-Gateway abgedeckt werden kann, können Sie ein virtuelles oder physisches ATA-Gateway verwenden, wie unter [Konfigurieren der Portspiegelung](/advanced-threat-analytics/deploy-use/configure-port-mirroring) beschrieben.  <br />Die einfachste Möglichkeit ist jeweils ein virtuelles ATA-Gateway auf jedem Host, auf dem ein virtueller Domänencontroller vorhanden ist.<br />Wenn die virtuellen Domänencontroller zwischen Hosts verschoben werden, müssen Sie eine der folgenden Aktionen ausführen:

-   Wenn der virtuelle Domänencontroller auf einen anderen Host verschoben wird, konfigurieren Sie das ATA-Gateway auf diesem Host so vor, dass der Datenverkehr von dem zuvor verschobenen virtuellen Domänencontroller empfangen wird.
-   Stellen Sie sicher, dass Sie das virtuelle ATA-Gateway dem virtuellen Domänencontroller zuordnen, sodass das ATA-Gateway ggf. mit dem Controller verschoben wird.
-   Es gibt einige virtuelle Switches, über die der Datenverkehr zwischen Hosts gesendet werden kann.

## Wie kann ich ATA sichern?
Zwei Elemente müssen gesichert werden:

-   Der Datenverkehr und die Ereignisse, die von ATA gespeichert werden und die mit jedem unterstützten Verfahren zur Datenbanksicherung gesichert werden können. Weitere Informationen hierzu finden Sie unter [ATA-Datenbankverwaltung](/advanced-threat-analytics/deploy-use/ata-database-management). 
-   Die Konfiguration von ATA. Sie ist in der Datenbank gespeichert und wird automatisch jede Stunde im Ordner **Sicherung** im Bereitstellungsspeicherort von ATA Center gesichert.  Weitere Informationen finden Sie unter [ATA-Datenbankverwaltung](https://docs.microsoft.com/advanced-threat-analytics/deploy-use/ata-database-management).
## Was kann ATA erkennen?
ATA erkennt bekannte Angriffe und Techniken, Sicherheitsprobleme und Risiken.
Die vollständige Liste der ATA-Erkennungen finden Sie unter [Welche Bedrohungen erkennt ATA?](ata-threats.md).

## Welche Art von Speicher benötige ich für ATA?
Wir empfehlen ein schnelles Speichermedium (Datenträger mit 7200 U/min werden nicht empfohlen) mit Datenträgerzugriff mit niedriger Latenz (weniger als 10 ms). Die RAID-Konfiguration sollte hohe Schreiblasten unterstützen (RAID-5/6 und zugehörige Ableitungen werden nicht empfohlen).

## Wie viele Netzwerkkarten sind für das ATA-Gateway erforderlich?
Für das ATA-Gateway sind mindestens zwei Netzwerkkarten erforderlich:<br>1. Eine Netzwerkkarte für die Verbindung mit dem internen Netzwerk und ATA Center.<br>2. Eine Netzwerkkarte zum Erfassen des Domänencontroller-Netzwerkverkehrs über Portspiegelung.<br>* Dies gilt nicht für das ATA-Lightweight-Gateway, das systemintern alle Netzwerkadapter verwendet, die der Domänencontroller verwendet.

## Welche Art der Integration weist ATA mit SIEMs auf?
ATA weist eine bidirektionale Integration mit SIEMs auf:

1. ATA kann so konfiguriert werden, dass im Fall einer verdächtigen Aktivität eine Syslog-Warnung an alle SIEM-Server gesendet wird, die das CEF-Format verwenden.
2. ATA kann so konfiguriert werden, dass für jedes Windows-Ereignis mit der ID 4776 Syslog-Meldungen von [diesen SIEMs](/advanced-threat-analytics/deploy-use/configure-event-collection#siem-support) empfangen werden.

## Kann ATA in Ihrer IaaS-Lösung virtualisierte Domänencontroller überwachen?

Ja, Sie können mit dem ATA-Lightweight-Gateway Domänencontroller in einer beliebigen IaaS-Lösung überwachen.

## Wird das Produkt lokal oder in der Cloud angeboten?
Microsoft Advanced Threat Analytics ist ein lokales Produkt.

## Wird das Produkt ein Bestandteil von Azure Active Directory oder von lokalem Active Directory sein?
Diese Lösung ist derzeit ein eigenständiges Angebot und ist weder ein Bestandteil von Azure Active Directory noch von lokalem Active Directory.

## Müssen eigene Regeln geschrieben und ein Schwellenwert/eine Basislinie erstellt werden?
Bei Microsoft Advanced Threat Analytics besteht keine Notwendigkeit zum Erstellen von Regeln, Schwellenwerten oder Basislinien und der anschließenden Optimierung. ATA analysiert das Verhalten von Benutzern, Geräten und Ressourcen – sowie deren Beziehungen untereinander – und kann verdächtige Aktivitäten und bekannte Angriffe schnell erkennen. Drei Wochen nach der Bereitstellung beginnt ATA, verdächtige Verhaltensaktivitäten zu erkennen. Bekannte Angriffe und Sicherheitsprobleme werden hingegen sofort nach der Bereitstellung von ATA erkannt.

## Wenn bei Ihnen bereits eine Sicherheitsverletzung aufgetreten ist, kann Microsoft Advanced Threat Analytics dann auch nicht normales Verhalten erkennen?
Ja, selbst wenn ATA nach einer Sicherheitsverletzung installiert wird, kann ATA verdächtige Aktivitäten des Hackers erkennen. ATA überprüft nicht nur das Verhalten des einen Benutzers, sondern auch das der anderen Benutzer in der Sicherheitsstruktur der Organisation. Wenn das Verhalten des Angreifers während der ersten Analyse nicht normal ist, wird es als „Ausreißer“ identifiziert, und ATA fährt damit fort, das nicht normale Verhalten zu melden. Darüber hinaus kann ATA die verdächtige Aktivität erkennen, wenn der Hacker versucht, die Anmeldeinformationen eines anderen Benutzers zu stehlen, z.B. Pass-the-Ticket, oder wenn er versucht, eine Remoteausführung auf einem Domänencontroller durchzuführen.

## Wird nur Active Directory-Datenverkehr genutzt?
Zusätzlich zur Analyse des Active Directory-Datenverkehrs mit der DPI-Technologie (Deep Packet Inspection) kann ATA auch relevante Ereignisse aus Ihrem SIEM-System (Security Information and Event Management) sammeln und Entitätenprofile auf Grundlage von Informationen aus Active Directory-Domänendiensten erstellen. ATA kann auch Ereignisse aus den Ereignisprotokollen erfassen, wenn die Organisation die Windows-Ereignisprotokollweiterleitung konfiguriert hat.

## Was ist Portspiegelung?
Auch als SPAN (Switched Port Analyzer) bekannt, ist die Portspiegelung eine Methode zur Überwachung des Netzwerkverkehrs. Wenn die Portspiegelung aktiviert ist, sendet der Switch eine Kopie aller Netzwerkpakete von einem Port (oder einem gesamten VLAN) an einen anderen Port, an dem das Paket analysiert werden kann.

## Überwacht ATA nur Geräte, die der Domäne angehören?
Nein. ATA überwacht alle Geräte im Netzwerk und führt die Authentifizierung sowie Autorisierungsanfragen für Active Directory durch. Dies schließt Nicht-Windows-Geräte und mobile Geräte ein.

## Überwacht ATA sowohl Computerkonten als auch Benutzerkonten?
Ja. Da Computerkonten (ebenso wie alle anderen Entitäten) zum Durchführen böswilliger Aktivitäten verwendet werden können, überwacht ATA das Verhalten aller Computerkonten und aller weiteren Entitäten in der Umgebung.

## Kann ATA kann mehrere Domänen und mehrere Gesamtstrukturen unterstützen?
Microsoft Advanced Threat Analytics unterstützt-Umgebungen mit mehreren Domänen innerhalb der gleichen Gesamtstrukturbegrenzung. Mehrere Gesamtstrukturen erfordern eine ATA-Bereitstellung für jede Gesamtstruktur.
## Kann die Gesamtintegrität der Bereitstellung angezeigt werden?
Ja, Sie können die Gesamtintegrität der Bereitstellung sowie spezifische Probleme im Zusammenhang mit der Konfiguration, Konnektivität usw. anzeigen, und werden bei Eintreten eines Problems benachrichtigt.


## Weitere Informationen
- [ATA-Voraussetzungen](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA-Kapazitätsplanung](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Konfigurieren der Ereignissammlung](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurieren der Windows-Ereignisweiterleitung](/advanced-threat-analytics/deploy-use/configure-event-collection#Configuring-Windows-Event-Forwarding)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Sep16_HO4-->


