---
title: "Controle de acesso baseado em função com REST – Azure AD | Microsoft Docs"
description: "Gerenciar o controle de acesso com base em função com a API REST"
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
ms.openlocfilehash: a5c19fd87ce1ae3e199bf1dfc8cf82f5653baac2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-role-based-access-control-with-the-rest-api"></a><span data-ttu-id="f250e-103">Gerenciar o Controle de Acesso com Base em Função com a API REST</span><span class="sxs-lookup"><span data-stu-id="f250e-103">Manage Role-Based Access Control with the REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f250e-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f250e-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="f250e-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="f250e-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="f250e-106">API REST</span><span class="sxs-lookup"><span data-stu-id="f250e-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="f250e-107">O RBAC (controle de acesso baseado em função) no portal do Azure e na API do Azure Resource Manager ajuda você a gerenciar o acesso à sua assinatura e aos seus recursos em um nível detalhado.</span><span class="sxs-lookup"><span data-stu-id="f250e-107">Role-Based Access Control (RBAC) in the Azure portal and Azure Resource Manager API helps you manage access to your subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="f250e-108">Com esse recurso, você pode conceder acesso aos usuários, grupos ou entidades de serviço do Active Directory atribuindo algumas funções para eles em um determinado escopo.</span><span class="sxs-lookup"><span data-stu-id="f250e-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles to them at a particular scope.</span></span>

## <a name="list-all-role-assignments"></a><span data-ttu-id="f250e-109">Lista todas as atribuições de função</span><span class="sxs-lookup"><span data-stu-id="f250e-109">List all role assignments</span></span>
<span data-ttu-id="f250e-110">Lista todas as atribuições de função no escopo e sub-escopos especificados.</span><span class="sxs-lookup"><span data-stu-id="f250e-110">Lists all the role assignments at the specified scope and subscopes.</span></span>

<span data-ttu-id="f250e-111">Para listar as atribuições de função, é necessário ter acesso à operação `Microsoft.Authorization/roleAssignments/read` no escopo.</span><span class="sxs-lookup"><span data-stu-id="f250e-111">To list role assignments, you must have access to `Microsoft.Authorization/roleAssignments/read` operation at the scope.</span></span> <span data-ttu-id="f250e-112">Todas as funções internas recebem acesso a essa operação.</span><span class="sxs-lookup"><span data-stu-id="f250e-112">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="f250e-113">Para saber mais sobre as atribuições de função e o gerenciamento de acesso para recursos do Azure, consulte [Controle de Acesso Baseado em Função do Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f250e-113">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="f250e-114">Solicitação</span><span class="sxs-lookup"><span data-stu-id="f250e-114">Request</span></span>
<span data-ttu-id="f250e-115">Use o método **GET** com o seguinte URI:</span><span class="sxs-lookup"><span data-stu-id="f250e-115">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments?api-version={api-version}&$filter={filter}

<span data-ttu-id="f250e-116">Dentro do URI, faça as seguintes substituições para personalizar sua solicitação:</span><span class="sxs-lookup"><span data-stu-id="f250e-116">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="f250e-117">Substitua *{scope}* pelo escopo para o qual você deseja listar as atribuições de função.</span><span class="sxs-lookup"><span data-stu-id="f250e-117">Replace *{scope}* with the scope for which you wish to list the role assignments.</span></span> <span data-ttu-id="f250e-118">Os exemplos a seguir mostram como especificar o escopo para diferentes níveis:</span><span class="sxs-lookup"><span data-stu-id="f250e-118">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="f250e-119">Assinatura: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="f250e-119">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="f250e-120">Grupo de Recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="f250e-120">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="f250e-121">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="f250e-121">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="f250e-122">Substitua *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="f250e-122">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="f250e-123">Substitua *{filter}* pela condição que você deseja aplicar a fim de filtrar a lista de atribuições de função:</span><span class="sxs-lookup"><span data-stu-id="f250e-123">Replace *{filter}* with the condition that you wish to apply to filter the role assignment list:</span></span>

   * <span data-ttu-id="f250e-124">Liste atribuições de função para apenas o escopo especificado, não incluindo as atribuições de função em sub-escopos: `atScope()`</span><span class="sxs-lookup"><span data-stu-id="f250e-124">List role assignments for only the specified scope, not including the role assignments at subscopes: `atScope()`</span></span>    
   * <span data-ttu-id="f250e-125">Liste atribuições de função para um usuário, grupo ou aplicativo específico: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span><span class="sxs-lookup"><span data-stu-id="f250e-125">List role assignments for a specific user, group, or application: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span></span>  
   * <span data-ttu-id="f250e-126">Liste atribuições de função para um usuário específico, incluindo aqueles herdados de grupos | `assignedTo('{objectId of user}')`</span><span class="sxs-lookup"><span data-stu-id="f250e-126">List role assignments for a specific user, including ones inherited from groups | `assignedTo('{objectId of user}')`</span></span>

### <a name="response"></a><span data-ttu-id="f250e-127">Response</span><span class="sxs-lookup"><span data-stu-id="f250e-127">Response</span></span>
<span data-ttu-id="f250e-128">Código de status: 200</span><span class="sxs-lookup"><span data-stu-id="f250e-128">Status code: 200</span></span>

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

## <a name="get-information-about-a-role-assignment"></a><span data-ttu-id="f250e-129">Obter informações sobre uma atribuição de função</span><span class="sxs-lookup"><span data-stu-id="f250e-129">Get information about a role assignment</span></span>
<span data-ttu-id="f250e-130">Obtém informações sobre uma atribuição de função única especificada pelo identificador de atribuição de função.</span><span class="sxs-lookup"><span data-stu-id="f250e-130">Gets information about a single role assignment specified by the role assignment identifier.</span></span>

<span data-ttu-id="f250e-131">Para saber mais sobre uma atribuição de função, é necessário ter acesso à operação `Microsoft.Authorization/roleAssignments/read` .</span><span class="sxs-lookup"><span data-stu-id="f250e-131">To get information about a role assignment, you must have access to `Microsoft.Authorization/roleAssignments/read` operation.</span></span> <span data-ttu-id="f250e-132">Todas as funções internas recebem acesso a essa operação.</span><span class="sxs-lookup"><span data-stu-id="f250e-132">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="f250e-133">Para saber mais sobre as atribuições de função e o gerenciamento de acesso para recursos do Azure, consulte [Controle de Acesso Baseado em Função do Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f250e-133">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="f250e-134">Solicitação</span><span class="sxs-lookup"><span data-stu-id="f250e-134">Request</span></span>
<span data-ttu-id="f250e-135">Use o método **GET** com o seguinte URI:</span><span class="sxs-lookup"><span data-stu-id="f250e-135">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="f250e-136">Dentro do URI, faça as seguintes substituições para personalizar sua solicitação:</span><span class="sxs-lookup"><span data-stu-id="f250e-136">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="f250e-137">Substitua *{scope}* pelo escopo para o qual você deseja listar as atribuições de função.</span><span class="sxs-lookup"><span data-stu-id="f250e-137">Replace *{scope}* with the scope for which you wish to list the role assignments.</span></span> <span data-ttu-id="f250e-138">Os exemplos a seguir mostram como especificar o escopo para diferentes níveis:</span><span class="sxs-lookup"><span data-stu-id="f250e-138">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="f250e-139">Assinatura: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="f250e-139">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="f250e-140">Grupo de Recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="f250e-140">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="f250e-141">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="f250e-141">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="f250e-142">Substitua *{role-assignment-id}* pelo identificador GUID da atribuição de função.</span><span class="sxs-lookup"><span data-stu-id="f250e-142">Replace *{role-assignment-id}* with the GUID identifier of the role assignment.</span></span>
3. <span data-ttu-id="f250e-143">Substitua *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="f250e-143">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="f250e-144">Response</span><span class="sxs-lookup"><span data-stu-id="f250e-144">Response</span></span>
<span data-ttu-id="f250e-145">Código de status: 200</span><span class="sxs-lookup"><span data-stu-id="f250e-145">Status code: 200</span></span>

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

## <a name="create-a-role-assignment"></a><span data-ttu-id="f250e-146">Criar uma atribuição de função</span><span class="sxs-lookup"><span data-stu-id="f250e-146">Create a Role Assignment</span></span>
<span data-ttu-id="f250e-147">Crie uma atribuição de função no escopo especificado para a entidade especificada, concedendo a função especificada.</span><span class="sxs-lookup"><span data-stu-id="f250e-147">Create a role assignment at the specified scope for the specified principal granting the specified role.</span></span>

<span data-ttu-id="f250e-148">Para criar uma atribuição de função, é necessário ter acesso à operação `Microsoft.Authorization/roleAssignments/write` .</span><span class="sxs-lookup"><span data-stu-id="f250e-148">To create a role assignment, you must have access to `Microsoft.Authorization/roleAssignments/write` operation.</span></span> <span data-ttu-id="f250e-149">Das funções internas, somente *Proprietário* e *Administrador do Acesso do Usuário* recebem permissão para acessar essa operação.</span><span class="sxs-lookup"><span data-stu-id="f250e-149">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="f250e-150">Para saber mais sobre as atribuições de função e o gerenciamento de acesso para recursos do Azure, consulte [Controle de Acesso Baseado em Função do Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f250e-150">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="f250e-151">Solicitação</span><span class="sxs-lookup"><span data-stu-id="f250e-151">Request</span></span>
<span data-ttu-id="f250e-152">Use o método **PUT** com o seguinte URI:</span><span class="sxs-lookup"><span data-stu-id="f250e-152">Use the **PUT** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="f250e-153">Dentro do URI, faça as seguintes substituições para personalizar sua solicitação:</span><span class="sxs-lookup"><span data-stu-id="f250e-153">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="f250e-154">Substitua *{scope}* pelo escopo para o qual você deseja criar as atribuições de função.</span><span class="sxs-lookup"><span data-stu-id="f250e-154">Replace *{scope}* with the scope at which you wish to create the role assignments.</span></span> <span data-ttu-id="f250e-155">Quando você cria uma atribuição de função em um escopo pai, todos os escopos filho herdam a mesma atribuição de função.</span><span class="sxs-lookup"><span data-stu-id="f250e-155">When you create a role assignment at a parent scope, all child scopes inherit the same role assignment.</span></span> <span data-ttu-id="f250e-156">Os exemplos a seguir mostram como especificar o escopo para diferentes níveis:</span><span class="sxs-lookup"><span data-stu-id="f250e-156">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="f250e-157">Assinatura: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="f250e-157">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="f250e-158">Grupo de Recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="f250e-158">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>   
   * <span data-ttu-id="f250e-159">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="f250e-159">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="f250e-160">Substitua *{role-assignment-id}* pelo novo GUID, que se torna o identificador GUID da nova atribuição de função.</span><span class="sxs-lookup"><span data-stu-id="f250e-160">Replace *{role-assignment-id}* with a new GUID, which becomes the GUID identifier of the new role assignment.</span></span>
3. <span data-ttu-id="f250e-161">Substitua *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="f250e-161">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="f250e-162">Para o corpo da solicitação, forneça os valores no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="f250e-162">For the request body, provide the values in the following format:</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b"
  }
}

```

| <span data-ttu-id="f250e-163">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="f250e-163">Element Name</span></span> | <span data-ttu-id="f250e-164">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="f250e-164">Required</span></span> | <span data-ttu-id="f250e-165">Tipo</span><span class="sxs-lookup"><span data-stu-id="f250e-165">Type</span></span> | <span data-ttu-id="f250e-166">Descrição</span><span class="sxs-lookup"><span data-stu-id="f250e-166">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f250e-167">roleDefinitionId</span><span class="sxs-lookup"><span data-stu-id="f250e-167">roleDefinitionId</span></span> |<span data-ttu-id="f250e-168">Sim</span><span class="sxs-lookup"><span data-stu-id="f250e-168">Yes</span></span> |<span data-ttu-id="f250e-169">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f250e-169">String</span></span> |<span data-ttu-id="f250e-170">Identificador da função.</span><span class="sxs-lookup"><span data-stu-id="f250e-170">The identifier of the role.</span></span> <span data-ttu-id="f250e-171">O formato do identificador é: `{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span><span class="sxs-lookup"><span data-stu-id="f250e-171">The format of the identifier is: `{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span></span> |
| <span data-ttu-id="f250e-172">principalId</span><span class="sxs-lookup"><span data-stu-id="f250e-172">principalId</span></span> |<span data-ttu-id="f250e-173">Sim</span><span class="sxs-lookup"><span data-stu-id="f250e-173">Yes</span></span> |<span data-ttu-id="f250e-174">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f250e-174">String</span></span> |<span data-ttu-id="f250e-175">ID de objeto da entidade de segurança do Azure AD (usuário, grupo ou entidade de serviço) para o qual a função é atribuída.</span><span class="sxs-lookup"><span data-stu-id="f250e-175">objectId of the Azure AD principal (user, group, or service principal) to which the role is assigned.</span></span> |

### <a name="response"></a><span data-ttu-id="f250e-176">Response</span><span class="sxs-lookup"><span data-stu-id="f250e-176">Response</span></span>
<span data-ttu-id="f250e-177">Código de status: 201</span><span class="sxs-lookup"><span data-stu-id="f250e-177">Status code: 201</span></span>

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

## <a name="delete-a-role-assignment"></a><span data-ttu-id="f250e-178">Excluir uma atribuição de função</span><span class="sxs-lookup"><span data-stu-id="f250e-178">Delete a Role Assignment</span></span>
<span data-ttu-id="f250e-179">Exclua uma atribuição de função no escopo especificado.</span><span class="sxs-lookup"><span data-stu-id="f250e-179">Delete a role assignment at the specified scope.</span></span>

<span data-ttu-id="f250e-180">Para excluir uma atribuição de função, é necessário ter acesso à operação `Microsoft.Authorization/roleAssignments/delete` .</span><span class="sxs-lookup"><span data-stu-id="f250e-180">To delete a role assignment, you must have access to the `Microsoft.Authorization/roleAssignments/delete` operation.</span></span> <span data-ttu-id="f250e-181">Das funções internas, somente *Proprietário* e *Administrador do Acesso do Usuário* recebem permissão para acessar essa operação.</span><span class="sxs-lookup"><span data-stu-id="f250e-181">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="f250e-182">Para saber mais sobre as atribuições de função e o gerenciamento de acesso para recursos do Azure, consulte [Controle de Acesso Baseado em Função do Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f250e-182">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="f250e-183">Solicitação</span><span class="sxs-lookup"><span data-stu-id="f250e-183">Request</span></span>
<span data-ttu-id="f250e-184">Use o método **DELETE** com o seguinte URI:</span><span class="sxs-lookup"><span data-stu-id="f250e-184">Use the **DELETE** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="f250e-185">Dentro do URI, faça as seguintes substituições para personalizar sua solicitação:</span><span class="sxs-lookup"><span data-stu-id="f250e-185">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="f250e-186">Substitua *{scope}* pelo escopo para o qual você deseja criar as atribuições de função.</span><span class="sxs-lookup"><span data-stu-id="f250e-186">Replace *{scope}* with the scope at which you wish to create the role assignments.</span></span> <span data-ttu-id="f250e-187">Os exemplos a seguir mostram como especificar o escopo para diferentes níveis:</span><span class="sxs-lookup"><span data-stu-id="f250e-187">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="f250e-188">Assinatura: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="f250e-188">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="f250e-189">Grupo de Recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="f250e-189">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="f250e-190">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="f250e-190">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="f250e-191">Substitua *{role-assignment-id}* pelo GUID da ID da atribuição de função.</span><span class="sxs-lookup"><span data-stu-id="f250e-191">Replace *{role-assignment-id}* with the role assignment id GUID.</span></span>
3. <span data-ttu-id="f250e-192">Substitua *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="f250e-192">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="f250e-193">Response</span><span class="sxs-lookup"><span data-stu-id="f250e-193">Response</span></span>
<span data-ttu-id="f250e-194">Código de status: 200</span><span class="sxs-lookup"><span data-stu-id="f250e-194">Status code: 200</span></span>

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

## <a name="list-all-roles"></a><span data-ttu-id="f250e-195">Lista todas as Funções</span><span class="sxs-lookup"><span data-stu-id="f250e-195">List all Roles</span></span>
<span data-ttu-id="f250e-196">Lista todas as funções que estão disponíveis para atribuição no escopo especificado.</span><span class="sxs-lookup"><span data-stu-id="f250e-196">Lists all the roles that are available for assignment at the specified scope.</span></span>

<span data-ttu-id="f250e-197">Para listar as funções, é necessário ter acesso à operação `Microsoft.Authorization/roleDefinitions/read` no escopo.</span><span class="sxs-lookup"><span data-stu-id="f250e-197">To list roles, you must have access to `Microsoft.Authorization/roleDefinitions/read` operation at the scope.</span></span> <span data-ttu-id="f250e-198">Todas as funções internas recebem acesso a essa operação.</span><span class="sxs-lookup"><span data-stu-id="f250e-198">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="f250e-199">Para saber mais sobre as atribuições de função e o gerenciamento de acesso para recursos do Azure, consulte [Controle de Acesso Baseado em Função do Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f250e-199">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="f250e-200">Solicitação</span><span class="sxs-lookup"><span data-stu-id="f250e-200">Request</span></span>
<span data-ttu-id="f250e-201">Use o método **GET** com o seguinte URI:</span><span class="sxs-lookup"><span data-stu-id="f250e-201">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?api-version={api-version}&$filter={filter}

<span data-ttu-id="f250e-202">Dentro do URI, faça as seguintes substituições para personalizar sua solicitação:</span><span class="sxs-lookup"><span data-stu-id="f250e-202">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="f250e-203">Substitua *{scope}* pelo escopo para o qual você deseja listar as funções.</span><span class="sxs-lookup"><span data-stu-id="f250e-203">Replace *{scope}* with the scope for which you wish to list the roles.</span></span> <span data-ttu-id="f250e-204">Os exemplos a seguir mostram como especificar o escopo para diferentes níveis:</span><span class="sxs-lookup"><span data-stu-id="f250e-204">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="f250e-205">Assinatura: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="f250e-205">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="f250e-206">Grupo de Recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="f250e-206">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="f250e-207">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="f250e-207">Resource /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="f250e-208">Substitua *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="f250e-208">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="f250e-209">Substitua *{filter}* pela condição que você deseja aplicar a fim de filtrar a lista de funções:</span><span class="sxs-lookup"><span data-stu-id="f250e-209">Replace *{filter}* with the condition that you wish to apply to filter the list of roles:</span></span>

   * <span data-ttu-id="f250e-210">Liste funções disponíveis para atribuição no escopo especificado e qualquer de seus escopos filho: `atScopeAndBelow()`</span><span class="sxs-lookup"><span data-stu-id="f250e-210">List roles available for assignment at the specified scope and any of its child scopes: `atScopeAndBelow()`</span></span>
   * <span data-ttu-id="f250e-211">Pesquise uma função usando o nome de exibição exato: `roleName%20eq%20'{role-display-name}'`.</span><span class="sxs-lookup"><span data-stu-id="f250e-211">Search for a role using exact display name: `roleName%20eq%20'{role-display-name}'`.</span></span> <span data-ttu-id="f250e-212">Use a forma codificada da URL do nome de exibição exato da função.</span><span class="sxs-lookup"><span data-stu-id="f250e-212">Use the URL encoded form of the exact display name of the role.</span></span> <span data-ttu-id="f250e-213">Por exemplo, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span><span class="sxs-lookup"><span data-stu-id="f250e-213">For instance, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span></span>

### <a name="response"></a><span data-ttu-id="f250e-214">Response</span><span class="sxs-lookup"><span data-stu-id="f250e-214">Response</span></span>
<span data-ttu-id="f250e-215">Código de status: 200</span><span class="sxs-lookup"><span data-stu-id="f250e-215">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access to them, and not the virtual network or storage account they\u2019re connected to.",
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

## <a name="get-information-about-a-role"></a><span data-ttu-id="f250e-216">Obter informações sobre uma Função</span><span class="sxs-lookup"><span data-stu-id="f250e-216">Get information about a Role</span></span>
<span data-ttu-id="f250e-217">Obtém informações sobre uma função única especificada pelo identificador de definição da função.</span><span class="sxs-lookup"><span data-stu-id="f250e-217">Gets information about a single role specified by the role definition identifier.</span></span> <span data-ttu-id="f250e-218">Para obter informações sobre uma única função usando seu nome de exibição, consulte [Listar todas as funções](role-based-access-control-manage-access-rest.md#list-all-roles).</span><span class="sxs-lookup"><span data-stu-id="f250e-218">To get information about a single role using its display name, see [List all roles](role-based-access-control-manage-access-rest.md#list-all-roles).</span></span>

<span data-ttu-id="f250e-219">Para saber mais sobre uma função, é necessário ter acesso à operação `Microsoft.Authorization/roleDefinitions/read` .</span><span class="sxs-lookup"><span data-stu-id="f250e-219">To get information about a role, you must have access to `Microsoft.Authorization/roleDefinitions/read` operation.</span></span> <span data-ttu-id="f250e-220">Todas as funções internas recebem acesso a essa operação.</span><span class="sxs-lookup"><span data-stu-id="f250e-220">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="f250e-221">Para saber mais sobre as atribuições de função e o gerenciamento de acesso para recursos do Azure, consulte [Controle de Acesso Baseado em Função do Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f250e-221">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="f250e-222">Solicitação</span><span class="sxs-lookup"><span data-stu-id="f250e-222">Request</span></span>
<span data-ttu-id="f250e-223">Use o método **GET** com o seguinte URI:</span><span class="sxs-lookup"><span data-stu-id="f250e-223">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="f250e-224">Dentro do URI, faça as seguintes substituições para personalizar sua solicitação:</span><span class="sxs-lookup"><span data-stu-id="f250e-224">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="f250e-225">Substitua *{scope}* pelo escopo para o qual você deseja listar as atribuições de função.</span><span class="sxs-lookup"><span data-stu-id="f250e-225">Replace *{scope}* with the scope for which you wish to list the role assignments.</span></span> <span data-ttu-id="f250e-226">Os exemplos a seguir mostram como especificar o escopo para diferentes níveis:</span><span class="sxs-lookup"><span data-stu-id="f250e-226">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="f250e-227">Assinatura: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="f250e-227">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="f250e-228">Grupo de Recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="f250e-228">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="f250e-229">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="f250e-229">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="f250e-230">Substitua *{role-definition-id}* pelo identificador GUID de definição da função.</span><span class="sxs-lookup"><span data-stu-id="f250e-230">Replace *{role-definition-id}* with the GUID identifier of the role definition.</span></span>
3. <span data-ttu-id="f250e-231">Substitua *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="f250e-231">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="f250e-232">Response</span><span class="sxs-lookup"><span data-stu-id="f250e-232">Response</span></span>
<span data-ttu-id="f250e-233">Código de status: 200</span><span class="sxs-lookup"><span data-stu-id="f250e-233">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access to them, and not the virtual network or storage account they\u2019re connected to.",
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

## <a name="create-a-custom-role"></a><span data-ttu-id="f250e-234">Criar uma Função personalizada</span><span class="sxs-lookup"><span data-stu-id="f250e-234">Create a Custom Role</span></span>
<span data-ttu-id="f250e-235">Criar uma função personalizada.</span><span class="sxs-lookup"><span data-stu-id="f250e-235">Create a custom role.</span></span>

<span data-ttu-id="f250e-236">Para criar uma função personalizada, é necessário ter acesso à operação `Microsoft.Authorization/roleDefinitions/write` em todos os `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="f250e-236">To create a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/write` operation on all the `AssignableScopes`.</span></span> <span data-ttu-id="f250e-237">Das funções internas, somente *Proprietário* e *Administrador do Acesso do Usuário* recebem permissão para acessar essa operação.</span><span class="sxs-lookup"><span data-stu-id="f250e-237">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="f250e-238">Para saber mais sobre as atribuições de função e o gerenciamento de acesso para recursos do Azure, consulte [Controle de Acesso Baseado em Função do Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f250e-238">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="f250e-239">Solicitação</span><span class="sxs-lookup"><span data-stu-id="f250e-239">Request</span></span>
<span data-ttu-id="f250e-240">Use o método **PUT** com o seguinte URI:</span><span class="sxs-lookup"><span data-stu-id="f250e-240">Use the **PUT** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="f250e-241">Dentro do URI, faça as seguintes substituições para personalizar sua solicitação:</span><span class="sxs-lookup"><span data-stu-id="f250e-241">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="f250e-242">Substitua *{scope}* pelo primeiro *AssignableScope* da função personalizada.</span><span class="sxs-lookup"><span data-stu-id="f250e-242">Replace *{scope}* with the first *AssignableScope* of the custom role.</span></span> <span data-ttu-id="f250e-243">Os exemplos a seguir mostram como especificar o escopo para diferentes níveis.</span><span class="sxs-lookup"><span data-stu-id="f250e-243">The following examples show how to specify the scope for different levels.</span></span>

   * <span data-ttu-id="f250e-244">Assinatura: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="f250e-244">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="f250e-245">Grupo de Recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="f250e-245">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="f250e-246">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="f250e-246">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="f250e-247">Substitua *{role-definition-id}* pelo novo GUID, que se torna o identificador GUID da nova função personalizada.</span><span class="sxs-lookup"><span data-stu-id="f250e-247">Replace *{role-definition-id}* with a new GUID, which becomes the GUID identifier of the new custom role.</span></span>
3. <span data-ttu-id="f250e-248">Substitua *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="f250e-248">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="f250e-249">Para o corpo da solicitação, forneça os valores no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="f250e-249">For the request body, provide the values in the following format:</span></span>

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

| <span data-ttu-id="f250e-250">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="f250e-250">Element Name</span></span> | <span data-ttu-id="f250e-251">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="f250e-251">Required</span></span> | <span data-ttu-id="f250e-252">Tipo</span><span class="sxs-lookup"><span data-stu-id="f250e-252">Type</span></span> | <span data-ttu-id="f250e-253">Descrição</span><span class="sxs-lookup"><span data-stu-id="f250e-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f250e-254">name</span><span class="sxs-lookup"><span data-stu-id="f250e-254">name</span></span> |<span data-ttu-id="f250e-255">Sim</span><span class="sxs-lookup"><span data-stu-id="f250e-255">Yes</span></span> |<span data-ttu-id="f250e-256">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f250e-256">String</span></span> |<span data-ttu-id="f250e-257">Identificador GUID da função personalizada.</span><span class="sxs-lookup"><span data-stu-id="f250e-257">GUID identifier of the custom role.</span></span> |
| <span data-ttu-id="f250e-258">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="f250e-258">properties.roleName</span></span> |<span data-ttu-id="f250e-259">Sim</span><span class="sxs-lookup"><span data-stu-id="f250e-259">Yes</span></span> |<span data-ttu-id="f250e-260">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f250e-260">String</span></span> |<span data-ttu-id="f250e-261">Nome de exibição da função personalizada.</span><span class="sxs-lookup"><span data-stu-id="f250e-261">Display name of the custom role.</span></span> <span data-ttu-id="f250e-262">Tamanho máximo de 128 caracteres.</span><span class="sxs-lookup"><span data-stu-id="f250e-262">Maximum size 128 characters.</span></span> |
| <span data-ttu-id="f250e-263">properties.description</span><span class="sxs-lookup"><span data-stu-id="f250e-263">properties.description</span></span> |<span data-ttu-id="f250e-264">Não</span><span class="sxs-lookup"><span data-stu-id="f250e-264">No</span></span> |<span data-ttu-id="f250e-265">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f250e-265">String</span></span> |<span data-ttu-id="f250e-266">Descrição da função personalizada.</span><span class="sxs-lookup"><span data-stu-id="f250e-266">Description of the custom role.</span></span> <span data-ttu-id="f250e-267">Tamanho máximo de 1024 caracteres.</span><span class="sxs-lookup"><span data-stu-id="f250e-267">Maximum size 1024 characters.</span></span> |
| <span data-ttu-id="f250e-268">properties.type</span><span class="sxs-lookup"><span data-stu-id="f250e-268">properties.type</span></span> |<span data-ttu-id="f250e-269">Sim</span><span class="sxs-lookup"><span data-stu-id="f250e-269">Yes</span></span> |<span data-ttu-id="f250e-270">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f250e-270">String</span></span> |<span data-ttu-id="f250e-271">Defina como "CustomRole".</span><span class="sxs-lookup"><span data-stu-id="f250e-271">Set to "CustomRole."</span></span> |
| <span data-ttu-id="f250e-272">properties.permissions.actions</span><span class="sxs-lookup"><span data-stu-id="f250e-272">properties.permissions.actions</span></span> |<span data-ttu-id="f250e-273">Sim</span><span class="sxs-lookup"><span data-stu-id="f250e-273">Yes</span></span> |<span data-ttu-id="f250e-274">String[]</span><span class="sxs-lookup"><span data-stu-id="f250e-274">String[]</span></span> |<span data-ttu-id="f250e-275">Uma matriz de cadeias de caracteres de ação especificando as operações concedidas pela função personalizada.</span><span class="sxs-lookup"><span data-stu-id="f250e-275">An array of action strings specifying the operations granted by the custom role.</span></span> |
| <span data-ttu-id="f250e-276">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="f250e-276">properties.permissions.notActions</span></span> |<span data-ttu-id="f250e-277">Não</span><span class="sxs-lookup"><span data-stu-id="f250e-277">No</span></span> |<span data-ttu-id="f250e-278">String[]</span><span class="sxs-lookup"><span data-stu-id="f250e-278">String[]</span></span> |<span data-ttu-id="f250e-279">Uma matriz de cadeias de caracteres de ação especificando as operações a serem excluídas das operações concedidas pela função personalizada.</span><span class="sxs-lookup"><span data-stu-id="f250e-279">An array of action strings specifying the operations to exclude from the operations granted by the custom role.</span></span> |
| <span data-ttu-id="f250e-280">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="f250e-280">properties.assignableScopes</span></span> |<span data-ttu-id="f250e-281">Sim</span><span class="sxs-lookup"><span data-stu-id="f250e-281">Yes</span></span> |<span data-ttu-id="f250e-282">String[]</span><span class="sxs-lookup"><span data-stu-id="f250e-282">String[]</span></span> |<span data-ttu-id="f250e-283">Uma matriz de escopos no qual a função personalizada pode ser usada.</span><span class="sxs-lookup"><span data-stu-id="f250e-283">An array of scopes in which the custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="f250e-284">Response</span><span class="sxs-lookup"><span data-stu-id="f250e-284">Response</span></span>
<span data-ttu-id="f250e-285">Código de status: 201</span><span class="sxs-lookup"><span data-stu-id="f250e-285">Status code: 201</span></span>

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

## <a name="update-a-custom-role"></a><span data-ttu-id="f250e-286">Atualizar uma Função personalizada</span><span class="sxs-lookup"><span data-stu-id="f250e-286">Update a Custom Role</span></span>
<span data-ttu-id="f250e-287">Modificar uma função personalizada.</span><span class="sxs-lookup"><span data-stu-id="f250e-287">Modify a custom role.</span></span>

<span data-ttu-id="f250e-288">Para modificar uma função personalizada, é necessário ter acesso à operação `Microsoft.Authorization/roleDefinitions/write` em todos os seus `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="f250e-288">To modify a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/write` operation on all the `AssignableScopes`.</span></span> <span data-ttu-id="f250e-289">Das funções internas, somente *Proprietário* e *Administrador do Acesso do Usuário* recebem permissão para acessar essa operação.</span><span class="sxs-lookup"><span data-stu-id="f250e-289">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="f250e-290">Para saber mais sobre as atribuições de função e o gerenciamento de acesso para recursos do Azure, consulte [Controle de Acesso Baseado em Função do Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f250e-290">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="f250e-291">Solicitação</span><span class="sxs-lookup"><span data-stu-id="f250e-291">Request</span></span>
<span data-ttu-id="f250e-292">Use o método **PUT** com o seguinte URI:</span><span class="sxs-lookup"><span data-stu-id="f250e-292">Use the **PUT** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="f250e-293">Dentro do URI, faça as seguintes substituições para personalizar sua solicitação:</span><span class="sxs-lookup"><span data-stu-id="f250e-293">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="f250e-294">Substitua *{scope}* pelo primeiro *AssignableScope* da função personalizada.</span><span class="sxs-lookup"><span data-stu-id="f250e-294">Replace *{scope}* with the first *AssignableScope* of the custom role.</span></span> <span data-ttu-id="f250e-295">Os exemplos a seguir mostram como especificar o escopo para diferentes níveis:</span><span class="sxs-lookup"><span data-stu-id="f250e-295">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="f250e-296">Assinatura: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="f250e-296">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="f250e-297">Grupo de Recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="f250e-297">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="f250e-298">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="f250e-298">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="f250e-299">Substitua *{role-definition-id}* pelo identificador GUID de definição da função personalizada.</span><span class="sxs-lookup"><span data-stu-id="f250e-299">Replace *{role-definition-id}* with the GUID identifier of the custom role.</span></span>
3. <span data-ttu-id="f250e-300">Substitua *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="f250e-300">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="f250e-301">Para o corpo da solicitação, forneça os valores no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="f250e-301">For the request body, provide the values in the following format:</span></span>

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

| <span data-ttu-id="f250e-302">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="f250e-302">Element Name</span></span> | <span data-ttu-id="f250e-303">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="f250e-303">Required</span></span> | <span data-ttu-id="f250e-304">Tipo</span><span class="sxs-lookup"><span data-stu-id="f250e-304">Type</span></span> | <span data-ttu-id="f250e-305">Descrição</span><span class="sxs-lookup"><span data-stu-id="f250e-305">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f250e-306">name</span><span class="sxs-lookup"><span data-stu-id="f250e-306">name</span></span> |<span data-ttu-id="f250e-307">Sim</span><span class="sxs-lookup"><span data-stu-id="f250e-307">Yes</span></span> |<span data-ttu-id="f250e-308">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f250e-308">String</span></span> |<span data-ttu-id="f250e-309">Identificador GUID da função personalizada.</span><span class="sxs-lookup"><span data-stu-id="f250e-309">GUID identifier of the custom role.</span></span> |
| <span data-ttu-id="f250e-310">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="f250e-310">properties.roleName</span></span> |<span data-ttu-id="f250e-311">Sim</span><span class="sxs-lookup"><span data-stu-id="f250e-311">Yes</span></span> |<span data-ttu-id="f250e-312">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f250e-312">String</span></span> |<span data-ttu-id="f250e-313">Nome de exibição da função personalizada a ser atualizada.</span><span class="sxs-lookup"><span data-stu-id="f250e-313">Display name of the updated custom role.</span></span> |
| <span data-ttu-id="f250e-314">properties.description</span><span class="sxs-lookup"><span data-stu-id="f250e-314">properties.description</span></span> |<span data-ttu-id="f250e-315">Não</span><span class="sxs-lookup"><span data-stu-id="f250e-315">No</span></span> |<span data-ttu-id="f250e-316">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f250e-316">String</span></span> |<span data-ttu-id="f250e-317">Nome de exibição da função personalizada atualizada.</span><span class="sxs-lookup"><span data-stu-id="f250e-317">Description of the updated custom role.</span></span> |
| <span data-ttu-id="f250e-318">properties.type</span><span class="sxs-lookup"><span data-stu-id="f250e-318">properties.type</span></span> |<span data-ttu-id="f250e-319">Sim</span><span class="sxs-lookup"><span data-stu-id="f250e-319">Yes</span></span> |<span data-ttu-id="f250e-320">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f250e-320">String</span></span> |<span data-ttu-id="f250e-321">Defina como "CustomRole".</span><span class="sxs-lookup"><span data-stu-id="f250e-321">Set to "CustomRole."</span></span> |
| <span data-ttu-id="f250e-322">properties.permissions.actions</span><span class="sxs-lookup"><span data-stu-id="f250e-322">properties.permissions.actions</span></span> |<span data-ttu-id="f250e-323">Sim</span><span class="sxs-lookup"><span data-stu-id="f250e-323">Yes</span></span> |<span data-ttu-id="f250e-324">String[]</span><span class="sxs-lookup"><span data-stu-id="f250e-324">String[]</span></span> |<span data-ttu-id="f250e-325">Uma matriz de cadeias de caracteres de ação especificando as operações para as quais a função personalizada atualizada concede acesso.</span><span class="sxs-lookup"><span data-stu-id="f250e-325">An array of action strings specifying the operations to which the updated custom role grants access.</span></span> |
| <span data-ttu-id="f250e-326">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="f250e-326">properties.permissions.notActions</span></span> |<span data-ttu-id="f250e-327">Não</span><span class="sxs-lookup"><span data-stu-id="f250e-327">No</span></span> |<span data-ttu-id="f250e-328">String[]</span><span class="sxs-lookup"><span data-stu-id="f250e-328">String[]</span></span> |<span data-ttu-id="f250e-329">Uma matriz de cadeias de caracteres de ação especificando as operações a serem excluídas das operações para as quais a função personalizada atualizada concede acesso.</span><span class="sxs-lookup"><span data-stu-id="f250e-329">An array of action strings specifying the operations to exclude from the operations which the updated custom role grants.</span></span> |
| <span data-ttu-id="f250e-330">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="f250e-330">properties.assignableScopes</span></span> |<span data-ttu-id="f250e-331">Sim</span><span class="sxs-lookup"><span data-stu-id="f250e-331">Yes</span></span> |<span data-ttu-id="f250e-332">String[]</span><span class="sxs-lookup"><span data-stu-id="f250e-332">String[]</span></span> |<span data-ttu-id="f250e-333">Uma matriz de escopos na qual a função personalizada atualizada pode ser usada.</span><span class="sxs-lookup"><span data-stu-id="f250e-333">An array of scopes in which the updated custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="f250e-334">Response</span><span class="sxs-lookup"><span data-stu-id="f250e-334">Response</span></span>
<span data-ttu-id="f250e-335">Código de status: 201</span><span class="sxs-lookup"><span data-stu-id="f250e-335">Status code: 201</span></span>

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

## <a name="delete-a-custom-role"></a><span data-ttu-id="f250e-336">Excluir uma Função personalizada</span><span class="sxs-lookup"><span data-stu-id="f250e-336">Delete a Custom Role</span></span>
<span data-ttu-id="f250e-337">Excluir uma função personalizada.</span><span class="sxs-lookup"><span data-stu-id="f250e-337">Delete a custom role.</span></span>

<span data-ttu-id="f250e-338">Para excluir uma função personalizada, é necessário ter acesso à operação `Microsoft.Authorization/roleDefinitions/delete` em todos os seus `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="f250e-338">To delete a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/delete` operation on all the `AssignableScopes`.</span></span> <span data-ttu-id="f250e-339">Das funções internas, somente *Proprietário* e *Administrador do Acesso do Usuário* recebem permissão para acessar essa operação.</span><span class="sxs-lookup"><span data-stu-id="f250e-339">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="f250e-340">Para saber mais sobre as atribuições de função e o gerenciamento de acesso para recursos do Azure, consulte [Controle de Acesso Baseado em Função do Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f250e-340">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="f250e-341">Solicitação</span><span class="sxs-lookup"><span data-stu-id="f250e-341">Request</span></span>
<span data-ttu-id="f250e-342">Use o método **DELETE** com o seguinte URI:</span><span class="sxs-lookup"><span data-stu-id="f250e-342">Use the **DELETE** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="f250e-343">Dentro do URI, faça as seguintes substituições para personalizar sua solicitação:</span><span class="sxs-lookup"><span data-stu-id="f250e-343">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="f250e-344">Substitua *{scope}* pelo escopo para o qual deseja você excluir as atribuições de função.</span><span class="sxs-lookup"><span data-stu-id="f250e-344">Replace *{scope}* with the scope at which you wish to delete the role definition.</span></span> <span data-ttu-id="f250e-345">Os exemplos a seguir mostram como especificar o escopo para diferentes níveis:</span><span class="sxs-lookup"><span data-stu-id="f250e-345">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="f250e-346">Assinatura: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="f250e-346">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="f250e-347">Grupo de Recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="f250e-347">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="f250e-348">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="f250e-348">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="f250e-349">Substitua *{role-definition-id}* pela definição de função do GUID da função personalizada.</span><span class="sxs-lookup"><span data-stu-id="f250e-349">Replace *{role-definition-id}* with the GUID role definition id of the custom role.</span></span>
3. <span data-ttu-id="f250e-350">Substitua *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="f250e-350">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="f250e-351">Response</span><span class="sxs-lookup"><span data-stu-id="f250e-351">Response</span></span>
<span data-ttu-id="f250e-352">Código de status: 200</span><span class="sxs-lookup"><span data-stu-id="f250e-352">Status code: 200</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f250e-353">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f250e-353">Next steps</span></span>

[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]
