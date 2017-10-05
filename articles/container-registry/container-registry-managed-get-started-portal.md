---
title: Criar registro privado do Docker - portal do Azure | Microsoft Docs
description: "Introdução à criação e ao gerenciamento de contêiner privado do Docker com o portal do Azure"
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
ms.openlocfilehash: 560aee42b0c5a61c37c594d7937f833ab7183d49
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="create-a-managed-container-registry-using-the-azure-portal"></a><span data-ttu-id="dc09c-103">Criar um registro de contêiner gerenciado usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="dc09c-103">Create a managed container registry using the Azure portal</span></span>

<span data-ttu-id="dc09c-104">O Registro de Contêiner do Azure é um serviço de registro de contêiner Docker gerenciado usado para armazenar imagens de contêiner de Docker particulares.</span><span class="sxs-lookup"><span data-stu-id="dc09c-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="dc09c-105">Este guia detalha a criação de uma instância gerenciada do Registro de Contêiner do Azure usando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dc09c-105">This guide details creating a managed Azure Container Registry instance using the Azure portal.</span></span>

<span data-ttu-id="dc09c-106">Os registros de contêiner gerenciados do Azure estão em versão prévia e não estão disponíveis em todas as regiões.</span><span class="sxs-lookup"><span data-stu-id="dc09c-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="dc09c-107">Fazer logon no Azure</span><span class="sxs-lookup"><span data-stu-id="dc09c-107">Log in to Azure</span></span>

<span data-ttu-id="dc09c-108">Faça logon no Portal do Azure em http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="dc09c-108">Log in to the Azure portal at http://portal.azure.com.</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="dc09c-109">Criar um registro de contêiner</span><span class="sxs-lookup"><span data-stu-id="dc09c-109">Create a container registry</span></span>

1. <span data-ttu-id="dc09c-110">Clique no botão **Novo** no canto superior esquerdo do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dc09c-110">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="dc09c-111">Pesquise no marketplace o **registro de contêiner do Azure** e selecione-o.</span><span class="sxs-lookup"><span data-stu-id="dc09c-111">Search the marketplace for **Azure container registry** and select it.</span></span>

3. <span data-ttu-id="dc09c-112">Clique em **Criar**, que abrirá a folha de criação do ACR.</span><span class="sxs-lookup"><span data-stu-id="dc09c-112">Click **Create** which will open the ACR creation blade.</span></span>

    ![Configurações de registro de contêiner](./media/container-registry-get-started-portal/managed-container-registry-settings.png)

4. <span data-ttu-id="dc09c-114">Na folha **Registro de Contêiner do Azure**, insira as informações a seguir.</span><span class="sxs-lookup"><span data-stu-id="dc09c-114">In the **Azure Container Registry** blade, enter the following information.</span></span> <span data-ttu-id="dc09c-115">Clique em **Criar** quando terminar.</span><span class="sxs-lookup"><span data-stu-id="dc09c-115">Click **Create** when you are done.</span></span>

    <span data-ttu-id="dc09c-116">a.</span><span class="sxs-lookup"><span data-stu-id="dc09c-116">a.</span></span> <span data-ttu-id="dc09c-117">**Nome do registro**: um nome de domínio de nível superior exclusivo para o registro específico.</span><span class="sxs-lookup"><span data-stu-id="dc09c-117">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="dc09c-118">Neste exemplo, o nome do registro é *myAzureContainerRegistry1*, mas substitua-o por um nome exclusivo.</span><span class="sxs-lookup"><span data-stu-id="dc09c-118">In this example, the registry name is *myAzureContainerRegistry1*, but substitute a unique name of your own.</span></span> <span data-ttu-id="dc09c-119">O nome pode conter apenas letras e números.</span><span class="sxs-lookup"><span data-stu-id="dc09c-119">The name can contain only letters and numbers.</span></span>

    <span data-ttu-id="dc09c-120">b.</span><span class="sxs-lookup"><span data-stu-id="dc09c-120">b.</span></span> <span data-ttu-id="dc09c-121">**Grupo de recursos**: selecione um [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups) existente ou digite o nome de um novo.</span><span class="sxs-lookup"><span data-stu-id="dc09c-121">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type the name for a new one.</span></span>

    <span data-ttu-id="dc09c-122">c.</span><span class="sxs-lookup"><span data-stu-id="dc09c-122">c.</span></span> <span data-ttu-id="dc09c-123">**Local**: selecione um local de datacenter do Azure em que o serviço está [disponível](https://azure.microsoft.com/regions/services/), como **Centro-Sul dos EUA**.</span><span class="sxs-lookup"><span data-stu-id="dc09c-123">**Location**: Select an Azure datacenter location where the service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="dc09c-124">d.</span><span class="sxs-lookup"><span data-stu-id="dc09c-124">d.</span></span> <span data-ttu-id="dc09c-125">**Usuário administrador**: se desejar, habilite um usuário administrador para acessar o registro.</span><span class="sxs-lookup"><span data-stu-id="dc09c-125">**Admin user**: If you want, enable an admin user to access the registry.</span></span> <span data-ttu-id="dc09c-126">Você pode alterar essa configuração após a criação do registro.</span><span class="sxs-lookup"><span data-stu-id="dc09c-126">You can change this setting after creating the registry.</span></span>

    <span data-ttu-id="dc09c-127">e.</span><span class="sxs-lookup"><span data-stu-id="dc09c-127">e.</span></span> <span data-ttu-id="dc09c-128">**Registro gerenciado Use**: selecione Sim para que o ACR gerencie automaticamente o armazenamento de registro, use webhooks e use a autenticação do AAD.</span><span class="sxs-lookup"><span data-stu-id="dc09c-128">**Use managed registry**: Select yes to have ACR automatically manage the registry storage, use webhooks, and use AAD authentication.</span></span>

    <span data-ttu-id="dc09c-129">f.</span><span class="sxs-lookup"><span data-stu-id="dc09c-129">f.</span></span> <span data-ttu-id="dc09c-130">**Tipo de Preço**: selecione um tipo de preço, veja aqui os preços do ACR para saber mais.</span><span class="sxs-lookup"><span data-stu-id="dc09c-130">**Pricing Tier**: Select a pricing tier, see here ACR pricing for more information.</span></span>

## <a name="log-in-to-acr-instance"></a><span data-ttu-id="dc09c-131">Fazer logon na instância ACR</span><span class="sxs-lookup"><span data-stu-id="dc09c-131">Log in to ACR instance</span></span>

<span data-ttu-id="dc09c-132">Antes de enviar por push e pull imagens de contêiner, você deverá fazer logon na instância ACR.</span><span class="sxs-lookup"><span data-stu-id="dc09c-132">Before pushing and pulling container images, you must log in to the ACR instance.</span></span> 

<span data-ttu-id="dc09c-133">Para fazer isso, use a CLI do Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="dc09c-133">To do so, use the Azure CLI 2.0.</span></span> <span data-ttu-id="dc09c-134">Primeiro, se necessário, faça logon no Azure usando o comando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="dc09c-134">First, if needed, log into Azure using the [az login](/cli/azure/#login) command.</span></span> 

```azurecli
az login
```

<span data-ttu-id="dc09c-135">Em seguida, use o comando [az acr login](/cli/azure/acr#login) para fazer logon no Registro de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="dc09c-135">Next, use the [az acr login](/cli/azure/acr#login) command to log in to the Azure Container Registry.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

## <a name="use-azure-container-registry"></a><span data-ttu-id="dc09c-136">Usar o Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="dc09c-136">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="dc09c-137">Listar imagens de contêiner</span><span class="sxs-lookup"><span data-stu-id="dc09c-137">List container images</span></span>

<span data-ttu-id="dc09c-138">Use os comandos de CLI `az acr` para consultar as imagens e marcas em um repositório.</span><span class="sxs-lookup"><span data-stu-id="dc09c-138">Use the `az acr` CLI commands to query the images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="dc09c-139">Atualmente, o Registro de Contêiner não dá suporte ao comando `docker search` para consulta para imagens e marcas.</span><span class="sxs-lookup"><span data-stu-id="dc09c-139">Currently, Container Registry does not support the `docker search` command to query for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="dc09c-140">Listar repositórios</span><span class="sxs-lookup"><span data-stu-id="dc09c-140">List repositories</span></span>

<span data-ttu-id="dc09c-141">O seguinte exemplo lista os repositórios em um registro, no formato JSON (JavaScript Object Notation):</span><span class="sxs-lookup"><span data-stu-id="dc09c-141">The following example lists the repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="dc09c-142">Listar marcas</span><span class="sxs-lookup"><span data-stu-id="dc09c-142">List tags</span></span>

<span data-ttu-id="dc09c-143">O seguinte exemplo lista as marcas no repositório **samples/nginx**, no formato JSON:</span><span class="sxs-lookup"><span data-stu-id="dc09c-143">The following example lists the tags on the **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="dc09c-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dc09c-144">Next steps</span></span>

<span data-ttu-id="dc09c-145">Neste início rápido, você criou uma instância gerenciada do Registro de Contêiner do Azure usando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dc09c-145">In this quick start, you've created a managed Azure Container Registry instance using the Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dc09c-146">Enviar por push sua primeira imagem usando a CLI do Docker</span><span class="sxs-lookup"><span data-stu-id="dc09c-146">Push your first image using the Docker CLI</span></span>](container-registry-get-started-docker-cli.md)