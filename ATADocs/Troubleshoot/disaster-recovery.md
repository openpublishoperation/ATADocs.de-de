---
title: "Notfallwiederherstellung für Advanced Threat Analytics | Microsoft-Dokumentation"
description: "Beschreibt, wie Sie die ATA-Funktionalität nach einem Notfall schnell wiederherstellen können"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 02/28/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 7620e171-76d5-4e3f-8b03-871678217a3a
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: e315e9731fa9715c3b41b9292349ee5aca13fbce
ms.sourcegitcommit: 4f5927f30089655e3984d69623ea4439b7c36845
translationtype: HT
---
*Gilt für: Advanced Threat Analytics Version 1.7*



# <a name="ata-disaster-recovery"></a>ATA-Notfallwiederherstellung
Dieser Artikel beschreibt, wie Sie ATA Center und Ihre ATA-Funktionalität schnell wiederherstellen können, wenn die ATA Center-Funktionalität verloren gegangen ist, die ATA-Gateways jedoch noch funktionieren. 

>[!NOTE]
> Der beschriebene Prozess stellt keine zuvor erkannten verdächtigen Aktivitäten wieder her, sorgt jedoch dafür, dass ATA Center wieder voll funktionstüchtig ist. Darüber hinaus wird der erforderliche Lernzeitraum für einige Verhaltenserkennungen neu gestartet, jedoch sind die meisten Erkennungen, die ATA nach der Wiederherstellung von ATA Center zurückgibt, betriebsbereit. 

## <a name="back-up-your-ata-center-configuration"></a>Sichern Ihrer ATA Center-Konfiguration

1. Die ATA Center-Konfiguration wird stündlich in einer Datei gesichert. Suchen Sie die neueste Sicherungskopie der ATA Center-Konfiguration, und speichern Sie sie auf einem separaten Computer. Eine ausführliche Erläuterung zum Auffinden dieser Dateien finden Sie unter [Exportieren und Importieren der ATA-Konfiguration](/advanced-threat-analytics/deploy-use/ata-configuration-file). 
2. Exportieren Sie das Zertifikats für ATA Center.
    1. Wechseln Sie im Zertifikat-Manager (`certlm.msc`) zu **Zertifikate (Lokaler Computer)** -> **Persönlich** ->**Zertifikate**, und wählen Sie **ATA Center** aus.
    2. Klicken Sie mit der rechten Maustaste auf **ATA Center**, wählen Sie **Alle Tasks** und dann **Exportieren** aus. 
     ![Zertifikat für ATA Center](media/ata-center-cert.png)
    3. Befolgen Sie die Anweisungen zum Exportieren des Zertifikats, und stellen Sie sicher, dass Sie auch den privaten Schlüssel exportieren.
    4. Sichern Sie die exportierte Zertifikatsdatei auf einem separaten Computer.

  > [!NOTE] 
  > Wenn der private Schlüssel nicht exportiert werden konnte, müssen Sie ein neues Zertifikat erstellen, es auf ATA bereitstellen, wie in [Ändern des Zertifikats für ATA Center](/advanced-threat-analytics/deploy-use/modifying-ata-config-centercert) beschrieben, und es dann exportieren. 

## <a name="recover-your-ata-center"></a>Wiederherstellen von ATA Center

1. Erstellen Sie einen neuen Windows Server-Computer mit der gleichen IP-Adresse und dem gleichen Computernamen wie beim vorherigen ATA Center-Computer.
4. Importieren Sie das Zertifikat, das Sie in den oben genannten Vorgängen auf dem neuen Server gesichert haben.
5. Befolgen Sie die Anweisungen unter [Deploy the ATA Center (Bereitstellen von ATA Center)](/advanced-threat-analytics/deploy-use/install-ata-step1) auf dem neu erstellten Windows Server-Computer. Stellen Sie sicher, dass Sie die gleiche IP-Adresse und den gleichen Port wie beim alten Center auswählen. Die ATA-Gateways müssen nicht noch einmal bereitgestellt werden. Erhalten Sie eine Aufforderung zur Angabe eines Zertifikats, dann stellen Sie das Zertifikat bereit, das Sie bei der Sicherung der ATA Center-Konfiguration exportiert haben. 
![Wiederherstellung von ATA Center](media/ata-center-restore.png)
6. Importieren Sie die gesicherte ATA Center-Konfiguration:
    1. Entfernen Sie das Systemprofildokument von ATA Center aus MongoDB: 
        1. Gehen Sie unter **C:\Programme\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**. 
        2. Ausführen von `mongo.exe ATA` 
        3. Führen Sie zum Entfernen des Standardsystemprofils diesen Befehl aus: `db.SystemProfile.remove({})`
    2. Führen Sie den folgenden Befehl `mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert` mithilfe der Sicherungsdatei aus Schritt 1 aus.</br>
    Eine ausführliche Erläuterung zum Auffinden und Importieren von Sicherungsdateien finden Sie unter [Exportieren und Importieren der ATA-Konfiguration](/advanced-threat-analytics/deploy-use/ata-configuration-file). 
    3. Führen Sie nach dem Importieren diesen Befehl aus, um einige der Standardsystemprofile zu entfernen (um sie für die neue Umgebung zurückzusetzen): `db.SystemProfile.remove({$or:[{"_t":"DetectorProfile"}, "_t":"DirectoryServicesSystemProfile"}]}) `
    4. Öffnen Sie die ATA-Konsole. Sie sollten alle ATA-Gateways auf der Registerkarte „Konfiguration/Gateways“ verknüpft sehen. 
    5. Definieren Sie einen [**Verzeichnisdienstebenutzer**](/advanced-threat-analytics/deploy-use/install-ata-step2), und wählen Sie eine [**Domänencontrollersynchronisierung**](/advanced-threat-analytics/deploy-use/install-ata-step5) aus. 






## <a name="see-also"></a>Siehe auch
- [Voraussetzungen für ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA-Kapazitätsplanung](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Konfigurieren der Ereignissammlung](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurieren der Windows-Ereignisweiterleitung](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
