---
title: Usar o Docker Compose em uma VM Linux no Azure | Microsoft Docs
description: "Como usar o Docker e o Compose em máquinas virtuais Linux com a CLI do Azure"
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
ms.openlocfilehash: 541722cb02dd991228726e62a2304b49cdd806f2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-docker-and-compose-to-define-and-run-a-multi-container-application-in-azure"></a><span data-ttu-id="c3fe6-103">Introdução ao Docker e Compose para definir e executar um aplicativo de vários contêineres no Azure</span><span class="sxs-lookup"><span data-stu-id="c3fe6-103">Get started with Docker and Compose to define and run a multi-container application in Azure</span></span>
<span data-ttu-id="c3fe6-104">Com o [Compose](http://github.com/docker/compose), você usa um arquivo de texto simples para definir um aplicativo que consiste em vários contêineres do Docker.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-104">With [Compose](http://github.com/docker/compose), you use a simple text file to define an application consisting of multiple Docker containers.</span></span> <span data-ttu-id="c3fe6-105">Em seguida, você acelera seu aplicativo com um único comando que faz tudo que é necessário para implantar o ambiente definido.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-105">You then spin up your application in a single command that does everything to deploy your defined environment.</span></span> <span data-ttu-id="c3fe6-106">Por exemplo, este artigo mostra como configurar rapidamente um blog WordPress com um banco de dados SQL MariaDB de back-end em uma VM Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-106">As an example, this article shows you how to quickly set up a WordPress blog with a backend MariaDB SQL database on an Ubuntu VM.</span></span> <span data-ttu-id="c3fe6-107">Você também pode usar o Redigir para configurar aplicativos mais complexos.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-107">You can also use Compose to set up more complex applications.</span></span>


## <a name="set-up-a-linux-vm-as-a-docker-host"></a><span data-ttu-id="c3fe6-108">Configurar uma VM Linux como um host do Docker</span><span class="sxs-lookup"><span data-stu-id="c3fe6-108">Set up a Linux VM as a Docker host</span></span>
<span data-ttu-id="c3fe6-109">Você pode usar vários procedimentos do Azure e imagens disponíveis ou modelos do Resource Manager no Azure Marketplace para criar uma VM do Linux e configurá-la como um host do Docker.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-109">You can use various Azure procedures and available images or Resource Manager templates in the Azure Marketplace to create a Linux VM and set it up as a Docker host.</span></span> <span data-ttu-id="c3fe6-110">Por exemplo, veja [Uso da extensão de VM do Docker para implantar seu ambiente](dockerextension.md) para criar rapidamente uma VM do Ubuntu com a extensão de VM do Docker do Azure usando um [modelo de início rápido](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="c3fe6-110">For example, see [Using the Docker VM Extension to deploy your environment](dockerextension.md) to quickly create an Ubuntu VM with the Azure Docker VM extension by using a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="c3fe6-111">Quando você usa a extensão da VM do Docker, sua VM é configurada automaticamente como um host do Docker e o Redigir já está instalado.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-111">When you use the Docker VM extension, your VM is automatically set up as a Docker host and Compose is already installed.</span></span>


### <a name="create-docker-host-with-azure-cli-20"></a><span data-ttu-id="c3fe6-112">Criar host do Docker com a CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="c3fe6-112">Create Docker host with Azure CLI 2.0</span></span>
<span data-ttu-id="c3fe6-113">Instale a [CLI 2.0 do Azure](/cli/azure/install-az-cli2) mais recente e faça logon em uma conta do Azure usando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="c3fe6-113">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="c3fe6-114">Primeiro, crie um grupo de recursos para seu ambiente do Docker com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="c3fe6-114">First, create a resource group for your Docker environment with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="c3fe6-115">O exemplo a seguir cria um grupo de recursos chamado *myResourceGroup* na localização *westus*:</span><span class="sxs-lookup"><span data-stu-id="c3fe6-115">The following example creates a resource group named *myResourceGroup* in the *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="c3fe6-116">Em seguida, implante uma VM com [az group deployment create](/cli/azure/group/deployment#create), o que inclui a extensão da VM do Docker do Azure [deste modelo do Azure Resource Manager no GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="c3fe6-116">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes the Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="c3fe6-117">Forneça seus próprios valores para *newStorageAccountName*, *adminUsername*, *adminPassword* e *dnsNameForPublicIP*:</span><span class="sxs-lookup"><span data-stu-id="c3fe6-117">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="c3fe6-118">Leva alguns minutos para a conclusão da implantação.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-118">It takes a few minutes for the deployment to finish.</span></span> <span data-ttu-id="c3fe6-119">Após a conclusão da implantação, [vá para a próxima etapa](#verify-that-compose-is-installed) a fim de usar SSH em sua VM.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-119">Once the deployment is finished, [move to next step](#verify-that-compose-is-installed) to SSH to your VM.</span></span> 

<span data-ttu-id="c3fe6-120">Como opção, para, em vez disso, retornar o controle ao prompt e permitir que a implantação continue em segundo plano, adicione o sinalizador `--no-wait` ao comando anterior.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-120">Optionally, to instead return control to the prompt and let the deployment continue in the background, add the `--no-wait` flag to the preceding command.</span></span> <span data-ttu-id="c3fe6-121">Esse processo permite que você execute outro trabalho na CLI enquanto a implantação continua por alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-121">This process allows you to perform other work in the CLI while the deployment continues for a few minutes.</span></span> <span data-ttu-id="c3fe6-122">Você pode exibir detalhes sobre o status de host do Docker usando o comando [az vm show](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="c3fe6-122">You can then view details about the Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="c3fe6-123">O exemplo a seguir verifica o status da VM chamada *myDockerVM* (o nome padrão do modelo – não altere esse nome) no grupo de recursos chamado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="c3fe6-123">The following example checks the status of the VM named *myDockerVM* (the default name from the template - don't change this name) in the resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="c3fe6-124">Quando esse comando retornar *Succeeded*, a implantação terá sido concluída e você poderá usar SSH na VM na etapa a seguir.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-124">When this command returns *Succeeded*, the deployment has finished and you can SSH to the VM in the following step.</span></span>


## <a name="verify-that-compose-is-installed"></a><span data-ttu-id="c3fe6-125">Verificar se o Compose está instalado</span><span class="sxs-lookup"><span data-stu-id="c3fe6-125">Verify that Compose is installed</span></span>
<span data-ttu-id="c3fe6-126">Depois que a implantação for concluída, faça a conexão SSH com seu novo host do Docker usando o nome DNS que você forneceu durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-126">Once the deployment is finished, SSH to your new Docker host using the DNS name you provided during deployment.</span></span> <span data-ttu-id="c3fe6-127">Você pode usar `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` para exibir detalhes de sua VM, incluindo o nome DNS.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-127">You can use  `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` to view details of your VM, including the DNS name.</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="c3fe6-128">Para verificar se o Redigir está instalado na VM, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c3fe6-128">To check that Compose is installed on the VM, run the following command:</span></span>

```bash
docker-compose --version
```

<span data-ttu-id="c3fe6-129">Você ver uma saída semelhante a *docker-compose 1.6.2, build 4d72027*.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-129">You see output similar to *docker-compose 1.6.2, build 4d72027*.</span></span>

> [!TIP]
> <span data-ttu-id="c3fe6-130">Se você usou outro método para criar um host do Docker e precisa instalar o Redigir por conta própria, veja a [documentação do Redigir](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span><span class="sxs-lookup"><span data-stu-id="c3fe6-130">If you used another method to create a Docker host and need to install Compose yourself, see the [Compose documentation](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span></span>


## <a name="create-a-docker-composeyml-configuration-file"></a><span data-ttu-id="c3fe6-131">Criar um arquivo de configuração docker-compose.yml</span><span class="sxs-lookup"><span data-stu-id="c3fe6-131">Create a docker-compose.yml configuration file</span></span>
<span data-ttu-id="c3fe6-132">Em seguida, você criará um arquivo `docker-compose.yml` , que é apenas um arquivo de configuração de texto, para definir os contêineres de Docker a serem executados na VM.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-132">Next you create a `docker-compose.yml` file, which is just a text configuration file, to define the Docker containers to run on the VM.</span></span> <span data-ttu-id="c3fe6-133">O arquivo especifica a imagem a ser executada em cada contêiner (ou pode ser um build de um Dockerfile), as variáveis de ambiente e as dependências necessárias, as portas e os links entre contêineres.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-133">The file specifies the image to run on each container (or it could be a build from a Dockerfile), necessary environment variables and dependencies, ports, and the links between containers.</span></span> <span data-ttu-id="c3fe6-134">Para obter detalhes sobre a sintaxe do arquivo yml, veja a [referência de arquivo do Redigir](https://docs.docker.com/compose/compose-file/).</span><span class="sxs-lookup"><span data-stu-id="c3fe6-134">For details on yml file syntax, see [Compose file reference](https://docs.docker.com/compose/compose-file/).</span></span>

<span data-ttu-id="c3fe6-135">Crie o arquivo *docker-compose.yml* da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="c3fe6-135">Create the *docker-compose.yml* file as follows:</span></span>

```bash
touch docker-compose.yml
```

<span data-ttu-id="c3fe6-136">Use seu editor de texto favorito para adicionar alguns dados ao arquivo.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-136">Use your favorite text editor to add some data to the file.</span></span> <span data-ttu-id="c3fe6-137">O exemplo a seguir usa o editor *vi*:</span><span class="sxs-lookup"><span data-stu-id="c3fe6-137">The following example uses the *vi* editor:</span></span>

```bash
vi docker-compose.yml
```

<span data-ttu-id="c3fe6-138">Cole o exemplo a seguir em seu arquivo de texto.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-138">Paste the following example into your text file.</span></span> <span data-ttu-id="c3fe6-139">Essa configuração usa imagens do [Registro do DockerHub](https://registry.hub.docker.com/_/wordpress/) para instalar o WordPress (o sistema de blog e gerenciamento de conteúdo de software livre) e um banco de dados SQL MariaDB de back-end vinculado.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-139">This configuration uses images from the [DockerHub Registry](https://registry.hub.docker.com/_/wordpress/) to install WordPress (the open source blogging and content management system) and a linked backend MariaDB SQL database.</span></span> <span data-ttu-id="c3fe6-140">Insira seu próprio *MYSQL_ROOT_PASSWORD* da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="c3fe6-140">Enter your own *MYSQL_ROOT_PASSWORD* as follows:</span></span>

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

## <a name="start-the-containers-with-compose"></a><span data-ttu-id="c3fe6-141">Iniciar os contêineres com o Compose</span><span class="sxs-lookup"><span data-stu-id="c3fe6-141">Start the containers with Compose</span></span>
<span data-ttu-id="c3fe6-142">No mesmo diretório que seu arquivo *docker-compose.yml*, execute o comando a seguir (dependendo do seu ambiente, talvez seja necessário executar `docker-compose` usando `sudo`):</span><span class="sxs-lookup"><span data-stu-id="c3fe6-142">In the same directory as your *docker-compose.yml* file, run the following command (depending on your environment, you might need to run `docker-compose` using `sudo`):</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="c3fe6-143">Esse comando inicia os contêineres do Docker especificados em *docker-compose.yml*.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-143">This command starts the Docker containers specified in *docker-compose.yml*.</span></span> <span data-ttu-id="c3fe6-144">Leva um ou dois minutos para concluir esta etapa.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-144">It takes a minute or two for this step to complete.</span></span> <span data-ttu-id="c3fe6-145">Você verá uma saída semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="c3fe6-145">You see output similar to the following example:</span></span>

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> <span data-ttu-id="c3fe6-146">Não se esqueça de usar a opção **-d** na inicialização para que os contêineres sejam executados continuamente em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-146">Be sure to use the **-d** option on start-up so that the containers run in the background continuously.</span></span>


<span data-ttu-id="c3fe6-147">Para verificar se os contêineres estão ativos, digite `docker-compose ps`.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-147">To verify that the containers are up, type `docker-compose ps`.</span></span> <span data-ttu-id="c3fe6-148">Você deve ver algo como:</span><span class="sxs-lookup"><span data-stu-id="c3fe6-148">You should see something like:</span></span>

```bash
        Name                       Command               State         Ports
-----------------------------------------------------------------------------------
azureuser_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
azureuser_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:80->80/tcp
```

<span data-ttu-id="c3fe6-149">Agora você pode conectar o WordPress diretamente na VM na porta 80.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-149">You can now connect to WordPress directly on the VM on port 80.</span></span> <span data-ttu-id="c3fe6-150">Abra um navegador da Web e digite o nome DNS da VM (como `http://mypublicdns.westus.cloudapp.azure.com`).</span><span class="sxs-lookup"><span data-stu-id="c3fe6-150">Open a web browser and enter the DNS name of your VM (such as `http://mypublicdns.westus.cloudapp.azure.com`).</span></span> <span data-ttu-id="c3fe6-151">Agora você deve ver a tela inicial do WordPress, na qual você pode concluir a instalação e começar a usar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-151">You should now see the WordPress start screen, where you can complete the installation and get started with the application.</span></span>

![Tela inicial do WordPress][wordpress_start]

## <a name="next-steps"></a><span data-ttu-id="c3fe6-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c3fe6-153">Next steps</span></span>
* <span data-ttu-id="c3fe6-154">Vá para o [Guia do usuário da extensão da VM do Docker](https://github.com/Azure/azure-docker-extension/blob/master/README.md) para obter mais opções para configurar o Docker e o Redigir em sua VM do Docker.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-154">Go to the [Docker VM extension user guide](https://github.com/Azure/azure-docker-extension/blob/master/README.md) for more options to configure Docker and Compose in your Docker VM.</span></span> <span data-ttu-id="c3fe6-155">Por exemplo, uma opção é colocar o arquivo yml do Compose (convertido em JSON) diretamente na configuração da extensão da VM do Docker.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-155">For example, one option is to put the Compose yml file (converted to JSON) directly in the configuration of the Docker VM extension.</span></span>
* <span data-ttu-id="c3fe6-156">Confira a [referência da linha de comando do Compose](http://docs.docker.com/compose/reference/) e o [guia do usuário](http://docs.docker.com/compose/) para obter mais exemplos de criação e implantação de aplicativos com vários contêineres.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-156">Check out the [Compose command-line reference](http://docs.docker.com/compose/reference/) and [user guide](http://docs.docker.com/compose/) for more examples of building and deploying multi-container apps.</span></span>
* <span data-ttu-id="c3fe6-157">Use um modelo do Gerenciador de Recursos do Azure, seu ou da do [comunidade](https://azure.microsoft.com/documentation/templates/), para implantar uma VM do Azure com Docker e um aplicativo configurado com o Redigir.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-157">Use an Azure Resource Manager template, either your own or one contributed from the [community](https://azure.microsoft.com/documentation/templates/), to deploy an Azure VM with Docker and an application set up with Compose.</span></span> <span data-ttu-id="c3fe6-158">Por exemplo, o modelo [Implantar um blog WordPress com Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) usa Docker e Redigir para implantar rapidamente o WordPress com um back-end do MySQL em uma VM do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-158">For example, the [Deploy a WordPress blog with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) template uses Docker and Compose to quickly deploy WordPress with a MySQL backend on an Ubuntu VM.</span></span>
* <span data-ttu-id="c3fe6-159">Tente integrar o Docker Compose com um cluster do Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-159">Try integrating Docker Compose with a Docker Swarm cluster.</span></span> <span data-ttu-id="c3fe6-160">Veja [Using Compose with Swarm (Uso do Redigir com o Swarm)](https://docs.docker.com/compose/swarm/) para obter os cenários.</span><span class="sxs-lookup"><span data-stu-id="c3fe6-160">See [Using Compose with Swarm](https://docs.docker.com/compose/swarm/) for scenarios.</span></span>

<!--Image references-->

[wordpress_start]: media/docker-compose-quickstart/WordPress.png
