<!--author=SharS last changed: 9/17/15-->

<span data-ttu-id="76648-101">Neste procedimento, você vai:</span><span class="sxs-lookup"><span data-stu-id="76648-101">In this procedure, you will:</span></span>

1. <span data-ttu-id="76648-102">[Preparar o executável de mantenedor Olá toorun](#to-prepare-to-run-the-maintainer) .</span><span class="sxs-lookup"><span data-stu-id="76648-102">[Prepare toorun hello Maintainer executable](#to-prepare-to-run-the-maintainer) .</span></span>
2. <span data-ttu-id="76648-103">[Preparar o banco de dados de conteúdo do hello e a Lixeira para exclusão imediata de BLOBs órfãos](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span><span class="sxs-lookup"><span data-stu-id="76648-103">[Prepare hello content database and Recycle Bin for immediate deletion of orphaned BLOBs](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span></span>
3. <span data-ttu-id="76648-104">[Executar o Maintainer.exe](#to-run-the-maintainer).</span><span class="sxs-lookup"><span data-stu-id="76648-104">[Run Maintainer.exe](#to-run-the-maintainer).</span></span>
4. <span data-ttu-id="76648-105">[Reverter o banco de dados de conteúdo do hello e configurações da Lixeira](#to-revert-the-content-database-and-recycle-bin-settings).</span><span class="sxs-lookup"><span data-stu-id="76648-105">[Revert hello content database and Recycle Bin settings](#to-revert-the-content-database-and-recycle-bin-settings).</span></span>

#### <a name="tooprepare-toorun-hello-maintainer"></a><span data-ttu-id="76648-106">tooprepare toorun Olá mantenedor</span><span class="sxs-lookup"><span data-stu-id="76648-106">tooprepare toorun hello Maintainer</span></span>
1. <span data-ttu-id="76648-107">No servidor front-end da Web de hello, abra Olá Shell de gerenciamento do SharePoint 2013 como um administrador.</span><span class="sxs-lookup"><span data-stu-id="76648-107">On hello Web front-end server, open hello SharePoint 2013 Management Shell as an administrator.</span></span>
2. <span data-ttu-id="76648-108">Navegue pasta toohello *unidade de inicialização*: \Program Files\Microsoft 10.50\Maintainer SQL Remote Blob Storage\.</span><span class="sxs-lookup"><span data-stu-id="76648-108">Navigate toohello folder *boot drive*:\Program Files\Microsoft SQL Remote Blob Storage 10.50\Maintainer\.</span></span>
3. <span data-ttu-id="76648-109">Renomear **Microsoft.Data.sqlremoteblobs.maintainer.exe. config** muito**Web. config**.</span><span class="sxs-lookup"><span data-stu-id="76648-109">Rename **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** too**web.config**.</span></span>
4. <span data-ttu-id="76648-110">Use `aspnet_regiis -pdf connectionStrings` toodecrypt Olá Web. config.</span><span class="sxs-lookup"><span data-stu-id="76648-110">Use `aspnet_regiis -pdf connectionStrings` toodecrypt hello web.config file.</span></span>
5. <span data-ttu-id="76648-111">No arquivo de Web. config descriptografada Olá, em hello `connectionStrings` nó, adicionar Olá cadeia de caracteres de conexão para sua instância do SQL server e Olá nome do banco de dados de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="76648-111">In hello decrypted web.config file, under hello `connectionStrings` node, add hello connection string for your SQL server instance and hello content database name.</span></span> <span data-ttu-id="76648-112">Consulte Olá exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="76648-112">See hello following example.</span></span>
   
    `<add name=”RBSMaintainerConnectionWSSContent” connectionString="Data Source=SHRPT13-SQL12\SHRPT13;Initial Catalog=WSS_Content;Integrated Security=True;Application Name=&quot;Remote Blob Storage Maintainer for WSS_Content&quot;" providerName="System.Data.SqlClient" />`
6. <span data-ttu-id="76648-113">Use `aspnet_regiis –pef connectionStrings` toore-criptografar o arquivo Web. config de saudação.</span><span class="sxs-lookup"><span data-stu-id="76648-113">Use `aspnet_regiis –pef connectionStrings` toore-encrypt hello web.config file.</span></span> 
7. <span data-ttu-id="76648-114">Renomear tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config Web. config.</span><span class="sxs-lookup"><span data-stu-id="76648-114">Rename web.config tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config.</span></span> 

#### <a name="tooprepare-hello-content-database-and-recycle-bin-tooimmediately-delete-orphaned-blobs"></a><span data-ttu-id="76648-115">banco de dados conteúdo tooprepare hello e Lixeira tooimmediately excluir BLOBs órfãos</span><span class="sxs-lookup"><span data-stu-id="76648-115">tooprepare hello content database and Recycle Bin tooimmediately delete orphaned BLOBs</span></span>
1. <span data-ttu-id="76648-116">Em saudação do SQL Server no SQL Management Studio, execute Olá consultas de atualização para o banco de dados de destino Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="76648-116">On hello SQL Server, in SQL Management Studio, run hello following update queries for hello target content database:</span></span> 
   
       `use WSS_Content`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ’time 00:00:00’`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’time 00:00:00’`
2. <span data-ttu-id="76648-117">Em Olá web servidor de front-end, em **Administração Central**, editar Olá **configurações gerais do aplicativo Web** para Olá desejado Olá de desabilitar banco de dados de conteúdo tootemporarily Lixeira.</span><span class="sxs-lookup"><span data-stu-id="76648-117">On hello web front-end server, under **Central Administration**, edit hello **Web Application General Settings** for hello desired content database tootemporarily disable hello Recycle Bin.</span></span> <span data-ttu-id="76648-118">Essa ação também será vazio hello Lixeira para todas as coleções de site relacionado.</span><span class="sxs-lookup"><span data-stu-id="76648-118">This action will also empty hello Recycle Bin for any related site collections.</span></span> <span data-ttu-id="76648-119">toodo, clique **Administração Central** -> **gerenciamento de aplicativos** -> **Web Applications (gerenciar aplicativos de web)**  ->  **SharePoint - 80** -> **configurações gerais do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="76648-119">toodo this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="76648-120">Saudação de conjunto **reciclar Bin Status** muito**OFF**.</span><span class="sxs-lookup"><span data-stu-id="76648-120">Set hello **Recycle Bin Status** too**OFF**.</span></span>
   
    ![Configurações Gerais do Aplicativo Web](./media/storsimple-sharepoint-adapter-garbage-collection/HCS_WebApplicationGeneralSettings-include.png)

#### <a name="toorun-hello-maintainer"></a><span data-ttu-id="76648-122">Olá toorun mantenedor</span><span class="sxs-lookup"><span data-stu-id="76648-122">toorun hello Maintainer</span></span>
* <span data-ttu-id="76648-123">No servidor front-end da web de hello, em Olá Shell de gerenciamento do SharePoint 2013, execute Olá mantenedor da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="76648-123">On hello web front-end server, in hello SharePoint 2013 Management Shell, run hello Maintainer as follows:</span></span>
  
      `Microsoft.Data.SqlRemoteBlobs.Maintainer.exe -ConnectionStringName RBSMaintainerConnectionWSSContent -Operation GarbageCollection -GarbageCollectionPhases rdo`
  
  > [!NOTE]
  > <span data-ttu-id="76648-124">Olá apenas `GarbageCollection` operação tem suporte para StorSimple no momento.</span><span class="sxs-lookup"><span data-stu-id="76648-124">Only hello `GarbageCollection` operation is supported for StorSimple at this time.</span></span> <span data-ttu-id="76648-125">Observe também que os parâmetros Olá emitidos para Microsoft.Data.SqlRemoteBlobs.Maintainer.exe diferenciam maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="76648-125">Also note that hello parameters issued for Microsoft.Data.SqlRemoteBlobs.Maintainer.exe are case sensitive.</span></span> 
  > 
  > 

#### <a name="toorevert-hello-content-database-and-recycle-bin-settings"></a><span data-ttu-id="76648-126">banco de dados do toorevert Olá conteúdo e configurações da Lixeira</span><span class="sxs-lookup"><span data-stu-id="76648-126">toorevert hello content database and Recycle Bin settings</span></span>
1. <span data-ttu-id="76648-127">Em saudação do SQL Server no SQL Management Studio, execute Olá consultas de atualização para o banco de dados de destino Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="76648-127">On hello SQL Server, in SQL Management Studio, run hello following update queries for hello target content database:</span></span>
   
      `use WSS_Content`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ‘days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘orphan_scan_period’ , ’days 30’`
2. <span data-ttu-id="76648-128">No servidor front-end da web de hello, em **Administração Central**, editar Olá **configurações gerais do aplicativo Web** para Olá desejado saudação do banco de dados de conteúdo toore habilitar Lixeira.</span><span class="sxs-lookup"><span data-stu-id="76648-128">On hello web front-end server, in **Central Administration**, edit hello **Web Application General Settings** for hello desired content database toore-enable hello Recycle Bin.</span></span> <span data-ttu-id="76648-129">toodo, clique **Administração Central** -> **gerenciamento de aplicativos** -> **Web Applications (gerenciar aplicativos de web)**  ->  **SharePoint - 80** -> **configurações gerais do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="76648-129">toodo this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="76648-130">Definir Olá reciclar Bin Status muito**ON**.</span><span class="sxs-lookup"><span data-stu-id="76648-130">Set hello Recycle Bin Status too**ON**.</span></span>

