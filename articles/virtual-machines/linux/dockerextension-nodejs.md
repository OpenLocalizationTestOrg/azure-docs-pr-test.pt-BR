---
title: "Olá aaaUse extensão VM Docker do Azure com hello 1.0 da CLI do Azure | Microsoft Docs"
description: "Saiba como toouse Olá tooquickly de extensão de VM Docker e implantar com segurança um ambiente de Docker no Azure usando o Gerenciador de recursos de modelos."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 2133cdb1af741fe30093910fae5c3b2c91e8d5fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension-with-hello-azure-cli-10"></a><span data-ttu-id="9b483-103">Criar um ambiente de Docker no Azure com extensão de VM Docker Olá Olá 1.0 da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="9b483-103">Create a Docker environment in Azure using hello Docker VM extension with hello Azure CLI 1.0</span></span>
<span data-ttu-id="9b483-104">O docker é uma plataforma geração de imagens que permite que você tooquickly o trabalho com contêineres do Linux (e também do Windows) e o gerenciamento de contêiner populares.</span><span class="sxs-lookup"><span data-stu-id="9b483-104">Docker is a popular container management and imaging platform that allows you tooquickly work with containers on Linux (and Windows as well).</span></span> <span data-ttu-id="9b483-105">No Azure, há várias maneiras que você pode implantar o Docker de acordo com as necessidades de tooyour.</span><span class="sxs-lookup"><span data-stu-id="9b483-105">In Azure, there are various ways you can deploy Docker according tooyour needs.</span></span> <span data-ttu-id="9b483-106">Este artigo enfoca usando a extensão de VM Docker hello e modelos do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b483-106">This article focuses on using hello Docker VM extension and Azure Resource Manager templates.</span></span> 

<span data-ttu-id="9b483-107">Para obter mais informações sobre métodos de implantação diferentes hello, incluindo o uso de máquina do Docker e serviços de contêiner do Azure, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="9b483-107">For more information about hello different deployment methods, including using Docker Machine and Azure Container Services, see hello following articles:</span></span>

* <span data-ttu-id="9b483-108">protótipo tooquickly um aplicativo, você pode criar um único host Docker usando [Docker máquina](docker-machine.md).</span><span class="sxs-lookup"><span data-stu-id="9b483-108">tooquickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md).</span></span>
* <span data-ttu-id="9b483-109">Em ambientes maiores e mais estáveis, você pode usar a extensão de VM do Azure Docker hello, que também oferece suporte a [Docker Compose](https://docs.docker.com/compose/overview/) toogenerate implantações de contêiner consistente.</span><span class="sxs-lookup"><span data-stu-id="9b483-109">For larger, more stable environments, you can use hello Azure Docker VM extension, which also supports [Docker Compose](https://docs.docker.com/compose/overview/) toogenerate consistent container deployments.</span></span> <span data-ttu-id="9b483-110">Este artigo detalha usando a extensão de VM do Azure Docker hello.</span><span class="sxs-lookup"><span data-stu-id="9b483-110">This article details using hello Azure Docker VM extension.</span></span>
* <span data-ttu-id="9b483-111">toobuild ambientes de pronto para produção e escalonável que fornece ferramentas adicionais de planejamento e gerenciamento, você pode implantar um [Docker Swarm cluster nos serviços de contêiner do Azure](../../container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="9b483-111">toobuild production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="9b483-112">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="9b483-112">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="9b483-113">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="9b483-113">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="9b483-114">[1.0 de CLI do Azure](#azure-docker-vm-extension-overview) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="9b483-114">[Azure CLI 1.0](#azure-docker-vm-extension-overview) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="9b483-115">[2.0 do CLI do Azure](dockerextension.md) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="9b483-115">[Azure CLI 2.0](dockerextension.md) - our next generation CLI for hello resource management deployment model</span></span> 

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="9b483-116">Visão geral da extensão de VM do Docker do Azure</span><span class="sxs-lookup"><span data-stu-id="9b483-116">Azure Docker VM extension overview</span></span>
<span data-ttu-id="9b483-117">Olá extensão VM Docker do Azure instala e configura o daemon do Docker hello, cliente do Docker e compor Docker em sua máquina virtual do Linux (VM).</span><span class="sxs-lookup"><span data-stu-id="9b483-117">hello Azure Docker VM extension installs and configures hello Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="9b483-118">Usando a extensão de VM do Azure Docker hello, você tem mais controle e recursos do que simplesmente usando o Docker máquina ou criação de host do Docker Olá por conta própria.</span><span class="sxs-lookup"><span data-stu-id="9b483-118">By using hello Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating hello Docker host yourself.</span></span> <span data-ttu-id="9b483-119">Adicionais esses recursos, tais como [Docker Compose](https://docs.docker.com/compose/overview/), tornar extensão de VM Docker do Azure Olá adequada para ambientes de produção ou desenvolvedor mais robustos.</span><span class="sxs-lookup"><span data-stu-id="9b483-119">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make hello Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="9b483-120">Modelos do Gerenciador de recursos do Azure definem a estrutura inteira saudação do seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="9b483-120">Azure Resource Manager templates define hello entire structure of your environment.</span></span> <span data-ttu-id="9b483-121">Modelos permitem toocreate e configurar recursos como host do Docker Olá máquinas virtuais, armazenamento, controles de acesso baseado em função (RBAC) e diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="9b483-121">Templates allow you toocreate and configure resources such as hello Docker host VMs, storage, Role-Based Access Controls (RBAC), and diagnostics.</span></span> <span data-ttu-id="9b483-122">Você pode reutilizar essas implantações adicionais de toocreate modelos de maneira consistente.</span><span class="sxs-lookup"><span data-stu-id="9b483-122">You can reuse these templates toocreate additional deployments in a consistent manner.</span></span> <span data-ttu-id="9b483-123">Para obter mais informações sobre o Azure Resource Manager e modelos, veja a [Visão geral do Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9b483-123">For more information about Azure Resource Manager and templates, see [Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span> 

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a><span data-ttu-id="9b483-124">Implantar um modelo com hello extensão VM Docker do Azure</span><span class="sxs-lookup"><span data-stu-id="9b483-124">Deploy a template with hello Azure Docker VM extension</span></span>
<span data-ttu-id="9b483-125">Vamos usar um existente toocreate de modelo de início rápido um Ubuntu VM que utilize Olá tooinstall de extensão de VM Docker do Azure e configurar o host do Docker hello.</span><span class="sxs-lookup"><span data-stu-id="9b483-125">Let's use an existing quickstart template toocreate an Ubuntu VM that uses hello Azure Docker VM extension tooinstall and configure hello Docker host.</span></span> <span data-ttu-id="9b483-126">Você pode exibir o modelo de saudação aqui: [implantação simples de uma VM Ubuntu com o Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="9b483-126">You can view hello template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="9b483-127">Você precisa Olá [CLI do Azure mais recentes](../../cli-install-nodejs.md) instalado e registrado usando o modo do Gerenciador de recursos de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="9b483-127">You need hello [latest Azure CLI](../../cli-install-nodejs.md) installed and logged in using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="9b483-128">Implante o modelo de saudação usando Olá CLI do Azure, especificando o modelo de saudação URI.</span><span class="sxs-lookup"><span data-stu-id="9b483-128">Deploy hello template using hello Azure CLI, specifying hello template URI.</span></span> <span data-ttu-id="9b483-129">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *westus* local.</span><span class="sxs-lookup"><span data-stu-id="9b483-129">hello following example creates a resource group named *myResourceGroup* in hello *westus* location.</span></span> <span data-ttu-id="9b483-130">Use seu próprio nome de grupo de recursos e local da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="9b483-130">Use your own resource group name and location as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="9b483-131">Responder Olá prompts tooname sua conta de armazenamento, forneça um nome de usuário e a senha e forneça um nome DNS.</span><span class="sxs-lookup"><span data-stu-id="9b483-131">Answer hello prompts tooname your storage account, provide a username and password, and provide a DNS name.</span></span> <span data-ttu-id="9b483-132">saudação de saída é similar toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="9b483-132">hello output is similar toohello following example:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Updating resource group myResourceGroup
info:    Updated resource group myResourceGroup
info:    Supply values for hello following parameters
newStorageAccountName: mystorageaccount
adminUsername: azureuser
adminPassword: P@ssword!
dnsNameForPublicIP: mypublicidns
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

<span data-ttu-id="9b483-133">Olá CLI do Azure retorna toohello prompt após alguns segundos, mas o host do Docker ainda está sendo criado e configurado por Olá extensão VM Docker do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b483-133">hello Azure CLI returns you toohello prompt after only a few seconds, but your Docker host is still being created and configured by hello Azure Docker VM extension.</span></span> <span data-ttu-id="9b483-134">Leva alguns minutos para Olá toofinish de implantação.</span><span class="sxs-lookup"><span data-stu-id="9b483-134">It takes a few minutes for hello deployment toofinish.</span></span> <span data-ttu-id="9b483-135">Você pode exibir detalhes sobre o status de host do Docker hello usando Olá `azure vm show` comando.</span><span class="sxs-lookup"><span data-stu-id="9b483-135">You can view details about hello Docker host status using hello `azure vm show` command.</span></span>

<span data-ttu-id="9b483-136">Olá, exemplo a seguir verifica o status de saudação do hello VM denominada *myDockerVM* (Olá nome padrão do modelo hello, não altere esse nome) no grupo de recursos de saudação denominado *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="9b483-136">hello following example checks hello status of hello VM named *myDockerVM* (hello default name from hello template - don't change this name) in hello resource group named *myResourceGroup*.</span></span> <span data-ttu-id="9b483-137">Digite o nome de Olá Olá do grupo de recursos criado na saudação anterior etapa:</span><span class="sxs-lookup"><span data-stu-id="9b483-137">Enter hello name of hello resource group you created in hello preceding step:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myDockerVM
```

<span data-ttu-id="9b483-138">Olá saída de hello `azure vm show` comando é semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="9b483-138">hello output of hello `azure vm show` command is similar toohello following example:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myDockerVM"
+ Looking up hello NIC "myVMNicD"
+ Looking up hello public ip "myPublicIPD"
data:    Id                              :/subscriptions/guid/resourceGroups/myresourcegroup/providers/Microsoft.Compute/virtualMachines/MyDockerVM
data:    ProvisioningState               :Succeeded
data:    Name                            :MyDockerVM
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
[...]
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-33-D3-95
data:          Provisioning State        :Succeeded
data:          Name                      :myVMNicD
data:          Location                  :westus
data:            Public IP address       :13.91.107.235
data:            FQDN                    :mypublicdns.westus.cloudapp.azure.com
data:
data:    Diagnostics Instance View:
info:    vm show command OK
```

<span data-ttu-id="9b483-139">Topo Olá da saída de hello, você verá Olá **ProvisioningState** de saudação VM.</span><span class="sxs-lookup"><span data-stu-id="9b483-139">Near hello top of hello output, you see hello **ProvisioningState** of hello VM.</span></span> <span data-ttu-id="9b483-140">Quando exibe *êxito*, Olá implantação for concluída e você pode SSH toohello VM.</span><span class="sxs-lookup"><span data-stu-id="9b483-140">When this displays *Succeeded*, hello deployment has finished and you can SSH toohello VM.</span></span>

<span data-ttu-id="9b483-141">Final de saudação da saída de hello *FQDN* exibe o nome de domínio totalmente qualificado de saudação do seu host do Docker.</span><span class="sxs-lookup"><span data-stu-id="9b483-141">Towards hello end of hello output, *FQDN* displays hello fully qualified domain name of your Docker host.</span></span> <span data-ttu-id="9b483-142">O FQDN é o que você use host do Docker tooyour tooSSH em Olá restantes etapas.</span><span class="sxs-lookup"><span data-stu-id="9b483-142">This FQDN is what you use tooSSH tooyour Docker host in hello remaining steps.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="9b483-143">Implantar seu primeiro contêiner nginx</span><span class="sxs-lookup"><span data-stu-id="9b483-143">Deploy your first nginx container</span></span>
<span data-ttu-id="9b483-144">Uma vez Olá implantação for concluída, SSH tooyour novo host do Docker do computador local.</span><span class="sxs-lookup"><span data-stu-id="9b483-144">Once hello deployment has finished, SSH tooyour new Docker host from your local computer.</span></span> <span data-ttu-id="9b483-145">Insira seu próprio nome de usuário e o FQDN da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="9b483-145">Enter your own username and FQDN as follows:</span></span>

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="9b483-146">Depois de conectado toohello host Docker, vamos executar um contêiner nginx:</span><span class="sxs-lookup"><span data-stu-id="9b483-146">Once logged in toohello Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="9b483-147">saída de Hello é semelhante toohello exemplo a seguir como Olá nginx imagem é baixada e um contêiner iniciado:</span><span class="sxs-lookup"><span data-stu-id="9b483-147">hello output is similar toohello following example as hello nginx image is downloaded and a container started:</span></span>

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

<span data-ttu-id="9b483-148">Verifique o status de saudação de contêineres de saudação em execução no host do Docker da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="9b483-148">Check hello status of hello containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="9b483-149">saída de Hello é semelhante toohello exemplo a seguir, mostrando o contêiner Olá nginx está em execução e as portas TCP 80 e 443 e encaminhadas:</span><span class="sxs-lookup"><span data-stu-id="9b483-149">hello output is similar toohello following example, showing that hello nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="9b483-150">toosee seu contêiner em ação, abra um navegador da web e digite o nome FQDN de saudação do seu host do Docker:</span><span class="sxs-lookup"><span data-stu-id="9b483-150">toosee your container in action, open up a web browser and enter hello FQDN name of your Docker host:</span></span>

![Contêiner ngnix em execução](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="9b483-152">Referência de modelo da extensão de VM do Docker do Azure</span><span class="sxs-lookup"><span data-stu-id="9b483-152">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="9b483-153">exemplo de Hello anterior usa um modelo existente do guia de início rápido.</span><span class="sxs-lookup"><span data-stu-id="9b483-153">hello previous example uses an existing quickstart template.</span></span> <span data-ttu-id="9b483-154">Você também pode implantar a extensão de VM do Azure Docker Olá com seus próprios modelos do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="9b483-154">You can also deploy hello Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="9b483-155">toodo, então, adicionar Olá tooyour modelos de Gerenciador de recursos a seguir, a definição de saudação *vmName* da VM adequadamente:</span><span class="sxs-lookup"><span data-stu-id="9b483-155">toodo so, add hello following tooyour Resource Manager templates, defining hello *vmName* of your VM appropriately:</span></span>

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
    "typeHandlerVersion": "1.1",
    "autoUpgradeMinorVersion": true,
    "settings": {},
    "protectedSettings": {}
  }
}
```

<span data-ttu-id="9b483-156">Você pode encontrar um passo a passo mais detalhado de como usar modelos do Gerenciador de Recursos lendo a [Visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9b483-156">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b483-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9b483-157">Next steps</span></span>
<span data-ttu-id="9b483-158">Pode ser muito[configurar Olá Docker daemon TCP porta](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), entender [segurança de Docker](https://docs.docker.com/engine/security/security/), ou implantar contêineres usando [Docker Compose](https://docs.docker.com/compose/overview/).</span><span class="sxs-lookup"><span data-stu-id="9b483-158">You may wish too[configure hello Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="9b483-159">Para obter mais informações sobre Olá extensão da VM Docker do Azure em si, consulte Olá [GitHub projeto](https://github.com/Azure/azure-docker-extension/).</span><span class="sxs-lookup"><span data-stu-id="9b483-159">For more information on hello Azure Docker VM Extension itself, see hello [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="9b483-160">Ler mais informações sobre as opções implantação Docker de saudação adicionais no Azure:</span><span class="sxs-lookup"><span data-stu-id="9b483-160">Read more information about hello additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="9b483-161">Use Docker máquina com hello driver do Azure</span><span class="sxs-lookup"><span data-stu-id="9b483-161">Use Docker Machine with hello Azure driver</span></span>](docker-machine.md)  
* <span data-ttu-id="9b483-162">[Introdução ao Docker e compor toodefine e executar um aplicativo de multi-contêiner em uma máquina virtual do Azure](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="9b483-162">[Get Started with Docker and Compose toodefine and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md).</span></span>
* [<span data-ttu-id="9b483-163">Implantar um cluster do Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="9b483-163">Deploy an Azure Container Service cluster</span></span>](../../container-service/dcos-swarm/container-service-deployment.md)

