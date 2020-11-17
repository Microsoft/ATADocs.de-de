---
title: Ausschließen von Entitäten von Erkennungen in Advanced Threat Analytics
description: Beschreibt, wie Sie verhindern, dass ATA bestimmte Entitätsaktivitäten als verdächtige Aktivitäten erkennt.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 344c0f33-45e1-42e2-a051-f722a4504531
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: b9589c431b787d1cc5af85102925616bc092f7d9
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2020
ms.locfileid: "94690719"
---
# <a name="excluding-entities-from-detections"></a>Ausschließen von Entitäten von der Erkennung

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Dieser Artikel erläutert, wie Sie Entitäten ausschließen, sodass diese keine Warnungen auslösen. So können Sie unbedenkliche wahr-positive Ergebnisse minimieren, aber gleichzeitig sicherstellen, dass wahr-positive Ergebnisse festgestellt werden. Um zu verhindern, dass ATA Warnungen bei Aktivitäten ausgibt, die bei bestimmten Benutzern zu Ihrem ganz normalen Geschäftsalltag gehören, können Sie bestimmte Entitäten ausschließen, sodass diese keine Warnungen auslösen.

Beispiele: Ein Sicherheitsscanner führt eine DNS-Reconnaissance aus, oder ein Administrator führt remote Skripts auf dem Domänencontroller aus. Beides sind sanktionierte Aktivitäten, die im Rahmen des alltäglichen IT-Betriebs in Ihrer Organisation durchgeführt werden.

So schließen Sie Entitäten aus, damit diese keine Warnungen in ATA auslösen:

Es gibt zwei Möglichkeiten, Entitäten ausschließen: in der verdächtigen Aktivität selbst oder über die Registerkarte **Ausschlüsse** auf der Seite **Konfiguration**.

- **In der verdächtigen Aktivität**: Wenn Sie eine Warnung zu einer Aktivität eines Benutzers, eines Computers oder einer IP-Adresse erhalten, der bzw. die diese bestimmte Aktivität ausführen darf und dies möglicherweise häufig tut, klicken Sie in der Zeitachse mit verdächtigen Aktivitäten auf diese Entität, und wählen Sie **Schließen und ausschließen**. <br></br>Dadurch wird der Benutzer, der Computer oder die IP-Adresse der Ausschlussliste für diese verdächtige Aktivität hinzugefügt. Die verdächtige Aktivität wird geschlossen, und Sie wird nicht mehr in der Liste **geöffnete** Ereignisse auf der **Zeitachse für verdächtige Aktivitäten** aufgeführt.

    ![Ausschließen einer Entität](media/exclude-in-sa.png)

- **Auf der Konfigurationsseite**: Um Ausschlüsse zu überprüfen oder zu ändern, klicken Sie auf der Seite **Konfiguration** auf **Ausschlüsse**, und wählen Sie die verdächtige Aktivität aus, z.B. **Sensible Anmeldeinformationen wurden offengelegt**.

    ![Konfiguration von Ausschlüssen](media/exclusions-config-page.png)

Um eine Entität aus der Konfiguration der **Ausschlüsse** zu entfernen, klicken Sie auf das Minuszeichen neben dem Namen der Entität, und klicken Sie dann unten auf der Seite auf **Speichern**.

Es wird empfohlen, Ausschlüsse erst zu Erkennungen hinzuzufügen, nachdem Sie Warnungen des entsprechenden Typs erhalten haben und entscheiden können, dass diese tatsächlich unbedenklich wahr positiv sind. 

> [!NOTE]
> Zu Ihrem Schutz bieten nicht alle Erkennungen die Möglichkeit, Ausschlüsse festzulegen. 

Einige Erkennungen bieten Tipps, die Sie bei der Entscheidung unterstützen, was Sie ausschließen können. 

Jeder Ausschluss richtet sich nach dem Kontext. In einigen Kontexten können Sie Benutzer festlegen, in anderen Computer oder IP-Adressen. 

Wenn Sie die Möglichkeit haben, eine IP-Adresse oder einen Computer auszuschließen, können Sie eine der beiden Entitäten auswählen – Sie müssen nicht beide angeben.

> [!NOTE]
> Die Seiten für die Konfiguration können nur von ATA-Administratoren bearbeitet werden.


## <a name="see-also"></a>Weitere Informationen
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Ändern der ATA-Konfiguration](modifying-ata-center-configuration.md)
