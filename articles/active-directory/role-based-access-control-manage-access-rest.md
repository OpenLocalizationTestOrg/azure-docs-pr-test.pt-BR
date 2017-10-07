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
# <a name="manage-role-based-access-control-with-hello-rest-api"></a><span data-ttu-id="0dd96-103">Gerenciar o controle de acesso baseado em função com hello API REST</span><span class="sxs-lookup"><span data-stu-id="0dd96-103">Manage Role-Based Access Control with hello REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0dd96-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0dd96-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="0dd96-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="0dd96-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="0dd96-106">API REST</span><span class="sxs-lookup"><span data-stu-id="0dd96-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="0dd96-107">Baseado em função RBAC controle de acesso () em Olá portal do Azure e API do Gerenciador de recursos do Azure ajuda a gerenciar o acesso tooyour assinatura e recursos em um nível granular.</span><span class="sxs-lookup"><span data-stu-id="0dd96-107">Role-Based Access Control (RBAC) in hello Azure portal and Azure Resource Manager API helps you manage access tooyour subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="0dd96-108">Com esse recurso, você pode conceder acesso para usuários, grupos ou entidades de serviço do Active Directory, atribuindo toothem algumas funções em um escopo específico.</span><span class="sxs-lookup"><span data-stu-id="0dd96-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles toothem at a particular scope.</span></span>

## <a name="list-all-role-assignments"></a><span data-ttu-id="0dd96-109">Lista todas as atribuições de função</span><span class="sxs-lookup"><span data-stu-id="0dd96-109">List all role assignments</span></span>
<span data-ttu-id="0dd96-110">Lista todas as atribuições de função hello em Olá especificado escopo e subscopes.</span><span class="sxs-lookup"><span data-stu-id="0dd96-110">Lists all hello role assignments at hello specified scope and subscopes.</span></span>

<span data-ttu-id="0dd96-111">atribuições de função toolist, você deve ter acesso muito`Microsoft.Authorization/roleAssignments/read` operação no escopo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0dd96-111">toolist role assignments, you must have access too`Microsoft.Authorization/roleAssignments/read` operation at hello scope.</span></span> <span data-ttu-id="0dd96-112">Todas as funções internas de saudação recebem acesso toothis operação.</span><span class="sxs-lookup"><span data-stu-id="0dd96-112">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="0dd96-113">Para saber mais sobre as atribuições de função e o gerenciamento de acesso para recursos do Azure, consulte [Controle de Acesso Baseado em Função do Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="0dd96-113">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="0dd96-114">Solicitação</span><span class="sxs-lookup"><span data-stu-id="0dd96-114">Request</span></span>
<span data-ttu-id="0dd96-115">Saudação de uso **obter** método com hello URI a seguir:</span><span class="sxs-lookup"><span data-stu-id="0dd96-115">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments?api-version={api-version}&$filter={filter}

<span data-ttu-id="0dd96-116">Dentro de Olá URI, verifique Olá toocustomize substituições a seguir sua solicitação:</span><span class="sxs-lookup"><span data-stu-id="0dd96-116">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="0dd96-117">Substituir *{scope}* com escopo Olá para o qual você deseja toolist atribuições de função hello.</span><span class="sxs-lookup"><span data-stu-id="0dd96-117">Replace *{scope}* with hello scope for which you wish toolist hello role assignments.</span></span> <span data-ttu-id="0dd96-118">Olá exemplos a seguir mostra como toospecify Olá escopo para os diferentes níveis:</span><span class="sxs-lookup"><span data-stu-id="0dd96-118">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="0dd96-119">Assinatura: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="0dd96-119">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="0dd96-120">Grupo de Recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="0dd96-120">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="0dd96-121">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="0dd96-121">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="0dd96-122">Substitua *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="0dd96-122">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="0dd96-123">Substituir *{filter}* com a condição de saudação que desejar que a lista de atribuições de função do tooapply toofilter hello:</span><span class="sxs-lookup"><span data-stu-id="0dd96-123">Replace *{filter}* with hello condition that you wish tooapply toofilter hello role assignment list:</span></span>

   * <span data-ttu-id="0dd96-124">Lista de atribuições de função para apenas Olá especificado escopo, não incluindo atribuições de função hello subscopes:`atScope()`</span><span class="sxs-lookup"><span data-stu-id="0dd96-124">List role assignments for only hello specified scope, not including hello role assignments at subscopes: `atScope()`</span></span>    
   * <span data-ttu-id="0dd96-125">Liste atribuições de função para um usuário, grupo ou aplicativo específico: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span><span class="sxs-lookup"><span data-stu-id="0dd96-125">List role assignments for a specific user, group, or application: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span></span>  
   * <span data-ttu-id="0dd96-126">Liste atribuições de função para um usuário específico, incluindo aqueles herdados de grupos | `assignedTo('{objectId of user}')`</span><span class="sxs-lookup"><span data-stu-id="0dd96-126">List role assignments for a specific user, including ones inherited from groups | `assignedTo('{objectId of user}')`</span></span>

### <a name="response"></a><span data-ttu-id="0dd96-127">Response</span><span class="sxs-lookup"><span data-stu-id="0dd96-127">Response</span></span>
<span data-ttu-id="0dd96-128">Código de status: 200</span><span class="sxs-lookup"><span data-stu-id="0dd96-128">Status code: 200</span></span>

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

## <a name="get-information-about-a-role-assignment"></a><span data-ttu-id="0dd96-129">Obter informações sobre uma atribuição de função</span><span class="sxs-lookup"><span data-stu-id="0dd96-129">Get information about a role assignment</span></span>
<span data-ttu-id="0dd96-130">Obtém informações sobre uma única atribuição de função especificada pelo identificador de atribuição de função hello.</span><span class="sxs-lookup"><span data-stu-id="0dd96-130">Gets information about a single role assignment specified by hello role assignment identifier.</span></span>

<span data-ttu-id="0dd96-131">tooget informações sobre uma atribuição de função, você deve ter acesso muito`Microsoft.Authorization/roleAssignments/read` operação.</span><span class="sxs-lookup"><span data-stu-id="0dd96-131">tooget information about a role assignment, you must have access too`Microsoft.Authorization/roleAssignments/read` operation.</span></span> <span data-ttu-id="0dd96-132">Todas as funções internas de saudação recebem acesso toothis operação.</span><span class="sxs-lookup"><span data-stu-id="0dd96-132">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="0dd96-133">Para saber mais sobre as atribuições de função e o gerenciamento de acesso para recursos do Azure, consulte [Controle de Acesso Baseado em Função do Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="0dd96-133">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="0dd96-134">Solicitação</span><span class="sxs-lookup"><span data-stu-id="0dd96-134">Request</span></span>
<span data-ttu-id="0dd96-135">Saudação de uso **obter** método com hello URI a seguir:</span><span class="sxs-lookup"><span data-stu-id="0dd96-135">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="0dd96-136">Dentro de Olá URI, verifique Olá toocustomize substituições a seguir sua solicitação:</span><span class="sxs-lookup"><span data-stu-id="0dd96-136">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="0dd96-137">Substituir *{scope}* com escopo Olá para o qual você deseja toolist atribuições de função hello.</span><span class="sxs-lookup"><span data-stu-id="0dd96-137">Replace *{scope}* with hello scope for which you wish toolist hello role assignments.</span></span> <span data-ttu-id="0dd96-138">Olá exemplos a seguir mostra como toospecify Olá escopo para os diferentes níveis:</span><span class="sxs-lookup"><span data-stu-id="0dd96-138">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="0dd96-139">Assinatura: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="0dd96-139">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="0dd96-140">Grupo de Recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="0dd96-140">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="0dd96-141">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="0dd96-141">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="0dd96-142">Substituir *{role-assignment-id}* com identificador de GUID Olá Olá de atribuição de função.</span><span class="sxs-lookup"><span data-stu-id="0dd96-142">Replace *{role-assignment-id}* with hello GUID identifier of hello role assignment.</span></span>
3. <span data-ttu-id="0dd96-143">Substitua *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="0dd96-143">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="0dd96-144">Response</span><span class="sxs-lookup"><span data-stu-id="0dd96-144">Response</span></span>
<span data-ttu-id="0dd96-145">Código de status: 200</span><span class="sxs-lookup"><span data-stu-id="0dd96-145">Status code: 200</span></span>

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

## <a name="create-a-role-assignment"></a><span data-ttu-id="0dd96-146">Criar uma atribuição de função</span><span class="sxs-lookup"><span data-stu-id="0dd96-146">Create a Role Assignment</span></span>
<span data-ttu-id="0dd96-147">Criar uma função de atribuição no hello especificado escopo para Olá especificado função especificado principal de concessão hello.</span><span class="sxs-lookup"><span data-stu-id="0dd96-147">Create a role assignment at hello specified scope for hello specified principal granting hello specified role.</span></span>

<span data-ttu-id="0dd96-148">toocreate uma atribuição de função, você deve ter acesso muito`Microsoft.Authorization/roleAssignments/write` operação.</span><span class="sxs-lookup"><span data-stu-id="0dd96-148">toocreate a role assignment, you must have access too`Microsoft.Authorization/roleAssignments/write` operation.</span></span> <span data-ttu-id="0dd96-149">De saudação funções internas, apenas *proprietário* e *administrador de acesso do usuário* recebem acesso toothis operação.</span><span class="sxs-lookup"><span data-stu-id="0dd96-149">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="0dd96-150">Para saber mais sobre as atribuições de função e o gerenciamento de acesso para recursos do Azure, consulte [Controle de Acesso Baseado em Função do Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="0dd96-150">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="0dd96-151">Solicitação</span><span class="sxs-lookup"><span data-stu-id="0dd96-151">Request</span></span>
<span data-ttu-id="0dd96-152">Saudação de uso **colocar** método com hello URI a seguir:</span><span class="sxs-lookup"><span data-stu-id="0dd96-152">Use hello **PUT** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="0dd96-153">Dentro de Olá URI, verifique Olá toocustomize substituições a seguir sua solicitação:</span><span class="sxs-lookup"><span data-stu-id="0dd96-153">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="0dd96-154">Substituir *{scope}* com escopo de saudação em que você deseja toocreate atribuições de função hello.</span><span class="sxs-lookup"><span data-stu-id="0dd96-154">Replace *{scope}* with hello scope at which you wish toocreate hello role assignments.</span></span> <span data-ttu-id="0dd96-155">Quando você criar uma atribuição de função em um escopo pai, todos os escopos filho herdam Olá mesma atribuição de função.</span><span class="sxs-lookup"><span data-stu-id="0dd96-155">When you create a role assignment at a parent scope, all child scopes inherit hello same role assignment.</span></span> <span data-ttu-id="0dd96-156">Olá exemplos a seguir mostra como toospecify Olá escopo para os diferentes níveis:</span><span class="sxs-lookup"><span data-stu-id="0dd96-156">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="0dd96-157">Assinatura: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="0dd96-157">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="0dd96-158">Grupo de Recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="0dd96-158">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>   
   * <span data-ttu-id="0dd96-159">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="0dd96-159">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="0dd96-160">Substituir *{role-assignment-id}* com um novo GUID, que se torna o identificador GUID de saudação da nova atribuição de função hello.</span><span class="sxs-lookup"><span data-stu-id="0dd96-160">Replace *{role-assignment-id}* with a new GUID, which becomes hello GUID identifier of hello new role assignment.</span></span>
3. <span data-ttu-id="0dd96-161">Substitua *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="0dd96-161">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="0dd96-162">Corpo da solicitação Olá, fornece valores Olá Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="0dd96-162">For hello request body, provide hello values in hello following format:</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b"
  }
}

```

| <span data-ttu-id="0dd96-163">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="0dd96-163">Element Name</span></span> | <span data-ttu-id="0dd96-164">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="0dd96-164">Required</span></span> | <span data-ttu-id="0dd96-165">Tipo</span><span class="sxs-lookup"><span data-stu-id="0dd96-165">Type</span></span> | <span data-ttu-id="0dd96-166">Descrição</span><span class="sxs-lookup"><span data-stu-id="0dd96-166">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0dd96-167">roleDefinitionId</span><span class="sxs-lookup"><span data-stu-id="0dd96-167">roleDefinitionId</span></span> |<span data-ttu-id="0dd96-168">Sim</span><span class="sxs-lookup"><span data-stu-id="0dd96-168">Yes</span></span> |<span data-ttu-id="0dd96-169">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0dd96-169">String</span></span> |<span data-ttu-id="0dd96-170">Identificador de saudação da função de saudação.</span><span class="sxs-lookup"><span data-stu-id="0dd96-170">hello identifier of hello role.</span></span> <span data-ttu-id="0dd96-171">formato de saudação do identificador de saudação é:`{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span><span class="sxs-lookup"><span data-stu-id="0dd96-171">hello format of hello identifier is: `{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span></span> |
| <span data-ttu-id="0dd96-172">principalId</span><span class="sxs-lookup"><span data-stu-id="0dd96-172">principalId</span></span> |<span data-ttu-id="0dd96-173">Sim</span><span class="sxs-lookup"><span data-stu-id="0dd96-173">Yes</span></span> |<span data-ttu-id="0dd96-174">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0dd96-174">String</span></span> |<span data-ttu-id="0dd96-175">ID do objeto de entidade de saudação do AD do Azure (usuário, grupo ou entidade de serviço) toowhich Olá função é atribuída.</span><span class="sxs-lookup"><span data-stu-id="0dd96-175">objectId of hello Azure AD principal (user, group, or service principal) toowhich hello role is assigned.</span></span> |

### <a name="response"></a><span data-ttu-id="0dd96-176">Resposta</span><span class="sxs-lookup"><span data-stu-id="0dd96-176">Response</span></span>
<span data-ttu-id="0dd96-177">Código de status: 201</span><span class="sxs-lookup"><span data-stu-id="0dd96-177">Status code: 201</span></span>

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

## <a name="delete-a-role-assignment"></a><span data-ttu-id="0dd96-178">Excluir uma atribuição de função</span><span class="sxs-lookup"><span data-stu-id="0dd96-178">Delete a Role Assignment</span></span>
<span data-ttu-id="0dd96-179">Excluir uma atribuição de função em Olá especificado escopo.</span><span class="sxs-lookup"><span data-stu-id="0dd96-179">Delete a role assignment at hello specified scope.</span></span>

<span data-ttu-id="0dd96-180">toodelete uma atribuição de função, você deve ter acesso toohello `Microsoft.Authorization/roleAssignments/delete` operação.</span><span class="sxs-lookup"><span data-stu-id="0dd96-180">toodelete a role assignment, you must have access toohello `Microsoft.Authorization/roleAssignments/delete` operation.</span></span> <span data-ttu-id="0dd96-181">De saudação funções internas, apenas *proprietário* e *administrador de acesso do usuário* recebem acesso toothis operação.</span><span class="sxs-lookup"><span data-stu-id="0dd96-181">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="0dd96-182">Para saber mais sobre as atribuições de função e o gerenciamento de acesso para recursos do Azure, consulte [Controle de Acesso Baseado em Função do Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="0dd96-182">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="0dd96-183">Solicitação</span><span class="sxs-lookup"><span data-stu-id="0dd96-183">Request</span></span>
<span data-ttu-id="0dd96-184">Saudação de uso **excluir** método com hello URI a seguir:</span><span class="sxs-lookup"><span data-stu-id="0dd96-184">Use hello **DELETE** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="0dd96-185">Dentro de Olá URI, verifique Olá toocustomize substituições a seguir sua solicitação:</span><span class="sxs-lookup"><span data-stu-id="0dd96-185">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="0dd96-186">Substituir *{scope}* com escopo de saudação em que você deseja toocreate atribuições de função hello.</span><span class="sxs-lookup"><span data-stu-id="0dd96-186">Replace *{scope}* with hello scope at which you wish toocreate hello role assignments.</span></span> <span data-ttu-id="0dd96-187">Olá exemplos a seguir mostra como toospecify Olá escopo para os diferentes níveis:</span><span class="sxs-lookup"><span data-stu-id="0dd96-187">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="0dd96-188">Assinatura: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="0dd96-188">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="0dd96-189">Grupo de Recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="0dd96-189">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="0dd96-190">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="0dd96-190">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="0dd96-191">Substituir *{role-assignment-id}* com a id de atribuição de função hello GUID.</span><span class="sxs-lookup"><span data-stu-id="0dd96-191">Replace *{role-assignment-id}* with hello role assignment id GUID.</span></span>
3. <span data-ttu-id="0dd96-192">Substitua *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="0dd96-192">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="0dd96-193">Response</span><span class="sxs-lookup"><span data-stu-id="0dd96-193">Response</span></span>
<span data-ttu-id="0dd96-194">Código de status: 200</span><span class="sxs-lookup"><span data-stu-id="0dd96-194">Status code: 200</span></span>

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

## <a name="list-all-roles"></a><span data-ttu-id="0dd96-195">Lista todas as Funções</span><span class="sxs-lookup"><span data-stu-id="0dd96-195">List all Roles</span></span>
<span data-ttu-id="0dd96-196">Lista todas as funções hello que estão disponíveis para atribuição de saudação especificada escopo.</span><span class="sxs-lookup"><span data-stu-id="0dd96-196">Lists all hello roles that are available for assignment at hello specified scope.</span></span>

<span data-ttu-id="0dd96-197">funções de toolist, você deve ter acesso muito`Microsoft.Authorization/roleDefinitions/read` operação no escopo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0dd96-197">toolist roles, you must have access too`Microsoft.Authorization/roleDefinitions/read` operation at hello scope.</span></span> <span data-ttu-id="0dd96-198">Todas as funções internas de saudação recebem acesso toothis operação.</span><span class="sxs-lookup"><span data-stu-id="0dd96-198">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="0dd96-199">Para saber mais sobre as atribuições de função e o gerenciamento de acesso para recursos do Azure, consulte [Controle de Acesso Baseado em Função do Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="0dd96-199">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="0dd96-200">Solicitação</span><span class="sxs-lookup"><span data-stu-id="0dd96-200">Request</span></span>
<span data-ttu-id="0dd96-201">Saudação de uso **obter** método com hello URI a seguir:</span><span class="sxs-lookup"><span data-stu-id="0dd96-201">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?api-version={api-version}&$filter={filter}

<span data-ttu-id="0dd96-202">Dentro de Olá URI, verifique Olá toocustomize substituições a seguir sua solicitação:</span><span class="sxs-lookup"><span data-stu-id="0dd96-202">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="0dd96-203">Substituir *{scope}* com escopo Olá para o qual você deseja toolist funções hello.</span><span class="sxs-lookup"><span data-stu-id="0dd96-203">Replace *{scope}* with hello scope for which you wish toolist hello roles.</span></span> <span data-ttu-id="0dd96-204">Olá exemplos a seguir mostra como toospecify Olá escopo para os diferentes níveis:</span><span class="sxs-lookup"><span data-stu-id="0dd96-204">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="0dd96-205">Assinatura: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="0dd96-205">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="0dd96-206">Grupo de Recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="0dd96-206">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="0dd96-207">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="0dd96-207">Resource /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="0dd96-208">Substitua *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="0dd96-208">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="0dd96-209">Substituir *{filter}* com a condição de saudação que você deseja tooapply lista de saudação toofilter de funções:</span><span class="sxs-lookup"><span data-stu-id="0dd96-209">Replace *{filter}* with hello condition that you wish tooapply toofilter hello list of roles:</span></span>

   * <span data-ttu-id="0dd96-210">Lista de funções disponíveis para atribuição de saudação especificado escopo e qualquer um de seus escopos filhos:`atScopeAndBelow()`</span><span class="sxs-lookup"><span data-stu-id="0dd96-210">List roles available for assignment at hello specified scope and any of its child scopes: `atScopeAndBelow()`</span></span>
   * <span data-ttu-id="0dd96-211">Pesquise uma função usando o nome de exibição exato: `roleName%20eq%20'{role-display-name}'`.</span><span class="sxs-lookup"><span data-stu-id="0dd96-211">Search for a role using exact display name: `roleName%20eq%20'{role-display-name}'`.</span></span> <span data-ttu-id="0dd96-212">Formato de nome de exibição exato Olá da função hello codificados da URL de saudação de uso.</span><span class="sxs-lookup"><span data-stu-id="0dd96-212">Use hello URL encoded form of hello exact display name of hello role.</span></span> <span data-ttu-id="0dd96-213">Por exemplo, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span><span class="sxs-lookup"><span data-stu-id="0dd96-213">For instance, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span></span>

### <a name="response"></a><span data-ttu-id="0dd96-214">Response</span><span class="sxs-lookup"><span data-stu-id="0dd96-214">Response</span></span>
<span data-ttu-id="0dd96-215">Código de status: 200</span><span class="sxs-lookup"><span data-stu-id="0dd96-215">Status code: 200</span></span>

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

## <a name="get-information-about-a-role"></a><span data-ttu-id="0dd96-216">Obter informações sobre uma Função</span><span class="sxs-lookup"><span data-stu-id="0dd96-216">Get information about a Role</span></span>
<span data-ttu-id="0dd96-217">Obtém informações sobre uma única função especificada pelo identificador de definição de função hello.</span><span class="sxs-lookup"><span data-stu-id="0dd96-217">Gets information about a single role specified by hello role definition identifier.</span></span> <span data-ttu-id="0dd96-218">tooget informações sobre uma única função usando seu nome de exibição, consulte [liste todas as funções](role-based-access-control-manage-access-rest.md#list-all-roles).</span><span class="sxs-lookup"><span data-stu-id="0dd96-218">tooget information about a single role using its display name, see [List all roles](role-based-access-control-manage-access-rest.md#list-all-roles).</span></span>

<span data-ttu-id="0dd96-219">tooget informações sobre uma função, você deve ter acesso muito`Microsoft.Authorization/roleDefinitions/read` operação.</span><span class="sxs-lookup"><span data-stu-id="0dd96-219">tooget information about a role, you must have access too`Microsoft.Authorization/roleDefinitions/read` operation.</span></span> <span data-ttu-id="0dd96-220">Todas as funções internas de saudação recebem acesso toothis operação.</span><span class="sxs-lookup"><span data-stu-id="0dd96-220">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="0dd96-221">Para saber mais sobre as atribuições de função e o gerenciamento de acesso para recursos do Azure, consulte [Controle de Acesso Baseado em Função do Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="0dd96-221">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="0dd96-222">Solicitação</span><span class="sxs-lookup"><span data-stu-id="0dd96-222">Request</span></span>
<span data-ttu-id="0dd96-223">Saudação de uso **obter** método com hello URI a seguir:</span><span class="sxs-lookup"><span data-stu-id="0dd96-223">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="0dd96-224">Dentro de Olá URI, verifique Olá toocustomize substituições a seguir sua solicitação:</span><span class="sxs-lookup"><span data-stu-id="0dd96-224">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="0dd96-225">Substituir *{scope}* com escopo Olá para o qual você deseja toolist atribuições de função hello.</span><span class="sxs-lookup"><span data-stu-id="0dd96-225">Replace *{scope}* with hello scope for which you wish toolist hello role assignments.</span></span> <span data-ttu-id="0dd96-226">Olá exemplos a seguir mostra como toospecify Olá escopo para os diferentes níveis:</span><span class="sxs-lookup"><span data-stu-id="0dd96-226">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="0dd96-227">Assinatura: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="0dd96-227">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="0dd96-228">Grupo de Recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="0dd96-228">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="0dd96-229">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="0dd96-229">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="0dd96-230">Substituir *{id de definição de função}* com identificador de GUID Olá Olá da definição da função.</span><span class="sxs-lookup"><span data-stu-id="0dd96-230">Replace *{role-definition-id}* with hello GUID identifier of hello role definition.</span></span>
3. <span data-ttu-id="0dd96-231">Substitua *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="0dd96-231">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="0dd96-232">Response</span><span class="sxs-lookup"><span data-stu-id="0dd96-232">Response</span></span>
<span data-ttu-id="0dd96-233">Código de status: 200</span><span class="sxs-lookup"><span data-stu-id="0dd96-233">Status code: 200</span></span>

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

## <a name="create-a-custom-role"></a><span data-ttu-id="0dd96-234">Criar uma Função personalizada</span><span class="sxs-lookup"><span data-stu-id="0dd96-234">Create a Custom Role</span></span>
<span data-ttu-id="0dd96-235">Criar uma função personalizada.</span><span class="sxs-lookup"><span data-stu-id="0dd96-235">Create a custom role.</span></span>

<span data-ttu-id="0dd96-236">toocreate uma função personalizada, você deve ter acesso muito`Microsoft.Authorization/roleDefinitions/write` operação em todos os Olá `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="0dd96-236">toocreate a custom role, you must have access too`Microsoft.Authorization/roleDefinitions/write` operation on all hello `AssignableScopes`.</span></span> <span data-ttu-id="0dd96-237">De saudação funções internas, apenas *proprietário* e *administrador de acesso do usuário* recebem acesso toothis operação.</span><span class="sxs-lookup"><span data-stu-id="0dd96-237">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="0dd96-238">Para saber mais sobre as atribuições de função e o gerenciamento de acesso para recursos do Azure, consulte [Controle de Acesso Baseado em Função do Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="0dd96-238">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="0dd96-239">Solicitação</span><span class="sxs-lookup"><span data-stu-id="0dd96-239">Request</span></span>
<span data-ttu-id="0dd96-240">Saudação de uso **colocar** método com hello URI a seguir:</span><span class="sxs-lookup"><span data-stu-id="0dd96-240">Use hello **PUT** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="0dd96-241">Dentro de Olá URI, verifique Olá toocustomize substituições a seguir sua solicitação:</span><span class="sxs-lookup"><span data-stu-id="0dd96-241">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="0dd96-242">Substituir *{scope}* com hello primeiro *AssignableScope* de função personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="0dd96-242">Replace *{scope}* with hello first *AssignableScope* of hello custom role.</span></span> <span data-ttu-id="0dd96-243">Olá exemplos a seguir mostra como toospecify Olá escopo para os diferentes níveis.</span><span class="sxs-lookup"><span data-stu-id="0dd96-243">hello following examples show how toospecify hello scope for different levels.</span></span>

   * <span data-ttu-id="0dd96-244">Assinatura: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="0dd96-244">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="0dd96-245">Grupo de Recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="0dd96-245">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="0dd96-246">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="0dd96-246">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="0dd96-247">Substituir *{id de definição de função}* com um novo GUID, que se torna o identificador GUID de saudação da nova função personalizada de saudação.</span><span class="sxs-lookup"><span data-stu-id="0dd96-247">Replace *{role-definition-id}* with a new GUID, which becomes hello GUID identifier of hello new custom role.</span></span>
3. <span data-ttu-id="0dd96-248">Substitua *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="0dd96-248">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="0dd96-249">Corpo da solicitação Olá, fornece valores Olá Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="0dd96-249">For hello request body, provide hello values in hello following format:</span></span>

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

| <span data-ttu-id="0dd96-250">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="0dd96-250">Element Name</span></span> | <span data-ttu-id="0dd96-251">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="0dd96-251">Required</span></span> | <span data-ttu-id="0dd96-252">Tipo</span><span class="sxs-lookup"><span data-stu-id="0dd96-252">Type</span></span> | <span data-ttu-id="0dd96-253">Descrição</span><span class="sxs-lookup"><span data-stu-id="0dd96-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0dd96-254">name</span><span class="sxs-lookup"><span data-stu-id="0dd96-254">name</span></span> |<span data-ttu-id="0dd96-255">Sim</span><span class="sxs-lookup"><span data-stu-id="0dd96-255">Yes</span></span> |<span data-ttu-id="0dd96-256">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0dd96-256">String</span></span> |<span data-ttu-id="0dd96-257">Identificador GUID de função personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="0dd96-257">GUID identifier of hello custom role.</span></span> |
| <span data-ttu-id="0dd96-258">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="0dd96-258">properties.roleName</span></span> |<span data-ttu-id="0dd96-259">Sim</span><span class="sxs-lookup"><span data-stu-id="0dd96-259">Yes</span></span> |<span data-ttu-id="0dd96-260">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0dd96-260">String</span></span> |<span data-ttu-id="0dd96-261">Exibir o nome da função personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="0dd96-261">Display name of hello custom role.</span></span> <span data-ttu-id="0dd96-262">Tamanho máximo de 128 caracteres.</span><span class="sxs-lookup"><span data-stu-id="0dd96-262">Maximum size 128 characters.</span></span> |
| <span data-ttu-id="0dd96-263">properties.description</span><span class="sxs-lookup"><span data-stu-id="0dd96-263">properties.description</span></span> |<span data-ttu-id="0dd96-264">Não</span><span class="sxs-lookup"><span data-stu-id="0dd96-264">No</span></span> |<span data-ttu-id="0dd96-265">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0dd96-265">String</span></span> |<span data-ttu-id="0dd96-266">Descrição da função de saudação personalizada.</span><span class="sxs-lookup"><span data-stu-id="0dd96-266">Description of hello custom role.</span></span> <span data-ttu-id="0dd96-267">Tamanho máximo de 1024 caracteres.</span><span class="sxs-lookup"><span data-stu-id="0dd96-267">Maximum size 1024 characters.</span></span> |
| <span data-ttu-id="0dd96-268">properties.type</span><span class="sxs-lookup"><span data-stu-id="0dd96-268">properties.type</span></span> |<span data-ttu-id="0dd96-269">Sim</span><span class="sxs-lookup"><span data-stu-id="0dd96-269">Yes</span></span> |<span data-ttu-id="0dd96-270">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0dd96-270">String</span></span> |<span data-ttu-id="0dd96-271">Definir muito "CustomRole".</span><span class="sxs-lookup"><span data-stu-id="0dd96-271">Set too"CustomRole."</span></span> |
| <span data-ttu-id="0dd96-272">properties.permissions.actions</span><span class="sxs-lookup"><span data-stu-id="0dd96-272">properties.permissions.actions</span></span> |<span data-ttu-id="0dd96-273">Sim</span><span class="sxs-lookup"><span data-stu-id="0dd96-273">Yes</span></span> |<span data-ttu-id="0dd96-274">String[]</span><span class="sxs-lookup"><span data-stu-id="0dd96-274">String[]</span></span> |<span data-ttu-id="0dd96-275">Uma matriz de ação de cadeias de caracteres especificando operações Olá concedidas pela função personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="0dd96-275">An array of action strings specifying hello operations granted by hello custom role.</span></span> |
| <span data-ttu-id="0dd96-276">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="0dd96-276">properties.permissions.notActions</span></span> |<span data-ttu-id="0dd96-277">Não</span><span class="sxs-lookup"><span data-stu-id="0dd96-277">No</span></span> |<span data-ttu-id="0dd96-278">String[]</span><span class="sxs-lookup"><span data-stu-id="0dd96-278">String[]</span></span> |<span data-ttu-id="0dd96-279">Uma matriz de cadeias de caracteres de ação especificando Olá operações tooexclude de operações de saudação concedido pela função personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="0dd96-279">An array of action strings specifying hello operations tooexclude from hello operations granted by hello custom role.</span></span> |
| <span data-ttu-id="0dd96-280">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="0dd96-280">properties.assignableScopes</span></span> |<span data-ttu-id="0dd96-281">Sim</span><span class="sxs-lookup"><span data-stu-id="0dd96-281">Yes</span></span> |<span data-ttu-id="0dd96-282">String[]</span><span class="sxs-lookup"><span data-stu-id="0dd96-282">String[]</span></span> |<span data-ttu-id="0dd96-283">Uma matriz de escopos que Olá função personalizada pode ser usada.</span><span class="sxs-lookup"><span data-stu-id="0dd96-283">An array of scopes in which hello custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="0dd96-284">Resposta</span><span class="sxs-lookup"><span data-stu-id="0dd96-284">Response</span></span>
<span data-ttu-id="0dd96-285">Código de status: 201</span><span class="sxs-lookup"><span data-stu-id="0dd96-285">Status code: 201</span></span>

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

## <a name="update-a-custom-role"></a><span data-ttu-id="0dd96-286">Atualizar uma Função personalizada</span><span class="sxs-lookup"><span data-stu-id="0dd96-286">Update a Custom Role</span></span>
<span data-ttu-id="0dd96-287">Modificar uma função personalizada.</span><span class="sxs-lookup"><span data-stu-id="0dd96-287">Modify a custom role.</span></span>

<span data-ttu-id="0dd96-288">toomodify uma função personalizada, você deve ter acesso muito`Microsoft.Authorization/roleDefinitions/write` operação em todos os Olá `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="0dd96-288">toomodify a custom role, you must have access too`Microsoft.Authorization/roleDefinitions/write` operation on all hello `AssignableScopes`.</span></span> <span data-ttu-id="0dd96-289">De saudação funções internas, apenas *proprietário* e *administrador de acesso do usuário* recebem acesso toothis operação.</span><span class="sxs-lookup"><span data-stu-id="0dd96-289">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="0dd96-290">Para saber mais sobre as atribuições de função e o gerenciamento de acesso para recursos do Azure, consulte [Controle de Acesso Baseado em Função do Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="0dd96-290">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="0dd96-291">Solicitação</span><span class="sxs-lookup"><span data-stu-id="0dd96-291">Request</span></span>
<span data-ttu-id="0dd96-292">Saudação de uso **colocar** método com hello URI a seguir:</span><span class="sxs-lookup"><span data-stu-id="0dd96-292">Use hello **PUT** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="0dd96-293">Dentro de Olá URI, verifique Olá toocustomize substituições a seguir sua solicitação:</span><span class="sxs-lookup"><span data-stu-id="0dd96-293">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="0dd96-294">Substituir *{scope}* com hello primeiro *AssignableScope* de função personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="0dd96-294">Replace *{scope}* with hello first *AssignableScope* of hello custom role.</span></span> <span data-ttu-id="0dd96-295">Olá exemplos a seguir mostra como toospecify Olá escopo para os diferentes níveis:</span><span class="sxs-lookup"><span data-stu-id="0dd96-295">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="0dd96-296">Assinatura: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="0dd96-296">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="0dd96-297">Grupo de Recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="0dd96-297">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="0dd96-298">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="0dd96-298">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="0dd96-299">Substituir *{id de definição de função}* com identificador de GUID de saudação de função personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="0dd96-299">Replace *{role-definition-id}* with hello GUID identifier of hello custom role.</span></span>
3. <span data-ttu-id="0dd96-300">Substitua *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="0dd96-300">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="0dd96-301">Corpo da solicitação Olá, fornece valores Olá Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="0dd96-301">For hello request body, provide hello values in hello following format:</span></span>

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

| <span data-ttu-id="0dd96-302">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="0dd96-302">Element Name</span></span> | <span data-ttu-id="0dd96-303">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="0dd96-303">Required</span></span> | <span data-ttu-id="0dd96-304">Tipo</span><span class="sxs-lookup"><span data-stu-id="0dd96-304">Type</span></span> | <span data-ttu-id="0dd96-305">Descrição</span><span class="sxs-lookup"><span data-stu-id="0dd96-305">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0dd96-306">name</span><span class="sxs-lookup"><span data-stu-id="0dd96-306">name</span></span> |<span data-ttu-id="0dd96-307">Sim</span><span class="sxs-lookup"><span data-stu-id="0dd96-307">Yes</span></span> |<span data-ttu-id="0dd96-308">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0dd96-308">String</span></span> |<span data-ttu-id="0dd96-309">Identificador GUID de função personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="0dd96-309">GUID identifier of hello custom role.</span></span> |
| <span data-ttu-id="0dd96-310">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="0dd96-310">properties.roleName</span></span> |<span data-ttu-id="0dd96-311">Sim</span><span class="sxs-lookup"><span data-stu-id="0dd96-311">Yes</span></span> |<span data-ttu-id="0dd96-312">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0dd96-312">String</span></span> |<span data-ttu-id="0dd96-313">Nome para exibição da saudação atualizado função personalizada.</span><span class="sxs-lookup"><span data-stu-id="0dd96-313">Display name of hello updated custom role.</span></span> |
| <span data-ttu-id="0dd96-314">properties.description</span><span class="sxs-lookup"><span data-stu-id="0dd96-314">properties.description</span></span> |<span data-ttu-id="0dd96-315">Não</span><span class="sxs-lookup"><span data-stu-id="0dd96-315">No</span></span> |<span data-ttu-id="0dd96-316">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0dd96-316">String</span></span> |<span data-ttu-id="0dd96-317">Descrição da saudação atualizado função personalizada.</span><span class="sxs-lookup"><span data-stu-id="0dd96-317">Description of hello updated custom role.</span></span> |
| <span data-ttu-id="0dd96-318">properties.type</span><span class="sxs-lookup"><span data-stu-id="0dd96-318">properties.type</span></span> |<span data-ttu-id="0dd96-319">Sim</span><span class="sxs-lookup"><span data-stu-id="0dd96-319">Yes</span></span> |<span data-ttu-id="0dd96-320">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0dd96-320">String</span></span> |<span data-ttu-id="0dd96-321">Definir muito "CustomRole".</span><span class="sxs-lookup"><span data-stu-id="0dd96-321">Set too"CustomRole."</span></span> |
| <span data-ttu-id="0dd96-322">properties.permissions.actions</span><span class="sxs-lookup"><span data-stu-id="0dd96-322">properties.permissions.actions</span></span> |<span data-ttu-id="0dd96-323">Sim</span><span class="sxs-lookup"><span data-stu-id="0dd96-323">Yes</span></span> |<span data-ttu-id="0dd96-324">String[]</span><span class="sxs-lookup"><span data-stu-id="0dd96-324">String[]</span></span> |<span data-ttu-id="0dd96-325">Uma matriz de cadeias de caracteres de ação especificando Olá Olá de toowhich operações atualizada função personalizada que concede acesso.</span><span class="sxs-lookup"><span data-stu-id="0dd96-325">An array of action strings specifying hello operations toowhich hello updated custom role grants access.</span></span> |
| <span data-ttu-id="0dd96-326">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="0dd96-326">properties.permissions.notActions</span></span> |<span data-ttu-id="0dd96-327">Não</span><span class="sxs-lookup"><span data-stu-id="0dd96-327">No</span></span> |<span data-ttu-id="0dd96-328">String[]</span><span class="sxs-lookup"><span data-stu-id="0dd96-328">String[]</span></span> |<span data-ttu-id="0dd96-329">Uma matriz de ação de cadeias de caracteres especificando tooexclude de operações de saudação de operações de saudação quais Olá atualizado concessões de função personalizada.</span><span class="sxs-lookup"><span data-stu-id="0dd96-329">An array of action strings specifying hello operations tooexclude from hello operations which hello updated custom role grants.</span></span> |
| <span data-ttu-id="0dd96-330">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="0dd96-330">properties.assignableScopes</span></span> |<span data-ttu-id="0dd96-331">Sim</span><span class="sxs-lookup"><span data-stu-id="0dd96-331">Yes</span></span> |<span data-ttu-id="0dd96-332">String[]</span><span class="sxs-lookup"><span data-stu-id="0dd96-332">String[]</span></span> |<span data-ttu-id="0dd96-333">Uma matriz de escopos que Olá atualizada função personalizada pode ser usada.</span><span class="sxs-lookup"><span data-stu-id="0dd96-333">An array of scopes in which hello updated custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="0dd96-334">Resposta</span><span class="sxs-lookup"><span data-stu-id="0dd96-334">Response</span></span>
<span data-ttu-id="0dd96-335">Código de status: 201</span><span class="sxs-lookup"><span data-stu-id="0dd96-335">Status code: 201</span></span>

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

## <a name="delete-a-custom-role"></a><span data-ttu-id="0dd96-336">Excluir uma Função personalizada</span><span class="sxs-lookup"><span data-stu-id="0dd96-336">Delete a Custom Role</span></span>
<span data-ttu-id="0dd96-337">Excluir uma função personalizada.</span><span class="sxs-lookup"><span data-stu-id="0dd96-337">Delete a custom role.</span></span>

<span data-ttu-id="0dd96-338">toodelete uma função personalizada, você deve ter acesso muito`Microsoft.Authorization/roleDefinitions/delete` operação em todos os Olá `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="0dd96-338">toodelete a custom role, you must have access too`Microsoft.Authorization/roleDefinitions/delete` operation on all hello `AssignableScopes`.</span></span> <span data-ttu-id="0dd96-339">De saudação funções internas, apenas *proprietário* e *administrador de acesso do usuário* recebem acesso toothis operação.</span><span class="sxs-lookup"><span data-stu-id="0dd96-339">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="0dd96-340">Para saber mais sobre as atribuições de função e o gerenciamento de acesso para recursos do Azure, consulte [Controle de Acesso Baseado em Função do Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="0dd96-340">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="0dd96-341">Solicitação</span><span class="sxs-lookup"><span data-stu-id="0dd96-341">Request</span></span>
<span data-ttu-id="0dd96-342">Saudação de uso **excluir** método com hello URI a seguir:</span><span class="sxs-lookup"><span data-stu-id="0dd96-342">Use hello **DELETE** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="0dd96-343">Dentro de Olá URI, verifique Olá toocustomize substituições a seguir sua solicitação:</span><span class="sxs-lookup"><span data-stu-id="0dd96-343">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="0dd96-344">Substituir *{scope}* com escopo de saudação que deseja definição de função toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="0dd96-344">Replace *{scope}* with hello scope at which you wish toodelete hello role definition.</span></span> <span data-ttu-id="0dd96-345">Olá exemplos a seguir mostra como toospecify Olá escopo para os diferentes níveis:</span><span class="sxs-lookup"><span data-stu-id="0dd96-345">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="0dd96-346">Assinatura: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="0dd96-346">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="0dd96-347">Grupo de Recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="0dd96-347">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="0dd96-348">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="0dd96-348">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="0dd96-349">Substituir *{id de definição de função}* com a id de definição de função hello GUID de função personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="0dd96-349">Replace *{role-definition-id}* with hello GUID role definition id of hello custom role.</span></span>
3. <span data-ttu-id="0dd96-350">Substitua *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="0dd96-350">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="0dd96-351">Response</span><span class="sxs-lookup"><span data-stu-id="0dd96-351">Response</span></span>
<span data-ttu-id="0dd96-352">Código de status: 200</span><span class="sxs-lookup"><span data-stu-id="0dd96-352">Status code: 200</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0dd96-353">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0dd96-353">Next steps</span></span>

[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]
