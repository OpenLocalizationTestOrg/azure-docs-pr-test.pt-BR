---
title: aaaInstall MongoDB em uma VM do Windows Azure | Microsoft Docs
description: "Saiba como tooinstall MongoDB em uma VM do Azure executando o Windows Server 2012 R2 criados com o modelo de implantação do Gerenciador de recursos de saudação."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 53faf630-8da5-4955-8d0b-6e829bf30cba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: becd2c607d098e2bc806139e03f2c42f1f01f6f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="e04ae-103">Instalar e configurar o MongoDB em uma VM do Windows no Azure</span><span class="sxs-lookup"><span data-stu-id="e04ae-103">Install and configure MongoDB on a Windows VM in Azure</span></span>
<span data-ttu-id="e04ae-104">[O MongoDB](http://www.mongodb.org) é um popular banco de dados NoSQL de código-fonte aberto e de alto desempenho.</span><span class="sxs-lookup"><span data-stu-id="e04ae-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="e04ae-105">Este artigo lhe orienta pela instalação e configuração do MongoDB em uma VM (máquina virtual) do Windows Server 2012 R2 no Azure.</span><span class="sxs-lookup"><span data-stu-id="e04ae-105">This article guides you through installing and configuring MongoDB on a Windows Server 2012 R2 virtual machine (VM) in Azure.</span></span> <span data-ttu-id="e04ae-106">Você também pode [instalar o MongoDB em uma VM do Linux no Azure](../linux/install-mongodb.md).</span><span class="sxs-lookup"><span data-stu-id="e04ae-106">You can also [install MongoDB on a Linux VM in Azure](../linux/install-mongodb.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e04ae-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e04ae-107">Prerequisites</span></span>
<span data-ttu-id="e04ae-108">Antes de instalar e configurar o MongoDB, você precisa toocreate uma VM e, idealmente, adicione um tooit de disco de dados.</span><span class="sxs-lookup"><span data-stu-id="e04ae-108">Before you install and configure MongoDB, you need toocreate a VM and, ideally, add a data disk tooit.</span></span> <span data-ttu-id="e04ae-109">Consulte Olá artigos toocreate uma máquina virtual a seguir e adicione um disco de dados:</span><span class="sxs-lookup"><span data-stu-id="e04ae-109">See hello following articles toocreate a VM and add a data disk:</span></span>

* <span data-ttu-id="e04ae-110">Criar uma VM do Windows Server usando [Olá portal do Azure](quick-create-portal.md) ou [Azure PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e04ae-110">Create a Windows Server VM using [hello Azure portal](quick-create-portal.md) or [Azure PowerShell](quick-create-powershell.md).</span></span>
* <span data-ttu-id="e04ae-111">Anexar um dados disco tooa VM do Windows Server usando [Olá portal do Azure](attach-managed-disk-portal.md) ou [Azure PowerShell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e04ae-111">Attach a data disk tooa Windows Server VM using [hello Azure portal](attach-managed-disk-portal.md) or [Azure PowerShell](attach-disk-ps.md).</span></span>

<span data-ttu-id="e04ae-112">toobegin instalando e configurando o MongoDB, [logon tooyour VM do Windows Server](connect-logon.md) usando a área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="e04ae-112">toobegin installing and configuring MongoDB, [log on tooyour Windows Server VM](connect-logon.md) by using Remote Desktop.</span></span>

## <a name="install-mongodb"></a><span data-ttu-id="e04ae-113">Instalar o MongoDB</span><span class="sxs-lookup"><span data-stu-id="e04ae-113">Install MongoDB</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e04ae-114">Os recursos de segurança do MongoDB, como autenticação e associação com o endereço IP, não são habilitados por padrão.</span><span class="sxs-lookup"><span data-stu-id="e04ae-114">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="e04ae-115">Recursos de segurança devem ser habilitados antes de implantar o ambiente de produção do MongoDB tooa.</span><span class="sxs-lookup"><span data-stu-id="e04ae-115">Security features should be enabled before deploying MongoDB tooa production environment.</span></span> <span data-ttu-id="e04ae-116">Para obter mais informações, veja [Segurança e Autenticação do MongoDB](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span><span class="sxs-lookup"><span data-stu-id="e04ae-116">For more information, see [MongoDB Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>


1. <span data-ttu-id="e04ae-117">Depois de conectado tooyour VM usando a área de trabalho remota, abra o Internet Explorer da saudação **iniciar** menu Olá VM.</span><span class="sxs-lookup"><span data-stu-id="e04ae-117">After you've connected tooyour VM using Remote Desktop, open Internet Explorer from hello **Start** menu on hello VM.</span></span>
2. <span data-ttu-id="e04ae-118">Selecione **usar as configurações de segurança, privacidade e compatibilidade recomendadas** quando o Internet Explorer abrir pela primeira vez e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-118">Select **Use recommended security, privacy, and compatibility settings** when Internet Explorer first opens, and click **OK**.</span></span>
3. <span data-ttu-id="e04ae-119">A configuração de segurança reforçada do Internet Explorer é habilitada por padrão.</span><span class="sxs-lookup"><span data-stu-id="e04ae-119">Internet Explorer enhanced security configuration is enabled by default.</span></span> <span data-ttu-id="e04ae-120">Adicione lista de toohello de sites Olá MongoDB de sites permitidos:</span><span class="sxs-lookup"><span data-stu-id="e04ae-120">Add hello MongoDB website toohello list of allowed sites:</span></span>
   
   * <span data-ttu-id="e04ae-121">Selecione Olá **ferramentas** ícone no canto superior direito de saudação.</span><span class="sxs-lookup"><span data-stu-id="e04ae-121">Select hello **Tools** icon in hello upper-right corner.</span></span>
   * <span data-ttu-id="e04ae-122">Em **opções da Internet**, selecione Olá **segurança** guia e, em seguida, selecione Olá **Sites confiáveis** ícone.</span><span class="sxs-lookup"><span data-stu-id="e04ae-122">In **Internet Options**, select hello **Security** tab, and then select hello **Trusted Sites** icon.</span></span>
   * <span data-ttu-id="e04ae-123">Clique em Olá **Sites** botão.</span><span class="sxs-lookup"><span data-stu-id="e04ae-123">Click hello **Sites** button.</span></span> <span data-ttu-id="e04ae-124">Adicionar *https://\*. mongodb.org* toohello lista de sites confiáveis e caixa de diálogo Olá feche.</span><span class="sxs-lookup"><span data-stu-id="e04ae-124">Add *https://\*.mongodb.org* toohello list of trusted sites, and then close hello dialog box.</span></span>
     
     ![Definir as configurações de segurança do Internet Explorer](./media/install-mongodb/configure-internet-explorer-security.png)
4. <span data-ttu-id="e04ae-126">Procurar toohello [Downloads do MongoDB -](http://www.mongodb.org/downloads) (http://www.mongodb.org/downloads) da página.</span><span class="sxs-lookup"><span data-stu-id="e04ae-126">Browse toohello [MongoDB - Downloads](http://www.mongodb.org/downloads) page (http://www.mongodb.org/downloads).</span></span>
5. <span data-ttu-id="e04ae-127">Se necessário, selecione Olá **Community Server** edition e, em seguida, selecione Olá versão mais recente atual estável e posterior para Windows Server 2008 R2 de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="e04ae-127">If needed, select hello **Community Server** edition and then select hello latest current stable release for Windows Server 2008 R2 64-bit and later.</span></span> <span data-ttu-id="e04ae-128">toodownload Olá instalador, clique em **DOWNLOAD (msi)**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-128">toodownload hello installer, click **DOWNLOAD (msi)**.</span></span>
   
    ![Baixar o instalador do MongoDB](./media/install-mongodb/download-mongodb.png)
   
    <span data-ttu-id="e04ae-130">Execute o instalador de saudação após a conclusão do download de saudação.</span><span class="sxs-lookup"><span data-stu-id="e04ae-130">Run hello installer after hello download is complete.</span></span>
6. <span data-ttu-id="e04ae-131">Leia e aceite o contrato de licença de saudação.</span><span class="sxs-lookup"><span data-stu-id="e04ae-131">Read and accept hello license agreement.</span></span> <span data-ttu-id="e04ae-132">Quando solicitado, selecione a instalação **Completa**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-132">When you're prompted, select **Complete** install.</span></span>
7. <span data-ttu-id="e04ae-133">Na tela final do hello, clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-133">On hello final screen, click **Install**.</span></span>

## <a name="configure-hello-vm-and-mongodb"></a><span data-ttu-id="e04ae-134">Configurar hello VM e o MongoDB</span><span class="sxs-lookup"><span data-stu-id="e04ae-134">Configure hello VM and MongoDB</span></span>
1. <span data-ttu-id="e04ae-135">variáveis de caminho Olá não são atualizadas pelo instalador do MongoDB hello.</span><span class="sxs-lookup"><span data-stu-id="e04ae-135">hello path variables are not updated by hello MongoDB installer.</span></span> <span data-ttu-id="e04ae-136">Sem Olá MongoDB `bin` local em sua variável de caminho, você precisa toospecify Olá completo caminho sempre que usar um executável do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e04ae-136">Without hello MongoDB `bin` location in your path variable, you need toospecify hello full path each time you use a MongoDB executable.</span></span> <span data-ttu-id="e04ae-137">variável de caminho do tooyour tooadd Olá local:</span><span class="sxs-lookup"><span data-stu-id="e04ae-137">tooadd hello location tooyour path variable:</span></span>
   
   * <span data-ttu-id="e04ae-138">Saudação de atalho **iniciar** menu e selecione **sistema**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-138">Right-click hello **Start** menu, and select **System**.</span></span>
   * <span data-ttu-id="e04ae-139">Clique na guia **Configurações avançadas do sistema** e em **Variáveis de Ambiente**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-139">Click **Advanced system settings**, and then click **Environment Variables**.</span></span>
   * <span data-ttu-id="e04ae-140">Em **Variáveis de sistema**, selecione **Caminho** e, em seguida, clique em **Editar**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-140">Under **System variables**, select **Path**, and then click **Edit**.</span></span>
     
     ![Configurar variáveis PATH](./media/install-mongodb/configure-path-variables.png)
     
     <span data-ttu-id="e04ae-142">Adicionar caminho de saudação tooyour MongoDB `bin` pasta.</span><span class="sxs-lookup"><span data-stu-id="e04ae-142">Add hello path tooyour MongoDB `bin` folder.</span></span> <span data-ttu-id="e04ae-143">Geralmente, o MongoDB é instalado em *C:\Arquivos de Programas\MongoDB*.</span><span class="sxs-lookup"><span data-stu-id="e04ae-143">MongoDB is typically installed in *C:\Program Files\MongoDB*.</span></span> <span data-ttu-id="e04ae-144">Verifique se o caminho de instalação Olá na sua VM.</span><span class="sxs-lookup"><span data-stu-id="e04ae-144">Verify hello installation path on your VM.</span></span> <span data-ttu-id="e04ae-145">Olá, exemplo a seguir adiciona saudação padrão MongoDB instalação local toohello `PATH` variável:</span><span class="sxs-lookup"><span data-stu-id="e04ae-145">hello following example adds hello default MongoDB install location toohello `PATH` variable:</span></span>
     
     ```
     ;C:\Program Files\MongoDB\Server\3.2\bin
     ```
     
     > [!NOTE]
     > <span data-ttu-id="e04ae-146">Ser se tooadd Olá principal-e-vírgula (`;`) tooindicate que você está adicionando um tooyour local `PATH` variável.</span><span class="sxs-lookup"><span data-stu-id="e04ae-146">Be sure tooadd hello leading semicolon (`;`) tooindicate that you are adding a location tooyour `PATH` variable.</span></span>

2. <span data-ttu-id="e04ae-147">Crie diretórios de dados e de log do MongoDB no disco de dados.</span><span class="sxs-lookup"><span data-stu-id="e04ae-147">Create MongoDB data and log directories on your data disk.</span></span> <span data-ttu-id="e04ae-148">De saudação **iniciar** menu, selecione **Prompt de comando**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-148">From hello **Start** menu, select **Command Prompt**.</span></span> <span data-ttu-id="e04ae-149">Olá exemplos a seguir cria diretórios Olá na unidade f:</span><span class="sxs-lookup"><span data-stu-id="e04ae-149">hello following examples create hello directories on drive F:</span></span>
   
    ```
    mkdir F:\MongoData
    mkdir F:\MongoLogs
    ```
3. <span data-ttu-id="e04ae-150">Iniciar uma instância do MongoDB com hello comando a seguir, ajustando dados tooyour do caminho do hello e diretórios de log adequadamente:</span><span class="sxs-lookup"><span data-stu-id="e04ae-150">Start a MongoDB instance with hello following command, adjusting hello path tooyour data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log
    ```
   
    <span data-ttu-id="e04ae-151">Pode levar vários minutos para o MongoDB tooallocate arquivos de diário hello e comece a escutar conexões.</span><span class="sxs-lookup"><span data-stu-id="e04ae-151">It may take several minutes for MongoDB tooallocate hello journal files and start listening for connections.</span></span> <span data-ttu-id="e04ae-152">Todas as mensagens de log são direcionado toohello *F:\MongoLogs\mongolog.log* de arquivos como `mongod.exe` server é iniciado e aloca arquivos de diário.</span><span class="sxs-lookup"><span data-stu-id="e04ae-152">All log messages are directed toohello *F:\MongoLogs\mongolog.log* file as `mongod.exe` server starts and allocates journal files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e04ae-153">prompt de comando Olá permanece voltada para essa tarefa enquanto a instância do MongoDB está em execução.</span><span class="sxs-lookup"><span data-stu-id="e04ae-153">hello command prompt stays focused on this task while your MongoDB instance is running.</span></span> <span data-ttu-id="e04ae-154">Deixe Olá prompt de comando janela aberta toocontinue executando o MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e04ae-154">Leave hello command prompt window open toocontinue running MongoDB.</span></span> <span data-ttu-id="e04ae-155">Ou, instale o MongoDB como serviço, conforme detalhado na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="e04ae-155">Or, install MongoDB as service, as detailed in hello next step.</span></span>

4. <span data-ttu-id="e04ae-156">Para uma experiência mais robusta do MongoDB, instalar Olá `mongod.exe` como um serviço.</span><span class="sxs-lookup"><span data-stu-id="e04ae-156">For a more robust MongoDB experience, install hello `mongod.exe` as a service.</span></span> <span data-ttu-id="e04ae-157">Criando um serviço significa que você não precisa tooleave um prompt de comando executando cada vez que você deseja toouse MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e04ae-157">Creating a service means you don't need tooleave a command prompt running each time you want toouse MongoDB.</span></span> <span data-ttu-id="e04ae-158">Crie serviço de saudação como a seguir, ajustando os diretórios de dados e log de tooyour de caminho do hello adequadamente:</span><span class="sxs-lookup"><span data-stu-id="e04ae-158">Create hello service as follows, adjusting hello path tooyour data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log `
        --logappend  --install
    ```
   
    <span data-ttu-id="e04ae-159">Olá comando anterior cria um serviço denominado MongoDB, com uma descrição de "Mongo DB".</span><span class="sxs-lookup"><span data-stu-id="e04ae-159">hello preceding command creates a service named MongoDB, with a description of "Mongo DB".</span></span> <span data-ttu-id="e04ae-160">Olá parâmetros a seguir também está especificada:</span><span class="sxs-lookup"><span data-stu-id="e04ae-160">hello following parameters are also specified:</span></span>
   
   * <span data-ttu-id="e04ae-161">Olá `--dbpath` opção especifica o local de saudação do diretório de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e04ae-161">hello `--dbpath` option specifies hello location of hello data directory.</span></span>
   * <span data-ttu-id="e04ae-162">Olá `--logpath` opção deve ser usado toospecify um arquivo de log, porque o serviço em execução Olá não tem uma saída toodisplay da janela de comando.</span><span class="sxs-lookup"><span data-stu-id="e04ae-162">hello `--logpath` option must be used toospecify a log file, because hello running service does not have a command window toodisplay output.</span></span>
   * <span data-ttu-id="e04ae-163">Olá `--logappend` opção especifica que uma reinicialização do serviço Olá faz com que o arquivo de log existente do saída tooappend toohello.</span><span class="sxs-lookup"><span data-stu-id="e04ae-163">hello `--logappend` option specifies that a restart of hello service causes output tooappend toohello existing log file.</span></span>
   
   <span data-ttu-id="e04ae-164">serviço de MongoDB em Olá toostart, execute o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="e04ae-164">toostart hello MongoDB service, run hello following command:</span></span>
   
    ```
    net start MongoDB
    ```
   
    <span data-ttu-id="e04ae-165">Para obter mais informações sobre como criar um serviço do MongoDB hello, consulte [configurar um serviço do Windows para o MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span><span class="sxs-lookup"><span data-stu-id="e04ae-165">For more information about creating hello MongoDB service, see [Configure a Windows Service for MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span></span>

## <a name="test-hello-mongodb-instance"></a><span data-ttu-id="e04ae-166">Instância do teste Olá MongoDB</span><span class="sxs-lookup"><span data-stu-id="e04ae-166">Test hello MongoDB instance</span></span>
<span data-ttu-id="e04ae-167">Com o MongoDB em execução como uma única instância ou instalado como um serviço, agora você pode começar a criar e usar seus bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="e04ae-167">With MongoDB running as a single instance or installed as a service, you can now start creating and using your databases.</span></span> <span data-ttu-id="e04ae-168">Olá toostart shell administrativo do MongoDB, abrir outra janela do prompt de comando do hello **iniciar** menu e digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e04ae-168">toostart hello MongoDB administrative shell, open another command prompt window from hello **Start** menu, and enter hello following command:</span></span>

```
mongo  
```

<span data-ttu-id="e04ae-169">Você pode listar os bancos de dados de saudação com hello `db` comando.</span><span class="sxs-lookup"><span data-stu-id="e04ae-169">You can list hello databases with hello `db` command.</span></span> <span data-ttu-id="e04ae-170">Inserir alguns dados da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e04ae-170">Insert some data as follows:</span></span>

```
db.foo.insert( { a : 1 } )
```

<span data-ttu-id="e04ae-171">Pesquise por dados da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e04ae-171">Search for data as follows:</span></span>

```
db.foo.find()
```

<span data-ttu-id="e04ae-172">saudação de saída é similar toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="e04ae-172">hello output is similar toohello following example:</span></span>

```
{ "_id" : "ObjectId("57f6a86cee873a6232d74842"), "a" : 1 }
```

<span data-ttu-id="e04ae-173">Saudação de saída `mongo` console da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e04ae-173">Exit hello `mongo` console as follows:</span></span>

```
exit
```

## <a name="configure-firewall-and-network-security-group-rules"></a><span data-ttu-id="e04ae-174">Configurar regras de firewall e de Grupo de Segurança de Rede</span><span class="sxs-lookup"><span data-stu-id="e04ae-174">Configure firewall and Network Security Group rules</span></span>
<span data-ttu-id="e04ae-175">Agora que o MongoDB está instalado e em execução, abra uma porta no Firewall do Windows para conectar-se remotamente tooMongoDB.</span><span class="sxs-lookup"><span data-stu-id="e04ae-175">Now that MongoDB is installed and running, open a port in Windows Firewall so you can remotely connect tooMongoDB.</span></span> <span data-ttu-id="e04ae-176">toocreate uma nova regra de entrada tooallow a porta TCP 27017, abra um prompt do PowerShell administrativo e digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e04ae-176">toocreate a new inbound rule tooallow TCP port 27017, open an administrative PowerShell prompt and enter hello following command:</span></span>

```powerahell
New-NetFirewallRule `
    -DisplayName "Allow MongoDB" `
    -Direction Inbound `
    -Protocol TCP `
    -LocalPort 27017 `
    -Action Allow
```

<span data-ttu-id="e04ae-177">Você também pode criar regra de saudação usando Olá **Firewall do Windows com segurança avançada** ferramenta de gerenciamento gráfico.</span><span class="sxs-lookup"><span data-stu-id="e04ae-177">You can also create hello rule by using hello **Windows Firewall with Advanced Security** graphical management tool.</span></span> <span data-ttu-id="e04ae-178">Crie uma nova regra de entrada tooallow TCP porta 27017.</span><span class="sxs-lookup"><span data-stu-id="e04ae-178">Create a new inbound rule tooallow TCP port 27017.</span></span>

<span data-ttu-id="e04ae-179">Se necessário, crie um grupo de segurança de rede regra tooallow acesso tooMongoDB de fora da sub-rede de rede virtual do Azure existente hello.</span><span class="sxs-lookup"><span data-stu-id="e04ae-179">If needed, create a Network Security Group rule tooallow access tooMongoDB from outside of hello existing Azure virtual network subnet.</span></span> <span data-ttu-id="e04ae-180">Você pode criar regras de grupo de segurança de rede de saudação usando Olá [portal do Azure](nsg-quickstart-portal.md) ou [Azure PowerShell](nsg-quickstart-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e04ae-180">You can create hello Network Security Group rules by using hello [Azure portal](nsg-quickstart-portal.md) or [Azure PowerShell](nsg-quickstart-powershell.md).</span></span> <span data-ttu-id="e04ae-181">Assim como acontece com as regras de Firewall do Windows hello, permitir a interface de rede virtual do TCP porta 27017 toohello da VM MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e04ae-181">As with hello Windows Firewall rules, allow TCP port 27017 toohello virtual network interface of your MongoDB VM.</span></span>

> [!NOTE]
> <span data-ttu-id="e04ae-182">A porta TCP 27017 é saudação padrão usado pelo MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e04ae-182">TCP port 27017 is hello default port used by MongoDB.</span></span> <span data-ttu-id="e04ae-183">Você pode alterar essa porta usando Olá `--port` parâmetro ao iniciar `mongod.exe` manualmente ou de um serviço.</span><span class="sxs-lookup"><span data-stu-id="e04ae-183">You can change this port by using hello `--port` parameter when starting `mongod.exe` manually or from a service.</span></span> <span data-ttu-id="e04ae-184">Se você alterar a porta hello, tornar-se de que tooupdate Olá Firewall do Windows e o grupo de segurança de rede regras em Olá etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="e04ae-184">If you change hello port, make sure tooupdate hello Windows Firewall and Network Security Group rules in hello preceding steps.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e04ae-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e04ae-185">Next steps</span></span>
<span data-ttu-id="e04ae-186">Neste tutorial, você aprendeu como tooinstall e configurar o MongoDB em VM do Windows.</span><span class="sxs-lookup"><span data-stu-id="e04ae-186">In this tutorial, you learned how tooinstall and configure MongoDB on your Windows VM.</span></span> <span data-ttu-id="e04ae-187">Agora você pode acessar MongoDB em sua VM do Windows, por seguintes Olá avançado tópicos Olá [documentação do MongoDB](https://docs.mongodb.com/manual/).</span><span class="sxs-lookup"><span data-stu-id="e04ae-187">You can now access MongoDB on your Windows VM, by following hello advanced topics in hello [MongoDB documentation](https://docs.mongodb.com/manual/).</span></span>

