---
title: Instalar o MongoDB em uma VM Windows no Azure | Microsoft Docs
description: "Saiba como instalar o MongoDB em uma VM do Azure que executa o Windows Server 2012 R2 criada com o modelo de implantação do Resource Manager."
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
ms.openlocfilehash: db1a550b9273925b304fe4280f2a1b0e115f856d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="install-and-configure-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="cefe3-103">Instalar e configurar o MongoDB em uma VM do Windows no Azure</span><span class="sxs-lookup"><span data-stu-id="cefe3-103">Install and configure MongoDB on a Windows VM in Azure</span></span>
<span data-ttu-id="cefe3-104">[O MongoDB](http://www.mongodb.org) é um popular banco de dados NoSQL de código-fonte aberto e de alto desempenho.</span><span class="sxs-lookup"><span data-stu-id="cefe3-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="cefe3-105">Este artigo lhe orienta pela instalação e configuração do MongoDB em uma VM (máquina virtual) do Windows Server 2012 R2 no Azure.</span><span class="sxs-lookup"><span data-stu-id="cefe3-105">This article guides you through installing and configuring MongoDB on a Windows Server 2012 R2 virtual machine (VM) in Azure.</span></span> <span data-ttu-id="cefe3-106">Você também pode [instalar o MongoDB em uma VM do Linux no Azure](../linux/install-mongodb.md).</span><span class="sxs-lookup"><span data-stu-id="cefe3-106">You can also [install MongoDB on a Linux VM in Azure](../linux/install-mongodb.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cefe3-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cefe3-107">Prerequisites</span></span>
<span data-ttu-id="cefe3-108">Antes de instalar e configurar o MongoDB, você precisa criar uma VM e, idealmente, adicionar um disco de dados a ela.</span><span class="sxs-lookup"><span data-stu-id="cefe3-108">Before you install and configure MongoDB, you need to create a VM and, ideally, add a data disk to it.</span></span> <span data-ttu-id="cefe3-109">Consulte os artigos a seguir para criar uma VM e adicionar um disco de dados:</span><span class="sxs-lookup"><span data-stu-id="cefe3-109">See the following articles to create a VM and add a data disk:</span></span>

* <span data-ttu-id="cefe3-110">Criar uma VM do Windows Server usando o [Portal do Azure](quick-create-portal.md) ou o [Azure PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="cefe3-110">Create a Windows Server VM using [the Azure portal](quick-create-portal.md) or [Azure PowerShell](quick-create-powershell.md).</span></span>
* <span data-ttu-id="cefe3-111">Anexar um disco de dados a uma VM do Windows Server usando o [Portal do Azure](attach-managed-disk-portal.md) ou o [Azure PowerShell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="cefe3-111">Attach a data disk to a Windows Server VM using [the Azure portal](attach-managed-disk-portal.md) or [Azure PowerShell](attach-disk-ps.md).</span></span>

<span data-ttu-id="cefe3-112">Para começar a instalar e configurar o MongoDB, [Faça logon em sua VM do Windows Server](connect-logon.md) usando a Área de Trabalho Remota.</span><span class="sxs-lookup"><span data-stu-id="cefe3-112">To begin installing and configuring MongoDB, [log on to your Windows Server VM](connect-logon.md) by using Remote Desktop.</span></span>

## <a name="install-mongodb"></a><span data-ttu-id="cefe3-113">Instalar o MongoDB</span><span class="sxs-lookup"><span data-stu-id="cefe3-113">Install MongoDB</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cefe3-114">Os recursos de segurança do MongoDB, como autenticação e associação com o endereço IP, não são habilitados por padrão.</span><span class="sxs-lookup"><span data-stu-id="cefe3-114">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="cefe3-115">Os recursos de segurança devem ser ativados antes de implantar o MongoDB em um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="cefe3-115">Security features should be enabled before deploying MongoDB to a production environment.</span></span> <span data-ttu-id="cefe3-116">Para obter mais informações, veja [Segurança e Autenticação do MongoDB](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span><span class="sxs-lookup"><span data-stu-id="cefe3-116">For more information, see [MongoDB Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>


1. <span data-ttu-id="cefe3-117">Depois de se conectar à VM usando a Área de Trabalho Remota, abra o Internet Explorer pelo menu **Iniciar** na VM.</span><span class="sxs-lookup"><span data-stu-id="cefe3-117">After you've connected to your VM using Remote Desktop, open Internet Explorer from the **Start** menu on the VM.</span></span>
2. <span data-ttu-id="cefe3-118">Selecione **usar as configurações de segurança, privacidade e compatibilidade recomendadas** quando o Internet Explorer abrir pela primeira vez e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="cefe3-118">Select **Use recommended security, privacy, and compatibility settings** when Internet Explorer first opens, and click **OK**.</span></span>
3. <span data-ttu-id="cefe3-119">A configuração de segurança reforçada do Internet Explorer é habilitada por padrão.</span><span class="sxs-lookup"><span data-stu-id="cefe3-119">Internet Explorer enhanced security configuration is enabled by default.</span></span> <span data-ttu-id="cefe3-120">Adicione o site do MongoDB à lista de sites permitidos:</span><span class="sxs-lookup"><span data-stu-id="cefe3-120">Add the MongoDB website to the list of allowed sites:</span></span>
   
   * <span data-ttu-id="cefe3-121">Selecione o ícone **Ferramentas** no canto superior direito.</span><span class="sxs-lookup"><span data-stu-id="cefe3-121">Select the **Tools** icon in the upper-right corner.</span></span>
   * <span data-ttu-id="cefe3-122">Em **Opções da Internet**, selecione a guia **Segurança**, selecione o ícone **Sites confiáveis**.</span><span class="sxs-lookup"><span data-stu-id="cefe3-122">In **Internet Options**, select the **Security** tab, and then select the **Trusted Sites** icon.</span></span>
   * <span data-ttu-id="cefe3-123">Clique no botão **Sites**.</span><span class="sxs-lookup"><span data-stu-id="cefe3-123">Click the **Sites** button.</span></span> <span data-ttu-id="cefe3-124">Adicione *https://\*.mongodb.org* à lista de sites confiáveis e então feche a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cefe3-124">Add *https://\*.mongodb.org* to the list of trusted sites, and then close the dialog box.</span></span>
     
     ![Definir as configurações de segurança do Internet Explorer](./media/install-mongodb/configure-internet-explorer-security.png)
4. <span data-ttu-id="cefe3-126">Navegue até a página [MongoDB – Downloads](http://www.mongodb.org/downloads) (http://www.mongodb.org/downloads).</span><span class="sxs-lookup"><span data-stu-id="cefe3-126">Browse to the [MongoDB - Downloads](http://www.mongodb.org/downloads) page (http://www.mongodb.org/downloads).</span></span>
5. <span data-ttu-id="cefe3-127">Se necessário, selecione o **Community Server** Edition e, em seguida, selecione a última versão estável atual do Windows Server 2008 R2 64 bits e posterior.</span><span class="sxs-lookup"><span data-stu-id="cefe3-127">If needed, select the **Community Server** edition and then select the latest current stable release for Windows Server 2008 R2 64-bit and later.</span></span> <span data-ttu-id="cefe3-128">Para baixar o instalador, clique em **BAIXAR (msi)**.</span><span class="sxs-lookup"><span data-stu-id="cefe3-128">To download the installer, click **DOWNLOAD (msi)**.</span></span>
   
    ![Baixar o instalador do MongoDB](./media/install-mongodb/download-mongodb.png)
   
    <span data-ttu-id="cefe3-130">Quando o download for concluído, execute o instalador.</span><span class="sxs-lookup"><span data-stu-id="cefe3-130">Run the installer after the download is complete.</span></span>
6. <span data-ttu-id="cefe3-131">Leia e aceite o contrato de licença.</span><span class="sxs-lookup"><span data-stu-id="cefe3-131">Read and accept the license agreement.</span></span> <span data-ttu-id="cefe3-132">Quando solicitado, selecione a instalação **Completa**.</span><span class="sxs-lookup"><span data-stu-id="cefe3-132">When you're prompted, select **Complete** install.</span></span>
7. <span data-ttu-id="cefe3-133">Na primeira tela, clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="cefe3-133">On the final screen, click **Install**.</span></span>

## <a name="configure-the-vm-and-mongodb"></a><span data-ttu-id="cefe3-134">Configurar a VM e o MongoDB</span><span class="sxs-lookup"><span data-stu-id="cefe3-134">Configure the VM and MongoDB</span></span>
1. <span data-ttu-id="cefe3-135">As variáveis de caminho não são atualizadas pelo instalador do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="cefe3-135">The path variables are not updated by the MongoDB installer.</span></span> <span data-ttu-id="cefe3-136">Sem a localização `bin` do MongoDB na variável de caminho, você precisará especificar o caminho completo sempre que usar um executável do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="cefe3-136">Without the MongoDB `bin` location in your path variable, you need to specify the full path each time you use a MongoDB executable.</span></span> <span data-ttu-id="cefe3-137">Para adicionar a localização à variável de caminho:</span><span class="sxs-lookup"><span data-stu-id="cefe3-137">To add the location to your path variable:</span></span>
   
   * <span data-ttu-id="cefe3-138">Clique com o botão direito do mouse no menu **Iniciar** e selecione **Sistema**.</span><span class="sxs-lookup"><span data-stu-id="cefe3-138">Right-click the **Start** menu, and select **System**.</span></span>
   * <span data-ttu-id="cefe3-139">Clique na guia **Configurações avançadas do sistema** e em **Variáveis de Ambiente**.</span><span class="sxs-lookup"><span data-stu-id="cefe3-139">Click **Advanced system settings**, and then click **Environment Variables**.</span></span>
   * <span data-ttu-id="cefe3-140">Em **Variáveis de sistema**, selecione **Caminho** e, em seguida, clique em **Editar**.</span><span class="sxs-lookup"><span data-stu-id="cefe3-140">Under **System variables**, select **Path**, and then click **Edit**.</span></span>
     
     ![Configurar variáveis PATH](./media/install-mongodb/configure-path-variables.png)
     
     <span data-ttu-id="cefe3-142">Adicione o caminho à pasta `bin` do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="cefe3-142">Add the path to your MongoDB `bin` folder.</span></span> <span data-ttu-id="cefe3-143">Geralmente, o MongoDB é instalado em *C:\Arquivos de Programas\MongoDB*.</span><span class="sxs-lookup"><span data-stu-id="cefe3-143">MongoDB is typically installed in *C:\Program Files\MongoDB*.</span></span> <span data-ttu-id="cefe3-144">Verifique se o caminho de instalação na sua VM.</span><span class="sxs-lookup"><span data-stu-id="cefe3-144">Verify the installation path on your VM.</span></span> <span data-ttu-id="cefe3-145">O exemplo a seguir adiciona a localização de instalação padrão do MongoDB à variável `PATH`:</span><span class="sxs-lookup"><span data-stu-id="cefe3-145">The following example adds the default MongoDB install location to the `PATH` variable:</span></span>
     
     ```
     ;C:\Program Files\MongoDB\Server\3.2\bin
     ```
     
     > [!NOTE]
     > <span data-ttu-id="cefe3-146">Certifique-se de adicionar o ponto e vírgula à esquerda (`;`) para indicar que você está adicionando uma localização à variável `PATH`.</span><span class="sxs-lookup"><span data-stu-id="cefe3-146">Be sure to add the leading semicolon (`;`) to indicate that you are adding a location to your `PATH` variable.</span></span>

2. <span data-ttu-id="cefe3-147">Crie diretórios de dados e de log do MongoDB no disco de dados.</span><span class="sxs-lookup"><span data-stu-id="cefe3-147">Create MongoDB data and log directories on your data disk.</span></span> <span data-ttu-id="cefe3-148">No menu **Iniciar**, selecione **Prompt de Comando**.</span><span class="sxs-lookup"><span data-stu-id="cefe3-148">From the **Start** menu, select **Command Prompt**.</span></span> <span data-ttu-id="cefe3-149">Os exemplos a seguir criam os diretórios na unidade F:</span><span class="sxs-lookup"><span data-stu-id="cefe3-149">The following examples create the directories on drive F:</span></span>
   
    ```
    mkdir F:\MongoData
    mkdir F:\MongoLogs
    ```
3. <span data-ttu-id="cefe3-150">Inicie uma instância do MongoDB com o comando a seguir, ajustando o caminho adequadamente para os diretórios de dados e de log:</span><span class="sxs-lookup"><span data-stu-id="cefe3-150">Start a MongoDB instance with the following command, adjusting the path to your data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log
    ```
   
    <span data-ttu-id="cefe3-151">Pode levar alguns minutos para que o MongoDB aloque os arquivos de diário e comece a detectar conexões.</span><span class="sxs-lookup"><span data-stu-id="cefe3-151">It may take several minutes for MongoDB to allocate the journal files and start listening for connections.</span></span> <span data-ttu-id="cefe3-152">Todas as mensagens de log serão direcionadas ao arquivo *F:\MongoLogs\mongolog.log* quando o servidor `mongod.exe` for iniciado e alocar arquivos de diário.</span><span class="sxs-lookup"><span data-stu-id="cefe3-152">All log messages are directed to the *F:\MongoLogs\mongolog.log* file as `mongod.exe` server starts and allocates journal files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="cefe3-153">O prompt de comando permanece focado nessa tarefa enquanto sua instância do MongoDB está em execução.</span><span class="sxs-lookup"><span data-stu-id="cefe3-153">The command prompt stays focused on this task while your MongoDB instance is running.</span></span> <span data-ttu-id="cefe3-154">Deixe a janela de prompt de comando aberta para continuar a executar o MongoDB.</span><span class="sxs-lookup"><span data-stu-id="cefe3-154">Leave the command prompt window open to continue running MongoDB.</span></span> <span data-ttu-id="cefe3-155">Ou, se preferir, instale o MongoDB como um serviço, conforme detalhado na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="cefe3-155">Or, install MongoDB as service, as detailed in the next step.</span></span>

4. <span data-ttu-id="cefe3-156">Para obter uma experiência mais robusta do MongoDB, instale o `mongod.exe` como um serviço.</span><span class="sxs-lookup"><span data-stu-id="cefe3-156">For a more robust MongoDB experience, install the `mongod.exe` as a service.</span></span> <span data-ttu-id="cefe3-157">Criar um serviço significa que você não precisa deixar um prompt de comando em execução cada vez que você deseje usar o MongoDB.</span><span class="sxs-lookup"><span data-stu-id="cefe3-157">Creating a service means you don't need to leave a command prompt running each time you want to use MongoDB.</span></span> <span data-ttu-id="cefe3-158">Crie o serviço da seguinte maneira, ajustando o caminho para os diretórios de dados e de log adequadamente:</span><span class="sxs-lookup"><span data-stu-id="cefe3-158">Create the service as follows, adjusting the path to your data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log `
        --logappend  --install
    ```
   
    <span data-ttu-id="cefe3-159">Isso cria um serviço chamado MongoDB e com a descrição "Mongo DB".</span><span class="sxs-lookup"><span data-stu-id="cefe3-159">The preceding command creates a service named MongoDB, with a description of "Mongo DB".</span></span> <span data-ttu-id="cefe3-160">Os parâmetros a seguir também são especificados:</span><span class="sxs-lookup"><span data-stu-id="cefe3-160">The following parameters are also specified:</span></span>
   
   * <span data-ttu-id="cefe3-161">A opção `--dbpath` especifica o local do diretório de dados.</span><span class="sxs-lookup"><span data-stu-id="cefe3-161">The `--dbpath` option specifies the location of the data directory.</span></span>
   * <span data-ttu-id="cefe3-162">A opção `--logpath` deve ser usada para especificar um arquivo de log, uma vez que o serviço em execução não tem uma janela de comando para exibir a saída.</span><span class="sxs-lookup"><span data-stu-id="cefe3-162">The `--logpath` option must be used to specify a log file, because the running service does not have a command window to display output.</span></span>
   * <span data-ttu-id="cefe3-163">A opção `--logappend` especifica que uma reinicialização do serviço fará com que a saída seja acrescentada ao arquivo de log existente.</span><span class="sxs-lookup"><span data-stu-id="cefe3-163">The `--logappend` option specifies that a restart of the service causes output to append to the existing log file.</span></span>
   
   <span data-ttu-id="cefe3-164">Execute o seguinte comando para iniciar o serviço MongoDB:</span><span class="sxs-lookup"><span data-stu-id="cefe3-164">To start the MongoDB service, run the following command:</span></span>
   
    ```
    net start MongoDB
    ```
   
    <span data-ttu-id="cefe3-165">Para obter mais informações sobre como criar o serviço MongoDB, veja [Configurar um Serviço Windows para o MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span><span class="sxs-lookup"><span data-stu-id="cefe3-165">For more information about creating the MongoDB service, see [Configure a Windows Service for MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span></span>

## <a name="test-the-mongodb-instance"></a><span data-ttu-id="cefe3-166">Testar a instância do MongoDB</span><span class="sxs-lookup"><span data-stu-id="cefe3-166">Test the MongoDB instance</span></span>
<span data-ttu-id="cefe3-167">Com o MongoDB em execução como uma única instância ou instalado como um serviço, agora você pode começar a criar e usar seus bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="cefe3-167">With MongoDB running as a single instance or installed as a service, you can now start creating and using your databases.</span></span> <span data-ttu-id="cefe3-168">Para iniciar o shell administrativo do MongoDB, abra outra janela de prompt de comando do menu **Iniciar** e digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="cefe3-168">To start the MongoDB administrative shell, open another command prompt window from the **Start** menu, and enter the following command:</span></span>

```
mongo  
```

<span data-ttu-id="cefe3-169">Você pode listar os bancos de dados com o comando `db`.</span><span class="sxs-lookup"><span data-stu-id="cefe3-169">You can list the databases with the `db` command.</span></span> <span data-ttu-id="cefe3-170">Inserir alguns dados da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="cefe3-170">Insert some data as follows:</span></span>

```
db.foo.insert( { a : 1 } )
```

<span data-ttu-id="cefe3-171">Pesquise por dados da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="cefe3-171">Search for data as follows:</span></span>

```
db.foo.find()
```

<span data-ttu-id="cefe3-172">A saída deverá ser semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="cefe3-172">The output is similar to the following example:</span></span>

```
{ "_id" : "ObjectId("57f6a86cee873a6232d74842"), "a" : 1 }
```

<span data-ttu-id="cefe3-173">Saia do console `mongo` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="cefe3-173">Exit the `mongo` console as follows:</span></span>

```
exit
```

## <a name="configure-firewall-and-network-security-group-rules"></a><span data-ttu-id="cefe3-174">Configurar regras de firewall e de Grupo de Segurança de Rede</span><span class="sxs-lookup"><span data-stu-id="cefe3-174">Configure firewall and Network Security Group rules</span></span>
<span data-ttu-id="cefe3-175">Agora que o MongoDB está instalado e em execução, abra uma porta no Firewall do Windows para poder se conectar remotamente ao MongoDB.</span><span class="sxs-lookup"><span data-stu-id="cefe3-175">Now that MongoDB is installed and running, open a port in Windows Firewall so you can remotely connect to MongoDB.</span></span> <span data-ttu-id="cefe3-176">Para criar uma nova regra de entrada que permita o uso da porta TCP 27017, abra um prompt do PowerShell com privilégios administrativos e digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="cefe3-176">To create a new inbound rule to allow TCP port 27017, open an administrative PowerShell prompt and enter the following command:</span></span>

```powerahell
New-NetFirewallRule `
    -DisplayName "Allow MongoDB" `
    -Direction Inbound `
    -Protocol TCP `
    -LocalPort 27017 `
    -Action Allow
```

<span data-ttu-id="cefe3-177">Você também pode criar a regra usando a ferramenta de gerenciamento gráfica **Firewall do Windows com Segurança Avançada**.</span><span class="sxs-lookup"><span data-stu-id="cefe3-177">You can also create the rule by using the **Windows Firewall with Advanced Security** graphical management tool.</span></span> <span data-ttu-id="cefe3-178">Crie uma nova regra de entrada para permitir o uso da porta TCP 27017.</span><span class="sxs-lookup"><span data-stu-id="cefe3-178">Create a new inbound rule to allow TCP port 27017.</span></span>

<span data-ttu-id="cefe3-179">Se necessário, crie uma regra de Grupo de Segurança de Rede para permitir o acesso ao MongoDB de fora da sub-rede da rede virtual do Azure existente.</span><span class="sxs-lookup"><span data-stu-id="cefe3-179">If needed, create a Network Security Group rule to allow access to MongoDB from outside of the existing Azure virtual network subnet.</span></span> <span data-ttu-id="cefe3-180">Você pode criar as regras de Grupo de Segurança de Rede usando o [Portal do Azure](nsg-quickstart-portal.md) ou [Azure PowerShell](nsg-quickstart-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="cefe3-180">You can create the Network Security Group rules by using the [Azure portal](nsg-quickstart-portal.md) or [Azure PowerShell](nsg-quickstart-powershell.md).</span></span> <span data-ttu-id="cefe3-181">Assim como acontece com as regras de Firewall do Windows, permita o uso da porta TCP 27017 pela adaptador de rede virtual da VM do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="cefe3-181">As with the Windows Firewall rules, allow TCP port 27017 to the virtual network interface of your MongoDB VM.</span></span>

> [!NOTE]
> <span data-ttu-id="cefe3-182">A porta TCP 27017 é a porta padrão usada pelo MongoDB.</span><span class="sxs-lookup"><span data-stu-id="cefe3-182">TCP port 27017 is the default port used by MongoDB.</span></span> <span data-ttu-id="cefe3-183">Você pode alterar essa porta usando o parâmetro `--port` ao iniciar `mongod.exe` manualmente ou de um serviço.</span><span class="sxs-lookup"><span data-stu-id="cefe3-183">You can change this port by using the `--port` parameter when starting `mongod.exe` manually or from a service.</span></span> <span data-ttu-id="cefe3-184">Se você alterar a porta, deverá certificar-se de atualizar as regras de Firewall do Windows e o grupo de segurança de rede nas etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="cefe3-184">If you change the port, make sure to update the Windows Firewall and Network Security Group rules in the preceding steps.</span></span>


## <a name="next-steps"></a><span data-ttu-id="cefe3-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cefe3-185">Next steps</span></span>
<span data-ttu-id="cefe3-186">Neste tutorial, você também aprendeu como instalar e configurar o MongoDB na VM do Windows.</span><span class="sxs-lookup"><span data-stu-id="cefe3-186">In this tutorial, you learned how to install and configure MongoDB on your Windows VM.</span></span> <span data-ttu-id="cefe3-187">Agora você pode acessar o MongoDB na VM do Windows seguindo os tópicos avançados na [documentação do MongoDB](https://docs.mongodb.com/manual/).</span><span class="sxs-lookup"><span data-stu-id="cefe3-187">You can now access MongoDB on your Windows VM, by following the advanced topics in the [MongoDB documentation](https://docs.mongodb.com/manual/).</span></span>

