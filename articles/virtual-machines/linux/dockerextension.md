---
title: "Olá aaaUse extensão VM Docker do Azure | Microsoft Docs"
description: "Saiba como toouse Olá tooquickly de extensão de VM Docker e com segurança implantar um ambiente de Docker no Azure usando o Gerenciador de recursos de modelos e Olá 2.0 do CLI do Azure"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 936d67d7-6921-4275-bf11-1e0115e66b7f
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 8e43adc594192773466ccd2d3e455105f14c1a61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension"></a><span data-ttu-id="eac29-103">Criar um ambiente de Docker no Azure usando a extensão de VM Docker Olá</span><span class="sxs-lookup"><span data-stu-id="eac29-103">Create a Docker environment in Azure using hello Docker VM extension</span></span>
<span data-ttu-id="eac29-104">O docker é uma plataforma de geração de imagens que permite que você tooquickly o trabalho com contêineres no Linux e o gerenciamento de contêiner populares.</span><span class="sxs-lookup"><span data-stu-id="eac29-104">Docker is a popular container management and imaging platform that allows you tooquickly work with containers on Linux.</span></span> <span data-ttu-id="eac29-105">No Azure, há várias maneiras que você pode implantar o Docker de acordo com as necessidades de tooyour.</span><span class="sxs-lookup"><span data-stu-id="eac29-105">In Azure, there are various ways you can deploy Docker according tooyour needs.</span></span> <span data-ttu-id="eac29-106">Este artigo enfoca usando a extensão de VM Docker hello e modelos do Gerenciador de recursos do Azure com hello 2.0 do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="eac29-106">This article focuses on using hello Docker VM extension and Azure Resource Manager templates with hello Azure CLI 2.0.</span></span> <span data-ttu-id="eac29-107">Você também pode executar essas etapas com hello [Azure CLI 1.0](dockerextension-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="eac29-107">You can also perform these steps with hello [Azure CLI 1.0](dockerextension-nodejs.md).</span></span>

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="eac29-108">Visão geral da extensão de VM do Docker do Azure</span><span class="sxs-lookup"><span data-stu-id="eac29-108">Azure Docker VM extension overview</span></span>
<span data-ttu-id="eac29-109">Olá extensão VM Docker do Azure instala e configura o daemon do Docker hello, cliente do Docker e compor Docker em sua máquina virtual do Linux (VM).</span><span class="sxs-lookup"><span data-stu-id="eac29-109">hello Azure Docker VM extension installs and configures hello Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="eac29-110">Usando a extensão de VM do Azure Docker hello, você tem mais controle e recursos do que simplesmente usando o Docker máquina ou criação de host do Docker Olá por conta própria.</span><span class="sxs-lookup"><span data-stu-id="eac29-110">By using hello Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating hello Docker host yourself.</span></span> <span data-ttu-id="eac29-111">Adicionais esses recursos, tais como [Docker Compose](https://docs.docker.com/compose/overview/), tornar extensão de VM Docker do Azure Olá adequada para ambientes de produção ou desenvolvedor mais robustos.</span><span class="sxs-lookup"><span data-stu-id="eac29-111">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make hello Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="eac29-112">Para obter mais informações sobre métodos de implantação diferentes hello, incluindo o uso de máquina do Docker e serviços de contêiner do Azure, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="eac29-112">For more information about hello different deployment methods, including using Docker Machine and Azure Container Services, see hello following articles:</span></span>

* <span data-ttu-id="eac29-113">protótipo tooquickly um aplicativo, você pode criar um único host Docker usando [Docker máquina](docker-machine.md).</span><span class="sxs-lookup"><span data-stu-id="eac29-113">tooquickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md).</span></span>
* <span data-ttu-id="eac29-114">toobuild ambientes de pronto para produção e escalonável que fornece ferramentas adicionais de planejamento e gerenciamento, você pode implantar um [Docker Swarm cluster nos serviços de contêiner do Azure](../../container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="eac29-114">toobuild production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span></span>

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a><span data-ttu-id="eac29-115">Implantar um modelo com hello extensão VM Docker do Azure</span><span class="sxs-lookup"><span data-stu-id="eac29-115">Deploy a template with hello Azure Docker VM extension</span></span>
<span data-ttu-id="eac29-116">Vamos usar um existente toocreate de modelo de início rápido um Ubuntu VM que utilize Olá tooinstall de extensão de VM Docker do Azure e configurar o host do Docker hello.</span><span class="sxs-lookup"><span data-stu-id="eac29-116">Let's use an existing quickstart template toocreate an Ubuntu VM that uses hello Azure Docker VM extension tooinstall and configure hello Docker host.</span></span> <span data-ttu-id="eac29-117">Você pode exibir o modelo de saudação aqui: [implantação simples de uma VM Ubuntu com o Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="eac29-117">You can view hello template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="eac29-118">Você precisa hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e conectado através de conta do Azure tooan [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="eac29-118">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="eac29-119">Primeiro, crie um grupo de recursos com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="eac29-119">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="eac29-120">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *westus* local:</span><span class="sxs-lookup"><span data-stu-id="eac29-120">hello following example creates a resource group named *myResourceGroup* in hello *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="eac29-121">Em seguida, implantar uma VM com [criar implantação de grupo az](/cli/azure/group/deployment#create) que inclui a extensão de VM do Azure Docker de saudação do [este modelo do Gerenciador de recursos do Azure no GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="eac29-121">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes hello Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="eac29-122">Forneça seus próprios valores para *newStorageAccountName*, *adminUsername*, *adminPassword* e *dnsNameForPublicIP* da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="eac29-122">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP* as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="eac29-123">Leva alguns minutos para Olá toofinish de implantação.</span><span class="sxs-lookup"><span data-stu-id="eac29-123">It takes a few minutes for hello deployment toofinish.</span></span> <span data-ttu-id="eac29-124">Quando terminar de implantação Olá, [mover etapa toonext](#deploy-your-first-nginx-container) tooSSH tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="eac29-124">Once hello deployment is finished, [move toonext step](#deploy-your-first-nginx-container) tooSSH tooyour VM.</span></span> 

<span data-ttu-id="eac29-125">Opcionalmente, a solicitação de toohello de controle de retorno de tooinstead e implantação Olá permitem continuar no plano de fundo Olá, adicione Olá `--no-wait` sinalizador toohello antes do comando.</span><span class="sxs-lookup"><span data-stu-id="eac29-125">Optionally, tooinstead return control toohello prompt and let hello deployment continue in hello background, add hello `--no-wait` flag toohello preceding command.</span></span> <span data-ttu-id="eac29-126">Esse processo permite que você tooperform outro trabalho no hello CLI interromper a implantação de saudação por alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="eac29-126">This process allows you tooperform other work in hello CLI while hello deployment continues for a few minutes.</span></span> 

<span data-ttu-id="eac29-127">Você pode exibir detalhes sobre o status do host Docker Olá com [Mostrar de vm az](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="eac29-127">You can then view details about hello Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="eac29-128">Olá, exemplo a seguir verifica o status de saudação do hello VM denominada *myDockerVM* (Olá nome padrão do modelo hello, não altere esse nome) no grupo de recursos de saudação denominado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="eac29-128">hello following example checks hello status of hello VM named *myDockerVM* (hello default name from hello template - don't change this name) in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="eac29-129">Quando esse comando retorna *êxito*, Olá implantação for concluída e você poderá SSH toohello VM em Olá etapa a seguir.</span><span class="sxs-lookup"><span data-stu-id="eac29-129">When this command returns *Succeeded*, hello deployment has finished and you can SSH toohello VM in hello following step.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="eac29-130">Implantar seu primeiro contêiner nginx</span><span class="sxs-lookup"><span data-stu-id="eac29-130">Deploy your first nginx container</span></span>
<span data-ttu-id="eac29-131">tooview detalhes da VM, incluindo nome DNS hello, usam `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span><span class="sxs-lookup"><span data-stu-id="eac29-131">tooview details of your VM, including hello DNS name, use `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span></span> <span data-ttu-id="eac29-132">SSH tooyour Docker novo host do computador local da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="eac29-132">SSH tooyour new Docker host from your local computer as follows:</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="eac29-133">Depois de conectado toohello host Docker, vamos executar um contêiner nginx:</span><span class="sxs-lookup"><span data-stu-id="eac29-133">Once logged in toohello Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="eac29-134">saída de Hello é semelhante toohello exemplo a seguir como Olá nginx imagem é baixada e um contêiner iniciado:</span><span class="sxs-lookup"><span data-stu-id="eac29-134">hello output is similar toohello following example as hello nginx image is downloaded and a container started:</span></span>

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

<span data-ttu-id="eac29-135">Verifique o status de saudação de contêineres de saudação em execução no host do Docker da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="eac29-135">Check hello status of hello containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="eac29-136">saída de Hello é semelhante toohello exemplo a seguir, mostrando o contêiner Olá nginx está em execução e as portas TCP 80 e 443 e encaminhadas:</span><span class="sxs-lookup"><span data-stu-id="eac29-136">hello output is similar toohello following example, showing that hello nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="eac29-137">toosee seu contêiner em ação, abra um navegador da web e digite o nome DNS de saudação do seu host do Docker:</span><span class="sxs-lookup"><span data-stu-id="eac29-137">toosee your container in action, open up a web browser and enter hello DNS name of your Docker host:</span></span>

![Contêiner ngnix em execução](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="eac29-139">Referência de modelo da extensão de VM do Docker do Azure</span><span class="sxs-lookup"><span data-stu-id="eac29-139">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="eac29-140">exemplo de Hello anterior usa um modelo existente do guia de início rápido.</span><span class="sxs-lookup"><span data-stu-id="eac29-140">hello previous example uses an existing quickstart template.</span></span> <span data-ttu-id="eac29-141">Você também pode implantar a extensão de VM do Azure Docker Olá com seus próprios modelos do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="eac29-141">You can also deploy hello Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="eac29-142">toodo, então, adicionar Olá tooyour modelos de Gerenciador de recursos a seguir, a definição de saudação `vmName` da VM adequadamente:</span><span class="sxs-lookup"><span data-stu-id="eac29-142">toodo so, add hello following tooyour Resource Manager templates, defining hello `vmName` of your VM appropriately:</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "[concat(variables('vmName'), '/DockerExtension'))]",
  "apiVersion": "2015-05-01-preview",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
  ],
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "DockerExtension",
    "typeHandlerVersion": "1.*",
    "autoUpgradeMinorVersion": true,
    "settings": {},
    "protectedSettings": {}
  }
}
```

<span data-ttu-id="eac29-143">Você pode encontrar um passo a passo mais detalhado de como usar modelos do Gerenciador de Recursos lendo a [Visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eac29-143">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="eac29-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="eac29-144">Next steps</span></span>
<span data-ttu-id="eac29-145">Pode ser muito[configurar Olá Docker daemon TCP porta](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), entender [segurança de Docker](https://docs.docker.com/engine/security/security/), ou implantar contêineres usando [Docker Compose](https://docs.docker.com/compose/overview/).</span><span class="sxs-lookup"><span data-stu-id="eac29-145">You may wish too[configure hello Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="eac29-146">Para obter mais informações sobre Olá extensão da VM Docker do Azure em si, consulte Olá [GitHub projeto](https://github.com/Azure/azure-docker-extension/).</span><span class="sxs-lookup"><span data-stu-id="eac29-146">For more information on hello Azure Docker VM Extension itself, see hello [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="eac29-147">Ler mais informações sobre as opções implantação Docker de saudação adicionais no Azure:</span><span class="sxs-lookup"><span data-stu-id="eac29-147">Read more information about hello additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="eac29-148">Use Docker máquina com hello driver do Azure</span><span class="sxs-lookup"><span data-stu-id="eac29-148">Use Docker Machine with hello Azure driver</span></span>](docker-machine.md)  
* <span data-ttu-id="eac29-149">[Introdução ao Docker e compor toodefine e executar um aplicativo de multi-contêiner em uma máquina virtual do Azure](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="eac29-149">[Get Started with Docker and Compose toodefine and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md).</span></span>
* [<span data-ttu-id="eac29-150">Implantar um cluster do Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="eac29-150">Deploy an Azure Container Service cluster</span></span>](../../container-service/dcos-swarm/container-service-deployment.md)

