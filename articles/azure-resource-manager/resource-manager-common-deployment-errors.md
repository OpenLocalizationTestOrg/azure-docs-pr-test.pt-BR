---
title: "Solução de erros comuns de implantação do Azure | Microsoft Docs"
description: Descreve como resolver erros comuns ao implantar recursos no Azure usando o Azure Resource Manager.
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "erro de implantação, implantação do azure, implante no azure"
ms.assetid: c002a9be-4de5-4963-bd14-b54aa3d8fa59
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: tomfitz
ms.openlocfilehash: 30adc10d01290f14a3e116813b19916fa36ab0bc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a><span data-ttu-id="a01bf-104">Solução de erros comuns de implantação do Azure com o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a01bf-104">Troubleshoot common Azure deployment errors with Azure Resource Manager</span></span>
<span data-ttu-id="a01bf-105">Este tópico descreve como é possível resolver alguns erros de implantação comuns do Azure que você pode encontrar.</span><span class="sxs-lookup"><span data-stu-id="a01bf-105">This topic describes how you can resolve some common Azure deployment errors you may encounter.</span></span>

<span data-ttu-id="a01bf-106">Os seguintes códigos de erro estão descritos neste tópico:</span><span class="sxs-lookup"><span data-stu-id="a01bf-106">The following error codes are described in this topic:</span></span>

* [<span data-ttu-id="a01bf-107">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="a01bf-107">AccountNameInvalid</span></span>](#accountnameinvalid)
* [<span data-ttu-id="a01bf-108">Falha na autorização</span><span class="sxs-lookup"><span data-stu-id="a01bf-108">Authorization failed</span></span>](#authorization-failed)
* [<span data-ttu-id="a01bf-109">BadRequest</span><span class="sxs-lookup"><span data-stu-id="a01bf-109">BadRequest</span></span>](#badrequest)
* [<span data-ttu-id="a01bf-110">DeploymentFailed</span><span class="sxs-lookup"><span data-stu-id="a01bf-110">DeploymentFailed</span></span>](#deploymentfailed)
* [<span data-ttu-id="a01bf-111">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="a01bf-111">DisallowedOperation</span></span>](#disallowedoperation)
* [<span data-ttu-id="a01bf-112">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="a01bf-112">InvalidContentLink</span></span>](#invalidcontentlink)
* [<span data-ttu-id="a01bf-113">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="a01bf-113">InvalidTemplate</span></span>](#invalidtemplate)
* [<span data-ttu-id="a01bf-114">MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="a01bf-114">MissingSubscriptionRegistration</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="a01bf-115">NotFound</span><span class="sxs-lookup"><span data-stu-id="a01bf-115">NotFound</span></span>](#notfound)
* [<span data-ttu-id="a01bf-116">NoRegisteredProviderFound</span><span class="sxs-lookup"><span data-stu-id="a01bf-116">NoRegisteredProviderFound</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="a01bf-117">OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="a01bf-117">OperationNotAllowed</span></span>](#quotaexceeded)
* [<span data-ttu-id="a01bf-118">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="a01bf-118">ParentResourceNotFound</span></span>](#parentresourcenotfound)
* [<span data-ttu-id="a01bf-119">QuotaExceeded</span><span class="sxs-lookup"><span data-stu-id="a01bf-119">QuotaExceeded</span></span>](#quotaexceeded)
* [<span data-ttu-id="a01bf-120">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="a01bf-120">RequestDisallowedByPolicy</span></span>](#requestdisallowedbypolicy)
* [<span data-ttu-id="a01bf-121">ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="a01bf-121">ResourceNotFound</span></span>](#notfound)
* [<span data-ttu-id="a01bf-122">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="a01bf-122">SkuNotAvailable</span></span>](#skunotavailable)
* [<span data-ttu-id="a01bf-123">StorageAccountAlreadyExists</span><span class="sxs-lookup"><span data-stu-id="a01bf-123">StorageAccountAlreadyExists</span></span>](#storagenamenotunique)
* [<span data-ttu-id="a01bf-124">StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="a01bf-124">StorageAccountAlreadyTaken</span></span>](#storagenamenotunique)

## <a name="deploymentfailed"></a><span data-ttu-id="a01bf-125">DeploymentFailed</span><span class="sxs-lookup"><span data-stu-id="a01bf-125">DeploymentFailed</span></span>

<span data-ttu-id="a01bf-126">Esse código de erro indica um erro de implantação geral, mas não é o código de erro que você precisa para começar a solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="a01bf-126">This error code indicates a general deployment error, but it is not the error code you need to start troubleshooting.</span></span> <span data-ttu-id="a01bf-127">O código de erro que o ajuda a resolver o problema de verdade fica um nível abaixo desse erro.</span><span class="sxs-lookup"><span data-stu-id="a01bf-127">The error code that actually helps you resolve the issue is usually one level below this error.</span></span> <span data-ttu-id="a01bf-128">Por exemplo, a imagem a seguir mostra o código de erro **RequestDisallowedByPolicy** que está por baixo do erro de implantação.</span><span class="sxs-lookup"><span data-stu-id="a01bf-128">For example, the following image shows the **RequestDisallowedByPolicy** error code that is under the deployment error.</span></span>

![mostrar código de erro](./media/resource-manager-common-deployment-errors/error-code.png)

## <a name="skunotavailable"></a><span data-ttu-id="a01bf-130">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="a01bf-130">SkuNotAvailable</span></span>

<span data-ttu-id="a01bf-131">Ao implantar um recurso (normalmente uma máquina virtual), você pode receber o seguinte código de erro e a mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="a01bf-131">When deploying a resource (typically a virtual machine), you may receive the following error code and error message:</span></span>

```
Code: SkuNotAvailable
Message: The requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy to a different location.
```

<span data-ttu-id="a01bf-132">Você recebe esse erro quando o recurso SKU selecionado (como o tamanho da VM) não está disponível para o local escolhido.</span><span class="sxs-lookup"><span data-stu-id="a01bf-132">You receive this error when the resource SKU you have selected (such as VM size) is not available for the location you have selected.</span></span> <span data-ttu-id="a01bf-133">Para resolver esse problema, você precisa determinar quais SKUs estão disponíveis em uma região.</span><span class="sxs-lookup"><span data-stu-id="a01bf-133">To resolve this issue, you need to determine which SKUs are available in a region.</span></span> <span data-ttu-id="a01bf-134">Você pode usar o PowerShell, o portal ou uma operação REST para localizar SKUs disponíveis.</span><span class="sxs-lookup"><span data-stu-id="a01bf-134">You can use PowerShell, the portal, or a REST operation to find available SKUs.</span></span>

- <span data-ttu-id="a01bf-135">Para o PowerShell, use [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) e filtre por localização.</span><span class="sxs-lookup"><span data-stu-id="a01bf-135">For PowerShell, use [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) and filter by location.</span></span> <span data-ttu-id="a01bf-136">Você deve ter a versão mais recente do PowerShell para esse comando.</span><span class="sxs-lookup"><span data-stu-id="a01bf-136">You must have the latest version of PowerShell for this command.</span></span>

  ```powershell
  Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
  ```

  <span data-ttu-id="a01bf-137">Os resultados incluem uma lista de SKUs para o local e as restrições desse SKU.</span><span class="sxs-lookup"><span data-stu-id="a01bf-137">The results include a list of SKUs for the location and any restrictions for that SKU.</span></span>

  ```powershell
  ResourceType                Name      Locations Restriction                      Capability Value
  ------------                ----      --------- -----------                      ---------- -----
  availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
  availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
  virtualMachines      Standard_A0 southcentralus
  virtualMachines      Standard_A1 southcentralus
  virtualMachines      Standard_A2 southcentralus
  ```

- <span data-ttu-id="a01bf-138">Para usar o [portal](https://portal.azure.com), faça logon no portal e adicionar um recurso por meio da interface.</span><span class="sxs-lookup"><span data-stu-id="a01bf-138">To use the [portal](https://portal.azure.com), log in to the portal and add a resource through the interface.</span></span> <span data-ttu-id="a01bf-139">Ao definir os valores, verá os SKUs disponíveis para esse recurso.</span><span class="sxs-lookup"><span data-stu-id="a01bf-139">As you set the values, you see the available SKUs for that resource.</span></span> <span data-ttu-id="a01bf-140">Não é necessário concluir a implantação.</span><span class="sxs-lookup"><span data-stu-id="a01bf-140">You do not need to complete the deployment.</span></span>

    ![SKUs disponíveis](./media/resource-manager-common-deployment-errors/view-sku.png)

- <span data-ttu-id="a01bf-142">Para usar a API REST para máquinas virtuais, envie a solicitação a seguir:</span><span class="sxs-lookup"><span data-stu-id="a01bf-142">To use the REST API for virtual machines, send the following request:</span></span>

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  <span data-ttu-id="a01bf-143">Ele retorna SKUs e regiões disponíveis no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="a01bf-143">It returns available SKUs and regions in the following format:</span></span>

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

<span data-ttu-id="a01bf-144">Caso você não consiga encontrar um SKU adequado na região ou em uma região alternativa que atende às suas necessidades de negócios, envie uma [solicitação de SKU](https://aka.ms/skurestriction) para o Suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="a01bf-144">If you are unable to find a suitable SKU in that region or an alternative region that meets your business needs, submit a [SKU request](https://aka.ms/skurestriction) to Azure Support.</span></span>

## <a name="disallowedoperation"></a><span data-ttu-id="a01bf-145">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="a01bf-145">DisallowedOperation</span></span>

```
Code: DisallowedOperation
Message: The current subscription type is not permitted to perform operations on any provider 
namespace. Please use a different subscription.
```

<span data-ttu-id="a01bf-146">Se você receber esse erro, você estará usando uma assinatura que não tem permissão para acessar nenhum serviço do Azure com a exceção do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a01bf-146">If you receive this error, you are using a subscription that is not permitted to access any Azure services other than Azure Active Directory.</span></span> <span data-ttu-id="a01bf-147">Você pode ter esse tipo de assinatura quando você precisa acessar o portal clássico, mas não tem permissão para implantar recursos.</span><span class="sxs-lookup"><span data-stu-id="a01bf-147">You might have this type of subscription when you need to access the classic portal but are not permitted to deploy resources.</span></span> <span data-ttu-id="a01bf-148">Para resolver esse problema, você deve usar uma assinatura que tenha permissão para implantar recursos.</span><span class="sxs-lookup"><span data-stu-id="a01bf-148">To resolve this issue, you must use a subscription that has permission to deploy resources.</span></span>  

<span data-ttu-id="a01bf-149">Para exibir suas assinaturas disponíveis com o PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="a01bf-149">To view your available subscriptions with PowerShell, use:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="a01bf-150">E para definir a assinatura atual, use:</span><span class="sxs-lookup"><span data-stu-id="a01bf-150">And, to set the current subscription, use:</span></span>

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

<span data-ttu-id="a01bf-151">Para exibir suas assinaturas disponíveis com a CLI do Azure 2.0, use:</span><span class="sxs-lookup"><span data-stu-id="a01bf-151">To view your available subscriptions with Azure CLI 2.0, use:</span></span>

```azurecli
az account list
```

<span data-ttu-id="a01bf-152">E para definir a assinatura atual, use:</span><span class="sxs-lookup"><span data-stu-id="a01bf-152">And, to set the current subscription, use:</span></span>

```azurecli
az account set --subscription {subscription-name}
```

## <a name="invalidtemplate"></a><span data-ttu-id="a01bf-153">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="a01bf-153">InvalidTemplate</span></span>
<span data-ttu-id="a01bf-154">Esse erro pode resultar de vários tipos diferentes de erros.</span><span class="sxs-lookup"><span data-stu-id="a01bf-154">This error can result from several different types of errors.</span></span>

- <span data-ttu-id="a01bf-155">Erro de sintaxe</span><span class="sxs-lookup"><span data-stu-id="a01bf-155">Syntax error</span></span>

   <span data-ttu-id="a01bf-156">Se você receber uma mensagem de erro que indica a validação do modelo falhou, você poderá ter um problema de sintaxe em seu modelo.</span><span class="sxs-lookup"><span data-stu-id="a01bf-156">If you receive an error message that indicates the template failed validation, you may have a syntax problem in your template.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   <span data-ttu-id="a01bf-157">Esse erro é fácil de cometer porque as expressões do modelo podem ser complexas.</span><span class="sxs-lookup"><span data-stu-id="a01bf-157">This error is easy to make because template expressions can be intricate.</span></span> <span data-ttu-id="a01bf-158">Por exemplo, a atribuição de nome a seguir para uma conta de armazenamento contém um par de colchetes, três funções, três pares de parênteses, um par de aspas simples e uma propriedade:</span><span class="sxs-lookup"><span data-stu-id="a01bf-158">For example, the following name assignment for a storage account contains one set of brackets, three functions, three sets of parentheses, one set of single quotes, and one property:</span></span>

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   <span data-ttu-id="a01bf-159">Se você não fornecer a sintaxe correspondente, o modelo produzirá um valor diferente do que era sua intenção.</span><span class="sxs-lookup"><span data-stu-id="a01bf-159">If you do not provide the matching syntax, the template produces a value that is different than your intention.</span></span>

   <span data-ttu-id="a01bf-160">Quando você receber esse tipo de erro, examine cuidadosamente a sintaxe da expressão.</span><span class="sxs-lookup"><span data-stu-id="a01bf-160">When you receive this type of error, carefully review the expression syntax.</span></span> <span data-ttu-id="a01bf-161">Considere usar um editor JSON como o [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) ou o [Visual Studio Code](resource-manager-vs-code.md) que pode avisá-lo sobre os erros de sintaxe.</span><span class="sxs-lookup"><span data-stu-id="a01bf-161">Consider using a JSON editor like [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) or [Visual Studio Code](resource-manager-vs-code.md), which can warn you about syntax errors.</span></span>

- <span data-ttu-id="a01bf-162">Comprimentos de segmento incorretos</span><span class="sxs-lookup"><span data-stu-id="a01bf-162">Incorrect segment lengths</span></span>

   <span data-ttu-id="a01bf-163">Outro erro de modelo inválido ocorre quando o nome do recurso não está no formato correto.</span><span class="sxs-lookup"><span data-stu-id="a01bf-163">Another invalid template error occurs when the resource name is not in the correct format.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'The template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   <span data-ttu-id="a01bf-164">Um recurso no nível-raiz deve ter um segmento a menos no nome que no tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="a01bf-164">A root level resource must have one less segment in the name than in the resource type.</span></span> <span data-ttu-id="a01bf-165">Cada segmento é diferenciado por uma barra.</span><span class="sxs-lookup"><span data-stu-id="a01bf-165">Each segment is differentiated by a slash.</span></span> <span data-ttu-id="a01bf-166">No exemplo a seguir, o tipo tem dois segmentos e o nome tem um segmento, portanto, é um **nome válido**.</span><span class="sxs-lookup"><span data-stu-id="a01bf-166">In the following example, the type has two segments and the name has one segment, so it is a **valid name**.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="a01bf-167">Mas o exemplo a seguir não é **um nome válido** porque ele tem o mesmo número de segmentos do tipo.</span><span class="sxs-lookup"><span data-stu-id="a01bf-167">But the next example is **not a valid name** because it has the same number of segments as the type.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="a01bf-168">Para os recursos-filho, o tipo e o nome têm o mesmo número de segmentos.</span><span class="sxs-lookup"><span data-stu-id="a01bf-168">For child resources, the type and name have the same number of segments.</span></span> <span data-ttu-id="a01bf-169">Esse número de segmentos faz sentido, porque o nome completo e o tipo para o filho incluem o nome do pai e o tipo.</span><span class="sxs-lookup"><span data-stu-id="a01bf-169">This number of segments makes sense because the full name and type for the child includes the parent name and type.</span></span> <span data-ttu-id="a01bf-170">Portanto, o nome completo ainda tem um segmento a menos que o tipo completo.</span><span class="sxs-lookup"><span data-stu-id="a01bf-170">Therefore, the full name still has one less segment than the full type.</span></span>

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

   <span data-ttu-id="a01bf-171">Ter os segmentos corretos pode ser difícil com os tipos de Resource Manager que são aplicados aos provedores de recursos.</span><span class="sxs-lookup"><span data-stu-id="a01bf-171">Getting the segments right can be tricky with Resource Manager types that are applied across resource providers.</span></span> <span data-ttu-id="a01bf-172">Por exemplo, aplicar um bloqueio de recurso a um site da Web requer um tipo com quatro segmentos.</span><span class="sxs-lookup"><span data-stu-id="a01bf-172">For example, applying a resource lock to a web site requires a type with four segments.</span></span> <span data-ttu-id="a01bf-173">Portanto, o nome tem três segmentos:</span><span class="sxs-lookup"><span data-stu-id="a01bf-173">Therefore, the name is three segments:</span></span>

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- <span data-ttu-id="a01bf-174">O índice de cópia não é esperado</span><span class="sxs-lookup"><span data-stu-id="a01bf-174">Copy index is not expected</span></span>

   <span data-ttu-id="a01bf-175">Você encontrou esse erro **InvalidTemplate** quando aplicou o elemento **copy** em uma parte do modelo que não dá suporte a esse elemento.</span><span class="sxs-lookup"><span data-stu-id="a01bf-175">You encounter this **InvalidTemplate** error when you have applied the **copy** element to a part of the template that does not support this element.</span></span> <span data-ttu-id="a01bf-176">Só é possível aplicar o elemento copy em um tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="a01bf-176">You can only apply the copy element to a resource type.</span></span> <span data-ttu-id="a01bf-177">Não é possível aplicar a cópia em uma propriedade dentro de um tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="a01bf-177">You cannot apply copy to a property within a resource type.</span></span> <span data-ttu-id="a01bf-178">Por exemplo, você aplica a cópia em uma máquina virtual, mas não pode aplicá-la nos discos do SO para uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a01bf-178">For example, you apply copy to a virtual machine, but you cannot apply it to the OS disks for a virtual machine.</span></span> <span data-ttu-id="a01bf-179">Em alguns casos, você pode converter um recurso-filho em um recurso-pai para criar um loop de cópia.</span><span class="sxs-lookup"><span data-stu-id="a01bf-179">In some cases, you can convert a child resource to a parent resource to create a copy loop.</span></span> <span data-ttu-id="a01bf-180">Para obter mais informações sobre como usar a cópia, consulte [Criar várias instâncias de recursos no Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="a01bf-180">For more information about using copy, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

- <span data-ttu-id="a01bf-181">O parâmetro não é válido</span><span class="sxs-lookup"><span data-stu-id="a01bf-181">Parameter is not valid</span></span>

   <span data-ttu-id="a01bf-182">Se o modelo especificar os valores permitidos para um parâmetro e você fornecer um valor que não é um deles, você receberá uma mensagem semelhante ao erro a seguir:</span><span class="sxs-lookup"><span data-stu-id="a01bf-182">If the template specifies permitted values for a parameter, and you provide a value that is not one of those values, you receive a message similar to the following error:</span></span>

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'The provided value {parameter value}
  for the template parameter {parameter name} is not valid. The parameter value is not
  part of the allowed values
  ``` 

   <span data-ttu-id="a01bf-183">Verifique uma segunda vez os valores permitidos no modelo e forneça um durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="a01bf-183">Double check the allowed values in the template, and provide one during deployment.</span></span>

- <span data-ttu-id="a01bf-184">Dependência circular detectada</span><span class="sxs-lookup"><span data-stu-id="a01bf-184">Circular dependency detected</span></span>

   <span data-ttu-id="a01bf-185">Você recebe esse erro quando recursos dependem entre si de uma maneira que impede que a implantação seja iniciado.</span><span class="sxs-lookup"><span data-stu-id="a01bf-185">You receive this error when resources depend on each other in a way that prevents the deployment from starting.</span></span> <span data-ttu-id="a01bf-186">Uma combinação de interdependências faz com que dois ou mais recursos aguardar para outros recursos que também estão aguardando.</span><span class="sxs-lookup"><span data-stu-id="a01bf-186">A combination of interdependencies makes two or more resource wait for other resources that are also waiting.</span></span> <span data-ttu-id="a01bf-187">Por exemplo, recurso1 depende resource3 resource2 depende recurso1 e resource3 depende resource2.</span><span class="sxs-lookup"><span data-stu-id="a01bf-187">For example, resource1 depends on resource3, resource2 depends on resource1, and resource3 depends on resource2.</span></span> <span data-ttu-id="a01bf-188">Geralmente você pode resolver esse problema removendo dependências desnecessárias.</span><span class="sxs-lookup"><span data-stu-id="a01bf-188">You can usually solve this problem by removing unnecessary dependencies.</span></span> 

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a><span data-ttu-id="a01bf-189">NotFound e ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="a01bf-189">NotFound and ResourceNotFound</span></span>
<span data-ttu-id="a01bf-190">Quando o modelo inclui o nome de um recurso que não pode ser resolvido, você recebe um erro semelhante a:</span><span class="sxs-lookup"><span data-stu-id="a01bf-190">When your template includes the name of a resource that cannot be resolved, you receive an error similar to:</span></span>

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

<span data-ttu-id="a01bf-191">Caso você esteja tentando implantar o recurso ausente no modelo, verifique se você precisa adicionar uma dependência.</span><span class="sxs-lookup"><span data-stu-id="a01bf-191">If you are attempting to deploy the missing resource in the template, check whether you need to add a dependency.</span></span> <span data-ttu-id="a01bf-192">O Gerenciador de Recursos otimiza a implantação criando recursos em paralelo, quando possível.</span><span class="sxs-lookup"><span data-stu-id="a01bf-192">Resource Manager optimizes deployment by creating resources in parallel, when possible.</span></span> <span data-ttu-id="a01bf-193">Se um recurso precisar ser implantado após outro recurso, você precisará usar o elemento **dependsOn** em seu modelo para criar uma dependência no outro recurso.</span><span class="sxs-lookup"><span data-stu-id="a01bf-193">If one resource must be deployed after another resource, you need to use the **dependsOn** element in your template to create a dependency on the other resource.</span></span> <span data-ttu-id="a01bf-194">Por exemplo, ao implantar um aplicativo Web, o plano do Serviço de Aplicativo deve existir.</span><span class="sxs-lookup"><span data-stu-id="a01bf-194">For example, when deploying a web app, the App Service plan must exist.</span></span> <span data-ttu-id="a01bf-195">Se você não tiver especificado que o aplicativo Web depende do plano do Serviço de Aplicativo, o Gerenciador de Recursos criará os dois recursos ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="a01bf-195">If you have not specified that the web app depends on the App Service plan, Resource Manager creates both resources at the same time.</span></span> <span data-ttu-id="a01bf-196">Você recebe um erro informando que o recurso do plano do Serviço de Aplicativo não pode ser encontrado porque ele ainda não existe ao tentar definir uma propriedade no aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="a01bf-196">You receive an error stating that the App Service plan resource cannot be found, because it does not exist yet when attempting to set a property on the web app.</span></span> <span data-ttu-id="a01bf-197">Você evita esse erro configurando a dependência no aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="a01bf-197">You prevent this error by setting the dependency in the web app.</span></span>

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

<span data-ttu-id="a01bf-198">Para obter sugestões sobre como solucionar erros de dependência, veja [Verificar a sequência de implantação](#check-deployment-sequence).</span><span class="sxs-lookup"><span data-stu-id="a01bf-198">For suggestions on troubleshooting dependency errors, see [Check deployment sequence](#check-deployment-sequence).</span></span>

<span data-ttu-id="a01bf-199">Você também vê esse erro quando o recurso existe em um grupo de recursos diferente daquele que está sendo implantado.</span><span class="sxs-lookup"><span data-stu-id="a01bf-199">You also see this error when the resource exists in a different resource group than the one being deployed to.</span></span> <span data-ttu-id="a01bf-200">Nesse caso, use a [função resourceId](resource-group-template-functions-resource.md#resourceid) para obter o nome totalmente qualificado do recurso.</span><span class="sxs-lookup"><span data-stu-id="a01bf-200">In that case, use the [resourceId function](resource-group-template-functions-resource.md#resourceid) to get the fully qualified name of the resource.</span></span>

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

<span data-ttu-id="a01bf-201">Se tentar usar as funções [reference](resource-group-template-functions-resource.md#reference) ou [listKeys](resource-group-template-functions-resource.md#listkeys) com um recurso que não pode ser resolvido, você receberá o seguinte erro:</span><span class="sxs-lookup"><span data-stu-id="a01bf-201">If you attempt to use the [reference](resource-group-template-functions-resource.md#reference) or [listKeys](resource-group-template-functions-resource.md#listkeys) functions with a resource that cannot be resolved, you receive the following error:</span></span>

```
Code=ResourceNotFound;
Message=The Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

<span data-ttu-id="a01bf-202">Procure por uma expressão que inclui a função **reference**.</span><span class="sxs-lookup"><span data-stu-id="a01bf-202">Look for an expression that includes the **reference** function.</span></span> <span data-ttu-id="a01bf-203">Verifique uma segunda vez se os valores de parâmetro estão corretos.</span><span class="sxs-lookup"><span data-stu-id="a01bf-203">Double check that the parameter values are correct.</span></span>

## <a name="parentresourcenotfound"></a><span data-ttu-id="a01bf-204">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="a01bf-204">ParentResourceNotFound</span></span>

<span data-ttu-id="a01bf-205">Quando um recurso é pai de outro recurso, o recurso pai deve existir antes da criação do recurso filho.</span><span class="sxs-lookup"><span data-stu-id="a01bf-205">When one resource is a parent to another resource, the parent resource must exist before creating the child resource.</span></span> <span data-ttu-id="a01bf-206">Se ele ainda não existir, você receberá o seguinte erro:</span><span class="sxs-lookup"><span data-stu-id="a01bf-206">If it does not yet exist, you receive the following error:</span></span>

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

<span data-ttu-id="a01bf-207">O nome do recurso filho inclui o nome do pai.</span><span class="sxs-lookup"><span data-stu-id="a01bf-207">The name of the child resource includes the parent name.</span></span> <span data-ttu-id="a01bf-208">Por exemplo, um Banco de Dados SQL pode ser definido como:</span><span class="sxs-lookup"><span data-stu-id="a01bf-208">For example, a SQL Database might be defined as:</span></span>

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

<span data-ttu-id="a01bf-209">Mas, se você não especificar uma dependência no recurso pai, o recurso filho poderá obter implantado antes do pai.</span><span class="sxs-lookup"><span data-stu-id="a01bf-209">But, if you do not specify a dependency on the parent resource, the child resource may get deployed before the parent.</span></span> <span data-ttu-id="a01bf-210">Para resolver esse erro, inclua uma dependência.</span><span class="sxs-lookup"><span data-stu-id="a01bf-210">To resolve this error, include a dependency.</span></span>

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />

## <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a><span data-ttu-id="a01bf-211">StorageAccountAlreadyExists e StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="a01bf-211">StorageAccountAlreadyExists and StorageAccountAlreadyTaken</span></span>
<span data-ttu-id="a01bf-212">Para contas de armazenamento, você deve fornecer um nome para o recurso que é exclusivo no Azure.</span><span class="sxs-lookup"><span data-stu-id="a01bf-212">For storage accounts, you must provide a name for the resource that is unique across Azure.</span></span> <span data-ttu-id="a01bf-213">Se você não fornecer um nome exclusivo, receberá um erro como:</span><span class="sxs-lookup"><span data-stu-id="a01bf-213">If you do not provide a unique name, you receive an error like:</span></span>

```
Code=StorageAccountAlreadyTaken
Message=The storage account named mystorage is already taken.
```

<span data-ttu-id="a01bf-214">Você pode criar um nome exclusivo concatenando a convenção de nomenclatura com o resultado da função [uniqueString](resource-group-template-functions-string.md#uniquestring) .</span><span class="sxs-lookup"><span data-stu-id="a01bf-214">You can create a unique name by concatenating your naming convention with the result of the [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span>

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

<span data-ttu-id="a01bf-215">Se você implantar uma conta de armazenamento com o mesmo nome que uma conta de armazenamento existente na sua assinatura, mas fornecer um local diferente, você receberá um erro indicando que a conta de armazenamento já existe em um local diferente.</span><span class="sxs-lookup"><span data-stu-id="a01bf-215">If you deploy a storage account with the same name as an existing storage account in your subscription, but provide a different location, you receive an error indicating the storage account already exists in a different location.</span></span> <span data-ttu-id="a01bf-216">Exclua a conta de armazenamento existente ou forneça o mesmo local da conta de armazenamento existente.</span><span class="sxs-lookup"><span data-stu-id="a01bf-216">Either delete the existing storage account, or provide the same location as the existing storage account.</span></span>

## <a name="accountnameinvalid"></a><span data-ttu-id="a01bf-217">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="a01bf-217">AccountNameInvalid</span></span>
<span data-ttu-id="a01bf-218">Você verá o erro **AccountNameInvalid** ao tentar conceder um nome que inclui caracteres proibidos a uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a01bf-218">You see the **AccountNameInvalid** error when attempting to give a storage account a name that includes prohibited characters.</span></span> <span data-ttu-id="a01bf-219">Os nomes da conta de armazenamento devem ter entre 3 e 24 caracteres, usar números e apenas letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="a01bf-219">Storage account names must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span> <span data-ttu-id="a01bf-220">O [uniqueString](resource-group-template-functions-string.md#uniquestring) função retorna 13 caracteres.</span><span class="sxs-lookup"><span data-stu-id="a01bf-220">The [uniqueString](resource-group-template-functions-string.md#uniquestring) function returns 13 characters.</span></span> <span data-ttu-id="a01bf-221">Se você concatenar um prefixo para o **uniqueString** resultar, forneça um prefixo de 11 caracteres ou menos.</span><span class="sxs-lookup"><span data-stu-id="a01bf-221">If you concatenate a prefix to the **uniqueString** result, provide a prefix that is 11 characters or less.</span></span>

## <a name="badrequest"></a><span data-ttu-id="a01bf-222">BadRequest</span><span class="sxs-lookup"><span data-stu-id="a01bf-222">BadRequest</span></span>

<span data-ttu-id="a01bf-223">Você pode receber um status BadRequest ao fornecer um valor inválido para uma propriedade.</span><span class="sxs-lookup"><span data-stu-id="a01bf-223">You may encounter a BadRequest status when you provide an invalid value for a property.</span></span> <span data-ttu-id="a01bf-224">Por exemplo, se você fornecer um valor incorreto de SKU para uma conta de armazenamento, a implantação falhará.</span><span class="sxs-lookup"><span data-stu-id="a01bf-224">For example, if you provide an incorrect SKU value for a storage account, the deployment fails.</span></span> <span data-ttu-id="a01bf-225">Para determinar os valores válidos para a propriedade, veja o [API REST](/rest/api) para o tipo de recurso que você está implantando.</span><span class="sxs-lookup"><span data-stu-id="a01bf-225">To determine valid values for property, look at the [REST API](/rest/api) for the resource type you are deploying.</span></span>

<a id="noregisteredproviderfound" />

## <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a><span data-ttu-id="a01bf-226">NoRegisteredProviderFound e MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="a01bf-226">NoRegisteredProviderFound and MissingSubscriptionRegistration</span></span>
<span data-ttu-id="a01bf-227">Ao implantar recursos, você pode receber o seguinte código de erro e a mensagem:</span><span class="sxs-lookup"><span data-stu-id="a01bf-227">When deploying resource, you may receive the following error code and message:</span></span>

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

<span data-ttu-id="a01bf-228">Ou você poderá receber uma mensagem semelhante que indica:</span><span class="sxs-lookup"><span data-stu-id="a01bf-228">Or, you may receive a similar message that states:</span></span>

```
Code: MissingSubscriptionRegistration
Message: The subscription is not registered to use namespace {resource-provider-namespace}
```

<span data-ttu-id="a01bf-229">Você recebe esses erros por um dos três motivos:</span><span class="sxs-lookup"><span data-stu-id="a01bf-229">You receive these errors for one of three reasons:</span></span>

1. <span data-ttu-id="a01bf-230">O provedor de recursos não foi registrado para sua assinatura</span><span class="sxs-lookup"><span data-stu-id="a01bf-230">The resource provider has not been registered for your subscription</span></span>
2. <span data-ttu-id="a01bf-231">Versão da API não suportada para o tipo de recurso</span><span class="sxs-lookup"><span data-stu-id="a01bf-231">API version not supported for the resource type</span></span>
3. <span data-ttu-id="a01bf-232">Local não suportado para o tipo de recurso</span><span class="sxs-lookup"><span data-stu-id="a01bf-232">Location not supported for the resource type</span></span>

<span data-ttu-id="a01bf-233">A mensagem de erro deve fornecer sugestões para os locais com suporte e as versões da API.</span><span class="sxs-lookup"><span data-stu-id="a01bf-233">The error message should give you suggestions for the supported locations and API versions.</span></span> <span data-ttu-id="a01bf-234">Você pode alterar o modelo para um dos valores sugeridos.</span><span class="sxs-lookup"><span data-stu-id="a01bf-234">You can change your template to one of the suggested values.</span></span> <span data-ttu-id="a01bf-235">A maioria dos provedores são registrados automaticamente pelo portal do Azure ou pela interface de linha de comando que você está usando, mas nem todos.</span><span class="sxs-lookup"><span data-stu-id="a01bf-235">Most providers are registered automatically by the Azure portal or the command-line interface you are using, but not all.</span></span> <span data-ttu-id="a01bf-236">Se você não usou um provedor de recursos específico antes, precisará registrá-lo.</span><span class="sxs-lookup"><span data-stu-id="a01bf-236">If you have not used a particular resource provider before, you may need to register that provider.</span></span> <span data-ttu-id="a01bf-237">Você pode descobrir mais sobre provedores de recursos por meio do PowerShell ou CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="a01bf-237">You can discover more about resource providers through PowerShell or Azure CLI.</span></span>

<span data-ttu-id="a01bf-238">**Portal**</span><span class="sxs-lookup"><span data-stu-id="a01bf-238">**Portal**</span></span>

<span data-ttu-id="a01bf-239">É possível ver o status de registro e registrar um namespace do provedor de recursos por meio do portal.</span><span class="sxs-lookup"><span data-stu-id="a01bf-239">You can see the registration status and register a resource provider namespace through the portal.</span></span>

1. <span data-ttu-id="a01bf-240">Em sua assinatura, selecione **Provedores de recursos**.</span><span class="sxs-lookup"><span data-stu-id="a01bf-240">For your subscription, select **Resource providers**.</span></span>

   ![selecionar provedores de recursos](./media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. <span data-ttu-id="a01bf-242">Examine a lista de provedores de recursos e, se necessário, selecione o link **Registrar** para registrar o provedor de recursos do tipo que você está tentando implantar.</span><span class="sxs-lookup"><span data-stu-id="a01bf-242">Look at the list of resource providers, and if necessary, select the **Register** link to register the resource provider of the type you are trying to deploy.</span></span>

   ![listar provedores de recursos](./media/resource-manager-common-deployment-errors/list-resource-providers.png)

<span data-ttu-id="a01bf-244">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="a01bf-244">**PowerShell**</span></span>

<span data-ttu-id="a01bf-245">Para ver o status do registro, use **Get-AzureRmResourceProvider**.</span><span class="sxs-lookup"><span data-stu-id="a01bf-245">To see your registration status, use **Get-AzureRmResourceProvider**.</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

<span data-ttu-id="a01bf-246">Para registrar um provedor, use **Register-AzureRmResourceProvider** e forneça o nome do provedor de recursos que você deseja registrar.</span><span class="sxs-lookup"><span data-stu-id="a01bf-246">To register a provider, use **Register-AzureRmResourceProvider** and provide the name of the resource provider you wish to register.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

<span data-ttu-id="a01bf-247">Para obter os locais com suporte para um determinado tipo de recurso, use:</span><span class="sxs-lookup"><span data-stu-id="a01bf-247">To get the supported locations for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="a01bf-248">Para obter as versões da API com suporte para um determinado tipo de recurso, use:</span><span class="sxs-lookup"><span data-stu-id="a01bf-248">To get the supported API versions for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

<span data-ttu-id="a01bf-249">**CLI do Azure**</span><span class="sxs-lookup"><span data-stu-id="a01bf-249">**Azure CLI**</span></span>

<span data-ttu-id="a01bf-250">Para ver se o provedor está registrado, use o comando `azure provider list` .</span><span class="sxs-lookup"><span data-stu-id="a01bf-250">To see whether the provider is registered, use the `azure provider list` command.</span></span>

```azurecli
az provider list
```

<span data-ttu-id="a01bf-251">Para registrar um provedor de recursos, use o comando `azure provider register` e especifique o *namespace* para registrar.</span><span class="sxs-lookup"><span data-stu-id="a01bf-251">To register a resource provider, use the `azure provider register` command, and specify the *namespace* to register.</span></span>

```azurecli
az provider register --namespace Microsoft.Cdn
```

<span data-ttu-id="a01bf-252">Para ver os locais com suporte e as versões da API para um tipo de recurso, use:</span><span class="sxs-lookup"><span data-stu-id="a01bf-252">To see the supported locations and API versions for a resource type, use:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />

## <a name="quotaexceeded-and-operationnotallowed"></a><span data-ttu-id="a01bf-253">QuotaExceeded e OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="a01bf-253">QuotaExceeded and OperationNotAllowed</span></span>
<span data-ttu-id="a01bf-254">Você pode ter problemas quando a implantação ultrapassar uma cota, que pode ser por grupo de recursos, assinaturas, contas e outros escopos.</span><span class="sxs-lookup"><span data-stu-id="a01bf-254">You might have issues when deployment exceeds a quota, which could be per resource group, subscriptions, accounts, and other scopes.</span></span> <span data-ttu-id="a01bf-255">Por exemplo, sua assinatura pode estar configurada para limitar o número de núcleos de uma região.</span><span class="sxs-lookup"><span data-stu-id="a01bf-255">For example, your subscription may be configured to limit the number of cores for a region.</span></span> <span data-ttu-id="a01bf-256">Se tentar implantar uma máquina virtual com mais núcleos do que o valor permitido, você receberá um erro informando que a cota foi excedida.</span><span class="sxs-lookup"><span data-stu-id="a01bf-256">If you attempt to deploy a virtual machine with more cores than the permitted amount, you receive an error stating the quota has been exceeded.</span></span>
<span data-ttu-id="a01bf-257">Para obter informações completas sobre cotas, consulte [Limites, cotas e restrições de serviço e assinatura do Azure](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="a01bf-257">For complete quota information, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="a01bf-258">Para examinar as cotas de núcleos da assinatura, você deve usar o comando `azure vm list-usage` na CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="a01bf-258">To examine your subscription's quotas for cores, you can use the `azure vm list-usage` command in the Azure CLI.</span></span> <span data-ttu-id="a01bf-259">O exemplo a seguir ilustra que a cota de núcleo de uma conta de avaliação gratuita é 4:</span><span class="sxs-lookup"><span data-stu-id="a01bf-259">The following example illustrates that the core quota for a free trial account is 4:</span></span>

```azurecli
az vm list-usage --location "South Central US"
```

<span data-ttu-id="a01bf-260">Que retorna:</span><span class="sxs-lookup"><span data-stu-id="a01bf-260">Which returns:</span></span>

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

<span data-ttu-id="a01bf-261">Se implantar um modelo que cria mais de quatro núcleos na região Oeste dos EUA, você receberá um erro de implantação que se parece com:</span><span class="sxs-lookup"><span data-stu-id="a01bf-261">If you deploy a template that creates more than four cores in the West US region, you get a deployment error that looks like:</span></span>

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

<span data-ttu-id="a01bf-262">Ou no PowerShell, você pode usar o cmdlet **Get-AzureRmVMUsage** .</span><span class="sxs-lookup"><span data-stu-id="a01bf-262">Or in PowerShell, you can use the **Get-AzureRmVMUsage** cmdlet.</span></span>

```powershell
Get-AzureRmVMUsage
```

<span data-ttu-id="a01bf-263">Que retorna:</span><span class="sxs-lookup"><span data-stu-id="a01bf-263">Which returns:</span></span>

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

<span data-ttu-id="a01bf-264">Nesses casos, você deve ir para o portal e abrir um problema de suporte para aumentar a cota para a região na qual você deseja implantar.</span><span class="sxs-lookup"><span data-stu-id="a01bf-264">In these cases, you should go to the portal and file a support issue to raise your quota for the region into which you want to deploy.</span></span>

> [!NOTE]
> <span data-ttu-id="a01bf-265">Lembre-se de que, para grupos de recursos, a cota é para cada região individual, não para a assinatura inteira.</span><span class="sxs-lookup"><span data-stu-id="a01bf-265">Remember that for resource groups, the quota is for each individual region, not for the entire subscription.</span></span> <span data-ttu-id="a01bf-266">Se você precisar implantar 30 núcleos no Oeste dos EUA, será necessário pedir 30 núcleos do Gerenciador de Recursos no Oeste dos EUA.</span><span class="sxs-lookup"><span data-stu-id="a01bf-266">If you need to deploy 30 cores in West US, you have to ask for 30 Resource Manager cores in West US.</span></span> <span data-ttu-id="a01bf-267">Se precisar implantar 30 núcleos em qualquer uma das regiões às quais tenha acesso, você deverá solicitar 30 núcleos do Resource Manager em todas as regiões.</span><span class="sxs-lookup"><span data-stu-id="a01bf-267">If you need to deploy 30 cores in any of the regions to which you have access, you should ask for 30 Resource Manager cores in all regions.</span></span>
>
>

## <a name="invalidcontentlink"></a><span data-ttu-id="a01bf-268">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="a01bf-268">InvalidContentLink</span></span>
<span data-ttu-id="a01bf-269">Quando você recebe a mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="a01bf-269">When you receive the error message:</span></span>

```
Code=InvalidContentLink
Message=Unable to download deployment content from ...
```

<span data-ttu-id="a01bf-270">Provavelmente você tentou vincular a um modelo aninhado que não está disponível.</span><span class="sxs-lookup"><span data-stu-id="a01bf-270">You have most likely attempted to link to a nested template that is not available.</span></span> <span data-ttu-id="a01bf-271">Verifique uma segunda vez o URI que você forneceu para o modelo aninhado.</span><span class="sxs-lookup"><span data-stu-id="a01bf-271">Double check the URI you provided for the nested template.</span></span> <span data-ttu-id="a01bf-272">Caso o modelo exista em uma conta de armazenamento, verifique se o URI está acessível.</span><span class="sxs-lookup"><span data-stu-id="a01bf-272">If the template exists in a storage account, make sure the URI is accessible.</span></span> <span data-ttu-id="a01bf-273">Pode ser necessário passar um token SAS.</span><span class="sxs-lookup"><span data-stu-id="a01bf-273">You may need to pass a SAS token.</span></span> <span data-ttu-id="a01bf-274">Para saber mais, confira [Usando modelos vinculados com o Gerenciador de Recursos do Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a01bf-274">For more information, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="requestdisallowedbypolicy"></a><span data-ttu-id="a01bf-275">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="a01bf-275">RequestDisallowedByPolicy</span></span>
<span data-ttu-id="a01bf-276">Você recebe esse erro quando sua assinatura inclui uma política de recursos que impede uma ação que está tentando executar durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="a01bf-276">You receive this error when your subscription includes a resource policy that prevents an action you are trying to perform during deployment.</span></span> <span data-ttu-id="a01bf-277">Na mensagem de erro, procure o identificador da política.</span><span class="sxs-lookup"><span data-stu-id="a01bf-277">In the error message, look for the policy identifier.</span></span>

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

<span data-ttu-id="a01bf-278">No **PowerShell**, forneça o identificador de política como o parâmetro **Id** para recuperar detalhes sobre a política que bloqueou a sua implantação.</span><span class="sxs-lookup"><span data-stu-id="a01bf-278">In **PowerShell**, provide that policy identifier as the **Id** parameter to retrieve details about the policy that blocked your deployment.</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

<span data-ttu-id="a01bf-279">Na **CLI do Azure**, forneça o nome da definição da política:</span><span class="sxs-lookup"><span data-stu-id="a01bf-279">In **Azure CLI**, provide the name of the policy definition:</span></span>

```azurecli
az policy definition show --name regionPolicyAssignment
```

<span data-ttu-id="a01bf-280">Para obter mais informações, consulte os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="a01bf-280">For more information, see the following articles:</span></span>

- [<span data-ttu-id="a01bf-281">Erro RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="a01bf-281">RequestDisallowedByPolicy error</span></span>](resource-manager-policy-requestdisallowedbypolicy-error.md)
- <span data-ttu-id="a01bf-282">[Usar a Política para gerenciar recursos e controlar o acesso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="a01bf-282">[Use Policy to manage resources and control access](resource-manager-policy.md).</span></span>

## <a name="authorization-failed"></a><span data-ttu-id="a01bf-283">Falha na autorização</span><span class="sxs-lookup"><span data-stu-id="a01bf-283">Authorization failed</span></span>
<span data-ttu-id="a01bf-284">Você pode receber um erro durante a implantação porque a conta ou a entidade de serviço que está tentando implantar os recursos de serviço não tem acesso para executar essas ações.</span><span class="sxs-lookup"><span data-stu-id="a01bf-284">You may receive an error during deployment because the account or service principal attempting to deploy the resources does not have access to perform those actions.</span></span> <span data-ttu-id="a01bf-285">O Azure Active Directory permite que você ou seu administrador controlem quais identidades podem acessar os recursos com um alto grau de precisão.</span><span class="sxs-lookup"><span data-stu-id="a01bf-285">Azure Active Directory enables you or your administrator to control which identities can access what resources with a great degree of precision.</span></span> <span data-ttu-id="a01bf-286">Por exemplo, se sua conta estiver atribuída à função Leitor, você não poderá criar recursos.</span><span class="sxs-lookup"><span data-stu-id="a01bf-286">For example, if your account is assigned to the Reader role, you are not able to create resources.</span></span> <span data-ttu-id="a01bf-287">Nesse caso, você vê uma mensagem de erro indicando que houve falha na autorização.</span><span class="sxs-lookup"><span data-stu-id="a01bf-287">In that case, you see an error message indicating that authorization failed.</span></span>

<span data-ttu-id="a01bf-288">Para obter mais informações sobre o controle de acesso baseado em funções, consulte [Controle de Acesso Baseado em Funções do Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="a01bf-288">For more information about role-based access control, see [Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="a01bf-289">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a01bf-289">Next steps</span></span>
* <span data-ttu-id="a01bf-290">Para saber sobre as ações de auditoria, consulte [Auditar operações com o Gerenciador de Recursos](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="a01bf-290">To learn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="a01bf-291">Para saber sobre as ações para determinar os erros durante a implantação, consulte [Exibir operações de implantação](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="a01bf-291">To learn about actions to determine the errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
