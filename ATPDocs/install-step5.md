---
title: Konfigurieren von Microsoft Defender für Identitäts Sensor Einstellungen konzeptionell
description: In Schritt 5 der Installation von Microsoft Defender für Identity können Sie die Einstellungen für den eigenständigen Defender für Identity-Sensor konfigurieren.
ms.date: 09/15/2019
ms.topic: how-to
ms.openlocfilehash: 42dc42caad1b76cf706cf85d34fd60f5c7a52756
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/16/2021
ms.locfileid: "100534013"
---
# <a name="configure-microsoft-defender-for-identity-sensor-settings"></a>Konfigurieren von Microsoft Defender für Identitäts Sensor Einstellungen

In diesem Artikel erfahren Sie, wie Sie Sensor Einstellungen ordnungsgemäß konfigurieren [!INCLUDE [Product long](includes/product-long.md)] , damit Sie mit dem Anzeigen von Daten beginnen können. Sie müssen zusätzliche Konfiguration und Integration durchführen, um [!INCLUDE [Product short](includes/product-short.md)] die vollständigen Funktionen von nutzen zu können.

## <a name="prerequisites"></a>Voraussetzungen

- Eine [[!INCLUDE [Product short](includes/product-short.md)]-Instanz](install-step1.md), die [mit Active Directory verbunden](install-step2.md) ist
- Eine heruntergeladene Kopie des [[!INCLUDE [Product short](includes/product-short.md)]-Sensorsetuppakets](install-step3.md) und den Zugriffsschlüssel

## <a name="configure-sensor-settings"></a>Konfigurieren von Sensoreinstellungen

[!INCLUDE [Product short](includes/product-short.md)]Führen Sie nach der Installation des Sensors die folgenden Schritte aus, um die [!INCLUDE [Product short](includes/product-short.md)] Sensor Einstellungen zu konfigurieren.

1. Klicken Sie auf **starten** , um den Browser zu öffnen und sich beim [!INCLUDE [Product short](includes/product-short.md)] Portal anzumelden.

1. Wechseln [!INCLUDE [Product short](includes/product-short.md)] Sie im Portal zu **Konfiguration** , und wählen Sie unter **System** die Option **Sensoren** aus.

    ![Sensorseite](media/sensor-config.png)

1. Klicken Sie auf den Sensor, den Sie konfigurieren möchten, und geben Sie die folgenden Informationen ein:

    ![Konfigurieren von Sensoreinstellungen](media/sensor-config-2.png)

    - **Beschreibung**: Geben Sie eine Beschreibung für den [!INCLUDE [Product short](includes/product-short.md)] Sensor ein (optional).
    - **Domänen Controller (FQDN)** (erforderlich für den [!INCLUDE [Product short](includes/product-short.md)] eigenständigen Sensor, dies kann für den Sensor nicht geändert werden [!INCLUDE [Product short](includes/product-short.md)] ): Geben Sie den vollständigen FQDN Ihres Domänen Controllers ein, und klicken Sie auf das Pluszeichen, um ihn der Liste hinzuzufügen. z. B. **dc01.contoso.com**.

    Die folgenden Informationen gelten für die Server, die Sie in der Liste **Domänencontroller** eingeben.
    - Alle Domänen Controller, deren Datenverkehr über die Port Spiegelung durch den [!INCLUDE [Product short](includes/product-short.md)] eigenständigen Sensor überwacht wird, müssen in der Liste **Domänen Controller** aufgeführt sein. Wenn ein Domänencontroller nicht in der Liste **Domänencontroller** aufgeführt wird, werden verdächtige Aktivitäten möglicherweise nicht wie erwartet erkannt.
    - Mindestens ein Domänencontroller in der Liste sollte ein globaler Katalog sein. Dadurch können [!INCLUDE [Product short](includes/product-short.md)] Computer-und Benutzer Objekte in anderen Domänen in der Gesamtstruktur aufgelöst werden.

    - **Netzwerkadapter für Erfassung** (erforderlich):

    - Für [!INCLUDE [Product short](includes/product-short.md)] Sensoren: alle Netzwerkadapter, die für die Kommunikation mit anderen Computern in Ihrer Organisation verwendet werden.
    - [!INCLUDE [Product short](includes/product-short.md)]Wählen Sie für eigenständigen Sensor auf einem dedizierten Server die Netzwerkadapter aus, die als Ziel Spiegelungs Port konfiguriert sind. Diese Netzwerkadapter empfangen den Datenverkehr des gespiegelten Domänencontrollers.

1. Klicken Sie auf **Speichern**.

## <a name="validate-installations"></a>Überprüfen von Installationen

[!INCLUDE [Product short](includes/product-short.md)]Überprüfen Sie Folgendes, um zu überprüfen, ob der Sensor erfolgreich bereitgestellt wurde:

1. Überprüfen Sie, ob der Dienst mit dem Namen **Azure Advanced Threat Protection-Sensor** ausgeführt wird. Nachdem Sie die [!INCLUDE [Product short](includes/product-short.md)] Sensor Einstellungen gespeichert haben, kann es einige Sekunden dauern, bis der Dienst gestartet wird.

1. Wenn der Dienst nicht gestartet wird, überprüfen Sie die Datei „Microsoft.Tri.sensor-Errors.log“ im Standardordner „%programfiles%\Azure Advanced Threat Protection sensor\Version X\Logs“.

    >[!NOTE]
    > Die Version der [!INCLUDE [Product short](includes/product-short.md)] Updates, um die neueste Version zu überprüfen, wechseln Sie im [!INCLUDE [Product short](includes/product-short.md)] Portal zu **Konfiguration** und dann **zu**.

1. Wechseln Sie zu Ihrer [!INCLUDE [Product short](includes/product-short.md)] Instanz-URL. [!INCLUDE [Product short](includes/product-short.md)]Suchen Sie im Portal nach etwas in der Suchleiste, z. b. in einem Benutzer oder einer Gruppe in Ihrer Domäne.

1. Überprüfen [!INCLUDE [Product short](includes/product-short.md)] Sie die Konnektivität auf einem beliebigen Domänen Gerät mithilfe der folgenden Schritte:
    1. Öffnen Sie eine Eingabeaufforderung.
    1. Geben Sie `nslookup` ein.
    1. Geben Sie **Server** und dann den FQDN oder die IP-Adresse des Domänen Controllers ein, auf dem der [!INCLUDE [Product short](includes/product-short.md)] Sensor installiert ist. Beispiel: `server contosodc.contoso.azure`
        - Stellen Sie sicher, dass Sie "ContosoDC. contoso. Azure" und "contoso. Azure" durch den FQDN Ihres [!INCLUDE [Product short](includes/product-short.md)] Sensors bzw. Domänen namens ersetzen.
    1. Geben Sie `ls -d contoso.azure` ein.
    1. Wiederholen Sie die Schritte 3 und 4 für jeden Sensor, den Sie testen möchten.
    1. Öffnen Sie in der- [!INCLUDE [Product short](includes/product-short.md)] Konsole das Entitäts Profil für den Computer, auf dem der Konnektivitätstest ausgeführt wurde.
    1. Überprüfen Sie die zugehörige logische Aktivität, und bestätigen Sie die Konnektivität.

    > [!NOTE]
    >Wenn der zu testende Domänencontroller der erste bereitgestellte Sensor ist, warten Sie mindestens 15 Minuten, damit das Datenbank-Back-End die erste Bereitstellung der erforderlichen Microservices abschließen kann. Versuchen Sie erst anschließend, die zugehörige logische Aktivität für diesen Domänencontroller zu überprüfen.

## <a name="next-steps"></a>Nächste Schritte

- [Proxykonfiguration](configure-proxy.md)
- [Überprüfung der erweiterten Überwachungsrichtlinie von Azure ATP](configure-windows-event-collection.md)
- [Konfigurieren von [!INCLUDE [Product short](includes/product-short.md)] für das Ausführen von Remoteaufrufen an SAM](install-step8-samr.md)

## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über [!INCLUDE [Product short](includes/product-short.md)] und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [[!INCLUDE [Product short](includes/product-short.md)]Community](https://aka.ms/MDIcommunity) bei.
