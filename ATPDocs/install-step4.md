---
title: 'Schnellstart: Installieren des Microsoft Defender for Identity-Sensors'
description: Im vierten Schritt der Installation von Microsoft Defender for Identity installieren Sie den Defender for Identity-Sensor.
ms.date: 02/17/2021
ms.topic: quickstart
ms.openlocfilehash: a9837c36dcdb90dba124eda5f8d6b9f082787d74
ms.sourcegitcommit: 5bf0c6a204b71126306a0c64108eaf9cb7fc042f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/18/2021
ms.locfileid: "101097407"
---
# <a name="quickstart-install-the-microsoft-defender-for-identity-sensor"></a>Schnellstart: Installieren des Microsoft Defender for Identity-Sensors

In diesem Schnellstart installieren Sie den [!INCLUDE [Product long](includes/product-long.md)]-Sensor auf einem Domänencontroller. Wenn Sie eine automatische Installation bevorzugen, finden Sie im [entsprechenden Artikel](silent-installation.md) weitere Informationen.

## <a name="prerequisites"></a>Voraussetzungen

- Eine [[!INCLUDE [Product short](includes/product-short.md)]-Instanz](install-step1.md), die [mit Active Directory verbunden](install-step2.md) ist
- Eine heruntergeladene Kopie des [[!INCLUDE [Product short](includes/product-short.md)]-Sensorsetuppakets](install-step3.md) und den Zugriffsschlüssel
- Stellen Sie sicher, dass Microsoft .NET Framework 4.7 oder höher auf dem Computer installiert ist. Wenn Microsoft .NET Framework 4.7 oder höher nicht installiert ist, wird es vom Setuppaket für den [!INCLUDE [Product short](includes/product-short.md)]-Sensor installiert. Dadurch ist möglicherweise ein Neustart des Servers erforderlich.
- Wenn Sie bei der Sensorinstallation auf AD FS-Servern eine externe SQL Server-Instanz verwenden, konfigurieren Sie diese, um für das *Verzeichnisdienstkonto* (**Konfiguration** > **Verzeichnisdienste** > **Benutzername**) die Berechtigungen *Verbinden*, *Anmelden*, *Lesen* und *Auswählen* für die **AdfsConfiguration**-Datenbank zuzulassen.

## <a name="install-the-sensor"></a>Installieren des Sensors

Führen Sie auf dem Domänencontroller folgende Schritte aus.

1. Stellen Sie sicher, dass der Computer mit den relevanten Endpunkten des [[!INCLUDE [Product short](includes/product-short.md)]-Clouddiensts](configure-proxy.md#enable-access-to-azure-atp-service-urls-in-the-proxy-server) verbunden ist.
1. Extrahieren Sie die Installationsdateien aus der ZIP-Datei. Eine Installation direkt aus der ZIP-Datei schlägt fehl.
1. Führen Sie **Azure ATP sensor setup.exe** mit erhöhten Rechten (**Als Administrator ausführen**) aus, und befolgen Sie die Anweisungen im Setup-Assistenten.
1. Wählen Sie auf der Seite **Willkommen** Ihre Sprache aus, und klicken Sie auf **Weiter**.

    ![Installationssprache des eigenständigen [!INCLUDE [Product short](includes/product-short.md)]-Sensors](media/sensor-install-language.png)

1. Der Installations-Assistent überprüft automatisch, ob der Server ein Domänencontroller oder ein dedizierter Server ist. Wenn es sich um einen Domänencontroller handelt, wird der [!INCLUDE [Product short](includes/product-short.md)]-Sensor installiert. Wenn es sich um einen dedizierten Server handelt, wird der eigenständige [!INCLUDE [Product short](includes/product-short.md)]-Sensor installiert.

    Beispielsweise wird im Falle eines [!INCLUDE [Product short](includes/product-short.md)]-Sensors die folgende Anzeige angezeigt, um Sie darüber zu informieren, dass ein [!INCLUDE [Product short](includes/product-short.md)]-Sensor auf Ihrem dedizierten Server installiert wird:

    ![[!INCLUDE [Product short](includes/product-short.md)]-Sensorinstallation](media/sensor-install-deployment-type.png)

    Klicken Sie auf **Weiter**.

    > [!NOTE]
    > Wenn der Domänencontroller oder der dedizierte Server nicht den Mindestanforderungen der Hardware für die Installation entspricht, wird eine Warnung ausgegeben. Die Warnung verhindert nicht, dass Sie auf **Weiter** klicken und mit der Installation fortfahren können. Dies kann dennoch die richtige Option für die Installation von [!INCLUDE [Product short](includes/product-short.md)] in einer kleinen Labtestumgebung sein, für die nicht viel Platz für die Datenspeicherung erforderlich ist. Für Produktionsumgebungen wird empfohlen, mit dem Leitfaden zur [Kapazitätsplanung](capacity-planning.md) von [!INCLUDE [Product short](includes/product-short.md)] zu arbeiten, um sicherzustellen, dass Domänencontroller oder dedizierte Server den nötigen Anforderungen entsprechen.

1. Geben Sie basierend auf Ihrer Umgebung unter **Configure the sensor** (Sensor konfigurieren) den Installationspfad und den Zugriffsschlüssel ein, die Sie im vorherigen Schritt kopiert haben:

    ![Abbildung der [!INCLUDE [Product short](includes/product-short.md)]-Sensorkonfiguration](media/sensor-install-config.png)

    - Installationspfad: Hierbei handelt es sich um den Speicherort, an dem der [!INCLUDE [Product short](includes/product-short.md)]-Sensor installiert wird. Dabei handelt es sich standardmäßig um folgenden Pfad: %programfiles%\Azure Advanced Threat Protection sensor. Behalten Sie den Standardwert bei.
    - Zugriffsschlüssel: Dieser wird im vorherigen Schritt vom [!INCLUDE [Product short](includes/product-short.md)]-Portal abgerufen.

1. Klicken Sie auf **Installieren**. Die folgenden Komponenten werden während der Installation des [!INCLUDE [Product short](includes/product-short.md)]-Sensors installiert und konfiguriert:

    - KB 3047154 (nur für Windows Server 2012 R2)

        > [!IMPORTANT]
        >
        > - Installieren Sie KB 3047154 nicht auf einem Virtualisierungshost (der Host, auf dem die Virtualisierung ausgeführt wird; die Ausführung auf einem virtuellen Computer ist möglich). Dies kann dazu führen, dass die Portspiegelung nicht mehr ordnungsgemäß ausgeführt wird.
        > - Wenn Wireshark auf dem Computer mit dem [!INCLUDE [Product short](includes/product-short.md)]-Sensor installiert ist, müssen Sie den [!INCLUDE [Product short](includes/product-short.md)]-Sensor neu starten, nachdem Sie Wireshark ausgeführt haben, da beide die gleichen Treiber verwenden.

    - Der [!INCLUDE [Product short](includes/product-short.md)]-Sensordienst und der [!INCLUDE [Product short](includes/product-short.md)]-Sensorupdatedienst
    - Microsoft Visual C++ 2013 Redistributable

## <a name="post-installation-steps-for-ad-fs-servers"></a>Schritte nach der Installation für AD FS-Server

Führen Sie die folgenden Schritte aus, um Defender for Identity zu konfigurieren, sobald Sie die Installation des Sensors auf dem AD FS-Server abgeschlossen haben.

1. Wählen Sie im [!INCLUDE [Product short](includes/product-short.md)]-Portal **Konfiguration** aus.

1. Wählen Sie unter **System** die Option **Sensoren** aus.

    ![[!INCLUDE [Product short](includes/product-short.md)]-Sensorkonfigurationsseite](media/sensor-config.png)

1. Wählen Sie den Sensor aus, den Sie auf dem AD FS Server installiert haben.
1. Geben Sie im Popupfenster im Feld **Resolverdomänencontroller (FQDN)** den FQDN des Resolverdomänencontrollers ein, und klicken Sie dann auf das Pluszeichen **(+)** und auf **Speichern**.  

    ![[!INCLUDE [Product short](includes/product-short.md)] Konfigurieren des AD FS-Sensorresolvers](media/sensor-config-adfs-resolver.png)

    Die Initialisierung des Sensors kann einige Minuten dauern. Zu diesem Zeitpunkt sollte sich der Status des AD FS-Sensordiensts von **beendet** in **wird ausgeführt** ändern.

## <a name="next-steps"></a>Nächste Schritte

Der [!INCLUDE [Product short](includes/product-short.md)]-Sensor ist so konzipiert, dass er nur minimale Auswirkung auf Ihre Domänencontrollerressourcen und Netzwerkaktivitäten hat. Informationen zum Erstellen einer Leistungsbewertung finden Sie unter [Planen der Kapazität für [!INCLUDE [Product short](includes/product-short.md)]](capacity-planning.md).

## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über [!INCLUDE [Product short](includes/product-short.md)] und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [[!INCLUDE [Product short](includes/product-short.md)]Community](https://aka.ms/MDIcommunity) bei.
