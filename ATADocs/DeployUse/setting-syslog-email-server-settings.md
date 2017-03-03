---
title: Festlegen der E-Mail-Benachrichtigungseinstellungen in Advanced Threat Analytics | Microsoft-Dokumentation
description: "Beschreibt, wie ATA für den Versand von Benachrichtigungen (per E-Mail oder ATA-Ereignisweiterleitung) bei verdächtigen Aktivitäten konfiguriert werden kann"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: bff20bf7-8b53-49da-81e5-b818a1c3b24e
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 22d08a20291b1651a36247e9ffbeff8c881aefc5
ms.openlocfilehash: 9b4db2f6489afc1687783d0a879f9303f3a8c775


---

*Gilt für: Advanced Threat Analytics Version 1.7*



# <a name="provide-ata-with-up-your-email-server-settings"></a>Bereitstellen der Einstellungen Ihres E-Mail-Servers für ATA
ATA kann Benachrichtigungen senden, wenn eine verdächtige Aktivität erkannt wird. Damit ATA E-Mail-Benachrichtigungen senden kann, müssen Sie zunächst die **E-Mail-Servereinstellungen** konfigurieren.

1.  Klicken Sie auf dem ATA Center-Server auf das Symbol **Microsoft Advanced Threat Analytics Management** auf dem Desktop.

2.  Geben Sie Ihren Benutzernamen und Ihr Kennwort ein, und klicken Sie auf **Anmelden**.

3.  Wählen Sie auf der Symbolleiste die Einstellungsoption und dann **Konfiguration** aus.

    ![Symbol der ATA-Konfigurationseinstellungen](media/ATA-config-icon.JPG)

4.  Geben Sie im Bereich **Benachrichtigungen** unter **Mailserver** die folgenden Informationen ein:

    |Feld|Beschreibung|Wert|
    |---------|---------------|---------|
    |SMTP-Server-Endpunkt (erforderlich)|Geben Sie den vollqualifizierten Domänennamen des SMTP-Servers ein, und ändern Sie optional die Portnummer (standardmäßig 25).|Beispiel:<br />smtp.contoso.com|
    |SSL|Schalten Sie auf SSL-Betrieb um, falls der SMTP-Server SSL erfordert. **Hinweis:** Wenn Sie SSL aktivieren, müssen Sie auch die Portnummer ändern.|Der Standardwert ist „deaktiviert“|
    |Authentifizierung|Aktivieren Sie diese Option, falls der Proxyserver eine Authentifizierung erfordert. **Hinweis:** Wenn Authentifizierung aktiviert ist, müssen ein Benutzername und ein Kennwort für ein E-Mail-Konto eingegeben werden, das für den Aufbau einer Verbindung mit dem SMTP-Server berechtigt ist.|Der Standardwert ist „deaktiviert“|
    |Senden von (erforderlich)|Geben Sie die E-Mail-Adresse ein, die als Absender der E-Mail eingetragen wird.|Beispiel:<br />ATA@contoso.com|
    ![Bild mit den ATA-E-Mail-Servereinstellungen](media/ATA-email-server-1.7.png)

## <a name="provide-ata-with-your-syslog-server-settings"></a>Bereitstellen der Einstellungen Ihres Syslog-Servers für ATA
ATA kann Sie durch Senden der Benachrichtigung an den Syslog-Server benachrichtigen, wenn verdächtige Aktivität erkannt wird. Wenn Syslog-Benachrichtigungen aktiviert werden, lassen sich dafür folgende Einstellungen vornehmen.

1.  Vor dem Konfigurieren von Syslog-Benachrichtigungen sollten Sie gemeinsam mit dem zuständigen SIEM-Administrator folgende Angaben ermitteln:

    -   FQDN oder IP-Adresse des SIEM-Servers

    -   Port, der vom SIEM-Server abgehört wird

    -   Transportprotokoll: UDP, TCP oder TLS (geschütztes Syslog)

    -   Versandformat der Daten: RFC 3164 oder 5424

2.  Klicken Sie auf dem ATA Center-Server auf das Symbol **Microsoft Advanced Threat Analytics Management** auf dem Desktop.

3.  Geben Sie Ihren Benutzernamen und Ihr Kennwort ein, und klicken Sie auf **Anmelden**.

4.  Wählen Sie auf der Symbolleiste die Einstellungsoption und dann **Konfiguration** aus.

    ![Symbol der ATA-Konfigurationseinstellungen](media/ATA-config-icon.JPG)

5.  Wählen Sie im Bereich „Benachrichtigungen“ **Syslog-Server** aus, und geben Sie die folgende Informationen ein:

    |Feld|Beschreibung|
    |---------|---------------|
    |Syslog-Server-Endpunkt|Geben Sie den vollqualifizierten Domänennamen des Syslog-Servers ein, und ändern Sie optional die Portnummer (standardmäßig 514).|
    |Transport|Kann UDP, TCP oder TLS (sicheres Syslog) sein|
    |Format|Dies ist das von ATA verwendete Format für das Senden der Ereignisse an den SIEM-Server: RFC 5424 oder RFC 3164.|

 ![ATA Syslog server settings image](media/ata-syslog-server-settings-1.7.png)



## <a name="see-also"></a>Siehe auch
[Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Feb17_HO1-->


