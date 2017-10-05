---
title: "Gerenciar o RBAC (Controle de Acesso Baseado em Função) com o Azure PowerShell | Microsoft Docs"
description: "Como gerenciar o RBAC com o Azure PowerShell, incluindo listagem e atribuição e funções, e exclusão de atribuições de funções."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 9e225dba-9044-4b13-b573-2f30d77925a9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: d7b11df21650b5cb27f9c3dd8306f8d12664185e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-role-based-access-control-with-azure-powershell"></a><span data-ttu-id="97308-103">Gerenciar o Controle de Acesso baseado em função com o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="97308-103">Manage Role-Based Access Control with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="97308-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="97308-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="97308-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="97308-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="97308-106">API REST</span><span class="sxs-lookup"><span data-stu-id="97308-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="97308-107">Você pode usar o RBAC (Controle de Acesso Baseado em Função) no portal do Azure e na API de Gerenciamento de Recursos do Azure para gerenciar o acesso à sua assinatura em um nível refinado.</span><span class="sxs-lookup"><span data-stu-id="97308-107">You can use Role-Based Access Control (RBAC) in the Azure portal and Azure Resource Management API to manage access to your subscription at a fine-grained level.</span></span> <span data-ttu-id="97308-108">Com esse recurso, você pode conceder acesso aos usuários, grupos ou entidades de serviço do Active Directory atribuindo algumas funções para eles em um determinado escopo.</span><span class="sxs-lookup"><span data-stu-id="97308-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles to them at a particular scope.</span></span>

<span data-ttu-id="97308-109">Antes de poder usar o PowerShell para gerenciar o RBAC, você precisa dos seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="97308-109">Before you can use PowerShell to manage RBAC, you need the following prerequisites:</span></span>

* <span data-ttu-id="97308-110">PowerShell do Azure, versão 0.8.8 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="97308-110">Azure PowerShell version 0.8.8 or later.</span></span> <span data-ttu-id="97308-111">Para instalar a última versão e associá-la à sua assinatura do Azure, consulte [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="97308-111">To install the latest version and associate it with your Azure subscription, see [how to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="97308-112">Cmdlets do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="97308-112">Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="97308-113">Instale os [cmdlets do Azure Resource Manager](/powershell/azure/overview) no PowerShell.</span><span class="sxs-lookup"><span data-stu-id="97308-113">Install the [Azure Resource Manager cmdlets](/powershell/azure/overview) in PowerShell.</span></span>

## <a name="list-roles"></a><span data-ttu-id="97308-114">Listar funções</span><span class="sxs-lookup"><span data-stu-id="97308-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="97308-115">Relacionar todas as funções disponíveis</span><span class="sxs-lookup"><span data-stu-id="97308-115">List all available roles</span></span>
<span data-ttu-id="97308-116">Para listar as funções RBAC disponíveis para a atribuição e inspecionar as operações para as quais elas concedem acesso, use `Get-AzureRmRoleDefinition`.</span><span class="sxs-lookup"><span data-stu-id="97308-116">To list RBAC roles that are available for assignment and to inspect the operations to which they grant access, use `Get-AzureRmRoleDefinition`.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, Description
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - captura de tela](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition1.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="97308-118">Relacionar ações de uma função</span><span class="sxs-lookup"><span data-stu-id="97308-118">List actions of a role</span></span>
<span data-ttu-id="97308-119">Para listar as ações para uma função específica, use `Get-AzureRmRoleDefinition <role name>`.</span><span class="sxs-lookup"><span data-stu-id="97308-119">To list the actions for a specific role, use `Get-AzureRmRoleDefinition <role name>`.</span></span>

```
Get-AzureRmRoleDefinition Contributor | FL Actions, NotActions

(Get-AzureRmRoleDefinition "Virtual Machine Contributor").Actions
```

![RBAC PowerShell - Get-AzureRmRoleDefinition para uma função específica - captura de tela](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition2.png)

## <a name="see-who-has-access"></a><span data-ttu-id="97308-121">Veja quem tem acesso</span><span class="sxs-lookup"><span data-stu-id="97308-121">See who has access</span></span>
<span data-ttu-id="97308-122">Para listar as atribuições de acesso do RBAC, use `Get-AzureRmRoleAssignment`.</span><span class="sxs-lookup"><span data-stu-id="97308-122">To list RBAC access assignments, use `Get-AzureRmRoleAssignment`.</span></span>

### <a name="list-role-assignments-at-a-specific-scope"></a><span data-ttu-id="97308-123">Listar as atribuições de função em um escopo específico</span><span class="sxs-lookup"><span data-stu-id="97308-123">List role assignments at a specific scope</span></span>
<span data-ttu-id="97308-124">Você pode ver todas as atribuições de acesso para uma assinatura, grupo de recursos ou recurso especificados.</span><span class="sxs-lookup"><span data-stu-id="97308-124">You can see all the access assignments for a specified subscription, resource group, or resource.</span></span> <span data-ttu-id="97308-125">Por exemplo, para ver todas as atribuições ativas para um grupo de recursos, use `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.</span><span class="sxs-lookup"><span data-stu-id="97308-125">For example, to see the all the active assignments for a resource group, use `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.</span></span>

```
Get-AzureRmRoleAssignment -ResourceGroupName Pharma-Sales-ProjectForcast | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - Get-AzureRmRoleAssignment para um grupo de recursos - captura de tela](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment1.png)

### <a name="list-roles-assigned-to-a-user"></a><span data-ttu-id="97308-127">Listar funções atribuídas a um usuário</span><span class="sxs-lookup"><span data-stu-id="97308-127">List roles assigned to a user</span></span>
<span data-ttu-id="97308-128">Para listar todas as funções que são atribuídas a um usuário específico e as funções que são atribuídas aos grupos aos quais o usuário pertence, use `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.</span><span class="sxs-lookup"><span data-stu-id="97308-128">To list all the roles that are assigned to a specified user and the roles that are assigned to the groups to which the user belongs, use `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.</span></span>

```
Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com | FL DisplayName, RoleDefinitionName, Scope

Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com -ExpandPrincipalGroups | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - Get-AzureRmRoleAssignment para um usuário - captura de tela](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment2.png)

### <a name="list-classic-service-administrator-and-coadmin-role-assignments"></a><span data-ttu-id="97308-130">Listar atribuições de função de administrador e coadministrador de serviços clássicos</span><span class="sxs-lookup"><span data-stu-id="97308-130">List classic service administrator and coadmin role assignments</span></span>
<span data-ttu-id="97308-131">Para listar as atribuições para administrador e coadministradores da assinatura clássica, use:</span><span class="sxs-lookup"><span data-stu-id="97308-131">To list access assignments for the classic subscription administrator and coadministrators, use:</span></span>

    Get-AzureRmRoleAssignment -IncludeClassicAdministrators

## <a name="grant-access"></a><span data-ttu-id="97308-132">Conceder acesso</span><span class="sxs-lookup"><span data-stu-id="97308-132">Grant access</span></span>
### <a name="search-for-object-ids"></a><span data-ttu-id="97308-133">Pesquisar IDs de objeto</span><span class="sxs-lookup"><span data-stu-id="97308-133">Search for object IDs</span></span>
<span data-ttu-id="97308-134">Para atribuir uma função, você precisa identificar o objeto (usuário, grupo ou aplicativo) e o escopo.</span><span class="sxs-lookup"><span data-stu-id="97308-134">To assign a role, you need to identify both the object (user, group, or application) and the scope.</span></span>

<span data-ttu-id="97308-135">Se você não souber a ID da assinatura, poderá encontrá-la na folha **Assinaturas** no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="97308-135">If you don't know the subscription ID, you can find it in the **Subscriptions** blade on the Azure portal.</span></span> <span data-ttu-id="97308-136">Para saber como consultar a ID da assinatura, consulte [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) no MSDN.</span><span class="sxs-lookup"><span data-stu-id="97308-136">To learn how to query for the subscription ID, see [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) on MSDN.</span></span>

<span data-ttu-id="97308-137">Para obter a ID de objeto para um grupo do Azure AD, use:</span><span class="sxs-lookup"><span data-stu-id="97308-137">To get the object ID for an Azure AD group, use:</span></span>

    Get-AzureRmADGroup -SearchString <group name in quotes>

<span data-ttu-id="97308-138">Para obter a ID de objeto de uma Entidade de Serviço do Azure AD ou um aplicativo, use:</span><span class="sxs-lookup"><span data-stu-id="97308-138">To get the object ID for an Azure AD service principal or application, use:</span></span>

    Get-AzureRmADServicePrincipal -SearchString <service name in quotes>

### <a name="assign-a-role-to-an-application-at-the-subscription-scope"></a><span data-ttu-id="97308-139">Atribuir uma função a um aplicativo no escopo da assinatura</span><span class="sxs-lookup"><span data-stu-id="97308-139">Assign a role to an application at the subscription scope</span></span>
<span data-ttu-id="97308-140">Para conceder acesso a um aplicativo no escopo da assinatura, use:</span><span class="sxs-lookup"><span data-stu-id="97308-140">To grant access to an application at the subscription scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <application id> -RoleDefinitionName <role name> -Scope <subscription id>

![RBAC PowerShell - New-AzureRmRoleAssignment - captura de tela](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment2.png)

### <a name="assign-a-role-to-a-user-at-the-resource-group-scope"></a><span data-ttu-id="97308-142">Atribuir uma função ao usuário no escopo do grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="97308-142">Assign a role to a user at the resource group scope</span></span>
<span data-ttu-id="97308-143">Para conceder acesso a um usuário no escopo do grupo de recursos, use:</span><span class="sxs-lookup"><span data-stu-id="97308-143">To grant access to a user at the resource group scope, use:</span></span>

    New-AzureRmRoleAssignment -SignInName <email of user> -RoleDefinitionName <role name in quotes> -ResourceGroupName <resource group name>

![RBAC PowerShell - New-AzureRmRoleAssignment - captura de tela](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment3.png)

### <a name="assign-a-role-to-a-group-at-the-resource-scope"></a><span data-ttu-id="97308-145">Atribuir uma função a um grupo no escopo de recursos</span><span class="sxs-lookup"><span data-stu-id="97308-145">Assign a role to a group at the resource scope</span></span>
<span data-ttu-id="97308-146">Para conceder acesso a um grupo no escopo de recursos, use:</span><span class="sxs-lookup"><span data-stu-id="97308-146">To grant access to a group at the resource scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name in quotes> -ResourceName <resource name> -ResourceType <resource type> -ParentResource <parent resource> -ResourceGroupName <resource group name>

![RBAC PowerShell - New-AzureRmRoleAssignment - captura de tela](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment4.png)

## <a name="remove-access"></a><span data-ttu-id="97308-148">Remover acesso</span><span class="sxs-lookup"><span data-stu-id="97308-148">Remove access</span></span>
<span data-ttu-id="97308-149">Para remover o acesso a usuários, grupos e aplicativos, use:</span><span class="sxs-lookup"><span data-stu-id="97308-149">To remove access for users, groups, and applications, use:</span></span>

    Remove-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name> -Scope <scope such as subscription id>

![RBAC PowerShell - Remove-AzureRmRoleAssignment - captura de tela](./media/role-based-access-control-manage-access-powershell/3-remove-azure-rm-role-assignment.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="97308-151">Criar uma função personalizada</span><span class="sxs-lookup"><span data-stu-id="97308-151">Create a custom role</span></span>
<span data-ttu-id="97308-152">Para criar uma função personalizada, use o comando ```New-AzureRmRoleDefinition``` .</span><span class="sxs-lookup"><span data-stu-id="97308-152">To create a custom role, use the ```New-AzureRmRoleDefinition``` command.</span></span> <span data-ttu-id="97308-153">Há dois métodos de estruturar a função, usando PSRoleDefinitionObject ou um modelo JSON.</span><span class="sxs-lookup"><span data-stu-id="97308-153">There are two methods of structuring the role, using PSRoleDefinitionObject or a JSON template.</span></span> 

## <a name="get-actions-for-a-resource-provider"></a><span data-ttu-id="97308-154">Obter ações para um provedor de recursos</span><span class="sxs-lookup"><span data-stu-id="97308-154">Get Actions for a Resource Provider</span></span>
<span data-ttu-id="97308-155">Quando estiver criando funções personalizadas do zero, é importante conhecer todas as possíveis operações dos provedores de recursos.</span><span class="sxs-lookup"><span data-stu-id="97308-155">When You are creating custom roles from scratch, it is important to know all the possible operations from the resource providers.</span></span>
<span data-ttu-id="97308-156">Use o comando ```Get-AzureRMProviderOperation``` para obter essas informações.</span><span class="sxs-lookup"><span data-stu-id="97308-156">Use the ```Get-AzureRMProviderOperation``` command to get this information.</span></span>
<span data-ttu-id="97308-157">Por exemplo, se desejar verificar todas as operações disponíveis para a máquina virtual, use este comando:</span><span class="sxs-lookup"><span data-stu-id="97308-157">For example, if you want to check all the available operations for virtual Machine use this command:</span></span>

```
Get-AzureRMProviderOperation "Microsoft.Compute/virtualMachines/*" | FT OperationName, Operation , Description -AutoSize
```

### <a name="create-role-with-psroledefinitionobject"></a><span data-ttu-id="97308-158">Criar função com PSRoleDefinitionObject</span><span class="sxs-lookup"><span data-stu-id="97308-158">Create role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="97308-159">Ao usar o PowerShell para criar uma função personalizada, é possível começar do zero ou usar uma das [funções internas](role-based-access-built-in-roles.md) como ponto de partida.</span><span class="sxs-lookup"><span data-stu-id="97308-159">When you use PowerShell to create a custom role, you can start from scratch or use one of the [built-in roles](role-based-access-built-in-roles.md) as a starting point.</span></span> <span data-ttu-id="97308-160">O exemplo nesta seção começa com uma função interna e, em seguida, a personaliza com mais privilégios.</span><span class="sxs-lookup"><span data-stu-id="97308-160">The example in this section starts with a built-in role and then customizes it with more privileges.</span></span> <span data-ttu-id="97308-161">Edite os atributos para adicionar *Actions*, *notActions* ou *scopes* desejados e salve as alterações como uma nova função.</span><span class="sxs-lookup"><span data-stu-id="97308-161">Edit the attributes to add the *Actions*, *notActions*, or *scopes* that you want, and then save the changes as a new role.</span></span>

<span data-ttu-id="97308-162">O exemplo a seguir inicia com a função *Colaborador da Máquina Virtual* e utiliza-a para criar uma função personalizada denominada *Operador da Máquina Virtual*.</span><span class="sxs-lookup"><span data-stu-id="97308-162">The following example starts with the *Virtual Machine Contributor* role and uses that to create a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="97308-163">A nova função concede acesso a todas as operações de leitura dos provedores de recursos *Microsoft.Compute*, *Microsoft.Storage* e *Microsoft.Network* e concede acesso para iniciar, reiniciar e monitorar as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="97308-163">The new role grants access to all read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access to start, restart, and monitor virtual machines.</span></span> <span data-ttu-id="97308-164">A função personalizada pode ser usada em duas assinaturas.</span><span class="sxs-lookup"><span data-stu-id="97308-164">The custom role can be used in two subscriptions.</span></span>

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Contributor"
$role.Id = $null
$role.Name = "Virtual Machine Operator"
$role.Description = "Can monitor and restart virtual machines."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Storage/*/read")
$role.Actions.Add("Microsoft.Network/*/read")
$role.Actions.Add("Microsoft.Compute/*/read")
$role.Actions.Add("Microsoft.Compute/virtualMachines/start/action")
$role.Actions.Add("Microsoft.Compute/virtualMachines/restart/action")
$role.Actions.Add("Microsoft.Authorization/*/read")
$role.Actions.Add("Microsoft.Resources/subscriptions/resourceGroups/read")
$role.Actions.Add("Microsoft.Insights/alertRules/*")
$role.Actions.Add("Microsoft.Support/*")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e")
$role.AssignableScopes.Add("/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624")
New-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - captura de tela](./media/role-based-access-control-manage-access-powershell/2-new-azurermroledefinition.png)

### <a name="create-role-with-json-template"></a><span data-ttu-id="97308-166">Criar função com modelo JSON</span><span class="sxs-lookup"><span data-stu-id="97308-166">Create role with JSON template</span></span>
<span data-ttu-id="97308-167">Um modelo JSON pode ser usado como a definição da fonte para a função personalizada.</span><span class="sxs-lookup"><span data-stu-id="97308-167">A JSON template can be used as the source definition for the custom role.</span></span> <span data-ttu-id="97308-168">O exemplo a seguir cria uma função personalizada que permite acesso de leitura ao armazenamento e aos recursos de computação, acesso ao suporte e adiciona essa função a duas assinaturas.</span><span class="sxs-lookup"><span data-stu-id="97308-168">The following example creates a custom role that allows read access to storage and compute resources, access to support, and adds that role to two subscriptions.</span></span> <span data-ttu-id="97308-169">Crie um novo arquivo `C:\CustomRoles\customrole1.json` com o exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="97308-169">Create a new file `C:\CustomRoles\customrole1.json` with the following example.</span></span> <span data-ttu-id="97308-170">A ID deve ser definida como `null` na criação de função inicial, pois uma nova ID é gerada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="97308-170">The Id should be set to `null` on initial role creation as a new ID is generated automatically.</span></span> 

```
{
  "Name": "Custom Role 1",
  "Id": null,
  "IsCustom": true,
  "Description": "Allows for read access to Azure storage and compute resources and access to support",
  "Actions": [
    "Microsoft.Compute/*/read",
    "Microsoft.Storage/*/read",
    "Microsoft.Support/*"
  ],
  "NotActions": [
  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624"
  ]
}
```
<span data-ttu-id="97308-171">Para adicionar a função às assinaturas, execute o seguinte comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="97308-171">To add the role to the subscriptions, run the following PowerShell command:</span></span>
```
New-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="modify-a-custom-role"></a><span data-ttu-id="97308-172">Modificar uma função personalizada</span><span class="sxs-lookup"><span data-stu-id="97308-172">Modify a custom role</span></span>
<span data-ttu-id="97308-173">Assim como na criação de uma função personalizada, você pode modificar uma função personalizada existente usando PSRoleDefinitionObject ou um modelo JSON.</span><span class="sxs-lookup"><span data-stu-id="97308-173">Similar to creating a custom role, you can modify an existing custom role using either the PSRoleDefinitionObject or a JSON template.</span></span>

### <a name="modify-role-with-psroledefinitionobject"></a><span data-ttu-id="97308-174">Modificar função com PSRoleDefinitionObject</span><span class="sxs-lookup"><span data-stu-id="97308-174">Modify role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="97308-175">Para modificar uma função personalizada, primeiro use o comando `Get-AzureRmRoleDefinition` para recuperar a definição da função.</span><span class="sxs-lookup"><span data-stu-id="97308-175">To modify a custom role, first, use the `Get-AzureRmRoleDefinition` command to retrieve the role definition.</span></span> <span data-ttu-id="97308-176">Depois, faça as alterações desejadas na definição da função.</span><span class="sxs-lookup"><span data-stu-id="97308-176">Second, make the desired changes to the role definition.</span></span> <span data-ttu-id="97308-177">Por fim, use o comando `Set-AzureRmRoleDefinition` para salvar a definição da função modificada.</span><span class="sxs-lookup"><span data-stu-id="97308-177">Finally, use the `Set-AzureRmRoleDefinition` command to save the modified role definition.</span></span>

<span data-ttu-id="97308-178">O exemplo a seguir adiciona a operação `Microsoft.Insights/diagnosticSettings/*` à função personalizada *Operador de Máquina Virtual* .</span><span class="sxs-lookup"><span data-stu-id="97308-178">The following example adds the `Microsoft.Insights/diagnosticSettings/*` operation to the *Virtual Machine Operator* custom role.</span></span>

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.Actions.Add("Microsoft.Insights/diagnosticSettings/*")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - captura de tela](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-1.png)

<span data-ttu-id="97308-180">O exemplo a seguir adiciona uma assinatura do Azure para os escopos atribuíveis da função personalizada de *Operador da Máquina Virtual* .</span><span class="sxs-lookup"><span data-stu-id="97308-180">The following example adds an Azure subscription to the assignable scopes of the *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmSubscription - SubscriptionName Production3

$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.AssignableScopes.Add("/subscriptions/34370e90-ac4a-4bf9-821f-85eeedead1a2")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - captura de tela](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-2.png)

### <a name="modify-role-with-json-template"></a><span data-ttu-id="97308-182">Modificar função com modelo JSON</span><span class="sxs-lookup"><span data-stu-id="97308-182">Modify role with JSON template</span></span>
<span data-ttu-id="97308-183">Usando o modelo JSON anterior, você pode facilmente modificar uma função personalizada existente para adicionar ou remover ações.</span><span class="sxs-lookup"><span data-stu-id="97308-183">Using the previous JSON template, you can easily modify an existing custom role to add or remove Actions.</span></span> <span data-ttu-id="97308-184">Atualize o modelo JSON e adicione a ação de leitura para rede, conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="97308-184">Update the JSON template and add the read action for networking as shown in the following example.</span></span> <span data-ttu-id="97308-185">As definições listadas no modelo não são aplicadas de forma cumulativa a uma definição existente, o que significa que a função aparece exatamente como especificada no modelo.</span><span class="sxs-lookup"><span data-stu-id="97308-185">The definitions listed in the template are not cumulatively applied to an existing definition, meaning that the role appears exactly as you specify in the template.</span></span> <span data-ttu-id="97308-186">Você também precisa atualizar o campo de ID com a ID da função.</span><span class="sxs-lookup"><span data-stu-id="97308-186">You also need to update the Id field with the ID of the role.</span></span> <span data-ttu-id="97308-187">Se não tiver certeza de qual é esse valor, você poderá usar o cmdlet `Get-AzureRmRoleDefinition` para obter essa informação.</span><span class="sxs-lookup"><span data-stu-id="97308-187">If you aren't sure what this value is, you can use the `Get-AzureRmRoleDefinition` cmdlet to get this information.</span></span>

```
{
  "Name": "Custom Role 1",
  "Id": "acce7ded-2559-449d-bcd5-e9604e50bad1",
  "IsCustom": true,
  "Description": "Allows for read access to Azure storage and compute resources and access to support",
  "Actions": [
    "Microsoft.Compute/*/read",
    "Microsoft.Storage/*/read",
    "Microsoft.Network/*/read",
    "Microsoft.Support/*"
  ],
  "NotActions": [
  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624"
  ]
}
```

<span data-ttu-id="97308-188">Para atualizar a função existente, execute o seguinte comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="97308-188">To update the existing role, run the following PowerShell command:</span></span>
```
Set-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="delete-a-custom-role"></a><span data-ttu-id="97308-189">Excluir uma função personalizada</span><span class="sxs-lookup"><span data-stu-id="97308-189">Delete a custom role</span></span>
<span data-ttu-id="97308-190">Para excluir uma função personalizada, use o comando `Remove-AzureRmRoleDefinition` .</span><span class="sxs-lookup"><span data-stu-id="97308-190">To delete a custom role, use the `Remove-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="97308-191">O exemplo a seguir remove a função personalizada *Operador de Máquina Virtual* .</span><span class="sxs-lookup"><span data-stu-id="97308-191">The following example removes the *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmRoleDefinition "Virtual Machine Operator"

Get-AzureRmRoleDefinition "Virtual Machine Operator" | Remove-AzureRmRoleDefinition
```

![RBAC PowerShell - Remove-AzureRmRoleDefinition - captura de tela](./media/role-based-access-control-manage-access-powershell/4-remove-azurermroledefinition.png)

## <a name="list-custom-roles"></a><span data-ttu-id="97308-193">Listar funções personalizadas</span><span class="sxs-lookup"><span data-stu-id="97308-193">List custom roles</span></span>
<span data-ttu-id="97308-194">Para listar as funções disponíveis para atribuição em um escopo, use o comando `Get-AzureRmRoleDefinition` .</span><span class="sxs-lookup"><span data-stu-id="97308-194">To list the roles that are available for assignment at a scope, use the `Get-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="97308-195">O exemplo a seguir lista todas as funções disponíveis para atribuição na assinatura selecionada.</span><span class="sxs-lookup"><span data-stu-id="97308-195">The following example lists all roles that are available for assignment in the selected subscription.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, IsCustom
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - captura de tela](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition-1.png)

<span data-ttu-id="97308-197">No exemplo a seguir, a função personalizada *Operador de Máquina Virtual* não está disponível na assinatura *Production4*, pois essa assinatura não está no **AssignableScopes** da função.</span><span class="sxs-lookup"><span data-stu-id="97308-197">In the following example, the *Virtual Machine Operator* custom role isn’t available in the *Production4* subscription because that subscription isn’t in the **AssignableScopes** of the role.</span></span>

![RBAC PowerShell - Get-AzureRmRoleDefinition - captura de tela](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition2.png)

## <a name="see-also"></a><span data-ttu-id="97308-199">Consulte também</span><span class="sxs-lookup"><span data-stu-id="97308-199">See also</span></span>
* <span data-ttu-id="97308-200">[Usando o Azure PowerShell com o Azure Resource Manager](../powershell-azure-resource-manager.md)
  [!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]</span><span class="sxs-lookup"><span data-stu-id="97308-200">[Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]</span></span>

