---
title: "ATA-Handbuch zu verdächtigen Aktivitäten | Microsoft-Dokumentation"
d|Description: This article provides a list of the suspicious activities ATA can detect and steps for remediation.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/2/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1fe5fd6f-1b79-4a25-8051-2f94ff6c71c1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: f9f9fee8ad8d75d3510c86890201dd719e074b8c
ms.sourcegitcommit: 129bee06ff89b72d21b64f9aa0d1a29f66bf9153
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2017
---
*Gilt für: Advanced Threat Analytics Version 1.8*


# <a name="introduction"></a>Einführung

ATA ermöglicht die Erkennung der folgenden verschiedenen Phasen eines erweiterten Angriffs: Reconnaissance, gefährdete Anmeldeinformationen, seitliche Verschiebung, Berechtigungsausweitung, Domänendominanz und mehr.

Die Phasen in der Angriffskette, in der ATA derzeit Erkennungen bereitstellt, werden im nachstehenden Diagramm veranschaulicht.

![ATA focus on lateral activity in attack kill chain](media/attack-kill-chain-small.jpg)

In diesem Artikel wird jede verdächtige Aktivität in jeder Phase näher erläutert.


## <a name="reconnaissance-using-account-enumeration"></a>Reconnaissance mithilfe von Kontoenumeration

> [!div class="mx-tableFixed"]
|Beschreibung|Untersuchung|Empfehlung|Schweregrad|
|------|----|------|----------|
| Mit Enumerationsangriffen auf Konten versuchen Angreifer mit Authentifizierungsversuchen mit Kerberos Kontonamen zu erraten, um herauszufinden, ob dieser Benutzer im Netzwerk vorhanden ist. Wenn sie ein Konto erraten können, können die Angreifer sich dies in den folgenden Schritten des Angriff zunutze machen. | Schauen Sie sich den betroffenen Computer an, um festzustellen, ob es einen berechtigten Grund gibt, warum dieser Computer so viele Kerberos-Authentifizierungsprozesse durchführt. Dabei handelt es sich um Prozesse, bei denen erfolglos versucht wurde, mehrere Konten in Erfahrung zu bringen (Client_Principal_Unknown error), der Benutzer jedoch nicht vorhanden war, und bei denen mindestens ein Zugriffsversuch Erfolg hatte. <br></br>**Ausnahmen**: Diese Erkennung funktioniert nur, wenn nach mehreren nicht vorhandenen Konten gesucht wurde, und wenn die Authentifizierung von einem Computer ausgeht. Wenn ein Benutzer einen Fehler bei der manuellen Eingabe des Benutzernamens oder der Domäne macht, wird der Authentifizierungsversuch als Versuch der Anmeldung bei einem nicht vorhandenen Konto gewertet. Terminalserver, die erfordern, dass sich viele Benutzer anmelden, können tatsächlich eine hohe Zahl von fehlgeschlagenen Anmeldungen aufweisen. |Untersuchen Sie den Prozess, der diese Anforderungen erzeugt hat.  Weitere Informationen zum Identifizieren von Prozessen auf Grundlage von Quellports finden Sie im Blogpost [Have you ever wanted to see which Windows process sends a certain packet out to network? (Welcher Windows-Prozess schickt welches Paket ans Netzwerk?)](https://blogs.technet.microsoft.com/nettracer/2010/08/02/have-you-ever-wanted-to-see-which-windows-process-sends-a-certain-packet-out-to-network/).|Mittel|

## <a name="reconnaissance-using-directory-services-enumeration-sam-r"></a>Reconnaissance mithilfe von Verzeichnisdienstenumeration (SAM-R)

> [!div class="mx-tableFixed"]
|Beschreibung|Untersuchung|Empfehlung|Schweregrad|
|------|----|------|----------|
Bei der Reconnaissance von Verzeichnisdiensten handelt es sich um eine Technik, die Angreifer einsetzen, um die Verzeichnisstruktur und die Zielkonten mit hohen Berechtigungen für die weiteren Schritte des Angriffs auszukundschaften. Das Protokoll Security Account Manager Remote (SAM-R) ist eine Methode, die zur Abfrage des Verzeichnisses verwendet wird. | Bringen Sie in Erfahrung, weshalb der betroffene Computer Security Account Manager Remote (MS-SAMR) ausführt. Es wird auf ungewöhnliche Weise ausgeführt und fragt höchst wahrscheinlich sensible Entitäten ab. <br></br>**Ausnahmen**: Diese Erkennung funktioniert nur, wenn das normale Verhalten von Benutzern, die Abfragen mit SAM-R durchführen, erfasst wird, damit Sie dann gewarnt werden können, wenn ungewöhnliche Abfragen erkannt werden. Sensible Benutzer, die sich bei Computern anmelden, die nicht ihre eigenen sind, lösen möglicherweise eine Abfrage mit SAM-R aus, die als ungewöhnlich angesehen wird, auch wenn es sich dabei um einen Teil des normalen Arbeitsprozesses handelt. Dies passiert häufig bei Mitgliedern des IT-Teams. Wenn dies als verdächtig markiert wird, aber von normaler Aktivität herrührt, liegt dies daran, dass dieses Verhalt vorher noch nicht von ATA erfasst wurde. | In diesem Fall wird empfohlen, dass Sie eine längere Lernphase und eine bessere ATA-Erfassung in der Domäne pro AD-Gesamtstruktur erlauben.<br></br>[Laden Sie die das Tool „SAMRi10“ herunter](https://gallery.technet.microsoft.com/SAMRi10-Hardening-Remote-48d94b5b). SAMRi10 wurde vom ATA-Team veröffentlicht. Es erhöht den Schutz Ihrer Umgebung vor Abfragen mit SAM-R. | Mittel|

## <a name="reconnaissance-using-dns"></a>Reconnaissance über DNS


> [!div class="mx-tableFixed"]
|Beschreibung|Untersuchung|Empfehlung|Schweregrad|
|------|----|------|----------|
| Ihr DNS-Server enthält eine Struktur aller Computer, IP-Adressen und Dienste in Ihrem Netzwerk. Diese Informationen werden von Angreifern verwendet, um Ihre Netzwerkstruktur auszukundschaften und um interessante Zielcomputer zu bestimmten, die sie in den nächsten Schritten des Angriffs benötigen. | Bringen Sie in Erfahrung, warum der betroffene Computer eine AXFR-Abfrage (Full Transfer Zone) durchführt, um alle Einträger der DNS-Domäne zu erhalten. <br></br>**Ausnahmen**: Diese Erkennung identifiziert Nicht-DNS-Server, die DNS-Zonentransferabfragen ausstellen. Es gibt mehrere Lösungen zur Sicherheitsüberprüfung, die derartige Abfragen an DNS-Server ausstellen. <br></br>Überprüfen Sie auch, ob ATA vom ATA-Gateway über Port 53 mit den DNS-Servern kommunizieren kann, um falsch positive Szenarios zu verhindern.| Schränken Sie den Zonentransfer ein, indem Sie darauf achten, welchem Host Sie Zugriffsberechtigungen erteilen. Weitere Informationen finden Sie unter [Sichern von DNS](https://technet.microsoft.com/library/cc770474(v=ws.11).aspx) und [Prüfliste: Sichern des DNS-Servers](https://technet.microsoft.com/library/cc770432(v=ws.11).aspx). |Mittel|

## <a name="reconnaissance-using-smb-session-enumeration"></a>Reconnaissance mithilfe der SMB-Sitzungsenumeration


> [!div class="mx-tableFixed"]
|Beschreibung|Untersuchung|Empfehlung|Schweregrad|
|------|----|------|----------|
| Mit der SMB-Enumeration (Server Message Block) kann ein Angreifer Informationen dazu erhalten, von welchen IP-Adressen aus sich die Benutzer in Ihrem Netzwerk zuletzt angemeldet haben. Wenn ein Angreifer erst einmal über diese Informationen verfügt, kann er sie verwenden, um bestimmte Konten anzugreifen und sich quer (seitlich) durch das Netzwerk zu bewegen. | Bringen Sie in Erfahrung, warum der betroffene Computer eine SMB-Sitzungsenumeration durchführt.<br></br>**Ausnahme**: Diese Erkennung funktioniert nur, wenn die SMB-Sitzungsenumeration nicht auch so im Unternehmensnetzwerk verwendet wird, aber einige Sicherheitsüberprüfungslösungen (wie z.B. Websense) stellen derartige Abfragen aus. | [Verwenden Sie das Tool Net Cease, um den Schutz Ihrer Umgebung zu erhöhen](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b) | Mittel   |

## <a name="brute-force-ldap-kerberos-ntlm"></a>Brute Force (LDAP, Kerberos, NTLM)


> [!div class="mx-tableFixed"]
|Beschreibung|Untersuchung|Empfehlung|Schweregrad|
|------|----|------|----------|
| Bei einem Brute-Force-Angriff versucht ein Angreifer sich mit sehr vielen Kennwörtern anzumelden, in der Hoffnung, dass er irgendwann das richtige errät. Der Angreifer überprüft systematisch alle Kennwörter – oder einen Großteil möglicher Kennwörter –, bis er das richtige findet. Nachdem der Angreifer das richtige Kennwort erraten hat, kann er sich wie ein Benutzer im Netzwerk anmelden. Aktuell unterstützt ATA horizontale (mehrere Konten) Brute-Force-Angriffe mit dem Kerberos- oder NTLM-Protokoll, und horizontale und vertikale Angriffe (einzelne Konten, mehrere Kennwortversuche) mit einfachen LDAP-Bindungen. | Bringen Sie in Erfahrung, warum die Authentifizierung beim betroffenen Computer für mehrere Benutzerkonten fehlschlägt (wobei die Zahl der Authentifizierungsversuche bei jedem Benutzer ungefähr gleich sind) oder warum es eine hohe Zahl an fehlgeschlagenen Authentifizierungen für ein Benutzerkonto gab. <br></br>**Ausnahmen**: Diese Erkennung funktioniert nur, wenn das normale Verhalten der Konten erfasst wird, die sich bei mehreren Ressourcen authentifizieren und eine Warnung ausgelöst wird, wenn ein ungewöhnliches Muster erkannt wird. Dieses Muster tritt häufiger in Skripts auf, die automatisch authentifizieren, aber möglicherweise veraltete Anmeldeinformationen verwenden (d.h. falsche Kennwörter oder Benutzernamen). | Komplexe bzw. lange Kennwörter stellen die erste Sicherheitsstufe zum Schutz gegen Brute-Force-Angriffe dar. | Mittel   |

## <a name="sensitive-account-exposed-in-plain-text-authentication-and-service-exposing-accounts-in-plain-text-authentication"></a>Sensible Konten, die in der Textauthentifizierung verfügbar gemacht werden, und Konten, die in der Textauthentifizierung Dienste verfügbar machen


> [!div class="mx-tableFixed"]
|Beschreibung|Untersuchung|Empfehlung|Schweregrad|
|------|----|------|----------|
| Einige Dienste, die sich auf einem Computer befinden, senden Kontoanmeldeinformationen in Nur-Text, und das auch für sensible Konten. Angreifer, die Ihren Datenverkehr überwachen, können diese Anmeldeinformationen abfangen und diese zu böswilligen Zwecken verwenden. Jedes Klartextkennwort eines sensiblen Kontos löst die Warnung aus. | Machen Sie den verübenden Computer ausfindig, und bringen Sie in Erfahrung, warum er einfache LDAP-Bindungen verwendet. | Überprüfen Sie die Konfiguration des Quellcomputers, um sicherzustellen, dass Sie keine einfache LDAP-Bindung verwenden. Statt einfachen LDAP-Bindungen können Sie LDAP SALS oder LDAPS verwenden. Halten Sie sich an das Framework mit Sicherheitsebenen und schränken Sie den Zugriff ebenenübergreifend ein, um eine Rechteausweitung zu verhindern. | „Niedrig“ für das Verfügbarmachen von Diensten. „Hoch“ für sensible Konten |

## <a name="honey-token-account-suspicious-activities"></a>Verdächtige Aktivitäten an einem Honeytoken-Konto


> [!div class="mx-tableFixed"]
|Beschreibung|Untersuchung|Empfehlung|Schweregrad|
|------|----|------|----------|
| Honeytoken-Konten sind Köderkonten, die eingerichtet werden, um schädliche Aktivitäten zu erfassen, zu erkennen und zu verfolgen, die versuchen, diese Konten zu verwenden. Dabei handelt es sich um Konten, die in Ihrem Netzwerk nicht verwendet werden und ruhen. Falls plötzlich Aktivitäten von einem dieser Honeytoken-Konten ausgeht, weist dies darauf hin, dass ein böswilliger Benutzer versucht, dieses Konto zu verwenden. | Bringen Sie in Erfahrung, warum ein Honeytoken-Konto von diesem Computer aus authentifiziert. | Durchsuchen Sie die ATA-Profilseite anderer sensibler (berechtigter) Konten in Ihrer Umgebung, um zu bestimmen, ob es mögliche verdächtige Aktivitäten gibt. | Mittel   |

## <a name="unusual-protocol-implementation"></a>Ungewöhnliche Protokollimplementierung


> [!div class="mx-tableFixed"]
|Beschreibung|Untersuchung|Empfehlung|Schweregrad|
|------|----|------|----------|
|Angreifer können Tools verwenden, die SMB- bzw. Kerberos-Protokolle so verwenden, dass sie Kontrolle über Ihr Netzwerk erhalten. Dies deutet auf böswillige Techniken von Over-Pass-The-Hash- oder Brute-Force-Attacken hin. | Bringen Sie in Erfahrung, weshalb der betroffene Computer ein Authentifizierungsprotokoll oder SMB derartig ungewöhnlich verwendet. <br></br>Um festzustellen, ob es sich dabei um einen WannaCry-Angriff handelt, führen Sie Folgendes durch:<br></br> 1.    Laden Sie den Excel-Export der verdächtigen Aktivität herunter.<br></br>2.    Öffnen Sie die Registerkarte zur Netzwerkaktivität, und gehen Sie zum Feld „Json“, um die verknüpften „Smb1SessionSetup & Ntlm“-JSONs zu kopieren.<br></br>3.   Wenn es sich bei „Smb1SessionSetup.OperatingSystem“ um „Windows 2000 2195“ handelt und „Smb1SessionSetup.IsEmbeddedNtlm“ „TRUE“ ist, und wenn „Ntlm.SourceAccountId“ „NULL“ ist, handelt es sich um einen WannaCry-Angriff.<br></br><br></br>**Ausnahmen**: Diese Erkennung kann in seltenen Fällen ausgelöst werden, wenn berechtigte Tools verwendet werden, die Protokolle auf eine Weise, die nicht dem Standard entspricht, implementieren. Es gibt einige bekannte Anwendungen zum Prüfen von Stiften, die dies tun. | Erfassen Sie den Netzwerkdatenverkehr, und bestimmen Sie, welcher Prozess den Datenverkehr mit der ungewöhnlichen Protokollimplementierung erzeugt.| Mittel|

## <a name="malicious-data-protection-private-information-request"></a>Böswillige Anforderung privater Informationen im Rahmen der Datensicherheit


> [!div class="mx-tableFixed"]
|Beschreibung|Untersuchung|Empfehlung|Schweregrad|
|------|----|------|----------|
|Die Datenschutz-API (DPAPI) wird von mehreren Windows-Komponenten verwendet, um Kennwörter, Verschlüsselungsschlüssel und andere sensible Daten sicher zu speichern. Domänencontroller enthalten einen Hauptschlüssel zur Sicherung, der verwendet werden kann, um alle mit der DPAPI verschlüsselten Geheimnisse nach mit einer Domäne verbundenen Windows-Computern zu entschlüsseln. Angreifer können den Hauptschlüssel zur Domänensicherung der DPAPI verwenden, um alle Geheimnisse auf allen mit einer Domäne verbundenen Computern zu entschlüsseln (Browserkennwörter, verschlüsselte Dateien, usw.).| Bringen Sie in Erfahrung, warum der Computer einer Anfrage mit diesem nicht dokumentierten API-Aufruf des Hauptschlüssels für die DPAPI ausgestellt hat.|Unter [Windows Data Protection (Windows-Datenschutz)](https://msdn.microsoft.com/library/ms995355.aspx) können Sie mehr über die DPAPI erfahren.|Hoch|

## <a name="suspicion-of-identity-theft-based-on-abnormal-behavior"></a>Verdacht des Identitätsdiebstahls auf Grundlage von ungewöhnlichem Verhalten


> [!div class="mx-tableFixed"]
|Beschreibung|Untersuchung|Empfehlung|Schweregrad|
|------|----|------|----------|
| Nachdem Sie ein Verhaltensmodell erstellt haben (dazu benötigen Sie mindestens 50 Konten, um über einen Zeitraum von 3 Wochen ein Modell zu erstellen), löst jedes ungewöhnliche Verhalten eine Warnung aus. Verhalten, dass nicht dem Modell eines bestimmten Benutzerkontos entspricht, kann auf einen Identitätsdiebstahl hinweisen. | Bringen Sie in Erfahrung, warum sich der betroffene Benutzer anders verhält. <br></br>**Ausnahmen**: Wenn ATA nur Teile erfasst (nicht alle Domänencontroller werden an ein ATA-Gateway weitergeleitet), werden für einen bestimmten Benutzer auch nur Teilaktivitäten erfasst. Wenn ATA nach mehr als 3 Wochen plötzlich allen Ihren Datenverkehr erfasst, kann es sein, dass die vollständigen Aktivitäten des Benutzer eine Warnung auslösen. | Achten Sie darauf, dass ATA auf allen Ihren Domänencontrollern bereitgestellt wird. <br></br>1.  Überprüfen Sie, ob der Benutzer eine neue Position in Ihrer Organisation innehat.<br></br>2.  Überprüfen Sie, ob es sich bei dem Benutzer um einen Saisonarbeiter handelt.<br></br>3.  Überprüfen Sie, ob der Benutzer nach längerer Abwesenheit wieder da ist.| „Medium“ für alle Benutzer und „Hoch“ für sensible Benutzer |


## <a name="pass-the-ticket"></a>Pass-the-Ticket


> [!div class="mx-tableFixed"]
|Beschreibung|Untersuchung|Empfehlung|Schweregrad|
|------|----|------|----------|
| Bei Pass-the-Ticket-Angriffen ist eine Technik mit seitlicher Bewegung, bei der die Angreifer ein Kerberos-Ticket von einem Computer stehlen und dieses verwenden, um Zugriff auf einen anderen Computer zu erhalten, indem sie die Identität einer Entität in Ihrem Netzwerk annehmen. | Diese Erkennung funktioniert nur, wenn das gleiche Kerberos-Ticket von mindestens zwei Computern verwendet wird. Wenn sich Ihre IP-Adressen oft ändern, kann ATA in einigen Fällen nicht bestimmen, ob unterschiedliche IP-Adressen vom gleichen Computer oder von unterschiedlichen Computern verwendet werden. Dies ist ein häufiges Problem bei zu kleinen DHCP-Pools (VPN, WLAN usw.) und freigegebenen IP-Adressen (NAT-Geräte). | Halten Sie sich an das Framework mit Sicherheitsebenen und schränken Sie den Zugriff ebenenübergreifend ein, um eine Rechteausweitung zu verhindern. | Hoch     |

## <a name="pass-the-hash"></a>Pass-the-Hash


> [!div class="mx-tableFixed"]
|Beschreibung|Untersuchung|Empfehlung|Schweregrad|
|------|----|------|----------|
| Bei einer Pass-The-Hash-Attacke authentifiziert der Angreifer sich bei einem remoten Server oder Dienst mit dem zugrunde liegenden Hash des Kennworts eines Benutzers statt mit dem Nur-Text-Kennwort (was der Normalfall wäre). | Überprüfen Sie, ob das Konto ungewöhnliche Aktivitäten in dem Zeitraum, in dem die Warnung ausgelöst wurde, durchgeführt hat. | Implementieren Sie die Empfehlungen, die unter [Pass-the-Hash](http://aka.ms/PtH) gegeben werden. Halten Sie sich an das Framework mit Sicherheitsebenen und schränken Sie den Zugriff ebenenübergreifend ein, um eine Rechteausweitung zu verhindern. | Hoch|

## <a name="over-pass-the-hash"></a>Overpass-The-Hash


> [!div class="mx-tableFixed"]
|Beschreibung|Untersuchung|Empfehlung|Schweregrad|
|------|----|------|----------|
| Eine Over-Pass-The-Hash-Attacke macht sich eine Implementierungsschwachstelle im Kerberos-Authentifizierungsprotokoll zu Nutze, bei der ein NTLM-Hash verwendet wird, um ein Kerberos-Ticket zu erstellen, mit dem sich der Angreifer bei Diensten im Netzwerk ohne das Kennwort des Benutzers authentifizieren kann. | Herunterstufung der Verschlüsselung: Bringen Sie in Erfahrung, warum das betroffene Konto RC4 in Kerberos verwendet, nachdem es gelernt hat, AES zu verwenden. <br></br>**Ausnahmen**: Diese Erkennung funktioniert nur, wenn Verschlüsselungsmethoden, die in der Domäne verwendet werden, erfasst werden, sodass eine Warnung ausgelöst wird, wenn eine ungewöhnliche oder schwächere Methode erkannt wird. In einigen Fällen wird eine schwächere Verschlüsselungsmethode verwendet, und ATA erkennt dies als ungewöhnlich, obwohl die Methode möglicherweise Teil eines normalen (wenn auch selten vorkommenden) Arbeitsprozesses ist. Dies kann auftreten, wenn derartiges Verhalten noch nicht von ATA erfasst wurde. Ein besseres Erfassen durch ATA in der Domäne verbessert dies. | Implementieren Sie die Empfehlungen, die unter [Pass-the-Hash](http://aka.ms/PtH) gegeben werden. Halten Sie sich an das Framework mit Sicherheitsebenen und schränken Sie den Zugriff ebenenübergreifend ein, um eine Rechteausweitung zu verhindern. | Hoch     |

## <a name="privilege-escalation-using-forged-authorization-data-ms14-068-exploit-forged-pac--ms11-013-exploit-silver-pac"></a>Die Rechteausweitung mit gefälschten Authentifizierungsdaten (MS14-068-Exploit (gefälschte PAC-Datei)/MS11-013-Exploit (Silver PAC))


> [!div class="mx-tableFixed"]
|Beschreibung|Untersuchung|Empfehlung|Schweregrad|
|------|----|------|----------|
| Durch bekannte Sicherheitslücken in älteren Versionen von Windows Server können Angreifer das Privileged Attribute Certificate (PAC) manipulieren, ein Feld im Kerberos-Ticket, das die Autorisierungsdaten eines Benutzer enthält (in Active Directory ist dies die Gruppenmitgliedschaft) und einem Angreifer zusätzliche Berechtigungen erteilt. | Überprüfen Sie, ob ein besonderer Dienst auf dem betroffenen Computer ausgeführt wird, der möglicherweise eine Authentifizierungsmethode, die nicht PAC ist, verwendet. <br></br>**Ausnahmen**: In bestimmten Szenarios implementieren Ressourcen ihren eigenen Autorisierungsmechanismus und lösen möglicherweise eine Warnung in ATA aus. | Stellen Sie sicher, dass alle Domänencontroller mit Betriebssystemen bis Windows Server 2012 R2 mit [KB3011780](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privilege) installiert sind, und dass alle Memberserver und Domänencontroller bis 2012 R2 das aktuellste KB2496930 haben. Weitere Informationen finden Sie unter [Silver PAC](https://technet.microsoft.com/library/security/ms11-013.aspx) und [Gefälschte PAC-Datei](https://technet.microsoft.com/library/security/ms14-068.aspx). | Hoch     |

## <a name="abnormal-sensitive-group-modification"></a>Ungewöhnliche Modifizierung von sensiblen Gruppen


> [!div class="mx-tableFixed"]
|Beschreibung|Untersuchung|Empfehlung|Schweregrad|
|------|----|------|----------|
|Im Rahmen der Rechteausweitungsphase modifizieren Angreifer Gruppen mit hohen Berechtigungen, um Zugriff auf sensible Ressourcen zu erhalten.| Überprüfen Sie, dass die Gruppenänderungen zulässig sind. <br></br>**Ausnahmen**: Die Erkennung funktioniert nur, wenn das normale Verhalten von Benutzern, die sensible Gruppen modifizieren, erfasst wird, damit Sie dann gewarnt werden können, wenn ungewöhnliche Änderungen erkannt werden. Zulässige Änderungen lösen möglicherweise eine Warnung aus, wenn derartiges Verhalten von ATA noch nicht erfasst wurde. Eine längere Lernphase und eine bessere Erfassung durch ATA in Ihrer Domäne verbessert dies. | Achten Sie darauf, dass Sie die Zahl von Benutzern, die autorisiert sind, sensible Gruppen zu modifizieren, so gering wie möglich halten. Verwenden Sie möglichst Just-In-Time-Berechtigungen. | Mittel   |

## <a name="encryption-downgrade---skeleton-key-malware"></a>Herunterstufung der Verschlüsselung: Skeleton Key Malware


> [!div class="mx-tableFixed"]
|Beschreibung|Untersuchung|Empfehlung|Schweregrad|
|------|----|------|----------|
| Skeleton Key ist eine Schadsoftware, die auf einem Domänencontroller ausgeführt wird und mit der eine Authentifizierung bei der Domäne mit jedem Konto möglich ist, ohne das jeweilige Kennwort zu wissen. Diese Schadsoftware verwendet häufig schwächere Verschlüsselungsalgorithmen, um das Kennwort des Benutzers auf dem Domänencontroller zu verschlüsseln. | Herunterstufung der Verschlüsselung: Bringen Sie in Erfahrung, warum das betroffene Konto RC4 in Kerberos verwendet, nachdem es gelernt hat, AES zu verwenden. <br></br>**Ausnahmen**: Diese Erkennung funktioniert nur, wenn Verschlüsselungsmethoden der Domäne erfasst werden. In einigen Fällen wird eine schwächere Verschlüsselungsmethode verwendet, und ATA erkennt dies als ungewöhnlich, obwohl die Methode Teil eines normalen (wenn auch selten vorkommenden) Arbeitsprozesses ist. | Sie können überprüfen, ob Ihre Domänencontroller von Skeleton Key betroffen sind, indem Sie [den vom ATA-Team entwickelten Scanner](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73) verwenden. | Hoch |

## <a name="golden-ticket"></a>Golden Ticket


> [!div class="mx-tableFixed"]
|Beschreibung|Untersuchung|Empfehlung|Schweregrad|
|------|----|------|----------|
| Wenn ein Angreifer über Domänenadministratorrechte verfügt, kann er ein Kerberos-Ticket-Granting-Ticket (TGT) erstellen, das die Autorisierung für alle Ressourcen im Netzwerk erteilt, und mit dem er den Ablaufzeitpunkt des Tickets auf jeden beliebigen Zeitpunkt legen kann. So werden Angreifer im Netzwerk beständig. | Herunterstufung der Verschlüsselung: Bringen Sie in Erfahrung, warum das betroffene Konto RC4 in Kerberos verwendet, nachdem es gelernt hat, AES zu verwenden. <br></br>**Ausnahmen**: Diese Erkennung funktioniert nur, wenn Verschlüsselungsmethoden, die in der Domäne verwendet werden, erfasst werden, sodass eine Warnung ausgelöst wird, wenn eine ungewöhnliche oder schwächere Methode erkannt wird. In einigen Fällen wird eine schwächere Verschlüsselungsmethode verwendet, und ATA erkennt dies als ungewöhnlich, auch wenn die Methode Teil eines normalen (wenn auch selten vorkommenden) Arbeitsprozesses ist. Dies kann auftreten, wenn derartiges Verhalten noch nicht von ATA erfasst wurde. Achten Sie darauf, dass ATA Ihre gesamte Domäne erfasst. | Sie können das Kerberos-Ticket-Granting-Ticket des Hauptschlüssels (KRBTGT) auf folgende Weisen so gut wie möglich schützen:<br></br>1.  Physische Sicherheit<br></br>2.  Physische Sicherheit für virtuelle Maschinen<br></br>3. Absichern des Domänencontrollers<br></br>4.  Isolation der lokale Sicherheitsautorität (LSA)/Credential Guard<br></br>Wenn Golden Tickets erkannt werden, muss eine ausführlichere Untersuchung durchgeführt werden, um zu bestimmen, ob eine taktische Wiederherstellung nötig ist.<br></br>Ändern Sie das Kerberos-Ticket-Granting-Ticket regelmäßig zweimal gemäß den Anweisungen im Microsoft-Blogpost [KRBTGT Account Password Reset Scripts now available for customers (Skripts zur Zurücksetzen von Kennwörtern des KRBTGT-Kontos stehen Kunden jetzt zur Verfügung)](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) mithilfe der [Option „Kennwort/Schlüssel des KRBTGT-Kontos zurücksetzen“](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). <br></br>Implementieren Sie diese [Empfehlungen zu Pass-the-Hash](http://aka.ms/PtH). | Mittel   |



## <a name="remote-execution"></a>Remoteausführung


> [!div class="mx-tableFixed"]
|Beschreibung|Untersuchung|Empfehlung|Schweregrad|
|------|----|------|----------|
| Angreifer, die Administratoranmeldeinformationen kompromittiert haben, können remote Befehle auf Ihrem Domänencontroller ausführen. Damit können sie Beständigkeit erhalten, Informationen sammeln, oder DOS-Attacken (Denial of Service) ausführen usw. | Bringen Sie in Erfahrung, ob das betroffene Konto dazu berechtigt ist, diese remote Ausführung auf Ihrem Domänencontroller durchzuführen. <br></br>**Ausnahmen**: Tatsächliche Benutzer, die manchmal Befehle auf dem Domänencontroller ausführen, können diese Warnung auslösen, auch wenn es sich dabei um Aktivitäten handelt, die Teil des üblichen Administratorprozesses sind. Dies tritt am häufigsten bei Mitgliedern des IT-Teams oder bei Dienstkonten auf, die administrative Aufgaben auf Domänencontrollern durchführen. | Schränken Sie den Remotezugriff auf Domänencontroller von Computern ein, die nicht den Tier 0 aufweisen. Löschen Sie alle verdächtigen, ungesicherten und nicht benötigten Dateien und Ordner. Implementieren Sie widerstandsfähige Richtlinien zu Benutzerkontensteuerung (UAC). Implementieren Sie [PAW](https://technet.microsoft.com/en-us/windows-server-docs/security/securing-privileged-access/securing-privileged-access), damit nur abgesicherte Computer eine Verbindung für Administratoren mit dem Domänencontroller herstellen können. | Niedrig      |

## <a name="malicious-replication-requests"></a>Böswillige Replikationsanforderungen


> [!div class="mx-tableFixed"]
|Beschreibung|Untersuchung|Empfehlung|Schweregrad|
|------|----|------|----------|
| Bei der Replikation mit Active Directory (AD) werden Änderungen eines Domänencontrollers mit allen anderen Domänencontrollern in der Domäne oder der Gesamtstruktur synchronisiert, die Kopien der gleichen Daten enthalten. Mit den entsprechenden Berechtigungen kann ein Angreifer eine Replikationsanforderung ausstellen, als sei er ein Domänencontroller. Damit kann der Angreifer dann die in AD gespeicherten Daten abrufen, einschließlich Kennworthashes. | Bringen Sie in Erfahrung, weshalb der Computer die Replikations-API des Domänencontrollers verwendet. Diese Erkennung funktioniert nur, wenn ATA die Konfigurationspartition der Verzeichnisgesamtstruktur verwendet, um zu erfahren, ob ein Computer ein Domänencontroller ist. <br></br>**Ausnahmen**: Azure AD DirSync löst möglicherweise diese Warnung aus. | Überprüfen Sie die folgenden Berechtigungen: - Replizieren von Verzeichnisänderungen <br></br>- Replizieren von allen Verzeichnisänderungen<br></br>Weitere Informationen finden Sie unter [Erteilen von AD DS-Berechtigungen für die Profilsynchronisierung in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).<br></br>Nutzen Sie [AD ACL Scanner](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/), oder erstellen Sie ein PowerShell-Skript, um festzustellen, wer in der Domäne über diese Berechtigungen verfügt. | Mittel   |



## <a name="broken-trust-between-domain-and-computers"></a>Fehlerhafte Vertrauensstellung zwischen Domäne und Arbeitsgruppe


> [!div class="mx-tableFixed"]
|Beschreibung|Untersuchung|Empfehlung|Schweregrad|
|------|----|------|----------|
| Fehlerhafte Vertrauensstellung bedeutet, dass Sicherheitsanforderungen von AD möglicherweise nicht angewendet werden. Dies ist ein grundlegender Sicherheits- und Kompatibilitätsfehler und stellt ein leichtes Ziel für Angreifer dar. Dadurch wird eine Warnung in ATA ausgelöst, wenn mehr als fünf aufeinanderfolgende Kerberos-Authentifizierungen von einem Computerkonto in einem Zeitraum von 24 Stunden fehlgeschlagen sind. Da der Computer nicht mit dem Domänencontroller kommuniziert, hat er (1) keine aktualisierte Gruppenrichtlinie und (2) das Anmelden ist auf die zwischengespeicherten Anmeldeinformationen beschränkt. | Stellen Sie sicher, dass die Vertrauensstellung des Computers mit der Domäne ordnungsgemäß ist, indem Sie das Ereignisprotokoll überprüfen. | Verknüpfen Sie den Computer erneut mit der Domäne, wenn notwendig, oder setzen Sie das Computerkennwort zurück. | Niedrig      |

## <a name="massive-object-deletion"></a>Umfangreiche Objektlöschungen


> [!div class="mx-tableFixed"]
|Beschreibung|Untersuchung|Empfehlung|Schweregrad|
|------|----|------|----------|
| ATA löst diese Warnung aus, wenn mehr als 5% aller Konten gelöscht werden. Dafür müssen Sie Lesezugriff auf die gelöschten Elementcontainer haben. | Bringen Sie in Erfahrung, weshalb 5% aller Konten auf einmal gelöscht wurden. | Entziehen Sie Benutzern die Berechtigung, Konten in AD löschen zu können. Weitere Informationen finden Sie unter [View or Set Permissions on a Directory Object (Anzeigen oder Festlegen von Berechtigungen in einem Verzeichnisobjekt)](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx). | Niedrig |

## <a name="related-videos"></a>Verwandte Videos
- [Joining the security community](https://channel9.msdn.com/Shows/Microsoft-Security/Join-the-Security-Community) (Der Sicherheitscommunity beitreten)


## <a name="see-also"></a>Siehe auch
- [Verdächtige ATA-Aktivitäten – Playbook](http://aka.ms/ataplaybook)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md)
- [Investigating Forged PAC attacks (Untersuchen von Angriffen mit gefälschten PAC-Dateien)](use-case-forged-pac.md)
- [Troubleshooting ATA known errors (Problembehandlung bei bekannten ATA-Fehlern)](troubleshooting-ata-known-errors.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
