---
title: "Installieren von Advanced Threat Analytics – Schritt 7 | Microsoft-Dokumentation"
description: Im letzten Schritt der Installation von ATA konfigurieren Sie den Honeytoken-Benutzer.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 09/03/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: f5cb87148741c92dc7832da16cc37a749fa72fae
ms.sourcegitcommit: 654500928025e3cb127e095c17cc1d6444defd3a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/03/2017
---
*Gilt für: Advanced Threat Analytics Version 1.8*



# <a name="install-ata---step-7"></a>Installieren von ATA – Schritt 7

>[!div class="step-by-step"]
[« Schritt 6 ](install-ata-step6.md)

## <a name="step-7-configure-ip-address-exclusions-and-honeytoken-user"></a>Schritt 7: Konfigurieren von IP-Adressausschlüssen und Honeytoken-Benutzern
ATA ermöglicht den Ausschluss bestimmter IP-Adressen oder Benutzer aus einer Reihe von Erkennungen. 

Angenommen, ein **DNS-Reconnaissance-Ausschluss** könnte eine Sicherheitsprüfung sein, die DNS als Überprüfungsmechanismus verwendet. Der Ausschluss hilft ATA, Überprüfungen dieser Art zu ignorieren. Ein Beispiel für einen *Pass-the-Ticket*-Ausschluss ist ein NAT-Gerät.    

ATA ermöglicht auch die Konfiguration eines Honeytoken-Benutzers, der als ein Trap für böswillige Teilnehmer verwendet wird – jede Authentifizierung die Ihrem (normalerweise ruhenden) Konto zugeordnet ist, löst eine Warnung aus.

Führen Sie folgende Schritte durch, um dies zu konfigurieren:

1.  Klicken Sie in der ATA-Konsole auf das Symbol „Einstellungen“, und wählen Sie **Konfiguration** aus.

    ![ATA-Konfigurationseinstellungen](media/ATA-config-icon.png)

2.  Klicken Sie unter **Erkennung** auf **Allgemein**.

2. Geben Sie unter **Honeytoken-Konto** den Honeytoken-Kontonamen an. Das Honeytoken-Kontenfeld kann gesucht werden und zeigt automatisch Entitäten in Ihrem Netzwerk an.

   ![Honeytoken](media/honeytoken.png)

3. Klicken Sie auf **Ausschlüsse**. Geben Sie für jeden Bedrohungstyp ein Benutzerkonto oder eine IP-Adresse ein, das/die von der Erkennung dieser Bedrohungen ausgeschlossen werden soll, und klicken Sie auf das *Pluszeichen*. Das Feld **Entität hinzufügen** (Benutzer oder Computer) kann durchsucht werden und wird automatisch mit Entitäten in Ihrem Netzwerk gefüllt. Weitere Informationen finden Sie unter [Ausschließen von Entitäten von der Erkennung](excluding-entities-from-detections.md).

   ![Ausschlüsse](media/exclusions.png)

4.  Klicken Sie auf **Speichern**.


Damit haben Sie Microsoft Advanced Threat Analytics erfolgreich bereitgestellt.

Sie können nun die Angriffszeitleiste auf erkannte verdächtige Aktivitäten prüfen sowie nach Benutzern oder Computern suchen und deren Profile anzeigen.

ATA startet sofort die automatische Überprüfung auf verdächtige Aktivitäten. Einige Aktivitäten, beispielsweise bestimmtes verdächtiges Verhalten, ist erst wieder verfügbar, nachdem ATA Verhaltensprofile erstellen konnte (nach mindestens drei Wochen).

Sie können sich die [Sammlung von Angriffssimulationsszenarios von Advanced Threat Analytics](https://docs.microsoft.com/enterprise-mobility-security/solutions/ata-attack-simulation-playbook) ansehen, um zu überprüfen, ob ATA ordnungsgemäß funktioniert und Sicherheitslücken in Ihrem Netzwerk erfasst.


>[!div class="step-by-step"]
[« Schritt 6 ](install-ata-step6.md)



## <a name="related-videos"></a>Verwandte Videos
- [Auswählen des richtigen ATA-Gatewaytyps](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Weitere Informationen
- [Handbuch für die ATA POC-Bereitstellung](http://aka.ms/atapoc)
- [Tool zur Bemessung von ATA-Gateways](http://aka.ms/atasizingtool)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Voraussetzungen für ATA](ata-prerequisites.md)

