---
title: "Elemento de interface do usuário SizeSelector de aplicativo gerenciado do Azure | Microsoft Docs"
description: "Descreve o elemento Microsoft.Compute.SizeSelector da interface do usuário para aplicativos gerenciados do Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: e54962f73028ada258a7faef271d66f0fbcef649
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcomputesizeselector-ui-element"></a><span data-ttu-id="9c19f-103">Elemento de interface do usuário Microsoft.Compute.SizeSelector</span><span class="sxs-lookup"><span data-stu-id="9c19f-103">Microsoft.Compute.SizeSelector UI element</span></span>
<span data-ttu-id="9c19f-104">Um controle para selecionar um tamanho de uma ou mais instâncias de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9c19f-104">A control for selecting a size for one or more virtual machine instances.</span></span> <span data-ttu-id="9c19f-105">Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="9c19f-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="9c19f-106">Exemplo de interface do usuário</span><span class="sxs-lookup"><span data-stu-id="9c19f-106">UI sample</span></span>
![Microsoft.Compute.SizeSelector](./media/managed-application-elements/microsoft.compute.sizeselector.png)

## <a name="schema"></a><span data-ttu-id="9c19f-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="9c19f-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.SizeSelector",
  "label": "Size",
  "toolTip": "",
  "recommendedSizes": [
    "Standard_D1",
    "Standard_D2",
    "Standard_D3"
  ],
  "constraints": {
    "allowedSizes": [],
    "excludedSizes": []
  },
  "osPlatform": "Windows",
  "imageReference": {
    "publisher": "MicrosoftWindowsServer",
    "offer": "WindowsServer",
    "sku": "2012-R2-Datacenter"
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="9c19f-109">Comentários</span><span class="sxs-lookup"><span data-stu-id="9c19f-109">Remarks</span></span>
- <span data-ttu-id="9c19f-110">`recommendedSizes` deve conter pelo menos um tamanho.</span><span class="sxs-lookup"><span data-stu-id="9c19f-110">`recommendedSizes` should contain at least one size.</span></span> <span data-ttu-id="9c19f-111">O primeiro tamanho recomendado é usado como padrão.</span><span class="sxs-lookup"><span data-stu-id="9c19f-111">The first recommended size is used as the default.</span></span>
- <span data-ttu-id="9c19f-112">Se um tamanho recomendado não estiver disponível no local selecionado, o tamanho será ignorado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9c19f-112">If a recommended size is not available in the selected location, the size is automatically skipped.</span></span> <span data-ttu-id="9c19f-113">O próximo tamanho recomendado será usado.</span><span class="sxs-lookup"><span data-stu-id="9c19f-113">Instead, the next recommended size is used.</span></span>
- <span data-ttu-id="9c19f-114">Os tamanhos não especificados em `constraints.allowedSizes` ficam ocultos e os tamanhos não especificados em `constraints.excludedSizes` são mostrados.</span><span class="sxs-lookup"><span data-stu-id="9c19f-114">Any size not specified in the `constraints.allowedSizes` is hidden, and any size not specified in `constraints.excludedSizes` is shown.</span></span>
<span data-ttu-id="9c19f-115">`constraints.allowedSizes` e `constraints.excludedSizes` são opcionais, mas não podem ser usados simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="9c19f-115">`constraints.allowedSizes` and `constraints.excludedSizes` are both optional, but cannot be used simultaneously.</span></span> <span data-ttu-id="9c19f-116">A lista de tamanhos disponíveis pode ser determinada chamando [Listar tamanhos de máquinas virtuais disponíveis para uma assinatura](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span><span class="sxs-lookup"><span data-stu-id="9c19f-116">The list of available sizes can be determined by calling [List available virtual machine sizes for a subscription](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span></span>
- <span data-ttu-id="9c19f-117">`osPlatform` deve ser especificada e pode ser **Windows** ou **Linux**.</span><span class="sxs-lookup"><span data-stu-id="9c19f-117">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span> <span data-ttu-id="9c19f-118">Ela é usada para determinar os custos de hardware das máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="9c19f-118">It's used to determine the hardware costs of the virtual machines.</span></span>
- <span data-ttu-id="9c19f-119">`imageReference` é omitida para imagens próprias, mas fornecida para imagens de terceiros.</span><span class="sxs-lookup"><span data-stu-id="9c19f-119">`imageReference` is omitted for first-party images, but provided for third-party images.</span></span> <span data-ttu-id="9c19f-120">Ela é usada para determinar os custos de software das máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="9c19f-120">It's used to determine the software costs of the virtual machines.</span></span>
- <span data-ttu-id="9c19f-121">`count` é usado para definir o multiplicador apropriado para o elemento.</span><span class="sxs-lookup"><span data-stu-id="9c19f-121">`count` is used to set the appropriate multiplier for the element.</span></span> <span data-ttu-id="9c19f-122">Ele dá suporte a um valor estático, como **2**, ou a um valor dinâmico de outro elemento, como `[steps('step1').vmCount]`.</span><span class="sxs-lookup"><span data-stu-id="9c19f-122">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').vmCount]`.</span></span> <span data-ttu-id="9c19f-123">O valor padrão é **1**.</span><span class="sxs-lookup"><span data-stu-id="9c19f-123">The default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="9c19f-124">Saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="9c19f-124">Sample output</span></span>
```json
"Standard_D1"
```

## <a name="next-steps"></a><span data-ttu-id="9c19f-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9c19f-125">Next steps</span></span>
* <span data-ttu-id="9c19f-126">Para obter uma introdução aos aplicativos gerenciados, consulte [Visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9c19f-126">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="9c19f-127">Para obter uma introdução à criação de definições de interface do usuário, consulte [Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9c19f-127">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="9c19f-128">Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="9c19f-128">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
