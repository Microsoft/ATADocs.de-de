---
title: Microsoft Defender for Identity-Sicherheitswarnungen zur Domänendominanz
description: In diesem Artikel werden die Microsoft Defender for Identity-Warnungen erläutert, die ausgegeben werden, wenn Angriffe in Ihrer Organisation erkannt werden, die in der Regel Teil der Maßnahmen der Domänendominanzphase sind.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 733ae9db30bef0958234cf3ba3157b33533a85e1
ms.sourcegitcommit: 218ba562a2a109ff456b011004530f503a4e82c6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/04/2020
ms.locfileid: "93342444"
---
# <a name="tutorial-domain-dominance-alerts"></a>Tutorial: Warnungen zu Domänendominanz

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Cyberangriffe werden üblicherweise auf alle zugänglichen Entitäten wie etwa Benutzer mit geringen Rechten durchgeführt. Anschließend dringt der Angreifer schnell im internen Netzwerk vor (Lateral Movement), um Zugriff auf wertvolle Ressourcen zu erhalten. Dabei kann es sich um sensible Konten, Konten von Domänenadministratoren oder streng vertrauliche Daten handeln. [!INCLUDE [Product long](includes/product-long.md)] identifiziert diese komplexen Bedrohungen an der Quelle über die gesamte Kette der Angriffsabwehr hinweg und ordnet sie in die folgenden Phasen ein:

1. [Reconnaissance](reconnaissance-alerts.md)
1. [Kompromittierte Anmeldeinformationen](compromised-credentials-alerts.md)
1. [Seitliche Verschiebung](lateral-movement-alerts.md)
1. **Warnungen zu Domänendominanz**
1. [Exfiltration](exfiltration-alerts.md)

Weitere Informationen zur Struktur und zu gängigen Komponenten aller [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnungen finden Sie unter [Grundlegendes zu Sicherheitswarnungen](understanding-security-alerts.md). Weitere Informationen zu **True Positive (TP)** , **Benign True Positive (B-TP)** (unschädlich richtig positiv) und **False Positive (FP)** finden Sie unter [Klassifizierungen der Sicherheitswarnungen](understanding-security-alerts.md#security-alert-classifications).

Mit den folgenden Sicherheitswarnungen können Sie verdächtige Aktivitäten der Phase **Domänendominanz** identifizieren und beheben, die von [!INCLUDE [Product short](includes/product-short.md)] in Ihrem Netzwerk erkannt wurden. In diesem Tutorial machen Sie sich mit den folgenden Angriffstypen vertraut und erfahren, wie Sie diese klassifizieren, unterbinden und im Vorfeld verhindern:

> [!div class="checklist"]
>
> - Böswillige Anforderung des Datenschutz-API-Hauptschlüssels (externe ID 2020)
> - Versuch der Remotecodeausführung (externe ID 2019)
> - Vermuteter DCShadow-Angriff (Höherstufung eines Domänencontrollers) (externe ID 2028)
> - Vermuteter DCShadow-Angriff (Replikationsanforderung an Domänencontroller) (externe ID 2029)
> - Vermuteter DCSync-Angriff (Replikation der Verzeichnisdienste) (externe ID 2006)
> - Vermutete Golden Ticket-Verwendung (Herabstufung der Verschlüsselung) (externe ID 2009)
> - Vermutete Golden Ticket-Verwendung (gefälschte Autorisierungsdaten) (externe ID 2013)
> - Vermutete Golden Ticket-Verwendung (nicht vorhandenes Konto) (externe ID 2027)
> - Vermutete Golden Ticket-Verwendung (Ticketanomalie) (externe ID 2032)
> - Vermutete Golden Ticket-Verwendung (Ticketanomalie mithilfe von RBCD) (externe ID 2040)
> - Vermutete Golden Ticket-Verwendung (Zeitanomalie) (externe ID 2022)
> - Vermuteter Skeleton Key-Angriff (Herabstufung der Verschlüsselung) (externe ID 2010)
> - Verdächtige Hinzufügungen sensibler Gruppen (externe ID 2024)
> - Verdächtige Diensterstellung (externe ID 2026)

## <a name="malicious-request-of-data-protection-api-master-key-external-id-2020"></a>Böswillige Anforderung des Datenschutz-API-Hauptschlüssels (externe ID 2020)

*Vorheriger Name* : Böswillige Anforderung privater Informationen im Rahmen der Datensicherheit

**Beschreibung**

Die Datenschutz-API (DPAPI) wird von Windows verwendet, um von Browsern gespeicherte Kennwörter, verschlüsselte Dateien und andere sensible Daten sicher zu schützen. Domänencontroller enthalten einen Hauptschlüssel zur Sicherung, der verwendet werden kann, um alle mit der DPAPI verschlüsselten Geheimnisse auf mit einer Domäne verbundenen Windows-Computern zu entschlüsseln. Angreifer können den Hauptschlüssel verwenden, um sämtliche von der DPAPI geschützten Geheimnisse auf allen Computern zu entschlüsseln, die mit einer Domäne verbunden sind.
In dieser Erkennung wird eine [!INCLUDE [Product short](includes/product-short.md)]-Warnung ausgelöst, wenn die DPAPI zum Abrufen des Sicherungshauptschlüssels verwendet wird.

**Lernphase**

Nicht zutreffend

**TP, B-TP oder FP?**

Diese Aktivitäten werden möglicherweise von erweiterten Sicherheitsscannern für Active Directory Domain Services ausgeführt und sind in diesem Fall unbedenklich.

1. Überprüfen Sie, ob auf dem Quellcomputer ein von der Organisation genehmigter erweiterter Sicherheitsscanner für Active Directory Domain Services ausgeführt wird.

    - Wenn die Antwort **Ja** lautet und der Scanner nicht ausgeführt werden sollte, beheben Sie die Anwendungskonfiguration. Die Warnung ist eine **B-TP** -Aktivität und kann **geschlossen** werden.
    - Wenn die Antwort **Ja** lautet und der Scanner immer ausgeführt werden sollte, **schließen** Sie die Warnung, und schließen Sie diesen Computer aus. Es handelt sich wahrscheinlich um eine **B-TP** -Aktivität.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie den [Quellcomputer](investigate-a-computer.md).
1. Wenn ein [Quellbenutzer](investigate-a-user.md) vorhanden ist, untersuchen Sie diesen.

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

1. Setzen Sie das Kennwort des Quellbenutzers zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Kontrollieren Sie den Quellcomputer.
    - Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
    - Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch kompromittiert sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Der gestohlene private Schlüssel wird nie geändert. Dies bedeutet, dass der Akteur mit dem gestohlenen Schlüssel jederzeit geschützte Daten in der Zieldomäne entschlüsseln kann. Eine methodische Vorgehensweise zum Ändern des privaten Schlüssels gibt es nicht.
    - Verwenden Sie stattdessen den aktuellen privaten Schlüssel, erstellen Sie einen Schlüssel, und verschlüsseln Sie jeden Domänenhauptschlüssel noch einmal mit dem neuen privaten Schlüssel, um einen Schlüssel zu erstellen.

## <a name="remote-code-execution-attempt-external-id-2019"></a>Versuch der Remotecodeausführung (externe ID 2019)

*Vorheriger Name* : Versuchte Remote-Codeausführung

**Beschreibung**

Angreifer, die Administratoranmeldeinformationen kompromittiert haben oder einen Zero-Day-Exploit verwenden, können Remotebefehle auf Ihrem Domänencontroller ausführen. Damit können sie Beständigkeit erhalten, Informationen sammeln, oder DOS-Attacken (Denial of Service) ausführen usw. [!INCLUDE [Product short](includes/product-short.md)] erkennt PSexec- und PowerShell-Verbindungen sowie WMI-Remoteverbindungen.

**Lernphase**

Nicht zutreffend

**TP, B-TP oder FP?**

Zulässige administrative Aufgaben auf Domänencontrollern können von Arbeitsstationen für Administratoren, IT-Teammitgliedern und Dienstkonten durchgeführt werden.

1. Überprüfen Sie, ob diese Befehle tatsächlich vom Quellcomputer oder Benutzer auf Ihrem Domänencontroller ausgeführt werden sollen.
    - Wenn der Quellcomputer oder Benutzer diese Befehle ausführen darf, **schließen** Sie die Sicherheitswarnung als **B-TP** -Aktivität.
    - Wenn der Quellcomputer oder Benutzer diese Befehle jetzt und in Zukunft auf Ihrem lokalen Domänencontroller ausführen darf, handelt es sich um eine **B-TP** -Aktivität. **Schließen** Sie die Sicherheitswarnung, und schließen Sie den Computer aus.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie den [Quellcomputer](investigate-a-computer.md) und den [Benutzer](investigate-a-user.md).
1. Untersuchen Sie den [Domänencontroller](investigate-a-computer.md).

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung:**

**Wartung**

1. Setzen Sie das Kennwort der Quellbenutzer zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Isolieren Sie die Domänencontroller durch folgende Maßnahmen:
    - Unterbinden Sie die versuchte Remotecodeausführung.
    - Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der verdächtigen Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Kontrollieren Sie den Quellcomputer.
    - Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
    - Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der verdächtigen Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.

**Vorbeugung**

1. Schränken Sie den Remotezugriff auf Domänencontroller von Computern ein, die nicht den Tier 0 aufweisen.
1. Implementieren Sie [Zugriffseinschränkungen für Konten mit weitreichenden Rechten](/windows-server/identity/securing-privileged-access/securing-privileged-access). Dadurch wird sichergestellt, dass nur abgesicherte Computer eine Verbindung mit Domänencontrollern für Administratoren herstellen können.
1. Implementieren Sie weniger restriktive Zugriffseinschränkungen auf Domänencomputern, um bestimmten Benutzern die Erstellung von Diensten zu erlauben.

> [!NOTE]
> Warnungen zur versuchten Remotecodeausführung durch Powershell-Befehle werden nur von [!INCLUDE [Product short](includes/product-short.md)]-Sensoren unterstützt.

## <a name="suspected-dcshadow-attack-domain-controller-promotion-external-id-2028"></a>Vermuteter DCShadow-Angriff (Höherstufung eines Domänencontrollers) (externe ID 2028)

*Vorheriger Name* : Verdächtige Heraufstufung zu Domänencontrollern (potenzieller DcShadow-Angriff)

**Beschreibung**

Bei einem DCShadow-Angriff (Domain Controller Shadow) handelt es sich um einen Angriff, bei dem mithilfe einer schädlichen Replikation Verzeichnisobjekte geändert werden sollen. Ein solcher Angriff kann von jedem Computer aus erfolgen, indem mithilfe eines Replikationsvorgangs ein nicht autorisierter Domänencontroller erstellt wird.

Bei einem DCShadow-Angriff werden RPC und LDAP für folgende Vorgänge verwendet:

1. Das Computerkonto wird (mithilfe von Domänenadministratorrechten) als Domänencontroller registriert.
1. Die Replikation wird (unter Verwendung der gewährten Replikationsrechte) über DRSUAPI durchgeführt, und Änderungen werden an Verzeichnisobjekte gesendet.

Bei dieser [!INCLUDE [Product short](includes/product-short.md)]-Erkennung wird eine Sicherheitswarnung ausgelöst, wenn ein Computer im Netzwerk versucht, sich als nicht autorisierter Domänencontroller zu registrieren.

**Lernphase**

Nicht zutreffend

**TP, B-TP oder FP?**

Wenn der Quellcomputer ein Domänencontroller ist, wird [!INCLUDE [Product short](includes/product-short.md)] möglicherweise aufgrund fehlender Entscheidungssicherheit an der Identifikation gehindert.

1. Überprüfen Sie, ob der Quellcomputer ein Domänencontroller ist.
    Wenn die Antwort **Ja** lautet, **schließen** Sie die Warnung als **B-TP** -Aktivität.

Die Synchronisierung von Änderungen in Active Directory Domain Services kann etwas Zeit in Anspruch nehmen.

1. Ist der Quellcomputer ein Domänencontroller, der kürzlich höher gestuft wurde? Wenn die Antwort **Ja** lautet, **schließen** Sie die Warnung als **B-TP** -Aktivität.

Server und Anwendungen wie Azure AD Connect oder Geräte zur Leistungsüberwachung im Netzwerk können möglicherweise Daten aus Active Directory Domain Services replizieren.

1. Überprüfen Sie, ob diese Aktivitäten tatsächlich vom Quellcomputer ausgeführt werden sollen.

    - Wenn die Antwort **Ja** lautet, diese Aktivität aber in Zukunft nicht mehr vom Quellcomputer ausgeführt werden soll, beheben Sie die Konfiguration des Servers oder der Anwendung. **Schließen** Sie die Sicherheitswarnung als **B-TP** -Aktivität.

    - Wenn die Antwort **Ja** lautet und diese Aktivität in der Zukunft weiterhin vom Quellcomputer ausgeführt werden soll, **schließen** Sie die Sicherheitswarnung als **B-TP** -Aktivität, und schließen Sie den Computer aus, um zusätzliche B-TP-Warnungen zu vermeiden.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie den [Quellcomputer](investigate-a-computer.md).
1. Sehen Sie sich in der Ereignisanzeige [Active Directory-Ereignisse an, die im Protokoll der Verzeichnisdienste aufgezeichnet wurden](/previous-versions/windows/it-pro/windows-2000-server/cc961809(v=technet.10)/). Sie können das Protokoll verwenden, um Änderungen in Active Directory zu überwachen. Standardmäßig zeichnet Active Directory nur kritische Fehlerereignisse auf. Wenn diese Warnung aber wiederholt auftritt, aktivieren Sie diese Überwachung auf dem entsprechenden Domänencontroller, um eine weitere Untersuchung zu ermöglichen.

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung:**

**Abhilfemaßnahmen:**

1. Kontrollieren Sie den Quellcomputer.
    - Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
    - Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch kompromittiert sind.
    Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.

**Vorbeugung:**

Überprüfen Sie die folgenden Berechtigungen:

1. Replizieren von Verzeichnisänderungen.
1. Replizieren von allen Verzeichnisänderungen.
1. Weitere Informationen finden Sie unter [Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013 (Erteilen von AD DS-Berechtigungen für die Profilsynchronisierung in SharePoint Server 2013)](/SharePoint/administration/user-profile-service-administration). Nutzen Sie den [AD-ACL-Scanner](/archive/blogs/pfesweplat/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool), oder erstellen Sie ein Windows PowerShell-Skript, um festzustellen, wer in der Domäne über diese Berechtigungen verfügt.

> [!NOTE]
> Warnungen vor verdächtigen Höherstufungen von Domänencontrollern (potenzieller DCShadow-Angriff) werden nur von [!INCLUDE [Product short](includes/product-short.md)]-Sensoren unterstützt.

## <a name="suspected-dcshadow-attack-domain-controller-replication-request-external-id-2029"></a>Vermuteter DCShadow-Angriff (Replikationsanforderung an Domänencontroller) (externe ID 2029)

*Vorheriger Name* : Verdächtige Replikationsanforderung (potenzieller DCShadow-Angriff)

**Beschreibung**

Bei der Active Directory-Replikation werden Änderungen, die auf einem Domänencontroller durchgeführt wurden, mit anderen Domänencontrollern synchronisiert. Wenn Angreifer über die erforderlichen Berechtigungen verfügen, können sie ihren Computerkonten Rechte gewähren, die es ihnen ermöglichen, die Identität eines Domänencontrollers anzunehmen. Angreifer versuchen, eine schädliche Replikationsanforderung zu initiieren, die es ihnen ermöglicht, Active Directory Domain Services-Objekte auf einem echten Domänencontroller zu ändern und so dauerhaft die Kontrolle über die Domäne zu erhalten.
Bei dieser Erkennungsfunktion wird eine Warnung ausgelöst, wenn eine verdächtige Replikationsanforderung für einen echten Domänencontroller generiert wird, der durch [!INCLUDE [Product short](includes/product-short.md)] geschützt ist. Dieses Verhalten weist auf Techniken hin, die bei DCShadow-Angriffen verwendet werden.

**Lernphase**

Nicht zutreffend

**TP, B-TP oder FP?**

Wenn der Quellcomputer ein Domänencontroller ist, wird [!INCLUDE [Product short](includes/product-short.md)] möglicherweise aufgrund fehlender Entscheidungssicherheit an der Identifikation gehindert.

1. Überprüfen Sie, ob der Quellcomputer ein Domänencontroller ist.
    Wenn die Antwort **Ja** lautet, **schließen** Sie die Warnung als **B-TP** -Aktivität.

Die Synchronisierung von Änderungen in Active Directory Domain Services kann etwas Zeit in Anspruch nehmen.

1. Ist der Quellcomputer ein Domänencontroller, der kürzlich höher gestuft wurde? Wenn die Antwort **Ja** lautet, **schließen** Sie die Warnung als **B-TP** -Aktivität.

Server und Anwendungen wie Azure AD Connect oder Geräte zur Leistungsüberwachung im Netzwerk können möglicherweise Daten aus Active Directory Domain Services replizieren.

1. Sollten diese Aktivitäten tatsächlich vom Quellcomputer ausgeführt werden?

    - Wenn die Antwort **Ja** lautet, diese Aktivität aber in Zukunft nicht mehr vom Quellcomputer ausgeführt werden soll, beheben Sie die Konfiguration des Servers oder der Anwendung. **Schließen** Sie die Sicherheitswarnung als **B-TP** -Aktivität.

    - Wenn die Antwort **Ja** lautet und diese Aktivität in der Zukunft weiterhin vom Quellcomputer ausgeführt werden soll, **schließen** Sie die Sicherheitswarnung als **B-TP** -Aktivität, und schließen Sie den Computer aus, um zusätzliche **B-TP** -Warnungen zu vermeiden.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie den [Quellcomputer](investigate-a-computer.md).

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

**Abhilfemaßnahmen:**

1. Kontrollieren Sie den Quellcomputer.
    - Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
    - Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch kompromittiert sind.
    Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Korrigieren Sie die Daten, die auf den Domänencontrollern repliziert wurden.

**Vorbeugung:**

Überprüfen Sie die folgenden Berechtigungen:

1. Replizieren von Verzeichnisänderungen.
1. Replizieren von allen Verzeichnisänderungen.
1. Weitere Informationen finden Sie unter [Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013 (Erteilen von AD DS-Berechtigungen für die Profilsynchronisierung in SharePoint Server 2013)](/SharePoint/administration/user-profile-service-administration). Nutzen Sie den [AD-ACL-Scanner](/archive/blogs/pfesweplat/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool), oder erstellen Sie ein Windows PowerShell-Skript, um festzustellen, wer in der Domäne über diese Berechtigungen verfügt.

> [!NOTE]
> Warnungen vor verdächtigen Replikationsanforderungen (potenzieller DCShadow-Angriff) werden nur von [!INCLUDE [Product short](includes/product-short.md)]-Sensoren unterstützt.

## <a name="suspected-dcsync-attack-replication-of-directory-services-external-id-2006"></a>Vermuteter DCSync-Angriff (Replikation der Verzeichnisdienste) (externe ID 2006)

*Vorheriger Name* : Böswillige Replikation von Verzeichnisdiensten

**Beschreibung**

Bei der Replikation mit Active Directory werden Änderungen eines Domänencontrollers mit allen anderen Domänencontrollern synchronisiert. Mit den erforderlichen Berechtigungen können Angreifer eine Replikationsanforderung initiieren, die ihnen das Abrufen der in Active Directory gespeicherten Daten ermöglicht, einschließlich der Kennworthashes.

In dieser Erkennung wird eine Warnung ausgelöst, wenn eine Replikationsanforderung von einem Computer initiiert wird, der kein Domänencontroller ist.

> [!NOTE]
> Falls Sie über Domänencontroller verfügen, auf denen keine [!INCLUDE [Product short](includes/product-short.md)]-Sensoren installiert sind, werden diese nicht von [!INCLUDE [Product short](includes/product-short.md)] abgedeckt. Wenn Sie einen neuen Domänencontroller auf einem nicht registrierten oder ungeschützten Domänencontroller bereitstellen, wird dieser möglicherweise nicht unmittelbar von [!INCLUDE [Product short](includes/product-short.md)] als Domänencontroller erkannt. Es wird dringend empfohlen, den [!INCLUDE [Product short](includes/product-short.md)]-Sensor für eine vollständige Abdeckung auf jedem Domänencontroller zu installieren.

**Lernphase**

Nicht zutreffend

**TP, B-TP oder FP?**

Wenn der Quellcomputer ein Domänencontroller ist, wird [!INCLUDE [Product short](includes/product-short.md)] möglicherweise aufgrund fehlender Entscheidungssicherheit an der Identifikation gehindert.

1. Überprüfen Sie, ob der Quellcomputer ein Domänencontroller ist.
    Wenn die Antwort **Ja** lautet, **schließen** Sie die Warnung als **B-TP** -Aktivität.

Die Synchronisierung von Änderungen in Active Directory Domain Services kann etwas Zeit in Anspruch nehmen.

1. Ist der Quellcomputer ein Domänencontroller, der kürzlich höher gestuft wurde? Wenn die Antwort **Ja** lautet, **schließen** Sie die Warnung als **B-TP** -Aktivität.

Server und Anwendungen wie Azure AD Connect oder Geräte zur Leistungsüberwachung im Netzwerk können möglicherweise Daten aus Active Directory Domain Services replizieren.

1. Sollten diese Aktivitäten tatsächlich vom Quellcomputer ausgeführt werden?

    - Wenn die Antwort **Ja** lautet, diese Aktivitäten aber in Zukunft nicht mehr vom Quellcomputer ausgeführt werden sollen, beheben Sie die Konfiguration des Servers oder der Anwendung. **Schließen** Sie die Sicherheitswarnung als **B-TP** -Aktivität.

    - Wenn die Antwort **Ja** lautet und diese Aktivität in der Zukunft weiterhin vom Quellcomputer ausgeführt werden soll, **schließen** Sie die Sicherheitswarnung als **B-TP** -Aktivität, und schließen Sie den Computer aus, um zusätzliche B-TP-Warnungen zu vermeiden.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie den [Quellcomputer](investigate-a-computer.md) und den [Benutzer](investigate-a-user.md).

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung:**

**Abhilfemaßnahmen:**

1. Setzen Sie das Kennwort der Quellbenutzer zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Kontrollieren Sie den Quellcomputer.
    - Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
    - Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch kompromittiert sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.

**Vorbeugung:**

Überprüfen Sie die folgenden Berechtigungen:

1. Replizieren von Verzeichnisänderungen.
1. Replizieren von allen Verzeichnisänderungen.
1. Weitere Informationen finden Sie unter [Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013 (Erteilen von AD DS-Berechtigungen für die Profilsynchronisierung in SharePoint Server 2013)](/SharePoint/administration/user-profile-service-administration). Nutzen Sie den [AD-ACL-Scanner](/archive/blogs/pfesweplat/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool), oder erstellen Sie ein Windows PowerShell-Skript, um festzustellen, wer in der Domäne über diese Berechtigungen verfügt.

## <a name="suspected-golden-ticket-usage-encryption-downgrade-external-id-2009"></a>Vermutete Golden Ticket-Verwendung (Herabstufung der Verschlüsselung) (externe ID 2009)

*Vorheriger Name* : Aktivität zur Herabstufung der Verschlüsselung

**Beschreibung**

Die Herabstufung der Verschlüsselung ist eine Methode, die dazu dient, Kerberos zu schwächen, indem die Verschlüsselungsstufe von verschiedenen Protokollfeldern herabgestuft wird, die normalerweise mit der höchsten Verschlüsselungsstufe verschlüsselt werden. Ein abgeschwächtes verschlüsseltes Feld ist ein leichteres Ziel für versuchte Brute-Force-Angriffe offline. Verschiedene Angriffsmethoden nutzen schwache Kerberos-Verschlüsselungsverfahren. Bei dieser Erkennung lernt [!INCLUDE [Product short](includes/product-short.md)] die Kerberos-Verschlüsselungsverfahren, die von Computern und Benutzern verwendet werden, und benachrichtigt Sie, wenn ein schwächeres Verschlüsselungsverfahren verwendet wird, das unüblich für den Quellcomputer und/oder den Benutzer ist und mit bekannten Angriffstechniken übereinstimmt.

Bei einer Golden Ticket-Warnung wurde die Verschlüsselungsmethode des TGT-Felds der TGS_REQ-Nachricht (Dienstanforderung) vom Quellcomputer im Vergleich zum zuvor gelernten Verhalten als herabgestuft erkannt. Dies basiert nicht auf einer Zeitanomalie (wie bei der anderen Golden Ticket-Erkennung). Zusätzlich wurde bei dieser Warnung der vorherigen von [!INCLUDE [Product short](includes/product-short.md)] erkannten Dienstanforderung keine Kerberos-Authentifizierungsanforderung zugeordnet.

**Lernphase**

Für diese Warnung gilt eine Lernphase von 5 Tagen ab dem Start der Domänencontrollerüberwachung.

**TP, B-TP oder FP?**

Einige zulässige Ressourcen unterstützen keine starken Verschlüsselungsverfahren und können diese Warnung auslösen.

1. Greifen Quellbenutzer auf gemeinsam verwendete Ressourcen zu?
   1. Beispielsweise können Sie überprüfen, ob alle Mitarbeiter des Marketingteams auf eine bestimmte Ressource zugreifen und dadurch eine Warnung auslösen.
   1. Überprüfen Sie die Ressourcen, auf die mit diesen Tickets zugegriffen wurde.
      - Verwenden Sie dafür das *msDS-SupportedEncryptionTypes* -Attribut des Ressourcendienstkontos in Azure Active Directory.
   1. Wenn nur auf eine Ressource zugegriffen wird, überprüfen Sie, ob die Benutzer tatsächlich auf diese zugreifen sollten.

      Wenn die Antwort auf eine der vorherigen Fragen **Ja** lautet, handelt es sich vermutlich um eine **B-TP** -Aktivität. Überprüfen Sie, ob von der Ressource ein starkes Verschlüsselungsverfahren unterstützt wird, implementieren Sie es nach Möglichkeit, und **schließen** Sie die Sicherheitswarnung.

Bei Anwendungen wird möglicherweise ein schwächeres Verschlüsselungsverfahren für die Authentifizierung verwendet. Einige dieser Anwendungen wie IIS und SQL Server melden sich im Auftrag von Benutzern an.

1. Lassen sich bei Quellbenutzern Gemeinsamkeiten feststellen?
    - Beispielsweise können Sie überprüfen, ob alle Vertriebsmitarbeiter eine bestimmte App nutzen und dadurch eine Warnung auslösen.
    - Überprüfen Sie, ob Anwendungen dieses Typs auf dem Quellcomputer vorhanden sind.
    - Überprüfen Sie die Rollen der Computer.
    Handelt es sich um Server, die diese Anwendungen nutzen?

     Wenn die Antwort auf eine der vorherigen Fragen **Ja** lautet, handelt es sich vermutlich um eine **B-TP** -Aktivität. Überprüfen Sie, ob von der Ressource ein starkes Verschlüsselungsverfahren unterstützt wird, implementieren Sie es nach Möglichkeit, und **schließen** Sie die Sicherheitswarnung.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie den [Quellcomputer und die Ressourcen](investigate-a-computer.md), auf die zugegriffen wurde.
1. Untersuchen Sie die [Benutzer](investigate-a-computer.md).

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

**Wartung**

1. Setzen Sie das Kennwort des Quellbenutzers zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Kontrollieren Sie den Quellcomputer.
    - Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
    - Suchen Sie nach Benutzern, die zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
    - Wenn Microsoft Defender für Endpunkt installiert ist, nutzen Sie **klist.exe purge** , um alle Tickets der angegebenen Anmeldesitzung endgültig zu löschen und zu verhindern, dass die Tickets in Zukunft verwendet werden.
1. Isolieren Sie die Ressourcen, auf die über das Ticket zugegriffen wurde.
1. Ändern Sie das Kennwort für das Kerberos Ticket Granting Ticket (KRBTGT) zweimal gemäß den Anweisungen unter [KRBTGT Account Password Reset Scripts now available for customers (Skripts zum Zurücksetzen von Kennwörtern des KRBTGT-Kontos stehen Kunden jetzt zur Verfügung)](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) mithilfe des [Reset the KRBTGT account password/keys tool (Tools zum Zurücksetzen des Kennworts/Schlüssels eines KRBTGT-Kontos)](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).
    - Durch zweimaliges Zurücksetzen von KRBTGT werden alle Kerberos-Tickets in dieser Domäne ungültig. Dies bedeutet, dass **alle** Dienste außer Kraft gesetzt werden und erst wieder funktionieren, wenn sie erneuert werden. In einigen Fällen muss der Dienst neu gestartet werden.
    - **Planen Sie daher das zweimalige Zurücksetzen von KRBTGT genau. Das zweimalige Zurücksetzen von KRBTGT wirkt sich auf alle Computer, Server und Benutzer in der Umgebung aus.**

1. Stellen Sie sicher, dass auf allen Domänencontrollern mit Betriebssystemen bis Windows Server 2012 R2 das Sicherheitsupdate [KB3011780](https://www.microsoft.com/download/details.aspx?id=44978) und auf allen Mitgliedsservern und Domänencontrollern bis 2012 R2 das aktuelle Sicherheitsupdate [KB2496930](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privileg) installiert ist. Weitere Informationen finden Sie unter [Silver PAC](/security-updates/SecurityBulletins/2011/ms11-013) und [Gefälschte PAC-Datei](/security-updates/SecurityBulletins/2014/ms14-068).

## <a name="suspected-golden-ticket-usage-forged-authorization-data-external-id-2013"></a>Vermutete Golden Ticket-Verwendung (gefälschte Autorisierungsdaten) (externe ID 2013)

Alter Name: Berechtigungsausweitung mithilfe von gefälschten Autorisierungsdaten

**Beschreibung**

Durch bekannte Sicherheitslücken in älteren Versionen von Windows Server können Angreifer das Privileged Attribute Certificate (PAC) manipulieren. Dabei handelt es sich um ein Feld im Kerberos-Ticket, das die Autorisierungsdaten eines Benutzer enthält (in Active Directory ist dies die Gruppenmitgliedschaft) und Angreifern zusätzliche Berechtigungen erteilt.

**Lernphase**

Nicht zutreffend

**TP, B-TP oder FP?**

Bei Computern mit dem Sicherheitspatch MS14-068 (für Domänencontroller) oder MS11-013 (für Server) schlagen Angriffsversuche fehl und führen zu einem Kerberos-Fehler.

1. Überprüfen Sie, auf welche Ressourcen in der Beweisliste der Sicherheitswarnung zugegriffen wurde, und stellen Sie fest, ob die Versuche erfolgreich waren oder fehlschlugen.
1. Überprüfen Sie, ob wie oben beschrieben auf den Computern, auf die zugegriffen wurde, Sicherheitspatches installiert wurden.
    - Wenn die Computer gepatcht wurden, **schließen** Sie die Sicherheitswarnung als **B-TP** -Aktivität.

Einige Betriebssysteme und Anwendungen sind dafür bekannt, dass sie die Autorisierungsdaten ändern. Linux- und Unix-Dienste verfügen beispielsweise über einen eigenen Autorisierungsmechanismus, der die Warnung auslösen kann.

1. Wird auf dem Quellcomputer ein Betriebssystem oder eine Anwendung ausgeführt, die über einen eigenen Autorisierungsmechanismus verfügt?
    - Wenn auf dem Quellcomputer diese Art von Autorisierungsmechanismus ausgeführt wird, sollten Sie ein Upgrade des Betriebssystems erwägen oder die Anwendungskonfiguration beheben. **Schließen** die Warnung als **B-TP** -Aktivität.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie den [Quellcomputer](investigate-a-computer.md).
1. Wenn ein [Quellbenutzer](investigate-a-user.md) vorhanden ist, untersuchen Sie diesen.
1. Überprüfen Sie, auf welche Ressourcen erfolgreich zugegriffen wurde, und [untersuchen](investigate-a-computer.md) Sie diese.

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

1. Setzen Sie das Kennwort des Quellbenutzers zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Kontrollieren Sie den Quellcomputer.
    - Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
    - Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Ändern Sie das Kennwort für das Kerberos Ticket Granting Ticket (KRBTGT) zweimal gemäß den Anweisungen unter [KRBTGT Account Password Reset Scripts now available for customers (Skripts zum Zurücksetzen von Kennwörtern des KRBTGT-Kontos stehen Kunden jetzt zur Verfügung)](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) mithilfe des [Reset the KRBTGT account password/keys tool (Tools zum Zurücksetzen des Kennworts/Schlüssels eines KRBTGT-Kontos)](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).
    - Durch zweimaliges Zurücksetzen von KRBTGT werden alle Kerberos-Tickets in dieser Domäne ungültig. Dies bedeutet, dass **alle** Dienste außer Kraft gesetzt werden und erst wieder funktionieren, wenn sie erneuert werden. In einigen Fällen muss der Dienst neu gestartet werden. Planen Sie daher das zweimalige Zurücksetzen von KRBTGT genau, da hiervon alle Computer, Server und Benutzer in der Umgebung betroffen sind.
1. Stellen Sie sicher, dass auf allen Domänencontrollern mit Betriebssystemen bis Windows Server 2012 R2 das Sicherheitsupdate [KB3011780](https://www.microsoft.com/download/details.aspx?id=44978) und auf allen Mitgliedsservern und Domänencontrollern bis 2012 R2 das aktuelle Sicherheitsupdate [KB2496930](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privileg) installiert ist. Weitere Informationen finden Sie unter [Silver PAC](/security-updates/SecurityBulletins/2011/ms11-013) und [Gefälschte PAC-Datei](/security-updates/SecurityBulletins/2014/ms14-068).

## <a name="suspected-golden-ticket-usage-nonexistent-account-external-id-2027"></a>Vermutete Golden Ticket-Verwendung (nicht vorhandenes Konto) (externe ID 2027)

Alter Name: Kerberos Golden Ticket

**Beschreibung**

Angreifer mit Domänenadministratorrechten können das KRBTGT-Konto beeinträchtigen. Indem diese das KRBTGT-Konto verwenden, können sie ein Kerberos Ticket Granting Ticket (TGT) erstellen, das die Autorisierung für jede Ressource erteilen und den Ablaufzeitpunkt des Tickets auf einen beliebigen Zeitpunkt festlegen kann. Dieses gefälschte TGT wird als „Golden Ticket“ bezeichnet und ermöglicht es Angreifern, dauerhaft die Kontrolle über das Netzwerk zu erhalten. Bei dieser Erkennung wird durch ein nicht vorhandenes Konto eine Warnung ausgelöst.

**Lernphase**

Nicht zutreffend

**TP, B-TP oder FP?**

Die Synchronisierung von Änderungen in Active Directory Domain Services kann etwas Zeit in Anspruch nehmen.

1. Ist der Benutzer ein bekannter und gültiger Domänenbenutzer?
1. Wurde der Benutzer kürzlich hinzugefügt?
1. Wurde der Benutzer kürzlich aus Active Directory Domain Services gelöscht?

Wenn die Antwort auf alle vorherigen Fragen **Ja** lautet, **schließen** Sie die Warnung als **B-TP** -Aktivität.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie [den Quellcomputer und die Ressourcen, auf die zugegriffen wurde](investigate-a-computer.md).

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

1. Isolieren Sie die Quellcomputer.
    - Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
    - Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
    - Wenn Microsoft Defender für Endpunkt installiert ist, nutzen Sie **klist.exe purge** , um alle Tickets der angegebenen Anmeldesitzung endgültig zu löschen und zu verhindern, dass die Tickets in Zukunft verwendet werden.
1. Isolieren Sie die Ressourcen, auf die über das Ticket zugegriffen wurde.
1. Ändern Sie das Kennwort für das Kerberos Ticket Granting Ticket (KRBTGT) zweimal gemäß den Anweisungen unter [KRBTGT Account Password Reset Scripts now available for customers (Skripts zum Zurücksetzen von Kennwörtern des KRBTGT-Kontos stehen Kunden jetzt zur Verfügung)](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) mithilfe des [Reset the KRBTGT account password/keys tool (Tools zum Zurücksetzen des Kennworts/Schlüssels eines KRBTGT-Kontos)](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).
    - Durch zweimaliges Zurücksetzen von KRBTGT werden alle Kerberos-Tickets in dieser Domäne ungültig. Dies bedeutet, dass **alle** Dienste außer Kraft gesetzt werden und erst wieder funktionieren, wenn sie erneuert werden. In einigen Fällen muss der Dienst neu gestartet werden. Planen Sie daher das zweimalige Zurücksetzen von KRBTGT genau, da hiervon alle Computer, Server und Benutzer in der Umgebung betroffen sind.

## <a name="suspected-golden-ticket-usage-ticket-anomaly-external-id-2032"></a>Vermutete Golden Ticket-Verwendung (Ticketanomalie) (externe ID 2032)

**Beschreibung**

Angreifer mit Domänenadministratorrechten können das KRBTGT-Konto beeinträchtigen. Indem diese das KRBTGT-Konto verwenden, können sie ein Kerberos Ticket Granting Ticket (TGT) erstellen, das die Autorisierung für jede Ressource erteilen und den Ablaufzeitpunkt des Tickets auf einen beliebigen Zeitpunkt festlegen kann. Dieses gefälschte TGT wird als „Golden Ticket“ bezeichnet und ermöglicht es Angreifern, dauerhaft die Kontrolle über das Netzwerk zu erhalten. Gefälschte Golden Tickets dieses Typs haben eindeutige Merkmale, die speziell durch diese Erkennung identifiziert werden.

**Lernphase**

Nicht zutreffend

**TP, B-TP oder FP?**

Verbunddienste generieren möglicherweise Tickets, die diese Warnung auslösen.
1. Werden auf dem Quellcomputer Verbunddienste gehostet, die derartige Tickets erstellen?
    - Wenn ja, schließen Sie die Sicherheitswarnung als **B-TP** -Aktivität.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie [den Quellcomputer und die Ressourcen, auf die zugegriffen wurde](investigate-a-computer.md).
1. Untersuchen Sie den [Quellbenutzer](investigate-a-user.md).

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

1. Isolieren Sie die Quellcomputer.
    - Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
    - Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
    - Wenn Microsoft Defender für Endpunkt installiert ist, nutzen Sie **klist.exe purge** , um alle Tickets der angegebenen Anmeldesitzung endgültig zu löschen und zu verhindern, dass die Tickets in Zukunft verwendet werden.
1. Isolieren Sie die Ressourcen, auf die über das Ticket zugegriffen wurde.
1. Ändern Sie das Kennwort für das Kerberos Ticket Granting Ticket (KRBTGT) zweimal gemäß den Anweisungen unter [KRBTGT Account Password Reset Scripts now available for customers (Skripts zum Zurücksetzen von Kennwörtern des KRBTGT-Kontos stehen Kunden jetzt zur Verfügung)](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) mithilfe des [Reset the KRBTGT account password/keys tool (Tools zum Zurücksetzen des Kennworts/Schlüssels eines KRBTGT-Kontos)](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).
    - Durch zweimaliges Zurücksetzen von KRBTGT werden alle Kerberos-Tickets in dieser Domäne ungültig. Dies bedeutet, dass **alle** Dienste außer Kraft gesetzt werden und erst wieder funktionieren, wenn sie erneuert werden. In einigen Fällen muss der Dienst neu gestartet werden.

    **Planen Sie daher das zweimalige Zurücksetzen von KRBTGT genau. Das Zurücksetzen wirkt sich auf alle Computer, Server und Benutzer in der Umgebung aus.**

## <a name="suspected-golden-ticket-usage-ticket-anomaly-using-rbcd-external-id-2040"></a>Vermutete Golden Ticket-Verwendung (Ticketanomalie mithilfe von RBCD) (externe ID 2040)

**Beschreibung**

Angreifer mit Domänenadministratorrechten können das KRBTGT-Konto beeinträchtigen. Angreifer können das KRBTGT-Konto verwenden, um ein Kerberos Ticket Granting Ticket (TGT) zu erstellen, das Autorisierung für jede beliebige Ressource bietet. Dieses gefälschte TGT wird als „Golden Ticket“ bezeichnet und ermöglicht es Angreifern, dauerhaft die Kontrolle über das Netzwerk zu erhalten. Bei dieser Erkennung wird die Warnung durch ein Golden Ticket ausgelöst, das durch Festlegen der Berechtigungen für die ressourcenbasierte eingeschränkte Delegierung (Resource Based Constrained Delegation, RBCD) mithilfe des KRBTGT-Kontos für das Konto (user\computer) mit SPN erstellt wurde.

**Lernphase**

Nicht zutreffend

**TP, B-TP oder FP?**

1. Verbunddienste generieren möglicherweise Tickets, die diese Warnung auslösen. Werden auf dem Quellcomputer derartige Dienste gehostet?
    - Falls ja, schließen Sie die Sicherheitswarnung als **B-TP** -Aktivität.
1. Zeigen Sie die Profilseite des Quellbenutzers an, und überprüfen Sie, was zum Zeitpunkt der Aktivität geschehen ist.
    1. Soll der Benutzer Zugriff auf diese Ressource haben?
    1. Wird erwartet, dass der Prinzipal auf den Dienst zugreifen kann?
    1. Sollen alle Benutzer, die am Computer angemeldet waren, tatsächlich angemeldet sein?
    1. Sind die Berechtigungen für das Konto geeignet?
1. Sollen die angemeldeten Benutzer Zugriff auf diese Ressourcen haben?
    - Wenn Sie die Microsoft Defender für Endpunkt-Integration aktiviert haben, klicken Sie auf das Symbol, um weitere Untersuchungen anzustellen.

Wenn die Antwort auf eine der vorherigen Fragen „Ja“ lautet, schließen Sie die Sicherheitswarnung als **FP** -Aktivität.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie den [Quellcomputer und die Ressourcen](investigate-a-computer.md), auf die zugegriffen wurde.
1. Untersuchen Sie die [Benutzer](investigate-a-user.md).

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung:**

1. Befolgen Sie die Anweisungen im Rahmen der Sicherheitsbewertung für die [unsichere Kerberos-Delegierung](cas-isp-unconstrained-kerberos.md).
1. Überprüfen Sie die in der Warnung aufgeführten potenziell gefährdeten Benutzer, und entfernen Sie sie aus der Ressource.
1. Ändern Sie das Kennwort für das Kerberos Ticket Granting Ticket (KRBTGT) zweimal gemäß den Anweisungen unter [KRBTGT Account Password Reset Scripts now available for customers (Skripts zum Zurücksetzen von Kennwörtern des KRBTGT-Kontos stehen Kunden jetzt zur Verfügung)](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) mithilfe des [Reset the KRBTGT account password/keys tool (Tools zum Zurücksetzen des Kennworts/Schlüssels eines KRBTGT-Kontos)](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Durch das zweimalige Zurücksetzen von KRBTGT werden alle Kerberos-Tickets in dieser Domäne ungültig. Daher sollten Sie diesen Schritt im Voraus planen. Implementieren Sie ebenfalls die [Pass-the-Hash-Empfehlungen](lateral-movement-alerts.md#suspected-identity-theft-pass-the-hash-external-id-2017), da für das Erstellen eines Golden Tickets Domänenadministratorrechte erforderlich sind.

## <a name="suspected-golden-ticket-usage-time-anomaly-external-id-2022"></a>Vermutete Golden Ticket-Verwendung (Zeitanomalie) (externe ID 2022)

Alter Name: Kerberos Golden Ticket

**Beschreibung**

Angreifer mit Domänenadministratorrechten können das KRBTGT-Konto beeinträchtigen. Indem diese das KRBTGT-Konto verwenden, können sie ein Kerberos Ticket Granting Ticket (TGT) erstellen, das die Autorisierung für jede Ressource erteilen und den Ablaufzeitpunkt des Tickets auf einen beliebigen Zeitpunkt festlegen kann. Dieses gefälschte TGT wird als „Golden Ticket“ bezeichnet und ermöglicht es Angreifern, dauerhaft die Kontrolle über das Netzwerk zu erhalten. Diese Warnung wird ausgelöst, wenn ein Kerberos Ticket Granting Ticket länger als erlaubt verwendet wird. Die zulässige Dauer ist in der Sicherheitsrichtlinie für die maximale Gültigkeitsdauer des Benutzertickets angegeben.

**Lernphase**

Nicht zutreffend

**TP, B-TP oder FP?**

1. Wurden in den letzten Stunden an der Einstellung **Maximale Gültigkeitsdauer für Benutzerticket** innerhalb der Gruppenrichtlinie Änderungen vorgenommen, die sich auf die Warnung auswirken könnten?
1. Ist der eigenständige [!INCLUDE [Product short](includes/product-short.md)]-Sensor, der am Auslösen dieser Warnung beteiligt ist, ein virtueller Computer?
    - Wenn der eigenständige [!INCLUDE [Product short](includes/product-short.md)]-Sensor beteiligt ist, wurde dieser kürzlich aus einem gespeicherten Zustand wiederhergestellt und seine Ausführung fortgesetzt?
1. Gibt es ein Problem mit der Zeitsynchronisierung im Netzwerk, durch das nicht alle Computer synchronisiert werden?
    - Klicken Sie auf die Schaltfläche **Details herunterladen** , um die Excel-Datei für den Sicherheitswarnungsbericht anzuzeigen und zugehörige Netzwerkaktivitäten aufzurufen. Überprüfen Sie, ob sich „StartTime“ und „DomainControllerStartTime“ unterscheiden.

Wenn die Antwort auf die vorherigen Fragen **Ja** lautet, **schließen** Sie die Sicherheitswarnung als **B-TP** -Aktivität.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie [den Quellcomputer und die Ressourcen, auf die zugegriffen wurde](investigate-a-computer.md).
1. Untersuchen Sie den [kompromittierten Benutzer](investigate-a-user.md).

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

1. Kontrollieren Sie den Quellcomputer.
    - Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
    - Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
    - Wenn Microsoft Defender für Endpunkt installiert ist, nutzen Sie **klist.exe purge** , um alle Tickets der angegebenen Anmeldesitzung endgültig zu löschen und zu verhindern, dass die Tickets in Zukunft verwendet werden.
1. Isolieren Sie die Ressourcen, auf die über das Ticket zugegriffen wurde.
1. Ändern Sie das Kennwort für das Kerberos Ticket Granting Ticket (KRBTGT) zweimal gemäß den Anweisungen unter [KRBTGT Account Password Reset Scripts now available for customers (Skripts zum Zurücksetzen von Kennwörtern des KRBTGT-Kontos stehen Kunden jetzt zur Verfügung)](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) mithilfe des [Reset the KRBTGT account password/keys tool (Tools zum Zurücksetzen des Kennworts/Schlüssels eines KRBTGT-Kontos)](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).
    - Durch zweimaliges Zurücksetzen von KRBTGT werden alle Kerberos-Tickets in dieser Domäne ungültig. Dies bedeutet, dass **alle** Dienste außer Kraft gesetzt werden und erst wieder funktionieren, wenn sie erneuert werden. In einigen Fällen muss der Dienst neu gestartet werden.

    **Planen Sie daher das zweimalige Zurücksetzen von KRBTGT genau. Das Zurücksetzen wirkt sich auf alle Computer, Server und Benutzer in der Umgebung aus.**

## <a name="suspected-skeleton-key-attack-encryption-downgrade-external-id-2010"></a>Vermuteter Skeleton Key-Angriff (Herabstufung der Verschlüsselung) (externe ID 2010)

*Vorheriger Name* : Aktivität zur Herabstufung der Verschlüsselung

**Beschreibung**

Die Herabstufung der Verschlüsselung ist eine Methode, die dazu dient, Kerberos zu schwächen, indem die Verschlüsselungsstufe von verschiedenen Protokollfeldern herabgestuft wird, die normalerweise mit der höchsten Verschlüsselungsstufe verschlüsselt werden. Ein abgeschwächtes verschlüsseltes Feld ist ein leichteres Ziel für versuchte Brute-Force-Angriffe offline. Verschiedene Angriffsmethoden nutzen schwache Kerberos-Verschlüsselungsverfahren. Bei dieser Erkennung lernt [!INCLUDE [Product short](includes/product-short.md)] die Kerberos-Verschlüsselungstypen, die von Computern und Benutzern verwendet werden. Die Warnung wird ausgegeben, wenn ein schwächeres Verschlüsselungsverfahren verwendet wird, das unüblich für den Quellcomputer und/oder den Benutzer ist und mit bekannten Angriffstechniken übereinstimmt.

Skeleton Key ist eine Schadsoftware, die auf einem Domänencontroller ausgeführt wird und mit der eine Authentifizierung bei der Domäne mit jedem Konto ohne das passende Kennwort möglich ist. Diese Schadsoftware verwendet häufig schwächere Verschlüsselungsalgorithmen, um einen Hashwert für das Kennwort des Benutzers auf dem Domänencontroller zu erstellen. Wenn diese Warnung auftritt, wurde das gelernte Verhalten der vorherigen KRB_ERR-Nachrichtenverschlüsselung zwischen dem Domänencontroller und dem Konto, das das Ticket anfordert, herabgestuft.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie den [Domänencontroller](investigate-a-computer.md).
1. Überprüfen Sie mithilfe des [vom [!INCLUDE [Product short](includes/product-short.md)]-Team entwickelten Scanners](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73), ob Ihre Domänencontroller von einem Skeleton Key-Angriff betroffen sind.
1. Untersuchen Sie die beteiligten [Benutzer](investigate-a-user.md) und [Computer](investigate-a-computer.md).

**Empfohlene Abhilfemaßnahmen Schritte zur Vorbeugung**

1. Setzen Sie die Kennwörter der kompromittierten Benutzer zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Isolieren Sie den Domänencontroller.
    - Entfernen Sie die Schadsoftware. Weitere Informationen finden Sie in der [Skeleton Key Malware Analysis](https://www.virusbulletin.com/virusbulletin/2016/01/paper-digital-bian-lian-face-changing-skeleton-key-malware) (Analyse der Skeleton Key-Schadsoftware).
    - Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der verdächtigen Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.

## <a name="suspicious-additions-to-sensitive-groups-external-id-2024"></a>Verdächtige Hinzufügungen sensibler Gruppen (externe ID 2024)

**Beschreibung**

Angreifer fügen Benutzer zu sehr privilegierten Gruppen hinzu. Dadurch erhalten Angreifer Zugriff auf weitere Ressourcen und dauerhafte Kontrolle. Diese Erkennung basiert auf dem Erfassen der Aktivitäten von Benutzern, die Gruppen ändern, und den Warnungen, die angezeigt werden, wenn einer sensiblen Gruppe unerwartet ein Benutzer hinzugefügt wird. [!INCLUDE [Product short](includes/product-short.md)] führt kontinuierlich Profilerstellungen durch.

Eine Definition von sensiblen Gruppen in [!INCLUDE [Product short](includes/product-short.md)] finden Sie unter [Arbeiten mit sensiblen Konten](sensitive-accounts.md).

Die Erkennung basiert auf Ereignissen, die auf Domänencontrollern überwacht werden. Stellen Sie sicher, dass Ihre Domänencontroller die [erforderlichen Ereignisse überwachen](configure-windows-event-collection.md).

**Lernphase**

Vier Wochen pro Domänencontroller, beginnend mit dem ersten Ereignis.

**TP, B-TP oder FP?**

Zulässige Änderungen an Gruppen, die nur selten auftreten und vom System noch nicht als unbedenklich eingestuft wurden, können einen Alarm auslösen. Diese Warnungen werden als **B-TP** -Aktivität klassifiziert.

1. Ist das Ändern der Gruppe zulässig?
    - Wenn das Ändern der Gruppe zulässig ist, **schließen** Sie die Sicherheitswarnung als **B-TP** -Aktivität.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie die Benutzer, die Gruppen hinzugefügt wurden.
    - Konzentrieren Sie sich auf ihre Aktivitäten, nachdem sie den sensiblen Gruppen hinzugefügt wurden.
1. Untersuchen Sie den Quellbenutzer.
    - Laden Sie den Bericht **Sensitive Group Modification** (Änderungen an sensiblen Gruppen) herunter, um festzustellen, welche Änderungen von wem im gleichen Zeitraum vorgenommen wurden.
1. Untersuchen Sie die Computer, bei denen Benutzer ungefähr zum Zeitpunkt der Aktivität angemeldet waren.

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

**Abhilfemaßnahmen:**

1. Setzen Sie das Kennwort des Quellbenutzers zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
    - Suchen Sie nach dem Computer, auf dem der Benutzer aktiv war.
    - Überprüfen Sie, bei welchen Computern der Benutzer ungefähr zum Zeitpunkt der Aktivität angemeldet war. Überprüfen Sie, ob diese Computer kompromittiert sind.
    - Wenn die Benutzer kompromittiert wurden, setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.

**Vorbeugung:**

1. Schränken Sie die Anzahl der Benutzer, die zu Änderungen an sensiblen Gruppen autorisiert sind, auf ein Minimum ein, um zukünftige Angriffe zu verhindern.
1. Richten Sie gegebenenfalls Privileged Access Management für Active Directory Domain Services ein.

## <a name="suspicious-service-creation-external-id-2026"></a>Verdächtige Diensterstellung (externe ID 2026)

*Alter Name:* Verdächtige Diensterstellung

**Beschreibung**

Ein verdächtiger Dienst wurde von Ihrer Organisation auf einem Domänencontroller erstellt. Diese Warnung basiert auf Ereignis 7045, um die verdächtige Aktivität zu identifizieren.

**Lernphase**

Nicht zutreffend

**TP, B-TP oder FP?**

Einige zulässige administrative Aufgaben auf Domänencontrollern können von Arbeitsstationen für Administratoren, IT-Teammitgliedern und Dienstkonten durchgeführt werden.

1. Sollen diese Dienste tatsächlich auf dem Domänencontroller vom Quellbenutzer oder -computer ausgeführt werden?
    - Wenn das aktuell der Fall ist, jedoch in Zukunft nicht mehr so sein sollte, **schließen** Sie die Warnung als **B-TP** -Aktivität.
    - Wenn das aktuell der Fall ist und auch in Zukunft so bleiben sollte, **schließen** Sie die Sicherheitswarnung als **B-TP** -Aktivität, und schließen Sie diesen Computer aus.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie den [Quellbenutzer](investigate-a-user.md).
1. Untersuchen Sie die [Zielcomputer](investigate-a-computer.md), auf denen die Dienste erstellt wurden.

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

**Wartung**

1. Setzen Sie das Kennwort des Quellbenutzers zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Isolieren Sie die Domänencontroller.
    - Korrigieren Sie den verdächtigen Dienst.
    - Suchen Sie nach Benutzern, die zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Suchen Sie nach dem Computer, auf dem der Benutzer aktiv war.
    - Überprüfen Sie die Computer, bei denen der Benutzer ungefähr zum Zeitpunkt der Aktivität angemeldet war. Überprüfen Sie außerdem, ob diese Computer ebenfalls kompromittiert wurden.

**Vorbeugung:**

1. Schränken Sie den Remotezugriff auf Domänencontroller von Computern ein, die nicht den Tier 0 aufweisen.
1. Implementieren Sie [Zugriffseinschränkungen für Konten mit weitreichenden Rechten](/windows-server/identity/securing-privileged-access/securing-privileged-access), damit nur abgesicherte Computer eine Verbindung mit Domänencontrollern für Administratoren herstellen können.
1. Implementieren Sie weniger restriktive Zugriffseinschränkungen auf Domänencomputern, um nur bestimmten Benutzern die Erstellung von Diensten zu erlauben.

> [!div class="nextstepaction"]
> [Tutorial: Exfiltrationswarnungen](exfiltration-alerts.md)

## <a name="see-also"></a>Weitere Informationen

- [Untersuchen eines Computers](investigate-a-computer.md)
- [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md)
- [Arbeiten mit Lateral Movement-Pfaden](use-case-lateral-movement-path.md)
- [Warnungen zu Reconnaissance](reconnaissance-alerts.md)
- [Warnungen zu kompromittierten Anmeldeinformationen](compromised-credentials-alerts.md)
- [Lateral Movement-Warnungen](lateral-movement-alerts.md)
- [Warnungen zu Exfiltration](exfiltration-alerts.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
