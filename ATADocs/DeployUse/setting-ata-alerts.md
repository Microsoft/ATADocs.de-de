---
# required metadata

title: Festlegen von ATA-Warnungen | Microsoft Advanced Threat Analytics
description: Beschreibt, wie ATA für den Versand von Warnungen (per E-Mail oder ATA-Ereignisweiterleitung) bei verdächtigen Aktivitäten konfiguriert werden kann 
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Festlegen von ATA-Warnungen
ATA kann Sie bei verdächtiger Aktivität per E-Mail oder über ATA-Ereignisweiterleitung warnen und das Ereignis an den SIEM-/Syslog-Server weiterleiten. Wenn Sie eine oder beide Arten dieser Warnungen aktivieren, können Sie dabei folgende Optionen festlegen.

> [!NOTE]
> -   E-Mail-Benachrichtigungen enthalten einen Link, mit denen der Benutzer direkt die erkannte verdächtige Aktivität aufrufen kann. Der Hostnamenteil des Links wird von der Einstellung für die ATA-Konsolen-URL auf der Seite „ATA Center“ übernommen. Standardmäßig ist die URL der ATA-Konsole die IP-Adresse, die während der Installation von ATA Center ausgewählt wurde.  Wenn Sie das Konfigurieren von E-Mail-Warnungen beabsichtigen, wird die Verwendung eines FQDN als URL der ATA-Konsole empfohlen.
> -   System Health Alert-Warnungen werden nur per E-Mail gesendet.
> -   Warnungen werden von ATA Center entweder an den SMTP-Server oder an den Syslog-Server gesendet.
> -   E-Mail-Benachrichtigungen über verdächtige Aktivitäten werden nur beim Erstellen der verdächtigen Aktivität gesendet.

## Festlegen von Sprache und die Häufigkeit
Die Einstellung **Sprache** gilt für Benachrichtigungen per E-Mail und für Benachrichtigungen, die an den Syslog-Server gesendet werden.

Die Einstellung **Häufigkeit** gilt nur für die Benachrichtigung, die an den Syslog-Server gesendet werden.

1.  Öffnen Sie die ATA-Konsole.

2.  Wählen Sie auf der Symbolleiste die Einstellungsoption und dann **Konfiguration** aus.

    ![Symbol der ATA-Konfigurationseinstellungen](media/ATA-config-icon.JPG)

3.  Wählen Sie **Warnungen** aus.

4.  Wählen Sie unter **Sprache** die gewünschte Sprache aus.

5.  Wählen Sie unter **Häufigkeit** die Option **Niedrige Frequenz** aus, falls Sie nur eine kurze Benachrichtigung erhalten möchten, wenn eine neue Warnung erstellt wird. Wählen Sie **Hohe Frequenz** aus, falls Sie eine detaillierte Benachrichtigung erhalten möchten, wenn eine neue Warnung erstellt wird oder bestehende Warnungen geändert werden.

    ![Konfigurieren des Ausführlichkeitsgrads für Warnungen](media/ATA-alerts-verbosity-language.png)

6.  Klicken Sie auf **Speichern**.

## Einrichten von E-Mail-Benachrichtigungen
ATA kann Warnungen senden, wenn eine verdächtige Aktivität erkannt wird. Falls E-Mail-Benachrichtigungen aktiviert werden, lassen sich dabei folgende Einstellungen vornehmen.

1.  Klicken Sie auf dem ATA Center-Server auf das Symbol **Microsoft Advanced Threat Analytics Management** auf dem Desktop.

2.  Geben Sie Ihren Benutzernamen und Ihr Kennwort ein, und klicken Sie auf **Anmelden**.

3.  Wählen Sie auf der Symbolleiste die Einstellungsoption und dann **Konfiguration** aus.

    ![Symbol der ATA-Konfigurationseinstellungen](media/ATA-config-icon.JPG)

4.  Wählen Sie **Warnungen** aus.

5.  Aktivieren Sie **E-Mail**, um den Versand von Warn-E-Mails zu aktivieren, und geben Sie die folgenden Informationen ein:

    |Feld|Beschreibung|Wert|
    |---------|---------------|---------|
    |SMTP-Server-Endpunkt (erforderlich)|Geben Sie den vollqualifizierten Domänennamen des SMTP-Servers ein.|Beispiel:<br />smtp.contoso.com|
    |SSL|Schalten Sie auf SSL-Betrieb um, falls der SMTP-Server SSL erfordert. **Hinweis:** Wenn Sie SSL aktivieren, müssen Sie auch die Portnummer ändern.|Der Standardwert ist „deaktiviert“|
    |Authentifizierung|Aktivieren Sie diese Option, falls der Proxyserver eine Authentifizierung erfordert. **Hinweis:** Wenn Authentifizierung aktiviert ist, müssen ein Benutzername und ein Kennwort für ein E-Mail-Konto eingegeben werden, das für den Aufbau einer Verbindung mit dem SMTP-Server berechtigt ist.|Der Standardwert ist „deaktiviert“|
    |Senden von (erforderlich)|Geben Sie die E-Mail-Adresse ein, die als Absender der E-Mail eingetragen wird.|Beispiel:<br />ATA@contoso.com|
    |Senden an (erforderlich)|Geben Sie die E-Mail-Adressen der Benutzer oder E-Mail-Gruppen ein, die per E-Mail benachrichtigt werden sollen, wenn ATA verdächtige Aktivität erkennt. **Hinweis:** Geben Sie jeweils nur eine E-Mail-Adresse ein, und klicken Sie zum Hinzufügen auf das Pluszeichen.|Beispiel:<br />securityteam@contoso.com|

## Einrichten der ATA-Ereignisweiterleitung an SIEM
ATA kann Sie durch das Senden eines Eintrags an den Syslog-Server warnen, wenn verdächtige Aktivität erkannt wird. Falls Syslog-Warnungen aktiviert werden, lassen sich dabei folgende Einstellungen vornehmen.

1.  Vor dem Konfigurieren von Syslog-Warnungen sollten Sie gemeinsam mit dem zuständigen SIEM-Administrator folgende Angaben ermitteln:

    -   FQDN oder IP-Adresse des SIEM-Servers

    -   Port, der vom SIEM-Server abgehört wird

    -   Transportprotokoll: UDP, TCP oder Secure TCP

    -   Versandformat der Daten: RFC 3164 oder 5424

2.  Klicken Sie auf dem ATA Center-Server auf das Symbol **Microsoft Advanced Threat Analytics Management** auf dem Desktop.

3.  Geben Sie Ihren Benutzernamen und Ihr Kennwort ein, und klicken Sie auf **Anmelden**.

4.  Wählen Sie auf der Symbolleiste die Einstellungsoption und dann **Konfiguration** aus.

    ![Symbol der ATA-Konfigurationseinstellungen](media/ATA-config-icon.JPG)

5.  Wählen Sie **Warnungen** aus.

6.  Aktivieren Sie die Option **Syslog**, um das Senden von Warnungen an den Syslog-Server zu veranlassen, und geben Sie folgende Informationen an:

    |Feld|Beschreibung|
    |---------|---------------|
    |Syslog-Server-Endpunkt|FQDN des Syslog-Servers|
    |Transport|UDP, TCP oder Secure TCP|
    |Format|Dies ist das von ATA verwendete Format für das Senden der Ereignisse an den SIEM-Server: RFC 5424 oder RFC 3164.|

## Siehe auch
[Unterstützung finden Sie in unserem Forum.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


