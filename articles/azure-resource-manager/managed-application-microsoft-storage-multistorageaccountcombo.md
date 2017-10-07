---
title: "elemento de interface do usuário MultiStorageAccountCombo de aplicativo gerenciado aaaAzure | Microsoft Docs"
description: "Descreve Olá elemento Microsoft.Storage.MultiStorageAccountCombo da interface do usuário para aplicativos gerenciados do Azure"
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
ms.openlocfilehash: 765be145b61c3dbf0a035a7a00aa18eee464a3eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftstoragemultistorageaccountcombo-ui-element"></a><span data-ttu-id="6e5a2-103">Elemento de interface do usuário Microsoft.Storage.MultiStorageAccountCombo</span><span class="sxs-lookup"><span data-stu-id="6e5a2-103">Microsoft.Storage.MultiStorageAccountCombo UI element</span></span>
<span data-ttu-id="6e5a2-104">Um grupo de controles para criar várias contas de armazenamento com nomes que começam com um prefixo comum.</span><span class="sxs-lookup"><span data-stu-id="6e5a2-104">A group of controls for creating multiple storage accounts, with names that start with a common prefix.</span></span> <span data-ttu-id="6e5a2-105">Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="6e5a2-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="6e5a2-106">Exemplo de interface do usuário</span><span class="sxs-lookup"><span data-stu-id="6e5a2-106">UI sample</span></span>
![Microsoft.Storage.MultiStorageAccountCombo](./media/managed-application-elements/microsoft.storage.multistorageaccountcombo.png)

## <a name="schema"></a><span data-ttu-id="6e5a2-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="6e5a2-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="6e5a2-109">Comentários</span><span class="sxs-lookup"><span data-stu-id="6e5a2-109">Remarks</span></span>
- <span data-ttu-id="6e5a2-110">Olá valor `defaultValue.prefix` é concatenado com um ou mais inteiros toogenerate Olá sequência de nomes de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6e5a2-110">hello value for `defaultValue.prefix` is concatenated with one or more integers toogenerate hello sequence of storage account names.</span></span> <span data-ttu-id="6e5a2-111">Por exemplo, se `defaultValue.prefix` é **foobar** e `count` é **2**, os nomes de conta de armazenamento **foobar1** e **foobar2** são gerados.</span><span class="sxs-lookup"><span data-stu-id="6e5a2-111">For example, if `defaultValue.prefix` is **foobar** and `count` is **2**, then storage account names **foobar1** and **foobar2** are generated.</span></span> <span data-ttu-id="6e5a2-112">Os nomes de conta de armazenamento gerados são validados por exclusividade automaticamente.</span><span class="sxs-lookup"><span data-stu-id="6e5a2-112">Generated storage account names are validated for uniqueness automatically.</span></span>
- <span data-ttu-id="6e5a2-113">os nomes de conta de armazenamento Olá gerados lexicograficamente com base em `count`.</span><span class="sxs-lookup"><span data-stu-id="6e5a2-113">hello storage account names are generated lexicographically based on `count`.</span></span> <span data-ttu-id="6e5a2-114">Por exemplo, se `count` for 10, nomes de conta de armazenamento Olá terminam com números inteiros de 2 dígitos (01, 02, 03, etc.).</span><span class="sxs-lookup"><span data-stu-id="6e5a2-114">For example, if `count` is 10, then hello storage account names end with 2-digit integers (01, 02, 03, etc.).</span></span>
- <span data-ttu-id="6e5a2-115">Olá valor padrão para `defaultValue.prefix` é **nulo**e para `defaultValue.type` é **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="6e5a2-115">hello default value for `defaultValue.prefix` is **null**, and for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="6e5a2-116">Os tipos não especificados em `constraints.allowedTypes` ficam ocultos e os tipos não especificados em `constraints.excludedTypes` são mostrados.</span><span class="sxs-lookup"><span data-stu-id="6e5a2-116">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="6e5a2-117">`constraints.allowedTypes` e `constraints.excludedTypes` são opcionais, mas não podem ser usados simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="6e5a2-117">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="6e5a2-118">Nomes de conta de armazenamento de toogenerating adição, `count` é tooset usado o multiplicador apropriado para o elemento de saudação.</span><span class="sxs-lookup"><span data-stu-id="6e5a2-118">In addition toogenerating storage account names, `count` is used tooset the appropriate multiplier for hello element.</span></span> <span data-ttu-id="6e5a2-119">Ele dá suporte a um valor estático, como **2**, ou a um valor dinâmico de outro elemento, como `[steps('step1').storageAccountCount]`.</span><span class="sxs-lookup"><span data-stu-id="6e5a2-119">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').storageAccountCount]`.</span></span> <span data-ttu-id="6e5a2-120">valor padrão de saudação é **1**.</span><span class="sxs-lookup"><span data-stu-id="6e5a2-120">hello default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="6e5a2-121">Saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="6e5a2-121">Sample output</span></span>
```json
{
  "prefix": "sa",
  "count": 2,
  "resourceGroup": "rg01",
  "type": "Premium_LRS"
}
```

## <a name="next-steps"></a><span data-ttu-id="6e5a2-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6e5a2-122">Next steps</span></span>
* <span data-ttu-id="6e5a2-123">Para aplicativos de toomanaged uma introdução, consulte [visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6e5a2-123">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="6e5a2-124">Para definições de interface do usuário de toocreating uma introdução, consulte [guia de Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6e5a2-124">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="6e5a2-125">Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="6e5a2-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
