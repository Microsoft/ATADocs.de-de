---
title: Problembehandlung bei Advanced Threat Analytics mithilfe der Datenbank
description: Beschreibt die Verwendung der ATA-Datenbank zum Behandeln von Problemen.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 377a3c81-5c1d-486f-8942-85249aacf560
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 6178593296c56bbe622aa9ac7763ffab50fbd66c
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2020
ms.locfileid: "94690141"
---
# <a name="troubleshooting-ata-using-the-ata-database"></a>Behandeln von Problemen mit ATA mithilfe der ATA-Datenbank

[!INCLUDE [Banner for top of topics](includes/banner.md)]

ATA verwendet MongoDB als Datenbank.
Die Interaktion mit der Datenbank ist über die Standardbefehlszeile möglich oder über ein Benutzeroberflächentool, mit dem Sie erweiterte Aufgaben und Problembehandlung ausführen können.

## <a name="interacting-with-the-database"></a>Interagieren mit der Datenbank
Die Datenbank lässt sich standardmäßig und am einfachsten über die Mongo-Shell abfragen:

1. Öffnen Sie ein Befehlszeilenfenster, und ändern Sie den Pfad in den MongoDB-Ordner „bin“. Der Standardpfad lautet **C:\Programme\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**.

1. Führen Sie `mongo.exe ATA` aus. Geben Sie „ATA“ in Großbuchstaben ein.

> [!div class="mx-tableFixed"]
> 
> |So wird es gemacht|Syntax|Notizen|
> |-------------|----------|---------|
> |Suchen nach Sammlungen in der Datenbank.|`show collections`|Hilfreich als End-to-End-Test, um zu überprüfen, ob Datenverkehr in die Datenbank geschrieben und das Ereignis 4776 von ATA empfangen wird.|
> |Abrufen der Details eines Benutzers, eines Computers oder einer Gruppe (UniqueEntity), z. B. eine Benutzer-ID.|`db.UniqueEntity.find({CompleteSearchNames: "<name of entity in lower case>"})`||
> |Ermitteln des Kerberos-Authentifizierungsdatenverkehrs von einem bestimmten Computer an einem bestimmten Tag.|`db.KerberosAs_<datetime>.find({SourceComputerId: "<Id of the source computer>"})`|Um die &lt;ID des Quellcomputers&gt; abzurufen, können Sie die UniqueEntity-Sammlungen abfragen (siehe Beispiel).<br /><br />Für jeden Netzwerkaktivitätstyp (z. B. Kerberos-Authentifizierungen) ist eine eigene Sammlung pro UTC-Datum vorhanden.|
> |Vornehmen erweiterter Konfigurationsänderungen. In diesem Beispiel wird die Größe der Sendewarteschlange für alle ATA-Gateways in 10.000 geändert.|`db.SystemProfile.update( {_t: "GatewaySystemProfile"} ,`<br>`{$set:{"Configuration.EntitySenderConfiguration.EntityBatchBlockMaxSize" : "10000"}})`|`|

Das folgende Beispiel enthält Beispielcode mit der zuvor angegebenen Syntax. Wenn Sie eine verdächtige Aktivität untersuchen, die am 20.10.2015 erfolgt ist, und mehr über die NTLM-Aktivitäten erfahren möchten, die „John Doe“ an diesem Tag ausgeführt hat, gehen Sie wie folgt vor:<br /><br />Suchen Sie zunächst die ID von „John Doe“.

`db.UniqueEntity.find({Name: "John Doe"})`<br>Notieren Sie sich die ID, die durch den Wert von `_id` angegeben wird. In diesem Beispiel gehen wir von der ID `123bdd24-b269-h6e1-9c72-7737as875351` aus.<br>Suchen Sie dann die Sammlung mit dem nächstgelegenen Datum vor dem Datum, das Sie suchen, in diesem Beispiel 20.10.2015.<br>Suchen Sie anschließend die NTLM-Aktivitäten des Kontos von John Doe: 

`db.Ntlms_<closest date>.find({SourceAccountId: "123bdd24-b269-h6e1-9c72-7737as875351"})`

## <a name="see-also"></a>Weitere Informationen
- [ATA-Voraussetzungen](ata-prerequisites.md)
- [ATA-Kapazitätsplanung](ata-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-collection.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
