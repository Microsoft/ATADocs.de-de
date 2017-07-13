---
title: "Häufig gestellte Fragen zu Advanced Threat Analytics | Microsoft-Dokumentation"
description: "Liste häufig gestellter Fragen zu ATA und zugehörige Antworten"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/3/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: a7d378ec-68ed-4a7b-a0db-f5e439c3e852
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 5beabd2617f55ecbcc717338dc40d9f597cc25d4
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
*Gilt für: Advanced Threat Analytics Version 1.8*

# Häufig gestellte Fragen zu ATA
<a id="ata-frequently-asked-questions" class="xliff"></a>
Dieser Artikel enthält eine Reihe häufig gestellter Fragen zu ATA sowie Hintergrundwissen und Antworten.


## Wo erhalte ich eine Lizenz für Advanced Threat Analytics (ATA)?
<a id="where-can-i-get-a-license-for-advanced-threat-analytics-ata" class="xliff"></a>

Wenn Sie über ein aktives Enterprise Agreement verfügen, können Sie die Software aus dem Microsoft Volume Licensing Center (VLSC) herunterladen.

Wenn Sie eine Lizenz für Enterprise Mobility + Security (EMS) direkt über das Office 365-Portal oder über das Cloud Solution Partner-Lizenzmodell (CSP) erworben haben, und Sie keinen Zugriff auf ATA über das Microsoft Volume Licensing Center (VLSC) verfügen, kontaktieren Sie den Microsoft-Kundendienst, um den Prozess zum Aktivieren von Advanced Threat Analytics (ATA) abzurufen.

## Das ATA-Gateway startet nicht. Wie sollte ich vorgehen?
<a id="what-should-i-do-if-the-ata-gateway-wont-start" class="xliff"></a>
Sehen Sie sich den letzten Fehlereintrag im aktuellen Fehlerprotokoll an (Installationsverzeichnis von ATA unter dem Ordner „Logs“).

## Wie kann ich ATA testen?
<a id="how-can-i-test-ata" class="xliff"></a>
Sie können einen End-to-End-Test durchführen und verdächtige Aktivitäten simulieren. Führen Sie dazu eine der folgenden Aktionen aus:

1.  DNS-Reconnaissance durch Verwendung von „Nslookup.exe“
2.  Remoteausführung durch Verwendung von „psexec.exe“


Dies muss remote für den überwachten Domänencontroller und nicht über das ATA-Gateway ausgeführt werden.

## Welcher ATA-Build entspricht der jeweiligen Version?
<a id="which-ata-build-corresponds-to-each-version" class="xliff"></a>

|Version|Build #|
|----|----|
|1.6|1.6.4103|
|1.6 Update 1|1.6.4317|
|1.7|1.7.5402| 
|1.7 Update 1|1.7.5647|
|1.7 Update 2|1.7.5757|
|1,8|1.8.6645|

## Welche Version soll ich verwenden, um meine aktuelle ATA-Bereitstellung auf die neueste Version upzugraden?
<a id="what-version-should-i-use-to-upgrade-my-current-ata-deployment-to-the-latest-version" class="xliff"></a>

![Matrix zum Upgrade der ATA-Version](./media/version-matrix.png)


## Wie kann ich die Windows-Ereignisweiterleitung überprüfen?
<a id="how-do-i-verify-windows-event-forwarding" class="xliff"></a>
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
<a id="does-ata-work-with-encrypted-traffic" class="xliff"></a>
ATA stützt sich auf die Analyse mehrerer Netzwerkprotokolle sowie auf Ereignisse, die aus dem SIEM-Server oder über die Windows-Ereignisweiterleitung gesammelt wurden, sodass ATA wie gewohnt arbeitet und der Großteil der Erkennungen nicht betroffen ist, obwohl der verschlüsselte Datenverkehr nicht analysiert wird (z.B. LDAPS und IPSEC ESP).

## Funktioniert ATA mit Kerberos Armoring?
<a id="does-ata-work-with-kerberos-armoring" class="xliff"></a>
Die Aktivierung von Kerberos Armoring (auch als Flexible Authentication Secure Tunneling (FAST) bezeichnet) wird von ATA unterstützt. Einzige Ausnahme ist die Overpass-The-Hash-Erkennung, die nicht unterstützt wird.

## Wie viele ATA-Gateways benötige ich?
<a id="how-many-ata-gateways-do-i-need" class="xliff"></a>

Die Anzahl der ATA-Gateways hängt von Ihrem Netzwerklayout, der Menge der Pakete und der Anzahl der Ereignisse ab, die von ATA erfasst werden. Lesen Sie den Abschnitt [Größenzuteilung für ATA Center](ata-capacity-planning.md#ata-lightweight-gateway-sizing), um die genaue Anzahl zu ermitteln. 

## Wie viel Speicher benötige ich für ATA?
<a id="how-much-storage-do-i-need-for-ata" class="xliff"></a>
Für jeden ganzen Tag mit durchschnittlich 1000 Paketen/Sekunde sind 0,3 GB Speicher erforderlich.<br /><br />Weitere Informationen zur Dimensionierung von ATA Center finden Sie unter [ATA-Kapazitätsplanung](ata-capacity-planning.md).


## Warum gelten bestimmte Konten als sensible Konten?
<a id="why-are-certain-accounts-considered-sensitive" class="xliff"></a>
Dies ist der Fall, wenn ein Konto bestimmten Gruppen angehört, die als sensibel festgelegt sind (z. B. „Domänen-Admins“).

Um nachzuvollziehen, warum ein Konto ein sensibles Konto ist, können Sie seine Gruppenmitgliedschaft überprüfen, um festzustellen, welchen sensiblen Gruppen es angehört (die Gruppe, der das Konto angehört, kann auch wegen einer anderen Gruppe eine sensible Gruppe sein. Daher sollten Sie immer die höchste sensible Gruppe überprüfen).

## Wie kann ich einen virtuellen Domänencontroller mit ATA überwachen?
<a id="how-do-i-monitor-a-virtual-domain-controller-using-ata" class="xliff"></a>
Die meisten virtuellen Domänencontroller können vom ATA-Lightweight-Gateway abgedeckt werden. Um festzustellen, ob das ATA-Lightweight-Gateway sich für Ihre Umgebung eignet, lesen Sie die Informationen unter [ATA-Kapazitätsplanung](ata-capacity-planning.md).

Wenn ein virtueller Domänencontroller nicht durch das ATA-Lightweight-Gateway abgedeckt werden kann, können Sie ein virtuelles oder physisches ATA-Gateway verwenden, wie unter [Konfigurieren der Portspiegelung](configure-port-mirroring.md) beschrieben.  <br />Die einfachste Möglichkeit ist jeweils ein virtuelles ATA-Gateway auf jedem Host, auf dem ein virtueller Domänencontroller vorhanden ist.<br />Wenn die virtuellen Domänencontroller zwischen Hosts verschoben werden, müssen Sie eine der folgenden Aktionen ausführen:

-   Wenn der virtuelle Domänencontroller auf einen anderen Host verschoben wird, konfigurieren Sie das ATA-Gateway auf diesem Host so vor, dass der Datenverkehr von dem zuvor verschobenen virtuellen Domänencontroller empfangen wird.
-   Stellen Sie sicher, dass Sie das virtuelle ATA-Gateway dem virtuellen Domänencontroller zuordnen, sodass das ATA-Gateway ggf. mit dem Controller verschoben wird.
-   Es gibt einige virtuelle Switches, über die der Datenverkehr zwischen Hosts gesendet werden kann.

## Wie kann ich ATA sichern?
<a id="how-do-i-back-up-ata" class="xliff"></a>

Informationen finden Sie unter [ATA-Notfallwiederherstellung](disaster-recovery.md)



## Was kann ATA erkennen?
<a id="what-can-ata-detect" class="xliff"></a>

ATA erkennt bekannte Angriffe und Techniken, Sicherheitsprobleme und Risiken.
Die vollständige Liste der ATA-Erkennungen finden Sie unter [Welche Bedrohungen erkennt ATA?](ata-threats.md).

## Welche Art von Speicher benötige ich für ATA?
<a id="what-kind-of-storage-do-i-need-for-ata" class="xliff"></a>
Wir empfehlen ein schnelles Speichermedium (Datenträger mit 7200 U/min werden nicht empfohlen) mit Datenträgerzugriff mit niedriger Latenz (weniger als 10 ms). Die RAID-Konfiguration sollte hohe Schreiblasten unterstützen (RAID-5/6 und zugehörige Ableitungen werden nicht empfohlen).

## Wie viele Netzwerkkarten sind für das ATA-Gateway erforderlich?
<a id="how-many-nics-does-the-ata-gateway-require" class="xliff"></a>
Für das ATA-Gateway sind mindestens zwei Netzwerkkarten erforderlich:<br>1. Eine Netzwerkkarte für die Verbindung mit dem internen Netzwerk und ATA Center.<br>2. Eine Netzwerkkarte zum Erfassen des Domänencontroller-Netzwerkverkehrs über Portspiegelung.<br>* Dies gilt nicht für das ATA-Lightweight-Gateway, das systemintern alle Netzwerkadapter verwendet, die der Domänencontroller verwendet.

## Welche Art der Integration weist ATA mit SIEMs auf?
<a id="what-kind-of-integration-does-ata-have-with-siems" class="xliff"></a>
ATA weist eine bidirektionale Integration mit SIEMs auf:

1. ATA kann so konfiguriert werden, dass im Fall einer verdächtigen Aktivität eine Syslog-Warnung an alle SIEM-Server gesendet wird, die das CEF-Format verwenden.
2. ATA kann so konfiguriert werden, dass für jedes Windows-Ereignis Syslog-Meldungen von [diesen SIEMs](install-ata-step6.md) empfangen werden.

## Kann ATA in Ihrer IaaS-Lösung virtualisierte Domänencontroller überwachen?
<a id="can-ata-monitor-domain-controllers-virtualized-on-your-iaas-solution" class="xliff"></a>
Ja, Sie können mit dem ATA-Lightweight-Gateway Domänencontroller in einer beliebigen IaaS-Lösung überwachen.

## Wird das Produkt lokal oder in der Cloud angeboten?
<a id="is-this-an-on-premises-or-in-cloud-offering" class="xliff"></a>
Microsoft Advanced Threat Analytics ist ein lokales Produkt.

## Wird das Produkt ein Bestandteil von Azure Active Directory oder von lokalem Active Directory sein?
<a id="is-this-going-to-be-a-part-of-azure-active-directory-or-on-premises-active-directory" class="xliff"></a>
Diese Lösung ist derzeit ein eigenständiges Angebot und ist weder ein Bestandteil von Azure Active Directory noch von lokalem Active Directory.

## Müssen eigene Regeln geschrieben und ein Schwellenwert/eine Basislinie erstellt werden?
<a id="do-you-have-to-write-your-own-rules-and-create-a-thresholdbaseline" class="xliff"></a>
Bei Microsoft Advanced Threat Analytics besteht keine Notwendigkeit zum Erstellen von Regeln, Schwellenwerten oder Basislinien und der anschließenden Optimierung. ATA analysiert das Verhalten von Benutzern, Geräten und Ressourcen – sowie deren Beziehungen untereinander – und kann verdächtige Aktivitäten und bekannte Angriffe schnell erkennen. Drei Wochen nach der Bereitstellung beginnt ATA, verdächtige Verhaltensaktivitäten zu erkennen. Bekannte Angriffe und Sicherheitsprobleme werden hingegen sofort nach der Bereitstellung von ATA erkannt.

## Wenn bei Ihnen bereits eine Sicherheitsverletzung aufgetreten ist, kann Microsoft Advanced Threat Analytics dann auch nicht normales Verhalten erkennen?
<a id="if-you-are-already-breached-will-microsoft-advanced-threat-analytics-be-able-to-identify-abnormal-behavior" class="xliff"></a>
Ja, selbst wenn ATA nach einer Sicherheitsverletzung installiert wird, kann ATA verdächtige Aktivitäten des Hackers erkennen. ATA überprüft nicht nur das Verhalten des einen Benutzers, sondern auch das der anderen Benutzer in der Sicherheitsstruktur der Organisation. Wenn das Verhalten des Angreifers während der ersten Analyse nicht normal ist, wird es als „Ausreißer“ identifiziert, und ATA fährt damit fort, das nicht normale Verhalten zu melden. Darüber hinaus kann ATA die verdächtige Aktivität erkennen, wenn der Hacker versucht, die Anmeldeinformationen eines anderen Benutzers zu stehlen, z.B. Pass-the-Ticket, oder wenn er versucht, eine Remoteausführung auf einem Domänencontroller durchzuführen.

## Wird nur Active Directory-Datenverkehr genutzt?
<a id="does-this-only-leverage-traffic-from-active-directory" class="xliff"></a>
Zusätzlich zur Analyse des Active Directory-Datenverkehrs mit der DPI-Technologie (Deep Packet Inspection) kann ATA auch relevante Ereignisse aus Ihrem SIEM-System (Security Information and Event Management) sammeln und Entitätenprofile auf Grundlage von Informationen aus Active Directory-Domänendiensten erstellen. ATA kann auch Ereignisse aus den Ereignisprotokollen erfassen, wenn die Organisation die Windows-Ereignisprotokollweiterleitung konfiguriert hat.

## Was ist Portspiegelung?
<a id="what-is-port-mirroring" class="xliff"></a>
Auch als SPAN (Switched Port Analyzer) bekannt, ist die Portspiegelung eine Methode zur Überwachung des Netzwerkverkehrs. Wenn die Portspiegelung aktiviert ist, sendet der Switch eine Kopie aller Netzwerkpakete von einem Port (oder einem gesamten VLAN) an einen anderen Port, an dem das Paket analysiert werden kann.

## Überwacht ATA nur Geräte, die der Domäne angehören?
<a id="does-ata-monitor-only-domain-joined-devices" class="xliff"></a>
Nein. ATA überwacht alle Geräte im Netzwerk und führt die Authentifizierung sowie Autorisierungsanfragen für Active Directory durch. Dies schließt Nicht-Windows-Geräte und mobile Geräte ein.

## Überwacht ATA sowohl Computerkonten als auch Benutzerkonten?
<a id="does-ata-monitor-computer-accounts-as-well-as-user-accounts" class="xliff"></a>
Ja. Da Computerkonten (ebenso wie alle anderen Entitäten) zum Durchführen böswilliger Aktivitäten verwendet werden können, überwacht ATA das Verhalten aller Computerkonten und aller weiteren Entitäten in der Umgebung.

## Kann ATA kann mehrere Domänen und mehrere Gesamtstrukturen unterstützen?
<a id="can-ata-support-multi-domain-and-multi-forest" class="xliff"></a>
Microsoft Advanced Threat Analytics unterstützt-Umgebungen mit mehreren Domänen innerhalb der gleichen Gesamtstrukturbegrenzung. Mehrere Gesamtstrukturen erfordern eine ATA-Bereitstellung für jede Gesamtstruktur.

## Kann die Gesamtintegrität der Bereitstellung angezeigt werden?
<a id="can-you-see-the-overall-health-of-the-deployment" class="xliff"></a>
Ja, Sie können die Gesamtintegrität der Bereitstellung sowie spezifische Probleme im Zusammenhang mit der Konfiguration, Konnektivität usw. anzeigen, und werden bei Eintreten eines Problems benachrichtigt.


## Weitere Informationen
<a id="see-also" class="xliff"></a>
- [Voraussetzungen für ATA](ata-prerequisites.md)
- [ATA-Kapazitätsplanung](ata-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-collection.md#configuring-windows-event-forwarding)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

