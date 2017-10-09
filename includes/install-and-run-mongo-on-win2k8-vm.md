<span data-ttu-id="5778c-101">Siga estas etapas tooinstall e execute o MongoDB em uma máquina virtual executando o Windows Server.</span><span class="sxs-lookup"><span data-stu-id="5778c-101">Follow these steps tooinstall and run MongoDB on a virtual machine running Windows Server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5778c-102">Os recursos de segurança do MongoDB, como autenticação e associação com o endereço IP, não são habilitados por padrão.</span><span class="sxs-lookup"><span data-stu-id="5778c-102">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="5778c-103">Recursos de segurança devem ser habilitados antes de implantar o ambiente de produção do MongoDB tooa.</span><span class="sxs-lookup"><span data-stu-id="5778c-103">Security features should be enabled before deploying MongoDB tooa production environment.</span></span>  <span data-ttu-id="5778c-104">Para obter mais informações, confira [Segurança e autenticação](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span><span class="sxs-lookup"><span data-stu-id="5778c-104">For more information, see [Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>
>
>

1. <span data-ttu-id="5778c-105">Depois de se conectar a máquina virtual de toohello usando a área de trabalho remota, abra o Internet Explorer da saudação **iniciar** menu na máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="5778c-105">After you've connected toohello virtual machine using Remote Desktop, open Internet Explorer from hello **Start** menu on hello virtual machine.</span></span>
2. <span data-ttu-id="5778c-106">Selecione Olá **ferramentas** botão no canto superior direito da saudação.</span><span class="sxs-lookup"><span data-stu-id="5778c-106">Select hello **Tools** button in hello upper right corner.</span></span>  <span data-ttu-id="5778c-107">Em **opções da Internet**, selecione Olá **segurança** guia e, em seguida, selecione Olá **Sites confiáveis** ícone e finalmente clique Olá **Sites** botão.</span><span class="sxs-lookup"><span data-stu-id="5778c-107">In **Internet Options**, select hello **Security** tab, and then select hello **Trusted Sites** icon, and finally click hello **Sites** button.</span></span> <span data-ttu-id="5778c-108">Adicionar *https://\*. mongodb.org* toohello lista de sites confiáveis.</span><span class="sxs-lookup"><span data-stu-id="5778c-108">Add *https://\*.mongodb.org* toohello list of trusted sites.</span></span>
3. <span data-ttu-id="5778c-109">Vá muito[Downloads - MongoDB](https://www.mongodb.com/download-center#community).</span><span class="sxs-lookup"><span data-stu-id="5778c-109">Go too[Downloads - MongoDB](https://www.mongodb.com/download-center#community).</span></span>
4. <span data-ttu-id="5778c-110">Localize Olá **atual versão estável** de **Community Server**, selecione hello mais recente **64-bit** versão na coluna do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="5778c-110">Find hello **Current Stable Release** of **Community Server**, select hello latest **64-bit** version in hello Windows column.</span></span> <span data-ttu-id="5778c-111">Baixe e execute o instalador MSI de saudação.</span><span class="sxs-lookup"><span data-stu-id="5778c-111">Download, then run hello MSI installer.</span></span>
5. <span data-ttu-id="5778c-112">Geralmente, o MongoDB é instalado em C:\Arquivos de Programas\MongoDB.</span><span class="sxs-lookup"><span data-stu-id="5778c-112">MongoDB is typically installed in C:\Program Files\MongoDB.</span></span> <span data-ttu-id="5778c-113">Pesquisar variáveis de ambiente na área de trabalho hello e adicionar a variável de caminho de toohello Olá MongoDB binários path.</span><span class="sxs-lookup"><span data-stu-id="5778c-113">Search for Environment Variables on hello desktop and add hello MongoDB binaries path toohello PATH variable.</span></span> <span data-ttu-id="5778c-114">Por exemplo, você pode encontrar binários Olá em C:\Program Files\MongoDB\Server\3.4\bin em seu computador.</span><span class="sxs-lookup"><span data-stu-id="5778c-114">For example, you might find hello binaries at C:\Program Files\MongoDB\Server\3.4\bin on your machine.</span></span>
6. <span data-ttu-id="5778c-115">Criar os diretórios de dados e log do MongoDB no disco de dados hello (como unidade **f:**) criado na Olá etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="5778c-115">Create MongoDB data and log directories in hello data disk (such as drive **F:**) you created in hello preceding steps.</span></span> <span data-ttu-id="5778c-116">De **iniciar**, selecione **Prompt de comando** tooopen uma janela de prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="5778c-116">From **Start**, select **Command Prompt** tooopen a command prompt window.</span></span>  <span data-ttu-id="5778c-117">Tipo:</span><span class="sxs-lookup"><span data-stu-id="5778c-117">Type:</span></span>

        C:\> F:
        F:\> mkdir \MongoData
        F:\> mkdir \MongoLogs
7. <span data-ttu-id="5778c-118">toorun Olá banco de dados, execute:</span><span class="sxs-lookup"><span data-stu-id="5778c-118">toorun hello database, run:</span></span>

        F:\> C:
        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log

    <span data-ttu-id="5778c-119">Todas as mensagens de log são direcionado toohello *F:\MongoLogs\mongolog.log* de arquivos como mongod.exe server é iniciado e preallocates arquivos de diário.</span><span class="sxs-lookup"><span data-stu-id="5778c-119">All log messages are directed toohello *F:\MongoLogs\mongolog.log* file as mongod.exe server starts and preallocates journal files.</span></span> <span data-ttu-id="5778c-120">Pode levar vários minutos para o MongoDB toopreallocate arquivos de diário hello e comece a escutar conexões.</span><span class="sxs-lookup"><span data-stu-id="5778c-120">It may take several minutes for MongoDB toopreallocate hello journal files and start listening for connections.</span></span> <span data-ttu-id="5778c-121">prompt de comando Olá permanece voltada para essa tarefa enquanto a instância do MongoDB está em execução.</span><span class="sxs-lookup"><span data-stu-id="5778c-121">hello command prompt stays focused on this task while your MongoDB instance is running.</span></span>
8. <span data-ttu-id="5778c-122">Olá toostart shell administrativo do MongoDB, abrir outra janela de comando do **iniciar** e Olá tipo comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="5778c-122">toostart hello MongoDB administrative shell, open another command window from **Start** and type hello following commands:</span></span>

        C:\> cd \my_mongo_dir\bin  
        C:\my_mongo_dir\bin> mongo  
        >db  
        test
        > db.foo.insert( { a : 1 } )  
        > db.foo.find()  
        { _id : ..., a : 1 }  
        > show dbs  
        ...  
        > show collections  
        ...  
        > help  

    <span data-ttu-id="5778c-123">banco de dados de saudação é criado pelo Olá insert.</span><span class="sxs-lookup"><span data-stu-id="5778c-123">hello database is created by hello insert.</span></span>
9. <span data-ttu-id="5778c-124">Como alternativa, é possível instalar mongod.exe como um serviço:</span><span class="sxs-lookup"><span data-stu-id="5778c-124">Alternatively, you can install mongod.exe as a service:</span></span>

        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log --logappend  --install

    <span data-ttu-id="5778c-125">É instalado um serviço chamado MongoDB, com a descrição "Mongo DB".</span><span class="sxs-lookup"><span data-stu-id="5778c-125">A service is installed named MongoDB with a description of "Mongo DB".</span></span> <span data-ttu-id="5778c-126">Olá `--logpath` opção deve ser usado toospecify um arquivo de log, pois Olá executar o serviço não tem uma saída toodisplay da janela de comando.</span><span class="sxs-lookup"><span data-stu-id="5778c-126">hello `--logpath` option must be used toospecify a log file, since hello running service does not have a command window toodisplay output.</span></span>  <span data-ttu-id="5778c-127">Olá `--logappend` opção especifica que uma reinicialização do serviço Olá faz com que o arquivo de log existente do saída tooappend toohello.</span><span class="sxs-lookup"><span data-stu-id="5778c-127">hello `--logappend` option specifies that a restart of hello service causes output tooappend toohello existing log file.</span></span>  <span data-ttu-id="5778c-128">Olá `--dbpath` opção especifica o local de saudação do diretório de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="5778c-128">hello `--dbpath` option specifies hello location of hello data directory.</span></span> <span data-ttu-id="5778c-129">Para obter mais opções de linha de comando relacionadas ao serviço, consulte [Opções de linha de comando relacionadas ao serviço][MongoWindowsSvcOptions].</span><span class="sxs-lookup"><span data-stu-id="5778c-129">For more service-related command-line options, see [Service-related command-line options][MongoWindowsSvcOptions].</span></span>

    <span data-ttu-id="5778c-130">serviço de saudação toostart, execute este comando:</span><span class="sxs-lookup"><span data-stu-id="5778c-130">toostart hello service, run this command:</span></span>

        C:\> net start MongoDB
10. <span data-ttu-id="5778c-131">Agora que o MongoDB está instalado e em execução, você precisa tooopen uma porta no Firewall do Windows assim você pode se conectar remotamente tooMongoDB.</span><span class="sxs-lookup"><span data-stu-id="5778c-131">Now that MongoDB is installed and running, you need tooopen a port in Windows Firewall so you can remotely connect tooMongoDB.</span></span>  <span data-ttu-id="5778c-132">De saudação **iniciar** menu, selecione **ferramentas administrativas** e **Firewall do Windows com segurança avançada**.</span><span class="sxs-lookup"><span data-stu-id="5778c-132">From hello **Start** menu, select **Administrative Tools** and then **Windows Firewall with Advanced Security**.</span></span>
11. <span data-ttu-id="5778c-133">a) no painel esquerdo do hello, selecione **regras de entrada**.</span><span class="sxs-lookup"><span data-stu-id="5778c-133">a) In hello left pane, select **Inbound Rules**.</span></span>  <span data-ttu-id="5778c-134">Em Olá **ações** painel saudação à direita, selecione **nova regra...** .</span><span class="sxs-lookup"><span data-stu-id="5778c-134">In hello **Actions** pane on hello right, select **New Rule...**.</span></span>

    ![Firewall do Windows][Image1]

    <span data-ttu-id="5778c-136">b) na Olá **novo Assistente de regra de entrada**, selecione **porta** e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="5778c-136">b) In hello **New Inbound Rule Wizard**, select **Port** and then click **Next**.</span></span>

    ![Firewall do Windows][Image2]

    <span data-ttu-id="5778c-138">Selecione **TCP** e **Portas locais específicas**.</span><span class="sxs-lookup"><span data-stu-id="5778c-138">c) Select **TCP** and then **Specific local ports**.</span></span>  <span data-ttu-id="5778c-139">Especifique uma porta de "27017" (porta de padrão Olá MongoDB escuta) e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="5778c-139">Specify a port of "27017" (hello default port MongoDB listens on) and click **Next**.</span></span>

    ![Firewall do Windows][Image3]

    <span data-ttu-id="5778c-141">d) selecione **Permitir conexão Olá** e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="5778c-141">d) Select **Allow hello connection** and click **Next**.</span></span>

    ![Firewall do Windows][Image4]

    <span data-ttu-id="5778c-143">Clique em **Avançar** novamente.</span><span class="sxs-lookup"><span data-stu-id="5778c-143">e) Click **Next** again.</span></span>

    ![Firewall do Windows][Image5]

    <span data-ttu-id="5778c-145">f) Especifique um nome para a regra de saudação, como "MongoPort" e clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="5778c-145">f) Specify a name for hello rule, such as "MongoPort", and click **Finish**.</span></span>

    ![Firewall do Windows][Image6]

12. <span data-ttu-id="5778c-147">Se você não configurar um ponto de extremidade para o MongoDB quando você criou a máquina virtual de saudação, você pode fazer isso agora.</span><span class="sxs-lookup"><span data-stu-id="5778c-147">If you didn't configure an endpoint for MongoDB when you created hello virtual machine, you can do it now.</span></span> <span data-ttu-id="5778c-148">Você precisa de regra de firewall hello e Olá ponto de extremidade toobe capaz de tooconnect tooMongoDB remotamente.</span><span class="sxs-lookup"><span data-stu-id="5778c-148">You need both hello firewall rule and hello endpoint toobe able tooconnect tooMongoDB remotely.</span></span>

  <span data-ttu-id="5778c-149">No portal do Azure de Olá, clique em **máquinas virtuais (clássicas)**, clique em nome de saudação da nova máquina virtual e, em seguida, clique em **pontos de extremidade**.</span><span class="sxs-lookup"><span data-stu-id="5778c-149">In hello Azure portal, click **Virtual Machines (classic)**, click hello name of your new virtual machine, and then click **Endpoints**.</span></span>

    ![Pontos de extremidade][Image7]

13. <span data-ttu-id="5778c-151">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5778c-151">Click **Add**.</span></span>

14. <span data-ttu-id="5778c-152">Adicionar um ponto de extremidade com o nome "Mongo", protocolo **TCP**e ambos **pública** e **privada** portas conjunto muito "27017".</span><span class="sxs-lookup"><span data-stu-id="5778c-152">Add an endpoint with name "Mongo", protocol **TCP**, and both **Public** and **Private** ports set too"27017".</span></span> <span data-ttu-id="5778c-153">Esta porta permite toobe MongoDB acessado remotamente.</span><span class="sxs-lookup"><span data-stu-id="5778c-153">Opening this port allows MongoDB toobe accessed remotely.</span></span>

    ![Pontos de extremidade][Image9]

> [!NOTE]
> <span data-ttu-id="5778c-155">Olá porta 27017 é saudação padrão usado pelo MongoDB.</span><span class="sxs-lookup"><span data-stu-id="5778c-155">hello port 27017 is hello default port used by MongoDB.</span></span> <span data-ttu-id="5778c-156">Você pode alterar essa porta padrão especificando Olá `--port` parâmetro durante a inicialização do servidor de mongod.exe hello.</span><span class="sxs-lookup"><span data-stu-id="5778c-156">You can change this default port by specifying hello `--port` parameter when starting hello mongod.exe server.</span></span> <span data-ttu-id="5778c-157">Tornar toogive se Olá o mesmo número de porta no firewall hello e Olá ponto de extremidade de "Mongo" hello anterior instruções.</span><span class="sxs-lookup"><span data-stu-id="5778c-157">Make sure toogive hello same port number in hello firewall and hello "Mongo" endpoint in hello preceding instructions.</span></span>
>
>

[MongoDownloads]: http://www.mongodb.org/downloads

[MongoWindowsSvcOptions]: http://www.mongodb.org/display/DOCS/Windows+Service


[Image1]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall1.png
[Image2]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall2.png
[Image3]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall3.png
[Image4]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall4.png
[Image5]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall5.png
[Image6]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall6.png
[Image7]: ./media/install-and-run-mongo-on-win2k8-vm/menusendpointadd.png
<!-- Removed 03/08/2017. Not in new portal. -->
<!-- [Image8]: ./media/install-and-run-mongo-on-win2k8-vm/WinVmAddEndpoint2.png
-->
[Image9]: ./media/install-and-run-mongo-on-win2k8-vm/newendpointdetails.png
