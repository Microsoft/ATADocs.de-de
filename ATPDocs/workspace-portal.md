---
title: Grundlegende Informationen zum Azure Advanced Threat Protection-Arbeitsbereichsportal | Microsoft-Dokumentation
description: Informationen zum Anmelden im Azure ATP-Arbeitsbereichsportal und zu dessen Komponenten
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/22/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 4ba46d60-3a74-480e-8f0f-9a082d62f343
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 40e139cc5e7dc6396914b0314d2d698a4782af02
ms.sourcegitcommit: 324dc941282f2948366afa5a919bda0b029bd59d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/22/2018
ms.locfileid: "34444704"
---
*Gilt für: Azure Advanced Threat Protection*



# <a name="working-with-the-azure-atp-workspace-portal"></a>Arbeiten mit dem Azure ATP-Arbeitsbereichsportal

Verwenden Sie das Azure ATP-Arbeitsbereichsportal, um die von ATP erkannten verdächtigen Aktivitäten zu überwachen und darauf zu reagieren.

Durch Drücken der `?`-Taste werden die Tastenkombinationen für den Zugriff auf das Azure ATP-Arbeitsbereichsportal bereitgestellt. 

Das Azure ATP-Arbeitsbereichsportal stellt Ihnen einen schnellen Überblick über alle verdächtigen Aktivitäten in chronologischer Reihenfolge zur Verfügung. Sie ermöglicht es Ihnen, sich die Details einer Aktivität anzusehen und Aktionen entsprechend der jeweiligen Aktivität auszuführen. Das Arbeitsbereichsportal zeigt außerdem Warnungen und Benachrichtigungen an, um Probleme mit Azure ATP oder neue Aktivitäten hervorzuheben, die als verdächtig eingestuft werden.

In diesem Artikel wird beschrieben, wie Sie mit den wichtigsten Elementen des Azure ATP-Arbeitsbereichsportals arbeiten können.


## <a name="enabling-access-to-the-azure-atp-workspace-portal"></a>Aktivieren des Zugriffs auf das Azure ATP-Arbeitsbereichsportal
Für eine erfolgreiche Anmeldung im Azure ATP-Arbeitsbereichsportal müssen Sie sich mit einem Benutzernamen anmelden, der der richtigen Azure Active Directory-Sicherheitsgruppe zugewiesen wurde. Erst dann können Sie auf das Azure ATP-Arbeitsbereichsportal zugreifen. Weitere Informationen zur rollenbasierten Zugriffssteuerung in Azure ATP finden Sie unter [Working with Azure ATP role groups (Arbeiten mit Azure ATP-Rollengruppen)](atp-role-groups.md).

## <a name="logging-into-the-azure-atp-workspace-portal"></a>Anmelden im Azure ATP-Arbeitsbereichsportal

1. Sie haben zwei Möglichkeiten, um sich im Arbeitsbereichsportal anzumelden: Sie können sich entweder über [https://portal.atp.azure.com](https://portal.atp.azure.com) im Portal für die Verwaltung des Arbeitsbereichs anmelden und dann auf den relevanten Arbeitsbereich klicken, oder Sie durchsuchen die Arbeitsbereich-URL [https://*workspacename*.atp.azure.com](https://*workspacename*.atp.azure.com).


2.  Azure ATP unterstützt die in die Windows-Authentifizierung integrierte einmalige Anmeldung: Wenn Sie sich schon auf Ihrem Computer angemeldet haben, verwendet Azure ATP dieses Token, um Sie im Azure ATP-Arbeitsbereichsportal anzumelden. Sie können sich auch mit einer Smartcard anmelden. Ihre Berechtigungen in Azure ATP entsprechen Ihrer [Administratorrolle](atp-role-groups.md).

 > [!NOTE]
 > Stellen Sie sicher, dass Sie sich auf dem Computer anmelden, von dem aus Sie auf das Azure ATP-Arbeitsbereichsportal zugreifen möchten. Verwenden Sie hierzu Ihren Azure ATP-Administratorbenutzernamen und das entsprechende Kennwort. Alternativ können Sie Ihren Browser als ein anderer Benutzer ausführen oder sich von Windows abmelden und danach mit Ihrem Azure ATP-Administratorbenutzerkonto anmelden. 


### <a name="attack-time-line"></a>Angriffszeitachse

Dies ist die Standardzielseite, auf die Sie gelangen, wenn Sie sich im Azure ATP-Arbeitsbereich anmelden. Standardmäßig werden alle offenen verdächtigen Aktivitäten auf der Angriffszeitachse angezeigt. Sie können die Angriffszeitachse filtern, um alle bzw. offene, verworfene oder unterdrückte verdächtige Aktivitäten anzuzeigen. Außerdem wird der Schweregrad angezeigt, der den einzelnen Aktivitäten zugewiesen wurde.

![Abbildung der Angriffszeitachse in Azure ATP](media/atp-sa-timeline.png)

Weitere Informationen finden Sie unter [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md).

### <a name="whats-new"></a>Neuheiten

Nach der Veröffentlichung einer neuen Version von Azure ATP wird das Fenster **Neuigkeiten** in der oberen rechten Ecke angezeigt, und Sie erhalten Informationen darüber, was in der neusten Version hinzugefügt wurde. Außerdem erhalten Sie einen Link zum Download der Version.

### <a name="filtering-panel"></a>Filterbereich

Sie können basierend auf Status und Schweregrad filtern, welche verdächtigen Aktivitäten auf der Angriffszeitachse oder auf der Registerkarte für verdächtige Aktivitäten des Entitätsprofils angezeigt werden.

### Suchleiste <a name="search-bar"></a>

Im obersten Menü finden Sie eine Suchleiste. Sie können nach einem bestimmten Benutzer, Computer oder nach Gruppen in Azure ATP suchen. Beginnen Sie als Versuch einfach mit der Eingabe. Unten in der Suchleiste wird die Anzahl der gefundenen Suchergebnisse angezeigt. 

![Abbildung zur Suche im Azure ATP-Arbeitsbereichsportal](media/atp-workspace-portal-search.png)

Wenn Sie auf die Nummer klicken, können Sie auf die Seite mit den Suchergebnissen zugreifen, auf der Sie die Ergebnisse nach Entitätstyp für weitere Untersuchungen filtern können.

!["search results" (Ergebnisse durchsuchen)](media/search-results.png)

### <a name="health-center"></a>Integritätscenter

Das Integritätscenter warnt Sie, wenn in Ihrem Azure ATP-Arbeitsbereich etwas nicht ordnungsgemäß funktioniert.

![Abbildung zum Azure ATP-Integritätscenter](media/atp-health-issue.png)

Jedes Mal, wenn auf Ihrem System ein Problem auftritt (z.B. ein Verbindungsfehler oder ein nicht verbundener eigenständiger Azure ATP-Sensor), können Sie dies an dem Symbol für das Integritätscenter erkennen, auf dem ein roter Punkt angezeigt wird. 

![Abbildung des roten Punkts auf dem Symbol für das Azure ATP-Integritätscenter](media/atp-health-bar.png)

### <a name="sensitive-groups"></a>Sensible Gruppen

Informationen zu sensiblen Gruppen in ATP finden Sie unter [Working with sensitive groups (Arbeiten mit sensiblen Gruppen)](sensitive-accounts.md).

### <a name="mini-profile"></a>Miniprofil

Wenn Sie an einer Stelle im Arbeitsbereich, an der eine einzelne Entität dargestellt wird (z.B. ein Benutzer oder ein Computer), mit der Maus auf eine Entität zeigen, wird automatisch ein Miniprofil geöffnet. Das Miniprofil enthält die folgenden Informationen (sofern verfügbar und relevant):

![Abbildung des Azure ATP-Miniprofils](media/atp-mini-profile.png)

- Name
- Titel
- Abteilung
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

- [Creating Azure ATP workspaces (Erstellen von Azure ATP-Arbeitsbereichen)](install-atp-step1.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)