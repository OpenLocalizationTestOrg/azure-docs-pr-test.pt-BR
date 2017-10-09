---
title: aaaQuickstart - cluster Kubernetes do Azure para Linux | Microsoft Docs
description: "Aprenda rapidamente toocreate um cluster Kubernetes para contêineres do Linux no serviço de contêiner do Azure com hello CLI do Azure."
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 8da267e8-2aeb-4c24-9a7a-65bdca3a82d6
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 8b0d7a803148c1cbf329f4b76f2e99b4b7e14983
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-linux-containers"></a><span data-ttu-id="f73ae-103">Implantar um cluster Kubernetes para contêineres do Linux</span><span class="sxs-lookup"><span data-stu-id="f73ae-103">Deploy Kubernetes cluster for Linux containers</span></span>

<span data-ttu-id="f73ae-104">Esse início rápido, um cluster Kubernetes é implantado usando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="f73ae-104">In this quick start, a Kubernetes cluster is deployed using hello Azure CLI.</span></span> <span data-ttu-id="f73ae-105">Um aplicativo de contêiner vários consistindo de front-end da web e uma instância do Redis, em seguida, é implantado e executado no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="f73ae-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on hello cluster.</span></span> <span data-ttu-id="f73ae-106">Depois de concluído, o aplicativo hello está acessível pela internet de hello.</span><span class="sxs-lookup"><span data-stu-id="f73ae-106">Once completed, hello application is accessible over hello internet.</span></span> 

<span data-ttu-id="f73ae-107">aplicativo de exemplo Hello usado neste documento é gravado em Python.</span><span class="sxs-lookup"><span data-stu-id="f73ae-107">hello example application used in this document is written in Python.</span></span> <span data-ttu-id="f73ae-108">conceitos de saudação e as etapas descritas aqui podem ser usado toodeploy qualquer contêiner da imagem em um cluster de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="f73ae-108">hello concepts and steps detailed here can be used toodeploy any container image into a Kubernetes cluster.</span></span> <span data-ttu-id="f73ae-109">Hello código, Dockerfile e projeto de toothis relacionados de arquivos de manifesto Kubernetes pré-criados estão disponíveis em [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git).</span><span class="sxs-lookup"><span data-stu-id="f73ae-109">hello code, Dockerfile, and pre-created Kubernetes manifest files related toothis project are available on [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git).</span></span>

![Imagem de navegação tooAzure voto](media/container-service-kubernetes-walkthrough/azure-vote.png)

<span data-ttu-id="f73ae-111">Esse início rápido pressupõe uma compreensão básica dos conceitos de Kubernetes, para obter informações detalhadas sobre Kubernetes consulte Olá [Kubernetes documentação]( https://kubernetes.io/docs/home/).</span><span class="sxs-lookup"><span data-stu-id="f73ae-111">This quick start assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see hello [Kubernetes documentation]( https://kubernetes.io/docs/home/).</span></span>

<span data-ttu-id="f73ae-112">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="f73ae-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f73ae-113">Se você escolher tooinstall e usa o hello CLI localmente, este guia de início rápido requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="f73ae-113">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="f73ae-114">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="f73ae-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="f73ae-115">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f73ae-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="f73ae-116">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="f73ae-116">Create a resource group</span></span>

<span data-ttu-id="f73ae-117">Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="f73ae-117">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="f73ae-118">Um grupo de recursos do Azure é um grupo lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="f73ae-118">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="f73ae-119">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *westeurope* local.</span><span class="sxs-lookup"><span data-stu-id="f73ae-119">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="f73ae-120">Saída:</span><span class="sxs-lookup"><span data-stu-id="f73ae-120">Output:</span></span>

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westeurope",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="f73ae-121">Criar cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="f73ae-121">Create Kubernetes cluster</span></span>

<span data-ttu-id="f73ae-122">Criar um cluster Kubernetes no serviço de contêiner do Azure com hello [az acs criar](/cli/azure/acs#create) comando.</span><span class="sxs-lookup"><span data-stu-id="f73ae-122">Create a Kubernetes cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> <span data-ttu-id="f73ae-123">Olá, exemplo a seguir cria um cluster denominado *myK8sCluster* com um Linux mestre de nó e três nós de agente do Linux.</span><span class="sxs-lookup"><span data-stu-id="f73ae-123">hello following example creates a cluster named *myK8sCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive 
az acs create --orchestrator-type kubernetes --resource-group myResourceGroup --name myK8sCluster --generate-ssh-keys 
```

<span data-ttu-id="f73ae-124">Após alguns minutos, o comando de saudação for concluído e retorna informações de formatados em json sobre cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="f73ae-124">After several minutes, hello command completes and returns json formatted information about hello cluster.</span></span> 

## <a name="connect-toohello-cluster"></a><span data-ttu-id="f73ae-125">Conecte-se o cluster toohello</span><span class="sxs-lookup"><span data-stu-id="f73ae-125">Connect toohello cluster</span></span>

<span data-ttu-id="f73ae-126">use toomanage um cluster de Kubernetes [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), cliente de linha de comando do hello Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="f73ae-126">toomanage a Kubernetes cluster, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes command-line client.</span></span> 

<span data-ttu-id="f73ae-127">Se você estiver usando o Azure CloudShell, o kubectl já estará instalado.</span><span class="sxs-lookup"><span data-stu-id="f73ae-127">If you're using Azure CloudShell, kubectl is already installed.</span></span> <span data-ttu-id="f73ae-128">Se você quiser tooinstall localmente, você pode usar Olá [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) comando.</span><span class="sxs-lookup"><span data-stu-id="f73ae-128">If you want tooinstall it locally, you can use hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="f73ae-129">tooconfigure kubectl tooconnect tooyour Kubernetes cluster, execute Olá [az get-credenciais do acs kubernetes](/cli/azure/acs/kubernetes#get-credentials) comando.</span><span class="sxs-lookup"><span data-stu-id="f73ae-129">tooconfigure kubectl tooconnect tooyour Kubernetes cluster, run hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="f73ae-130">Esta etapa baixa credenciais e configura Olá toouse Kubernetes CLI-los.</span><span class="sxs-lookup"><span data-stu-id="f73ae-130">This step downloads credentials and configures hello Kubernetes CLI toouse them.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

<span data-ttu-id="f73ae-131">tooverify Olá conexão tooyour cluster use Olá [kubectl obter](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooreturn comando uma lista de nós de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="f73ae-131">tooverify hello connection tooyour cluster, use hello [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command tooreturn a list of hello cluster nodes.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="f73ae-132">Saída:</span><span class="sxs-lookup"><span data-stu-id="f73ae-132">Output:</span></span>

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-14ad53a1-0    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-1    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-2    Ready                      10m       v1.6.6
k8s-master-14ad53a1-0   Ready,SchedulingDisabled   10m       v1.6.6
```

## <a name="run-hello-application"></a><span data-ttu-id="f73ae-133">Executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="f73ae-133">Run hello application</span></span>

<span data-ttu-id="f73ae-134">Um arquivo de manifesto Kubernetes define o estado desejado para cluster hello, incluindo quais imagens de contêiner devem estar em execução.</span><span class="sxs-lookup"><span data-stu-id="f73ae-134">A Kubernetes manifest file defines a desired state for hello cluster, including what container images should be running.</span></span> <span data-ttu-id="f73ae-135">Neste exemplo, um manifesto é usada toocreate todos os objetos necessários toorun Olá aplicativo voto do Azure.</span><span class="sxs-lookup"><span data-stu-id="f73ae-135">For this example, a manifest is used toocreate all objects needed toorun hello Azure Vote application.</span></span> 

<span data-ttu-id="f73ae-136">Crie um arquivo chamado `azure-vote.yml` e copie nele Olá YAML a seguir.</span><span class="sxs-lookup"><span data-stu-id="f73ae-136">Create a file named `azure-vote.yml` and copy into it hello following YAML.</span></span> <span data-ttu-id="f73ae-137">Se você estiver trabalhando no Azure Cloud Shell, esse arquivo poderá ser criado usando o vi ou Nano, como se estivesse trabalhando em um sistema físico ou virtual.</span><span class="sxs-lookup"><span data-stu-id="f73ae-137">If you are working in Azure Cloud Shell, this file can be created using vi or Nano as if working on a virtual or physical system.</span></span>

```yaml
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-back
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-back
    spec:
      containers:
      - name: azure-vote-back
        image: redis
        ports:
        - containerPort: 6379
          name: redis
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-back
spec:
  ports:
  - port: 6379
  selector:
    app: azure-vote-back
---
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-front
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-front
    spec:
      containers:
      - name: azure-vote-front
        image: microsoft/azure-vote-front:redis-v1
        ports:
        - containerPort: 80
        env:
        - name: REDIS
          value: "azure-vote-back"
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-front
spec:
  type: LoadBalancer
  ports:
  - port: 80
  selector:
    app: azure-vote-front
```

<span data-ttu-id="f73ae-138">Saudação de uso [kubectl criar](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) aplicativo hello de toorun de comando.</span><span class="sxs-lookup"><span data-stu-id="f73ae-138">Use hello [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) command toorun hello application.</span></span>

```azurecli-interactive
kubectl create -f azure-vote.yml
```

<span data-ttu-id="f73ae-139">Saída:</span><span class="sxs-lookup"><span data-stu-id="f73ae-139">Output:</span></span>

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-hello-application"></a><span data-ttu-id="f73ae-140">Testar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="f73ae-140">Test hello application</span></span>

<span data-ttu-id="f73ae-141">Como o aplicativo hello é executado, uma [Kubernetes serviço](https://kubernetes.io/docs/concepts/services-networking/service/) é criado que expõe Olá toohello de front-end do aplicativo à internet.</span><span class="sxs-lookup"><span data-stu-id="f73ae-141">As hello application is run, a [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created that exposes hello application front end toohello internet.</span></span> <span data-ttu-id="f73ae-142">Esse processo pode levar alguns toocomplete de minutos.</span><span class="sxs-lookup"><span data-stu-id="f73ae-142">This process can take a few minutes toocomplete.</span></span> 

<span data-ttu-id="f73ae-143">toomonitor andamento, use Olá [kubectl obter serviço](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) com hello `--watch` argumento.</span><span class="sxs-lookup"><span data-stu-id="f73ae-143">toomonitor progress, use hello [kubectl get service](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command with hello `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="f73ae-144">Olá inicialmente **IP externo** para Olá *front do azure-voto* serviço aparece como *pendente*.</span><span class="sxs-lookup"><span data-stu-id="f73ae-144">Initially hello **EXTERNAL-IP** for hello *azure-vote-front* service appears as *pending*.</span></span> <span data-ttu-id="f73ae-145">Depois que o endereço IP externo de saudação foi alterado de *pendente* tooan *endereço IP*, use `CTRL-C` processo de inspeção de kubectl toostop hello.</span><span class="sxs-lookup"><span data-stu-id="f73ae-145">Once hello EXTERNAL-IP address has changed from *pending* tooan *IP address*, use `CTRL-C` toostop hello kubectl watch process.</span></span> 
  
```bash
azure-vote-front   10.0.34.242   <pending>     80:30676/TCP   7s
azure-vote-front   10.0.34.242   52.179.23.131   80:30676/TCP   2m
```

<span data-ttu-id="f73ae-146">Agora você pode procurar toohello externo toosee hello Azure voto de aplicativo do IP endereço.</span><span class="sxs-lookup"><span data-stu-id="f73ae-146">You can now browse toohello external IP address toosee hello Azure Vote App.</span></span>

![Imagem de navegação tooAzure voto](media/container-service-kubernetes-walkthrough/azure-vote.png)  

## <a name="delete-cluster"></a><span data-ttu-id="f73ae-148">Excluir cluster</span><span class="sxs-lookup"><span data-stu-id="f73ae-148">Delete cluster</span></span>
<span data-ttu-id="f73ae-149">Ao cluster Olá não for mais necessário, você pode usar o hello [excluir grupo de az](/cli/azure/group#delete) comando tooremove grupo de recursos de hello, serviço de contêiner e recursos todos relacionados.</span><span class="sxs-lookup"><span data-stu-id="f73ae-149">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a><span data-ttu-id="f73ae-150">Obter o código de saudação</span><span class="sxs-lookup"><span data-stu-id="f73ae-150">Get hello code</span></span>

<span data-ttu-id="f73ae-151">Nesse início rápido, imagens de contêiner criada previamente foram usada toocreate uma implantação Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="f73ae-151">In this quick start, pre-created container images have been used toocreate a Kubernetes deployment.</span></span> <span data-ttu-id="f73ae-152">Olá relacionados ao código do aplicativo, Dockerfile, e o arquivo de manifesto Kubernetes estão disponíveis no GitHub.</span><span class="sxs-lookup"><span data-stu-id="f73ae-152">hello related application code, Dockerfile, and Kubernetes manifest file are available on GitHub.</span></span>

[<span data-ttu-id="f73ae-153">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="f73ae-153">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="f73ae-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f73ae-154">Next steps</span></span>

<span data-ttu-id="f73ae-155">Nesse início rápido, implantado um cluster Kubernetes e implantado um aplicativo de multi-contêiner tooit.</span><span class="sxs-lookup"><span data-stu-id="f73ae-155">In this quick start, you deployed a Kubernetes cluster and deployed a multi-container application tooit.</span></span> 

<span data-ttu-id="f73ae-156">toolearn mais sobre o serviço de contêiner do Azure e passo a passo de um exemplo de código completo a toodeployment, continuar tutorial de cluster Kubernetes toohello.</span><span class="sxs-lookup"><span data-stu-id="f73ae-156">toolearn more about Azure Container Service, and walk through a complete code toodeployment example, continue toohello Kubernetes cluster tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f73ae-157">Gerenciar um cluster ACS Kubernetes</span><span class="sxs-lookup"><span data-stu-id="f73ae-157">Manage an ACS Kubernetes cluster</span></span>](./container-service-tutorial-kubernetes-prepare-app.md)
