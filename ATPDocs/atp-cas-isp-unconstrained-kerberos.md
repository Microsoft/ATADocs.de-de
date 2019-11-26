---
title: Azure Advanced Threat Protection-Bewertungen des Identitätssicherheitsstatus von uneingeschränktem Kerberos | Microsoft-Dokumentation
description: Dieser Artikel bietet eine Übersicht über die Berichte von Azure ATP zur Bewertung des Identitätssicherheitsstatus von uneingeschränktem Kerberos.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/15/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 7eea354b-7a50-40d9-bfa7-dcccaef23179
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 949f99c2ab19a5765a69c21121a274257c20efb6
ms.sourcegitcommit: be4525a93601d9356a4e487398262a2ffaf8c202
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2019
ms.locfileid: "74206313"
---
# <a name="security-assessment-unsecure-kerberos-delegation"></a>Sicherheitsbewertung: Unsichere Kerberos-Delegierung


## <a name="what-is-kerberos-delegation"></a>Was ist die Kerberos-Delegierung? 

Die Kerberos-Delegierung ist eine Delegierungseinstellung, die es Anwendungen ermöglicht, die Anmeldeinformationen von Endbenutzern für den Zugriff auf Ressourcen im Namen des ursprünglichen Benutzers anzufordern.  

## <a name="what-risk-does-unsecure-kerberos-delegation-pose-to-an-organization"></a>Welches Risiko birgt eine unsichere Kerberos-Delegierung für eine Organisation? 

Eine unsichere Kerberos-Delegierung ermöglicht es einer Entität, bei einem beliebigen anderen Dienst Ihre Identität anzunehmen. Nehmen Sie beispielweise an, Sie verfügen über eine IIS-Website, und das Anwendungspoolkonto ist mit uneingeschränkter Delegierung konfiguriert. Für die IIS-Website ist auch die Windows-Authentifizierung aktiviert, die eine native Kerberos-Authentifizierung ermöglicht, und die Website verwendet einen SQL-Back-End-Server für Geschäftsdaten. Mit Ihrem Domänenadministratorkonto wechseln Sie zur Website und authentifizieren sich dort. Die Website, auf der die uneingeschränkte Delegierung verwendet wird, kann in Ihrem Namen ein Dienstticket von einem Domänencontroller für den SQL-Dienst abrufen.

Das Hauptproblem bei der unsicheren Kerberos-Delegierung besteht darin, dass Sie darauf vertrauen müssen, dass die Anwendung immer die richtigen Aktionen ausführt. Angreifer könnten die Anwendung aber dazu zwingen, ungewünschte Aktionen auszuführen. Wenn Sie als **Domänenadministrator** angemeldet sind, kann die Website ein Ticket für jeden anderen beliebigen Dienst erstellen – und zwar in Ihrem Namen als **Domänenadministrator**. Die Website könnte z.B. einen Domänencontroller auswählen und die Gruppe **Unternehmensadministrator** ändern. Die Website könnte auch den Hash eines KRBTGT-Kontos abrufen oder eine interessante Datei aus Ihrer Personalabteilung herunterladen. Das Risiko ist also bekannt, und die Möglichkeiten, die die unsichere Delegierung eröffnet, sind schier unendlich. 

 
## <a name="how-do-i-use-this-security-assessment"></a>Wie wird diese Sicherheitsbewertung verwendet?

1. Verwenden Sie die Berichtstabelle, um zu ermitteln, welche Ihrer Entitäten, bei denen es sich nicht um Domänencontroller handelt, für die **unsichere Kerberos-Delegierung** konfiguriert sind.    
    <br>![Sicherheitsbewertung: unsichere Kerberos-Delegierung](media/atp-cas-isp-kerberos-delegation-2.png)
1. Führen Sie für Benutzer, die einem Risiko ausgesetzt sind, entsprechende Maßnahmen durch: Entfernen Sie beispielsweise das Attribut für die uneingeschränkte Delegierung, oder richten Sie eine sicherere eingeschränkte Delegierung ein.

## <a name="remediation"></a>Wartung

Weitere Informationen zum Wiederherstellen dieser Kontoarten finden Sie unter [Entfernen von Konten, die eine uneingeschränkte Kerberos-Delegierung verwenden](https://blogs.technet.microsoft.com/389thoughts/2017/04/18/get-rid-of-accounts-that-use-kerberos-unconstrained-delegation/).

## <a name="next-steps"></a>Nächste Schritte
- [Azure ATP-Aktivitätsfilter in Cloud App Security](atp-activities-filtering-mcas.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
