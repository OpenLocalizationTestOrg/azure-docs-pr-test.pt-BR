---
title: "tutorial de serviço de contêiner aaaAzure - Cluster implantar | Microsoft Docs"
description: "Tutorial do Serviço de Contêiner do Azure – implantar cluster"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Contêineres, Microsserviços, Kubernetes, DC/SO, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c4c8cc95c88d9c2077d0322f57e5d3159e2dd0ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="839e7-104">Implantar um cluster Kubernetes no Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="839e7-104">Deploy a Kubernetes cluster in Azure Container Service</span></span>

<span data-ttu-id="839e7-105">Kubernetes fornece uma plataforma distribuída para aplicativos em contêineres.</span><span class="sxs-lookup"><span data-stu-id="839e7-105">Kubernetes provides a distributed platform for containerized applications.</span></span> <span data-ttu-id="839e7-106">Com o Serviço de Contêiner do Azure, o provisionamento de um cluster Kubernetes pronto para produção é simples e rápido.</span><span class="sxs-lookup"><span data-stu-id="839e7-106">With Azure Container Service, provisioning of a production ready Kubernetes cluster is simple and quick.</span></span> <span data-ttu-id="839e7-107">Neste tutorial, parte 3 de 7, um cluster Kubernetes do Serviço de Contêiner do Azure é implantado.</span><span class="sxs-lookup"><span data-stu-id="839e7-107">In this tutorial, part 3 of 7, an Azure Container Service Kubernetes cluster is deployed.</span></span> <span data-ttu-id="839e7-108">As etapas concluídas incluem:</span><span class="sxs-lookup"><span data-stu-id="839e7-108">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="839e7-109">Implantação de um cluster ACS Kubernetes</span><span class="sxs-lookup"><span data-stu-id="839e7-109">Deploying a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="839e7-110">Instalação do hello Kubernetes CLI (kubectl)</span><span class="sxs-lookup"><span data-stu-id="839e7-110">Installation of hello Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="839e7-111">Configuração de kubectl</span><span class="sxs-lookup"><span data-stu-id="839e7-111">Configuration of kubectl</span></span>

<span data-ttu-id="839e7-112">Em tutoriais subsequentes, hello Azure voto aplicativo é implantado cluster toohello, escala, atualizado e Operations Management Suite é o cluster de Kubernetes Olá toomonitor configurado.</span><span class="sxs-lookup"><span data-stu-id="839e7-112">In subsequent tutorials, hello Azure Vote application is deployed toohello cluster, scaled, updated, and Operations Management Suite is configured toomonitor hello Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="839e7-113">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="839e7-113">Before you begin</span></span>

<span data-ttu-id="839e7-114">Nos tutoriais anteriores, uma imagem de contêiner foi criada e carregado tooan instância de registro de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="839e7-114">In previous tutorials, a container image was created and uploaded tooan Azure Container Registry instance.</span></span> <span data-ttu-id="839e7-115">Se você ainda não tiver feito essas etapas e deseja toofollow ao longo, retornar muito[Tutorial 1 – criar imagens de contêiner](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="839e7-115">If you have not done these steps, and would like toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span>

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="839e7-116">Criar cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="839e7-116">Create Kubernetes cluster</span></span>

<span data-ttu-id="839e7-117">Em Olá [tutorial anterior](./container-service-tutorial-kubernetes-prepare-acr.md), um grupo de recursos denominado *myResourceGroup* foi criado.</span><span class="sxs-lookup"><span data-stu-id="839e7-117">In hello [previous tutorial](./container-service-tutorial-kubernetes-prepare-acr.md), a resource group named *myResourceGroup* was created.</span></span> <span data-ttu-id="839e7-118">Se você não tiver feito isso, crie esse grupo de recursos agora.</span><span class="sxs-lookup"><span data-stu-id="839e7-118">If you have not done so, create this resource group now.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="839e7-119">Criar um cluster Kubernetes no serviço de contêiner do Azure com hello [az acs criar](/cli/azure/acs#create) comando.</span><span class="sxs-lookup"><span data-stu-id="839e7-119">Create a Kubernetes cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="839e7-120">Olá, exemplo a seguir cria um cluster denominado *myK8sCluster* com um Linux mestre de nó e três nós de agente do Linux.</span><span class="sxs-lookup"><span data-stu-id="839e7-120">hello following example creates a cluster named *myK8sCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive 
az acs create --orchestrator-type=kubernetes --resource-group myResourceGroup --name=myK8SCluster --generate-ssh-keys 
```

<span data-ttu-id="839e7-121">Após alguns minutos, Olá comando for concluído e formatadas em json de retorna informações sobre a implantação de saudação ACS.</span><span class="sxs-lookup"><span data-stu-id="839e7-121">After several minutes, hello command completes, and returns json formatted information about hello ACS deployment.</span></span>

## <a name="install-hello-kubectl-cli"></a><span data-ttu-id="839e7-122">Instalar Olá kubectl CLI</span><span class="sxs-lookup"><span data-stu-id="839e7-122">Install hello kubectl CLI</span></span>

<span data-ttu-id="839e7-123">tooconnect toohello Kubernetes cluster do computador cliente, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), cliente de linha de comando do hello Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="839e7-123">tooconnect toohello Kubernetes cluster from your client computer, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes command-line client.</span></span> 

<span data-ttu-id="839e7-124">Se você estiver usando o Azure CloudShell, `kubectl` já estará instalado.</span><span class="sxs-lookup"><span data-stu-id="839e7-124">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="839e7-125">Se você quiser tooinstall-lo localmente, use Olá [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) comando.</span><span class="sxs-lookup"><span data-stu-id="839e7-125">If you want tooinstall it locally, use hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="839e7-126">Se executado em Linux ou macOS, talvez seja necessário toorun com sudo.</span><span class="sxs-lookup"><span data-stu-id="839e7-126">If running in Linux or macOS, you may need toorun with sudo.</span></span> <span data-ttu-id="839e7-127">No Windows, certifique-se de que shell foi executado como administrador.</span><span class="sxs-lookup"><span data-stu-id="839e7-127">On Windows, ensure your shell has been run as administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli 
```

<span data-ttu-id="839e7-128">No Windows, a instalação de padrão de saudação é *c:\program files (x86)\kubectl.exe*.</span><span class="sxs-lookup"><span data-stu-id="839e7-128">On Windows, hello default installation is *c:\program files (x86)\kubectl.exe*.</span></span> <span data-ttu-id="839e7-129">Talvez seja necessário tooadd esse caminho do arquivo toohello Windows.</span><span class="sxs-lookup"><span data-stu-id="839e7-129">You may need tooadd this file toohello Windows path.</span></span> 

## <a name="connect-with-kubectl"></a><span data-ttu-id="839e7-130">Conectar-se com kubectl</span><span class="sxs-lookup"><span data-stu-id="839e7-130">Connect with kubectl</span></span>

<span data-ttu-id="839e7-131">tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster, execute Olá [az get-credenciais do acs kubernetes](/cli/azure/acs/kubernetes#get-credentials) comando.</span><span class="sxs-lookup"><span data-stu-id="839e7-131">tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster, run hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8SCluster
```

<span data-ttu-id="839e7-132">tooverify Olá conexão tooyour cluster executar Olá [kubectl obter nós](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) comando.</span><span class="sxs-lookup"><span data-stu-id="839e7-132">tooverify hello connection tooyour cluster, run hello [kubectl get nodes](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="839e7-133">Saída:</span><span class="sxs-lookup"><span data-stu-id="839e7-133">Output:</span></span>

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.6.2
k8s-agent-98dc3136-1    Ready                      5m        v1.6.2
k8s-agent-98dc3136-2    Ready                      5m        v1.6.2
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.6.2
```

<span data-ttu-id="839e7-134">Ao concluir o tutorial, você tem um cluster ACS Kubernetes pronto para cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="839e7-134">At tutorial completion, you have an ACS Kubernetes cluster ready for workloads.</span></span> <span data-ttu-id="839e7-135">Em tutoriais subsequentes, um aplicativo de multi-contêiner é implantado toothis cluster expandida, atualizado e monitorados.</span><span class="sxs-lookup"><span data-stu-id="839e7-135">In subsequent tutorials, a multi-container application is deployed toothis cluster, scaled out, updated, and monitored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="839e7-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="839e7-136">Next steps</span></span>

<span data-ttu-id="839e7-137">Neste tutorial, um cluster Kubernetes do Serviço de Contêiner do Azure foi implantado.</span><span class="sxs-lookup"><span data-stu-id="839e7-137">In this tutorial, an Azure Container Service Kubernetes cluster was deployed.</span></span> <span data-ttu-id="839e7-138">Olá, as etapas a seguir foram concluída:</span><span class="sxs-lookup"><span data-stu-id="839e7-138">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="839e7-139">Implantação de um cluster ACS Kubernetes</span><span class="sxs-lookup"><span data-stu-id="839e7-139">Deployed a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="839e7-140">Olá instalado Kubernetes CLI (kubectl)</span><span class="sxs-lookup"><span data-stu-id="839e7-140">Installed hello Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="839e7-141">Configuração de kubectl</span><span class="sxs-lookup"><span data-stu-id="839e7-141">Configured kubectl</span></span>

<span data-ttu-id="839e7-142">Avançar toohello toolearn próximo de tutorial sobre como executar o aplicativo no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="839e7-142">Advance toohello next tutorial toolearn about running application on hello cluster.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="839e7-143">Implantar o aplicativo no Kubernetes</span><span class="sxs-lookup"><span data-stu-id="839e7-143">Deploy application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-deploy-application.md)
