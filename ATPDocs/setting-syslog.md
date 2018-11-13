---
title: Festlegen von Syslog-Einstellungen in Azure Advanced Threat Protection | Microsoft-Dokumentation
description: Beschreibt, wie Azure ATP für den Versand von Benachrichtigungen (per E-Mail oder Azure ATP-Ereignisweiterleitung) bei verdächtigen Aktivitäten konfiguriert werden kann
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 11/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: a2d29c9c-7ecb-4804-b74b-fde899b28648
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ac01e5ae534fc5df5da70a8d1c47c11c1c455c98
ms.sourcegitcommit: 03b1949beaf2f78a3cdf9396356a96488ea2e127
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2018
ms.locfileid: "50983088"
---
*Gilt für: Azure Advanced Threat Protection*



# <a name="integrate-with-syslog"></a>Integration in Syslog

Azure ATP kann Sie durch Senden der Benachrichtigung an den Syslog-Server benachrichtigen und gibt Sicherheits- und Integritätswarnungen aus, wenn eine verdächtige Aktivität erkannt wird. Wenn Syslog-Benachrichtigungen aktiviert werden, lassen sich folgende Einstellungen vornehmen:

1.  Vor dem Konfigurieren von Syslog-Benachrichtigungen sollten Sie gemeinsam mit dem zuständigen SIEM-Administrator folgende Angaben ermitteln:

    -   FQDN oder IP-Adresse des SIEM-Servers

    -   Port, der vom SIEM-Server abgehört wird

    -   Transportprotokoll: UDP, TCP oder TLS (sicheres Syslog)

    -   Versandformat der Daten: RFC 3164 oder 5424

2.  Geben Sie die URL zum Arbeitsbereich ein.

3.  Geben Sie Ihren Azure Active Directory-Benutzernamen und Ihr Kennwort ein, und klicken Sie auf **Anmelden**.

4.  Wählen Sie auf der Symbolleiste die Einstellungsoption und dann **Konfiguration** aus.

    ![Symbol der Azure ATP-Konfigurationseinstellungen](media/ATP-config-menu.png)

5.  Klicken Sie zunächst auf **Benachrichtigungen** und dann unter **Syslog-Benachrichtigungen** auf **Konfigurieren**:

    |Feld|Beschreibung|
    |---------|---------------|
    |Sensor|Klicken Sie auf einen ausgewählten Sensor, der für das Aggregieren aller Syslog-Ereignisse und die anschließende Weiterleitung von diesen an Ihren SIEM-Server verantwortlich sein soll.|
    |Dienstendpunkt|Geben Sie den vollqualifizierten Domänennamen des Syslog-Servers ein, und ändern Sie optional die Portnummer (standardmäßig 514).|
    |Transport|Kann UDP, TCP oder TLS (sicheres Syslog) sein|
    |Format|Dies ist das von Azure ATP verwendete Format für das Senden der Ereignisse an den SIEM-Server: RFC 5424 oder RFC 3164.|

 ![Abbildung der Syslog-Servereinstellungen für Azure ATP](media/atp-syslog.png)

6. Sie können auswählen, welche Ereignisse an Ihren Syslog-Server gesendet werden sollen. Geben Sie unter **Syslog-Benachrichtigungen** an, welche Benachrichtigungen an Ihren Syslog-Server gesendet werden sollen: neue Sicherheitswarnungen, aktualisierte Sicherheitswarnungen und neue Integritätsprobleme.

> [!NOTE]
> Wenn Sie eine Automatisierung oder Skripts für Azure ATP-SIEM-Protokoll erstellen möchten, sollten Sie zur Identifizierung des Warnungstyps das Feld **externalID** statt des Warnungsnamens verwenden. Warnungsnamen können nämlich gelegentlich geändert werden, während die **externalId** jeder Warnung dauerhaft ist. Weitere Informationen finden Sie unter [Azure ATP-SIEM-Protokollreferenz](cef-format-sa.md). 


## <a name="see-also"></a>Weitere Informationen

- [Working with sensitive accounts (Arbeiten mit sensiblen Konten)](sensitive-accounts.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)