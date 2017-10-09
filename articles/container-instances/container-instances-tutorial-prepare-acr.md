---
title: "tutorial de instâncias de contêiner aaaAzure - preparar o registro de contêiner do Azure | Microsoft Docs"
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
ms.openlocfilehash: 2525626125740c3c861fad36aad207d0b587ff54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="8113f-104">Implantar e usar o Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="8113f-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="8113f-105">Esta é a parte dois de um tutorial de três partes.</span><span class="sxs-lookup"><span data-stu-id="8113f-105">This is part two of a three-part tutorial.</span></span> <span data-ttu-id="8113f-106">Em Olá [etapa anterior](./container-instances-tutorial-prepare-app.md), uma imagem de contêiner foi criada para um aplicativo da web simples escrito em [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="8113f-106">In hello [previous step](./container-instances-tutorial-prepare-app.md), a container image was created for a simple web application written in [Node.js](http://nodejs.org).</span></span> <span data-ttu-id="8113f-107">Neste tutorial, esta imagem é enviada por push tooan registro de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="8113f-107">In this tutorial, this image is pushed tooan Azure Container Registry.</span></span> <span data-ttu-id="8113f-108">Se você não criou a imagem de contêiner hello, retornar muito[Tutorial 1 – Criar imagem de contêiner](./container-instances-tutorial-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="8113f-108">If you have not created hello container image, return too[Tutorial 1 – Create container image](./container-instances-tutorial-prepare-app.md).</span></span> 

<span data-ttu-id="8113f-109">Olá registro de contêiner do Azure é um registro baseado no Azure, em particular, para imagens de contêiner do Docker.</span><span class="sxs-lookup"><span data-stu-id="8113f-109">hello Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="8113f-110">Este tutorial orienta por meio de implantação de uma instância de registro de contêiner do Azure e enviar um tooit da imagem de contêiner.</span><span class="sxs-lookup"><span data-stu-id="8113f-110">This tutorial walks through deploying an Azure Container Registry instance, and pushing a container image tooit.</span></span> <span data-ttu-id="8113f-111">As etapas concluídas incluem:</span><span class="sxs-lookup"><span data-stu-id="8113f-111">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8113f-112">Implantando uma instância do Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="8113f-112">Deploying an Azure Container Registry instance</span></span>
> * <span data-ttu-id="8113f-113">Marcação de imagem de contêiner para o Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="8113f-113">Tagging container image for Azure Container Registry</span></span>
> * <span data-ttu-id="8113f-114">Carregar imagem tooAzure registro de contêiner</span><span class="sxs-lookup"><span data-stu-id="8113f-114">Uploading image tooAzure Container Registry</span></span>

<span data-ttu-id="8113f-115">Tutoriais subsequentes, você implanta contêiner de saudação do tooAzure seu registro privada instâncias de contêiner.</span><span class="sxs-lookup"><span data-stu-id="8113f-115">In subsequent tutorials, you deploy hello container from your private registry tooAzure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8113f-116">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="8113f-116">Before you begin</span></span>

<span data-ttu-id="8113f-117">Este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="8113f-117">This tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="8113f-118">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="8113f-118">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="8113f-119">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8113f-119">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="8113f-120">Implantar o Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="8113f-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="8113f-121">Ao implantar um Registro de Contêiner do Azure, primeiro você precisa de um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8113f-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="8113f-122">Um grupo de recursos do Azure é uma coleção lógica na qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="8113f-122">An Azure resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="8113f-123">Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="8113f-123">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="8113f-124">Neste exemplo, um grupo de recursos denominado *myResourceGroup* é criado no hello *eastus* região.</span><span class="sxs-lookup"><span data-stu-id="8113f-124">In this example, a resource group named *myResourceGroup* is created in hello *eastus* region.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="8113f-125">Criar um registro de contêiner do Azure com hello [criar acr az](/cli/azure/acr#create) comando.</span><span class="sxs-lookup"><span data-stu-id="8113f-125">Create an Azure Container registry with hello [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="8113f-126">nome de saudação de um registro de contêiner **devem ser exclusivos**.</span><span class="sxs-lookup"><span data-stu-id="8113f-126">hello name of a Container Registry **must be unique**.</span></span> <span data-ttu-id="8113f-127">Olá exemplo a seguir, usamos o nome de saudação *mycontainerregistry082*.</span><span class="sxs-lookup"><span data-stu-id="8113f-127">In hello following example, we use hello name *mycontainerregistry082*.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name mycontainerregistry082 --sku Basic --admin-enabled true
```

<span data-ttu-id="8113f-128">Restante Olá deste tutorial, usamos `<acrname>` como um espaço reservado para nome hello de registro de contêiner que você escolheu.</span><span class="sxs-lookup"><span data-stu-id="8113f-128">Throughout hello rest of this tutorial, we use `<acrname>` as a placeholder for hello container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="8113f-129">Logon no registro de contêiner</span><span class="sxs-lookup"><span data-stu-id="8113f-129">Container registry login</span></span>

<span data-ttu-id="8113f-130">Você deve fazer na instância ACR tooyour antes de enviar imagens tooit.</span><span class="sxs-lookup"><span data-stu-id="8113f-130">You must log in tooyour ACR instance before pushing images tooit.</span></span> <span data-ttu-id="8113f-131">Saudação de uso [logon de acr az](https://docs.microsoft.com/en-us/cli/azure/acr#login) toocomplete operação de saudação do comando.</span><span class="sxs-lookup"><span data-stu-id="8113f-131">Use hello [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command toocomplete hello operation.</span></span> <span data-ttu-id="8113f-132">É necessário nome exclusivo do hello tooprovide atribuído toohello registro de contêiner quando ele foi criado.</span><span class="sxs-lookup"><span data-stu-id="8113f-132">You need tooprovide hello unique name given toohello container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="8113f-133">comando Olá retorna uma mensagem de 'Logon bem-sucedido' uma vez concluída.</span><span class="sxs-lookup"><span data-stu-id="8113f-133">hello command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-image"></a><span data-ttu-id="8113f-134">Marcar imagem de contêiner</span><span class="sxs-lookup"><span data-stu-id="8113f-134">Tag container image</span></span>

<span data-ttu-id="8113f-135">toodeploy uma imagem de contêiner de um registro particular, a imagem de saudação precisa toobe marcado com hello `loginServer` nome do registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="8113f-135">toodeploy a container image from a private registry, hello image needs toobe tagged with hello `loginServer` name of hello registry.</span></span>

<span data-ttu-id="8113f-136">toosee uma lista de imagens atuais, use Olá `docker images` comando.</span><span class="sxs-lookup"><span data-stu-id="8113f-136">toosee a list of current images, use hello `docker images` command.</span></span>

```bash
docker images
```

<span data-ttu-id="8113f-137">Saída:</span><span class="sxs-lookup"><span data-stu-id="8113f-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

<span data-ttu-id="8113f-138">nome de loginServer em Olá tooget, execute Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="8113f-138">tooget hello loginServer name, run hello following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="8113f-139">Saudação de marca *aci de tutorial de aplicativo* imagem com loginServer de saudação do registro de contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="8113f-139">Tag hello *aci-tutorial-app* image with hello loginServer of hello container registry.</span></span> <span data-ttu-id="8113f-140">Além disso, adicionar `:v1` toohello final do nome da imagem hello.</span><span class="sxs-lookup"><span data-stu-id="8113f-140">Also, add `:v1` toohello end of hello image name.</span></span> <span data-ttu-id="8113f-141">Essa marca indica o número de versão de imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="8113f-141">This tag indicates hello image version number.</span></span>

```bash
docker tag aci-tutorial-app <acrLoginServer>/aci-tutorial-app:v1
```

<span data-ttu-id="8113f-142">Quando marcada, executar `docker images` tooverify operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="8113f-142">Once tagged, run `docker images` tooverify hello operation.</span></span>

```bash
docker images
```

<span data-ttu-id="8113f-143">Saída:</span><span class="sxs-lookup"><span data-stu-id="8113f-143">Output:</span></span>

```bash
REPOSITORY                                                TAG                 IMAGE ID            CREATED             SIZE
aci-tutorial-app                                          latest              5c745774dfa9        39 seconds ago      68.1 MB
mycontainerregistry082.azurecr.io/aci-tutorial-app        v1                  a9dace4e1a17        7 minutes ago       68.1 MB
```

## <a name="push-image-tooazure-container-registry"></a><span data-ttu-id="8113f-144">Imagem de push tooAzure registro de contêiner</span><span class="sxs-lookup"><span data-stu-id="8113f-144">Push image tooAzure Container Registry</span></span>

<span data-ttu-id="8113f-145">Enviar por push Olá *aci de tutorial de aplicativo* toohello registro da imagem.</span><span class="sxs-lookup"><span data-stu-id="8113f-145">Push hello *aci-tutorial-app* image toohello registry.</span></span>

<span data-ttu-id="8113f-146">Usando Olá exemplo a seguir, substitua Olá contêiner do registro loginServer por loginServer de saudação do seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="8113f-146">Using hello following example, replace hello container registry loginServer name with hello loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/aci-tutorial-app:v1
```

## <a name="list-images-in-azure-container-registry"></a><span data-ttu-id="8113f-147">Listar imagens no Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="8113f-147">List images in Azure Container Registry</span></span>

<span data-ttu-id="8113f-148">tooreturn uma lista de imagens que foram empurrados para registro de contêiner do Azure tooyour, Olá usuário [lista de repositórios de acr az](/cli/azure/acr/repository#list) comando.</span><span class="sxs-lookup"><span data-stu-id="8113f-148">tooreturn a list of images that have been pushed tooyour Azure Container registry, user hello [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="8113f-149">Atualize o comando Olá com nome de registro do contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="8113f-149">Update hello command with hello container registry name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="8113f-150">Saída:</span><span class="sxs-lookup"><span data-stu-id="8113f-150">Output:</span></span>

```azurecli
Result
----------------
aci-tutorial-app
```

<span data-ttu-id="8113f-151">E, em seguida, marcas de saudação toosee para uma imagem específica, use Olá [az acr Mostrar repositório marcas](/cli/azure/acr/repository#show-tags) comando.</span><span class="sxs-lookup"><span data-stu-id="8113f-151">And then toosee hello tags for a specific image, use hello [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository aci-tutorial-app --output table
```

<span data-ttu-id="8113f-152">Saída:</span><span class="sxs-lookup"><span data-stu-id="8113f-152">Output:</span></span>

```azurecli
Result
--------
v1
```

## <a name="next-steps"></a><span data-ttu-id="8113f-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8113f-153">Next steps</span></span>

<span data-ttu-id="8113f-154">Neste tutorial, um registro de contêiner do Azure foi preparado para uso com instâncias de contêiner do Azure e imagem de contêiner Olá foi enviada por push.</span><span class="sxs-lookup"><span data-stu-id="8113f-154">In this tutorial, an Azure Container Registry was prepared for use with Azure Container Instances, and hello container image was pushed.</span></span> <span data-ttu-id="8113f-155">Olá, as etapas a seguir foram concluída:</span><span class="sxs-lookup"><span data-stu-id="8113f-155">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8113f-156">Implantando uma instância do Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="8113f-156">Deploying an Azure Container Registry instance</span></span>
> * <span data-ttu-id="8113f-157">Marcação de imagem de contêiner para o Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="8113f-157">Tagging container image for Azure Container Registry</span></span>
> * <span data-ttu-id="8113f-158">Carregar imagem tooAzure registro de contêiner</span><span class="sxs-lookup"><span data-stu-id="8113f-158">Uploading image tooAzure Container Registry</span></span>

<span data-ttu-id="8113f-159">Avançar toohello toolearn próximo de tutorial sobre como implantar Olá contêiner tooAzure usando instâncias de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="8113f-159">Advance toohello next tutorial toolearn about deploying hello container tooAzure using Azure Container Instances.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8113f-160">Implantar contêineres tooAzure instâncias de contêiner</span><span class="sxs-lookup"><span data-stu-id="8113f-160">Deploy containers tooAzure Container Instances</span></span>](./container-instances-tutorial-deploy-app.md)
