---
title: Advanced Threat Analytics-Datenbankverwaltung | Microsoft-Dokumentation
description: "Vorgänge zum Verschieben, Sichern oder Wiederherstellen der ATA-Datenbank."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/12/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 05e49e23-6e0a-4ec0-9a63-a2093173c8a1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 4fe667574ea011c032bacd8f5bce4b07c2c46602
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/30/2017
---
*Gilt für: Advanced Threat Analytics Version 1.8*



# ATA-Datenbankverwaltung
<a id="ata-database-management" class="xliff"></a>
Verwenden Sie diese Verfahren im Umgang mit MongoDB, wenn die ATA-Datenbank verschoben, gesichert oder wiederhergestellt werden soll.

## Sichern der ATA-Datenbank
<a id="backing-up-the-ata-database" class="xliff"></a>
Informationen hierzu finden Sie in der [entsprechenden MongoDB-Dokumentation](http://docs.mongodb.org/manual/administration/backup/).

## Wiederherstellen der ATA-Datenbank
<a id="restoring-the-ata-database" class="xliff"></a>
Informationen hierzu finden Sie in der [entsprechenden MongoDB-Dokumentation](http://docs.mongodb.org/manual/administration/backup/).

## Verschieben der ATA-Datenbank auf ein anderes Laufwerk
<a id="moving-the-ata-database-to-another-drive" class="xliff"></a>

1.  Halten Sie den Dienst **Microsoft Advanced Threat Analytics Center** an.
> [!Important] 
> Stellen Sie sicher, dass der ATA Center-Dienst beendet wurde, bevor Sie mit dem nächsten Schritt fortfahren.

2.  Halten Sie den Dienst **MongoDB** an.

3.  Öffnen Sie die MongoDB-Konfigurationsdatei, die standardmäßig unter „C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongod.cfg“ zu finden ist.

    Finden Sie den `storage: dbPath`-Parameter.

4.  Verschieben Sie den im `dbPath`-Parameter aufgeführten Ordner an den neuen Speicherort.

5.  Ändern Sie den `dbPath`-Parameter innerhalb der MongoDB-Konfiguration in den neuen Ordnerpfad der Datei, und speichern und schließen Sie die Datei.

    ![Ändern des MongoDB-Konfigurationsimages](media/ATA-mongoDB-moveDB.png)

6.  Starten Sie den Dienst **MongoDB**.

7. Starten Sie den Dienst **Microsoft Advanced Threat Analytics Center**.

## Siehe auch
<a id="see-also" class="xliff"></a>
- [ATA-Architektur](ata-architecture.md)
- [Voraussetzungen für ATA](ata-prerequisites.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

