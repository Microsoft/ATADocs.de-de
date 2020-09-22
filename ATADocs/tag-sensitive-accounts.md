---
title: Kennzeichnen von sensiblen Konten mit ATA
description: Informationen zum Markieren von sensiblen Konten mit Advanced Threat Analytics (ATA)
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 6/14/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 40a1c5c4-b8d6-477c-8ae5-562b37661624
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 233d6f51e35081740d068635646318abc503268f
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2020
ms.locfileid: "90911968"
---
# <a name="tag-sensitive-accounts"></a>Kennzeichnen von sensiblen Konten


[!INCLUDE [Banner for top of topics](includes/banner.md)]

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Sie können Gruppen oder Konten manuell als sensibel markieren, um den Erkennungsvorgang zu verbessern. Achten Sie darauf, dass die Markierungen aktualisiert werden, weil für einige ATA-Erkennungsvorgänge, wie die Vorgänge zum Erkennen von Änderungen sensibler Gruppen und von Lateral Movement-Pfaden, die Information erforderlich ist, welche Gruppen und Konten als sensibel angesehen werden. In der Vergangenheit hat ATA automatisch Entitäten als *sensibel* festgelegt, wenn es sich um ein Mitglied einer bestimmten Liste von Gruppen gehandelt hat. Sie können manuell andere Benutzer und Gruppen als sensibel markieren, z.B. Vorstandsmitglieder, leitende Angestellte und Verkaufsleiter, damit ATA diese als sensibel erkennt.

1. Klicken Sie in der ATA-Konsole in der Menüleiste auf das Zahnradsymbol **Konfiguration**.

1. Klicken Sie unter **Erkennung** auf **Entitätstag**.

    ![ATA-Entitätstags](media/entity-tags.png)

1. Geben Sie im Abschnitt **Sensibel** die Namen der **sensiblen Konten** und **sensiblen Gruppen** ein, und klicken Sie anschließend auf das Zeichen **+**, um diese hinzuzufügen.

    ![Beispiel: sensibles ATA-Konto](media/sensitive-account-sample.png)

1. Klicken Sie auf **Speichern**.

1. Wenn Sie auf den Entitätsnamen klicken, gelangen Sie zur Seite „Entitätsprofil“. Auf dieser Seite wird angezeigt, warum die Entität als sensibel markiert ist. Dies hängt entweder von der Mitgliedschaft in einer Gruppe oder von einer manuellen Markierung ab.


## <a name="sensitive-groups"></a>Sensible Gruppen

Die Gruppen in der folgenden Liste werden von ATA als „Sensibel“ eingestuft. Jede Entität, die Mitglied dieser Gruppen ist, wird als sensibel angesehen:

- Administratoren
- Hauptbenutzer
- Konten-Operatoren
- Server-Operatoren
- Druck-Operatoren
- Sicherungsoperatoren
- Replikatoren
- Remotedesktopbenutzer 
- Netzwerkkonfigurations-Operatoren 
- Eingehende Gesamtstruktur-Vertrauensstellung
- Domänenadministratoren
- Domänencontroller
- Gruppenrichtlinienersteller-Besitzer 
- Schreibgeschützte Domänencontroller 
- Schreibgeschützte Domänencontroller der Organisation 
- Schema-Admins 
- Organisationsadministratoren
     
## <a name="see-also"></a>Weitere Informationen
[Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
