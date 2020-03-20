---
title: Tutorial zu Azure ATP-Sicherheitswarnungen
d|Description: This article explains how to use and understand Azure ATP security alerts.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 1/13/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 671747d5-faed-4352-a871-17b58fdc6574
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 863211852883cc2db2192abd1dffbe87ab3d52f9
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2020
ms.locfileid: "79414623"
---
# <a name="tutorial-understanding-security-alerts"></a>Tutorial: Grundlegendes zu Sicherheitswarnungen

Mit Azure ATP-Sicherheitswarnungen wird in verständlicher Sprache und anhand von Grafiken dargestellt, welche verdächtigen Aktivitäten in Ihrem Netzwerk identifiziert wurden und welche Benutzer und Computer an der Bedrohung beteiligt sind. Warnungen werden nach ihrem Schweregrad eingestuft. Sie sind für ein einfaches visuelles Filtern farbcodiert und werden nach Bedrohungsphasen sortiert. Jede Warnung soll Ihnen dabei helfen, einen schnellen Überblick darüber zu erhalten, was genau in Ihrem Netzwerk passiert. Damit Sie leicht und direkt weitere Untersuchungen durchführen können, enthalten Beweislisten für Sicherheitswarnungen einen direkten Link zu den betroffenen Benutzern und Computern.

In diesem Tutorial wird erläutert, wie Azure ATP-Sicherheitswarnungen aufgebaut sind und wie sie verwendet werden: 

> [!div class="checklist"]
> * Aufbau der Sicherheitswarnungen
> * Klassifizierungen der Sicherheitswarnungen
> * Kategorien der Sicherheitswarnungen
> * Erweiterte Untersuchung der Sicherheitswarnungen
> * Verwandte Entitäten
> * Azure ATP und NNR (Network Name Resolution; Auflösung des Netzwerknamens)


## <a name="security-alert-structure"></a>Aufbau der Sicherheitswarnungen

Jede Azure ATP-Sicherheitswarnung enthält folgende Informationen:
 
- **Titel der Warnung** <br> Offizielle Azure ATP-Bezeichnung der Warnung.
- **Beschreibung** <br> Kurze Erklärung der Vorfälle.
- **Beweise** <br> Weitere relevante Informationen und verwandte Daten zu den Vorgängen, die im weiteren Untersuchungsprozess hilfreich sind.
- **Excel-Download** <br> Ausführlicher Excel-Downloadbericht zur Analyse.

![Aufbau einer Azure ATP-Sicherheitswarnung](media/security-alert-structure.png)

## <a name="security-alert-classifications"></a>Klassifizierungen der Sicherheitswarnungen

Nach einer gründlichen Untersuchung können alle Azure ATP-Sicherheitswarnungen als einer der folgenden Aktivitätstypen klassifiziert werden:

- **Richtig positiv (True Positive, TP):** Eine von Azure ATP erkannte schädliche Aktion.

- **Unschädlich richtig positiv (Benign True Positive, B-TP)** : Eine von Azure ATP erkannte Aktion, die tatsächlich durchgeführt wurde, aber nicht böswillig ist, wie z.B. ein Penetrationstest oder eine bekannte Aktivität, die von einer genehmigten Anwendung generiert wurde.

- **Falsch positiv (False Positive, FP)** : Ein falscher Alarm, das heißt, die Aktivität wurde nicht ausgeführt.

### <a name="is-the-security-alert-a-tp-b-tp-or-fp"></a>Unterscheidung der Sicherheitswarnung in TP, B-TP oder FP

Stellen Sie sich bei jeder Sicherheitswarnung die folgenden Fragen, um die Klassifizierung der Warnung zu ermitteln und über weitere Schritte zu entscheiden:

1. Wie häufig kommt die entsprechende Sicherheitswarnung in Ihrer Umgebung vor?
2. Wurde die Warnung durch dieselben Computer- oder Benutzertypen ausgelöst?
   Handelt es sich z.B. um Server mit derselben Rolle oder denselben Benutzern aus derselben Gruppe/Abteilung? Handelte es sich um ähnliche Computer oder Benutzer, können Sie diese eventuell ausschließen, um weitere FP-Warnungen künftig zu vermeiden.

Anmerkung: Eine zunehmende Anzahl von Warnungen des exakt selben Typs verringert in der Regel die Verdächtigkeits-/Wichtigkeitsstufe der Warnung. Überprüfen Sie bei wiederholten Warnungen die Konfiguration, und verschaffen Sie sich mithilfe der Details und Definitionen der Sicherheitswarnungen einen Überblick über die genaue Ursache des wiederholten Auftretens. 

## <a name="security-alert-categories"></a>Kategorien der Sicherheitswarnungen

Azure ATP-Sicherheitswarnungen werden in die folgenden Kategorien oder Phasen unterteilt, wie die Phasen in einer typischen „Kill Chain“ eines Cyberangriffs. Die folgenden Links enthalten weitere Informationen zu den einzelnen Phasen sowie den Warnungen, die die Angriffe erkennen sollen:

- [Warnungen zu Reconnaissance](atp-reconnaissance-alerts.md)
- [Warnungen zu kompromittierten Anmeldeinformationen](atp-compromised-credentials-alerts.md)
- [Lateral Movement-Warnungen](atp-lateral-movement-alerts.md)
- [Warnungen zu Domänendominanz](atp-domain-dominance-alerts.md)
- [Warnungen zu Exfiltration](atp-exfiltration-alerts.md)

## <a name="advanced-security-alert-investigation"></a>Erweiterte Untersuchung der Sicherheitswarnungen

Laden Sie den ausführlichen Excel-Warnungsbericht herunter, um detaillierte Informationen zu einer Sicherheitswarnung zu erhalten.

1. Klicken Sie in der rechten oberen Ecke auf die drei Punkte, die bei jeder Warnung angezeigt werden, und wählen Sie *Details herunterladen* aus.
 
Jeder Excel-Download zu Azure ATP-Sicherheitswarnungen enthält die folgenden Informationen:   
- Zusammenfassung: Die erste Registerkarte enthält die wichtigsten Punkte der Warnung. 
  - Titel 
  - Beschreibung 
  - Startzeit (UTC) 
  - Endzeit (UTC) 
  - Schweregrad: niedrig/mittel/hoch
  - Status: offen/geschlossen
  - Zeitpunkt des Statusupdates (UTC)
  - In Browser anzeigen
- Alle betroffenen Entitäten (Konten, Computer und Ressourcen) werden nach ihrer Rolle getrennt aufgelistet. 
    - Quelle, Ziel oder Angriff – je nach Warnung 
- Die meisten Registerkarten enthalten für jede Entität die folgenden Daten: 
  - Name
  - Details 
  - Typ 
  - SAM-Name  
  - Quellcomputer
  - Quellbenutzer (sofern verfügbar)
  - Domänencontroller
  - Aufgerufene Ressource: Zeitpunkt, Computer, Name, Details, Typ, Dienst
  - Zusätzliche Registerkarten für jede Warnung: 
      - Für angegriffene Konten bei vermuteten Brute-Force-Angriffen.
      - Für DNS-Server (Domain Name System), wenn bei dem vermuteten Angriff Reconnaissance über Netzwerkzuordnungen (DNS) verwendet wurde.
  - Verwandte Entitäten: ID, Typ, Name, eindeutige JSON-Entität, eindeutiges JSON-Entitätsprofil
- Alle mit Azure ATP-Sensoren erfassten reinen Aktivitäten, die mit der Warnung verknüpft sind (Netzwerk- oder Ereignisaktivitäten), wie etwa:
  - Netzwerkaktivitäten
  - Ereignisaktivitäten

![Betroffene Entitäten](media/involved-entities.png)

### <a name="related-entities"></a>Verwandte Entitäten

Die letzte Registerkarte jeder Warnung enthält die **Verwandten Entitäten**. Verwandte Entitäten sind alle an einer verdächtigen Aktivität beteiligten Entitäten. Sie werden unabhängig von der Rolle dargestellt, die sie bei der Warnung gespielt haben. Jede Entität verfügt über zwei JSON-Dateien: die eindeutige JSON-Entität und die eindeutige JSON-Profilentität. Diese beiden JSON-Dateien enthalten weitere Informationen zur Entität und helfen bei der Untersuchung der Warnung. 
 
**Eindeutige JSON-Entität**
 
Enthält die Daten, die Azure ATP aus Active Directory zu dem Konto erhalten hat. Dazu zählen alle Attribute wie *Distinguished Name*, *SID*, <em>LockoutTime und *PasswordExpiryTime</em>. Für Benutzerkonten sind Daten enthalten wie *Department*  (Abteilung), *Mail* (E-Mail) und *PhoneNumber* (Telefonnummer). Für Computerkonten sind Daten enthalten wie *OperatingSystem*, <em>IsDomainController und *DnsName</em>.

**Eindeutiges JSON-Entitätsprofil**

Enthält alle Daten, für die Azure ATP in der Entität ein Profil erstellt hat. Azure ATP verwendet die Netzwerk- und Ereignisaktivitäten, die für weitere Informationen über die Benutzer und Computer der Umgebung erfasst wurden. Azure ATP erstellt ein Profil für relevante Informationen für jede Entität. Diese Informationen tragen zum Erkennen von Bedrohungen durch Azure ATP bei.

![Verwandte Entitäten](media/related-entities.png)
 
### <a name="how-can-i-use-azure-atp-information-in-an-investigation"></a>Wie verwende ich Azure ATP-Informationen bei einer Untersuchung? 

Je nach Bedarf kann eine Untersuchung mehr oder weniger ausführlich durchgeführt werden. Sie können die von Azure ATP bereitgestellten Daten etwa für die Beantwortung der folgenden Fragen verwenden:

- Gehören alle verwandten Benutzer zur gleichen Gruppe oder Abteilung?
- Verwenden verwandte Benutzer dieselben Ressourcen, Anwendungen oder Computer?
- Ist ein Konto aktiv, obwohl die PasswordExpiryTime bereits überschritten ist?

## <a name="azure-atp-and-nnr-network-name-resolution"></a>Azure ATP und NNR (Network Name Resolution; Auflösung des Netzwerknamens)

Die Azure ATP-Erkennungsfunktionen basieren auf einer aktiven Netzwerknamensauflösung (Network Name Resolution, NNR), bei der IP-Adressen in Computer innerhalb der Organisation aufgelöst werden. Durch die Verwendung von NNR ordnet Azure ATP reinen Aktivitäten (mit IP-Adressen) die entsprechenden, an der Aktivität beteiligten Computer zu. Auf Grundlage der reinen Aktivitäten erstellt Azure ATP ein Profil der Entitäten, wie etwa Computer, und generiert Warnungen.

NNR-Daten spielen beim Erkennen der folgenden Warnungen eine entscheidende Rolle:
- Suspected identity theft (pass-the-ticket) (Verdacht auf Identitätsdiebstahl (Pass-the-Ticket)) 
- Suspected DCSync attack (replication of directory services) (Verdacht auf einen DCSync-Angriff (Replikation von Verzeichnisdiensten))
- Network mapping reconnaissance (DNS) (Reconnaissance über Netzwerkzuordnung (DNS))

Verwenden Sie die im Downloadbericht der Warnung auf der Registerkarte **Netzwerkaktivitäten** bereitgestellten NNR-Informationen, um festzustellen, ob es sich bei einer Warnung um eine **FP**-Aktivität handelt. Bei **FP**-Warnungen liegt der NNR-Zuverlässigkeitswert üblicherweise im niedrigen Bereich.

Die Daten des Downloadberichts werden in zwei Spalten angezeigt: 
- **Quell-/Zielcomputer** 

    - *Zuverlässigkeit*: Ein niedriger Wert deutet möglicherweise auf eine falsche Namensauflösung hin.
- **Quell-/Zielcomputer**
    - *Auflösungsmethode*: Zeigt die NNR-Methoden an, die zum Auflösen der IP-Adressen in Computer innerhalb der Organisation verwendet wurden.

![Netzwerkaktivitäten](media/network-activities.png)

Weitere Informationen zum Arbeiten mit Azure ATP-Sicherheitswarnungen finden Sie unter [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md).

## <a name="see-also"></a>Weitere Informationen

- [Untersuchen eines Benutzers](investigate-a-user.md)
- [Untersuchen eines Computers](investigate-a-computer.md)
- [Arbeiten mit Lateral Movement-Pfaden](use-case-lateral-movement-path.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
