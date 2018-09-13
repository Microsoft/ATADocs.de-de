---
title: Installieren von Advanced Threat Analytics – Schritt 4 | Microsoft-Dokumentation
description: Im vierten Schritt beim Installieren von ATA installieren Sie das ATA-Gateway.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 6bbc50c3-bfa8-41db-a2f9-56eed68ef5d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 5414539edca088b49d16dc03c17dfe0ee0a2bfc5
ms.sourcegitcommit: 7f3ded32af35a433d4b407009f87cfa6099f8edf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44125871"
---
*Gilt für: Advanced Threat Analytics Version 1.9*



# <a name="install-ata---step-4"></a>Installieren von ATA – Schritt 4

>[!div class="step-by-step"]
[« Schritt 3](install-ata-step3.md)
[Schritt 5 »](install-ata-step5.md)

## <a name="step-4-install-the-ata-gateway"></a>Schritt 4: Installieren des ATA-Gateways

Überprüfen Sie vor der Installation des ATA-Gateways auf dem dedizierten Server, ob die Portspiegelung ordnungsgemäß konfiguriert ist und ob das ATA-Gateway Datenverkehr zu und von den Domänencontrollern anzeigen kann. Weitere Informationen finden Sie unter [Überprüfen der Portspiegelung](validate-port-mirroring.md).


> [!IMPORTANT]
> Stellen Sie sicher, dass [KB2919355](http://support.microsoft.com/kb/2919355/) installiert wurde.  Führen Sie das folgende PowerShell-Cmdlet aus, um zu überprüfen, ob der Hotfix installiert ist:
>
> `Get-HotFix -Id kb2919355`

Führen Sie die folgenden Schritte auf dem ATA-Gatewayserver aus.

1.  Extrahieren Sie die Dateien aus der ZIP-Datei. 
> [!NOTE] 
> Eine Installation direkt aus der ZIP-Datei verursacht einen Fehler.

2.  Führen Sie **Microsoft ATA Gateway Setup.exe** aus, und befolgen Sie die Anweisungen des Setup-Assistenten.

3.  Wählen Sie auf der Seite **Willkommen** Ihre Sprache aus, und klicken Sie auf **Weiter**.

4.  Der Installations-Assistent überprüft automatisch, ob der Server ein Domänencontroller oder ein dedizierter Server ist. Wenn es sich um einen Domänencontroller handelt, wird das ATA-Lightweight-Gateway installiert. Wenn es sich um einen dedizierten Server handelt, wird das ATA-Gateway installiert. 
    
    Beispielsweise wird im Falle eines ATA-Gateways der folgende Bildschirm angezeigt, um Sie darüber zu informieren, dass ein ATA-Gateway auf Ihrem dedizierten Server installiert wird:
    
    ![ATA-Gateway-Installation](media/ata-gw-install.png) Klicken Sie auf **Weiter**.

    > [!NOTE] 
    > Wenn der Domänencontroller oder der dedizierte Server nicht den Mindestanforderungen der Hardware für die Installation entspricht, erhalten Sie eine Warnung. Dies verhindert nicht, dass Sie auf **Weiter** klicken können und mit der Installation fortfahren können. Dies ist möglicherweise die richtige Option für die Installation von ATA in einer Testumgebung für ein kleines Labor, in der Sie nicht so viel Platz für die Datenspeicherung benötigen. Für Produktionsumgebungen wird empfohlen, mit dem Handbuch zur [Kapazitätsplanung](ata-capacity-planning.md) von ATA zu arbeiten, um sicherzustellen, dass Domänencontroller oder dedizierte Server den nötigen Anforderungen entsprechen.

4.  Geben Sie unter **Configure the Gateway** (Das Gateway konfigurieren) die folgenden Informationen basierend auf Ihrer Umgebung ein:

    ![Abbildung ATA-Gatewaykonfiguration](media/ata-gw-configure.png)

    > [!NOTE]
    > Wenn Sie das ATA-Gateway bereitstellen, müssen Sie keine Anmeldeinformationen angeben. Wenn die ATA-Gatewayinstallation Ihre Anmeldeinformationen nicht über einmaliges Anmelden abrufen kann (wenn sich ATA Center beispielsweise nicht in der Domäne befindet, da Sie dann über keine ATA-Administratoranmeldeinformationen verfügen), werden Sie aufgefordert, Anmeldeinformationen anzugeben, wie im folgenden Bildschirm: 

  ![Bereitstellen von Anmeldeinformationen für das ATA-Gateway](media/ata-install-credentials.png)

   - Installationspfad: Dies ist der Speicherort, an dem das ATA-Gateway installiert wird. Standardmäßig ist dies „%programfiles%\Microsoft Advanced Threat Analytics\Gateway“. Behalten Sie den Standardwert bei.
    
5. Klicken Sie auf **Installieren**. Bei der Installation des ATA-Gateways werden die folgenden Komponenten installiert und konfiguriert:

    -   KB 3047154 (nur für Windows Server 2012 R2)

        > [!IMPORTANT]
        > -   Installieren Sie KB 3047154 nicht auf einem Virtualisierungshost (der Host, auf dem die Virtualisierung ausgeführt wird; die Ausführung auf einem virtuellen Computer ist möglich). Dies kann dazu führen, dass die Portspiegelung nicht mehr ordnungsgemäß ausgeführt wird. 
        > -   Installieren Sie Message Analyzer, Wireshark oder andere Software zur Netzwerkerfassung nicht auf dem ATA-Gateway. Wenn Sie den Netzwerkverkehr erfassen möchten, installieren und verwenden Sie Microsoft Network Monitor 3.4.

    -   ATA-Gatewaydienst
    -   Microsoft Visual C++ 2013 Redistributable
    -   Benutzerdefinierter Systemmonitor-Datensammlungssatz

5.  Nach Abschluss der Installation klicken Sie für das ATA-Gateway auf **Starten**, um den Browser zu öffnen und sich bei der ATA-Konsole anzumelden, bzw. klicken Sie für das ATA-Lightweight-Gateway auf **Fertig stellen**.


>[!div class="step-by-step"]
[« Schritt 3](install-ata-step3.md)
[Schritt 5 »](install-ata-step5.md)


## <a name="related-videos"></a>Verwandte Videos
- [Übersicht über die ATA-Bereitstellung](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Auswählen des richtigen ATA-Gatewaytyps](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)

## <a name="see-also"></a>Weitere Informationen
- [Handbuch für die ATA POC-Bereitstellung](http://aka.ms/atapoc)
- [Tool zur Bemessung von ATA-Gateways](http://aka.ms/atasizingtool)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Voraussetzungen für ATA](ata-prerequisites.md)

