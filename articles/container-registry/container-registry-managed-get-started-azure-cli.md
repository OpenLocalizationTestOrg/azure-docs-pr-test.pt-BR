---
title: "registro de contêiner de Docker particular do aaaCreate - CLI do Azure | Microsoft Docs"
description: "Começar a criar e gerenciar registros privados de contêiner do Docker com hello 2.0 do CLI do Azure"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: 2cadf42db0681a09c95486510f1e65c6f87c5280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-cli"></a><span data-ttu-id="c7973-103">Criar um registro de contêiner gerenciado usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="c7973-103">Create a managed container registry using hello Azure CLI</span></span>

<span data-ttu-id="c7973-104">O Registro de Contêiner do Azure é um serviço de registro de contêiner Docker gerenciado usado para armazenar imagens de contêiner de Docker particulares.</span><span class="sxs-lookup"><span data-stu-id="c7973-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="c7973-105">Esses detalhes de guia criando uma instância gerenciada do registro de contêiner do Azure usando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7973-105">This guide details creating a managed Azure Container Registry instance using hello Azure CLI.</span></span>

<span data-ttu-id="c7973-106">Os registros de contêiner gerenciados do Azure estão em versão prévia e não estão disponíveis em todas as regiões.</span><span class="sxs-lookup"><span data-stu-id="c7973-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c7973-107">Se você escolher tooinstall e usa o hello CLI localmente, este guia de início rápido requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="c7973-107">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="c7973-108">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7973-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="c7973-109">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c7973-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="c7973-110">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="c7973-110">Create a resource group</span></span>

<span data-ttu-id="c7973-111">Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="c7973-111">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="c7973-112">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c7973-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="c7973-113">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *westcentralus* local.</span><span class="sxs-lookup"><span data-stu-id="c7973-113">hello following example creates a resource group named *myResourceGroup* in hello *westcentralus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location westcentralus
```

## <a name="create-a-container-registry"></a><span data-ttu-id="c7973-114">Criar um registro de contêiner</span><span class="sxs-lookup"><span data-stu-id="c7973-114">Create a container registry</span></span>

<span data-ttu-id="c7973-115">Criar uma instância ACR usando Olá [criar acr az](/cli/azure/acr#create) comando.</span><span class="sxs-lookup"><span data-stu-id="c7973-115">Create an ACR instance using hello [az acr create](/cli/azure/acr#create) command.</span></span>

> [!NOTE]
> <span data-ttu-id="c7973-116">Ao criar um registro, especifique um nome de domínio de nível superior exclusivo que contenha apenas letras e números.</span><span class="sxs-lookup"><span data-stu-id="c7973-116">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span>

 <span data-ttu-id="c7973-117">nome do registro de saudação no exemplo hello é *myContainerRegistry1*, substituir um nome exclusivo.</span><span class="sxs-lookup"><span data-stu-id="c7973-117">hello registry name in hello example is *myContainerRegistry1*, substitute a unique name of your own.</span></span>

```azurecli
az acr create --name myContainerRegistry1 --resource-group myResourceGroup --sku Managed_Standard
```

<span data-ttu-id="c7973-118">Quando Olá registro é criado, a saída de hello é a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="c7973-118">When hello registry is created, hello output is similar toohello following:</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-29T04:50:28.607134+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry1",
  "location": "westcentralus",
  "loginServer": "mycontainerregistry1.azurecr.io",
  "name": "myContainerRegistry1",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "name": "Managed_Standard",
    "tier": "Managed"
  },
  "storageAccount": null,
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

## <a name="log-in-tooacr-instance"></a><span data-ttu-id="c7973-119">Faça logon na instância de tooACR</span><span class="sxs-lookup"><span data-stu-id="c7973-119">Log in tooACR instance</span></span>

<span data-ttu-id="c7973-120">Antes de enviar por push e pull imagens de contêiner, você deve fazer logon na instância ACR toohello.</span><span class="sxs-lookup"><span data-stu-id="c7973-120">Before pushing and pulling container images, you must log in toohello ACR instance.</span></span> <span data-ttu-id="c7973-121">toodo assim, use Olá [logon de acr az](/cli/azure/acr#login) comando.</span><span class="sxs-lookup"><span data-stu-id="c7973-121">toodo so, use hello [az acr login](/cli/azure/acr#login) command.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

<span data-ttu-id="c7973-122">comando Olá retorna uma mensagem de 'Logon bem-sucedido' uma vez concluída.</span><span class="sxs-lookup"><span data-stu-id="c7973-122">hello command returns a 'Login Succeeded' message once completed.</span></span>

## <a name="use-azure-container-registry"></a><span data-ttu-id="c7973-123">Usar o Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="c7973-123">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="c7973-124">Listar imagens de contêiner</span><span class="sxs-lookup"><span data-stu-id="c7973-124">List container images</span></span>

<span data-ttu-id="c7973-125">Saudação de uso `az acr` CLI comandos de imagens de saudação tooquery marcas em um repositório.</span><span class="sxs-lookup"><span data-stu-id="c7973-125">Use hello `az acr` CLI commands tooquery hello images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="c7973-126">Atualmente, registro de contêiner não dá suporte a saudação `docker search` tooquery de comando para imagens e marcas.</span><span class="sxs-lookup"><span data-stu-id="c7973-126">Currently, Container Registry does not support hello `docker search` command tooquery for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="c7973-127">Listar repositórios</span><span class="sxs-lookup"><span data-stu-id="c7973-127">List repositories</span></span>

<span data-ttu-id="c7973-128">Olá, exemplo a seguir lista os repositórios de saudação em um registro, no formato JSON (JavaScript Object Notation):</span><span class="sxs-lookup"><span data-stu-id="c7973-128">hello following example lists hello repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="c7973-129">Listar marcas</span><span class="sxs-lookup"><span data-stu-id="c7973-129">List tags</span></span>

<span data-ttu-id="c7973-130">Olá, exemplo a seguir lista as marcas de Olá Olá **exemplos/nginx** repositório, no formato JSON:</span><span class="sxs-lookup"><span data-stu-id="c7973-130">hello following example lists hello tags on hello **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="c7973-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c7973-131">Next steps</span></span>

<span data-ttu-id="c7973-132">Esse início rápido, você criou uma instância gerenciada do registro de contêiner do Azure usando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7973-132">In this quick start, you've created a managed Azure Container Registry instance using hello Azure CLI.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c7973-133">Enviar por push sua primeira imagem usando Olá CLI do Docker</span><span class="sxs-lookup"><span data-stu-id="c7973-133">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
