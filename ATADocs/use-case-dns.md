---
title: Untersuchen der Reconnaissance mithilfe von DNS | Microsoft-Dokumentation
description: "In diesem Artikel wird die Reconnaissance mit DNS beschrieben. Außerdem erhalten Sie Anweisungen zu Untersuchungen, wenn eine derartige Bedrohung von ATA erkannt wird."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/4/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d186a96-ef70-4787-aa64-c03d1db94ce0
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 436b96f679836060cfaf40f6be3b92cf96dc0e04
ms.sourcegitcommit: 4118dd4bd98994ec8a7ea170b09aa301a4be2c8a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/05/2017
---
*Gilt für: Advanced Threat Analytics Version 1.8*

# Untersuchen der Reconnaissance mithilfe von DNS
<a id="investigating-reconnaissance-using-dns" class="xliff"></a>

Wenn ATA **Reconnaissance mithilfe von DNS** auf Ihrem Netzwerk erkennt und Sie daraufhin warnt, verwenden Sie diesen Artikel, um die Warnung zu untersuchen und zu verstehen, wie das Problem gelöst werden kann.

## Was ist Reconnaissance mithilfe von DNS?
<a id="what-is-reconnaissance-using-dns" class="xliff"></a>

Die Warnung **Reconnaissance mithilfe von DNS** gibt an, dass verdächtige Domain Name System-Abfragen (DNS) von einem ungewöhnlichen Host durchgeführt werden, um Reconnaissance auf Ihrem internen Netzwerk durchzuführen.

Das Domain Name System (DNS) ist ein Dienst, der als hierarchische, verteilte Datenbank implementiert wird, die die Auflösung von Hostnamen und Domänennamen bereitstellt. Die Namen in einer DNS-Datenbank bilden eine hierarchische Baumstruktur, genannt Domänennamespace.
Für einen Angreifer enthält Ihr DNS wertvolle Informationen über die Zuordnung eines internen Netzwerks, einschließlich einer Liste aller Server und auch oft aller Clients, die Ihren IP-Adressen zugeordnet sind. Des Weiteren sind diese Informationen von Wert, da Hostnamen aufgelistet werden, die oft in einer gegebenen Netzwerkumgebung beschreibend sind. Durch Abrufen dieser Information kann ein Angreifer den Aufwand für die relevanten Entitäten während einer Kampagne besser priorisieren. Tools, z.B. [Nmap](https://nmap.org/), [Fierce](https://github.com/mschwager/fierce), und integrierte Tools wie [Nslookup](https://technet.microsoft.com/library/cc725991(v=ws.11).aspx) bieten Funktionen für die Hostermittlung mithilfe der DNS-Reconnaissance.
Die Erkennung von Reconnaissance mithilfe von DNS-Abfragen von einem internen Host ist besorgniserregend und zeigt einen möglichen Angriff auf vorhandene Hosts, einen Angriff auf das weitere Netzwerk oder die Möglichkeit einer Bedrohung von Innen.

## DNS-Abfragetypen
<a id="dns-query-types" class="xliff"></a>

Es gibt mehrere Abfragetypen im DNS-Protokoll. ATA erkennt die AXFR-Anfragen (Transfer) und erstellt eine Warnung, wenn diese ermittelt werden. Dieser Abfragetyp darf nur von DNS-Servern stammen.

## Erkennen des Angriffs
<a id="discovering-the-attack" class="xliff"></a>

Wenn ein Angreifer versucht, Reconnaissance mithilfe von DNS auszuführen, erkennt ATA dies und kennzeichnet den Angriff mit mittleren Schweregrad.

![ATA erkennt DNS-Reconnaissance](./media/dns-recon.png)
 
ATA zeigt den Namen des Quellcomputers sowie zusätzliche Details über die eigentliche DNS-Abfrage, die ausgeführt wurde. Es könnten z.B. mehrere Versuche vom selben Host ausgegangen sein.

## Untersuchung
<a id="investigating" class="xliff"></a>

Um Reconnaissance mithilfe von DNS zu untersuchen, müssen Sie zuerst den Grund der Abfragen bestimmen. Diese können mit einer der folgenden Kategorien identifiziert werden: 
-   Wahr positiv: Es gibt einen Angreifer oder böswillige Schadsoftware auf Ihrem Netzwerk. Dies kann ein Angreifer sein, der eine Sicherheitsverletzung des Netzwerkperimeters ausgelöst hat, oder eine Bedrohung von Innen.
-   Unbedenklich wahr positiv: Dies können Warnungen sein, die durch Prüfen von Stiften, Team Rot-Aktivität, Sicherheitsscanner, eine Firewall der nächsten Generation oder IT-Administratoren, die sanktionierte Aktivitäten ausgeführt haben, ausgelöst wurden.
-   Falsch positiv: Sie erhalten womöglich Warnungen, die aufgrund einer Fehlkonfiguration aufgetreten sind, z.B: wenn Port 53 zwischen dem ATA-Gateway und Ihrem DNS-Server blockiert ist (oder ein anderes Netzwerkproblem).

Folgendes Diagramm hilft Ihnen dabei, zu bestimmen, welche Schritte sie durchführen müssen:

![Auflösen der DNS-Reconnaissance mit ATA](./media/dns-recon-diagram.png)
 
1.  Der erste Schritt ist, den Computer zu identifizieren, von dem die Warnung stammt, so wie unten dargestellt:
 
    ![Anzeigen der verdächtigen DNS-Reconnaissance-Aktivität in ATA](./media/dns-recon-2.png)
2.  Identifizieren Sie den Computer. Ist der Computer eine Arbeitsstation, ein Server, eine Administratorarbeitsstation, eine Station zum Prüfen von Stiften usw.?
3.  Wenn es sich um einen DNS-Server handelt, der legitime Rechte zum Anfordern einer zweiten Kopie der Zone hat, dann ist dies ein falsch-positiver-Fall. Wenn Sie einen falsch-positiven-Fall haben, verwenden Sie die Option **Ausschließen**, damit Sie diese bestimmte Warnung für diesen Computer nicht noch einmal erhalten.
4. Stellen Sie sicher, dass Port 53 zwischen dem ATA-Gateway und Ihrem DNS-Server geöffnet ist.
4.  Wenn der Computer für administrative Arbeit oder zur Stifteprüfung verwendet wird, ist es unbedenklicher wahr-positiv-Fall, und der betroffene Computer kann auch als Ausnahme betrachtet werden.
5.  Wenn er nicht für die Stifteprüfung verwendet wird, untersuchen Sie, ob der Computer in einem Sicherheitsscanner oder einer Firewall der nächsten Generation ausgeführt wird, was zu DNS-Anforderungen vom Typ AXFR führen kann.
6.  Wenn schließlich keine diese Kriterien erfüllt werden, besteht die Möglichkeit, dass der Computer kompromittiert ist und vollständig untersucht werden muss. 
7.  Wenn die Anfragen für bestimmte Computer isoliert sind und nicht unbedenklich sind, müssen die folgenden Schritte durchgegangen werden:
    1.  Überprüfen Sie die verfügbaren Protokollquellen. 
    2.  Führen Sie die hostbasierte Analyse durch. 
    3.  Wenn die Aktivität nicht von einem verdächtigen Benutzer ausgeführt wurde, muss die Analyse auf dem Computer durchgeführt werden, um zu bestimmen, ob dieser mit Schadsoftware kompromittiert wurde.

## Nach der Untersuchung
<a id="post-investigation" class="xliff"></a>

Schadsoftware, die zur Kompromittierung des Hosts verwendet wird, kann Trojaner mit Hintertürfunktionen enthalten. In Fällen, in denen eine seitliche Verschiebung im kompromittierten Host identifiziert wurde, müssen Herstellungsaktionen für diese Hosts ausgeweitet werden, einschließlich der Änderung der Kennwörter und Anmeldeinformationen, die auf dem Host und jedem anderen Host verwendet wird, der sich in der seitlichen Verschiebung befindet. 

In Fällen, in denen der Opferhost nicht ordnungsgemäß bereinigt nach den Schritten zur Wiederherstellung wurde, oder eine Grundursache der Kompromittierung nicht gefunden werden kann, empfiehlt Microsoft, die Sicherung der kritischen Daten und die Wiederherstellung des Hostcomputers. Zusätzlich müssen neue oder wiederhergestellte Hosts verstärkt werden, bevor Sie zurück auf dem Netzwerk platziert werden, sodass keine erneute Infizierung auftreten kann. 

Es wird von Microsoft empfohlen, ein professionelles Team zur Reaktion auf Sicherheitsfälle und zur Wiederherstellung einzusetzen, das Sie über das Microsoft-Kontoteam erreichen können. Dieses kann Ihnen dabei helfen, zu erkennen, ob ein Angreifer eine Persistenzmethode in Ihrem Netzwerk bereitgestellt hat.

## Maßnahme
<a id="mitigation" class="xliff"></a>

Die Sicherung eines internen DNS-Servers, um zu verhindern, dass Reconnaissance mithilfe von DNS auftritt, kann von der Deaktivierung oder Einschränkung von Zonenübertragungen nur auf bestimmte IP-Adressen erreicht werden. Zusätzliche Informationen zum Beschränken der Zonenübertragung finden Sie im Windows Server-TechNet-Artikel [Restrict Zone Transfers (Beschränken von Zonenübertragungen)](https://technet.microsoft.com/library/ee649273(v=ws.10).aspx). Beschränkte Zonenübertragungen können weiterhin durch die [Sicherung von Zonenübertragungen mithilfe von IPsec](https://technet.microsoft.com/library/ee649192(v=ws.10).aspx) gesperrt werden. Das Bearbeiten von Zonenübertragungen ist eine Aufgabe innerhalb einer Prüfliste, die für [Sichern des DNS-Servers gegen interne und externe Angriffe](https://technet.microsoft.com/library/cc770432(v=ws.11).aspx) gelten sollte.



## Siehe auch
<a id="see-also" class="xliff"></a>
- [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
