---
title: Fazer backup de seu aplicativo no Azure
description: "Saiba como criar backups de seus aplicativos no Serviço de Aplicativo do Azure."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 6223b6bd-84ec-48df-943f-461d84605694
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: 77e983afaaba8e944ab1f337e1c28ced83b63205
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="back-up-your-app-in-azure"></a><span data-ttu-id="35638-103">Fazer backup de seu aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="35638-103">Back up your app in Azure</span></span>
<span data-ttu-id="35638-104">O recurso de Backup e Restauração no [Serviço de Aplicativo do Azure](../app-service/app-service-value-prop-what-is.md) permite que você crie backups de aplicativos facilmente, de modo manual ou agendado.</span><span class="sxs-lookup"><span data-stu-id="35638-104">The Back up and Restore feature in [Azure App Service](../app-service/app-service-value-prop-what-is.md) lets you easily create app backups manually or on a schedule.</span></span> <span data-ttu-id="35638-105">Você pode restaurar o aplicativo em um instantâneo de um estado anterior, substituindo o aplicativo existente ou restaurando em outro aplicativo.</span><span class="sxs-lookup"><span data-stu-id="35638-105">You can restore the app to a snapshot of a previous state by overwriting the existing app or restoring to another app.</span></span> 

<span data-ttu-id="35638-106">Para obter informações sobre como restaurar um aplicativo por um backup, veja [Restaurar um aplicativo no Serviço de Aplicativo do Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="35638-106">For information on restoring an app from backup, see [Restore an app in Azure](web-sites-restore.md).</span></span>

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a><span data-ttu-id="35638-107">Do que é feito backup</span><span class="sxs-lookup"><span data-stu-id="35638-107">What gets backed up</span></span>
<span data-ttu-id="35638-108">O Serviço de Aplicativo pode fazer backup das seguintes em uma conta de armazenamento do Azure e um contêiner que você configurou para uso de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="35638-108">App Service can backup the following information to an Azure storage account and container that you have configured your app to use.</span></span> 

* <span data-ttu-id="35638-109">Configuração do aplicativo</span><span class="sxs-lookup"><span data-stu-id="35638-109">App configuration</span></span>
* <span data-ttu-id="35638-110">Conteúdo do arquivo</span><span class="sxs-lookup"><span data-stu-id="35638-110">File content</span></span>
* <span data-ttu-id="35638-111">Banco de dados conectado ao seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="35638-111">Database connected to your app</span></span>

<span data-ttu-id="35638-112">As soluções de banco de dados a seguir são compatíveis com o recurso de backup:</span><span class="sxs-lookup"><span data-stu-id="35638-112">The following database solutions are supported with backup feature:</span></span> 
   - [<span data-ttu-id="35638-113">Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="35638-113">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
   - [<span data-ttu-id="35638-114">Banco de Dados do Azure para MySQL (Visualização)</span><span class="sxs-lookup"><span data-stu-id="35638-114">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
   - [<span data-ttu-id="35638-115">Banco de Dados do Azure para PostgreSQL (Visualização)</span><span class="sxs-lookup"><span data-stu-id="35638-115">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
   - [<span data-ttu-id="35638-116">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="35638-116">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
   - [<span data-ttu-id="35638-117">MySQL no aplicativo</span><span class="sxs-lookup"><span data-stu-id="35638-117">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)
 

> [!NOTE]
>  <span data-ttu-id="35638-118">Cada backup é uma cópia offline completa do aplicativo, não uma atualização incremental.</span><span class="sxs-lookup"><span data-stu-id="35638-118">Each backup is a complete offline copy of your app, not an incremental update.</span></span>
>  

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a><span data-ttu-id="35638-119">Requisitos e restrições</span><span class="sxs-lookup"><span data-stu-id="35638-119">Requirements and restrictions</span></span>
* <span data-ttu-id="35638-120">O recurso de Backup e Restauração exige que o plano do Serviço de Aplicativo esteja na camada **Standard** ou **Premium**.</span><span class="sxs-lookup"><span data-stu-id="35638-120">The Back up and Restore feature requires the App Service plan to be in the **Standard** tier or **Premium** tier.</span></span> <span data-ttu-id="35638-121">Para obter mais informações sobre como dimensionar seu plano do Serviço de Aplicativo para usar uma camada superior, veja [Escalar verticalmente um aplicativo Web no Serviço de Aplicativo do Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="35638-121">For more information about scaling your App Service plan to use a higher tier, see [Scale up an app in Azure](web-sites-scale.md).</span></span>  
  <span data-ttu-id="35638-122">A camada **Premium** permite um número maior de backups diários do que a camada **Standard**.</span><span class="sxs-lookup"><span data-stu-id="35638-122">**Premium** tier allows a greater number of daily back ups than **Standard** tier.</span></span>
* <span data-ttu-id="35638-123">Você precisa de uma conta de armazenamento do Azure e do contêiner na mesma assinatura do aplicativo do qual você deseja fazer backup.</span><span class="sxs-lookup"><span data-stu-id="35638-123">You need an Azure storage account and container in the same subscription as the app that you want to backup.</span></span> <span data-ttu-id="35638-124">Para obter mais informações sobre contas de armazenamento do Azure, consulte os [links](#moreaboutstorage) no final deste artigo.</span><span class="sxs-lookup"><span data-stu-id="35638-124">For more information on Azure storage accounts, see the [links](#moreaboutstorage) at the end of this article.</span></span>
* <span data-ttu-id="35638-125">Backups podem ter até 10 GB de conteúdo do aplicativo e do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="35638-125">Backups can be up to 10 GB of app and database content.</span></span> <span data-ttu-id="35638-126">Se o tamanho do backup ultrapassar esse limite, você receberá um erro.</span><span class="sxs-lookup"><span data-stu-id="35638-126">If the backup size exceeds this limit, you get an error .</span></span>

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a><span data-ttu-id="35638-127">Criar um backup manual</span><span class="sxs-lookup"><span data-stu-id="35638-127">Create a manual backup</span></span>
1. <span data-ttu-id="35638-128">No [Portal do Azure](https://portal.azure.com), navegue até a folha do aplicativo, selecione **Backups**.</span><span class="sxs-lookup"><span data-stu-id="35638-128">In the [Azure Portal](https://portal.azure.com), navigate to your app's blade, select **Backups**.</span></span> <span data-ttu-id="35638-129">A folha **Backups** será exibida.</span><span class="sxs-lookup"><span data-stu-id="35638-129">The **Backups** blade will be displayed.</span></span>
   
    ![Página Backups][ChooseBackupsPage]
   
   > [!NOTE]
   > <span data-ttu-id="35638-131">Se você receber a mensagem abaixo, clique nela para atualizar seu plano do Serviço de Aplicativo antes de continuar com os backups.</span><span class="sxs-lookup"><span data-stu-id="35638-131">If you see the message below, click it to upgrade your App Service plan before you can proceed with backups.</span></span>
   > <span data-ttu-id="35638-132">Veja [Escalar verticalmente um aplicativo no Azure](web-sites-scale.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="35638-132">See [Scale up an app in Azure](web-sites-scale.md) for more information.</span></span>  
   > <span data-ttu-id="35638-133">![Escolher uma conta de armazenamento](./media/web-sites-backup/01UpgradePlan1.png)</span><span class="sxs-lookup"><span data-stu-id="35638-133">![Choose storage account](./media/web-sites-backup/01UpgradePlan1.png)</span></span>
   > 
   > 

2. <span data-ttu-id="35638-134">Na folha de **Backup**, clique em **Configurar**
![Clique em Configurar](./media/web-sites-backup/ClickConfigure1.png)</span><span class="sxs-lookup"><span data-stu-id="35638-134">In the **Backup** blade, Click **Configure**
![Click Configure](./media/web-sites-backup/ClickConfigure1.png)</span></span>
3. <span data-ttu-id="35638-135">Na folha **Configuração de Backup**, clique em **Armazenamento: não configurado** para configurar uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="35638-135">In the **Backup Configuration** blade, click **Storage: Not configured** to configure a storage account.</span></span>
   
    ![Escolher uma conta de armazenamento][ChooseStorageAccount]
4. <span data-ttu-id="35638-137">Escolha o destino de seu backup selecionando uma **Conta de Armazenamento** e um **Contêiner**.</span><span class="sxs-lookup"><span data-stu-id="35638-137">Choose your backup destination by selecting a **Storage Account** and **Container**.</span></span> <span data-ttu-id="35638-138">A conta de armazenamento deve pertencer à mesma assinatura do aplicativo do qual você deseja fazer backup.</span><span class="sxs-lookup"><span data-stu-id="35638-138">The storage account must belong to the same subscription as the app you want to back up.</span></span> <span data-ttu-id="35638-139">Se desejar, você pode criar uma nova conta de armazenamento ou um novo contêiner nas respectivas folhas.</span><span class="sxs-lookup"><span data-stu-id="35638-139">If you wish, you can create a new storage account or a new container in the respective blades.</span></span> <span data-ttu-id="35638-140">Quando terminar, clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="35638-140">When you're done, click **Select**.</span></span>
   
    ![Escolher uma conta de armazenamento](./media/web-sites-backup/02ChooseStorageAccount1-1.png)
5. <span data-ttu-id="35638-142">Na folha **Configuração de Backup** que ainda está aberta, você pode configurar o **Banco de Dados de Backup**, selecione os bancos de dados que deseja incluir nos backups (banco de dados SQL ou MySQL) e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="35638-142">In the **Backup Configuration** blade that is still left open, you can configure **Backup Database**, then select the databases you want to include in the backups (SQL database or MySQL), then click **OK**.</span></span>  
   
    ![Escolher uma conta de armazenamento](./media/web-sites-backup/03ConfigureDatabase1.png)
   
   > [!NOTE]
   > <span data-ttu-id="35638-144">Para que um banco de dados apareça nessa lista, sua cadeia de conexão deve existir na seção **Cadeias de conexão** da folha **Configurações do aplicativo** do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="35638-144">For a database to appear in this list, its connection string must exist in the **Connection strings** section of the **Application settings** blade for your app.</span></span>
   > 
   > 
6. <span data-ttu-id="35638-145">Na folha **Configuração de Backup**, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="35638-145">In the **Backup Configuration** blade, click **Save**.</span></span>    
7. <span data-ttu-id="35638-146">Na folha de **Backups**, clique em **Backup**.</span><span class="sxs-lookup"><span data-stu-id="35638-146">In the  **Backups** blade, click **Backup**.</span></span>
   
    ![Botão BackUpNow][BackUpNow]
   
    <span data-ttu-id="35638-148">Você verá uma mensagem informando o andamento do processo de backup.</span><span class="sxs-lookup"><span data-stu-id="35638-148">You see a progress message during the backup process.</span></span>

<span data-ttu-id="35638-149">Após a configuração da conta de armazenamento e do contêiner, você poderá iniciar um backup manual a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="35638-149">Once the storage account and container is configured you can initiate a manual backup at any time.</span></span>  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a><span data-ttu-id="35638-150">Configurar backups automáticos</span><span class="sxs-lookup"><span data-stu-id="35638-150">Configure automated backups</span></span>
1. <span data-ttu-id="35638-151">Na folha de **Configuração de Backup**, defina **Backup Agendado** para **Ativado**.</span><span class="sxs-lookup"><span data-stu-id="35638-151">In the **Backup Configuration** blade, set **Scheduled backup** to **On**.</span></span> 
   
    ![Escolher uma conta de armazenamento](./media/web-sites-backup/05ScheduleBackup1.png)
2. <span data-ttu-id="35638-153">Opções de Agendamento de Backups serão exibidas, defina **Backup Agendado** para **Ativado**, configure o agendamento de backup conforme desejado e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="35638-153">Backup schedule options will show up, set **Scheduled Backup** to **On**, then configure the backup schedule as desired and click **OK**.</span></span>
   
    ![Habilitar backups automatizados][SetAutomatedBackupOn]

<a name="partialbackups"></a>

## <a name="configure-partial-backups"></a><span data-ttu-id="35638-155">Configurar backups parciais</span><span class="sxs-lookup"><span data-stu-id="35638-155">Configure Partial Backups</span></span>
<span data-ttu-id="35638-156">Às vezes, você não quer fazer backup de tudo em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="35638-156">Sometimes you don't want to backup everything on your app.</span></span> <span data-ttu-id="35638-157">Veja alguns exemplos:</span><span class="sxs-lookup"><span data-stu-id="35638-157">Here are a few examples:</span></span>

* <span data-ttu-id="35638-158">Você [configura backups semanais](web-sites-backup.md#configure-automated-backups) do aplicativo que contém conteúdo estático que nunca muda, como imagens ou postagens antigas no blog.</span><span class="sxs-lookup"><span data-stu-id="35638-158">You [set up weekly backups](web-sites-backup.md#configure-automated-backups) of your app that contains static content that never changes, such as old blog posts or images.</span></span>
* <span data-ttu-id="35638-159">Seu aplicativo tem mais de 10 GB de conteúdo (que é o volume máximo de backup por vez).</span><span class="sxs-lookup"><span data-stu-id="35638-159">Your app has over 10 GB of content (that's the max amount you can backup at a time).</span></span>
* <span data-ttu-id="35638-160">Você não deseja fazer backup dos arquivos de log.</span><span class="sxs-lookup"><span data-stu-id="35638-160">You don't want to backup the log files.</span></span>

<span data-ttu-id="35638-161">Os backups parciais permitem que você escolha exatamente quais arquivos deseja incluir no backup.</span><span class="sxs-lookup"><span data-stu-id="35638-161">Partial backups allows you choose exactly which files you want to backup.</span></span>

### <a name="exclude-files-from-your-backup"></a><span data-ttu-id="35638-162">Excluir arquivos do backup</span><span class="sxs-lookup"><span data-stu-id="35638-162">Exclude files from your backup</span></span>
<span data-ttu-id="35638-163">Vamos supor que você tenha um aplicativo que contém arquivos de log e imagens estáticas que passaram por backup e não vão mais sofrer alteração.</span><span class="sxs-lookup"><span data-stu-id="35638-163">Suppose you have an app that contains log files and static images that have been backup once and are not going to change.</span></span> <span data-ttu-id="35638-164">Nesses casos, você pode excluir a exclusão desses arquivos e pastas em backups futuros.</span><span class="sxs-lookup"><span data-stu-id="35638-164">In such cases you can exclude those folders and files from being stored in your future backups.</span></span> <span data-ttu-id="35638-165">Para excluir arquivos e pastas de seus backups, crie um arquivo `_backup.filter` na pasta `D:\home\site\wwwroot` de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="35638-165">To exclude files and folders from your backups, create a `_backup.filter` file in the `D:\home\site\wwwroot` folder of your app.</span></span> <span data-ttu-id="35638-166">Especifique a lista de arquivos e pastas que você excluir deste arquivo.</span><span class="sxs-lookup"><span data-stu-id="35638-166">Specify the list of files and folders you want to exclude in this file.</span></span> 

<span data-ttu-id="35638-167">Uma maneira fácil de acessar seus arquivos é usando o Kudu.</span><span class="sxs-lookup"><span data-stu-id="35638-167">An easy way to access your files is to use Kudu .</span></span> <span data-ttu-id="35638-168">Clique na configuração **Ferramentas Avançadas-> Ir** em seu aplicativo Web para acessar o Kudu.</span><span class="sxs-lookup"><span data-stu-id="35638-168">Click **Advanced Tools -> Go** setting for your web app to access Kudu.</span></span>

![Kudu usando o Portal][kudu-portal]

<span data-ttu-id="35638-170">Identifique as pastas que você quer excluir de seus backups.</span><span class="sxs-lookup"><span data-stu-id="35638-170">Identify the folders that you want to exclude from your backups.</span></span>  <span data-ttu-id="35638-171">Por exemplo, você quer filtrar e remover os arquivos e pastas realçados.</span><span class="sxs-lookup"><span data-stu-id="35638-171">For example , you want to filter out the highlighted folder and files.</span></span>

![Pasta Imagens][ImagesFolder]

<span data-ttu-id="35638-173">Crie um arquivo chamado `_backup.filter` e coloque a lista acima no arquivo, mas remova `D:\home`.</span><span class="sxs-lookup"><span data-stu-id="35638-173">Create a file called `_backup.filter` and put the list above in the file, but remove `D:\home`.</span></span> <span data-ttu-id="35638-174">Liste um diretório ou arquivo por linha.</span><span class="sxs-lookup"><span data-stu-id="35638-174">List one directory or file per line.</span></span> <span data-ttu-id="35638-175">Portanto, o conteúdo do arquivo deve ser:</span><span class="sxs-lookup"><span data-stu-id="35638-175">So the content of the file should be:</span></span>
 ```bash
    \site\wwwroot\Images\brand.png
    \site\wwwroot\Images\2014
    \site\wwwroot\Images\2013
```

<span data-ttu-id="35638-176">Carregue o arquivo `_backup.filter` no diretório `D:\home\site\wwwroot\` de seu site usando o [ftp](web-sites-deploy.md#ftp) ou qualquer outro método.</span><span class="sxs-lookup"><span data-stu-id="35638-176">Upload `_backup.filter` file to the `D:\home\site\wwwroot\` directory of your site using [ftp](web-sites-deploy.md#ftp) or any other method.</span></span> <span data-ttu-id="35638-177">Se quiser, você pode criar o arquivo diretamente usando Kudu `DebugConsole` e inserir o conteúdo nesse local.</span><span class="sxs-lookup"><span data-stu-id="35638-177">If you wish, you can create the file directly using Kudu  `DebugConsole` and insert the content there.</span></span>

<span data-ttu-id="35638-178">Execute backups da mesma maneira que faria normalmente, de modo [manual](#create-a-manual-backup) ou [automático](#configure-automated-backups).</span><span class="sxs-lookup"><span data-stu-id="35638-178">Run backups the same way you would normally do it, [manually](#create-a-manual-backup) or [automatically](#configure-automated-backups).</span></span> <span data-ttu-id="35638-179">Agora, quaisquer arquivos e pastas especificados em `_backup.filter` serão excluídos dos backups futuros agendados ou iniciados manualmente.</span><span class="sxs-lookup"><span data-stu-id="35638-179">Now, any files and folders that are specified in `_backup.filter` is excluded from the future backups scheduled or manually initiated.</span></span> 

> [!NOTE]
> <span data-ttu-id="35638-180">Você restaura backups parciais de seu site da mesma maneira como [restauraria um backup regular](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="35638-180">You restore partial backups of your site the same way you would [restore a regular backup](web-sites-restore.md).</span></span> <span data-ttu-id="35638-181">O processo de restauração faz a coisa certa.</span><span class="sxs-lookup"><span data-stu-id="35638-181">The restore process does the right thing.</span></span>
> 
> <span data-ttu-id="35638-182">Quando um backup completo é restaurado, todo o conteúdo do site é substituído por tudo o que está no backup.</span><span class="sxs-lookup"><span data-stu-id="35638-182">When a full backup is restored, all content on the site is replaced with whatever is in the backup.</span></span> <span data-ttu-id="35638-183">Se um arquivo estiver no site mas não no backup, será excluído.</span><span class="sxs-lookup"><span data-stu-id="35638-183">If a file is on the site, but not in the backup it gets deleted.</span></span> <span data-ttu-id="35638-184">Mas, quando um backup parcial é restaurado, qualquer conteúdo que esteja localizado em um dos diretórios não autorizados ou qualquer arquivo não autorizado, é deixado como está.</span><span class="sxs-lookup"><span data-stu-id="35638-184">But when a partial backup is restored, any content that is located in one of the blacklisted directories, or any blacklisted file, is left as is.</span></span>
> 


<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a><span data-ttu-id="35638-185">Como os backups são armazenados</span><span class="sxs-lookup"><span data-stu-id="35638-185">How backups are stored</span></span>
<span data-ttu-id="35638-186">Depois de criar um ou mais backups para seu aplicativo, os backups ficam visíveis na folha **Contêineres** de sua conta de armazenamento, bem como em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="35638-186">After you have made one or more backups for your app, the backups are visible on the **Containers** blade of your storage account, and your app.</span></span> <span data-ttu-id="35638-187">Na conta de armazenamento, cada backup é formado por um arquivo `.zip` que contém os dados de backup e um arquivo `.xml` que contém um manifesto do conteúdo do arquivo `.zip`.</span><span class="sxs-lookup"><span data-stu-id="35638-187">In the storage account, each backup consists of a`.zip` file that contains the backup data and an `.xml` file that contains a manifest of the `.zip` file contents.</span></span> <span data-ttu-id="35638-188">Será possível descompactar e procurar esses arquivos se você quiser acessar seus backups sem realmente executar uma restauração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="35638-188">You can unzip and browse these files if you want to access your backups without actually performing an app restore.</span></span>

<span data-ttu-id="35638-189">O backup de banco de dados do aplicativo é armazenado na raiz do arquivo .zip.</span><span class="sxs-lookup"><span data-stu-id="35638-189">The database backup for the app is stored in the root of the.zip file.</span></span> <span data-ttu-id="35638-190">Para um banco de dados SQL, este é um arquivo BACPAC (sem extensão de arquivo) e pode ser importado.</span><span class="sxs-lookup"><span data-stu-id="35638-190">For a SQL database, this is a BACPAC file (no file extension) and can be imported.</span></span> <span data-ttu-id="35638-191">Para criar um banco de dados SQL com base na exportação do BACPAC, veja [Importar um arquivo BACPAC para criar um novo banco de dados de usuário](http://technet.microsoft.com/library/hh710052.aspx).</span><span class="sxs-lookup"><span data-stu-id="35638-191">To create a SQL database based on the BACPAC export, see [Import a BACPAC File to Create a New User Database](http://technet.microsoft.com/library/hh710052.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="35638-192">A alteração de qualquer um dos arquivos no contêiner **websitebackups** pode fazer com que o backup se torne inválido e, portanto, não restaurável.</span><span class="sxs-lookup"><span data-stu-id="35638-192">Altering any of the files in your **websitebackups** container can cause the backup to become invalid and therefore non-restorable.</span></span>
> 
> 

<a name="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="35638-193">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="35638-193">Next Steps</span></span>
<span data-ttu-id="35638-194">Para obter informações sobre como restaurar um aplicativo por um backup, veja [Restaurar um aplicativo no Serviço de Aplicativo do Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="35638-194">For information on restoring an app from a backup, see [Restore an app in Azure](web-sites-restore.md).</span></span> <span data-ttu-id="35638-195">Você também pode fazer backup e restaurar aplicativos do Serviço de Aplicativo usando a API REST (veja [Usar a REST para fazer backup e restaurar aplicativos do Serviço de Aplicativo](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="35638-195">You can also backup and restore App Service apps using REST API (see [Use REST to backup and restore App Service apps](websites-csm-backup.md)).</span></span>


<!-- IMAGES -->
[ChooseBackupsPage]: ./media/web-sites-backup/01ChooseBackupsPage1.png
[ChooseStorageAccount]: ./media/web-sites-backup/02ChooseStorageAccount-1.png
[IncludedDatabases]: ./media/web-sites-backup/03IncludedDatabases.png
[BackUpNow]: ./media/web-sites-backup/04BackUpNow1.png
[BackupProgress]: ./media/web-sites-backup/05BackupProgress.png
[SetAutomatedBackupOn]: ./media/web-sites-backup/06SetAutomatedBackupOn1.png
[Frequency]: ./media/web-sites-backup/07Frequency.png
[StartDate]: ./media/web-sites-backup/08StartDate.png
[StartTime]: ./media/web-sites-backup/09StartTime.png
[SaveIcon]: ./media/web-sites-backup/10SaveIcon.png
[ImagesFolder]: ./media/web-sites-backup/11Images.png
[LogsFolder]: ./media/web-sites-backup/12Logs.png
[GhostUpgradeWarning]: ./media/web-sites-backup/13GhostUpgradeWarning.png
[kudu-portal]:./media/web-sites-backup/kudu-portal.PNG

