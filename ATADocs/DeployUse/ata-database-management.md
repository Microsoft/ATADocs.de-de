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
ms.sourcegitcommit: 5cd030f3b952d08c6617a6cda121c344a9c36f51
ms.openlocfilehash: b4e68e9e8dbd94075a34a8e3e8f42d4f534caf50


---

*Gilt für: Advanced Threat Analytics Version 1.7*



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

7. Starten Sie den Dienst **Microsoft Advanced Threat Analytics Center**.

## ATA-Konfigurationsdatei
Die Konfiguration von ATA ist in der Sammlung „SystemProfile“ in der Datenbank gespeichert.
Diese Sammlung wird vom ATA Center-Dienst stündlich in Dateien mit dem Namen „SystemProfile_*Zeitstempel*.json“ gespeichert. Die 10 neuesten Versionen werden gespeichert.
Diese Datei befindet sich im Unterordner „Backup“. Im ATA-Standardinstallationsverzeichnis ist die Datei unter *C:\Programme\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_*Zeitstempel*.json* zu finden. 

**Hinweis**: Wenn Sie größere Änderungen an ATA vornehmen, wird empfohlen, eine Sicherung dieser Datei zu erstellen.

Sie können alle Einstellungen wiederherstellen, indem Sie den folgenden Befehl ausführen:

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## Siehe auch
- [ATA-Architektur](/advanced-threat-analytics/plan-design/ata-architecture)
- [ATA-Voraussetzungen](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Aug16_HO5-->


