---
title: registro de Docker privado aaaCreate - portal do Azure | Microsoft Docs
description: "Começar a criar e gerenciar registros privados de contêiner do Docker com hello portal do Azure"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: cf3ce0dcf3036d0e9cd1eaf01721deccb00248d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-portal"></a><span data-ttu-id="ded5b-103">Criar um registro de contêiner gerenciado usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ded5b-103">Create a managed container registry using hello Azure portal</span></span>

<span data-ttu-id="ded5b-104">O Registro de Contêiner do Azure é um serviço de registro de contêiner Docker gerenciado usado para armazenar imagens de contêiner de Docker particulares.</span><span class="sxs-lookup"><span data-stu-id="ded5b-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="ded5b-105">Esses detalhes de guia criando uma instância gerenciada do registro de contêiner do Azure usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ded5b-105">This guide details creating a managed Azure Container Registry instance using hello Azure portal.</span></span>

<span data-ttu-id="ded5b-106">Os registros de contêiner gerenciados do Azure estão em versão prévia e não estão disponíveis em todas as regiões.</span><span class="sxs-lookup"><span data-stu-id="ded5b-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="ded5b-107">Faça logon no tooAzure</span><span class="sxs-lookup"><span data-stu-id="ded5b-107">Log in tooAzure</span></span>

<span data-ttu-id="ded5b-108">Faça logon em toohello portal do Azure em http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="ded5b-108">Log in toohello Azure portal at http://portal.azure.com.</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="ded5b-109">Criar um registro de contêiner</span><span class="sxs-lookup"><span data-stu-id="ded5b-109">Create a container registry</span></span>

1. <span data-ttu-id="ded5b-110">Clique em Olá **novo** botão localizado no canto superior esquerdo de saudação do hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ded5b-110">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="ded5b-111">Marketplace de saudação de pesquisa para **registro de contêiner do Azure** e selecioná-lo.</span><span class="sxs-lookup"><span data-stu-id="ded5b-111">Search hello marketplace for **Azure container registry** and select it.</span></span>

3. <span data-ttu-id="ded5b-112">Clique em **criar** que abrirá a folha de criação de ACR hello.</span><span class="sxs-lookup"><span data-stu-id="ded5b-112">Click **Create** which will open hello ACR creation blade.</span></span>

    ![Configurações de registro de contêiner](./media/container-registry-get-started-portal/managed-container-registry-settings.png)

4. <span data-ttu-id="ded5b-114">Em Olá **registro de contêiner do Azure** folha, digite Olá informações a seguir.</span><span class="sxs-lookup"><span data-stu-id="ded5b-114">In hello **Azure Container Registry** blade, enter hello following information.</span></span> <span data-ttu-id="ded5b-115">Clique em **Criar** quando terminar.</span><span class="sxs-lookup"><span data-stu-id="ded5b-115">Click **Create** when you are done.</span></span>

    <span data-ttu-id="ded5b-116">a.</span><span class="sxs-lookup"><span data-stu-id="ded5b-116">a.</span></span> <span data-ttu-id="ded5b-117">**Nome do registro**: um nome de domínio de nível superior exclusivo para o registro específico.</span><span class="sxs-lookup"><span data-stu-id="ded5b-117">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="ded5b-118">Neste exemplo, o nome de registro de saudação é *myAzureContainerRegistry1*, mas substitua um nome exclusivo.</span><span class="sxs-lookup"><span data-stu-id="ded5b-118">In this example, hello registry name is *myAzureContainerRegistry1*, but substitute a unique name of your own.</span></span> <span data-ttu-id="ded5b-119">nome de saudação pode conter apenas letras e números.</span><span class="sxs-lookup"><span data-stu-id="ded5b-119">hello name can contain only letters and numbers.</span></span>

    <span data-ttu-id="ded5b-120">b.</span><span class="sxs-lookup"><span data-stu-id="ded5b-120">b.</span></span> <span data-ttu-id="ded5b-121">**Grupo de recursos**: selecione uma existente [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups) ou nome de saudação do tipo para um novo.</span><span class="sxs-lookup"><span data-stu-id="ded5b-121">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span>

    <span data-ttu-id="ded5b-122">c.</span><span class="sxs-lookup"><span data-stu-id="ded5b-122">c.</span></span> <span data-ttu-id="ded5b-123">**Local**: selecione um local de data center do Azure onde está o serviço Olá [disponível](https://azure.microsoft.com/regions/services/), como **Centro Sul dos EUA**.</span><span class="sxs-lookup"><span data-stu-id="ded5b-123">**Location**: Select an Azure datacenter location where hello service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="ded5b-124">d.</span><span class="sxs-lookup"><span data-stu-id="ded5b-124">d.</span></span> <span data-ttu-id="ded5b-125">**O usuário administrador**: se desejar, habilite um registro de saudação de tooaccess de usuário admin.</span><span class="sxs-lookup"><span data-stu-id="ded5b-125">**Admin user**: If you want, enable an admin user tooaccess hello registry.</span></span> <span data-ttu-id="ded5b-126">Você pode alterar essa configuração após a criação do registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="ded5b-126">You can change this setting after creating hello registry.</span></span>

    <span data-ttu-id="ded5b-127">e.</span><span class="sxs-lookup"><span data-stu-id="ded5b-127">e.</span></span> <span data-ttu-id="ded5b-128">**Registro gerenciado Use**: selecione Sim toohave ACR automaticamente gerenciar armazenamento de registro hello, use webhooks e usar a autenticação do AAD.</span><span class="sxs-lookup"><span data-stu-id="ded5b-128">**Use managed registry**: Select yes toohave ACR automatically manage hello registry storage, use webhooks, and use AAD authentication.</span></span>

    <span data-ttu-id="ded5b-129">f.</span><span class="sxs-lookup"><span data-stu-id="ded5b-129">f.</span></span> <span data-ttu-id="ded5b-130">**Tipo de Preço**: selecione um tipo de preço, veja aqui os preços do ACR para saber mais.</span><span class="sxs-lookup"><span data-stu-id="ded5b-130">**Pricing Tier**: Select a pricing tier, see here ACR pricing for more information.</span></span>

## <a name="log-in-tooacr-instance"></a><span data-ttu-id="ded5b-131">Faça logon na instância de tooACR</span><span class="sxs-lookup"><span data-stu-id="ded5b-131">Log in tooACR instance</span></span>

<span data-ttu-id="ded5b-132">Antes de enviar por push e pull imagens de contêiner, você deve fazer logon na instância ACR toohello.</span><span class="sxs-lookup"><span data-stu-id="ded5b-132">Before pushing and pulling container images, you must log in toohello ACR instance.</span></span> 

<span data-ttu-id="ded5b-133">Assim, o toodo usar Olá 2.0 do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="ded5b-133">toodo so, use hello Azure CLI 2.0.</span></span> <span data-ttu-id="ded5b-134">Primeiro, se necessário, faça logon no Azure usando Olá [logon az](/cli/azure/#login) comando.</span><span class="sxs-lookup"><span data-stu-id="ded5b-134">First, if needed, log into Azure using hello [az login](/cli/azure/#login) command.</span></span> 

```azurecli
az login
```

<span data-ttu-id="ded5b-135">Em seguida, use Olá [logon de acr az](/cli/azure/acr#login) comando toolog em toohello do registro de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="ded5b-135">Next, use hello [az acr login](/cli/azure/acr#login) command toolog in toohello Azure Container Registry.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

## <a name="use-azure-container-registry"></a><span data-ttu-id="ded5b-136">Usar o Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="ded5b-136">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="ded5b-137">Listar imagens de contêiner</span><span class="sxs-lookup"><span data-stu-id="ded5b-137">List container images</span></span>

<span data-ttu-id="ded5b-138">Saudação de uso `az acr` CLI comandos de imagens de saudação tooquery marcas em um repositório.</span><span class="sxs-lookup"><span data-stu-id="ded5b-138">Use hello `az acr` CLI commands tooquery hello images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="ded5b-139">Atualmente, registro de contêiner não dá suporte a saudação `docker search` tooquery de comando para imagens e marcas.</span><span class="sxs-lookup"><span data-stu-id="ded5b-139">Currently, Container Registry does not support hello `docker search` command tooquery for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="ded5b-140">Listar repositórios</span><span class="sxs-lookup"><span data-stu-id="ded5b-140">List repositories</span></span>

<span data-ttu-id="ded5b-141">Olá, exemplo a seguir lista os repositórios de saudação em um registro, no formato JSON (JavaScript Object Notation):</span><span class="sxs-lookup"><span data-stu-id="ded5b-141">hello following example lists hello repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="ded5b-142">Listar marcas</span><span class="sxs-lookup"><span data-stu-id="ded5b-142">List tags</span></span>

<span data-ttu-id="ded5b-143">Olá, exemplo a seguir lista as marcas de Olá Olá **exemplos/nginx** repositório, no formato JSON:</span><span class="sxs-lookup"><span data-stu-id="ded5b-143">hello following example lists hello tags on hello **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="ded5b-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ded5b-144">Next steps</span></span>

<span data-ttu-id="ded5b-145">Esse início rápido, você criou uma instância gerenciada do registro de contêiner do Azure usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ded5b-145">In this quick start, you've created a managed Azure Container Registry instance using hello Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ded5b-146">Enviar por push sua primeira imagem usando Olá CLI do Docker</span><span class="sxs-lookup"><span data-stu-id="ded5b-146">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
