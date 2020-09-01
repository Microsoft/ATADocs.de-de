---
title: Festlegen von Syslog-Einstellungen in Azure Advanced Threat Protection
description: Beschreibt, wie Azure ATP für den Versand von Benachrichtigungen (per E-Mail oder Azure ATP-Ereignisweiterleitung) bei verdächtigen Aktivitäten konfiguriert werden kann
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 09/16/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: a2d29c9c-7ecb-4804-b74b-fde899b28648
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4e7f9e3a5c2bf9e0cdfdd21c3d8f8a9f831ff4b0
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88955665"
---
# <a name="integrate-with-syslog"></a>Integration in Syslog

> [!NOTE]
> Die auf dieser Seite erläuterten Azure ATP-Features sind auch über das neue [Portal](https://portal.cloudappsecurity.com) zugänglich.

Azure ATP kann Sie über verdächtige Aktivitäten benachrichtigen, indem Sicherheits- und Integritätswarnungen über einen nominierten Sensor an Ihren Syslog-Server gesendet werden.

Wenn Syslog-Benachrichtigungen aktiviert werden, lassen sich folgende Einstellungen vornehmen:

   |Feld|Beschreibung|
   |---------|---------------|
   |Sensor|Klicken Sie auf einen ausgewählten Sensor, der für das Aggregieren aller Syslog-Ereignisse und die anschließende Weiterleitung von diesen an Ihren SIEM-Server verantwortlich sein soll.|
   |Dienstendpunkt|Geben Sie den vollqualifizierten Domänennamen des Syslog-Servers ein, und ändern Sie optional die Portnummer (standardmäßig 514).|
   |Transport|Kann UDP, TCP oder TLS (sicheres Syslog) sein|
   |Format|Dies ist das von Azure ATP verwendete Format für das Senden der Ereignisse an den SIEM-Server: RFC 5424 oder RFC 3164.|

1. Vor dem Konfigurieren von Syslog-Benachrichtigungen sollten Sie gemeinsam mit dem zuständigen SIEM-Administrator folgende Angaben ermitteln:

    - FQDN oder IP-Adresse des SIEM-Servers
    - Port, der vom SIEM-Server abgehört wird
    - Transporttyp: UDP, TCP oder TLS (sicheres Syslog)
    - Versandformat der Daten: RFC 3164 oder 5424

1. Öffnen Sie das Azure ATP-Portal.
1. Klicken Sie auf **Einstellungen**.
1. Wählen Sie im Untermenü **Benachrichtigungen und Berichte** die Option **Benachrichtigung** aus.
1. Klicken Sie unter **Syslog-Dienst** auf **Konfigurieren**.
1. Wählen Sie den **Sensor** aus.
1. Geben Sie die URL des **Dienstendpunkts** ein.
1. Wählen Sie das **Transportprotokoll** (TCP oder UDP) aus.
1. Wählen Sie das Format (RFC 3164 oder RFC 5424) aus.
1. Wählen Sie **Syslog-Textnachricht senden** aus, und überprüfen Sie, ob die Nachricht von Ihrer Syslog-Infrastrukturlösung empfangen wird.
1. Klicken Sie auf **Speichern**.

So überprüfen oder ändern Sie die Syslog-Einstellungen:

1. Klicken Sie zunächst auf **Benachrichtigungen** und dann unter **Syslog-Benachrichtigungen** auf **Konfigurieren**:

    ![Abbildung der Syslog-Servereinstellungen für Azure ATP](media/atp-syslog.png)

1. Sie können auswählen, welche Ereignisse an Ihren Syslog-Server gesendet werden sollen. Geben Sie unter **Syslog-Benachrichtigungen** an, welche Benachrichtigungen an Ihren Syslog-Server gesendet werden sollen: neue Sicherheitswarnungen, aktualisierte Sicherheitswarnungen und neue Integritätsprobleme.

> [!NOTE]
> Wenn Sie eine Automatisierung oder Skripts für Azure ATP-SIEM-Protokoll erstellen möchten, sollten Sie zur Identifizierung des Warnungstyps das Feld **externalID** statt des Warnungsnamens verwenden. Warnungsnamen können nämlich gelegentlich geändert werden, während die **externalId** jeder Warnung dauerhaft ist. Weitere Informationen finden Sie unter [Azure ATP-SIEM-Protokollreferenz](cef-format-sa.md).

## <a name="see-also"></a>Weitere Informationen

- [Working with sensitive accounts (Arbeiten mit sensiblen Konten)](sensitive-accounts.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
