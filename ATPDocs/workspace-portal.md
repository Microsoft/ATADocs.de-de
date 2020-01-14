---
title: Grundlegende Informationen zum Azure Advanced Threat Protection-Portal | Microsoft-Dokumentation
description: Informationen zum Anmelden im Azure ATP-Portal und zu dessen Komponenten
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 11/05/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 4ba46d60-3a74-480e-8f0f-9a082d62f343
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 5829d8564a65bbeba7f755e1e5cd1ad90c3da5ae
ms.sourcegitcommit: 9673eb49729a06d3a25d52c0f43c76ac61b9cf89
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/12/2020
ms.locfileid: "75905811"
---
# <a name="working-with-the-azure-atp-portal"></a>Arbeiten mit dem Azure ATP-Portal

> [!NOTE]
> Auf alle auf dieser Seite erläuterten Azure ATP-Features kann auch über das neue [Cloud App Security-Portal](https://portal.cloudappsecurity.com) zugegriffen werden.

Verwenden Sie das Azure ATP-Portal, um die von ATP erkannten verdächtigen Aktivitäten zu überwachen und darauf zu reagieren.

Durch Drücken der `?`-Taste werden die Tastenkombinationen für den Zugriff auf das Azure ATP-Portal bereitgestellt. 

Das Azure ATP-Portal stellt einen schnellen Überblick über alle verdächtigen Aktivitäten in chronologischer Reihenfolge zur Verfügung. Sie ermöglicht es Ihnen, sich die Details einer Aktivität anzusehen und Aktionen entsprechend der jeweiligen Aktivität auszuführen. Das Azure ATP-Portal zeigt außerdem Warnungen und Benachrichtigungen an, um Probleme mit Azure ATP oder neue Aktivitäten hervorzuheben, die als verdächtig eingestuft werden.

In diesem Artikel wird beschrieben, wie Sie mit den wichtigsten Elementen des Azure ATP-Portals arbeiten können.


## <a name="enabling-access-to-the-azure-atp-portal"></a>Aktivieren des Zugriffs auf das Azure ATP-Portal
Für eine erfolgreiche Anmeldung im Azure ATP-Portal müssen Sie sich mit einem Benutzernamen anmelden, der einer Azure Active Directory-Sicherheitsgruppe zugewiesen wurde, die über Zugriff auf das Azure ATP-Portal verfügt. Weitere Informationen zur rollenbasierten Zugriffssteuerung in Azure ATP finden Sie unter [Working with Azure ATP role groups (Arbeiten mit Azure ATP-Rollengruppen)](atp-role-groups.md).

## <a name="logging-into-the-azure-atp-portal"></a>Anmelden im Azure ATP-Portal

1. Sie können sich beim Azure ATP-Portal anmelden, indem Sie sich entweder beim Portal unter [https://portal.atp.azure.com](https://portal.atp.azure.com) anmelden und die relevante Instanz auswählen, oder indem Sie die folgende Instanz-URL öffnen:[https://*instanzname*.atp.azure.com](https://*instancename*.atp.azure.com).zure.com.


2. Azure ATP unterstützt die in die Windows-Authentifizierung integrierte einmalige Anmeldung: Wenn Sie sich schon auf Ihrem Computer angemeldet haben, verwendet Azure ATP dieses Token, um Sie im Azure ATP-Portal anzumelden. Sie können sich auch mit einer Smartcard anmelden. Ihre Berechtigungen in Azure ATP entsprechen Ihrer [Administratorrolle](atp-role-groups.md).

   > [!NOTE]
   > Stellen Sie sicher, dass Sie sich auf dem Computer anmelden, von dem aus Sie auf das Azure ATP-Portal zugreifen möchten. Verwenden Sie hierzu Ihren Azure ATP-Administratorbenutzernamen und das entsprechende Kennwort. Alternativ führen Sie Ihren Browser mit einem anderen Benutzer aus oder melden sich von Windows ab und melden sich danach mit Ihrem Azure ATP-Administratorbenutzerkonto an. Im Gegensatz zum Azure ATP-Portal ermöglicht das neue [Cloud App Security-Portal](https://portal.cloudappsecurity.com) die Anmeldung mehrerer Benutzer und erfordert keine zusätzlichen Lizenzen für die Verwendung mit Azure ATP.  


### <a name="attack-time-line"></a>Angriffszeitachse

Die Angriffszeitachse ist die Standard-Landing Page, auf die Sie gelangen, wenn Sie sich beim Azure ATP-Portal anmelden. Standardmäßig werden alle offenen verdächtigen Aktivitäten auf der Angriffszeitachse angezeigt. Sie können die Angriffszeitachse filtern, um alle bzw. offene, verworfene oder unterdrückte verdächtige Aktivitäten anzuzeigen. Außerdem wird der Schweregrad angezeigt, der den einzelnen Aktivitäten zugewiesen wurde.

![Abbildung der Angriffszeitachse in Azure ATP](media/atp-sa-timeline.png)

Weitere Informationen finden Sie unter [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md).

### <a name="whats-new"></a>Neuerungen

Nach der Veröffentlichung einer neuen Version von Azure ATP wird das Fenster **Neuigkeiten** in der oberen rechten Ecke angezeigt, und Sie erhalten Informationen darüber, was in der neusten Version hinzugefügt wurde. Außerdem erhalten Sie einen Link zum Download der Version.

### <a name="filtering-panel"></a>Filterbereich

Sie können basierend auf Status und Schweregrad filtern, welche verdächtigen Aktivitäten auf der Angriffszeitachse oder auf der Registerkarte für verdächtige Aktivitäten des Entitätsprofils angezeigt werden.

### Suchleiste <a name="search-bar"></a>

Im obersten Menü finden Sie eine Suchleiste. Sie können nach einem bestimmten Benutzer, Computer oder nach Gruppen in Azure ATP suchen. Beginnen Sie als Versuch einfach mit der Eingabe. Unten in der Suchleiste wird die Anzahl der gefundenen Suchergebnisse angezeigt. 

![Bild zur Suche im Azure ATP-Portal](media/atp-workspace-portal-search.png)

Wenn Sie auf die Nummer klicken, können Sie auf die Seite mit den Suchergebnissen zugreifen, auf der Sie die Ergebnisse nach Entitätstyp für weitere Untersuchungen filtern können.

!["search results" (Ergebnisse durchsuchen)](media/search-results.png)

### <a name="health-center"></a>Integritätscenter

Das Integritätscenter warnt Sie, wenn in Ihrem Azure ATP-Instanz etwas nicht ordnungsgemäß funktioniert.

![Abbildung zum Azure ATP-Integritätscenter](media/atp-health-issue.png)

Jedes Mal, wenn auf Ihrem System ein Problem auftritt (z.B. ein Verbindungsfehler oder ein nicht verbundener eigenständiger Azure ATP-Sensor), können Sie dies an dem Symbol für das Integritätscenter erkennen, auf dem ein roter Punkt angezeigt wird. 

![Abbildung des roten Punkts auf dem Symbol für das Azure ATP-Integritätscenter](media/atp-health-bar.png)

### <a name="sensitive-groups"></a>Sensible Gruppen

Informationen zu sensiblen Gruppen in Azure ATP finden Sie unter [Arbeiten mit sensiblen Gruppen](sensitive-accounts.md).

### <a name="mini-profile"></a>Miniprofil

Wenn Sie an einer Stelle im Azure ATP-Portal, an der eine einzelne Entität dargestellt wird (z.B. ein Benutzer oder ein Computer), mit der Maus auf eine Entität zeigen, wird automatisch ein Miniprofil geöffnet. Das Miniprofil enthält die folgenden Informationen (sofern verfügbar und relevant):

![Abbildung des Azure ATP-Miniprofils](media/atp-mini-profile.png)

- Name
- Titel
- Department
- AD-Tags
- E-Mail
- Office
- Telefonnummer
- Domain
- SAM-Name
- Erstellungsdatum: Datum, an dem die Entität in Active Directory erstellt wurde. Wenn sie erstellt wurde, bevor Azure ATP mit der Überwachung begonnen hat, wird diese nicht angezeigt.
- Erste Aktivität: Das erste Mal, als Azure ATP eine Aktivität von dieser Entität wahrgenommen hat.
- Letzte Aktivität: Das letzte Mal, als Azure ATP eine Aktivität von dieser Entität wahrgenommen hat.
- SA-Badge: Wird angezeigt, wenn dieser Entität verdächtige Aktivitäten zugeordnet werden.
- Windows Defender ATP-Badge: Wird angezeigt, wenn dieser Entität verdächtige Aktivitäten in Windows Defender ATP zugeordnet werden.
- Badge für Lateral Movement-Pfade: Wird angezeigt, wenn innerhalb der letzten beiden Tage Lateral Movement-Pfade für diese Entität ermittelt wurden.


## <a name="see-also"></a>Weitere Informationen

- [Erstellen von Azure ATP-Instanzen](install-atp-step1.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
