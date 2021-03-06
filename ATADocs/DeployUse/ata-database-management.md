---
title: Advanced Threat Analytics-Datenbankverwaltung | Microsoft-Dokumentation
description: "Vorgänge zum Verschieben, Sichern oder Wiederherstellen der ATA-Datenbank."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 05e49e23-6e0a-4ec0-9a63-a2093173c8a1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: e5bb1fa702d58b725b7052e5848741d4d24f279e
ms.sourcegitcommit: 49e892a82275efa5146998764e850959f20d3216
translationtype: HT
---
*Gilt für: Advanced Threat Analytics Version 1.7*



# <a name="ata-database-management"></a>ATA-Datenbankverwaltung
Verwenden Sie diese Verfahren im Umgang mit MongoDB, wenn die ATA-Datenbank verschoben, gesichert oder wiederhergestellt werden soll.

## <a name="backing-up-the-ata-database"></a>Sichern der ATA-Datenbank
Informationen hierzu finden Sie in der [entsprechenden MongoDB-Dokumentation](http://docs.mongodb.org/manual/administration/backup/).

## <a name="restoring-the-ata-database"></a>Wiederherstellen der ATA-Datenbank
Informationen hierzu finden Sie in der [entsprechenden MongoDB-Dokumentation](http://docs.mongodb.org/manual/administration/backup/).

## <a name="moving-the-ata-database-to-another-drive"></a>Verschieben der ATA-Datenbank auf ein anderes Laufwerk

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

## <a name="see-also"></a>Siehe auch
- [ATA-Architektur](/advanced-threat-analytics/plan-design/ata-architecture)
- [Voraussetzungen für ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

