---
title: "Repositórios de Registro de contêiner do Azure | Microsoft Docs"
description: "Como usar os repositórios de Registro de contêiner do Azure para imagens do Docker"
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
ms.openlocfilehash: 1e5d5ea5b1ec121fe008abc48178b1d58f540ce1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-private-docker-container-registry-using-the-azure-powershell"></a><span data-ttu-id="2a756-103">Criar um registro de contêiner privado do Docker usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2a756-103">Create a private Docker container registry using the Azure PowerShell</span></span>
<span data-ttu-id="2a756-104">Use comandos no [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) para criar um registro de contêiner e gerenciar suas configurações de seu computador com Windows.</span><span class="sxs-lookup"><span data-stu-id="2a756-104">Use commands in [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) to create a container registry and manage its settings from your Windows computer.</span></span> <span data-ttu-id="2a756-105">Você também pode criar e gerenciar registros de contêiner usando o [portal do Azure](container-registry-get-started-portal.md), a [CLI do Azure](container-registry-get-started-azure-cli.md) ou por meio de programação com a [API REST](https://go.microsoft.com/fwlink/p/?linkid=834376) do Registro de Contêiner.</span><span class="sxs-lookup"><span data-stu-id="2a756-105">You can also create and manage container registries using the [Azure portal](container-registry-get-started-portal.md), the [Azure CLI](container-registry-get-started-azure-cli.md), or programmatically with the Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="2a756-106">Para obter mais informações e conceitos, confira a [visão geral](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="2a756-106">For background and concepts, see [the overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="2a756-107">Para obter uma lista completa dos cmdlets com suporte, consulte [Cmdlets de gerenciamento do Registro de Contêiner do Azure](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span><span class="sxs-lookup"><span data-stu-id="2a756-107">For a full list of supported cmdlets, see [Azure Container Registry Management Cmdlets](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="2a756-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2a756-108">Prerequisites</span></span>
* <span data-ttu-id="2a756-109">**Azure PowerShell**: para instalar e começar a usar o Azure PowerShell, consulte as [instruções de instalação](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="2a756-109">**Azure PowerShell**: To install and get started with Azure PowerShell, see the [installation instructions](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="2a756-110">Faça logon em sua assinatura do Azure executando `Login-AzureRMAccount`.</span><span class="sxs-lookup"><span data-stu-id="2a756-110">Log in to your Azure subscription by running `Login-AzureRMAccount`.</span></span> <span data-ttu-id="2a756-111">Para obter mais informações, consulte [Introdução ao Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span><span class="sxs-lookup"><span data-stu-id="2a756-111">For more information, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span></span>
* <span data-ttu-id="2a756-112">**Grupo de recursos**: crie um [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups) antes de criar um registro de contêiner ou usar um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="2a756-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="2a756-113">Verifique se o grupo de recursos está em um local em que o serviço de Registro de Contêiner está [disponível](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="2a756-113">Make sure the resource group is in a location where the Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="2a756-114">Para criar um grupo de recursos usando o Azure PowerShell, consulte [Referência do PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span><span class="sxs-lookup"><span data-stu-id="2a756-114">To create a resource group using Azure PowerShell, see [the PowerShell reference](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span></span>
* <span data-ttu-id="2a756-115">**Conta de armazenamento** (opcional): cria uma [conta de armazenamento](../storage/common/storage-introduction.md) padrão do Azure para dar suporte ao registro de contêiner no mesmo local.</span><span class="sxs-lookup"><span data-stu-id="2a756-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) to back the container registry in the same location.</span></span> <span data-ttu-id="2a756-116">Se você não especificar uma conta de armazenamento ao criar um registro com `New-AzureRMContainerRegistry`, o comando criará um para você.</span><span class="sxs-lookup"><span data-stu-id="2a756-116">If you don't specify a storage account when creating a registry with `New-AzureRMContainerRegistry`, the command creates one for you.</span></span> <span data-ttu-id="2a756-117">Para criar uma conta de armazenamento usando o PowerShell, consulte [Referência do PowerShell](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span><span class="sxs-lookup"><span data-stu-id="2a756-117">To create a storage account using PowerShell, see [the PowerShell reference](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span></span> <span data-ttu-id="2a756-118">Atualmente, não há suporte para o Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="2a756-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="2a756-119">**Entidade de serviço** (opcional): quando você cria um registro com o PowerShell, por padrão, ele não é configurado para acesso.</span><span class="sxs-lookup"><span data-stu-id="2a756-119">**Service principal** (optional): When you create a registry with PowerShell, by default it is not set up for access.</span></span> <span data-ttu-id="2a756-120">Dependendo das suas necessidades, você pode atribuir uma entidade de serviço do Azure Active Directory existente a um registro ou criar e atribuir uma nova.</span><span class="sxs-lookup"><span data-stu-id="2a756-120">Depending on your needs, you can assign an existing Azure Active Directory service principal to a registry or create and assign a new one.</span></span> <span data-ttu-id="2a756-121">Como alternativa, você pode habilitar a conta de usuário administrador do registro.</span><span class="sxs-lookup"><span data-stu-id="2a756-121">Alternatively, you can enable the registry's admin user account.</span></span> <span data-ttu-id="2a756-122">Confira as seções mais adiante neste artigo.</span><span class="sxs-lookup"><span data-stu-id="2a756-122">See the sections later in this article.</span></span> <span data-ttu-id="2a756-123">Para obter mais informações sobre o acesso ao registro, confira [Autenticar no registro de contêiner](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="2a756-123">For more information about registry access, see [Authenticate with the container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="2a756-124">Criar um registro de contêiner</span><span class="sxs-lookup"><span data-stu-id="2a756-124">Create a container registry</span></span>
<span data-ttu-id="2a756-125">Execute o comando `New-AzureRMContainerRegistry` para criar um registro de contêiner.</span><span class="sxs-lookup"><span data-stu-id="2a756-125">Run the `New-AzureRMContainerRegistry` command to create a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="2a756-126">Ao criar um registro, especifique um nome de domínio de nível superior exclusivo que contenha apenas letras e números.</span><span class="sxs-lookup"><span data-stu-id="2a756-126">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="2a756-127">O nome do registro nos exemplos é `MyRegistry`, mas substitua-o por um nome exclusivo.</span><span class="sxs-lookup"><span data-stu-id="2a756-127">The registry name in the examples is `MyRegistry`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="2a756-128">O seguinte comando usa os parâmetros mínimos para criar o registro de contêiner `MyRegistry` no grupo de recursos `MyResourceGroup` no local Centro-Sul dos EUA:</span><span class="sxs-lookup"><span data-stu-id="2a756-128">The following command uses the minimal parameters to create container registry `MyRegistry` in the resource group `MyResourceGroup` in the South Central US location:</span></span>

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* <span data-ttu-id="2a756-129">`-StorageAccountName` é opcional.</span><span class="sxs-lookup"><span data-stu-id="2a756-129">`-StorageAccountName` is optional.</span></span> <span data-ttu-id="2a756-130">Se não for especificada, uma conta de armazenamento será criada com um nome que consiste no nome do registro e em um carimbo de data e hora no grupo de recursos especificado.</span><span class="sxs-lookup"><span data-stu-id="2a756-130">If not specified, a storage account is created with a name consisting of the registry name and a timestamp in the specified resource group.</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="2a756-131">Atribuir uma entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="2a756-131">Assign a service principal</span></span>
<span data-ttu-id="2a756-132">Use comandos do PowerShell para atribuir uma [entidade de serviço](../azure-resource-manager/resource-group-authenticate-service-principal.md) do Azure Active Directory a um registro.</span><span class="sxs-lookup"><span data-stu-id="2a756-132">Use PowerShell commands to assign an Azure Active Directory [service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md) to a registry.</span></span> <span data-ttu-id="2a756-133">A entidade de serviço nesses exemplos é atribuída à função de Proprietário, mas você poderá atribuir [outras funções](../active-directory/role-based-access-control-configure.md), se desejar.</span><span class="sxs-lookup"><span data-stu-id="2a756-133">The service principal in these examples is assigned the Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal"></a><span data-ttu-id="2a756-134">Criar uma entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="2a756-134">Create a service principal</span></span>
<span data-ttu-id="2a756-135">No comando a seguir, uma nova entidade de serviço é criada.</span><span class="sxs-lookup"><span data-stu-id="2a756-135">In the following command, a new service principal is created.</span></span> <span data-ttu-id="2a756-136">Especifique uma senha forte com o parâmetro `-Password`.</span><span class="sxs-lookup"><span data-stu-id="2a756-136">Specify a strong password with the `-Password` parameter.</span></span>

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a><span data-ttu-id="2a756-137">Atribuir uma entidade de serviço nova ou existente</span><span class="sxs-lookup"><span data-stu-id="2a756-137">Assign a new or existing service principal</span></span>
<span data-ttu-id="2a756-138">Você pode atribuir uma entidade de serviço nova ou existente a um registro.</span><span class="sxs-lookup"><span data-stu-id="2a756-138">You can assign a new or an existing service principal to a registry.</span></span> <span data-ttu-id="2a756-139">Para atribuir acesso de função de Proprietário ao Registro, execute um comando semelhante ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="2a756-139">To assign it Owner role access to the registry, run a command similar to the following example:</span></span>

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-to-the-registry-with-the-service-principal"></a><span data-ttu-id="2a756-140">Entrar no registro com a entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="2a756-140">Sign in to the registry with the service principal</span></span>
<span data-ttu-id="2a756-141">Depois de atribuir a entidade de serviço ao registro, você pode entrar usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="2a756-141">After assigning the service principal to the registry, you can sign in using the following command:</span></span>

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a><span data-ttu-id="2a756-142">Gerenciar credenciais de administrador</span><span class="sxs-lookup"><span data-stu-id="2a756-142">Manage admin credentials</span></span>
<span data-ttu-id="2a756-143">Uma conta de administrador é automaticamente criada para cada registro de contêiner e é desabilitada por padrão.</span><span class="sxs-lookup"><span data-stu-id="2a756-143">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="2a756-144">Os exemplos a seguir mostram comandos do PowerShell para gerenciar as credenciais de administrador para seu registro de contêiner.</span><span class="sxs-lookup"><span data-stu-id="2a756-144">The following examples show PowerShell commands to manage the admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="2a756-145">Obter credenciais de usuário administrador</span><span class="sxs-lookup"><span data-stu-id="2a756-145">Obtain admin user credentials</span></span>
```PowerShell
Get-AzureRMContainerRegistryCredential -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="2a756-146">Habilitar o usuário administrador para um registro existente</span><span class="sxs-lookup"><span data-stu-id="2a756-146">Enable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -EnableAdminUser
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="2a756-147">Desabilitar o usuário administrador para um registro existente</span><span class="sxs-lookup"><span data-stu-id="2a756-147">Disable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -DisableAdminUser
```

## <a name="next-steps"></a><span data-ttu-id="2a756-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2a756-148">Next steps</span></span>
* [<span data-ttu-id="2a756-149">Enviar por push sua primeira imagem usando a CLI do Docker</span><span class="sxs-lookup"><span data-stu-id="2a756-149">Push your first image using the Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
