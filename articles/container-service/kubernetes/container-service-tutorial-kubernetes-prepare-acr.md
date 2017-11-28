---
title: "Tutorial do Serviço de Contêiner do Azure – preparar o ACR | Microsoft Docs"
description: "Tutorial do Serviço de Contêiner do Azure – preparar o ACR"
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
ms.openlocfilehash: 3e1f7617bf2fc52ee4c15598f51a46276f4dc57d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="77928-104">Implantar e usar o Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="77928-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="77928-105">O ACR (Registro de Contêiner do Azure) é um registro privado baseado no Azure, para imagens de contêiner do Docker.</span><span class="sxs-lookup"><span data-stu-id="77928-105">Azure Container Registry (ACR) is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="77928-106">Este tutorial, parte dois de sete, demonstra a implantação de uma instância de Registro de Contêiner do Azure e envia por push uma imagem de contêiner.</span><span class="sxs-lookup"><span data-stu-id="77928-106">This tutorial, part two of seven, walks through deploying an Azure Container Registry instance, and pushing a container image to it.</span></span> <span data-ttu-id="77928-107">As etapas concluídas incluem:</span><span class="sxs-lookup"><span data-stu-id="77928-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="77928-108">Implantando uma instância de ACR (Registro de Contêiner do Azure)</span><span class="sxs-lookup"><span data-stu-id="77928-108">Deploying an Azure Container Registry (ACR) instance</span></span>
> * <span data-ttu-id="77928-109">Marcando uma imagem de contêiner para ACR</span><span class="sxs-lookup"><span data-stu-id="77928-109">Tagging a container image for ACR</span></span>
> * <span data-ttu-id="77928-110">Carregando da imagem para ACR</span><span class="sxs-lookup"><span data-stu-id="77928-110">Uploading the image to ACR</span></span>

<span data-ttu-id="77928-111">Nos próximos tutoriais, essa instância do ACR será integrada a um cluster do Kubernetes de Serviço de Contêiner do Azure, para executar as imagens de contêiner com segurança.</span><span class="sxs-lookup"><span data-stu-id="77928-111">In subsequent tutorials, this ACR instance is integrated with an Azure Container Service Kubernetes cluster, for securely running container images.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="77928-112">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="77928-112">Before you begin</span></span>

<span data-ttu-id="77928-113">No [tutorial anterior](./container-service-tutorial-kubernetes-prepare-app.md), uma imagem de contêiner foi criada para um aplicativo de Votação do Azure simples.</span><span class="sxs-lookup"><span data-stu-id="77928-113">In the [previous tutorial](./container-service-tutorial-kubernetes-prepare-app.md), a container image was created for a simple Azure Voting application.</span></span> <span data-ttu-id="77928-114">Neste tutorial, essa imagem é enviada por push para um Registro de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="77928-114">In this tutorial, this image is pushed to an Azure Container Registry.</span></span> <span data-ttu-id="77928-115">Se você não tiver criado a imagem do aplicativo de Votação do Azure, retorne ao [Tutorial 1 – Criar imagens de contêiner](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="77928-115">If you have not created the Azure Voting app image, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> <span data-ttu-id="77928-116">Como alternativa, as etapas descritas aqui funcionam com qualquer imagem de contêiner.</span><span class="sxs-lookup"><span data-stu-id="77928-116">Alternatively, the steps detailed here work with any container image.</span></span>

<span data-ttu-id="77928-117">Este tutorial exige que você esteja executando a CLI do Azure versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="77928-117">This tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="77928-118">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="77928-118">Run `az --version` to find the version.</span></span> <span data-ttu-id="77928-119">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="77928-119">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="77928-120">Implantar o Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="77928-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="77928-121">Ao implantar um Registro de Contêiner do Azure, primeiro você precisa de um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="77928-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="77928-122">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="77928-122">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="77928-123">Crie um grupo de recursos com o comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="77928-123">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="77928-124">Neste exemplo, um grupo de recursos chamado *myResourceGroup* é criado na região *westeurope*.</span><span class="sxs-lookup"><span data-stu-id="77928-124">In this example, a resource group named *myResourceGroup* is created in the *westeurope* region.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="77928-125">Crie um Registro de Contêiner do Azure com o comando [az acr create](/cli/azure/acr#create).</span><span class="sxs-lookup"><span data-stu-id="77928-125">Create an Azure Container registry with the [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="77928-126">O nome de um registro de contêiner **deve ser exclusivo**.</span><span class="sxs-lookup"><span data-stu-id="77928-126">The name of a Container Registry **must be unique**.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic --admin-enabled true
```

<span data-ttu-id="77928-127">Durante o restante deste tutorial, utilizamos "acrname" como um espaço reservado para o nome do registro de contêiner escolhido.</span><span class="sxs-lookup"><span data-stu-id="77928-127">Throughout the rest of this tutorial, we use "acrname" as a placeholder for the container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="77928-128">Logon no registro de contêiner</span><span class="sxs-lookup"><span data-stu-id="77928-128">Container registry login</span></span>

<span data-ttu-id="77928-129">Você deverá entrar na instância do ACR antes de enviar imagens por push a ele.</span><span class="sxs-lookup"><span data-stu-id="77928-129">You must log in to your ACR instance before pushing images to it.</span></span> <span data-ttu-id="77928-130">Use o comando [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) para concluir a operação.</span><span class="sxs-lookup"><span data-stu-id="77928-130">Use the [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command to complete the operation.</span></span> <span data-ttu-id="77928-131">Você precisa fornecer o nome exclusivo fornecido para o registro de contêiner quando ele foi criado.</span><span class="sxs-lookup"><span data-stu-id="77928-131">You need to provide the unique name given to the container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="77928-132">O comando retorna uma mensagem de 'Logon bem-sucedido' quando é concluído.</span><span class="sxs-lookup"><span data-stu-id="77928-132">The command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-images"></a><span data-ttu-id="77928-133">Marcar imagens de contêiner</span><span class="sxs-lookup"><span data-stu-id="77928-133">Tag container images</span></span>

<span data-ttu-id="77928-134">Cada imagem de contêiner precisa ser marcada com o nome do registro loginServer.</span><span class="sxs-lookup"><span data-stu-id="77928-134">Each container image needs to be tagged with the loginServer name of the registry.</span></span> <span data-ttu-id="77928-135">Essa marca é usada para roteamento ao enviar imagens de contêiner por push a um registro da imagem.</span><span class="sxs-lookup"><span data-stu-id="77928-135">This tag is used for routing when pushing container images to an image registry.</span></span>

<span data-ttu-id="77928-136">Para consultar uma lista de imagens atuais, utilize o comando [docker images](https://docs.docker.com/engine/reference/commandline/images/).</span><span class="sxs-lookup"><span data-stu-id="77928-136">To see a list of current images, use the [docker images](https://docs.docker.com/engine/reference/commandline/images/) command.</span></span>

```bash
docker images
```

<span data-ttu-id="77928-137">Saída:</span><span class="sxs-lookup"><span data-stu-id="77928-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front             latest              4675398c9172        13 minutes ago      694MB
redis                        latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask               788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="77928-138">Para obter o nome de loginServer, execute o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="77928-138">To get the loginServer name, run the following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="77928-139">Agora, marque a imagem *azure-vote-front* com o loginServer do registro de contêiner.</span><span class="sxs-lookup"><span data-stu-id="77928-139">Now, tag the *azure-vote-front* image with the loginServer of the container registry.</span></span> <span data-ttu-id="77928-140">Além disso, adicione `:redis-v1` ao final do nome da imagem.</span><span class="sxs-lookup"><span data-stu-id="77928-140">Also, add `:redis-v1` to the end of the image name.</span></span> <span data-ttu-id="77928-141">Esta marcação indica a versão da imagem.</span><span class="sxs-lookup"><span data-stu-id="77928-141">This tag indicates the image version.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="77928-142">Quando marcada, execute [docker images] (https://docs.docker.com/engine/reference/commandline/images/) para verificar a operação.</span><span class="sxs-lookup"><span data-stu-id="77928-142">Once tagged, run [docker images] (https://docs.docker.com/engine/reference/commandline/images/) to verify the operation.</span></span>

```bash
docker images
```

<span data-ttu-id="77928-143">Saída:</span><span class="sxs-lookup"><span data-stu-id="77928-143">Output:</span></span>

```bash
REPOSITORY                                           TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front                                     latest              eaf2b9c57e5e        8 minutes ago       716 MB
mycontainerregistry082.azurecr.io/azure-vote-front   redis-v1            eaf2b9c57e5e        8 minutes ago       716 MB
redis                                                latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask                           flask               788ca94b2313        8 months ago        694 MB
```

## <a name="push-images-to-registry"></a><span data-ttu-id="77928-144">Efetuar push de imagens para registro</span><span class="sxs-lookup"><span data-stu-id="77928-144">Push images to registry</span></span>

<span data-ttu-id="77928-145">Enviar a imagem *azure-vote-front* por push ao registro.</span><span class="sxs-lookup"><span data-stu-id="77928-145">Push the *azure-vote-front* image to the registry.</span></span> 

<span data-ttu-id="77928-146">Usando o exemplo a seguir, substitua o nome do loginServer do ACR pelo loginServer do seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="77928-146">Using the following example, replace the ACR loginServer name with the loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="77928-147">Isso leva alguns minutos para ser concluído.</span><span class="sxs-lookup"><span data-stu-id="77928-147">This takes a couple of minutes to complete.</span></span>

## <a name="list-images-in-registry"></a><span data-ttu-id="77928-148">Lista de imagens no registro</span><span class="sxs-lookup"><span data-stu-id="77928-148">List images in registry</span></span>

<span data-ttu-id="77928-149">Para retornar uma lista de imagens que foram enviadas por push ao Registro de Contêiner do Azure, use o comando [az acr repository list](/cli/azure/acr/repository#list).</span><span class="sxs-lookup"><span data-stu-id="77928-149">To return a list of images that have been pushed to your Azure Container registry, user the [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="77928-150">Atualize o comando com o nome da instância do ACR.</span><span class="sxs-lookup"><span data-stu-id="77928-150">Update the command with the ACR instance name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="77928-151">Saída:</span><span class="sxs-lookup"><span data-stu-id="77928-151">Output:</span></span>

```azurecli
Result
----------------
azure-vote-front
```

<span data-ttu-id="77928-152">E, em seguida, para ver as marcas de uma imagem específica, use o comando [az acr repository show-tags](/cli/azure/acr/repository#show-tags).</span><span class="sxs-lookup"><span data-stu-id="77928-152">And then to see the tags for a specific image, use the [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository azure-vote-front --output table
```

<span data-ttu-id="77928-153">Saída:</span><span class="sxs-lookup"><span data-stu-id="77928-153">Output:</span></span>

```azurecli
Result
--------
redis-v1
```

<span data-ttu-id="77928-154">Na conclusão do tutorial, a imagem de contêiner foi armazenada em uma instância privada de Registro de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="77928-154">At tutorial completion, the container image has been stored in a private Azure Container Registry instance.</span></span> <span data-ttu-id="77928-155">Essa imagem será implantada do ACR para um cluster Kubernetes em tutoriais subsequentes.</span><span class="sxs-lookup"><span data-stu-id="77928-155">This image is deployed from ACR to a Kubernetes cluster in subsequent tutorials.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77928-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="77928-156">Next steps</span></span>

<span data-ttu-id="77928-157">Neste tutorial, um Registro de Contêiner do Azure foi preparado para ser usado em um cluster do Kubernetes do ACS.</span><span class="sxs-lookup"><span data-stu-id="77928-157">In this tutorial, an Azure Container Registry was prepared for use in an ACS Kubernetes cluster.</span></span> <span data-ttu-id="77928-158">As etapas a seguir foram concluídas:</span><span class="sxs-lookup"><span data-stu-id="77928-158">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="77928-159">Implantando uma instância de Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="77928-159">Deployed an Azure Container Registry instance</span></span>
> * <span data-ttu-id="77928-160">Marcando uma imagem de contêiner para ACR</span><span class="sxs-lookup"><span data-stu-id="77928-160">Tagged a container image for ACR</span></span>
> * <span data-ttu-id="77928-161">Carregando a imagem para ACR</span><span class="sxs-lookup"><span data-stu-id="77928-161">Uploaded the image to ACR</span></span>

<span data-ttu-id="77928-162">Avance para o próximo tutorial para saber mais sobre a implantação de um cluster do Kubernetes no Azure.</span><span class="sxs-lookup"><span data-stu-id="77928-162">Advance to the next tutorial to learn about deploying a Kubernetes cluster in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="77928-163">Implantar um cluster do Kubernetes</span><span class="sxs-lookup"><span data-stu-id="77928-163">Deploy Kubernetes cluster</span></span>](./container-service-tutorial-kubernetes-deploy-cluster.md)