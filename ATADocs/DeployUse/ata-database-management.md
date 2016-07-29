---
title: ATA-Datenbankverwaltung | Microsoft ATA
description: "Vorgänge zum Verschieben, Sichern oder Wiederherstellen der ATA-Datenbank."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: 83222c6d29434d93fa1b5ecd613de30408ccfe59


---

# ATA-Datenbankverwaltung
Verwenden Sie diese Verfahren im Umgang mit MongoDB, wenn die ATA-Datenbank verschoben, gesichert oder wiederhergestellt werden soll.

## Sichern der ATA-Datenbank
Informationen hierzu finden Sie in der [entsprechenden MongoDB-Dokumentation](http://docs.mongodb.org/manual/administration/backup/).

## Wiederherstellen der ATA-Datenbank
Informationen hierzu finden Sie in der [entsprechenden MongoDB-Dokumentation](http://docs.mongodb.org/manual/administration/backup/).

## Verschieben der ATA-Datenbank auf ein anderes Laufwerk

1.  Halten Sie den Dienst **Microsoft Advanced Threat Analytics Center** an.

2.  Halten Sie den Dienst **MongoDB** an.

3.  Öffnen Sie die MongoDB-Konfigurationsdatei, die standardmäßig unter „C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongod.cfg“ zu finden ist.

    Suchen Sie den Parameter. `storage: dbPath`

4.  Verschieben Sie den im `dbPath`-Parameter aufgeführten Ordner an den neuen Speicherort.

5.  Ändern Sie den `dbPath`-Parameter innerhalb der MongoDB-Konfiguration in den neuen Ordnerpfad der Datei, und speichern und schließen Sie die Datei.

    ![Ändern des MongoDB-Konfigurationsimages](media/ATA-mongoDB-moveDB.png)

6.  Starten Sie den Dienst **MongoDB**.

7.  Öffnen Sie eine Befehlszeile, und führen Sie die Mongo-Shell aus, indem Sie `mongo.exe ATA` ausführen.

    Standardmäßig befindet sich „mongo.exe“ unter: „C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin“.

8.  Führen Sie den folgenden Befehl aus: `db.SystemProfiles.update( {_t: "CenterSystemProfile"} , {$set:{"Configuration.CenterDatabaseClientConfiguration.DataPath" : "<New DB Location>"}})`

   Anstelle von <New DB Location>, wobei `&lt;New DB Location&gt;` der neue Ordnerpfad ist.

9.  Aktualisieren Sie „HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center\DatabaseDataPath“ auf den neuen Ordnerpfad.

9. Starten Sie den Dienst **Microsoft Advanced Threat Analytics Center**.

## Siehe auch
- [ATA-Architektur](/advanced-threat-analytics/plan-design/ata-architecture)
- [ATA-Voraussetzungen](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Jul16_HO4-->


