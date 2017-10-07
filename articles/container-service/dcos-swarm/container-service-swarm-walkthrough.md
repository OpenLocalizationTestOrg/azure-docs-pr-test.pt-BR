---
title: aaaQuickstart - Azure Docker Swarm cluster para Linux | Microsoft Docs
description: "Aprenda rapidamente toocreate um cluster de Docker Swarm para contêineres do Linux no serviço de contêiner do Azure com hello CLI do Azure."
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, Docker, Swarm
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/14/2017
ms.author: nepeters
ms.custom: 
ms.openlocfilehash: 3028d2d00585360ec163518bf98f69bb0dd44dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-docker-swarm-cluster"></a><span data-ttu-id="82f89-103">Implantar cluster do Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="82f89-103">Deploy Docker Swarm cluster</span></span>

<span data-ttu-id="82f89-104">Esse início rápido, um cluster de Docker Swarm é implantado usando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="82f89-104">In this quick start, a Docker Swarm cluster is deployed using hello Azure CLI.</span></span> <span data-ttu-id="82f89-105">Um aplicativo de contêiner vários consistindo de front-end da web e uma instância do Redis, em seguida, é implantado e executado no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="82f89-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on hello cluster.</span></span> <span data-ttu-id="82f89-106">Depois de concluído, o aplicativo hello está acessível pela internet de hello.</span><span class="sxs-lookup"><span data-stu-id="82f89-106">Once completed, hello application is accessible over hello internet.</span></span>

<span data-ttu-id="82f89-107">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="82f89-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="82f89-108">Este guia de início rápido requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="82f89-108">This quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="82f89-109">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="82f89-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="82f89-110">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="82f89-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="82f89-111">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="82f89-111">Create a resource group</span></span>

<span data-ttu-id="82f89-112">Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="82f89-112">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="82f89-113">Um grupo de recursos do Azure é um grupo lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="82f89-113">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="82f89-114">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *westus* local.</span><span class="sxs-lookup"><span data-stu-id="82f89-114">hello following example creates a resource group named *myResourceGroup* in hello *westus* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="82f89-115">Saída:</span><span class="sxs-lookup"><span data-stu-id="82f89-115">Output:</span></span>

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westcentralus",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-docker-swarm-cluster"></a><span data-ttu-id="82f89-116">Criar um cluster do Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="82f89-116">Create Docker Swarm cluster</span></span>

<span data-ttu-id="82f89-117">Criar um cluster de Docker Swarm no serviço de contêiner do Azure com hello [az acs criar](/cli/azure/acs#create) comando.</span><span class="sxs-lookup"><span data-stu-id="82f89-117">Create a Docker Swarm cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="82f89-118">Olá, exemplo a seguir cria um cluster denominado *mySwarmCluster* com um Linux mestre de nó e três nós de agente do Linux.</span><span class="sxs-lookup"><span data-stu-id="82f89-118">hello following example creates a cluster named *mySwarmCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type Swarm --resource-group myResourceGroup --generate-ssh-keys
```

<span data-ttu-id="82f89-119">Após alguns minutos, o comando de saudação for concluído e retorna informações de formatados em json sobre cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="82f89-119">After several minutes, hello command completes and returns json formatted information about hello cluster.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="82f89-120">Conecte-se o cluster toohello</span><span class="sxs-lookup"><span data-stu-id="82f89-120">Connect toohello cluster</span></span>

<span data-ttu-id="82f89-121">Em todo este guia rápido, é necessário o endereço IP de saudação do mestre de Docker Swarm hello e pool de agente Olá Docker.</span><span class="sxs-lookup"><span data-stu-id="82f89-121">Throughout this quick start, you need hello IP address of both hello Docker Swarm master and hello Docker agent pool.</span></span> <span data-ttu-id="82f89-122">Execute Olá tooreturn de comando a seguir os dois endereços IP.</span><span class="sxs-lookup"><span data-stu-id="82f89-122">Run hello following command tooreturn both IP addresses.</span></span>


```bash
az network public-ip list --resource-group myResourceGroup --query '[*].{Name:name,IPAddress:ipAddress}' -o table
```

<span data-ttu-id="82f89-123">Saída:</span><span class="sxs-lookup"><span data-stu-id="82f89-123">Output:</span></span>

```bash
Name                                                                 IPAddress
-------------------------------------------------------------------  -------------
swarmm-agent-ip-myswarmcluster-myresourcegroup-d5b9d4agent-66066781  52.179.23.131
swarmm-master-ip-myswarmcluster-myresourcegroup-d5b9d4mgmt-66066781  52.141.37.199
```

<span data-ttu-id="82f89-124">Crie um SSH mestre do túnel toohello por nuvem.</span><span class="sxs-lookup"><span data-stu-id="82f89-124">Create an SSH tunnel toohello Swarm master.</span></span> <span data-ttu-id="82f89-125">Substituir `IPAddress` com o endereço IP de saudação do mestre do hello por nuvem.</span><span class="sxs-lookup"><span data-stu-id="82f89-125">Replace `IPAddress` with hello IP address of hello Swarm master.</span></span>

```bash
ssh -p 2200 -fNL 2375:localhost:2375 azureuser@IPAddress
```

<span data-ttu-id="82f89-126">Saudação de conjunto `DOCKER_HOST` variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="82f89-126">Set hello `DOCKER_HOST` environment variable.</span></span> <span data-ttu-id="82f89-127">Isso permite comandos do docker toorun contra Olá Docker Swarm sem ter que toospecify Olá nome de host de saudação.</span><span class="sxs-lookup"><span data-stu-id="82f89-127">This allows you toorun docker commands against hello Docker Swarm without having toospecify hello name of hello host.</span></span>

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="82f89-128">Agora você está pronto toorun serviços Docker Olá Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="82f89-128">You are now ready toorun Docker services on hello Docker Swarm.</span></span>


## <a name="run-hello-application"></a><span data-ttu-id="82f89-129">Executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="82f89-129">Run hello application</span></span>

<span data-ttu-id="82f89-130">Crie um arquivo chamado `docker-compose.yaml` e Olá cópia após o conteúdo nele.</span><span class="sxs-lookup"><span data-stu-id="82f89-130">Create a file named `docker-compose.yaml` and copy hello following content into it.</span></span>

```yaml
version: '3'
services:
  azure-vote-back:
    image: redis
    container_name: azure-vote-back
    ports:
        - "6379:6379"

  azure-vote-front:
    image: microsoft/azure-vote-front:redis-v1
    container_name: azure-vote-front
    environment:
      REDIS: azure-vote-back
    ports:
        - "80:80"
```

<span data-ttu-id="82f89-131">Execute Olá após comando toocreate hello Azure voto serviço.</span><span class="sxs-lookup"><span data-stu-id="82f89-131">Run hello following command toocreate hello Azure Vote service.</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="82f89-132">Saída:</span><span class="sxs-lookup"><span data-stu-id="82f89-132">Output:</span></span>

```bash
Creating network "user_default" with hello default driver
Pulling azure-vote-front (microsoft/azure-vote-front:redis-v1)...
swarm-agent-EE873B23000005: Pulling microsoft/azure-vote-front:redis-v1...
swarm-agent-EE873B23000004: Pulling microsoft/azure-vote-front:redis-v1... : downloaded
Pulling azure-vote-back (redis:latest)...
swarm-agent-EE873B23000004: Pulling redis:latest... : downloaded
Creating azure-vote-front ... 
Creating azure-vote-back ... 
Creating azure-vote-front
Creating azure-vote-back ...
```

## <a name="test-hello-application"></a><span data-ttu-id="82f89-133">Testar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="82f89-133">Test hello application</span></span>

<span data-ttu-id="82f89-134">Procure o endereço IP toohello Olá por nuvem agente pool tootest aplicativo do Azure voto hello.</span><span class="sxs-lookup"><span data-stu-id="82f89-134">Browse toohello IP address of hello Swarm agent pool tootest out hello Azure Vote application.</span></span>

![Imagem de navegação tooAzure voto](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a><span data-ttu-id="82f89-136">Excluir cluster</span><span class="sxs-lookup"><span data-stu-id="82f89-136">Delete cluster</span></span>
<span data-ttu-id="82f89-137">Ao cluster Olá não for mais necessário, você pode usar o hello [excluir grupo de az](/cli/azure/group#delete) comando tooremove grupo de recursos de hello, serviço de contêiner e recursos todos relacionados.</span><span class="sxs-lookup"><span data-stu-id="82f89-137">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a><span data-ttu-id="82f89-138">Obter o código de saudação</span><span class="sxs-lookup"><span data-stu-id="82f89-138">Get hello code</span></span>

<span data-ttu-id="82f89-139">Nesse início rápido, imagens de contêiner criada previamente foram toocreate usado um serviço do Docker.</span><span class="sxs-lookup"><span data-stu-id="82f89-139">In this quick start, pre-created container images have been used toocreate a Docker service.</span></span> <span data-ttu-id="82f89-140">Olá relacionados ao código do aplicativo, Dockerfile, e compor arquivo estão disponíveis no GitHub.</span><span class="sxs-lookup"><span data-stu-id="82f89-140">hello related application code, Dockerfile, and Compose file are available on GitHub.</span></span>

[<span data-ttu-id="82f89-141">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="82f89-141">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="82f89-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="82f89-142">Next steps</span></span>

<span data-ttu-id="82f89-143">Nesse início rápido, implantado de um cluster de Docker Swarm e implantado um aplicativo de multi-contêiner tooit.</span><span class="sxs-lookup"><span data-stu-id="82f89-143">In this quick start, you deployed a Docker Swarm cluster and deployed a multi-container application tooit.</span></span>

<span data-ttu-id="82f89-144">toolearn sobre a integração de Docker passiva com o Visual Studio Team Services continuar toohello CI/CD com o Docker Swarm e VSTS.</span><span class="sxs-lookup"><span data-stu-id="82f89-144">toolearn about integrating Docker warm with Visual Studio Team Services, continue toohello CI/CD with Docker Swarm and VSTS.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="82f89-145">CI/CD com Docker Swarm e VSTS</span><span class="sxs-lookup"><span data-stu-id="82f89-145">CI/CD with Docker Swarm and VSTS</span></span>](./container-service-docker-swarm-setup-ci-cd.md)