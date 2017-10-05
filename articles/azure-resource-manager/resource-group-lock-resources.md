---
title: "Bloquear recursos do Azure para evitar alterações | Microsoft Docs"
description: "Impeça que os usuários atualizem ou excluam recursos críticos do Azure ao aplicar um bloqueio a todos os usuários e funções."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 53c57e8f-741c-4026-80e0-f4c02638c98b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: 44c87b00f4fc63dbfd45a07d9a8cddc5eaf1a65c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="lock-resources-to-prevent-unexpected-changes"></a><span data-ttu-id="acae8-103">Bloquear recursos para evitar alterações inesperadas</span><span class="sxs-lookup"><span data-stu-id="acae8-103">Lock resources to prevent unexpected changes</span></span> 
<span data-ttu-id="acae8-104">Como administrador, talvez você precise bloquear uma assinatura, um recurso ou grupo de recursos para impedir que outros usuários em sua organização excluam ou modifiquem acidentalmente recursos críticos.</span><span class="sxs-lookup"><span data-stu-id="acae8-104">As an administrator, you may need to lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="acae8-105">É possível definir o nível de bloqueio como **CanNotDelete** ou **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="acae8-105">You can set the lock level to **CanNotDelete** or **ReadOnly**.</span></span> 

* <span data-ttu-id="acae8-106">**CanNotDelete** significa que os usuários autorizados ainda poderão ler e modificar um recurso, mas não poderão excluir o recurso.</span><span class="sxs-lookup"><span data-stu-id="acae8-106">**CanNotDelete** means authorized users can still read and modify a resource, but they can't delete the resource.</span></span> 
* <span data-ttu-id="acae8-107">**ReadOnly** significa que os usuários autorizados poderão ler um recurso, mas não poderão excluir ou atualizar o recurso.</span><span class="sxs-lookup"><span data-stu-id="acae8-107">**ReadOnly** means authorized users can read a resource, but they can't delete or update the resource.</span></span> <span data-ttu-id="acae8-108">Aplicar esse bloqueio é semelhante ao restringir todos os usuários autorizados para as permissões concedidas pela função **Leitor**.</span><span class="sxs-lookup"><span data-stu-id="acae8-108">Applying this lock is similar to restricting all authorized users to the permissions granted by the **Reader** role.</span></span> 

## <a name="how-locks-are-applied"></a><span data-ttu-id="acae8-109">Como os bloqueios são aplicados</span><span class="sxs-lookup"><span data-stu-id="acae8-109">How locks are applied</span></span>

<span data-ttu-id="acae8-110">Quando você aplica um bloqueio a um escopo pai, todos os recursos filho herdam o mesmo bloqueio.</span><span class="sxs-lookup"><span data-stu-id="acae8-110">When you apply a lock at a parent scope, all resources within that scope inherit the same lock.</span></span> <span data-ttu-id="acae8-111">Até mesmo os recursos que você adiciona posteriormente herdam o bloqueio do pai.</span><span class="sxs-lookup"><span data-stu-id="acae8-111">Even resources you add later inherit the lock from the parent.</span></span> <span data-ttu-id="acae8-112">O bloqueio mais restritivo na herança terá precedência.</span><span class="sxs-lookup"><span data-stu-id="acae8-112">The most restrictive lock in the inheritance takes precedence.</span></span>

<span data-ttu-id="acae8-113">Ao contrário do controle de acesso baseado em função, é possível usar bloqueios de gerenciamento para aplicar uma restrição a todos os usuários e a todas as funções.</span><span class="sxs-lookup"><span data-stu-id="acae8-113">Unlike role-based access control, you use management locks to apply a restriction across all users and roles.</span></span> <span data-ttu-id="acae8-114">Para saber mais sobre como configurar permissões para usuários e funções, veja [Controle de Acesso Baseado em Função do Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="acae8-114">To learn about setting permissions for users and roles, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>

<span data-ttu-id="acae8-115">Bloqueios do Resource Manager se aplicam apenas às operações que ocorrem no plano de gerenciamento, que consistem em operações enviadas para `https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="acae8-115">Resource Manager locks apply only to operations that happen in the management plane, which consists of operations sent to `https://management.azure.com`.</span></span> <span data-ttu-id="acae8-116">Os bloqueios não restringem a maneira como os recursos executam suas próprias funções.</span><span class="sxs-lookup"><span data-stu-id="acae8-116">The locks do not restrict how resources perform their own functions.</span></span> <span data-ttu-id="acae8-117">Alterações de recursos são restritas, mas as operações de recursos não são restritas.</span><span class="sxs-lookup"><span data-stu-id="acae8-117">Resource changes are restricted, but resource operations are not restricted.</span></span> <span data-ttu-id="acae8-118">Por exemplo, um bloqueio ReadOnly em um Banco de Dados SQL impede que você exclua ou modifique o banco de dados, mas ele não impede que você crie, atualize ou exclua dados no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="acae8-118">For example, a ReadOnly lock on a SQL Database prevents you from deleting or modifying the database, but it does not prevent you from creating, updating, or deleting data in the database.</span></span> <span data-ttu-id="acae8-119">Transações de dados são permitidas porque essas operações não são enviadas para `https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="acae8-119">Data transactions are permitted because those operations are not sent to `https://management.azure.com`.</span></span>

<span data-ttu-id="acae8-120">A aplicação de **ReadOnly** pode gerar resultados inesperados, pois algumas operações que parecem operações de leitura exigem ações adicionais.</span><span class="sxs-lookup"><span data-stu-id="acae8-120">Applying **ReadOnly** can lead to unexpected results because some operations that seem like read operations actually require additional actions.</span></span> <span data-ttu-id="acae8-121">Por exemplo, aplicar um bloqueio **ReadOnly** em uma conta de armazenamento impedirá que todos os usuários listem as chaves.</span><span class="sxs-lookup"><span data-stu-id="acae8-121">For example, placing a **ReadOnly** lock on a storage account prevents all users from listing the keys.</span></span> <span data-ttu-id="acae8-122">A operação de lista de chaves é tratada por meio de uma solicitação POST, pois as chaves retornadas estão disponíveis para operações de gravação.</span><span class="sxs-lookup"><span data-stu-id="acae8-122">The list keys operation is handled through a POST request because the returned keys are available for write operations.</span></span> <span data-ttu-id="acae8-123">Em outro exemplo, a aplicação de um bloqueio **ReadOnly** em um recurso do Serviço de Aplicativo impedirá o Visual Studio Server Explorer de exibir os arquivos para o recurso, pois essa interação exige acesso de gravação.</span><span class="sxs-lookup"><span data-stu-id="acae8-123">For another example, placing a **ReadOnly** lock on an App Service resource prevents Visual Studio Server Explorer from displaying files for the resource because that interaction requires write access.</span></span>

## <a name="who-can-create-or-delete-locks-in-your-organization"></a><span data-ttu-id="acae8-124">Quem pode criar ou excluir bloqueios na sua organização</span><span class="sxs-lookup"><span data-stu-id="acae8-124">Who can create or delete locks in your organization</span></span>
<span data-ttu-id="acae8-125">Para criar ou excluir bloqueios de gerenciamento, você deve ter acesso às ações `Microsoft.Authorization/*` ou `Microsoft.Authorization/locks/*`.</span><span class="sxs-lookup"><span data-stu-id="acae8-125">To create or delete management locks, you must have access to `Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="acae8-126">Das funções internas, somente **Proprietário** e **Administrador do Acesso de Usuário** recebem essas ações.</span><span class="sxs-lookup"><span data-stu-id="acae8-126">Of the built-in roles, only **Owner** and **User Access Administrator** are granted those actions.</span></span>

## <a name="portal"></a><span data-ttu-id="acae8-127">Portal</span><span class="sxs-lookup"><span data-stu-id="acae8-127">Portal</span></span>
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a><span data-ttu-id="acae8-128">Modelo</span><span class="sxs-lookup"><span data-stu-id="acae8-128">Template</span></span>
<span data-ttu-id="acae8-129">O exemplo a seguir mostra um modelo que cria um bloqueio em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="acae8-129">The following example shows a template that creates a lock on a storage account.</span></span> <span data-ttu-id="acae8-130">A conta de armazenamento em que o bloqueio será aplicado é fornecida como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="acae8-130">The storage account on which to apply the lock is provided as a parameter.</span></span> <span data-ttu-id="acae8-131">O nome do bloqueio é criado por meio da concatenação do nome do recurso com **/Microsoft.Authorization/** e do nome do bloqueio, que nesse caso é **myLock**.</span><span class="sxs-lookup"><span data-stu-id="acae8-131">The name of the lock is created by concatenating the resource name with **/Microsoft.Authorization/** and the name of the lock, in this case **myLock**.</span></span>

<span data-ttu-id="acae8-132">O tipo fornecido é específico para o tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="acae8-132">The type provided is specific to the resource type.</span></span> <span data-ttu-id="acae8-133">Para armazenamento, defina o tipo como "Microsoft.Storage/storageaccounts/providers/locks".</span><span class="sxs-lookup"><span data-stu-id="acae8-133">For storage, set the type to "Microsoft.Storage/storageaccounts/providers/locks".</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "lockedResource": {
          "type": "string"
        }
      },
      "resources": [
        {
          "name": "[concat(parameters('lockedResource'), '/Microsoft.Authorization/myLock')]",
          "type": "Microsoft.Storage/storageAccounts/providers/locks",
          "apiVersion": "2015-01-01",
          "properties": {
            "level": "CannotDelete"
          }
        }
      ]
    }

## <a name="powershell"></a><span data-ttu-id="acae8-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="acae8-134">PowerShell</span></span>
<span data-ttu-id="acae8-135">Você bloqueia recursos implantados com o Azure PowerShell usando o comando [New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock).</span><span class="sxs-lookup"><span data-stu-id="acae8-135">You lock deployed resources with Azure PowerShell by using the [New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) command.</span></span>

<span data-ttu-id="acae8-136">Para bloquear um recurso, forneça o nome dele, seu tipo de recurso e o nome do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="acae8-136">To lock a resource, provide the name of the resource, its resource type, and its resource group name.</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="acae8-137">Para bloquear um grupo de recursos, forneça o nome dele.</span><span class="sxs-lookup"><span data-stu-id="acae8-137">To lock a resource group, provide the name of the resource group.</span></span>

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="acae8-138">Para saber mais sobre um bloqueio, use [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span><span class="sxs-lookup"><span data-stu-id="acae8-138">To get information about a lock, use [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span></span> <span data-ttu-id="acae8-139">Para obter todos os bloqueios em sua assinatura, use:</span><span class="sxs-lookup"><span data-stu-id="acae8-139">To get all the locks in your subscription, use:</span></span>

```powershell
Get-AzureRmResourceLock
```

<span data-ttu-id="acae8-140">Para obter todos os bloqueios de um recurso, use:</span><span class="sxs-lookup"><span data-stu-id="acae8-140">To get all locks for a resource, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="acae8-141">Para obter todos os bloqueios de um grupo de recursos, use:</span><span class="sxs-lookup"><span data-stu-id="acae8-141">To get all locks for a resource group, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="acae8-142">O Azure PowerShell fornece outros comandos para trabalhar com bloqueios, tais como [Set-AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) para atualizar um bloqueio e [Remove-AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) para excluir um bloqueio.</span><span class="sxs-lookup"><span data-stu-id="acae8-142">Azure PowerShell provides other commands for working locks, such as [Set-AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) to update a lock, and [Remove-AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) to delete a lock.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="acae8-143">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="acae8-143">Azure CLI</span></span>

<span data-ttu-id="acae8-144">Bloqueie recursos implantados com a CLI do Azure usando o comando [az lock create](/cli/azure/lock#create).</span><span class="sxs-lookup"><span data-stu-id="acae8-144">You lock deployed resources with Azure CLI by using the [az lock create](/cli/azure/lock#create) command.</span></span>

<span data-ttu-id="acae8-145">Para bloquear um recurso, forneça o nome dele, seu tipo de recurso e o nome do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="acae8-145">To lock a resource, provide the name of the resource, its resource type, and its resource group name.</span></span>

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

<span data-ttu-id="acae8-146">Para bloquear um grupo de recursos, forneça o nome dele.</span><span class="sxs-lookup"><span data-stu-id="acae8-146">To lock a resource group, provide the name of the resource group.</span></span>

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

<span data-ttu-id="acae8-147">Para saber mais sobre um bloqueio, use [az lock list](/cli/azure/lock#list).</span><span class="sxs-lookup"><span data-stu-id="acae8-147">To get information about a lock, use [az lock list](/cli/azure/lock#list).</span></span> <span data-ttu-id="acae8-148">Para obter todos os bloqueios em sua assinatura, use:</span><span class="sxs-lookup"><span data-stu-id="acae8-148">To get all the locks in your subscription, use:</span></span>

```azurecli
az lock list
```

<span data-ttu-id="acae8-149">Para obter todos os bloqueios de um recurso, use:</span><span class="sxs-lookup"><span data-stu-id="acae8-149">To get all locks for a resource, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

<span data-ttu-id="acae8-150">Para obter todos os bloqueios de um grupo de recursos, use:</span><span class="sxs-lookup"><span data-stu-id="acae8-150">To get all locks for a resource group, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup
```

<span data-ttu-id="acae8-151">A CLI do Azure oferece outros comandos para bloqueios de trabalho, como [az lock update](/cli/azure/lock#update) para atualizar um bloqueio e [az lock delete](/cli/azure/lock#delete) para excluir um bloqueio.</span><span class="sxs-lookup"><span data-stu-id="acae8-151">Azure CLI provides other commands for working locks, such as [az lock update](/cli/azure/lock#update) to update a lock, and [az lock delete](/cli/azure/lock#delete) to delete a lock.</span></span>

## <a name="rest-api"></a><span data-ttu-id="acae8-152">API REST</span><span class="sxs-lookup"><span data-stu-id="acae8-152">REST API</span></span>
<span data-ttu-id="acae8-153">Você pode bloquear os recursos implantados com a [API REST para bloqueios de gerenciamento](https://docs.microsoft.com/rest/api/resources/managementlocks).</span><span class="sxs-lookup"><span data-stu-id="acae8-153">You can lock deployed resources with the [REST API for management locks](https://docs.microsoft.com/rest/api/resources/managementlocks).</span></span> <span data-ttu-id="acae8-154">A API REST permite que você crie e exclua bloqueios e recupere informações sobre bloqueios existentes.</span><span class="sxs-lookup"><span data-stu-id="acae8-154">The REST API enables you to create and delete locks, and retrieve information about existing locks.</span></span>

<span data-ttu-id="acae8-155">Para criar um bloqueio, execute:</span><span class="sxs-lookup"><span data-stu-id="acae8-155">To create a lock, run:</span></span>

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

<span data-ttu-id="acae8-156">O escopo pode ser uma assinatura, grupo de recursos ou recurso.</span><span class="sxs-lookup"><span data-stu-id="acae8-156">The scope could be a subscription, resource group, or resource.</span></span> <span data-ttu-id="acae8-157">O nome do bloqueio é como você deseja chamar o bloqueio.</span><span class="sxs-lookup"><span data-stu-id="acae8-157">The lock-name is whatever you want to call the lock.</span></span> <span data-ttu-id="acae8-158">Para a api-version, use **2015-01-01**.</span><span class="sxs-lookup"><span data-stu-id="acae8-158">For api-version, use **2015-01-01**.</span></span>

<span data-ttu-id="acae8-159">Na solicitação, inclua um objeto JSON que especifica as propriedades do bloqueio.</span><span class="sxs-lookup"><span data-stu-id="acae8-159">In the request, include a JSON object that specifies the properties for the lock.</span></span>

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a><span data-ttu-id="acae8-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="acae8-160">Next steps</span></span>
* <span data-ttu-id="acae8-161">Para saber mais sobre como trabalhar com bloqueios de recursos, confira [Bloquear os recursos do Azure](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span><span class="sxs-lookup"><span data-stu-id="acae8-161">For more information about working with resource locks, see [Lock Down Your Azure Resources](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span></span>
* <span data-ttu-id="acae8-162">Para saber mais sobre a organização lógica de recursos, confira [Usando marcas para organizar os recursos](resource-group-using-tags.md)</span><span class="sxs-lookup"><span data-stu-id="acae8-162">To learn about logically organizing your resources, see [Using tags to organize your resources](resource-group-using-tags.md)</span></span>
* <span data-ttu-id="acae8-163">Para alterar o grupo de recursos em que um recurso reside, confira [Mover recursos para um novo grupo de recursos](resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="acae8-163">To change which resource group a resource resides in, see [Move resources to new resource group](resource-group-move-resources.md)</span></span>
* <span data-ttu-id="acae8-164">É possível aplicar restrições e convenções em sua assinatura com políticas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="acae8-164">You can apply restrictions and conventions across your subscription with customized policies.</span></span> <span data-ttu-id="acae8-165">Para saber mais, confira [Usar a Política para gerenciar recursos e controlar o acesso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="acae8-165">For more information, see [Use Policy to manage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="acae8-166">Para obter orientação sobre como as empresas podem usar o Resource Manager para gerenciar assinaturas de forma eficaz, consulte [Azure enterprise scaffold – controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="acae8-166">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

