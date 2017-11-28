---
title: "repositórios de registro de contêiner aaaAzure | Microsoft Docs"
description: "Como repositórios de registro de contêiner do Azure toouse para imagens do Docker"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: cristyg
ms.openlocfilehash: 448fb812f537c9502041ce5fb372b0681a9dac4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-powershell"></a><span data-ttu-id="d6915-103">Criar um registro de contêiner do Docker privado usando hello Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d6915-103">Create a private Docker container registry using hello Azure PowerShell</span></span>
<span data-ttu-id="d6915-104">Usar comandos em [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) toocreate um registro de contêiner e gerenciar suas configurações de seu computador com Windows.</span><span class="sxs-lookup"><span data-stu-id="d6915-104">Use commands in [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) toocreate a container registry and manage its settings from your Windows computer.</span></span> <span data-ttu-id="d6915-105">Você também pode criar e gerenciar registros de contêiner usando Olá [portal do Azure](container-registry-get-started-portal.md), Olá [CLI do Azure](container-registry-get-started-azure-cli.md), ou programaticamente com hello registro de contêiner [API REST](https://go.microsoft.com/fwlink/p/?linkid=834376).</span><span class="sxs-lookup"><span data-stu-id="d6915-105">You can also create and manage container registries using hello [Azure portal](container-registry-get-started-portal.md), hello [Azure CLI](container-registry-get-started-azure-cli.md), or programmatically with hello Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="d6915-106">Para o plano de fundo e conceitos, consulte [Olá visão geral](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="d6915-106">For background and concepts, see [hello overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="d6915-107">Para obter uma lista completa dos cmdlets com suporte, consulte [Cmdlets de gerenciamento do Registro de Contêiner do Azure](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span><span class="sxs-lookup"><span data-stu-id="d6915-107">For a full list of supported cmdlets, see [Azure Container Registry Management Cmdlets](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="d6915-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d6915-108">Prerequisites</span></span>
* <span data-ttu-id="d6915-109">**O Azure PowerShell**: tooinstall e começar com o Azure PowerShell, consulte Olá [instruções de instalação](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="d6915-109">**Azure PowerShell**: tooinstall and get started with Azure PowerShell, see hello [installation instructions](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="d6915-110">Faça logon no tooyour assinatura do Azure executando `Login-AzureRMAccount`.</span><span class="sxs-lookup"><span data-stu-id="d6915-110">Log in tooyour Azure subscription by running `Login-AzureRMAccount`.</span></span> <span data-ttu-id="d6915-111">Para obter mais informações, consulte [Introdução ao Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span><span class="sxs-lookup"><span data-stu-id="d6915-111">For more information, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span></span>
* <span data-ttu-id="d6915-112">**Grupo de recursos**: crie um [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups) antes de criar um registro de contêiner ou usar um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="d6915-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="d6915-113">Verifique se o grupo de recursos hello está em um local onde está o serviço de registro de contêiner de saudação [disponível](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="d6915-113">Make sure hello resource group is in a location where hello Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="d6915-114">toocreate um grupo de recursos usando o PowerShell do Azure, consulte [Olá referência do PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span><span class="sxs-lookup"><span data-stu-id="d6915-114">toocreate a resource group using Azure PowerShell, see [hello PowerShell reference](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span></span>
* <span data-ttu-id="d6915-115">**Conta de armazenamento** (opcional): criar um padrão Azure [conta de armazenamento](../storage/common/storage-introduction.md) tooback registro de contêiner de saudação em Olá mesmo local.</span><span class="sxs-lookup"><span data-stu-id="d6915-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) tooback hello container registry in hello same location.</span></span> <span data-ttu-id="d6915-116">Se você não especificar uma conta de armazenamento ao criar um registro com `New-AzureRMContainerRegistry`, comando Olá criará um para você.</span><span class="sxs-lookup"><span data-stu-id="d6915-116">If you don't specify a storage account when creating a registry with `New-AzureRMContainerRegistry`, hello command creates one for you.</span></span> <span data-ttu-id="d6915-117">toocreate um armazenamento de conta usando o PowerShell, consulte [Olá referência do PowerShell](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span><span class="sxs-lookup"><span data-stu-id="d6915-117">toocreate a storage account using PowerShell, see [hello PowerShell reference](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span></span> <span data-ttu-id="d6915-118">Atualmente, não há suporte para o Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="d6915-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="d6915-119">**Entidade de serviço** (opcional): quando você cria um registro com o PowerShell, por padrão, ele não é configurado para acesso.</span><span class="sxs-lookup"><span data-stu-id="d6915-119">**Service principal** (optional): When you create a registry with PowerShell, by default it is not set up for access.</span></span> <span data-ttu-id="d6915-120">Dependendo de suas necessidades, você pode atribuir um registro de tooa principal de serviço existente do Active Directory do Azure ou criar e atribuir um novo.</span><span class="sxs-lookup"><span data-stu-id="d6915-120">Depending on your needs, you can assign an existing Azure Active Directory service principal tooa registry or create and assign a new one.</span></span> <span data-ttu-id="d6915-121">Como alternativa, você pode habilitar a conta de usuário admin do registro hello.</span><span class="sxs-lookup"><span data-stu-id="d6915-121">Alternatively, you can enable hello registry's admin user account.</span></span> <span data-ttu-id="d6915-122">Consulte as seções Olá posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="d6915-122">See hello sections later in this article.</span></span> <span data-ttu-id="d6915-123">Para obter mais informações sobre o acesso de registro, consulte [autenticar com o registro de contêiner Olá](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d6915-123">For more information about registry access, see [Authenticate with hello container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="d6915-124">Criar um registro de contêiner</span><span class="sxs-lookup"><span data-stu-id="d6915-124">Create a container registry</span></span>
<span data-ttu-id="d6915-125">Executar Olá `New-AzureRMContainerRegistry` comando toocreate um registro de contêiner.</span><span class="sxs-lookup"><span data-stu-id="d6915-125">Run hello `New-AzureRMContainerRegistry` command toocreate a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="d6915-126">Ao criar um registro, especifique um nome de domínio de nível superior exclusivo que contenha apenas letras e números.</span><span class="sxs-lookup"><span data-stu-id="d6915-126">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="d6915-127">nome do registro de saudação nos exemplos de saudação é `MyRegistry`, mas substitua um nome exclusivo.</span><span class="sxs-lookup"><span data-stu-id="d6915-127">hello registry name in hello examples is `MyRegistry`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="d6915-128">Olá usa Olá registro de contêiner toocreate mínimo de parâmetros de comando a seguir `MyRegistry` no grupo de recursos de saudação `MyResourceGroup` em Olá Centro Sul dos EUA local:</span><span class="sxs-lookup"><span data-stu-id="d6915-128">hello following command uses hello minimal parameters toocreate container registry `MyRegistry` in hello resource group `MyResourceGroup` in hello South Central US location:</span></span>

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* <span data-ttu-id="d6915-129">`-StorageAccountName` é opcional.</span><span class="sxs-lookup"><span data-stu-id="d6915-129">`-StorageAccountName` is optional.</span></span> <span data-ttu-id="d6915-130">Se não for especificado, uma conta de armazenamento é criada com um nome que consiste do nome do registro de saudação e um carimbo de hora Olá especificado o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d6915-130">If not specified, a storage account is created with a name consisting of hello registry name and a timestamp in hello specified resource group.</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="d6915-131">Atribuir uma entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="d6915-131">Assign a service principal</span></span>
<span data-ttu-id="d6915-132">Usar comandos de PowerShell tooassign um Azure Active Directory [entidade de serviço](../azure-resource-manager/resource-group-authenticate-service-principal.md) tooa registro.</span><span class="sxs-lookup"><span data-stu-id="d6915-132">Use PowerShell commands tooassign an Azure Active Directory [service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md) tooa registry.</span></span> <span data-ttu-id="d6915-133">Hello entidade de serviço nesses exemplos é designada como Olá proprietário, mas você pode atribuir [outras funções](../active-directory/role-based-access-control-configure.md) se desejar.</span><span class="sxs-lookup"><span data-stu-id="d6915-133">hello service principal in these examples is assigned hello Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal"></a><span data-ttu-id="d6915-134">Criar uma entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="d6915-134">Create a service principal</span></span>
<span data-ttu-id="d6915-135">Olá comando a seguir, uma nova entidade de serviço é criada.</span><span class="sxs-lookup"><span data-stu-id="d6915-135">In hello following command, a new service principal is created.</span></span> <span data-ttu-id="d6915-136">Especifique uma senha forte com hello `-Password` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="d6915-136">Specify a strong password with hello `-Password` parameter.</span></span>

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a><span data-ttu-id="d6915-137">Atribuir uma entidade de serviço nova ou existente</span><span class="sxs-lookup"><span data-stu-id="d6915-137">Assign a new or existing service principal</span></span>
<span data-ttu-id="d6915-138">Você pode atribuir um novo ou um registro de tooa principal de serviço existente.</span><span class="sxs-lookup"><span data-stu-id="d6915-138">You can assign a new or an existing service principal tooa registry.</span></span> <span data-ttu-id="d6915-139">tooassign-proprietário função acessar toohello o registro, execute um toohello semelhante do comando exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="d6915-139">tooassign it Owner role access toohello registry, run a command similar toohello following example:</span></span>

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-toohello-registry-with-hello-service-principal"></a><span data-ttu-id="d6915-140">Entrar no registro toohello com a entidade de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="d6915-140">Sign in toohello registry with hello service principal</span></span>
<span data-ttu-id="d6915-141">Depois de atribuir o registro de toohello principal do serviço hello, você pode entrar usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="d6915-141">After assigning hello service principal toohello registry, you can sign in using hello following command:</span></span>

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a><span data-ttu-id="d6915-142">Gerenciar credenciais de administrador</span><span class="sxs-lookup"><span data-stu-id="d6915-142">Manage admin credentials</span></span>
<span data-ttu-id="d6915-143">Uma conta de administrador é automaticamente criada para cada registro de contêiner e é desabilitada por padrão.</span><span class="sxs-lookup"><span data-stu-id="d6915-143">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="d6915-144">Olá exemplos a seguir mostram comandos do PowerShell credenciais de administrador toomanage Olá para o registro de contêiner.</span><span class="sxs-lookup"><span data-stu-id="d6915-144">hello following examples show PowerShell commands toomanage hello admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="d6915-145">Obter credenciais de usuário administrador</span><span class="sxs-lookup"><span data-stu-id="d6915-145">Obtain admin user credentials</span></span>
```PowerShell
Get-AzureRMContainerRegistryCredential -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="d6915-146">Habilitar o usuário administrador para um registro existente</span><span class="sxs-lookup"><span data-stu-id="d6915-146">Enable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -EnableAdminUser
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="d6915-147">Desabilitar o usuário administrador para um registro existente</span><span class="sxs-lookup"><span data-stu-id="d6915-147">Disable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -DisableAdminUser
```

## <a name="next-steps"></a><span data-ttu-id="d6915-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d6915-148">Next steps</span></span>
* [<span data-ttu-id="d6915-149">Enviar por push sua primeira imagem usando Olá CLI do Docker</span><span class="sxs-lookup"><span data-stu-id="d6915-149">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
