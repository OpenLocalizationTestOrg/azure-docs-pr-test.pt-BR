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
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a><span data-ttu-id="32e28-103">Elevar o acesso como um administrador de locatários com Controle de Acesso Baseado em Função</span><span class="sxs-lookup"><span data-stu-id="32e28-103">Elevate access as a tenant admin with Role-Based Access Control</span></span>

<span data-ttu-id="32e28-104">O Controle de Acesso Baseado em Função ajuda os administradores de locatários a obter elevações temporárias no acesso para que eles possam conceder permissões mais elevadas que o normal.</span><span class="sxs-lookup"><span data-stu-id="32e28-104">Role-based Access Control helps tenant administrators get temporary elevations in access so that they can grant higher permissions than normal.</span></span> <span data-ttu-id="32e28-105">Um administrador de locatários pode elevar a mesmo toohello função de administrador de acesso do usuário quando necessário.</span><span class="sxs-lookup"><span data-stu-id="32e28-105">A tenant admin can elevate herself toohello User Access Administrator role when needed.</span></span> <span data-ttu-id="32e28-106">Essa função fornece Olá toogrant de permissões de administrador de locatário por conta própria ou outras funções em Olá escopo "/".</span><span class="sxs-lookup"><span data-stu-id="32e28-106">That role gives hello tenant admin permissions toogrant herself or others roles at hello "/" scope.</span></span>

<span data-ttu-id="32e28-107">Esse recurso é importante porque ela permite locatário Olá administrador toosee que todos Olá assinaturas que existem em uma organização.</span><span class="sxs-lookup"><span data-stu-id="32e28-107">This feature is important because it allows hello tenant admin toosee all hello subscriptions that exist in an organization.</span></span> <span data-ttu-id="32e28-108">Ele também permite tooaccess de aplicativos (como faturamento e auditoria) de automação todas as assinaturas de saudação e fornecer uma exibição precisa do estado de saudação da organização Olá para cobrança ou gerenciamento de ativos.</span><span class="sxs-lookup"><span data-stu-id="32e28-108">It also allows for automation apps (like invoicing and auditing) tooaccess all hello subscriptions and provide an accurate view of hello state of hello organization for billing or asset management.</span></span>  

## <a name="how-toouse-elevateaccess-toogive-tenant-access"></a><span data-ttu-id="32e28-109">Como o acesso de locatário toouse elevateAccess toogive</span><span class="sxs-lookup"><span data-stu-id="32e28-109">How toouse elevateAccess toogive tenant access</span></span>

<span data-ttu-id="32e28-110">processo básico de saudação funciona com hello etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="32e28-110">hello basic process works with hello following steps:</span></span>

1. <span data-ttu-id="32e28-111">Usando REST, chame *elevateAccess*, que concede a você Olá a função de administrador de acesso do usuário em "/" de escopo.</span><span class="sxs-lookup"><span data-stu-id="32e28-111">Using REST, call *elevateAccess*, which grants you hello User Access Administrator role at "/" scope.</span></span>

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. <span data-ttu-id="32e28-112">Criar um [atribuição de função](/rest/api/authorization/roleassignments) tooassign qualquer função em qualquer escopo.</span><span class="sxs-lookup"><span data-stu-id="32e28-112">Create a [role assignment](/rest/api/authorization/roleassignments) tooassign any role at any scope.</span></span> <span data-ttu-id="32e28-113">Olá exemplo a seguir mostra as propriedades Olá para atribuir Olá a função de leitor em "/" de escopo:</span><span class="sxs-lookup"><span data-stu-id="32e28-113">hello following example shows hello properties for assigning hello Reader role at "/" scope:</span></span>

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

3. <span data-ttu-id="32e28-114">Enquanto um Administrador de Acesso do Usuário, você também pode excluir a atribuição de função no escopo "/".</span><span class="sxs-lookup"><span data-stu-id="32e28-114">While a User Access Admin, you can also delete role assignments at "/" scope.</span></span>

4. <span data-ttu-id="32e28-115">Revogue seus privilégios de Administrador de Acesso do Usuário até que sejam necessários novamente.</span><span class="sxs-lookup"><span data-stu-id="32e28-115">Revoke your User Access Admin privileges until they're needed again.</span></span>


## <a name="how-tooundo-hello-elevateaccess-action"></a><span data-ttu-id="32e28-116">Como tooundo Olá elevateAccess ação</span><span class="sxs-lookup"><span data-stu-id="32e28-116">How tooundo hello elevateAccess action</span></span>

<span data-ttu-id="32e28-117">Quando você chama *elevateAccess* criar uma atribuição de função por conta própria, portanto toorevoke os privilégios que você precisa toodelete Olá atribuição.</span><span class="sxs-lookup"><span data-stu-id="32e28-117">When you call *elevateAccess* you create a role assignment for yourself, so toorevoke those privileges you need toodelete hello assignment.</span></span>

1.  <span data-ttu-id="32e28-118">Chamar [roleDefinitions GET](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) onde roleName = toodetermine do administrador do acesso de usuário Olá nome GUID da função de administrador de acesso de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="32e28-118">Call [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) where roleName = User Access Administrator toodetermine hello name GUID of hello User Access Administrator role.</span></span> <span data-ttu-id="32e28-119">resposta de saudação deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="32e28-119">hello response should look like this:</span></span>

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

    <span data-ttu-id="32e28-120">Salvar Olá GUID de saudação *nome* parâmetro, neste caso **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span><span class="sxs-lookup"><span data-stu-id="32e28-120">Save hello GUID from hello *name* parameter, in this case **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span></span>

2. <span data-ttu-id="32e28-121">Chame [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get), em que principalId = sua própria ObjectId.</span><span class="sxs-lookup"><span data-stu-id="32e28-121">Call [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) where principalId = your own ObjectId.</span></span> <span data-ttu-id="32e28-122">Lista todas as atribuições no locatário hello.</span><span class="sxs-lookup"><span data-stu-id="32e28-122">This lists all your assignments in hello tenant.</span></span> <span data-ttu-id="32e28-123">Procure Olá um em que o escopo de saudação é "/" e Olá RoleDefinitionId termina com a função hello nome GUID encontrado na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="32e28-123">Look for hello one where hello scope is "/" and hello RoleDefinitionId ends with hello role name GUID you found in step 1.</span></span> <span data-ttu-id="32e28-124">atribuição de função Hello deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="32e28-124">hello role assignment should look like this:</span></span>

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

    <span data-ttu-id="32e28-125">Salvar novamente, Olá GUID de saudação *nome* parâmetro, neste caso **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span><span class="sxs-lookup"><span data-stu-id="32e28-125">Again, save hello GUID from hello *name* parameter, in this case **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span></span>

3. <span data-ttu-id="32e28-126">Finalmente, chame [excluir roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) onde roleAssignmentId = Olá nome GUID encontrado na etapa 2.</span><span class="sxs-lookup"><span data-stu-id="32e28-126">Finally, call [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) where roleAssignmentId = hello name GUID you found in step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32e28-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="32e28-127">Next steps</span></span>

- <span data-ttu-id="32e28-128">Saiba mais sobre [como gerenciar o Controle de Acesso Baseado em Função com REST](role-based-access-control-manage-access-rest.md)</span><span class="sxs-lookup"><span data-stu-id="32e28-128">Learn more about [managing Role-Based Access Control with REST](role-based-access-control-manage-access-rest.md)</span></span>

- <span data-ttu-id="32e28-129">[Gerenciar atribuições de acesso](role-based-access-control-manage-assignments.md) em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="32e28-129">[Manage access assignments](role-based-access-control-manage-assignments.md) in hello Azure portal</span></span>
