---
title: "elemento de interface do usuário suspensa de aplicativo gerenciado aaaAzure | Microsoft Docs"
description: "Descreve Olá elemento Microsoft.Common.DropDown da interface do usuário para aplicativos gerenciados do Azure"
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
ms.openlocfilehash: 1c07a48ad66b8e8b7fd8f59561776ecb1fc6224f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommondropdown-ui-element"></a><span data-ttu-id="72cf4-103">Elemento de interface do usuário Microsoft.Common.DropDown</span><span class="sxs-lookup"><span data-stu-id="72cf4-103">Microsoft.Common.DropDown UI element</span></span>
<span data-ttu-id="72cf4-104">Um controle de seleção com uma lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="72cf4-104">A selection control with a dropdown list.</span></span> <span data-ttu-id="72cf4-105">Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="72cf4-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="72cf4-106">Exemplo de interface do usuário</span><span class="sxs-lookup"><span data-stu-id="72cf4-106">UI sample</span></span>
![Microsoft.Common.DropDown](./media/managed-application-elements/microsoft.common.dropdown.png)

## <a name="schema"></a><span data-ttu-id="72cf4-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="72cf4-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.DropDown",
  "label": "Some drop down",
  "defaultValue": "Foo",
  "toolTip": "",
  "constraints": {
    "allowedValues": [
      {
        "label": "Foo",
        "value": "Bar"
      },
      {
        "label": "Baz",
        "value": "Qux"
      }
    ]
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="72cf4-109">Comentários</span><span class="sxs-lookup"><span data-stu-id="72cf4-109">Remarks</span></span>
- <span data-ttu-id="72cf4-110">rótulo de saudação para `constraints.allowedValues` é Olá texto de exibição para um item e seu valor é o valor de saída de saudação do elemento de saudação quando selecionado.</span><span class="sxs-lookup"><span data-stu-id="72cf4-110">hello label for `constraints.allowedValues` is hello display text for an item, and its value is hello output value of hello element when selected.</span></span>
- <span data-ttu-id="72cf4-111">Se especificado, o valor de padrão de saudação deve ser um rótulo presente no `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="72cf4-111">If specified, hello default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="72cf4-112">Se não for especificado, Olá primeiro item na `constraints.allowedValues` está selecionado.</span><span class="sxs-lookup"><span data-stu-id="72cf4-112">If not specified, hello first item in `constraints.allowedValues` is selected.</span></span> <span data-ttu-id="72cf4-113">valor padrão de saudação é **nulo**.</span><span class="sxs-lookup"><span data-stu-id="72cf4-113">hello default value is **null**.</span></span>
- <span data-ttu-id="72cf4-114">`constraints.allowedValues` deve conter pelo menos um item.</span><span class="sxs-lookup"><span data-stu-id="72cf4-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="72cf4-115">Esse elemento não oferece suporte a saudação `constraints.required` propriedade.</span><span class="sxs-lookup"><span data-stu-id="72cf4-115">This element doesn't support hello `constraints.required` property.</span></span> <span data-ttu-id="72cf4-116">tooemulate esse comportamento, adicione um item com um rótulo e um valor de `""` (cadeia de caracteres vazia) muito`constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="72cf4-116">tooemulate this behavior, add an item with a label and value of `""` (empty string) too`constraints.allowedValues`.</span></span>

## <a name="sample-output"></a><span data-ttu-id="72cf4-117">Saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="72cf4-117">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="72cf4-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="72cf4-118">Next steps</span></span>
* <span data-ttu-id="72cf4-119">Para aplicativos de toomanaged uma introdução, consulte [visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="72cf4-119">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="72cf4-120">Para definições de interface do usuário de toocreating uma introdução, consulte [guia de Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="72cf4-120">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="72cf4-121">Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="72cf4-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
