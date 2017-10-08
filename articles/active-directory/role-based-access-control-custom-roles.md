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
# <a name="create-custom-roles-for-azure-role-based-access-control"></a>Criar funções personalizadas para o Controle de Acesso Baseado em Função do Azure
Crie uma função personalizada no acesso de RBAC (controle) se nenhuma das funções internas Olá atender às suas necessidades de acesso específicas. Funções personalizadas podem ser criadas usando [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [Interface de linha de comando do Azure](role-based-access-control-manage-access-azure-cli.md) (CLI) e hello [API REST](role-based-access-control-manage-access-rest.md). Assim como funções internas, você pode atribuir funções personalizadas toousers, grupos e aplicativos na assinatura, no grupo de recursos e escopos do recurso. As funções personalizadas são armazenadas em um locatário do Azure AD e podem ser compartilhadas entre assinaturas.

Cada locatário pode criar funções personalizadas too2000. 

Olá, exemplo a seguir mostra uma função personalizada para monitoramento e reiniciar as máquinas virtuais:

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
## <a name="actions"></a>Ações
Olá **ações** propriedade de uma função personalizada especifica hello Azure operações toowhich Olá função concede acesso. É uma coleção de cadeias de operação que identificam as operações protegíveis dos provedores de recursos do Azure. Cadeias de caracteres de operação seguem o formato de saudação do `Microsoft.<ProviderName>/<ChildResourceType>/<action>`. Cadeias de caracteres de operação que contêm caracteres curinga (\*) conceder acesso a operações tooall que correspondem a cadeia de caracteres de operação de saudação. Por exemplo:

* `*/read`concede acesso a operações tooread para todos os tipos de recursos de todos os provedores de recursos do Azure.
* `Microsoft.Compute/*`concede acesso a operações de tooall para todos os tipos de recursos no provedor de recursos Microsoft. Compute hello.
* `Microsoft.Network/*/read`concede acesso a operações de tooread para todos os tipos de recursos no provedor de recursos Microsoft. Network saudação do Azure.
* `Microsoft.Compute/virtualMachines/*`concede acesso tooall operações de máquinas virtuais e seus tipos de recursos filho.
* `Microsoft.Web/sites/restart/Action`concede acesso toorestart sites.

Use `Get-AzureRmProviderOperation` (no PowerShell) ou `azure provider operations show` (no Azure CLI) operações toolist de provedores de recursos do Azure. Você também pode usar esses comandos tooverify que uma cadeia de caracteres de operação é válida e cadeias de caracteres de operação de curinga tooexpand.

```
Get-AzureRMProviderOperation Microsoft.Compute/virtualMachines/*/action | FT Operation, OperationName

Get-AzureRMProviderOperation Microsoft.Network/*
```

![PowerShell screenshot - Get-AzureRMProviderOperation](./media/role-based-access-control-configure/1-get-azurermprovideroperation-1.png)

```
azure provider operations show "Microsoft.Compute/virtualMachines/*/action" --js on | jq '.[] | .operation'

azure provider operations show "Microsoft.Network/*"
```

![Captura de tela da CLI do Azure – as operações do provedor do Azure mostram "Microsoft.Compute/virtualMachines/\*/action" ](./media/role-based-access-control-configure/1-azure-provider-operations-show.png)

## <a name="notactions"></a>NotActions
Saudação de uso **NotActions** propriedade se o conjunto de saudação de operações que você deseja tooallow é definido mais facilmente excluindo operações restritas. Olá acesso concedido por uma função personalizada é calculado pela subtração Olá **NotActions** operações de saudação **ações** operações.

> [!NOTE]
> Se um usuário é atribuído a uma função que exclui uma operação em **NotActions**e é atribuído a uma segunda função que concede acesso toohello mesma operação, o usuário Olá é permitido tooperform essa operação. **NotActions** não é uma negação de regra – é simplesmente uma maneira conveniente de toocreate um conjunto de operações permitidas quando precisam de operações específicas toobe excluído.
>
>

## <a name="assignablescopes"></a>AssignableScopes
Olá **AssignableScopes** propriedade de função personalizada Olá Especifica escopos hello (assinaturas, grupos de recursos ou recursos) no qual Olá função personalizada está disponível para a atribuição. Você pode fazer disponíveis para atribuição de função personalizada Olá em assinaturas de saudação apenas ou grupos de recursos que exigem e não o usuário desordem experiência para o restante de saudação de assinaturas de saudação ou grupos de recursos.

Exemplos de escopos válidos que podem ser atribuídos incluem:

* "assinaturas/c276fc76-9cd4-44c9-99a7-4fd71546436e", "assinaturas/e91d47c4-76f3-4271-a796-21b4ecfe3624" - torna a função hello disponíveis para atribuição em duas assinaturas.
* "assinaturas/c276fc76-9cd4-44c9-99a7-4fd71546436e" - torna a função hello disponíveis para atribuição em uma única assinatura.
* "/ assinaturas c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/rede /" - torna Olá função disponível para atribuição apenas no grupo de recursos de rede de saudação.

> [!NOTE]
> Você deve usar pelo menos uma assinatura, grupo de recursos ou ID de recurso.
>
>

## <a name="custom-roles-access-control"></a>Controle de acesso de funções personalizadas
Olá **AssignableScopes** propriedade de função personalizada Olá também controla quem pode exibir, modificar e excluir a função hello.

* Quem pode criar uma função personalizada?
    Os Proprietários (e os Administradores de acesso do usuário) de assinaturas, grupos de recursos e recursos podem criar funções personalizadas para uso nesses escopos.
    Olá, criar função de saudação do usuário precisa tooperform capaz de toobe `Microsoft.Authorization/roleDefinition/write` operação em todos os Olá **AssignableScopes** da função hello.
* Quem pode modificar uma função personalizada?
    Os Proprietários (e os Administradores de acesso do usuário) de assinaturas, grupos de recursos e recursos podem modificar funções personalizadas nesses escopos. Os usuários precisam toobe tooperform capaz de saudação `Microsoft.Authorization/roleDefinition/write` operação em todos os Olá **AssignableScopes** de uma função personalizada.
* Quem pode exibir funções personalizadas?
    Todas as funções internas no RBAC do Azure permitem a visualização de funções disponíveis para atribuição. Os usuários que podem executar Olá `Microsoft.Authorization/roleDefinition/read` operação em um escopo pode exibir funções RBAC Olá que estão disponíveis para atribuição nesse escopo.

## <a name="see-also"></a>Consulte também
* [Controle de acesso baseado em função](role-based-access-control-configure.md): Introdução ao RBAC em Olá portal do Azure.
* Saiba como toomanage acessar com:
  * [PowerShell](role-based-access-control-manage-access-powershell.md)
  * [CLI do Azure](role-based-access-control-manage-access-azure-cli.md)
  * [API REST](role-based-access-control-manage-access-rest.md)
* [Funções internas](role-based-access-built-in-roles.md): obter detalhes sobre as funções hello incluídos por padrão em RBAC.
