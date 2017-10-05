---
title: "Elemento de interface do usuário DropDown de aplicativo gerenciado do Azure | Microsoft Docs"
description: "Descreve o elemento Microsoft.Common.DropDown da interface do usuário para aplicativos gerenciados do Azure"
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
ms.openlocfilehash: a769e14efbae928b811fa1f1b1c2d4fba3c7692b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommondropdown-ui-element"></a><span data-ttu-id="6b989-103">Elemento de interface do usuário Microsoft.Common.DropDown</span><span class="sxs-lookup"><span data-stu-id="6b989-103">Microsoft.Common.DropDown UI element</span></span>
<span data-ttu-id="6b989-104">Um controle de seleção com uma lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="6b989-104">A selection control with a dropdown list.</span></span> <span data-ttu-id="6b989-105">Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="6b989-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="6b989-106">Exemplo de interface do usuário</span><span class="sxs-lookup"><span data-stu-id="6b989-106">UI sample</span></span>
![Microsoft.Common.DropDown](./media/managed-application-elements/microsoft.common.dropdown.png)

## <a name="schema"></a><span data-ttu-id="6b989-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="6b989-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="6b989-109">Comentários</span><span class="sxs-lookup"><span data-stu-id="6b989-109">Remarks</span></span>
- <span data-ttu-id="6b989-110">O rótulo de `constraints.allowedValues` é o texto exibido para um item e seu valor é o valor de saída do elemento quando selecionado.</span><span class="sxs-lookup"><span data-stu-id="6b989-110">The label for `constraints.allowedValues` is the display text for an item, and its value is the output value of the element when selected.</span></span>
- <span data-ttu-id="6b989-111">Se especificado, o valor padrão deve ser um rótulo presente em `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="6b989-111">If specified, the default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="6b989-112">Se não for especificado, o primeiro item em `constraints.allowedValues` será selecionado.</span><span class="sxs-lookup"><span data-stu-id="6b989-112">If not specified, the first item in `constraints.allowedValues` is selected.</span></span> <span data-ttu-id="6b989-113">O valor padrão é **null**.</span><span class="sxs-lookup"><span data-stu-id="6b989-113">The default value is **null**.</span></span>
- <span data-ttu-id="6b989-114">`constraints.allowedValues` deve conter pelo menos um item.</span><span class="sxs-lookup"><span data-stu-id="6b989-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="6b989-115">Esse elemento não dá suporte à propriedade `constraints.required`.</span><span class="sxs-lookup"><span data-stu-id="6b989-115">This element doesn't support the `constraints.required` property.</span></span> <span data-ttu-id="6b989-116">Para emular esse comportamento, adicione um item com um rótulo e um valor de `""` (cadeia de caracteres vazia) a `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="6b989-116">To emulate this behavior, add an item with a label and value of `""` (empty string) to `constraints.allowedValues`.</span></span>

## <a name="sample-output"></a><span data-ttu-id="6b989-117">Saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="6b989-117">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="6b989-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6b989-118">Next steps</span></span>
* <span data-ttu-id="6b989-119">Para obter uma introdução aos aplicativos gerenciados, consulte [Visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6b989-119">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="6b989-120">Para obter uma introdução à criação de definições de interface do usuário, consulte [Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6b989-120">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="6b989-121">Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="6b989-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
