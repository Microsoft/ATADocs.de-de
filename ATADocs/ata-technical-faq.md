---
title: Häufig gestellte Fragen zu Advanced Threat Analytics | Microsoft-Dokumentation
description: Liste häufig gestellter Fragen zu ATA und zugehörige Antworten
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/6/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: a7d378ec-68ed-4a7b-a0db-f5e439c3e852
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: c28783170764c117a07fa19946c83638f24dc1a6
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166492"
---
*Gilt für: Advanced Threat Analytics Version 1.9*

# <a name="ata-frequently-asked-questions"></a>Häufig gestellte Fragen zu ATA
Dieser Artikel enthält eine Reihe häufig gestellter Fragen zu ATA sowie Hintergrundwissen und Antworten.


## <a name="where-can-i-get-a-license-for-advanced-threat-analytics-ata"></a>Wo erhalte ich eine Lizenz für Advanced Threat Analytics (ATA)?

Wenn Sie über ein aktives Enterprise Agreement verfügen, können Sie die Software aus dem Microsoft Volume Licensing Center (VLSC) herunterladen.

Wenn Sie eine Lizenz für Enterprise Mobility + Security (EMS) direkt über das Office 365-Portal oder über das Cloud Solution Partner-Lizenzmodell (CSP) erworben haben, und Sie keinen Zugriff auf ATA über das Microsoft Volume Licensing Center (VLSC) verfügen, kontaktieren Sie den Microsoft-Kundendienst, um den Prozess zum Aktivieren von Advanced Threat Analytics (ATA) abzurufen.

## <a name="what-should-i-do-if-the-ata-gateway-wont-start"></a>Das ATA-Gateway startet nicht. Wie sollte ich vorgehen?
Sehen Sie sich den letzten Fehlereintrag im aktuellen Fehlerprotokoll an (Installationsverzeichnis von ATA unter dem Ordner „Logs“).

## <a name="how-can-i-test-ata"></a>Wie kann ich ATA testen?
Sie können einen End-to-End-Test durchführen und verdächtige Aktivitäten simulieren. Führen Sie dazu eine der folgenden Aktionen aus:

1.  DNS-Reconnaissance durch Verwendung von „Nslookup.exe“
2.  Remoteausführung durch Verwendung von „psexec.exe“


Dies muss remote für den überwachten Domänencontroller und nicht über das ATA-Gateway ausgeführt werden.

## <a name="which-ata-build-corresponds-to-each-version"></a>Welcher ATA-Build entspricht der jeweiligen Version?

Weitere Informationen zum Upgrade der Version finden Sie unter [ATA-Upgradepfad](upgrade-path.md).

## <a name="what-version-should-i-use-to-upgrade-my-current-ata-deployment-to-the-latest-version"></a>Welche Version soll ich verwenden, um meine aktuelle ATA-Bereitstellung auf die neueste Version upzugraden?

Weitere Informationen zur Matrix zum Upgrade der ATA-Version finden Sie unter [ATA-Upgradepfad](upgrade-path.md).


## <a name="how-does-the-ata-center-update-its-latest-signatures"></a>Wie aktualisiert das ATA Center seine neuesten Signaturen?

Der ATA-Erkennungsmechanismus wird erweitert, wenn eine neue Version im ATA Center installiert wird. Sie können ein Upgrade für das Center entweder über Microsoft Update (MU) durchführen, oder indem Sie manuell die neueste Version aus dem Download Center oder von der Volume License-Website herunterladen.

## <a name="how-do-i-verify-windows-event-forwarding"></a>Wie kann ich die Windows-Ereignisweiterleitung überprüfen?
Sie können den folgenden Code in einer Datei ablegen und ihn dann über eine Eingabeaufforderung im Verzeichnis **\Programme\Microsoft Advanced Threat Analytics\Center\MongoDB\bin** wie folgt ausführen:

ATA-Dateiname mongo.exe

        db.getCollectionNames().forEach(function(collection) {
        if (collection.substring(0,10)=="NtlmEvent_") {
                if (db[collection].count() > 0) {
                                  print ("Found "+db[collection].count()+" NTLM events") 
                                }
                }
        });

## <a name="does-ata-work-with-encrypted-traffic"></a>Funktioniert ATA mit verschlüsseltem Datenverkehr?
ATA analysiert mehrere Netzwerkprotokolle sowie von SIEM oder der Windows-Ereignisweiterleitung erfasste Ereignisse. Erkennungen auf Grundlage von Netzwerkprotokollen mit verschlüsseltem Datenverkehr (z.B. LDAPS und IPSEC) werden nicht analysiert.


## <a name="does-ata-work-with-kerberos-armoring"></a>Funktioniert ATA mit Kerberos Armoring?
Die Aktivierung von Kerberos Armoring (auch als Flexible Authentication Secure Tunneling (FAST) bezeichnet) wird von ATA unterstützt. Einzige Ausnahme ist die Overpass-The-Hash-Erkennung, die nicht unterstützt wird.

## <a name="how-many-ata-gateways-do-i-need"></a>Wie viele ATA-Gateways benötige ich?

Die Anzahl der ATA-Gateways hängt von Ihrem Netzwerklayout, der Menge der Pakete und der Anzahl der Ereignisse ab, die von ATA erfasst werden. Lesen Sie den Abschnitt [Größenzuteilung für ATA Center](ata-capacity-planning.md#ata-lightweight-gateway-sizing), um die genaue Anzahl zu ermitteln. 

## <a name="how-much-storage-do-i-need-for-ata"></a>Wie viel Speicher benötige ich für ATA?
Für jeden ganzen Tag mit durchschnittlich 1000 Paketen/Sekunde sind 0,3 GB Speicher erforderlich.<br /><br />Weitere Informationen zur Dimensionierung von ATA Center finden Sie unter [ATA-Kapazitätsplanung](ata-capacity-planning.md).


## <a name="why-are-certain-accounts-considered-sensitive"></a>Warum gelten bestimmte Konten als sensible Konten?
Dies ist der Fall, wenn ein Konto bestimmten Gruppen angehört, die als sensibel festgelegt sind (z. B. „Domänen-Admins“).

Um nachzuvollziehen, warum ein Konto ein sensibles Konto ist, können Sie seine Gruppenmitgliedschaft überprüfen, um festzustellen, welchen sensiblen Gruppen es angehört (die Gruppe, der das Konto angehört, kann auch wegen einer anderen Gruppe eine sensible Gruppe sein. Daher sollten Sie immer die höchste sensible Gruppe überprüfen). 

Außerdem können Sie manuell einen Benutzer, eine Gruppe oder einen Computer als vertraulich markieren. Weitere Informationen finden Sie unter [Tag sensitive accounts (Markieren von vertraulichen Konten)](tag-sensitive-accounts.md).

## <a name="how-do-i-monitor-a-virtual-domain-controller-using-ata"></a>Wie kann ich einen virtuellen Domänencontroller mit ATA überwachen?
Die meisten virtuellen Domänencontroller können vom ATA-Lightweight-Gateway abgedeckt werden. Um festzustellen, ob das ATA-Lightweight-Gateway sich für Ihre Umgebung eignet, lesen Sie die Informationen unter [ATA-Kapazitätsplanung](ata-capacity-planning.md).

Wenn ein virtueller Domänencontroller nicht durch das ATA-Lightweight-Gateway abgedeckt werden kann, können Sie ein virtuelles oder physisches ATA-Gateway verwenden, wie unter [Konfigurieren der Portspiegelung](configure-port-mirroring.md) beschrieben.  <br />Die einfachste Möglichkeit ist jeweils ein virtuelles ATA-Gateway auf jedem Host, auf dem ein virtueller Domänencontroller vorhanden ist.<br />Wenn die virtuellen Domänencontroller zwischen Hosts verschoben werden, müssen Sie einen der folgenden Schritte ausführen:

-   Wenn der virtuelle Domänencontroller auf einen anderen Host verschoben wird, konfigurieren Sie das ATA-Gateway auf diesem Host so vor, dass der Datenverkehr von dem zuvor verschobenen virtuellen Domänencontroller empfangen wird.
-   Stellen Sie sicher, dass Sie das virtuelle ATA-Gateway dem virtuellen Domänencontroller zuordnen, sodass das ATA-Gateway ggf. mit dem Controller verschoben wird.
-   Es gibt einige virtuelle Switches, über die der Datenverkehr zwischen Hosts gesendet werden kann.

## <a name="how-do-i-back-up-ata"></a>Wie kann ich ATA sichern?

Informationen finden Sie unter [ATA-Notfallwiederherstellung](disaster-recovery.md)



## <a name="what-can-ata-detect"></a>Was kann ATA erkennen?

ATA erkennt bekannte Angriffe und Techniken, Sicherheitsprobleme und Risiken.
Die vollständige Liste der ATA-Erkennungen finden Sie unter [Welche Bedrohungen erkennt ATA?](ata-threats.md).

## <a name="what-kind-of-storage-do-i-need-for-ata"></a>Welche Art von Speicher benötige ich für ATA?
Wir empfehlen ein schnelles Speichermedium (Datenträger mit 7200 U/min werden nicht empfohlen) mit Datenträgerzugriff mit niedriger Latenz (weniger als 10 ms). Die RAID-Konfiguration sollte hohe Schreiblasten unterstützen (RAID-5/6 und zugehörige Ableitungen werden nicht empfohlen).

## <a name="how-many-nics-does-the-ata-gateway-require"></a>Wie viele Netzwerkkarten sind für das ATA-Gateway erforderlich?
Für das ATA-Gateway sind mindestens zwei Netzwerkkarten erforderlich:<br>1. Eine Netzwerkkarte für die Verbindung mit dem internen Netzwerk und ATA Center.<br>2. Eine Netzwerkschnittstelle zum Erfassen des Netzwerkdatenverkehrs des Domänencontrollers über Portspiegelung.<br>* Dies gilt nicht für das ATA-Lightweight-Gateway, das systemintern alle Netzwerkadapter verwendet, die der Domänencontroller verwendet.

## <a name="what-kind-of-integration-does-ata-have-with-siems"></a>Welche Art der Integration weist ATA mit SIEMs auf?
ATA weist eine bidirektionale Integration mit SIEMs auf:

1. ATA kann so konfiguriert werden, dass bei Feststellung einer verdächtigen Aktivität eine Syslog-Warnung an einen SIEM-Server gesendet wird, der das CEF-Format verwendet.
2. ATA kann so konfiguriert werden, dass für jedes Windows-Ereignis Syslog-Meldungen von [diesen SIEMs](install-ata-step6.md) empfangen werden.

## <a name="can-ata-monitor-domain-controllers-virtualized-on-your-iaas-solution"></a>Kann ATA in Ihrer IaaS-Lösung virtualisierte Domänencontroller überwachen?
Ja, Sie können mit dem ATA-Lightweight-Gateway Domänencontroller in einer beliebigen IaaS-Lösung überwachen.

## <a name="is-this-an-on-premises-or-in-cloud-offering"></a>Wird das Produkt lokal oder in der Cloud angeboten?
Microsoft Advanced Threat Analytics ist ein lokales Produkt.

## <a name="is-this-going-to-be-a-part-of-azure-active-directory-or-on-premises-active-directory"></a>Wird das Produkt ein Bestandteil von Azure Active Directory oder von lokalem Active Directory sein?
Diese Lösung ist derzeit ein eigenständiges Angebot und ist weder ein Bestandteil von Azure Active Directory noch von lokalem Active Directory.

## <a name="do-you-have-to-write-your-own-rules-and-create-a-thresholdbaseline"></a>Müssen eigene Regeln geschrieben und ein Schwellenwert/eine Basislinie erstellt werden?
Bei Microsoft Advanced Threat Analytics besteht keine Notwendigkeit zum Erstellen von Regeln, Schwellenwerten oder Basislinien und der anschließenden Optimierung. ATA analysiert das Verhalten von Benutzern, Geräten und Ressourcen – sowie deren Beziehungen untereinander – und kann verdächtige Aktivitäten und bekannte Angriffe schnell erkennen. Drei Wochen nach der Bereitstellung beginnt ATA, verdächtige Verhaltensaktivitäten zu erkennen. Bekannte Angriffe und Sicherheitsprobleme werden hingegen sofort nach der Bereitstellung von ATA erkannt.

## <a name="if-you-are-already-breached-can-microsoft-advanced-threat-analytics-identify-abnormal-behavior"></a>Kann Microsoft Advanced Threat Analytics auch dann nicht normales Verhalten erkennen, wenn bei Ihnen bereits eine Sicherheitsverletzung aufgetreten ist?
Ja, selbst wenn ATA nach einer Sicherheitsverletzung installiert wird, kann ATA verdächtige Aktivitäten des Hackers erkennen. ATA überprüft nicht nur das Verhalten des einen Benutzers, sondern auch das der anderen Benutzer in der Sicherheitsstruktur der Organisation. Wenn das Verhalten des Angreifers während der ersten Analyse nicht normal ist, wird es als „Ausreißer“ identifiziert, und ATA fährt damit fort, das nicht normale Verhalten zu melden. Darüber hinaus kann ATA die verdächtige Aktivität erkennen, wenn der Hacker versucht, die Anmeldeinformationen eines anderen Benutzers zu stehlen, z.B. Pass-the-Ticket, oder wenn er versucht, eine Remoteausführung auf einem Domänencontroller durchzuführen.

## <a name="does-this-only-leverage-traffic-from-active-directory"></a>Wird nur Active Directory-Datenverkehr genutzt?
Zusätzlich zur Analyse des Active Directory-Datenverkehrs mit der DPI-Technologie (Deep Packet Inspection) kann ATA auch relevante Ereignisse aus Ihrem SIEM-System (Security Information and Event Management) sammeln und Entitätenprofile auf Grundlage von Informationen aus Active Directory-Domänendiensten erstellen. ATA kann auch Ereignisse aus den Ereignisprotokollen erfassen, wenn die Organisation die Windows-Ereignisprotokollweiterleitung konfiguriert hat.

## <a name="what-is-port-mirroring"></a>Was ist Portspiegelung?
Auch als SPAN (Switched Port Analyzer) bekannt, ist die Portspiegelung eine Methode zur Überwachung des Netzwerkverkehrs. Wenn die Portspiegelung aktiviert ist, sendet der Switch eine Kopie aller Netzwerkpakete von einem Port (oder einem gesamten VLAN) an einen anderen Port, an dem das Paket analysiert werden kann.

## <a name="does-ata-monitor-only-domain-joined-devices"></a>Überwacht ATA nur Geräte, die der Domäne angehören?
Nein. ATA überwacht alle Geräte im Netzwerk und führt die Authentifizierung sowie Autorisierungsanfragen für Active Directory durch. Dies schließt Nicht-Windows-Geräte und mobile Geräte ein.

## <a name="does-ata-monitor-computer-accounts-as-well-as-user-accounts"></a>Überwacht ATA sowohl Computerkonten als auch Benutzerkonten?
Ja. Da Computerkonten (ebenso wie alle anderen Entitäten) zum Durchführen böswilliger Aktivitäten verwendet werden können, überwacht ATA das Verhalten aller Computerkonten und aller weiteren Entitäten in der Umgebung.

## <a name="can-ata-support-multi-domain-and-multi-forest"></a>Kann ATA kann mehrere Domänen und mehrere Gesamtstrukturen unterstützen?
Microsoft Advanced Threat Analytics unterstützt-Umgebungen mit mehreren Domänen innerhalb der gleichen Gesamtstrukturbegrenzung. Mehrere Gesamtstrukturen erfordern eine ATA-Bereitstellung für jede Gesamtstruktur.

## <a name="can-you-see-the-overall-health-of-the-deployment"></a>Kann die Gesamtintegrität der Bereitstellung angezeigt werden?
Ja, Sie können die Gesamtintegrität der Bereitstellung sowie spezifische Probleme im Zusammenhang mit der Konfiguration, Konnektivität usw. anzeigen und werden bei Eintreten eines Problems benachrichtigt.


## <a name="see-also"></a>Weitere Informationen
- [Voraussetzungen für ATA](ata-prerequisites.md)
- [ATA-Kapazitätsplanung](ata-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-collection.md#configuring-windows-event-forwarding)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

