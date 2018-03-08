---
title: Konfigurieren Ihres Proxy oder der Firewall zum Aktivieren der Azure ATP-Kommunikation mit dem Sensor | Microsoft-Dokumentation
description: Beschreibt, wie Sie Ihre Firewall oder den Proxyserver so einrichten, um die Kommunikation zwischen dem Azure ATP-Clouddienst und den Azure ATP-Sensoren zuzulassen.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/3/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 9c173d28-a944-491a-92c1-9690eb06b151
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f077bbd9990affbb6c552c5ad8875fdfebbd70f2
ms.sourcegitcommit: 84556e94a3efdf20ca1ebf89a481550d7f8f0f69
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
*Gilt für: Azure Advanced Threat Protection*



# <a name="configure-your-proxy-to-allow-communication-between-azure-atp-sensors-and-the-azure-atp-cloud-service"></a>Konfigurieren Ihres Proxyservers, um die Kommunikation zwischen Azure ATP-Sensoren und dem Azure ATP-Clouddienst zuzulassen

Für die Kommunikation Ihrer Domänencontroller mit dem Clouddienst müssen Sie in Ihrer Firewall oder auf Ihrem Proxyserver Port 443 für „*.atp.azure.com“ freigeben. Die Konfiguration muss sich auf Computerebene (=Computerkonto) und nicht auf Benutzerkontoebene befinden. Sie können die Konfiguration mithilfe folgender Schritte testen:
 
1.  Bestätigen Sie, dass der **aktuelle Benutzer** Zugriff auf den Prozessorendpunkt mit IE hat, indem Sie vom DC aus folgende URL öffnen: https://triprd1wcuse1sensorapi.eastus.cloudapp.azure.com (für USA). Der Fehler 503 sollte daraufhin angezeigt werden:

 ![Dienst nicht verfügbar.](./media/service-unavailable.png)
 
2.  Wenn der Fehler 503 nicht auftritt, überprüfen Sie die Proxykonfiguration, und versuchen Sie es erneut.

3.  Wenn die Proxykonfiguration für den **CURRENT_USER** funktioniert (wenn also der Fehler 503 angezeigt wird), überprüfen Sie, ob die Proxyeinstellungen für WinInet für das Konto **LOCAL_SYSTEM** aktiviert sind (das Konto wird vom Sensorupdatedienst verwendet), indem Sie den folgenden Befehl in einer Eingabeaufforderung mit erhöhten Rechten ausführen:
 
    reg compare "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" "HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" /v DefaultConnectionSettings

Wenn der Fehler „Fehler: Der angegebene Registrierungsschlüssel bzw. Wert wurde nicht gefunden.“ angezeigt wird, bedeutet dies, dass kein Proxy auf der Ebene **LOCAL_SYSTEM** festgelegt wurde.
 
 ![Lokaler Proxysystemfehler](./media/proxy-local-system-error.png)

Wenn das Ergebnis „ Ergebnis verglichen: unterschiedlich“ angezeigt wird, bedeutet das, dass der Proxy für **LOCAL_SYSTEM** festgelegt ist, er aber nicht der gleiche wie **CURRENT_USER** ist:
 
  ![Proxy-Ergebnis im Vergleich](./media/proxy-result-compared.png)

5.  Wenn **LOCAL_SYSTEM** nicht über dieselben Proxyeinstellungen verfügt (entweder nicht konfiguriert, oder sie unterscheiden sich von **CURRENT_USER**), sollten Sie die Proxyeinstellung aus **CURRENT_USER** in **LOCAL_SYSTEM** kopieren. Stellen Sie sicher, dass Sie diesen Registrierungsschlüssel sichern, bevor Sie ihn bearbeiten:

 Aktueller Benutzerschlüssel: HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings” Local system key: HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings”

 
6.  Schließen Sie die Schritte 4 und 5 für das **Local_Service**-Konto ab (dasselbe wie bei **Local_System**, nur S-1-5-19 anstatt 1-5-18).



## <a name="see-also"></a>Weitere Informationen
- [Configure event forwarding (Konfigurieren der Ereignisweiterleitung)](configure-event-forwarding.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)