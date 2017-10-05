---
title: "Acesso elevado de administrador de locatários — Azure AD | Microsoft Docs"
description: "Este tópico descreve as funções internas para o RBAC (controle de acesso baseado em função)."
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
ms.openlocfilehash: bf64a92b359a6f68d84fa5ee17eda64ed6371990
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a><span data-ttu-id="16256-103">Elevar o acesso como um administrador de locatários com Controle de Acesso Baseado em Função</span><span class="sxs-lookup"><span data-stu-id="16256-103">Elevate access as a tenant admin with Role-Based Access Control</span></span>

<span data-ttu-id="16256-104">O Controle de Acesso Baseado em Função ajuda os administradores de locatários a obter elevações temporárias no acesso para que eles possam conceder permissões mais elevadas que o normal.</span><span class="sxs-lookup"><span data-stu-id="16256-104">Role-based Access Control helps tenant administrators get temporary elevations in access so that they can grant higher permissions than normal.</span></span> <span data-ttu-id="16256-105">Um administrador de locatários pode elevar a si mesmo para a função de Administrador de Acesso do Usuário quando necessário.</span><span class="sxs-lookup"><span data-stu-id="16256-105">A tenant admin can elevate herself to the User Access Administrator role when needed.</span></span> <span data-ttu-id="16256-106">Essa função fornece ao administrador de locatários permissões para conceder a si mesmo ou a outras funções no escopo "/".</span><span class="sxs-lookup"><span data-stu-id="16256-106">That role gives the tenant admin permissions to grant herself or others roles at the "/" scope.</span></span>

<span data-ttu-id="16256-107">Esse recurso é importante porque permite que o administrador de locatários veja todas as assinaturas que existem em uma organização.</span><span class="sxs-lookup"><span data-stu-id="16256-107">This feature is important because it allows the tenant admin to see all the subscriptions that exist in an organization.</span></span> <span data-ttu-id="16256-108">Também permite aos aplicativos de automação (como faturamento e auditoria) acessar todas as assinaturas e fornecer uma exibição precisa do estado da organização em termos de gerenciamento de ativos ou cobrança.</span><span class="sxs-lookup"><span data-stu-id="16256-108">It also allows for automation apps (like invoicing and auditing) to access all the subscriptions and provide an accurate view of the state of the organization for billing or asset management.</span></span>  

## <a name="how-to-use-elevateaccess-to-give-tenant-access"></a><span data-ttu-id="16256-109">Como usar elevateAccess para fornecer acesso de locatário</span><span class="sxs-lookup"><span data-stu-id="16256-109">How to use elevateAccess to give tenant access</span></span>

<span data-ttu-id="16256-110">O processo básico funciona com as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="16256-110">The basic process works with the following steps:</span></span>

1. <span data-ttu-id="16256-111">Usando REST, chame *elevateAccess*, que concede a você a função Administrador de Acesso do Usuário no escopo "/".</span><span class="sxs-lookup"><span data-stu-id="16256-111">Using REST, call *elevateAccess*, which grants you the User Access Administrator role at "/" scope.</span></span>

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. <span data-ttu-id="16256-112">Crie uma [atribuição de função](/rest/api/authorization/roleassignments) para atribuir qualquer função em qualquer escopo.</span><span class="sxs-lookup"><span data-stu-id="16256-112">Create a [role assignment](/rest/api/authorization/roleassignments) to assign any role at any scope.</span></span> <span data-ttu-id="16256-113">O exemplo a seguir mostra as propriedades para atribuir a função Leitor no escopo "/":</span><span class="sxs-lookup"><span data-stu-id="16256-113">The following example shows the properties for assigning the Reader role at "/" scope:</span></span>

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

3. <span data-ttu-id="16256-114">Enquanto um Administrador de Acesso do Usuário, você também pode excluir a atribuição de função no escopo "/".</span><span class="sxs-lookup"><span data-stu-id="16256-114">While a User Access Admin, you can also delete role assignments at "/" scope.</span></span>

4. <span data-ttu-id="16256-115">Revogue seus privilégios de Administrador de Acesso do Usuário até que sejam necessários novamente.</span><span class="sxs-lookup"><span data-stu-id="16256-115">Revoke your User Access Admin privileges until they're needed again.</span></span>


## <a name="how-to-undo-the-elevateaccess-action"></a><span data-ttu-id="16256-116">Como desfazer a ação de elevateAccess</span><span class="sxs-lookup"><span data-stu-id="16256-116">How to undo the elevateAccess action</span></span>

<span data-ttu-id="16256-117">Ao chamar *elevateAccess*, você cria uma atribuição de função para si mesmo, de modo que para revogar esses privilégios é preciso excluir a atribuição.</span><span class="sxs-lookup"><span data-stu-id="16256-117">When you call *elevateAccess* you create a role assignment for yourself, so to revoke those privileges you need to delete the assignment.</span></span>

1.  <span data-ttu-id="16256-118">Chame [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get), em que roleName = Administrador de Acesso do Usuário determina o GUID do nome da função de Administrador de Acesso do Usuário.</span><span class="sxs-lookup"><span data-stu-id="16256-118">Call [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) where roleName = User Access Administrator to determine the name GUID of the User Access Administrator role.</span></span> <span data-ttu-id="16256-119">A resposta deve se parecer com esta:</span><span class="sxs-lookup"><span data-stu-id="16256-119">The response should look like this:</span></span>

    ```
    {"value":[{"properties":{
    "roleName":"User Access Administrator",
    "type":"BuiltInRole",
    "description":"Lets you manage user access to Azure resources.",
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

    <span data-ttu-id="16256-120">Salve o GUID do parâmetro *name*, neste caso **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span><span class="sxs-lookup"><span data-stu-id="16256-120">Save the GUID from the *name* parameter, in this case **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span></span>

2. <span data-ttu-id="16256-121">Chame [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get), em que principalId = sua própria ObjectId.</span><span class="sxs-lookup"><span data-stu-id="16256-121">Call [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) where principalId = your own ObjectId.</span></span> <span data-ttu-id="16256-122">Isso lista todas as suas atribuições no locatário.</span><span class="sxs-lookup"><span data-stu-id="16256-122">This lists all your assignments in the tenant.</span></span> <span data-ttu-id="16256-123">Procure aquela em que o escopo é "/" e a RoleDefinitionId termina com o GUID do nome da função que você encontrou na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="16256-123">Look for the one where the scope is "/" and the RoleDefinitionId ends with the role name GUID you found in step 1.</span></span> <span data-ttu-id="16256-124">A atribuição de função deve se parecer com esta:</span><span class="sxs-lookup"><span data-stu-id="16256-124">The role assignment should look like this:</span></span>

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

    <span data-ttu-id="16256-125">Novamente, salve o GUID do parâmetro *name* parâmetro, neste caso **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span><span class="sxs-lookup"><span data-stu-id="16256-125">Again, save the GUID from the *name* parameter, in this case **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span></span>

3. <span data-ttu-id="16256-126">Por fim, chame [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById), em que roleAssignmentId = o GUID do nome que você encontrou na etapa 2.</span><span class="sxs-lookup"><span data-stu-id="16256-126">Finally, call [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) where roleAssignmentId = the name GUID you found in step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16256-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="16256-127">Next steps</span></span>

- <span data-ttu-id="16256-128">Saiba mais sobre [como gerenciar o Controle de Acesso Baseado em Função com REST](role-based-access-control-manage-access-rest.md)</span><span class="sxs-lookup"><span data-stu-id="16256-128">Learn more about [managing Role-Based Access Control with REST](role-based-access-control-manage-access-rest.md)</span></span>

- <span data-ttu-id="16256-129">[Gerenciar atribuições de acesso](role-based-access-control-manage-assignments.md) no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="16256-129">[Manage access assignments](role-based-access-control-manage-assignments.md) in the Azure portal</span></span>
