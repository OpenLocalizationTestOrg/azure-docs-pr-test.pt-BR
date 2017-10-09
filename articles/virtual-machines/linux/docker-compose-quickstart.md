---
title: aaaUse Docker Compose em uma VM do Linux no Azure | Microsoft Docs
description: "Como toouse Docker e compor em máquinas virtuais Linux Olá CLI do Azure"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 02ab8cf9-318d-4a28-9d0c-4a31dccc2a84
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: cf7254ad4813ccdc641fcacbb06ed1514a93cee5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-docker-and-compose-toodefine-and-run-a-multi-container-application-in-azure"></a><span data-ttu-id="c8b15-103">Obter Introdução ao Docker e compor toodefine e executar um aplicativo de contêiner vários no Azure</span><span class="sxs-lookup"><span data-stu-id="c8b15-103">Get started with Docker and Compose toodefine and run a multi-container application in Azure</span></span>
<span data-ttu-id="c8b15-104">Com [redigir](http://github.com/docker/compose), você usar um toodefine do arquivo de texto simples, um aplicativo que consiste em vários contêineres de Docker.</span><span class="sxs-lookup"><span data-stu-id="c8b15-104">With [Compose](http://github.com/docker/compose), you use a simple text file toodefine an application consisting of multiple Docker containers.</span></span> <span data-ttu-id="c8b15-105">Em seguida, você criar seu aplicativo em um único comando que faz toodeploy seu ambiente definido.</span><span class="sxs-lookup"><span data-stu-id="c8b15-105">You then spin up your application in a single command that does everything toodeploy your defined environment.</span></span> <span data-ttu-id="c8b15-106">Por exemplo, este artigo mostra como tooquickly configurado um blog do WordPress com um back-end banco de dados SQL MariaDB em uma VM do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c8b15-106">As an example, this article shows you how tooquickly set up a WordPress blog with a backend MariaDB SQL database on an Ubuntu VM.</span></span> <span data-ttu-id="c8b15-107">Você também pode usar tooset compor aplicativos mais complexos.</span><span class="sxs-lookup"><span data-stu-id="c8b15-107">You can also use Compose tooset up more complex applications.</span></span>


## <a name="set-up-a-linux-vm-as-a-docker-host"></a><span data-ttu-id="c8b15-108">Configurar uma VM Linux como um host do Docker</span><span class="sxs-lookup"><span data-stu-id="c8b15-108">Set up a Linux VM as a Docker host</span></span>
<span data-ttu-id="c8b15-109">Você pode usar vários procedimentos do Azure e as imagens disponíveis ou modelos do Gerenciador de recursos no Azure Marketplace de saudação toocreate uma VM do Linux e configurá-lo como um host Docker.</span><span class="sxs-lookup"><span data-stu-id="c8b15-109">You can use various Azure procedures and available images or Resource Manager templates in hello Azure Marketplace toocreate a Linux VM and set it up as a Docker host.</span></span> <span data-ttu-id="c8b15-110">Por exemplo, consulte [usando Olá extensão da VM Docker toodeploy seu ambiente](dockerextension.md) tooquickly criar uma VM Ubuntu com hello extensão VM Docker do Azure usando um [quickstart modelo](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="c8b15-110">For example, see [Using hello Docker VM Extension toodeploy your environment](dockerextension.md) tooquickly create an Ubuntu VM with hello Azure Docker VM extension by using a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="c8b15-111">Quando você usa a extensão de VM Docker hello, sua VM é automaticamente configurada como um host Docker e compor já está instalado.</span><span class="sxs-lookup"><span data-stu-id="c8b15-111">When you use hello Docker VM extension, your VM is automatically set up as a Docker host and Compose is already installed.</span></span>


### <a name="create-docker-host-with-azure-cli-20"></a><span data-ttu-id="c8b15-112">Criar host do Docker com a CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="c8b15-112">Create Docker host with Azure CLI 2.0</span></span>
<span data-ttu-id="c8b15-113">Saudação de instalação mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) e fazer logon na conta do Azure usando o tooan [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="c8b15-113">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="c8b15-114">Primeiro, crie um grupo de recursos para seu ambiente do Docker com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="c8b15-114">First, create a resource group for your Docker environment with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="c8b15-115">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *westus* local:</span><span class="sxs-lookup"><span data-stu-id="c8b15-115">hello following example creates a resource group named *myResourceGroup* in hello *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="c8b15-116">Em seguida, implantar uma VM com [criar implantação de grupo az](/cli/azure/group/deployment#create) que inclui a extensão de VM do Azure Docker de saudação do [este modelo do Gerenciador de recursos do Azure no GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="c8b15-116">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes hello Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="c8b15-117">Forneça seus próprios valores para *newStorageAccountName*, *adminUsername*, *adminPassword* e *dnsNameForPublicIP*:</span><span class="sxs-lookup"><span data-stu-id="c8b15-117">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="c8b15-118">Leva alguns minutos para Olá toofinish de implantação.</span><span class="sxs-lookup"><span data-stu-id="c8b15-118">It takes a few minutes for hello deployment toofinish.</span></span> <span data-ttu-id="c8b15-119">Quando terminar de implantação Olá, [mover etapa toonext](#verify-that-compose-is-installed) tooSSH tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="c8b15-119">Once hello deployment is finished, [move toonext step](#verify-that-compose-is-installed) tooSSH tooyour VM.</span></span> 

<span data-ttu-id="c8b15-120">Opcionalmente, a solicitação de toohello de controle de retorno de tooinstead e implantação Olá permitem continuar no plano de fundo Olá, adicione Olá `--no-wait` sinalizador toohello antes do comando.</span><span class="sxs-lookup"><span data-stu-id="c8b15-120">Optionally, tooinstead return control toohello prompt and let hello deployment continue in hello background, add hello `--no-wait` flag toohello preceding command.</span></span> <span data-ttu-id="c8b15-121">Esse processo permite que você tooperform outro trabalho no hello CLI interromper a implantação de saudação por alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="c8b15-121">This process allows you tooperform other work in hello CLI while hello deployment continues for a few minutes.</span></span> <span data-ttu-id="c8b15-122">Você pode exibir detalhes sobre o status do host Docker Olá com [Mostrar de vm az](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="c8b15-122">You can then view details about hello Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="c8b15-123">Olá, exemplo a seguir verifica o status de saudação do hello VM denominada *myDockerVM* (Olá nome padrão do modelo hello, não altere esse nome) no grupo de recursos de saudação denominado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="c8b15-123">hello following example checks hello status of hello VM named *myDockerVM* (hello default name from hello template - don't change this name) in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="c8b15-124">Quando esse comando retorna *êxito*, Olá implantação for concluída e você poderá SSH toohello VM em Olá etapa a seguir.</span><span class="sxs-lookup"><span data-stu-id="c8b15-124">When this command returns *Succeeded*, hello deployment has finished and you can SSH toohello VM in hello following step.</span></span>


## <a name="verify-that-compose-is-installed"></a><span data-ttu-id="c8b15-125">Verificar se o Compose está instalado</span><span class="sxs-lookup"><span data-stu-id="c8b15-125">Verify that Compose is installed</span></span>
<span data-ttu-id="c8b15-126">Quando terminar de implantação Olá, SSH tooyour novo host do Docker usando o nome DNS de saudação que você forneceu durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="c8b15-126">Once hello deployment is finished, SSH tooyour new Docker host using hello DNS name you provided during deployment.</span></span> <span data-ttu-id="c8b15-127">Você pode usar `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` tooview detalhes de sua VM, incluindo o nome DNS hello.</span><span class="sxs-lookup"><span data-stu-id="c8b15-127">You can use  `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` tooview details of your VM, including hello DNS name.</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="c8b15-128">toocheck compor estiver instalado em Olá VM, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c8b15-128">toocheck that Compose is installed on hello VM, run hello following command:</span></span>

```bash
docker-compose --version
```

<span data-ttu-id="c8b15-129">Você verá uma saída semelhante muito*docker-compor 1.6.2, crie 4d 72027*.</span><span class="sxs-lookup"><span data-stu-id="c8b15-129">You see output similar too*docker-compose 1.6.2, build 4d72027*.</span></span>

> [!TIP]
> <span data-ttu-id="c8b15-130">Se você tiver usado outro método toocreate um host Docker e precisa tooinstall redigir por conta própria, consulte Olá [compor documentação](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span><span class="sxs-lookup"><span data-stu-id="c8b15-130">If you used another method toocreate a Docker host and need tooinstall Compose yourself, see hello [Compose documentation](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span></span>


## <a name="create-a-docker-composeyml-configuration-file"></a><span data-ttu-id="c8b15-131">Criar um arquivo de configuração docker-compose.yml</span><span class="sxs-lookup"><span data-stu-id="c8b15-131">Create a docker-compose.yml configuration file</span></span>
<span data-ttu-id="c8b15-132">Agora você criará um `docker-compose.yml` arquivo, que é apenas um arquivo de configuração de texto, toodefine Olá Docker contêineres toorun em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="c8b15-132">Next you create a `docker-compose.yml` file, which is just a text configuration file, toodefine hello Docker containers toorun on hello VM.</span></span> <span data-ttu-id="c8b15-133">arquivo Hello Especifica Olá imagem toorun em cada contêiner (ou pode ser uma compilação de um Dockerfile), variáveis de ambiente necessários e dependências, portas e links de saudação entre contêineres.</span><span class="sxs-lookup"><span data-stu-id="c8b15-133">hello file specifies hello image toorun on each container (or it could be a build from a Dockerfile), necessary environment variables and dependencies, ports, and hello links between containers.</span></span> <span data-ttu-id="c8b15-134">Para obter detalhes sobre a sintaxe do arquivo yml, veja a [referência de arquivo do Redigir](https://docs.docker.com/compose/compose-file/).</span><span class="sxs-lookup"><span data-stu-id="c8b15-134">For details on yml file syntax, see [Compose file reference](https://docs.docker.com/compose/compose-file/).</span></span>

<span data-ttu-id="c8b15-135">Criar hello *docker compose.yml* arquivos da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="c8b15-135">Create hello *docker-compose.yml* file as follows:</span></span>

```bash
touch docker-compose.yml
```

<span data-ttu-id="c8b15-136">Use o tooadd do editor de texto favorito algum arquivo toohello de dados.</span><span class="sxs-lookup"><span data-stu-id="c8b15-136">Use your favorite text editor tooadd some data toohello file.</span></span> <span data-ttu-id="c8b15-137">Olá, exemplo a seguir usa Olá *vi* editor:</span><span class="sxs-lookup"><span data-stu-id="c8b15-137">hello following example uses hello *vi* editor:</span></span>

```bash
vi docker-compose.yml
```

<span data-ttu-id="c8b15-138">Cole o exemplo a seguir em seu arquivo de texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="c8b15-138">Paste hello following example into your text file.</span></span> <span data-ttu-id="c8b15-139">Essa configuração usa imagens de saudação [DockerHub registro](https://registry.hub.docker.com/_/wordpress/) tooinstall WordPress (Olá código-fonte aberto blogs e conteúdo do sistema de gerenciamento) e um back-end vinculado MariaDB SQL de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c8b15-139">This configuration uses images from hello [DockerHub Registry](https://registry.hub.docker.com/_/wordpress/) tooinstall WordPress (hello open source blogging and content management system) and a linked backend MariaDB SQL database.</span></span> <span data-ttu-id="c8b15-140">Insira seu próprio *MYSQL_ROOT_PASSWORD* da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="c8b15-140">Enter your own *MYSQL_ROOT_PASSWORD* as follows:</span></span>

```sh
wordpress:
  image: wordpress
  links:
    - db:mysql
  ports:
    - 80:80

db:
  image: mariadb
  environment:
    MYSQL_ROOT_PASSWORD: <your password>
```

## <a name="start-hello-containers-with-compose"></a><span data-ttu-id="c8b15-141">Contêineres de saudação inicial com redigir</span><span class="sxs-lookup"><span data-stu-id="c8b15-141">Start hello containers with Compose</span></span>
<span data-ttu-id="c8b15-142">Em Olá mesmo diretório como o *docker compose.yml* arquivo, execute o comando a seguir de saudação (dependendo do seu ambiente, talvez seja necessário toorun `docker-compose` usando `sudo`):</span><span class="sxs-lookup"><span data-stu-id="c8b15-142">In hello same directory as your *docker-compose.yml* file, run hello following command (depending on your environment, you might need toorun `docker-compose` using `sudo`):</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="c8b15-143">Esse comando inicia a contêineres do Docker Olá especificados em *docker compose.yml*.</span><span class="sxs-lookup"><span data-stu-id="c8b15-143">This command starts hello Docker containers specified in *docker-compose.yml*.</span></span> <span data-ttu-id="c8b15-144">Ele usa um ou dois minutos para toocomplete esta etapa.</span><span class="sxs-lookup"><span data-stu-id="c8b15-144">It takes a minute or two for this step toocomplete.</span></span> <span data-ttu-id="c8b15-145">Você verá a saída toohello semelhante exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="c8b15-145">You see output similar toohello following example:</span></span>

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> <span data-ttu-id="c8b15-146">Ser Olá-se de toouse **-d** opção na inicialização para que os contêineres de saudação executado continuamente no plano de fundo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c8b15-146">Be sure toouse hello **-d** option on start-up so that hello containers run in hello background continuously.</span></span>


<span data-ttu-id="c8b15-147">tooverify que são contêineres hello, tipo `docker-compose ps`.</span><span class="sxs-lookup"><span data-stu-id="c8b15-147">tooverify that hello containers are up, type `docker-compose ps`.</span></span> <span data-ttu-id="c8b15-148">Você deve ver algo como:</span><span class="sxs-lookup"><span data-stu-id="c8b15-148">You should see something like:</span></span>

```bash
        Name                       Command               State         Ports
-----------------------------------------------------------------------------------
azureuser_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
azureuser_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:80->80/tcp
```

<span data-ttu-id="c8b15-149">Agora você pode conectar tooWordPress diretamente no hello VM na porta 80.</span><span class="sxs-lookup"><span data-stu-id="c8b15-149">You can now connect tooWordPress directly on hello VM on port 80.</span></span> <span data-ttu-id="c8b15-150">Abra um navegador da web e digite o nome DNS de saudação da VM (como `http://mypublicdns.westus.cloudapp.azure.com`).</span><span class="sxs-lookup"><span data-stu-id="c8b15-150">Open a web browser and enter hello DNS name of your VM (such as `http://mypublicdns.westus.cloudapp.azure.com`).</span></span> <span data-ttu-id="c8b15-151">Agora você deve ver Olá que WordPress iniciar tela, onde você pode concluir a instalação de saudação e introdução ao aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="c8b15-151">You should now see hello WordPress start screen, where you can complete hello installation and get started with hello application.</span></span>

![Tela inicial do WordPress][wordpress_start]

## <a name="next-steps"></a><span data-ttu-id="c8b15-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c8b15-153">Next steps</span></span>
* <span data-ttu-id="c8b15-154">Vá toohello [guia do usuário de extensão de VM Docker](https://github.com/Azure/azure-docker-extension/blob/master/README.md) para obter mais opções tooconfigure Docker e compor em sua VM Docker.</span><span class="sxs-lookup"><span data-stu-id="c8b15-154">Go toohello [Docker VM extension user guide](https://github.com/Azure/azure-docker-extension/blob/master/README.md) for more options tooconfigure Docker and Compose in your Docker VM.</span></span> <span data-ttu-id="c8b15-155">Por exemplo, uma opção é tooput Olá redigir yml arquivo (tooJSON convertido) diretamente na configuração Olá Olá extensão da VM Docker.</span><span class="sxs-lookup"><span data-stu-id="c8b15-155">For example, one option is tooput hello Compose yml file (converted tooJSON) directly in hello configuration of hello Docker VM extension.</span></span>
* <span data-ttu-id="c8b15-156">Check-out Olá [compõem a referência de linha de comando](http://docs.docker.com/compose/reference/) e [guia do usuário](http://docs.docker.com/compose/) para obter mais exemplos de criação e implantação de aplicativos de contêiner vários.</span><span class="sxs-lookup"><span data-stu-id="c8b15-156">Check out hello [Compose command-line reference](http://docs.docker.com/compose/reference/) and [user guide](http://docs.docker.com/compose/) for more examples of building and deploying multi-container apps.</span></span>
* <span data-ttu-id="c8b15-157">Usar um modelo do Gerenciador de recursos do Azure, sua própria ou uma contribuição de saudação [community](https://azure.microsoft.com/documentation/templates/), toodeploy uma VM do Azure com o Docker e um aplicativo configurado com redação.</span><span class="sxs-lookup"><span data-stu-id="c8b15-157">Use an Azure Resource Manager template, either your own or one contributed from hello [community](https://azure.microsoft.com/documentation/templates/), toodeploy an Azure VM with Docker and an application set up with Compose.</span></span> <span data-ttu-id="c8b15-158">Por exemplo, Olá [implantar um blog do WordPress com o Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) Docker usa o modelo e compor tooquickly implantar WordPress com um back-end do MySQL em uma VM do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c8b15-158">For example, hello [Deploy a WordPress blog with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) template uses Docker and Compose tooquickly deploy WordPress with a MySQL backend on an Ubuntu VM.</span></span>
* <span data-ttu-id="c8b15-159">Tente integrar o Docker Compose com um cluster do Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="c8b15-159">Try integrating Docker Compose with a Docker Swarm cluster.</span></span> <span data-ttu-id="c8b15-160">Veja [Using Compose with Swarm (Uso do Redigir com o Swarm)](https://docs.docker.com/compose/swarm/) para obter os cenários.</span><span class="sxs-lookup"><span data-stu-id="c8b15-160">See [Using Compose with Swarm](https://docs.docker.com/compose/swarm/) for scenarios.</span></span>

<!--Image references-->

[wordpress_start]: media/docker-compose-quickstart/WordPress.png
