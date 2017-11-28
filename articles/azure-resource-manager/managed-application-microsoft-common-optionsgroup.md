---
title: "elemento de interface do usuário OptionsGroup de aplicativo gerenciado aaaAzure | Microsoft Docs"
description: "Descreve Olá elemento Microsoft.Common.OptionsGroup da interface do usuário para aplicativos gerenciados do Azure"
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
ms.openlocfilehash: e222468009c8db567bdde9f42836a48fb791da00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonoptionsgroup-ui-element"></a><span data-ttu-id="b8d87-103">Elemento de interface do usuário Microsoft.Common.OptionsGroup</span><span class="sxs-lookup"><span data-stu-id="b8d87-103">Microsoft.Common.OptionsGroup UI element</span></span>
<span data-ttu-id="b8d87-104">Um controle de seleção com uma linha de opções disponíveis.</span><span class="sxs-lookup"><span data-stu-id="b8d87-104">A selection control with a row of available options.</span></span> <span data-ttu-id="b8d87-105">Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="b8d87-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="b8d87-106">Exemplo de interface do usuário</span><span class="sxs-lookup"><span data-stu-id="b8d87-106">UI sample</span></span>
![Microsoft.Common.OptionsGroup](./media/managed-application-elements/microsoft.common.optionsgroup.png)

## <a name="schema"></a><span data-ttu-id="b8d87-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="b8d87-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="b8d87-109">Comentários</span><span class="sxs-lookup"><span data-stu-id="b8d87-109">Remarks</span></span>
- <span data-ttu-id="b8d87-110">rótulo de saudação para `constraints.allowedValues` é Olá texto de exibição para um item e seu valor é o valor de saída de saudação do elemento de saudação quando selecionado.</span><span class="sxs-lookup"><span data-stu-id="b8d87-110">hello label for `constraints.allowedValues` is hello display text for an item, and its value is hello output value of hello element when selected.</span></span>
- <span data-ttu-id="b8d87-111">Se especificado, o valor de padrão de saudação deve ser um rótulo presente no `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="b8d87-111">If specified, hello default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="b8d87-112">Se não for especificado, Olá primeiro item na `constraints.allowedValues` é selecionada por padrão.</span><span class="sxs-lookup"><span data-stu-id="b8d87-112">If not specified, hello first item in `constraints.allowedValues` is selected by default.</span></span> <span data-ttu-id="b8d87-113">valor padrão de saudação é **nulo**.</span><span class="sxs-lookup"><span data-stu-id="b8d87-113">hello default value is **null**.</span></span>
- <span data-ttu-id="b8d87-114">`constraints.allowedValues` deve conter pelo menos um item.</span><span class="sxs-lookup"><span data-stu-id="b8d87-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="b8d87-115">Esse elemento não oferece suporte a saudação `constraints.required` propriedade; um item deve ser selecionado toovalidate com êxito.</span><span class="sxs-lookup"><span data-stu-id="b8d87-115">This element doesn't support hello `constraints.required` property; an item must be selected toovalidate successfully.</span></span>

## <a name="sample-output"></a><span data-ttu-id="b8d87-116">Saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="b8d87-116">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="b8d87-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b8d87-117">Next steps</span></span>
* <span data-ttu-id="b8d87-118">Para aplicativos de toomanaged uma introdução, consulte [visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b8d87-118">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="b8d87-119">Para definições de interface do usuário de toocreating uma introdução, consulte [guia de Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b8d87-119">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="b8d87-120">Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="b8d87-120">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
