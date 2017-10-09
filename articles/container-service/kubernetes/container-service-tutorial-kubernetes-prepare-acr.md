---
title: "tutorial de serviço de contêiner aaaAzure - preparar ACR | Microsoft Docs"
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
ms.openlocfilehash: 3980e5ce4eb9836f83c761a2f76c944bb3f13060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="4fa07-104">Implantar e usar o Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="4fa07-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="4fa07-105">O ACR (Registro de Contêiner do Azure) é um registro privado baseado no Azure, para imagens de contêiner do Docker.</span><span class="sxs-lookup"><span data-stu-id="4fa07-105">Azure Container Registry (ACR) is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="4fa07-106">Este tutorial, a parte dois dos sete, orienta por meio de implantação de uma instância de registro de contêiner do Azure e enviar um tooit da imagem de contêiner.</span><span class="sxs-lookup"><span data-stu-id="4fa07-106">This tutorial, part two of seven, walks through deploying an Azure Container Registry instance, and pushing a container image tooit.</span></span> <span data-ttu-id="4fa07-107">As etapas concluídas incluem:</span><span class="sxs-lookup"><span data-stu-id="4fa07-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4fa07-108">Implantando uma instância de ACR (Registro de Contêiner do Azure)</span><span class="sxs-lookup"><span data-stu-id="4fa07-108">Deploying an Azure Container Registry (ACR) instance</span></span>
> * <span data-ttu-id="4fa07-109">Marcando uma imagem de contêiner para ACR</span><span class="sxs-lookup"><span data-stu-id="4fa07-109">Tagging a container image for ACR</span></span>
> * <span data-ttu-id="4fa07-110">Carregando Olá imagem tooACR</span><span class="sxs-lookup"><span data-stu-id="4fa07-110">Uploading hello image tooACR</span></span>

<span data-ttu-id="4fa07-111">Nos próximos tutoriais, essa instância do ACR será integrada a um cluster do Kubernetes de Serviço de Contêiner do Azure, para executar as imagens de contêiner com segurança.</span><span class="sxs-lookup"><span data-stu-id="4fa07-111">In subsequent tutorials, this ACR instance is integrated with an Azure Container Service Kubernetes cluster, for securely running container images.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="4fa07-112">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="4fa07-112">Before you begin</span></span>

<span data-ttu-id="4fa07-113">Em Olá [tutorial anterior](./container-service-tutorial-kubernetes-prepare-app.md), uma imagem de contêiner foi criada para um aplicativo simples de votação do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fa07-113">In hello [previous tutorial](./container-service-tutorial-kubernetes-prepare-app.md), a container image was created for a simple Azure Voting application.</span></span> <span data-ttu-id="4fa07-114">Neste tutorial, esta imagem é enviada por push tooan registro de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fa07-114">In this tutorial, this image is pushed tooan Azure Container Registry.</span></span> <span data-ttu-id="4fa07-115">Se você não criou a imagem de aplicativo do Azure votação hello, retornar muito[Tutorial 1 – criar imagens de contêiner](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="4fa07-115">If you have not created hello Azure Voting app image, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> <span data-ttu-id="4fa07-116">Como alternativa, etapas Olá detalhadas aqui funcionam com qualquer imagem de contêiner.</span><span class="sxs-lookup"><span data-stu-id="4fa07-116">Alternatively, hello steps detailed here work with any container image.</span></span>

<span data-ttu-id="4fa07-117">Este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="4fa07-117">This tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="4fa07-118">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="4fa07-118">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="4fa07-119">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4fa07-119">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="4fa07-120">Implantar o Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="4fa07-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="4fa07-121">Ao implantar um Registro de Contêiner do Azure, primeiro você precisa de um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="4fa07-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="4fa07-122">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="4fa07-122">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="4fa07-123">Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="4fa07-123">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="4fa07-124">Neste exemplo, um grupo de recursos denominado *myResourceGroup* é criado no hello *westeurope* região.</span><span class="sxs-lookup"><span data-stu-id="4fa07-124">In this example, a resource group named *myResourceGroup* is created in hello *westeurope* region.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="4fa07-125">Criar um registro de contêiner do Azure com hello [criar acr az](/cli/azure/acr#create) comando.</span><span class="sxs-lookup"><span data-stu-id="4fa07-125">Create an Azure Container registry with hello [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="4fa07-126">nome de saudação de um registro de contêiner **devem ser exclusivos**.</span><span class="sxs-lookup"><span data-stu-id="4fa07-126">hello name of a Container Registry **must be unique**.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic --admin-enabled true
```

<span data-ttu-id="4fa07-127">Restante Olá deste tutorial, usamos "acrname" como um espaço reservado para nome hello de registro de contêiner que você escolheu.</span><span class="sxs-lookup"><span data-stu-id="4fa07-127">Throughout hello rest of this tutorial, we use "acrname" as a placeholder for hello container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="4fa07-128">Logon no registro de contêiner</span><span class="sxs-lookup"><span data-stu-id="4fa07-128">Container registry login</span></span>

<span data-ttu-id="4fa07-129">Você deve fazer na instância ACR tooyour antes de enviar imagens tooit.</span><span class="sxs-lookup"><span data-stu-id="4fa07-129">You must log in tooyour ACR instance before pushing images tooit.</span></span> <span data-ttu-id="4fa07-130">Saudação de uso [logon de acr az](https://docs.microsoft.com/en-us/cli/azure/acr#login) toocomplete operação de saudação do comando.</span><span class="sxs-lookup"><span data-stu-id="4fa07-130">Use hello [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command toocomplete hello operation.</span></span> <span data-ttu-id="4fa07-131">É necessário nome exclusivo do hello tooprovide atribuído toohello registro de contêiner quando ele foi criado.</span><span class="sxs-lookup"><span data-stu-id="4fa07-131">You need tooprovide hello unique name given toohello container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="4fa07-132">comando Olá retorna uma mensagem de 'Logon bem-sucedido' uma vez concluída.</span><span class="sxs-lookup"><span data-stu-id="4fa07-132">hello command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-images"></a><span data-ttu-id="4fa07-133">Marcar imagens de contêiner</span><span class="sxs-lookup"><span data-stu-id="4fa07-133">Tag container images</span></span>

<span data-ttu-id="4fa07-134">Cada imagem de contêiner precisa toobe marcada com o nome de loginServer de saudação do registro hello.</span><span class="sxs-lookup"><span data-stu-id="4fa07-134">Each container image needs toobe tagged with hello loginServer name of hello registry.</span></span> <span data-ttu-id="4fa07-135">Essa marca é usada para roteamento ao enviar o registro de imagem de tooan de imagens de contêiner.</span><span class="sxs-lookup"><span data-stu-id="4fa07-135">This tag is used for routing when pushing container images tooan image registry.</span></span>

<span data-ttu-id="4fa07-136">toosee uma lista de imagens atuais, use Olá [imagens do docker](https://docs.docker.com/engine/reference/commandline/images/) comando.</span><span class="sxs-lookup"><span data-stu-id="4fa07-136">toosee a list of current images, use hello [docker images](https://docs.docker.com/engine/reference/commandline/images/) command.</span></span>

```bash
docker images
```

<span data-ttu-id="4fa07-137">Saída:</span><span class="sxs-lookup"><span data-stu-id="4fa07-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front             latest              4675398c9172        13 minutes ago      694MB
redis                        latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask               788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="4fa07-138">nome de loginServer em Olá tooget, execute Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="4fa07-138">tooget hello loginServer name, run hello following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="4fa07-139">Agora, Olá de marca *front do azure-voto* imagem com loginServer de saudação do registro de contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="4fa07-139">Now, tag hello *azure-vote-front* image with hello loginServer of hello container registry.</span></span> <span data-ttu-id="4fa07-140">Além disso, adicionar `:redis-v1` toohello final do nome da imagem hello.</span><span class="sxs-lookup"><span data-stu-id="4fa07-140">Also, add `:redis-v1` toohello end of hello image name.</span></span> <span data-ttu-id="4fa07-141">Essa marca indica a versão da imagem hello.</span><span class="sxs-lookup"><span data-stu-id="4fa07-141">This tag indicates hello image version.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="4fa07-142">Quando marcada, execute [imagens docker] operação de saudação tooverify (https://docs.docker.com/engine/reference/commandline/images/).</span><span class="sxs-lookup"><span data-stu-id="4fa07-142">Once tagged, run [docker images] (https://docs.docker.com/engine/reference/commandline/images/) tooverify hello operation.</span></span>

```bash
docker images
```

<span data-ttu-id="4fa07-143">Saída:</span><span class="sxs-lookup"><span data-stu-id="4fa07-143">Output:</span></span>

```bash
REPOSITORY                                           TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front                                     latest              eaf2b9c57e5e        8 minutes ago       716 MB
mycontainerregistry082.azurecr.io/azure-vote-front   redis-v1            eaf2b9c57e5e        8 minutes ago       716 MB
redis                                                latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask                           flask               788ca94b2313        8 months ago        694 MB
```

## <a name="push-images-tooregistry"></a><span data-ttu-id="4fa07-144">Enviar por push tooregistry imagens</span><span class="sxs-lookup"><span data-stu-id="4fa07-144">Push images tooregistry</span></span>

<span data-ttu-id="4fa07-145">Enviar por push Olá *front do azure-voto* toohello registro da imagem.</span><span class="sxs-lookup"><span data-stu-id="4fa07-145">Push hello *azure-vote-front* image toohello registry.</span></span> 

<span data-ttu-id="4fa07-146">Usando Olá exemplo a seguir, substitua Olá ACR loginServer por loginServer de saudação do seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="4fa07-146">Using hello following example, replace hello ACR loginServer name with hello loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="4fa07-147">Isso leva alguns minutos toocomplete.</span><span class="sxs-lookup"><span data-stu-id="4fa07-147">This takes a couple of minutes toocomplete.</span></span>

## <a name="list-images-in-registry"></a><span data-ttu-id="4fa07-148">Lista de imagens no registro</span><span class="sxs-lookup"><span data-stu-id="4fa07-148">List images in registry</span></span>

<span data-ttu-id="4fa07-149">tooreturn uma lista de imagens que foram empurrados para registro de contêiner do Azure tooyour, Olá usuário [lista de repositórios de acr az](/cli/azure/acr/repository#list) comando.</span><span class="sxs-lookup"><span data-stu-id="4fa07-149">tooreturn a list of images that have been pushed tooyour Azure Container registry, user hello [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="4fa07-150">Atualize o comando Olá com nome de instância ACR hello.</span><span class="sxs-lookup"><span data-stu-id="4fa07-150">Update hello command with hello ACR instance name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="4fa07-151">Saída:</span><span class="sxs-lookup"><span data-stu-id="4fa07-151">Output:</span></span>

```azurecli
Result
----------------
azure-vote-front
```

<span data-ttu-id="4fa07-152">E, em seguida, marcas de saudação toosee para uma imagem específica, use Olá [az acr Mostrar repositório marcas](/cli/azure/acr/repository#show-tags) comando.</span><span class="sxs-lookup"><span data-stu-id="4fa07-152">And then toosee hello tags for a specific image, use hello [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository azure-vote-front --output table
```

<span data-ttu-id="4fa07-153">Saída:</span><span class="sxs-lookup"><span data-stu-id="4fa07-153">Output:</span></span>

```azurecli
Result
--------
redis-v1
```

<span data-ttu-id="4fa07-154">Na conclusão do tutorial, a imagem de contêiner de saudação foi armazenada em uma instância particular de registro de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fa07-154">At tutorial completion, hello container image has been stored in a private Azure Container Registry instance.</span></span> <span data-ttu-id="4fa07-155">Esta imagem é implantada do cluster do ACR tooa Kubernetes em tutoriais subsequentes.</span><span class="sxs-lookup"><span data-stu-id="4fa07-155">This image is deployed from ACR tooa Kubernetes cluster in subsequent tutorials.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fa07-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4fa07-156">Next steps</span></span>

<span data-ttu-id="4fa07-157">Neste tutorial, um Registro de Contêiner do Azure foi preparado para ser usado em um cluster do Kubernetes do ACS.</span><span class="sxs-lookup"><span data-stu-id="4fa07-157">In this tutorial, an Azure Container Registry was prepared for use in an ACS Kubernetes cluster.</span></span> <span data-ttu-id="4fa07-158">Olá, as etapas a seguir foram concluída:</span><span class="sxs-lookup"><span data-stu-id="4fa07-158">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4fa07-159">Implantando uma instância de Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="4fa07-159">Deployed an Azure Container Registry instance</span></span>
> * <span data-ttu-id="4fa07-160">Marcando uma imagem de contêiner para ACR</span><span class="sxs-lookup"><span data-stu-id="4fa07-160">Tagged a container image for ACR</span></span>
> * <span data-ttu-id="4fa07-161">Olá carregado tooACR de imagem</span><span class="sxs-lookup"><span data-stu-id="4fa07-161">Uploaded hello image tooACR</span></span>

<span data-ttu-id="4fa07-162">Avançar toohello toolearn próximo de tutorial sobre como implantar um cluster Kubernetes no Azure.</span><span class="sxs-lookup"><span data-stu-id="4fa07-162">Advance toohello next tutorial toolearn about deploying a Kubernetes cluster in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4fa07-163">Implantar um cluster do Kubernetes</span><span class="sxs-lookup"><span data-stu-id="4fa07-163">Deploy Kubernetes cluster</span></span>](./container-service-tutorial-kubernetes-deploy-cluster.md)