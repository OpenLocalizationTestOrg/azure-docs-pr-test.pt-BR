---
title: "Gerenciar as soluções do Azure com o PowerShell | Microsoft Docs"
description: Use o Azure PowerShell e o Resource Manager para gerenciar seus recursos.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: b33b7303-3330-4af8-8329-c80ac7e9bc7f
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: ff42e5cb29005c5f4b97babdae58bef9382071f0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-resources-with-azure-powershell-and-resource-manager"></a><span data-ttu-id="cc17a-103">Gerenciar recursos com o Azure PowerShell e o Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cc17a-103">Manage resources with Azure PowerShell and Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cc17a-104">Portal</span><span class="sxs-lookup"><span data-stu-id="cc17a-104">Portal</span></span>](resource-group-portal.md)
> * [<span data-ttu-id="cc17a-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="cc17a-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="cc17a-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc17a-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="cc17a-107">API REST</span><span class="sxs-lookup"><span data-stu-id="cc17a-107">REST API</span></span>](resource-manager-rest-api.md)
>
>

<span data-ttu-id="cc17a-108">Neste artigo, você aprenderá a gerenciar suas soluções com o Azure PowerShell e o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cc17a-108">In this article, you learn how to manage your solutions with Azure PowerShell and Azure Resource Manager.</span></span> <span data-ttu-id="cc17a-109">Se você não estiver familiarizado com o Resource Manager, veja [Visão geral do Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cc17a-109">If you are not familiar with Resource Manager, see [Resource Manager Overview](resource-group-overview.md).</span></span> <span data-ttu-id="cc17a-110">Este tópico se concentra nas tarefas de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="cc17a-110">This topic focuses on management tasks.</span></span> <span data-ttu-id="cc17a-111">Você irá:</span><span class="sxs-lookup"><span data-stu-id="cc17a-111">You will:</span></span>

1. <span data-ttu-id="cc17a-112">Criar um grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="cc17a-112">Create a resource group</span></span>
2. <span data-ttu-id="cc17a-113">Adicionar um recurso ao grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="cc17a-113">Add a resource to the resource group</span></span>
3. <span data-ttu-id="cc17a-114">Adicionar uma marca ao recurso</span><span class="sxs-lookup"><span data-stu-id="cc17a-114">Add a tag to the resource</span></span>
4. <span data-ttu-id="cc17a-115">Recursos de consulta baseados em nomes ou em valores de marca</span><span class="sxs-lookup"><span data-stu-id="cc17a-115">Query resources based on names or tag values</span></span>
5. <span data-ttu-id="cc17a-116">Aplicar e remover um bloqueio no recurso</span><span class="sxs-lookup"><span data-stu-id="cc17a-116">Apply and remove a lock on the resource</span></span>
6. <span data-ttu-id="cc17a-117">Excluir um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="cc17a-117">Delete a resource group</span></span>

<span data-ttu-id="cc17a-118">Este artigo mostra como implantar um modelo do Resource Manager à sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="cc17a-118">This article does not show how to deploy a Resource Manager template to your subscription.</span></span> <span data-ttu-id="cc17a-119">Para obter essas informações, veja [Implantar recursos com modelos do Resource Manager e o Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="cc17a-119">For that information, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>

## <a name="get-started-with-azure-powershell"></a><span data-ttu-id="cc17a-120">Introdução ao Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc17a-120">Get started with Azure PowerShell</span></span>

<span data-ttu-id="cc17a-121">Se você não tiver o Azure PowerShell instalado, veja [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cc17a-121">If you have not installed Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="cc17a-122">Se você tiver instalado o Azure PowerShell no passado, mas não o tiver atualizado recentemente, considere a possibilidade de instalar a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="cc17a-122">If you have installed Azure PowerShell in the past but have not updated it recently, consider installing the latest version.</span></span> <span data-ttu-id="cc17a-123">Você pode atualizar a versão por meio do mesmo método usado para instalá-lo.</span><span class="sxs-lookup"><span data-stu-id="cc17a-123">You can update the version through the same method you used to install it.</span></span> <span data-ttu-id="cc17a-124">Por exemplo, se você tiver usado o Web Platform Installer, inicie-o novamente e procure uma atualização.</span><span class="sxs-lookup"><span data-stu-id="cc17a-124">For example, if you used the Web Platform Installer, launch it again and look for an update.</span></span>

<span data-ttu-id="cc17a-125">Para verificar a versão do módulo de Recursos do Azure, use o seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="cc17a-125">To check your version of the Azure Resources module, use the following cmdlet:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="cc17a-126">Este tópico foi atualizado para a versão 3.3.0.</span><span class="sxs-lookup"><span data-stu-id="cc17a-126">This topic was updated for version 3.3.0.</span></span> <span data-ttu-id="cc17a-127">Se você tiver uma versão anterior, sua experiência pode não corresponder às etapas mostradas neste tópico.</span><span class="sxs-lookup"><span data-stu-id="cc17a-127">If you have an earlier version, your experience might not match the steps shown in this topic.</span></span> <span data-ttu-id="cc17a-128">Para obter a documentação sobre os cmdlets nesta versão, veja [AzureRM.Resources módulo](/powershell/module/azurerm.resources).</span><span class="sxs-lookup"><span data-stu-id="cc17a-128">For documentation about the cmdlets in this version, see [AzureRM.Resources Module](/powershell/module/azurerm.resources).</span></span>

## <a name="log-in-to-your-azure-account"></a><span data-ttu-id="cc17a-129">Fazer logon na sua conta do Azure</span><span class="sxs-lookup"><span data-stu-id="cc17a-129">Log in to your Azure account</span></span>
<span data-ttu-id="cc17a-130">Antes de trabalhar em sua solução, você deve fazer logon em sua conta.</span><span class="sxs-lookup"><span data-stu-id="cc17a-130">Before working on your solution, you must log in to your account.</span></span>

<span data-ttu-id="cc17a-131">Para fazer logon em sua conta do Azure, use o cmdlet **Login-AzureRmAccount**.</span><span class="sxs-lookup"><span data-stu-id="cc17a-131">To log in to your Azure account, use the **Login-AzureRmAccount** cmdlet.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="cc17a-132">O cmdlet solicita as credenciais de logon para sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc17a-132">The cmdlet prompts you for the login credentials for your Azure account.</span></span> <span data-ttu-id="cc17a-133">Depois de entrar, ele baixa as configurações da conta para que elas estejam disponíveis para o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cc17a-133">After logging in, it downloads your account settings so they are available to Azure PowerShell.</span></span>

<span data-ttu-id="cc17a-134">O cmdlet retorna informações sobre sua conta e a assinatura a ser usada para as tarefas.</span><span class="sxs-lookup"><span data-stu-id="cc17a-134">The cmdlet returns information about your account and the subscription to use for the tasks.</span></span>

```powershell
Environment           : AzureCloud
Account               : example@contoso.com
TenantId              : {guid}
SubscriptionId        : {guid}
SubscriptionName      : Example Subscription One
CurrentStorageAccount :

```

<span data-ttu-id="cc17a-135">Se você tiver mais de uma assinatura, você pode alternar para uma assinatura diferente.</span><span class="sxs-lookup"><span data-stu-id="cc17a-135">If you have more than one subscription, you can switch to a different subscription.</span></span> <span data-ttu-id="cc17a-136">Primeiro, vamos ver todas as assinaturas para sua conta.</span><span class="sxs-lookup"><span data-stu-id="cc17a-136">First, let's see all the subscriptions for your account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="cc17a-137">Retorna habilitados e desabilitados de assinaturas.</span><span class="sxs-lookup"><span data-stu-id="cc17a-137">It returns enabled and disabled subscriptions.</span></span>

```powershell
SubscriptionName : Example Subscription One
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Two
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Three
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Disabled
```

<span data-ttu-id="cc17a-138">Para alternar para uma assinatura diferente, forneça o nome da assinatura com o **AzureRmContext conjunto** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cc17a-138">To switch to a different subscription, provide the subscription name with the **Set-AzureRmContext** cmdlet.</span></span>

```powershell
Set-AzureRmContext -SubscriptionName "Example Subscription Two"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="cc17a-139">Criar um grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="cc17a-139">Create a resource group</span></span>
<span data-ttu-id="cc17a-140">Antes de implantar os recursos em sua assinatura, você deve criar um grupo de recursos que conterá os recursos.</span><span class="sxs-lookup"><span data-stu-id="cc17a-140">Before deploying any resources to your subscription, you must create a resource group that will contain the resources.</span></span>

<span data-ttu-id="cc17a-141">Para criar um grupo de recursos, use o cmdlet **New-AzureRmResourceGroup** .</span><span class="sxs-lookup"><span data-stu-id="cc17a-141">To create a resource group, use the **New-AzureRmResourceGroup** cmdlet.</span></span> <span data-ttu-id="cc17a-142">O comando usa o parâmetro **Name** para especificar um nome para o grupo de recursos e o parâmetro **Location** para especificar o local.</span><span class="sxs-lookup"><span data-stu-id="cc17a-142">The command uses the **Name** parameter to specify a name for the resource group and the **Location** parameter to specify its location.</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location "South Central US"
```

<span data-ttu-id="cc17a-143">A saída está neste formato:</span><span class="sxs-lookup"><span data-stu-id="cc17a-143">The output is in the following format:</span></span>

```powershell
ResourceGroupName : TestRG1
Location          : southcentralus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/{guid}/resourceGroups/TestRG1
```

<span data-ttu-id="cc17a-144">Se você precisar recuperar o grupo de recursos posteriormente, use o seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="cc17a-144">If you need to retrieve the resource group later, use the following cmdlet:</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName TestRG1
```

<span data-ttu-id="cc17a-145">Para obter todos os grupos de recursos em sua assinatura, não especifique um nome:</span><span class="sxs-lookup"><span data-stu-id="cc17a-145">To get all the resource groups in your subscription, do not specify a name:</span></span>

```powershell
Get-AzureRmResourceGroup
```

## <a name="add-resources-to-a-resource-group"></a><span data-ttu-id="cc17a-146">Adicionar recursos a um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="cc17a-146">Add resources to a resource group</span></span>
<span data-ttu-id="cc17a-147">Para adicionar um recurso ao grupo de recursos, você pode usar o **novo AzureRmResource** cmdlet ou um cmdlet que é específico para o tipo de recurso que você está criando (como **novo AzureRmStorageAccount**).</span><span class="sxs-lookup"><span data-stu-id="cc17a-147">To add a resource to the resource group, you can use the **New-AzureRmResource** cmdlet or a cmdlet that is specific to the type of resource you are creating (like **New-AzureRmStorageAccount**).</span></span> <span data-ttu-id="cc17a-148">Talvez seja mais fácil de usar um cmdlet que é específico para um tipo de recurso porque ele inclui parâmetros para as propriedades que são necessárias para o novo recurso.</span><span class="sxs-lookup"><span data-stu-id="cc17a-148">You might find it easier to use a cmdlet that is specific to a resource type because it includes parameters for the properties that are needed for the new resource.</span></span> <span data-ttu-id="cc17a-149">Usar **AzureRmResource novo**, você deve conhecer todas as propriedades para definir sem ser solicitado para eles.</span><span class="sxs-lookup"><span data-stu-id="cc17a-149">To use **New-AzureRmResource**, you must know all the properties to set without being prompted for them.</span></span>

<span data-ttu-id="cc17a-150">No entanto, a adição de um recurso por meio de cmdlets pode causar uma confusão futura, pois o novo recurso não existe em um modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cc17a-150">However, adding a resource through cmdlets might cause future confusion because the new resource does not exist in a Resource Manager template.</span></span> <span data-ttu-id="cc17a-151">A Microsoft recomenda definir a infraestrutura para sua solução do Azure em um modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cc17a-151">Microsoft recommends defining the infrastructure for your Azure solution in a Resource Manager template.</span></span> <span data-ttu-id="cc17a-152">Modelos permitem repetidamente e confiável implantar sua solução.</span><span class="sxs-lookup"><span data-stu-id="cc17a-152">Templates enable you to reliably and repeatedly deploy your solution.</span></span> <span data-ttu-id="cc17a-153">Para este tópico, você cria uma conta de armazenamento com um cmdlet do PowerShell, mas posteriormente você gerar um modelo de seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="cc17a-153">For this topic, you create a storage account with a PowerShell cmdlet, but later you generate a template from your resource group.</span></span>

<span data-ttu-id="cc17a-154">O cmdlet a seguir cria uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cc17a-154">The following cmdlet creates a storage account.</span></span> <span data-ttu-id="cc17a-155">Em vez de usar o nome mostrado no exemplo, forneça um nome exclusivo para a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cc17a-155">Instead of using the name shown in the example, provide a unique name for the storage account.</span></span> <span data-ttu-id="cc17a-156">O nome deve ter entre 3 e 24 caracteres de comprimento e usar somente números e letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="cc17a-156">The name must be between 3 and 24 characters in length, and use only numbers and lower-case letters.</span></span> <span data-ttu-id="cc17a-157">Se você usar o nome mostrado no exemplo, você recebe um erro porque esse nome já está em uso.</span><span class="sxs-lookup"><span data-stu-id="cc17a-157">If you use the name shown in the example, you receive an error because that name is already in use.</span></span>

```powershell
New-AzureRmStorageAccount -ResourceGroupName TestRG1 -AccountName mystoragename -Type "Standard_LRS" -Location "South Central US"
```

<span data-ttu-id="cc17a-158">Se você precisar recuperar esse recurso posteriormente, use o seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="cc17a-158">If you need to retrieve this resource later, use the following cmdlet:</span></span>

```powershell
Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1
```

## <a name="add-a-tag"></a><span data-ttu-id="cc17a-159">Adicione uma marca</span><span class="sxs-lookup"><span data-stu-id="cc17a-159">Add a tag</span></span>

<span data-ttu-id="cc17a-160">Marcas permitem que você organize seus recursos de acordo com propriedades diferentes.</span><span class="sxs-lookup"><span data-stu-id="cc17a-160">Tags enable you to organize your resources according to different properties.</span></span> <span data-ttu-id="cc17a-161">Por exemplo, você pode ter vários recursos em diferentes grupos de recursos que pertencem ao mesmo departamento.</span><span class="sxs-lookup"><span data-stu-id="cc17a-161">For example, you may have several resources in different resource groups that belong to the same department.</span></span> <span data-ttu-id="cc17a-162">Você pode aplicar uma marca de departamento e o valor desses recursos para marcá-los como pertencentes à mesma categoria.</span><span class="sxs-lookup"><span data-stu-id="cc17a-162">You can apply a department tag and value to those resources to mark them as belonging to the same category.</span></span> <span data-ttu-id="cc17a-163">Ou, você pode marcar se um recurso é usado em um ambiente de produção ou de teste.</span><span class="sxs-lookup"><span data-stu-id="cc17a-163">Or, you can mark whether a resource is used in a production or test environment.</span></span> <span data-ttu-id="cc17a-164">Neste tópico, você aplicar marcas em apenas um recurso, mas em seu ambiente provavelmente faz sentido aplicar marcas em todos os seus recursos.</span><span class="sxs-lookup"><span data-stu-id="cc17a-164">In this topic, you apply tags to only one resource, but in your environment it most likely makes sense to apply tags to all your resources.</span></span>

<span data-ttu-id="cc17a-165">O cmdlet a seguir aplica-se duas marcas à sua conta de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="cc17a-165">The following cmdlet applies two tags to your storage account:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
 ```

<span data-ttu-id="cc17a-166">Marcas são atualizadas como um único objeto.</span><span class="sxs-lookup"><span data-stu-id="cc17a-166">Tags are updated as a single object.</span></span> <span data-ttu-id="cc17a-167">Para adicionar uma marca a um recurso que já inclui marcas, primeiro recupere as marcas existentes.</span><span class="sxs-lookup"><span data-stu-id="cc17a-167">To add a tag to a resource that already includes tags, first retrieve the existing tags.</span></span> <span data-ttu-id="cc17a-168">Adicionar nova marca para o objeto que contém as marcas existentes e reaplicar todas as marcas para o recurso.</span><span class="sxs-lookup"><span data-stu-id="cc17a-168">Add the new tag to the object that contains the existing tags, and reapply all the tags to the resource.</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
```

## <a name="search-for-resources"></a><span data-ttu-id="cc17a-169">Pesquisa de recursos</span><span class="sxs-lookup"><span data-stu-id="cc17a-169">Search for resources</span></span>

<span data-ttu-id="cc17a-170">Use o **AzureRmResource localizar** cmdlet para recuperar os recursos para os critérios de pesquisa diferentes.</span><span class="sxs-lookup"><span data-stu-id="cc17a-170">Use the **Find-AzureRmResource** cmdlet to retrieve resources for different search conditions.</span></span>

* <span data-ttu-id="cc17a-171">Para obter um recurso por nome, forneça o **ResourceNameContains** parâmetro:</span><span class="sxs-lookup"><span data-stu-id="cc17a-171">To get a resource by name, provide the **ResourceNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceNameContains mystoragename
  ```

* <span data-ttu-id="cc17a-172">Para obter todos os recursos em um grupo de recursos, forneça o **ResourceGroupNameContains** parâmetro:</span><span class="sxs-lookup"><span data-stu-id="cc17a-172">To get all the resources in a resource group, provide the **ResourceGroupNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceGroupNameContains TestRG1
  ```

* <span data-ttu-id="cc17a-173">Para obter todos os recursos com um valor e nome de marca, forneça o **TagName** e **TagValue** parâmetros:</span><span class="sxs-lookup"><span data-stu-id="cc17a-173">To get all the resources with a tag name and value, provide the **TagName** and **TagValue** parameters:</span></span>

  ```powershell
  Find-AzureRmResource -TagName Dept -TagValue IT
  ```

* <span data-ttu-id="cc17a-174">Para todos os recursos com um tipo de recurso específico, forneça o **ResourceType** parâmetro:</span><span class="sxs-lookup"><span data-stu-id="cc17a-174">To all the resources with a particular resource type, provide the **ResourceType** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceType Microsoft.Storage/storageAccounts
  ```

## <a name="lock-a-resource"></a><span data-ttu-id="cc17a-175">Um recurso de bloqueio</span><span class="sxs-lookup"><span data-stu-id="cc17a-175">Lock a resource</span></span>

<span data-ttu-id="cc17a-176">Quando você precisa certificar-se de um recurso crítico for acidentalmente excluído ou modificado, aplica um bloqueio no recurso.</span><span class="sxs-lookup"><span data-stu-id="cc17a-176">When you need to make sure a critical resource is not accidentally deleted or modified, apply a lock to the resource.</span></span> <span data-ttu-id="cc17a-177">Você pode especificar um **CanNotDelete** ou **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="cc17a-177">You can specify either a **CanNotDelete** or **ReadOnly**.</span></span>

<span data-ttu-id="cc17a-178">Para criar ou excluir bloqueios de gerenciamento, você deve ter acesso às ações `Microsoft.Authorization/*` ou `Microsoft.Authorization/locks/*`.</span><span class="sxs-lookup"><span data-stu-id="cc17a-178">To create or delete management locks, you must have access to `Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="cc17a-179">Das funções internas, somente Proprietário e Administrador do Acesso de Usuário recebem essas ações.</span><span class="sxs-lookup"><span data-stu-id="cc17a-179">Of the built-in roles, only Owner and User Access Administrator are granted those actions.</span></span>

<span data-ttu-id="cc17a-180">Para aplicar um bloqueio, use o seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="cc17a-180">To apply a lock, use the following cmdlet:</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="cc17a-181">O recurso bloqueado no exemplo anterior não pode ser excluído até que o bloqueio seja removido.</span><span class="sxs-lookup"><span data-stu-id="cc17a-181">The locked resource in the preceding example cannot be deleted until the lock is removed.</span></span> <span data-ttu-id="cc17a-182">Para remover um bloqueio, use:</span><span class="sxs-lookup"><span data-stu-id="cc17a-182">To remove a lock, use:</span></span>

```powershell
Remove-AzureRmResourceLock -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="cc17a-183">Para saber mais sobre bloqueios de configuração, confira [Bloquear recursos com o Azure Resource Manager](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="cc17a-183">For more information about setting locks, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

## <a name="remove-resources-or-resource-group"></a><span data-ttu-id="cc17a-184">Remover recursos ou grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="cc17a-184">Remove resources or resource group</span></span>
<span data-ttu-id="cc17a-185">Você pode remover um recurso ou grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="cc17a-185">You can remove a resource or resource group.</span></span> <span data-ttu-id="cc17a-186">Ao remover um grupo de recursos, você também removerá todos os recursos dentro daquele grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="cc17a-186">When you remove a resource group, you also remove all the resources within that resource group.</span></span>

* <span data-ttu-id="cc17a-187">Para excluir um recurso do grupo de recursos, use o cmdlet **Remove-AzureRmResource** .</span><span class="sxs-lookup"><span data-stu-id="cc17a-187">To delete a resource from the resource group, use the **Remove-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="cc17a-188">Esse cmdlet exclui o recurso, mas não exclui o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="cc17a-188">This cmdlet deletes the resource, but does not delete the resource group.</span></span>

  ```powershell
  Remove-AzureRmResource -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
  ```

* <span data-ttu-id="cc17a-189">Para excluir um grupo de recursos e todos os seus recursos, use o cmdlet **Remove-AzureRmResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="cc17a-189">To delete a resource group and all its resources, use the **Remove-AzureRmResourceGroup** cmdlet.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name TestRG1
  ```

<span data-ttu-id="cc17a-190">Para ambos os cmdlets, você deve confirmar que você deseja remover o recurso ou grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="cc17a-190">For both cmdlets, you are asked to confirm that you wish to remove the resource or resource group.</span></span> <span data-ttu-id="cc17a-191">Se a operação com êxito exclui o recurso ou grupo de recursos, ele retorna **True**.</span><span class="sxs-lookup"><span data-stu-id="cc17a-191">If the operation successfully deletes the resource or resource group, it returns **True**.</span></span>

## <a name="run-resource-manager-scripts-with-azure-automation"></a><span data-ttu-id="cc17a-192">Executar scripts do Resource Manager com a automação do Azure</span><span class="sxs-lookup"><span data-stu-id="cc17a-192">Run Resource Manager scripts with Azure Automation</span></span>

<span data-ttu-id="cc17a-193">Este tópico mostra como executar operações básicas em seus recursos com o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cc17a-193">This topic shows you how to perform basic operations on your resources with Azure PowerShell.</span></span> <span data-ttu-id="cc17a-194">Para cenários mais avançados de gerenciamento, normalmente você deseja criar um script e reutilizar esse script conforme necessário ou em uma agenda.</span><span class="sxs-lookup"><span data-stu-id="cc17a-194">For more advanced management scenarios, you typically want to create a script, and reuse that script as needed or on a schedule.</span></span> <span data-ttu-id="cc17a-195">[A automação do Azure](../automation/automation-intro.md) fornece uma maneira de automatizar frequentemente usados scripts que gerenciam as soluções do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc17a-195">[Azure Automation](../automation/automation-intro.md) provides a way for you to automate frequently used scripts that manage your Azure solutions.</span></span>

<span data-ttu-id="cc17a-196">Os tópicos a seguir mostram como usar a automação do Azure, o Resource Manager e o PowerShell para a realização de tarefas de gerenciamento:</span><span class="sxs-lookup"><span data-stu-id="cc17a-196">The following topics show you how to use Azure Automation, Resource Manager, and PowerShell to effectively perform management tasks:</span></span>

- <span data-ttu-id="cc17a-197">Para obter informações sobre como criar um runbook, consulte [meu primeiro runbook PowerShell](../automation/automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="cc17a-197">For information about creating a runbook, see [My first PowerShell runbook](../automation/automation-first-runbook-textual-powershell.md).</span></span>
- <span data-ttu-id="cc17a-198">Para obter informações sobre como trabalhar com galerias de scripts, consulte [galerias de Runbook e módulo de automação do Azure](../automation/automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="cc17a-198">For information about working with galleries of scripts, see [Runbook and module galleries for Azure Automation](../automation/automation-runbook-gallery.md).</span></span>
- <span data-ttu-id="cc17a-199">Para runbooks que inicie e pare as máquinas virtuais, consulte [cenário de automação do Azure: formato JSON usando marcas para criar uma agenda para a VM do Azure inicialização e desligamento](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span><span class="sxs-lookup"><span data-stu-id="cc17a-199">For runbooks that start and stop virtual machines, see [Azure Automation scenario: Using JSON-formatted tags to create a schedule for Azure VM startup and shutdown](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span></span>
- <span data-ttu-id="cc17a-200">Para runbooks que iniciar e parar máquinas virtuais fora do horário comercial, consulte [VMs iniciar/parar durante a solução de fora do horário comercial em automação](../automation/automation-solution-vm-management.md).</span><span class="sxs-lookup"><span data-stu-id="cc17a-200">For runbooks that start and stop virtual machines off-hours, see [Start/Stop VMs during off-hours solution in Automation](../automation/automation-solution-vm-management.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc17a-201">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cc17a-201">Next steps</span></span>
* <span data-ttu-id="cc17a-202">Para saber mais sobre a criação de modelos do Gerenciador de Recursos, consulte [Criando Modelos do Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="cc17a-202">To learn about creating Resource Manager templates, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="cc17a-203">Para saber mais sobre como implantar modelos, consulte [Implantar um aplicativo com o Modelo do Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="cc17a-203">To learn about deploying templates, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="cc17a-204">Você pode mover os recursos existentes para um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="cc17a-204">You can move existing resources to a new resource group.</span></span> <span data-ttu-id="cc17a-205">Para obter exemplos, confira [Mover recursos para um novo grupo de recursos ou uma nova assinatura](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="cc17a-205">For examples, see [Move Resources to New Resource Group or Subscription](resource-group-move-resources.md).</span></span>
* <span data-ttu-id="cc17a-206">Para obter orientação sobre como as empresas podem usar o Resource Manager para gerenciar assinaturas de forma eficaz, consulte [Azure enterprise scaffold – controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="cc17a-206">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

