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
# <a name="manage-role-based-access-control-with-hello-azure-command-line-interface"></a>Gerenciar o controle de acesso baseado em função com hello interface de linha de comando do Azure
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [CLI do Azure](role-based-access-control-manage-access-azure-cli.md)
> * [API REST](role-based-access-control-manage-access-rest.md)


Você pode usar o controle de acesso baseado em função (RBAC) em hello portal do Azure e assinatura do Azure Resource Manager API toomanage acesso tooyour e recursos em um nível granular. Com esse recurso, você pode conceder acesso para usuários, grupos ou entidades de serviço do Active Directory, atribuindo toothem algumas funções em um escopo específico.

Antes de usar toomanage de interface de linha de comando (CLI) do Azure Olá RBAC, você deve ter Olá pré-requisitos a seguir:

* CLI do Azure versão 0.8.8 ou posterior. versão mais recente do tooinstall hello e associe-o com sua assinatura do Azure, consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md).
* Azure Resource Manager na Azure CLI. Vá muito[usando Olá CLI do Azure com o Gerenciador de recursos de hello](../xplat-cli-azure-resource-manager.md) para obter mais detalhes.

## <a name="list-roles"></a>Listar funções
### <a name="list-all-available-roles"></a>Relacionar todas as funções disponíveis
toolist todas as funções disponíveis, use:

        azure role list

Olá, exemplo a seguir mostra a lista de saudação do *todas as funções disponíveis*.

```
azure role list --json | jq '.[] | {"roleName":.properties.roleName, "description":.properties.description}'
```

![Linha de comando do Azure RBAC  - lista de funções do azure - captura de tela](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-list.png)

### <a name="list-actions-of-a-role"></a>Relacionar ações de uma função
ações de saudação toolist de uma função, use:

    azure role show "<role name>"

Olá, exemplo a seguir mostra as ações de saudação do hello *Colaborador* e *colaborador da máquina Virtual* funções.

```
azure role show "contributor" --json | jq '.[] | {"Actions":.properties.permissions[0].actions,"NotActions":properties.permissions[0].notActions}'

azure role show "virtual machine contributor" --json | jq '.[] | .properties.permissions[0].actions'
```

![Linha de comando do Azure RBAC  - exibição de funções do azure - captura de tela](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-show.png)

## <a name="list-access"></a>Relacionar acesso
### <a name="list-role-assignments-effective-on-a-resource-group"></a>Relacionar as atribuições de função como efetivas em um grupo de recursos
toolist Olá atribuições de função que existem em um grupo de recursos, use:

    azure role assignment list --resource-group <resource group name>

Olá exemplo a seguir mostra as atribuições de função hello em Olá *pharma de vendas de projecforcast* grupo.

```
azure role assignment list --resource-group pharma-sales-projecforcast --json | jq '.[] | {"DisplayName":.properties.aADObject.displayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Linha de comando do RBAC do Azure – lista de atribuição de funções do Azure por grupo – captura de tela](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-1.png)

### <a name="list-role-assignments-for-a-user"></a>Listar as atribuições de função de um usuário
atribuições de função toolist Olá para um usuário específico e atribuições de saudação que são atribuídas a grupos de usuários tooa, use:

    azure role assignment list --signInName <user email>

Você também pode ver as atribuições de função são herdadas de grupos, modificando o comando hello:

    azure role assignment list --expandPrincipalGroups --signInName <user email>

Olá, exemplo a seguir mostra as atribuições de função de saudação que recebem toohello  *sameert@aaddemo.com*  usuário. Isso inclui funções que são atribuídas diretamente toohello usuário e que são herdadas de grupos.

```
azure role assignment list --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'

azure role assignment list --expandPrincipalGroups --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Linha de comando do Azure RBAC  - lista de atribuição de funções do azure por usuário - captura de tela](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-2.png)

## <a name="grant-access"></a>Conceder acesso
acesso de toogrant depois de ter identificado a função hello que você deseja tooassign, use:

    azure role assignment create

### <a name="assign-a-role-toogroup-at-hello-subscription-scope"></a>Atribuir um toogroup de função no escopo de assinatura Olá
tooassign um grupo de tooa de função no escopo de assinatura hello, use:

    azure role assignment create --objectId  <group object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

Olá, exemplo a seguir atribui Olá *leitor* função muito*equipe de Christine Koch* em Olá *assinatura* escopo.

![Linha de comando do Azure RBAC – criação de atribuição de funções do Azure por grupo – captura de tela](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-1.png)

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a>Atribuir um aplicativo de tooan de função no escopo de assinatura Olá
tooassign um aplicativo de tooan de função no escopo de assinatura hello, use:

    azure role assignment create --objectId  <applications object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

Olá, exemplo a seguir concede Olá *Colaborador* função tooan *AD do Azure* aplicativo hello selecionado assinatura.

 ![Linha de comando do Azure RBAC  - criação de atribuição de funções do azure por aplicativo](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a>Atribuir um usuário de tooa de função no escopo do grupo de recursos de saudação
tooassign um usuário de tooa de função no escopo de grupo de recursos do hello, use:

    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>

Olá, exemplo a seguir concede Olá *colaborador da máquina Virtual* função muito *samert@aaddemo.com*  usuário Olá *Pharma de vendas de ProjectForcast* escopo do grupo de recursos.

![Linha de comando do RBAC do Azure – criação de atribuição de funções do Azure por usuário – captura de tela](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a>Atribua um grupo de tooa de função no escopo do recurso Olá
tooassign um grupo de tooa de função no escopo do recurso hello, use:

    azure role assignment create --objectId <group id> --role "<name of role>" --resource-name <resource group name> --resource-type <resource group type> --parent <resource group parent> --resource-group <resource group>

Olá, exemplo a seguir concede Olá *colaborador da máquina Virtual* função tooan *AD do Azure* grupo um *sub-rede*.

![Linha de comando do Azure RBAC – criação de atribuição de funções do Azure por grupo – captura de tela](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-4.png)

## <a name="remove-access"></a>Remover acesso
tooremove uma atribuição de função, use:

    azure role assignment delete --objectId <object id toofrom which tooremove role> --roleName "<role name>"

Olá, exemplo a seguir remove Olá *colaborador da máquina Virtual* atribuição de função de saudação  *sammert@aaddemo.com*  usuário Olá *Pharma de vendas de ProjectForcast* grupo de recursos.
exemplo Hello, em seguida, remove a atribuição de função de saudação de um grupo na assinatura de saudação.

![Linha de comando do Azure RBAC  - exclusão de atribuição de funções do azure - captura de tela](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-assignment-delete.png)

## <a name="create-a-custom-role"></a>Criar uma função personalizada
toocreate uma função personalizada, use:

    azure role create --inputfile <file path>

Olá, exemplo a seguir cria uma função personalizada chamada *operador de máquina Virtual*. Esta função personalizada que concede acesso tooall ler as operações de *Microsoft. Compute*, *Microsoft*, e *Network* provedores e concede acesso a recursos toostart, reiniciar e monitorar as máquinas virtuais. Essa função personalizada pode ser usada em duas assinaturas. Este exemplo utiliza um arquivo JSON como entrada.

![JSON - definição de função personalizada - captura de tela](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-1.png)

![Linha de comando do Azure RBAC  - criação de função do azure - captura de tela](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-2.png)

## <a name="modify-a-custom-role"></a>Modificar uma função personalizada
toomodify uma função personalizada, primeiro use Olá `azure role show` comando tooretrieve definição de função. Em seguida, verifique o arquivo de definição de função do hello alterações desejadas toohello. Por fim, use `azure role set` toosave Olá modificou a definição de função.

    azure role set --inputfile <file path>

Olá, exemplo a seguir adiciona Olá *Microsoft.Insights/diagnosticSettings/* operação toohello **ações**e uma assinatura do Azure toohello **AssignableScopes**Olá Máquina Virtual personalizada da função de operador.

![JSON - modificar definição de função personalizada - captura de tela](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set-1.png)

![Linha de comando do Azure RBAC  - conjunto de funções do azure - captura de tela](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set2.png)

## <a name="delete-a-custom-role"></a>Excluir uma função personalizada
toodelete uma função personalizada, primeiro use Olá `azure role show` saudação do comando toodetermine **ID** da função hello. Em seguida, use Olá `azure role delete` função de saudação do comando toodelete especificando Olá **ID**.

Olá, exemplo a seguir remove Olá *operador de máquina Virtual* função personalizada.

![Linha de comando do Azure RBAC  - exclusão de funções do azure - captura de tela](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-delete.png)

## <a name="list-custom-roles"></a>Listar funções personalizadas
funções de saudação toolist que estão disponíveis para atribuição a um escopo, usar Olá `azure role list` comando.

saudação de comando a seguir lista todas as funções que estão disponíveis para atribuição na assinatura de saudação selecionada.

```
azure role list --json | jq '.[] | {"name":.properties.roleName, type:.properties.type}'
```

![Linha de comando do Azure RBAC  - lista de funções do azure - captura de tela](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list1.png)

Em Olá exemplo a seguir, Olá *operador de máquina Virtual* função personalizada não está disponível no hello *Production4* assinatura porque a assinatura não está em Olá  **AssignableScopes** da função hello.

```
azure role list --json | jq '.[] | if .properties.type == "CustomRole" then .properties.roleName else empty end'
```

![Linha de comando do Azure RBAC  - lista de funções do azure para funções personalizadas - captura de tela](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list2.png)

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

