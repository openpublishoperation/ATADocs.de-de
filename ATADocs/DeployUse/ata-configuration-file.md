---
title: Exportieren und Importieren der Advanced Threat Analytics-Konfiguration | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie die ATA-Konfiguration exportieren und importieren.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: b0d85b60129e2638880c11b5f1faadca2feeae2c
ms.sourcegitcommit: 49e892a82275efa5146998764e850959f20d3216
translationtype: HT
---
*Gilt für: Advanced Threat Analytics Version 1.7*



# <a name="export-and-import-the-ata-configuration"></a>Exportieren und Importieren der ATA-Konfiguration
Die Konfiguration von ATA ist in der Sammlung „SystemProfile“ in der Datenbank gespeichert.
Diese Sammlung wird vom ATA Center-Dienst stündlich in Dateien mit dem Namen „SystemProfile_*Zeitstempel*.json“ gespeichert. Die 10 neuesten Versionen werden gespeichert.
Diese Datei befindet sich im Unterordner „Backup“. Im ATA-Standardinstallationsverzeichnis ist die Datei unter *C:\Programme\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_*Zeitstempel*.json* zu finden. 

**Hinweis**: Wenn Sie größere Änderungen an ATA vornehmen, wird empfohlen, eine Sicherung dieser Datei zu erstellen.

Sie können alle Einstellungen wiederherstellen, indem Sie den folgenden Befehl ausführen:

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## <a name="see-also"></a>Siehe auch
- [ATA-Architektur](/advanced-threat-analytics/plan-design/ata-architecture)
- [Voraussetzungen für ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

