---
title: Advanced Threat Analytics-Datenbankverwaltung
description: Vorgänge zum Verschieben, Sichern oder Wiederherstellen der ATA-Datenbank.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 05e49e23-6e0a-4ec0-9a63-a2093173c8a1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: f6f39619aa3ba960384b646f2b4237118cabf725
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2020
ms.locfileid: "94691076"
---
# <a name="ata-database-management"></a>ATA-Datenbankverwaltung

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Verwenden Sie diese Verfahren im Umgang mit MongoDB, wenn die ATA-Datenbank verschoben, gesichert oder wiederhergestellt werden soll.

## <a name="backing-up-the-ata-database"></a>Sichern der ATA-Datenbank
Weitere Informationen finden Sie in der [entsprechenden MongoDB-Dokumentation](http://docs.mongodb.org/manual/administration/backup/).

## <a name="restoring-the-ata-database"></a>Wiederherstellen der ATA-Datenbank
Weitere Informationen finden Sie in der [entsprechenden MongoDB-Dokumentation](http://docs.mongodb.org/manual/administration/backup/).

## <a name="moving-the-ata-database-to-another-drive"></a>Verschieben der ATA-Datenbank auf ein anderes Laufwerk

1. Halten Sie den Dienst **Microsoft Advanced Threat Analytics Center** an.
   > [!Important] 
   > Stellen Sie sicher, dass der ATA Center-Dienst beendet wurde, bevor Sie mit dem nächsten Schritt fortfahren.

1. Halten Sie den Dienst **MongoDB** an.

1. Öffnen Sie die MongoDB-Konfigurationsdatei, die standardmäßig unter „C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongod.cfg“ zu finden ist.

   Finden Sie den `storage: dbPath`-Parameter.

1. Verschieben Sie den im `dbPath`-Parameter aufgeführten Ordner an den neuen Speicherort.

1. Ändern Sie den `dbPath`-Parameter innerhalb der MongoDB-Konfiguration in den neuen Ordnerpfad der Datei, und speichern und schließen Sie die Datei.

    ![Ändern des MongoDB-Konfigurationsimages](media/ATA-mongoDB-moveDB.png)

1. Starten Sie den **MongoDB** -Dienst.

1. Starten Sie den Dienst **Microsoft Advanced Threat Analytics Center**.

## <a name="see-also"></a>Weitere Informationen
- [ATA-Architektur](ata-architecture.md)
- [ATA-Voraussetzungen](ata-prerequisites.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

