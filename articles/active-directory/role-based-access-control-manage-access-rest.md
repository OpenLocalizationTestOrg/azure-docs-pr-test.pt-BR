---
title: Controle de acesso baseado em aaaRole com REST - AD do Azure | Microsoft Docs
description: "Gerenciando o controle de acesso baseado em função com hello API REST"
services: active-directory
documentationcenter: na
author: andredm7
manager: femila
editor: 
ms.assetid: 1f90228a-7aac-4ea7-ad82-b57d222ab128
ms.service: active-directory
ms.workload: multiple
ms.tgt_pltfrm: rest-api
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: andredm
ms.openlocfilehash: ccd402fd4fe4583288076cac23753dd067694681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-hello-rest-api"></a>Gerenciar o controle de acesso baseado em função com hello API REST
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [CLI do Azure](role-based-access-control-manage-access-azure-cli.md)
> * [API REST](role-based-access-control-manage-access-rest.md)

Baseado em função RBAC controle de acesso () em Olá portal do Azure e API do Gerenciador de recursos do Azure ajuda a gerenciar o acesso tooyour assinatura e recursos em um nível granular. Com esse recurso, você pode conceder acesso para usuários, grupos ou entidades de serviço do Active Directory, atribuindo toothem algumas funções em um escopo específico.

## <a name="list-all-role-assignments"></a>Lista todas as atribuições de função
Lista todas as atribuições de função hello em Olá especificado escopo e subscopes.

atribuições de função toolist, você deve ter acesso muito`Microsoft.Authorization/roleAssignments/read` operação no escopo de saudação. Todas as funções internas de saudação recebem acesso toothis operação. Para saber mais sobre as atribuições de função e o gerenciamento de acesso para recursos do Azure, consulte [Controle de Acesso Baseado em Função do Azure](role-based-access-control-configure.md).

### <a name="request"></a>Solicitação
Saudação de uso **obter** método com hello URI a seguir:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments?api-version={api-version}&$filter={filter}

Dentro de Olá URI, verifique Olá toocustomize substituições a seguir sua solicitação:

1. Substituir *{scope}* com escopo Olá para o qual você deseja toolist atribuições de função hello. Olá exemplos a seguir mostra como toospecify Olá escopo para os diferentes níveis:

   * Assinatura: /subscriptions/{subscription-id}  
   * Grupo de Recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Substitua *{api-version}* por 2015-07-01.
3. Substituir *{filter}* com a condição de saudação que desejar que a lista de atribuições de função do tooapply toofilter hello:

   * Lista de atribuições de função para apenas Olá especificado escopo, não incluindo atribuições de função hello subscopes:`atScope()`    
   * Liste atribuições de função para um usuário, grupo ou aplicativo específico: `principalId%20eq%20'{objectId of user, group, or service principal}'`  
   * Liste atribuições de função para um usuário específico, incluindo aqueles herdados de grupos | `assignedTo('{objectId of user}')`

### <a name="response"></a>Response
Código de status: 200

```
{
  "value": [
    {
      "properties": {
        "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7",
        "principalId": "2f9d4375-cbf1-48e8-83c9-2a0be4cb33fb",
        "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
        "createdOn": "2015-10-08T07:28:24.3905077Z",
        "updatedOn": "2015-10-08T07:28:24.3905077Z",
        "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
        "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/baa6e199-ad19-4667-b768-623fde31aedd",
      "type": "Microsoft.Authorization/roleAssignments",
      "name": "baa6e199-ad19-4667-b768-623fde31aedd"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role-assignment"></a>Obter informações sobre uma atribuição de função
Obtém informações sobre uma única atribuição de função especificada pelo identificador de atribuição de função hello.

tooget informações sobre uma atribuição de função, você deve ter acesso muito`Microsoft.Authorization/roleAssignments/read` operação. Todas as funções internas de saudação recebem acesso toothis operação. Para saber mais sobre as atribuições de função e o gerenciamento de acesso para recursos do Azure, consulte [Controle de Acesso Baseado em Função do Azure](role-based-access-control-configure.md).

### <a name="request"></a>Solicitação
Saudação de uso **obter** método com hello URI a seguir:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

Dentro de Olá URI, verifique Olá toocustomize substituições a seguir sua solicitação:

1. Substituir *{scope}* com escopo Olá para o qual você deseja toolist atribuições de função hello. Olá exemplos a seguir mostra como toospecify Olá escopo para os diferentes níveis:

   * Assinatura: /subscriptions/{subscription-id}  
   * Grupo de Recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Substituir *{role-assignment-id}* com identificador de GUID Olá Olá de atribuição de função.
3. Substitua *{api-version}* por 2015-07-01.

### <a name="response"></a>Response
Código de status: 200

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/b24988ac-6180-42a0-ab88-20f7382dd24c",
    "principalId": "672f1afa-526a-4ef6-819c-975c7cd79022",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "createdOn": "2015-10-05T08:36:26.4014813Z",
    "updatedOn": "2015-10-05T08:36:26.4014813Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/196965ae-6088-4121-a92a-f1e33fdcc73e",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "196965ae-6088-4121-a92a-f1e33fdcc73e"
}

```

## <a name="create-a-role-assignment"></a>Criar uma atribuição de função
Criar uma função de atribuição no hello especificado escopo para Olá especificado função especificado principal de concessão hello.

toocreate uma atribuição de função, você deve ter acesso muito`Microsoft.Authorization/roleAssignments/write` operação. De saudação funções internas, apenas *proprietário* e *administrador de acesso do usuário* recebem acesso toothis operação. Para saber mais sobre as atribuições de função e o gerenciamento de acesso para recursos do Azure, consulte [Controle de Acesso Baseado em Função do Azure](role-based-access-control-configure.md).

### <a name="request"></a>Solicitação
Saudação de uso **colocar** método com hello URI a seguir:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

Dentro de Olá URI, verifique Olá toocustomize substituições a seguir sua solicitação:

1. Substituir *{scope}* com escopo de saudação em que você deseja toocreate atribuições de função hello. Quando você criar uma atribuição de função em um escopo pai, todos os escopos filho herdam Olá mesma atribuição de função. Olá exemplos a seguir mostra como toospecify Olá escopo para os diferentes níveis:

   * Assinatura: /subscriptions/{subscription-id}  
   * Grupo de Recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1   
   * Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Substituir *{role-assignment-id}* com um novo GUID, que se torna o identificador GUID de saudação da nova atribuição de função hello.
3. Substitua *{api-version}* por 2015-07-01.

Corpo da solicitação Olá, fornece valores Olá Olá formato a seguir:

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b"
  }
}

```

| Nome do elemento | Obrigatório | Tipo | Descrição |
| --- | --- | --- | --- |
| roleDefinitionId |Sim |Cadeia de caracteres |Identificador de saudação da função de saudação. formato de saudação do identificador de saudação é:`{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}` |
| principalId |Sim |Cadeia de caracteres |ID do objeto de entidade de saudação do AD do Azure (usuário, grupo ou entidade de serviço) toowhich Olá função é atribuída. |

### <a name="response"></a>Resposta
Código de status: 201

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-16T00:27:19.6447515Z",
    "updatedOn": "2015-12-16T00:27:19.6447515Z",
    "createdBy": null,
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/2e9e86c8-0e91-4958-b21f-20f51f27bab2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "2e9e86c8-0e91-4958-b21f-20f51f27bab2"
}

```

## <a name="delete-a-role-assignment"></a>Excluir uma atribuição de função
Excluir uma atribuição de função em Olá especificado escopo.

toodelete uma atribuição de função, você deve ter acesso toohello `Microsoft.Authorization/roleAssignments/delete` operação. De saudação funções internas, apenas *proprietário* e *administrador de acesso do usuário* recebem acesso toothis operação. Para saber mais sobre as atribuições de função e o gerenciamento de acesso para recursos do Azure, consulte [Controle de Acesso Baseado em Função do Azure](role-based-access-control-configure.md).

### <a name="request"></a>Solicitação
Saudação de uso **excluir** método com hello URI a seguir:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

Dentro de Olá URI, verifique Olá toocustomize substituições a seguir sua solicitação:

1. Substituir *{scope}* com escopo de saudação em que você deseja toocreate atribuições de função hello. Olá exemplos a seguir mostra como toospecify Olá escopo para os diferentes níveis:

   * Assinatura: /subscriptions/{subscription-id}  
   * Grupo de Recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Substituir *{role-assignment-id}* com a id de atribuição de função hello GUID.
3. Substitua *{api-version}* por 2015-07-01.

### <a name="response"></a>Response
Código de status: 200

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-17T23:21:40.8921564Z",
    "updatedOn": "2015-12-17T23:21:40.8921564Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/5eec22ee-ea5c-431e-8f41-82c560706fd2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "5eec22ee-ea5c-431e-8f41-82c560706fd2"
}

```

## <a name="list-all-roles"></a>Lista todas as Funções
Lista todas as funções hello que estão disponíveis para atribuição de saudação especificada escopo.

funções de toolist, você deve ter acesso muito`Microsoft.Authorization/roleDefinitions/read` operação no escopo de saudação. Todas as funções internas de saudação recebem acesso toothis operação. Para saber mais sobre as atribuições de função e o gerenciamento de acesso para recursos do Azure, consulte [Controle de Acesso Baseado em Função do Azure](role-based-access-control-configure.md).

### <a name="request"></a>Solicitação
Saudação de uso **obter** método com hello URI a seguir:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?api-version={api-version}&$filter={filter}

Dentro de Olá URI, verifique Olá toocustomize substituições a seguir sua solicitação:

1. Substituir *{scope}* com escopo Olá para o qual você deseja toolist funções hello. Olá exemplos a seguir mostra como toospecify Olá escopo para os diferentes níveis:

   * Assinatura: /subscriptions/{subscription-id}  
   * Grupo de Recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Substitua *{api-version}* por 2015-07-01.
3. Substituir *{filter}* com a condição de saudação que você deseja tooapply lista de saudação toofilter de funções:

   * Lista de funções disponíveis para atribuição de saudação especificado escopo e qualquer um de seus escopos filhos:`atScopeAndBelow()`
   * Pesquise uma função usando o nome de exibição exato: `roleName%20eq%20'{role-display-name}'`. Formato de nome de exibição exato Olá da função hello codificados da URL de saudação de uso. Por exemplo, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |

### <a name="response"></a>Response
Código de status: 200

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access toothem, and not hello virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role"></a>Obter informações sobre uma Função
Obtém informações sobre uma única função especificada pelo identificador de definição de função hello. tooget informações sobre uma única função usando seu nome de exibição, consulte [liste todas as funções](role-based-access-control-manage-access-rest.md#list-all-roles).

tooget informações sobre uma função, você deve ter acesso muito`Microsoft.Authorization/roleDefinitions/read` operação. Todas as funções internas de saudação recebem acesso toothis operação. Para saber mais sobre as atribuições de função e o gerenciamento de acesso para recursos do Azure, consulte [Controle de Acesso Baseado em Função do Azure](role-based-access-control-configure.md).

### <a name="request"></a>Solicitação
Saudação de uso **obter** método com hello URI a seguir:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

Dentro de Olá URI, verifique Olá toocustomize substituições a seguir sua solicitação:

1. Substituir *{scope}* com escopo Olá para o qual você deseja toolist atribuições de função hello. Olá exemplos a seguir mostra como toospecify Olá escopo para os diferentes níveis:

   * Assinatura: /subscriptions/{subscription-id}  
   * Grupo de Recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Substituir *{id de definição de função}* com identificador de GUID Olá Olá da definição da função.
3. Substitua *{api-version}* por 2015-07-01.

### <a name="response"></a>Response
Código de status: 200

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access toothem, and not hello virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="create-a-custom-role"></a>Criar uma Função personalizada
Criar uma função personalizada.

toocreate uma função personalizada, você deve ter acesso muito`Microsoft.Authorization/roleDefinitions/write` operação em todos os Olá `AssignableScopes`. De saudação funções internas, apenas *proprietário* e *administrador de acesso do usuário* recebem acesso toothis operação. Para saber mais sobre as atribuições de função e o gerenciamento de acesso para recursos do Azure, consulte [Controle de Acesso Baseado em Função do Azure](role-based-access-control-configure.md).

### <a name="request"></a>Solicitação
Saudação de uso **colocar** método com hello URI a seguir:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

Dentro de Olá URI, verifique Olá toocustomize substituições a seguir sua solicitação:

1. Substituir *{scope}* com hello primeiro *AssignableScope* de função personalizada hello. Olá exemplos a seguir mostra como toospecify Olá escopo para os diferentes níveis.

   * Assinatura: /subscriptions/{subscription-id}  
   * Grupo de Recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Substituir *{id de definição de função}* com um novo GUID, que se torna o identificador GUID de saudação da nova função personalizada de saudação.
3. Substitua *{api-version}* por 2015-07-01.

Corpo da solicitação Olá, fornece valores Olá Olá formato a seguir:

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| Nome do elemento | Obrigatório | Tipo | Descrição |
| --- | --- | --- | --- |
| name |Sim |Cadeia de caracteres |Identificador GUID de função personalizada hello. |
| properties.roleName |Sim |Cadeia de caracteres |Exibir o nome da função personalizada hello. Tamanho máximo de 128 caracteres. |
| properties.description |Não |Cadeia de caracteres |Descrição da função de saudação personalizada. Tamanho máximo de 1024 caracteres. |
| properties.type |Sim |Cadeia de caracteres |Definir muito "CustomRole". |
| properties.permissions.actions |Sim |String[] |Uma matriz de ação de cadeias de caracteres especificando operações Olá concedidas pela função personalizada hello. |
| properties.permissions.notActions |Não |String[] |Uma matriz de cadeias de caracteres de ação especificando Olá operações tooexclude de operações de saudação concedido pela função personalizada hello. |
| properties.assignableScopes |Sim |String[] |Uma matriz de escopos que Olá função personalizada pode ser usada. |

### <a name="response"></a>Resposta
Código de status: 201

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="update-a-custom-role"></a>Atualizar uma Função personalizada
Modificar uma função personalizada.

toomodify uma função personalizada, você deve ter acesso muito`Microsoft.Authorization/roleDefinitions/write` operação em todos os Olá `AssignableScopes`. De saudação funções internas, apenas *proprietário* e *administrador de acesso do usuário* recebem acesso toothis operação. Para saber mais sobre as atribuições de função e o gerenciamento de acesso para recursos do Azure, consulte [Controle de Acesso Baseado em Função do Azure](role-based-access-control-configure.md).

### <a name="request"></a>Solicitação
Saudação de uso **colocar** método com hello URI a seguir:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

Dentro de Olá URI, verifique Olá toocustomize substituições a seguir sua solicitação:

1. Substituir *{scope}* com hello primeiro *AssignableScope* de função personalizada hello. Olá exemplos a seguir mostra como toospecify Olá escopo para os diferentes níveis:

   * Assinatura: /subscriptions/{subscription-id}  
   * Grupo de Recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Substituir *{id de definição de função}* com identificador de GUID de saudação de função personalizada hello.
3. Substitua *{api-version}* por 2015-07-01.

Corpo da solicitação Olá, fornece valores Olá Olá formato a seguir:

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| Nome do elemento | Obrigatório | Tipo | Descrição |
| --- | --- | --- | --- |
| name |Sim |Cadeia de caracteres |Identificador GUID de função personalizada hello. |
| properties.roleName |Sim |Cadeia de caracteres |Nome para exibição da saudação atualizado função personalizada. |
| properties.description |Não |Cadeia de caracteres |Descrição da saudação atualizado função personalizada. |
| properties.type |Sim |Cadeia de caracteres |Definir muito "CustomRole". |
| properties.permissions.actions |Sim |String[] |Uma matriz de cadeias de caracteres de ação especificando Olá Olá de toowhich operações atualizada função personalizada que concede acesso. |
| properties.permissions.notActions |Não |String[] |Uma matriz de ação de cadeias de caracteres especificando tooexclude de operações de saudação de operações de saudação quais Olá atualizado concessões de função personalizada. |
| properties.assignableScopes |Sim |String[] |Uma matriz de escopos que Olá atualizada função personalizada pode ser usada. |

### <a name="response"></a>Resposta
Código de status: 201

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="delete-a-custom-role"></a>Excluir uma Função personalizada
Excluir uma função personalizada.

toodelete uma função personalizada, você deve ter acesso muito`Microsoft.Authorization/roleDefinitions/delete` operação em todos os Olá `AssignableScopes`. De saudação funções internas, apenas *proprietário* e *administrador de acesso do usuário* recebem acesso toothis operação. Para saber mais sobre as atribuições de função e o gerenciamento de acesso para recursos do Azure, consulte [Controle de Acesso Baseado em Função do Azure](role-based-access-control-configure.md).

### <a name="request"></a>Solicitação
Saudação de uso **excluir** método com hello URI a seguir:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

Dentro de Olá URI, verifique Olá toocustomize substituições a seguir sua solicitação:

1. Substituir *{scope}* com escopo de saudação que deseja definição de função toodelete hello. Olá exemplos a seguir mostra como toospecify Olá escopo para os diferentes níveis:

   * Assinatura: /subscriptions/{subscription-id}  
   * Grupo de Recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Substituir *{id de definição de função}* com a id de definição de função hello GUID de função personalizada hello.
3. Substitua *{api-version}* por 2015-07-01.

### <a name="response"></a>Response
Código de status: 200

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-16T00:07:02.9236555Z",
    "updatedOn": "2015-12-16T00:07:02.9236555Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/0bd62a70-e1b8-4e0b-a7c2-75cab365c95b",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "0bd62a70-e1b8-4e0b-a7c2-75cab365c95b"
}

```

## <a name="next-steps"></a>Próximas etapas

[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]
