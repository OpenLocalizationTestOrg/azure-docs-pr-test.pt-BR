---
title: "Usar o PowerShell para fazer backup e restaurar aplicativos do Serviço de Aplicativo"
description: "Saiba como usar o PowerShell para fazer backup e restaurar um aplicativo no Serviço de Aplicativo do Azure"
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
ms.openlocfilehash: 34a7e1d025c301ca056753d964bb3c5f4f1a62d8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-powershell-to-back-up-and-restore-app-service-apps"></a><span data-ttu-id="9ce09-103">Usar o PowerShell para fazer backup e restaurar aplicativos do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="9ce09-103">Use PowerShell to back up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9ce09-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9ce09-104">PowerShell</span></span>](app-service-powershell-backup.md)
> * [<span data-ttu-id="9ce09-105">API REST</span><span class="sxs-lookup"><span data-stu-id="9ce09-105">REST API</span></span>](../app-service-web/websites-csm-backup.md)
> 
> 

<span data-ttu-id="9ce09-106">Saiba como usar o Azure PowerShell para fazer backup e restaurar [aplicativos do Serviço de Aplicativo](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="9ce09-106">Learn how to use Azure PowerShell to back up and restore [App Service apps](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="9ce09-107">Para saber mais sobre os backups de aplicativo Web, incluindo requisitos e restrições, confira [Fazer backup de um aplicativo Web no Serviço de Aplicativo do Azure](../app-service-web/web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="9ce09-107">For more information about web app backups, including requirements and restrictions, see [Back up a web app in Azure App Service](../app-service-web/web-sites-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ce09-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9ce09-108">Prerequisites</span></span>
<span data-ttu-id="9ce09-109">Para usar o PowerShell para gerenciar os backups do seu aplicativo, você precisa do seguinte:</span><span class="sxs-lookup"><span data-stu-id="9ce09-109">To use PowerShell to manage your app backups, you need the following:</span></span>

* <span data-ttu-id="9ce09-110">**Um URL de SAS** que permite o acesso de leitura e gravação a um contêiner do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ce09-110">**A SAS URL** that allows read and write access to an Azure Storage container.</span></span> <span data-ttu-id="9ce09-111">Consulte [Noções básicas do modelo de SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) para ver uma explicação sobre URLs SAS.</span><span class="sxs-lookup"><span data-stu-id="9ce09-111">See [Understanding the SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for an explanation of SAS URLs.</span></span> <span data-ttu-id="9ce09-112">Consulte [Usar o Azure PowerShell com o Armazenamento do Azure](../storage/common/storage-powershell-guide-full.md) para obter exemplos de gerenciamento do Armazenamento do Azure usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9ce09-112">See [Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) for examples of managing Azure Storage using PowerShell.</span></span>
* <span data-ttu-id="9ce09-113">**Uma cadeia de conexão de banco de dados** se você quiser fazer backup de um banco de dados junto com seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="9ce09-113">**A database connection string** if you want to back up a database along with your web app.</span></span>

### <a name="how-to-generate-a-sas-url-to-use-with-the-web-app-backup-cmdlets"></a><span data-ttu-id="9ce09-114">Como gerar uma URL SAS para usar com os cmdlets do backup do aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="9ce09-114">How to generate a SAS URL to use with the web app backup cmdlets</span></span>
<span data-ttu-id="9ce09-115">Uma URL SAS pode ser gerada com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9ce09-115">A SAS URL can be generated with PowerShell.</span></span> <span data-ttu-id="9ce09-116">Aqui está um exemplo de como gerar uma que pode ser usada com os cmdlets discutidos neste artigo.</span><span class="sxs-lookup"><span data-stu-id="9ce09-116">Here is an example of how to generate one that can be used with the cmdlets discussed in this article.</span></span>

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure to select the appropriate key. Here we select the first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a><span data-ttu-id="9ce09-117">Instalar o Azure PowerShell 1.3.2 ou superior</span><span class="sxs-lookup"><span data-stu-id="9ce09-117">Install Azure PowerShell 1.3.2 or greater</span></span>
<span data-ttu-id="9ce09-118">Confira [Como usar o Azure PowerShell com o Azure Resource Manager](/powershell/azure/overview) para obter instruções sobre como instalar e usar o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9ce09-118">See [Using Azure PowerShell with Azure Resource Manager](/powershell/azure/overview) for instructions on installing and using Azure PowerShell.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="9ce09-119">Criar um backup</span><span class="sxs-lookup"><span data-stu-id="9ce09-119">Create a backup</span></span>
<span data-ttu-id="9ce09-120">Use o cmdlet New-AzureRmWebAppBackup para criar um backup de um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="9ce09-120">Use the New-AzureRmWebAppBackup cmdlet to create a backup of a web app.</span></span>

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

<span data-ttu-id="9ce09-121">Isso cria um backup com um nome gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9ce09-121">This creates a backup with an automatically generated name.</span></span> <span data-ttu-id="9ce09-122">Se você quiser fornecer um nome para seu backup, use o parâmetro opcional BackupName.</span><span class="sxs-lookup"><span data-stu-id="9ce09-122">If you would like to provide a name for your backup, use the BackupName optional parameter.</span></span>

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

<span data-ttu-id="9ce09-123">Para incluir um banco de dados no backup, primeiro crie uma configuração de backup de banco de dados usando o cmdlet New-AzureRmWebAppDatabaseBackupSetting e depois forneça essa configuração no parâmetro Databases do cmdlet New-AzureRmWebAppBackup.</span><span class="sxs-lookup"><span data-stu-id="9ce09-123">To include a database in the backup, first create a database backup setting using the New-AzureRmWebAppDatabaseBackupSetting cmdlet, then supply that setting in the Databases parameter of the New-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="9ce09-124">O parâmetro Databases aceita uma matriz de configurações de banco de dados, permitindo que você faça backup de mais de um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="9ce09-124">The Databases parameter accepts an array of database settings, allowing you to back up more than one database.</span></span>

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a><span data-ttu-id="9ce09-125">Obter backups</span><span class="sxs-lookup"><span data-stu-id="9ce09-125">Get backups</span></span>
<span data-ttu-id="9ce09-126">O cmdlet Get-AzureRmWebAppBackupList retornará uma matriz de todos os backups de um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="9ce09-126">The Get-AzureRmWebAppBackupList cmdlet returns an array of all backups for a web app.</span></span> <span data-ttu-id="9ce09-127">Você deve fornecer o nome do aplicativo Web e de seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9ce09-127">You must supply the name of the web app and its resource group.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

<span data-ttu-id="9ce09-128">Para obter um backup específico, use o cmdlet Get-AzureRmWebAppBackup.</span><span class="sxs-lookup"><span data-stu-id="9ce09-128">To get a specific backup, use the Get-AzureRmWebAppBackup cmdlet.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

<span data-ttu-id="9ce09-129">Você também pode redirecionar um objeto de aplicativo Web para qualquer um dos cmdlets do gerenciamento de backup para sua conveniência.</span><span class="sxs-lookup"><span data-stu-id="9ce09-129">You can also pipe a web app object into any of the backup management cmdlets for convenience.</span></span>

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a><span data-ttu-id="9ce09-130">Agendar backups automáticos</span><span class="sxs-lookup"><span data-stu-id="9ce09-130">Schedule automatic backups</span></span>
<span data-ttu-id="9ce09-131">Você pode agendar backups automáticos em um intervalo especificado.</span><span class="sxs-lookup"><span data-stu-id="9ce09-131">You can schedule backups to happen automatically at a specified interval.</span></span> <span data-ttu-id="9ce09-132">Para configurar um agendamento de backup, use o cmdlet Edit-AzureRmWebAppBackupConfiguration.</span><span class="sxs-lookup"><span data-stu-id="9ce09-132">To configure a backup schedule, use the Edit-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="9ce09-133">Este cmdlet aceita vários parâmetros:</span><span class="sxs-lookup"><span data-stu-id="9ce09-133">This cmdlet takes several parameters:</span></span>

* <span data-ttu-id="9ce09-134">**Name** - O nome do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="9ce09-134">**Name** - The name of the web app.</span></span>
* <span data-ttu-id="9ce09-135">**ResourceGroupName** - O nome do grupo de recursos que contém o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="9ce09-135">**ResourceGroupName** - The name of the resource group containing the web app.</span></span>
* <span data-ttu-id="9ce09-136">**Slot** - Opcional.</span><span class="sxs-lookup"><span data-stu-id="9ce09-136">**Slot** - Optional.</span></span> <span data-ttu-id="9ce09-137">O nome do slot do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="9ce09-137">The name of the web app slot.</span></span>
* <span data-ttu-id="9ce09-138">**StorageAccountUrl** - A URL SAS do contêiner do Armazenamento do Azure usado para armazenar os backups.</span><span class="sxs-lookup"><span data-stu-id="9ce09-138">**StorageAccountUrl** - The SAS URL for the Azure Storage container used to store the backups.</span></span>
* <span data-ttu-id="9ce09-139">**FrequencyInterval** - Valor numérico relacionado à frequência dos backups.</span><span class="sxs-lookup"><span data-stu-id="9ce09-139">**FrequencyInterval** - Numeric value for how often the backups should be made.</span></span> <span data-ttu-id="9ce09-140">Deve ser um número inteiro positivo.</span><span class="sxs-lookup"><span data-stu-id="9ce09-140">Must be a positive integer.</span></span>
* <span data-ttu-id="9ce09-141">**FrequencyUnit** - Unidade de tempo relacionada à frequência dos backups.</span><span class="sxs-lookup"><span data-stu-id="9ce09-141">**FrequencyUnit** - Unit of time for how often the backups should be made.</span></span> <span data-ttu-id="9ce09-142">As opções são Hour (Hora) e Day (Dia).</span><span class="sxs-lookup"><span data-stu-id="9ce09-142">Options are Hour and Day.</span></span>
* <span data-ttu-id="9ce09-143">**RetentionPeriodInDays** - Quantos dias os backups automáticos devem ser salvos antes de serem automaticamente excluídos.</span><span class="sxs-lookup"><span data-stu-id="9ce09-143">**RetentionPeriodInDays** - How many days the automatic backups should be saved before being automatically deleted.</span></span>
* <span data-ttu-id="9ce09-144">**StartTime** - Opcional.</span><span class="sxs-lookup"><span data-stu-id="9ce09-144">**StartTime** - Optional.</span></span> <span data-ttu-id="9ce09-145">A hora de início dos backups automáticos.</span><span class="sxs-lookup"><span data-stu-id="9ce09-145">The time when the automatic backups should begin.</span></span> <span data-ttu-id="9ce09-146">Os backups começarão imediatamente se esse parâmetro for nulo.</span><span class="sxs-lookup"><span data-stu-id="9ce09-146">Backups begin immediately if this is null.</span></span> <span data-ttu-id="9ce09-147">Ele deve ser um DateTime.</span><span class="sxs-lookup"><span data-stu-id="9ce09-147">Must be a DateTime.</span></span>
* <span data-ttu-id="9ce09-148">**Databases** - Opcional.</span><span class="sxs-lookup"><span data-stu-id="9ce09-148">**Databases** - Optional.</span></span> <span data-ttu-id="9ce09-149">Uma matriz de DatabaseBackupSettings para backup dos bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="9ce09-149">An array of DatabaseBackupSettings for the databases to backup.</span></span>
* <span data-ttu-id="9ce09-150">**KeepAtLeastOneBackup** - Parâmetro opcional comutado.</span><span class="sxs-lookup"><span data-stu-id="9ce09-150">**KeepAtLeastOneBackup** - Optional switched parameter.</span></span> <span data-ttu-id="9ce09-151">Forneça esse parâmetro se um backup sempre precisar ser mantido na conta de armazenamento, independentemente de sua idade.</span><span class="sxs-lookup"><span data-stu-id="9ce09-151">Supply this if one backup should always be kept in the storage account, regardless of how old it is.</span></span>

<span data-ttu-id="9ce09-152">Veja a seguir um exemplo de como usar este cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9ce09-152">Following is an example of how to use this cmdlet.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

<span data-ttu-id="9ce09-153">Para obter a agenda de backup atual, use o cmdlet Get-AzureRmWebAppBackupConfiguration.</span><span class="sxs-lookup"><span data-stu-id="9ce09-153">To get the current backup schedule, use the Get-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="9ce09-154">Isso pode ser útil para modificar uma agenda que já foi configurada.</span><span class="sxs-lookup"><span data-stu-id="9ce09-154">This can be useful for modifying a schedule that has already been configured.</span></span>

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify the configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply the new configuration by piping it into the Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a><span data-ttu-id="9ce09-155">Restaurar um aplicativo Web a partir de um backup</span><span class="sxs-lookup"><span data-stu-id="9ce09-155">Restore a web app from a backup</span></span>
<span data-ttu-id="9ce09-156">Para restaurar um aplicativo Web a partir de um backup, use o cmdlet Restore-AzureRmWebAppBackup.</span><span class="sxs-lookup"><span data-stu-id="9ce09-156">To restore a web app from a backup, use the Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="9ce09-157">A maneira mais fácil de usar este cmdlet é direcionar um objeto de backup recuperado do cmdlet Get-AzureRmWebAppBackup ou do cmdlet Get-AzureRmWebAppBackupList.</span><span class="sxs-lookup"><span data-stu-id="9ce09-157">The easiest way to use this cmdlet is to pipe in a backup object retrieved from the Get-AzureRmWebAppBackup cmdlet or Get-AzureRmWebAppBackupList cmdlet.</span></span>

<span data-ttu-id="9ce09-158">Assim que você tiver um objeto de backup, será possível direcioná-lo para o cmdlet Restore-AzureRmWebAppBackup.</span><span class="sxs-lookup"><span data-stu-id="9ce09-158">Once you have a backup object, you can pipe it into the Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="9ce09-159">Especifique o parâmetro de opção Overwrite para indicar que pretende substituir o conteúdo de seu aplicativo Web pelo conteúdo do backup.</span><span class="sxs-lookup"><span data-stu-id="9ce09-159">Specify the Overwrite switch parameter to indicate that you intend to overwrite the contents of your web app with the contents of the backup.</span></span> <span data-ttu-id="9ce09-160">Se o backup contiver bancos de dados, eles também serão restaurados.</span><span class="sxs-lookup"><span data-stu-id="9ce09-160">If the backup contains databases, those databases are restored as well.</span></span>

        $backup | Restore-AzureRmWebAppBackup -Overwrite

<span data-ttu-id="9ce09-161">Veja a seguir um exemplo de como usar Restore-AzureRmWebAppBackup especificando todos os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="9ce09-161">Following is an example of how to use the Restore-AzureRmWebAppBackup by specifying all the parameters.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a><span data-ttu-id="9ce09-162">Excluir um conjunto de backups</span><span class="sxs-lookup"><span data-stu-id="9ce09-162">Delete a backup</span></span>
<span data-ttu-id="9ce09-163">Para excluir um backup, use o cmdlet Remove-AzureRmWebAppBackup.</span><span class="sxs-lookup"><span data-stu-id="9ce09-163">To delete a backup, use the Remove-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="9ce09-164">Isso removerá o backup da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9ce09-164">This removes the backup from your storage account.</span></span> <span data-ttu-id="9ce09-165">Especifique o nome do aplicativo, seu grupo de recursos e a ID do backup que você quer excluir.</span><span class="sxs-lookup"><span data-stu-id="9ce09-165">Specify your app name, its resource group, and the ID of the backup you want to delete.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

<span data-ttu-id="9ce09-166">Também é possível direcionar um objeto de backup para o cmdlet Remove-AzureRmWebAppBackup para excluí-lo.</span><span class="sxs-lookup"><span data-stu-id="9ce09-166">You can also pipe a backup object into the Remove-AzureRmWebAppBackup cmdlet to delete it.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
