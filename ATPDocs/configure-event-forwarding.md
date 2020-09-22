---
title: Konfigurieren der Windows-Ereignisweiterleitung in Azure Advanced Threat Protection
description: Beschreibt die Optionen zur Windows-Ereignisweiterleitung mit Azure ATP
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/18/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 3547519f-8d9c-40a9-8f0e-c7ba21081203
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 82d45c25ccb36e2ec4763cfec13a4f03d8a26575
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2020
ms.locfileid: "90910521"
---
# <a name="configuring-windows-event-forwarding"></a>Konfigurieren der Windows-Ereignisweiterleitung

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

> [!NOTE]
> Der Azure ATP-Sensor kann jetzt automatisch Ereignisse lokal lesen, ohne die Ereignisweiterleitung zu konfigurieren.

Damit die Erkennungsfunktionalität verbessert werden kann, benötigt Azure ATP die Windows-Ereignisse, die unter [Konfigurieren der Ereignissammlung](configure-windows-event-collection.md#configure-event-collection) aufgeführt sind. Diese können entweder automatisch vom Azure ATP-Sensor gelesen oder, falls dieser nicht bereitgestellt wurde, an den eigenständigen Azure ATP-Sensor weitergeleitet werden. Dazu gibt es zwei Möglichkeiten: die Konfiguration des eigenständigen Azure ATP-Sensors, sodass dieser auf SIEM-Ereignisse lauscht, oder die Konfiguration der Windows-Ereignisweiterleitung.

> [!NOTE]
>
> - Eigenständige Azure ATP-Server unterstützen nicht die Erstellung von Protokolleinträgen für Ereignisablaufverfolgung für Windows (Event Tracing for Windows, ETW), die Daten für mehrere Erkennungen bereitstellen. Zur vollständigen Abdeckung Ihrer Umgebung empfiehlt es sich, den Azure ATP-Sensor bereitzustellen.
> - Überprüfen Sie, ob der Domänencontroller ordnungsgemäß konfiguriert wurde, um die erforderlichen Ereignisse zu erfassen.

## <a name="wef-configuration-for-azure-atp-standalone-sensors-with-port-mirroring"></a>WEF-Konfiguration mit Portspiegelung für den eigenständigen Azure ATP-Sensor

Nachdem Sie die Portspiegelung von den Domänencontrollern zum eigenständigen Azure ATP-Sensor konfiguriert haben, befolgen Sie die folgenden Anweisungen, um die Windows-Ereignisweiterleitung mithilfe der quellinitiierten Konfiguration zu konfigurieren. Dies ist eine Möglichkeit, die Windows-Ereignisweiterleitung zu konfigurieren.

**Schritt 1: Fügen Sie das Netzwerkdienstkonto zur Domäne „Ereignisprotokolllesergruppe“ hinzu.**

In diesem Szenario wird davon ausgegangen, dass der eigenständige Azure ATP-Sensor Mitglied der Domäne ist.

1. Öffnen Sie „Active Directory-Benutzer und -Computer“, navigieren Sie zum Ordner **BuiltIn**, und doppelklicken Sie auf **Ereignisprotokollleser**.
1. Wählen Sie **Mitglieder** aus.
1. Wenn **Netzwerkdienst** nicht aufgelistet ist, klicken Sie auf **Hinzufügen**, und geben Sie **Netzwerkdienst** in das Feld **Geben Sie die zu verwendenden Objektnamen ein** ein. Klicken Sie anschließend auf **Namen überprüfen**, und klicken Sie zweimal auf **OK**.

Sie müssen die Domänencontroller neu starten, nachdem Sie den **Netzwerkdienst** der **Ereignisprotokollleser**-Gruppe hinzugefügt haben, damit die Änderungen in Kraft treten können.

**Schritt 2: Erstellen Sie eine Richtlinie auf den Domänencontrollern, um die Einstellung „Ziel-Abonnement-Manager konfigurieren“ festzulegen.**

> [!Note]
> Sie können eine Gruppenrichtlinie für diese Einstellungen erstellen und die Gruppenrichtlinie auf jeden Domänencontroller anwenden, der vom eigenständigen Azure ATP-Sensor überwacht wird. Über die folgenden Schritte ändern Sie die lokale Richtlinie des Domänencontrollers.

1. Führen Sie den folgenden Befehl auf jedem Domänencontroller aus: *winrm quickconfig*
1. Geben Sie an einer Eingabeaufforderung *gpedit.msc* ein.
1. Erweitern Sie **Computerkonfiguration > Administrative Vorlagen > Windows-Komponenten > Ereignisweiterleitung**.

    ![Local policy group editor image](media/wef%201%20local%20group%20policy%20editor.png)

1. Doppelklicken Sie auf **Ziel-Abonnement-Manager konfigurieren**.

    1. Wählen Sie **Aktiviert** aus.
    1. Klicken Sie unter **Optionen** auf **Anzeigen**.
    1. Geben Sie unter **SubscriptionManagers** folgenden Wert ein, und klicken Sie auf **OK**:  Server= http\://\<fqdnATPSensor>:5985/wsman/SubscriptionManager/WEC,Refresh=10` (Zum Beispiel: Server=http\://atpsensor9.contoso.com:5985/wsman/SubscriptionManager/WEC,Refresh=10)

    ![Configure target subscription image](media/wef%202%20config%20target%20sub%20manager.png)

1. Klicken Sie auf **OK**.
1. Geben Sie von einer Eingabeaufforderung mit erhöhten Rechten aus *gpupdate /force* ein.

**Schritt 3: Führen Sie die folgenden Schritte für den eigenständigen Azure ATP-Sensor aus**

1. Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, und geben Sie *wecutil.qc* ein.
1. Öffnen Sie die **Ereignisanzeige**.
1. Klicken Sie mit der rechten Maustaste auf **Abonnements**, und wählen Sie **Abonnement erstellen** aus.

    1. Geben Sie einen Namen und eine Beschreibung für das Abonnement ein.
    1. Bestätigen Sie für **Zielprotokoll**, dass **Weitergeleitete Ereignisse** aktiviert ist. Damit Azure ATP die Ereignisse lesen kann, muss das Zielprotokoll unter **Weitergeleitete Ereignisse** zu finden sein.
    1. Wählen Sie **Quellcomputerinitiiert** aus, und klicken Sie auf **Computergruppen auswählen** aus.
        1. Klicken Sie auf **Domänencomputer hinzufügen**.
        1. Geben Sie den Namen des Domänencontrollers in das Feld **Namen des auszuwählenden Objekts eingeben** ein. Klicken Sie anschließend auf **Namen überprüfen**, und klicken Sie auf **OK**.
        1. Klicken Sie auf **OK**.
        ![Event Viewer image](media/wef3%20event%20viewer.png)
    1. Klicken Sie auf **Ereignisse auswählen**.
        1. Klicken Sie auf **Per Protokoll** und wählen Sie **Sicherheit** aus.
        1. Tippen Sie im Feld **Ereignis-IDs ein-/ausschließen** die Ereignisnummer ein, und klicken Sie auf **OK**. Geben Sie wie im folgenden Beispiel 4776 ein:<br/>
        ![Query filter image](media/wef-4-query-filter.png)
    1. Klicken Sie mit der rechten Maustaste auf das erstellte Abonnement, und wählen Sie **Laufzeitstatus** aus, um festzustellen, ob es Probleme mit dem Status gibt.
    1. Überprüfen Sie nach einigen Minuten, ob die festgelegten Ereignisse im eigenständigen Azure ATP-Sensor unter „Weitergeleitete Ereignisse“ angezeigt werden.

Weitere Informationen finden Sie in folgenden Quellen: [Einrichten von Computern zum Weiterleiten und Sammeln von Ereignissen](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc748890(v=ws.11))

## <a name="see-also"></a>Weitere Informationen

- [Install Azure ATP (Installieren von Azure ATP)](install-step1.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)