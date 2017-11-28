---
title: "alterações de tooprevent de recursos do Azure aaaLock | Microsoft Docs"
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
ms.openlocfilehash: 1f0d8911b2b129069bd2f01a9a4ec0a3cf700118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="lock-resources-tooprevent-unexpected-changes"></a><span data-ttu-id="3d7d9-103">Bloquear recursos tooprevent alterações inesperadas</span><span class="sxs-lookup"><span data-stu-id="3d7d9-103">Lock resources tooprevent unexpected changes</span></span> 
<span data-ttu-id="3d7d9-104">Como administrador, talvez seja necessário toolock uma assinatura, o grupo de recursos ou o recurso tooprevent outros usuários em sua organização acidentalmente excluir ou modificar recursos críticos.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-104">As an administrator, you may need toolock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="3d7d9-105">Você pode definir o nível de bloqueio de saudação muito**CanNotDelete** ou **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-105">You can set hello lock level too**CanNotDelete** or **ReadOnly**.</span></span> 

* <span data-ttu-id="3d7d9-106">**CanNotDelete** significa que os usuários autorizados podem ler e modificar um recurso, mas eles não é possível excluir o recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-106">**CanNotDelete** means authorized users can still read and modify a resource, but they can't delete hello resource.</span></span> 
* <span data-ttu-id="3d7d9-107">**ReadOnly** significa que usuários autorizados possam ler um recurso, mas eles não podem excluir ou atualizar o recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-107">**ReadOnly** means authorized users can read a resource, but they can't delete or update hello resource.</span></span> <span data-ttu-id="3d7d9-108">Aplicar o bloqueio é semelhante toorestricting todos os autorizados toohello usuários as permissões concedidas pelo Olá **leitor** função.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-108">Applying this lock is similar toorestricting all authorized users toohello permissions granted by hello **Reader** role.</span></span> 

## <a name="how-locks-are-applied"></a><span data-ttu-id="3d7d9-109">Como os bloqueios são aplicados</span><span class="sxs-lookup"><span data-stu-id="3d7d9-109">How locks are applied</span></span>

<span data-ttu-id="3d7d9-110">Quando você aplica um bloqueio em um escopo pai, todos os recursos nesse escopo herdam Olá mesmo bloqueio.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-110">When you apply a lock at a parent scope, all resources within that scope inherit hello same lock.</span></span> <span data-ttu-id="3d7d9-111">Recursos até que você adicionar posteriormente herdam bloqueio de saudação do pai de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-111">Even resources you add later inherit hello lock from hello parent.</span></span> <span data-ttu-id="3d7d9-112">bloqueio de Hello mais restritivo em herança Olá terá precedência.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-112">hello most restrictive lock in hello inheritance takes precedence.</span></span>

<span data-ttu-id="3d7d9-113">Ao contrário de controle de acesso baseado em função, você pode usar bloqueios de gerenciamento tooapply uma restrição em todos os usuários e funções.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-113">Unlike role-based access control, you use management locks tooapply a restriction across all users and roles.</span></span> <span data-ttu-id="3d7d9-114">toolearn sobre como configurar permissões para usuários e funções, consulte [controle de acesso baseado em função do Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="3d7d9-114">toolearn about setting permissions for users and roles, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>

<span data-ttu-id="3d7d9-115">Bloqueios de Gerenciador de recursos se aplicam somente toooperations que acontecem no plano de gerenciamento hello, que consiste em operações enviadas muito`https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-115">Resource Manager locks apply only toooperations that happen in hello management plane, which consists of operations sent too`https://management.azure.com`.</span></span> <span data-ttu-id="3d7d9-116">bloqueios de saudação não restringem como recursos de executam suas próprias funções.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-116">hello locks do not restrict how resources perform their own functions.</span></span> <span data-ttu-id="3d7d9-117">Alterações de recursos são restritas, mas as operações de recursos não são restritas.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-117">Resource changes are restricted, but resource operations are not restricted.</span></span> <span data-ttu-id="3d7d9-118">Por exemplo, um bloqueio de somente leitura em um banco de dados SQL impede a exclusão ou modificação de banco de dados hello, mas ele não impedem que você criar, atualizar ou excluir dados no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-118">For example, a ReadOnly lock on a SQL Database prevents you from deleting or modifying hello database, but it does not prevent you from creating, updating, or deleting data in hello database.</span></span> <span data-ttu-id="3d7d9-119">Transações de dados são permitidas porque essas operações não são enviadas muito`https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-119">Data transactions are permitted because those operations are not sent too`https://management.azure.com`.</span></span>

<span data-ttu-id="3d7d9-120">Aplicando **ReadOnly** pode levar a resultados de toounexpected porque algumas operações que parecerem leitura operações realmente exigem ações adicionais.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-120">Applying **ReadOnly** can lead toounexpected results because some operations that seem like read operations actually require additional actions.</span></span> <span data-ttu-id="3d7d9-121">Por exemplo, colocando uma **ReadOnly** bloqueio em uma conta de armazenamento impede que todos os usuários listando chaves hello.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-121">For example, placing a **ReadOnly** lock on a storage account prevents all users from listing hello keys.</span></span> <span data-ttu-id="3d7d9-122">lista de saudação operação de chaves é tratada por meio de uma solicitação POST como Olá retornado chaves estão disponíveis para operações de gravação.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-122">hello list keys operation is handled through a POST request because hello returned keys are available for write operations.</span></span> <span data-ttu-id="3d7d9-123">Outro exemplo, colocando uma **ReadOnly** bloqueio em um recurso de serviço de aplicativo impede que o Visual Studio Server Explorer exibindo arquivos de recurso Olá porque essa interação requer acesso de gravação.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-123">For another example, placing a **ReadOnly** lock on an App Service resource prevents Visual Studio Server Explorer from displaying files for hello resource because that interaction requires write access.</span></span>

## <a name="who-can-create-or-delete-locks-in-your-organization"></a><span data-ttu-id="3d7d9-124">Quem pode criar ou excluir bloqueios na sua organização</span><span class="sxs-lookup"><span data-stu-id="3d7d9-124">Who can create or delete locks in your organization</span></span>
<span data-ttu-id="3d7d9-125">bloqueios de gerenciamento toocreate ou delete, você deve ter acesso muito`Microsoft.Authorization/*` ou `Microsoft.Authorization/locks/*` ações.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-125">toocreate or delete management locks, you must have access too`Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="3d7d9-126">De saudação funções internas, apenas **proprietário** e **administrador de acesso do usuário** recebem essas ações.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-126">Of hello built-in roles, only **Owner** and **User Access Administrator** are granted those actions.</span></span>

## <a name="portal"></a><span data-ttu-id="3d7d9-127">Portal</span><span class="sxs-lookup"><span data-stu-id="3d7d9-127">Portal</span></span>
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a><span data-ttu-id="3d7d9-128">Modelo</span><span class="sxs-lookup"><span data-stu-id="3d7d9-128">Template</span></span>
<span data-ttu-id="3d7d9-129">Olá, exemplo a seguir mostra um modelo que cria um bloqueio em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-129">hello following example shows a template that creates a lock on a storage account.</span></span> <span data-ttu-id="3d7d9-130">conta de armazenamento Olá no qual tooapply bloqueio Olá é fornecido como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-130">hello storage account on which tooapply hello lock is provided as a parameter.</span></span> <span data-ttu-id="3d7d9-131">Olá nome do bloqueio de saudação é criado pela concatenação do nome do recurso Olá com **/Microsoft.Authorization/** e Olá nesse caso o nome do bloqueio de saudação **myLock**.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-131">hello name of hello lock is created by concatenating hello resource name with **/Microsoft.Authorization/** and hello name of hello lock, in this case **myLock**.</span></span>

<span data-ttu-id="3d7d9-132">tipo Hello fornecido é o tipo de recurso de toohello específico.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-132">hello type provided is specific toohello resource type.</span></span> <span data-ttu-id="3d7d9-133">Para o armazenamento, defina Olá tipo too"Microsoft.Storage/storageaccounts/providers/locks".</span><span class="sxs-lookup"><span data-stu-id="3d7d9-133">For storage, set hello type too"Microsoft.Storage/storageaccounts/providers/locks".</span></span>

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

## <a name="powershell"></a><span data-ttu-id="3d7d9-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3d7d9-134">PowerShell</span></span>
<span data-ttu-id="3d7d9-135">Bloquear implantado recursos com o Azure PowerShell usando Olá [AzureRmResourceLock novo](/powershell/module/azurerm.resources/new-azurermresourcelock) comando.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-135">You lock deployed resources with Azure PowerShell by using hello [New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) command.</span></span>

<span data-ttu-id="3d7d9-136">toolock um recurso, forneça o nome de saudação do recurso de saudação, seu tipo de recurso e o nome do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-136">toolock a resource, provide hello name of hello resource, its resource type, and its resource group name.</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="3d7d9-137">toolock um grupo de recursos, forneça o nome de Olá Olá do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-137">toolock a resource group, provide hello name of hello resource group.</span></span>

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="3d7d9-138">tooget informações sobre um bloqueio, use [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span><span class="sxs-lookup"><span data-stu-id="3d7d9-138">tooget information about a lock, use [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span></span> <span data-ttu-id="3d7d9-139">tooget todos os bloqueios de saudação em sua assinatura, use:</span><span class="sxs-lookup"><span data-stu-id="3d7d9-139">tooget all hello locks in your subscription, use:</span></span>

```powershell
Get-AzureRmResourceLock
```

<span data-ttu-id="3d7d9-140">tooget todos os bloqueios de um recurso, use:</span><span class="sxs-lookup"><span data-stu-id="3d7d9-140">tooget all locks for a resource, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="3d7d9-141">tooget todos os bloqueios para um grupo de recursos, use:</span><span class="sxs-lookup"><span data-stu-id="3d7d9-141">tooget all locks for a resource group, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="3d7d9-142">PowerShell do Azure oferece outros comandos para bloqueios de trabalho, tais como [conjunto AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate um bloqueio e [AzureRmResourceLock remover](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete um bloqueio.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-142">Azure PowerShell provides other commands for working locks, such as [Set-AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate a lock, and [Remove-AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete a lock.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="3d7d9-143">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="3d7d9-143">Azure CLI</span></span>

<span data-ttu-id="3d7d9-144">Bloquear implantado recursos com CLI do Azure usando Olá [bloqueio az criar](/cli/azure/lock#create) comando.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-144">You lock deployed resources with Azure CLI by using hello [az lock create](/cli/azure/lock#create) command.</span></span>

<span data-ttu-id="3d7d9-145">toolock um recurso, forneça o nome de saudação do recurso de saudação, seu tipo de recurso e o nome do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-145">toolock a resource, provide hello name of hello resource, its resource type, and its resource group name.</span></span>

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

<span data-ttu-id="3d7d9-146">toolock um grupo de recursos, forneça o nome de Olá Olá do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-146">toolock a resource group, provide hello name of hello resource group.</span></span>

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

<span data-ttu-id="3d7d9-147">tooget informações sobre um bloqueio, use [lista de bloqueio az](/cli/azure/lock#list).</span><span class="sxs-lookup"><span data-stu-id="3d7d9-147">tooget information about a lock, use [az lock list](/cli/azure/lock#list).</span></span> <span data-ttu-id="3d7d9-148">tooget todos os bloqueios de saudação em sua assinatura, use:</span><span class="sxs-lookup"><span data-stu-id="3d7d9-148">tooget all hello locks in your subscription, use:</span></span>

```azurecli
az lock list
```

<span data-ttu-id="3d7d9-149">tooget todos os bloqueios de um recurso, use:</span><span class="sxs-lookup"><span data-stu-id="3d7d9-149">tooget all locks for a resource, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

<span data-ttu-id="3d7d9-150">tooget todos os bloqueios para um grupo de recursos, use:</span><span class="sxs-lookup"><span data-stu-id="3d7d9-150">tooget all locks for a resource group, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup
```

<span data-ttu-id="3d7d9-151">CLI do Azure oferece outros comandos para bloqueios de trabalho, tais como [atualização de bloqueio az](/cli/azure/lock#update) tooupdate um bloqueio e [bloqueio az excluir](/cli/azure/lock#delete) toodelete um bloqueio.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-151">Azure CLI provides other commands for working locks, such as [az lock update](/cli/azure/lock#update) tooupdate a lock, and [az lock delete](/cli/azure/lock#delete) toodelete a lock.</span></span>

## <a name="rest-api"></a><span data-ttu-id="3d7d9-152">API REST</span><span class="sxs-lookup"><span data-stu-id="3d7d9-152">REST API</span></span>
<span data-ttu-id="3d7d9-153">Você pode bloquear recursos implantados com hello [API REST para bloqueios de gerenciamento](https://docs.microsoft.com/rest/api/resources/managementlocks).</span><span class="sxs-lookup"><span data-stu-id="3d7d9-153">You can lock deployed resources with hello [REST API for management locks](https://docs.microsoft.com/rest/api/resources/managementlocks).</span></span> <span data-ttu-id="3d7d9-154">Olá REST API permite toocreate e excluir bloqueios e recuperar informações sobre bloqueios existentes.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-154">hello REST API enables you toocreate and delete locks, and retrieve information about existing locks.</span></span>

<span data-ttu-id="3d7d9-155">toocreate um bloqueio, execute:</span><span class="sxs-lookup"><span data-stu-id="3d7d9-155">toocreate a lock, run:</span></span>

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

<span data-ttu-id="3d7d9-156">escopo de saudação pode ser uma assinatura, o grupo de recursos ou o recurso.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-156">hello scope could be a subscription, resource group, or resource.</span></span> <span data-ttu-id="3d7d9-157">Olá nome do bloqueio é tudo o que você quiser toocall bloqueio de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-157">hello lock-name is whatever you want toocall hello lock.</span></span> <span data-ttu-id="3d7d9-158">Para a api-version, use **2015-01-01**.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-158">For api-version, use **2015-01-01**.</span></span>

<span data-ttu-id="3d7d9-159">Na solicitação de hello, inclua um objeto JSON que especifica propriedades Olá para bloqueio de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-159">In hello request, include a JSON object that specifies hello properties for hello lock.</span></span>

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a><span data-ttu-id="3d7d9-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3d7d9-160">Next steps</span></span>
* <span data-ttu-id="3d7d9-161">Para saber mais sobre como trabalhar com bloqueios de recursos, confira [Bloquear os recursos do Azure](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span><span class="sxs-lookup"><span data-stu-id="3d7d9-161">For more information about working with resource locks, see [Lock Down Your Azure Resources](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span></span>
* <span data-ttu-id="3d7d9-162">toolearn sobre logicamente organizar seus recursos, consulte [usando marcas tooorganize seus recursos](resource-group-using-tags.md)</span><span class="sxs-lookup"><span data-stu-id="3d7d9-162">toolearn about logically organizing your resources, see [Using tags tooorganize your resources](resource-group-using-tags.md)</span></span>
* <span data-ttu-id="3d7d9-163">toochange reside de um recurso com a qual grupo de recursos, consulte [Mover grupo de recursos de toonew de recursos](resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="3d7d9-163">toochange which resource group a resource resides in, see [Move resources toonew resource group](resource-group-move-resources.md)</span></span>
* <span data-ttu-id="3d7d9-164">É possível aplicar restrições e convenções em sua assinatura com políticas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="3d7d9-164">You can apply restrictions and conventions across your subscription with customized policies.</span></span> <span data-ttu-id="3d7d9-165">Para obter mais informações, consulte [recursos de toomanage de política de uso e controlar o acesso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="3d7d9-165">For more information, see [Use Policy toomanage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="3d7d9-166">Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="3d7d9-166">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

