---
title: "Ändern der ATA-Konfiguration – IP-Adresse der ATA-Konsole | Microsoft Advanced Threat Analytics"
description: "Beschreibt, wie die IP-Adresse der ATA-Konsole geändert wird, über die eine Verknüpfung mit der ATA-Konsole auf den ATA-Gateways erstellt wird."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 50118465-df34-4e04-b0cc-48808b6a96b1
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: ee775e66de1a56b5270b0d32c7d5ca33d4d7980c


---

# Ändern der ATA-Konfiguration – IP-Adresse der ATA-Konsole

>[!div class="step-by-step"]
[« Zertifikat von ATA Center](modifying-ata-config-centercert.md)
[IIS-Zertifikat »](modifying-ata-config-iiscert.md)

## Ändern der IP-Adresse der ATA-Konsole
Standardmäßig ist die URL der ATA-Konsole die IP-Adresse, die Sie beim Installieren von ATA Center als IP-Adresse der ATA-Konsole ausgewählt haben.

Die URL wird in den folgenden Szenarios verwendet:

-   Installation von ATA-Gateways: Wenn ein ATA-Gateway installiert wird, registriert es sich bei ATA Center. Diese Registrierung erfolgt durch Herstellen einer Verbindung mit der ATA-Konsole. Wenn Sie einen vollqualifizierten Domänennamen (FQDN) für die URL der ATA-Konsole eingeben, müssen Sie sicherstellen, dass das ATA-Gateway den FQDN in die IP-Adresse auflösen kann, an die die ATA-Konsole in IIS gebunden ist. Zudem wird die URL zum Erstellen der Verknüpfung mit der ATA-Konsole auf den ATA-Gateways verwendet.

-   Warnungen: Wenn ATA eine SIEM- oder E-Mail-Warnung sendet, enthält diese einen Link zur jeweiligen verdächtigen Aktivität. Dabei bildet die URL der ATA-Konsole den Hostteil des Links.

-   Wenn Sie ein Zertifikat von Ihrer internen Zertifizierungsstelle installiert haben, empfiehlt es sich, die URL mit dem Antragstellernamen im Zertifikat anzugleichen, sodass Benutzer beim Herstellen einer Verbindung mit der ATA-Konsole keine Warnmeldung erhalten.

-   Durch die Verwendung eines FQDN für die URL der ATA-Konsole können Sie die von IIS für die ATA-Konsole verwendete IP-Adresse ändern, ohne dass Warnungen, die in der Vergangenheit gesendet wurden, ungültig werden oder ohne das ATA-Gateway-Setuppaket erneut herunterladen zu müssen. Sie müssen lediglich den DNS mit der neuen IP-Adresse aktualisieren.

> [!NOTE]
> Nach dem Ändern der URL der ATA-Konsole sollten Sie vor der Installation neuer ATA-Gateways das ATA-Gateway-Setuppaket herunterladen.

Führen Sie zum Ändern der von IIS für die ATA-Konsole verwendeten IP-Adresse die folgenden Schritte auf dem ATA Center-Server aus.

1.  Installieren Sie die IP-Adresse auf dem ATA Center-Server.

2.  Öffnen Sie den Internetinformationsdienste-Manager (Internet Information Services (IIS) Manager).

3.  Erweitern Sie den Namen des Servers und dann den Ordner **Sites**.

4.  Wählen Sie die Site „Microsoft ATA Console“ aus, und klicken Sie im Bereich **Aktionen** auf **Bindungen**.

    ![Abbildung – Aktion „Bindungen“ in ATA-Konsole](media/ATA-console-change-IP-bindings.jpg)

5.  Wählen Sie **HTTP** aus, und klicken Sie auf **Bearbeiten**, um die neue IP-Adresse auszuwählen. Wählen Sie dann **HTTPS** und die gleiche IP-Adresse aus.

    ![Abbildung: Bearbeiten der Sitebindung](media/ATA-change-console-IP.jpg)

6.  Klicken Sie im Bereich **Aktion** unter **Websites verwalten** auf **Neu starten**.

7.  Öffnen Sie eine Administratorbefehlszeile, und geben Sie die folgenden Befehle zum Aktualisieren des HTTP.SYS-Treibers ein:

    -   Hinzufügen der neuen IP-Adresse:  `netsh http add iplisten ipaddress=newipaddress`

    -   Überprüfen, ob die neue Adresse verwendet wird:  `netsh http show iplisten`

    -   Löschen der alten IP-Adresse:  `netsh http delete iplisten ipaddress=oldipaddress`

8.  Wenn die URL der ATA-Konsole noch eine IP-Adresse verwendet, ändern Sie die URL in die neue IP-Adresse, und laden Sie vor der Bereitstellung neuer ATA-Gateways das ATA-Gateway-Setuppaket herunter.

9. Wenn für die URL der ATA-Konsole ein FQDN angegeben ist, aktualisieren Sie den DNS mit der neuen IP-Adresse für den FQDN.

>[!div class="step-by-step"]
[« Zertifikat von ATA Center](modifying-ata-config-centercert.md)
[IIS-Zertifikat »](modifying-ata-config-iiscert.md)


## Siehe auch
- [Arbeiten mit der ATA-Konsole](working-with-ata-console.md)
- [Installieren von ATA](install-ata.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jun16_HO4-->


