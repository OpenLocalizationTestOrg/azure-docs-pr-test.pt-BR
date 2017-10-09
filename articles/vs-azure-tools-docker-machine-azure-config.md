---
title: "hospeda aaaCreate Docker no Azure com o Docker máquina | Microsoft Docs"
description: "Descreve o uso de hosts de docker toocreate Docker máquina no Azure."
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 7a3ff6e1-fa93-4a62-b524-ab182d2fea08
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: fbf67e8189bbf33f874c4a9b619a931f28ccee12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-docker-hosts-in-azure-with-docker-machine"></a><span data-ttu-id="ed3d2-103">Criar hosts do Docker no Azure com docker-machine</span><span class="sxs-lookup"><span data-stu-id="ed3d2-103">Create Docker Hosts in Azure with Docker-Machine</span></span>
<span data-ttu-id="ed3d2-104">Executando [Docker](https://www.docker.com/) contêineres requer um daemon do docker host VM em execução hello.</span><span class="sxs-lookup"><span data-stu-id="ed3d2-104">Running [Docker](https://www.docker.com/) containers requires a host VM running hello docker daemon.</span></span>
<span data-ttu-id="ed3d2-105">Este tópico descreve como Olá toouse [docker máquina](https://docs.docker.com/machine/) comando toocreate novas VMs do Linux, configurada com hello daemon do Docker, em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="ed3d2-105">This topic describes how toouse hello [docker-machine](https://docs.docker.com/machine/) command toocreate new Linux VMs, configured with hello Docker daemon, running in Azure.</span></span> 

<span data-ttu-id="ed3d2-106">**Observação:**</span><span class="sxs-lookup"><span data-stu-id="ed3d2-106">**Note:**</span></span> 

* <span data-ttu-id="ed3d2-107">*Este artigo depende do docker-machine 0.9.0-rc2 ou superior*</span><span class="sxs-lookup"><span data-stu-id="ed3d2-107">*This article depends on docker-machine version 0.9.0-rc2 or greater*</span></span>
* <span data-ttu-id="ed3d2-108">*Contêineres do Windows terá suporte por meio de docker-máquina no hello futuro próximo*</span><span class="sxs-lookup"><span data-stu-id="ed3d2-108">*Windows Containers will be supported through docker-machine in hello near future*</span></span>

## <a name="create-vms-with-docker-machine"></a><span data-ttu-id="ed3d2-109">Criar VMs com o computador Docker</span><span class="sxs-lookup"><span data-stu-id="ed3d2-109">Create VMs with Docker Machine</span></span>
<span data-ttu-id="ed3d2-110">Criar docker host VMs no Azure com hello `docker-machine create` comando usando Olá `azure` driver.</span><span class="sxs-lookup"><span data-stu-id="ed3d2-110">Create docker host VMs in Azure with hello `docker-machine create` command using hello `azure` driver.</span></span> 

<span data-ttu-id="ed3d2-111">Olá driver do Azure requer sua ID de assinatura.</span><span class="sxs-lookup"><span data-stu-id="ed3d2-111">hello Azure driver requires your subscription ID.</span></span> <span data-ttu-id="ed3d2-112">Você pode usar o hello [CLI do Azure](cli-install-nodejs.md) ou hello [Portal do Azure](https://portal.azure.com) tooretrieve sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed3d2-112">You can use hello [Azure CLI](cli-install-nodejs.md) or hello [Azure Portal](https://portal.azure.com) tooretrieve your Azure Subscription.</span></span> 

<span data-ttu-id="ed3d2-113">**Usando Olá Portal do Azure**</span><span class="sxs-lookup"><span data-stu-id="ed3d2-113">**Using hello Azure Portal**</span></span>

* <span data-ttu-id="ed3d2-114">Selecione **assinaturas** Olá navegação esquerdo página e cópia Olá da id de assinatura.</span><span class="sxs-lookup"><span data-stu-id="ed3d2-114">Select **Subscriptions** from hello left navigation page and copy hello subscription id.</span></span>

<span data-ttu-id="ed3d2-115">**Usando Olá CLI do Azure**</span><span class="sxs-lookup"><span data-stu-id="ed3d2-115">**Using hello Azure CLI**</span></span>

* <span data-ttu-id="ed3d2-116">Tipo ```azure account list``` e id de assinatura de saudação de cópia.</span><span class="sxs-lookup"><span data-stu-id="ed3d2-116">Type ```azure account list``` and copy hello subscription id.</span></span>

<span data-ttu-id="ed3d2-117">Tipo `docker-machine create --driver azure` toosee Olá opções e seus valores padrão.</span><span class="sxs-lookup"><span data-stu-id="ed3d2-117">Type `docker-machine create --driver azure` toosee hello options and their default values.</span></span>
<span data-ttu-id="ed3d2-118">Você também pode ver Olá [documentação do Driver do Docker do Azure](https://docs.docker.com/machine/drivers/azure/) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="ed3d2-118">You can also see hello [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/) for more info.</span></span> 

<span data-ttu-id="ed3d2-119">Olá exemplo a seguir se baseia Olá [valores padrão](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), mas ele se desejar definir esses valores:</span><span class="sxs-lookup"><span data-stu-id="ed3d2-119">hello following example relies upon hello [default values](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), but it does optionally set these values:</span></span> 

* <span data-ttu-id="ed3d2-120">dns do Azure para nome hello associado com o IP público hello e certificados gerados.</span><span class="sxs-lookup"><span data-stu-id="ed3d2-120">azure-dns for hello name associated with hello public IP and certificates generated.</span></span> <span data-ttu-id="ed3d2-121">Esse é o nome DNS de saudação de sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ed3d2-121">This is hello DNS name of your virtual machine.</span></span> <span data-ttu-id="ed3d2-122">Olá VM pode, em seguida, com segurança parar, versão IP dinâmico Olá e fornecer Olá capacidade tooreconnect após Olá vm começa novamente com um novo IP.</span><span class="sxs-lookup"><span data-stu-id="ed3d2-122">hello VM can then safely stop, release hello dynamic IP, and provide hello ability tooreconnect after hello vm starts again with a new IP.</span></span> <span data-ttu-id="ed3d2-123">prefixo do nome Hello deve ser exclusivo para essa região UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="ed3d2-123">hello name prefix must be unique for that region  UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span></span>
* <span data-ttu-id="ed3d2-124">Abra a porta 80 no hello VM para acesso de saída à internet</span><span class="sxs-lookup"><span data-stu-id="ed3d2-124">open port 80 on hello VM for outbound internet access</span></span>
* <span data-ttu-id="ed3d2-125">tamanho da saudação um armazenamento VM tooutilize mais rápido premium</span><span class="sxs-lookup"><span data-stu-id="ed3d2-125">size of hello VM tooutilize faster premium storage</span></span>
* <span data-ttu-id="ed3d2-126">armazenamento Premium usado para o disco de vm Olá</span><span class="sxs-lookup"><span data-stu-id="ed3d2-126">premium storage used for hello vm disk</span></span>

```
docker-machine create -d azure --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> --azure-dns <Your UNIQUE_DNSNAME_PREFIX> --azure-open-port 80 --azure-size Standard_DS1_v2 --azure-storage-type "Premium_LRS" mydockerhost 
```

## <a name="choose-a-docker-host-with-docker-machine"></a><span data-ttu-id="ed3d2-127">Escolha um host docker com docker-machine</span><span class="sxs-lookup"><span data-stu-id="ed3d2-127">Choose a docker host with docker-machine</span></span>
<span data-ttu-id="ed3d2-128">Depois que você tem uma entrada na máquina de docker para o host, você pode definir o host de padrão de saudação ao executar os comandos.</span><span class="sxs-lookup"><span data-stu-id="ed3d2-128">Once you have an entry in docker-machine for your host, you can set hello default host when running docker commands.</span></span>

## <a name="using-powershell"></a><span data-ttu-id="ed3d2-129">Usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="ed3d2-129">Using PowerShell</span></span>
```powershell
docker-machine env MyDockerHost | Invoke-Expression 
```

## <a name="using-bash"></a><span data-ttu-id="ed3d2-130">Como usar o Bash</span><span class="sxs-lookup"><span data-stu-id="ed3d2-130">Using Bash</span></span>
```bash
eval $(docker-machine env MyDockerHost)
```

<span data-ttu-id="ed3d2-131">Agora você pode executar os comandos no host especificado Olá</span><span class="sxs-lookup"><span data-stu-id="ed3d2-131">You can now run docker commands against hello specified host</span></span>

```
docker ps
docker info
```

## <a name="run-a-container"></a><span data-ttu-id="ed3d2-132">Executar um contêiner</span><span class="sxs-lookup"><span data-stu-id="ed3d2-132">Run a container</span></span>
<span data-ttu-id="ed3d2-133">Com um host configurado, agora você pode executar um tootest de servidor da web simples se o host foi configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="ed3d2-133">With a host configured, you can now run a simple web server tootest whether your host was configured correctly.</span></span>
<span data-ttu-id="ed3d2-134">Aqui é usar uma imagem padrão nginx, especificar que ele deve escutar na porta 80 e que se reinicia a VM do host hello, contêiner Olá reiniciem também (`--restart=always`).</span><span class="sxs-lookup"><span data-stu-id="ed3d2-134">Here we use a standard nginx image, specify that it should listen on port 80, and that if hello host VM restarts, hello container will restart as well (`--restart=always`).</span></span> 

```bash
docker run -d -p 80:80 --restart=always nginx
```

<span data-ttu-id="ed3d2-135">saída de Hello deve ser semelhante a saudação a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed3d2-135">hello output should look something like hello following:</span></span>

```
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
83f52fbfa5f8: Pull complete
fa664caa1402: Pull complete
Digest: sha256:12127e07a75bda1022fbd4ea231f5527a1899aad4679e3940482db3b57383b1d
Status: Downloaded newer image for nginx:latest
25942c35d86fe43c688d0c03ad478f14cc9c16913b0e1c2971cb32eb4d0ab721
```

## <a name="test-hello-container"></a><span data-ttu-id="ed3d2-136">Contêiner de saudação do teste</span><span class="sxs-lookup"><span data-stu-id="ed3d2-136">Test hello container</span></span>
<span data-ttu-id="ed3d2-137">Examine os contêineres em execução usando `docker ps`:</span><span class="sxs-lookup"><span data-stu-id="ed3d2-137">Examine running containers using `docker ps`:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

<span data-ttu-id="ed3d2-138">E, Olá toosee executando o contêiner, tipo `docker-machine ip <VM name>` toofind Olá IP endereço tooenter no navegador de saudação:</span><span class="sxs-lookup"><span data-stu-id="ed3d2-138">And, toosee hello running container, type `docker-machine ip <VM name>` toofind hello IP address tooenter in hello browser:</span></span>

```
PS C:\> docker-machine ip MyDockerHost
191.237.46.90
```

![Contêiner ngnix em execução](./media/vs-azure-tools-docker-machine-azure-config/nginxsuccess.png)

## <a name="summary"></a><span data-ttu-id="ed3d2-140">Resumo</span><span class="sxs-lookup"><span data-stu-id="ed3d2-140">Summary</span></span>
<span data-ttu-id="ed3d2-141">Com o docker-machine você pode provisionar hosts do docker facilmente no Azure para suas validações individuais de host do docker.</span><span class="sxs-lookup"><span data-stu-id="ed3d2-141">With docker-machine, you can easily provision docker hosts in Azure for your individual docker host validations.</span></span>
<span data-ttu-id="ed3d2-142">Para a produção de hospedagem de contêineres, consulte Olá [serviço de contêiner do Azure](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="ed3d2-142">For production hosting of containers, see hello [Azure Container Service](http://aka.ms/AzureContainerService)</span></span>

<span data-ttu-id="ed3d2-143">toodevelop .NET Core aplicativos com o Visual Studio, consulte [Docker Tools para Visual Studio](http://aka.ms/DockerToolsForVS)</span><span class="sxs-lookup"><span data-stu-id="ed3d2-143">toodevelop .NET Core Applications with Visual Studio, see [Docker Tools for Visual Studio](http://aka.ms/DockerToolsForVS)</span></span>

