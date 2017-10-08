---
title: aaaRestore um aplicativo no Azure
description: Saiba como toorestore seu aplicativo a partir de um backup.
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
ms.openlocfilehash: 4b54029a9197064f990f29a3c4558c8322668714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-app-in-azure"></a><span data-ttu-id="6ac7b-103">Restaurar um aplicativo no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="6ac7b-103">Restore an app in Azure</span></span>
<span data-ttu-id="6ac7b-104">Este artigo mostra como toorestore um aplicativo em [do serviço de aplicativo do Azure](../app-service/app-service-value-prop-what-is.md) que você fez backup anteriormente (consulte [backup de seu aplicativo no Azure](web-sites-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="6ac7b-104">This article shows you how toorestore an app in [Azure App Service](../app-service/app-service-value-prop-what-is.md) that you have previously backed up (see [Back up your app in Azure](web-sites-backup.md)).</span></span> <span data-ttu-id="6ac7b-105">Você pode restaurar seu aplicativo com seu estado anterior do bancos de dados vinculados tooa sob demanda ou criar um novo aplicativo com base em um backup do seu aplicativo original.</span><span class="sxs-lookup"><span data-stu-id="6ac7b-105">You can restore your app with its linked databases on-demand tooa previous state, or create a new app based on one of your original app's backup.</span></span> <span data-ttu-id="6ac7b-106">Serviço de aplicativo do Azure dá suporte a saudação bancos de dados para backup e restauração a seguir:</span><span class="sxs-lookup"><span data-stu-id="6ac7b-106">Azure App Service supports hello following databases for backup and restore:</span></span>
- [<span data-ttu-id="6ac7b-107">Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="6ac7b-107">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
- [<span data-ttu-id="6ac7b-108">Banco de Dados do Azure para MySQL (Visualização)</span><span class="sxs-lookup"><span data-stu-id="6ac7b-108">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
- [<span data-ttu-id="6ac7b-109">Banco de Dados do Azure para PostgreSQL (Visualização)</span><span class="sxs-lookup"><span data-stu-id="6ac7b-109">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
- [<span data-ttu-id="6ac7b-110">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="6ac7b-110">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
- [<span data-ttu-id="6ac7b-111">MySQL no aplicativo</span><span class="sxs-lookup"><span data-stu-id="6ac7b-111">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)

<span data-ttu-id="6ac7b-112">Restaurando de backups é tooapps disponíveis em execução no **padrão** e **Premium** camada.</span><span class="sxs-lookup"><span data-stu-id="6ac7b-112">Restoring from backups is available tooapps running in **Standard** and **Premium** tier.</span></span> <span data-ttu-id="6ac7b-113">Para obter informações sobre como escalar verticalmente seu aplicativo, veja [Escalar verticalmente um aplicativo Web no Serviço de Aplicativo do Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="6ac7b-113">For information about scaling up your app, see [Scale up an app in Azure](web-sites-scale.md).</span></span> <span data-ttu-id="6ac7b-114">**Premium** nível permite que um número maior de toobe de backups diários executada que **padrão** camada.</span><span class="sxs-lookup"><span data-stu-id="6ac7b-114">**Premium** tier allows a greater number of daily backups toobe performed than **Standard** tier.</span></span>

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a><span data-ttu-id="6ac7b-115">Restaurar um aplicativo por meio de um backup existente</span><span class="sxs-lookup"><span data-stu-id="6ac7b-115">Restore an app from an existing backup</span></span>
1. <span data-ttu-id="6ac7b-116">Em Olá **configurações** folha do seu aplicativo em Olá Portal do Azure, clique em **Backups** toodisplay Olá **Backups** folha.</span><span class="sxs-lookup"><span data-stu-id="6ac7b-116">On hello **Settings** blade of your app in hello Azure Portal, click **Backups** toodisplay hello **Backups** blade.</span></span> <span data-ttu-id="6ac7b-117">Depois, clique em **Restaurar**.</span><span class="sxs-lookup"><span data-stu-id="6ac7b-117">Then click **Restore**.</span></span>
   
    ![Escolha restaurar agora][ChooseRestoreNow]
2. <span data-ttu-id="6ac7b-119">Em Olá **restaurar** folha, uma fonte de backup Olá selecione primeiro.</span><span class="sxs-lookup"><span data-stu-id="6ac7b-119">In hello **Restore** blade, first select hello backup source.</span></span>
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    <span data-ttu-id="6ac7b-120">Olá **backup do aplicativo** opção mostra todos Olá backups existentes do aplicativo atual hello e você pode facilmente selecionar um.</span><span class="sxs-lookup"><span data-stu-id="6ac7b-120">hello **App backup** option shows you all hello existing backups of hello current app, and you can easily select one.</span></span>
    <span data-ttu-id="6ac7b-121">Olá **armazenamento** opção permite selecionar qualquer arquivo ZIP de backup de qualquer conta de armazenamento do Azure e o contêiner na sua assinatura existente.</span><span class="sxs-lookup"><span data-stu-id="6ac7b-121">hello **Storage** option lets you select any backup ZIP file from any existing Azure Storage account and container in your subscription.</span></span>
    <span data-ttu-id="6ac7b-122">Se você estiver tentando toorestore um backup de outro aplicativo, use Olá **armazenamento** opção.</span><span class="sxs-lookup"><span data-stu-id="6ac7b-122">If you're trying toorestore a backup of another app, use hello **Storage** option.</span></span>
3. <span data-ttu-id="6ac7b-123">Em seguida, especifique o destino Olá Olá restauração dos aplicativos em **destino de restauração**.</span><span class="sxs-lookup"><span data-stu-id="6ac7b-123">Then, specify hello destination for hello app restore in **Restore destination**.</span></span>
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > <span data-ttu-id="6ac7b-124">Se você escolher **Substituir**, todos os dados existentes em seu aplicativo atual serão apagados e substituídos.</span><span class="sxs-lookup"><span data-stu-id="6ac7b-124">If you choose **Overwrite**, all existing data in your current app is erased and overwritten.</span></span> <span data-ttu-id="6ac7b-125">Antes de clicar em **Okey**, certifique-se de que ele é exatamente o que você deseja toodo.</span><span class="sxs-lookup"><span data-stu-id="6ac7b-125">Before you click **OK**, make sure that it is exactly what you want toodo.</span></span>
   > 
   > 
   
    <span data-ttu-id="6ac7b-126">Você pode selecionar **aplicativo existente** toorestore Olá aplicativo tooanother backup app Olá mesmo grupo de recurso.</span><span class="sxs-lookup"><span data-stu-id="6ac7b-126">You can select **Existing App** toorestore hello app backup tooanother app in hello same resoure group.</span></span> <span data-ttu-id="6ac7b-127">Antes de usar essa opção, você deve já ter criado outro aplicativo no seu grupo de recursos com o espelhamento de banco de dados configuração toohello definido no backup do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="6ac7b-127">Before you use this option, you should have already created another app in your resource group with mirroring database configuration toohello one defined in hello app backup.</span></span> <span data-ttu-id="6ac7b-128">Você também pode criar um **novo** aplicativo toorestore seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="6ac7b-128">You can also Create a **New** app toorestore your content to.</span></span>

4. <span data-ttu-id="6ac7b-129">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="6ac7b-129">Click **OK**.</span></span>

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a><span data-ttu-id="6ac7b-130">Baixar ou excluir um backup de uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="6ac7b-130">Download or delete a backup from a storage account</span></span>
1. <span data-ttu-id="6ac7b-131">De saudação principal **procurar** folha de saudação portal do Azure, selecione **contas de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="6ac7b-131">From hello main **Browse** blade of hello Azure portal, select **Storage accounts**.</span></span> <span data-ttu-id="6ac7b-132">Uma lista de suas contas de armazenamento existentes é exibida.</span><span class="sxs-lookup"><span data-stu-id="6ac7b-132">A list of your existing storage accounts is displayed.</span></span>
2. <span data-ttu-id="6ac7b-133">Selecione a conta de armazenamento de saudação que contém o backup Olá ser toodownload ou delete.hello folha Olá conta de armazenamento é exibida.</span><span class="sxs-lookup"><span data-stu-id="6ac7b-133">Select hello storage account that contains hello backup that you want toodownload or delete.hello blade for hello storage account is displayed.</span></span>
3. <span data-ttu-id="6ac7b-134">Na folha de conta de armazenamento hello, selecione o contêiner de saudação desejado</span><span class="sxs-lookup"><span data-stu-id="6ac7b-134">In hello storage account blade, select hello container you want</span></span>
   
    ![Exibir contêineres][ViewContainers]
4. <span data-ttu-id="6ac7b-136">Selecione o arquivo de backup você deseja toodownload ou excluir.</span><span class="sxs-lookup"><span data-stu-id="6ac7b-136">Select backup file you want toodownload or delete.</span></span>
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. <span data-ttu-id="6ac7b-138">Clique em **baixar** ou **excluir** dependendo do que você deseja toodo.</span><span class="sxs-lookup"><span data-stu-id="6ac7b-138">Click **Download** or **Delete** depending on what you want toodo.</span></span>  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a><span data-ttu-id="6ac7b-139">Monitorar uma operação de restauração</span><span class="sxs-lookup"><span data-stu-id="6ac7b-139">Monitor a restore operation</span></span>
<span data-ttu-id="6ac7b-140">toosee detalhes sobre o sucesso de saudação ou falha da operação de restauração do aplicativo hello, navegar toohello **Log de atividades** folha em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ac7b-140">toosee details about hello success or failure of hello app restore operation, navigate toohello **Activity Log** blade in hello Azure portal.</span></span>  
 

<span data-ttu-id="6ac7b-141">Role para baixo toofind Olá desejado restauração operação e clique em tooselect-lo.</span><span class="sxs-lookup"><span data-stu-id="6ac7b-141">Scroll down toofind hello desired restore operation and click tooselect it.</span></span>

<span data-ttu-id="6ac7b-142">Olá detalhes folha exibe Olá informações disponíveis relacionadas toohello operação de restauração.</span><span class="sxs-lookup"><span data-stu-id="6ac7b-142">hello details blade displays hello available information related toohello restore operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ac7b-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6ac7b-143">Next Steps</span></span>
<span data-ttu-id="6ac7b-144">Você pode fazer backup e restaurar aplicativos de serviço de aplicativo usando a API REST (consulte [tooback de REST de uso de backup e restauração de aplicativos de serviço de aplicativo](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="6ac7b-144">You can backup and restore App Service apps using REST API (see [Use REST tooback up and restore App Service apps](websites-csm-backup.md)).</span></span>


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
