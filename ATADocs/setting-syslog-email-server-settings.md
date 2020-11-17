---
title: Festlegen von e-Mail-Benachrichtigungen in Advanced Threat Analytics
description: Beschreibt, wie ATA für den Versand von Benachrichtigungen (per E-Mail oder ATA-Ereignisweiterleitung) bei verdächtigen Aktivitäten konfiguriert werden kann
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: bff20bf7-8b53-49da-81e5-b818a1c3b24e
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 833b5604a957ff5910598bfcf8b12c86027ee638
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2020
ms.locfileid: "94690328"
---
# <a name="provide-ata-with-your-email-server-settings"></a>Bereitstellen der Einstellungen Ihres E-Mail-Servers für ATA

[!INCLUDE [Banner for top of topics](includes/banner.md)]

ATA kann Benachrichtigungen senden, wenn eine verdächtige Aktivität erkannt wird. Damit ATA e-Mail-Benachrichtigungen senden kann, müssen Sie zunächst die **e-Mail-Servereinstellungen** konfigurieren.

1. Klicken Sie auf dem ATA Center-Server auf das Symbol **Microsoft Advanced Threat Analytics Management** auf dem Desktop.

1. Geben Sie Ihren Benutzernamen und Ihr Kennwort ein, und klicken Sie auf **Anmelden**

1. Wählen Sie auf der Symbolleiste die Option Einstellungen, und wählen Sie **Konfiguration** aus.

    ![Symbol der ATA-Konfigurationseinstellungen](media/ATA-config-icon.png)

1. Geben Sie im Bereich **Benachrichtigungen** unter **Mailserver** die folgenden Informationen ein:


   |              Feld              |                                                                                                 BESCHREIBUNG                                                                                                  |               Wert                |
   |---------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------|
   | SMTP-Server-Endpunkt (erforderlich) |                                                            Geben Sie den vollqualifizierten Domänennamen des SMTP-Servers ein, und ändern Sie optional die Portnummer (standardmäßig 25).                                                            | Beispiel:<br />smtp.contoso.com |
   |               SSL               |                                              Schalten Sie auf SSL-Betrieb um, falls der SMTP-Server SSL erfordert. **Hinweis:** Wenn Sie SSL aktivieren, müssen Sie auch die Portnummer ändern.                                               |        Der Standardwert ist „deaktiviert“         |
   |         Authentifizierung          | Aktivieren Sie diese Option, falls der Proxyserver eine Authentifizierung erfordert. **Hinweis:** Wenn Authentifizierung aktiviert ist, müssen ein Benutzername und ein Kennwort für ein E-Mail-Konto eingegeben werden, das für den Aufbau einer Verbindung mit dem SMTP-Server berechtigt ist. |        Der Standardwert ist „deaktiviert“         |
   |      Senden von (erforderlich)       |                                                                        Geben Sie die E-Mail-Adresse ein, die als Absender der E-Mail eingetragen wird.                                                                         | Beispiel:<br />ATA@contoso.com  |

    ![Bild mit den ATA-E-Mail-Servereinstellungen](media/ata-email-server.png)

## <a name="provide-ata-with-your-syslog-server-settings"></a>Bereitstellen der Einstellungen Ihres Syslog-Servers für ATA
ATA kann Sie durch Senden der Benachrichtigung an den Syslog-Server benachrichtigen, wenn verdächtige Aktivität erkannt wird. Wenn Syslog-Benachrichtigungen aktiviert werden, lassen sich dafür folgende Einstellungen vornehmen.

1. Vor dem Konfigurieren von Syslog-Benachrichtigungen sollten Sie gemeinsam mit dem zuständigen SIEM-Administrator folgende Angaben ermitteln:

   - FQDN oder IP-Adresse des SIEM-Servers

   - Port, der vom SIEM-Server abgehört wird

   - Transporttyp: UDP, TCP oder TLS (sicheres Syslog)

   - Versandformat der Daten: RFC 3164 oder 5424

1. Klicken Sie auf dem ATA Center-Server auf das Symbol **Microsoft Advanced Threat Analytics Management** auf dem Desktop.

1. Geben Sie Ihren Benutzernamen und Ihr Kennwort ein, und klicken Sie auf **Anmelden**

1. Wählen Sie auf der Symbolleiste die Option Einstellungen, und wählen Sie **Konfiguration** aus.

    ![Symbol der ATA-Konfigurationseinstellungen](media/ATA-config-icon.png)

1. Wählen Sie im Bereich „Benachrichtigungen“ **Syslog-Server** aus, und geben Sie die folgende Informationen ein:

   |Feld|BESCHREIBUNG|
   |---------|---------------|
   |Syslog-Server-Endpunkt|Geben Sie den vollqualifizierten Domänennamen des Syslog-Servers ein, und ändern Sie optional die Portnummer (standardmäßig 514).|
   |Transport|Kann UDP, TCP oder TLS (sicheres Syslog) sein|
   |Format|Dies ist das von ATA verwendete Format für das Senden der Ereignisse an den SIEM-Server: RFC 5424 oder RFC 3164.|

    ![ATA Syslog server settings image](media/ata-syslog-server-settings.png)



## <a name="see-also"></a>Weitere Informationen
[Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
