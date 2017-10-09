---
title: "tutorial de serviço de contêiner aaaAzure - implantar aplicativos | Microsoft Docs"
description: "Tutorial do Serviço de Contêiner do Azure – implantar aplicativo"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Contêineres, Microsserviços, Kubernetes, DC/SO, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7e2fa06d359caf83e684df3966624a6e9a8e7efa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-applications-in-kubernetes"></a><span data-ttu-id="8a726-104">Executar aplicativos no Kubernetes</span><span class="sxs-lookup"><span data-stu-id="8a726-104">Run applications in Kubernetes</span></span>

<span data-ttu-id="8a726-105">Neste tutorial, parte quatro de sete, um aplicativo de exemplo é implantado em um cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="8a726-105">In this tutorial, part four of seven, a sample application is deployed into a Kubernetes cluster.</span></span> <span data-ttu-id="8a726-106">As etapas concluídas incluem:</span><span class="sxs-lookup"><span data-stu-id="8a726-106">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8a726-107">Baixar arquivos de manifesto Kubernetes</span><span class="sxs-lookup"><span data-stu-id="8a726-107">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="8a726-108">Executar um aplicativo no Kubernetes</span><span class="sxs-lookup"><span data-stu-id="8a726-108">Run application in Kubernetes</span></span>
> * <span data-ttu-id="8a726-109">Testar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="8a726-109">Test hello application</span></span>

<span data-ttu-id="8a726-110">Em tutoriais subsequentes, este aplicativo é expandido, atualizado, e Operations Management Suite configurado o cluster de Kubernetes toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="8a726-110">In subsequent tutorials, this application is scaled out, updated, and Operations Management Suite configured toomonitor hello Kubernetes cluster.</span></span>

<span data-ttu-id="8a726-111">Este tutorial assume uma compreensão básica dos conceitos de Kubernetes, para obter informações detalhadas sobre Kubernetes consulte Olá [Kubernetes documentação](https://kubernetes.io/docs/home/).</span><span class="sxs-lookup"><span data-stu-id="8a726-111">This tutorial assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see hello [Kubernetes documentation](https://kubernetes.io/docs/home/).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8a726-112">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="8a726-112">Before you begin</span></span>

<span data-ttu-id="8a726-113">Nos tutoriais anteriores, um aplicativo foi empacotado em uma imagem de contêiner, esta imagem foi carregada tooAzure registro de contêiner e um cluster Kubernetes foi criado.</span><span class="sxs-lookup"><span data-stu-id="8a726-113">In previous tutorials, an application was packaged into a container image, this image was uploaded tooAzure Container Registry, and a Kubernetes cluster was created.</span></span> <span data-ttu-id="8a726-114">Se você ainda não tiver feito essas etapas e deseja toofollow ao longo, retornar muito[Tutorial 1 – criar imagens de contêiner](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="8a726-114">If you have not done these steps, and would like toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="8a726-115">No mínimo, este tutorial requer um cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="8a726-115">At minimum, this tutorial requires a Kubernetes cluster.</span></span>

## <a name="get-manifest-file"></a><span data-ttu-id="8a726-116">Obter arquivo de manifesto</span><span class="sxs-lookup"><span data-stu-id="8a726-116">Get manifest file</span></span>

<span data-ttu-id="8a726-117">Para este tutorial, [objetos Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) dão implantados utilizando um manifesto Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="8a726-117">For this tutorial, [Kubernetes objects](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) are deployed using a Kubernetes manifest.</span></span> <span data-ttu-id="8a726-118">Um manifesto Kubernetes é um arquivo formatado YAML ou JSON que contém instruções de implantação e configuração de objetos Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="8a726-118">A Kubernetes manifest is a YAML or JSON formatted file containing Kubernetes object deployment and configuration instructions.</span></span>

<span data-ttu-id="8a726-119">arquivo de manifesto de aplicativo Hello para este tutorial está disponível no repositório de aplicativo do hello Azure voto, foi clonado em um tutorial anterior.</span><span class="sxs-lookup"><span data-stu-id="8a726-119">hello application manifest file for this tutorial is available in hello Azure Vote application repo, which was cloned in a previous tutorial.</span></span> <span data-ttu-id="8a726-120">Se você ainda não tiver feito isso, clone o repositório de saudação com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8a726-120">If you have not already done so, clone hello repo with hello following command:</span></span> 

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="8a726-121">arquivo de manifesto Olá encontra-se em Olá seguindo o diretório de repositório de saudação clonado.</span><span class="sxs-lookup"><span data-stu-id="8a726-121">hello manifest file is found in hello following directory of hello cloned repo.</span></span>

```bash
/azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

## <a name="update-manifest-file"></a><span data-ttu-id="8a726-122">Atualizar arquivo de manifesto</span><span class="sxs-lookup"><span data-stu-id="8a726-122">Update manifest file</span></span>

<span data-ttu-id="8a726-123">Se usar imagens de contêiner do registro de contêiner do Azure toostore hello, Olá toobe necessidades de manifesto atualizado com o nome de loginServer Olá ACR.</span><span class="sxs-lookup"><span data-stu-id="8a726-123">If using Azure Container Registry toostore hello container images, hello manifest needs toobe updated with hello ACR loginServer name.</span></span>

<span data-ttu-id="8a726-124">Obter o nome de servidor de logon do hello ACR com hello [lista de acr az](/cli/azure/acr#list) comando.</span><span class="sxs-lookup"><span data-stu-id="8a726-124">Get hello ACR login server name with hello [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli-interactive
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="8a726-125">Olá exemplo manifesto foi previamente criado com um nome de repositório de *microsoft*.</span><span class="sxs-lookup"><span data-stu-id="8a726-125">hello sample manifest has been pre-created with a repository name of *microsoft*.</span></span> <span data-ttu-id="8a726-126">Abra o arquivo hello com qualquer editor de texto e substitua Olá *microsoft* valor com o nome do servidor de logon de saudação da sua instância ACR.</span><span class="sxs-lookup"><span data-stu-id="8a726-126">Open hello file with any text editor, and replace hello *microsoft* value with hello login server name of your ACR instance.</span></span>

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:redis-v1
```

## <a name="deploy-application"></a><span data-ttu-id="8a726-127">Implantar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="8a726-127">Deploy application</span></span>

<span data-ttu-id="8a726-128">Saudação de uso [kubectl criar](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) aplicativo hello de toorun de comando.</span><span class="sxs-lookup"><span data-stu-id="8a726-128">Use hello [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) command toorun hello application.</span></span> <span data-ttu-id="8a726-129">Saudação de analisa esse comando arquivo de manifesto e criar objetos de Kubernetes de saudação definido.</span><span class="sxs-lookup"><span data-stu-id="8a726-129">This command parses hello manifest file and create hello defined Kubernetes objects.</span></span>

```azurecli-interactive
kubectl create -f ./azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

<span data-ttu-id="8a726-130">Saída:</span><span class="sxs-lookup"><span data-stu-id="8a726-130">Output:</span></span>

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-application"></a><span data-ttu-id="8a726-131">Testar aplicativo</span><span class="sxs-lookup"><span data-stu-id="8a726-131">Test application</span></span>

<span data-ttu-id="8a726-132">Um [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) é criado que expõe Olá aplicativo toohello internet.</span><span class="sxs-lookup"><span data-stu-id="8a726-132">A [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created which exposes hello application toohello internet.</span></span> <span data-ttu-id="8a726-133">Esse processo pode levar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="8a726-133">This process can take a few minutes.</span></span> 

<span data-ttu-id="8a726-134">toomonitor andamento, use Olá [kubectl obter serviço](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) com hello `--watch` argumento.</span><span class="sxs-lookup"><span data-stu-id="8a726-134">toomonitor progress, use hello [kubectl get service](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) command with hello `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="8a726-135">Inicialmente, hello **IP externo** para Olá *front do azure-voto* serviço aparece como *pendente*.</span><span class="sxs-lookup"><span data-stu-id="8a726-135">Initially, hello **EXTERNAL-IP** for hello *azure-vote-front* service appears as *pending*.</span></span> <span data-ttu-id="8a726-136">Depois que o endereço IP externo de saudação foi alterado de *pendente* tooan *endereço IP*, use `CTRL-C` processo de inspeção de kubectl toostop hello.</span><span class="sxs-lookup"><span data-stu-id="8a726-136">Once hello EXTERNAL-IP address has changed from *pending* tooan *IP address*, use `CTRL-C` toostop hello kubectl watch process.</span></span>

```bash
NAME               CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   10.0.42.158   <pending>     80:31873/TCP   1m
azure-vote-front   10.0.42.158   52.179.23.131 80:31873/TCP   2m
```

<span data-ttu-id="8a726-137">aplicativo de hello toosee, endereço IP externo de toohello procurar.</span><span class="sxs-lookup"><span data-stu-id="8a726-137">toosee hello application, browse toohello external IP address.</span></span>

![Imagem do cluster Kubernetes no Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="next-steps"></a><span data-ttu-id="8a726-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8a726-139">Next steps</span></span>

<span data-ttu-id="8a726-140">Neste tutorial, Olá aplicativo voto do Azure foi implantado tooan Kubernetes de serviço de contêiner do Azure cluster.</span><span class="sxs-lookup"><span data-stu-id="8a726-140">In this tutorial, hello Azure vote application was deployed tooan Azure Container Service Kubernetes cluster.</span></span> <span data-ttu-id="8a726-141">As tarefas concluídas incluem:</span><span class="sxs-lookup"><span data-stu-id="8a726-141">Tasks completed include:</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="8a726-142">Baixar arquivos de manifesto Kubernetes</span><span class="sxs-lookup"><span data-stu-id="8a726-142">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="8a726-143">Executar o aplicativo hello em Kubernetes</span><span class="sxs-lookup"><span data-stu-id="8a726-143">Run hello application in Kubernetes</span></span>
> * <span data-ttu-id="8a726-144">Aplicativo hello testado</span><span class="sxs-lookup"><span data-stu-id="8a726-144">Tested hello application</span></span>

<span data-ttu-id="8a726-145">Avançar toohello toolearn próximo de tutorial sobre como dimensionar um aplicativo Kubernetes e Olá Kubernetes infra-estrutura subjacente.</span><span class="sxs-lookup"><span data-stu-id="8a726-145">Advance toohello next tutorial toolearn about scaling both a Kubernetes application and hello underlying Kubernetes infrastructure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="8a726-146">Dimensionar um aplicativo do Kubernetes e sua infraestrutura</span><span class="sxs-lookup"><span data-stu-id="8a726-146">Scale Kubernetes application and infrastructure</span></span>](./container-service-tutorial-kubernetes-scale.md)