---
title: Festlegen der E-Mail-Benachrichtigungseinstellungen in Azure Advanced Threat Protection | Microsoft-Dokumentation
description: Beschreibt, wie Azure ATP für den Versand von Benachrichtigungen (per E-Mail oder Azure ATP-Ereignisweiterleitung) bei verdächtigen Aktivitäten konfiguriert werden kann
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: a2d29c9c-7ecb-4804-b74b-fde899b28648
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 74fe9976df769ae01c58a5d66ca491c3fa8958d9
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/21/2018
ms.locfileid: "29444866"
---
*Gilt für: Azure Advanced Threat Protection*



# <a name="integrate-with-syslog"></a>Integration in Syslog

Azure ATP kann Sie durch Senden der Benachrichtigung an den Syslog-Server benachrichtigen, wenn eine verdächtige Aktivität erkannt wird. Wenn Syslog-Benachrichtigungen aktiviert werden, lassen sich dafür folgende Einstellungen vornehmen.

1.  Vor dem Konfigurieren von Syslog-Benachrichtigungen sollten Sie gemeinsam mit dem zuständigen SIEM-Administrator folgende Angaben ermitteln:

    -   FQDN oder IP-Adresse des SIEM-Servers

    -   Port, der vom SIEM-Server abgehört wird

    -   Transportprotokoll: UDP, TCP oder TLS (sicheres Syslog)

    -   Versandformat der Daten: RFC 3164 oder 5424

2.  Geben Sie die URL zum Arbeitsbereichsportal ein.

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


## <a name="see-also"></a>Weitere Informationen

- [Working with sensitive accounts (Arbeiten mit sensiblen Konten)](sensitive-accounts.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)