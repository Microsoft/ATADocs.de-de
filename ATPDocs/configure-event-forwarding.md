---
title: Konfigurieren der Windows-Ereignisweiterleitung in Microsoft Defender for Identity
description: Hier werden die verfügbaren Optionen zum Konfigurieren der Windows-Ereignisweiterleitung mit Microsoft Defender for Identity beschrieben.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6addbfe12b8c7bf56274cea0e185e2b45d2149aa
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93277326"
---
# <a name="configuring-windows-event-forwarding"></a>Konfigurieren der Windows-Ereignisweiterleitung

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

> [!NOTE]
> Der [!INCLUDE [Product long](includes/product-long.md)]-Sensor liest Ereignisse automatisch lokal, ohne dass die Ereignisweiterleitung konfiguriert werden muss.

Zur Erweiterung der Erkennungsfunktionen benötigt [!INCLUDE [Product short](includes/product-short.md)] die Windows-Ereignisse, die unter [Konfigurieren der Ereignissammlung](configure-windows-event-collection.md#configure-event-collection) aufgeführt sind. Diese Ereignisse können entweder automatisch vom [!INCLUDE [Product short](includes/product-short.md)]-Sensor gelesen oder – falls dieser nicht bereitgestellt wurde – an den eigenständigen [!INCLUDE [Product short](includes/product-short.md)]-Sensor weitergeleitet werden. Dazu gibt es zwei Möglichkeiten: die Konfiguration des eigenständigen [!INCLUDE [Product short](includes/product-short.md)]-Sensors, sodass dieser auf SIEM-Ereignisse lauscht, oder die Konfiguration der Windows-Ereignisweiterleitung.

> [!NOTE]
>
> - Eigenständige [!INCLUDE [Product short](includes/product-short.md)]-Sensoren unterstützen keine Erfassung von Protokolleinträgen für die Ereignisablaufverfolgung für Windows (Event Tracing for Windows, ETW), die Daten für mehrere Erkennungen bereitstellen. Zur vollständigen Erfassung Ihrer Umgebung empfiehlt sich die Bereitstellung des [!INCLUDE [Product short](includes/product-short.md)]-Sensors.
> - Überprüfen Sie, ob der Domänencontroller ordnungsgemäß konfiguriert wurde, um die erforderlichen Ereignisse zu erfassen.

## <a name="wef-configuration-for-product-short-standalone-sensors-with-port-mirroring"></a>WEF-Konfiguration für eigenständige [!INCLUDE [Product short](includes/product-short.md)]-Sensoren mit Portspiegelung

Nachdem Sie die Portspiegelung von den Domänencontrollern zum eigenständigen [!INCLUDE [Product short](includes/product-short.md)]-Sensor konfiguriert haben, führen Sie die folgenden Schritte aus, um die Windows-Ereignisweiterleitung mithilfe der quellinitiierten Konfiguration zu konfigurieren. Dies ist eine Möglichkeit, die Windows-Ereignisweiterleitung zu konfigurieren.

**Schritt 1: Fügen Sie das Netzwerkdienstkonto zur Domäne „Ereignisprotokolllesergruppe“ hinzu.**

In diesem Szenario wird davon ausgegangen, dass der eigenständige [!INCLUDE [Product short](includes/product-short.md)]-Sensor Mitglied der Domäne ist.

1. Öffnen Sie „Active Directory-Benutzer und -Computer“, navigieren Sie zum Ordner **BuiltIn** , und doppelklicken Sie auf **Ereignisprotokollleser**.
1. Wählen Sie **Mitglieder** aus.
1. Wenn **Netzwerkdienst** nicht aufgelistet ist, klicken Sie auf **Hinzufügen** , und geben Sie **Netzwerkdienst** in das Feld **Geben Sie die zu verwendenden Objektnamen ein** ein. Klicken Sie anschließend auf **Namen überprüfen** , und klicken Sie zweimal auf **OK**.

Sie müssen die Domänencontroller neu starten, nachdem Sie den **Netzwerkdienst** der **Ereignisprotokollleser** -Gruppe hinzugefügt haben, damit die Änderungen in Kraft treten können.

**Schritt 2: Erstellen Sie eine Richtlinie auf den Domänencontrollern, um die Einstellung „Ziel-Abonnement-Manager konfigurieren“ festzulegen.**

> [!Note]
> Sie können eine Gruppenrichtlinie für diese Einstellungen erstellen und auf jeden Domänencontroller anwenden, der vom eigenständigen [!INCLUDE [Product short](includes/product-short.md)]-Sensor überwacht wird. Über die folgenden Schritte ändern Sie die lokale Richtlinie des Domänencontrollers.

1. Führen Sie den folgenden Befehl auf jedem Domänencontroller aus: *winrm quickconfig*
1. Geben Sie an einer Eingabeaufforderung *gpedit.msc* ein.
1. Erweitern Sie **Computerkonfiguration > Administrative Vorlagen > Windows-Komponenten > Ereignisweiterleitung**.

    ![Local policy group editor image](media/wef-1-local-group-policy-editor.png)

1. Doppelklicken Sie auf **Ziel-Abonnement-Manager konfigurieren**.

    1. Wählen Sie **Aktiviert** aus.
    1. Klicken Sie unter **Optionen** auf **Anzeigen**.
    1. Geben Sie unter **SubscriptionManagers** folgenden Wert ein, und klicken Sie auf **OK** :  `Server=http\://\<fqdnMicrosoftDefenderForIdentitySensor>:5985/wsman/SubscriptionManager/WEC,Refresh=10` (Beispiel: `Server=http\://atpsensor9.contoso.com:5985/wsman/SubscriptionManager/WEC,Refresh=10`)

    ![Configure target subscription image](media/wef-2-config-target-sub-manager.png)

1. Klicken Sie auf **OK**.
1. Geben Sie von einer Eingabeaufforderung mit erhöhten Rechten aus *gpupdate /force* ein.

**Schritt 3: Führen Sie die folgenden Schritte im eigenständigen [!INCLUDE [Product short](includes/product-short.md)]-Sensor aus**.

1. Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, und geben Sie *wecutil.qc* ein.
1. Öffnen Sie die **Ereignisanzeige**.
1. Klicken Sie mit der rechten Maustaste auf **Abonnements** , und wählen Sie **Abonnement erstellen** aus.

    1. Geben Sie einen Namen und eine Beschreibung für das Abonnement ein.
    1. Bestätigen Sie für **Zielprotokoll** , dass **Weitergeleitete Ereignisse** aktiviert ist. Damit [!INCLUDE [Product short](includes/product-short.md)] die Ereignisse lesen kann, muss das Zielprotokoll **Weitergeleitete Ereignisse** lauten.
    1. Wählen Sie **Quellcomputerinitiiert** aus, und klicken Sie auf **Computergruppen auswählen** aus.
        1. Klicken Sie auf **Domänencomputer hinzufügen**.
        1. Geben Sie den Namen des Domänencontrollers in das Feld **Namen des auszuwählenden Objekts eingeben** ein. Klicken Sie anschließend auf **Namen überprüfen** , und klicken Sie auf **OK**.
        1. Klicken Sie auf **OK**.
        ![Event Viewer image](media/wef-3-event-viewer.png)
    1. Klicken Sie auf **Ereignisse auswählen**.
        1. Klicken Sie auf **Per Protokoll** und wählen Sie **Sicherheit** aus.
        1. Tippen Sie im Feld **Ereignis-IDs ein-/ausschließen** die Ereignisnummer ein, und klicken Sie auf **OK**. Geben Sie wie im folgenden Beispiel 4776 ein:<br/>
        ![Query filter image](media/wef-4-query-filter.png)
    1. Klicken Sie mit der rechten Maustaste auf das erstellte Abonnement, und wählen Sie **Laufzeitstatus** aus, um festzustellen, ob es Probleme mit dem Status gibt.
    1. Überprüfen Sie nach einigen Minuten, ob die zur Weiterleitung festgelegten Ereignisse im eigenständigen [!INCLUDE [Product short](includes/product-short.md)]-Sensor in der Liste der weitergeleiteten Ereignisse angezeigt werden.

Weitere Informationen finden Sie in folgenden Quellen: [Einrichten von Computern zum Weiterleiten und Sammeln von Ereignissen](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc748890(v=ws.11))

## <a name="see-also"></a>Weitere Informationen

- [Installieren von [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
