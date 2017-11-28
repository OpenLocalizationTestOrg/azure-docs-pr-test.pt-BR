---
title: aaaBack backup de seu aplicativo no Azure
description: "Saiba como toocreate backups de seus aplicativos no serviço de aplicativo do Azure."
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
ms.openlocfilehash: e41d93d322bbc48b45b28eeaa817928d83c2b9d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-your-app-in-azure"></a><span data-ttu-id="ba703-103">Fazer backup de seu aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="ba703-103">Back up your app in Azure</span></span>
<span data-ttu-id="ba703-104">Olá fazer backup e restaurar o recurso no [do serviço de aplicativo do Azure](../app-service/app-service-value-prop-what-is.md) permite que você crie facilmente os backups de aplicativos manualmente ou em uma agenda.</span><span class="sxs-lookup"><span data-stu-id="ba703-104">hello Back up and Restore feature in [Azure App Service](../app-service/app-service-value-prop-what-is.md) lets you easily create app backups manually or on a schedule.</span></span> <span data-ttu-id="ba703-105">Você pode restaurar o instantâneo de tooa aplicativo hello de um estado anterior por sobrescrever app existente de saudação ou restauração tooanother.</span><span class="sxs-lookup"><span data-stu-id="ba703-105">You can restore hello app tooa snapshot of a previous state by overwriting hello existing app or restoring tooanother app.</span></span> 

<span data-ttu-id="ba703-106">Para obter informações sobre como restaurar um aplicativo por um backup, veja [Restaurar um aplicativo no Serviço de Aplicativo do Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="ba703-106">For information on restoring an app from backup, see [Restore an app in Azure](web-sites-restore.md).</span></span>

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a><span data-ttu-id="ba703-107">Do que é feito backup</span><span class="sxs-lookup"><span data-stu-id="ba703-107">What gets backed up</span></span>
<span data-ttu-id="ba703-108">Serviço de aplicativo pode fazer o backup do seguinte Olá conta de armazenamento do Azure tooan informações e contêiner que você tenha configurado toouse seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ba703-108">App Service can backup hello following information tooan Azure storage account and container that you have configured your app toouse.</span></span> 

* <span data-ttu-id="ba703-109">Configuração do aplicativo</span><span class="sxs-lookup"><span data-stu-id="ba703-109">App configuration</span></span>
* <span data-ttu-id="ba703-110">Conteúdo do arquivo</span><span class="sxs-lookup"><span data-stu-id="ba703-110">File content</span></span>
* <span data-ttu-id="ba703-111">Banco de dados conectado tooyour aplicativo</span><span class="sxs-lookup"><span data-stu-id="ba703-111">Database connected tooyour app</span></span>

<span data-ttu-id="ba703-112">Olá soluções de banco de dados a seguir têm suporte com o recurso de backup:</span><span class="sxs-lookup"><span data-stu-id="ba703-112">hello following database solutions are supported with backup feature:</span></span> 
   - [<span data-ttu-id="ba703-113">Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="ba703-113">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
   - [<span data-ttu-id="ba703-114">Banco de Dados do Azure para MySQL (Visualização)</span><span class="sxs-lookup"><span data-stu-id="ba703-114">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
   - [<span data-ttu-id="ba703-115">Banco de Dados do Azure para PostgreSQL (Visualização)</span><span class="sxs-lookup"><span data-stu-id="ba703-115">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
   - [<span data-ttu-id="ba703-116">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="ba703-116">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
   - [<span data-ttu-id="ba703-117">MySQL no aplicativo</span><span class="sxs-lookup"><span data-stu-id="ba703-117">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)
 

> [!NOTE]
>  <span data-ttu-id="ba703-118">Cada backup é uma cópia offline completa do aplicativo, não uma atualização incremental.</span><span class="sxs-lookup"><span data-stu-id="ba703-118">Each backup is a complete offline copy of your app, not an incremental update.</span></span>
>  

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a><span data-ttu-id="ba703-119">Requisitos e restrições</span><span class="sxs-lookup"><span data-stu-id="ba703-119">Requirements and restrictions</span></span>
* <span data-ttu-id="ba703-120">Olá fazer backup e o recurso de restauração requer Olá toobe do plano de serviço de aplicativo no hello **padrão** camada ou **Premium** camada.</span><span class="sxs-lookup"><span data-stu-id="ba703-120">hello Back up and Restore feature requires hello App Service plan toobe in hello **Standard** tier or **Premium** tier.</span></span> <span data-ttu-id="ba703-121">Para obter mais informações sobre como dimensionar seu plano de serviço de aplicativo toouse uma camada superior, consulte [dimensionar um aplicativo no Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="ba703-121">For more information about scaling your App Service plan toouse a higher tier, see [Scale up an app in Azure](web-sites-scale.md).</span></span>  
  <span data-ttu-id="ba703-122">A camada **Premium** permite um número maior de backups diários do que a camada **Standard**.</span><span class="sxs-lookup"><span data-stu-id="ba703-122">**Premium** tier allows a greater number of daily back ups than **Standard** tier.</span></span>
* <span data-ttu-id="ba703-123">Você precisa de uma conta de armazenamento do Azure e o contêiner no hello mesma assinatura que você deseja toobackup de aplicativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ba703-123">You need an Azure storage account and container in hello same subscription as hello app that you want toobackup.</span></span> <span data-ttu-id="ba703-124">Para obter mais informações sobre contas de armazenamento do Azure, consulte Olá [links](#moreaboutstorage) final Olá deste artigo.</span><span class="sxs-lookup"><span data-stu-id="ba703-124">For more information on Azure storage accounts, see hello [links](#moreaboutstorage) at hello end of this article.</span></span>
* <span data-ttu-id="ba703-125">Backups podem ser a too10 GB de conteúdo do aplicativo e banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ba703-125">Backups can be up too10 GB of app and database content.</span></span> <span data-ttu-id="ba703-126">Se o tamanho do backup Olá exceder esse limite, você receberá um erro.</span><span class="sxs-lookup"><span data-stu-id="ba703-126">If hello backup size exceeds this limit, you get an error .</span></span>

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a><span data-ttu-id="ba703-127">Criar um backup manual</span><span class="sxs-lookup"><span data-stu-id="ba703-127">Create a manual backup</span></span>
1. <span data-ttu-id="ba703-128">Em Olá [Portal do Azure](https://portal.azure.com), navegue folha tooyour do aplicativo, selecione **Backups**.</span><span class="sxs-lookup"><span data-stu-id="ba703-128">In hello [Azure Portal](https://portal.azure.com), navigate tooyour app's blade, select **Backups**.</span></span> <span data-ttu-id="ba703-129">Olá **Backups** folha será exibida.</span><span class="sxs-lookup"><span data-stu-id="ba703-129">hello **Backups** blade will be displayed.</span></span>
   
    ![Página Backups][ChooseBackupsPage]
   
   > [!NOTE]
   > <span data-ttu-id="ba703-131">Se você vir a mensagem de saudação abaixo, clique nele tooupgrade seu plano de serviço de aplicativo antes de prosseguir com backups.</span><span class="sxs-lookup"><span data-stu-id="ba703-131">If you see hello message below, click it tooupgrade your App Service plan before you can proceed with backups.</span></span>
   > <span data-ttu-id="ba703-132">Veja [Escalar verticalmente um aplicativo no Azure](web-sites-scale.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="ba703-132">See [Scale up an app in Azure](web-sites-scale.md) for more information.</span></span>  
   > <span data-ttu-id="ba703-133">![Escolher uma conta de armazenamento](./media/web-sites-backup/01UpgradePlan1.png)</span><span class="sxs-lookup"><span data-stu-id="ba703-133">![Choose storage account](./media/web-sites-backup/01UpgradePlan1.png)</span></span>
   > 
   > 

2. <span data-ttu-id="ba703-134">Em Olá **Backup** folha, clique em **configurar**
![clique em configurar](./media/web-sites-backup/ClickConfigure1.png)</span><span class="sxs-lookup"><span data-stu-id="ba703-134">In hello **Backup** blade, Click **Configure**
![Click Configure](./media/web-sites-backup/ClickConfigure1.png)</span></span>
3. <span data-ttu-id="ba703-135">Em Olá **configuração de Backup** folha, clique em **armazenamento: não configurado** tooconfigure uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ba703-135">In hello **Backup Configuration** blade, click **Storage: Not configured** tooconfigure a storage account.</span></span>
   
    ![Escolher uma conta de armazenamento][ChooseStorageAccount]
4. <span data-ttu-id="ba703-137">Escolha o destino de seu backup selecionando uma **Conta de Armazenamento** e um **Contêiner**.</span><span class="sxs-lookup"><span data-stu-id="ba703-137">Choose your backup destination by selecting a **Storage Account** and **Container**.</span></span> <span data-ttu-id="ba703-138">conta de armazenamento Olá deve pertencer toohello mesma assinatura que o aplicativo hello desejar tooback.</span><span class="sxs-lookup"><span data-stu-id="ba703-138">hello storage account must belong toohello same subscription as hello app you want tooback up.</span></span> <span data-ttu-id="ba703-139">Se desejar, você pode criar uma nova conta de armazenamento ou um novo contêiner folhas respectivos hello.</span><span class="sxs-lookup"><span data-stu-id="ba703-139">If you wish, you can create a new storage account or a new container in hello respective blades.</span></span> <span data-ttu-id="ba703-140">Quando terminar, clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="ba703-140">When you're done, click **Select**.</span></span>
   
    ![Escolher uma conta de armazenamento](./media/web-sites-backup/02ChooseStorageAccount1-1.png)
5. <span data-ttu-id="ba703-142">Em Olá **configuração de Backup** folha que for deixada aberta, você pode configurar **banco de dados de Backup**, em seguida, selecione os bancos de dados de saudação desejado tooinclude nos backups de saudação (banco de dados SQL ou MySQL) e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="ba703-142">In hello **Backup Configuration** blade that is still left open, you can configure **Backup Database**, then select hello databases you want tooinclude in hello backups (SQL database or MySQL), then click **OK**.</span></span>  
   
    ![Escolher uma conta de armazenamento](./media/web-sites-backup/03ConfigureDatabase1.png)
   
   > [!NOTE]
   > <span data-ttu-id="ba703-144">Para um tooappear de banco de dados nessa lista, sua cadeia de caracteres de conexão deve existir no hello **cadeias de caracteres de Conexão** seção Olá **configurações de aplicativo** folha para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ba703-144">For a database tooappear in this list, its connection string must exist in hello **Connection strings** section of hello **Application settings** blade for your app.</span></span>
   > 
   > 
6. <span data-ttu-id="ba703-145">Em Olá **configuração de Backup** folha, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="ba703-145">In hello **Backup Configuration** blade, click **Save**.</span></span>    
7. <span data-ttu-id="ba703-146">Em Olá **Backups** folha, clique em **Backup**.</span><span class="sxs-lookup"><span data-stu-id="ba703-146">In hello  **Backups** blade, click **Backup**.</span></span>
   
    ![Botão BackUpNow][BackUpNow]
   
    <span data-ttu-id="ba703-148">Você verá uma mensagem de progresso durante o processo de backup hello.</span><span class="sxs-lookup"><span data-stu-id="ba703-148">You see a progress message during hello backup process.</span></span>

<span data-ttu-id="ba703-149">Depois da configuração do contêiner e a conta de armazenamento hello, você pode iniciar um backup manual a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="ba703-149">Once hello storage account and container is configured you can initiate a manual backup at any time.</span></span>  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a><span data-ttu-id="ba703-150">Configurar backups automáticos</span><span class="sxs-lookup"><span data-stu-id="ba703-150">Configure automated backups</span></span>
1. <span data-ttu-id="ba703-151">Em Olá **configuração de Backup** folha, defina **backup agendado** muito**em**.</span><span class="sxs-lookup"><span data-stu-id="ba703-151">In hello **Backup Configuration** blade, set **Scheduled backup** too**On**.</span></span> 
   
    ![Escolher uma conta de armazenamento](./media/web-sites-backup/05ScheduleBackup1.png)
2. <span data-ttu-id="ba703-153">Definir opções de serão exibida, agendamento de backup **Backup agendado** muito**na**, em seguida, configurar o agendamento de backup Olá conforme desejado e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="ba703-153">Backup schedule options will show up, set **Scheduled Backup** too**On**, then configure hello backup schedule as desired and click **OK**.</span></span>
   
    ![Habilitar backups automatizados][SetAutomatedBackupOn]

<a name="partialbackups"></a>

## <a name="configure-partial-backups"></a><span data-ttu-id="ba703-155">Configurar backups parciais</span><span class="sxs-lookup"><span data-stu-id="ba703-155">Configure Partial Backups</span></span>
<span data-ttu-id="ba703-156">Às vezes, você não quer toobackup tudo em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ba703-156">Sometimes you don't want toobackup everything on your app.</span></span> <span data-ttu-id="ba703-157">Veja alguns exemplos:</span><span class="sxs-lookup"><span data-stu-id="ba703-157">Here are a few examples:</span></span>

* <span data-ttu-id="ba703-158">Você [configura backups semanais](web-sites-backup.md#configure-automated-backups) do aplicativo que contém conteúdo estático que nunca muda, como imagens ou postagens antigas no blog.</span><span class="sxs-lookup"><span data-stu-id="ba703-158">You [set up weekly backups](web-sites-backup.md#configure-automated-backups) of your app that contains static content that never changes, such as old blog posts or images.</span></span>
* <span data-ttu-id="ba703-159">Seu aplicativo tem mais de 10 GB de conteúdo (que é o valor máximo hello, que você pode fazer backup de cada vez).</span><span class="sxs-lookup"><span data-stu-id="ba703-159">Your app has over 10 GB of content (that's hello max amount you can backup at a time).</span></span>
* <span data-ttu-id="ba703-160">Você não deseja que os arquivos de log Olá toobackup.</span><span class="sxs-lookup"><span data-stu-id="ba703-160">You don't want toobackup hello log files.</span></span>

<span data-ttu-id="ba703-161">Backups parciais permite que você escolha exatamente quais arquivos que você deseja toobackup.</span><span class="sxs-lookup"><span data-stu-id="ba703-161">Partial backups allows you choose exactly which files you want toobackup.</span></span>

### <a name="exclude-files-from-your-backup"></a><span data-ttu-id="ba703-162">Excluir arquivos do backup</span><span class="sxs-lookup"><span data-stu-id="ba703-162">Exclude files from your backup</span></span>
<span data-ttu-id="ba703-163">Suponha que você tenha um aplicativo que contém os arquivos de log e imagens estáticas que tenham sido backup uma vez e não serão toochange.</span><span class="sxs-lookup"><span data-stu-id="ba703-163">Suppose you have an app that contains log files and static images that have been backup once and are not going toochange.</span></span> <span data-ttu-id="ba703-164">Nesses casos, você pode excluir a exclusão desses arquivos e pastas em backups futuros.</span><span class="sxs-lookup"><span data-stu-id="ba703-164">In such cases you can exclude those folders and files from being stored in your future backups.</span></span> <span data-ttu-id="ba703-165">tooexclude arquivos e pastas de seus backups, criar um `_backup.filter` arquivo hello `D:\home\site\wwwroot` pasta do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ba703-165">tooexclude files and folders from your backups, create a `_backup.filter` file in hello `D:\home\site\wwwroot` folder of your app.</span></span> <span data-ttu-id="ba703-166">Especifica Olá lista de arquivos e pastas que você deseja tooexclude neste arquivo.</span><span class="sxs-lookup"><span data-stu-id="ba703-166">Specify hello list of files and folders you want tooexclude in this file.</span></span> 

<span data-ttu-id="ba703-167">Um tooaccess de maneira fácil seus arquivos é toouse Kudu.</span><span class="sxs-lookup"><span data-stu-id="ba703-167">An easy way tooaccess your files is toouse Kudu .</span></span> <span data-ttu-id="ba703-168">Clique em **ferramentas avançadas -> Go** configuração para seu aplicativo de web tooaccess Kudu.</span><span class="sxs-lookup"><span data-stu-id="ba703-168">Click **Advanced Tools -> Go** setting for your web app tooaccess Kudu.</span></span>

![Kudu usando o Portal][kudu-portal]

<span data-ttu-id="ba703-170">Identifica Olá pastas que você deseja tooexclude de seus backups.</span><span class="sxs-lookup"><span data-stu-id="ba703-170">Identify hello folders that you want tooexclude from your backups.</span></span>  <span data-ttu-id="ba703-171">Por exemplo, você deseja toofilter pasta realçado hello e arquivos.</span><span class="sxs-lookup"><span data-stu-id="ba703-171">For example , you want toofilter out hello highlighted folder and files.</span></span>

![Pasta Imagens][ImagesFolder]

<span data-ttu-id="ba703-173">Crie um arquivo chamado `_backup.filter` e colocar a lista de saudação acima no arquivo hello, mas remover `D:\home`.</span><span class="sxs-lookup"><span data-stu-id="ba703-173">Create a file called `_backup.filter` and put hello list above in hello file, but remove `D:\home`.</span></span> <span data-ttu-id="ba703-174">Liste um diretório ou arquivo por linha.</span><span class="sxs-lookup"><span data-stu-id="ba703-174">List one directory or file per line.</span></span> <span data-ttu-id="ba703-175">Então o conteúdo de saudação do arquivo hello deve ser:</span><span class="sxs-lookup"><span data-stu-id="ba703-175">So hello content of hello file should be:</span></span>
 ```bash
    \site\wwwroot\Images\brand.png
    \site\wwwroot\Images\2014
    \site\wwwroot\Images\2013
```

<span data-ttu-id="ba703-176">Carregar `_backup.filter` arquivo toohello `D:\home\site\wwwroot\` diretório de seu site usando [ftp](web-sites-deploy.md#ftp) ou qualquer outro método.</span><span class="sxs-lookup"><span data-stu-id="ba703-176">Upload `_backup.filter` file toohello `D:\home\site\wwwroot\` directory of your site using [ftp](web-sites-deploy.md#ftp) or any other method.</span></span> <span data-ttu-id="ba703-177">Se desejar, você pode criar o arquivo hello diretamente usando Kudu `DebugConsole` e inserir seu conteúdo hello.</span><span class="sxs-lookup"><span data-stu-id="ba703-177">If you wish, you can create hello file directly using Kudu  `DebugConsole` and insert hello content there.</span></span>

<span data-ttu-id="ba703-178">Executar backups Olá mesmo como você faria normalmente, [manualmente](#create-a-manual-backup) ou [automaticamente](#configure-automated-backups).</span><span class="sxs-lookup"><span data-stu-id="ba703-178">Run backups hello same way you would normally do it, [manually](#create-a-manual-backup) or [automatically](#configure-automated-backups).</span></span> <span data-ttu-id="ba703-179">Agora, todos os arquivos e pastas que são especificadas em `_backup.filter` é excluído da saudação futuros backups agendados ou iniciado manualmente.</span><span class="sxs-lookup"><span data-stu-id="ba703-179">Now, any files and folders that are specified in `_backup.filter` is excluded from hello future backups scheduled or manually initiated.</span></span> 

> [!NOTE]
> <span data-ttu-id="ba703-180">Restaurar backups parciais de saudação seu site mesma maneira que faria [restaurar um backup regular](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="ba703-180">You restore partial backups of your site hello same way you would [restore a regular backup](web-sites-restore.md).</span></span> <span data-ttu-id="ba703-181">o processo de restauração Olá Olá certo.</span><span class="sxs-lookup"><span data-stu-id="ba703-181">hello restore process does hello right thing.</span></span>
> 
> <span data-ttu-id="ba703-182">Quando um backup completo for restaurado, todo o conteúdo no site de saudação é substituído por tudo o que está em backup de saudação.</span><span class="sxs-lookup"><span data-stu-id="ba703-182">When a full backup is restored, all content on hello site is replaced with whatever is in hello backup.</span></span> <span data-ttu-id="ba703-183">Se um arquivo estiver no site hello, mas não no backup Olá é excluído.</span><span class="sxs-lookup"><span data-stu-id="ba703-183">If a file is on hello site, but not in hello backup it gets deleted.</span></span> <span data-ttu-id="ba703-184">Mas, quando um backup parcial é restaurado, qualquer conteúdo que está localizado em um dos diretórios de saudação na lista negra ou qualquer arquivo na lista negra, será deixado como está.</span><span class="sxs-lookup"><span data-stu-id="ba703-184">But when a partial backup is restored, any content that is located in one of hello blacklisted directories, or any blacklisted file, is left as is.</span></span>
> 


<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a><span data-ttu-id="ba703-185">Como os backups são armazenados</span><span class="sxs-lookup"><span data-stu-id="ba703-185">How backups are stored</span></span>
<span data-ttu-id="ba703-186">Depois de ter feito uma ou mais backups para seu aplicativo, backups de saudação são visíveis em Olá **contêineres** folha de sua conta de armazenamento e seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ba703-186">After you have made one or more backups for your app, hello backups are visible on hello **Containers** blade of your storage account, and your app.</span></span> <span data-ttu-id="ba703-187">Conta de armazenamento hello, cada backup consiste em uma`.zip` arquivo que contém os dados de backup hello e um `.xml` arquivo que contém um manifesto de saudação `.zip` o conteúdo do arquivo.</span><span class="sxs-lookup"><span data-stu-id="ba703-187">In hello storage account, each backup consists of a`.zip` file that contains hello backup data and an `.xml` file that contains a manifest of hello `.zip` file contents.</span></span> <span data-ttu-id="ba703-188">Você pode descompactar e procurar esses arquivos se você quiser tooaccess seus backups sem realmente executar uma restauração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ba703-188">You can unzip and browse these files if you want tooaccess your backups without actually performing an app restore.</span></span>

<span data-ttu-id="ba703-189">backup de banco de dados Olá para o aplicativo hello é armazenado na raiz de saudação do arquivo the.zip.</span><span class="sxs-lookup"><span data-stu-id="ba703-189">hello database backup for hello app is stored in hello root of the.zip file.</span></span> <span data-ttu-id="ba703-190">Para um banco de dados SQL, este é um arquivo BACPAC (sem extensão de arquivo) e pode ser importado.</span><span class="sxs-lookup"><span data-stu-id="ba703-190">For a SQL database, this is a BACPAC file (no file extension) and can be imported.</span></span> <span data-ttu-id="ba703-191">toocreate um banco de dados do SQL com base em Olá exportação do BACPAC, consulte [importar um arquivo BACPAC de tooCreate um novo banco de dados de usuário](http://technet.microsoft.com/library/hh710052.aspx).</span><span class="sxs-lookup"><span data-stu-id="ba703-191">toocreate a SQL database based on hello BACPAC export, see [Import a BACPAC File tooCreate a New User Database](http://technet.microsoft.com/library/hh710052.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="ba703-192">Alterar qualquer um dos arquivos Olá no seu **websitebackups** contêiner pode fazer com que o hello toobecome de backup inválido e, portanto, não recuperáveis.</span><span class="sxs-lookup"><span data-stu-id="ba703-192">Altering any of hello files in your **websitebackups** container can cause hello backup toobecome invalid and therefore non-restorable.</span></span>
> 
> 

<a name="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="ba703-193">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ba703-193">Next Steps</span></span>
<span data-ttu-id="ba703-194">Para obter informações sobre como restaurar um aplicativo por um backup, veja [Restaurar um aplicativo no Serviço de Aplicativo do Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="ba703-194">For information on restoring an app from a backup, see [Restore an app in Azure](web-sites-restore.md).</span></span> <span data-ttu-id="ba703-195">Você também pode fazer backup e restaurar aplicativos de serviço de aplicativo usando a API REST (consulte [REST de uso toobackup e restauração de aplicativos de serviço de aplicativo](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="ba703-195">You can also backup and restore App Service apps using REST API (see [Use REST toobackup and restore App Service apps](websites-csm-backup.md)).</span></span>


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

