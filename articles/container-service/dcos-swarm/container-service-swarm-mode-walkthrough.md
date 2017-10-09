---
title: aaaQuickstart - cluster CE do Docker do Azure para Linux | Microsoft Docs
description: "Aprenda rapidamente toocreate um cluster de Docker CE para contêineres do Linux no serviço de contêiner do Azure com hello CLI do Azure."
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
ms.date: 08/25/2017
ms.author: nepeters
ms.custom: 
ms.openlocfilehash: 6c26c12ed085ec379c3486095a5fa51379afc5a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-docker-ce-cluster"></a><span data-ttu-id="a4b38-103">Implantar um cluster do Docker CE</span><span class="sxs-lookup"><span data-stu-id="a4b38-103">Deploy Docker CE cluster</span></span>

<span data-ttu-id="a4b38-104">Esse início rápido, um cluster de Docker CE é implantado usando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4b38-104">In this quick start, a Docker CE cluster is deployed using hello Azure CLI.</span></span> <span data-ttu-id="a4b38-105">Um aplicativo de contêiner vários consistindo de front-end da web e uma instância do Redis, em seguida, é implantado e executado no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="a4b38-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on hello cluster.</span></span> <span data-ttu-id="a4b38-106">Depois de concluído, o aplicativo hello está acessível pela internet de hello.</span><span class="sxs-lookup"><span data-stu-id="a4b38-106">Once completed, hello application is accessible over hello internet.</span></span>

<span data-ttu-id="a4b38-107">O Docker CE no Serviço de Contêiner do Azure está na versão prévia e **não deve ser usado para cargas de trabalho de produção**.</span><span class="sxs-lookup"><span data-stu-id="a4b38-107">Docker CE on Azure Container Service is in preview and **should not be used for production workloads**.</span></span>

<span data-ttu-id="a4b38-108">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="a4b38-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="a4b38-109">Se você escolher tooinstall e usa o hello CLI localmente, este guia de início rápido requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="a4b38-109">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="a4b38-110">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4b38-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a4b38-111">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a4b38-111">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="a4b38-112">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="a4b38-112">Create a resource group</span></span>

<span data-ttu-id="a4b38-113">Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="a4b38-113">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="a4b38-114">Um grupo de recursos do Azure é um grupo lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="a4b38-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="a4b38-115">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *ukwest* local.</span><span class="sxs-lookup"><span data-stu-id="a4b38-115">hello following example creates a resource group named *myResourceGroup* in hello *ukwest* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location ukwest
```

<span data-ttu-id="a4b38-116">Saída:</span><span class="sxs-lookup"><span data-stu-id="a4b38-116">Output:</span></span>

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

## <a name="create-docker-swarm-cluster"></a><span data-ttu-id="a4b38-117">Criar um cluster do Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="a4b38-117">Create Docker Swarm cluster</span></span>

<span data-ttu-id="a4b38-118">Criar um cluster de Docker CE no serviço de contêiner do Azure com hello [az acs criar](/cli/azure/acs#create) comando.</span><span class="sxs-lookup"><span data-stu-id="a4b38-118">Create a Docker CE cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="a4b38-119">Olá, exemplo a seguir cria um cluster denominado *mySwarmCluster* com um Linux mestre de nó e três nós de agente do Linux.</span><span class="sxs-lookup"><span data-stu-id="a4b38-119">hello following example creates a cluster named *mySwarmCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type dockerce --resource-group myResourceGroup --generate-ssh-keys
```

<span data-ttu-id="a4b38-120">Após alguns minutos, o comando de saudação for concluído e retorna informações de formatados em json sobre cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4b38-120">After several minutes, hello command completes and returns json formatted information about hello cluster.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="a4b38-121">Conecte-se o cluster toohello</span><span class="sxs-lookup"><span data-stu-id="a4b38-121">Connect toohello cluster</span></span>

<span data-ttu-id="a4b38-122">Em todo este guia rápido, você precisa Olá FQDN do mestre de Docker Swarm hello e pool de agente Olá Docker.</span><span class="sxs-lookup"><span data-stu-id="a4b38-122">Throughout this quick start, you need hello FQDN of both hello Docker Swarm master and hello Docker agent pool.</span></span> <span data-ttu-id="a4b38-123">Execute Olá tooreturn ambos Olá FQDNs mestre e o agente de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="a4b38-123">Run hello following command tooreturn both hello master and agent FQDNs.</span></span>


```bash
az acs list --resource-group myResourceGroup --query '[*].{Master:masterProfile.fqdn,Agent:agentPoolProfiles[0].fqdn}' -o table
```

<span data-ttu-id="a4b38-124">Saída:</span><span class="sxs-lookup"><span data-stu-id="a4b38-124">Output:</span></span>

```bash
Master                                                               Agent
-------------------------------------------------------------------  --------------------------------------------------------------------
myswarmcluster-myresourcegroup-d5b9d4mgmt.ukwest.cloudapp.azure.com  myswarmcluster-myresourcegroup-d5b9d4agent.ukwest.cloudapp.azure.com
```

<span data-ttu-id="a4b38-125">Crie um SSH mestre do túnel toohello por nuvem.</span><span class="sxs-lookup"><span data-stu-id="a4b38-125">Create an SSH tunnel toohello Swarm master.</span></span> <span data-ttu-id="a4b38-126">Substituir `MasterFQDN` com o endereço FQDN Olá mestre do hello por nuvem.</span><span class="sxs-lookup"><span data-stu-id="a4b38-126">Replace `MasterFQDN` with hello FQDN address of hello Swarm master.</span></span>

```bash
ssh -p 2200 -fNL localhost:2374:/var/run/docker.sock azureuser@MasterFQDN
```

<span data-ttu-id="a4b38-127">Saudação de conjunto `DOCKER_HOST` variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="a4b38-127">Set hello `DOCKER_HOST` environment variable.</span></span> <span data-ttu-id="a4b38-128">Isso permite comandos do docker toorun contra Olá Docker Swarm sem ter que toospecify Olá nome de host de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4b38-128">This allows you toorun docker commands against hello Docker Swarm without having toospecify hello name of hello host.</span></span>

```bash
export DOCKER_HOST=localhost:2374
```

<span data-ttu-id="a4b38-129">Agora você está pronto toorun serviços Docker Olá Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="a4b38-129">You are now ready toorun Docker services on hello Docker Swarm.</span></span>


## <a name="run-hello-application"></a><span data-ttu-id="a4b38-130">Executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="a4b38-130">Run hello application</span></span>

<span data-ttu-id="a4b38-131">Crie um arquivo chamado `azure-vote.yaml` e Olá cópia após o conteúdo nele.</span><span class="sxs-lookup"><span data-stu-id="a4b38-131">Create a file named `azure-vote.yaml` and copy hello following content into it.</span></span>


```yaml
version: '3'
services:
  azure-vote-back:
    image: redis
    ports:
        - "6379:6379"

  azure-vote-front:
    image: microsoft/azure-vote-front:redis-v1
    environment:
      REDIS: azure-vote-back
    ports:
        - "80:80"
```

<span data-ttu-id="a4b38-132">Executar Olá [implantar pilha docker](https://docs.docker.com/engine/reference/commandline/stack_deploy/) toocreate serviço de Azure voto de saudação do comando.</span><span class="sxs-lookup"><span data-stu-id="a4b38-132">Run hello [docker stack deploy](https://docs.docker.com/engine/reference/commandline/stack_deploy/) command toocreate hello Azure Vote service.</span></span>

```bash
docker stack deploy azure-vote --compose-file azure-vote.yaml
```

<span data-ttu-id="a4b38-133">Saída:</span><span class="sxs-lookup"><span data-stu-id="a4b38-133">Output:</span></span>

```bash
Creating network azure-vote_default
Creating service azure-vote_azure-vote-back
Creating service azure-vote_azure-vote-front
```

<span data-ttu-id="a4b38-134">Saudação de uso [docker ps de pilha](https://docs.docker.com/engine/reference/commandline/stack_ps/) comando tooreturn status de implantação de saudação do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="a4b38-134">Use hello [docker stack ps](https://docs.docker.com/engine/reference/commandline/stack_ps/) command tooreturn hello deployment status of hello application.</span></span>

```bash
docker stack ps azure-vote
```

<span data-ttu-id="a4b38-135">Uma vez Olá `CURRENT STATE` de cada serviço é `Running`, aplicativo hello está pronto.</span><span class="sxs-lookup"><span data-stu-id="a4b38-135">Once hello `CURRENT STATE` of each service is `Running`, hello application is ready.</span></span>

```bash
ID                  NAME                            IMAGE                                 NODE                               DESIRED STATE       CURRENT STATE                ERROR               PORTS
tnklkv3ogu3i        azure-vote_azure-vote-front.1   microsoft/azure-vote-front:redis-v1   swarmm-agentpool0-66066781000004   Running             Running 5 seconds ago                            
lg99i4hy68r9        azure-vote_azure-vote-back.1    redis:latest                          swarmm-agentpool0-66066781000002   Running             Running about a minute ago
```

## <a name="test-hello-application"></a><span data-ttu-id="a4b38-136">Testar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="a4b38-136">Test hello application</span></span>

<span data-ttu-id="a4b38-137">Procure toohello FQDN do hello por nuvem agente pool tootest out Olá aplicativo voto do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4b38-137">Browse toohello FQDN of hello Swarm agent pool tootest out hello Azure Vote application.</span></span>

![Imagem de navegação tooAzure voto](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a><span data-ttu-id="a4b38-139">Excluir cluster</span><span class="sxs-lookup"><span data-stu-id="a4b38-139">Delete cluster</span></span>
<span data-ttu-id="a4b38-140">Ao cluster Olá não for mais necessário, você pode usar o hello [excluir grupo de az](/cli/azure/group#delete) comando tooremove grupo de recursos de hello, serviço de contêiner e recursos todos relacionados.</span><span class="sxs-lookup"><span data-stu-id="a4b38-140">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a><span data-ttu-id="a4b38-141">Obter o código de saudação</span><span class="sxs-lookup"><span data-stu-id="a4b38-141">Get hello code</span></span>

<span data-ttu-id="a4b38-142">Nesse início rápido, imagens de contêiner criada previamente foram toocreate usado um serviço do Docker.</span><span class="sxs-lookup"><span data-stu-id="a4b38-142">In this quick start, pre-created container images have been used toocreate a Docker service.</span></span> <span data-ttu-id="a4b38-143">Olá relacionados ao código do aplicativo, Dockerfile, e compor arquivo estão disponíveis no GitHub.</span><span class="sxs-lookup"><span data-stu-id="a4b38-143">hello related application code, Dockerfile, and Compose file are available on GitHub.</span></span>

[<span data-ttu-id="a4b38-144">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="a4b38-144">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="a4b38-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a4b38-145">Next steps</span></span>

<span data-ttu-id="a4b38-146">Nesse início rápido, implantado de um cluster de Docker Swarm e implantado um aplicativo de multi-contêiner tooit.</span><span class="sxs-lookup"><span data-stu-id="a4b38-146">In this quick start, you deployed a Docker Swarm cluster and deployed a multi-container application tooit.</span></span>

<span data-ttu-id="a4b38-147">toolearn sobre a integração de Docker passiva com o Visual Studio Team Services continuar toohello CI/CD com o Docker Swarm e VSTS.</span><span class="sxs-lookup"><span data-stu-id="a4b38-147">toolearn about integrating Docker warm with Visual Studio Team Services, continue toohello CI/CD with Docker Swarm and VSTS.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a4b38-148">CI/CD com Docker Swarm e VSTS</span><span class="sxs-lookup"><span data-stu-id="a4b38-148">CI/CD with Docker Swarm and VSTS</span></span>](./container-service-docker-swarm-setup-ci-cd.md)