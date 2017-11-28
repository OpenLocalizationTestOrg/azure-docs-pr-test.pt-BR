---
title: aaaManage baseada em controle de acesso (RBAC) com CLI do Azure | Microsoft Docs
description: "Saiba como interface toomanage baseada em controle de acesso (RBAC) com hello Azure de linha de comando por função e funções de listagem ações e atribuindo funções toohello escopos de assinatura e o aplicativo."
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
ms.openlocfilehash: 438418e5f6ee9b98908c9c264d516eb722a4e26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-hello-azure-command-line-interface"></a><span data-ttu-id="1ff63-103">Gerenciar o controle de acesso baseado em função com hello interface de linha de comando do Azure</span><span class="sxs-lookup"><span data-stu-id="1ff63-103">Manage Role-Based Access Control with hello Azure command-line interface</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1ff63-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ff63-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="1ff63-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="1ff63-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="1ff63-106">API REST</span><span class="sxs-lookup"><span data-stu-id="1ff63-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)


<span data-ttu-id="1ff63-107">Você pode usar o controle de acesso baseado em função (RBAC) em hello portal do Azure e assinatura do Azure Resource Manager API toomanage acesso tooyour e recursos em um nível granular.</span><span class="sxs-lookup"><span data-stu-id="1ff63-107">You can use Role-Based Access Control (RBAC) in hello Azure portal and Azure Resource Manager API toomanage access tooyour subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="1ff63-108">Com esse recurso, você pode conceder acesso para usuários, grupos ou entidades de serviço do Active Directory, atribuindo toothem algumas funções em um escopo específico.</span><span class="sxs-lookup"><span data-stu-id="1ff63-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles toothem at a particular scope.</span></span>

<span data-ttu-id="1ff63-109">Antes de usar toomanage de interface de linha de comando (CLI) do Azure Olá RBAC, você deve ter Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ff63-109">Before you can use hello Azure command-line interface (CLI) toomanage RBAC, you must have hello following prerequisites:</span></span>

* <span data-ttu-id="1ff63-110">CLI do Azure versão 0.8.8 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="1ff63-110">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="1ff63-111">versão mais recente do tooinstall hello e associe-o com sua assinatura do Azure, consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="1ff63-111">tooinstall hello latest version and associate it with your Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="1ff63-112">Azure Resource Manager na Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="1ff63-112">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="1ff63-113">Vá muito[usando Olá CLI do Azure com o Gerenciador de recursos de hello](../xplat-cli-azure-resource-manager.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="1ff63-113">Go too[Using hello Azure CLI with hello Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

## <a name="list-roles"></a><span data-ttu-id="1ff63-114">Listar funções</span><span class="sxs-lookup"><span data-stu-id="1ff63-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="1ff63-115">Relacionar todas as funções disponíveis</span><span class="sxs-lookup"><span data-stu-id="1ff63-115">List all available roles</span></span>
<span data-ttu-id="1ff63-116">toolist todas as funções disponíveis, use:</span><span class="sxs-lookup"><span data-stu-id="1ff63-116">toolist all available roles, use:</span></span>

        azure role list

<span data-ttu-id="1ff63-117">Olá, exemplo a seguir mostra a lista de saudação do *todas as funções disponíveis*.</span><span class="sxs-lookup"><span data-stu-id="1ff63-117">hello following example shows hello list of *all available roles*.</span></span>

```
azure role list --json | jq '.[] | {"roleName":.properties.roleName, "description":.properties.description}'
```

![Linha de comando do Azure RBAC  - lista de funções do azure - captura de tela](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-list.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="1ff63-119">Relacionar ações de uma função</span><span class="sxs-lookup"><span data-stu-id="1ff63-119">List actions of a role</span></span>
<span data-ttu-id="1ff63-120">ações de saudação toolist de uma função, use:</span><span class="sxs-lookup"><span data-stu-id="1ff63-120">toolist hello actions of a role, use:</span></span>

    azure role show "<role name>"

<span data-ttu-id="1ff63-121">Olá, exemplo a seguir mostra as ações de saudação do hello *Colaborador* e *colaborador da máquina Virtual* funções.</span><span class="sxs-lookup"><span data-stu-id="1ff63-121">hello following example shows hello actions of hello *Contributor* and *Virtual Machine Contributor* roles.</span></span>

```
azure role show "contributor" --json | jq '.[] | {"Actions":.properties.permissions[0].actions,"NotActions":properties.permissions[0].notActions}'

azure role show "virtual machine contributor" --json | jq '.[] | .properties.permissions[0].actions'
```

![Linha de comando do Azure RBAC  - exibição de funções do azure - captura de tela](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-show.png)

## <a name="list-access"></a><span data-ttu-id="1ff63-123">Relacionar acesso</span><span class="sxs-lookup"><span data-stu-id="1ff63-123">List access</span></span>
### <a name="list-role-assignments-effective-on-a-resource-group"></a><span data-ttu-id="1ff63-124">Relacionar as atribuições de função como efetivas em um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="1ff63-124">List role assignments effective on a resource group</span></span>
<span data-ttu-id="1ff63-125">toolist Olá atribuições de função que existem em um grupo de recursos, use:</span><span class="sxs-lookup"><span data-stu-id="1ff63-125">toolist hello role assignments that exist in a resource group, use:</span></span>

    azure role assignment list --resource-group <resource group name>

<span data-ttu-id="1ff63-126">Olá exemplo a seguir mostra as atribuições de função hello em Olá *pharma de vendas de projecforcast* grupo.</span><span class="sxs-lookup"><span data-stu-id="1ff63-126">hello following example shows hello role assignments in hello *pharma-sales-projecforcast* group.</span></span>

```
azure role assignment list --resource-group pharma-sales-projecforcast --json | jq '.[] | {"DisplayName":.properties.aADObject.displayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Linha de comando do RBAC do Azure – lista de atribuição de funções do Azure por grupo – captura de tela](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-1.png)

### <a name="list-role-assignments-for-a-user"></a><span data-ttu-id="1ff63-128">Listar as atribuições de função de um usuário</span><span class="sxs-lookup"><span data-stu-id="1ff63-128">List role assignments for a user</span></span>
<span data-ttu-id="1ff63-129">atribuições de função toolist Olá para um usuário específico e atribuições de saudação que são atribuídas a grupos de usuários tooa, use:</span><span class="sxs-lookup"><span data-stu-id="1ff63-129">toolist hello role assignments for a specific user and hello assignments that are assigned tooa user's groups, use:</span></span>

    azure role assignment list --signInName <user email>

<span data-ttu-id="1ff63-130">Você também pode ver as atribuições de função são herdadas de grupos, modificando o comando hello:</span><span class="sxs-lookup"><span data-stu-id="1ff63-130">You can also see role assignments that are inherited from groups by modifying hello command:</span></span>

    azure role assignment list --expandPrincipalGroups --signInName <user email>

<span data-ttu-id="1ff63-131">Olá, exemplo a seguir mostra as atribuições de função de saudação que recebem toohello  *sameert@aaddemo.com*  usuário.</span><span class="sxs-lookup"><span data-stu-id="1ff63-131">hello following example shows hello role assignments that are granted toohello *sameert@aaddemo.com* user.</span></span> <span data-ttu-id="1ff63-132">Isso inclui funções que são atribuídas diretamente toohello usuário e que são herdadas de grupos.</span><span class="sxs-lookup"><span data-stu-id="1ff63-132">This includes roles that are assigned directly toohello user and roles that are inherited from groups.</span></span>

```
azure role assignment list --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'

azure role assignment list --expandPrincipalGroups --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Linha de comando do Azure RBAC  - lista de atribuição de funções do azure por usuário - captura de tela](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-2.png)

## <a name="grant-access"></a><span data-ttu-id="1ff63-134">Conceder acesso</span><span class="sxs-lookup"><span data-stu-id="1ff63-134">Grant access</span></span>
<span data-ttu-id="1ff63-135">acesso de toogrant depois de ter identificado a função hello que você deseja tooassign, use:</span><span class="sxs-lookup"><span data-stu-id="1ff63-135">toogrant access after you have identified hello role that you want tooassign, use:</span></span>

    azure role assignment create

### <a name="assign-a-role-toogroup-at-hello-subscription-scope"></a><span data-ttu-id="1ff63-136">Atribuir um toogroup de função no escopo de assinatura Olá</span><span class="sxs-lookup"><span data-stu-id="1ff63-136">Assign a role toogroup at hello subscription scope</span></span>
<span data-ttu-id="1ff63-137">tooassign um grupo de tooa de função no escopo de assinatura hello, use:</span><span class="sxs-lookup"><span data-stu-id="1ff63-137">tooassign a role tooa group at hello subscription scope, use:</span></span>

    azure role assignment create --objectId  <group object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="1ff63-138">Olá, exemplo a seguir atribui Olá *leitor* função muito*equipe de Christine Koch* em Olá *assinatura* escopo.</span><span class="sxs-lookup"><span data-stu-id="1ff63-138">hello following example assigns hello *Reader* role too*Christine Koch's Team* at hello *subscription* scope.</span></span>

![Linha de comando do Azure RBAC – criação de atribuição de funções do Azure por grupo – captura de tela](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-1.png)

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a><span data-ttu-id="1ff63-140">Atribuir um aplicativo de tooan de função no escopo de assinatura Olá</span><span class="sxs-lookup"><span data-stu-id="1ff63-140">Assign a role tooan application at hello subscription scope</span></span>
<span data-ttu-id="1ff63-141">tooassign um aplicativo de tooan de função no escopo de assinatura hello, use:</span><span class="sxs-lookup"><span data-stu-id="1ff63-141">tooassign a role tooan application at hello subscription scope, use:</span></span>

    azure role assignment create --objectId  <applications object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="1ff63-142">Olá, exemplo a seguir concede Olá *Colaborador* função tooan *AD do Azure* aplicativo hello selecionado assinatura.</span><span class="sxs-lookup"><span data-stu-id="1ff63-142">hello following example grants hello *Contributor* role tooan *Azure AD* application on hello selected subscription.</span></span>

 ![Linha de comando do Azure RBAC  - criação de atribuição de funções do azure por aplicativo](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a><span data-ttu-id="1ff63-144">Atribuir um usuário de tooa de função no escopo do grupo de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="1ff63-144">Assign a role tooa user at hello resource group scope</span></span>
<span data-ttu-id="1ff63-145">tooassign um usuário de tooa de função no escopo de grupo de recursos do hello, use:</span><span class="sxs-lookup"><span data-stu-id="1ff63-145">tooassign a role tooa user at hello resource group scope, use:</span></span>

    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>

<span data-ttu-id="1ff63-146">Olá, exemplo a seguir concede Olá *colaborador da máquina Virtual* função muito *samert@aaddemo.com*  usuário Olá *Pharma de vendas de ProjectForcast* escopo do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1ff63-146">hello following example grants hello *Virtual Machine Contributor* role too*samert@aaddemo.com* user at hello *Pharma-Sales-ProjectForcast* resource group scope.</span></span>

![Linha de comando do RBAC do Azure – criação de atribuição de funções do Azure por usuário – captura de tela](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a><span data-ttu-id="1ff63-148">Atribua um grupo de tooa de função no escopo do recurso Olá</span><span class="sxs-lookup"><span data-stu-id="1ff63-148">Assign a role tooa group at hello resource scope</span></span>
<span data-ttu-id="1ff63-149">tooassign um grupo de tooa de função no escopo do recurso hello, use:</span><span class="sxs-lookup"><span data-stu-id="1ff63-149">tooassign a role tooa group at hello resource scope, use:</span></span>

    azure role assignment create --objectId <group id> --role "<name of role>" --resource-name <resource group name> --resource-type <resource group type> --parent <resource group parent> --resource-group <resource group>

<span data-ttu-id="1ff63-150">Olá, exemplo a seguir concede Olá *colaborador da máquina Virtual* função tooan *AD do Azure* grupo um *sub-rede*.</span><span class="sxs-lookup"><span data-stu-id="1ff63-150">hello following example grants hello *Virtual Machine Contributor* role tooan *Azure AD* group on a *subnet*.</span></span>

![Linha de comando do Azure RBAC – criação de atribuição de funções do Azure por grupo – captura de tela](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-4.png)

## <a name="remove-access"></a><span data-ttu-id="1ff63-152">Remover acesso</span><span class="sxs-lookup"><span data-stu-id="1ff63-152">Remove access</span></span>
<span data-ttu-id="1ff63-153">tooremove uma atribuição de função, use:</span><span class="sxs-lookup"><span data-stu-id="1ff63-153">tooremove a role assignment, use:</span></span>

    azure role assignment delete --objectId <object id toofrom which tooremove role> --roleName "<role name>"

<span data-ttu-id="1ff63-154">Olá, exemplo a seguir remove Olá *colaborador da máquina Virtual* atribuição de função de saudação  *sammert@aaddemo.com*  usuário Olá *Pharma de vendas de ProjectForcast* grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1ff63-154">hello following example removes hello *Virtual Machine Contributor* role assignment from hello *sammert@aaddemo.com* user on hello *Pharma-Sales-ProjectForcast* resource group.</span></span>
<span data-ttu-id="1ff63-155">exemplo Hello, em seguida, remove a atribuição de função de saudação de um grupo na assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ff63-155">hello example then removes hello role assignment from a group on hello subscription.</span></span>

![Linha de comando do Azure RBAC  - exclusão de atribuição de funções do azure - captura de tela](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-assignment-delete.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="1ff63-157">Criar uma função personalizada</span><span class="sxs-lookup"><span data-stu-id="1ff63-157">Create a custom role</span></span>
<span data-ttu-id="1ff63-158">toocreate uma função personalizada, use:</span><span class="sxs-lookup"><span data-stu-id="1ff63-158">toocreate a custom role, use:</span></span>

    azure role create --inputfile <file path>

<span data-ttu-id="1ff63-159">Olá, exemplo a seguir cria uma função personalizada chamada *operador de máquina Virtual*.</span><span class="sxs-lookup"><span data-stu-id="1ff63-159">hello following example creates a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="1ff63-160">Esta função personalizada que concede acesso tooall ler as operações de *Microsoft. Compute*, *Microsoft*, e *Network* provedores e concede acesso a recursos toostart, reiniciar e monitorar as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="1ff63-160">This custom role grants access tooall read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access toostart, restart, and monitor virtual machines.</span></span> <span data-ttu-id="1ff63-161">Essa função personalizada pode ser usada em duas assinaturas.</span><span class="sxs-lookup"><span data-stu-id="1ff63-161">This custom role can be used in two subscriptions.</span></span> <span data-ttu-id="1ff63-162">Este exemplo utiliza um arquivo JSON como entrada.</span><span class="sxs-lookup"><span data-stu-id="1ff63-162">This example uses a JSON file as an input.</span></span>

![JSON - definição de função personalizada - captura de tela](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-1.png)

![Linha de comando do Azure RBAC  - criação de função do azure - captura de tela](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-2.png)

## <a name="modify-a-custom-role"></a><span data-ttu-id="1ff63-165">Modificar uma função personalizada</span><span class="sxs-lookup"><span data-stu-id="1ff63-165">Modify a custom role</span></span>
<span data-ttu-id="1ff63-166">toomodify uma função personalizada, primeiro use Olá `azure role show` comando tooretrieve definição de função.</span><span class="sxs-lookup"><span data-stu-id="1ff63-166">toomodify a custom role, first use hello `azure role show` command tooretrieve role definition.</span></span> <span data-ttu-id="1ff63-167">Em seguida, verifique o arquivo de definição de função do hello alterações desejadas toohello.</span><span class="sxs-lookup"><span data-stu-id="1ff63-167">Second, make hello desired changes toohello role definition file.</span></span> <span data-ttu-id="1ff63-168">Por fim, use `azure role set` toosave Olá modificou a definição de função.</span><span class="sxs-lookup"><span data-stu-id="1ff63-168">Finally, use `azure role set` toosave hello modified role definition.</span></span>

    azure role set --inputfile <file path>

<span data-ttu-id="1ff63-169">Olá, exemplo a seguir adiciona Olá *Microsoft.Insights/diagnosticSettings/* operação toohello **ações**e uma assinatura do Azure toohello **AssignableScopes**Olá Máquina Virtual personalizada da função de operador.</span><span class="sxs-lookup"><span data-stu-id="1ff63-169">hello following example adds hello *Microsoft.Insights/diagnosticSettings/* operation toohello **Actions**, and an Azure subscription toohello **AssignableScopes** of hello Virtual Machine Operator custom role.</span></span>

![JSON - modificar definição de função personalizada - captura de tela](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set-1.png)

![Linha de comando do Azure RBAC  - conjunto de funções do azure - captura de tela](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set2.png)

## <a name="delete-a-custom-role"></a><span data-ttu-id="1ff63-172">Excluir uma função personalizada</span><span class="sxs-lookup"><span data-stu-id="1ff63-172">Delete a custom role</span></span>
<span data-ttu-id="1ff63-173">toodelete uma função personalizada, primeiro use Olá `azure role show` saudação do comando toodetermine **ID** da função hello.</span><span class="sxs-lookup"><span data-stu-id="1ff63-173">toodelete a custom role, first use hello `azure role show` command toodetermine hello **ID** of hello role.</span></span> <span data-ttu-id="1ff63-174">Em seguida, use Olá `azure role delete` função de saudação do comando toodelete especificando Olá **ID**.</span><span class="sxs-lookup"><span data-stu-id="1ff63-174">Then, use hello `azure role delete` command toodelete hello role by specifying hello **ID**.</span></span>

<span data-ttu-id="1ff63-175">Olá, exemplo a seguir remove Olá *operador de máquina Virtual* função personalizada.</span><span class="sxs-lookup"><span data-stu-id="1ff63-175">hello following example removes hello *Virtual Machine Operator* custom role.</span></span>

![Linha de comando do Azure RBAC  - exclusão de funções do azure - captura de tela](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-delete.png)

## <a name="list-custom-roles"></a><span data-ttu-id="1ff63-177">Listar funções personalizadas</span><span class="sxs-lookup"><span data-stu-id="1ff63-177">List custom roles</span></span>
<span data-ttu-id="1ff63-178">funções de saudação toolist que estão disponíveis para atribuição a um escopo, usar Olá `azure role list` comando.</span><span class="sxs-lookup"><span data-stu-id="1ff63-178">toolist hello roles that are available for assignment at a scope, use hello `azure role list` command.</span></span>

<span data-ttu-id="1ff63-179">saudação de comando a seguir lista todas as funções que estão disponíveis para atribuição na assinatura de saudação selecionada.</span><span class="sxs-lookup"><span data-stu-id="1ff63-179">hello following command lists all roles that are available for assignment in hello selected subscription.</span></span>

```
azure role list --json | jq '.[] | {"name":.properties.roleName, type:.properties.type}'
```

![Linha de comando do Azure RBAC  - lista de funções do azure - captura de tela](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list1.png)

<span data-ttu-id="1ff63-181">Em Olá exemplo a seguir, Olá *operador de máquina Virtual* função personalizada não está disponível no hello *Production4* assinatura porque a assinatura não está em Olá  **AssignableScopes** da função hello.</span><span class="sxs-lookup"><span data-stu-id="1ff63-181">In hello following example, hello *Virtual Machine Operator* custom role isn’t available in hello *Production4* subscription because that subscription isn’t in hello **AssignableScopes** of hello role.</span></span>

```
azure role list --json | jq '.[] | if .properties.type == "CustomRole" then .properties.roleName else empty end'
```

![Linha de comando do Azure RBAC  - lista de funções do azure para funções personalizadas - captura de tela](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list2.png)

## <a name="next-steps"></a><span data-ttu-id="1ff63-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1ff63-183">Next steps</span></span>
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

