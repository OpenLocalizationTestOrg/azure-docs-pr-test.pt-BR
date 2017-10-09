---
title: "aaaDeploy um cluster de contêiner do Docker - CLI do Azure | Microsoft Docs"
description: "Implante uma solução Kubernetes, CD/SO ou Docker Swarm no Serviço de Contêiner do Azure usando a CLI 2.0 do Azure"
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.assetid: 8da267e8-2aeb-4c24-9a7a-65bdca3a82d6
ms.service: container-service
ms.devlang: azurecli
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: saudas
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: cdfa4ce69de343dcc7070bc2c58b5132c4062084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-hello-azure-cli-20"></a><span data-ttu-id="79343-103">Implantar um contêiner do Docker usando hello Azure CLI 2.0 de solução de hospedagem</span><span class="sxs-lookup"><span data-stu-id="79343-103">Deploy a Docker container hosting solution using hello Azure CLI 2.0</span></span>

<span data-ttu-id="79343-104">Saudação de uso `az acs` comandos no toocreate Olá 2.0 do CLI do Azure e gerenciar clusters no serviço de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="79343-104">Use hello `az acs` commands in hello Azure CLI 2.0 toocreate and manage clusters in Azure Container Service.</span></span> <span data-ttu-id="79343-105">Você também pode implantar um cluster do serviço de contêiner do Azure usando Olá [portal do Azure](container-service-deployment.md) ou Olá APIs de serviço de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="79343-105">You can also deploy an Azure Container Service cluster by using hello [Azure portal](container-service-deployment.md) or hello Azure Container Service APIs.</span></span>

<span data-ttu-id="79343-106">Para obter ajuda sobre `az acs` comandos, passar Olá `-h` comando de tooany do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="79343-106">For help on `az acs` commands, pass hello `-h` parameter tooany command.</span></span> <span data-ttu-id="79343-107">Por exemplo: `az acs create -h`.</span><span class="sxs-lookup"><span data-stu-id="79343-107">For example: `az acs create -h`.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="79343-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="79343-108">Prerequisites</span></span>
<span data-ttu-id="79343-109">toocreate um cluster do serviço de contêiner do Azure usando Olá 2.0 do CLI do Azure, você deve:</span><span class="sxs-lookup"><span data-stu-id="79343-109">toocreate an Azure Container Service cluster using hello Azure CLI 2.0, you must:</span></span>
* <span data-ttu-id="79343-110">ter uma conta do Azure ([obtenha uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/))</span><span class="sxs-lookup"><span data-stu-id="79343-110">have an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/))</span></span>
* <span data-ttu-id="79343-111">instalar e configurar Olá [2.0 do CLI do Azure](/cli/azure/install-az-cli2)</span><span class="sxs-lookup"><span data-stu-id="79343-111">have installed and set up hello [Azure CLI 2.0](/cli/azure/install-az-cli2)</span></span>

## <a name="get-started"></a><span data-ttu-id="79343-112">Introdução</span><span class="sxs-lookup"><span data-stu-id="79343-112">Get started</span></span> 
### <a name="log-in-tooyour-account"></a><span data-ttu-id="79343-113">Faça logon na conta tooyour</span><span class="sxs-lookup"><span data-stu-id="79343-113">Log in tooyour account</span></span>
```azurecli
az login 
```

<span data-ttu-id="79343-114">Siga Olá prompts toolog em interativamente.</span><span class="sxs-lookup"><span data-stu-id="79343-114">Follow hello prompts toolog in interactively.</span></span> <span data-ttu-id="79343-115">Para outros toolog métodos no, consulte [Introdução ao Azure CLI 2.0](/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="79343-115">For other methods toolog in, see [Get started with Azure CLI 2.0](/cli/azure/get-started-with-az-cli2).</span></span>

### <a name="set-your-azure-subscription"></a><span data-ttu-id="79343-116">Definir sua assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="79343-116">Set your Azure subscription</span></span>

<span data-ttu-id="79343-117">Se você tiver mais de uma assinatura do Azure, defina a assinatura padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="79343-117">If you have more than one Azure subscription, set hello default subscription.</span></span> <span data-ttu-id="79343-118">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="79343-118">For example:</span></span>

```
az account set --subscription "f66xxxxx-xxxx-xxxx-xxx-zgxxxx33cha5"
```


### <a name="create-a-resource-group"></a><span data-ttu-id="79343-119">Criar um grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="79343-119">Create a resource group</span></span>
<span data-ttu-id="79343-120">Recomendamos que você crie um grupo de recursos para cada cluster.</span><span class="sxs-lookup"><span data-stu-id="79343-120">We recommend that you create a resource group for every cluster.</span></span> <span data-ttu-id="79343-121">Especifique uma região do Azure no qual o serviço de contêiner do Azure é [disponível](https://azure.microsoft.com/en-us/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="79343-121">Specify an Azure region in which Azure Container Service is [available](https://azure.microsoft.com/en-us/regions/services/).</span></span> <span data-ttu-id="79343-122">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="79343-122">For example:</span></span>

```azurecli
az group create -n acsrg1 -l "westus"
```
<span data-ttu-id="79343-123">O resultado é a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="79343-123">Output is similar toohello following:</span></span>

![Criar um grupo de recursos](./media/container-service-create-acs-cluster-cli/rg-create.png)


## <a name="create-an-azure-container-service-cluster"></a><span data-ttu-id="79343-125">Criar um cluster do Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="79343-125">Create an Azure Container Service cluster</span></span>

<span data-ttu-id="79343-126">toocreate um cluster, use `az acs create`.</span><span class="sxs-lookup"><span data-stu-id="79343-126">toocreate a cluster, use `az acs create`.</span></span>
<span data-ttu-id="79343-127">Um nome para o cluster de saudação e Olá Olá do grupo de recursos criado na etapa anterior Olá são parâmetros obrigatórios.</span><span class="sxs-lookup"><span data-stu-id="79343-127">A name for hello cluster and hello name of hello resource group created in hello previous step are mandatory parameters.</span></span> 

<span data-ttu-id="79343-128">Outras entradas são valores do conjunto de toodefault (consulte Olá tela a seguir), a menos que substituído usando seus respectivos comutadores.</span><span class="sxs-lookup"><span data-stu-id="79343-128">Other inputs are set toodefault values (see hello following screen) unless overwritten using their respective switches.</span></span> <span data-ttu-id="79343-129">Por exemplo, o orchestrator Olá é definido por padrão tooDC/OS.</span><span class="sxs-lookup"><span data-stu-id="79343-129">For example, hello orchestrator is set by default tooDC/OS.</span></span> <span data-ttu-id="79343-130">E se não for especificada, um prefixo de nome DNS é criado com base no nome do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="79343-130">And if you don't specify one, a DNS name prefix is created based on hello cluster name.</span></span>

![az acs create usage](./media/container-service-create-acs-cluster-cli/create-help.png)


### <a name="quick-acs-create-using-defaults"></a><span data-ttu-id="79343-132">`acs create` rápido usando padrões</span><span class="sxs-lookup"><span data-stu-id="79343-132">Quick `acs create` using defaults</span></span>
<span data-ttu-id="79343-133">Se você tiver um arquivo de chave pública RSA SSH `id_rsa.pub` no local padrão de saudação (ou criar uma para [OS X e Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) ou [Windows](../../virtual-machines/linux/ssh-from-windows.md)), use um comando como Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="79343-133">If you have an SSH RSA public key file `id_rsa.pub` in hello default location (or created one for [OS X and Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../../virtual-machines/linux/ssh-from-windows.md)), use a command like hello following:</span></span>

```azurecli
az acs create -n acs-cluster -g acsrg1 -d applink789
```
<span data-ttu-id="79343-134">Se você não tiver uma chave pública SSH, use este segundo comando.</span><span class="sxs-lookup"><span data-stu-id="79343-134">If you don't have an SSH public key, use this second command.</span></span> <span data-ttu-id="79343-135">Esse comando com hello `--generate-ssh-keys` opção criará um para você.</span><span class="sxs-lookup"><span data-stu-id="79343-135">This command with hello `--generate-ssh-keys` switch creates one for you.</span></span>

```azurecli
az acs create -n acs-cluster -g acsrg1 -d applink789 --generate-ssh-keys
```

<span data-ttu-id="79343-136">Depois de inserir o comando hello, aguarde cerca de 10 minutos para Olá cluster toobe criado.</span><span class="sxs-lookup"><span data-stu-id="79343-136">After you enter hello command, wait for about 10 minutes for hello cluster toobe created.</span></span> <span data-ttu-id="79343-137">saída do comando Olá inclui nomes de domínio totalmente qualificados (FQDNs) de mestre hello e nós de agente e um SSH comando tooconnect toohello primeiro mestre.</span><span class="sxs-lookup"><span data-stu-id="79343-137">hello command output includes fully qualified domain names (FQDNs) of hello master and agent nodes and an SSH command tooconnect toohello first master.</span></span> <span data-ttu-id="79343-138">Aqui está a saída abreviada:</span><span class="sxs-lookup"><span data-stu-id="79343-138">Here is abbreviated output:</span></span>

![Criação ACS de imagem](./media/container-service-create-acs-cluster-cli/cluster-create.png)

> [!TIP]
> <span data-ttu-id="79343-140">Olá [Kubernetes passo a passo](../kubernetes/container-service-kubernetes-walkthrough.md) mostra como toouse `az acs create` com padrão valores toocreate um Kubernetes de cluster.</span><span class="sxs-lookup"><span data-stu-id="79343-140">hello [Kubernetes walkthrough](../kubernetes/container-service-kubernetes-walkthrough.md) shows how toouse `az acs create` with default values toocreate a Kubernetes cluster.</span></span>
>

## <a name="manage-acs-clusters"></a><span data-ttu-id="79343-141">Gerenciar clusters do ACS</span><span class="sxs-lookup"><span data-stu-id="79343-141">Manage ACS clusters</span></span>

<span data-ttu-id="79343-142">Use adicional `az acs` comandos toomanage seu cluster.</span><span class="sxs-lookup"><span data-stu-id="79343-142">Use additional `az acs` commands toomanage your cluster.</span></span> <span data-ttu-id="79343-143">Veja alguns exemplos.</span><span class="sxs-lookup"><span data-stu-id="79343-143">Here are some examples.</span></span>

### <a name="list-clusters-under-a-subscription"></a><span data-ttu-id="79343-144">Listar os clusters em uma assinatura</span><span class="sxs-lookup"><span data-stu-id="79343-144">List clusters under a subscription</span></span>

```azurecli
az acs list --output table
```

### <a name="list-clusters-in-a-resource-group"></a><span data-ttu-id="79343-145">Listar os clusters em um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="79343-145">List clusters in a resource group</span></span>

```azurecli
az acs list -g acsrg1 --output table
```

![acs list](./media/container-service-create-acs-cluster-cli/acs-list.png)


### <a name="display-details-of-a-container-service-cluster"></a><span data-ttu-id="79343-147">Exibir detalhes de um cluster do serviço de contêiner</span><span class="sxs-lookup"><span data-stu-id="79343-147">Display details of a container service cluster</span></span>

```azurecli
az acs show -g acsrg1 -n acs-cluster --output list
```

![acs show](./media/container-service-create-acs-cluster-cli/acs-show.png)


### <a name="scale-hello-cluster"></a><span data-ttu-id="79343-149">Cluster de saudação de escala</span><span class="sxs-lookup"><span data-stu-id="79343-149">Scale hello cluster</span></span>
<span data-ttu-id="79343-150">A ampliação e a redução dos nós de agente são permitidas.</span><span class="sxs-lookup"><span data-stu-id="79343-150">Both scaling in and scaling out of agent nodes are allowed.</span></span> <span data-ttu-id="79343-151">Olá parâmetro `new-agent-count` é novo número de saudação de agentes no cluster Olá ACS.</span><span class="sxs-lookup"><span data-stu-id="79343-151">hello parameter `new-agent-count` is hello new number of agents in hello ACS cluster.</span></span>

```azurecli
az acs scale -g acsrg1 -n acs-cluster --new-agent-count 4
```

![acs scale](./media/container-service-create-acs-cluster-cli/acs-scale.png)

## <a name="delete-a-container-service-cluster"></a><span data-ttu-id="79343-153">Exclui um cluster do serviço de contêiner</span><span class="sxs-lookup"><span data-stu-id="79343-153">Delete a container service cluster</span></span>
```azurecli
az acs delete -g acsrg1 -n acs-cluster 
```
<span data-ttu-id="79343-154">Este comando não exclui todos os recursos (rede e armazenamento) criados durante a criação de serviço de contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="79343-154">This command does not delete all resources (network and storage) created while creating hello container service.</span></span> <span data-ttu-id="79343-155">toodelete todos os recursos facilmente, é recomendável implantar cada cluster em um grupo de recursos distintos.</span><span class="sxs-lookup"><span data-stu-id="79343-155">toodelete all resources easily, it is recommended you deploy each cluster in a distinct resource group.</span></span> <span data-ttu-id="79343-156">Em seguida, exclua o grupo de recursos de Olá ao cluster Olá não é mais necessário.</span><span class="sxs-lookup"><span data-stu-id="79343-156">Then, delete hello resource group when hello cluster is no longer required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79343-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="79343-157">Next steps</span></span>
<span data-ttu-id="79343-158">Agora que você tem um cluster em funcionamento, confira estes documentos para obter detalhes sobre conexão e gerenciamento:</span><span class="sxs-lookup"><span data-stu-id="79343-158">Now that you have a functioning cluster, see these documents for connection and management details:</span></span>

* [<span data-ttu-id="79343-159">Conecte-se o cluster do serviço de contêiner do Azure tooan</span><span class="sxs-lookup"><span data-stu-id="79343-159">Connect tooan Azure Container Service cluster</span></span>](../container-service-connect.md)
* [<span data-ttu-id="79343-160">Trabalhar com o Serviço de Contêiner do Azure e o DC/SO</span><span class="sxs-lookup"><span data-stu-id="79343-160">Work with Azure Container Service and DC/OS</span></span>](container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="79343-161">Trabalhar com o Serviço de Contêiner do Azure e o Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="79343-161">Work with Azure Container Service and Docker Swarm</span></span>](container-service-docker-swarm.md)
* [<span data-ttu-id="79343-162">Trabalhar com o Serviço de Contêiner do Azure e o Kubernetes</span><span class="sxs-lookup"><span data-stu-id="79343-162">Work with Azure Container Service and Kubernetes</span></span>](../kubernetes/container-service-kubernetes-walkthrough.md)