---
title: Verweis auf ATA-Ereignis-IDs | Microsoft-Dokumentation
description: "Gibt eine Liste der ATA-Ereignis-IDs und deren Beschreibungen zurück."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 10/25/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 5d639e84-2e37-43a9-9667-49be6c4fa8b7
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 7bd0f90acbb6a2d8eb84fd09bc4d859fff082273
ms.sourcegitcommit: 5563c6861bb5db5cb73e058e5a51b4938b9a7d46
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2017
---
*Gilt für: Advanced Threat Analytics Version 1.8*


# <a name="ata-event-id-reference"></a>Verweis auf ATA-Ereignis-IDs

Die Ereignisanzeige des ATA Centers protokolliert Ereignisse für ATA. In diesem Artikel wird eine Liste mit Event-IDs und den dazugehörigen Beschreibungen zur Verfügung gestellt.

Die Ereignisse finden Sie hier:

![Speicherort der Ereignis-ID](./media/event-id-location.png)

## <a name="ata-health-events"></a>ATA-Integritätsereignisse

1001 – Integritätswarnung für den freien Speicherplatz des Datenträgers der ATA Center-Datenbank 

1003 – Integritätswarnung bei ATA Center-Überladung 

1004 – Integritätswarnung bei Ablauf des Zertifikats 

1005 – Integritätswarnung bei Trennung der Verbindung zur Center-Datenbank 

1006 – Integritätswarnung bei Ablauf des Kennworts für das Clientkonto bei den ATA-Gateway-Verzeichnisdiensten 

1007 – Integritätswarnung, wenn der ATA-Gateway-Domänensynchronizer nicht zugewiesen ist 

1008 – Integritätswarnung bei einem Fehler des Netzwerkdatenerfassungs-Adapters für ATA Gateway 

1009 – Integritätswarnung beim Fehlen des Netzwerkdatenerfassungs-Adapter für ATA Gateway 

1010 – Integritätswarnung für die Clientkonnektivität der ATA-Gateway-Verzeichnisdienste 

1011 – Integritätswarnung bei Trennung der Verbindung zu ATA-Gateway 

1012 – Integritätswarnung bei Überlastung der ATA-Gateway-Ereignisaktivitäten 

1013 – Integritätswarnung bei Überlastung der ATA-Gateway-Netzwerkaktivitäten 

1014 – Integritätswarnung bei einer Center-Nachricht 

1015 – Integritätswarnung bei Center-Syslog 

1016 – Integritätswarnung für veraltete ATA-Gateways 

1017 – Integritätswarnung, wenn das Center keinen Datenverkehr empfängt 

1018 – Integritätswarnung bei fehlgeschlagenem Start von ATA-Gateway 

1019 – Integritätswarnung bei geringem Speicherplatz in ATA-Gateway 

1020 – Integritätswarnung für den RADIUS-Ereignislistener in ATA-Gateway 

1021 – Integritätswarnung für den Syslog-Ereignislistener in ATA-Gateway 

1022 – Integritätswarnung bei einem Fehler der Auflösung der externen IP-Adresse in ATA Center 
 
## <a name="ata-suspicious-ctivity-events"></a>Verdächtige ATA-Aktivitätsereignisse

2001 – Ungewöhnliches Verhalten im Zusammenhang mit einer verdächtigen Aktivität 

2002 – Ungewöhnliches Verhalten im Zusammenhang mit einem verdächtigen Protokoll 

2003 – Verdächtige Aktivität einer Kontoenumeration 

2004 – Verdächtige Aktivität eines Brute Force-LDAPs 

2005 – Verdächtige Aktivität bei einer fehlgeschlagenen Vorauthentifizierung eines Computers 

2006 – Verdächtige Aktivität bei einer Replikation von Verzeichnisdiensten 

2007 – Verdächtige Aktivität bei einer DNS-Reconnaissance 

2008 – Verdächtige Aktivität bei Herabstufung der Verschlüsselung 

2012 – Verdächtige Aktivität beim Auflisten der Sitzungen 

2013 – Verdächtige Aktivität mit gefälschtem PAC 

2014 – Verdächtige Aktivität einer Honeytoken-Aktivität 

2015 – Verdächtige Aktivität eines LDAP-Kennworts in Klartext 

2016 – Verdächtige Aktivität bei einer umfangreichen Objektlöschung 

2017 – Verdächtige Aktivität bei Pass-the-Hash 

2018 – Verdächtige Aktivität bei Pass-the-Ticket 

2019 – Verdächtige Aktivität bei der Remoteausführung 

2020 – Verdächtige Aktivität beim Abrufen des Sicherungsschlüssels für den Datenschutz 

2021 – Verdächtige Aktivität bei einer SAMR-Reconnaissance 

2022 – Verdächtige Aktivität bei Golden Ticket 

2023 – Verdächtige Aktivität bei Änderung einer ungewöhnlich sensiblen Gruppenmitgliedschaft 

2023 – Verdächtige Brute Force-Aktivität 

## <a name="ata-auditing-events"></a>ATA-Überwachungsereignisse

3001 – Ändern zur ATA-Konfiguration 

3002 – Hinzufügen von ATA-Gateway

3003 – Löschen von ATA-Gateway

3004 – Aktivieren der ATA-Lizenz

3005 – Anmelden bei der ATA-Konsole

3006 – Manuelle Änderung zum Status „Integritätsaktivität“ 

3007 – Manuelle Änderung zum Status „verdächtige Aktivität“ 


## <a name="see-also"></a>Siehe auch
- [Voraussetzungen für ATA](ata-prerequisites.md)
- [ATA-Kapazitätsplanung](ata-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-collection.md#configuring-windows-event-forwarding)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)