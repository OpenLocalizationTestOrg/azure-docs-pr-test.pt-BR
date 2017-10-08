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
# <a name="manage-role-based-access-control-with-azure-powershell"></a>Gerenciar o Controle de Acesso baseado em função com o Azure PowerShell
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [CLI do Azure](role-based-access-control-manage-access-azure-cli.md)
> * [API REST](role-based-access-control-manage-access-rest.md)

Você pode usar o controle de acesso baseado em função (RBAC) na Olá portal do Azure e uma API de gerenciamento de recursos do Azure toomanage acesso tooyour assinatura em um nível granular. Com esse recurso, você pode conceder acesso para usuários, grupos ou entidades de serviço do Active Directory, atribuindo toothem algumas funções em um escopo específico.

Antes de usar PowerShell toomanage RBAC, você precisa Olá pré-requisitos a seguir:

* PowerShell do Azure, versão 0.8.8 ou posterior. versão mais recente do tooinstall hello e associe-o com sua assinatura do Azure, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).
* Cmdlets do Azure Resource Manager. Instalar Olá [cmdlets do Azure Resource Manager](/powershell/azure/overview) no PowerShell.

## <a name="list-roles"></a>Listar funções
### <a name="list-all-available-roles"></a>Relacionar todas as funções disponíveis
funções RBAC toolist que estão disponíveis para atribuição e tooinspect Olá operações toowhich eles conceder acesso, use `Get-AzureRmRoleDefinition`.

```
Get-AzureRmRoleDefinition | FT Name, Description
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - captura de tela](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition1.png)

### <a name="list-actions-of-a-role"></a>Relacionar ações de uma função
ações de saudação toolist para uma função específica, use `Get-AzureRmRoleDefinition <role name>`.

```
Get-AzureRmRoleDefinition Contributor | FL Actions, NotActions

(Get-AzureRmRoleDefinition "Virtual Machine Contributor").Actions
```

![RBAC PowerShell - Get-AzureRmRoleDefinition para uma função específica - captura de tela](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition2.png)

## <a name="see-who-has-access"></a>Veja quem tem acesso
atribuições de acesso RBAC toolist, use `Get-AzureRmRoleAssignment`.

### <a name="list-role-assignments-at-a-specific-scope"></a>Listar as atribuições de função em um escopo específico
Você pode ver todas as atribuições de acesso de saudação de uma assinatura especificada, o grupo de recursos ou o recurso. Por exemplo, toosee Olá todas as atribuições de saudação ativo para um grupo de recursos, use `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.

```
Get-AzureRmRoleAssignment -ResourceGroupName Pharma-Sales-ProjectForcast | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - Get-AzureRmRoleAssignment para um grupo de recursos - captura de tela](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment1.png)

### <a name="list-roles-assigned-tooa-user"></a>Listar funções tooa usuário atribuídas
toolist todas as funções hello atribuídos tooa especificado usuário e funções de saudação que são atribuídas a grupos de toohello toowhich Olá usuário pertence, use `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.

```
Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com | FL DisplayName, RoleDefinitionName, Scope

Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com -ExpandPrincipalGroups | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - Get-AzureRmRoleAssignment para um usuário - captura de tela](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment2.png)

### <a name="list-classic-service-administrator-and-coadmin-role-assignments"></a>Listar atribuições de função de administrador e coadministrador de serviços clássicos
atribuições de acesso de toolist para o administrador de assinatura clássico hello e coadministrators, use:

    Get-AzureRmRoleAssignment -IncludeClassicAdministrators

## <a name="grant-access"></a>Conceder acesso
### <a name="search-for-object-ids"></a>Pesquisar IDs de objeto
tooassign uma função, você precisa tooidentify objeto hello (usuário, grupo ou aplicativo) e o escopo de saudação.

Se você não souber a ID da assinatura hello, você pode ser encontrado no hello **assinaturas** folha no hello portal do Azure. toolearn como tooquery Olá ID da assinatura, consulte [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) no MSDN.

ID de objeto tooget Olá para um grupo do AD do Azure, use:

    Get-AzureRmADGroup -SearchString <group name in quotes>

ID de objeto tooget Olá para uma entidade de serviço do AD do Azure ou o aplicativo, use:

    Get-AzureRmADServicePrincipal -SearchString <service name in quotes>

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a>Atribuir um aplicativo de tooan de função no escopo de assinatura Olá
aplicativo de tooan toogrant acesso no escopo de assinatura hello, use:

    New-AzureRmRoleAssignment -ObjectId <application id> -RoleDefinitionName <role name> -Scope <subscription id>

![RBAC PowerShell - New-AzureRmRoleAssignment - captura de tela](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a>Atribuir um usuário de tooa de função no escopo do grupo de recursos de saudação
usuário de tooa toogrant acesso no escopo de grupo de recursos do hello, use:

    New-AzureRmRoleAssignment -SignInName <email of user> -RoleDefinitionName <role name in quotes> -ResourceGroupName <resource group name>

![RBAC PowerShell - New-AzureRmRoleAssignment - captura de tela](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a>Atribua um grupo de tooa de função no escopo do recurso Olá
grupo de tooa toogrant acesso no escopo do recurso hello, use:

    New-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name in quotes> -ResourceName <resource name> -ResourceType <resource type> -ParentResource <parent resource> -ResourceGroupName <resource group name>

![RBAC PowerShell - New-AzureRmRoleAssignment - captura de tela](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment4.png)

## <a name="remove-access"></a>Remover acesso
tooremove acesso para usuários, grupos e aplicativos, use:

    Remove-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name> -Scope <scope such as subscription id>

![RBAC PowerShell - Remove-AzureRmRoleAssignment - captura de tela](./media/role-based-access-control-manage-access-powershell/3-remove-azure-rm-role-assignment.png)

## <a name="create-a-custom-role"></a>Criar uma função personalizada
toocreate uma função personalizada, use Olá ```New-AzureRmRoleDefinition``` comando. Há dois métodos de estruturação função hello, usando PSRoleDefinitionObject ou um modelo JSON. 

## <a name="get-actions-for-a-resource-provider"></a>Obter ações para um provedor de recursos
Ao criar funções personalizadas do zero, é importante tooknow todos Olá possíveis operações Olá de provedores de recursos.
Saudação de uso ```Get-AzureRMProviderOperation``` comando tooget essas informações.
Por exemplo, se você quiser toocheck todas as operações de saudação disponíveis para a máquina virtual usam este comando:

```
Get-AzureRMProviderOperation "Microsoft.Compute/virtualMachines/*" | FT OperationName, Operation , Description -AutoSize
```

### <a name="create-role-with-psroledefinitionobject"></a>Criar função com PSRoleDefinitionObject
Quando você usar o PowerShell toocreate uma função personalizada, você pode começar do zero ou usar uma saudação [funções internas](role-based-access-built-in-roles.md) como um ponto de partida. exemplo Hello nesta seção começa com uma função interna e, em seguida, personaliza-lo com mais privilégios. Editar saudação do hello atributos tooadd *ações*, *notActions*, ou *escopos* desejado e, em seguida, salvar alterações de saudação como uma nova função.

Olá exemplo a seguir inicia com hello *colaborador da máquina Virtual* função e usa esse toocreate uma função personalizada chamada *operador de máquina Virtual*. nova função de saudação concede acesso tooall ler as operações de *Microsoft. Compute*, *Microsoft*, e *Network* provedores e concede acesso a recursos toostart, reiniciar e monitorar as máquinas virtuais. função personalizada Olá pode ser usada em duas assinaturas.

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

### <a name="create-role-with-json-template"></a>Criar função com modelo JSON
Um modelo JSON pode ser usado como definição de fonte de saudação de função personalizada hello. Olá, exemplo a seguir cria uma função personalizada que permite acesso de leitura toostorage e recursos de computação, acessar toosupport e adiciona a função tootwo assinaturas. Criar um novo arquivo `C:\CustomRoles\customrole1.json` com hello exemplo a seguir. Olá Id deve ser definido muito`null` na criação de função inicial como uma nova ID é gerada automaticamente. 

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
tooadd Olá função toohello assinaturas, executadas Olá comando PowerShell a seguir:
```
New-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="modify-a-custom-role"></a>Modificar uma função personalizada
Toocreating semelhante uma função personalizada, você pode modificar uma função personalizada existente usando Olá PSRoleDefinitionObject ou um modelo JSON.

### <a name="modify-role-with-psroledefinitionobject"></a>Modificar função com PSRoleDefinitionObject
toomodify uma função personalizada, primeiro, use Olá `Get-AzureRmRoleDefinition` tooretrieve Olá função definição de comando. Em seguida, fazer alterações de saudação desejada toohello definição de função. Por fim, use Olá `Set-AzureRmRoleDefinition` saudação do comando toosave modificou a definição de função.

Olá, exemplo a seguir adiciona Olá `Microsoft.Insights/diagnosticSettings/*` operação toohello *operador de máquina Virtual* função personalizada.

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.Actions.Add("Microsoft.Insights/diagnosticSettings/*")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - captura de tela](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-1.png)

Olá, exemplo a seguir adiciona um escopos atribuíveis de toohello de assinatura do Azure de saudação *operador de máquina Virtual* função personalizada.

```
Get-AzureRmSubscription - SubscriptionName Production3

$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.AssignableScopes.Add("/subscriptions/34370e90-ac4a-4bf9-821f-85eeedead1a2")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - captura de tela](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-2.png)

### <a name="modify-role-with-json-template"></a>Modificar função com modelo JSON
Usando o modelo anterior de JSON Olá, você pode modificar um tooadd de função personalizada existente ou remover facilmente ações. Atualizar o modelo JSON hello e adicionar ação de leitura de saudação de rede, conforme mostrado no exemplo a seguir de saudação. definições de saudação listadas no modelo de saudação não são definição existente de tooan cumulativamente aplicado, que significa que essa função hello aparece exatamente como você especificar no modelo de saudação. Também é necessário o campo de Id de saudação tooupdate com a ID de saudação da função hello. Se você não tiver certeza de que esse valor é, você pode usar o hello `Get-AzureRmRoleDefinition` tooget cmdlet essas informações.

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

função existente de saudação do tooupdate executar Olá comando PowerShell a seguir:
```
Set-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="delete-a-custom-role"></a>Excluir uma função personalizada
toodelete uma função personalizada, use Olá `Remove-AzureRmRoleDefinition` comando.

Olá, exemplo a seguir remove Olá *operador de máquina Virtual* função personalizada.

```
Get-AzureRmRoleDefinition "Virtual Machine Operator"

Get-AzureRmRoleDefinition "Virtual Machine Operator" | Remove-AzureRmRoleDefinition
```

![RBAC PowerShell - Remove-AzureRmRoleDefinition - captura de tela](./media/role-based-access-control-manage-access-powershell/4-remove-azurermroledefinition.png)

## <a name="list-custom-roles"></a>Listar funções personalizadas
funções de saudação toolist que estão disponíveis para atribuição a um escopo, usar Olá `Get-AzureRmRoleDefinition` comando.

saudação de exemplo a seguir lista todas as funções que estão disponíveis para atribuição na assinatura de saudação selecionada.

```
Get-AzureRmRoleDefinition | FT Name, IsCustom
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - captura de tela](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition-1.png)

Em Olá exemplo a seguir, Olá *operador de máquina Virtual* função personalizada não está disponível no hello *Production4* assinatura porque a assinatura não está em Olá  **AssignableScopes** da função hello.

![RBAC PowerShell - Get-AzureRmRoleDefinition - captura de tela](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition2.png)

## <a name="see-also"></a>Consulte também
* [Usando o Azure PowerShell com o Azure Resource Manager](../powershell-azure-resource-manager.md)
  [!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

