---
title: "Tutorial do Serviço de Contêiner do Azure – implantar aplicativo | Microsoft Docs"
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
ms.openlocfilehash: ea67f0beb6a5926393b26e7590302ad0f46a63f9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="run-applications-in-kubernetes"></a><span data-ttu-id="2a7dd-104">Executar aplicativos no Kubernetes</span><span class="sxs-lookup"><span data-stu-id="2a7dd-104">Run applications in Kubernetes</span></span>

<span data-ttu-id="2a7dd-105">Neste tutorial, parte quatro de sete, um aplicativo de exemplo é implantado em um cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="2a7dd-105">In this tutorial, part four of seven, a sample application is deployed into a Kubernetes cluster.</span></span> <span data-ttu-id="2a7dd-106">As etapas concluídas incluem:</span><span class="sxs-lookup"><span data-stu-id="2a7dd-106">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2a7dd-107">Baixar arquivos de manifesto Kubernetes</span><span class="sxs-lookup"><span data-stu-id="2a7dd-107">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="2a7dd-108">Executar um aplicativo no Kubernetes</span><span class="sxs-lookup"><span data-stu-id="2a7dd-108">Run application in Kubernetes</span></span>
> * <span data-ttu-id="2a7dd-109">Testar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="2a7dd-109">Test the application</span></span>

<span data-ttu-id="2a7dd-110">Nos tutoriais subsequentes, esse aplicativo é escalado horizontalmente, atualizado e o Operations Management Suite configurado para monitorar o cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="2a7dd-110">In subsequent tutorials, this application is scaled out, updated, and Operations Management Suite configured to monitor the Kubernetes cluster.</span></span>

<span data-ttu-id="2a7dd-111">Este tutorial assume uma compreensão básica dos conceitos de Kubernetes; para obter informações detalhadas sobre Kubernetes consulte a [documentação do Kubernetes](https://kubernetes.io/docs/home/).</span><span class="sxs-lookup"><span data-stu-id="2a7dd-111">This tutorial assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see the [Kubernetes documentation](https://kubernetes.io/docs/home/).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2a7dd-112">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="2a7dd-112">Before you begin</span></span>

<span data-ttu-id="2a7dd-113">Nos tutoriais anteriores, um aplicativo foi empacotado em uma imagem de contêiner, essa imagem foi carregada no Registro de Contêiner do Azure e um cluster Kubernetes foi criado.</span><span class="sxs-lookup"><span data-stu-id="2a7dd-113">In previous tutorials, an application was packaged into a container image, this image was uploaded to Azure Container Registry, and a Kubernetes cluster was created.</span></span> <span data-ttu-id="2a7dd-114">Se você ainda não realizou essas etapas e deseja continuar acompanhando, retorne ao [Tutorial 1 – Criar imagens de contêiner](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="2a7dd-114">If you have not done these steps, and would like to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="2a7dd-115">No mínimo, este tutorial requer um cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="2a7dd-115">At minimum, this tutorial requires a Kubernetes cluster.</span></span>

## <a name="get-manifest-file"></a><span data-ttu-id="2a7dd-116">Obter arquivo de manifesto</span><span class="sxs-lookup"><span data-stu-id="2a7dd-116">Get manifest file</span></span>

<span data-ttu-id="2a7dd-117">Para este tutorial, [objetos Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) dão implantados utilizando um manifesto Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="2a7dd-117">For this tutorial, [Kubernetes objects](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) are deployed using a Kubernetes manifest.</span></span> <span data-ttu-id="2a7dd-118">Um manifesto Kubernetes é um arquivo formatado YAML ou JSON que contém instruções de implantação e configuração de objetos Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="2a7dd-118">A Kubernetes manifest is a YAML or JSON formatted file containing Kubernetes object deployment and configuration instructions.</span></span>

<span data-ttu-id="2a7dd-119">O arquivo de manifesto do aplicativo para este tutorial está disponível no repositório do aplicativo Azure Vote, que foi clonado em um tutorial anterior.</span><span class="sxs-lookup"><span data-stu-id="2a7dd-119">The application manifest file for this tutorial is available in the Azure Vote application repo, which was cloned in a previous tutorial.</span></span> <span data-ttu-id="2a7dd-120">Se você ainda não tiver feito isso, clone o repositório com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="2a7dd-120">If you have not already done so, clone the repo with the following command:</span></span> 

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="2a7dd-121">O arquivo de manifesto está localizado no seguinte diretório do repositório clonado.</span><span class="sxs-lookup"><span data-stu-id="2a7dd-121">The manifest file is found in the following directory of the cloned repo.</span></span>

```bash
/azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

## <a name="update-manifest-file"></a><span data-ttu-id="2a7dd-122">Atualizar arquivo de manifesto</span><span class="sxs-lookup"><span data-stu-id="2a7dd-122">Update manifest file</span></span>

<span data-ttu-id="2a7dd-123">Se estiver utilizando o Registro de Contêiner do Azure para armazenar as imagens de contêiner, será necessário atualizar o manifesto com o nome ACR loginServer.</span><span class="sxs-lookup"><span data-stu-id="2a7dd-123">If using Azure Container Registry to store the container images, the manifest needs to be updated with the ACR loginServer name.</span></span>

<span data-ttu-id="2a7dd-124">Obter o nome do servidor de logon ACR com o comando [az acr list](/cli/azure/acr#list).</span><span class="sxs-lookup"><span data-stu-id="2a7dd-124">Get the ACR login server name with the [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli-interactive
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="2a7dd-125">O manifesto de amostra foi pré-criado com um nome de repositório da *microsoft*.</span><span class="sxs-lookup"><span data-stu-id="2a7dd-125">The sample manifest has been pre-created with a repository name of *microsoft*.</span></span> <span data-ttu-id="2a7dd-126">Abra o arquivo com qualquer editor de texto e substitua o valor *microsoft* com o nome do servidor de logon da sua instância ACR.</span><span class="sxs-lookup"><span data-stu-id="2a7dd-126">Open the file with any text editor, and replace the *microsoft* value with the login server name of your ACR instance.</span></span>

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:redis-v1
```

## <a name="deploy-application"></a><span data-ttu-id="2a7dd-127">Implantar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="2a7dd-127">Deploy application</span></span>

<span data-ttu-id="2a7dd-128">Use o comando [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2a7dd-128">Use the [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) command to run the application.</span></span> <span data-ttu-id="2a7dd-129">Esse comando analisa o arquivo de manifesto e cria objetos Kubernetes definidos.</span><span class="sxs-lookup"><span data-stu-id="2a7dd-129">This command parses the manifest file and create the defined Kubernetes objects.</span></span>

```azurecli-interactive
kubectl create -f ./azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

<span data-ttu-id="2a7dd-130">Saída:</span><span class="sxs-lookup"><span data-stu-id="2a7dd-130">Output:</span></span>

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-application"></a><span data-ttu-id="2a7dd-131">Testar aplicativo</span><span class="sxs-lookup"><span data-stu-id="2a7dd-131">Test application</span></span>

<span data-ttu-id="2a7dd-132">Um [serviço Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/) é criado que expõe o aplicativo para a internet.</span><span class="sxs-lookup"><span data-stu-id="2a7dd-132">A [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created which exposes the application to the internet.</span></span> <span data-ttu-id="2a7dd-133">Esse processo pode levar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="2a7dd-133">This process can take a few minutes.</span></span> 

<span data-ttu-id="2a7dd-134">Para monitorar o andamento, use o comando [kubectl get service](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) com o argumento `--watch`.</span><span class="sxs-lookup"><span data-stu-id="2a7dd-134">To monitor progress, use the [kubectl get service](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) command with the `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="2a7dd-135">Inicialmente, o **EXTERNAL -IP** para o serviço *azure-vote-front* aparece como *pendente*.</span><span class="sxs-lookup"><span data-stu-id="2a7dd-135">Initially, the **EXTERNAL-IP** for the *azure-vote-front* service appears as *pending*.</span></span> <span data-ttu-id="2a7dd-136">Depois que o endereço EXTERNAL -IP foi alterado de *pendente* para *endereço IP*, use `CTRL-C` para interromper o processo kubectl watch.</span><span class="sxs-lookup"><span data-stu-id="2a7dd-136">Once the EXTERNAL-IP address has changed from *pending* to an *IP address*, use `CTRL-C` to stop the kubectl watch process.</span></span>

```bash
NAME               CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   10.0.42.158   <pending>     80:31873/TCP   1m
azure-vote-front   10.0.42.158   52.179.23.131 80:31873/TCP   2m
```

<span data-ttu-id="2a7dd-137">Para consultar o aplicativo, navegue até o endereço IP externo.</span><span class="sxs-lookup"><span data-stu-id="2a7dd-137">To see the application, browse to the external IP address.</span></span>

![Imagem do cluster Kubernetes no Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="next-steps"></a><span data-ttu-id="2a7dd-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2a7dd-139">Next steps</span></span>

<span data-ttu-id="2a7dd-140">Neste tutorial, o aplicativo Azure Vote foi implantado em um cluster Kubernetes do Serviço de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a7dd-140">In this tutorial, the Azure vote application was deployed to an Azure Container Service Kubernetes cluster.</span></span> <span data-ttu-id="2a7dd-141">As tarefas concluídas incluem:</span><span class="sxs-lookup"><span data-stu-id="2a7dd-141">Tasks completed include:</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="2a7dd-142">Baixar arquivos de manifesto Kubernetes</span><span class="sxs-lookup"><span data-stu-id="2a7dd-142">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="2a7dd-143">Executar um aplicativo no Kubernetes</span><span class="sxs-lookup"><span data-stu-id="2a7dd-143">Run the application in Kubernetes</span></span>
> * <span data-ttu-id="2a7dd-144">Testado o aplicativo</span><span class="sxs-lookup"><span data-stu-id="2a7dd-144">Tested the application</span></span>

<span data-ttu-id="2a7dd-145">Avance para o próximo tutorial para saber mais sobre como dimensionar um aplicativo Kubernetes e a infraestrutura do Kubernetes subjacente.</span><span class="sxs-lookup"><span data-stu-id="2a7dd-145">Advance to the next tutorial to learn about scaling both a Kubernetes application and the underlying Kubernetes infrastructure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="2a7dd-146">Dimensionar um aplicativo do Kubernetes e sua infraestrutura</span><span class="sxs-lookup"><span data-stu-id="2a7dd-146">Scale Kubernetes application and infrastructure</span></span>](./container-service-tutorial-kubernetes-scale.md)