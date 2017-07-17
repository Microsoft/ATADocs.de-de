---
title: "Installieren von Advanced Threat Analytics – Schritt 4 | Microsoft-Dokumentation"
description: Im vierten Schritt beim Installieren von ATA installieren Sie das ATA-Gateway.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/18/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 6bbc50c3-bfa8-41db-a2f9-56eed68ef5d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 2713f6939c8756d0ecb438e866e6649f13d3c490
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/30/2017
---
*Gilt für: Advanced Threat Analytics Version 1.8*



# Installieren von ATA – Schritt 4
<a id="install-ata---step-4" class="xliff"></a>

>[!div class="step-by-step"]
[« Schritt 3](install-ata-step3.md)
[Schritt 5 »](install-ata-step5.md)

## Schritt 4: Installieren des ATA-Gateways
<a id="step-4-install-the-ata-gateway" class="xliff"></a>

Überprüfen Sie vor der Installation des ATA-Gateways auf dem dedizierten Server, ob die Portspiegelung ordnungsgemäß konfiguriert ist und ob das ATA-Gateway Datenverkehr zu und von den Domänencontrollern anzeigen kann. Weitere Informationen finden Sie unter [Überprüfen der Portspiegelung](validate-port-mirroring.md).


> [!IMPORTANT]
> Stellen Sie sicher, dass [KB2919355](http://support.microsoft.com/kb/2919355/) installiert wurde.  Führen Sie das folgende PowerShell-Cmdlet aus, um zu überprüfen, ob der Hotfix installiert ist:
>
> `Get-HotFix -Id kb2919355`

Führen Sie die folgenden Schritte auf dem ATA-Gatewayserver aus.

1.  Extrahieren Sie die Dateien aus der ZIP-Datei. 
> [!NOTE] 
> Eine Installation direkt aus der ZIP-Datei schlägt fehl.

2.  Führen Sie **Microsoft ATA Gateway Setup.exe** aus, und befolgen Sie die Anweisungen des Setup-Assistenten.

3.  Wählen Sie auf der Seite **Willkommen** Ihre Sprache aus, und klicken Sie auf **Weiter**.

4.  Der Installations-Assistent überprüft automatisch, ob der Server ein Domänencontroller oder ein dedizierter Server ist. Wenn es sich um einen Domänencontroller handelt wird der ATA-Lightweight-Gateway installiert. Wenn es sich um einen dedizierten Server handelt, wird das ATA-Gateway installiert. 
    
    Beispielsweise wird im Falle eines ATA-Gateways der folgende Bildschirm angezeigt, um Sie darüber zu informieren, dass ein ATA-Gateway auf Ihrem dedizierten Server installiert wird:
    
    ![ATA-Gateway-Installation](media/ata-gw-install.png) Klicken Sie auf **Weiter**.

    > [!NOTE] 
    > Wenn der Domänencontroller oder der dedizierte Server nicht den Mindestanforderungen der Hardware für die Installation entspricht, wird eine Warnung ausgegeben. Dies verhindert nicht, dass Sie auf **Weiter** klicken können und mit der Installation fortfahren können. Dies ist möglicherweise die richtige Option für die Installation von ATA in einer Testumgebung für ein kleines Labor, in der Sie nicht so viel Platz für die Datenspeicherung benötigen. Für Produktionsumgebungen wird empfohlen, mit dem Handbuch zur [Kapazitätsplanung](ata-capacity-planning.md) von ATA zu arbeiten, um sicherzustellen, dass Domänencontroller oder dedizierte Server den nötigen Anforderungen entsprechen.

4.  Geben Sie unter **Configure the Gateway** (Das Gateway konfigurieren) die folgenden Informationen basierend auf Ihrer Umgebung ein:

    ![Abbildung ATA-Gatewaykonfiguration](media/ata-gw-configure.png)

    > [!NOTE]
    > Wenn Sie das ATA-Gateway bereitstellen, müssen Sie keine Anmeldeinformationen bereitstellen. Wenn die ATA-Gatewayinstallation Ihre Anmeldeinformationen nicht mit dem einmaligen Anmelden abrufen kann (die kann z.B. passieren, wenn sich ATA Center nicht in der Domäne befindet, wenn sich das ATA-Gateway nicht dort befindet, verfügen Sie über keine ATA-Gatewayanmeldeinformationen), werden Sie aufgefordert, Anmeldeinformationen anzugeben, so wie folgt. 

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

## Weitere Informationen
<a id="see-also" class="xliff"></a>

- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Voraussetzungen für ATA](ata-prerequisites.md)
