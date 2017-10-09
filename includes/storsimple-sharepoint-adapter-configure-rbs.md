<!--author=SharS last changed: 1/14/2016 -->

> [!NOTE]
> <span data-ttu-id="2c02a-101">Quando você faz alterações toohello adaptador StorSimple para configuração do SharePoint RBS, você deve fazer logon com uma conta de usuário que pertence o grupo de Admins. do domínio toohello.</span><span class="sxs-lookup"><span data-stu-id="2c02a-101">When making changes toohello StorSimple Adapter for SharePoint RBS configuration, you must be logged on with a user account that belongs toohello Domain Admins group.</span></span> <span data-ttu-id="2c02a-102">Além disso, é necessário acessar a página de configuração de saudação de um navegador em execução no hello mesmo host como a Administração Central.</span><span class="sxs-lookup"><span data-stu-id="2c02a-102">Additionally, you must access hello configuration page from a browser running on hello same host as Central Administration.</span></span>
> 
> 

#### <a name="tooconfigure-rbs"></a><span data-ttu-id="2c02a-103">tooconfigure RBS</span><span class="sxs-lookup"><span data-stu-id="2c02a-103">tooconfigure RBS</span></span>
1. <span data-ttu-id="2c02a-104">Abra a página de Administração Central do SharePoint hello e procurar muito**configurações do sistema**.</span><span class="sxs-lookup"><span data-stu-id="2c02a-104">Open hello SharePoint Central Administration page, and browse too**System Settings**.</span></span> 
2. <span data-ttu-id="2c02a-105">Em Olá **Azure StorSimple** seção, clique em **configurar adaptador do StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="2c02a-105">In hello **Azure StorSimple** section, click **Configure StorSimple Adapter**.</span></span>
   
    ![Configurar Olá adaptador StorSimple](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS1-include.png) 
3. <span data-ttu-id="2c02a-107">Em Olá **configurar adaptador do StorSimple** página:</span><span class="sxs-lookup"><span data-stu-id="2c02a-107">On hello **Configure StorSimple Adapter** page:</span></span>
   
   1. <span data-ttu-id="2c02a-108">Certifique-se de que Olá **habilitar edição de caminho** caixa de seleção é marcada.</span><span class="sxs-lookup"><span data-stu-id="2c02a-108">Make sure that hello **Enable editing path** check box is selected.</span></span>
   2. <span data-ttu-id="2c02a-109">Na caixa de texto de saudação, digite o caminho de convenção de nomenclatura Universal (UNC) de Olá Olá do repositório de BLOB.</span><span class="sxs-lookup"><span data-stu-id="2c02a-109">In hello text box, type hello Universal Naming Convention (UNC) path of hello BLOB store.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="2c02a-110">volume de armazenamento BLOB Olá deve ser hospedado em um volume iSCSI configurado no dispositivo do StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="2c02a-110">hello BLOB store volume must be hosted on an iSCSI volume configured on hello StorSimple device.</span></span>

   3. <span data-ttu-id="2c02a-111">Clique em Olá **habilitar** botão abaixo de cada Olá bancos de dados que você deseja tooconfigure para armazenamento remoto.</span><span class="sxs-lookup"><span data-stu-id="2c02a-111">Click hello **Enable** button below each of hello content databases that you want tooconfigure for remote storage.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="2c02a-112">armazenamento de BLOB Olá deve ser compartilhado por todos os servidores web front-end (WFE) e conta de usuário de Olá configurado para o farm do SharePoint server Olá deve ter o compartilhamento de toohello de acesso.</span><span class="sxs-lookup"><span data-stu-id="2c02a-112">hello BLOB store must be shared and reachable by all web front-end (WFE) servers, and hello user account that is configured for hello SharePoint server farm must have access toohello share.</span></span>
      
      ![Habilitar provedor RBS Olá](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS2-include.png)
      
      <span data-ttu-id="2c02a-114">Quando você habilita ou desabilita o RBS, você também verá seguinte mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c02a-114">When you enable or disable RBS, you will also see hello following message.</span></span>
      
      ![Configurar o Adaptador StorSimple para Habilitado/Desabilitado](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_ConfigureStorSimpleAdapterEnableDisableMessage-include.png)

   4. <span data-ttu-id="2c02a-116">Clique em Olá **atualização** configuração de saudação do botão tooapply.</span><span class="sxs-lookup"><span data-stu-id="2c02a-116">Click hello **Update** button tooapply hello configuration.</span></span> <span data-ttu-id="2c02a-117">Quando você clica em Olá **atualização** botão, Olá status de configuração de RBS será atualizado em todos os servidores WFE e toda a farm Olá será habilitado para RBS.</span><span class="sxs-lookup"><span data-stu-id="2c02a-117">When you click hello **Update** button, hello RBS configuration status will be updated on all WFE servers, and hello entire farm will be RBS-enabled.</span></span> <span data-ttu-id="2c02a-118">Olá a seguinte mensagem será exibida.</span><span class="sxs-lookup"><span data-stu-id="2c02a-118">hello following message appears.</span></span>
      
      ![Mensagem de configuração do adaptador](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS3-include.png)
      
      > [!NOTE]
      > <span data-ttu-id="2c02a-120">Se você estiver configurando o RBS para um farm do SharePoint com um número muito grande de bancos de dados (mais de 200), página de web de Administração Central do SharePoint Olá pode atingir o tempo limite. Se isso ocorrer, atualize a página de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c02a-120">If you are configuring RBS for a SharePoint farm with a very large number of databases (greater than 200), hello SharePoint Central Administration web page might time out. If that occurs, refresh hello page.</span></span> <span data-ttu-id="2c02a-121">Isso não afeta o processo de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c02a-121">This does not affect hello configuration process.</span></span>

4. <span data-ttu-id="2c02a-122">Verificar configuração hello:</span><span class="sxs-lookup"><span data-stu-id="2c02a-122">Verify hello configuration:</span></span>
   
   1. <span data-ttu-id="2c02a-123">Faça logon no site de Administração Central do SharePoint toohello e procurar toohello **configurar adaptador do StorSimple** página.</span><span class="sxs-lookup"><span data-stu-id="2c02a-123">Log on toohello SharePoint Central Administration website, and browse toohello **Configure StorSimple Adapter** page.</span></span>
   2. <span data-ttu-id="2c02a-124">Verifique toomake detalhes de configuração de saudação se eles correspondem às configurações de saudação que você inseriu.</span><span class="sxs-lookup"><span data-stu-id="2c02a-124">Check hello configuration details toomake sure that they match hello settings that you entered.</span></span> 
5. <span data-ttu-id="2c02a-125">Verifique se o RBS funciona corretamente:</span><span class="sxs-lookup"><span data-stu-id="2c02a-125">Verify that RBS works correctly:</span></span>
   
   1. <span data-ttu-id="2c02a-126">Carregar um documento tooSharePoint.</span><span class="sxs-lookup"><span data-stu-id="2c02a-126">Upload a document tooSharePoint.</span></span> 
   2. <span data-ttu-id="2c02a-127">Procure caminho UNC toohello que você configurou.</span><span class="sxs-lookup"><span data-stu-id="2c02a-127">Browse toohello UNC path that you configured.</span></span> <span data-ttu-id="2c02a-128">Certifique-se de que a estrutura de diretório RBS Olá foi criada e que ele contém o objeto Olá carregado.</span><span class="sxs-lookup"><span data-stu-id="2c02a-128">Make sure that hello RBS directory structure was created and that it contains hello uploaded object.</span></span>
6. <span data-ttu-id="2c02a-129">(Opcional) Você pode usar o hello Microsoft RBS `Migrate()` cmdlet do PowerShell incluído com o SharePoint toomigrate existente BLOB conteúdo toohello dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="2c02a-129">(Optional) You can use hello Microsoft RBS `Migrate()` PowerShell cmdlet included with SharePoint toomigrate existing BLOB content toohello StorSimple device.</span></span> <span data-ttu-id="2c02a-130">Para obter mais informações, consulte [migrar conteúdo para dentro ou fora do RBS no SharePoint 2013] [ 6] ou [migrar conteúdo para dentro ou fora do RBS (SharePoint Foundation 2010)] [7].</span><span class="sxs-lookup"><span data-stu-id="2c02a-130">For more information, see [Migrate content into or out of RBS in SharePoint 2013][6] or [Migrate content into or out of RBS (SharePoint Foundation 2010)][7].</span></span>
7. <span data-ttu-id="2c02a-131">(Opcional) Em instalações de teste, você pode verificar que Olá BLOBs foram movidos para fora do banco de dados de conteúdo do hello da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="2c02a-131">(Optional) On test installations, you can verify that hello BLOBs were moved out of hello content database as follows:</span></span> 
   
   1. <span data-ttu-id="2c02a-132">Inicie o SQL Management Studio.</span><span class="sxs-lookup"><span data-stu-id="2c02a-132">Start SQL Management Studio.</span></span>
   2. <span data-ttu-id="2c02a-133">Execute a consulta de ListBlobsInDB_2010.sql ou ListBlobsInDB_2013.sql hello, da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="2c02a-133">Run hello ListBlobsInDB_2010.sql or ListBlobsInDB_2013.sql query, as follows.</span></span>
      
      ```
      **ListBlobsInDB_2013.sql**
      
        USE WSS_Content
        GO
      
        SELECT DocStreams.DocId,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               DocStreams.RbsId,
               TimeLastModified
      
        FROM DocStreams
      
             INNER JOIN AllDocs ON DocStreams.DocId = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      
      **ListBlobsInDB_2010.sql**
      
        USE WSS_Content
        GO
      
        SELECT AllDocStreams.Id,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               RbsId,
               TimeLastModified
        FROM AllDocStreams
      
             INNER JOIN AllDocs ON AllDocStreams.Id = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      ```
      
      <span data-ttu-id="2c02a-134">Se o RBS foi configurado corretamente, um valor NULL aparece na coluna de SizeOfContentInDB Olá para qualquer objeto que foi carregado e externalizado com êxito com RBS.</span><span class="sxs-lookup"><span data-stu-id="2c02a-134">If RBS was configured correctly, a NULL value should appear in hello SizeOfContentInDB column for any object that was uploaded and successfully externalized with RBS.</span></span>
8. <span data-ttu-id="2c02a-135">(Opcional) Depois de configurar o RBS e mover todas as toohello conteúdo BLOB dispositivo StorSimple, você pode mover o dispositivo de toohello do banco de dados de conteúdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c02a-135">(Optional) After you configure RBS and move all BLOB content toohello StorSimple device, you can move hello content database toohello device.</span></span> <span data-ttu-id="2c02a-136">Se você escolher o banco de dados conteúdo toomove Olá, é recomendável que você configure o armazenamento de banco de dados de conteúdo Olá no dispositivo hello como um volume primário.</span><span class="sxs-lookup"><span data-stu-id="2c02a-136">If you choose toomove hello content database, we recommend that you configure hello content database storage on hello device as a primary volume.</span></span> <span data-ttu-id="2c02a-137">Em seguida, use estabelecida que dispositivo StorSimple do toomigrate Olá banco de dados de conteúdo toohello de práticas recomendadas do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2c02a-137">Then, use established SQL Server best practices toomigrate hello content database toohello StorSimple device.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="2c02a-138">Dispositivo móvel de toohello de banco de dados de conteúdo Olá somente há suporte para séries Olá StorSimple 8000 (não há suporte para a série de saudação 5000 ou 7000).</span><span class="sxs-lookup"><span data-stu-id="2c02a-138">Moving hello content database toohello device is only supported for hello StorSimple 8000 series (it is not supported for hello 5000 or 7000 series).</span></span>
   
   <span data-ttu-id="2c02a-139">Se você armazenar BLOBs e banco de dados de conteúdo do hello em volumes separados no dispositivo do StorSimple Olá, é recomendável que você configure no hello mesmo contêiner de volume.</span><span class="sxs-lookup"><span data-stu-id="2c02a-139">If you store BLOBs and hello content database in separate volumes on hello StorSimple device, we recommend that you configure them in hello same volume container.</span></span> <span data-ttu-id="2c02a-140">Isso garante que os respectivos backups sejam feitos juntos.</span><span class="sxs-lookup"><span data-stu-id="2c02a-140">This ensures that they will be backed up together.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="2c02a-141">Se você não tiver habilitado o RBS, não recomendamos mover o dispositivo de StorSimple toohello Olá conteúdo do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="2c02a-141">If you have not enabled RBS, we do not recommend moving hello content database toohello StorSimple device.</span></span> <span data-ttu-id="2c02a-142">Essa é uma configuração não testada.</span><span class="sxs-lookup"><span data-stu-id="2c02a-142">This is an untested configuration.</span></span>
   
9. <span data-ttu-id="2c02a-143">Vá toohello próxima etapa: [configurar coleta de lixo](#configure-garbage-collection).</span><span class="sxs-lookup"><span data-stu-id="2c02a-143">Go toohello next step: [Configure garbage collection](#configure-garbage-collection).</span></span>

[6]: https://technet.microsoft.com/library/ff628254(v=office.15).aspx
[7]: https://technet.microsoft.com/library/ff628255(v=office.14).aspx
