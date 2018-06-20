---
title: Kennzeichnen von sensiblen Konten mit Azure ATP | Microsoft-Dokumentation
description: Informationen zum Kennzeichnen von sensiblen Konten mit Azure Advanced Threat Protection (ATP)
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4270ebda76309e19518f9d49b72bbce7f9bb5f32
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/21/2018
ms.locfileid: "29444956"
---
*Gilt für: Azure Advanced Threat Protection Version 1.9*



# <a name="working-with-sensitive-accounts"></a>Arbeiten mit sensiblen Konten

## <a name="sensitive-groups"></a>Sensible Gruppen

In der folgenden Liste werden die Gruppen aufgeführt, die von Azure ATP als „Sensibel“ eingestuft werden. Jede Entität, die Mitglied dieser Gruppen ist, wird als sensibel angesehen:

-   Administratoren
-   Hauptbenutzer
-   Konten-Operatoren
-   Server-Operatoren
-   Druck-Operatoren
-   Sicherungsoperatoren
-   Replikatoren
-   Remotedesktopbenutzer 
-   Netzwerkkonfigurations-Operatoren 
-   Eingehende Gesamtstruktur-Vertrauensstellung
-   Domänen-Admins
-   Domänencontroller
-   Gruppenrichtlinienersteller-Besitzer 
-   Schreibgeschützte Domänencontroller 
-   Schreibgeschützte Domänencontroller der Organisation 
-   Schema-Admins 
-   Organisations-Admins


## <a name="tagging-sensitive-accounts"></a>Kennzeichnen von sensiblen Konten

Neben den obenstehend aufgelisteten Gruppen können Sie auch manuell Gruppen oder Konten als sensibel markieren, um den Erkennungsvorgang zu verbessern. Dies ist wichtig, da für einige Azure ATP-Erkennungsvorgänge, wie die Vorgänge zum Erkennen von Änderungen sensibler Gruppen und von Lateral Movement-Pfaden, die Information erforderlich ist, welche Gruppen und Konten als sensibel angesehen werden. Sie können manuell andere Benutzer und Gruppen als sensibel markieren, z.B. Vorstandsmitglieder, leitende Angestellte und Verkaufsleiter, damit Azure ATP diese als sensibel erkennt.

1.  Klicken Sie im Azure ATP-Arbeitsbereichsportal in der Menüleiste auf das Zahnrad **Konfiguration**.

2.  Klicken Sie unter **Erkennung** auf **Entitätstag**.

    ![Azure ATP-Entitätstags](media/entity-tags.png)

3.  Geben Sie im Abschnitt **Sensibel** die Namen der **sensiblen Konten** und **sensiblen Gruppen** ein, und klicken Sie anschließend auf das Zeichen **+**, um diese hinzuzufügen.

    ![Beispiel: sensibles Azure ATP-Konto](media/sensitive-account-sample.png)

4. Klicken Sie auf **Speichern**.

    
## <a name="see-also"></a>Siehe auch

- [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)