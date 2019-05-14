---
title: Festlegen von Syslog-Einstellungen in Azure Advanced Threat Protection | Microsoft-Dokumentation
description: Beschreibt, wie Azure ATP für den Versand von Benachrichtigungen (per E-Mail oder Azure ATP-Ereignisweiterleitung) bei verdächtigen Aktivitäten konfiguriert werden kann
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 12/02/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: a2d29c9c-7ecb-4804-b74b-fde899b28648
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7a17f5156f7060028e10a66907776f23a9709442
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2019
ms.locfileid: "65196434"
---
# <a name="integrate-with-syslog"></a>Integration in Syslog

Azure ATP kann Sie durch Senden der Benachrichtigung an den Syslog-Server benachrichtigen und gibt Sicherheits- und Integritätswarnungen aus, wenn eine verdächtige Aktivität erkannt wird. Wenn Syslog-Benachrichtigungen aktiviert werden, lassen sich folgende Einstellungen vornehmen:

1. Vor dem Konfigurieren von Syslog-Benachrichtigungen sollten Sie gemeinsam mit dem zuständigen SIEM-Administrator folgende Angaben ermitteln:

   -   FQDN oder IP-Adresse des SIEM-Servers

   -   Port, der vom SIEM-Server abgehört wird

   -   Transporttyp: UDP, TCP oder TLS (sicheres Syslog)

   -   Versandformat der Daten: RFC 3164 oder 5424

2. Geben Sie die Instanz-URL ein.

3. Geben Sie Ihren Azure Active Directory-Benutzernamen und Ihr Kennwort ein, und klicken Sie auf **Anmelden**.

4. Wählen Sie auf der Symbolleiste die Einstellungsoption und dann **Konfiguration** aus.

   ![Symbol der Azure ATP-Konfigurationseinstellungen](media/ATP-config-menu.png)

5. Klicken Sie zunächst auf **Benachrichtigungen** und dann unter **Syslog-Benachrichtigungen** auf **Konfigurieren**:

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
