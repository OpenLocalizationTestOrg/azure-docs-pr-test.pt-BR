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
# <a name="use-powershell-tooback-up-and-restore-app-service-apps"></a><span data-ttu-id="99010-103">Use o PowerShell tooback e restaurar aplicativos de serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="99010-103">Use PowerShell tooback up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="99010-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="99010-104">PowerShell</span></span>](app-service-powershell-backup.md)
> * [<span data-ttu-id="99010-105">API REST</span><span class="sxs-lookup"><span data-stu-id="99010-105">REST API</span></span>](../app-service-web/websites-csm-backup.md)
> 
> 

<span data-ttu-id="99010-106">Saiba como toouse tooback de PowerShell do Azure de backup e restauração [aplicativos de serviço de aplicativo](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="99010-106">Learn how toouse Azure PowerShell tooback up and restore [App Service apps](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="99010-107">Para saber mais sobre os backups de aplicativo Web, incluindo requisitos e restrições, confira [Fazer backup de um aplicativo Web no Serviço de Aplicativo do Azure](../app-service-web/web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="99010-107">For more information about web app backups, including requirements and restrictions, see [Back up a web app in Azure App Service](../app-service-web/web-sites-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99010-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="99010-108">Prerequisites</span></span>
<span data-ttu-id="99010-109">toouse PowerShell toomanage seus backups de aplicativo, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="99010-109">toouse PowerShell toomanage your app backups, you need hello following:</span></span>

* <span data-ttu-id="99010-110">**Uma URL SAS** que permite a leitura e o contêiner de armazenamento do Azure tooan acesso de gravação.</span><span class="sxs-lookup"><span data-stu-id="99010-110">**A SAS URL** that allows read and write access tooan Azure Storage container.</span></span> <span data-ttu-id="99010-111">Consulte [modelo SAS Olá Noções básicas sobre](../storage/common/storage-dotnet-shared-access-signature-part-1.md) para obter uma explicação de URLs da SAS.</span><span class="sxs-lookup"><span data-stu-id="99010-111">See [Understanding hello SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for an explanation of SAS URLs.</span></span> <span data-ttu-id="99010-112">Consulte [Usar o Azure PowerShell com o Armazenamento do Azure](../storage/common/storage-powershell-guide-full.md) para obter exemplos de gerenciamento do Armazenamento do Azure usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="99010-112">See [Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) for examples of managing Azure Storage using PowerShell.</span></span>
* <span data-ttu-id="99010-113">**Uma cadeia de caracteres de conexão do banco de dados** se você quiser tooback um banco de dados junto com seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="99010-113">**A database connection string** if you want tooback up a database along with your web app.</span></span>

### <a name="how-toogenerate-a-sas-url-toouse-with-hello-web-app-backup-cmdlets"></a><span data-ttu-id="99010-114">Como o backup cmdlets toogenerate toouse uma URL SAS com Olá web app</span><span class="sxs-lookup"><span data-stu-id="99010-114">How toogenerate a SAS URL toouse with hello web app backup cmdlets</span></span>
<span data-ttu-id="99010-115">Uma URL SAS pode ser gerada com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="99010-115">A SAS URL can be generated with PowerShell.</span></span> <span data-ttu-id="99010-116">Aqui está um exemplo de como toogenerate que pode ser usado com hello cmdlets discutidos neste artigo.</span><span class="sxs-lookup"><span data-stu-id="99010-116">Here is an example of how toogenerate one that can be used with hello cmdlets discussed in this article.</span></span>

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure tooselect hello appropriate key. Here we select hello first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a><span data-ttu-id="99010-117">Instalar o Azure PowerShell 1.3.2 ou superior</span><span class="sxs-lookup"><span data-stu-id="99010-117">Install Azure PowerShell 1.3.2 or greater</span></span>
<span data-ttu-id="99010-118">Confira [Como usar o Azure PowerShell com o Azure Resource Manager](/powershell/azure/overview) para obter instruções sobre como instalar e usar o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="99010-118">See [Using Azure PowerShell with Azure Resource Manager](/powershell/azure/overview) for instructions on installing and using Azure PowerShell.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="99010-119">Criar um backup</span><span class="sxs-lookup"><span data-stu-id="99010-119">Create a backup</span></span>
<span data-ttu-id="99010-120">Use Olá AzureRmWebAppBackup novo cmdlet toocreate um backup de um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="99010-120">Use hello New-AzureRmWebAppBackup cmdlet toocreate a backup of a web app.</span></span>

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

<span data-ttu-id="99010-121">Isso cria um backup com um nome gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="99010-121">This creates a backup with an automatically generated name.</span></span> <span data-ttu-id="99010-122">Se você quiser tooprovide um nome para o backup, use parâmetro opcional de BackupName hello.</span><span class="sxs-lookup"><span data-stu-id="99010-122">If you would like tooprovide a name for your backup, use hello BackupName optional parameter.</span></span>

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

<span data-ttu-id="99010-123">tooinclude um banco de dados no backup Olá, primeiro crie uma configuração de backup do banco de dados usando o cmdlet do novo AzureRmWebAppDatabaseBackupSetting hello e fornecer a configuração no hello parâmetro bancos de dados de saudação AzureRmWebAppBackup novo cmdlet.</span><span class="sxs-lookup"><span data-stu-id="99010-123">tooinclude a database in hello backup, first create a database backup setting using hello New-AzureRmWebAppDatabaseBackupSetting cmdlet, then supply that setting in hello Databases parameter of hello New-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="99010-124">parâmetro de bancos de dados Hello aceita uma matriz de configurações de banco de dados, permitindo que você tooback mais de um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="99010-124">hello Databases parameter accepts an array of database settings, allowing you tooback up more than one database.</span></span>

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a><span data-ttu-id="99010-125">Obter backups</span><span class="sxs-lookup"><span data-stu-id="99010-125">Get backups</span></span>
<span data-ttu-id="99010-126">Olá Get-AzureRmWebAppBackupList cmdlet retorna uma matriz de todos os backups para um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="99010-126">hello Get-AzureRmWebAppBackupList cmdlet returns an array of all backups for a web app.</span></span> <span data-ttu-id="99010-127">Você deve fornecer o nome de saudação do aplicativo web de saudação e seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="99010-127">You must supply hello name of hello web app and its resource group.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

<span data-ttu-id="99010-128">tooget um backup específico, use o cmdlet Get-AzureRmWebAppBackup de saudação.</span><span class="sxs-lookup"><span data-stu-id="99010-128">tooget a specific backup, use hello Get-AzureRmWebAppBackup cmdlet.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

<span data-ttu-id="99010-129">Também é possível redirecionar um objeto de aplicativo da web em qualquer um dos cmdlets de gerenciamento de backup Olá para sua conveniência.</span><span class="sxs-lookup"><span data-stu-id="99010-129">You can also pipe a web app object into any of hello backup management cmdlets for convenience.</span></span>

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a><span data-ttu-id="99010-130">Agendar backups automáticos</span><span class="sxs-lookup"><span data-stu-id="99010-130">Schedule automatic backups</span></span>
<span data-ttu-id="99010-131">Você pode agendar backups toohappen automaticamente em um intervalo especificado.</span><span class="sxs-lookup"><span data-stu-id="99010-131">You can schedule backups toohappen automatically at a specified interval.</span></span> <span data-ttu-id="99010-132">tooconfigure um agendamento de backup, use cmdlet Olá AzureRmWebAppBackupConfiguration de edição.</span><span class="sxs-lookup"><span data-stu-id="99010-132">tooconfigure a backup schedule, use hello Edit-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="99010-133">Este cmdlet aceita vários parâmetros:</span><span class="sxs-lookup"><span data-stu-id="99010-133">This cmdlet takes several parameters:</span></span>

* <span data-ttu-id="99010-134">**Nome** - Olá nome do aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="99010-134">**Name** - hello name of hello web app.</span></span>
* <span data-ttu-id="99010-135">**ResourceGroupName** - Olá nome do aplicativo de web do hello recurso grupo contentor hello.</span><span class="sxs-lookup"><span data-stu-id="99010-135">**ResourceGroupName** - hello name of hello resource group containing hello web app.</span></span>
* <span data-ttu-id="99010-136">**Slot** - Opcional.</span><span class="sxs-lookup"><span data-stu-id="99010-136">**Slot** - Optional.</span></span> <span data-ttu-id="99010-137">nome de saudação do slot do aplicativo web hello.</span><span class="sxs-lookup"><span data-stu-id="99010-137">hello name of hello web app slot.</span></span>
* <span data-ttu-id="99010-138">**StorageAccountUrl** -Olá URL SAS para contêiner de armazenamento do Azure Olá usados backups de saudação toostore.</span><span class="sxs-lookup"><span data-stu-id="99010-138">**StorageAccountUrl** - hello SAS URL for hello Azure Storage container used toostore hello backups.</span></span>
* <span data-ttu-id="99010-139">**FrequencyInterval** -valor numérico para a frequência hello backups devem ser feitos.</span><span class="sxs-lookup"><span data-stu-id="99010-139">**FrequencyInterval** - Numeric value for how often hello backups should be made.</span></span> <span data-ttu-id="99010-140">Deve ser um número inteiro positivo.</span><span class="sxs-lookup"><span data-stu-id="99010-140">Must be a positive integer.</span></span>
* <span data-ttu-id="99010-141">**FrequencyUnit** -unidade de tempo para frequência hello backups devem ser feitos.</span><span class="sxs-lookup"><span data-stu-id="99010-141">**FrequencyUnit** - Unit of time for how often hello backups should be made.</span></span> <span data-ttu-id="99010-142">As opções são Hour (Hora) e Day (Dia).</span><span class="sxs-lookup"><span data-stu-id="99010-142">Options are Hour and Day.</span></span>
* <span data-ttu-id="99010-143">**RetentionPeriodInDays** - backups automáticos Olá devem ser salvo antes de serem excluídos automaticamente o número de dias.</span><span class="sxs-lookup"><span data-stu-id="99010-143">**RetentionPeriodInDays** - How many days hello automatic backups should be saved before being automatically deleted.</span></span>
* <span data-ttu-id="99010-144">**StartTime** - Opcional.</span><span class="sxs-lookup"><span data-stu-id="99010-144">**StartTime** - Optional.</span></span> <span data-ttu-id="99010-145">tempo de saudação quando os backups automáticos Olá devem começar.</span><span class="sxs-lookup"><span data-stu-id="99010-145">hello time when hello automatic backups should begin.</span></span> <span data-ttu-id="99010-146">Os backups começarão imediatamente se esse parâmetro for nulo.</span><span class="sxs-lookup"><span data-stu-id="99010-146">Backups begin immediately if this is null.</span></span> <span data-ttu-id="99010-147">Ele deve ser um DateTime.</span><span class="sxs-lookup"><span data-stu-id="99010-147">Must be a DateTime.</span></span>
* <span data-ttu-id="99010-148">**Databases** - Opcional.</span><span class="sxs-lookup"><span data-stu-id="99010-148">**Databases** - Optional.</span></span> <span data-ttu-id="99010-149">Uma matriz de DatabaseBackupSettings Olá toobackup de bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="99010-149">An array of DatabaseBackupSettings for hello databases toobackup.</span></span>
* <span data-ttu-id="99010-150">**KeepAtLeastOneBackup** - Parâmetro opcional comutado.</span><span class="sxs-lookup"><span data-stu-id="99010-150">**KeepAtLeastOneBackup** - Optional switched parameter.</span></span> <span data-ttu-id="99010-151">Isso se um backup sempre deve ser mantido em Olá conta de armazenamento, independentemente de quanto tempo é de fonte.</span><span class="sxs-lookup"><span data-stu-id="99010-151">Supply this if one backup should always be kept in hello storage account, regardless of how old it is.</span></span>

<span data-ttu-id="99010-152">A seguir está um exemplo de como toouse esse cmdlet.</span><span class="sxs-lookup"><span data-stu-id="99010-152">Following is an example of how toouse this cmdlet.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

<span data-ttu-id="99010-153">tooget Olá agenda de backup atual, use o cmdlet Get-AzureRmWebAppBackupConfiguration de saudação.</span><span class="sxs-lookup"><span data-stu-id="99010-153">tooget hello current backup schedule, use hello Get-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="99010-154">Isso pode ser útil para modificar uma agenda que já foi configurada.</span><span class="sxs-lookup"><span data-stu-id="99010-154">This can be useful for modifying a schedule that has already been configured.</span></span>

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify hello configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply hello new configuration by piping it into hello Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a><span data-ttu-id="99010-155">Restaurar um aplicativo Web a partir de um backup</span><span class="sxs-lookup"><span data-stu-id="99010-155">Restore a web app from a backup</span></span>
<span data-ttu-id="99010-156">toorestore um aplicativo web de um backup, use o cmdlet Olá AzureRmWebAppBackup de restauração.</span><span class="sxs-lookup"><span data-stu-id="99010-156">toorestore a web app from a backup, use hello Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="99010-157">Olá toouse de maneira mais fácil esse cmdlet é toopipe em um objeto de backup recuperado do cmdlet Get-AzureRmWebAppBackup de saudação ou o cmdlet Get-AzureRmWebAppBackupList.</span><span class="sxs-lookup"><span data-stu-id="99010-157">hello easiest way toouse this cmdlet is toopipe in a backup object retrieved from hello Get-AzureRmWebAppBackup cmdlet or Get-AzureRmWebAppBackupList cmdlet.</span></span>

<span data-ttu-id="99010-158">Uma vez que um objeto de backup, poderá direcioná-lo para Olá restauração AzureRmWebAppBackup cmdlet.</span><span class="sxs-lookup"><span data-stu-id="99010-158">Once you have a backup object, you can pipe it into hello Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="99010-159">Especifique Olá substituir comutador parâmetro tooindicate que você pretende que o conteúdo de saudação do toooverwrite de seu aplicativo web com saudação do backup hello.</span><span class="sxs-lookup"><span data-stu-id="99010-159">Specify hello Overwrite switch parameter tooindicate that you intend toooverwrite hello contents of your web app with hello contents of hello backup.</span></span> <span data-ttu-id="99010-160">Se o backup Olá contém bancos de dados, esses bancos de dados são restaurados também.</span><span class="sxs-lookup"><span data-stu-id="99010-160">If hello backup contains databases, those databases are restored as well.</span></span>

        $backup | Restore-AzureRmWebAppBackup -Overwrite

<span data-ttu-id="99010-161">A seguir está um exemplo de como toouse Olá AzureRmWebAppBackup de restauração, especificando todos os parâmetros de saudação.</span><span class="sxs-lookup"><span data-stu-id="99010-161">Following is an example of how toouse hello Restore-AzureRmWebAppBackup by specifying all hello parameters.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a><span data-ttu-id="99010-162">Excluir um conjunto de backups</span><span class="sxs-lookup"><span data-stu-id="99010-162">Delete a backup</span></span>
<span data-ttu-id="99010-163">toodelete um backup, use cmdlet Olá AzureRmWebAppBackup remover.</span><span class="sxs-lookup"><span data-stu-id="99010-163">toodelete a backup, use hello Remove-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="99010-164">Isso remove o backup de saudação da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="99010-164">This removes hello backup from your storage account.</span></span> <span data-ttu-id="99010-165">Especifique o nome do aplicativo, seu grupo de recursos, e Olá ID da saudação backup você deseja toodelete.</span><span class="sxs-lookup"><span data-stu-id="99010-165">Specify your app name, its resource group, and hello ID of hello backup you want toodelete.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

<span data-ttu-id="99010-166">Também é possível redirecionar um objeto de backup em Olá remover AzureRmWebAppBackup cmdlet toodelete-lo.</span><span class="sxs-lookup"><span data-stu-id="99010-166">You can also pipe a backup object into hello Remove-AzureRmWebAppBackup cmdlet toodelete it.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
