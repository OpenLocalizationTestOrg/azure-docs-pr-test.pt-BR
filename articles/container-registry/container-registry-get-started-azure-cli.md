---
title: "registro de contêiner de Docker particular do aaaCreate - CLI do Azure | Microsoft Docs"
description: "Começar a criar e gerenciar registros privados de contêiner do Docker com hello 2.0 do CLI do Azure"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0d876a70b71a5e1bd564fbc9198f693dfe8a347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-cli-20"></a><span data-ttu-id="97714-103">Criar um registro de contêiner do Docker privado usando Olá 2.0 do CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="97714-103">Create a private Docker container registry using hello Azure CLI 2.0</span></span>
<span data-ttu-id="97714-104">Usar os comandos Olá [2.0 do CLI do Azure](https://github.com/Azure/azure-cli) toocreate um registro de contêiner e gerenciar as configurações do seu computador Linux, Mac ou Windows.</span><span class="sxs-lookup"><span data-stu-id="97714-104">Use commands in hello [Azure CLI 2.0](https://github.com/Azure/azure-cli) toocreate a container registry and manage its settings from your Linux, Mac, or Windows computer.</span></span> <span data-ttu-id="97714-105">Você também pode criar e gerenciar registros de contêiner usando Olá [portal do Azure](container-registry-get-started-portal.md) ou programaticamente com hello registro de contêiner [API REST](https://go.microsoft.com/fwlink/p/?linkid=834376).</span><span class="sxs-lookup"><span data-stu-id="97714-105">You can also create and manage container registries using hello [Azure portal](container-registry-get-started-portal.md) or programmatically with hello Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="97714-106">Para o plano de fundo e conceitos, consulte [Olá visão geral](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="97714-106">For background and concepts, see [hello overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="97714-107">Para obter ajuda sobre comandos do contêiner do registro (`az acr` comandos), passar Olá `-h` comando de tooany do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="97714-107">For help on Container Registry CLI commands (`az acr` commands), pass hello `-h` parameter tooany command.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="97714-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="97714-108">Prerequisites</span></span>
* <span data-ttu-id="97714-109">**2.0 do CLI do Azure**: tooinstall e começar com hello CLI 2.0, consulte Olá [instruções de instalação](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="97714-109">**Azure CLI 2.0**: tooinstall and get started with hello CLI 2.0, see hello [installation instructions](/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="97714-110">Faça logon no tooyour assinatura do Azure executando `az login`.</span><span class="sxs-lookup"><span data-stu-id="97714-110">Log in tooyour Azure subscription by running `az login`.</span></span> <span data-ttu-id="97714-111">Para obter mais informações, consulte [começar com hello CLI 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="97714-111">For more information, see [Get started with hello CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>
* <span data-ttu-id="97714-112">**Grupo de recursos**: crie um [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups) antes de criar um registro de contêiner ou usar um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="97714-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="97714-113">Verifique se o grupo de recursos hello está em um local onde está o serviço de registro de contêiner de saudação [disponível](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="97714-113">Make sure hello resource group is in a location where hello Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="97714-114">toocreate um grupo de recursos usando Olá CLI 2.0, consulte [Olá referência CLI 2.0](/cli/azure/group).</span><span class="sxs-lookup"><span data-stu-id="97714-114">toocreate a resource group using hello CLI 2.0, see [hello CLI 2.0 reference](/cli/azure/group).</span></span>
* <span data-ttu-id="97714-115">**Conta de armazenamento** (opcional): criar um padrão Azure [conta de armazenamento](../storage/common/storage-introduction.md) tooback registro de contêiner de saudação em Olá mesmo local.</span><span class="sxs-lookup"><span data-stu-id="97714-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) tooback hello container registry in hello same location.</span></span> <span data-ttu-id="97714-116">Se você não especificar uma conta de armazenamento ao criar um registro com `az acr create`, comando Olá criará um para você.</span><span class="sxs-lookup"><span data-stu-id="97714-116">If you don't specify a storage account when creating a registry with `az acr create`, hello command creates one for you.</span></span> <span data-ttu-id="97714-117">toocreate um armazenamento de conta usando Olá CLI 2.0, consulte [Olá referência CLI 2.0](/cli/azure/storage/account).</span><span class="sxs-lookup"><span data-stu-id="97714-117">toocreate a storage account using hello CLI 2.0, see [hello CLI 2.0 reference](/cli/azure/storage/account).</span></span> <span data-ttu-id="97714-118">Atualmente, não há suporte para o Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="97714-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="97714-119">**Entidade de serviço** (opcional): quando você cria um registro com hello CLI, por padrão ele não é configurado para acesso.</span><span class="sxs-lookup"><span data-stu-id="97714-119">**Service principal** (optional): When you create a registry with hello CLI, by default it is not set up for access.</span></span> <span data-ttu-id="97714-120">Dependendo de suas necessidades, você pode atribuir um registro de tooa principal de serviço existente do Active Directory do Azure (ou criar e atribuir um novo), ou habilite a conta de usuário admin do registro hello.</span><span class="sxs-lookup"><span data-stu-id="97714-120">Depending on your needs, you can assign an existing Azure Active Directory service principal tooa registry (or create and assign a new one), or enable hello registry's admin user account.</span></span> <span data-ttu-id="97714-121">Consulte as seções Olá posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="97714-121">See hello sections later in this article.</span></span> <span data-ttu-id="97714-122">Para obter mais informações sobre o acesso de registro, consulte [autenticar com o registro de contêiner Olá](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="97714-122">For more information about registry access, see [Authenticate with hello container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="97714-123">Criar um registro de contêiner</span><span class="sxs-lookup"><span data-stu-id="97714-123">Create a container registry</span></span>
<span data-ttu-id="97714-124">Executar Olá `az acr create` comando toocreate um registro de contêiner.</span><span class="sxs-lookup"><span data-stu-id="97714-124">Run hello `az acr create` command toocreate a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="97714-125">Ao criar um registro, especifique um nome de domínio de nível superior exclusivo que contenha apenas letras e números.</span><span class="sxs-lookup"><span data-stu-id="97714-125">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="97714-126">nome do registro de saudação nos exemplos de saudação é `myRegistry1`, mas substitua um nome exclusivo.</span><span class="sxs-lookup"><span data-stu-id="97714-126">hello registry name in hello examples is `myRegistry1`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="97714-127">Olá usa Olá registro de contêiner toocreate mínimo de parâmetros de comando a seguir `myRegistry1` no grupo de recursos de saudação `myResourceGroup`e usando Olá *básica* sku:</span><span class="sxs-lookup"><span data-stu-id="97714-127">hello following command uses hello minimal parameters toocreate container registry `myRegistry1` in hello resource group `myResourceGroup`, and using hello *Basic* sku:</span></span>

```azurecli
az acr create --name myRegistry1 --resource-group myResourceGroup --sku Basic
```

* <span data-ttu-id="97714-128">`--storage-account-name` é opcional.</span><span class="sxs-lookup"><span data-stu-id="97714-128">`--storage-account-name` is optional.</span></span> <span data-ttu-id="97714-129">Se não for especificado, uma conta de armazenamento é criada com um nome que consiste do nome do registro de saudação e um carimbo de hora Olá especificado o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="97714-129">If not specified, a storage account is created with a name consisting of hello registry name and a timestamp in hello specified resource group.</span></span>

<span data-ttu-id="97714-130">Quando Olá registro é criado, a saída de hello é a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="97714-130">When hello registry is created, hello output is similar toohello following:</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T18:36:29.124842+00:00",
  "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry
/registries/myRegistry1",
  "location": "southcentralus",
  "loginServer": "myregistry1.azurecr.io",
  "name": "myRegistry1",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "myregistry123456789"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}

```


<span data-ttu-id="97714-131">Observe particularmente:</span><span class="sxs-lookup"><span data-stu-id="97714-131">Take special note:</span></span>

* <span data-ttu-id="97714-132">`id`-Identificador para registro de saudação em sua assinatura, que é necessário se você quiser tooassign uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="97714-132">`id` - Identifier for hello registry in your subscription, which you need if you want tooassign a service principal.</span></span>
* <span data-ttu-id="97714-133">`loginServer`-nome totalmente qualificado de saudação especificado muito[toohello registro de log](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="97714-133">`loginServer` - hello fully qualified name you specify too[log in toohello registry](container-registry-authentication.md).</span></span> <span data-ttu-id="97714-134">Neste exemplo, o nome de saudação é `myregistry1.exp.azurecr.io` (todas as minúsculas).</span><span class="sxs-lookup"><span data-stu-id="97714-134">In this example, hello name is `myregistry1.exp.azurecr.io` (all lowercase).</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="97714-135">Atribuir uma entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="97714-135">Assign a service principal</span></span>
<span data-ttu-id="97714-136">Use comandos de CLI 2.0 tooassign um registro de tooa principal de serviço do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="97714-136">Use CLI 2.0 commands tooassign an Azure Active Directory service principal tooa registry.</span></span> <span data-ttu-id="97714-137">Hello entidade de serviço nesses exemplos é designada como Olá proprietário, mas você pode atribuir [outras funções](../active-directory/role-based-access-control-configure.md) se desejar.</span><span class="sxs-lookup"><span data-stu-id="97714-137">hello service principal in these examples is assigned hello Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal-and-assign-access-toohello-registry"></a><span data-ttu-id="97714-138">Criar uma entidade de serviço e atribuir toohello acessar o registro</span><span class="sxs-lookup"><span data-stu-id="97714-138">Create a service principal and assign access toohello registry</span></span>
<span data-ttu-id="97714-139">Olá comando a seguir, uma nova entidade de serviço é atribuída identificador de registro de toohello do proprietário função acesso passado com hello `--scopes` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="97714-139">In hello following command, a new service principal is assigned Owner role access toohello registry identifier passed with hello `--scopes` parameter.</span></span> <span data-ttu-id="97714-140">Especifique uma senha forte com hello `--password` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="97714-140">Specify a strong password with hello `--password` parameter.</span></span>

```azurecli
az ad sp create-for-rbac --scopes /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --password myPassword
```



### <a name="assign-an-existing-service-principal"></a><span data-ttu-id="97714-141">Atribuir uma entidade de serviço existente</span><span class="sxs-lookup"><span data-stu-id="97714-141">Assign an existing service principal</span></span>
<span data-ttu-id="97714-142">Se você já tiver uma entidade de serviço e deseja tooassign-proprietário função acessar toohello o registro, execute um toohello semelhante do comando exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="97714-142">If you already have a service principal and want tooassign it Owner role access toohello registry, run a command similar toohello following example.</span></span> <span data-ttu-id="97714-143">Passar o ID do aplicativo principal de serviço hello usando Olá `--assignee` parâmetro:</span><span class="sxs-lookup"><span data-stu-id="97714-143">You pass hello service principal app ID using hello `--assignee` parameter:</span></span>

```azurecli
az role assignment create --scope /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --assignee myAppId
```



## <a name="manage-admin-credentials"></a><span data-ttu-id="97714-144">Gerenciar credenciais de administrador</span><span class="sxs-lookup"><span data-stu-id="97714-144">Manage admin credentials</span></span>
<span data-ttu-id="97714-145">Uma conta de administrador é automaticamente criada para cada registro de contêiner e é desabilitada por padrão.</span><span class="sxs-lookup"><span data-stu-id="97714-145">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="97714-146">Olá a seguir mostram exemplos `az acr` CLI comandos toomanage credenciais de administrador Olá para o registro de contêiner.</span><span class="sxs-lookup"><span data-stu-id="97714-146">hello following examples show `az acr` CLI commands toomanage hello admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="97714-147">Obter credenciais de usuário administrador</span><span class="sxs-lookup"><span data-stu-id="97714-147">Obtain admin user credentials</span></span>
```azurecli
az acr credential show -n myRegistry1
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="97714-148">Habilitar o usuário administrador para um registro existente</span><span class="sxs-lookup"><span data-stu-id="97714-148">Enable admin user for an existing registry</span></span>
```azurecli
az acr update -n myRegistry1 --admin-enabled true
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="97714-149">Desabilitar o usuário administrador para um registro existente</span><span class="sxs-lookup"><span data-stu-id="97714-149">Disable admin user for an existing registry</span></span>
```azurecli
az acr update -n myRegistry1 --admin-enabled false
```

## <a name="list-images-and-tags"></a><span data-ttu-id="97714-150">Listar imagens e marcas</span><span class="sxs-lookup"><span data-stu-id="97714-150">List images and tags</span></span>
<span data-ttu-id="97714-151">Saudação de uso `az acr` CLI comandos de imagens de saudação tooquery marcas em um repositório.</span><span class="sxs-lookup"><span data-stu-id="97714-151">Use hello `az acr` CLI commands tooquery hello images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="97714-152">Atualmente, registro de contêiner não dá suporte a saudação `docker search` tooquery de comando para imagens e marcas.</span><span class="sxs-lookup"><span data-stu-id="97714-152">Currently, Container Registry does not support hello `docker search` command tooquery for images and tags.</span></span>


### <a name="list-repositories"></a><span data-ttu-id="97714-153">Listar repositórios</span><span class="sxs-lookup"><span data-stu-id="97714-153">List repositories</span></span>
<span data-ttu-id="97714-154">Olá, exemplo a seguir lista os repositórios de saudação em um registro, no formato JSON (JavaScript Object Notation):</span><span class="sxs-lookup"><span data-stu-id="97714-154">hello following example lists hello repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="97714-155">Listar marcas</span><span class="sxs-lookup"><span data-stu-id="97714-155">List tags</span></span>
<span data-ttu-id="97714-156">Olá, exemplo a seguir lista as marcas de Olá Olá **exemplos/nginx** repositório, no formato JSON:</span><span class="sxs-lookup"><span data-stu-id="97714-156">hello following example lists hello tags on hello **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="97714-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="97714-157">Next steps</span></span>
* [<span data-ttu-id="97714-158">Enviar por push sua primeira imagem usando Olá CLI do Docker</span><span class="sxs-lookup"><span data-stu-id="97714-158">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
