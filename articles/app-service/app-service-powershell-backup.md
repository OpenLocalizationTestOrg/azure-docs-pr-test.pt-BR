---
title: "aaaUse PowerShell tooback de backup e restauração de aplicativos de serviço de aplicativo"
description: "Saiba como toouse PowerShell tooback de backup e restauração de um aplicativo no serviço de aplicativo do Azure"
services: app-service
documentationcenter: 
author: NKing92
manager: erikre
editor: 
ms.assetid: 7ea8661e-aefb-4823-9626-6bff980cdebf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2016
ms.author: nicking
ms.openlocfilehash: 4042166f6c650841926f010056d6c80ab2de57e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooback-up-and-restore-app-service-apps"></a>Use o PowerShell tooback e restaurar aplicativos de serviço de aplicativo
> [!div class="op_single_selector"]
> * [PowerShell](app-service-powershell-backup.md)
> * [API REST](../app-service-web/websites-csm-backup.md)
> 
> 

Saiba como toouse tooback de PowerShell do Azure de backup e restauração [aplicativos de serviço de aplicativo](https://azure.microsoft.com/services/app-service/web/). Para saber mais sobre os backups de aplicativo Web, incluindo requisitos e restrições, confira [Fazer backup de um aplicativo Web no Serviço de Aplicativo do Azure](../app-service-web/web-sites-backup.md).

## <a name="prerequisites"></a>Pré-requisitos
toouse PowerShell toomanage seus backups de aplicativo, você precisa Olá a seguir:

* **Uma URL SAS** que permite a leitura e o contêiner de armazenamento do Azure tooan acesso de gravação. Consulte [modelo SAS Olá Noções básicas sobre](../storage/common/storage-dotnet-shared-access-signature-part-1.md) para obter uma explicação de URLs da SAS. Consulte [Usar o Azure PowerShell com o Armazenamento do Azure](../storage/common/storage-powershell-guide-full.md) para obter exemplos de gerenciamento do Armazenamento do Azure usando o PowerShell.
* **Uma cadeia de caracteres de conexão do banco de dados** se você quiser tooback um banco de dados junto com seu aplicativo web.

### <a name="how-toogenerate-a-sas-url-toouse-with-hello-web-app-backup-cmdlets"></a>Como o backup cmdlets toogenerate toouse uma URL SAS com Olá web app
Uma URL SAS pode ser gerada com o PowerShell. Aqui está um exemplo de como toogenerate que pode ser usado com hello cmdlets discutidos neste artigo.

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure tooselect hello appropriate key. Here we select hello first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a>Instalar o Azure PowerShell 1.3.2 ou superior
Confira [Como usar o Azure PowerShell com o Azure Resource Manager](/powershell/azure/overview) para obter instruções sobre como instalar e usar o Azure PowerShell.

## <a name="create-a-backup"></a>Criar um backup
Use Olá AzureRmWebAppBackup novo cmdlet toocreate um backup de um aplicativo web.

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

Isso cria um backup com um nome gerado automaticamente. Se você quiser tooprovide um nome para o backup, use parâmetro opcional de BackupName hello.

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

tooinclude um banco de dados no backup Olá, primeiro crie uma configuração de backup do banco de dados usando o cmdlet do novo AzureRmWebAppDatabaseBackupSetting hello e fornecer a configuração no hello parâmetro bancos de dados de saudação AzureRmWebAppBackup novo cmdlet. parâmetro de bancos de dados Hello aceita uma matriz de configurações de banco de dados, permitindo que você tooback mais de um banco de dados.

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a>Obter backups
Olá Get-AzureRmWebAppBackupList cmdlet retorna uma matriz de todos os backups para um aplicativo web. Você deve fornecer o nome de saudação do aplicativo web de saudação e seu grupo de recursos.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

tooget um backup específico, use o cmdlet Get-AzureRmWebAppBackup de saudação.

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

Também é possível redirecionar um objeto de aplicativo da web em qualquer um dos cmdlets de gerenciamento de backup Olá para sua conveniência.

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a>Agendar backups automáticos
Você pode agendar backups toohappen automaticamente em um intervalo especificado. tooconfigure um agendamento de backup, use cmdlet Olá AzureRmWebAppBackupConfiguration de edição. Este cmdlet aceita vários parâmetros:

* **Nome** - Olá nome do aplicativo web de saudação.
* **ResourceGroupName** - Olá nome do aplicativo de web do hello recurso grupo contentor hello.
* **Slot** - Opcional. nome de saudação do slot do aplicativo web hello.
* **StorageAccountUrl** -Olá URL SAS para contêiner de armazenamento do Azure Olá usados backups de saudação toostore.
* **FrequencyInterval** -valor numérico para a frequência hello backups devem ser feitos. Deve ser um número inteiro positivo.
* **FrequencyUnit** -unidade de tempo para frequência hello backups devem ser feitos. As opções são Hour (Hora) e Day (Dia).
* **RetentionPeriodInDays** - backups automáticos Olá devem ser salvo antes de serem excluídos automaticamente o número de dias.
* **StartTime** - Opcional. tempo de saudação quando os backups automáticos Olá devem começar. Os backups começarão imediatamente se esse parâmetro for nulo. Ele deve ser um DateTime.
* **Databases** - Opcional. Uma matriz de DatabaseBackupSettings Olá toobackup de bancos de dados.
* **KeepAtLeastOneBackup** - Parâmetro opcional comutado. Isso se um backup sempre deve ser mantido em Olá conta de armazenamento, independentemente de quanto tempo é de fonte.

A seguir está um exemplo de como toouse esse cmdlet.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

tooget Olá agenda de backup atual, use o cmdlet Get-AzureRmWebAppBackupConfiguration de saudação. Isso pode ser útil para modificar uma agenda que já foi configurada.

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify hello configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply hello new configuration by piping it into hello Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a>Restaurar um aplicativo Web a partir de um backup
toorestore um aplicativo web de um backup, use o cmdlet Olá AzureRmWebAppBackup de restauração. Olá toouse de maneira mais fácil esse cmdlet é toopipe em um objeto de backup recuperado do cmdlet Get-AzureRmWebAppBackup de saudação ou o cmdlet Get-AzureRmWebAppBackupList.

Uma vez que um objeto de backup, poderá direcioná-lo para Olá restauração AzureRmWebAppBackup cmdlet. Especifique Olá substituir comutador parâmetro tooindicate que você pretende que o conteúdo de saudação do toooverwrite de seu aplicativo web com saudação do backup hello. Se o backup Olá contém bancos de dados, esses bancos de dados são restaurados também.

        $backup | Restore-AzureRmWebAppBackup -Overwrite

A seguir está um exemplo de como toouse Olá AzureRmWebAppBackup de restauração, especificando todos os parâmetros de saudação.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a>Excluir um conjunto de backups
toodelete um backup, use cmdlet Olá AzureRmWebAppBackup remover. Isso remove o backup de saudação da conta de armazenamento. Especifique o nome do aplicativo, seu grupo de recursos, e Olá ID da saudação backup você deseja toodelete.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

Também é possível redirecionar um objeto de backup em Olá remover AzureRmWebAppBackup cmdlet toodelete-lo.

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
