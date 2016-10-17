---
title: Was ist Microsoft Advanced Threat Analytics (ATA)? | Microsoft ATA
description: "Hier wird erläutert, was Microsoft Advanced Threat Analytics (ATA) ist und welche Arten von verdächtigen Aktivitäten erkannt werden können"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 09/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 3768cd103fc2a938d2d39fe34179d74587abc118
ms.openlocfilehash: 0bc2bcc42b2b59cf297b4af86f0c38aafebc379f


---

*Gilt für: Advanced Threat Analytics Version 1.7*


## Was ist Advanced Threat Analytics?
Advanced Threat Analytics (ATA) ist eine lokale Plattform, mit deren Hilfe Sie Ihr Unternehmen vor verschiedenen hochentwickelten und gezielten Cyberangriffen und Insiderbedrohungen schützen können.

## So funktioniert ATA
ATA bezieht aus mehreren Datenquellen wie Protokollen und Ereignissen in Ihrem Netzwerk Informationen, um das Verhalten von Benutzern und anderen Personen in der Organisation zu lernen und anschließend ein Verhaltensprofil zu erstellen.
ATA kann Ereignisse und Protokolle aus folgenden Quellen beziehen:

-   SIEM-Integration
-   Windows-Ereignisweiterleitung (Windows Event Forwarding; WEF)

Darüber hinaus nutzt ATA ein proprietäres Netzwerkanalysemodul, um den Netzwerkverkehr verschiedener Protokolle (z.B. Kerberos, DNS, RPC, NTLM und andere) zwecks Authentifizierung, Autorisierung und zum Sammeln von Informationen zu erfassen und zu analysieren. ATA sammelt die Informationen über:

-   die Portspiegelung von Domänencontrollern und DNS-Servern bis zum ATA-Gateway.
-   die direkt Bereitstellung eines ATA-Lightweight-Gateways (LGW) auf Domänencontrollern.

Weitere Informationen zur ATA-Architektur finden Sie unter [ATA-Architektur](/advanced-threat-analytics/plan-design/ata-architecture).

## Wie funktioniert ATA?

Die ATA-Technologie erkennt verschiedene verdächtige Aktivitäten und konzentriert sich dabei auf die verschiedenen Phasen der Angriffskette von Cyber-Angriffen, so z.B.:

-   Die Reconnaissance: Die Angreifer sammeln Informationen über die Bauweise der Umgebung und die unterschiedlichen, vorhandenen Ressourcen und Entitäten und erstellen ihren Plan für die nächsten Angriffsphasen.
-   Der Zyklus der Seitwärtsbewegung: Die Angreifer investieren Zeit und Mühe in die Verbreiterung ihrer Angriffsfläche in Ihrem Netzwerk.
-   Domänendominanz (-persistenz): Die Angreifer sammeln die Informationen, mithilfe derer sie ihren Angriff fortsetzen und dabei eine Vielzahl von Einstiegspunkten, Anmeldeinformationen und Techniken anwenden können. 

Diese Phasen eines Cyberangriffs ähneln sich und sind vorhersagbar, unabhängig davon, welche Art von Unternehmen angegriffen oder auf welche Art von Informationen abgezielt wird.
ATA sucht nach drei Haupttypen von Angriffen: böswillige Angriffe, ungewöhnliches/nicht normales Verhalten und Sicherheitsprobleme und -risiken.

**Böswillige Angriffe** werden deterministisch erkannt, indem nach der vollständigen Liste bekannter Angriffstypen gesucht wird, wie z.B.:

-   Pass-the-Ticket (PtT)
-   Pass-the-Hash (PtH)
-   Overpass-the-Hash
-   Forged PAC (MS14-068)
-   Golden Ticket
-   Böswillige Replikationen
-   Reconnaissance
-   Brute-Force-Angriffe
-   Remoteausführung

Eine vollständige Liste der Erkennungstypen und deren Beschreibungen finden Sie unter [What Suspicious Activities Can ATA detect?](ata-threats.md) (Welche verdächtigen Aktivitäten kann ATA erkennen?).
ATA erkennt diese verdächtigen Aktivitäten und zeigt Informationen dazu in der ATA-Konsole an, einschließlich einer Übersicht darüber, wer den Angriff wann und wie ausgeführt hat und was dabei geschehen ist. Durch die Überwachung dieses einfachen und benutzerfreundlichen Dashboards werden Sie also benachrichtigt, wenn ATA vermutet, dass ein Pass-the-Hash-Angriff auf die Computer Client 1 und Client 2 in Ihrem Netzwerk versucht wurde.

 ![sample ATA screen pass-the-hash](media/sample screen pth.png)

**ungewöhnliches/nicht normales Verhalten** wird von ATA mithilfe der Verhaltensanalyse und Machine Learning erkannt. So werden fragwürdige Aktivitäten und ungewöhnliches/nicht normales Verhalten wie von Benutzern und Geräten in Ihrem Netzwerk wie die folgenden erkannt:

-   Nicht normale Anmeldungen
-   Unbekannte Gefahren
-   Kennwortfreigabe
-   Seitliche Verschiebung


Sie können die verdächtigen Aktivitäten dieses Typs im ATA-Dashboard anzeigen. Im folgenden Beispiel benachrichtigt Sie ATA, wenn ein Benutzer auf 4 Computer zugreift, die in der Regel nicht von diesem Benutzer verwendet werden. Dies kann Anlass zur Sorge geben.

 ![sample ATA screen abnormal behavior](media/sample screen abnormal behavior.png) 

ATA erkennt darüber hinaus **Sicherheitsprobleme und -risiken**, einschließlich:

-   einer fehlerhaften Vertrauensstellung
-   schwacher Protokolle
-   bekannter Protokollschwachstellen.

Sie können die verdächtigen Aktivitäten dieses Typs im ATA-Dashboard anzeigen. Im folgenden Beispiel weist Sie ATA darauf hin, dass eine fehlerhafte Vertrauensstellung zwischen einem Computer in Ihrem Netzwerk und der Domäne vorhanden ist.

  ![sample ATA screen broken trust](media/sample screen broken trust.png)


## Wie geht es weiter?

-   Weitere Informationen zum Integrieren von ATA in Ihr Netzwerk: [ATA-Architektur](/advanced-threat-analytics/plan-design/ata-architecture)

-   Erste Schritte bei der Bereitstellung von ATA: [Installieren von ATA](/advanced-threat-analytics/deploy-use/install-ata)

## Weitere Informationen
[Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Oct16_HO2-->


