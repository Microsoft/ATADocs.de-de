---
title: Festlegen von Syslog-Einstellungen in Microsoft Defender for Identity
description: Beschreibt, wie Microsoft Defender for Identity für den Versand von Benachrichtigungen (per E-Mail oder Microsoft Defender for Identity-Ereignisweiterleitung) bei verdächtigen Aktivitäten konfiguriert werden kann
ms.date: 10/27/2020
ms.topic: how-to
ms.openlocfilehash: 06064b549db61a65b068f78a66d886f29805444f
ms.sourcegitcommit: f92dca4dc3d8a25b1a06f68ac7a9f8318105bcd8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/17/2021
ms.locfileid: "100630508"
---
# <a name="integrate-with-syslog"></a>Integration in Syslog

> [!NOTE]
> Die auf dieser Seite erläuterten [!INCLUDE [Product long](includes/product-long.md)]-Features sind auch über das neue [Portal](https://portal.cloudappsecurity.com) zugänglich.

[!INCLUDE [Product long](includes/product-long.md)] kann Sie über verdächtige Aktivitäten benachrichtigen, indem Sicherheits- und Integritätswarnungen über einen nominierten Sensor an Ihren Syslog-Server gesendet werden.

Wenn Syslog-Benachrichtigungen aktiviert werden, lassen sich folgende Einstellungen vornehmen:

|Feld|Beschreibung|
|---------|---------------|
|Sensor|Klicken Sie auf einen ausgewählten Sensor, der für das Aggregieren aller Syslog-Ereignisse und die anschließende Weiterleitung von diesen an Ihren SIEM-Server verantwortlich sein soll.|
|Dienstendpunkt|Geben Sie den vollqualifizierten Domänennamen des Syslog-Servers ein, und ändern Sie optional die Portnummer (standardmäßig 514).|
|Transport|Kann UDP, TCP oder TLS (sicheres Syslog) sein|
|Format|Dies ist das von [!INCLUDE [Product short](includes/product-short.md)] verwendete Format für das Senden der Ereignisse an den SIEM-Server: RFC 5424 oder RFC 3164.|

1. Vor dem Konfigurieren von Syslog-Benachrichtigungen sollten Sie gemeinsam mit dem zuständigen SIEM-Administrator folgende Angaben ermitteln:

    - FQDN oder IP-Adresse des SIEM-Servers
    - Port, der vom SIEM-Server abgehört wird
    - Transporttyp: UDP, TCP oder TLS (sicheres Syslog)
    - Versandformat der Daten: RFC 3164 oder 5424

1. Öffnen Sie das [!INCLUDE [Product short](includes/product-short.md)]-Portal.
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

    ![Abbildung der Syslog-Servereinstellungen für [!INCLUDE [Product short](includes/product-short.md)]](media/syslog.png)

1. Sie können auswählen, welche Ereignisse an Ihren Syslog-Server gesendet werden sollen. Geben Sie unter **Syslog-Benachrichtigungen** an, welche Benachrichtigungen an Ihren Syslog-Server gesendet werden sollen: neue Sicherheitswarnungen, aktualisierte Sicherheitswarnungen und neue Integritätsprobleme.

> [!NOTE]
> Wenn Sie eine Automatisierung oder Skripts für [!INCLUDE [Product short](includes/product-short.md)]-SIEM-Protokoll erstellen möchten, sollten Sie zur Identifizierung des Warnungstyps das Feld **externalID** statt des Warnungsnamens verwenden. Warnungsnamen können nämlich gelegentlich geändert werden, während die **externalId** jeder Warnung dauerhaft ist. Weitere Informationen finden Sie unter [[!INCLUDE [Product short](includes/product-short.md)]Referenz zum SIEM-Protokoll](cef-format-sa.md).

## <a name="see-also"></a>Weitere Informationen

- [Working with sensitive accounts (Arbeiten mit sensiblen Konten)](manage-sensitive-honeytoken-accounts.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
