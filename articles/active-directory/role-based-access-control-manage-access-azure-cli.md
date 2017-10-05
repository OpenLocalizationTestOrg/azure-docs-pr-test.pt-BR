---
title: "Gerenciar RBAC (controle de acesso baseado em função) com a CLI do Azure | Microsoft Docs"
description: "Saiba como gerenciar o RBAC (Controle de Acesso baseado em função) com a interface de linha de comando do Azure listando as funções e ações de função, e atribuindo funções às assinaturas e escopos de aplicativo."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 3483ee01-8177-49e7-b337-4d5cb14f5e32
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: ad644de6d23950e699d99042d27381336626caab
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-role-based-access-control-with-the-azure-command-line-interface"></a><span data-ttu-id="1275e-103">Gerenciar o Controle de Acesso baseado em função com a Interface de Linha de Comando do Azure</span><span class="sxs-lookup"><span data-stu-id="1275e-103">Manage Role-Based Access Control with the Azure command-line interface</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1275e-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1275e-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="1275e-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="1275e-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="1275e-106">API REST</span><span class="sxs-lookup"><span data-stu-id="1275e-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)


<span data-ttu-id="1275e-107">Você pode usar o RBAC (Controle de Acesso baseado em função) no Portal do Azure e na API do Azure Resource Manager para gerenciar o acesso a sua assinatura e aos recursos de maneira detalhada.</span><span class="sxs-lookup"><span data-stu-id="1275e-107">You can use Role-Based Access Control (RBAC) in the Azure portal and Azure Resource Manager API to manage access to your subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="1275e-108">Com esse recurso, você pode conceder acesso aos usuários, grupos ou entidades de serviço do Active Directory atribuindo algumas funções para eles em um determinado escopo.</span><span class="sxs-lookup"><span data-stu-id="1275e-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles to them at a particular scope.</span></span>

<span data-ttu-id="1275e-109">Antes de poder usar a CLI (interface de linha de comando) do Azure para gerenciar o RBAC, é necessário ter os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="1275e-109">Before you can use the Azure command-line interface (CLI) to manage RBAC, you must have the following prerequisites:</span></span>

* <span data-ttu-id="1275e-110">CLI do Azure versão 0.8.8 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="1275e-110">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="1275e-111">Para instalar a versão mais recente e associá-la à sua assinatura do Azure, consulte [Instalar e configurar a CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="1275e-111">To install the latest version and associate it with your Azure subscription, see [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="1275e-112">Azure Resource Manager na Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="1275e-112">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="1275e-113">Acesse [Usando a Azure CLI com o Resource Manager](../xplat-cli-azure-resource-manager.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="1275e-113">Go to [Using the Azure CLI with the Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

## <a name="list-roles"></a><span data-ttu-id="1275e-114">Listar funções</span><span class="sxs-lookup"><span data-stu-id="1275e-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="1275e-115">Relacionar todas as funções disponíveis</span><span class="sxs-lookup"><span data-stu-id="1275e-115">List all available roles</span></span>
<span data-ttu-id="1275e-116">Para listar todas as funções disponíveis, use:</span><span class="sxs-lookup"><span data-stu-id="1275e-116">To list all available roles, use:</span></span>

        azure role list

<span data-ttu-id="1275e-117">O exemplo a seguir mostra a relação de *todas as funções disponíveis*.</span><span class="sxs-lookup"><span data-stu-id="1275e-117">The following example shows the list of *all available roles*.</span></span>

```
azure role list --json | jq '.[] | {"roleName":.properties.roleName, "description":.properties.description}'
```

![Linha de comando do Azure RBAC  - lista de funções do azure - captura de tela](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-list.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="1275e-119">Relacionar ações de uma função</span><span class="sxs-lookup"><span data-stu-id="1275e-119">List actions of a role</span></span>
<span data-ttu-id="1275e-120">Para listar as ações de uma função, use:</span><span class="sxs-lookup"><span data-stu-id="1275e-120">To list the actions of a role, use:</span></span>

    azure role show "<role name>"

<span data-ttu-id="1275e-121">O exemplo a seguir mostra as ações das funções *Colaborador* e *Colaborador da Máquina Virtual*.</span><span class="sxs-lookup"><span data-stu-id="1275e-121">The following example shows the actions of the *Contributor* and *Virtual Machine Contributor* roles.</span></span>

```
azure role show "contributor" --json | jq '.[] | {"Actions":.properties.permissions[0].actions,"NotActions":properties.permissions[0].notActions}'

azure role show "virtual machine contributor" --json | jq '.[] | .properties.permissions[0].actions'
```

![Linha de comando do Azure RBAC  - exibição de funções do azure - captura de tela](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-show.png)

## <a name="list-access"></a><span data-ttu-id="1275e-123">Relacionar acesso</span><span class="sxs-lookup"><span data-stu-id="1275e-123">List access</span></span>
### <a name="list-role-assignments-effective-on-a-resource-group"></a><span data-ttu-id="1275e-124">Relacionar as atribuições de função como efetivas em um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="1275e-124">List role assignments effective on a resource group</span></span>
<span data-ttu-id="1275e-125">Para listar as atribuições de função que existem em um grupo de recursos, use:</span><span class="sxs-lookup"><span data-stu-id="1275e-125">To list the role assignments that exist in a resource group, use:</span></span>

    azure role assignment list --resource-group <resource group name>

<span data-ttu-id="1275e-126">O exemplo a seguir mostra as atribuições de função no grupo *pharma-sales-projecforcast* .</span><span class="sxs-lookup"><span data-stu-id="1275e-126">The following example shows the role assignments in the *pharma-sales-projecforcast* group.</span></span>

```
azure role assignment list --resource-group pharma-sales-projecforcast --json | jq '.[] | {"DisplayName":.properties.aADObject.displayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Linha de comando do RBAC do Azure – lista de atribuição de funções do Azure por grupo – captura de tela](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-1.png)

### <a name="list-role-assignments-for-a-user"></a><span data-ttu-id="1275e-128">Listar as atribuições de função de um usuário</span><span class="sxs-lookup"><span data-stu-id="1275e-128">List role assignments for a user</span></span>
<span data-ttu-id="1275e-129">Para listar as atribuições de função para um usuário específico e as atribuições que são atribuídas aos grupos do usuário, use:</span><span class="sxs-lookup"><span data-stu-id="1275e-129">To list the role assignments for a specific user and the assignments that are assigned to a user's groups, use:</span></span>

    azure role assignment list --signInName <user email>

<span data-ttu-id="1275e-130">Você também pode ver as atribuições da função herdadas dos grupos modificando o comando:</span><span class="sxs-lookup"><span data-stu-id="1275e-130">You can also see role assignments that are inherited from groups by modifying the command:</span></span>

    azure role assignment list --expandPrincipalGroups --signInName <user email>

<span data-ttu-id="1275e-131">O exemplo a seguir mostra as atribuições da função concedidas ao usuário *sameert@aaddemo.com* .</span><span class="sxs-lookup"><span data-stu-id="1275e-131">The following example shows the role assignments that are granted to the *sameert@aaddemo.com* user.</span></span> <span data-ttu-id="1275e-132">Isso inclui funções atribuídas diretamente ao usuário e funções herdadas de grupos.</span><span class="sxs-lookup"><span data-stu-id="1275e-132">This includes roles that are assigned directly to the user and roles that are inherited from groups.</span></span>

```
azure role assignment list --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'

azure role assignment list --expandPrincipalGroups --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Linha de comando do Azure RBAC  - lista de atribuição de funções do azure por usuário - captura de tela](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-2.png)

## <a name="grant-access"></a><span data-ttu-id="1275e-134">Conceder acesso</span><span class="sxs-lookup"><span data-stu-id="1275e-134">Grant access</span></span>
<span data-ttu-id="1275e-135">Para conceder acesso após ter identificado a função que você deseja atribuir, use:</span><span class="sxs-lookup"><span data-stu-id="1275e-135">To grant access after you have identified the role that you want to assign, use:</span></span>

    azure role assignment create

### <a name="assign-a-role-to-group-at-the-subscription-scope"></a><span data-ttu-id="1275e-136">Atribuir uma função ao grupo no escopo da assinatura</span><span class="sxs-lookup"><span data-stu-id="1275e-136">Assign a role to group at the subscription scope</span></span>
<span data-ttu-id="1275e-137">Para atribuir uma função a um grupo no escopo da assinatura, use:</span><span class="sxs-lookup"><span data-stu-id="1275e-137">To assign a role to a group at the subscription scope, use:</span></span>

    azure role assignment create --objectId  <group object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="1275e-138">O exemplo a seguir atribui a função *Leitor* à *equipe de Christine Koch* no escopo da *assinatura*.</span><span class="sxs-lookup"><span data-stu-id="1275e-138">The following example assigns the *Reader* role to *Christine Koch's Team* at the *subscription* scope.</span></span>

![Linha de comando do Azure RBAC – criação de atribuição de funções do Azure por grupo – captura de tela](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-1.png)

### <a name="assign-a-role-to-an-application-at-the-subscription-scope"></a><span data-ttu-id="1275e-140">Atribuir uma função a um aplicativo no escopo da assinatura</span><span class="sxs-lookup"><span data-stu-id="1275e-140">Assign a role to an application at the subscription scope</span></span>
<span data-ttu-id="1275e-141">Para atribuir uma função a um aplicativo no escopo da assinatura, use:</span><span class="sxs-lookup"><span data-stu-id="1275e-141">To assign a role to an application at the subscription scope, use:</span></span>

    azure role assignment create --objectId  <applications object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="1275e-142">O exemplo a seguir concede a função *Colaborador* a um aplicativo *Azure AD* na assinatura selecionada.</span><span class="sxs-lookup"><span data-stu-id="1275e-142">The following example grants the *Contributor* role to an *Azure AD* application on the selected subscription.</span></span>

 ![Linha de comando do Azure RBAC  - criação de atribuição de funções do azure por aplicativo](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-2.png)

### <a name="assign-a-role-to-a-user-at-the-resource-group-scope"></a><span data-ttu-id="1275e-144">Atribuir uma função ao usuário no escopo do grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="1275e-144">Assign a role to a user at the resource group scope</span></span>
<span data-ttu-id="1275e-145">Para atribuir uma função a um usuário no escopo do grupo de recursos, use:</span><span class="sxs-lookup"><span data-stu-id="1275e-145">To assign a role to a user at the resource group scope, use:</span></span>

    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>

<span data-ttu-id="1275e-146">O exemplo a seguir concede a função *Colaborador da Máquina Virtual* ao usuário *samert@aaddemo.com* no escopo do grupo de recursos *Pharma-Sales-ProjectForcast*.</span><span class="sxs-lookup"><span data-stu-id="1275e-146">The following example grants the *Virtual Machine Contributor* role to *samert@aaddemo.com* user at the *Pharma-Sales-ProjectForcast* resource group scope.</span></span>

![Linha de comando do RBAC do Azure – criação de atribuição de funções do Azure por usuário – captura de tela](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-3.png)

### <a name="assign-a-role-to-a-group-at-the-resource-scope"></a><span data-ttu-id="1275e-148">Atribuir uma função a um grupo no escopo de recursos</span><span class="sxs-lookup"><span data-stu-id="1275e-148">Assign a role to a group at the resource scope</span></span>
<span data-ttu-id="1275e-149">Para atribuir uma função a um grupo no escopo de recursos, use:</span><span class="sxs-lookup"><span data-stu-id="1275e-149">To assign a role to a group at the resource scope, use:</span></span>

    azure role assignment create --objectId <group id> --role "<name of role>" --resource-name <resource group name> --resource-type <resource group type> --parent <resource group parent> --resource-group <resource group>

<span data-ttu-id="1275e-150">O exemplo a seguir concede a função *Colaborador da Máquina Virtual* a um grupo do *Azure AD* em uma *sub-rede*.</span><span class="sxs-lookup"><span data-stu-id="1275e-150">The following example grants the *Virtual Machine Contributor* role to an *Azure AD* group on a *subnet*.</span></span>

![Linha de comando do Azure RBAC – criação de atribuição de funções do Azure por grupo – captura de tela](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-4.png)

## <a name="remove-access"></a><span data-ttu-id="1275e-152">Remover acesso</span><span class="sxs-lookup"><span data-stu-id="1275e-152">Remove access</span></span>
<span data-ttu-id="1275e-153">Para remover uma atribuição de função, use:</span><span class="sxs-lookup"><span data-stu-id="1275e-153">To remove a role assignment, use:</span></span>

    azure role assignment delete --objectId <object id to from which to remove role> --roleName "<role name>"

<span data-ttu-id="1275e-154">O exemplo a seguir remove a atribuição da função *Colaborador da Máquina Virtual* do usuário *sammert@aaddemo.com* no grupo de recursos *Pharma-Sales-ProjectForcast*.</span><span class="sxs-lookup"><span data-stu-id="1275e-154">The following example removes the *Virtual Machine Contributor* role assignment from the *sammert@aaddemo.com* user on the *Pharma-Sales-ProjectForcast* resource group.</span></span>
<span data-ttu-id="1275e-155">Em seguida, o exemplo remove a atribuição de função de um grupo na assinatura.</span><span class="sxs-lookup"><span data-stu-id="1275e-155">The example then removes the role assignment from a group on the subscription.</span></span>

![Linha de comando do Azure RBAC  - exclusão de atribuição de funções do azure - captura de tela](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-assignment-delete.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="1275e-157">Criar uma função personalizada</span><span class="sxs-lookup"><span data-stu-id="1275e-157">Create a custom role</span></span>
<span data-ttu-id="1275e-158">Para criar uma função personalizada, use:</span><span class="sxs-lookup"><span data-stu-id="1275e-158">To create a custom role, use:</span></span>

    azure role create --inputfile <file path>

<span data-ttu-id="1275e-159">O exemplo a seguir cria uma função personalizada chamada *Operador de Máquina Virtual*.</span><span class="sxs-lookup"><span data-stu-id="1275e-159">The following example creates a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="1275e-160">Essa função personalizada concede acesso a todas as operações de leitura dos provedores de recursos *Microsoft.Compute*, *Microsoft.Storage* e *Microsoft.Network*, além de conceder acesso para iniciar, reiniciar e monitorar máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="1275e-160">This custom role grants access to all read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access to start, restart, and monitor virtual machines.</span></span> <span data-ttu-id="1275e-161">Essa função personalizada pode ser usada em duas assinaturas.</span><span class="sxs-lookup"><span data-stu-id="1275e-161">This custom role can be used in two subscriptions.</span></span> <span data-ttu-id="1275e-162">Este exemplo utiliza um arquivo JSON como entrada.</span><span class="sxs-lookup"><span data-stu-id="1275e-162">This example uses a JSON file as an input.</span></span>

![JSON - definição de função personalizada - captura de tela](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-1.png)

![Linha de comando do Azure RBAC  - criação de função do azure - captura de tela](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-2.png)

## <a name="modify-a-custom-role"></a><span data-ttu-id="1275e-165">Modificar uma função personalizada</span><span class="sxs-lookup"><span data-stu-id="1275e-165">Modify a custom role</span></span>
<span data-ttu-id="1275e-166">Para modificar uma função personalizada, use o comando `azure role show` para recuperar a definição da função.</span><span class="sxs-lookup"><span data-stu-id="1275e-166">To modify a custom role, first use the `azure role show` command to retrieve role definition.</span></span> <span data-ttu-id="1275e-167">Depois, faça as alterações desejadas no arquivo de definição da função.</span><span class="sxs-lookup"><span data-stu-id="1275e-167">Second, make the desired changes to the role definition file.</span></span> <span data-ttu-id="1275e-168">Por fim, use `azure role set` para salvar a definição da função modificada.</span><span class="sxs-lookup"><span data-stu-id="1275e-168">Finally, use `azure role set` to save the modified role definition.</span></span>

    azure role set --inputfile <file path>

<span data-ttu-id="1275e-169">O exemplo a seguir adiciona a operação *Microsoft.Insights/diagnosticSettings/* a **Actions** e uma assinatura do Azure a **AssignableScopes** da função personalizada Operador de Máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="1275e-169">The following example adds the *Microsoft.Insights/diagnosticSettings/* operation to the **Actions**, and an Azure subscription to the **AssignableScopes** of the Virtual Machine Operator custom role.</span></span>

![JSON - modificar definição de função personalizada - captura de tela](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set-1.png)

![Linha de comando do Azure RBAC  - conjunto de funções do azure - captura de tela](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set2.png)

## <a name="delete-a-custom-role"></a><span data-ttu-id="1275e-172">Excluir uma função personalizada</span><span class="sxs-lookup"><span data-stu-id="1275e-172">Delete a custom role</span></span>
<span data-ttu-id="1275e-173">Para excluir uma função personalizada, primeiro use o comando `azure role show` para determinar a **ID** da função.</span><span class="sxs-lookup"><span data-stu-id="1275e-173">To delete a custom role, first use the `azure role show` command to determine the **ID** of the role.</span></span> <span data-ttu-id="1275e-174">Em seguida, use o comando `azure role delete` para excluir a função especificando a **ID**.</span><span class="sxs-lookup"><span data-stu-id="1275e-174">Then, use the `azure role delete` command to delete the role by specifying the **ID**.</span></span>

<span data-ttu-id="1275e-175">O exemplo a seguir remove a função personalizada *Operador de Máquina Virtual* .</span><span class="sxs-lookup"><span data-stu-id="1275e-175">The following example removes the *Virtual Machine Operator* custom role.</span></span>

![Linha de comando do Azure RBAC  - exclusão de funções do azure - captura de tela](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-delete.png)

## <a name="list-custom-roles"></a><span data-ttu-id="1275e-177">Listar funções personalizadas</span><span class="sxs-lookup"><span data-stu-id="1275e-177">List custom roles</span></span>
<span data-ttu-id="1275e-178">Para listar as funções disponíveis para atribuição em um escopo, use o comando `azure role list` .</span><span class="sxs-lookup"><span data-stu-id="1275e-178">To list the roles that are available for assignment at a scope, use the `azure role list` command.</span></span>

<span data-ttu-id="1275e-179">O comando a seguir lista todas as funções disponíveis para atribuição na assinatura selecionada.</span><span class="sxs-lookup"><span data-stu-id="1275e-179">The following command lists all roles that are available for assignment in the selected subscription.</span></span>

```
azure role list --json | jq '.[] | {"name":.properties.roleName, type:.properties.type}'
```

![Linha de comando do Azure RBAC  - lista de funções do azure - captura de tela](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list1.png)

<span data-ttu-id="1275e-181">No exemplo a seguir, a função personalizada *Operador de Máquina Virtual* não está disponível na assinatura *Production4*, pois essa assinatura não está nos **AssignableScopes** da função.</span><span class="sxs-lookup"><span data-stu-id="1275e-181">In the following example, the *Virtual Machine Operator* custom role isn’t available in the *Production4* subscription because that subscription isn’t in the **AssignableScopes** of the role.</span></span>

```
azure role list --json | jq '.[] | if .properties.type == "CustomRole" then .properties.roleName else empty end'
```

![Linha de comando do Azure RBAC  - lista de funções do azure para funções personalizadas - captura de tela](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list2.png)

## <a name="next-steps"></a><span data-ttu-id="1275e-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1275e-183">Next steps</span></span>
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

