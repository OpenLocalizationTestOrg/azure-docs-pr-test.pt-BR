---
title: "Usar a extensão de VM do Docker do Azure | Microsoft Docs"
description: "Saiba como usar a extensão de VM do Docker para implantar de maneira rápida e segura um ambiente Docker no Azure usando modelos do Resource Manager e a CLI 2.0 do Azure"
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
ms.openlocfilehash: 63d0d80999fd57d014c74d5c6aef3733ec2afe85
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-docker-environment-in-azure-using-the-docker-vm-extension"></a><span data-ttu-id="9c63b-103">Criar um ambiente de Docker no Azure usando a extensão de VM do Docker</span><span class="sxs-lookup"><span data-stu-id="9c63b-103">Create a Docker environment in Azure using the Docker VM extension</span></span>
<span data-ttu-id="9c63b-104">O Docker é uma plataforma popular de geração de imagens e gerenciamento de contêineres que permite que você trabalhe rapidamente com contêineres no Linux.</span><span class="sxs-lookup"><span data-stu-id="9c63b-104">Docker is a popular container management and imaging platform that allows you to quickly work with containers on Linux.</span></span> <span data-ttu-id="9c63b-105">No Azure, há várias maneiras de que você pode implantar o Docker de acordo com suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="9c63b-105">In Azure, there are various ways you can deploy Docker according to your needs.</span></span> <span data-ttu-id="9c63b-106">Este artigo se concentra no uso de modelos do Azure Resource Manager e da extensão de VM do Docker com a CLI 2.0 do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c63b-106">This article focuses on using the Docker VM extension and Azure Resource Manager templates with the Azure CLI 2.0.</span></span> <span data-ttu-id="9c63b-107">Você também pode executar essas etapas com a [CLI do Azure 1.0](dockerextension-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="9c63b-107">You can also perform these steps with the [Azure CLI 1.0](dockerextension-nodejs.md).</span></span>

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="9c63b-108">Visão geral da extensão de VM do Docker do Azure</span><span class="sxs-lookup"><span data-stu-id="9c63b-108">Azure Docker VM extension overview</span></span>
<span data-ttu-id="9c63b-109">A Extensão de VM do Docker do Azure instala e configura o daemon do Docker, o cliente do Docker e o Docker Compose em sua VM (máquina virtual) Linux.</span><span class="sxs-lookup"><span data-stu-id="9c63b-109">The Azure Docker VM extension installs and configures the Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="9c63b-110">Usando a extensão de VM do Docker do Azure, você tem mais controle e recursos do que simplesmente usando a Máquina do Docker ou criando o host do Docker você mesmo.</span><span class="sxs-lookup"><span data-stu-id="9c63b-110">By using the Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating the Docker host yourself.</span></span> <span data-ttu-id="9c63b-111">Esses recursos adicionais, como [Docker Compose](https://docs.docker.com/compose/overview/), tornam a extensão de VM do Docker do Azure adequada para ambientes de produção ou de desenvolvedor mais robustos.</span><span class="sxs-lookup"><span data-stu-id="9c63b-111">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make the Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="9c63b-112">Para obter mais informações sobre os diferentes métodos de implantação, incluindo o uso de Máquina do Docker e dos Serviços de Contêiner do Azure, consulte os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="9c63b-112">For more information about the different deployment methods, including using Docker Machine and Azure Container Services, see the following articles:</span></span>

* <span data-ttu-id="9c63b-113">Para fazer rapidamente o protótipo de um aplicativo, você pode criar um único host do Docker usando a [Máquina do Docker](docker-machine.md).</span><span class="sxs-lookup"><span data-stu-id="9c63b-113">To quickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md).</span></span>
* <span data-ttu-id="9c63b-114">Você também pode implantar um [cluster do Docker Swarm nos Serviços de Contêiner do Azure](../../container-service/dcos-swarm/container-service-deployment.md) para criar ambientes escalonáveis, prontos para produção que fornecem ferramentas de gerenciamento e agendamento adicionais.</span><span class="sxs-lookup"><span data-stu-id="9c63b-114">To build production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span></span>

## <a name="deploy-a-template-with-the-azure-docker-vm-extension"></a><span data-ttu-id="9c63b-115">Implantar um modelo com a extensão de VM do Docker do Azure</span><span class="sxs-lookup"><span data-stu-id="9c63b-115">Deploy a template with the Azure Docker VM extension</span></span>
<span data-ttu-id="9c63b-116">Vamos usar um modelo existente de início rápido para criar uma VM do Ubuntu que use a extensão de VM do Docker do Azure para instalar e configurar o host do Docker.</span><span class="sxs-lookup"><span data-stu-id="9c63b-116">Let's use an existing quickstart template to create an Ubuntu VM that uses the Azure Docker VM extension to install and configure the Docker host.</span></span> <span data-ttu-id="9c63b-117">Você pode conferir o modelo aqui: [Simple deployment of an Ubuntu VM with Docker (Implantação simples de uma VM do Ubuntu com o Docker)](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="9c63b-117">You can view the template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="9c63b-118">É preciso ter a [CLI 2.0 do Azure](/cli/azure/install-az-cli2) mais recente instalada e conectada a uma conta do Azure usando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="9c63b-118">You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="9c63b-119">Primeiro, crie um grupo de recursos com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="9c63b-119">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="9c63b-120">O exemplo a seguir cria um grupo de recursos chamado *myResourceGroup* na localização *westus*:</span><span class="sxs-lookup"><span data-stu-id="9c63b-120">The following example creates a resource group named *myResourceGroup* in the *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="9c63b-121">Em seguida, implante uma VM com [az group deployment create](/cli/azure/group/deployment#create), o que inclui a extensão da VM do Docker do Azure [deste modelo do Azure Resource Manager no GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="9c63b-121">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes the Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="9c63b-122">Forneça seus próprios valores para *newStorageAccountName*, *adminUsername*, *adminPassword* e *dnsNameForPublicIP* da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="9c63b-122">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP* as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="9c63b-123">Leva alguns minutos para a conclusão da implantação.</span><span class="sxs-lookup"><span data-stu-id="9c63b-123">It takes a few minutes for the deployment to finish.</span></span> <span data-ttu-id="9c63b-124">Após a conclusão da implantação, [vá para a próxima etapa](#deploy-your-first-nginx-container) a fim de usar SSH em sua VM.</span><span class="sxs-lookup"><span data-stu-id="9c63b-124">Once the deployment is finished, [move to next step](#deploy-your-first-nginx-container) to SSH to your VM.</span></span> 

<span data-ttu-id="9c63b-125">Como opção, para, em vez disso, retornar o controle ao prompt e permitir que a implantação continue em segundo plano, adicione o sinalizador `--no-wait` ao comando anterior.</span><span class="sxs-lookup"><span data-stu-id="9c63b-125">Optionally, to instead return control to the prompt and let the deployment continue in the background, add the `--no-wait` flag to the preceding command.</span></span> <span data-ttu-id="9c63b-126">Esse processo permite que você execute outro trabalho na CLI enquanto a implantação continua por alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="9c63b-126">This process allows you to perform other work in the CLI while the deployment continues for a few minutes.</span></span> 

<span data-ttu-id="9c63b-127">Você pode exibir detalhes sobre o status de host do Docker usando o comando [az vm show](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="9c63b-127">You can then view details about the Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="9c63b-128">O exemplo a seguir verifica o status da VM chamada *myDockerVM* (o nome padrão do modelo – não altere esse nome) no grupo de recursos chamado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="9c63b-128">The following example checks the status of the VM named *myDockerVM* (the default name from the template - don't change this name) in the resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="9c63b-129">Quando esse comando retornar *Succeeded*, a implantação terá sido concluída e você poderá usar SSH na VM na etapa a seguir.</span><span class="sxs-lookup"><span data-stu-id="9c63b-129">When this command returns *Succeeded*, the deployment has finished and you can SSH to the VM in the following step.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="9c63b-130">Implantar seu primeiro contêiner nginx</span><span class="sxs-lookup"><span data-stu-id="9c63b-130">Deploy your first nginx container</span></span>
<span data-ttu-id="9c63b-131">Para exibir detalhes de sua VM, incluindo o nome DNS, use `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span><span class="sxs-lookup"><span data-stu-id="9c63b-131">To view details of your VM, including the DNS name, use `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span></span> <span data-ttu-id="9c63b-132">Use o SSH para o host do seu novo Docker no computador local, como se segue:</span><span class="sxs-lookup"><span data-stu-id="9c63b-132">SSH to your new Docker host from your local computer as follows:</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="9c63b-133">Após fazer logon no host do Docker, vamos executar um contêiner nginx:</span><span class="sxs-lookup"><span data-stu-id="9c63b-133">Once logged in to the Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="9c63b-134">A saída é semelhante ao exemplo a seguir, conforme a imagem de nginx é baixada um contêiner é iniciado:</span><span class="sxs-lookup"><span data-stu-id="9c63b-134">The output is similar to the following example as the nginx image is downloaded and a container started:</span></span>

```bash
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

<span data-ttu-id="9c63b-135">Verifique o status dos contêineres em execução no host do Docker da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="9c63b-135">Check the status of the containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="9c63b-136">A saída é semelhante ao exemplo a seguir, mostrando que o contêiner nginx está em execução nas portas TCP 80 e 443 e está sendo encaminhado:</span><span class="sxs-lookup"><span data-stu-id="9c63b-136">The output is similar to the following example, showing that the nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="9c63b-137">Para ver seu contêiner em ação, abra um navegador da Web e digite o nome DNS do host do Docker:</span><span class="sxs-lookup"><span data-stu-id="9c63b-137">To see your container in action, open up a web browser and enter the DNS name of your Docker host:</span></span>

![Contêiner ngnix em execução](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="9c63b-139">Referência de modelo da extensão de VM do Docker do Azure</span><span class="sxs-lookup"><span data-stu-id="9c63b-139">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="9c63b-140">O exemplo anterior usa um modelo de início rápido existente.</span><span class="sxs-lookup"><span data-stu-id="9c63b-140">The previous example uses an existing quickstart template.</span></span> <span data-ttu-id="9c63b-141">Você também pode implantar a extensão de VM do Docker do Azure com seus próprios modelos do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9c63b-141">You can also deploy the Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="9c63b-142">Para fazer isso, adicione o seguinte a seus modelos do Resource Manager, definindo o `vmName` da sua VM adequadamente:</span><span class="sxs-lookup"><span data-stu-id="9c63b-142">To do so, add the following to your Resource Manager templates, defining the `vmName` of your VM appropriately:</span></span>

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

<span data-ttu-id="9c63b-143">Você pode encontrar um passo a passo mais detalhado de como usar modelos do Gerenciador de Recursos lendo a [Visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9c63b-143">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c63b-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9c63b-144">Next steps</span></span>
<span data-ttu-id="9c63b-145">Você poderá [configurar a porta TCP do daemon do Docker](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), compreender a [segurança do Docker](https://docs.docker.com/engine/security/security/) ou implantar contêineres usando o [Docker Compose](https://docs.docker.com/compose/overview/).</span><span class="sxs-lookup"><span data-stu-id="9c63b-145">You may wish to [configure the Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="9c63b-146">Para obter mais informações sobre a extensão de VM do Docker do Azure em si, consulte o [projeto GitHub](https://github.com/Azure/azure-docker-extension/).</span><span class="sxs-lookup"><span data-stu-id="9c63b-146">For more information on the Azure Docker VM Extension itself, see the [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="9c63b-147">Leia mais informações sobre as opções de implantação adicionais do Docker no Azure:</span><span class="sxs-lookup"><span data-stu-id="9c63b-147">Read more information about the additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="9c63b-148">Usar o computador Docker com o driver do Azure</span><span class="sxs-lookup"><span data-stu-id="9c63b-148">Use Docker Machine with the Azure driver</span></span>](docker-machine.md)  
* <span data-ttu-id="9c63b-149">[Introdução ao Docker e Compose para definir e executar um aplicativo de vários contêineres em uma máquina virtual do Azure](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="9c63b-149">[Get Started with Docker and Compose to define and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md).</span></span>
* [<span data-ttu-id="9c63b-150">Implantar um cluster do Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="9c63b-150">Deploy an Azure Container Service cluster</span></span>](../../container-service/dcos-swarm/container-service-deployment.md)

