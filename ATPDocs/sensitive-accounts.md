---
title: Tag-sensitive Konten mit Microsoft Defender for Identity
description: Hier werden Tag-sensitive Konten mit Microsoft Defender for Identity beschrieben.
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
ms.openlocfilehash: 74e97750d25f48522d38246337682e0399d24c4d
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93274480"
---
# <a name="working-with-sensitive-accounts"></a>Arbeiten mit sensiblen Konten

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="sensitive-entities"></a>Sensible Entitäten

Die Gruppen in der folgenden Liste werden von [!INCLUDE [Product long](includes/product-long.md)] als **Sensibel** eingestuft. Jede Entität, die Mitglied einer dieser Gruppen ist, wird als sensibel angesehen:

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
- Schreibgeschützte Domänencontroller
- Schreibgeschützte Domänencontroller der Organisation
- Schema-Admins
- Organisations-Admins
- Microsoft Exchange Server

  > [!NOTE]
  > Bis September 2018 wurden auch Remotedesktopbenutzer von [!INCLUDE [Product short](includes/product-short.md)] automatisch als sensibel erkannt. Remotedesktopentitäten oder -gruppen, die nach diesem Datum hinzugefügt wurden, werden nicht mehr automatisch als sensibel erkannt, während Remotedesktopentitäten oder -gruppen, die vor diesem Datum hinzugefügt wurden, möglicherweise als sensibel markiert bleiben. Diese „Sensibel“-Einstellung kann nun manuell geändert werden.

Zusätzlich zu diesen Gruppen identifiziert [!INCLUDE [Product short](includes/product-short.md)] die folgenden Server mit hochwertigen Ressourcen und bezeichnet diese automatisch als **Sensibel** :

- Zertifizierungsstellenserver
- DHCP-Server
- DNS-Server
- Microsoft Exchange Server

## <a name="tagging-sensitive-accounts"></a>Kennzeichnen von sensiblen Konten

Neben den obenstehend aufgelisteten Gruppen können Sie auch manuell Gruppen oder Konten als sensibel markieren, um den Erkennungsvorgang zu verbessern. Dies ist wichtig, da für einige [!INCLUDE [Product short](includes/product-short.md)]-Erkennungsvorgänge, wie die Vorgänge zum Erkennen von Änderungen sensibler Gruppen und von Lateral Movement-Pfaden, die Information erforderlich ist, welche Gruppen und Konten als sensibel angesehen werden. Sie können manuell andere Benutzer und Gruppen als sensibel markieren, z. B. Vorstandsmitglieder, leitende Angestellte und Verkaufsleiter, damit [!INCLUDE [Product short](includes/product-short.md)] diese als sensibel erkennt.

1. Wählen Sie im [!INCLUDE [Product short](includes/product-short.md)]-Portal **Konfiguration** aus.

1. Klicken Sie unter **Erkennung** auf **Entitätstag**.

    ![[!INCLUDE [Product short](includes/product-short.md)]-Entitätsmarkierungen](media/entity-tags.png)

1. Geben Sie im Abschnitt **Sensibel** die Namen der **sensiblen Konten** und **sensiblen Gruppen** ein, und klicken Sie anschließend auf das Zeichen **+** , um diese hinzuzufügen.

    ![Beispiel für ein sensibles [!INCLUDE [Product short](includes/product-short.md)]-Konto](media/sensitive-account-sample.png)

1. Klicken Sie auf **Speichern**.

## <a name="see-also"></a>Weitere Informationen:

- [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
