---
title: "Restaurar um aplicativo no Serviço de Aplicativo do Azure"
description: Saiba como restaurar seu aplicativo de um backup.
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 4444dbf7-363c-47e2-b24a-dbd45cb08491
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: 5fe74d992edb7028fa4a2500e427013d98ebc250
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="restore-an-app-in-azure"></a><span data-ttu-id="52846-103">Restaurar um aplicativo no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="52846-103">Restore an app in Azure</span></span>
<span data-ttu-id="52846-104">Este artigo mostra como restaurar um aplicativo no [Serviço de Aplicativo do Azure](../app-service/app-service-value-prop-what-is.md) do qual você fez backup anteriormente (veja [Fazer backup de seu aplicativo no Azure](web-sites-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="52846-104">This article shows you how to restore an app in [Azure App Service](../app-service/app-service-value-prop-what-is.md) that you have previously backed up (see [Back up your app in Azure](web-sites-backup.md)).</span></span> <span data-ttu-id="52846-105">É possível restaurar seu aplicativo com seus bancos de dados vinculados sob demanda para um estado anterior ou criar um novo aplicativo com base em um backup de seu aplicativo original.</span><span class="sxs-lookup"><span data-stu-id="52846-105">You can restore your app with its linked databases on-demand to a previous state, or create a new app based on one of your original app's backup.</span></span> <span data-ttu-id="52846-106">O Serviço de Aplicativo do Azure oferece suporte aos seguintes bancos de dados para backup e restauração:</span><span class="sxs-lookup"><span data-stu-id="52846-106">Azure App Service supports the following databases for backup and restore:</span></span>
- [<span data-ttu-id="52846-107">Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="52846-107">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
- [<span data-ttu-id="52846-108">Banco de Dados do Azure para MySQL (Visualização)</span><span class="sxs-lookup"><span data-stu-id="52846-108">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
- [<span data-ttu-id="52846-109">Banco de Dados do Azure para PostgreSQL (Visualização)</span><span class="sxs-lookup"><span data-stu-id="52846-109">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
- [<span data-ttu-id="52846-110">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="52846-110">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
- [<span data-ttu-id="52846-111">MySQL no aplicativo</span><span class="sxs-lookup"><span data-stu-id="52846-111">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)

<span data-ttu-id="52846-112">A restauração usando backups está disponível para aplicativos que são executados nas camadas **Standard** e **Premium**.</span><span class="sxs-lookup"><span data-stu-id="52846-112">Restoring from backups is available to apps running in **Standard** and **Premium** tier.</span></span> <span data-ttu-id="52846-113">Para obter informações sobre como escalar verticalmente seu aplicativo, veja [Escalar verticalmente um aplicativo Web no Serviço de Aplicativo do Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="52846-113">For information about scaling up your app, see [Scale up an app in Azure](web-sites-scale.md).</span></span> <span data-ttu-id="52846-114">A camada **Premium** permite um número maior de backups diários do que a camada **Standard**.</span><span class="sxs-lookup"><span data-stu-id="52846-114">**Premium** tier allows a greater number of daily backups to be performed than **Standard** tier.</span></span>

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a><span data-ttu-id="52846-115">Restaurar um aplicativo por meio de um backup existente</span><span class="sxs-lookup"><span data-stu-id="52846-115">Restore an app from an existing backup</span></span>
1. <span data-ttu-id="52846-116">Na folha **Configurações** de seu aplicativo no portal do Azure, clique em **Backups** para exibir a folha **Backups**.</span><span class="sxs-lookup"><span data-stu-id="52846-116">On the **Settings** blade of your app in the Azure Portal, click **Backups** to display the **Backups** blade.</span></span> <span data-ttu-id="52846-117">Depois, clique em **Restaurar**.</span><span class="sxs-lookup"><span data-stu-id="52846-117">Then click **Restore**.</span></span>
   
    ![Escolha restaurar agora][ChooseRestoreNow]
2. <span data-ttu-id="52846-119">Na folha **Restauração** , primeiro selecione a fonte do backup.</span><span class="sxs-lookup"><span data-stu-id="52846-119">In the **Restore** blade, first select the backup source.</span></span>
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    <span data-ttu-id="52846-120">A opção **Backup do aplicativo** mostra todos os backups existentes do aplicativo atual, e você pode selecionar um com facilidade.</span><span class="sxs-lookup"><span data-stu-id="52846-120">The **App backup** option shows you all the existing backups of the current app, and you can easily select one.</span></span>
    <span data-ttu-id="52846-121">A opção **Armazenamento** permite selecionar qualquer arquivo ZIP de backup em qualquer conta do Armazenamento do Azure e contêiner existentes em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="52846-121">The **Storage** option lets you select any backup ZIP file from any existing Azure Storage account and container in your subscription.</span></span>
    <span data-ttu-id="52846-122">Se você está tentando restaurar um backup de outro aplicativo, use a opção **Armazenamento** .</span><span class="sxs-lookup"><span data-stu-id="52846-122">If you're trying to restore a backup of another app, use the **Storage** option.</span></span>
3. <span data-ttu-id="52846-123">Em seguida, especifique o destino para a restauração de aplicativo em **Destino de restauração**.</span><span class="sxs-lookup"><span data-stu-id="52846-123">Then, specify the destination for the app restore in **Restore destination**.</span></span>
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > <span data-ttu-id="52846-124">Se você escolher **Substituir**, todos os dados existentes em seu aplicativo atual serão apagados e substituídos.</span><span class="sxs-lookup"><span data-stu-id="52846-124">If you choose **Overwrite**, all existing data in your current app is erased and overwritten.</span></span> <span data-ttu-id="52846-125">Antes de clicar em **OK**, certifique-se de que isso é exatamente o que você deseja fazer.</span><span class="sxs-lookup"><span data-stu-id="52846-125">Before you click **OK**, make sure that it is exactly what you want to do.</span></span>
   > 
   > 
   
    <span data-ttu-id="52846-126">Você pode selecionar um **Aplicativo Existente** para restaurar o backup do aplicativo para outro aplicativo no mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="52846-126">You can select **Existing App** to restore the app backup to another app in the same resoure group.</span></span> <span data-ttu-id="52846-127">Antes de usar essa opção, você já precisa ter criado outro aplicativo em seu grupo de recursos com o espelhamento da configuração de banco de dados para aquele definido no backup do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="52846-127">Before you use this option, you should have already created another app in your resource group with mirroring database configuration to the one defined in the app backup.</span></span> <span data-ttu-id="52846-128">Você também pode criar um **Novo** aplicativo no qual o conteúdo será restaurado.</span><span class="sxs-lookup"><span data-stu-id="52846-128">You can also Create a **New** app to restore your content to.</span></span>

4. <span data-ttu-id="52846-129">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="52846-129">Click **OK**.</span></span>

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a><span data-ttu-id="52846-130">Baixar ou excluir um backup de uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="52846-130">Download or delete a backup from a storage account</span></span>
1. <span data-ttu-id="52846-131">Na folha principal **Procurar** do Portal do Azure, selecione **Contas de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="52846-131">From the main **Browse** blade of the Azure portal, select **Storage accounts**.</span></span> <span data-ttu-id="52846-132">Uma lista de suas contas de armazenamento existentes é exibida.</span><span class="sxs-lookup"><span data-stu-id="52846-132">A list of your existing storage accounts is displayed.</span></span>
2. <span data-ttu-id="52846-133">Selecione a conta de armazenamento que contém o backup que você deseja baixar ou excluir. A folha da conta de armazenamento é exibida.</span><span class="sxs-lookup"><span data-stu-id="52846-133">Select the storage account that contains the backup that you want to download or delete.The blade for the storage account is displayed.</span></span>
3. <span data-ttu-id="52846-134">Na folha da conta de armazenamento, selecione o contêiner desejado</span><span class="sxs-lookup"><span data-stu-id="52846-134">In the storage account blade, select the container you want</span></span>
   
    ![Exibir contêineres][ViewContainers]
4. <span data-ttu-id="52846-136">Selecione o arquivo de backup que você deseja baixar ou excluir.</span><span class="sxs-lookup"><span data-stu-id="52846-136">Select backup file you want to download or delete.</span></span>
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. <span data-ttu-id="52846-138">Clique em **Baixar** ou **Excluir**, dependendo da ação desejada.</span><span class="sxs-lookup"><span data-stu-id="52846-138">Click **Download** or **Delete** depending on what you want to do.</span></span>  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a><span data-ttu-id="52846-139">Monitorar uma operação de restauração</span><span class="sxs-lookup"><span data-stu-id="52846-139">Monitor a restore operation</span></span>
<span data-ttu-id="52846-140">Para ver detalhes sobre o sucesso ou a falha da operação de restauração do aplicativo, navegue até a folha **Log de Atividades** no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="52846-140">To see details about the success or failure of the app restore operation, navigate to the **Activity Log** blade in the Azure portal.</span></span>  
 

<span data-ttu-id="52846-141">Role para baixo para encontrar a operação de restauração desejada e clique para selecioná-la.</span><span class="sxs-lookup"><span data-stu-id="52846-141">Scroll down to find the desired restore operation and click to select it.</span></span>

<span data-ttu-id="52846-142">A folha de detalhes exibe as informações disponíveis relacionadas à operação de restauração.</span><span class="sxs-lookup"><span data-stu-id="52846-142">The details blade displays the available information related to the restore operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52846-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="52846-143">Next Steps</span></span>
<span data-ttu-id="52846-144">Você pode fazer backup e restaurar aplicativos do Serviço de Aplicativo usando a API REST (veja [Usar a REST para fazer backup e restaurar aplicativos do Serviço de Aplicativo](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="52846-144">You can backup and restore App Service apps using REST API (see [Use REST to back up and restore App Service apps](websites-csm-backup.md)).</span></span>


<!-- IMAGES -->
[ChooseRestoreNow]: ./media/web-sites-restore/02ChooseRestoreNow1.png
[ViewContainers]: ./media/web-sites-restore/03ViewContainers.png
[StorageAccountFile]: ./media/web-sites-restore/02StorageAccountFile.png
[BrowseCloudStorage]: ./media/web-sites-restore/03BrowseCloudStorage.png
[StorageAccountFileSelected]: ./media/web-sites-restore/04StorageAccountFileSelected.png
[ChooseRestoreSettings]: ./media/web-sites-restore/05ChooseRestoreSettings.png
[ChooseDBServer]: ./media/web-sites-restore/06ChooseDBServer.png
[RestoreToNewSQLDB]: ./media/web-sites-restore/07RestoreToNewSQLDB.png
[NewSQLDBConfig]: ./media/web-sites-restore/08NewSQLDBConfig.png
[RestoredContosoWebSite]: ./media/web-sites-restore/09RestoredContosoWebSite.png
[DashboardOperationLogsLink]: ./media/web-sites-restore/10DashboardOperationLogsLink.png
[ManagementServicesOperationLogsList]: ./media/web-sites-restore/11ManagementServicesOperationLogsList.png
[DetailsButton]: ./media/web-sites-restore/12DetailsButton.png
[OperationDetails]: ./media/web-sites-restore/13OperationDetails.png
