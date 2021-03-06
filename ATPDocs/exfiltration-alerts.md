---
title: Tutorial zu Exfiltrationswarnungen in Microsoft Defender for Identity
description: In diesem Artikel werden die Microsoft Defender for Identity-Warnungen erläutert, die ausgegeben werden, wenn Angriffe in Ihrer Organisation erkannt werden, die in der Regel Teil der Maßnahmen der Exfiltrationsphase sind.
ms.date: 10/26/2020
ms.topic: tutorial
ms.openlocfilehash: fe933d2fa989645fbe0ea7fd586816905e75ee6a
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/03/2020
ms.locfileid: "96544027"
---
# <a name="tutorial-exfiltration-alerts"></a>Tutorial: Warnungen zu Exfiltration

Cyberangriffe werden üblicherweise auf alle zugänglichen Entitäten wie etwa Benutzer mit geringen Rechten durchgeführt. Anschließend dringt der Angreifer schnell im internen Netzwerk vor (Lateral Movement), um Zugriff auf wertvolle Ressourcen zu erhalten. Dabei kann es sich um sensible Konten, Konten von Domänenadministratoren oder streng vertrauliche Daten handeln. [!INCLUDE [Product long](includes/product-long.md)] identifiziert diese komplexen Bedrohungen an der Quelle über die gesamte Kette der Angriffsabwehr hinweg und ordnet sie in die folgenden Phasen ein:

1. [Reconnaissance](reconnaissance-alerts.md)
1. [Kompromittierte Anmeldeinformationen](compromised-credentials-alerts.md)
1. [Seitliche Verschiebung](lateral-movement-alerts.md)
1. [Warnungen zu Domänendominanz](domain-dominance-alerts.md)
1. **Exfiltration**

Weitere Informationen zur Struktur und zu gängigen Komponenten aller [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnungen finden Sie unter [Grundlegendes zu Sicherheitswarnungen](understanding-security-alerts.md). Weitere Informationen zu **True Positive (TP)** , **Benign True Positive (B-TP)** (unschädlich richtig positiv) und **False Positive (FP)** finden Sie unter [Klassifizierungen der Sicherheitswarnungen](understanding-security-alerts.md#security-alert-classifications).

Mit den folgenden Sicherheitswarnungen können Sie verdächtige Aktivitäten der Phase **Exfiltration** identifizieren und beheben, die von [!INCLUDE [Product short](includes/product-short.md)] in Ihrem Netzwerk erkannt wurden. In diesem Tutorial machen Sie sich mit den folgenden Angriffstypen vertraut und erfahren, wie Sie diese klassifizieren, verhindern und beheben:

> [!div class="checklist"]
>
> - Datenexfiltration über den SMB – (externe ID 2030)
> - Verdächtige Kommunikation über DNS (externe ID 2031)

## <a name="data-exfiltration-over-smb-external-id-2030"></a>Datenexfiltration über den SMB – (externe ID 2030)

**Beschreibung**

Domänencontroller enthalten Organisationsdaten mit der höchsten Vertraulichkeit. Die meisten Angreifer versuchen vorrangig, auf den Domänencontroller zuzugreifen, um an die vertraulichsten Daten zu gelangen. Die Exfiltration der auf dem Domänencontroller gespeicherten Datei „Ntds.dit“ ermöglicht es einem Angreifer beispielsweise, ein Kerberos Ticket Granting Ticket (TGT) zu fälschen, das den Zugriff auf jede beliebige Ressource autorisiert. Mit einem gefälschten Kerberos-TGT kann der Angreifer den Ablaufzeitpunkt des Tickets auf einen beliebigen Zeitpunkt festlegen. Die [!INCLUDE [Product short](includes/product-short.md)]-Warnung **Datenexfiltration über SMB** wird ausgelöst, wenn verdächtige Datenübertragungen von Ihren überwachten Domänencontrollern festgestellt werden.

**TP, B-TP oder FP?**

1. Sollen diese Benutzer diese Dateien auf diesen Computer kopieren?
    - Lautet die Antwort **Ja**, **Schließen** Sie die Sicherheitswarnung, und schließen Sie den Computer als **B-TP**-Aktivität aus.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie die [Quellbenutzer](investigate-a-user.md).
1. Untersuchen Sie die [Quell- und Zielcomputer](investigate-a-computer.md) der Kopien.

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

1. Setzen Sie das Kennwort der Quellbenutzer zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Kontrollieren Sie den Quellcomputer.
    - Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
    - Suchen und entfernen Sie die Dateien, die kopiert wurden.  
    Überprüfen Sie, ob für diese Dateien weitere Aktivitäten ausgeführt wurden. Wurden sie an einen anderen Ort übertragen? Überprüfen Sie, ob die Dateien außerhalb des Organisationsnetzwerks übertragen wurden.
    - Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Sollte es sich bei einer der Dateien um die Datei **ntds.dit** handeln:
    - Ändern Sie das Kennwort für das Kerberos Ticket Granting Ticket (KRBTGT) zweimal gemäß den Anweisungen unter [KRBTGT Account Password Reset Scripts now available for customers (Skripts zum Zurücksetzen von Kennwörtern des KRBTGT-Kontos stehen Kunden jetzt zur Verfügung)](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) mithilfe des [Reset the KRBTGT account password/keys tool (Tools zum Zurücksetzen des Kennworts/Schlüssels eines KRBTGT-Kontos)](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).
    - Durch zweimaliges Zurücksetzen von KRBTGT werden alle Kerberos-Tickets in dieser Domäne ungültig. Dies bedeutet, dass **alle** Dienste außer Kraft gesetzt werden und erst wieder funktionieren, wenn sie erneuert werden. In einigen Fällen muss der Dienst neu gestartet werden.

    - **Planen Sie daher das zweimalige Zurücksetzen von KRBTGT genau. Das zweimalige Zurücksetzen von KRBTGT wirkt sich auf alle Computer, Server und Benutzer in der Umgebung aus.**

    - Schließen Sie alle bestehenden Sitzungen der Domänencontroller.

## <a name="suspicious-communication-over-dns-external-id-2031"></a>Verdächtige Kommunikation über DNS (externe ID 2031)

*Vorheriger Name*: Verdächtige Kommunikation über DNS

**Beschreibung**

In den meisten Organisationen wird das DNS-Protokoll nicht überwacht und nur selten wegen böswilliger Angriffe blockiert. Das gibt einem Angreifer auf einem kompromittierten Computer die Möglichkeit, das DNS-Protokoll zu missbrauchen. Schädliche Kommunikation über DNS kann für Datenexfiltration, Command-and-Control-Zugriff und/oder zur Umgehung von Einschränkungen des Unternehmensnetzwerks verwendet werden.

**TP, B-TP oder FP?**

In einigen Unternehmen wird DNS auf legitime Weise für die reguläre Kommunikation verwendet. Gehen Sie folgendermaßen vor, um den Status der Sicherheitswarnung zu bestimmen:

1. Überprüfen Sie, ob die registrierte Abfragedomäne zu einer vertrauenswürdigen Quelle gehört, wie etwa Ihrem Virenschutzanbieter.
    - Wenn die Domäne bekannt und vertrauenswürdig ist und DNS-Abfragen zulässig sind, handelt es sich wahrscheinlich um eine **B-TP**-Aktivität. *Schließen* Sie die Sicherheitswarnung, und schließen Sie die Domäne aus zukünftigen Warnungen aus.
    - Ist die registrierte Abfragedomäne nicht vertrauenswürdig, identifizieren Sie den Prozess, der die Anforderung erstellt hat, auf dem Quellcomputer. Verwenden Sie zur Unterstützung bei dieser Aufgabe den [Prozessmonitor](/sysinternals/downloads/procmon).

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Suchen Sie auf dem Zielcomputer, bei dem es sich um einen DNS-Server handeln sollte, nach den Datensätzen der entsprechenden Domäne.
    - Welcher IP ist sie zugeordnet?
    - Wer ist der Besitzer der Domäne?
    - Wo befindet sich die IP-Adresse?
1. Untersuchen Sie die [Quell- und Zielcomputer](investigate-a-computer.md).

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

1. Kontrollieren Sie den Quellcomputer.
    - Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
    - Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Ist die registrierte Abfragedomäne nach Ihrer Untersuchung weiterhin nicht vertrauenswürdig, wird empfohlen, die Zieldomäne zu blockieren, um zukünftig jede Kommunikation zu vermeiden.

> [!NOTE]
> *Verdächtige Kommunikation über DNS*: Diese Sicherheitswarnungen listen die vermutete Domäne auf. Neue Domänen oder Domänen, die erst vor Kurzem hinzugefügt wurden, [!INCLUDE [Product short](includes/product-short.md)] aber noch nicht bekannt sind und nicht erkannt werden, von denen aber feststeht, dass sie Teil Ihrer Organisation sind, können geschlossen werden.

## <a name="see-also"></a>Weitere Informationen

- [Untersuchen eines Computers](investigate-a-computer.md)
- [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md)
- [Arbeiten mit Lateral Movement-Pfaden](use-case-lateral-movement-path.md)
- [Warnungen zu Reconnaissance](reconnaissance-alerts.md)
- [Warnungen zu kompromittierten Anmeldeinformationen](compromised-credentials-alerts.md)
- [Lateral Movement-Warnungen](lateral-movement-alerts.md)
- [Warnungen zu Domänendominanz](domain-dominance-alerts.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
