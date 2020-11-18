---
title: Ausschließen von Entitäten von der Erkennung in Microsoft Defender for Identity
description: Hier wird beschrieben, wie Sie verhindern, dass Microsoft Defender for Identity bestimmte Entitätsaktivitäten als verdächtige Aktivitäten erkennt.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: e0f7f1d21132aadba7fc6b3719baf3d290e8d2fb
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848600"
---
# <a name="excluding-entities-from-detections"></a>Ausschließen von Entitäten von der Erkennung

In diesem Artikel wird erläutert, wie Entitäten ausgeschlossen werden, sodass sie keine Warnungen auslösen. Bestimmte Entitäten werden ausgeschlossen, um unbedenkliche richtig positive Ergebnisse zu reduzieren, während gleichzeitig sichergestellt wird, dass Sie die richtig positiven Ergebnisse ermitteln können. Um zu verhindern, dass [!INCLUDE [Product long](includes/product-long.md)] störende Warnungen bei Aktivitäten ausgibt, die bei bestimmten Benutzern zu Ihrem ganz normalen Geschäftsalltag gehören, können Sie bestimmte Entitäten ausschließen, sodass diese keine Warnungen auslösen. Zusätzlich werden standardmäßig bestimmte beliebte Entitäten ausgeschlossen.

Beispiele: Ein Sicherheitsscanner führt eine DNS-Reconnaissance aus, oder ein Administrator führt Remoteskripts auf dem Domänencontroller aus. Beides sind sanktionierte Aktivitäten, die im Rahmen des alltäglichen IT-Betriebs in Ihrer Organisation durchgeführt werden und ausgeschlossen werden können. Weitere Informationen zu jeder Erkennung in [!INCLUDE [Product short](includes/product-short.md)], die Ihnen dabei helfen, zu entscheiden, welche Entitäten ausgeschlossen werden sollen, finden Sie im [Leitfaden für Sicherheitswarnungen](suspicious-activity-guide.md).

## <a name="entities-excluded-by-default-from-raising-alerts"></a>Entitäten, die standardmäßig ausgeschlossen werden, sodass sie keine Warnungen auslösen können

 Für bestimmte Warnungen (z. B. **verdächtige Kommunikation über DNS**) werden automatische Domänenausschlüsse durch [!INCLUDE [Product short](includes/product-short.md)] basierend auf Kundenfeedback und Recherche hinzugefügt.

![Verdächtige Kommunikation über DNS: automatische Ausschlüsse](media/dns-auto-exclusions.png)

## <a name="exclude-entities-from-raising-alerts"></a>Ausschließen von Entitäten, damit diese keine Warnungen auslösen

Es gibt zwei Möglichkeiten, Entitäten manuell auszuschließen: entweder direkt über die Sicherheitswarnung oder über die Registerkarte **Ausschlüsse** auf der Seite **Konfiguration**.

- **Von der Sicherheitswarnung:** Wenn Sie auf der Aktivitätszeitachse eine Warnung oder Aktivität für einen Benutzer, Computer oder eine IP-Adresse erhalten, der bzw. die die bestimmte Aktivität **ausführen darf** und dies häufig auch tut, führen Sie folgende Schritte aus:
  - Klicken Sie mit der rechten Maustaste auf die drei Punkte am Ende der Zeile für die Sicherheitswarnung auf dieser Entität, und wählen Sie **Close and exclude** (Schließen und ausschließen) aus. Dadurch wird der Benutzer, der Computer oder die IP-Adresse der Ausschlussliste für diese Sicherheitswarnung hinzugefügt. Die Sicherheitswarnung wird daraufhin geschlossen, und die Warnung wird nicht länger in der Ereignisliste auf der **Warnungszeitachse** unter **Open** (Offen) aufgeführt.

    ![Ausschließen einer Entität](media/exclude-in-sa.png)

- **Auf der Konfigurationsseite**:  Um Ausschlüsse zu überprüfen oder zu ändern, klicken Sie unter **Konfiguration** > **Erkennung** auf **Ausschlüsse**, und wählen Sie die Sicherheitswarnung aus, für die der Ausschluss angewendet werden soll, z. B. **DNS-Reconnaissance**.

    ![Konfiguration von Ausschlüssen](media/exclusions.png)

So fügen Sie eine Entität aus der Konfiguration **Ausschlüsse** hinzu: Geben Sie den Identitätsnamen ein, und klicken Sie auf das Pluszeichen. Klicken Sie anschließend am unteren Seitenrand auf **Speichern**.

Um eine Entität aus der Konfiguration der **Ausschlüsse** zu entfernen, klicken Sie auf das Minuszeichen neben dem Namen der Entität, und klicken Sie dann unten auf der Seite auf **Speichern**.

Es wird empfohlen, Ausschlüsse erst zu Erkennungen hinzuzufügen, nachdem Sie Warnungen des bestimmten Typs erhalten haben *und* entscheiden können, dass diese tatsächlich unbedenklich wahr positiv sind.

> [!NOTE]
> Zu Ihrem Schutz bieten nicht alle Erkennungen die Möglichkeit, Ausschlüsse festzulegen.

Einige Erkennungen bieten Tipps, die Sie bei der Entscheidung unterstützen, was Sie ausschließen können.

Jeder Ausschluss richtet sich nach dem Kontext. In einigen Kontexten können Sie Benutzer festlegen, in anderen Computer oder IP-Adressen.

Wenn Sie die Möglichkeit haben, eine IP-Adresse oder einen Computer auszuschließen, können Sie eine der beiden Entitäten auswählen – Sie müssen nicht beide angeben.

> [!NOTE]
> Die Seiten für die Konfiguration können nur von [!INCLUDE [Product short](includes/product-short.md)]-Administratoren bearbeitet werden.

## <a name="see-also"></a>Weitere Informationen:

- [Leitfaden für [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnungen](suspicious-activity-guide.md)
- [Integration in Microsoft Defender for Identity](integrate-mde.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
