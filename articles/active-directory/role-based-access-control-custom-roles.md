---
title: "aaaCreate de funções personalizadas para o RBAC do Azure | Microsoft Docs"
description: "Saiba como toodefine funções personalizadas com o controle de acesso para o gerenciamento de identidade mais preciso em sua assinatura do Azure."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: e4206ea9-52c3-47ee-af29-f6eef7566fa5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/11/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 60df12632ef6c086d5feeb1809196d7c4ee5e021
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-roles-for-azure-role-based-access-control"></a><span data-ttu-id="9d6f4-103">Criar funções personalizadas para o Controle de Acesso Baseado em Função do Azure</span><span class="sxs-lookup"><span data-stu-id="9d6f4-103">Create custom roles for Azure Role-Based Access Control</span></span>
<span data-ttu-id="9d6f4-104">Crie uma função personalizada no acesso de RBAC (controle) se nenhuma das funções internas Olá atender às suas necessidades de acesso específicas.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-104">Create a custom role in Azure Role-Based Access Control (RBAC) if none of hello built-in roles meet your specific access needs.</span></span> <span data-ttu-id="9d6f4-105">Funções personalizadas podem ser criadas usando [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [Interface de linha de comando do Azure](role-based-access-control-manage-access-azure-cli.md) (CLI) e hello [API REST](role-based-access-control-manage-access-rest.md).</span><span class="sxs-lookup"><span data-stu-id="9d6f4-105">Custom roles can be created using [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface](role-based-access-control-manage-access-azure-cli.md) (CLI), and hello [REST API](role-based-access-control-manage-access-rest.md).</span></span> <span data-ttu-id="9d6f4-106">Assim como funções internas, você pode atribuir funções personalizadas toousers, grupos e aplicativos na assinatura, no grupo de recursos e escopos do recurso.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-106">Just like built-in roles, you can assign custom roles toousers, groups, and applications at subscription, resource group, and resource scopes.</span></span> <span data-ttu-id="9d6f4-107">As funções personalizadas são armazenadas em um locatário do Azure AD e podem ser compartilhadas entre assinaturas.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-107">Custom roles are stored in an Azure AD tenant and can be shared across subscriptions.</span></span>

<span data-ttu-id="9d6f4-108">Cada locatário pode criar funções personalizadas too2000.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-108">Each tenant can create up too2000 custom roles.</span></span> 

<span data-ttu-id="9d6f4-109">Olá, exemplo a seguir mostra uma função personalizada para monitoramento e reiniciar as máquinas virtuais:</span><span class="sxs-lookup"><span data-stu-id="9d6f4-109">hello following example shows a custom role for monitoring and restarting virtual machines:</span></span>

```
{
  "Name": "Virtual Machine Operator",
  "Id": "cadb4a5a-4e7a-47be-84db-05cad13b6769",
  "IsCustom": true,
  "Description": "Can monitor and restart virtual machines.",
  "Actions": [
    "Microsoft.Storage/*/read",
    "Microsoft.Network/*/read",
    "Microsoft.Compute/*/read",
    "Microsoft.Compute/virtualMachines/start/action",
    "Microsoft.Compute/virtualMachines/restart/action",
    "Microsoft.Authorization/*/read",
    "Microsoft.Resources/subscriptions/resourceGroups/read",
    "Microsoft.Insights/alertRules/*",
    "Microsoft.Insights/diagnosticSettings/*",
    "Microsoft.Support/*"
  ],
  "NotActions": [

  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624",
    "/subscriptions/34370e90-ac4a-4bf9-821f-85eeedeae1a2"
  ]
}
```
## <a name="actions"></a><span data-ttu-id="9d6f4-110">Ações</span><span class="sxs-lookup"><span data-stu-id="9d6f4-110">Actions</span></span>
<span data-ttu-id="9d6f4-111">Olá **ações** propriedade de uma função personalizada especifica hello Azure operações toowhich Olá função concede acesso.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-111">hello **Actions** property of a custom role specifies hello Azure operations toowhich hello role grants access.</span></span> <span data-ttu-id="9d6f4-112">É uma coleção de cadeias de operação que identificam as operações protegíveis dos provedores de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-112">It is a collection of operation strings that identify securable operations of Azure resource providers.</span></span> <span data-ttu-id="9d6f4-113">Cadeias de caracteres de operação seguem o formato de saudação do `Microsoft.<ProviderName>/<ChildResourceType>/<action>`.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-113">Operation strings follow hello format of `Microsoft.<ProviderName>/<ChildResourceType>/<action>`.</span></span> <span data-ttu-id="9d6f4-114">Cadeias de caracteres de operação que contêm caracteres curinga (\*) conceder acesso a operações tooall que correspondem a cadeia de caracteres de operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-114">Operation strings that contain wildcards (\*) grant access tooall operations that match hello operation string.</span></span> <span data-ttu-id="9d6f4-115">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9d6f4-115">For instance:</span></span>

* <span data-ttu-id="9d6f4-116">`*/read`concede acesso a operações tooread para todos os tipos de recursos de todos os provedores de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-116">`*/read` grants access tooread operations for all resource types of all Azure resource providers.</span></span>
* <span data-ttu-id="9d6f4-117">`Microsoft.Compute/*`concede acesso a operações de tooall para todos os tipos de recursos no provedor de recursos Microsoft. Compute hello.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-117">`Microsoft.Compute/*` grants access tooall operations for all resource types in hello Microsoft.Compute resource provider.</span></span>
* <span data-ttu-id="9d6f4-118">`Microsoft.Network/*/read`concede acesso a operações de tooread para todos os tipos de recursos no provedor de recursos Microsoft. Network saudação do Azure.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-118">`Microsoft.Network/*/read` grants access tooread operations for all resource types in hello Microsoft.Network resource provider of Azure.</span></span>
* <span data-ttu-id="9d6f4-119">`Microsoft.Compute/virtualMachines/*`concede acesso tooall operações de máquinas virtuais e seus tipos de recursos filho.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-119">`Microsoft.Compute/virtualMachines/*` grants access tooall operations of virtual machines and its child resource types.</span></span>
* <span data-ttu-id="9d6f4-120">`Microsoft.Web/sites/restart/Action`concede acesso toorestart sites.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-120">`Microsoft.Web/sites/restart/Action` grants access toorestart websites.</span></span>

<span data-ttu-id="9d6f4-121">Use `Get-AzureRmProviderOperation` (no PowerShell) ou `azure provider operations show` (no Azure CLI) operações toolist de provedores de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-121">Use `Get-AzureRmProviderOperation` (in PowerShell) or `azure provider operations show` (in Azure CLI) toolist operations of Azure resource providers.</span></span> <span data-ttu-id="9d6f4-122">Você também pode usar esses comandos tooverify que uma cadeia de caracteres de operação é válida e cadeias de caracteres de operação de curinga tooexpand.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-122">You may also use these commands tooverify that an operation string is valid, and tooexpand wildcard operation strings.</span></span>

```
Get-AzureRMProviderOperation Microsoft.Compute/virtualMachines/*/action | FT Operation, OperationName

Get-AzureRMProviderOperation Microsoft.Network/*
```

![PowerShell screenshot - Get-AzureRMProviderOperation](./media/role-based-access-control-configure/1-get-azurermprovideroperation-1.png)

```
azure provider operations show "Microsoft.Compute/virtualMachines/*/action" --js on | jq '.[] | .operation'

azure provider operations show "Microsoft.Network/*"
```

![<span data-ttu-id="9d6f4-124">Captura de tela da CLI do Azure – as operações do provedor do Azure mostram "Microsoft.Compute/virtualMachines/\*/action"</span><span class="sxs-lookup"><span data-stu-id="9d6f4-124">Azure CLI screenshot - azure provider operations show "Microsoft.Compute/virtualMachines/\*/action"</span></span> ](./media/role-based-access-control-configure/1-azure-provider-operations-show.png)

## <a name="notactions"></a><span data-ttu-id="9d6f4-125">NotActions</span><span class="sxs-lookup"><span data-stu-id="9d6f4-125">NotActions</span></span>
<span data-ttu-id="9d6f4-126">Saudação de uso **NotActions** propriedade se o conjunto de saudação de operações que você deseja tooallow é definido mais facilmente excluindo operações restritas.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-126">Use hello **NotActions** property if hello set of operations that you wish tooallow is more easily defined by excluding restricted operations.</span></span> <span data-ttu-id="9d6f4-127">Olá acesso concedido por uma função personalizada é calculado pela subtração Olá **NotActions** operações de saudação **ações** operações.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-127">hello access granted by a custom role is computed by subtracting hello **NotActions** operations from hello **Actions** operations.</span></span>

> [!NOTE]
> <span data-ttu-id="9d6f4-128">Se um usuário é atribuído a uma função que exclui uma operação em **NotActions**e é atribuído a uma segunda função que concede acesso toohello mesma operação, o usuário Olá é permitido tooperform essa operação.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-128">If a user is assigned a role that excludes an operation in **NotActions**, and is assigned a second role that grants access toohello same operation, hello user is allowed tooperform that operation.</span></span> <span data-ttu-id="9d6f4-129">**NotActions** não é uma negação de regra – é simplesmente uma maneira conveniente de toocreate um conjunto de operações permitidas quando precisam de operações específicas toobe excluído.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-129">**NotActions** is not a deny rule – it is simply a convenient way toocreate a set of allowed operations when specific operations need toobe excluded.</span></span>
>
>

## <a name="assignablescopes"></a><span data-ttu-id="9d6f4-130">AssignableScopes</span><span class="sxs-lookup"><span data-stu-id="9d6f4-130">AssignableScopes</span></span>
<span data-ttu-id="9d6f4-131">Olá **AssignableScopes** propriedade de função personalizada Olá Especifica escopos hello (assinaturas, grupos de recursos ou recursos) no qual Olá função personalizada está disponível para a atribuição.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-131">hello **AssignableScopes** property of hello custom role specifies hello scopes (subscriptions, resource groups, or resources) within which hello custom role is available for assignment.</span></span> <span data-ttu-id="9d6f4-132">Você pode fazer disponíveis para atribuição de função personalizada Olá em assinaturas de saudação apenas ou grupos de recursos que exigem e não o usuário desordem experiência para o restante de saudação de assinaturas de saudação ou grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-132">You can make hello custom role available for assignment in only hello subscriptions or resource groups that require it, and not clutter user experience for hello rest of hello subscriptions or resource groups.</span></span>

<span data-ttu-id="9d6f4-133">Exemplos de escopos válidos que podem ser atribuídos incluem:</span><span class="sxs-lookup"><span data-stu-id="9d6f4-133">Examples of valid assignable scopes include:</span></span>

* <span data-ttu-id="9d6f4-134">"assinaturas/c276fc76-9cd4-44c9-99a7-4fd71546436e", "assinaturas/e91d47c4-76f3-4271-a796-21b4ecfe3624" - torna a função hello disponíveis para atribuição em duas assinaturas.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-134">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e”, “/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624” - makes hello role available for assignment in two subscriptions.</span></span>
* <span data-ttu-id="9d6f4-135">"assinaturas/c276fc76-9cd4-44c9-99a7-4fd71546436e" - torna a função hello disponíveis para atribuição em uma única assinatura.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-135">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e” - makes hello role available for assignment in a single subscription.</span></span>
* <span data-ttu-id="9d6f4-136">"/ assinaturas c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/rede /" - torna Olá função disponível para atribuição apenas no grupo de recursos de rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-136">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network” - makes hello role available for assignment only in hello Network resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="9d6f4-137">Você deve usar pelo menos uma assinatura, grupo de recursos ou ID de recurso.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-137">You must use at least one subscription, resource group, or resource ID.</span></span>
>
>

## <a name="custom-roles-access-control"></a><span data-ttu-id="9d6f4-138">Controle de acesso de funções personalizadas</span><span class="sxs-lookup"><span data-stu-id="9d6f4-138">Custom roles access control</span></span>
<span data-ttu-id="9d6f4-139">Olá **AssignableScopes** propriedade de função personalizada Olá também controla quem pode exibir, modificar e excluir a função hello.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-139">hello **AssignableScopes** property of hello custom role also controls who can view, modify, and delete hello role.</span></span>

* <span data-ttu-id="9d6f4-140">Quem pode criar uma função personalizada?</span><span class="sxs-lookup"><span data-stu-id="9d6f4-140">Who can create a custom role?</span></span>
    <span data-ttu-id="9d6f4-141">Os Proprietários (e os Administradores de acesso do usuário) de assinaturas, grupos de recursos e recursos podem criar funções personalizadas para uso nesses escopos.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-141">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can create custom roles for use in those scopes.</span></span>
    <span data-ttu-id="9d6f4-142">Olá, criar função de saudação do usuário precisa tooperform capaz de toobe `Microsoft.Authorization/roleDefinition/write` operação em todos os Olá **AssignableScopes** da função hello.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-142">hello user creating hello role needs toobe able tooperform `Microsoft.Authorization/roleDefinition/write` operation on all hello **AssignableScopes** of hello role.</span></span>
* <span data-ttu-id="9d6f4-143">Quem pode modificar uma função personalizada?</span><span class="sxs-lookup"><span data-stu-id="9d6f4-143">Who can modify a custom role?</span></span>
    <span data-ttu-id="9d6f4-144">Os Proprietários (e os Administradores de acesso do usuário) de assinaturas, grupos de recursos e recursos podem modificar funções personalizadas nesses escopos.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-144">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can modify custom roles in those scopes.</span></span> <span data-ttu-id="9d6f4-145">Os usuários precisam toobe tooperform capaz de saudação `Microsoft.Authorization/roleDefinition/write` operação em todos os Olá **AssignableScopes** de uma função personalizada.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-145">Users need toobe able tooperform hello `Microsoft.Authorization/roleDefinition/write` operation on all hello **AssignableScopes** of a custom role.</span></span>
* <span data-ttu-id="9d6f4-146">Quem pode exibir funções personalizadas?</span><span class="sxs-lookup"><span data-stu-id="9d6f4-146">Who can view custom roles?</span></span>
    <span data-ttu-id="9d6f4-147">Todas as funções internas no RBAC do Azure permitem a visualização de funções disponíveis para atribuição.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-147">All built-in roles in Azure RBAC allow viewing of roles that are available for assignment.</span></span> <span data-ttu-id="9d6f4-148">Os usuários que podem executar Olá `Microsoft.Authorization/roleDefinition/read` operação em um escopo pode exibir funções RBAC Olá que estão disponíveis para atribuição nesse escopo.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-148">Users who can perform hello `Microsoft.Authorization/roleDefinition/read` operation at a scope can view hello RBAC roles that are available for assignment at that scope.</span></span>

## <a name="see-also"></a><span data-ttu-id="9d6f4-149">Consulte também</span><span class="sxs-lookup"><span data-stu-id="9d6f4-149">See also</span></span>
* <span data-ttu-id="9d6f4-150">[Controle de acesso baseado em função](role-based-access-control-configure.md): Introdução ao RBAC em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-150">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in hello Azure portal.</span></span>
* <span data-ttu-id="9d6f4-151">Saiba como toomanage acessar com:</span><span class="sxs-lookup"><span data-stu-id="9d6f4-151">Learn how toomanage access with:</span></span>
  * [<span data-ttu-id="9d6f4-152">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9d6f4-152">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
  * [<span data-ttu-id="9d6f4-153">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="9d6f4-153">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
  * [<span data-ttu-id="9d6f4-154">API REST</span><span class="sxs-lookup"><span data-stu-id="9d6f4-154">REST API</span></span>](role-based-access-control-manage-access-rest.md)
* <span data-ttu-id="9d6f4-155">[Funções internas](role-based-access-built-in-roles.md): obter detalhes sobre as funções hello incluídos por padrão em RBAC.</span><span class="sxs-lookup"><span data-stu-id="9d6f4-155">[Built-in roles](role-based-access-built-in-roles.md): Get details about hello roles that come standard in RBAC.</span></span>
