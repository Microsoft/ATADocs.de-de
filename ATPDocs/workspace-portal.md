---
title: Grundlegendes zum Microsoft Defender for Identity-Portal
description: Hier erfahren Sie, wie Sie sich beim Microsoft Defender for Identity-Portal anmelden, und erhalten Informationen zu den Komponenten des Portals.
ms.date: 10/27/2020
ms.topic: conceptual
ms.openlocfilehash: db140bafe14f0667348c96ecf318669abbdae5f3
ms.sourcegitcommit: f92dca4dc3d8a25b1a06f68ac7a9f8318105bcd8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/17/2021
ms.locfileid: "100630746"
---
# <a name="working-with-the-microsoft-defender-for-identity-portal"></a>Arbeiten mit dem Microsoft Defender for Identity-Portal

> [!NOTE]
> Auf alle auf dieser Seite erläuterten [!INCLUDE [Product long](includes/product-long.md)]-Features kann auch über das neue [Cloud App Security-Portal](https://portal.cloudappsecurity.com) zugegriffen werden.

Verwenden Sie das [!INCLUDE [Product long](includes/product-long.md)]-Portal, um von [!INCLUDE [Product short](includes/product-short.md)] erkannte verdächtige Aktivitäten zu überwachen und darauf zu reagieren.

Drücken Sie die `?`-Taste, um die Tastenkombinationen für den Zugriff auf das [!INCLUDE [Product short](includes/product-short.md)]-Portal anzuzeigen.

Das [!INCLUDE [Product short](includes/product-short.md)]-Portal bietet einen schnellen Überblick über alle verdächtigen Aktivitäten in chronologischer Reihenfolge. Sie ermöglicht es Ihnen, sich die Details einer Aktivität anzusehen und Aktionen entsprechend der jeweiligen Aktivität auszuführen. Das [!INCLUDE [Product short](includes/product-short.md)]-Portal zeigt außerdem Warnungen und Benachrichtigungen an, um von [!INCLUDE [Product short](includes/product-short.md)] erkannte Probleme oder neue, als verdächtig eingestufte Aktivitäten hervorzuheben.

In diesem Artikel wird beschrieben, wie Sie die wichtigsten Elemente des [!INCLUDE [Product short](includes/product-short.md)]-Portals verwenden.

## <a name="enabling-access-to-the-defender-for-identity-portal"></a>Aktivieren des Zugriffs auf das Defender for Identity-Portal

Für eine erfolgreiche Anmeldung beim [!INCLUDE [Product short](includes/product-short.md)]-Portal müssen Sie einen Benutzernamen verwenden, der einer Azure Active Directory-Sicherheitsgruppe mit Zugriff auf das [!INCLUDE [Product short](includes/product-short.md)]-Portal zugewiesen wurde.
Weitere Informationen zur rollenbasierten Zugriffssteuerung in [!INCLUDE [Product short](includes/product-short.md)] finden Sie unter [Arbeiten mit [!INCLUDE [Product short](includes/product-short.md)]-Rollengruppen](role-groups.md).

## <a name="logging-into-the-defender-for-identity-portal"></a>Anmelden beim Defender for Identity-Portal

1. Sie können auf das [!INCLUDE [Product short](includes/product-short.md)]-Portal zugreifen, indem Sie sich unter [https://portal.atp.azure.com](https://portal.atp.azure.com) beim Portal anmelden und Ihre Instanz auswählen oder indem Sie die folgende Instanz-URL öffnen: `https://*instancename*.atp.azure.com`.

1. [!INCLUDE [Product short](includes/product-short.md)] unterstützt die in die Windows-Authentifizierung integrierte einmalige Anmeldung: Wenn Sie schon bei Ihrem Computer angemeldet sind, verwendet [!INCLUDE [Product short](includes/product-short.md)] dieses Token, um Sie beim [!INCLUDE [Product short](includes/product-short.md)]-Portal anzumelden. Sie können sich auch mit einer Smartcard anmelden. Ihre Berechtigungen in [!INCLUDE [Product short](includes/product-short.md)] entsprechen Ihrer [Administratorrolle](role-groups.md).

   > [!NOTE]
   > Stellen Sie sicher, dass Sie sich bei dem Computer anmelden, von dem aus Sie auf das [!INCLUDE [Product short](includes/product-short.md)]-Portal zugreifen möchten. Verwenden Sie hierzu Ihren Administratorbenutzernamen für [!INCLUDE [Product short](includes/product-short.md)] und das dazugehörige Kennwort. Alternativ dazu führen Sie Ihren Browser als anderer Benutzer aus oder melden sich von Windows ab und melden sich danach mit Ihrem [!INCLUDE [Product short](includes/product-short.md)]-Administratorbenutzerkonto an. Im Gegensatz zum [!INCLUDE [Product short](includes/product-short.md)]-Portal ermöglicht das neue [Cloud App Security-Portal](https://portal.cloudappsecurity.com) die Anmeldung mehrerer Benutzer und erfordert keine zusätzlichen Lizenzen für die Verwendung mit [!INCLUDE [Product short](includes/product-short.md)].

### <a name="attack-time-line"></a>Angriffszeitachse

Die Angriffszeitachse ist die standardmäßige Landing Page, auf die Sie gelangen, wenn Sie sich beim [!INCLUDE [Product short](includes/product-short.md)]-Portal anmelden. Standardmäßig werden alle offenen verdächtigen Aktivitäten auf der Angriffszeitachse angezeigt. Sie können die Angriffszeitachse filtern, um alle bzw. offene, verworfene oder unterdrückte verdächtige Aktivitäten anzuzeigen. Außerdem wird der Schweregrad angezeigt, der den einzelnen Aktivitäten zugewiesen wurde.

![Abbildung der Angriffszeitachse von [!INCLUDE [Product short](includes/product-short.md)]](media/sa-timeline.png)

Weitere Informationen finden Sie unter [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md).

### <a name="whats-new"></a>Neuerungen

Nach der Veröffentlichung einer neuen Version von [!INCLUDE [Product short](includes/product-short.md)] wird in der oberen rechten Ecke das Fenster **Neuerungen** angezeigt. In diesem Fenster können Sie sich darüber informieren, welche Features in der neusten Version hinzugefügt wurden. Außerdem erhalten Sie einen Link zum Download der Version.

### <a name="filtering-panel"></a>Filterbereich

Sie können basierend auf Status und Schweregrad filtern, welche verdächtigen Aktivitäten auf der Angriffszeitachse oder auf der Registerkarte für verdächtige Aktivitäten des Entitätsprofils angezeigt werden.

<a name="search-bar"></a>

### <a name="search-bar"></a>Suchleiste

Im obersten Menü finden Sie eine Suchleiste. Sie können nach einem bestimmten Benutzer, einem Computer oder nach Gruppen in [!INCLUDE [Product short](includes/product-short.md)] suchen. Beginnen Sie als Versuch einfach mit der Eingabe. Unten in der Suchleiste wird die Anzahl der gefundenen Suchergebnisse angezeigt.

![Abbildung der Suche im [!INCLUDE [Product short](includes/product-short.md)]-Portal](media/workspace-portal-search.png)

Wenn Sie auf die Nummer klicken, können Sie auf die Seite mit den Suchergebnissen zugreifen, auf der Sie die Ergebnisse nach Entitätstyp für weitere Untersuchungen filtern können.

!["search results" (Ergebnisse durchsuchen)](media/search-results.png)

### <a name="health-center"></a>Integritätscenter

Das Integritätscenter zeigt Warnungen an, wenn in Ihrer [!INCLUDE [Product short](includes/product-short.md)]-Instanz etwas nicht ordnungsgemäß funktioniert.

![Abbildung des Integritätscenters von [!INCLUDE [Product short](includes/product-short.md)]](media/health-issue.png)

Jedes Mal, wenn in Ihrem System ein Problem auftritt (z. B. ein Verbindungsfehler oder ein nicht verbundener eigenständiger [!INCLUDE [Product short](includes/product-short.md)]-Sensor), können Sie dies an dem Integritätscenter-Symbol erkennen, auf dem ein roter Punkt angezeigt wird.

![Abbildung des roten Punkts im Integritätscenter von [!INCLUDE [Product short](includes/product-short.md)]](media/health-bar.png)

### <a name="sensitive-groups"></a>Sensible Gruppen

Informationen zu vertraulichen Gruppen in [!INCLUDE [Product short](includes/product-short.md)] finden Sie unter [Arbeiten mit sensiblen Konten](manage-sensitive-honeytoken-accounts.md).

### <a name="mini-profile"></a>Miniprofil

Wenn Sie an einer Stelle im [!INCLUDE [Product short](includes/product-short.md)]-Portal, an der eine einzelne Entität dargestellt wird (z. B. ein Benutzer oder ein Computer), mit der Maus auf diese Entität zeigen, wird automatisch ein Miniprofil geöffnet. Dieses enthält die folgenden Informationen (sofern verfügbar und relevant):

![Abbildung eines Miniprofils in [!INCLUDE [Product short](includes/product-short.md)]](media/mini-profile.png)

- Name
- Titel
- Department
- AD-Tags
- E-Mail
- Office
- Telefonnummer
- Domain
- SAM-Name
- Erstellungsdatum: Datum, an dem die Entität in Active Directory erstellt wurde. Wenn die Entität vor Beginn der Überwachung durch [!INCLUDE [Product short](includes/product-short.md)] erstellt wurde, wird sie nicht angezeigt.
- Erste Aktivität: Der Zeitpunkt der ersten Wahrnehmung einer Aktivität dieser Entität durch [!INCLUDE [Product short](includes/product-short.md)].
- Letzte Aktivität: Der Zeitpunkt der letzten Wahrnehmung einer Aktivität dieser Entität durch [!INCLUDE [Product short](includes/product-short.md)].
- SA-Badge: Wird angezeigt, wenn dieser Entität verdächtige Aktivitäten zugeordnet werden.
- Microsoft Defender ATP-Badge: Wird angezeigt, wenn dieser Entität verdächtige Aktivitäten in Microsoft Defender für Endpunkte zugeordnet werden.
- Badge für Lateral Movement-Pfade: Wird angezeigt, wenn innerhalb der letzten beiden Tage Lateral Movement-Pfade für diese Entität ermittelt wurden.

## <a name="see-also"></a>Weitere Informationen

- [Erstellen von [!INCLUDE [Product short](includes/product-short.md)]-Instanzen](install-step1.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
