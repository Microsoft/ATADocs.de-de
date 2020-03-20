---
title: Kennzeichnen von vertraulichen Konten mit Azure ATP
description: Informationen zum Kennzeichnen von sensiblen Konten mit Azure Advanced Threat Protection (ATP)
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 02/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 465879661322a7e71412570ad052c18575df3ade
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2020
ms.locfileid: "79410968"
---
# <a name="working-with-sensitive-accounts"></a>Arbeiten mit sensiblen Konten

## <a name="sensitive-entities"></a>Sensible Entitäten

In der folgenden Liste werden die Gruppen aufgeführt, die von Azure ATP als **Sensibel** eingestuft werden. Jede Entität, die Mitglied einer dieser Gruppen ist, wird als sensibel angesehen:

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
  > Bis September 2018 wurden auch Remotedesktopbenutzer von Azure ATP automatisch als sensibel erkannt. Remotedesktopentitäten oder -gruppen, die nach diesem Datum hinzugefügt wurden, werden nicht mehr automatisch als sensibel erkannt, während Remotedesktopentitäten oder -gruppen, die vor diesem Datum hinzugefügt wurden, möglicherweise als sensibel markiert bleiben. Diese „Sensibel“-Einstellung kann nun manuell geändert werden.

Zusätzlich zu diesen Gruppen identifiziert Azure ATP die folgenden Server mit hochwertigen Ressourcen und bezeichnet diese automatisch als **sensibel**:

- Zertifizierungsstellenserver
- DHCP-Server
- DNS-Server
- Microsoft Exchange Server

## <a name="tagging-sensitive-accounts"></a>Kennzeichnen von sensiblen Konten

Neben den obenstehend aufgelisteten Gruppen können Sie auch manuell Gruppen oder Konten als sensibel markieren, um den Erkennungsvorgang zu verbessern. Dies ist wichtig, da für einige Azure ATP-Erkennungsvorgänge, wie die Vorgänge zum Erkennen von Änderungen sensibler Gruppen und von Lateral Movement-Pfaden, die Information erforderlich ist, welche Gruppen und Konten als sensibel angesehen werden. Sie können manuell andere Benutzer und Gruppen als sensibel markieren, z.B. Vorstandsmitglieder, leitende Angestellte und Verkaufsleiter, damit Azure ATP diese als sensibel erkennt.

1. Klicken Sie im Azure ATP-Portal in der Menüleiste auf das Zahnrad **Konfiguration**.

1. Klicken Sie unter **Erkennung** auf **Entitätstag**.

    ![Azure ATP-Entitätstags](media/entity-tags.png)

1. Geben Sie im Abschnitt **Sensibel** die Namen der **sensiblen Konten** und **sensiblen Gruppen** ein, und klicken Sie anschließend auf das Zeichen **+** , um diese hinzuzufügen.

    ![Beispiel: sensibles Azure ATP-Konto](media/sensitive-account-sample.png)

1. Klicken Sie auf **Speichern**.

## <a name="see-also"></a>Weitere Informationen:

- [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
