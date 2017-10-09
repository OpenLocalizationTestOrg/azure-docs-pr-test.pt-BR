---
title: aaaQuickstart - cluster Kubernetes do Azure para Windows | Microsoft Docs
description: "Aprenda rapidamente toocreate um cluster Kubernetes para contêineres do Windows no serviço de contêiner do Azure com hello CLI do Azure."
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 85fe65a46ae8c78797e8a8a097c2a37f06329335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-windows-containers"></a><span data-ttu-id="986f3-103">Implantar um cluster Kubernetes para contêineres do Windows</span><span class="sxs-lookup"><span data-stu-id="986f3-103">Deploy Kubernetes cluster for Windows containers</span></span>

<span data-ttu-id="986f3-104">Olá CLI do Azure é usado toocreate e gerenciar recursos do Azure Olá linha de comando ou em scripts.</span><span class="sxs-lookup"><span data-stu-id="986f3-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="986f3-105">Esses detalhes de guia usando Olá CLI do Azure toodeploy um [Kubernetes](https://kubernetes.io/docs/home/) cluster no [serviço de contêiner do Azure](../container-service-intro.md).</span><span class="sxs-lookup"><span data-stu-id="986f3-105">This guide details using hello Azure CLI toodeploy a [Kubernetes](https://kubernetes.io/docs/home/) cluster in [Azure Container Service](../container-service-intro.md).</span></span> <span data-ttu-id="986f3-106">Depois de saudação cluster for implantado, você se conectar tooit com hello Kubernetes `kubectl` ferramenta de linha de comando e se você implantar o primeiro contêiner do Windows.</span><span class="sxs-lookup"><span data-stu-id="986f3-106">Once hello cluster is deployed, you connect tooit with hello Kubernetes `kubectl` command-line tool, and you deploy your first Windows container.</span></span>

<span data-ttu-id="986f3-107">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="986f3-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="986f3-108">Se você escolher tooinstall e usa o hello CLI localmente, este guia de início rápido requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="986f3-108">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="986f3-109">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="986f3-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="986f3-110">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="986f3-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

> [!NOTE]
> <span data-ttu-id="986f3-111">O suporte para contêineres do Windows no Kubernetes no Serviço de Contêiner do Azure está em versão prévia.</span><span class="sxs-lookup"><span data-stu-id="986f3-111">Support for Windows containers on Kubernetes in Azure Container Service is in preview.</span></span> 
>

## <a name="create-a-resource-group"></a><span data-ttu-id="986f3-112">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="986f3-112">Create a resource group</span></span>

<span data-ttu-id="986f3-113">Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="986f3-113">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="986f3-114">Um grupo de recursos do Azure é um grupo lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="986f3-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="986f3-115">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local.</span><span class="sxs-lookup"><span data-stu-id="986f3-115">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="986f3-116">Criar cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="986f3-116">Create Kubernetes cluster</span></span>
<span data-ttu-id="986f3-117">Criar um cluster Kubernetes no serviço de contêiner do Azure com hello [az acs criar](/cli/azure/acs#create) comando.</span><span class="sxs-lookup"><span data-stu-id="986f3-117">Create a Kubernetes cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="986f3-118">Olá, exemplo a seguir cria um cluster denominado *myK8sCluster* com um Linux mestre de nó e dois nós de agente do Windows.</span><span class="sxs-lookup"><span data-stu-id="986f3-118">hello following example creates a cluster named *myK8sCluster* with one Linux master node and two Windows agent nodes.</span></span> <span data-ttu-id="986f3-119">Este exemplo cria SSH mestre do Linux chaves necessárias tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="986f3-119">This example creates SSH keys needed tooconnect toohello Linux master.</span></span> <span data-ttu-id="986f3-120">Este exemplo usa *azureuser* para um nome de usuário administrativo e *myPassword12* senha Olá em nós do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="986f3-120">This example uses *azureuser* for an administrative user name and *myPassword12* as hello password on hello Windows nodes.</span></span> <span data-ttu-id="986f3-121">Atualize ambiente de tooyour apropriado de toosomething esses valores.</span><span class="sxs-lookup"><span data-stu-id="986f3-121">Update these values toosomething appropriate tooyour environment.</span></span> 



```azurecli-interactive 
az acs create --orchestrator-type=kubernetes \
    --resource-group myResourceGroup \
    --name=myK8sCluster \
    --agent-count=2 \
    --generate-ssh-keys \
    --windows --admin-username azureuser \
    --admin-password myPassword12
```

<span data-ttu-id="986f3-122">Após alguns minutos, o comando de Olá for concluída e mostra informações sobre a implantação.</span><span class="sxs-lookup"><span data-stu-id="986f3-122">After several minutes, hello command completes, and shows you information about your deployment.</span></span>

## <a name="install-kubectl"></a><span data-ttu-id="986f3-123">Instalar kubectl</span><span class="sxs-lookup"><span data-stu-id="986f3-123">Install kubectl</span></span>

<span data-ttu-id="986f3-124">tooconnect toohello Kubernetes cluster do computador cliente, use [ `kubectl` ](https://kubernetes.io/docs/user-guide/kubectl/), cliente de linha de comando do hello Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="986f3-124">tooconnect toohello Kubernetes cluster from your client computer, use [`kubectl`](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes command-line client.</span></span> 

<span data-ttu-id="986f3-125">Se você estiver usando o Azure CloudShell, `kubectl` já estará instalado.</span><span class="sxs-lookup"><span data-stu-id="986f3-125">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="986f3-126">Se você quiser tooinstall localmente, você pode usar Olá [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) comando.</span><span class="sxs-lookup"><span data-stu-id="986f3-126">If you want tooinstall it locally, you can use hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="986f3-127">Olá CLI do Azure instala de exemplo a seguir `kubectl` tooyour sistema.</span><span class="sxs-lookup"><span data-stu-id="986f3-127">hello following Azure CLI example installs `kubectl` tooyour system.</span></span> <span data-ttu-id="986f3-128">No Windows, execute este comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="986f3-128">On Windows, run this command as an administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli
```


## <a name="connect-with-kubectl"></a><span data-ttu-id="986f3-129">Conectar-se com kubectl</span><span class="sxs-lookup"><span data-stu-id="986f3-129">Connect with kubectl</span></span>

<span data-ttu-id="986f3-130">tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster, execute Olá [az get-credenciais do acs kubernetes](/cli/azure/acs/kubernetes#get-credentials) comando.</span><span class="sxs-lookup"><span data-stu-id="986f3-130">tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster, run hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="986f3-131">Olá, exemplo a seguir baixa Olá configuração de cluster para o cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="986f3-131">hello following example downloads hello cluster configuration for your Kubernetes cluster.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

<span data-ttu-id="986f3-132">cluster de tooyour tooverify Olá conexão em seu computador, tente executar:</span><span class="sxs-lookup"><span data-stu-id="986f3-132">tooverify hello connection tooyour cluster from your machine, try running:</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="986f3-133">`kubectl`lista nós de mestre e agente hello.</span><span class="sxs-lookup"><span data-stu-id="986f3-133">`kubectl` lists hello master and agent nodes.</span></span>

```azurecli-interactive
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.5.3
k8s-agent-98dc3136-1    Ready                      5m        v1.5.3
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.5.3

```

## <a name="deploy-a-windows-iis-container"></a><span data-ttu-id="986f3-134">Implantar um contêiner do IIS do Windows</span><span class="sxs-lookup"><span data-stu-id="986f3-134">Deploy a Windows IIS container</span></span>

<span data-ttu-id="986f3-135">Você pode executar um contêiner do Docker dentro de um *pod* Kubernetes, que contém um ou mais contêineres.</span><span class="sxs-lookup"><span data-stu-id="986f3-135">You can run a Docker container inside a Kubernetes *pod*, which contains one or more containers.</span></span> 

<span data-ttu-id="986f3-136">Este exemplo básico usa um arquivo JSON toospecify um contêiner do Microsoft Internet Information Server (IIS) e cria pod hello usando Olá `kubctl apply` comando.</span><span class="sxs-lookup"><span data-stu-id="986f3-136">This basic example uses a JSON file toospecify a Microsoft Internet Information Server (IIS) container, and then creates hello pod using hello `kubctl apply` command.</span></span> 

<span data-ttu-id="986f3-137">Crie um arquivo local chamado `iis.json` e Olá copiar texto a seguir.</span><span class="sxs-lookup"><span data-stu-id="986f3-137">Create a local file named `iis.json` and copy hello following text.</span></span> <span data-ttu-id="986f3-138">Este arquivo informa Kubernetes toorun IIS no Windows Server 2016 Nano Server, usando uma imagem de contêiner público de [Hub do Docker](https://hub.docker.com/r/nanoserver/iis/).</span><span class="sxs-lookup"><span data-stu-id="986f3-138">This file tells Kubernetes toorun IIS on Windows Server 2016 Nano Server, using a public container image from [Docker Hub](https://hub.docker.com/r/nanoserver/iis/).</span></span> <span data-ttu-id="986f3-139">contêiner de saudação usa a porta 80, mas inicialmente só está acessível na rede do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="986f3-139">hello container uses port 80, but initially is only accessible within hello cluster network.</span></span>

 ```JSON
 {
  "apiVersion": "v1",
  "kind": "Pod",
  "metadata": {
    "name": "iis",
    "labels": {
      "name": "iis"
    }
  },
  "spec": {
    "containers": [
      {
        "name": "iis",
        "image": "nanoserver/iis",
        "ports": [
          {
          "containerPort": 80
          }
        ]
      }
    ],
    "nodeSelector": {
     "beta.kubernetes.io/os": "windows"
     }
   }
 }
 ```

<span data-ttu-id="986f3-140">pod de saudação toostart, tipo:</span><span class="sxs-lookup"><span data-stu-id="986f3-140">toostart hello pod, type:</span></span>
  
```azurecli-interactive
kubectl apply -f iis.json
```  

<span data-ttu-id="986f3-141">implantação de saudação tootrack, tipo:</span><span class="sxs-lookup"><span data-stu-id="986f3-141">tootrack hello deployment, type:</span></span>
  
```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="986f3-142">Quando está implantando pod hello, status de saudação é `ContainerCreating`.</span><span class="sxs-lookup"><span data-stu-id="986f3-142">While hello pod is deploying, hello status is `ContainerCreating`.</span></span> <span data-ttu-id="986f3-143">Pode levar alguns minutos para saudação do hello contêiner tooenter `Running` estado.</span><span class="sxs-lookup"><span data-stu-id="986f3-143">It can take a few minutes for hello container tooenter hello `Running` state.</span></span>

```azurecli-interactive
NAME     READY        STATUS        RESTARTS    AGE
iis      1/1          Running       0           32s
```

## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="986f3-144">Olá exibir página de boas-vindas do IIS</span><span class="sxs-lookup"><span data-stu-id="986f3-144">View hello IIS welcome page</span></span>

<span data-ttu-id="986f3-145">tooexpose pod toohello Olá com um endereço IP público, Olá tipo comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="986f3-145">tooexpose hello pod toohello world with a public IP address, type hello following command:</span></span>

```azurecli-interactive
kubectl expose pods iis --port=80 --type=LoadBalancer
```

<span data-ttu-id="986f3-146">Com este comando Kubernetes cria um serviço e um [regra do balanceador de carga do Azure](container-service-kubernetes-load-balancing.md) com um endereço IP público para o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="986f3-146">With this command, Kubernetes creates a service and an [Azure load balancer rule](container-service-kubernetes-load-balancing.md) with a public IP address for hello service.</span></span> 

<span data-ttu-id="986f3-147">Execute Olá comando toosee Olá status Olá serviço a seguir.</span><span class="sxs-lookup"><span data-stu-id="986f3-147">Run hello following command toosee hello status of hello service.</span></span>

```azurecli-interactive
kubectl get svc
```

<span data-ttu-id="986f3-148">Inicialmente o endereço IP hello aparece como `pending`.</span><span class="sxs-lookup"><span data-stu-id="986f3-148">Initially hello IP address appears as `pending`.</span></span> <span data-ttu-id="986f3-149">Depois de alguns minutos, Olá endereço IP externo de saudação `iis` pod está definido:</span><span class="sxs-lookup"><span data-stu-id="986f3-149">After a few minutes, hello external IP address of hello `iis` pod is set:</span></span>
  
```azurecli-interactive
NAME         CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE       
kubernetes   10.0.0.1       <none>          443/TCP        21h       
iis          10.0.111.25    13.64.158.233   80/TCP         22m
```

<span data-ttu-id="986f3-150">Você pode usar um navegador da web da página toosee choice saudação padrão IIS bem-vindo ao endereço IP externo de saudação:</span><span class="sxs-lookup"><span data-stu-id="986f3-150">You can use a web browser of your choice toosee hello default IIS welcome page at hello external IP address:</span></span>

![Imagem de navegação tooIIS](./media/container-service-kubernetes-windows-walkthrough/kubernetes-iis.png)  


## <a name="delete-cluster"></a><span data-ttu-id="986f3-152">Excluir cluster</span><span class="sxs-lookup"><span data-stu-id="986f3-152">Delete cluster</span></span>
<span data-ttu-id="986f3-153">Ao cluster Olá não for mais necessário, você pode usar o hello [excluir grupo de az](/cli/azure/group#delete) comando tooremove grupo de recursos de hello, serviço de contêiner e recursos todos relacionados.</span><span class="sxs-lookup"><span data-stu-id="986f3-153">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```


## <a name="next-steps"></a><span data-ttu-id="986f3-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="986f3-154">Next steps</span></span>

<span data-ttu-id="986f3-155">Neste início rápido, você implantou um cluster Kubernetes, conectou-o a um `kubectl`e implantou um pod com um contêiner do IIS.</span><span class="sxs-lookup"><span data-stu-id="986f3-155">In this quick start, you deployed a Kubernetes cluster, connected with `kubectl`, and deployed a pod with an IIS container.</span></span> <span data-ttu-id="986f3-156">toolearn mais sobre o serviço de contêiner do Azure, continuar toohello Kubernetes tutorial.</span><span class="sxs-lookup"><span data-stu-id="986f3-156">toolearn more about Azure Container Service, continue toohello Kubernetes tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="986f3-157">Gerenciar um cluster ACS Kubernetes</span><span class="sxs-lookup"><span data-stu-id="986f3-157">Manage an ACS Kubernetes cluster</span></span>](container-service-tutorial-kubernetes-prepare-app.md)
