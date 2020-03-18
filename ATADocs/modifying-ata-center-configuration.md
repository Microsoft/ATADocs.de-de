---
title: Ändern der ATA Center-Konfiguration von Advanced Threat Analytics
description: Beschreibt, wie die IP-Adresse, der Port, die URL der Konsole oder das Zertifikat für ATA Center geändert werden.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: rkarlin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 498eea7cfe1393bd0b616fc5cfbb11bd18334f8f
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2020
ms.locfileid: "79414011"
---
# <a name="modifying-the-ata-center-configuration"></a>Bearbeiten der ATA Center-Konfiguration



*Gilt für: Advanced Threat Analytics Version 1.9*

Nach der ersten Bereitstellung sollten Änderungen an ATA Center vorsichtig vorgenommen werden. Gehen Sie wie folgt vor, wenn Sie die URL der Konsole oder das Zertifikat ändern.

## <a name="the-ata-console-url"></a>URL der ATA-Konsole

Die URL wird in den folgenden Szenarios verwendet:

-   Diese URL wird von den ATA-Gateways zur Kommunikation mit ATA Center verwendet.

- Installation von ATA-Gateways: Wenn ein ATA-Gateway installiert wird, registriert es sich bei ATA Center. Diese Registrierung erfolgt durch Herstellen einer Verbindung mit der ATA-Konsole. Wenn Sie einen vollqualifizierten Domänennamen (FQDN) für die URL der ATA-Konsole eingeben, stellen Sie sicher, dass das ATA-Gateway den FQDN in die IP-Adresse auflösen kann, die an die ATA-Konsole gebunden ist.

-   Warnungen: Wenn ATA eine SIEM- oder E-Mail-Warnung sendet, enthält diese einen Link zur jeweiligen verdächtigen Aktivität. Dabei bildet die URL der ATA-Konsole den Hostteil des Links.

-   Wenn Sie ein Zertifikat von Ihrer internen Zertifizierungsstelle (Certification Authority, CA) installiert haben, muss die URL mit dem der Antragstellernamen im Zertifikat übereinstimmen. Dadurch wird verhindert, dass Benutzer beim Verbinden mit der ATA-Konsole eine Warnmeldung erhalten.

-   Durch die Verwendung eines FQDN für die URL der ATA-Konsole können Sie die von der ATA-Konsole verwendete IP-Adresse ändern, ohne dass vorherige Warnungen ungültig werden oder das ATA-Gateway-Paket erneut herunterzuladen. Sie müssen lediglich den DNS mit der neuen IP-Adresse aktualisieren.

1. Vergewissern Sie sich, dass die neue URL, die Sie verwenden möchten, in die IP-Adresse der ATA-Konsole aufgelöst wird.

2. Geben Sie in den ATA-Einstellungen unter **Center** die neue URL ein. Momentan verwendet ATA Center noch immer die ursprüngliche URL. 

   ![Ändern der ATA-Konfiguration](media/change-center-config.png)

   > [!NOTE]
   > Wenn Sie eine benutzerdefinierte IP-Adresse eingegeben haben, können Sie erst auf **Aktivieren** klicken, nachdem die IP-Adresse auf dem ATA Center-Server installiert wurde.
    
3. Warten Sie, bis die ATA-Gateways synchronisiert wurden. Sie verfügen jetzt über zwei mögliche URLs, über die auf die ATA-Konsole zugegriffen werden kann. Solange ein ATA-Gateway eine Verbindung über die ursprüngliche URL herstellen kann, wird die neue nicht verwendet.

4. Klicken Sie, nachdem alle ATA-Gateways mit der aktualisierten Konfiguration synchronisiert wurden, auf der Konfigurationsseite des Centers auf die Schaltfläche **Aktivieren**, um die neue URL zu aktivieren. Bei der Aktivierung der neuen URL verwenden die ATA-Gateways nicht die neue URL für den Zugriff auf ATA Center. Nach dem Herstellen der Verbindung mit dem ATA Center-Dienst ruft das ATA-Gateway die neueste Konfiguration ab und verfügt nur noch über die neue URL für die ATA-Konsole. 

   ![Aktivieren des Zertifikats](media/center-activation.png)

> [!NOTE]
> -   Wenn ein ATA-Gateway während der Aktivierung der neuen URL offline geschaltet war und die aktualisierte Konfiguration nicht abrufen konnte, aktualisieren Sie die JSON-Konfigurationsdatei im ATA-Gateway manuell.
> -   Wenn Sie nach dem Aktivieren der neuen URL ein neues ATA-Gateway bereitstellen möchten, müssen Sie das ATA-Gateway-Setuppaket erneut herunterladen.


## <a name="the-ata-center-certificate"></a>Zertifikat für ATA Center

> [!WARNING]
> - Die Erneuerung eines vorhandenen Zertifikats wird nicht unterstützt. Zertifikate lassen sich nur erneuern, indem ein neues Zertifikat erstellt und ATA für die Verwendung des neuen Zertifikats konfiguriert wird.


Ersetzen Sie das Zertifikat wie folgt:

1. Bevor das aktuelle Zertifikat abläuft, erstellen Sie ein neues Zertifikat, und stellen Sie sicher, dass es auf dem ATA Center-Server installiert ist. <br></br>Es wird empfohlen, dass Sie ein Zertifikat von einer internen Zertifizierungsstelle auswählen. Es ist jedoch auch möglich, ein neues selbstsigniertes Zertifikat zu erstellen. Weitere Informationen finden Sie unter [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).

2. Wählen Sie in den ATA-Einstellungen unter **Center** dieses neu erstellte Zertifikat aus. Zu diesem Zeitpunkt ist der ATA Center-Dienst noch an das ursprüngliche Zertifikat gebunden. 

   ![Ändern der ATA-Konfiguration](media/change-center-config.png)

3. Warten Sie, bis die ATA-Gateways synchronisiert wurden. Sie verfügen jetzt über zwei potenzielle Zertifikate, die für die gegenseitige Authentifizierung gültig sind. Solange ein ATA-Gateway eine Verbindung über das ursprüngliche Zertifikat herstellen kann, wird das neue Zertifikat nicht verwendet.

4. Nachdem alle ATA-Gateways mit der aktualisierten Konfiguration synchronisiert wurden, aktivieren Sie das neue Zertifikat, an das der ATA Center-Dienst gebunden ist. Wenn Sie das neue Zertifikat aktivieren, bindet der ATA Center-Dienst an das neue Zertifikat. ATA-Gateways verwenden von jetzt an das neue Zertifikat für die Authentifizierung bei ATA Center. Nach dem Herstellen der Verbindung mit dem ATA Center-Dienst ruft das ATA-Gateway die neueste Konfiguration ab und verfügt nur noch über das neue Zertifikat für ATA Center. 

> [!NOTE]
> -   Wenn ein ATA-Gateway während der Aktivierung des neuen Zertifikats offline geschaltet war und die aktualisierte Konfiguration nicht abrufen konnte, aktualisieren Sie die JSON-Konfigurationsdatei im ATA-Gateway manuell.
> -   Das verwendete Zertifikat muss von den ATA-Gateways als vertrauenswürdig eingestuft werden.
> -   Das Zertifikat wird auch für die ATA-Konsole verwendet, deshalb sollte es der Adresse der ATA-Konsole entsprechen, um Browserwarnungen zu vermeiden.
> -   Wenn Sie nach dem Aktivieren des neuen Zertifikats ein neues ATA-Gateway bereitstellen möchten, müssen Sie das ATA-Gateway-Setuppaket erneut herunterladen.



 
## <a name="see-also"></a>Weitere Informationen
- [Arbeiten mit der ATA-Konsole](working-with-ata-console.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://aka.ms/ata-forum)
