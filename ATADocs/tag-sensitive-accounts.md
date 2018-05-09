---
title: Markieren von sensiblen Konten mit ATA | Microsoft-Dokumentation
description: Informationen zum Markieren von sensiblen Konten mit Advanced Threat Analytics (ATA)
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 40a1c5c4-b8d6-477c-8ae5-562b37661624
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: d9666c0a4fb3aad027ac1f85719bc533e919d75a
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/22/2018
---
*Gilt für: Advanced Threat Analytics Version 1.9*



# <a name="tag-sensitive-accounts"></a>Kennzeichnen von sensiblen Konten

Sie können Gruppen oder Konten manuell als sensibel markieren, um den Erkennungsvorgang zu verbessern. Achten Sie darauf, dass die Markierungen aktualisiert werden, weil für einige ATA-Erkennungsvorgänge, wie die Vorgänge zum Erkennen von Änderungen sensibler Gruppen und von Lateral Movement-Pfaden, die Information erforderlich ist, welche Gruppen und Konten als sensibel angesehen werden. In der Vergangenheit hat ATA automatisch Entitäten als *sensibel* festgelegt, wenn es sich um ein Mitglied einer bestimmten Liste von Gruppen gehandelt hat. Sie können manuell andere Benutzer und Gruppen als sensibel markieren, z.B. Vorstandsmitglieder, leitende Angestellte und Verkaufsleiter, damit ATA diese als sensibel erkennt.

1.  Klicken Sie in der ATA-Konsole in der Menüleiste auf das Zahnradsymbol **Konfiguration**.

2.  Klicken Sie unter **Erkennung** auf **Entitätstag**.

    ![ATA-Entitätstags](media/entity-tags.png)

3.  Geben Sie im Abschnitt **Sensibel** die Namen der **sensiblen Konten** und **sensiblen Gruppen** ein, und klicken Sie anschließend auf das Zeichen **+**, um diese hinzuzufügen.

    ![Beispiel: sensibles ATA-Konto](media/sensitive-account-sample.png)

4. Klicken Sie auf **Speichern**.

5. Wenn Sie auf den Entitätsnamen klicken, gelangen Sie zur Seite „Entitätsprofil“. Auf dieser Seite wird angezeigt, warum die Entität als sensibel markiert ist. Dies hängt entweder von der Mitgliedschaft in einer Gruppe oder von einer manuellen Markierung ab.

     
## <a name="see-also"></a>Siehe auch
[Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)