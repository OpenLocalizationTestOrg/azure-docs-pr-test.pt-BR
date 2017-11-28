---
title: local do recurso aaaAzure no modelo | Microsoft Docs
description: Mostra como tooset um local para um recurso em um modelo do Gerenciador de recursos do Azure
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: tomfitz
ms.openlocfilehash: f2ad6ca6ac5f34484a2e5e57dd8d67c77dacc41a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-resource-location-in-azure-resource-manager-templates"></a><span data-ttu-id="dc6ff-103">Configure os locais dos recursos de modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dc6ff-103">Set resource location in Azure Resource Manager templates</span></span>
<span data-ttu-id="dc6ff-104">Ao implantar um modelo, é necessário fornecer um local para cada recurso.</span><span class="sxs-lookup"><span data-stu-id="dc6ff-104">When deploying a template, you must provide a location for each resource.</span></span> <span data-ttu-id="dc6ff-105">Este tópico mostra como locais de saudação toodetermine que estão disponíveis tooyour assinatura para cada recurso de tipo.</span><span class="sxs-lookup"><span data-stu-id="dc6ff-105">This topic shows how toodetermine hello locations that are available tooyour subscription for each resource type.</span></span>

## <a name="determine-supported-locations"></a><span data-ttu-id="dc6ff-106">Determinar locais com suporte</span><span class="sxs-lookup"><span data-stu-id="dc6ff-106">Determine supported locations</span></span>

<span data-ttu-id="dc6ff-107">Para obter uma lista completa de locais com suporte para cada tipo de recurso, consulte [Produtos disponíveis por região](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="dc6ff-107">For a complete list of supported locations for each resource type, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="dc6ff-108">No entanto, sua assinatura pode não ter acesso tooall Olá locais nessa lista.</span><span class="sxs-lookup"><span data-stu-id="dc6ff-108">However, your subscription might not have access tooall hello locations in that list.</span></span> <span data-ttu-id="dc6ff-109">toosee uma lista personalizada de locais que estão disponíveis tooyour assinatura, use o Azure PowerShell ou CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="dc6ff-109">toosee a customized list of locations that are available tooyour subscription, use Azure PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="dc6ff-110">Olá exemplo a seguir usa locais de saudação do PowerShell tooget para Olá `Microsoft.Web\sites` tipo de recurso:</span><span class="sxs-lookup"><span data-stu-id="dc6ff-110">hello following example uses PowerShell tooget hello locations for hello `Microsoft.Web\sites` resource type:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="dc6ff-111">Olá exemplo a seguir usa locais de saudação tooget 2.0 do CLI do Azure para Olá `Microsoft.Web\sites` tipo de recurso:</span><span class="sxs-lookup"><span data-stu-id="dc6ff-111">hello following example uses Azure CLI 2.0 tooget hello locations for hello `Microsoft.Web\sites` resource type:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="set-location-in-template"></a><span data-ttu-id="dc6ff-112">Configurar o local no modelo</span><span class="sxs-lookup"><span data-stu-id="dc6ff-112">Set location in template</span></span>

<span data-ttu-id="dc6ff-113">Depois de determinar os locais de saudação com suporte para os seus recursos, você precisa tooset local no seu modelo.</span><span class="sxs-lookup"><span data-stu-id="dc6ff-113">After determining hello supported locations for your resources, you need tooset that location in your template.</span></span> <span data-ttu-id="dc6ff-114">Olá tooset de maneira mais fácil esse valor é toocreate um recurso de grupo em um local que dá suporte a tipos de recurso hello e defina cada local muito`[resourceGroup().location]`.</span><span class="sxs-lookup"><span data-stu-id="dc6ff-114">hello easiest way tooset this value is toocreate a resource group in a location that supports hello resource types, and set each location too`[resourceGroup().location]`.</span></span> <span data-ttu-id="dc6ff-115">Você pode reimplantar os grupos de tooresource Olá modelos em diferentes locais e não alterar quaisquer valores no modelo de saudação ou parâmetros.</span><span class="sxs-lookup"><span data-stu-id="dc6ff-115">You can redeploy hello template tooresource groups in different locations, and not change any values in hello template or parameters.</span></span> 

<span data-ttu-id="dc6ff-116">Olá, exemplo a seguir mostra uma conta de armazenamento que é implantado toohello mesmo local que o grupo de recursos de saudação:</span><span class="sxs-lookup"><span data-stu-id="dc6ff-116">hello following example shows a storage account that is deployed toohello same location as hello resource group:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
      "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

<span data-ttu-id="dc6ff-117">Se precisar de local de saudação toohardcode em seu modelo, forneça o nome de saudação de uma das regiões Olá com suporte.</span><span class="sxs-lookup"><span data-stu-id="dc6ff-117">If you need toohardcode hello location in your template, provide hello name of one of hello supported regions.</span></span> <span data-ttu-id="dc6ff-118">saudação de exemplo a seguir mostra uma conta de armazenamento sempre é implantado tooNorth centro dos EUA:</span><span class="sxs-lookup"><span data-stu-id="dc6ff-118">hello following example shows a storage account that is always deployed tooNorth Central US:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storageloc', uniqueString(resourceGroup().id))]",
      "location": "North Central US",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

## <a name="next-steps"></a><span data-ttu-id="dc6ff-119">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dc6ff-119">Next steps</span></span>
* <span data-ttu-id="dc6ff-120">Para obter recomendações sobre como toocreate modelos, consulte [práticas recomendadas para a criação de modelos do Azure Resource Manager](resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="dc6ff-120">For recommendations about how toocreate templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>

