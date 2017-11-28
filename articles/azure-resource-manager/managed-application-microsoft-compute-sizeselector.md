---
title: "elemento de interface do usuário SizeSelector de aplicativo gerenciado aaaAzure | Microsoft Docs"
description: "Descreve Olá elemento Microsoft.Compute.SizeSelector da interface do usuário para aplicativos gerenciados do Azure"
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
ms.openlocfilehash: d93306135d9c6f9a83692766ce1ca7ea2b688086
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputesizeselector-ui-element"></a><span data-ttu-id="9191e-103">Elemento de interface do usuário Microsoft.Compute.SizeSelector</span><span class="sxs-lookup"><span data-stu-id="9191e-103">Microsoft.Compute.SizeSelector UI element</span></span>
<span data-ttu-id="9191e-104">Um controle para selecionar um tamanho de uma ou mais instâncias de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9191e-104">A control for selecting a size for one or more virtual machine instances.</span></span> <span data-ttu-id="9191e-105">Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="9191e-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="9191e-106">Exemplo de interface do usuário</span><span class="sxs-lookup"><span data-stu-id="9191e-106">UI sample</span></span>
![Microsoft.Compute.SizeSelector](./media/managed-application-elements/microsoft.compute.sizeselector.png)

## <a name="schema"></a><span data-ttu-id="9191e-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="9191e-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="9191e-109">Comentários</span><span class="sxs-lookup"><span data-stu-id="9191e-109">Remarks</span></span>
- <span data-ttu-id="9191e-110">`recommendedSizes` deve conter pelo menos um tamanho.</span><span class="sxs-lookup"><span data-stu-id="9191e-110">`recommendedSizes` should contain at least one size.</span></span> <span data-ttu-id="9191e-111">Olá recomendado primeiro tamanho é usado como padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="9191e-111">hello first recommended size is used as hello default.</span></span>
- <span data-ttu-id="9191e-112">Se um tamanho recomendado não está disponível no local de saudação selecionada, o tamanho de saudação automaticamente será ignorado.</span><span class="sxs-lookup"><span data-stu-id="9191e-112">If a recommended size is not available in hello selected location, hello size is automatically skipped.</span></span> <span data-ttu-id="9191e-113">Em vez disso, hello próximo tamanho recomendado é usado.</span><span class="sxs-lookup"><span data-stu-id="9191e-113">Instead, hello next recommended size is used.</span></span>
- <span data-ttu-id="9191e-114">Qualquer tamanho não está especificado no hello `constraints.allowedSizes` estiver oculto e qualquer tamanho não é especificado em `constraints.excludedSizes` é mostrado.</span><span class="sxs-lookup"><span data-stu-id="9191e-114">Any size not specified in hello `constraints.allowedSizes` is hidden, and any size not specified in `constraints.excludedSizes` is shown.</span></span>
<span data-ttu-id="9191e-115">`constraints.allowedSizes` e `constraints.excludedSizes` são opcionais, mas não podem ser usados simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="9191e-115">`constraints.allowedSizes` and `constraints.excludedSizes` are both optional, but cannot be used simultaneously.</span></span> <span data-ttu-id="9191e-116">lista de saudação de tamanhos disponíveis pode ser determinada chamando [lista tamanhos de máquina virtual disponível para uma assinatura](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span><span class="sxs-lookup"><span data-stu-id="9191e-116">hello list of available sizes can be determined by calling [List available virtual machine sizes for a subscription](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span></span>
- <span data-ttu-id="9191e-117">`osPlatform` deve ser especificada e pode ser **Windows** ou **Linux**.</span><span class="sxs-lookup"><span data-stu-id="9191e-117">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span> <span data-ttu-id="9191e-118">Ele usou os custos de hardware de saudação toodetermine de máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="9191e-118">It's used toodetermine hello hardware costs of hello virtual machines.</span></span>
- <span data-ttu-id="9191e-119">`imageReference` é omitida para imagens próprias, mas fornecida para imagens de terceiros.</span><span class="sxs-lookup"><span data-stu-id="9191e-119">`imageReference` is omitted for first-party images, but provided for third-party images.</span></span> <span data-ttu-id="9191e-120">Ele usou os custos de software de saudação toodetermine de máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="9191e-120">It's used toodetermine hello software costs of hello virtual machines.</span></span>
- <span data-ttu-id="9191e-121">`count`é usado tooset Olá apropriado multiplicador para o elemento de saudação.</span><span class="sxs-lookup"><span data-stu-id="9191e-121">`count` is used tooset hello appropriate multiplier for hello element.</span></span> <span data-ttu-id="9191e-122">Ele dá suporte a um valor estático, como **2**, ou a um valor dinâmico de outro elemento, como `[steps('step1').vmCount]`.</span><span class="sxs-lookup"><span data-stu-id="9191e-122">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').vmCount]`.</span></span> <span data-ttu-id="9191e-123">valor padrão de saudação é **1**.</span><span class="sxs-lookup"><span data-stu-id="9191e-123">hello default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="9191e-124">Saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="9191e-124">Sample output</span></span>
```json
"Standard_D1"
```

## <a name="next-steps"></a><span data-ttu-id="9191e-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9191e-125">Next steps</span></span>
* <span data-ttu-id="9191e-126">Para aplicativos de toomanaged uma introdução, consulte [visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9191e-126">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="9191e-127">Para definições de interface do usuário de toocreating uma introdução, consulte [guia de Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9191e-127">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="9191e-128">Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="9191e-128">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
