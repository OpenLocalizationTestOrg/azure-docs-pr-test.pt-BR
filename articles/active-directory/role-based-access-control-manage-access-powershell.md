---
title: aaaManage baseada em controle de acesso (RBAC) com o Azure PowerShell | Microsoft Docs
description: "Como toomanage RBAC com o Azure PowerShell, incluindo listando as funções, atribuir funções e excluir atribuições de função."
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
ms.openlocfilehash: fa44991113e75b345177867b0bede38de4373e04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-azure-powershell"></a><span data-ttu-id="01a9f-103">Gerenciar o Controle de Acesso baseado em função com o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="01a9f-103">Manage Role-Based Access Control with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="01a9f-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="01a9f-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="01a9f-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="01a9f-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="01a9f-106">API REST</span><span class="sxs-lookup"><span data-stu-id="01a9f-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="01a9f-107">Você pode usar o controle de acesso baseado em função (RBAC) na Olá portal do Azure e uma API de gerenciamento de recursos do Azure toomanage acesso tooyour assinatura em um nível granular.</span><span class="sxs-lookup"><span data-stu-id="01a9f-107">You can use Role-Based Access Control (RBAC) in hello Azure portal and Azure Resource Management API toomanage access tooyour subscription at a fine-grained level.</span></span> <span data-ttu-id="01a9f-108">Com esse recurso, você pode conceder acesso para usuários, grupos ou entidades de serviço do Active Directory, atribuindo toothem algumas funções em um escopo específico.</span><span class="sxs-lookup"><span data-stu-id="01a9f-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles toothem at a particular scope.</span></span>

<span data-ttu-id="01a9f-109">Antes de usar PowerShell toomanage RBAC, você precisa Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="01a9f-109">Before you can use PowerShell toomanage RBAC, you need hello following prerequisites:</span></span>

* <span data-ttu-id="01a9f-110">PowerShell do Azure, versão 0.8.8 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="01a9f-110">Azure PowerShell version 0.8.8 or later.</span></span> <span data-ttu-id="01a9f-111">versão mais recente do tooinstall hello e associe-o com sua assinatura do Azure, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="01a9f-111">tooinstall hello latest version and associate it with your Azure subscription, see [how tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="01a9f-112">Cmdlets do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="01a9f-112">Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="01a9f-113">Instalar Olá [cmdlets do Azure Resource Manager](/powershell/azure/overview) no PowerShell.</span><span class="sxs-lookup"><span data-stu-id="01a9f-113">Install hello [Azure Resource Manager cmdlets](/powershell/azure/overview) in PowerShell.</span></span>

## <a name="list-roles"></a><span data-ttu-id="01a9f-114">Listar funções</span><span class="sxs-lookup"><span data-stu-id="01a9f-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="01a9f-115">Relacionar todas as funções disponíveis</span><span class="sxs-lookup"><span data-stu-id="01a9f-115">List all available roles</span></span>
<span data-ttu-id="01a9f-116">funções RBAC toolist que estão disponíveis para atribuição e tooinspect Olá operações toowhich eles conceder acesso, use `Get-AzureRmRoleDefinition`.</span><span class="sxs-lookup"><span data-stu-id="01a9f-116">toolist RBAC roles that are available for assignment and tooinspect hello operations toowhich they grant access, use `Get-AzureRmRoleDefinition`.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, Description
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - captura de tela](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition1.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="01a9f-118">Relacionar ações de uma função</span><span class="sxs-lookup"><span data-stu-id="01a9f-118">List actions of a role</span></span>
<span data-ttu-id="01a9f-119">ações de saudação toolist para uma função específica, use `Get-AzureRmRoleDefinition <role name>`.</span><span class="sxs-lookup"><span data-stu-id="01a9f-119">toolist hello actions for a specific role, use `Get-AzureRmRoleDefinition <role name>`.</span></span>

```
Get-AzureRmRoleDefinition Contributor | FL Actions, NotActions

(Get-AzureRmRoleDefinition "Virtual Machine Contributor").Actions
```

![RBAC PowerShell - Get-AzureRmRoleDefinition para uma função específica - captura de tela](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition2.png)

## <a name="see-who-has-access"></a><span data-ttu-id="01a9f-121">Veja quem tem acesso</span><span class="sxs-lookup"><span data-stu-id="01a9f-121">See who has access</span></span>
<span data-ttu-id="01a9f-122">atribuições de acesso RBAC toolist, use `Get-AzureRmRoleAssignment`.</span><span class="sxs-lookup"><span data-stu-id="01a9f-122">toolist RBAC access assignments, use `Get-AzureRmRoleAssignment`.</span></span>

### <a name="list-role-assignments-at-a-specific-scope"></a><span data-ttu-id="01a9f-123">Listar as atribuições de função em um escopo específico</span><span class="sxs-lookup"><span data-stu-id="01a9f-123">List role assignments at a specific scope</span></span>
<span data-ttu-id="01a9f-124">Você pode ver todas as atribuições de acesso de saudação de uma assinatura especificada, o grupo de recursos ou o recurso.</span><span class="sxs-lookup"><span data-stu-id="01a9f-124">You can see all hello access assignments for a specified subscription, resource group, or resource.</span></span> <span data-ttu-id="01a9f-125">Por exemplo, toosee Olá todas as atribuições de saudação ativo para um grupo de recursos, use `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.</span><span class="sxs-lookup"><span data-stu-id="01a9f-125">For example, toosee hello all hello active assignments for a resource group, use `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.</span></span>

```
Get-AzureRmRoleAssignment -ResourceGroupName Pharma-Sales-ProjectForcast | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - Get-AzureRmRoleAssignment para um grupo de recursos - captura de tela](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment1.png)

### <a name="list-roles-assigned-tooa-user"></a><span data-ttu-id="01a9f-127">Listar funções tooa usuário atribuídas</span><span class="sxs-lookup"><span data-stu-id="01a9f-127">List roles assigned tooa user</span></span>
<span data-ttu-id="01a9f-128">toolist todas as funções hello atribuídos tooa especificado usuário e funções de saudação que são atribuídas a grupos de toohello toowhich Olá usuário pertence, use `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.</span><span class="sxs-lookup"><span data-stu-id="01a9f-128">toolist all hello roles that are assigned tooa specified user and hello roles that are assigned toohello groups toowhich hello user belongs, use `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.</span></span>

```
Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com | FL DisplayName, RoleDefinitionName, Scope

Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com -ExpandPrincipalGroups | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - Get-AzureRmRoleAssignment para um usuário - captura de tela](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment2.png)

### <a name="list-classic-service-administrator-and-coadmin-role-assignments"></a><span data-ttu-id="01a9f-130">Listar atribuições de função de administrador e coadministrador de serviços clássicos</span><span class="sxs-lookup"><span data-stu-id="01a9f-130">List classic service administrator and coadmin role assignments</span></span>
<span data-ttu-id="01a9f-131">atribuições de acesso de toolist para o administrador de assinatura clássico hello e coadministrators, use:</span><span class="sxs-lookup"><span data-stu-id="01a9f-131">toolist access assignments for hello classic subscription administrator and coadministrators, use:</span></span>

    Get-AzureRmRoleAssignment -IncludeClassicAdministrators

## <a name="grant-access"></a><span data-ttu-id="01a9f-132">Conceder acesso</span><span class="sxs-lookup"><span data-stu-id="01a9f-132">Grant access</span></span>
### <a name="search-for-object-ids"></a><span data-ttu-id="01a9f-133">Pesquisar IDs de objeto</span><span class="sxs-lookup"><span data-stu-id="01a9f-133">Search for object IDs</span></span>
<span data-ttu-id="01a9f-134">tooassign uma função, você precisa tooidentify objeto hello (usuário, grupo ou aplicativo) e o escopo de saudação.</span><span class="sxs-lookup"><span data-stu-id="01a9f-134">tooassign a role, you need tooidentify both hello object (user, group, or application) and hello scope.</span></span>

<span data-ttu-id="01a9f-135">Se você não souber a ID da assinatura hello, você pode ser encontrado no hello **assinaturas** folha no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="01a9f-135">If you don't know hello subscription ID, you can find it in hello **Subscriptions** blade on hello Azure portal.</span></span> <span data-ttu-id="01a9f-136">toolearn como tooquery Olá ID da assinatura, consulte [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) no MSDN.</span><span class="sxs-lookup"><span data-stu-id="01a9f-136">toolearn how tooquery for hello subscription ID, see [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) on MSDN.</span></span>

<span data-ttu-id="01a9f-137">ID de objeto tooget Olá para um grupo do AD do Azure, use:</span><span class="sxs-lookup"><span data-stu-id="01a9f-137">tooget hello object ID for an Azure AD group, use:</span></span>

    Get-AzureRmADGroup -SearchString <group name in quotes>

<span data-ttu-id="01a9f-138">ID de objeto tooget Olá para uma entidade de serviço do AD do Azure ou o aplicativo, use:</span><span class="sxs-lookup"><span data-stu-id="01a9f-138">tooget hello object ID for an Azure AD service principal or application, use:</span></span>

    Get-AzureRmADServicePrincipal -SearchString <service name in quotes>

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a><span data-ttu-id="01a9f-139">Atribuir um aplicativo de tooan de função no escopo de assinatura Olá</span><span class="sxs-lookup"><span data-stu-id="01a9f-139">Assign a role tooan application at hello subscription scope</span></span>
<span data-ttu-id="01a9f-140">aplicativo de tooan toogrant acesso no escopo de assinatura hello, use:</span><span class="sxs-lookup"><span data-stu-id="01a9f-140">toogrant access tooan application at hello subscription scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <application id> -RoleDefinitionName <role name> -Scope <subscription id>

![RBAC PowerShell - New-AzureRmRoleAssignment - captura de tela](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a><span data-ttu-id="01a9f-142">Atribuir um usuário de tooa de função no escopo do grupo de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="01a9f-142">Assign a role tooa user at hello resource group scope</span></span>
<span data-ttu-id="01a9f-143">usuário de tooa toogrant acesso no escopo de grupo de recursos do hello, use:</span><span class="sxs-lookup"><span data-stu-id="01a9f-143">toogrant access tooa user at hello resource group scope, use:</span></span>

    New-AzureRmRoleAssignment -SignInName <email of user> -RoleDefinitionName <role name in quotes> -ResourceGroupName <resource group name>

![RBAC PowerShell - New-AzureRmRoleAssignment - captura de tela](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a><span data-ttu-id="01a9f-145">Atribua um grupo de tooa de função no escopo do recurso Olá</span><span class="sxs-lookup"><span data-stu-id="01a9f-145">Assign a role tooa group at hello resource scope</span></span>
<span data-ttu-id="01a9f-146">grupo de tooa toogrant acesso no escopo do recurso hello, use:</span><span class="sxs-lookup"><span data-stu-id="01a9f-146">toogrant access tooa group at hello resource scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name in quotes> -ResourceName <resource name> -ResourceType <resource type> -ParentResource <parent resource> -ResourceGroupName <resource group name>

![RBAC PowerShell - New-AzureRmRoleAssignment - captura de tela](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment4.png)

## <a name="remove-access"></a><span data-ttu-id="01a9f-148">Remover acesso</span><span class="sxs-lookup"><span data-stu-id="01a9f-148">Remove access</span></span>
<span data-ttu-id="01a9f-149">tooremove acesso para usuários, grupos e aplicativos, use:</span><span class="sxs-lookup"><span data-stu-id="01a9f-149">tooremove access for users, groups, and applications, use:</span></span>

    Remove-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name> -Scope <scope such as subscription id>

![RBAC PowerShell - Remove-AzureRmRoleAssignment - captura de tela](./media/role-based-access-control-manage-access-powershell/3-remove-azure-rm-role-assignment.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="01a9f-151">Criar uma função personalizada</span><span class="sxs-lookup"><span data-stu-id="01a9f-151">Create a custom role</span></span>
<span data-ttu-id="01a9f-152">toocreate uma função personalizada, use Olá ```New-AzureRmRoleDefinition``` comando.</span><span class="sxs-lookup"><span data-stu-id="01a9f-152">toocreate a custom role, use hello ```New-AzureRmRoleDefinition``` command.</span></span> <span data-ttu-id="01a9f-153">Há dois métodos de estruturação função hello, usando PSRoleDefinitionObject ou um modelo JSON.</span><span class="sxs-lookup"><span data-stu-id="01a9f-153">There are two methods of structuring hello role, using PSRoleDefinitionObject or a JSON template.</span></span> 

## <a name="get-actions-for-a-resource-provider"></a><span data-ttu-id="01a9f-154">Obter ações para um provedor de recursos</span><span class="sxs-lookup"><span data-stu-id="01a9f-154">Get Actions for a Resource Provider</span></span>
<span data-ttu-id="01a9f-155">Ao criar funções personalizadas do zero, é importante tooknow todos Olá possíveis operações Olá de provedores de recursos.</span><span class="sxs-lookup"><span data-stu-id="01a9f-155">When You are creating custom roles from scratch, it is important tooknow all hello possible operations from hello resource providers.</span></span>
<span data-ttu-id="01a9f-156">Saudação de uso ```Get-AzureRMProviderOperation``` comando tooget essas informações.</span><span class="sxs-lookup"><span data-stu-id="01a9f-156">Use hello ```Get-AzureRMProviderOperation``` command tooget this information.</span></span>
<span data-ttu-id="01a9f-157">Por exemplo, se você quiser toocheck todas as operações de saudação disponíveis para a máquina virtual usam este comando:</span><span class="sxs-lookup"><span data-stu-id="01a9f-157">For example, if you want toocheck all hello available operations for virtual Machine use this command:</span></span>

```
Get-AzureRMProviderOperation "Microsoft.Compute/virtualMachines/*" | FT OperationName, Operation , Description -AutoSize
```

### <a name="create-role-with-psroledefinitionobject"></a><span data-ttu-id="01a9f-158">Criar função com PSRoleDefinitionObject</span><span class="sxs-lookup"><span data-stu-id="01a9f-158">Create role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="01a9f-159">Quando você usar o PowerShell toocreate uma função personalizada, você pode começar do zero ou usar uma saudação [funções internas](role-based-access-built-in-roles.md) como um ponto de partida.</span><span class="sxs-lookup"><span data-stu-id="01a9f-159">When you use PowerShell toocreate a custom role, you can start from scratch or use one of hello [built-in roles](role-based-access-built-in-roles.md) as a starting point.</span></span> <span data-ttu-id="01a9f-160">exemplo Hello nesta seção começa com uma função interna e, em seguida, personaliza-lo com mais privilégios.</span><span class="sxs-lookup"><span data-stu-id="01a9f-160">hello example in this section starts with a built-in role and then customizes it with more privileges.</span></span> <span data-ttu-id="01a9f-161">Editar saudação do hello atributos tooadd *ações*, *notActions*, ou *escopos* desejado e, em seguida, salvar alterações de saudação como uma nova função.</span><span class="sxs-lookup"><span data-stu-id="01a9f-161">Edit hello attributes tooadd hello *Actions*, *notActions*, or *scopes* that you want, and then save hello changes as a new role.</span></span>

<span data-ttu-id="01a9f-162">Olá exemplo a seguir inicia com hello *colaborador da máquina Virtual* função e usa esse toocreate uma função personalizada chamada *operador de máquina Virtual*.</span><span class="sxs-lookup"><span data-stu-id="01a9f-162">hello following example starts with hello *Virtual Machine Contributor* role and uses that toocreate a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="01a9f-163">nova função de saudação concede acesso tooall ler as operações de *Microsoft. Compute*, *Microsoft*, e *Network* provedores e concede acesso a recursos toostart, reiniciar e monitorar as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="01a9f-163">hello new role grants access tooall read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access toostart, restart, and monitor virtual machines.</span></span> <span data-ttu-id="01a9f-164">função personalizada Olá pode ser usada em duas assinaturas.</span><span class="sxs-lookup"><span data-stu-id="01a9f-164">hello custom role can be used in two subscriptions.</span></span>

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

### <a name="create-role-with-json-template"></a><span data-ttu-id="01a9f-166">Criar função com modelo JSON</span><span class="sxs-lookup"><span data-stu-id="01a9f-166">Create role with JSON template</span></span>
<span data-ttu-id="01a9f-167">Um modelo JSON pode ser usado como definição de fonte de saudação de função personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="01a9f-167">A JSON template can be used as hello source definition for hello custom role.</span></span> <span data-ttu-id="01a9f-168">Olá, exemplo a seguir cria uma função personalizada que permite acesso de leitura toostorage e recursos de computação, acessar toosupport e adiciona a função tootwo assinaturas.</span><span class="sxs-lookup"><span data-stu-id="01a9f-168">hello following example creates a custom role that allows read access toostorage and compute resources, access toosupport, and adds that role tootwo subscriptions.</span></span> <span data-ttu-id="01a9f-169">Criar um novo arquivo `C:\CustomRoles\customrole1.json` com hello exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="01a9f-169">Create a new file `C:\CustomRoles\customrole1.json` with hello following example.</span></span> <span data-ttu-id="01a9f-170">Olá Id deve ser definido muito`null` na criação de função inicial como uma nova ID é gerada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="01a9f-170">hello Id should be set too`null` on initial role creation as a new ID is generated automatically.</span></span> 

```
{
  "Name": "Custom Role 1",
  "Id": null,
  "IsCustom": true,
  "Description": "Allows for read access tooAzure storage and compute resources and access toosupport",
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
<span data-ttu-id="01a9f-171">tooadd Olá função toohello assinaturas, executadas Olá comando PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="01a9f-171">tooadd hello role toohello subscriptions, run hello following PowerShell command:</span></span>
```
New-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="modify-a-custom-role"></a><span data-ttu-id="01a9f-172">Modificar uma função personalizada</span><span class="sxs-lookup"><span data-stu-id="01a9f-172">Modify a custom role</span></span>
<span data-ttu-id="01a9f-173">Toocreating semelhante uma função personalizada, você pode modificar uma função personalizada existente usando Olá PSRoleDefinitionObject ou um modelo JSON.</span><span class="sxs-lookup"><span data-stu-id="01a9f-173">Similar toocreating a custom role, you can modify an existing custom role using either hello PSRoleDefinitionObject or a JSON template.</span></span>

### <a name="modify-role-with-psroledefinitionobject"></a><span data-ttu-id="01a9f-174">Modificar função com PSRoleDefinitionObject</span><span class="sxs-lookup"><span data-stu-id="01a9f-174">Modify role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="01a9f-175">toomodify uma função personalizada, primeiro, use Olá `Get-AzureRmRoleDefinition` tooretrieve Olá função definição de comando.</span><span class="sxs-lookup"><span data-stu-id="01a9f-175">toomodify a custom role, first, use hello `Get-AzureRmRoleDefinition` command tooretrieve hello role definition.</span></span> <span data-ttu-id="01a9f-176">Em seguida, fazer alterações de saudação desejada toohello definição de função.</span><span class="sxs-lookup"><span data-stu-id="01a9f-176">Second, make hello desired changes toohello role definition.</span></span> <span data-ttu-id="01a9f-177">Por fim, use Olá `Set-AzureRmRoleDefinition` saudação do comando toosave modificou a definição de função.</span><span class="sxs-lookup"><span data-stu-id="01a9f-177">Finally, use hello `Set-AzureRmRoleDefinition` command toosave hello modified role definition.</span></span>

<span data-ttu-id="01a9f-178">Olá, exemplo a seguir adiciona Olá `Microsoft.Insights/diagnosticSettings/*` operação toohello *operador de máquina Virtual* função personalizada.</span><span class="sxs-lookup"><span data-stu-id="01a9f-178">hello following example adds hello `Microsoft.Insights/diagnosticSettings/*` operation toohello *Virtual Machine Operator* custom role.</span></span>

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.Actions.Add("Microsoft.Insights/diagnosticSettings/*")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - captura de tela](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-1.png)

<span data-ttu-id="01a9f-180">Olá, exemplo a seguir adiciona um escopos atribuíveis de toohello de assinatura do Azure de saudação *operador de máquina Virtual* função personalizada.</span><span class="sxs-lookup"><span data-stu-id="01a9f-180">hello following example adds an Azure subscription toohello assignable scopes of hello *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmSubscription - SubscriptionName Production3

$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.AssignableScopes.Add("/subscriptions/34370e90-ac4a-4bf9-821f-85eeedead1a2")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - captura de tela](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-2.png)

### <a name="modify-role-with-json-template"></a><span data-ttu-id="01a9f-182">Modificar função com modelo JSON</span><span class="sxs-lookup"><span data-stu-id="01a9f-182">Modify role with JSON template</span></span>
<span data-ttu-id="01a9f-183">Usando o modelo anterior de JSON Olá, você pode modificar um tooadd de função personalizada existente ou remover facilmente ações.</span><span class="sxs-lookup"><span data-stu-id="01a9f-183">Using hello previous JSON template, you can easily modify an existing custom role tooadd or remove Actions.</span></span> <span data-ttu-id="01a9f-184">Atualizar o modelo JSON hello e adicionar ação de leitura de saudação de rede, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="01a9f-184">Update hello JSON template and add hello read action for networking as shown in hello following example.</span></span> <span data-ttu-id="01a9f-185">definições de saudação listadas no modelo de saudação não são definição existente de tooan cumulativamente aplicado, que significa que essa função hello aparece exatamente como você especificar no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="01a9f-185">hello definitions listed in hello template are not cumulatively applied tooan existing definition, meaning that hello role appears exactly as you specify in hello template.</span></span> <span data-ttu-id="01a9f-186">Também é necessário o campo de Id de saudação tooupdate com a ID de saudação da função hello.</span><span class="sxs-lookup"><span data-stu-id="01a9f-186">You also need tooupdate hello Id field with hello ID of hello role.</span></span> <span data-ttu-id="01a9f-187">Se você não tiver certeza de que esse valor é, você pode usar o hello `Get-AzureRmRoleDefinition` tooget cmdlet essas informações.</span><span class="sxs-lookup"><span data-stu-id="01a9f-187">If you aren't sure what this value is, you can use hello `Get-AzureRmRoleDefinition` cmdlet tooget this information.</span></span>

```
{
  "Name": "Custom Role 1",
  "Id": "acce7ded-2559-449d-bcd5-e9604e50bad1",
  "IsCustom": true,
  "Description": "Allows for read access tooAzure storage and compute resources and access toosupport",
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

<span data-ttu-id="01a9f-188">função existente de saudação do tooupdate executar Olá comando PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="01a9f-188">tooupdate hello existing role, run hello following PowerShell command:</span></span>
```
Set-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="delete-a-custom-role"></a><span data-ttu-id="01a9f-189">Excluir uma função personalizada</span><span class="sxs-lookup"><span data-stu-id="01a9f-189">Delete a custom role</span></span>
<span data-ttu-id="01a9f-190">toodelete uma função personalizada, use Olá `Remove-AzureRmRoleDefinition` comando.</span><span class="sxs-lookup"><span data-stu-id="01a9f-190">toodelete a custom role, use hello `Remove-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="01a9f-191">Olá, exemplo a seguir remove Olá *operador de máquina Virtual* função personalizada.</span><span class="sxs-lookup"><span data-stu-id="01a9f-191">hello following example removes hello *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmRoleDefinition "Virtual Machine Operator"

Get-AzureRmRoleDefinition "Virtual Machine Operator" | Remove-AzureRmRoleDefinition
```

![RBAC PowerShell - Remove-AzureRmRoleDefinition - captura de tela](./media/role-based-access-control-manage-access-powershell/4-remove-azurermroledefinition.png)

## <a name="list-custom-roles"></a><span data-ttu-id="01a9f-193">Listar funções personalizadas</span><span class="sxs-lookup"><span data-stu-id="01a9f-193">List custom roles</span></span>
<span data-ttu-id="01a9f-194">funções de saudação toolist que estão disponíveis para atribuição a um escopo, usar Olá `Get-AzureRmRoleDefinition` comando.</span><span class="sxs-lookup"><span data-stu-id="01a9f-194">toolist hello roles that are available for assignment at a scope, use hello `Get-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="01a9f-195">saudação de exemplo a seguir lista todas as funções que estão disponíveis para atribuição na assinatura de saudação selecionada.</span><span class="sxs-lookup"><span data-stu-id="01a9f-195">hello following example lists all roles that are available for assignment in hello selected subscription.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, IsCustom
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - captura de tela](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition-1.png)

<span data-ttu-id="01a9f-197">Em Olá exemplo a seguir, Olá *operador de máquina Virtual* função personalizada não está disponível no hello *Production4* assinatura porque a assinatura não está em Olá  **AssignableScopes** da função hello.</span><span class="sxs-lookup"><span data-stu-id="01a9f-197">In hello following example, hello *Virtual Machine Operator* custom role isn’t available in hello *Production4* subscription because that subscription isn’t in hello **AssignableScopes** of hello role.</span></span>

![RBAC PowerShell - Get-AzureRmRoleDefinition - captura de tela](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition2.png)

## <a name="see-also"></a><span data-ttu-id="01a9f-199">Consulte também</span><span class="sxs-lookup"><span data-stu-id="01a9f-199">See also</span></span>
* <span data-ttu-id="01a9f-200">[Usando o Azure PowerShell com o Azure Resource Manager](../powershell-azure-resource-manager.md)
  [!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]</span><span class="sxs-lookup"><span data-stu-id="01a9f-200">[Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]</span></span>

