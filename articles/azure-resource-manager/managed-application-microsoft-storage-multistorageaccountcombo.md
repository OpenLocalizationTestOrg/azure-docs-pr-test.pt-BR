---
title: "Elemento de interface do usuário MultiStorageAccountCombo de aplicativo gerenciado do Azure | Microsoft Docs"
description: "Descreve o elemento Microsoft.Storage.MultiStorageAccountCombo da interface do usuário para aplicativos gerenciados do Azure"
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
ms.openlocfilehash: 27843b116d949899e4eae65f342324f77ebca70b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftstoragemultistorageaccountcombo-ui-element"></a><span data-ttu-id="2d90f-103">Elemento de interface do usuário Microsoft.Storage.MultiStorageAccountCombo</span><span class="sxs-lookup"><span data-stu-id="2d90f-103">Microsoft.Storage.MultiStorageAccountCombo UI element</span></span>
<span data-ttu-id="2d90f-104">Um grupo de controles para criar várias contas de armazenamento com nomes que começam com um prefixo comum.</span><span class="sxs-lookup"><span data-stu-id="2d90f-104">A group of controls for creating multiple storage accounts, with names that start with a common prefix.</span></span> <span data-ttu-id="2d90f-105">Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="2d90f-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="2d90f-106">Exemplo de interface do usuário</span><span class="sxs-lookup"><span data-stu-id="2d90f-106">UI sample</span></span>
![Microsoft.Storage.MultiStorageAccountCombo](./media/managed-application-elements/microsoft.storage.multistorageaccountcombo.png)

## <a name="schema"></a><span data-ttu-id="2d90f-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="2d90f-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.MultiStorageAccountCombo",
  "label": {
    "prefix": "Storage account prefix",
    "type": "Storage account type"
  },
  "toolTip": {
    "prefix": "",
    "type": ""
  },
  "defaultValue": {
    "prefix": "sa",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="2d90f-109">Comentários</span><span class="sxs-lookup"><span data-stu-id="2d90f-109">Remarks</span></span>
- <span data-ttu-id="2d90f-110">O valor de `defaultValue.prefix` é concatenado com um ou mais números inteiros para gerar a sequência de nomes de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2d90f-110">The value for `defaultValue.prefix` is concatenated with one or more integers to generate the sequence of storage account names.</span></span> <span data-ttu-id="2d90f-111">Por exemplo, se `defaultValue.prefix` é **foobar** e `count` é **2**, os nomes de conta de armazenamento **foobar1** e **foobar2** são gerados.</span><span class="sxs-lookup"><span data-stu-id="2d90f-111">For example, if `defaultValue.prefix` is **foobar** and `count` is **2**, then storage account names **foobar1** and **foobar2** are generated.</span></span> <span data-ttu-id="2d90f-112">Os nomes de conta de armazenamento gerados são validados por exclusividade automaticamente.</span><span class="sxs-lookup"><span data-stu-id="2d90f-112">Generated storage account names are validated for uniqueness automatically.</span></span>
- <span data-ttu-id="2d90f-113">Os nomes de conta de armazenamento são gerados lexicograficamente com base em `count`.</span><span class="sxs-lookup"><span data-stu-id="2d90f-113">The storage account names are generated lexicographically based on `count`.</span></span> <span data-ttu-id="2d90f-114">Por exemplo, se `count` for 10, os nomes de conta de armazenamento terminarão com números inteiros de 2 dígitos (01, 02, 03, etc.).</span><span class="sxs-lookup"><span data-stu-id="2d90f-114">For example, if `count` is 10, then the storage account names end with 2-digit integers (01, 02, 03, etc.).</span></span>
- <span data-ttu-id="2d90f-115">O valor padrão de `defaultValue.prefix` é **null**e `defaultValue.type` é **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="2d90f-115">The default value for `defaultValue.prefix` is **null**, and for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="2d90f-116">Os tipos não especificados em `constraints.allowedTypes` ficam ocultos e os tipos não especificados em `constraints.excludedTypes` são mostrados.</span><span class="sxs-lookup"><span data-stu-id="2d90f-116">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="2d90f-117">`constraints.allowedTypes` e `constraints.excludedTypes` são opcionais, mas não podem ser usados simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="2d90f-117">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="2d90f-118">Além de gerar nomes de conta de armazenamento, `count` é usado para definir o multiplicador apropriado para o elemento.</span><span class="sxs-lookup"><span data-stu-id="2d90f-118">In addition to generating storage account names, `count` is used to set the appropriate multiplier for the element.</span></span> <span data-ttu-id="2d90f-119">Ele dá suporte a um valor estático, como **2**, ou a um valor dinâmico de outro elemento, como `[steps('step1').storageAccountCount]`.</span><span class="sxs-lookup"><span data-stu-id="2d90f-119">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').storageAccountCount]`.</span></span> <span data-ttu-id="2d90f-120">O valor padrão é **1**.</span><span class="sxs-lookup"><span data-stu-id="2d90f-120">The default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="2d90f-121">Saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="2d90f-121">Sample output</span></span>
```json
{
  "prefix": "sa",
  "count": 2,
  "resourceGroup": "rg01",
  "type": "Premium_LRS"
}
```

## <a name="next-steps"></a><span data-ttu-id="2d90f-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2d90f-122">Next steps</span></span>
* <span data-ttu-id="2d90f-123">Para obter uma introdução aos aplicativos gerenciados, consulte [Visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2d90f-123">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="2d90f-124">Para obter uma introdução à criação de definições de interface do usuário, consulte [Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2d90f-124">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="2d90f-125">Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="2d90f-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
