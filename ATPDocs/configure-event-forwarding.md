---
title: Konfigurieren der Windows-Ereignisweiterleitung in Azure Advanced Threat Protection | Microsoft-Dokumentation
description: Beschreibt die Optionen zur Windows-Ereignisweiterleitung mit Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/29/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 3547519f-8d9c-40a9-8f0e-c7ba21081203
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: c5acf930c53e27818d44cde99ad3aace15073090
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2019
ms.locfileid: "65197214"
---
# <a name="configuring-windows-event-forwarding"></a>Konfigurieren der Windows-Ereignisweiterleitung

> [!NOTE]
> Der Azure ATP-Sensor kann jetzt automatisch Ereignisse lokal lesen, ohne die Ereignisweiterleitung zu konfigurieren.


Um die Erkennungsfunktionalität zu verbessern, benötigt Azure ATP die folgenden Windows-Ereignisse: 4776, 4732, 4733, 4728, 4729, 4756, 4757 und 7045. Diese können entweder automatisch vom Azure ATP-Sensor gelesen oder, falls dieser nicht bereitgestellt wurde, an den eigenständigen Azure ATP-Sensor weitergeleitet werden. Dazu gibt es zwei Möglichkeiten: die Konfiguration des eigenständigen Azure ATP-Sensors, sodass dieser auf SIEM-Ereignisse lauscht, oder die Konfiguration der Windows-Ereignisweiterleitung.

> [!NOTE]
> Überprüfen Sie, ob der Domänencontroller ordnungsgemäß konfiguriert wurde, um die erforderlichen Ereignisse zu erfassen.

### <a name="wef-configuration-for-azure-atp-standalone-sensors-with-port-mirroring"></a>WEF-Konfiguration mit Portspiegelung für den eigenständigen Azure ATP-Sensor

Nachdem Sie die Portspiegelung von den Domänencontrollern zum eigenständigen Azure ATP-Sensor konfiguriert haben, befolgen Sie die folgenden Anweisungen, um die Windows-Ereignisweiterleitung mithilfe der quellinitiierten Konfiguration zu konfigurieren. Dies ist eine Möglichkeit, die Windows-Ereignisweiterleitung zu konfigurieren. 

**Schritt 1: Fügen Sie das Netzwerkdienstkonto zur Domäne „Ereignisprotokolllesergruppe“ hinzu.** 

In diesem Szenario wird davon ausgegangen, dass der eigenständige Azure ATP-Sensor Mitglied der Domäne ist.

1.  Öffnen Sie „Active Directory-Benutzer und -Computer“, navigieren Sie zum Ordner **BuiltIn**, und doppelklicken Sie auf **Ereignisprotokollleser**. 
2.  Wählen Sie **Mitglieder** aus.
3.  Wenn **Netzwerkdienst** nicht aufgelistet ist, klicken Sie auf **Hinzufügen**, und geben Sie **Netzwerkdienst** in das Feld **Geben Sie die zu verwendenden Objektnamen ein** ein. Klicken Sie anschließend auf **Namen überprüfen**, und klicken Sie zweimal auf **OK**. 

Sie müssen die Domänencontroller neu starten, nachdem Sie den **Netzwerkdienst** der **Ereignisprotokollleser**-Gruppe hinzugefügt haben, damit die Änderungen in Kraft treten können.

**Schritt 2: Erstellen Sie eine Richtlinie auf den Domänencontrollern, um die Einstellung „Ziel-Abonnement-Manager konfigurieren“ festzulegen.** 
> [!Note] 
> Sie können eine Gruppenrichtlinie für diese Einstellungen erstellen und die Gruppenrichtlinie auf jeden Domänencontroller anwenden, der vom eigenständigen Azure ATP-Sensor überwacht wird. Über die folgenden Schritte ändern Sie die lokale Richtlinie des Domänencontrollers.     

1. Führen Sie den folgenden Befehl auf jedem Domänencontroller aus: *winrm quickconfig*
2. Geben Sie an einer Eingabeaufforderung *gpedit.msc* ein.
3. Erweitern Sie **Computerkonfiguration > Administrative Vorlagen > Windows-Komponenten > Ereignisweiterleitung**.

   ![Local policy group editor image](media/wef%201%20local%20group%20policy%20editor.png)

4. Doppelklicken Sie auf **Ziel-Abonnement-Manager konfigurieren**.
   
   1.  Wählen Sie **Aktiviert** aus.
   2.  Klicken Sie unter **Optionen** auf **Anzeigen**.
   3.  Geben Sie unter **SubscriptionManagers** folgenden Wert ein, und klicken Sie auf **OK**: Server= http\://\<fqdnATPSensor>:5985/wsman/SubscriptionManager/WEC,Refresh=10` (z. B.: Server=http\://atpsensor9.contoso.com:5985/wsman/SubscriptionManager/WEC,Refresh=10)
    
   ![Configure target subscription image](media/wef%202%20config%20target%20sub%20manager.png)
    
5. Klicken Sie auf **OK**.
6. Geben Sie von einer Eingabeaufforderung mit erhöhten Rechten aus *gpupdate /force* ein. 

**Schritt 3: Führen Sie die folgenden Schritte für den eigenständigen Azure ATP-Sensor aus** 

1. Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, und geben Sie *wecutil.qc* ein.
2. Öffnen Sie die **Ereignisanzeige**. 
3. Klicken Sie mit der rechten Maustaste auf **Abonnements**, und wählen Sie **Abonnement erstellen** aus. 
    
    1. Geben Sie einen Namen und eine Beschreibung für das Abonnement ein. 
    2. Bestätigen Sie für **Zielprotokoll**, dass **Weitergeleitete Ereignisse** aktiviert ist. Damit Azure ATP die Ereignisse lesen kann, muss das Zielprotokoll unter **Weitergeleitete Ereignisse** zu finden sein. 
    3. Wählen Sie **Quellcomputerinitiiert** aus, und klicken Sie auf **Computergruppen auswählen** aus.
        1. Klicken Sie auf **Domänencomputer hinzufügen**.
        2. Geben Sie den Namen des Domänencontrollers in das Feld **Namen des auszuwählenden Objekts eingeben** ein. Klicken Sie anschließend auf **Namen überprüfen**, und klicken Sie auf **OK**. 
        3. Klicken Sie auf **OK**.
        ![Event Viewer image](media/wef3%20event%20viewer.png)     
    4. Klicken Sie auf **Ereignisse auswählen**.
        1. Klicken Sie auf **Per Protokoll** und wählen Sie **Sicherheit** aus.
        2. Tippen Sie im Feld **Ereignis-IDs ein-/ausschließen** die Ereignisnummer ein, und klicken Sie auf **OK**. Geben Sie wie im folgenden Beispiel 4776 ein:<br/>
        ![Query filter image](media/wef-4-query-filter.png)
    5. Klicken Sie mit der rechten Maustaste auf das erstellte Abonnement, und wählen Sie **Laufzeitstatus** aus, um festzustellen, ob es Probleme mit dem Status gibt. 
    6. Überprüfen Sie nach einigen Minuten, ob die festgelegten Ereignisse im eigenständigen Azure ATP-Sensor unter „Weitergeleitete Ereignisse“ angezeigt werden.


Weitere Informationen finden Sie in folgenden Quellen: [Einrichten von Computern zum Weiterleiten und Sammeln von Ereignissen](https://technet.microsoft.com/library/cc748890)

## <a name="see-also"></a>Weitere Informationen

- [Install Azure ATP (Installieren von Azure ATP)](install-atp-step1.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
