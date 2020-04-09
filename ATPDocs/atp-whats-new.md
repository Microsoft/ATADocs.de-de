---
title: Neuerungen in Azure Advanced Threat Protection (Azure ATP)
description: Dieser Artikel wird häufig aktualisiert, um Sie über die Neuerungen in der neuesten Version von Azure Advanced Threat Protection (Azure ATP) auf dem Laufenden zu halten.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 03/19/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: ort
ms.suite: ems
ms.openlocfilehash: f56f4a10a956cab92aa18c5f7dcdd208d0e4d8b3
ms.sourcegitcommit: bf5f58317121f1fb0fffc83d8b419cdd7ef27d9a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/05/2020
ms.locfileid: "80669645"
---
# <a name="whats-new-in-azure-advanced-threat-protection-azure-atp"></a>Neuerungen in Azure Advanced Threat Protection (Azure ATP)

Dieser Artikel wird häufig aktualisiert, um Sie über die Neuerungen in der aktuellen Version von Azure ATP auf dem Laufenden zu halten.

Ausführliche Informationen zu früheren Azure ATP-Versionen bis (und einschließlich von) Version 2.55 finden Sie in der [Azure ATP-Versionsreferenz](atp-release-reference.md).

RSS-Feed: Lassen Sie sich benachrichtigen, wenn diese Seite aktualisiert wird, indem Sie die folgende URL kopieren und in Ihren Feedreader einfügen: `https://docs.microsoft.com/api/search/rss?search=%22This+article+is+updated+frequently+to+let+you+know+what%27s+new+in+the+latest+release+of+Azure+ATP%22&locale=en-us`

## <a name="azure-atp-release-2112"></a>Azure ATP-Release 2.112

Veröffentlicht: 15. März 2020

- **Neue Azure ATP-Instanzen werden automatisch in Microsoft Cloud App Security integriert**  
Beim Erstellen einer Azure ATP-Instanz (früher als Arbeitsbereich bezeichnet) ist die Integration in Microsoft Cloud App Security standardmäßig aktiviert. Weitere Informationen zur Integration finden Sie unter [Verwenden von Azure ATP mit Microsoft Cloud App Security](atp-mcas-integration.md).

- **Neue überwachte Aktivitäten**  
Folgende Aktivitätsmonitore sind jetzt verfügbar:
  - Interaktive Anmeldung mit Zertifikat
  - Fehler bei Anmeldung mit Zertifikat
  - Delegierter Ressourcenzugriff

    Erfahren Sie mehr über [von Azure ATP überwachte Aktivitäten](monitored-activities.md) und über das [Filtern von und Suchen nach überwachten Aktivitäten](atp-activities-search.md) im Portal.

- **Featureerweiterung: Erweiterte Ressourcenzugriffsaktivität**  
Ab dieser Version bietet Azure ATP Informationen zu Ressourcenzugriffsaktivitäten, die zeigen, ob die Ressource in Bezug auf eine uneingeschränkte Delegierung vertrauenswürdig ist. Diese Ressourcenkonfiguration ist unsicher und birgt das Risiko, dass Angreifer die Anwendung für ihre Zwecke ausnutzen. Weitere Informationen zu diesem Risiko finden Sie unter [Sicherheitsbewertung: Unsichere Kerberos-Delegierung](atp-cas-isp-unconstrained-kerberos.md).

## <a name="azure-atp-release-2111"></a>Azure ATP-Release 2.111

Veröffentlicht: 1. März 2020

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-2110"></a>Azure ATP-Release 2.110

Veröffentlicht: 23. Februar 2020

- **Neue Sicherheitsbewertung: Nicht überwachte Domänencontroller**  
Die Azure ATP-Sicherheitsbewertungen beinhalten nun einen Bericht zu nicht überwachten Domänencontrollern (Server ohne Sensor), um Sie bei der Verwaltung einer umfassenden Sicherheit Ihrer Umgebung zu unterstützen. Weitere Informationen finden Sie unter [Nicht überwachte Domänencontroller](atp-cas-isp-unmonitored-domain-controller.md).

## <a name="azure-atp-release-2109"></a>Azure ATP, Release 2.109

Veröffentlicht: 16. Februar 2020

- **Featureerweiterung: Sensible Entitäten**  
Ab dieser Version (2.109) werden die von Azure ATP als Zertifizierungsstelle, DHCP- oder DNS-Server identifizierten Computer nun automatisch als **Sensibel** gekennzeichnet.

## <a name="azure-atp-release-2108"></a>Azure ATP, Release 2.108

Veröffentlicht: 9. Februar 2020

- **Neues Feature: Unterstützung für gruppenverwaltete Dienstkonten**  
Azure ATP unterstützt jetzt die Verwendung von gruppenverwalteten Dienstkonten für verbesserte Sicherheit beim Verbinden von Azure ATP-Sensoren mit Ihren Azure Active Directory-Gesamtstrukturen (AD-Gesamtstrukturen). Weitere Informationen zur Verwendung von gruppenverwalteten Dienstkonten bei Azure ATP-Sensoren finden Sie unter [Schnellstart: Herstellen einer Verbindung mit einer Active Directory-Gesamtstruktur](install-atp-step2.md#prerequisites).

- **Featureerweiterung: geplanter Bericht mit zu vielen Daten**  
Wenn ein geplanter Bericht zu viele Daten umfasst, werden Sie nun durch den folgenden Hinweis in der E-Mail darüber informiert: There was too much data during the specified period to generate a report. (Für den angegebenen Zeitraum stehen zu viele Daten zur Verfügung, um einen Bericht zu generieren.) Dieser Hinweis ersetzt das bisherige Verhalten, bei dem dieser Umstand erst nach dem Klicken auf den Link zum Bericht ersichtlich war.

- **Featureerweiterung: aktualisierte Logik der Domänencontrollerabdeckung**  
Die Logik des Berichts zur Domänencontrollerabdeckung wurde so aktualisiert, dass nun zusätzliche Informationen aus Azure AD einbezogen werden, wodurch die Genauigkeit der Übersicht über Domänencontroller ohne Sensoren verbessert wird. Diese neue Logik sollte sich auch positiv auf die entsprechende Microsoft-Sicherheitsbewertung auswirken.

## <a name="azure-atp-release-2107"></a>Azure ATP, Release 2.107

Veröffentlicht: 3. Februar 2020

- **Neue überwachte Aktivität: SID-Verlaufsänderung**  
Die SID-Verlaufsänderung ist jetzt eine überwachte und filterbare Aktivität. Erfahren Sie mehr über [von Azure ATP überwachte Aktivitäten](monitored-activities.md) und über das [Filtern von und Suchen nach überwachten Aktivitäten](atp-activities-search.md) im Portal.

- **Featureerweiterung: Geschlossene oder unterdrückte Warnungen werden nicht mehr erneut geöffnet.**  
Nachdem eine Warnung im Azure ATP-Portal geschlossen oder unterdrückt wurde, wird eine neue Warnung geöffnet, wenn die gleiche Aktivität innerhalb eines kurzen Zeitraums noch mal erkannt wird. Zuvor wurde in diesem Fall dieselbe Warnung wieder geöffnet.

- **TLS 1.2 erforderlich für Zugriff auf das Portal und Sensoren**  
TLS 1.2 ist nun erforderlich, um Azure ATP-Sensoren zu verwenden und den Clouddienst zu nutzen. Mit Browsern, die TLS 1.2 nicht unterstützen, kann nicht mehr auf das Azure ATP-Portal zugegriffen werden.

## <a name="azure-atp-release-2106"></a>Azure ATP Release 2.106

Veröffentlicht: 19. Januar 2020

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-2105"></a>Azure ATP Release 2.105

Veröffentlicht: 12. Januar 2020

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-2104"></a>Azure ATP-Release 2.104

Veröffentlicht am 23. Dezember 2019

- **Ablauf von Sensorversionen beseitigt**  
Azure ATP-Sensorbereitstellungs- und -Sensorinstallationspakete laufen nicht mehr nach einer Reihe von Versionen ab und werden nur einmal automatisch aktualisiert. Das Ergebnis dieses Features ist, dass bereits heruntergeladene Sensorinstallationspakete auch dann installiert werden können, wenn sie älter sind als unsere maximale Anzahl abgelaufener Versionen.

- **Kompromittierung bestätigen**  
Sie können jetzt die Kompromittierung bestimmter Office 365-Benutzer bestätigen und deren Risikostufe auf **hoch**festlegen. Dieser Workflow bietet Ihren Sicherheitsbetriebsteams eine andere Reaktionsfunktion, um die Schwellenwerte für die Zeit bis zum Auflösen von Sicherheitsvorfällen zu reduzieren. Erfahren Sie mehr über das [Bestätigen von Kompromittierungen](https://docs.microsoft.com/cloud-app-security/tutorial-ueba?branch=pr-en-us-1204#phase-4-protect-your-organization) mithilfe von Azure ATP und Cloud App Security.

- **Banner zu neuen Funktionen**  
Auf Azure ATP-Portalseiten, auf denen eine neue Funktion im Cloud App Security-Portal verfügbar ist, werden neue Banner mit Beschreibungen und Zugriffslinks zu den verfügbaren Funktionen angezeigt.

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-2103"></a>Azure ATP Release 2.103

Veröffentlicht am 15. Dezember 2019

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-2102"></a>Azure ATP Release 2.102

Veröffentlicht am 08. Dezember 2019

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-2101"></a>Azure ATP Release 2.101

Veröffentlicht am 24. November 2019

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-2100"></a>Azure ATP Release 2.100

Veröffentlicht: 17. November 2019

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-299"></a>Azure ATP Release 2.99

Veröffentlicht: 3. November 2019

- **Featureerweiterung:  Benachrichtigung in der Benutzeroberfläche über die Verfügbarkeit des Cloud App Security-Portals wurde dem Azure ATP-Portal hinzugefügt**  
Um sicherzustellen, dass alle Benutzer über die Verfügbarkeit der erweiterten Features informiert sind, die über das Cloud App Security-Portal verfügbar sind, wurde die Benachrichtigung für das Portal aus der vorhandenen Azure ATP-Warnungszeitachse hinzugefügt.

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-298"></a>Azure ATP Release 2.98

Veröffentlicht: 27. Oktober 2019

- **Featureerweiterung: Warnung wg. Verdacht auf einen Brute-Force-Angriff**  
Die Warnung bei [Verdacht auf einen Brute-Force-Angriff (SMB)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033) wurde mithilfe zusätzlicher Analysen verbessert, und die Erkennungslogik zum Reduzieren **unbedenklicher richtig positiver (B-TP)** und **falsch positiver (FP)** Warnungsergebnisse wurde verbessert.

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-297"></a>Azure ATP-Release 2.97

Veröffentlicht: 6. Oktober 2019

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-296"></a>Azure ATP Release 2.96

Veröffentlicht: 22. September 2019

- **Erweiterte NTLM-Authentifizierungsdaten mithilfe des Windows-Ereignisses 8004**  
Azure ATP-Sensoren sind nun in der Lage, automatisch die NTLM-Authentifizierungsaktivitäten zu lesen und mit den von Ihnen verwendeten Serverdaten anzureichern, wenn die NTLM-Überwachung aktiviert ist und Windows-Ereignis 8004 auftritt. Azure ATP analysiert Windows-Ereignis 8004 für NTLM-Authentifizierungen, um die für Azure ATP-Bedrohungsanalysen und -Warnungen verwendeten NTLM-Authentifizierungsdaten anzureichern. Diese erweiterte Funktion bietet Ressourcenzugriffsaktivität über NTLM-Daten sowie erweiterte Aktivitäten in Verbindung mit nicht gelungenen Anmeldungen, und bezieht dabei den Zielcomputer ein, auf den der Benutzer vergeblich zuzugreifen versuchte.

    Erfahren Sie mehr über NTLM-Authentifizierungsaktivitäten [unter Verwendung von Windows-Ereignis 8004](configure-windows-event-collection.md#ntlm-authentication-using-windows-event-8004).

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-295"></a>Azure ATP Release 2.95

Veröffentlicht: 15. September 2019

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-294"></a>Azure ATP Release 2.94

Veröffentlicht: 8. September 2019

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-293"></a>Azure ATP Release 2.93

Veröffentlicht: 1. September 2019

-   Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-292"></a>Azure ATP Release 2.92

Veröffentlicht: 25. August 2019

-   Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-291"></a>Azure ATP Release 2.91

Veröffentlicht: 18. August 2019

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-290"></a>Azure ATP Release 2.90

Veröffentlicht: 11. August 2019

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-289"></a>Azure ATP Release 2.89

Veröffentlicht: 4. August 2019

- **Verbesserung der Sensormethode**  
Um eine übermäßige Generierung von NTLM-Datenverkehr bei der Erstellung präziser LMP-Bewertungen (Lateral Movement Path) zu vermeiden, wurden Verbesserungen an den Azure ATP-Sensormethode vorgenommen, um weniger auf die NTLM-Nutzung angewiesen zu sein und Kerberos stärker zu nutzen.

- **Erweiterung von Warnungen: Suspected Golden Ticket usage (nonexistent account)** (Verdacht auf Verwendung eines Golden Ticket (nicht vorhandenes Konto))  
SAM-Namensänderungen wurden zu den unterstützenden Beweisarten hinzugefügt, die in dieser Art von Warnungen aufgeführt sind. Weitere Informationen zur Warnung, einschließlich Informationen zum Vermeidung dieser Art von Aktivitäten und zur Behebung des Fehlers finden Sie in [Suspected Golden Ticket usage (nonexistent account)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027) (Verdacht auf Verwendung eines Golden Ticket [nicht vorhandenes Konto]).

- **Allgemeine Verfügbarkeit: Suspected NTLM authentication tampering** (Vermutete Manipulation der NTLM-Authentifizierung)  
Die Warnung [Suspected NTLM authentication tampering](atp-lateral-movement-alerts.md#suspected-ntlm-authentication-tampering-external-id-2039) (Vermutete Manipulation der NTLM-Authentifizierung) befindet sich nicht mehr im Vorschaumodus und ist nun allgemein verfügbar.

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-288"></a>Azure ATP Release 2.88

Veröffentlicht: 28. Juli 2019

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-287"></a>Azure ATP Release 2.87

Veröffentlicht: 21. Juli 2019

- **Featureerweiterung: Automatisierte Syslog-Ereignissammlung für eigenständige Azure ATP-Sensoren**  
Eingehende Syslog-Verbindungen für eigenständige Azure ATP-Sensoren sind nun vollständig automatisiert, während die Umschaltoption aus dem Konfigurationsbildschirm entfernt wird. Diese Änderungen haben keine Auswirkungen auf ausgehende Syslog-Verbindungen.

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-286"></a>Azure ATP Release 2.86

Veröffentlicht: 14. Juli 2019

- **Neue Sicherheitswarnung: Suspected NTLM authentication tampering (external ID 2039) (Vermutete Manipulation der NTLM-Authentifizierung [Externe ID 2039])**  
Die neue Azure ATP-Sicherheitswarnung für die [vermutete Manipulation der NTLM-Authentifizierung](atp-lateral-movement-alerts.md#suspected-ntlm-authentication-tampering-external-id-2039) befindet sich jetzt in der Vorschauphase.    Bei dieser Erkennung wird eine Azure ATP-Sicherheitswarnung ausgelöst, wenn vermutet wird, dass ein Man-in-the-Middle-Angriff die Überprüfung der Nachrichtenintegrität (MIC, Message Integrity Check) durch NTLM umgeht. Dieses Sicherheitsrisiko wird im Microsoft Security Response Center unter [CVE-2019-040](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2019-1040) näher erläutert. Bei diesen Angriffen wird versucht, die NTLM-Sicherheitsfeatures herabzustufen und eine erfolgreiche Authentifizierung durchzuführen. Das Ziel besteht in einem Angriff mit Lateral-Movement-Pfaden.

- **Featureerweiterung: Erweiterte Identifikation des Gerätebetriebssystems**  
Bisher hat Azure ATP Entitätsinformationen zum Betriebssystem des Geräts bereitgestellt, die auf den verfügbaren Attributen in Active Directory Domain Services basieren. Wenn die Betriebssysteminformationen zuvor nicht in Active Directory Domain Services verfügbar waren, waren sie auch nicht auf den Azure ATP-Entitätsseiten verfügbar. Ab dieser Version bietet Azure ATP diese Informationen mithilfe von erweiterten Methoden zur Identifizierung des Gerätebetriebsystems für Geräte, zu denen die Informationen nicht in Active Directory vorliegen, oder die dort nicht registriert sind.

    Durch das Hinzufügen von Daten der erweiterten Methoden zur Identifizierung des Gerätebetriebsystems können nicht registrierte und Nicht-Windows-Geräte identifiziert werden, sodass der Untersuchungsprozess gleichzeitig vereinfacht wird. Weitere Informationen zur Netzwerknamensauflösung in Azure ATP finden Sie unter [Was ist Netzwerknamensauflösung?](atp-nnr-policy.md).  

- **Neues Feature: Authentifizierter Proxy (Vorschauversion)**  
Azure ATP unterstützt nun authentifizierte Proxys. Geben Sie die Proxy-URL über die Befehlszeile des Sensors ein, und geben Sie den Benutzernamen und das Kennwort an, um Proxys zu verwenden, für die eine Authentifizierung erforderlich ist. Weitere Informationen zur Verwendung authentifizierter Proxys finden Sie unter [Konfigurieren des Proxys](https://docs.microsoft.com/azure-advanced-threat-protection/configure-proxy#configure-the-proxy).

- **Featureerweiterung: automatisierter Domänensynchronisierungsprozess**  
Der Prozess zum Festlegen und Markieren von Domänencontrollern als Kandidaten für Domänensynchronizer während des Setups und der folgenden Konfiguration ist nun vollständig automatisiert. Die Umschaltoption für die manuelle Auswahl von Domänencontroller als Kandidaten für Domänensynchronizer wurde entfernt.

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-285"></a>Azure ATP Release 2.85

Veröffentlicht: 7. Juli 2019

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-284"></a>Azure ATP Release 2.84

Veröffentlicht: 1. Juli 2019

- **Unterstützung für neuen Standort: Azure UK-Rechenzentrum**  
Azure ATP-Instanzen werden jetzt im Azure UK-Rechenzentrum unterstützt. Weitere Informationen zum Erstellen von Azure ATP-Instanzen und den entsprechenden Rechenzentrumsstandorten finden Sie unter [Step 1 of Azure ATP installation (Azure ATP-Installation – Schritt 1)](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step10).

- **Featureerweiterung: Neuer Name und neue Features für die Warnungen bei verdächtigen Hinzufügungen zu sensiblen Gruppen (externe ID 2024)**  
Die Warnung **Suspicious additions to sensitive groups (Verdächtige Hinzufügungen zu sensiblen Gruppen)** lautete ursprünglich **Suspicious modifications to sensitive groups (Verdächtige Änderungen an sensiblen Gruppen)** . Die externe ID der Warnung (ID 2024) hat sich nicht geändert. Durch die beschreibende Namensänderung wird der Zweck der Warnung bei Ergänzungen zu Ihren **sensiblen** Gruppen genauer wiedergespiegelt. Die verbesserte Warnung enthält auch neue Beweise und verbesserte Beschreibungen. Weitere Informationen finden Sie unter [Suspicious additions to sensitive groups (Verdächtige Hinzufügungen zu sensiblen Gruppen)](https://docs.microsoft.com/azure-advanced-threat-protection/atp-domain-dominance-alerts#suspicious-additions-to-sensitive-groups-external-id-2024).  

- **Neues Dokumentationsfeature: Anleitung zum Verschieben von Advanced Threat Analytics zu Azure ATP**  
In diesem neuen Artikel finden Sie Informationen zu Voraussetzungen, Tipps zur Planung sowie Konfigurations- und Überprüfungsschritte für das Verschieben von ATA zum Azure ATP-Dienst. Weitere Informationen finden Sie unter [Verschieben von ATA zu Azure ATP](https://docs.microsoft.com/azure-advanced-threat-protection/ata-atp-move-overview).

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-283"></a>Azure ATP Release 2.83

Veröffentlicht: 23. Juni 2019

- **Featureerweiterung: Warnung aufgrund verdächtiger Diensterstellung (externe ID 2026)**  
Diese Warnung enthält jetzt eine verbesserte Warnungsseite mit zusätzlichen Beweisen und einer neue Beschreibung. Weitere Informationen finden Sie unter [Suspicious service creation security alert (Warnung aufgrund verdächtiger Diensterstellung)](https://docs.microsoft.com/azure-advanced-threat-protection/atp-domain-dominance-alerts#suspicious-service-creation-external-id-2026).

- **Unterstützung für die Benennung von Instanzen: Unterstützung wurde für Domänenpräfixe hinzugefügt, die nur aus Ziffern bestehen**  
Die Erstellung von Azure ATP-Instanzen unter Verwendung von Domänenanfangspräfixen, die nur aus Ziffern bestehen, wird jetzt unterstützt. Anfangspräfixe für Domänen, die nur Ziffern enthalten, wie z. B. 123456.contoso.com, können durch die Unterstützung verwendet werden.

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-282"></a>Azure ATP Release 2.82

Veröffentlicht: 18. Juni 2019

- **Neue öffentliche Vorschau**  
Die Benutzeroberfläche für die Untersuchung von Identitätsbedrohungen von Azure ATP befindet sich jetzt in der **öffentlichen Vorschau** und steht allen durch Azure ATP geschützten Mandanten zur Verfügung. Weitere Informationen finden Sie unter [Verwenden von Azure ATP mit Microsoft Cloud App Security](atp-mcas-integration.md).

- **Allgemeine Verfügbarkeit**  
Die Unterstützung von Azure ATP für nicht vertrauenswürdige Gesamtstrukturen ist jetzt allgemein verfügbar. Weitere Informationen finden Sie unter [Azure ATP für mehrere Gesamtstrukturen](atp-multi-forest.md).

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-281"></a>Azure ATP-Release 2.81

Veröffentlicht: 10. Juni 2019

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-280"></a>Azure ATP Release 2.80

Veröffentlicht: 2. Juni 2019

- **Featureerweiterung: Warnung zu verdächtiger VPN-Verbindung**  
Diese Warnung enthält jetzt verbesserte Nachweise und Texte, um die Benutzerfreundlichkeit zu erhöhen. Weitere Informationen zu Warnungsfeatures sowie empfohlene Schritte für Abhilfemaßnahmen und Vorbeugung finden Sie in der [Warnungsbeschreibung „Verdächtige VPN-Verbindung“](atp-compromised-credentials-alerts.md#suspicious-vpn-connection-external-id-2025).

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-279"></a>Azure ATP Release 2.79

Veröffentlicht: 26. Mai 2019

- **Allgemeine Verfügbarkeit: Sicherheitsprinzipalreconnaissance (LDAP) (externe ID 2038)**

    Diese Warnung ist jetzt allgemein verfügbar. Weitere Informationen zu Warnung, Warnfeatures und empfohlenen Abhilfemaßnahmen und Schritten zur Vorbeugung finden Sie unter in der [Sicherheitsprinzipalreconnaissance (LDAP) – Warnungsbeschreibung](atp-reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038)

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-278"></a>Azure ATP Release 2.78

Veröffentlicht: 19. Mai 2019

- **Featureerweiterung: Sensible Entitäten**  
Manuelles Kennzeichnen von Exchange-Servern als „sensibel“

    Sie können Entitäten jetzt manuell als Exchange-Server während der Konfiguration kennzeichnen.

    So kennzeichnen Sie eine Entität als Exchange-Server:
    1. Greifen Sie im Azure ATP-Portal auf das Menü **Konfiguration** zu.
    2. Wählen Sie unter **Erkennung** zunächst die Option **Entitätstags** und anschließend **sensibel** aus.
    3. Wählen Sie **Exchange-Server** aus, und fügen Sie dann die Entität hinzu, die Sie kennzeichnen möchten.

    Nach dem Kennzeichnen eines Computers als Exchange-Server wird dieser als „sensibel“ gekennzeichnet und zeigt an, dass er als Exchange-Server gekennzeichnet wurde.  Die Kennzeichnung „sensibel“ wird im Entitätsprofil des Computers angezeigt, und der Computer wird in allen Erkennungen berücksichtigt, die auf vertraulichen Konten und Lateral Movement-Pfaden basieren.

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-277"></a>Azure ATP Release 2.77

Veröffentlicht: 12. Mai 2019

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-276"></a>Azure ATP Release 2.76

Veröffentlicht: 6. Mai 2019

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-275"></a>Azure ATP Release 2.75

Veröffentlicht: 28. April 2019

- **Featureerweiterung: Sensible Entitäten**  
Ab dieser Version (2.75) werden die von Azure ATP als Exchange-Server identifizierte Computer nun automatisch als **Sensibel** gekennzeichnet.  

    Entitäten, die automatisch als **Sensibel** gekennzeichnet werden, da sie als Exchange-Server fungieren, führen diese Klassifizierung als Grund für die Kennzeichnung auf.

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-274"></a>Azure ATP Release 2.74

Wird am 14. April 2019 veröffentlicht

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-273"></a>Azure ATP Release 2.73

Veröffentlicht: 10. April 2019

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-272"></a>Azure ATP Release 2.72

Veröffentlicht: 31. März 2019

- **Featureerweiterung: Durch Lateral-Movement-Pfad (LMP) eingeschränkte Tiefe**  
Lateral-Movement-Pfade (LMP) sind eine wichtige Methode für die Ermittlung von Bedrohungen und Risiken in Azure ATP. Um sich auf die kritischen Risiken für Ihre sensibelsten Benutzer zu konzentrieren, macht es dieses Update einfacher und schneller, Risiken für die sensiblen Benutzer in jedem LMP zu analysieren und zu beseitigen, indem Umfang und Tiefe der einzelnen angezeigten Graphen begrenzt werden.

    Unter [Lateral-Movement-Pfade](use-case-lateral-movement-path.md) erfahren Sie mehr darüber, wie Azure ATP LMPs verwendet, um Zugriffsrisiken für jede Entität in Ihrer Umgebung zu vermeiden.

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-271"></a>Azure ATP Release 2.71

Veröffentlicht: 24. März 2019

- **Featureerweiterung: Integritätswarnungen der Netzwerknamensauflösung (Network Name Resolution, NNR)**  
Integritätswarnungen wurden für Konfidenzniveaus hinzugefügt, die Azure ATP-Sicherheitswarnungen zugeordnet sind, die sich auf NNR beziehen. Jede Integritätswarnung enthält umsetzbare und ausführliche Empfehlungen, wie Abhilfe bei niedriger NNR-Erfolgsquote geschaffen werden kann.

    Informationen dazu, wie Azure ATP NNR verwendet und warum dies für die Genauigkeit von Warnungen wichtig ist, finden Sie unter [Was ist Netzwerknamensauflösung](atp-nnr-policy.md).

- **Serverunterstützung: Es wurde Unterstützung für Server 2019 mithilfe von KB4487044 hinzugefügt**  
Es wurde Unterstützung für die Verwendung von Windows Server-2019 mit dem Patchlevel KB4487044 hinzugefügt. Die Verwendung von Server 2019 ohne den Patch wird nicht unterstützt und kann aus diesem Update nicht gestartet werden.

- **Featureerweiterung: Benutzerbasierter Ausschluss von Warnungen**  
Erweiterte Ausschlussoptionen ermöglichen jetzt den Ausschluss bestimmter Benutzer von bestimmten Warnungen. Ein solcher Ausschluss kann Situationen vermeiden helfen, in denen die Verwendung oder Konfiguration bestimmter Typen von interner Software wiederholt gutartige Sicherheitswarnungen auslöst.

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-270"></a>Azure ATP Release 2.70

Veröffentlicht: 17. März 2019

- **Featureerweiterung: Mehreren Warnungen wurde ein Vertrauensgrad für die Auflösung des Netzwerknamens (Network Name Resolution, NNR) hinzugefügt** Die Auflösung des Netzwerknamens wird verwendet, um die Identität der Quellentität vermuteter Angriffe eindeutig zu bestimmen. Durch Hinzufügen des NNR-Vertrauensgrads zur Beweisliste für Sicherheitswarnungen von Azure ATP können Sie nun sofort auf den NNR-Vertrauensgrad, der in Zusammenhang mit den möglichen identifizierten Quellen steht, zugreifen, diesen nachvollziehen und entsprechende Korrekturen durchführen.

    Der Beweis für den NNR-Vertrauensgrad wurde den folgenden Warnungen hinzugefügt:
  - [Network mapping reconnaissance (DNS) (Reconnaissance über Netzwerkzuordnung (DNS))](atp-reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)
  - [Suspected identity theft (Pass-the-Ticket) (Verdacht auf Identitätsdiebstahl (Pass-the-Ticket))](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018)
  - [Vermuteter NTLM-Relaisangriff (Exchange-Konto) – Vorschauversion](atp-lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037)
  - [Suspected DCSync attack (replication of directory services) (Verdacht auf einen DCSync-Angriff (Replikation von Verzeichnisdiensten))](atp-domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)

- **Zusätzliches Szenario zu Integritätswarnungen: Fehler beim Starten des Azure ATP-Sensordiensts**  
Für Instanzen, bei denen der Azure ATP-Sensordienst aufgrund eines Problems mit dem Treiber für die Netzwerkerfassung nicht gestartet werden konnte, wird nun eine Warnung für die Sensorintegrität ausgelöst. Weitere Informationen zu Azure ATP-Protokollen und deren Verwendung finden Sie unter [Troubleshooting Azure ATP sensor with Azure ATP logs (Problembehandlung eines Azure ATP-Sensors mit Azure ATP-Protokollen)](troubleshooting-atp-using-logs.md).

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-269"></a>Azure ATP Release 2.69

Veröffentlicht: 10. März 2019

- **Featureerweiterung: Warnung bei vermutetem Identitätsdiebstahl (Pass-the-Ticket)** Diese Warnung enthält nun neue Beweise mit Details zu Verbindungen, die über das Remotedesktopprotokoll (RDP) hergestellt wurden. Durch diese zusätzlichen Details lässt sich das bekannte Problem der B-TP-Warnungen (Benign true positive, unbedenklich richtig positiv) korrigieren, die durch die Verwendung von Remote Credential Guard bei RDP-Verbindungen verursacht werden.

- **Featureerweiterung: Remotecodeausführung über DNS-Warnung**  
Diese Warnung enthält nun weitere Sicherheitsupdatestatus Ihres Domänencontrollers, und Sie werden darüber informiert, wenn Updates erforderlich sind.

- **Neues Dokumentationsfeature: Azure ATP-Sicherheitswarnungen mit MITRE ATT&CK Matrix&trade;**  
Zur Erläuterung und einfacheren Zuordnung der Beziehung zwischen Azure ATP-Sicherheitswarnungen und der bekannten MITRE ATT&CK Matrix haben wir die relevanten MITRE-Methoden zur Liste der Azure ATP-Sicherheitswarnungen hinzugefügt. Durch diesen zusätzlichen Verweis lässt sich die vermutete Angriffsmethode leichter verstehen, die beim Auslösen einer Azure ATP-Sicherheitswarnung möglicherweise verwendet wird. Erfahren Sie mehr über den [Leitfaden zu Azure ATP-Sicherheitswarnungen](suspicious-activity-guide.md).  

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-268"></a>Azure ATP Release 2.68

Veröffentlicht: 3. März 2019

- **Featureerweiterung: Suspected Brute Force attack (LDAP) alert** (Warnung bei Verdacht auf einen Brute-Force-Angriff (LDAP))  
Die Benutzerfreundlichkeit dieser Sicherheitswarnung wurde erheblich verbessert. Zu den Verbesserungen zählen u.a. eine überarbeitete Beschreibung, die Bereitstellung zusätzlicher Quellinformationen, neue Infografiken und Details zu Rateversuchen, um eine schnellere Behebung zu erreichen.  
Erfahren Sie mehr zu Sicherheitswarnungen für [Suspected Brute Force attack (LDAP)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004) (Verdacht auf einen Brute-Force-Angriff (LDAP))

- **Neues Dokumentationsfeature: Sicherheitswarnungsumgebung**  
Um die Leistungsfähigkeit von Azure ATP bei der Erkennung der tatsächlichen Bedrohungen für Ihre Arbeitsumgebung zu erklären, haben wir dieser Dokumentation eine neue **Sicherheitswarnungsumgebung** hinzugefügt. Die **Sicherheitswarnungsumgebung** hilft Ihnen, schnell ein Labor oder eine Testumgebung einzurichten, und erklärt die beste Verteidigung gegen gängige, realitätsnahe Bedrohungen und Angriffe.  

    Das [Schritt-für-Schritt-Umgebung](atp-playbook-lab-overview.md) wurde entwickelt, um sicherzustellen, dass Sie nur wenig Zeit für den Aufbau aufwenden und mehr Zeit investieren können, sich über Ihre Bedrohungslage und die verfügbaren Azure ATP-Warnmeldungen und den Schutz zu informieren. Wir freuen uns auf Ihr Feedback.

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-267"></a>Azure ATP Release 2.67

Veröffentlichung: 24. Februar 2019

- **Neue Sicherheitswarnung: Sicherheitsprinzipalreconnaissance (LDAP) – Vorschauversion**  
[Sicherheitsprinzipalreconnaissance (LDAP) – Vorschauversion](atp-reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038)-Sicherheitswarnung für Azure ATP ist jetzt als öffentliche Vorschauversion verfügbar.    In dieser Erkennung wird eine Azure ATP-Sicherheitswarnung ausgelöst, wenn Sicherheitsprinzipalreconnaissance von Angreifern verwendet wird, um wichtige Informationen über die Domänenumgebung zu erlangen. Diese Informationen helfen Angreifern, die Domänenstruktur zu erfassen, und identifizieren auch privilegierte Konten für die Verwendung in späteren Schritten in ihrer Angriffsabwehrkette.

    Lightweight Directory Access Protocol (LDAP) ist eine der sowohl für zulässige als auch böswillige Zwecke am häufigsten verwendeten Methoden zum Abfragen von Active Directory. LDAP-fokussierte Sicherheitsprinzipalreconnaissance wird häufig als erste Phase eines Kerberoasting-Angriffs verwendet. Mit Kerberoasting-Angriffen wird eine Zielliste von Sicherheitsprinzipalnamen (Security Principal Names, SPNs) abgerufen, für die Angreifer dann versuchen, Ticket Granting Server-Tickets (TGS) zu erhalten.

- **Featureerweiterung: Reconnaissance über Kontoauflistung (NTLM)**  
Verbesserte **Reconnaissance über Kontoauflistung (NTLM)** -Warnung, die zusätzliche Analysen und verbesserte Erkennungslogik zum Reduzieren von **B-TP**- und **FP**-Warnungsergebnissen verwendet.

- **Featureerweiterung: „Reconnaissance über Netzwerkzuordnung“-Warnung (DNS)**  
Neue Typen von Erkennungen wurden „Reconnaissance über Netzwerkzuordnung“-Warnungen (DNS) hinzugefügt. Außer verdächtigen AXFR-Anfragen erkennt Azure ATP jetzt verdächtige Typen von Anforderungen von Nicht-DNS-Servern, die eine übermäßige Anzahl von Anforderungen verwenden.

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-266"></a>Azure ATP Release 2.66

Veröffentlichung: 17. Februar 2019

- **Featureerweiterung: Vermuteter DCSync-Angriff (Replikation der Verzeichnisdienste)**  
Die Benutzerfreundlichkeit dieser Sicherheitswarnung wurde verbessert. Zu den Verbesserungen zählen u.a. eine überarbeitete Beschreibung, die Bereitstellung zusätzlicher Quellinformationen, neue Infografiken und mehr Nachweisinformationen.
Erfahren Sie mehr über die Sicherheitswarnung [Vermuteter DCSync-Angriff (Replikation der Verzeichnisdienste)](atp-domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006).

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-265"></a>Azure ATP, Release 2.65

Veröffentlichung: 10. Februar 2019

- **Neue Sicherheitswarnung: Suspected NTLM relay attack (Exchange account) - preview** (Vermuteter NTLM-Relaisangriff (Exchange-Konto) – Vorschauversion)  
Die Azure ATP-Sicherheitswarnung [Suspected NTLM relay attack (Exchange account) - preview](atp-lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037) (Vermuteter NTLM-Relaisangriff (Exchange-Konto) – Vorschauversion) ist jetzt als öffentliche Vorschauversion verfügbar.    Hierbei wird eine Azure ATP-Sicherheitswarnung ausgelöst, wenn ermittelt wird, dass die Anmeldeinformationen eines Exchange-Kontos von einer verdächtigen Quelle verwendet werden. Bei solchen Angriffen werden NTLM-Relaistechniken verwendet, um die Exchange-Berechtigungen eines Domänencontrollers zu erlangen. Sie werden deshalb als **PrivExchange** bezeichnet. Weitere Informationen zur **PrivExchange**-Technik erhalten Sie in der [Sicherheitsempfehlung ADV190007](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/ADV190007) (Erstveröffentlichung: 31. Januar 2019) und im Blogbeitrag zur [Reaktion auf Warnungen in Azure ATP](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/How-to-win-the-latest-security-race-over-NTLM-relay/ba-p/334511).  

- **Allgemeine Verfügbarkeit: Remotecodeausführung über DNS**  
Diese Warnung ist jetzt allgemein verfügbar. Weitere Informationen und Warnungsfeatures finden Sie auf der Beschreibungsseite zur Warnung [Remotecodeausführung über DNS](atp-lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036).

- **Allgemeine Verfügbarkeit: Datenexfiltration über den SMB**  
Diese Warnung ist jetzt allgemein verfügbar. Weitere Informationen und Warnungsfeatures finden Sie auf der Beschreibungsseite zur Warnung [Datenexfiltration über SMB](atp-exfiltration-alerts.md#data-exfiltration-over-smb-external-id-2030).

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-264"></a>Azure ATP Release 2.64

Veröffentlicht: 4. Februar 2019

- **Allgemeine Verfügbarkeit: Vermutete Golden Ticket-Verwendung (Ticketanomalie)**  
Diese Warnung ist jetzt allgemein verfügbar. Weitere Informationen und Warnungsfeatures finden Sie auf der Beschreibungsseite zur Warnung [Vermutete Golden Ticket-Verwendung (Ticketanomalie)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032).

- **Featureerweiterung: Reconnaissance über Netzwerkzuordnung (DNS)**  
Verbesserte Erkennungslogik für diese Warnung, um falsch-positive Ergebnisse zu minimieren und eine zu hohe Anzahl von Warnungen zu vermeiden. Für diese Warnung gilt ab sofort eine Lernphase von acht Tagen, bevor die Warnung möglicherweise zum ersten Mal ausgelöst wird. Weitere Informationen zu dieser Warnung finden Sie auf der Beschreibungsseite zur Warnung [Reconnaissance über Netzwerkzuordnung (DNS)](atp-reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007).

    **Aufgrund der Verbesserung dieser Warnung sollte die nslookup-Methode nicht mehr verwendet werden, um die Azure ATP-Konnektivität während der Erstkonfiguration zu testen.**

- **Featureerweiterung:**  
Diese Version umfasst neu gestaltete Warnungsseiten und neue Nachweise, die eine bessere Untersuchung der Warnungen ermöglichen.
  - [Suspected Brute Force attack (SMB) (Verdacht auf einen Brute-Force-Angriff (SMB))](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)
  - [Vermutete Golden Ticket-Verwendung (Ticketanomalie): Beschreibungsseite zur Warnung](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)
  - [Suspected overpass-the-hash attack (Kerberos) (Verdacht auf einen Overpass-the-Hash-Angriff (Kerberos))](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)
  - [Suspected use of Metasploit hacking framework (Verdacht auf Verwendung eines Hackerframeworks)](atp-compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)
  - [Suspected WannaCry ransomware attack (Verdacht auf einen WannaCry-Ransomangriff)](atp-compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-263"></a>Azure ATP Release 2.63

Veröffentlicht am 27. Januar 2019

- **Neues Feature: Unterstützung nicht vertrauenswürdiger Gesamtstrukturen (Preview)**  
Die Azure ATP-Unterstützung von Sensoren in nicht vertrauenswürdigen Gesamtstrukturen befindet sich nun in der Public Preview.
Über die **Verzeichnisdienste**-Seite im Azure ATP-Portal können Sie zusätzliche Anmeldeinformationen konfigurieren, um Azure ATP-Sensoren zu ermöglichen, Verbindungen mit verschiedenen Active Directory-Gesamtstrukturen herzustellen und Informationen an den Azure ATP-Dienst zurückzugeben. Weitere Informationen finden Sie unter [Azure ATP für mehrere Gesamtstrukturen](atp-multi-forest.md).

- **Neues Feature: Abdeckung des Domänencontrollers**  
Azure ATP stellt nun Abdeckungsinformationen für überwachte Azure ATP-Domänencontroller bereit.  
Sie können die Anzahl der überwachten und nicht überwachten Domänencontroller, die Azure ATP in Ihrer Umgebung ermittelt hat, auf der Seite **Sensoren** im Azure ATP-Portal anzeigen. Laden Sie die Liste der überwachten Domänencontroller für weitere Analysen herunter, und erstellen Sie einen Aktionsplan. Weitere Informationen finden Sie in der Vorgehensweise zum [Überwachen von Domänencontrollern](atp-sensor-monitoring.md).

- **Featureerweiterung: Reconnaissance mithilfe von Kontoenumeration**  
Die Ermittlung der Reconnaissance mithilfe der Azure ATP-Kontoenumeration ermittelt und löst Warnungen bei Enumerationsangriffen mit Kerberos und NTLM aus. Zuvor wurden nur Versuche mit Kerberos ermittelt. Weitere Informationen finden Sie unter [Azure ATP-Warnungen zur Reconnaissance](atp-reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003).

- **Featureerweiterung: Warnung für versuchte Remotecodeausführung**
  - Jegliche Aktivitäten bezüglich der Remoteausführung, z. B. Diensterstellung, WMI-Ausführung und die neue **PowerShell**-Ausführung, wurden zur Profilzeitachse von Zielcomputern hinzugefügt. Der Zielcomputer ist der Domänencontroller, auf dem der Befehl ausgeführt wurde.
  - Die **PowerShell**-Ausführung wurde zur Aktivitätsliste der Remotecodeausführungen hinzugefügt, die im Entitätsprofil auf der Zeitachse für Warnungen aufgeführt werden.
  - Weitere Informationen finden Sie unter [Versuch der Remotecodeausführung](atp-domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019).  

- **Windows Server 2019-LSASS-Problem und Azure ATP**  
Gemäß des Kundenfeedbacks zur Nutzung von Azure ATP mit Domänencontrollern, auf denen Windows Server 2019 ausgeführt wird, enthält dieses Update weitere Logik zur Vermeidung des gemeldeten Verhaltens auf Windows Server 2019-Computern. Die vollständige Unterstützung von Azure ATP-Sensoren unter Windows Server 2019 ist für ein zukünftiges Azure ATP-Update geplant. Das Installieren und Ausführen von Azure ATP unter Windows Server 2019 wird derzeit **nicht** unterstützt. Weitere Informationen finden Sie unter [Voraussetzungen für den Azure ATP-Sensor](atp-prerequisites.md#azure-atp-sensor-requirements).

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-262"></a>Azure ATP Release 2.62

Veröffentlicht am 20. Januar 2019

- **Neue Sicherheitswarnung: Remotecodeausführung über DNS (Preview)**  
Die Azure ATP-Sicherheitswarnung [Remotecodeausführung über DNS](atp-lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036) ist nun in der öffentlichen Vorschauversion verfügbar.    Bei dieser Erkennung wird eine Azure ATP-Sicherheitswarnung ausgelöst, wenn DNS-Abfragen an einen Domänencontroller im Netzwerk gerichtet werden, die im Verdacht stehen, die Sicherheitslücke [CVE-2018-8626](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2018-8626) auszunutzen.

- **Featureerweiterung: Um 72 Stunden verzögertes Sensorupdate**  
Geänderte Option, damit nach jedem Releaseupdate von Azure ATP die Updates für ausgewählte Sensoren um 72 Stunden (anstelle der vorherigen 24-Stunden-Verzögerung) verzögert werden. Anweisungen zur Konfiguration finden Sie unter [Update für Azure ATP-Sensoren](sensor-update.md).

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-261"></a>Azure ATP Release 2.61

Veröffentlicht: 13. Januar 2019

- **Neue Sicherheitswarnung: Data exfiltration over SMB (Datenexfiltration über SMB) (Vorschauversion)**  
Die Azure ATP-Sicherheitswarnung [Data exfiltration over SMB](atp-exfiltration-alerts.md) (Datenexfiltration über SMB) ist nun in der öffentlichen Vorschauversion enthalten. Angreifer mit Domänenadministratorrechten können das KRBTGT-Konto beeinträchtigen. Angreifer können das KRBTGT-Konto verwenden, um ein Kerberos Ticket Granting Ticket (TGT) zu erstellen, das die Autorisierung für jede beliebige Ressource erlaubt.

- **Featureerweiterung: Remote code execution attempt (Versuchte Remotecodeausführung)** Sicherheitswarnung  
Eine neue Warnungsbeschreibung und ein zusätzlicher Beweis sind hinzugefügt worden, damit die Warnung einfacher zu verstehen ist, und um bessere Untersuchungsworkflows zu bieten.

- **Featureerweiterung: DNS query logical activities (Logische Aktivitäten zur DNS-Abfrage)**  
Weitere Abfragetypen sind den [von Azure ATP überwachten Aktivitäten](monitored-activities.md) hinzugefügt worden. Darunter die folgenden: **TXT**, **MX**, **NS**, **SRV**, **ANY**, **DNSKEY**.

- **Featureerweiterung: Suspected Golden Ticket usage (ticket anomaly) (Verdacht auf Verwendung eines Golden Ticket (anomalie)) und Suspected Golden Ticket usage (nonexistent account) (Verdacht auf Verwendung eines Golden Ticket (nicht vorhandenes Ticket))**  
Eine verbesserte Erkennungslogik wurde für beide Warnungen angewendet, um die Anzahl von FP-Warnungen zu reduzieren und genauere Ergebnisse zu liefern.

- **Featureerweiterung: Dokumentation zu Azure ATP-Sicherheitswarnungen**  
Die Dokumentation zu Azure ATP-Sicherheitswarnungen ist optimiert und erweitert worden, um bessere Warnungsbeschreibungen, genauere Klassifizierungen sowie Erklärungen zu Beweisen und Abhilfe- und Präventionsmaßnahmen einzuschließen. Lernen Sie über die folgenden Links das neuen Design der Dokumentation zu Sicherheitswarnungen kennen:
  - [Azure ATP-Sicherheitswarnungen](suspicious-activity-guide.md)
  - [Verstehen von Sicherheitswarnungen](understanding-security-alerts.md)
    - [Warnung zu Reconnaissancephase](atp-reconnaissance-alerts.md)
    - [Warnungen zu Phase der kompromittierten Anmeldeinformationen](atp-compromised-credentials-alerts.md)
    - [Lateral movement phase alerts (Warnung zur Lateral Movement-Phase)](atp-lateral-movement-alerts.md)
    - [Warnungen zu Domänendominanzphase](atp-domain-dominance-alerts.md)
    - [Warnungen zu Exfiltrationsphase](atp-exfiltration-alerts.md)
  - [Untersuchen eines Computers](investigate-a-computer.md)
  - [Untersuchen eines Benutzers](investigate-a-user.md)

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-260"></a>Azure ATP, Release 2.60

Veröffentlicht am 6. Januar 2019

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-259"></a>Azure ATP, Release 2.59

Am 16. Dezember 2018 veröffentlicht

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-258"></a>Azure ATP, Release 2.58

Veröffentlicht am 9. Dezember 2018

- **Erweiterung von Sicherheitswarnungen: Aufteilung der Warnung zu ungewöhnlichen Protokollimplementierungen**  
Die Azure ATP-Serie von Sicherheitswarnungen zu ungewöhnlichen Protokollimplementierungen, die zuvor eine externalId (2002) gemeinsam genutzt haben, ist jetzt in vier verschiedene Warnungen aufgeteilt, die jeweils eine eindeutige externe ID aufweisen.

### <a name="new-alert-externalids"></a>Neue externalIds für Warnungen

> [!div class="mx-tableFixed"]
> |Neuer Sicherheitswarnungsname|Alter Sicherheitswarnungsname|Eindeutige externe ID|
> |---------|----------|---------|
> |Suspected Brute Force attack (SMB) (Verdacht auf einen Brute-Force-Angriff (SMB))|Ungewöhnliche Protokollimplementierung (potenzielle Verwendung schädlicher Tools wie Hydra)|2033
> |Suspected overpass-the-hash attack (Kerberos) (Verdacht auf einen Overpass-the-Hash-Angriff (Kerberos))|Ungewöhnliche Kerberos-Protokollimplementierung (potenzieller Overpass-the-Hash-Angriff)|2002|
> |Suspected use of Metasploit hacking framework (Verdacht auf Verwendung eines Hackerframeworks)|Ungewöhnliche Protokollimplementierung (potenzielle Verwendung schädlicher Hackertools wie Metasploit)|2034
> |Suspected WannaCry ransomware attack (Verdacht auf einen WannaCry-Ransomangriff)|Ungewöhnliche Protokollimplementierung (potenzieller WannaCry-Ransomwareangriff)|2035
> |

- **Neue überwachte Aktivität: Dateikopie über SMB**  
Das Kopieren von Dateien über SMB ist jetzt eine überwachte und filterbare Aktivität. Erfahren Sie mehr über [von Azure ATP überwachte Aktivitäten](monitored-activities.md) und über das [Filtern von und Suchen nach überwachten Aktivitäten](atp-activities-search.md) im Portal.

- **Imageerweiterung für lange Lateral Movement-Pfade**  
Beim Anzeigen von langen Lateral Movement-Pfaden hebt Azure ATP jetzt nur die Knoten hervor, die mit einer ausgewählten Entität verbunden sind, anstatt die anderen Knoten unscharf darzustellen. Diese Änderung führt zu einer erheblichen Beschleunigung beim Rendern von langen Lateral Movement-Pfaden.

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-257"></a>Azure ATP Release 2.57

Veröffentlicht am 2. Dezember 2018

- **Neue Sicherheitswarnung: Verdacht auf Verwendung eines Golden Ticket – Ticketanomalie (Vorschau)**  
Die Azure ATP-Sicherheitswarnung [Verdacht auf Verwendung eines Golden Ticket – Ticketanomalie](suspicious-activity-guide.md) ist jetzt in der öffentlichen Vorschau verfügbar.    Angreifer mit Domänenadministratorrechten können das KRBTGT-Konto beeinträchtigen. Angreifer können das KRBTGT-Konto verwenden, um ein Kerberos Ticket Granting Ticket (TGT) zu erstellen, das Autorisierung für jede beliebige Ressource bietet.

    Ein gefälschtes TGT wird als „Golden Ticket“ bezeichnet, da Angreifer damit dauerhafte Netzwerkpersistenz erlangen. Gefälschte Golden Tickets dieses Typs weisen eindeutige Merkmale auf, für deren Identifikation diese neue Erkennung konzipiert ist.

- **Featureerweiterung: Automatisierte Erstellung von Azure ATP-Instanzen (Arbeitsbereichen)**  
Ab heute heißen Azure ATP-*Arbeitsbereiche* Azure ATP-*Instanzen*. Azure ATP unterstützt jetzt eine Azure ATP-Instanz pro Azure ATP-Konto. Instanzen für neue Kunden werden mithilfe des Assistenten für die Instanzenerstellung im [Azure ATP-Portal](https://portal.atp.azure.com) erstellt. Vorhandene Azure ATP-Arbeitsbereiche werden mit diesem Update automatisch in Azure ATP-Instanzen konvertiert.  

  - Vereinfachte Instanzerstellung für schnellere Bereitstellung und Schutz mit [Erstellung Ihrer Azure ATP-Instanz](install-atp-step1.md)
  - Alle [Anforderungen an Datenschutz und Compliance](atp-privacy-compliance.md) bleiben unverändert.

  Weitere Informationen zu Azure ATP-Instanzen finden Sie unter [Create your Azure ATP instance (Erstellen Ihrer Azure ATP-Instanz)](install-atp-step1.md).

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-256"></a>Azure ATP Release 2.56

Veröffentlicht: 25. November 2018

- **Featureerweiterung: Lateral Movement-Pfade (LMPs)**  
Zwei zusätzliche Funktionen wurden hinzugefügt, um die Fähigkeiten von Azure ATP Lateral Movement-Pfaden (LMP) zu verbessern:

  - Der LMP-Verlauf wird jetzt pro Entität gespeichert und erkannt, und bei der Verwendung von LMP-Berichten.
  - Verfolgen Sie eine Entität in einem LMP über die Aktivitätszeitachse und nehmen Sie die Untersuchung anhand zusätzlicher Beweise vor, die für die Ermittlung potenzieller Angriffspfade zur Verfügung stehen.

  Weitere Informationen zur Verwendung und Untersuchung mit verbesserten LMPs finden Sie unter [Azure ATP Lateral Movement-Pfade](use-case-lateral-movement-path.md).

- **Erweiterungen der Dokumentation: Lateral Movement-Pfade, Namen von Sicherheitswarnungen**  
Es wurden Ergänzungen und Aktualisierungen zu Azure ATP-Artikeln vorgenommen, die Beschreibungen und Funktionen des Lateral Movement-Pfads beschreiben, und es wurde eine Namenszuordnung von alten Namen von Sicherheitswarnungen zu den neuen Namen und externe IDs hinzugefügt.
  - Weitere Informationen finden Sie unter [Azure ATP Lateral Movement-Pfade](use-case-lateral-movement-path.md), [Untersuchen von Lateral Movement-Pfaden](investigate-lateral-movement-path.md) und [Leitfaden für Sicherheitswarnungen](suspicious-activity-guide.md).

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

Ausführliche Informationen zu Azure ATP-Versionen vor (und einschließlich von) Version 2.55 finden Sie in der [Azure ATP-Versionsreferenz](atp-release-reference.md).

## <a name="see-also"></a>Weitere Informationen

- [Was ist Azure Advanced Threat Protection?](what-is-atp.md)
- [Häufig gestellte Fragen](atp-technical-faq.md)
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Azure ATP capacity planning (Azure ATP-Kapazitätsplanung)](atp-capacity-planning.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
