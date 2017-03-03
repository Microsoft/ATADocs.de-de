---
title: Welche Bedrohungen werden von Advanced Threat Analytics erkannt? | Microsoft Docs
description: Listet die Bedrohungen auf, die Advanced Threat Analytics erkennt
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 22d08a20291b1651a36247e9ffbeff8c881aefc5
ms.openlocfilehash: 2378405d9d55ad40cb2cbfa21d2848536b86c1aa


---

*Gilt für: Advanced Threat Analytics Version 1.7*

# <a name="what-threats-does-ata-look-for"></a>Nach welchen Bedrohungen sucht ATA?

ATA ermöglicht die Erkennung der folgenden verschiedenen Phasen eines erweiterten Angriffs: Reconnaissance, gefährdete Anmeldeinformationen, seitliche Verschiebung, Berechtigungsausweitung, Domänendominanz und mehr. Damit sollen erweiterte Angriffe und interne Bedrohungen erkannt werden, bevor sie Schaden in Ihrer Organisation anrichten.
Die Erkennung von jeder Phase führt zu mehreren verdächtige Aktivitäten, die für die betreffende Phase relevant sind, wobei jede verdächtige Aktivität mit verschiedenen Varianten möglicher Angriffe korreliert.
Diese Phasen in der Angriffskette, in der ATA derzeit Erkennungen bereitstellt, sind im nachstehenden Bild hervorgehoben.

![ATA focus on lateral activity in attack kill chain](media/attack-kill-chain-small.jpg)


### <a name="reconnaissance"></a>Reconnaissance
ATA bietet mehrere Reconnaissance-Erkennungen. Diese Erkennungen umfassen:
-   **Reconnaissance mithilfe von Kontoenumeration** Erkennt Versuche von Angreifern, mithilfe des Kerberos-Protokolls zu ermitteln, ob ein Benutzer vorhanden ist, selbst dann, wenn die Aktivität nicht als Ereignis auf dem Domänencontroller protokolliert wurde.
-   **Net session-Enumeration** Im Rahmen der Reconnaissancephase könnten Angreifer den DC hinsichtlich aller aktiven SMB-Sitzungen auf dem Server abfragen. Dies würde ihnen denZugriff auf alle Benutzer und IP-Adressen ermöglichen, die diesen SMB-Sitzungen zugeordnet sind. SMB-Sitzungsenumeration kann von Angreifern verwendet werden, auf vertrauliche Konten abzuzielen, wodurch sie sich quer (seitlich) durch das Netzwerk bewegen können.
-   **Reconnaissance über DNS** DNS-Informationen im Zielnetzwerk sind häufig sehr nützliche Reconnaissanceinformationen. DNS-Informationen enthalten eine Liste aller Server und häufig aller Clients sowie die Zuordnung zu deren IP-Adressen. Anzeigen von DNS-Informationen kann Angreifern eine detaillierte Ansicht dieser Entitäten in Ihrer Umgebung bieten, die es den Angreifern ermöglicht, ihre Anstrengungen auf die relevanten Entitäten für die Kampagne zu konzentrieren.
-   **Reconnaissance über Verzeichnisdienst-Enumeration** Erkennen von Entitätssuchen (Benutzer, Gruppen, etc.), die mithilfe des SAM-Remoteprotokolls ausgeführt werden, um Abfragen für die Domänencontroller auszuführen. Diese Reconnaissancemethode kommt häufig in vielen Arten von Schadsoftware vor, die in realen Angriffsszenarios zum Einsatz kommt. 


### <a name="compromised-credentials"></a>Gefährdete Anmeldeinformationen
Damit die Gefährdung von Anmeldeinformationen erkannt werden kann, nutzt ATA sowohl Verhaltensanalysen auf Machine Learning-Basis als auch die Erkennung bekannter Angriffe und Verfahren.
Durch die Verwendung von Verhaltensanalysen und Machine Learning kann ATA verdächtige Aktivitäten wie ungewöhnliche Anmeldungen, Ressourcenzugriffe und Arbeitszeiten erkennen, die auf eine Gefährdung von Anmeldeinformationen hinweisen. Zum Schutz vor gefährdeten Anmeldeinformationen erkennt ATA die folgenden bekannten Angriffe und Techniken:
-   **Brute-Force** Bei Brute-Force-Angriffen versuchen die Angreifer, die Benutzeranmeldeinformationen zu erraten, indem sie mehrere Benutzerdaten mit mehreren Kennworteingaben kombinieren. Oft verwenden die Angreifer komplexe Algorithmen oder Wörterbücher, um so viele Werte auszuprobieren, wie das betreffende System erlaubt.
-   **Sensible Anmeldeinformationen wurden in Nur-Text Authentifizierung offengelegt** Wenn die Anmeldeinformationen von Konten mit hohen Berechtigungen im Nur-Text-Format gesendet werden, erhalten Sie eine Warnung von ATA, sodass Sie die Konfiguration des Computers aktualisieren können.
-   **Dienst legt Konten in Nur-Text-Authentifizierung offen** Wenn ein Dienst auf einem Computer mehrere Kontoanmeldeinformationen im Nur-Text-Format sendet, erhalten Sie eine Warnung von ATA, sodass Sie die Dienstkonfiguration aktualisieren können.
-   **Verdächtige Honeytoken-Kontoaktivitäten** Honeytoken-Konten sind Dummykonten, die eingerichtet werden, um schädliche Aktivitäten bei Verwendung dieser Dummykonten zu erfassen und zu verfolgen. ATA sendet Ihnen Warnungen zu allen Aktivitäten über diese Honeytoken-Konten.
-   **Ungewöhnliche Protokollimplementierung** Authentifizierungsanforderungen (Kerberos oder NTLM) erfolgen in der Regel über einen normalen Satz von Methoden und Protokollen. Für eine erfolgreiche Authentifizierung muss die Anforderung jedoch nur einen speziellen Satz von Anforderungen erfüllen. Angreifer können diese Protokolle mit geringfügigen Abweichungen von der normalen Implementierung in der Umgebung implementieren. Diese Abweichungen können ein Hinweis auf das Vorhandensein eines Angreifers sein, der versucht oder Erfolg damit hat, gefährdete Anmeldeinformationen zu nutzen.
-   **Böswillige Anforderung privater Informationen im Rahmen der Datensicherheit** Die Datenschutz-API (DPAPI) ist ein kennwortbasierter Datenschutzdienst. Dieser Schutzdienst wird von verschiedenen Clientanwendungen verwendet, die vertrauliche Informationen eines Benutzers, etwa Websitekennwörter und Anmeldeinformationen für Dateifreigaben, speichern. Um Fälle mit Kennwortverlust zu unterstützen, können Benutzer geschützte Daten mithilfe eines Wiederherstellungsschlüssels entschlüsseln, der nichts mit dem jeweiligen Kennwort zu tun hat. In einer Domänenumgebung können externe Angreifer den Wiederherstellungsschlüssel stehlen und diesen dazu verwenden, geschützte Daten auf allen Computern zu entschlüsseln, die zur Domäne gehören.
-   **Ungewöhnliches Verhalten** Häufig werden in Fällen von Bedrohungen von innen sowie von erweiterten Angriffen die Anmeldeinformationen eines Kontos mit Social-Engineering-Methoden oder neuen, noch nicht bekannten Methoden und Techniken gefährdet. ATA kann diese Arten von Gefährdungen erkennen, indem es das Verhalten der jeweiligen Entität analysiert und Auffälligkeiten der Vorgänge, die von der Entität ausgeführt werden, erkennt und vor diesen warnt.

### <a name="lateral-movement"></a>Seitliche Verschiebung
Um Erkennung von seitlicher Verschiebung (Bewegung) zu bieten, wenn Benutzer Anmeldeinformationen nutzen, die Zugriff auf einige Ressourcen ermöglichen, auf die die Benutzer eigentlich keinen Zugriff haben sollen, nutzt ATA sowohl verhaltensbasierte Analysen auf Machine Learning-Basis als auch bekannte Erkennung von böswilligen Attacken und Techniken.
Mithilfe von verhaltensbasierten Analysen und Machine Learning erkennt ATA nicht ordnungsgemäßen Zugriff auf Ressourcen, ungewöhnliche Geräte, die verwendet werden, und weitere Indikatoren, die auf seitliche Verschiebungen hindeuten.
Darüber hinaus kann ATA seitliche Verschiebungen erkennen, indem die Techniken erkannt werden, die Angreifer für die Durchführung seitlicher Verschiebungen einsetzen, zum Beispiel:
-   **Pass-the-Ticket** Bei Pass-the-Ticket-Angriffen stehlen die Angreifer ein Kerberos-Ticket von einem Computer und verwenden es, um Zugriff auf einen anderen Computer zu erhalten, indem sie die Identität einer Entität in Ihrem Netzwerk annehmen.
-   **Pass-the-Hash** Bei Pass-the-Hash-Angriffen stehlen die Angreifer den NTLM-Hash einer Entität, verwenden ihn für die Authentifizierung mit NTLM, nehmen die Identität einer Entität an und erhalten Zugriff auf Ressourcen in Ihrem Netzwerk.
-   **Overpass-The-Hash** Bei Overpass-The-Hash-Angriffen verwendet der Angreifer einen gestohlenen NTLM-Hash für die Kerberos-Authentifizierung, um ein gültiges Kerberos-TGT-Ticket zu erhalten, das anschließend genutzt wird, um sich als gültiger Benutzer zu authentifizieren und Zugriff auf Ressourcen in Ihrem Netzwerk zu erhalten.
-   **Ungewöhnliches Verhalten** Seitliche Verschiebung ist eine Technik, die häufig von Angreifern verwendet wird, um sich zwischen Geräten und Bereichen im Netzwerk des Opfers zu bewegen, um Zugriff auf privilegierte Anmeldeinformationen oder vertrauliche Informationen zu erhalten, an denen der Angreifer interessiert ist. ATA kann seitliche Verschiebung durch Analysieren des Verhaltens von Benutzern und Geräten sowie deren Beziehungen im Unternehmensnetzwerk erkennen und kann ungewöhnliche Zugriffsmuster erkennen, die auf eine seitliche Bewegung hindeuten, die von einem Angreifer ausgeführt wird.

### <a name="privilege-escalation"></a>Ausweitung von Berechtigungen
ATA erkennt erfolgreiche und versuchte Berechtigungsausweitungsangriffe, in denen Angreifer versuchen, vorhandene Berechtigungen auszuweiten und diese mehrmals zu verwenden, um schließlich die vollständige Kontrolle über die Umgebung des Opfers zu erlangen.
ATA ermöglicht Erkennung von Berechtigungsausweitung durch Kombinieren von verhaltensbasierten Analysen, um ungewöhnliches Verhaltens von privilegierten Konten zu erkennen, und Erkennung von bekannten und böswilligen Angriffen und Techniken, die häufig zur Ausweitung von Berechtigungen verwendet werden, so beispielsweise:
-   **MS14-068-Exploit (gefälschtes PAC)** Bei gefälschten PACs handelt es sich um Angriffe, bei denen der Angreifer Autorisierungsdaten in seinem gültigen TGT-Ticket in Form eines gefälschten Autorisierungsheaders platziert, die ihm zusätzliche Berechtigungen gewähren, die ihm von seiner Organisation nicht gewährt wurden. In diesem Szenario nutzt der Angreifer zuvor kompromittierte Anmeldeinformationen oder Anmeldeinformationen, die durch seitliche Verschiebungen beschafft wurden.
-   **MS11-013-Exploit (Silver PAC)** Ein MS11-013-Exploit-Angriff ist eine Erhöhung des Berechtigungssicherheitsrisikos in Kerberos, die es für bestimmte Aspekte eines Kerberos-Diensttickets ermöglicht, dass es gefälscht wird. Ein böswilliger Benutzer oder ein Angreifer, der dieses Sicherheitsrisiko erfolgreich ausnutzt, kann ein Token abrufen, das erhöhte Rechte auf dem Domänencontroller hat. In diesem Szenario nutzt der Angreifer zuvor kompromittierte Anmeldeinformationen oder Anmeldeinformationen, die durch seitliche Verschiebungen beschafft wurden.

### <a name="domain-dominance"></a>Domänendominanz
ATA erkennt Angreifer, die versuchen oder Erfolg damit hatten, vollständige Kontrolle und Dominanz über die Umgebung des Opfers zu erlangen. Dazu führt ATA Erkennung über bekannte Techniken aus, die von Angreifern genutzt werden, wozu gehören:
-   **Skeleton Key-Malware** Bei Skeleton Key-Angriffen wird Malware auf Ihrem Domänencontroller installiert, die es den Angreifern ermöglicht, sich als beliebiger Benutzer zu authentifizieren. Gültige Benutzer können sich währenddessen weiterhin anmelden.
-   **Golden Ticket** Bei Golden Ticket-Angriffen stiehlt ein Angreifer die KBTGT-Anmeldeinformationen, das Kerberos Golden Ticket. Dieses Ticket ermöglicht es dem Angreifer, offline ein TGT-Ticket zu erstellen, mit dem er dann Zugriff auf Ressourcen im Netzwerk erhält.
-   **Remoteausführung** Angreifer können versuchen, die Kontrolle über Ihr Netzwerk zu erlangen, indem sie Code remote auf Ihrem Domänencontroller ausführen.
-   **Böswillige Replikationsanforderungen** In Active Directory-Umgebungen (AD) erfolgt regelmäßig eine Replikation zwischen Domänencontrollern. Ein Angreifer kann eine AD-Replikationsanforderung (manchmal durch Annehmen der Identität eines Domänencontrollers) vortäuschen, wodurch es dem Angreifer gestattet wird, die in AD gespeicherten Daten abzurufen, einschließlich Kennworthashes, ohne auffallendere Techniken wie Volumeschattenkopie zu nutzen.


## <a name="whats-next"></a>Wie geht es weiter?

-   Weitere Informationen zum Integrieren von ATA in Ihr Netzwerk: [ATA-Architektur](/advanced-threat-analytics/plan-design/ata-architecture)

-   Erste Schritte bei der Bereitstellung von ATA: [Installieren von ATA](/advanced-threat-analytics/deploy-use/install-ata)

## <a name="see-also"></a>Siehe auch
[Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Feb17_HO1-->


