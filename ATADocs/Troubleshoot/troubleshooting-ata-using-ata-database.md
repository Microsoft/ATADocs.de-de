---
title: Behandeln von Problemen mit ATA mithilfe der ATA-Datenbank | Microsoft Docs
description: Beschreibt die Verwendung der ATA-Datenbank zum Behandeln von Problemen.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 377a3c81-5c1d-486f-8942-85249aacf560
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: fca7f1b2b8260cad6e0ce32aad1c9e1b53fc0ad5
ms.openlocfilehash: bff3224736981f38616172a6b1717d7d125c3c0a


---

*Gilt für: Advanced Threat Analytics Version 1.7*



# <a name="troubleshooting-ata-using-the-ata-database"></a>Behandeln von Problemen mit ATA mithilfe der ATA-Datenbank
ATA verwendet MongoDB als Datenbank.
Die Interaktion mit der Datenbank ist über die Standardbefehlszeile möglich oder über ein Benutzeroberflächentool, mit dem Sie erweiterte Aufgaben und Problembehandlung ausführen können.

## <a name="interacting-with-the-database"></a>Interagieren mit der Datenbank
Die Datenbank lässt sich standardmäßig und am einfachsten über die Mongo-Shell abfragen:

1.  Öffnen Sie ein Befehlszeilenfenster, und ändern Sie den Pfad in den MongoDB-Ordner „bin“. Der Standardpfad lautet **C:\Programme\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**.

2.  Führen Sie `mongo.exe ATA` aus. Geben Sie „ATA“ in Großbuchstaben ein.

|So wird es gemacht|Syntax|Hinweise|
|-------------|----------|---------|
|Suchen nach Sammlungen in der Datenbank.|`show collections`|Hilfreich als End-to-End-Test, um zu überprüfen, ob Datenverkehr in die Datenbank geschrieben und das Ereignis 4776 von ATA empfangen wird.|
|Abrufen der Details eines Benutzers, eines Computers oder einer Gruppe (UniqueEntity), z. B. eine Benutzer-ID.|`db.UniqueEntity.find({SearchNames: "<name of entity in lower case>"})`||
|Ermitteln des Kerberos-Authentifizierungsdatenverkehrs von einem bestimmten Computer an einem bestimmten Tag.|`db.KerberosAs_<datetime>.find({SourceComputerId: "<Id of the source computer>"})`|Um die &lt;ID des Quellcomputers&gt; abzurufen, können Sie die UniqueEntity-Sammlungen abfragen (siehe Beispiel).<br /><br />Für jeden Netzwerkaktivitätstyp (z. B. Kerberos-Authentifizierungen) ist eine eigene Sammlung pro UTC-Datum vorhanden.|
|Suchen des NTLM-Datenverkehrs von einem bestimmten Computer in Bezug auf ein bestimmtes Konto an einem bestimmten Tag.|`db.Ntlm_<datetime>.find({SourceComputerId: "<Id of the source computer>", SourceAccountId: "<Id of the account>"})`|Um die &lt;ID des Quellcomputers&gt; und die &lt;ID des Kontos&gt; abzurufen, können Sie die UniqueEntity-Sammlungen abfragen (siehe Beispiel).<br /><br />Für jeden Netzwerkaktivitätstyp (z. B. NTLM-Authentifizierungen) ist eine eigene Sammlung pro UTC-Datum vorhanden.|
|Suchen nach erweiterten Eigenschaften, z. B. den aktiven Datumsangaben eines Kontos. |`db.UniqueEntityProfile.find({UniqueEntityId: "<Id of the account>")`|Um die &lt;ID des Kontos&gt; abzurufen, können Sie die UniqueEntity-Sammlungen abfragen (siehe Beispiel).<br>Der Eigenschaftenname, der die Datumsangaben anzeigt, an denen das Konto aktiv war, lautet „ActiveDates“. <br>
Beispiel: Sie möchten wissen, ob ein Konto mindestens 21 Tage aktiv ist, damit der Machine Learning-Algorithmus für nicht normales Verhalten für das Konto ausgeführt werden kann.|
|Vornehmen erweiterter Konfigurationsänderungen. In diesem Beispiel wird die Größe der Sendewarteschlange für alle ATA-Gateways in 10.000 geändert.|`db.SystemProfile.update( {_t: "GatewaySystemProfile"} ,`<br>`{$set:{"Configuration.EntitySenderConfiguration.EntityBatchBlockMaxSize" : "10000"}})`|`|

Das folgende Beispiel enthält Beispielcode mit der oben aufgeführten Syntax. Wenn Sie eine verdächtige Aktivität untersuchen, die am 20.10.2015 erfolgt ist, und mehr über die NTLM-Aktivitäten erfahren möchten, die „John Doe“ an diesem Tag ausgeführt hat, gehen Sie wie folgt vor:<br /><br />Suchen Sie zunächst die ID von „John Doe“.

`db.UniqueEntity.find({Name: "John Doe"})`<br>Notieren Sie sich seine ID, die durch den Wert von „`_id`“ angegeben ist. In diesem Beispiel gehen wir von der ID „`123bdd24-b269-h6e1-9c72-7737as875351`“ aus.<br>Suchen Sie dann die Sammlung mit dem nächstgelegenen Datum vor dem Datum, das Sie suchen, in diesem Beispiel 20.10.2015.<br>Suchen Sie anschließend die NTLM-Aktivitäten des Kontos von John Doe: 

`db.Ntlms_<closest date>.find({SourceAccountId: "123bdd24-b269-h6e1-9c72-7737as875351"})`

## <a name="see-also"></a>Weitere Informationen
- [Voraussetzungen für ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA-Kapazitätsplanung](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Konfigurieren der Ereignissammlung](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurieren der Windows-Ereignisweiterleitung](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Nov16_HO3-->


