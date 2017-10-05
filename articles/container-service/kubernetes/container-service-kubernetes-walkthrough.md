---
title: "Guia de início rápido - cluster Kubernetes do Azure para Linux | Microsoft Docs"
description: "Aprenda a criar um cluster Kubernetes para contêineres do Linux no Serviço de Contêiner do Azure rapidamente com a CLI do Azure."
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
ms.openlocfilehash: 5a2131659903e79b28f4d1b795d25a31d8d4ce8d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-kubernetes-cluster-for-linux-containers"></a><span data-ttu-id="82d0f-103">Implantar um cluster Kubernetes para contêineres do Linux</span><span class="sxs-lookup"><span data-stu-id="82d0f-103">Deploy Kubernetes cluster for Linux containers</span></span>

<span data-ttu-id="82d0f-104">Neste início rápido, um cluster Kubernetes é implantado usando a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="82d0f-104">In this quick start, a Kubernetes cluster is deployed using the Azure CLI.</span></span> <span data-ttu-id="82d0f-105">Em seguida, um aplicativo com vários contêineres, composto por um front-end na Web e uma instância Redis, é executado no cluster.</span><span class="sxs-lookup"><span data-stu-id="82d0f-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on the cluster.</span></span> <span data-ttu-id="82d0f-106">Depois de concluído, o aplicativo pode ser acessado pela internet.</span><span class="sxs-lookup"><span data-stu-id="82d0f-106">Once completed, the application is accessible over the internet.</span></span> 

<span data-ttu-id="82d0f-107">O exemplo de aplicativo usado neste documento é escrito em Python.</span><span class="sxs-lookup"><span data-stu-id="82d0f-107">The example application used in this document is written in Python.</span></span> <span data-ttu-id="82d0f-108">Os conceitos e as etapas detalhadas aqui podem ser usadas para implantar uma imagem de contêiner em um cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="82d0f-108">The concepts and steps detailed here can be used to deploy any container image into a Kubernetes cluster.</span></span> <span data-ttu-id="82d0f-109">O código, Dockerfile e arquivos de manifesto do Kubernetes criados previamente relacionados a este projeto estão disponíveis no [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git).</span><span class="sxs-lookup"><span data-stu-id="82d0f-109">The code, Dockerfile, and pre-created Kubernetes manifest files related to this project are available on [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git).</span></span>

![Imagem de navegação para o Voto do Azure](media/container-service-kubernetes-walkthrough/azure-vote.png)

<span data-ttu-id="82d0f-111">Este início rápido pressupõe uma compreensão básica dos conceitos de Kubernetes; para saber mais sobre Kubernetes, consulte a [documentação do Kubernetes]( https://kubernetes.io/docs/home/).</span><span class="sxs-lookup"><span data-stu-id="82d0f-111">This quick start assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see the [Kubernetes documentation]( https://kubernetes.io/docs/home/).</span></span>

<span data-ttu-id="82d0f-112">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="82d0f-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="82d0f-113">Se você optar por instalar e usar a CLI localmente, este guia de início rápido exigirá a execução da CLI do Azure versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="82d0f-113">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="82d0f-114">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="82d0f-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="82d0f-115">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="82d0f-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="82d0f-116">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="82d0f-116">Create a resource group</span></span>

<span data-ttu-id="82d0f-117">Crie um grupo de recursos com o comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="82d0f-117">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="82d0f-118">Um grupo de recursos do Azure é um grupo lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="82d0f-118">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="82d0f-119">O seguinte exemplo cria um grupo de recursos chamado *myResourceGroup* no local *westeurope*.</span><span class="sxs-lookup"><span data-stu-id="82d0f-119">The following example creates a resource group named *myResourceGroup* in the *westeurope* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="82d0f-120">Saída:</span><span class="sxs-lookup"><span data-stu-id="82d0f-120">Output:</span></span>

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

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="82d0f-121">Criar cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="82d0f-121">Create Kubernetes cluster</span></span>

<span data-ttu-id="82d0f-122">Crie um cluster Kubernetes no Serviço de Contêiner do Azure com o comando [az acs create](/cli/azure/acs#create).</span><span class="sxs-lookup"><span data-stu-id="82d0f-122">Create a Kubernetes cluster in Azure Container Service with the [az acs create](/cli/azure/acs#create) command.</span></span> <span data-ttu-id="82d0f-123">O exemplo a seguir cria um cluster denominado *myK8sCluster* com um nó Linux mestre e três nós de agente do Linux.</span><span class="sxs-lookup"><span data-stu-id="82d0f-123">The following example creates a cluster named *myK8sCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive 
az acs create --orchestrator-type kubernetes --resource-group myResourceGroup --name myK8sCluster --generate-ssh-keys 
```

<span data-ttu-id="82d0f-124">Após alguns minutos, o comando é concluído e retorna informações formatadas em json sobre o cluster.</span><span class="sxs-lookup"><span data-stu-id="82d0f-124">After several minutes, the command completes and returns json formatted information about the cluster.</span></span> 

## <a name="connect-to-the-cluster"></a><span data-ttu-id="82d0f-125">Conectar-se ao cluster</span><span class="sxs-lookup"><span data-stu-id="82d0f-125">Connect to the cluster</span></span>

<span data-ttu-id="82d0f-126">Para gerenciar um cluster Kubernetes, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), o cliente de linha de comando Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="82d0f-126">To manage a Kubernetes cluster, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), the Kubernetes command-line client.</span></span> 

<span data-ttu-id="82d0f-127">Se você estiver usando o Azure CloudShell, o kubectl já estará instalado.</span><span class="sxs-lookup"><span data-stu-id="82d0f-127">If you're using Azure CloudShell, kubectl is already installed.</span></span> <span data-ttu-id="82d0f-128">Se você deseja instalá-lo localmente, pode usar o comando [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli).</span><span class="sxs-lookup"><span data-stu-id="82d0f-128">If you want to install it locally, you can use the [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="82d0f-129">Para configurar o kubectl e se conectar ao cluster Kubernetes, execute o comando [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials).</span><span class="sxs-lookup"><span data-stu-id="82d0f-129">To configure kubectl to connect to your Kubernetes cluster, run the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="82d0f-130">Esta etapa baixa credenciais e configura a CLI de Kubernetes para usá-las.</span><span class="sxs-lookup"><span data-stu-id="82d0f-130">This step downloads credentials and configures the Kubernetes CLI to use them.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

<span data-ttu-id="82d0f-131">Para verificar a conexão ao seu cluster, use o comando [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) para retornar uma lista de nós do cluster.</span><span class="sxs-lookup"><span data-stu-id="82d0f-131">To verify the connection to your cluster, use the [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command to return a list of the cluster nodes.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="82d0f-132">Saída:</span><span class="sxs-lookup"><span data-stu-id="82d0f-132">Output:</span></span>

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-14ad53a1-0    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-1    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-2    Ready                      10m       v1.6.6
k8s-master-14ad53a1-0   Ready,SchedulingDisabled   10m       v1.6.6
```

## <a name="run-the-application"></a><span data-ttu-id="82d0f-133">Executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="82d0f-133">Run the application</span></span>

<span data-ttu-id="82d0f-134">Um arquivo de manifesto Kubernetes define um estado desejado para o cluster, incluindo as imagens de contêiner que devem estar em execução.</span><span class="sxs-lookup"><span data-stu-id="82d0f-134">A Kubernetes manifest file defines a desired state for the cluster, including what container images should be running.</span></span> <span data-ttu-id="82d0f-135">Neste exemplo, um manifesto é usado para criar todos os objetos necessários para executar o aplicativo Azure Vote.</span><span class="sxs-lookup"><span data-stu-id="82d0f-135">For this example, a manifest is used to create all objects needed to run the Azure Vote application.</span></span> 

<span data-ttu-id="82d0f-136">Crie um arquivo chamado `azure-vote.yml` e copie no YAML a seguir.</span><span class="sxs-lookup"><span data-stu-id="82d0f-136">Create a file named `azure-vote.yml` and copy into it the following YAML.</span></span> <span data-ttu-id="82d0f-137">Se você estiver trabalhando no Azure Cloud Shell, esse arquivo poderá ser criado usando o vi ou Nano, como se estivesse trabalhando em um sistema físico ou virtual.</span><span class="sxs-lookup"><span data-stu-id="82d0f-137">If you are working in Azure Cloud Shell, this file can be created using vi or Nano as if working on a virtual or physical system.</span></span>

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

<span data-ttu-id="82d0f-138">Use o comando [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="82d0f-138">Use the [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) command to run the application.</span></span>

```azurecli-interactive
kubectl create -f azure-vote.yml
```

<span data-ttu-id="82d0f-139">Saída:</span><span class="sxs-lookup"><span data-stu-id="82d0f-139">Output:</span></span>

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-the-application"></a><span data-ttu-id="82d0f-140">Testar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="82d0f-140">Test the application</span></span>

<span data-ttu-id="82d0f-141">Conforme o aplicativo é executado, um [serviço Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/) é criado para expor o front-end do aplicativo à Internet.</span><span class="sxs-lookup"><span data-stu-id="82d0f-141">As the application is run, a [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created that exposes the application front end to the internet.</span></span> <span data-ttu-id="82d0f-142">A conclusão desse processo pode levar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="82d0f-142">This process can take a few minutes to complete.</span></span> 

<span data-ttu-id="82d0f-143">Para monitorar o andamento, use o comando [kubectl get service](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) com o argumento `--watch`.</span><span class="sxs-lookup"><span data-stu-id="82d0f-143">To monitor progress, use the [kubectl get service](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command with the `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="82d0f-144">Inicialmente o **EXTERNAL -IP** para o serviço *azure-vote-front* aparece como *pendente*.</span><span class="sxs-lookup"><span data-stu-id="82d0f-144">Initially the **EXTERNAL-IP** for the *azure-vote-front* service appears as *pending*.</span></span> <span data-ttu-id="82d0f-145">Depois que o endereço EXTERNAL -IP foi alterado de *pendente* para *endereço IP*, use `CTRL-C` para interromper o processo kubectl watch.</span><span class="sxs-lookup"><span data-stu-id="82d0f-145">Once the EXTERNAL-IP address has changed from *pending* to an *IP address*, use `CTRL-C` to stop the kubectl watch process.</span></span> 
  
```bash
azure-vote-front   10.0.34.242   <pending>     80:30676/TCP   7s
azure-vote-front   10.0.34.242   52.179.23.131   80:30676/TCP   2m
```

<span data-ttu-id="82d0f-146">Agora você pode navegar para o endereço IP externo a fim de ver o aplicativo Azure Vote.</span><span class="sxs-lookup"><span data-stu-id="82d0f-146">You can now browse to the external IP address to see the Azure Vote App.</span></span>

![Imagem de navegação para o Voto do Azure](media/container-service-kubernetes-walkthrough/azure-vote.png)  

## <a name="delete-cluster"></a><span data-ttu-id="82d0f-148">Excluir cluster</span><span class="sxs-lookup"><span data-stu-id="82d0f-148">Delete cluster</span></span>
<span data-ttu-id="82d0f-149">Quando o cluster não for mais necessário, você poderá usar o comando [az group delete](/cli/azure/group#delete) para remover o grupo de recursos, o serviço de contêiner e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="82d0f-149">When the cluster is no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, container service, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-the-code"></a><span data-ttu-id="82d0f-150">Obter o código</span><span class="sxs-lookup"><span data-stu-id="82d0f-150">Get the code</span></span>

<span data-ttu-id="82d0f-151">Neste início rápido, foram usadas imagens de contêiner criadas previamente para criar uma implantação de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="82d0f-151">In this quick start, pre-created container images have been used to create a Kubernetes deployment.</span></span> <span data-ttu-id="82d0f-152">O código de aplicativo relacionado, o Dockerfile e o arquivo de manifesto Kubernetes estão disponíveis no GitHub.</span><span class="sxs-lookup"><span data-stu-id="82d0f-152">The related application code, Dockerfile, and Kubernetes manifest file are available on GitHub.</span></span>

[<span data-ttu-id="82d0f-153">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="82d0f-153">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="82d0f-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="82d0f-154">Next steps</span></span>

<span data-ttu-id="82d0f-155">Neste início rápido, você implantou um cluster Kubernetes e um aplicativo de com vários contêineres nele.</span><span class="sxs-lookup"><span data-stu-id="82d0f-155">In this quick start, you deployed a Kubernetes cluster and deployed a multi-container application to it.</span></span> 

<span data-ttu-id="82d0f-156">Para saber mais sobre o Serviço de Contêiner do Azure e percorrer um código completo de exemplo de implantação, prossiga para o tutorial de cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="82d0f-156">To learn more about Azure Container Service, and walk through a complete code to deployment example, continue to the Kubernetes cluster tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="82d0f-157">Gerenciar um cluster ACS Kubernetes</span><span class="sxs-lookup"><span data-stu-id="82d0f-157">Manage an ACS Kubernetes cluster</span></span>](./container-service-tutorial-kubernetes-prepare-app.md)
