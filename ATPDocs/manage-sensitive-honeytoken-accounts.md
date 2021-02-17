---
title: Verwalten von sensiblen oder honeytoken-Konten mit Microsoft Defender für Identity
description: Beschreibt das Verwalten von sensiblen oder honeytoken-Konten mit Microsoft Defender für Identity
ms.date: 02/17/2021
ms.topic: how-to
ms.openlocfilehash: 7078e93ad384d81d59a13ff4b527ca59bc678ad2
ms.sourcegitcommit: f92dca4dc3d8a25b1a06f68ac7a9f8318105bcd8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/17/2021
ms.locfileid: "100630771"
---
# <a name="manage-sensitive-or-honeytoken-accounts"></a>Verwalten von sensiblen oder honeytoken-Konten

In diesem Artikel wird erläutert, wie Sie Entitäts Tags auf sensible Konten anwenden. Dies ist wichtig, da einige [!INCLUDE [Short long](includes/product-short.md)] Erkennungen, z. b. die Erkennung von sensiblen Gruppen Änderungen und der lateral Movement-Pfad, auf den Sensitivitäts Status einer Entität basieren

[!INCLUDE [Product short](includes/product-short.md)] ermöglicht außerdem die Konfiguration von honeytoken-Konten, die als Traps für böswillige Actors verwendet werden. jede Authentifizierung, die mit diesen honeytoken-Konten verknüpft ist (normalerweise ruhende Weise), löst eine Warnung aus.

## <a name="sensitive-entities"></a>Sensible Entitäten

Die Gruppen in der folgenden Liste werden von [!INCLUDE [Short long](includes/product-short.md)] als **Sensibel** eingestuft. Jede Entität, die Mitglied einer dieser Azure Active Directory Gruppen ist, wird als vertraulich eingestuft:

- Administratoren
- Hauptbenutzer
- Konten-Operatoren
- Server-Operatoren
- Druckoperatoren
- Sicherungsoperatoren
- Replikatoren
- Netzwerkkonfigurations-Operatoren
- Eingehende Gesamtstruktur-Vertrauensstellung
- Domänen-Admins
- Domänencontroller
- Gruppenrichtlinienersteller-Besitzer
- Read-only-Domänencontroller
- Schreibgeschützte Domänencontroller der Organisation
- Schema-Admins
- Organisations-Admins
- Microsoft Exchange Server

  > [!NOTE]
  > Bis September 2018 wurden auch Remotedesktopbenutzer von [!INCLUDE [Product short](includes/product-short.md)] automatisch als sensibel erkannt. Remotedesktopentitäten oder -gruppen, die nach diesem Datum hinzugefügt wurden, werden nicht mehr automatisch als sensibel erkannt, während Remotedesktopentitäten oder -gruppen, die vor diesem Datum hinzugefügt wurden, möglicherweise als sensibel markiert bleiben. Diese „Sensibel“-Einstellung kann nun manuell geändert werden.

Zusätzlich zu diesen Gruppen identifiziert [!INCLUDE [Product short](includes/product-short.md)] die folgenden Server mit hochwertigen Ressourcen und bezeichnet diese automatisch als **Sensibel**:

- Zertifizierungsstellenserver
- DHCP-Server
- DNS-Server
- Microsoft Exchange Server

## <a name="manually-tagging-entities"></a>Manuelles Markieren von Entitäten

Sie können Entitäten auch manuell als sensible oder honeytoken-Konten markieren. Wenn Sie manuell weitere Benutzer oder Gruppen, z. b. Boardmitglieder, Firmen Leiter und Vertriebsleiter, markieren, [!INCLUDE [Product short](includes/product-short.md)] werden Sie von bedacht.

### <a name="to-manually-tag-entities"></a>So markieren Sie Entitäten manuell

Gehen Sie folgendermaßen vor, um Entitäten zu markieren:

1. Wählen Sie im [!INCLUDE [Product short](includes/product-short.md)]-Portal **Konfiguration** aus.

    ![[! Konfigurationseinstellungen für [Produkt Short] (includes/Product-Short. MD)] einschließen](media/config-menu.png)

1. Wählen Sie unter **Erkennung** die Option **Entitäts Tags** aus.

    ![[!INCLUDE [Product short](includes/product-short.md)]-Entitätstags](media/entity-tags.png)

1. Führen Sie für jedes Konto, das Sie konfigurieren möchten, folgende Schritte aus:
    1. Geben Sie unter **honeytoken-Konten** **oder vertraulich** den Kontonamen ein.
    1. Klicken Sie auf das Pluszeichen **(+)**.

    > [!TIP]
    > Das Feld "sensitive" oder "honeytoken Account" ist durchsuchbar und wird automatisch mit Entitäten in Ihrem Netzwerk ausgefüllt.

    ![Beispiel für ein sensibles [!INCLUDE [Product short](includes/product-short.md)]-Konto](media/sensitive-account-sample.png)

1. Klicken Sie auf **Speichern**.

## <a name="see-also"></a>Weitere Informationen:

- [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
