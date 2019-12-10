---
title: Kennzeichnen von sensiblen Konten mit Azure ATP | Microsoft-Dokumentation
description: Informationen zum Kennzeichnen von sensiblen Konten mit Azure Advanced Threat Protection (ATP)
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 04/29/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2342a10f932664568065d2ef906d863a875c8096
ms.sourcegitcommit: 6dd002b5a34f230aaada55a6f6178c2f9e1584d9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2019
ms.locfileid: "65196440"
---
# <a name="working-with-sensitive-accounts"></a>Arbeiten mit sensiblen Konten

## <a name="sensitive-entites"></a>Sensible Entitäten

In der folgenden Liste werden die Gruppen aufgeführt, die von Azure ATP als **Sensibel** eingestuft werden. Jede Entität, die Mitglied einer dieser Gruppen ist, wird als sensibel angesehen:

- Administratoren
- Hauptbenutzer
- Konten-Operatoren
- Server-Operatoren
- Druck-Operatoren
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

## <a name="tagging-sensitive-accounts"></a>Kennzeichnen von sensiblen Konten

Neben den obenstehend aufgelisteten Gruppen können Sie auch manuell Gruppen oder Konten als sensibel markieren, um den Erkennungsvorgang zu verbessern. Dies ist wichtig, da für einige Azure ATP-Erkennungsvorgänge, wie die Vorgänge zum Erkennen von Änderungen sensibler Gruppen und von Lateral Movement-Pfaden, die Information erforderlich ist, welche Gruppen und Konten als sensibel angesehen werden. Sie können manuell andere Benutzer und Gruppen als sensibel markieren, z.B. Vorstandsmitglieder, leitende Angestellte und Verkaufsleiter, damit Azure ATP diese als sensibel erkennt.

1.  Klicken Sie im Azure ATP-Portal in der Menüleiste auf das Zahnrad **Konfiguration**.

2.  Klicken Sie unter **Erkennung** auf **Entitätstag**.

    ![Azure ATP-Entitätstags](media/entity-tags.png)

3.  Geben Sie im Abschnitt **Sensibel** die Namen der **sensiblen Konten** und **sensiblen Gruppen** ein, und klicken Sie anschließend auf das Zeichen **+** , um diese hinzuzufügen.

    ![Beispiel: sensibles Azure ATP-Konto](media/sensitive-account-sample.png)

4. Klicken Sie auf **Speichern**.

    
## <a name="see-also"></a>Siehe auch

- [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
