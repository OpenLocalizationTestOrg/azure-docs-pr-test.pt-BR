---
title: "erros comuns de implantação do Azure aaaTroubleshoot | Microsoft Docs"
description: "Descreve como erros comuns de tooresolve quando você implanta tooAzure de recursos usando o Gerenciador de recursos do Azure."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "Erro de implantação, implantação do azure, implantar tooazure"
ms.assetid: c002a9be-4de5-4963-bd14-b54aa3d8fa59
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: tomfitz
ms.openlocfilehash: 8571e9941879eb5586e4258a785b6a09247da771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a><span data-ttu-id="a2268-104">Solução de erros comuns de implantação do Azure com o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a2268-104">Troubleshoot common Azure deployment errors with Azure Resource Manager</span></span>
<span data-ttu-id="a2268-105">Este tópico descreve como é possível resolver alguns erros de implantação comuns do Azure que você pode encontrar.</span><span class="sxs-lookup"><span data-stu-id="a2268-105">This topic describes how you can resolve some common Azure deployment errors you may encounter.</span></span>

<span data-ttu-id="a2268-106">Olá códigos de erro a seguir é descrita neste tópico:</span><span class="sxs-lookup"><span data-stu-id="a2268-106">hello following error codes are described in this topic:</span></span>

* [<span data-ttu-id="a2268-107">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="a2268-107">AccountNameInvalid</span></span>](#accountnameinvalid)
* [<span data-ttu-id="a2268-108">Falha na autorização</span><span class="sxs-lookup"><span data-stu-id="a2268-108">Authorization failed</span></span>](#authorization-failed)
* [<span data-ttu-id="a2268-109">BadRequest</span><span class="sxs-lookup"><span data-stu-id="a2268-109">BadRequest</span></span>](#badrequest)
* [<span data-ttu-id="a2268-110">DeploymentFailed</span><span class="sxs-lookup"><span data-stu-id="a2268-110">DeploymentFailed</span></span>](#deploymentfailed)
* [<span data-ttu-id="a2268-111">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="a2268-111">DisallowedOperation</span></span>](#disallowedoperation)
* [<span data-ttu-id="a2268-112">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="a2268-112">InvalidContentLink</span></span>](#invalidcontentlink)
* [<span data-ttu-id="a2268-113">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="a2268-113">InvalidTemplate</span></span>](#invalidtemplate)
* [<span data-ttu-id="a2268-114">MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="a2268-114">MissingSubscriptionRegistration</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="a2268-115">NotFound</span><span class="sxs-lookup"><span data-stu-id="a2268-115">NotFound</span></span>](#notfound)
* [<span data-ttu-id="a2268-116">NoRegisteredProviderFound</span><span class="sxs-lookup"><span data-stu-id="a2268-116">NoRegisteredProviderFound</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="a2268-117">OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="a2268-117">OperationNotAllowed</span></span>](#quotaexceeded)
* [<span data-ttu-id="a2268-118">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="a2268-118">ParentResourceNotFound</span></span>](#parentresourcenotfound)
* [<span data-ttu-id="a2268-119">QuotaExceeded</span><span class="sxs-lookup"><span data-stu-id="a2268-119">QuotaExceeded</span></span>](#quotaexceeded)
* [<span data-ttu-id="a2268-120">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="a2268-120">RequestDisallowedByPolicy</span></span>](#requestdisallowedbypolicy)
* [<span data-ttu-id="a2268-121">ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="a2268-121">ResourceNotFound</span></span>](#notfound)
* [<span data-ttu-id="a2268-122">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="a2268-122">SkuNotAvailable</span></span>](#skunotavailable)
* [<span data-ttu-id="a2268-123">StorageAccountAlreadyExists</span><span class="sxs-lookup"><span data-stu-id="a2268-123">StorageAccountAlreadyExists</span></span>](#storagenamenotunique)
* [<span data-ttu-id="a2268-124">StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="a2268-124">StorageAccountAlreadyTaken</span></span>](#storagenamenotunique)

## <a name="deploymentfailed"></a><span data-ttu-id="a2268-125">DeploymentFailed</span><span class="sxs-lookup"><span data-stu-id="a2268-125">DeploymentFailed</span></span>

<span data-ttu-id="a2268-126">Esse código de erro indica um erro de implantação geral, mas não é código de erro Olá precisar toostart de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="a2268-126">This error code indicates a general deployment error, but it is not hello error code you need toostart troubleshooting.</span></span> <span data-ttu-id="a2268-127">código de erro de saudação que realmente ajuda você a resolver o problema de saudação geralmente é um nível abaixo desse erro.</span><span class="sxs-lookup"><span data-stu-id="a2268-127">hello error code that actually helps you resolve hello issue is usually one level below this error.</span></span> <span data-ttu-id="a2268-128">Por exemplo, hello imagem a seguir mostra Olá **RequestDisallowedByPolicy** código de erro que está sob o erro de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="a2268-128">For example, hello following image shows hello **RequestDisallowedByPolicy** error code that is under hello deployment error.</span></span>

![mostrar código de erro](./media/resource-manager-common-deployment-errors/error-code.png)

## <a name="skunotavailable"></a><span data-ttu-id="a2268-130">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="a2268-130">SkuNotAvailable</span></span>

<span data-ttu-id="a2268-131">Ao implantar um recurso (normalmente uma máquina virtual), você pode receber Olá mensagem de erro e o código de erro a seguir:</span><span class="sxs-lookup"><span data-stu-id="a2268-131">When deploying a resource (typically a virtual machine), you may receive hello following error code and error message:</span></span>

```
Code: SkuNotAvailable
Message: hello requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy tooa different location.
```

<span data-ttu-id="a2268-132">Você recebe esse erro quando o recurso Olá SKU selecionado (por exemplo, o tamanho da VM) não está disponível para o local de saudação selecionado.</span><span class="sxs-lookup"><span data-stu-id="a2268-132">You receive this error when hello resource SKU you have selected (such as VM size) is not available for hello location you have selected.</span></span> <span data-ttu-id="a2268-133">tooresolve esse problema, você precisa toodetermine que SKUs estão disponíveis em uma região.</span><span class="sxs-lookup"><span data-stu-id="a2268-133">tooresolve this issue, you need toodetermine which SKUs are available in a region.</span></span> <span data-ttu-id="a2268-134">Você pode usar o PowerShell, Olá portal ou um toofind da operação REST SKUs disponíveis.</span><span class="sxs-lookup"><span data-stu-id="a2268-134">You can use PowerShell, hello portal, or a REST operation toofind available SKUs.</span></span>

- <span data-ttu-id="a2268-135">Para o PowerShell, use [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) e filtre por localização.</span><span class="sxs-lookup"><span data-stu-id="a2268-135">For PowerShell, use [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) and filter by location.</span></span> <span data-ttu-id="a2268-136">Você deve ter a versão mais recente de saudação do PowerShell para este comando.</span><span class="sxs-lookup"><span data-stu-id="a2268-136">You must have hello latest version of PowerShell for this command.</span></span>

  ```powershell
  Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
  ```

  <span data-ttu-id="a2268-137">resultados da saudação incluem uma lista de SKUs para o local do hello e as restrições para a SKU.</span><span class="sxs-lookup"><span data-stu-id="a2268-137">hello results include a list of SKUs for hello location and any restrictions for that SKU.</span></span>

  ```powershell
  ResourceType                Name      Locations Restriction                      Capability Value
  ------------                ----      --------- -----------                      ---------- -----
  availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
  availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
  virtualMachines      Standard_A0 southcentralus
  virtualMachines      Standard_A1 southcentralus
  virtualMachines      Standard_A2 southcentralus
  ```

- <span data-ttu-id="a2268-138">Olá toouse [portal](https://portal.azure.com), faça logon no portal de toohello e adicionar um recurso por meio da interface de saudação.</span><span class="sxs-lookup"><span data-stu-id="a2268-138">toouse hello [portal](https://portal.azure.com), log in toohello portal and add a resource through hello interface.</span></span> <span data-ttu-id="a2268-139">Como definir os valores hello, você vê Olá SKUs disponíveis para esse recurso.</span><span class="sxs-lookup"><span data-stu-id="a2268-139">As you set hello values, you see hello available SKUs for that resource.</span></span> <span data-ttu-id="a2268-140">Implantação de saudação toocomplete não é necessário.</span><span class="sxs-lookup"><span data-stu-id="a2268-140">You do not need toocomplete hello deployment.</span></span>

    ![SKUs disponíveis](./media/resource-manager-common-deployment-errors/view-sku.png)

- <span data-ttu-id="a2268-142">Olá toouse API REST para máquinas virtuais, enviar Olá solicitação a seguir:</span><span class="sxs-lookup"><span data-stu-id="a2268-142">toouse hello REST API for virtual machines, send hello following request:</span></span>

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  <span data-ttu-id="a2268-143">Ele retorna disponível SKUs e regiões no hello formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="a2268-143">It returns available SKUs and regions in hello following format:</span></span>

  ```json
  {
    "value": [
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A0",
        "tier": "Standard",
        "size": "A0",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A1",
        "tier": "Standard",
        "size": "A1",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      ...
    ]
  }    
  ```

<span data-ttu-id="a2268-144">Se você não é possível toofind uma SKU adequada na região ou uma região alternativa que atenda às suas necessidades de negócios, enviar um [solicitação SKU](https://aka.ms/skurestriction) tooAzure suporte.</span><span class="sxs-lookup"><span data-stu-id="a2268-144">If you are unable toofind a suitable SKU in that region or an alternative region that meets your business needs, submit a [SKU request](https://aka.ms/skurestriction) tooAzure Support.</span></span>

## <a name="disallowedoperation"></a><span data-ttu-id="a2268-145">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="a2268-145">DisallowedOperation</span></span>

```
Code: DisallowedOperation
Message: hello current subscription type is not permitted tooperform operations on any provider 
namespace. Please use a different subscription.
```

<span data-ttu-id="a2268-146">Se você receber esse erro, você está usando uma assinatura que não é permitido tooaccess todos os serviços do Azure que não sejam do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="a2268-146">If you receive this error, you are using a subscription that is not permitted tooaccess any Azure services other than Azure Active Directory.</span></span> <span data-ttu-id="a2268-147">Você pode ter esse tipo de assinatura quando você precisar portal clássico do tooaccess hello, mas não é permitidas toodeploy recursos.</span><span class="sxs-lookup"><span data-stu-id="a2268-147">You might have this type of subscription when you need tooaccess hello classic portal but are not permitted toodeploy resources.</span></span> <span data-ttu-id="a2268-148">tooresolve esse problema, você deve usar uma assinatura que tem permissão toodeploy recursos.</span><span class="sxs-lookup"><span data-stu-id="a2268-148">tooresolve this issue, you must use a subscription that has permission toodeploy resources.</span></span>  

<span data-ttu-id="a2268-149">tooview suas assinaturas disponíveis com o PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="a2268-149">tooview your available subscriptions with PowerShell, use:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="a2268-150">E assinatura atual tooset hello, use:</span><span class="sxs-lookup"><span data-stu-id="a2268-150">And, tooset hello current subscription, use:</span></span>

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

<span data-ttu-id="a2268-151">tooview suas assinaturas disponíveis com o Azure 2.0 do CLI, use:</span><span class="sxs-lookup"><span data-stu-id="a2268-151">tooview your available subscriptions with Azure CLI 2.0, use:</span></span>

```azurecli
az account list
```

<span data-ttu-id="a2268-152">E assinatura atual tooset hello, use:</span><span class="sxs-lookup"><span data-stu-id="a2268-152">And, tooset hello current subscription, use:</span></span>

```azurecli
az account set --subscription {subscription-name}
```

## <a name="invalidtemplate"></a><span data-ttu-id="a2268-153">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="a2268-153">InvalidTemplate</span></span>
<span data-ttu-id="a2268-154">Esse erro pode resultar de vários tipos diferentes de erros.</span><span class="sxs-lookup"><span data-stu-id="a2268-154">This error can result from several different types of errors.</span></span>

- <span data-ttu-id="a2268-155">Erro de sintaxe</span><span class="sxs-lookup"><span data-stu-id="a2268-155">Syntax error</span></span>

   <span data-ttu-id="a2268-156">Se você receber uma mensagem de erro que indica a validação do modelo falha hello, você pode ter um problema de sintaxe em seu modelo.</span><span class="sxs-lookup"><span data-stu-id="a2268-156">If you receive an error message that indicates hello template failed validation, you may have a syntax problem in your template.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   <span data-ttu-id="a2268-157">Esse erro é fácil toomake como expressões de modelo podem ser complexas.</span><span class="sxs-lookup"><span data-stu-id="a2268-157">This error is easy toomake because template expressions can be intricate.</span></span> <span data-ttu-id="a2268-158">Por exemplo, hello seguinte atribuição de nome de uma conta de armazenamento contém um conjunto de colchetes, três funções, três conjuntos de parênteses, um conjunto de aspas simples e uma propriedade:</span><span class="sxs-lookup"><span data-stu-id="a2268-158">For example, hello following name assignment for a storage account contains one set of brackets, three functions, three sets of parentheses, one set of single quotes, and one property:</span></span>

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   <span data-ttu-id="a2268-159">Se você não fornecer uma sintaxe de correspondência de Olá, o modelo Olá produz um valor que é diferente de sua intenção.</span><span class="sxs-lookup"><span data-stu-id="a2268-159">If you do not provide hello matching syntax, hello template produces a value that is different than your intention.</span></span>

   <span data-ttu-id="a2268-160">Quando você receber esse tipo de erro, revise atentamente a sintaxe de expressão hello.</span><span class="sxs-lookup"><span data-stu-id="a2268-160">When you receive this type of error, carefully review hello expression syntax.</span></span> <span data-ttu-id="a2268-161">Considere usar um editor JSON como o [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) ou o [Visual Studio Code](resource-manager-vs-code.md) que pode avisá-lo sobre os erros de sintaxe.</span><span class="sxs-lookup"><span data-stu-id="a2268-161">Consider using a JSON editor like [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) or [Visual Studio Code](resource-manager-vs-code.md), which can warn you about syntax errors.</span></span>

- <span data-ttu-id="a2268-162">Comprimentos de segmento incorretos</span><span class="sxs-lookup"><span data-stu-id="a2268-162">Incorrect segment lengths</span></span>

   <span data-ttu-id="a2268-163">Outro erro de modelo inválida ocorre quando o nome do recurso Olá não está no formato correto de saudação.</span><span class="sxs-lookup"><span data-stu-id="a2268-163">Another invalid template error occurs when hello resource name is not in hello correct format.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'hello template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   <span data-ttu-id="a2268-164">Um recurso no nível raiz deve ter um segmento de menos em nome de saudação que no tipo de recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="a2268-164">A root level resource must have one less segment in hello name than in hello resource type.</span></span> <span data-ttu-id="a2268-165">Cada segmento é diferenciado por uma barra.</span><span class="sxs-lookup"><span data-stu-id="a2268-165">Each segment is differentiated by a slash.</span></span> <span data-ttu-id="a2268-166">Olá exemplo a seguir, o tipo de saudação possui dois segmentos e nome de saudação tem um segmento, portanto, é um **nome válido**.</span><span class="sxs-lookup"><span data-stu-id="a2268-166">In hello following example, hello type has two segments and hello name has one segment, so it is a **valid name**.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="a2268-167">Mas Olá próximo exemplo é **não é um nome válido** porque ele tem Olá mesmo número de segmentos que tipo de saudação.</span><span class="sxs-lookup"><span data-stu-id="a2268-167">But hello next example is **not a valid name** because it has hello same number of segments as hello type.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="a2268-168">Para obter recursos filho, Olá tipo e o nome tem Olá mesmo número de segmentos.</span><span class="sxs-lookup"><span data-stu-id="a2268-168">For child resources, hello type and name have hello same number of segments.</span></span> <span data-ttu-id="a2268-169">Esse número de segmentos faz sentido, porque o nome completo do hello e tipo filho Olá inclui o tipo e o nome do pai de saudação.</span><span class="sxs-lookup"><span data-stu-id="a2268-169">This number of segments makes sense because hello full name and type for hello child includes hello parent name and type.</span></span> <span data-ttu-id="a2268-170">Portanto, nome completo Olá ainda tem um menor do segmento de tipo completo hello.</span><span class="sxs-lookup"><span data-stu-id="a2268-170">Therefore, hello full name still has one less segment than hello full type.</span></span>

  ```json
  "resources": [
      {
          "type": "Microsoft.KeyVault/vaults",
          "name": "contosokeyvault",
          ...
          "resources": [
              {
                  "type": "secrets",
                  "name": "appPassword",
                  ...
              }
          ]
      }
  ]
  ```

   <span data-ttu-id="a2268-171">Obtendo segmentos de saudação à direita podem ser complicados com tipos de Gerenciador de recursos que são aplicados em todos os provedores de recursos.</span><span class="sxs-lookup"><span data-stu-id="a2268-171">Getting hello segments right can be tricky with Resource Manager types that are applied across resource providers.</span></span> <span data-ttu-id="a2268-172">Por exemplo, a aplicação de um site da web de tooa de bloqueio de recurso requer um tipo com quatro segmentos.</span><span class="sxs-lookup"><span data-stu-id="a2268-172">For example, applying a resource lock tooa web site requires a type with four segments.</span></span> <span data-ttu-id="a2268-173">Portanto, o nome de saudação é três segmentos:</span><span class="sxs-lookup"><span data-stu-id="a2268-173">Therefore, hello name is three segments:</span></span>

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- <span data-ttu-id="a2268-174">O índice de cópia não é esperado</span><span class="sxs-lookup"><span data-stu-id="a2268-174">Copy index is not expected</span></span>

   <span data-ttu-id="a2268-175">Você encontrar isso **InvalidTemplate** erro quando você aplicou Olá **cópia** parte de tooa do elemento do modelo de saudação que não oferece suporte a esse elemento.</span><span class="sxs-lookup"><span data-stu-id="a2268-175">You encounter this **InvalidTemplate** error when you have applied hello **copy** element tooa part of hello template that does not support this element.</span></span> <span data-ttu-id="a2268-176">Só é possível aplicar o tipo de recurso do hello cópia elemento tooa.</span><span class="sxs-lookup"><span data-stu-id="a2268-176">You can only apply hello copy element tooa resource type.</span></span> <span data-ttu-id="a2268-177">Não é possível aplicar cópia tooa propriedade dentro de um tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="a2268-177">You cannot apply copy tooa property within a resource type.</span></span> <span data-ttu-id="a2268-178">Por exemplo, você aplicar cópia tooa virtual machine, mas você não pode aplicar toohello OS discos para uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a2268-178">For example, you apply copy tooa virtual machine, but you cannot apply it toohello OS disks for a virtual machine.</span></span> <span data-ttu-id="a2268-179">Em alguns casos, você pode converter um filho toocreate de recursos pai do recurso tooa um loop de cópia.</span><span class="sxs-lookup"><span data-stu-id="a2268-179">In some cases, you can convert a child resource tooa parent resource toocreate a copy loop.</span></span> <span data-ttu-id="a2268-180">Para obter mais informações sobre como usar a cópia, consulte [Criar várias instâncias de recursos no Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="a2268-180">For more information about using copy, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

- <span data-ttu-id="a2268-181">O parâmetro não é válido</span><span class="sxs-lookup"><span data-stu-id="a2268-181">Parameter is not valid</span></span>

   <span data-ttu-id="a2268-182">Se o modelo Olá Especifica os valores permitidos para um parâmetro, e você fornecer um valor que não é um desses valores, você receberá um toohello semelhante de mensagem erro a seguir:</span><span class="sxs-lookup"><span data-stu-id="a2268-182">If hello template specifies permitted values for a parameter, and you provide a value that is not one of those values, you receive a message similar toohello following error:</span></span>

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'hello provided value {parameter value}
  for hello template parameter {parameter name} is not valid. hello parameter value is not
  part of hello allowed values
  ``` 

   <span data-ttu-id="a2268-183">Olá verifique valores permitidos no modelo de saudação e fornecê-lo durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="a2268-183">Double check hello allowed values in hello template, and provide one during deployment.</span></span>

- <span data-ttu-id="a2268-184">Dependência circular detectada</span><span class="sxs-lookup"><span data-stu-id="a2268-184">Circular dependency detected</span></span>

   <span data-ttu-id="a2268-185">Você recebe esse erro quando recursos dependem uns aos outros de forma que impede a implantação de saudação de iniciar.</span><span class="sxs-lookup"><span data-stu-id="a2268-185">You receive this error when resources depend on each other in a way that prevents hello deployment from starting.</span></span> <span data-ttu-id="a2268-186">Uma combinação de interdependências faz com que dois ou mais recursos aguardar para outros recursos que também estão aguardando.</span><span class="sxs-lookup"><span data-stu-id="a2268-186">A combination of interdependencies makes two or more resource wait for other resources that are also waiting.</span></span> <span data-ttu-id="a2268-187">Por exemplo, recurso1 depende resource3 resource2 depende recurso1 e resource3 depende resource2.</span><span class="sxs-lookup"><span data-stu-id="a2268-187">For example, resource1 depends on resource3, resource2 depends on resource1, and resource3 depends on resource2.</span></span> <span data-ttu-id="a2268-188">Geralmente você pode resolver esse problema removendo dependências desnecessárias.</span><span class="sxs-lookup"><span data-stu-id="a2268-188">You can usually solve this problem by removing unnecessary dependencies.</span></span> 

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a><span data-ttu-id="a2268-189">NotFound e ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="a2268-189">NotFound and ResourceNotFound</span></span>
<span data-ttu-id="a2268-190">Quando o modelo inclui nome de saudação de um recurso que não pode ser resolvido, você recebe um erro semelhante a:</span><span class="sxs-lookup"><span data-stu-id="a2268-190">When your template includes hello name of a resource that cannot be resolved, you receive an error similar to:</span></span>

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

<span data-ttu-id="a2268-191">Se você estiver tentando Olá toodeploy recurso no modelo de saudação ausente, verifique se é necessário tooadd uma dependência.</span><span class="sxs-lookup"><span data-stu-id="a2268-191">If you are attempting toodeploy hello missing resource in hello template, check whether you need tooadd a dependency.</span></span> <span data-ttu-id="a2268-192">O Gerenciador de Recursos otimiza a implantação criando recursos em paralelo, quando possível.</span><span class="sxs-lookup"><span data-stu-id="a2268-192">Resource Manager optimizes deployment by creating resources in parallel, when possible.</span></span> <span data-ttu-id="a2268-193">Se um recurso deve ser implantado após outro recurso, você precisa Olá toouse **dependsOn** toocreate seu modelo uma dependência no elemento Olá outro recurso.</span><span class="sxs-lookup"><span data-stu-id="a2268-193">If one resource must be deployed after another resource, you need toouse hello **dependsOn** element in your template toocreate a dependency on hello other resource.</span></span> <span data-ttu-id="a2268-194">Por exemplo, ao implantar um aplicativo web, Olá plano de serviço de aplicativo deve existir.</span><span class="sxs-lookup"><span data-stu-id="a2268-194">For example, when deploying a web app, hello App Service plan must exist.</span></span> <span data-ttu-id="a2268-195">Se você não especificou que o aplicativo web hello depende Olá plano de serviço de aplicativo, o Gerenciador de recursos cria os recursos no hello simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="a2268-195">If you have not specified that hello web app depends on hello App Service plan, Resource Manager creates both resources at hello same time.</span></span> <span data-ttu-id="a2268-196">Você recebe um erro informando que Olá não é possível encontrar o recurso de plano de serviço de aplicativo, porque ele ainda não existir durante a tentativa de tooset uma propriedade no aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="a2268-196">You receive an error stating that hello App Service plan resource cannot be found, because it does not exist yet when attempting tooset a property on hello web app.</span></span> <span data-ttu-id="a2268-197">Evitar esse erro, definindo a dependência de saudação no aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="a2268-197">You prevent this error by setting hello dependency in hello web app.</span></span>

```json
{
  "apiVersion": "2015-08-01",
  "type": "Microsoft.Web/sites",
  "dependsOn": [
    "[variables('hostingPlanName')]"
  ],
  ...
}
```

<span data-ttu-id="a2268-198">Para obter sugestões sobre como solucionar erros de dependência, veja [Verificar a sequência de implantação](#check-deployment-sequence).</span><span class="sxs-lookup"><span data-stu-id="a2268-198">For suggestions on troubleshooting dependency errors, see [Check deployment sequence](#check-deployment-sequence).</span></span>

<span data-ttu-id="a2268-199">Você também ver esse erro quando recursos Olá existe em outro grupo de recursos que Olá um sendo implantado.</span><span class="sxs-lookup"><span data-stu-id="a2268-199">You also see this error when hello resource exists in a different resource group than hello one being deployed to.</span></span> <span data-ttu-id="a2268-200">Nesse caso, use Olá [função resourceId](resource-group-template-functions-resource.md#resourceid) tooget nome totalmente qualificado do hello do recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="a2268-200">In that case, use hello [resourceId function](resource-group-template-functions-resource.md#resourceid) tooget hello fully qualified name of hello resource.</span></span>

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

<span data-ttu-id="a2268-201">Se você tentar Olá toouse [referência](resource-group-template-functions-resource.md#reference) ou [listkeys do](resource-group-template-functions-resource.md#listkeys) funções com um recurso que não pode ser resolvida, você receberá Olá erro a seguir:</span><span class="sxs-lookup"><span data-stu-id="a2268-201">If you attempt toouse hello [reference](resource-group-template-functions-resource.md#reference) or [listKeys](resource-group-template-functions-resource.md#listkeys) functions with a resource that cannot be resolved, you receive hello following error:</span></span>

```
Code=ResourceNotFound;
Message=hello Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

<span data-ttu-id="a2268-202">Procure por uma expressão que inclui Olá **referência** função.</span><span class="sxs-lookup"><span data-stu-id="a2268-202">Look for an expression that includes hello **reference** function.</span></span> <span data-ttu-id="a2268-203">Verifique se os valores de parâmetro hello estão corretos.</span><span class="sxs-lookup"><span data-stu-id="a2268-203">Double check that hello parameter values are correct.</span></span>

## <a name="parentresourcenotfound"></a><span data-ttu-id="a2268-204">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="a2268-204">ParentResourceNotFound</span></span>

<span data-ttu-id="a2268-205">Quando um recurso é um recurso de tooanother do pai, recurso pai de saudação deve existir antes de criar o recurso de filho hello.</span><span class="sxs-lookup"><span data-stu-id="a2268-205">When one resource is a parent tooanother resource, hello parent resource must exist before creating hello child resource.</span></span> <span data-ttu-id="a2268-206">Se ele ainda não existir, você receberá Olá erro a seguir:</span><span class="sxs-lookup"><span data-stu-id="a2268-206">If it does not yet exist, you receive hello following error:</span></span>

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

<span data-ttu-id="a2268-207">nome de saudação do recurso de filho Olá inclui nome de pai de hello.</span><span class="sxs-lookup"><span data-stu-id="a2268-207">hello name of hello child resource includes hello parent name.</span></span> <span data-ttu-id="a2268-208">Por exemplo, um Banco de Dados SQL pode ser definido como:</span><span class="sxs-lookup"><span data-stu-id="a2268-208">For example, a SQL Database might be defined as:</span></span>

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

<span data-ttu-id="a2268-209">Mas, se você não especificar uma dependência no recurso pai, Olá, recurso filho de saudação pode obter implantado antes do pai de saudação.</span><span class="sxs-lookup"><span data-stu-id="a2268-209">But, if you do not specify a dependency on hello parent resource, hello child resource may get deployed before hello parent.</span></span> <span data-ttu-id="a2268-210">tooresolve esse erro incluem uma dependência.</span><span class="sxs-lookup"><span data-stu-id="a2268-210">tooresolve this error, include a dependency.</span></span>

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />

## <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a><span data-ttu-id="a2268-211">StorageAccountAlreadyExists e StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="a2268-211">StorageAccountAlreadyExists and StorageAccountAlreadyTaken</span></span>
<span data-ttu-id="a2268-212">Para contas de armazenamento, você deve fornecer um nome para o recurso de saudação que é exclusivo no Azure.</span><span class="sxs-lookup"><span data-stu-id="a2268-212">For storage accounts, you must provide a name for hello resource that is unique across Azure.</span></span> <span data-ttu-id="a2268-213">Se você não fornecer um nome exclusivo, receberá um erro como:</span><span class="sxs-lookup"><span data-stu-id="a2268-213">If you do not provide a unique name, you receive an error like:</span></span>

```
Code=StorageAccountAlreadyTaken
Message=hello storage account named mystorage is already taken.
```

<span data-ttu-id="a2268-214">Você pode criar um nome exclusivo, concatenando a convenção de nomenclatura com resultado Olá Olá [uniqueString](resource-group-template-functions-string.md#uniquestring) função.</span><span class="sxs-lookup"><span data-stu-id="a2268-214">You can create a unique name by concatenating your naming convention with hello result of hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span>

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

<span data-ttu-id="a2268-215">Se você implantar uma conta de armazenamento com hello o mesmo nome como uma conta de armazenamento existente na sua assinatura, mas fornecem um local diferente, você receberá um erro indicando que conta de armazenamento Olá já existe em um local diferente.</span><span class="sxs-lookup"><span data-stu-id="a2268-215">If you deploy a storage account with hello same name as an existing storage account in your subscription, but provide a different location, you receive an error indicating hello storage account already exists in a different location.</span></span> <span data-ttu-id="a2268-216">Exclua a conta de armazenamento existente hello ou fornecer Olá mesmo local como Olá conta de armazenamento existente.</span><span class="sxs-lookup"><span data-stu-id="a2268-216">Either delete hello existing storage account, or provide hello same location as hello existing storage account.</span></span>

## <a name="accountnameinvalid"></a><span data-ttu-id="a2268-217">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="a2268-217">AccountNameInvalid</span></span>
<span data-ttu-id="a2268-218">Consulte Olá **AccountNameInvalid** erro ao tentar toogive um armazenamento de conta um nome que contenha caracteres proibidos.</span><span class="sxs-lookup"><span data-stu-id="a2268-218">You see hello **AccountNameInvalid** error when attempting toogive a storage account a name that includes prohibited characters.</span></span> <span data-ttu-id="a2268-219">Os nomes da conta de armazenamento devem ter entre 3 e 24 caracteres, usar números e apenas letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="a2268-219">Storage account names must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span> <span data-ttu-id="a2268-220">Olá [uniqueString](resource-group-template-functions-string.md#uniquestring) função retorna 13 caracteres.</span><span class="sxs-lookup"><span data-stu-id="a2268-220">hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function returns 13 characters.</span></span> <span data-ttu-id="a2268-221">Se você concatenar um prefixo toohello **uniqueString** resultados, forneça um prefixo de 11 caracteres ou menos.</span><span class="sxs-lookup"><span data-stu-id="a2268-221">If you concatenate a prefix toohello **uniqueString** result, provide a prefix that is 11 characters or less.</span></span>

## <a name="badrequest"></a><span data-ttu-id="a2268-222">BadRequest</span><span class="sxs-lookup"><span data-stu-id="a2268-222">BadRequest</span></span>

<span data-ttu-id="a2268-223">Você pode receber um status BadRequest ao fornecer um valor inválido para uma propriedade.</span><span class="sxs-lookup"><span data-stu-id="a2268-223">You may encounter a BadRequest status when you provide an invalid value for a property.</span></span> <span data-ttu-id="a2268-224">Por exemplo, se você fornecer um valor incorreto do SKU para uma conta de armazenamento, implantação de saudação falhará.</span><span class="sxs-lookup"><span data-stu-id="a2268-224">For example, if you provide an incorrect SKU value for a storage account, hello deployment fails.</span></span> <span data-ttu-id="a2268-225">os valores válidos para a propriedade, toodetermine examinar Olá [API REST](/rest/api) para tipo de recurso Olá você está implantando.</span><span class="sxs-lookup"><span data-stu-id="a2268-225">toodetermine valid values for property, look at hello [REST API](/rest/api) for hello resource type you are deploying.</span></span>

<a id="noregisteredproviderfound" />

## <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a><span data-ttu-id="a2268-226">NoRegisteredProviderFound e MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="a2268-226">NoRegisteredProviderFound and MissingSubscriptionRegistration</span></span>
<span data-ttu-id="a2268-227">Durante a implantação de recursos, você pode receber Olá após o código de erro e mensagem:</span><span class="sxs-lookup"><span data-stu-id="a2268-227">When deploying resource, you may receive hello following error code and message:</span></span>

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

<span data-ttu-id="a2268-228">Ou você poderá receber uma mensagem semelhante que indica:</span><span class="sxs-lookup"><span data-stu-id="a2268-228">Or, you may receive a similar message that states:</span></span>

```
Code: MissingSubscriptionRegistration
Message: hello subscription is not registered toouse namespace {resource-provider-namespace}
```

<span data-ttu-id="a2268-229">Você recebe esses erros por um dos três motivos:</span><span class="sxs-lookup"><span data-stu-id="a2268-229">You receive these errors for one of three reasons:</span></span>

1. <span data-ttu-id="a2268-230">provedor de recursos de saudação não foi registrado para sua assinatura</span><span class="sxs-lookup"><span data-stu-id="a2268-230">hello resource provider has not been registered for your subscription</span></span>
2. <span data-ttu-id="a2268-231">Versão de API não tem suportada para o tipo de recurso Olá</span><span class="sxs-lookup"><span data-stu-id="a2268-231">API version not supported for hello resource type</span></span>
3. <span data-ttu-id="a2268-232">Local não tem suportada para o tipo de recurso Olá</span><span class="sxs-lookup"><span data-stu-id="a2268-232">Location not supported for hello resource type</span></span>

<span data-ttu-id="a2268-233">mensagem de erro de saudação deve fornecer sugestões para locais de saudação com suporte e as versões de API.</span><span class="sxs-lookup"><span data-stu-id="a2268-233">hello error message should give you suggestions for hello supported locations and API versions.</span></span> <span data-ttu-id="a2268-234">Você pode alterar sua tooone do modelo de saudação valores sugeridos.</span><span class="sxs-lookup"><span data-stu-id="a2268-234">You can change your template tooone of hello suggested values.</span></span> <span data-ttu-id="a2268-235">A maioria dos provedores são registradas automaticamente pelo Olá interface de linha de comando de portal ou hello Azure você está usando, mas não todas.</span><span class="sxs-lookup"><span data-stu-id="a2268-235">Most providers are registered automatically by hello Azure portal or hello command-line interface you are using, but not all.</span></span> <span data-ttu-id="a2268-236">Se você não tiver usado um provedor de recursos específico antes, talvez seja necessário tooregister esse provedor.</span><span class="sxs-lookup"><span data-stu-id="a2268-236">If you have not used a particular resource provider before, you may need tooregister that provider.</span></span> <span data-ttu-id="a2268-237">Você pode descobrir mais sobre provedores de recursos por meio do PowerShell ou CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="a2268-237">You can discover more about resource providers through PowerShell or Azure CLI.</span></span>

<span data-ttu-id="a2268-238">**Portal**</span><span class="sxs-lookup"><span data-stu-id="a2268-238">**Portal**</span></span>

<span data-ttu-id="a2268-239">Você pode ver o status de registro hello e registrar um namespace de provedor de recursos por meio do portal hello.</span><span class="sxs-lookup"><span data-stu-id="a2268-239">You can see hello registration status and register a resource provider namespace through hello portal.</span></span>

1. <span data-ttu-id="a2268-240">Em sua assinatura, selecione **Provedores de recursos**.</span><span class="sxs-lookup"><span data-stu-id="a2268-240">For your subscription, select **Resource providers**.</span></span>

   ![selecionar provedores de recursos](./media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. <span data-ttu-id="a2268-242">Examinar a lista de saudação de provedores de recursos e, se necessário, selecione Olá **registrar** provedor de recursos do link tooregister saudação do tipo hello tentar toodeploy.</span><span class="sxs-lookup"><span data-stu-id="a2268-242">Look at hello list of resource providers, and if necessary, select hello **Register** link tooregister hello resource provider of hello type you are trying toodeploy.</span></span>

   ![listar provedores de recursos](./media/resource-manager-common-deployment-errors/list-resource-providers.png)

<span data-ttu-id="a2268-244">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="a2268-244">**PowerShell**</span></span>

<span data-ttu-id="a2268-245">toosee o status do registro, use **Get-AzureRmResourceProvider**.</span><span class="sxs-lookup"><span data-stu-id="a2268-245">toosee your registration status, use **Get-AzureRmResourceProvider**.</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

<span data-ttu-id="a2268-246">tooregister um provedor, use **AzureRmResourceProvider registro** e forneça o nome de saudação do provedor de recursos de saudação desejar tooregister.</span><span class="sxs-lookup"><span data-stu-id="a2268-246">tooregister a provider, use **Register-AzureRmResourceProvider** and provide hello name of hello resource provider you wish tooregister.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

<span data-ttu-id="a2268-247">locais de saudação suporte tooget para um determinado tipo de recurso, use:</span><span class="sxs-lookup"><span data-stu-id="a2268-247">tooget hello supported locations for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="a2268-248">Olá tooget versões de API com suporte para um determinado tipo de recurso, use:</span><span class="sxs-lookup"><span data-stu-id="a2268-248">tooget hello supported API versions for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

<span data-ttu-id="a2268-249">**CLI do Azure**</span><span class="sxs-lookup"><span data-stu-id="a2268-249">**Azure CLI**</span></span>

<span data-ttu-id="a2268-250">toosee se Olá provedor está registrado, use Olá `azure provider list` comando.</span><span class="sxs-lookup"><span data-stu-id="a2268-250">toosee whether hello provider is registered, use hello `azure provider list` command.</span></span>

```azurecli
az provider list
```

<span data-ttu-id="a2268-251">tooregister um provedor de recursos, use Olá `azure provider register` de comando e especificar Olá *namespace* tooregister.</span><span class="sxs-lookup"><span data-stu-id="a2268-251">tooregister a resource provider, use hello `azure provider register` command, and specify hello *namespace* tooregister.</span></span>

```azurecli
az provider register --namespace Microsoft.Cdn
```

<span data-ttu-id="a2268-252">locais de saudação suporte toosee e as versões de API para um tipo de recurso, use:</span><span class="sxs-lookup"><span data-stu-id="a2268-252">toosee hello supported locations and API versions for a resource type, use:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />

## <a name="quotaexceeded-and-operationnotallowed"></a><span data-ttu-id="a2268-253">QuotaExceeded e OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="a2268-253">QuotaExceeded and OperationNotAllowed</span></span>
<span data-ttu-id="a2268-254">Você pode ter problemas quando a implantação ultrapassar uma cota, que pode ser por grupo de recursos, assinaturas, contas e outros escopos.</span><span class="sxs-lookup"><span data-stu-id="a2268-254">You might have issues when deployment exceeds a quota, which could be per resource group, subscriptions, accounts, and other scopes.</span></span> <span data-ttu-id="a2268-255">Por exemplo, sua assinatura pode ser configurada toolimit Olá número de núcleos de uma região.</span><span class="sxs-lookup"><span data-stu-id="a2268-255">For example, your subscription may be configured toolimit hello number of cores for a region.</span></span> <span data-ttu-id="a2268-256">Se você tentar toodeploy uma máquina virtual com mais núcleos do que Olá permitido valor, você receber um erro informando a saudação cota foi excedida.</span><span class="sxs-lookup"><span data-stu-id="a2268-256">If you attempt toodeploy a virtual machine with more cores than hello permitted amount, you receive an error stating hello quota has been exceeded.</span></span>
<span data-ttu-id="a2268-257">Para obter informações completas sobre cotas, consulte [Limites, cotas e restrições de serviço e assinatura do Azure](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="a2268-257">For complete quota information, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="a2268-258">tooexamine cotas de sua assinatura para núcleos, você pode usar o hello `azure vm list-usage` do hello CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="a2268-258">tooexamine your subscription's quotas for cores, you can use hello `azure vm list-usage` command in hello Azure CLI.</span></span> <span data-ttu-id="a2268-259">saudação de exemplo a seguir ilustra essa cota de núcleo Olá para uma conta de avaliação gratuita é 4:</span><span class="sxs-lookup"><span data-stu-id="a2268-259">hello following example illustrates that hello core quota for a free trial account is 4:</span></span>

```azurecli
az vm list-usage --location "South Central US"
```

<span data-ttu-id="a2268-260">Que retorna:</span><span class="sxs-lookup"><span data-stu-id="a2268-260">Which returns:</span></span>

```azurecli
[
  {
    "currentValue": 0,
    "limit": 2000,
    "name": {
      "localizedValue": "Availability Sets",
      "value": "availabilitySets"
    }
  },
  ...
]
```

<span data-ttu-id="a2268-261">Se você implantar um modelo que cria mais de quatro núcleos na região Oeste dos EUA de Olá, você receberá um erro de implantação que se parece com:</span><span class="sxs-lookup"><span data-stu-id="a2268-261">If you deploy a template that creates more than four cores in hello West US region, you get a deployment error that looks like:</span></span>

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

<span data-ttu-id="a2268-262">Ou no PowerShell, você pode usar o hello **AzureRmVMUsage Get** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a2268-262">Or in PowerShell, you can use hello **Get-AzureRmVMUsage** cmdlet.</span></span>

```powershell
Get-AzureRmVMUsage
```

<span data-ttu-id="a2268-263">Que retorna:</span><span class="sxs-lookup"><span data-stu-id="a2268-263">Which returns:</span></span>

```powershell
...
CurrentValue : 0
Limit        : 4
Name         : {
                 "value": "cores",
                 "localizedValue": "Total Regional Cores"
               }
Unit         : null
...
```

<span data-ttu-id="a2268-264">Nesses casos, você deve ir toohello portal e a cota de região Olá no qual você deseja toodeploy um tooraise do problema de suporte do arquivo.</span><span class="sxs-lookup"><span data-stu-id="a2268-264">In these cases, you should go toohello portal and file a support issue tooraise your quota for hello region into which you want toodeploy.</span></span>

> [!NOTE]
> <span data-ttu-id="a2268-265">Lembre-se de que grupos de recursos, cota Olá para cada região, não para a assinatura inteira hello.</span><span class="sxs-lookup"><span data-stu-id="a2268-265">Remember that for resource groups, hello quota is for each individual region, not for hello entire subscription.</span></span> <span data-ttu-id="a2268-266">Se você precisar de núcleos de 30 toodeploy no Oeste dos EUA, você terá tooask para 30 núcleos do Gerenciador de recursos no Oeste dos EUA.</span><span class="sxs-lookup"><span data-stu-id="a2268-266">If you need toodeploy 30 cores in West US, you have tooask for 30 Resource Manager cores in West US.</span></span> <span data-ttu-id="a2268-267">Se você precisar de núcleos de 30 toodeploy em qualquer Olá regiões toowhich você tem acesso, você deve pedir 30 núcleos do Gerenciador de recursos em todas as regiões.</span><span class="sxs-lookup"><span data-stu-id="a2268-267">If you need toodeploy 30 cores in any of hello regions toowhich you have access, you should ask for 30 Resource Manager cores in all regions.</span></span>
>
>

## <a name="invalidcontentlink"></a><span data-ttu-id="a2268-268">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="a2268-268">InvalidContentLink</span></span>
<span data-ttu-id="a2268-269">Quando você receber a mensagem de saudação do erro:</span><span class="sxs-lookup"><span data-stu-id="a2268-269">When you receive hello error message:</span></span>

```
Code=InvalidContentLink
Message=Unable toodownload deployment content from ...
```

<span data-ttu-id="a2268-270">Você tentou provavelmente toolink tooa modelo aninhado que não está disponível.</span><span class="sxs-lookup"><span data-stu-id="a2268-270">You have most likely attempted toolink tooa nested template that is not available.</span></span> <span data-ttu-id="a2268-271">Verifique hello URI fornecido para o modelo aninhado hello.</span><span class="sxs-lookup"><span data-stu-id="a2268-271">Double check hello URI you provided for hello nested template.</span></span> <span data-ttu-id="a2268-272">Se o modelo de saudação existir em uma conta de armazenamento, certifique-se de Olá URI está acessível.</span><span class="sxs-lookup"><span data-stu-id="a2268-272">If hello template exists in a storage account, make sure hello URI is accessible.</span></span> <span data-ttu-id="a2268-273">Talvez seja necessário toopass um token SAS.</span><span class="sxs-lookup"><span data-stu-id="a2268-273">You may need toopass a SAS token.</span></span> <span data-ttu-id="a2268-274">Para saber mais, confira [Usando modelos vinculados com o Gerenciador de Recursos do Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a2268-274">For more information, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="requestdisallowedbypolicy"></a><span data-ttu-id="a2268-275">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="a2268-275">RequestDisallowedByPolicy</span></span>
<span data-ttu-id="a2268-276">Você recebe esse erro quando sua assinatura inclui uma política de recurso que impede que uma ação que você está tentando tooperform durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="a2268-276">You receive this error when your subscription includes a resource policy that prevents an action you are trying tooperform during deployment.</span></span> <span data-ttu-id="a2268-277">Na mensagem de erro hello, procure o identificador de política de saudação.</span><span class="sxs-lookup"><span data-stu-id="a2268-277">In hello error message, look for hello policy identifier.</span></span>

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

<span data-ttu-id="a2268-278">Em **PowerShell**, forneça esse identificador de política como Olá **Id** detalhes do parâmetro tooretrieve sobre a política de saudação que bloqueou a sua implantação.</span><span class="sxs-lookup"><span data-stu-id="a2268-278">In **PowerShell**, provide that policy identifier as hello **Id** parameter tooretrieve details about hello policy that blocked your deployment.</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

<span data-ttu-id="a2268-279">Em **CLI do Azure**, forneça o nome de saudação da definição de política de saudação:</span><span class="sxs-lookup"><span data-stu-id="a2268-279">In **Azure CLI**, provide hello name of hello policy definition:</span></span>

```azurecli
az policy definition show --name regionPolicyAssignment
```

<span data-ttu-id="a2268-280">Para obter mais informações, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="a2268-280">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="a2268-281">Erro RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="a2268-281">RequestDisallowedByPolicy error</span></span>](resource-manager-policy-requestdisallowedbypolicy-error.md)
- <span data-ttu-id="a2268-282">[Usar os recursos de toomanage de política e controlar o acesso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="a2268-282">[Use Policy toomanage resources and control access](resource-manager-policy.md).</span></span>

## <a name="authorization-failed"></a><span data-ttu-id="a2268-283">Falha na autorização</span><span class="sxs-lookup"><span data-stu-id="a2268-283">Authorization failed</span></span>
<span data-ttu-id="a2268-284">Você pode receber um erro durante a implantação porque hello conta ou entidade de tentativa de recursos de saudação toodeploy de serviço não tem acesso tooperform essas ações.</span><span class="sxs-lookup"><span data-stu-id="a2268-284">You may receive an error during deployment because hello account or service principal attempting toodeploy hello resources does not have access tooperform those actions.</span></span> <span data-ttu-id="a2268-285">Active Directory do Azure permite que você ou sua toocontrol administrador quais identidades podem acessar os recursos com um alto grau de precisão.</span><span class="sxs-lookup"><span data-stu-id="a2268-285">Azure Active Directory enables you or your administrator toocontrol which identities can access what resources with a great degree of precision.</span></span> <span data-ttu-id="a2268-286">Por exemplo, se sua conta é atribuída a função de leitor toohello, você não é toocreate capaz de recursos.</span><span class="sxs-lookup"><span data-stu-id="a2268-286">For example, if your account is assigned toohello Reader role, you are not able toocreate resources.</span></span> <span data-ttu-id="a2268-287">Nesse caso, você vê uma mensagem de erro indicando que houve falha na autorização.</span><span class="sxs-lookup"><span data-stu-id="a2268-287">In that case, you see an error message indicating that authorization failed.</span></span>

<span data-ttu-id="a2268-288">Para obter mais informações sobre o controle de acesso baseado em funções, consulte [Controle de Acesso Baseado em Funções do Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="a2268-288">For more information about role-based access control, see [Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="a2268-289">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a2268-289">Next steps</span></span>
* <span data-ttu-id="a2268-290">toolearn sobre a auditoria de ações, consulte [operações com o Gerenciador de recursos de auditoria](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="a2268-290">toolearn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="a2268-291">toolearn sobre erros de saudação toodetermine ações durante a implantação, consulte [Exibir operações de implantação](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="a2268-291">toolearn about actions toodetermine hello errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
