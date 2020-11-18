---
title: Tutorial zu Microsoft Defender for Identity-Sicherheitswarnungen
description: In diesem Artikel werden Sicherheitswarnungen von Microsoft Defender for Identity und deren Verwendung näher erläutert.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/27/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 27df0fb3be637b2a3390df9378f68b2db9a10b8d
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848906"
---
# <a name="understanding-security-alerts"></a>Grundlegendes zu Sicherheitswarnungen

Mit [!INCLUDE [Product long](includes/product-long.md)]-Sicherheitswarnungen wird in verständlicher Sprache und anhand von Grafiken dargestellt, welche verdächtigen Aktivitäten in Ihrem Netzwerk identifiziert wurden und welche Akteure und Computer an der Bedrohung beteiligt sind. Warnungen werden nach ihrem Schweregrad eingestuft. Sie sind für ein einfaches visuelles Filtern farbcodiert und werden nach Bedrohungsphasen sortiert. Jede Warnung soll Ihnen dabei helfen, einen schnellen Überblick darüber zu erhalten, was genau in Ihrem Netzwerk passiert. Damit Sie einfach und direkt weitere Untersuchungen durchführen können, enthalten Beweislisten für Sicherheitswarnungen direkte Links zu den betroffenen Benutzern und Computern.

In diesem Tutorial erfahren Sie, wie [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnungen aufgebaut sind und wie sie verwendet werden:

> [!div class="checklist"]
>
> - Aufbau der Sicherheitswarnungen
> - Klassifizierungen der Sicherheitswarnungen
> - Kategorien der Sicherheitswarnungen
> - Erweiterte Untersuchung der Sicherheitswarnungen
> - Verwandte Entitäten
> - [!INCLUDE [Product short](includes/product-short.md)] und Netzwerknamensauflösung (Network Name Resolution, NNR)

## <a name="security-alert-structure"></a>Aufbau der Sicherheitswarnungen

Jede [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnung enthält folgende Informationen:

- **Titel der Warnung**  
Offizieller [!INCLUDE [Product short](includes/product-short.md)]-Name der Warnung.
- **Beschreibung**  
Kurze Erklärung der Vorfälle.
- **Beweise**  
Weitere relevante Informationen und verwandte Daten zu den Vorgängen, die im weiteren Untersuchungsprozess hilfreich sind.
- **Excel-Download**  
Ausführlicher Excel-Downloadbericht zur Analyse.

![Struktur der Sicherheitswarnungen von [!INCLUDE [Product short](includes/product-short.md)]](media/security-alert-structure.png)

## <a name="security-alert-classifications"></a>Klassifizierungen der Sicherheitswarnungen

Nach einer gründlichen Untersuchung können alle [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnungen als einer der folgenden Aktivitätstypen klassifiziert werden:

- **Richtig positiv (True Positive, TP):** Eine von [!INCLUDE [Product short](includes/product-short.md)] erkannte schädliche Aktion.

- **Unschädlich richtig positiv (Benign True Positive, B-TP)** : Eine von [!INCLUDE [Product short](includes/product-short.md)] erkannte Aktion, die tatsächlich durchgeführt wurde, aber nicht schädlich ist, z. B. ein Penetrationstest oder eine bekannte Aktivität, die von einer genehmigten Anwendung generiert wurde.

- **Falsch positiv (False Positive, FP)** : Dies ist ein falscher Alarm, d. h., die Aktivität wurde nicht ausgeführt.

### <a name="is-the-security-alert-a-tp-b-tp-or-fp"></a>Unterscheidung der Sicherheitswarnung in TP, B-TP oder FP

Stellen Sie sich bei jeder Sicherheitswarnung die folgenden Fragen, um die Klassifizierung der Warnung zu ermitteln und über weitere Schritte zu entscheiden:

1. Wie häufig kommt die entsprechende Sicherheitswarnung in Ihrer Umgebung vor?
1. Wurde die Warnung durch dieselben Computer- oder Benutzertypen ausgelöst?
   Handelt es sich z.B. um Server mit derselben Rolle oder denselben Benutzern aus derselben Gruppe/Abteilung? Handelte es sich um ähnliche Computer oder Benutzer, können Sie diese eventuell ausschließen, um weitere FP-Warnungen künftig zu vermeiden.

Anmerkung: Eine zunehmende Anzahl von Warnungen des exakt selben Typs verringert in der Regel die Verdächtigkeits-/Wichtigkeitsstufe der Warnung. Überprüfen Sie bei wiederholten Warnungen die Konfiguration, und verschaffen Sie sich mithilfe der Details und Definitionen der Sicherheitswarnungen einen Überblick über die genaue Ursache des wiederholten Auftretens.

## <a name="security-alert-categories"></a>Kategorien der Sicherheitswarnungen

[!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnungen werden in die folgenden Kategorien bzw. Phasen unterteilt, ähnlich wie die Phasen in einer typischen „Kill Chain“ eines Cyberangriffs. Die folgenden Links enthalten weitere Informationen zu den einzelnen Phasen sowie den Warnungen, die die Angriffe erkennen sollen:

- [Warnungen zu Reconnaissance](reconnaissance-alerts.md)
- [Warnungen zu kompromittierten Anmeldeinformationen](compromised-credentials-alerts.md)
- [Lateral Movement-Warnungen](lateral-movement-alerts.md)
- [Warnungen zu Domänendominanz](domain-dominance-alerts.md)
- [Warnungen zu Exfiltration](exfiltration-alerts.md)

## <a name="advanced-security-alert-investigation"></a>Erweiterte Untersuchung der Sicherheitswarnungen

Laden Sie den ausführlichen Excel-Warnungsbericht herunter, um detaillierte Informationen zu einer Sicherheitswarnung zu erhalten.

1. Klicken Sie in der rechten oberen Ecke auf die drei Punkte, die bei jeder Warnung angezeigt werden, und wählen Sie *Details herunterladen* aus.

Jeder Excel-Download von [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnungen enthält die folgenden Informationen:

- Zusammenfassung: Die erste Registerkarte enthält die wichtigsten Punkte der Warnung.
  - Titel
  - BESCHREIBUNG
  - Startzeit (UTC)
  - Endzeit (UTC)
  - Schweregrad: niedrig/mittel/hoch
  - Status: offen/geschlossen
  - Zeitpunkt des Statusupdates (UTC)
  - Anzeigen im Browser
- Alle betroffenen Entitäten (Konten, Computer und Ressourcen) werden nach ihrer Rolle getrennt aufgelistet.
  - Quelle, Ziel oder Angriff – je nach Warnung
- Die meisten Registerkarten enthalten für jede Entität die folgenden Daten:
  - Name
  - Details
  - type
  - SAM-Name
  - Quellcomputer
  - Quellbenutzer (sofern verfügbar)
  - Domänencontroller
  - Aufgerufene Ressource: Zeitpunkt, Computer, Name, Details, Typ, Dienst
  - Zusätzliche Registerkarten für jede Warnung:
    - Für angegriffene Konten bei vermuteten Brute-Force-Angriffen.
    - Für DNS-Server (Domain Name System), wenn bei dem vermuteten Angriff Reconnaissance über Netzwerkzuordnungen (DNS) verwendet wurde.
  - Verwandte Entitäten: ID, Typ, Name, eindeutige JSON-Entität, eindeutiges JSON-Entitätsprofil
- Alle mit [!INCLUDE [Product short](includes/product-short.md)]-Sensoren erfassten reinen Aktivitäten in Zusammenhang mit der Warnung (Netzwerk- oder Ereignisaktivitäten), wie etwa:
  - Netzwerkaktivitäten
  - Ereignisaktivitäten

![Betroffene Entitäten](media/involved-entities.png)

### <a name="related-entities"></a>Verwandte Entitäten

Die letzte Registerkarte jeder Warnung enthält die **Verwandten Entitäten**. Verwandte Entitäten sind alle an einer verdächtigen Aktivität beteiligten Entitäten. Sie werden unabhängig von der Rolle dargestellt, die sie bei der Warnung gespielt haben. Jede Entität verfügt über zwei JSON-Dateien: die eindeutige JSON-Entität und die eindeutige JSON-Profilentität. Diese beiden JSON-Dateien enthalten weitere Informationen zur Entität und helfen bei der Untersuchung der Warnung.

**Eindeutige JSON-Entität**

Enthält die Daten, die [!INCLUDE [Product short](includes/product-short.md)] aus Active Directory zu dem Konto erhalten hat. Dazu zählen alle Attribute wie *Distinguished Name*, *SID*, *LockoutTime* und *PasswordExpiryTime*. Für Benutzerkonten sind Daten enthalten wie *Department* (Abteilung), *Mail* (E-Mail) und *PhoneNumber* (Telefonnummer). Für Computerkonten sind Daten enthalten wie *OperatingSystem*, *IsDomainController* und *DnsName*.

**Eindeutiges JSON-Entitätsprofil**

Enthält alle Daten, für die [!INCLUDE [Product short](includes/product-short.md)] in der Entität ein Profil erstellt hat. [!INCLUDE [Product short](includes/product-short.md)] verwendet die erfassten Netzwerk- und Ereignisaktivitäten, um weitere Informationen zu den Benutzern und Computern der Umgebung zu erhalten. [!INCLUDE [Product short](includes/product-short.md)] erstellt ein Profil der relevanten Informationen für jede Entität. Diese Informationen helfen [!INCLUDE [Product short](includes/product-short.md)] beim Erkennen von Bedrohungen.

![Verwandte Entitäten](media/related-entities.png)

### <a name="how-can-i-use-product-short-information-in-an-investigation"></a>Wie verwende ich [!INCLUDE [Product short](includes/product-short.md)]-Informationen bei einer Untersuchung?

Je nach Bedarf kann eine Untersuchung mehr oder weniger ausführlich durchgeführt werden. Sie können die von [!INCLUDE [Product short](includes/product-short.md)] bereitgestellten Daten beispielsweise für die Beantwortung der folgenden Fragen verwenden.

- Gehören alle verwandten Benutzer zur gleichen Gruppe oder Abteilung?
- Verwenden verwandte Benutzer dieselben Ressourcen, Anwendungen oder Computer?
- Ist ein Konto aktiv, obwohl die PasswordExpiryTime bereits überschritten ist?

## <a name="product-short-and-nnr-network-name-resolution"></a>[!INCLUDE [Product short](includes/product-short.md)] und Netzwerknamensauflösung (Network Name Resolution, NNR)

Die [!INCLUDE [Product short](includes/product-short.md)]-Erkennungsfunktionen basieren auf einer aktiven Netzwerknamensauflösung (Network Name Resolution, NNR), bei der IP-Adressen in Computer innerhalb der Organisation aufgelöst werden. Mithilfe von NNR kann [!INCLUDE [Product short](includes/product-short.md)] eine Korrelation zwischen den reinen Aktivitäten (mit IP-Adressen) und den an der Aktivität beteiligten Computer erstellen. Auf Grundlage der reinen Aktivitäten erstellt [!INCLUDE [Product short](includes/product-short.md)] ein Profil der Entitäten – einschließlich der Computer – und generiert Warnungen.

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

Weitere Informationen zum Arbeiten mit [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnungen finden Sie unter [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md).

## <a name="see-also"></a>Weitere Informationen

- [Untersuchen eines Benutzers](investigate-a-user.md)
- [Untersuchen eines Computers](investigate-a-computer.md)
- [Arbeiten mit Lateral Movement-Pfaden](use-case-lateral-movement-path.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
