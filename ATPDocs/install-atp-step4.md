---
title: 'Schnellstart: Installieren von Azure ATP-Sensoren'
description: Im vierten Schritt der Azure ATP-Installation erhalten Sie Hilfe zur Installation des Azure ATP-Sensors.
author: shsagir
ms.author: shsagir
ms.date: 07/29/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a6861b96143d1baafb315f276a278ff0b98f795f
ms.sourcegitcommit: 3cddeab2d22385a0efe8f95a196576de30c9a60d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/29/2020
ms.locfileid: "87379867"
---
# <a name="quickstart-install-the-azure-atp-sensor"></a>Schnellstart: Installieren des Azure ATP-Sensors

In diesem Schnellstart installieren Sie einen Azure ATP-Sensor auf einem Domänencontroller. Wenn Sie eine automatische Installation bevorzugen, finden Sie im [entsprechenden Artikel](atp-silent-installation.md) weitere Informationen.

## <a name="prerequisites"></a>Voraussetzungen

- Eine [Azure ATP](install-atp-step1.md)-Instanz, die mit [Active Directory verbunden ist](install-atp-step2.md).
- Eine heruntergeladene Kopie des [Setuppakets für Ihren ATP-Sensor](install-atp-step3.md) und den Zugriffsschlüssel.
- Stellen Sie sicher, dass Microsoft .NET Framework 4.7 oder höher auf dem Computer installiert ist. Wenn Microsoft .NET Framework 4.7 oder höher nicht installiert ist, wird es vom Setuppaket für den Azure ATP-Sensor installiert. Dadurch ist möglicherweise ein Neustart des Servers erforderlich.

## <a name="install-the-sensor"></a>Installieren des Sensors

Führen Sie auf dem Domänencontroller folgende Schritte aus.

1. Stellen Sie sicher, dass der Computer mit den relevanten [Azure ATP-Clouddienst](configure-proxy.md#enable-access-to-azure-atp-service-urls-in-the-proxy-server)-Endpunkten verbunden ist:
1. Extrahieren Sie die Installationsdateien aus der ZIP-Datei. Eine Installation direkt aus der ZIP-Datei schlägt fehl.
1. Führen Sie **Azure ATP sensor setup.exe** aus, und befolgen Sie die Anweisungen des Setup-Assistenten.
1. Wählen Sie auf der Seite **Willkommen** Ihre Sprache aus, und klicken Sie auf **Weiter**.

    ![Sprache der Installation des eigenständigen Azure ATP-Sensors](media/sensor-install-language.png)

1. Der Installations-Assistent überprüft automatisch, ob der Server ein Domänencontroller oder ein dedizierter Server ist. Wenn es sich um einen Domänencontroller handelt, wird der Azure ATP-Sensor installiert. Wenn es sich um einen dedizierten Server handelt, wird der eigenständige Azure ATP-Sensor installiert.

    Beispielsweise wird im Falle eines Azure ATP-Sensors die folgende Anzeige angezeigt, um Sie darüber zu informieren, dass ein Azure ATP-Sensor auf Ihrem dedizierten Server installiert wird:

    ![Installation des Azure ATP-Sensors](media/sensor-install-deployment-type.png)

    Klicken Sie auf **Weiter**.

    > [!NOTE]
    > Wenn der Domänencontroller oder der dedizierte Server nicht den Mindestanforderungen der Hardware für die Installation entspricht, wird eine Warnung ausgegeben. Die Warnung verhindert nicht, dass Sie auf **Weiter** klicken und mit der Installation fortfahren können. Dies kann dennoch die richtige Option für die Installation von Azure ATP in einer kleinen Labtestumgebung sein, für die nicht viel Platz für die Datenspeicherung erforderlich ist. Für Produktionsumgebungen wird dringend empfohlen, mit dem Handbuch zur [Kapazitätsplanung](atp-capacity-planning.md) von Azure ATP zu arbeiten, um sicherzustellen, dass Ihre Domänencontroller oder dedizierten Server den nötigen Anforderungen entsprechen.

1. Geben Sie basierend auf Ihrer Umgebung unter **Configure the sensor** (Sensor konfigurieren) den Installationspfad und den Zugriffsschlüssel ein, die Sie im vorherigen Schritt kopiert haben:

    ![Bild der Azure ATP-Sensorkonfiguration](media/sensor-install-config.png)

    - Installationspfad: An diesem Speicherort wird der eigenständige Azure ATP-Sensor installiert. Dabei handelt es sich standardmäßig um folgenden Pfad: %programfiles%\Azure Advanced Threat Protection sensor. Behalten Sie den Standardwert bei.
    - Zugriffsschlüssel: Dieser wird im vorherigen Schritt vom Azure ATP-Portal abgerufen.

1. Klicken Sie auf **Installieren**. Bei der Installation des Azure ATP-Sensors werden die folgenden Komponenten installiert und konfiguriert:

    - KB 3047154 (nur für Windows Server 2012 R2)

        > [!IMPORTANT]
        >
        > - Installieren Sie KB 3047154 nicht auf einem Virtualisierungshost (der Host, auf dem die Virtualisierung ausgeführt wird; die Ausführung auf einem virtuellen Computer ist möglich). Dies kann dazu führen, dass die Portspiegelung nicht mehr ordnungsgemäß ausgeführt wird.
        > - Wenn Wireshark auf Computer mit dem ATP-Sensor installiert ist, müssen Sie den ATP-Sensor neu starten, nachdem Sie Wireshark ausgeführt haben, da beide die gleichen Treiber verwenden.

    - Azure ATP-Sensordienst und Azure ATP-Sensorupdatedienst
    - Microsoft Visual C++ 2013 Redistributable

## <a name="next-steps"></a>Nächste Schritte

Der Azure ATP-Sensor ist so konzipiert, dass er nur minimale Auswirkung auf Ihre Domänencontrollerressourcen und Netzwerkaktivitäten hat. Informationen zum Erstellen einer Leistungsbewertung finden Sie unter [Planen der Kapazität für Azure ATP](atp-capacity-planning.md).

## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über Azure ATP und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [Azure ATP-Community](https://aka.ms/azureatpcommunity) bei!
