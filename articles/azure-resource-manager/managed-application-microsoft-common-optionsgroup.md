---
title: "Elemento de interface do usuário OptionsGroup de aplicativo gerenciado do Azure | Microsoft Docs"
description: "Descreve o elemento Microsoft.Common.OptionsGroup da interface do usuário para aplicativos gerenciados do Azure"
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
ms.openlocfilehash: 6e147ed28c8248f7f17cb36fd7ae13468141dced
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonoptionsgroup-ui-element"></a><span data-ttu-id="c9ff4-103">Elemento de interface do usuário Microsoft.Common.OptionsGroup</span><span class="sxs-lookup"><span data-stu-id="c9ff4-103">Microsoft.Common.OptionsGroup UI element</span></span>
<span data-ttu-id="c9ff4-104">Um controle de seleção com uma linha de opções disponíveis.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-104">A selection control with a row of available options.</span></span> <span data-ttu-id="c9ff4-105">Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="c9ff4-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="c9ff4-106">Exemplo de interface do usuário</span><span class="sxs-lookup"><span data-stu-id="c9ff4-106">UI sample</span></span>
![Microsoft.Common.OptionsGroup](./media/managed-application-elements/microsoft.common.optionsgroup.png)

## <a name="schema"></a><span data-ttu-id="c9ff4-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="c9ff4-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.OptionsGroup",
  "label": "Some options group",
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

## <a name="remarks"></a><span data-ttu-id="c9ff4-109">Comentários</span><span class="sxs-lookup"><span data-stu-id="c9ff4-109">Remarks</span></span>
- <span data-ttu-id="c9ff4-110">O rótulo de `constraints.allowedValues` é o texto exibido para um item e seu valor é o valor de saída do elemento quando selecionado.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-110">The label for `constraints.allowedValues` is the display text for an item, and its value is the output value of the element when selected.</span></span>
- <span data-ttu-id="c9ff4-111">Se especificado, o valor padrão deve ser um rótulo presente em `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-111">If specified, the default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="c9ff4-112">Se não for especificado, o primeiro item em `constraints.allowedValues` será selecionado por padrão.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-112">If not specified, the first item in `constraints.allowedValues` is selected by default.</span></span> <span data-ttu-id="c9ff4-113">O valor padrão é **null**.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-113">The default value is **null**.</span></span>
- <span data-ttu-id="c9ff4-114">`constraints.allowedValues` deve conter pelo menos um item.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="c9ff4-115">Esse elemento não dá suporte à propriedade `constraints.required`; um item deve ser selecionado para validar com êxito.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-115">This element doesn't support the `constraints.required` property; an item must be selected to validate successfully.</span></span>

## <a name="sample-output"></a><span data-ttu-id="c9ff4-116">Saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="c9ff4-116">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="c9ff4-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c9ff4-117">Next steps</span></span>
* <span data-ttu-id="c9ff4-118">Para obter uma introdução aos aplicativos gerenciados, consulte [Visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c9ff4-118">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="c9ff4-119">Para obter uma introdução à criação de definições de interface do usuário, consulte [Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c9ff4-119">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="c9ff4-120">Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="c9ff4-120">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
