---
title: Was ist Microsoft Advanced Threat Analytics (ATA)?
description: Hier wird erläutert, was Microsoft Advanced Threat Analytics (ATA) ist und welche Arten von verdächtigen Aktivitäten erkannt werden können
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 7/24/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: b88ca23b2d01d08357b3decb1e8e91c07848f5d8
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2020
ms.locfileid: "79410595"
---
# <a name="what-is-advanced-threat-analytics"></a>Was ist Advanced Threat Analytics?

*Gilt für: Advanced Threat Analytics Version 1.9*

Advanced Threat Analytics (ATA) ist eine lokale Plattform, mit deren Hilfe Sie Ihr Unternehmen vor verschiedenen hochentwickelten und gezielten Cyberangriffen und Insiderbedrohungen schützen können.

## <a name="how-ata-works"></a>So funktioniert ATA

ATA nutzt eine proprietäre Netzwerkanalyse-Engine, um den Netzwerkverkehr verschiedener Protokolle (z.B. Kerberos, DNS, RPC, NTLM und andere) zwecks Authentifizierung, Autorisierung und zum Sammeln von Informationen zu erfassen und zu analysieren. ATA sammelt die Informationen über:

-   die Portspiegelung von Domänencontrollern und DNS-Servern bis zum ATA-Gateway bzw.
-   die direkt Bereitstellung eines ATA-Lightweight-Gateways (LGW) auf Domänencontrollern.

ATA bezieht Informationen aus mehreren Datenquellen, wie z.B. aus Protokollen und Ereignissen in Ihrem Netzwerk, um das Verhalten von Benutzern und anderen Entitäten in der Organisation zu lernen und anschließend ein Verhaltensprofil zu erstellen.
ATA kann Ereignisse und Protokolle aus folgenden Quellen beziehen:

-   SIEM-Integration
-   Windows-Ereignisweiterleitung (Windows Event Forwarding; WEF)
-   Direkt aus der Windows-Ereignissammlung (für Lightweight-Gateways)


Weitere Informationen zur ATA-Architektur finden Sie unter [ATA-Architektur](ata-architecture.md).

## <a name="what-does-ata-do"></a>Wie funktioniert ATA?

Die ATA-Technologie erkennt verschiedene verdächtige Aktivitäten und konzentriert sich dabei auf die verschiedenen Phasen der Angriffskette von Cyber-Angriffen, so z.B.:

-   Reconnaissance, während der die Angreifer Informationen zum Aufbau der Umgebung, zu den verschiedenen Assets und zu den vorhandenen Entitäten erfassen. Häufig ist dies der Punkt, an dem Angreifer die nächsten Angriffsphasen planen.
-   Der Zyklus der Seitwärtsbewegung: Die Angreifer investieren Zeit und Mühe in die Verbreiterung ihrer Angriffsfläche in Ihrem Netzwerk.
-   Domänendominanz (Domänenpersistenz): In dieser Phase sammeln Angreifer die Informationen, mit deren Hilfe sie ihren Angriff fortsetzen und dabei verschiedene Einstiegspunkte, Anmeldeinformationen und Techniken nutzen können. 

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

Eine vollständige Liste der Erkennungstypen und deren Beschreibungen finden Sie unter [Nach welchen Bedrohungen sucht ATA](ata-threats.md). 

ATA erkennt diese verdächtigen Aktivitäten und zeigt Informationen dazu in der ATA-Konsole an, einschließlich einer Übersicht darüber, wer den Angriff wann und wie ausgeführt hat und was dabei geschehen ist. Durch die Überwachung dieses einfachen und benutzerfreundlichen Dashboards werden Sie also benachrichtigt, wenn ATA vermutet, dass ein Pass-the-Ticket-Angriff auf die Computer „Client 1“ und „Client 2“ in Ihrem Netzwerk versucht wurde.

 ![beispiel ATA bildschirm pass-the-ticket](media/pass_the_ticket_sa.png)

**ungewöhnliches/nicht normales Verhalten** wird von ATA mithilfe der Verhaltensanalyse und Machine Learning erkannt. So werden fragwürdige Aktivitäten und ungewöhnliches/nicht normales Verhalten wie von Benutzern und Geräten in Ihrem Netzwerk wie die folgenden erkannt:

-   Nicht normale Anmeldungen
-   Unbekannte Gefahren
-   Kennwortfreigabe
-   "Seitwärtsbewegung"
-   Modifizierung von sensiblen Gruppen


Sie können die verdächtigen Aktivitäten dieses Typs im ATA-Dashboard anzeigen. Im folgenden Beispiel werden Sie von ATA benachrichtigt, wenn ein Benutzer auf vier Computer zugreift, die in der Regel nicht von diesem Benutzer verwendet werden. Dies kann Anlass für eine Warnung geben.

 ![sample ATA screen abnormal behavior](media/abnormal-behavior-sa.png) 

ATA erkennt darüber hinaus **Sicherheitsprobleme und -risiken**, einschließlich:

-   einer fehlerhaften Vertrauensstellung
-   schwacher Protokolle
-   bekannter Protokollschwachstellen.

Sie können die verdächtigen Aktivitäten dieses Typs im ATA-Dashboard anzeigen. Im folgenden Beispiel weist Sie ATA darauf hin, dass eine fehlerhafte Vertrauensstellung zwischen einem Computer in Ihrem Netzwerk und der Domäne vorhanden ist.

  ![sample ATA screen broken trust](media/broken-trust-sa.png)


## <a name="known-issues"></a>Bekannte Probleme

- Wenn Sie ein Update auf ATA 1.7 durchführen und anschließen sofort auf ATA 1.8, ohne vorher die ATA-Gateways zu aktualisieren, können Sie nicht zu ATA 1.8 migrieren. Sie müssen zunächst alle Gateways auf Version 1.7.1 oder 1.7.2 aktualisieren, bevor Sie ATA Center auf Version 1.8 aktualisieren können.

- Wenn Sie sich dazu entscheiden, eine vollständige Migration durchzuführen, kann dies einige Zeit in Anspruch nehmen, je nach Größe der Datenbank. Bei der Auswahl der Migrationsoptionen wird die geschätzte Dauer angezeigt. Beachten Sie diese, bevor Sie sich für eine Option entscheiden. 


## <a name="whats-next"></a>Wie geht es weiter?

-   Weitere Informationen zum Integrieren von ATA in Ihr Netzwerk: [ATA-Architektur](ata-architecture.md)

-   Erste Schritte bei der Bereitstellung von ATA: [Installieren von ATA](install-ata-step1.md)

## <a name="related-videos"></a>Verwandte Videos
- [Beitritt zur Sicherheits Community](https://channel9.msdn.com/Shows/Microsoft-Security/Join-the-Security-Community)
- [Übersicht über die ATA-Bereitstellung](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)


## <a name="see-also"></a>Weitere Informationen:
[Verdächtige ATA-Aktivitäten – Playbook](https://aka.ms/ataplaybook)
[Besuchen Sie das ATA-Forum!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
