---
# required metadata

title: Was ist Microsoft Advanced Threat Analytics (ATA)? | Microsoft Advanced Threat Analytics
description: Hier wird erläutert, was Microsoft Advanced Threat Analytics (ATA) ist und welche Arten von verdächtigen Aktivitäten erkannt werden können
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


## Was ist ATA?
Microsoft Advanced Threat Analytics (ATA) ist eine Sicherheitslösung, mit der IT-Sicherheitsexperten ihre Organisation vor erweiterten gezielten Angriffen und Bedrohungen von innen schützen können. ATA analysiert, lernt und identifiziert automatisch normales und ungewöhnliches Verhalten von Entitäten (Benutzer, Geräte und Ressourcen), um bekannte Angriffe und schädliche Techniken, Sicherheitsprobleme sowie Risiken zu erkennen. Auf Basis von Informationen und Einblicken erstklassiger Sicherheitsforschung hilft diese innovative Technologie Unternehmen dabei, Sicherheitslücken zu identifizieren, bevor diese Schaden anrichten.

## Wie funktioniert ATA?
ATA erkennt:

  - Erweiterte permanente Bedrohungen (Advanced Persistent Threats, APTs) früh in der Angriffskette, bevor diese Schaden anrichten

  - Bedrohungen von innen

  Mithilfe von ATA können Sie jetzt auch Schwerpunkte ermitteln, sodass Sie sich auf die wirklich wichtigen Aspekte konzentrieren.

ATA verfügt über ein Erkennungsmodul, das Machine Learning, verschärfte Paketinspektionen im Entitätenkontext, Protokollanalysen und Informationen aus Active Directory (AD) verwendet, um Benutzer- und Entitätsverhalten zu analysieren.
ATA analysiert den Datenverkehr umfassend und erstellt unter Verwendung von Machine Learning eine Übersicht über die normalen Aktivitäten, den Datenverkehr und die Nutzung in Ihrer Organisation. Anschließend erfasst ATA von der Norm abweichendes Verhalten und benachrichtigt Sie in diesem Fall. Dieses Ergebnis wird durch die Ausführung der DPI-Technologie (Deep Packet Inspection) von Microsoft erreicht. Diese Technologie ermöglicht die Paketprüfung im Entitätenkontext auf tiefer Ebene der Netzwerkdatenverkehrsanalyse, sodass ATA alle Ebenen Ihres Netzwerkverkehrs analysieren kann.

Darüber hinaus erfasst ATA relevante Ereignisse von SIEM-Systemen und Domänencontrollern. Nach der Analyse erstellt ATA eine dynamische, fortlaufend aktualisierte Ansicht aller Personen, Geräte und Ressourcen innerhalb einer Organisation. Mithilfe dieser umfassenden Ansicht kann ATA bekannte Angriffe wie Pass-the-Hash-, Pass-the-Ticket-, Reconnaissance-Angriffe und mehr erkennen. Zudem sucht ATA nach Anomalien im Verhalten von Entitäten in Ihrem Netzwerk.  

Sobald eine verdächtige Aktivität erkannt wird, löst ATA eine Warnung aus. Die Anzahl der falsch positiven Ergebnisse, die Sie erhalten, wird minimiert, indem erweiterte Algorithmen für die Aggregation und Kontextüberprüfung verwendet werden.


## Nach welchen Bedrohungen sucht ATA?

ATA ermöglicht die Erkennung der folgenden verschiedenen Phasen eines erweiterten Angriffs: Reconnaissance, gefährdete Anmeldeinformationen, seitliche Verschiebung, Berechtigungsausweitung, Domänendominanz und mehr. Damit sollen erweiterte Angriffe und Bedrohungen von innen erkannt werden, bevor Schaden für Ihr Unternehmen entsteht.

Die Erkennung jeder Phase ergibt eine Reihe von verdächtigen Aktivitäten, die für die betreffende Phase relevant sind. Jede verdächtige Aktivität entspricht verschiedenen Arten von möglichen Angriffen.


### Reconnaissance
ATA bietet mehrere Reconnaissance-Erkennungen. Zum Beispiel erkennt die verdächtige Aktivität **Reconnaissance mithilfe von Kontoenumeration** Versuche von Angreifern, mithilfe des Kerberos-Protokolls zu ermitteln, ob ein Benutzer vorhanden ist, selbst wenn die Aktivität nicht als Ereignis auf dem Domänencontroller protokolliert wurde.

### Gefährdung der Anmeldeinformationen

Damit die Gefährdung von Anmeldeinformationen erkannt werden kann, nutzt ATA sowohl Verhaltensanalysen auf Machine Learning-Basis als auch die Erkennung bekannter Angriffe und Verfahren.  

Durch die Verwendung von Verhaltensanalysen und Machine Learning kann ATA verdächtige Aktivitäten wie ungewöhnliche Anmeldungen, Ressourcenzugriffe und Arbeitszeiten erkennen. Jede dieser verdächtigen Aktivitäten weist auf eine potenzielle Gefährdung der Anmeldeinformationen hin.

Zum Schutz vor gefährdeten Anmeldeinformationen erkennt ATA die folgenden bekannten Angriffe und Techniken:

 - **Brute-Force** – Bei Brute-Force-Angriffen versuchen die Angreifer, die Benutzeranmeldeinformationen zu erraten, indem sie mehrere Benutzerdaten mit mehreren Kennworteingaben kombinieren. Oft verwenden die Angreifer komplexe Algorithmen oder Wörterbücher, um so viele Werte auszuprobieren, wie das betreffende System erlaubt.

- **Sensible Anmeldeinformationen wurden in Nur-Text Authentifizierung offengelegt** – Wenn die Anmeldeinformationen von Konten mit hohen Berechtigungen im Nur-Text-Format gesendet werden, erhalten Sie eine Warnung von ATA, sodass Sie die Konfiguration des Computers aktualisieren können.

- **Dienst legt Konten in Nur-Text-Authentifizierung offen** – Wenn ein Dienst auf einem Computer mehrere Kontoanmeldeinformationen im Nur-Text-Format sendet, erhalten Sie eine Warnung von ATA, sodass Sie die Dienstkonfiguration aktualisieren können.

- **Verdächtige Honeytoken-Kontoaktivitäten** – Honeytoken-Konten sind Dummykonten, die eingerichtet werden, um schädliche Aktivitäten bei Verwendung dieser Dummykonten zu erfassen und zu verfolgen.

### Seitliche Verschiebung
Eine seitliche Verschiebung tritt auf, wenn ein Benutzer Anmeldeinformationen verwendet, die den Zugriff auf einige Ressourcen gewähren, um Zugriff auf andere, nicht eingeschlossene Ressourcen zu erhalten. Damit solche seitliche Verschiebungen erkannt werden können, nutzt ATA sowohl Verhaltensanalysen auf Machine Learning-Basis als auch die Erkennung bekannter Angriffe und Verfahren.  

ATA erkennt den nicht ordnungsgemäßen Zugriff auf Ressourcen, ungewöhnliche Geräte, die verwendet werden, und weitere Indikatoren, die auf seitliche Verschiebungen hindeuten. Darüber hinaus kann ATA seitliche Verschiebungen erkennen, indem die Techniken erkannt werden, die Angreifer für die Durchführung seitlicher Verschiebungen einsetzen, zum Beispiel:
- **Pass-the-Ticket** – Bei Pass-the-Ticket-Angriffen stehlen die Angreifer ein Kerberos-Ticket von einem Computer und verwenden es, um Zugriff auf einen anderen Computer zu erhalten, indem sie die Identität einer Entität in Ihrem Netzwerk annehmen.
- **Pass-the-Hash** – Bei Pass-the-Hash-Angriffen stehlen die Angreifer den NTLM-Hash einer Entität, verwenden ihn für die Authentifizierung mit NTLM, nehmen die Identität einer Entität an und erhalten Zugriff auf Ressourcen in Ihrem Netzwerk.
- **Overpass-The-Hash** – Bei Overpass-The-Hash-Angriffen verwendet der Angreifer einen gestohlenen NTLM-Hash für die Kerberos-Authentifizierung, um ein gültiges Kerberos-TGT-Ticket zu erhalten, das anschließend genutzt wird, um sich als gültiger Benutzer zu authentifizieren und Zugriff auf Ressourcen in Ihrem Netzwerk zu erhalten.

### Ausweitung von Berechtigungen
Ein Berechtigungsausweitungsangriff tritt auf, wenn Angreifer versuchen, vorhandene Berechtigungen auszuweiten und mehrmals zu verwenden, um schließlich die vollständige Kontrolle über die Umgebung des Opfers zu erlangen. ATA erkennt sowohl erfolgreiche als auch versuchte Berechtigungsausweitungsangriffe. ATA verwendet Verhaltensanalysen, um ungewöhnliches Verhalten bei Konten mit Berechtigungen zu erkennen. Zudem erkennt ATA bekannte Angriffe und Techniken, die häufig verwendet werden, um Berechtigungen auszuweiten, zum Beispiel:
- **MS14-068-Exploit (Gefälschtes PAC)** – Bei gefälschten PACs handelt es sich um Angriffe, bei denen der Angreifer Autorisierungsdaten in seinem gültigen TGT-Ticket in Form eines gefälschten Autorisierungsheaders platziert. Mit dieser Technik erlangt der Angreifer Berechtigungen, die ihm von seiner Organisation nicht gewährt wurden.
- Die Verwendung von zuvor kompromittierten Anmeldeinformationen oder von Anmeldeinformationen, die durch seitliche Verschiebungen erhalten wurden.

### Domänendominanz
Eine Domänendominanz tritt auf, wenn Angreifer versuchen, die vollständige Kontrolle und Dominanz über die Umgebung des Opfers zu erhalten, oder diese Kontrolle erfolgreich erlangen. ATA erkennt diese Versuche, indem nach bekannten Techniken gesucht wird, die Angreifer verwenden, darunter:
- **Skeleton Key-Malware** – Bei Skeleton Key-Angriffen wird Malware auf Ihrem Domänencontroller installiert, die es den Angreifern ermöglicht, sich als beliebiger Benutzer zu authentifizieren. Gültige Benutzer können sich währenddessen weiterhin anmelden.
- **Golden Ticket** – Bei Golden Ticket-Angriffen stiehlt ein Angreifer die KBTGT-Anmeldeinformationen, das Kerberos Golden Ticket. Dieses Ticket ermöglicht es dem Angreifer, offline ein TGT-Ticket zu erstellen, mit dem er dann Zugriff auf Ressourcen im Netzwerk erhält.
- **Remoteausführung** – Angreifer können versuchen, die Kontrolle über Ihr Netzwerk zu erlangen, indem sie Code remote auf Ihrem Domänencontroller ausführen.


## Was tue ich jetzt?

-   Weitere Informationen zum Integrieren von ATA in Ihr Netzwerk: [ATA-Architektur](ata-architecture.md)

-   Erste Schritte bei der Bereitstellung von ATA: [Installieren von ATA](/advanced-threat-analytics/DeployUse/install-ata)

## Siehe auch
[Unterstützung zu ATA finden Sie in unserem Forum.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


