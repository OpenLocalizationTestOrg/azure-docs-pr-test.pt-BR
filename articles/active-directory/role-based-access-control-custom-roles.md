---
title: "Criar funções personalizadas no RBAC do Azure | Microsoft Docs"
description: "Saiba como definir funções personalizadas com o Controle de Acesso Baseado em Função para um gerenciamento de identidade mais preciso na sua assinatura do Azure."
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
ms.openlocfilehash: 8e72f2c8095d13c4b6df3c6576bd58806a3c0f2f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-custom-roles-for-azure-role-based-access-control"></a><span data-ttu-id="13d7c-103">Criar funções personalizadas para o Controle de Acesso Baseado em Função do Azure</span><span class="sxs-lookup"><span data-stu-id="13d7c-103">Create custom roles for Azure Role-Based Access Control</span></span>
<span data-ttu-id="13d7c-104">Crie uma função personalizada no RBAC (Controle de Acesso Baseado em Função) do Azure se nenhuma das funções internas atende às suas necessidades de acesso específicas.</span><span class="sxs-lookup"><span data-stu-id="13d7c-104">Create a custom role in Azure Role-Based Access Control (RBAC) if none of the built-in roles meet your specific access needs.</span></span> <span data-ttu-id="13d7c-105">É possível criar funções personalizadas usando o [Azure PowerShell](role-based-access-control-manage-access-powershell.md), a [CLI (interface de linha de comando) do Azure](role-based-access-control-manage-access-azure-cli.md) e a [API REST](role-based-access-control-manage-access-rest.md).</span><span class="sxs-lookup"><span data-stu-id="13d7c-105">Custom roles can be created using [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface](role-based-access-control-manage-access-azure-cli.md) (CLI), and the [REST API](role-based-access-control-manage-access-rest.md).</span></span> <span data-ttu-id="13d7c-106">Assim como as funções internas, é possível atribuir funções personalizadas a usuários, grupos e aplicativos na assinatura, no grupo de recursos e nos escopos de recurso.</span><span class="sxs-lookup"><span data-stu-id="13d7c-106">Just like built-in roles, you can assign custom roles to users, groups, and applications at subscription, resource group, and resource scopes.</span></span> <span data-ttu-id="13d7c-107">As funções personalizadas são armazenadas em um locatário do Azure AD e podem ser compartilhadas entre assinaturas.</span><span class="sxs-lookup"><span data-stu-id="13d7c-107">Custom roles are stored in an Azure AD tenant and can be shared across subscriptions.</span></span>

<span data-ttu-id="13d7c-108">Cada locatário pode criar até 2000 funções personalizadas.</span><span class="sxs-lookup"><span data-stu-id="13d7c-108">Each tenant can create up to 2000 custom roles.</span></span> 

<span data-ttu-id="13d7c-109">O seguinte exemplo mostra uma função personalizada para monitorar e reiniciar máquinas virtuais:</span><span class="sxs-lookup"><span data-stu-id="13d7c-109">The following example shows a custom role for monitoring and restarting virtual machines:</span></span>

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
## <a name="actions"></a><span data-ttu-id="13d7c-110">Ações</span><span class="sxs-lookup"><span data-stu-id="13d7c-110">Actions</span></span>
<span data-ttu-id="13d7c-111">A propriedade **Actions** de uma função personalizada especifica as operações do Azure às quais a função concede acesso.</span><span class="sxs-lookup"><span data-stu-id="13d7c-111">The **Actions** property of a custom role specifies the Azure operations to which the role grants access.</span></span> <span data-ttu-id="13d7c-112">É uma coleção de cadeias de operação que identificam as operações protegíveis dos provedores de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="13d7c-112">It is a collection of operation strings that identify securable operations of Azure resource providers.</span></span> <span data-ttu-id="13d7c-113">Cadeias de caracteres de operação seguem o formato de `Microsoft.<ProviderName>/<ChildResourceType>/<action>`.</span><span class="sxs-lookup"><span data-stu-id="13d7c-113">Operation strings follow the format of `Microsoft.<ProviderName>/<ChildResourceType>/<action>`.</span></span> <span data-ttu-id="13d7c-114">As cadeias de operação que contêm caracteres curinga (\*) permitem acesso a todas as operações que correspondem à cadeia de operação.</span><span class="sxs-lookup"><span data-stu-id="13d7c-114">Operation strings that contain wildcards (\*) grant access to all operations that match the operation string.</span></span> <span data-ttu-id="13d7c-115">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="13d7c-115">For instance:</span></span>

* <span data-ttu-id="13d7c-116">`*/read` concede acesso a operações de leitura a todos os tipos de recursos de todos os provedores de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="13d7c-116">`*/read` grants access to read operations for all resource types of all Azure resource providers.</span></span>
* <span data-ttu-id="13d7c-117">`Microsoft.Compute/*` concede acesso a todas as operações a todos os tipos de recursos no provedor de recursos Microsoft.Compute.</span><span class="sxs-lookup"><span data-stu-id="13d7c-117">`Microsoft.Compute/*` grants access to all operations for all resource types in the Microsoft.Compute resource provider.</span></span>
* <span data-ttu-id="13d7c-118">`Microsoft.Network/*/read` concede acesso a operações de leitura a todos os tipos de recursos no provedor de recursos Microsoft.Network do Azure.</span><span class="sxs-lookup"><span data-stu-id="13d7c-118">`Microsoft.Network/*/read` grants access to read operations for all resource types in the Microsoft.Network resource provider of Azure.</span></span>
* <span data-ttu-id="13d7c-119">`Microsoft.Compute/virtualMachines/*` concede acesso a todas as operações de máquinas virtuais e seus tipos de recursos filhos.</span><span class="sxs-lookup"><span data-stu-id="13d7c-119">`Microsoft.Compute/virtualMachines/*` grants access to all operations of virtual machines and its child resource types.</span></span>
* <span data-ttu-id="13d7c-120">`Microsoft.Web/sites/restart/Action` concede acesso para reinicialização de sites.</span><span class="sxs-lookup"><span data-stu-id="13d7c-120">`Microsoft.Web/sites/restart/Action` grants access to restart websites.</span></span>

<span data-ttu-id="13d7c-121">Use `Get-AzureRmProviderOperation` (no PowerShell) ou `azure provider operations show` (na CLI do Azure) para listar as operações dos provedores de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="13d7c-121">Use `Get-AzureRmProviderOperation` (in PowerShell) or `azure provider operations show` (in Azure CLI) to list operations of Azure resource providers.</span></span> <span data-ttu-id="13d7c-122">Você também pode usar esses comandos para verificar se uma cadeia de operação é válida e para expandir as cadeias de operação curinga.</span><span class="sxs-lookup"><span data-stu-id="13d7c-122">You may also use these commands to verify that an operation string is valid, and to expand wildcard operation strings.</span></span>

```
Get-AzureRMProviderOperation Microsoft.Compute/virtualMachines/*/action | FT Operation, OperationName

Get-AzureRMProviderOperation Microsoft.Network/*
```

![PowerShell screenshot - Get-AzureRMProviderOperation](./media/role-based-access-control-configure/1-get-azurermprovideroperation-1.png)

```
azure provider operations show "Microsoft.Compute/virtualMachines/*/action" --js on | jq '.[] | .operation'

azure provider operations show "Microsoft.Network/*"
```

![<span data-ttu-id="13d7c-124">Captura de tela da CLI do Azure – as operações do provedor do Azure mostram "Microsoft.Compute/virtualMachines/\*/action"</span><span class="sxs-lookup"><span data-stu-id="13d7c-124">Azure CLI screenshot - azure provider operations show "Microsoft.Compute/virtualMachines/\*/action"</span></span> ](./media/role-based-access-control-configure/1-azure-provider-operations-show.png)

## <a name="notactions"></a><span data-ttu-id="13d7c-125">NotActions</span><span class="sxs-lookup"><span data-stu-id="13d7c-125">NotActions</span></span>
<span data-ttu-id="13d7c-126">Use a propriedade **NotActions** se o conjunto de operações que você deseja permitir fica definido mais facilmente pela exclusão das operações restritas.</span><span class="sxs-lookup"><span data-stu-id="13d7c-126">Use the **NotActions** property if the set of operations that you wish to allow is more easily defined by excluding restricted operations.</span></span> <span data-ttu-id="13d7c-127">A permissão de acesso concedida por uma função personalizada é computada subtraindo as operações **NotActions** das operações **Actions**.</span><span class="sxs-lookup"><span data-stu-id="13d7c-127">The access granted by a custom role is computed by subtracting the **NotActions** operations from the **Actions** operations.</span></span>

> [!NOTE]
> <span data-ttu-id="13d7c-128">Se um usuário for atribuído a uma função que exclui uma operação em **NotActions** e for atribuído a uma segunda função que concede acesso à mesma operação, ele terá permissão para executar essa operação.</span><span class="sxs-lookup"><span data-stu-id="13d7c-128">If a user is assigned a role that excludes an operation in **NotActions**, and is assigned a second role that grants access to the same operation, the user is allowed to perform that operation.</span></span> <span data-ttu-id="13d7c-129">**NotActions** não é uma regra de negação, é simplesmente uma maneira conveniente de criar um conjunto de operações permitidas quando for necessário excluir operações específicas.</span><span class="sxs-lookup"><span data-stu-id="13d7c-129">**NotActions** is not a deny rule – it is simply a convenient way to create a set of allowed operations when specific operations need to be excluded.</span></span>
>
>

## <a name="assignablescopes"></a><span data-ttu-id="13d7c-130">AssignableScopes</span><span class="sxs-lookup"><span data-stu-id="13d7c-130">AssignableScopes</span></span>
<span data-ttu-id="13d7c-131">A propriedade **AssignableScopes** da função personalizada especifica os escopos (assinaturas, grupos de recursos ou recursos) nos quais a função personalizada ficará disponível para a atribuição.</span><span class="sxs-lookup"><span data-stu-id="13d7c-131">The **AssignableScopes** property of the custom role specifies the scopes (subscriptions, resource groups, or resources) within which the custom role is available for assignment.</span></span> <span data-ttu-id="13d7c-132">Você pode disponibilizar a função personalizada para atribuição apenas nas assinaturas ou grupos de recursos que a exijam e não sobrecarregar a experiência do usuário nas assinaturas ou grupos de recursos restantes.</span><span class="sxs-lookup"><span data-stu-id="13d7c-132">You can make the custom role available for assignment in only the subscriptions or resource groups that require it, and not clutter user experience for the rest of the subscriptions or resource groups.</span></span>

<span data-ttu-id="13d7c-133">Exemplos de escopos válidos que podem ser atribuídos incluem:</span><span class="sxs-lookup"><span data-stu-id="13d7c-133">Examples of valid assignable scopes include:</span></span>

* <span data-ttu-id="13d7c-134">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e”, “/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624” – disponibiliza a função para atribuição em duas assinaturas.</span><span class="sxs-lookup"><span data-stu-id="13d7c-134">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e”, “/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624” - makes the role available for assignment in two subscriptions.</span></span>
* <span data-ttu-id="13d7c-135">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e” – disponibiliza a função para atribuição em uma única assinatura.</span><span class="sxs-lookup"><span data-stu-id="13d7c-135">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e” - makes the role available for assignment in a single subscription.</span></span>
* <span data-ttu-id="13d7c-136">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network” – disponibiliza a função para atribuição apenas no Grupo de recursos de rede.</span><span class="sxs-lookup"><span data-stu-id="13d7c-136">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network” - makes the role available for assignment only in the Network resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="13d7c-137">Você deve usar pelo menos uma assinatura, grupo de recursos ou ID de recurso.</span><span class="sxs-lookup"><span data-stu-id="13d7c-137">You must use at least one subscription, resource group, or resource ID.</span></span>
>
>

## <a name="custom-roles-access-control"></a><span data-ttu-id="13d7c-138">Controle de acesso de funções personalizadas</span><span class="sxs-lookup"><span data-stu-id="13d7c-138">Custom roles access control</span></span>
<span data-ttu-id="13d7c-139">A propriedade **AssignableScopes** da função personalizada também controla quem pode exibir, modificar e excluir a função.</span><span class="sxs-lookup"><span data-stu-id="13d7c-139">The **AssignableScopes** property of the custom role also controls who can view, modify, and delete the role.</span></span>

* <span data-ttu-id="13d7c-140">Quem pode criar uma função personalizada?</span><span class="sxs-lookup"><span data-stu-id="13d7c-140">Who can create a custom role?</span></span>
    <span data-ttu-id="13d7c-141">Os Proprietários (e os Administradores de acesso do usuário) de assinaturas, grupos de recursos e recursos podem criar funções personalizadas para uso nesses escopos.</span><span class="sxs-lookup"><span data-stu-id="13d7c-141">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can create custom roles for use in those scopes.</span></span>
    <span data-ttu-id="13d7c-142">O usuário que está criando a função precisa ser capaz de executar a operação `Microsoft.Authorization/roleDefinition/write` em todos os **AssignableScopes** da função.</span><span class="sxs-lookup"><span data-stu-id="13d7c-142">The user creating the role needs to be able to perform `Microsoft.Authorization/roleDefinition/write` operation on all the **AssignableScopes** of the role.</span></span>
* <span data-ttu-id="13d7c-143">Quem pode modificar uma função personalizada?</span><span class="sxs-lookup"><span data-stu-id="13d7c-143">Who can modify a custom role?</span></span>
    <span data-ttu-id="13d7c-144">Os Proprietários (e os Administradores de acesso do usuário) de assinaturas, grupos de recursos e recursos podem modificar funções personalizadas nesses escopos.</span><span class="sxs-lookup"><span data-stu-id="13d7c-144">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can modify custom roles in those scopes.</span></span> <span data-ttu-id="13d7c-145">Os usuários precisam poder executar a operação `Microsoft.Authorization/roleDefinition/write` em todos os **AssignableScopes** de uma função personalizada.</span><span class="sxs-lookup"><span data-stu-id="13d7c-145">Users need to be able to perform the `Microsoft.Authorization/roleDefinition/write` operation on all the **AssignableScopes** of a custom role.</span></span>
* <span data-ttu-id="13d7c-146">Quem pode exibir funções personalizadas?</span><span class="sxs-lookup"><span data-stu-id="13d7c-146">Who can view custom roles?</span></span>
    <span data-ttu-id="13d7c-147">Todas as funções internas no RBAC do Azure permitem a visualização de funções disponíveis para atribuição.</span><span class="sxs-lookup"><span data-stu-id="13d7c-147">All built-in roles in Azure RBAC allow viewing of roles that are available for assignment.</span></span> <span data-ttu-id="13d7c-148">Os usuários que podem executar a operação `Microsoft.Authorization/roleDefinition/read` em um escopo podem exibir as funções de RBAC disponíveis para atribuição nesse escopo.</span><span class="sxs-lookup"><span data-stu-id="13d7c-148">Users who can perform the `Microsoft.Authorization/roleDefinition/read` operation at a scope can view the RBAC roles that are available for assignment at that scope.</span></span>

## <a name="see-also"></a><span data-ttu-id="13d7c-149">Confira também</span><span class="sxs-lookup"><span data-stu-id="13d7c-149">See also</span></span>
* <span data-ttu-id="13d7c-150">[Controle de Acesso com Base em Funções](role-based-access-control-configure.md): introdução ao RBAC no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="13d7c-150">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in the Azure portal.</span></span>
* <span data-ttu-id="13d7c-151">Saiba como gerenciar o acesso com:</span><span class="sxs-lookup"><span data-stu-id="13d7c-151">Learn how to manage access with:</span></span>
  * [<span data-ttu-id="13d7c-152">PowerShell</span><span class="sxs-lookup"><span data-stu-id="13d7c-152">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
  * [<span data-ttu-id="13d7c-153">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="13d7c-153">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
  * [<span data-ttu-id="13d7c-154">API REST</span><span class="sxs-lookup"><span data-stu-id="13d7c-154">REST API</span></span>](role-based-access-control-manage-access-rest.md)
* <span data-ttu-id="13d7c-155">[Funções internas](role-based-access-built-in-roles.md): obtenha detalhes sobre as funções que são incluídas por padrão no RBAC.</span><span class="sxs-lookup"><span data-stu-id="13d7c-155">[Built-in roles](role-based-access-built-in-roles.md): Get details about the roles that come standard in RBAC.</span></span>
