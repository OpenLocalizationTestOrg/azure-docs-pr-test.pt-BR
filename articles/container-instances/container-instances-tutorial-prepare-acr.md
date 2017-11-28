---
title: "Tutorial sobre Instâncias de Contêiner do Azure – preparar o Registro de Contêiner do Azure | Microsoft Docs"
description: "Tutorial sobre Instâncias de Contêiner do Azure – preparar o Registro de Contêiner do Azure"
services: container-instances
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Contêineres, Microsserviços, Kubernetes, DC/SO, Azure"
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: cc96ba9f5abd45a7503ba3327b30e1f809391384
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="20a13-104">Implantar e usar o Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="20a13-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="20a13-105">Esta é a parte dois de um tutorial de três partes.</span><span class="sxs-lookup"><span data-stu-id="20a13-105">This is part two of a three-part tutorial.</span></span> <span data-ttu-id="20a13-106">Na [etapa anterior](./container-instances-tutorial-prepare-app.md), uma imagem de contêiner foi criada para um aplicativo Web simples escrito em [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="20a13-106">In the [previous step](./container-instances-tutorial-prepare-app.md), a container image was created for a simple web application written in [Node.js](http://nodejs.org).</span></span> <span data-ttu-id="20a13-107">Neste tutorial, essa imagem é enviada por push para um Registro de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="20a13-107">In this tutorial, this image is pushed to an Azure Container Registry.</span></span> <span data-ttu-id="20a13-108">Se você não criou a imagem de contêiner, retorne ao [Tutorial 1 – Criar imagem de contêiner](./container-instances-tutorial-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="20a13-108">If you have not created the container image, return to [Tutorial 1 – Create container image](./container-instances-tutorial-prepare-app.md).</span></span> 

<span data-ttu-id="20a13-109">O Registro de Contêiner do Azure é um registro privado baseado no Azure para imagens de contêiner do Docker.</span><span class="sxs-lookup"><span data-stu-id="20a13-109">The Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="20a13-110">Este tutorial demonstra a implantação de uma instância do Registro de Contêiner do Azure e o envio por push de uma imagem de contêiner a ele.</span><span class="sxs-lookup"><span data-stu-id="20a13-110">This tutorial walks through deploying an Azure Container Registry instance, and pushing a container image to it.</span></span> <span data-ttu-id="20a13-111">As etapas concluídas incluem:</span><span class="sxs-lookup"><span data-stu-id="20a13-111">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="20a13-112">Implantando uma instância do Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="20a13-112">Deploying an Azure Container Registry instance</span></span>
> * <span data-ttu-id="20a13-113">Marcação de imagem de contêiner para o Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="20a13-113">Tagging container image for Azure Container Registry</span></span>
> * <span data-ttu-id="20a13-114">Upload da imagem para o Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="20a13-114">Uploading image to Azure Container Registry</span></span>

<span data-ttu-id="20a13-115">Nos tutoriais subsequentes, você implanta o contêiner do seu registro particular nas Instâncias de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="20a13-115">In subsequent tutorials, you deploy the container from your private registry to Azure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="20a13-116">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="20a13-116">Before you begin</span></span>

<span data-ttu-id="20a13-117">Este tutorial exige que você esteja executando a CLI do Azure versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="20a13-117">This tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="20a13-118">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="20a13-118">Run `az --version` to find the version.</span></span> <span data-ttu-id="20a13-119">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="20a13-119">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="20a13-120">Implantar o Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="20a13-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="20a13-121">Ao implantar um Registro de Contêiner do Azure, primeiro você precisa de um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="20a13-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="20a13-122">Um grupo de recursos do Azure é uma coleção lógica na qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="20a13-122">An Azure resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="20a13-123">Crie um grupo de recursos com o comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="20a13-123">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="20a13-124">Neste exemplo, um grupo de recursos denominado *myResourceGroup* é criado na região *eastus*.</span><span class="sxs-lookup"><span data-stu-id="20a13-124">In this example, a resource group named *myResourceGroup* is created in the *eastus* region.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="20a13-125">Crie um Registro de Contêiner do Azure com o comando [az acr create](/cli/azure/acr#create).</span><span class="sxs-lookup"><span data-stu-id="20a13-125">Create an Azure Container registry with the [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="20a13-126">O nome de um registro de contêiner **deve ser exclusivo**.</span><span class="sxs-lookup"><span data-stu-id="20a13-126">The name of a Container Registry **must be unique**.</span></span> <span data-ttu-id="20a13-127">No exemplo a seguir, usamos o nome *mycontainerregistry082*.</span><span class="sxs-lookup"><span data-stu-id="20a13-127">In the following example, we use the name *mycontainerregistry082*.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name mycontainerregistry082 --sku Basic --admin-enabled true
```

<span data-ttu-id="20a13-128">Durante o restante deste tutorial, utilizamos `<acrname>` como um espaço reservado para o nome do registro de contêiner escolhido.</span><span class="sxs-lookup"><span data-stu-id="20a13-128">Throughout the rest of this tutorial, we use `<acrname>` as a placeholder for the container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="20a13-129">Logon no registro de contêiner</span><span class="sxs-lookup"><span data-stu-id="20a13-129">Container registry login</span></span>

<span data-ttu-id="20a13-130">Você deverá entrar na instância do ACR antes de enviar imagens por push a ele.</span><span class="sxs-lookup"><span data-stu-id="20a13-130">You must log in to your ACR instance before pushing images to it.</span></span> <span data-ttu-id="20a13-131">Use o comando [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) para concluir a operação.</span><span class="sxs-lookup"><span data-stu-id="20a13-131">Use the [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command to complete the operation.</span></span> <span data-ttu-id="20a13-132">Você precisa fornecer o nome exclusivo fornecido para o registro de contêiner quando ele foi criado.</span><span class="sxs-lookup"><span data-stu-id="20a13-132">You need to provide the unique name given to the container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="20a13-133">O comando retorna uma mensagem de 'Logon bem-sucedido' quando é concluído.</span><span class="sxs-lookup"><span data-stu-id="20a13-133">The command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-image"></a><span data-ttu-id="20a13-134">Marcar imagem de contêiner</span><span class="sxs-lookup"><span data-stu-id="20a13-134">Tag container image</span></span>

<span data-ttu-id="20a13-135">Para implantar uma imagem de contêiner de um registro privado, é necessário que a imagem seja marcada com o nome de `loginServer` do registro.</span><span class="sxs-lookup"><span data-stu-id="20a13-135">To deploy a container image from a private registry, the image needs to be tagged with the `loginServer` name of the registry.</span></span>

<span data-ttu-id="20a13-136">Para ver uma lista de imagens atuais, use o comando `docker images`.</span><span class="sxs-lookup"><span data-stu-id="20a13-136">To see a list of current images, use the `docker images` command.</span></span>

```bash
docker images
```

<span data-ttu-id="20a13-137">Saída:</span><span class="sxs-lookup"><span data-stu-id="20a13-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

<span data-ttu-id="20a13-138">Para obter o nome de loginServer, execute o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="20a13-138">To get the loginServer name, run the following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="20a13-139">Marque a imagem *aci-tutorial-app* com o loginServer do registro de contêiner.</span><span class="sxs-lookup"><span data-stu-id="20a13-139">Tag the *aci-tutorial-app* image with the loginServer of the container registry.</span></span> <span data-ttu-id="20a13-140">Além disso, adicione `:v1` ao final do nome da imagem.</span><span class="sxs-lookup"><span data-stu-id="20a13-140">Also, add `:v1` to the end of the image name.</span></span> <span data-ttu-id="20a13-141">Essa marca indica o número de versão da imagem.</span><span class="sxs-lookup"><span data-stu-id="20a13-141">This tag indicates the image version number.</span></span>

```bash
docker tag aci-tutorial-app <acrLoginServer>/aci-tutorial-app:v1
```

<span data-ttu-id="20a13-142">Depois de marcar, execute `docker images` para verificar a operação.</span><span class="sxs-lookup"><span data-stu-id="20a13-142">Once tagged, run `docker images` to verify the operation.</span></span>

```bash
docker images
```

<span data-ttu-id="20a13-143">Saída:</span><span class="sxs-lookup"><span data-stu-id="20a13-143">Output:</span></span>

```bash
REPOSITORY                                                TAG                 IMAGE ID            CREATED             SIZE
aci-tutorial-app                                          latest              5c745774dfa9        39 seconds ago      68.1 MB
mycontainerregistry082.azurecr.io/aci-tutorial-app        v1                  a9dace4e1a17        7 minutes ago       68.1 MB
```

## <a name="push-image-to-azure-container-registry"></a><span data-ttu-id="20a13-144">Enviar imagem por push ao Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="20a13-144">Push image to Azure Container Registry</span></span>

<span data-ttu-id="20a13-145">Envie por push a imagem *aci-tutorial-app* ao registro.</span><span class="sxs-lookup"><span data-stu-id="20a13-145">Push the *aci-tutorial-app* image to the registry.</span></span>

<span data-ttu-id="20a13-146">Usando o exemplo a seguir, substitua o nome do loginServer do registro de contêiner pelo loginServer do seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="20a13-146">Using the following example, replace the container registry loginServer name with the loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/aci-tutorial-app:v1
```

## <a name="list-images-in-azure-container-registry"></a><span data-ttu-id="20a13-147">Listar imagens no Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="20a13-147">List images in Azure Container Registry</span></span>

<span data-ttu-id="20a13-148">Para retornar uma lista de imagens que foram enviadas por push ao Registro de Contêiner do Azure, use o comando [az acr repository list](/cli/azure/acr/repository#list).</span><span class="sxs-lookup"><span data-stu-id="20a13-148">To return a list of images that have been pushed to your Azure Container registry, user the [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="20a13-149">Atualize o comando com o nome do registro de contêiner.</span><span class="sxs-lookup"><span data-stu-id="20a13-149">Update the command with the container registry name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="20a13-150">Saída:</span><span class="sxs-lookup"><span data-stu-id="20a13-150">Output:</span></span>

```azurecli
Result
----------------
aci-tutorial-app
```

<span data-ttu-id="20a13-151">E, em seguida, para ver as marcas de uma imagem específica, use o comando [az acr repository show-tags](/cli/azure/acr/repository#show-tags).</span><span class="sxs-lookup"><span data-stu-id="20a13-151">And then to see the tags for a specific image, use the [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository aci-tutorial-app --output table
```

<span data-ttu-id="20a13-152">Saída:</span><span class="sxs-lookup"><span data-stu-id="20a13-152">Output:</span></span>

```azurecli
Result
--------
v1
```

## <a name="next-steps"></a><span data-ttu-id="20a13-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="20a13-153">Next steps</span></span>

<span data-ttu-id="20a13-154">Neste tutorial, foi preparado um Registro de Contêiner do Azure para ser usado com Instâncias de Contêiner do Azure e a imagem de contêiner foi enviada por push.</span><span class="sxs-lookup"><span data-stu-id="20a13-154">In this tutorial, an Azure Container Registry was prepared for use with Azure Container Instances, and the container image was pushed.</span></span> <span data-ttu-id="20a13-155">As etapas a seguir foram concluídas:</span><span class="sxs-lookup"><span data-stu-id="20a13-155">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="20a13-156">Implantando uma instância do Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="20a13-156">Deploying an Azure Container Registry instance</span></span>
> * <span data-ttu-id="20a13-157">Marcação de imagem de contêiner para o Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="20a13-157">Tagging container image for Azure Container Registry</span></span>
> * <span data-ttu-id="20a13-158">Upload da imagem para o Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="20a13-158">Uploading image to Azure Container Registry</span></span>

<span data-ttu-id="20a13-159">Avance para o próximo tutorial para saber mais sobre a implantação do contêiner no Azure usando as Instâncias de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="20a13-159">Advance to the next tutorial to learn about deploying the container to Azure using Azure Container Instances.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="20a13-160">Implantar contêineres nas Instâncias de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="20a13-160">Deploy containers to Azure Container Instances</span></span>](./container-instances-tutorial-deploy-app.md)
