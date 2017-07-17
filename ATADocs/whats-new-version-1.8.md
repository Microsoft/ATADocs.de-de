---
title: Neuerungen in ATA Version 1.8 | Microsoft-Dokumentation
description: Listet Neuerungen sowie bekannte Probleme in ATA 1.8 auf.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/2/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 9592d413-df0e-4cec-8e03-be1ae00ba5dc
ms.reviewer: 
ms.suite: ems
ms.openlocfilehash: 6850c5e8e264a9610e377a9ab4aadca338971ee1
ms.sourcegitcommit: be6bdfa24a9b25a3375a4768d513b93900b3a498
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/11/2017
---
# Neuerungen in ATA 1.8
<a id="whats-new-in-ata-version-18" class="xliff"></a>

Die neueste Updateversion von ATA kann [aus dem Download Center heruntergeladen](https://www.microsoft.com/download/details.aspx?id=55536) werden. Die Vollversion kann aus dem [Evaluation Center](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics) heruntergeladen werden.

Die vorliegenden Anmerkungen zu dieser Version enthalten Informationen zu Updates, neuen Funktionen, Fehlerbehebungen und bekannten Problemen in dieser Version von Advanced Threat Analytics.



## Neue und aktualisierte Erkennung
<a id="new--updated-detections" class="xliff"></a>

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

## Verbesserte Selektierung von verdächtigen Aktivitäten
<a id="improved-triage-of-suspicious-activities" class="xliff"></a>

-   NEU! Mit ATA 1.8 können Sie die folgenden Aktionen für verdächtige Aktivitäten während des Selektierungsprozesses ausführen: 
    - **Ausschluss von Entitäten**: Sie können Entitäten ausschließen, die keine weiteren verdächtigen Aktivitäten verursachen sollen, damit ATA keine Warnungen mehr ausgibt, wenn es gutartige richtig positive Aktivitäten erkennt (wie z.B. ein Administrator, der remoten Code ausführt oder das Erkennen von Sicherheitsscannern).
    - **Unterdrücken des Warnens vor wiederholten** verdächtigen Aktivitäten.
    - **Löschen verdächtiger Aktivitäten** auf der Angriffszeitachse
-   Der Prozess des Nachverfolgens von Warnungen zu verdächtiger Aktivität ist jetzt effizienter. Die Zeitachse für verdächtige Aktivitäten wurde umgestaltet. In ATA 1.8 können Sie sich deutlich mehr verdächtige Aktivitäten auf einem Bildschirm anschauen. Diese enthalten ausführlichere Informationen zwecks Selektierung und Untersuchung. 

## Neue Berichte, um Sie bei der Untersuchung zu unterstützen
<a id="new-reports-to-help-you-investigate" class="xliff"></a> 
-   NEU! Der **Zusammenfassungsbericht** wurde hinzugefügt, damit Sie sich alle zusammengefassten Daten von ATA anschauen können, einschließlich verdächtiger Aktivitäten, Integritätsproblemen usw. Sie können sogar einen benutzerdefinierten Bericht definieren, der automatisch periodisch neu erstellt wird.
-   NEU! Der **Bericht zu sensiblen Gruppen** wurde hinzugefügt, damit Sie sich alle Änderungen an sensiblen Gruppen über einen bestimmten Zeitraum anschauen können.


## Verbesserungen der Infrastruktur
<a id="infrastructure-improvements" class="xliff"></a>

-   Die Leistung von ATA Center wurde verbessert. In ATA 1.8 kann ATA Center per als 1 Mio. Pakete in der Sekunde behandeln.
-   Das ATA-Lightweight-Gateway kann jetzt Ereignisse lokal lesen, ohne die Ereignisweiterleitung zu konfigurieren.
-   Sie können jetzt E-Mails für Überwachungsbenachrichtigungen und verdächtige Aktivitäten getrennt konfigurieren.

## Sicherheitsverbesserungen
<a id="security-improvements" class="xliff"></a>

-   NEU! **Einmalige Anmeldung für die Verwaltung von ATA** ATA unterstützt die in die Windows-Authentifizierung integrierte einmalige Anmeldung: wenn Sie sich schon bei Ihrem Computer angemeldet haben, verwenden ATA das Token, um Sie in der ATA-Konsole anzumelden. Sie können sich auch mit einer Smartcard anmelden. Stille Installationsskripts für das ATA-Gateway und das ATA-Lightweight-Gateway verwenden jetzt den Kontext des angemeldeten Benutzers, ohne Anmeldeinformationen eingeben zu müssen.
-   Berechtigungen für das lokale System wurden aus dem ATA-Gatewayprozess entfernt, damit Sie virtuelle Konten (nur in eigenständigen ATA-Gateways verfügbar), verwaltete Dienstkonten und gruppenverwaltete Dienstkonten verwenden können, um den ATA-Gatewayprozess auszuführen.   
-   Überwachungsprotokolle für ATA Center und Gateways wurden hinzugefügt, und alle Aktionen werden jetzt im Windows-Ereignisprotokoll erfasst.
-   Die Unterstützung für KSP-Zertifikate für ATA Center wurde hinzugefügt.




## Siehe auch
<a id="see-also" class="xliff"></a>
[Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Aktualisieren von ATA auf Version 1.8: Migrationshandbuch](ata-update-1.8-migration-guide.md)

