---
title: Installieren von Advanced Threat Analytics (Schritt 8)
description: Im letzten Schritt der Installation von ATA konfigurieren Sie den Honeytoken-Benutzer.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 6/14/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: cd3906dca902416a096106808036864422f82548
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2020
ms.locfileid: "94690600"
---
# <a name="install-ata---step-8"></a>Installieren von ATA – Schritt 8

[!INCLUDE [Banner for top of topics](includes/banner.md)]

> [!div class="step-by-step"]
> [«Schritt 7](vpn-integration-install-step.md) 
>  [Schritt 9»](install-ata-step9-samr.md)

## <a name="step-8-configure-ip-address-exclusions-and-honeytoken-user"></a>Schritt 8: Konfigurieren von IP-Adressausschlüssen und Honeytoken-Benutzern

ATA ermöglicht den Ausschluss bestimmter IP-Adressen oder Benutzer aus einer Reihe von Erkennungen.

Angenommen, ein **DNS-Reconnaissance-Ausschluss** könnte eine Sicherheitsprüfung sein, die DNS als Überprüfungsmechanismus verwendet. Der Ausschluss hilft ATA, Überprüfungen dieser Art zu ignorieren. Ein Beispiel für einen *Pass-the-Ticket*-Ausschluss ist ein NAT-Gerät.

ATA ermöglicht auch die Konfiguration eines Honeytoken-Benutzers, der als ein Trap für böswillige Teilnehmer verwendet wird – jede Authentifizierung die Ihrem (normalerweise ruhenden) Konto zugeordnet ist, löst eine Warnung aus.

Führen Sie zur Konfiguration die folgenden Schritte aus:

1. Klicken Sie in der ATA-Konsole auf das Symbol „Einstellungen“, und wählen Sie **Konfiguration** aus.

    ![ATA-Konfigurationseinstellungen](media/ATA-config-icon.png)

1. Klicken Sie unter **Erkennung** auf **Entitätstag**.

1. Geben Sie unter **Honeytoken-Konto** den Honeytoken-Kontonamen an. Das Honeytoken-Kontenfeld kann gesucht werden und zeigt automatisch Entitäten in Ihrem Netzwerk an.

    ![Screenshot mit honeytoken-Kontonamen Eintrag](media/honeytoken.png)

1. Klicken Sie auf **Ausschlüsse**. Geben Sie für jeden Bedrohungstyp ein Benutzerkonto oder eine IP-Adresse ein, das/die von der Erkennung dieser Bedrohungen ausgeschlossen werden soll, und klicken Sie auf das *Pluszeichen*. Das Feld **Entität hinzufügen** (Benutzer oder Computer) kann durchsucht werden und wird automatisch mit Entitäten in Ihrem Netzwerk gefüllt. Weitere Informationen finden Sie unter [Ausschließen von Entitäten von der Erkennung](excluding-entities-from-detections.md).

    ![Screenshot, der den Ausschluss von Entitäten von der Erkennung anzeigt](media/exclusions.png)

1. Klicken Sie auf **Speichern**.

Damit haben Sie Microsoft Advanced Threat Analytics erfolgreich bereitgestellt.

Sie können nun die Angriffszeitleiste auf erkannte verdächtige Aktivitäten prüfen sowie nach Benutzern oder Computern suchen und deren Profile anzeigen.

ATA startet sofort die automatische Überprüfung auf verdächtige Aktivitäten. Einige Aktivitäten, beispielsweise bestimmtes verdächtiges Verhalten, ist erst wieder verfügbar, nachdem ATA Verhaltensprofile erstellen konnte (nach mindestens drei Wochen).

Sie können sich die [Sammlung von Angriffssimulationsszenarios von Advanced Threat Analytics](/enterprise-mobility-security/solutions/ata-attack-simulation-playbook) ansehen, um zu überprüfen, ob ATA ordnungsgemäß funktioniert und Sicherheitslücken in Ihrem Netzwerk erfasst.

> [!div class="step-by-step"]
> [«Schritt 7](vpn-integration-install-step.md) 
>  [Schritt 9»](install-ata-step9-samr.md)

## <a name="related-videos"></a>Verwandte Videos

- [Übersicht über die ATA-Bereitstellung](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Auswählen des richtigen ATA-Gatewaytyps](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)

## <a name="see-also"></a>Weitere Informationen

- [Handbuch für die ATA POC-Bereitstellung](https://aka.ms/atapoc)
- [Tool zur Bemessung von ATA-Gateways](https://aka.ms/atasizingtool)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [ATA-Voraussetzungen](ata-prerequisites.md)
