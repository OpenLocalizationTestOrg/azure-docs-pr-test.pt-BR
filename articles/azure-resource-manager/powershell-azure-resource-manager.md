---
title: "aaaManage Azure soluções com o PowerShell | Microsoft Docs"
description: Use o PowerShell do Azure e o Gerenciador de recursos toomanage seus recursos.
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
ms.openlocfilehash: 47a91af8d7eb59585bcfd43571ce76b90a0d7971
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-with-azure-powershell-and-resource-manager"></a><span data-ttu-id="0d2fa-103">Gerenciar recursos com o Azure PowerShell e o Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0d2fa-103">Manage resources with Azure PowerShell and Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0d2fa-104">Portal</span><span class="sxs-lookup"><span data-stu-id="0d2fa-104">Portal</span></span>](resource-group-portal.md)
> * [<span data-ttu-id="0d2fa-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="0d2fa-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="0d2fa-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0d2fa-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="0d2fa-107">API REST</span><span class="sxs-lookup"><span data-stu-id="0d2fa-107">REST API</span></span>](resource-manager-rest-api.md)
>
>

<span data-ttu-id="0d2fa-108">Neste artigo, você aprenderá como toomanage suas soluções com o PowerShell do Azure e o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-108">In this article, you learn how toomanage your solutions with Azure PowerShell and Azure Resource Manager.</span></span> <span data-ttu-id="0d2fa-109">Se você não estiver familiarizado com o Resource Manager, veja [Visão geral do Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0d2fa-109">If you are not familiar with Resource Manager, see [Resource Manager Overview](resource-group-overview.md).</span></span> <span data-ttu-id="0d2fa-110">Este tópico se concentra nas tarefas de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-110">This topic focuses on management tasks.</span></span> <span data-ttu-id="0d2fa-111">Você irá:</span><span class="sxs-lookup"><span data-stu-id="0d2fa-111">You will:</span></span>

1. <span data-ttu-id="0d2fa-112">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="0d2fa-112">Create a resource group</span></span>
2. <span data-ttu-id="0d2fa-113">Adicionar um grupo de recursos do recurso toohello</span><span class="sxs-lookup"><span data-stu-id="0d2fa-113">Add a resource toohello resource group</span></span>
3. <span data-ttu-id="0d2fa-114">Adicionar um recurso de toohello de marca</span><span class="sxs-lookup"><span data-stu-id="0d2fa-114">Add a tag toohello resource</span></span>
4. <span data-ttu-id="0d2fa-115">Recursos de consulta baseados em nomes ou em valores de marca</span><span class="sxs-lookup"><span data-stu-id="0d2fa-115">Query resources based on names or tag values</span></span>
5. <span data-ttu-id="0d2fa-116">Aplicar e remover um bloqueio no recurso Olá</span><span class="sxs-lookup"><span data-stu-id="0d2fa-116">Apply and remove a lock on hello resource</span></span>
6. <span data-ttu-id="0d2fa-117">Excluir um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="0d2fa-117">Delete a resource group</span></span>

<span data-ttu-id="0d2fa-118">Este artigo não mostra como toodeploy uma assinatura de tooyour de modelo do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-118">This article does not show how toodeploy a Resource Manager template tooyour subscription.</span></span> <span data-ttu-id="0d2fa-119">Para obter essas informações, veja [Implantar recursos com modelos do Resource Manager e o Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="0d2fa-119">For that information, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>

## <a name="get-started-with-azure-powershell"></a><span data-ttu-id="0d2fa-120">Introdução ao Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0d2fa-120">Get started with Azure PowerShell</span></span>

<span data-ttu-id="0d2fa-121">Se você não tiver instalado o Azure PowerShell, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0d2fa-121">If you have not installed Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="0d2fa-122">Se você instalou o Azure PowerShell no hello anterior, mas não tiver atualizado-recentemente, considere a possibilidade de instalar a versão mais recente do hello.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-122">If you have installed Azure PowerShell in hello past but have not updated it recently, consider installing hello latest version.</span></span> <span data-ttu-id="0d2fa-123">Você pode atualizar a versão de hello por meio de saudação mesmo método usado tooinstall-lo.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-123">You can update hello version through hello same method you used tooinstall it.</span></span> <span data-ttu-id="0d2fa-124">Por exemplo, se você usou Olá Web Platform Installer, iniciá-lo novamente e procure uma atualização.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-124">For example, if you used hello Web Platform Installer, launch it again and look for an update.</span></span>

<span data-ttu-id="0d2fa-125">toocheck sua versão do hello módulo de recursos do Azure, use Olá cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="0d2fa-125">toocheck your version of hello Azure Resources module, use hello following cmdlet:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="0d2fa-126">Este tópico foi atualizado para a versão 3.3.0.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-126">This topic was updated for version 3.3.0.</span></span> <span data-ttu-id="0d2fa-127">Se você tiver uma versão anterior, sua experiência pode não corresponder etapas Olá mostradas neste tópico.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-127">If you have an earlier version, your experience might not match hello steps shown in this topic.</span></span> <span data-ttu-id="0d2fa-128">Para obter a documentação sobre os cmdlets de saudação nesta versão, consulte [AzureRM.Resources módulo](/powershell/module/azurerm.resources).</span><span class="sxs-lookup"><span data-stu-id="0d2fa-128">For documentation about hello cmdlets in this version, see [AzureRM.Resources Module](/powershell/module/azurerm.resources).</span></span>

## <a name="log-in-tooyour-azure-account"></a><span data-ttu-id="0d2fa-129">Faça logon no tooyour conta do Azure</span><span class="sxs-lookup"><span data-stu-id="0d2fa-129">Log in tooyour Azure account</span></span>
<span data-ttu-id="0d2fa-130">Antes de iniciar sua solução, você deve fazer logon na conta de tooyour.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-130">Before working on your solution, you must log in tooyour account.</span></span>

<span data-ttu-id="0d2fa-131">toolog em tooyour conta do Azure, use Olá **AzureRmAccount Login** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-131">toolog in tooyour Azure account, use hello **Login-AzureRmAccount** cmdlet.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="0d2fa-132">Olá cmdlet solicita as credenciais de logon de saudação para sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-132">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="0d2fa-133">Após o logon, ele baixa as configurações de conta para que eles fiquem disponível tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-133">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span>

<span data-ttu-id="0d2fa-134">Olá cmdlet retorna informações sobre sua conta e hello toouse de assinatura para tarefas de saudação.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-134">hello cmdlet returns information about your account and hello subscription toouse for hello tasks.</span></span>

```powershell
Environment           : AzureCloud
Account               : example@contoso.com
TenantId              : {guid}
SubscriptionId        : {guid}
SubscriptionName      : Example Subscription One
CurrentStorageAccount :

```

<span data-ttu-id="0d2fa-135">Se você tiver mais de uma assinatura, você pode alternar a assinatura de tooa diferente.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-135">If you have more than one subscription, you can switch tooa different subscription.</span></span> <span data-ttu-id="0d2fa-136">Primeiro, vamos ver todas as assinaturas de saudação para sua conta.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-136">First, let's see all hello subscriptions for your account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="0d2fa-137">Retorna habilitados e desabilitados de assinaturas.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-137">It returns enabled and disabled subscriptions.</span></span>

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

<span data-ttu-id="0d2fa-138">tooswitch tooa de assinatura diferente, forneça o nome de assinatura de saudação com hello **AzureRmContext conjunto** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-138">tooswitch tooa different subscription, provide hello subscription name with hello **Set-AzureRmContext** cmdlet.</span></span>

```powershell
Set-AzureRmContext -SubscriptionName "Example Subscription Two"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="0d2fa-139">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="0d2fa-139">Create a resource group</span></span>
<span data-ttu-id="0d2fa-140">Antes de implantar qualquer assinatura de recursos de tooyour, você deve criar um grupo de recursos que contém recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-140">Before deploying any resources tooyour subscription, you must create a resource group that will contain hello resources.</span></span>

<span data-ttu-id="0d2fa-141">toocreate um grupo de recursos, use Olá **AzureRmResourceGroup novo** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-141">toocreate a resource group, use hello **New-AzureRmResourceGroup** cmdlet.</span></span> <span data-ttu-id="0d2fa-142">usa o comando Olá Olá **nome** toospecify parâmetro um nome para o grupo de recursos de saudação e hello **local** parâmetro toospecify seu local.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-142">hello command uses hello **Name** parameter toospecify a name for hello resource group and hello **Location** parameter toospecify its location.</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location "South Central US"
```

<span data-ttu-id="0d2fa-143">saída de Hello for Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="0d2fa-143">hello output is in hello following format:</span></span>

```powershell
ResourceGroupName : TestRG1
Location          : southcentralus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/{guid}/resourceGroups/TestRG1
```

<span data-ttu-id="0d2fa-144">Se você precisar de grupo de recursos do tooretrieve hello mais tarde, use Olá cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="0d2fa-144">If you need tooretrieve hello resource group later, use hello following cmdlet:</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName TestRG1
```

<span data-ttu-id="0d2fa-145">tooget todos os grupos de recursos em sua assinatura de hello, não especifique um nome:</span><span class="sxs-lookup"><span data-stu-id="0d2fa-145">tooget all hello resource groups in your subscription, do not specify a name:</span></span>

```powershell
Get-AzureRmResourceGroup
```

## <a name="add-resources-tooa-resource-group"></a><span data-ttu-id="0d2fa-146">Adicionar grupo de recursos tooa de recursos</span><span class="sxs-lookup"><span data-stu-id="0d2fa-146">Add resources tooa resource group</span></span>
<span data-ttu-id="0d2fa-147">tooadd um grupo de recursos de toohello de recurso, você pode usar o hello **New-AzureRmResource** cmdlet ou um cmdlet que toohello específico de tipo de recurso que você está criando (como **novo AzureRmStorageAccount**).</span><span class="sxs-lookup"><span data-stu-id="0d2fa-147">tooadd a resource toohello resource group, you can use hello **New-AzureRmResource** cmdlet or a cmdlet that is specific toohello type of resource you are creating (like **New-AzureRmStorageAccount**).</span></span> <span data-ttu-id="0d2fa-148">Talvez seja mais fácil toouse um cmdlet que é o tipo de recurso específico tooa porque ele inclui parâmetros para propriedades de saudação que são necessários para o novo recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-148">You might find it easier toouse a cmdlet that is specific tooa resource type because it includes parameters for hello properties that are needed for hello new resource.</span></span> <span data-ttu-id="0d2fa-149">toouse **New-AzureRmResource**, você deve saber todas as tooset de propriedades de saudação sem ser solicitado para eles.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-149">toouse **New-AzureRmResource**, you must know all hello properties tooset without being prompted for them.</span></span>

<span data-ttu-id="0d2fa-150">No entanto, a adição de um recurso por meio de cmdlets pode causar confusão futuras porque o novo recurso de saudação não existe em um modelo do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-150">However, adding a resource through cmdlets might cause future confusion because hello new resource does not exist in a Resource Manager template.</span></span> <span data-ttu-id="0d2fa-151">A Microsoft recomenda definir a infraestrutura de saudação para sua solução do Azure em um modelo do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-151">Microsoft recommends defining hello infrastructure for your Azure solution in a Resource Manager template.</span></span> <span data-ttu-id="0d2fa-152">Modelos permitem que você tooreliably e repetidamente implantam sua solução.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-152">Templates enable you tooreliably and repeatedly deploy your solution.</span></span> <span data-ttu-id="0d2fa-153">Para este tópico, você cria uma conta de armazenamento com um cmdlet do PowerShell, mas posteriormente você gerar um modelo de seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-153">For this topic, you create a storage account with a PowerShell cmdlet, but later you generate a template from your resource group.</span></span>

<span data-ttu-id="0d2fa-154">Olá cmdlet a seguir cria uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-154">hello following cmdlet creates a storage account.</span></span> <span data-ttu-id="0d2fa-155">Em vez de usar o nome de saudação mostrado no exemplo hello, forneça um nome exclusivo para a conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-155">Instead of using hello name shown in hello example, provide a unique name for hello storage account.</span></span> <span data-ttu-id="0d2fa-156">Olá nome deve ter entre 3 e 24 caracteres de comprimento e usar somente números e letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-156">hello name must be between 3 and 24 characters in length, and use only numbers and lower-case letters.</span></span> <span data-ttu-id="0d2fa-157">Se você usar Olá nome mostrado no exemplo hello, você receberá um erro porque esse nome já está em uso.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-157">If you use hello name shown in hello example, you receive an error because that name is already in use.</span></span>

```powershell
New-AzureRmStorageAccount -ResourceGroupName TestRG1 -AccountName mystoragename -Type "Standard_LRS" -Location "South Central US"
```

<span data-ttu-id="0d2fa-158">Se você precisar desse recurso de tooretrieve posteriormente, use Olá cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="0d2fa-158">If you need tooretrieve this resource later, use hello following cmdlet:</span></span>

```powershell
Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1
```

## <a name="add-a-tag"></a><span data-ttu-id="0d2fa-159">Adicione uma marca</span><span class="sxs-lookup"><span data-stu-id="0d2fa-159">Add a tag</span></span>

<span data-ttu-id="0d2fa-160">As marcas permitem que você tooorganize seus recursos de acordo com as propriedades de toodifferent.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-160">Tags enable you tooorganize your resources according toodifferent properties.</span></span> <span data-ttu-id="0d2fa-161">Por exemplo, você pode ter vários recursos em diferentes grupos de recursos que pertencem a toohello mesmo departamento.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-161">For example, you may have several resources in different resource groups that belong toohello same department.</span></span> <span data-ttu-id="0d2fa-162">Você pode aplicar um toomark departamento marca e o valor toothose recursos-los como pertencentes toohello mesma categoria.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-162">You can apply a department tag and value toothose resources toomark them as belonging toohello same category.</span></span> <span data-ttu-id="0d2fa-163">Ou, você pode marcar se um recurso é usado em um ambiente de produção ou de teste.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-163">Or, you can mark whether a resource is used in a production or test environment.</span></span> <span data-ttu-id="0d2fa-164">Neste tópico, você aplicar marcas tooonly um recurso, mas em seu ambiente provavelmente faz sentido tooapply marcas tooall seus recursos.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-164">In this topic, you apply tags tooonly one resource, but in your environment it most likely makes sense tooapply tags tooall your resources.</span></span>

<span data-ttu-id="0d2fa-165">Olá cmdlet a seguir aplica-se a conta de armazenamento do duas marcas tooyour:</span><span class="sxs-lookup"><span data-stu-id="0d2fa-165">hello following cmdlet applies two tags tooyour storage account:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
 ```

<span data-ttu-id="0d2fa-166">Marcas são atualizadas como um único objeto.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-166">Tags are updated as a single object.</span></span> <span data-ttu-id="0d2fa-167">tooadd um recurso de tooa de marca que já inclua marcas, recuperar marcas existentes hello.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-167">tooadd a tag tooa resource that already includes tags, first retrieve hello existing tags.</span></span> <span data-ttu-id="0d2fa-168">Adicionar Olá nova marca toohello objeto que contém marcas existentes hello e reaplique todos os recursos de toohello marcas hello.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-168">Add hello new tag toohello object that contains hello existing tags, and reapply all hello tags toohello resource.</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
```

## <a name="search-for-resources"></a><span data-ttu-id="0d2fa-169">Pesquisa de recursos</span><span class="sxs-lookup"><span data-stu-id="0d2fa-169">Search for resources</span></span>

<span data-ttu-id="0d2fa-170">Saudação de uso **Find-AzureRmResource** cmdlet tooretrieve recursos para condições de pesquisa diferente.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-170">Use hello **Find-AzureRmResource** cmdlet tooretrieve resources for different search conditions.</span></span>

* <span data-ttu-id="0d2fa-171">tooget um recurso por nome, fornecer Olá **ResourceNameContains** parâmetro:</span><span class="sxs-lookup"><span data-stu-id="0d2fa-171">tooget a resource by name, provide hello **ResourceNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceNameContains mystoragename
  ```

* <span data-ttu-id="0d2fa-172">tooget todos os recursos de saudação em um grupo de recursos, fornecer Olá **ResourceGroupNameContains** parâmetro:</span><span class="sxs-lookup"><span data-stu-id="0d2fa-172">tooget all hello resources in a resource group, provide hello **ResourceGroupNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceGroupNameContains TestRG1
  ```

* <span data-ttu-id="0d2fa-173">tooget todos os recursos de saudação com um nome de marca e o valor fornecem Olá **TagName** e **TagValue** parâmetros:</span><span class="sxs-lookup"><span data-stu-id="0d2fa-173">tooget all hello resources with a tag name and value, provide hello **TagName** and **TagValue** parameters:</span></span>

  ```powershell
  Find-AzureRmResource -TagName Dept -TagValue IT
  ```

* <span data-ttu-id="0d2fa-174">recursos de saudação tooall com um tipo de recurso específico, forneça Olá **ResourceType** parâmetro:</span><span class="sxs-lookup"><span data-stu-id="0d2fa-174">tooall hello resources with a particular resource type, provide hello **ResourceType** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceType Microsoft.Storage/storageAccounts
  ```

## <a name="lock-a-resource"></a><span data-ttu-id="0d2fa-175">Um recurso de bloqueio</span><span class="sxs-lookup"><span data-stu-id="0d2fa-175">Lock a resource</span></span>

<span data-ttu-id="0d2fa-176">Quando você precisar toomake-se de que um recurso crítico é acidentalmente excluído ou modificado, aplica um recurso de bloqueio de toohello.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-176">When you need toomake sure a critical resource is not accidentally deleted or modified, apply a lock toohello resource.</span></span> <span data-ttu-id="0d2fa-177">Você pode especificar um **CanNotDelete** ou **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-177">You can specify either a **CanNotDelete** or **ReadOnly**.</span></span>

<span data-ttu-id="0d2fa-178">bloqueios de gerenciamento toocreate ou delete, você deve ter acesso muito`Microsoft.Authorization/*` ou `Microsoft.Authorization/locks/*` ações.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-178">toocreate or delete management locks, you must have access too`Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="0d2fa-179">De funções internas do hello, somente o proprietário e o administrador de acesso do usuário são concedidas as ações.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-179">Of hello built-in roles, only Owner and User Access Administrator are granted those actions.</span></span>

<span data-ttu-id="0d2fa-180">tooapply um bloqueio, use Olá cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="0d2fa-180">tooapply a lock, use hello following cmdlet:</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="0d2fa-181">Olá recurso bloqueado no hello anterior exemplo não pode ser excluído até que Olá bloqueio seja removido.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-181">hello locked resource in hello preceding example cannot be deleted until hello lock is removed.</span></span> <span data-ttu-id="0d2fa-182">tooremove um bloqueio, use:</span><span class="sxs-lookup"><span data-stu-id="0d2fa-182">tooremove a lock, use:</span></span>

```powershell
Remove-AzureRmResourceLock -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="0d2fa-183">Para saber mais sobre bloqueios de configuração, confira [Bloquear recursos com o Azure Resource Manager](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="0d2fa-183">For more information about setting locks, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

## <a name="remove-resources-or-resource-group"></a><span data-ttu-id="0d2fa-184">Remover recursos ou grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="0d2fa-184">Remove resources or resource group</span></span>
<span data-ttu-id="0d2fa-185">Você pode remover um recurso ou grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-185">You can remove a resource or resource group.</span></span> <span data-ttu-id="0d2fa-186">Quando você remove um grupo de recursos, você também remover todos os recursos de saudação dentro desse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-186">When you remove a resource group, you also remove all hello resources within that resource group.</span></span>

* <span data-ttu-id="0d2fa-187">toodelete um recurso do grupo de recursos hello, use Olá **Remove-AzureRmResource** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-187">toodelete a resource from hello resource group, use hello **Remove-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="0d2fa-188">Esse cmdlet exclui o recurso hello, mas não exclui o grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-188">This cmdlet deletes hello resource, but does not delete hello resource group.</span></span>

  ```powershell
  Remove-AzureRmResource -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
  ```

* <span data-ttu-id="0d2fa-189">toodelete um grupo de recursos e todos os seus recursos, use Olá **AzureRmResourceGroup remover** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-189">toodelete a resource group and all its resources, use hello **Remove-AzureRmResourceGroup** cmdlet.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name TestRG1
  ```

<span data-ttu-id="0d2fa-190">Para ambos os cmdlets, você será solicitado tooconfirm que desejar que recursos de saudação tooremove ou grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-190">For both cmdlets, you are asked tooconfirm that you wish tooremove hello resource or resource group.</span></span> <span data-ttu-id="0d2fa-191">Se o operação de saudação exclui com êxito recurso hello ou grupo de recursos, ele retorna **True**.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-191">If hello operation successfully deletes hello resource or resource group, it returns **True**.</span></span>

## <a name="run-resource-manager-scripts-with-azure-automation"></a><span data-ttu-id="0d2fa-192">Executar scripts do Resource Manager com a automação do Azure</span><span class="sxs-lookup"><span data-stu-id="0d2fa-192">Run Resource Manager scripts with Azure Automation</span></span>

<span data-ttu-id="0d2fa-193">Este tópico mostra como operações básicas de tooperform em seus recursos com o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-193">This topic shows you how tooperform basic operations on your resources with Azure PowerShell.</span></span> <span data-ttu-id="0d2fa-194">Para cenários mais avançados de gerenciamento, você normalmente deseja toocreate um script e reutilizar esse script conforme o necessário ou em uma agenda.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-194">For more advanced management scenarios, you typically want toocreate a script, and reuse that script as needed or on a schedule.</span></span> <span data-ttu-id="0d2fa-195">[Automação do Azure](../automation/automation-intro.md) fornece uma maneira para você scripts tooautomate usado com frequência que gerencia as soluções do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-195">[Azure Automation](../automation/automation-intro.md) provides a way for you tooautomate frequently used scripts that manage your Azure solutions.</span></span>

<span data-ttu-id="0d2fa-196">Olá tópicos a seguir mostram como toouse automação do Azure, o Gerenciador de recursos e o PowerShell tooeffectively executam tarefas de gerenciamento:</span><span class="sxs-lookup"><span data-stu-id="0d2fa-196">hello following topics show you how toouse Azure Automation, Resource Manager, and PowerShell tooeffectively perform management tasks:</span></span>

- <span data-ttu-id="0d2fa-197">Para obter informações sobre como criar um runbook, consulte [meu primeiro runbook PowerShell](../automation/automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="0d2fa-197">For information about creating a runbook, see [My first PowerShell runbook](../automation/automation-first-runbook-textual-powershell.md).</span></span>
- <span data-ttu-id="0d2fa-198">Para obter informações sobre como trabalhar com galerias de scripts, consulte [galerias de Runbook e módulo de automação do Azure](../automation/automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="0d2fa-198">For information about working with galleries of scripts, see [Runbook and module galleries for Azure Automation](../automation/automation-runbook-gallery.md).</span></span>
- <span data-ttu-id="0d2fa-199">Para runbooks que iniciar e parar máquinas virtuais, consulte [cenário de automação do Azure: toocreate marcas formatada em JSON usando uma agenda para a VM do Azure inicialização e desligamento](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span><span class="sxs-lookup"><span data-stu-id="0d2fa-199">For runbooks that start and stop virtual machines, see [Azure Automation scenario: Using JSON-formatted tags toocreate a schedule for Azure VM startup and shutdown](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span></span>
- <span data-ttu-id="0d2fa-200">Para runbooks que iniciar e parar máquinas virtuais fora do horário comercial, consulte [VMs iniciar/parar durante a solução de fora do horário comercial em automação](../automation/automation-solution-vm-management.md).</span><span class="sxs-lookup"><span data-stu-id="0d2fa-200">For runbooks that start and stop virtual machines off-hours, see [Start/Stop VMs during off-hours solution in Automation](../automation/automation-solution-vm-management.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d2fa-201">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0d2fa-201">Next steps</span></span>
* <span data-ttu-id="0d2fa-202">toolearn sobre como criar modelos do Gerenciador de recursos, consulte [criação de modelos de Gerenciador de recursos do Azure](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="0d2fa-202">toolearn about creating Resource Manager templates, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="0d2fa-203">toolearn sobre a implantação de modelos, consulte [implantar um aplicativo com o modelo do Gerenciador de recursos do Azure](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="0d2fa-203">toolearn about deploying templates, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="0d2fa-204">Você pode mover recursos tooa novo grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="0d2fa-204">You can move existing resources tooa new resource group.</span></span> <span data-ttu-id="0d2fa-205">Para obter exemplos, consulte [tooNew recursos Mover grupo de recursos ou assinatura](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="0d2fa-205">For examples, see [Move Resources tooNew Resource Group or Subscription](resource-group-move-resources.md).</span></span>
* <span data-ttu-id="0d2fa-206">Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="0d2fa-206">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

