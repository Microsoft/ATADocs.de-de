---
title: Konfigurieren der Windows-Ereignis Weiterleitung in Advanced Threat Analytics
description: Beschreibt die Optionen zur Windows-Ereignisweiterleitung mit ATA
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: f833b799f14dec5b1ae1a7cf18bd9813f9912cd9
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2020
ms.locfileid: "94690838"
---
# <a name="configuring-windows-event-forwarding"></a>Konfigurieren der Windows-Ereignisweiterleitung

[!INCLUDE [Banner for top of topics](includes/banner.md)]

> [!NOTE]
> Für die ATA-Version 1.8 und höher ist die Konfiguration der Ereignissammlung nicht länger für ATA-Lightweight-Gateways erforderlich. Das ATA-Lightweight-Gateway liest jetzt Ereignisse lokal, ohne die Ereignisweiterleitung zu konfigurieren.

Um die Erkennungsfunktionalität zu verbessern, benötigt ATA die folgenden Windows-Ereignisse:4776, 4732, 4733, 4728, 4729, 4756, 4757, 7045. Diese können entweder automatisch vom ATA-Lightweight-Gateway gelesen oder, falls das ATA-Lightweight-Gateway nicht bereitgestellt wurde, an das ATA-Gateway weitergeleitet werden. Dazu gibt es zwei Möglichkeiten: Konfigurieren des ATA-Gateways, sodass es auf SIEM-Ereignisse lauscht, oder Konfigurieren der Windows-Ereignisweiterleitung.

> [!NOTE]
> Bei Verwendung von Server Core kann [wecutil](/windows-server/administration/windows-commands/wecutil) zum Erstellen und Verwalten von Abonnements für Ereignisse verwendet werden, die von Remotecomputern weitergeleitet werden.

### <a name="wef-configuration-for-ata-gateways-with-port-mirroring"></a>Konfiguration der Windows-Ereignisweiterleitung für ATA-Gateways mit Portspiegelung

Nachdem Sie die Portspiegelung von den Domänencontrollern zum ATA-Gateway konfiguriert haben, verwenden Sie die folgenden Anweisungen, um die Windows-Ereignisweiterleitung mithilfe der quellinitiierten Konfiguration zu konfigurieren. Dies ist eine Möglichkeit, die Windows-Ereignisweiterleitung zu konfigurieren. 

**Schritt 1: Fügen Sie das Netzwerkdienstkonto zur Domäne „Ereignisprotokolllesergruppe“ hinzu.** 

In diesem Szenario gehen wir davon aus, dass das ATA-Gateway Mitglied der Domäne ist.

1. Öffnen Sie „Active Directory-Benutzer und -Computer“, navigieren Sie zum Ordner **BuiltIn**, und doppelklicken Sie auf **Ereignisprotokollleser**. 
1. Wählen Sie **Mitglieder** aus.
1. Wenn **Netzwerkdienst** nicht aufgelistet ist, klicken Sie auf **Hinzufügen**, und geben Sie **Netzwerkdienst** in das Feld **Geben Sie die zu verwendenden Objektnamen ein** ein. Klicken Sie anschließend auf **Namen überprüfen**, und klicken Sie zweimal auf **OK**. 

Sie müssen die Domänencontroller neu starten, nachdem Sie den **Netzwerkdienst** der **Ereignisprotokollleser**-Gruppe hinzugefügt haben, damit die Änderungen in Kraft treten können.

**Schritt 2: Erstellen Sie eine Richtlinie auf den Domänencontrollern, um die Einstellung „Ziel-Abonnement-Manager konfigurieren“ festzulegen.** 
> [!Note] 
> Sie können eine Gruppenrichtlinie für diese Einstellungen erstellen und die Gruppenrichtlinie auf jeden Domänencontroller anwenden, der vom ATA-Gateway überwacht wird. Die folgenden Schritte ändern die lokale Richtlinie des Domänencontrollers.  

1. Führen Sie den folgenden Befehl auf jedem Domänencontroller aus: *winrm quickconfig*
1. Geben Sie an einer Eingabeaufforderung *gpedit.msc* ein.
1. Erweitern Sie **Computerkonfiguration > Administrative Vorlagen > Windows-Komponenten > Ereignisweiterleitung**.

    ![Local policy group editor image](media/wef%201%20local%20group%20policy%20editor.png)

1. Doppelklicken Sie auf **Ziel-Abonnement-Manager konfigurieren**.
   
   1.  Wählen Sie **Aktiviert** aus.
   2.  Klicken Sie unter **Optionen** auf **Anzeigen**.

   3.  Geben Sie unter **SubscriptionManagers** folgenden Wert ein, und klicken Sie auf **OK**: *Server=http://<fqdnATAGateway>:5985/wsman/SubscriptionManager/WEC,Refresh=10* 
      
        *(Beispiel: Server=`http://atagateway9.contoso.com:5985/wsman/SubscriptionManager/WEC,Refresh=10`)*
      
        ![Configure target subscription image](media/wef%202%20config%20target%20sub%20manager.png)
      
   4.  Klicken Sie auf **OK**.
   5.  Geben Sie von einer Eingabeaufforderung mit erhöhten Rechten aus *gpupdate /force* ein. 

**Schritt 3: Führen Sie die folgenden Schritte auf dem ATA-Gateway aus.** 

1. Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, und geben Sie *wecutil.qc* ein.
1. Öffnen Sie die **Ereignisanzeige**. 
1. Klicken Sie mit der rechten Maustaste auf **Abonnements**, und wählen Sie **Abonnement erstellen** aus. 

    1. Geben Sie einen Namen und eine Beschreibung für das Abonnement ein. 
    2. Bestätigen Sie für **Zielprotokoll**, dass **Weitergeleitete Ereignisse** aktiviert ist. Damit ATA die Ereignisse lesen kann, muss das Ziel Protokoll **Weitergeleitete Ereignisse** sein. 
    3. Wählen Sie **Quellcomputerinitiiert** aus, und klicken Sie auf **Computergruppen auswählen** aus.
        1. Klicken Sie auf **Domänencomputer hinzufügen**.
        2. Geben Sie den Namen des Domänencontrollers in das Feld **Namen des auszuwählenden Objekts eingeben** ein. Klicken Sie anschließend auf **Namen überprüfen**, und klicken Sie auf **OK**.  
          ![Event Viewer image](media/wef3%20event%20viewer.png)  
        3. Klicken Sie auf **OK**.
    4. Klicken Sie auf **Ereignisse auswählen**.
        1. Klicken Sie auf **Per Protokoll** und wählen Sie **Sicherheit** aus.
        2. Tippen Sie im Feld **Ereignis-IDs ein-/ausschließen** die Ereignisnummer ein, und klicken Sie auf **OK**. Geben Sie wie im folgenden Beispiel 4776 ein.

        ![Query filter image](media/wef%204%20query%20filter.png)

    5. Klicken Sie mit der rechten Maustaste auf das erstellte Abonnement, und wählen Sie **Laufzeitstatus** aus, um festzustellen, ob es Probleme mit dem Status gibt. 
    6. Überprüfen Sie nach einigen Minuten, ob die festgelegten Ereignisse im ATA-Gateway in „Weitergeleitete Ereignisse“ angezeigt wird.


Weitere Informationen finden Sie in folgenden Quellen: [Einrichten von Computern zum Weiterleiten und Sammeln von Ereignissen](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc748890(v=ws.11))

## <a name="see-also"></a>Weitere Informationen
- [Installieren von ATA](install-ata-step1.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)