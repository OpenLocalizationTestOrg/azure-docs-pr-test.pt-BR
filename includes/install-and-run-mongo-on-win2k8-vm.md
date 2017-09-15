<span data-ttu-id="f518b-101">Siga estas etapas para instalar e executar o MongoDB em uma máquina virtual que executa o Windows Server.</span><span class="sxs-lookup"><span data-stu-id="f518b-101">Follow these steps to install and run MongoDB on a virtual machine running Windows Server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f518b-102">Os recursos de segurança do MongoDB, como autenticação e associação com o endereço IP, não são habilitados por padrão.</span><span class="sxs-lookup"><span data-stu-id="f518b-102">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="f518b-103">Os recursos de segurança devem ser ativados antes de implantar o MongoDB em um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="f518b-103">Security features should be enabled before deploying MongoDB to a production environment.</span></span>  <span data-ttu-id="f518b-104">Para obter mais informações, confira [Segurança e autenticação](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span><span class="sxs-lookup"><span data-stu-id="f518b-104">For more information, see [Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>
>
>

1. <span data-ttu-id="f518b-105">Depois de se conectar à máquina virtual usando a Área de Trabalho Remota, abra o Internet Explorer usando o menu **Iniciar** da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f518b-105">After you've connected to the virtual machine using Remote Desktop, open Internet Explorer from the **Start** menu on the virtual machine.</span></span>
2. <span data-ttu-id="f518b-106">Selecione o botão **Ferramentas** no canto superior direito.</span><span class="sxs-lookup"><span data-stu-id="f518b-106">Select the **Tools** button in the upper right corner.</span></span>  <span data-ttu-id="f518b-107">Em **Opções da Internet**, selecione a guia **Segurança**, selecione o ícone **Sites confiáveis** e, por fim, clique no botão **Sites**.</span><span class="sxs-lookup"><span data-stu-id="f518b-107">In **Internet Options**, select the **Security** tab, and then select the **Trusted Sites** icon, and finally click the **Sites** button.</span></span> <span data-ttu-id="f518b-108">Adicione *https://\*.mongodb.org* à lista de sites confiáveis.</span><span class="sxs-lookup"><span data-stu-id="f518b-108">Add *https://\*.mongodb.org* to the list of trusted sites.</span></span>
3. <span data-ttu-id="f518b-109">Acesse [Downloads- MongoDB](https://www.mongodb.com/download-center#community).</span><span class="sxs-lookup"><span data-stu-id="f518b-109">Go to [Downloads - MongoDB](https://www.mongodb.com/download-center#community).</span></span>
4. <span data-ttu-id="f518b-110">Encontre a **Compilação Estável Atual** de **Community Server** e selecione a mais recente versão de **64 bits** na coluna Windows.</span><span class="sxs-lookup"><span data-stu-id="f518b-110">Find the **Current Stable Release** of **Community Server**, select the latest **64-bit** version in the Windows column.</span></span> <span data-ttu-id="f518b-111">Baixe e execute o instalador MSI.</span><span class="sxs-lookup"><span data-stu-id="f518b-111">Download, then run the MSI installer.</span></span>
5. <span data-ttu-id="f518b-112">Geralmente, o MongoDB é instalado em C:\Arquivos de Programas\MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f518b-112">MongoDB is typically installed in C:\Program Files\MongoDB.</span></span> <span data-ttu-id="f518b-113">Procure pelas Variáveis de Ambiente na área de trabalho e adicione o caminho dos binários do MongoDB à variável PATH.</span><span class="sxs-lookup"><span data-stu-id="f518b-113">Search for Environment Variables on the desktop and add the MongoDB binaries path to the PATH variable.</span></span> <span data-ttu-id="f518b-114">Por exemplo, você pode localizar os binários em C:\Arquivos de Programas\MongoDB\Server\3.4\bin em seu computador.</span><span class="sxs-lookup"><span data-stu-id="f518b-114">For example, you might find the binaries at C:\Program Files\MongoDB\Server\3.4\bin on your machine.</span></span>
6. <span data-ttu-id="f518b-115">Crie diretórios de dados e de log do MongoDB no disco de dados (como a unidade **F:**) criado nas etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="f518b-115">Create MongoDB data and log directories in the data disk (such as drive **F:**) you created in the preceding steps.</span></span> <span data-ttu-id="f518b-116">No menu **Iniciar**, selecione **Prompt de Comando** para abrir uma janela do prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="f518b-116">From **Start**, select **Command Prompt** to open a command prompt window.</span></span>  <span data-ttu-id="f518b-117">Tipo:</span><span class="sxs-lookup"><span data-stu-id="f518b-117">Type:</span></span>

        C:\> F:
        F:\> mkdir \MongoData
        F:\> mkdir \MongoLogs
7. <span data-ttu-id="f518b-118">Para executar o banco de dados, execute:</span><span class="sxs-lookup"><span data-stu-id="f518b-118">To run the database, run:</span></span>

        F:\> C:
        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log

    <span data-ttu-id="f518b-119">Todas as mensagens de log serão direcionadas ao arquivo *F:\MongoLogs\mongolog.log* quando o servidor mongod.exe for iniciado e pré-alocar arquivos de diário.</span><span class="sxs-lookup"><span data-stu-id="f518b-119">All log messages are directed to the *F:\MongoLogs\mongolog.log* file as mongod.exe server starts and preallocates journal files.</span></span> <span data-ttu-id="f518b-120">Pode levar alguns minutos para que o MongoDB pré-aloque os arquivos de diário e comece a detectar conexões.</span><span class="sxs-lookup"><span data-stu-id="f518b-120">It may take several minutes for MongoDB to preallocate the journal files and start listening for connections.</span></span> <span data-ttu-id="f518b-121">O prompt de comando permanece focado nessa tarefa enquanto sua instância do MongoDB está em execução.</span><span class="sxs-lookup"><span data-stu-id="f518b-121">The command prompt stays focused on this task while your MongoDB instance is running.</span></span>
8. <span data-ttu-id="f518b-122">Para iniciar o shell administrativo do MongoDB, abra outra janela Comando no menu **Iniciar** e digite:</span><span class="sxs-lookup"><span data-stu-id="f518b-122">To start the MongoDB administrative shell, open another command window from **Start** and type the following commands:</span></span>

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

    <span data-ttu-id="f518b-123">O banco de dados é criado pelo comando insert.</span><span class="sxs-lookup"><span data-stu-id="f518b-123">The database is created by the insert.</span></span>
9. <span data-ttu-id="f518b-124">Como alternativa, é possível instalar mongod.exe como um serviço:</span><span class="sxs-lookup"><span data-stu-id="f518b-124">Alternatively, you can install mongod.exe as a service:</span></span>

        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log --logappend  --install

    <span data-ttu-id="f518b-125">É instalado um serviço chamado MongoDB, com a descrição "Mongo DB".</span><span class="sxs-lookup"><span data-stu-id="f518b-125">A service is installed named MongoDB with a description of "Mongo DB".</span></span> <span data-ttu-id="f518b-126">A opção `--logpath` deve ser usada para especificar um arquivo de log uma vez que o serviço em execução não terá uma janela de comando para exibir a saída.</span><span class="sxs-lookup"><span data-stu-id="f518b-126">The `--logpath` option must be used to specify a log file, since the running service does not have a command window to display output.</span></span>  <span data-ttu-id="f518b-127">A opção `--logappend` especifica que uma reinicialização do serviço fará com que a saída seja acrescentada ao arquivo de log existente.</span><span class="sxs-lookup"><span data-stu-id="f518b-127">The `--logappend` option specifies that a restart of the service causes output to append to the existing log file.</span></span>  <span data-ttu-id="f518b-128">A opção `--dbpath` especifica o local do diretório de dados.</span><span class="sxs-lookup"><span data-stu-id="f518b-128">The `--dbpath` option specifies the location of the data directory.</span></span> <span data-ttu-id="f518b-129">Para obter mais opções de linha de comando relacionadas ao serviço, consulte [Opções de linha de comando relacionadas ao serviço][MongoWindowsSvcOptions].</span><span class="sxs-lookup"><span data-stu-id="f518b-129">For more service-related command-line options, see [Service-related command-line options][MongoWindowsSvcOptions].</span></span>

    <span data-ttu-id="f518b-130">Para iniciar o serviço, execute este comando:</span><span class="sxs-lookup"><span data-stu-id="f518b-130">To start the service, run this command:</span></span>

        C:\> net start MongoDB
10. <span data-ttu-id="f518b-131">Agora que o MongoDB está instalado e em execução, você precisa abrir uma porta no Firewall do Windows para poder se conectar remotamente ao MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f518b-131">Now that MongoDB is installed and running, you need to open a port in Windows Firewall so you can remotely connect to MongoDB.</span></span>  <span data-ttu-id="f518b-132">No menu **Iniciar**, selecione **Ferramentas Administrativas** e depois **Firewall do Windows com segurança avançada**.</span><span class="sxs-lookup"><span data-stu-id="f518b-132">From the **Start** menu, select **Administrative Tools** and then **Windows Firewall with Advanced Security**.</span></span>
11. <span data-ttu-id="f518b-133">No painel esquerdo, selecione **Regras de Entrada**.</span><span class="sxs-lookup"><span data-stu-id="f518b-133">a) In the left pane, select **Inbound Rules**.</span></span>  <span data-ttu-id="f518b-134">À direita, no painel **Ações**, selecione **Nova Regra...**.</span><span class="sxs-lookup"><span data-stu-id="f518b-134">In the **Actions** pane on the right, select **New Rule...**.</span></span>

    ![Firewall do Windows][Image1]

    <span data-ttu-id="f518b-136">No **Assistente para Nova Regra de Entrada**, selecione **Porta** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="f518b-136">b) In the **New Inbound Rule Wizard**, select **Port** and then click **Next**.</span></span>

    ![Firewall do Windows][Image2]

    <span data-ttu-id="f518b-138">Selecione **TCP** e **Portas locais específicas**.</span><span class="sxs-lookup"><span data-stu-id="f518b-138">c) Select **TCP** and then **Specific local ports**.</span></span>  <span data-ttu-id="f518b-139">Especifique uma porta "27017" (a porta padrão em que MongoDB escuta) e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="f518b-139">Specify a port of "27017" (the default port MongoDB listens on) and click **Next**.</span></span>

    ![Firewall do Windows][Image3]

    <span data-ttu-id="f518b-141">Selecione **Permitir a conexão** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="f518b-141">d) Select **Allow the connection** and click **Next**.</span></span>

    ![Firewall do Windows][Image4]

    <span data-ttu-id="f518b-143">Clique em **Avançar** novamente.</span><span class="sxs-lookup"><span data-stu-id="f518b-143">e) Click **Next** again.</span></span>

    ![Firewall do Windows][Image5]

    <span data-ttu-id="f518b-145">Especifique um nome para a regra, como "MongoPort", e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="f518b-145">f) Specify a name for the rule, such as "MongoPort", and click **Finish**.</span></span>

    ![Firewall do Windows][Image6]

12. <span data-ttu-id="f518b-147">Se você não configurou um ponto de extremidade para o MongoDB quando criou a máquina virtual, pode fazer isso agora.</span><span class="sxs-lookup"><span data-stu-id="f518b-147">If you didn't configure an endpoint for MongoDB when you created the virtual machine, you can do it now.</span></span> <span data-ttu-id="f518b-148">Você precisa do ponto de extremidade e da regra de firewall para ser capaz de se conectar remotamente ao MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f518b-148">You need both the firewall rule and the endpoint to be able to connect to MongoDB remotely.</span></span>

  <span data-ttu-id="f518b-149">No portal do Azure, clique em **Máquinas Virtuais (clássicas)**, clique no nome de sua nova máquina virtual e clique em **Pontos de Extremidade**.</span><span class="sxs-lookup"><span data-stu-id="f518b-149">In the Azure portal, click **Virtual Machines (classic)**, click the name of your new virtual machine, and then click **Endpoints**.</span></span>

    ![Pontos de extremidade][Image7]

13. <span data-ttu-id="f518b-151">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f518b-151">Click **Add**.</span></span>

14. <span data-ttu-id="f518b-152">Adicione um ponto de extremidade com o nome "Mongo", protocolo **TCP** e defina as portas **Pública** e **Privada** como "27017".</span><span class="sxs-lookup"><span data-stu-id="f518b-152">Add an endpoint with name "Mongo", protocol **TCP**, and both **Public** and **Private** ports set to "27017".</span></span> <span data-ttu-id="f518b-153">Abrir essa porta permite que o MongoDB seja acessado remotamente.</span><span class="sxs-lookup"><span data-stu-id="f518b-153">Opening this port allows MongoDB to be accessed remotely.</span></span>

    ![Pontos de extremidade][Image9]

> [!NOTE]
> <span data-ttu-id="f518b-155">A porta 27017 é a porta padrão usada pelo MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f518b-155">The port 27017 is the default port used by MongoDB.</span></span> <span data-ttu-id="f518b-156">Você pode alterar essa porta padrão especificando o parâmetro `--port` ao iniciar o servidor mongod.exe.</span><span class="sxs-lookup"><span data-stu-id="f518b-156">You can change this default port by specifying the `--port` parameter when starting the mongod.exe server.</span></span> <span data-ttu-id="f518b-157">Forneça o mesmo número de porta no firewall e no ponto de extremidade "Mongo" nas instruções anteriores.</span><span class="sxs-lookup"><span data-stu-id="f518b-157">Make sure to give the same port number in the firewall and the "Mongo" endpoint in the preceding instructions.</span></span>
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
