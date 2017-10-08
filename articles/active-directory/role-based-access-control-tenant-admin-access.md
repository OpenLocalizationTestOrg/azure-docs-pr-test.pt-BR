---
title: "administração de aaaTenant elevar o acesso - o AD do Azure | Microsoft Docs"
description: "Este tópico descreve Olá criado nas funções de controle de acesso baseado em função (RBAC)."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: rqureshi
ms.assetid: b547c5a5-2da2-4372-9938-481cb962d2d6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andredm
ms.openlocfilehash: 7996f2af3277dc40e2a1766cc4a7862a2399cdef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a>Elevar o acesso como um administrador de locatários com Controle de Acesso Baseado em Função

O Controle de Acesso Baseado em Função ajuda os administradores de locatários a obter elevações temporárias no acesso para que eles possam conceder permissões mais elevadas que o normal. Um administrador de locatários pode elevar a mesmo toohello função de administrador de acesso do usuário quando necessário. Essa função fornece Olá toogrant de permissões de administrador de locatário por conta própria ou outras funções em Olá escopo "/".

Esse recurso é importante porque ela permite locatário Olá administrador toosee que todos Olá assinaturas que existem em uma organização. Ele também permite tooaccess de aplicativos (como faturamento e auditoria) de automação todas as assinaturas de saudação e fornecer uma exibição precisa do estado de saudação da organização Olá para cobrança ou gerenciamento de ativos.  

## <a name="how-toouse-elevateaccess-toogive-tenant-access"></a>Como o acesso de locatário toouse elevateAccess toogive

processo básico de saudação funciona com hello etapas a seguir:

1. Usando REST, chame *elevateAccess*, que concede a você Olá a função de administrador de acesso do usuário em "/" de escopo.

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. Criar um [atribuição de função](/rest/api/authorization/roleassignments) tooassign qualquer função em qualquer escopo. Olá exemplo a seguir mostra as propriedades Olá para atribuir Olá a função de leitor em "/" de escopo:

    ```
    { "properties":{
    "roleDefinitionId": "providers/Microsoft.Authorization/roleDefinitions/acdd72a7338548efbd42f606fba81ae7",
    "principalId": "cbc5e050-d7cd-4310-813b-4870be8ef5bb",
    "scope": "/"
    },
    "id": "providers/Microsoft.Authorization/roleAssignments/64736CA0-56D7-4A94-A551-973C2FE7888B",
    "type": "Microsoft.Authorization/roleAssignments",
    "name": "64736CA0-56D7-4A94-A551-973C2FE7888B"
    }
    ```

3. Enquanto um Administrador de Acesso do Usuário, você também pode excluir a atribuição de função no escopo "/".

4. Revogue seus privilégios de Administrador de Acesso do Usuário até que sejam necessários novamente.


## <a name="how-tooundo-hello-elevateaccess-action"></a>Como tooundo Olá elevateAccess ação

Quando você chama *elevateAccess* criar uma atribuição de função por conta própria, portanto toorevoke os privilégios que você precisa toodelete Olá atribuição.

1.  Chamar [roleDefinitions GET](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) onde roleName = toodetermine do administrador do acesso de usuário Olá nome GUID da função de administrador de acesso de usuário de saudação. resposta de saudação deve ter esta aparência:

    ```
    {"value":[{"properties":{
    "roleName":"User Access Administrator",
    "type":"BuiltInRole",
    "description":"Lets you manage user access tooAzure resources.",
    "assignableScopes":["/"],
    "permissions":[{"actions":["*/read","Microsoft.Authorization/*","Microsoft.Support/*"],"notActions":[]}],
    "createdOn":"0001-01-01T08:00:00.0000000Z",
    "updatedOn":"2016-05-31T23:14:04.6964687Z",
    "createdBy":null,
    "updatedBy":null},
    "id":"/providers/Microsoft.Authorization/roleDefinitions/18d7d88d-d35e-4fb5-a5c3-7773c20a72d9",
    "type":"Microsoft.Authorization/roleDefinitions",
    "name":"18d7d88d-d35e-4fb5-a5c3-7773c20a72d9"}],
    "nextLink":null}
    ```

    Salvar Olá GUID de saudação *nome* parâmetro, neste caso **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.

2. Chame [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get), em que principalId = sua própria ObjectId. Lista todas as atribuições no locatário hello. Procure Olá um em que o escopo de saudação é "/" e Olá RoleDefinitionId termina com a função hello nome GUID encontrado na etapa 1. atribuição de função Hello deve ter esta aparência:

    ```
    {"value":[{"properties":{
    "roleDefinitionId":"/providers/Microsoft.Authorization/roleDefinitions/18d7d88d-d35e-4fb5-a5c3-7773c20a72d9",
    "principalId":"{objectID}",
    "scope":"/",
    "createdOn":"2016-08-17T19:21:16.3422480Z",
    "updatedOn":"2016-08-17T19:21:16.3422480Z",
    "createdBy":"93ce6722-3638-4222-b582-78b75c5c6d65",
    "updatedBy":"93ce6722-3638-4222-b582-78b75c5c6d65"},
    "id":"/providers/Microsoft.Authorization/roleAssignments/e7dd75bc-06f6-4e71-9014-ee96a929d099",
    "type":"Microsoft.Authorization/roleAssignments",
    "name":"e7dd75bc-06f6-4e71-9014-ee96a929d099"}],
    "nextLink":null}
    ```

    Salvar novamente, Olá GUID de saudação *nome* parâmetro, neste caso **e7dd75bc-06f6-4e71-9014-ee96a929d099**.

3. Finalmente, chame [excluir roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) onde roleAssignmentId = Olá nome GUID encontrado na etapa 2.

## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre [como gerenciar o Controle de Acesso Baseado em Função com REST](role-based-access-control-manage-access-rest.md)

- [Gerenciar atribuições de acesso](role-based-access-control-manage-assignments.md) em Olá portal do Azure
