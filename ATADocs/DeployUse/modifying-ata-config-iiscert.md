---
title: "Ändern der ATA-Konfiguration – IIS-Zertifikat | Microsoft ATA"
description: "Beschreibt, wie das von IIS für ATA Center verwendete Zertifikat geändert wird."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e58a0390-57ef-4c68-a987-2e75e5f3d6b3
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: 18d3dfdc2262765d71d82f395273e2972118cbfb


---

# Ändern der ATA-Konfiguration – IIS-Zertifikat

>[!div class="step-by-step"]
[« IP-Adresse der ATA-Konsole](modifying-ata-config-consoleip.md)
[Domänenverbindungskennwort »](modifying-ata-config-dcpassword.md)

## Ändern des IIS-Zertifikats
In der Konsole können Sie das Zertifikat für den ATA Center-Dienst auswählen und ändern, jedoch nicht das von IIS verwendete Zertifikat.

Wenn Sie es ändern möchten, gehen Sie wie folgt vor:

> [!NOTE]
> Nach dem Ändern des IIS-Zertifikats sollten Sie vor der Installation neuer ATA-Gateways das ATA-Gateway-Setuppaket herunterladen.

Führen Sie zum Ändern des von IIS für ATA Center verwendeten Zertifikats die folgenden Schritte auf dem ATA Center-Server aus.

1.  Installieren Sie das neue Zertifikat auf dem ATA Center-Server.

2.  Öffnen Sie den Internetinformationsdienste (IIS)-Manager.

3.  Erweitern Sie den Namen des Servers und dann den Ordner **Sites**.

4.  Wählen Sie die Site „Microsoft ATA Console“ aus, und klicken Sie im Bereich **Aktionen** auf **Bindungen**.

    ![Aktion „Bindungen“ in ATA-Konsole](media/ATA-console-change-IP-bindings.jpg)

5.  Wählen Sie **HTTPS** aus, und klicken Sie auf **Bearbeiten**.

6.  Wählen Sie unter **SSL-Zertifikat** das neue Zertifikat aus.

7.  Laden Sie vor der Installation eines neuen ATA-Gateways das ATA-Gateway-Setuppaket herunter.

>[!div class="step-by-step"]
[« IP-Adresse der ATA-Konsole](modifying-ata-config-consoleip.md)
[Domänenverbindungskennwort »](modifying-ata-config-dcpassword.md)

## Siehe auch
- [Arbeiten mit der ATA-Konsole](working-with-ata-console.md)
- [Installieren von ATA](install-ata.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO4-->


