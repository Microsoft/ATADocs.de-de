---
title: Was ist Azure Advanced Threat Protection (ATP)? | Microsoft-Dokumentation
description: "Hier wird erläutert, worum es sich bei Azure Advanced Threat Protection (ATP) handelt und welche Arten von verdächtigen Aktivitäten erkannt werden können"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 2d14d0e9-1b03-4bcc-ae97-8fd41526ffc5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 5ccac90a171c895ee8b4d5336a125ccd7fa66239
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/21/2018
---
*Gilt für: Azure Advanced Threat Protection*


# <a name="what-is-azure-advanced-threat-protection"></a>Was ist Azure Advanced Threat Protection?
Bei Azure Advanced Threat Protection (ATP) handelt es sich um einen Clouddienst, mit dem Sie Ihre hybriden Unternehmensumgebungen vor verschiedenen hochentwickelten und gezielten Cyberangriffen und Bedrohungen von innen schützen können.

## <a name="how-azure-atp-works"></a>Wie funktioniert Azure ATP?

Azure ATP nutzt ein proprietäres Netzwerkanalysemodul, um den Netzwerkverkehr verschiedener Protokolle (z.B. Kerberos, DNS, RPC, NTLM und andere) zwecks Authentifizierung, Autorisierung und zum Sammeln von Informationen zu erfassen und zu analysieren. Azure ATP sammelt die Informationen über:

-   die Bereitstellung von Azure ATP-Sensoren direkt über Ihre Domänencontroller
-   die Portspiegelung von Domänencontrollern und DNS-Servern bis zum eigenständigen Azure ATP-Sensor

Azure ATP bezieht aus mehreren Datenquellen wie Protokollen und Ereignissen in Ihrem Netzwerk Informationen, um das Verhalten von Benutzern und anderen Personen in der Organisation zu erfassen und anschließend ein Verhaltensprofil zu erstellen.
Azure ATP kann Ereignisse und Protokolle aus folgenden Quellen beziehen:

-   SIEM-Integration
-   Windows-Ereignisweiterleitung (Windows Event Forwarding; WEF)
-   Direkt aus der Windows-Ereignissammlung (für den Sensor)
-   RADIUS-Kontoführung über VPN


Weitere Informationen zur Azure ATP-Architektur finden Sie unter [Azure ATP-Architektur](atp-architecture.md).

## <a name="what-does-azure-atp-do"></a>Was bewirkt Azure ATP?

Die Azure ATP-Technologie erkennt verschiedene verdächtige Aktivitäten und konzentriert sich dabei auf die verschiedenen Phasen der Angriffskette von Cyberangriffen, so z.B.:

-   Reconnaissance, während der die Angreifer Informationen zum Aufbau der Umgebung, zu den verschiedenen Assets und zu den vorhandenen Entitäten erfassen. Sie erstellen ganz allgemein einen Plan für die nächsten Phasen ihres Angriffs.
-   Der Zyklus der Seitwärtsbewegung: Die Angreifer investieren Zeit und Mühe in die Verbreiterung ihrer Angriffsfläche in Ihrem Netzwerk.
-   Domänendominanz (-persistenz): Die Angreifer sammeln die Informationen, mithilfe derer sie ihren Angriff fortsetzen und dabei eine Vielzahl von Einstiegspunkten, Anmeldeinformationen und Techniken anwenden können. 

Diese Phasen eines Cyberangriffs ähneln sich und sind vorhersagbar, unabhängig davon, welche Art von Unternehmen angegriffen oder auf welche Art von Informationen abgezielt wird.
Azure ATP sucht nach drei Haupttypen von Angriffen: böswillige Angriffe, ungewöhnliches Verhalten sowie Sicherheitsprobleme und -risiken.

**Böswillige Angriffe** werden auf deterministische Weise sowie über Analysen von ungewöhnlichem Verhalten ermittelt. Die vollständige Liste der bekannten Angriffstypen umfasst Folgendes:

-   Pass-the-Ticket (PtT)
-   Pass-the-Hash (PtH)
-   Overpass-the-Hash
-   Forged PAC (MS14-068)
-   Golden Ticket
-   Böswillige Replikation
-   Verzeichnisdienstenumeration
-   SMB-Sitzungsenumeration
-   DNS-Reconnaissance
-   Horizontaler Brute-Force-Angriff 
-   Vertikaler Brute-Force-Angriff
-   Skeleton Key
-   Ungewöhnliches Protokoll
-   Herunterstufung der Verschlüsselung
-   Remoteausführung
-   Erstellen eines schädlichen Diensts


Azure ATP erkennt diese verdächtigen Aktivitäten und zeigt Informationen dazu im Azure ATP-Arbeitsbereichsportal an, einschließlich einer Übersicht darüber, wer den Angriff wann und wie ausgeführt hat und was dabei geschehen ist. Durch die Überwachung dieses einfachen und benutzerfreundlichen Dashboards werden Sie also benachrichtigt, wenn Azure ATP vermutet, dass ein Pass-the-Ticket-Angriff auf die Computer Client 1 und Client 2 in Ihrem Netzwerk versucht wurde.

 ![Beispielanzeige in Azure ATP: Pass-the-Ticket-Angriff](media/pass-the-ticket-sa.png)


Azure ATP erkennt darüber hinaus **Sicherheitsprobleme und -risiken**, einschließlich:

-   schwacher Protokolle
-   bekannter Protokollschwachstellen.
-   [Lateral movement path to sensitive accounts (Lateral Movement-Pfade zu sensiblen Konten)](use-case-lateral-movement-path.md)

# <a name="what-threats-does-azure-atp-look-for"></a>Nach welchen Bedrohungen sucht Azure ATP?

Azure ATP ermöglicht die Erkennung der folgenden verschiedenen Phasen eines erweiterten Angriffs: Reconnaissance, gefährdete Anmeldeinformationen, Lateral Movement, Berechtigungsausweitung, Domänendominanz etc. Damit sollen erweiterte Angriffe und interne Bedrohungen erkannt werden, bevor sie Schaden in Ihrer Organisation anrichten.

Die Erkennung von jeder Phase führt zu mehreren verdächtige Aktivitäten, die für die betreffende Phase relevant sind, wobei jede verdächtige Aktivität mit verschiedenen Varianten möglicher Angriffe korreliert.
Diese Phasen in der Angriffskette, in der Azure ATP derzeit Erkennungen bereitstellt, werden in der folgenden Abbildung hervorgehoben:

![Azure ATP: Fokus auf Lateralaktivität in der Kette der Angriffsabwehr](media/attack-kill-chain-small.jpg)


Weitere Informationen finden Sie unter [Working with suspicious activities (Arbeiten mit verdächtigen Aktivitäten)](working-with-suspicious-activities.md) und dem [Azure ATP-Handbuch zu verdächtigen Aktivitäten](suspicious-activity-guide.md).

## <a name="whats-next"></a>Wie geht es weiter?

-   Weitere Informationen zum Integrieren von Azure ATP in Ihr Netzwerk finden Sie unter [Azure ATP-Architektur](atp-architecture.md)

-   Erste Schritte bei der Bereitstellung von ATP: [Install ATP (Installieren von ATP)](install-atp-step1.md)


## <a name="see-also"></a>Weitere Informationen
- [Häufig gestellte Fragen zu Azure ATP](atp-technical-faq.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)