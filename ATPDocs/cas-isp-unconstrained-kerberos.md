---
title: Bewertung von Microsoft Defender für Identitätsschutz in der Kerberos-Identität
description: Dieser Artikel bietet eine Übersicht über die nicht eingeschränkten Sicherheitsstatus Bewertungsberichte von Microsoft Defender for Identity.
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: 796dd3539f26ace93bd36a60f88c292d65de24b0
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/03/2020
ms.locfileid: "96543585"
---
# <a name="security-assessment-unsecure-kerberos-delegation"></a>Sicherheitsbewertung: Unsichere Kerberos-Delegierung

## <a name="what-is-kerberos-delegation"></a>Was ist die Kerberos-Delegierung?

Die Kerberos-Delegierung ist eine Delegierungseinstellung, die es Anwendungen ermöglicht, die Anmeldeinformationen von Endbenutzern für den Zugriff auf Ressourcen im Namen des ursprünglichen Benutzers anzufordern.

## <a name="what-risk-does-unsecure-kerberos-delegation-pose-to-an-organization"></a>Welches Risiko birgt eine unsichere Kerberos-Delegierung für eine Organisation?

Eine unsichere Kerberos-Delegierung ermöglicht es einer Entität, bei einem beliebigen anderen Dienst Ihre Identität anzunehmen. Nehmen Sie beispielweise an, Sie verfügen über eine IIS-Website, und das Anwendungspoolkonto ist mit uneingeschränkter Delegierung konfiguriert. Für die IIS-Website ist auch die Windows-Authentifizierung aktiviert, die eine native Kerberos-Authentifizierung ermöglicht, und die Website verwendet einen SQL-Back-End-Server für Geschäftsdaten. Mit Ihrem Domänenadministratorkonto wechseln Sie zur Website und authentifizieren sich dort. Die Website, die die uneingeschränkte Delegierung verwendet, kann ein Dienst Ticket von einem Domänen Controller an den SQL-Dienst übernehmen und dies in Ihrem Namen tun.

Das Hauptproblem bei der unsicheren Kerberos-Delegierung besteht darin, dass Sie darauf vertrauen müssen, dass die Anwendung immer die richtigen Aktionen ausführt. Angreifer könnten die Anwendung aber dazu zwingen, ungewünschte Aktionen auszuführen. Wenn Sie als **Domänen Administrator** angemeldet sind, kann der Standort ein Ticket für alle anderen gewünschten Dienste erstellen, die Sie als **Domänen Administrator** fungieren. Beispielsweise könnte die Site einen Domänen Controller auswählen und Änderungen an der Gruppe " **Unternehmens Administratoren** " vornehmen. Die Website könnte auch den Hash eines KRBTGT-Kontos abrufen oder eine interessante Datei aus Ihrer Personalabteilung herunterladen. Das Risiko ist also bekannt, und die Möglichkeiten, die die unsichere Delegierung eröffnet, sind schier unendlich.

Nachfolgend finden Sie eine Beschreibung des Risikos, das von verschiedenen Delegierungstypen verursacht wird:

- **Uneingeschränkte Delegierung:** Jeder Dienst kann missbraucht werden, wenn einer der Delegierungseinträge sensibel ist.
- **Eingeschränkte Delegierung:** Eingeschränkte Entitäten können missbraucht werden, wenn einer ihrer Delegierungsenträge sensibel ist.
- **Ressourcenbasierte eingeschränkte Delegierung (RBCD):** Ressourcenbasierte eingeschränkte Entitäten können missbraucht werden, wenn die Entität selbst sensibel ist.

## <a name="how-do-i-use-this-security-assessment"></a>Wie wird diese Sicherheitsbewertung verwendet?

1. Verwenden Sie die Berichtstabelle, um zu ermitteln, welche Ihrer Entitäten, bei denen es sich nicht um Domänencontroller handelt, für die **unsichere Kerberos-Delegierung** konfiguriert sind.

    ![Sicherheitsbewertung: unsichere Kerberos-Delegierung](media/cas-isp-kerberos-delegation-2.png)
1. Führen Sie für Benutzer, die einem Risiko ausgesetzt sind, entsprechende Maßnahmen durch: Entfernen Sie beispielsweise das Attribut für die uneingeschränkte Delegierung, oder richten Sie eine sicherere eingeschränkte Delegierung ein.

> [!NOTE]
> Diese Bewertung wird alle 24 Stunden aktualisiert.

## <a name="remediation"></a>Wartung

Verwenden Sie die für Ihren Delegierungstyp geeignete Wiederherstellung.

### <a name="unconstrained-delegation"></a>Uneingeschränkte Delegierung

Deaktivieren Sie entweder die Delegierung, oder verwenden Sie einen der folgenden KCD-Typen (eingeschränkte Kerberos-Delegierung):

- **Eingeschränkte Delegierung:** Schränkt ein, von welchen Diensten das Konto die Identität annehmen kann

    1. Klicken Sie auf **Computer nur bei Delegierungen angegebener Dienste vertrauen**.

        ![Uneingeschränkte Wartung der Kerberos-Delegierung](media/cas-isp-unconstrained-kerberos-1.png)

    2. Geben Sie die **Dienste an, für die dieses Konto delegierte Anmeldeinformationen verwenden kann**.

- **Ressourcenbasierte eingeschränkte Delegierung:** Schränkt ein, welche Entitäten die Identität des Kontos annehmen können  
Die ressourcenbasierte KCD wird mithilfe von PowerShell konfiguriert. Sie verwenden das Cmdlet [Set-ADComputer](/powershell/module/addsadministration/set-adcomputer?view=win10-ps&preserve-view=true) oder [Set-ADUser](/powershell/module/addsadministration/set-aduser?view=win10-ps&preserve-view=true), je nachdem, ob es sich beim Konto für den Identitätswechsel um ein Computerkonto oder ein Benutzerkonto/Dienstkonto handelt.

### <a name="constrained-delegation"></a>Eingeschränkte Delegierung

Überprüfen Sie die in den Empfehlungen aufgeführten sensiblen Benutzer, und entfernen Sie sie aus den Diensten, für die das betroffene Konto delegierte Anmeldeinformationen vorweisen kann.

![Eingeschränkte Wiederherstellung der Kerberos-Delegierung](media/cas-isp-unconstrained-kerberos-2.png)

### <a name="resource-based-constrained-delegation-rbcd"></a>Ressourcenbasierte eingeschränkte Delegierung (RBCD)

Überprüfen Sie die in den Empfehlungen aufgeführten sensiblen Benutzer, und entfernen Sie sie aus der Ressource. Weitere Informationen zum Konfigurieren von RBCD finden Sie unter [Konfigurieren der eingeschränkten Kerberos-Delegierung (KCD) in Azure Active Directory Domain Services](/azure/active-directory-domain-services/deploy-kcd).

## <a name="next-steps"></a>Nächste Schritte

- [[!INCLUDE [Product short](includes/product-short.md)] Aktivitäten Filtern in Cloud App Security](activities-filtering-mcas.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
