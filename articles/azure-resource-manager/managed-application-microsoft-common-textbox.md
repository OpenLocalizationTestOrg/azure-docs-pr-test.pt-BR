---
title: "Elemento de interface do usuário TextBox de aplicativo gerenciado do Azure | Microsoft Docs"
description: "Descreve o elemento Microsoft.Common.TextBox da interface do usuário para aplicativos gerenciados do Azure"
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
ms.openlocfilehash: 5a0ac5b811812c8c03f7f63aae12b8699d248ebf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommontextbox-ui-element"></a><span data-ttu-id="a6c30-103">Elemento de interface do usuário Microsoft.Common.TextBox</span><span class="sxs-lookup"><span data-stu-id="a6c30-103">Microsoft.Common.TextBox UI element</span></span>
<span data-ttu-id="a6c30-104">Um controle que pode ser usado para editar texto não formatado.</span><span class="sxs-lookup"><span data-stu-id="a6c30-104">A control that can be used to edit unformatted text.</span></span> <span data-ttu-id="a6c30-105">Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="a6c30-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="a6c30-106">Exemplo de interface do usuário</span><span class="sxs-lookup"><span data-stu-id="a6c30-106">UI sample</span></span>
![Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a><span data-ttu-id="a6c30-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="a6c30-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Halp!",
  "constraints": {
    "required": true,
    "regex": "^[a-z0-9A-Z]{1,30}$",
    "validationMessage": "Only alphanumeric characters are allowed, and the value must be 1-30 characters long."
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="a6c30-109">Comentários</span><span class="sxs-lookup"><span data-stu-id="a6c30-109">Remarks</span></span>
- <span data-ttu-id="a6c30-110">Se `constraints.required` é definido como **true**, a caixa de texto deve conter um valor a ser validado com êxito.</span><span class="sxs-lookup"><span data-stu-id="a6c30-110">If `constraints.required` is set to **true**, then the text box must contain a value to validate successfully.</span></span> <span data-ttu-id="a6c30-111">O valor padrão é **false**.</span><span class="sxs-lookup"><span data-stu-id="a6c30-111">The default value is **false**.</span></span>
- <span data-ttu-id="a6c30-112">`constraints.regex` é um padrão de expressão regular JavaScript.</span><span class="sxs-lookup"><span data-stu-id="a6c30-112">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="a6c30-113">Se especificado, o valor da caixa de texto deve corresponder ao padrão para validar com êxito.</span><span class="sxs-lookup"><span data-stu-id="a6c30-113">If specified, then the text box's value must match the pattern to validate successfully.</span></span> <span data-ttu-id="a6c30-114">O valor padrão é **null**.</span><span class="sxs-lookup"><span data-stu-id="a6c30-114">The default value is **null**.</span></span>
- <span data-ttu-id="a6c30-115">`constraints.validationMessage` é uma cadeia de caracteres a ser exibida quando o valor da caixa de texto falha na validação.</span><span class="sxs-lookup"><span data-stu-id="a6c30-115">`constraints.validationMessage` is a string to display when the text box's value fails validation.</span></span> <span data-ttu-id="a6c30-116">Se não for especificado, as mensagens de validação internas da caixa de texto serão usadas.</span><span class="sxs-lookup"><span data-stu-id="a6c30-116">If not specified, then the text box's built-in validation messages are used.</span></span> <span data-ttu-id="a6c30-117">O valor padrão é **null**.</span><span class="sxs-lookup"><span data-stu-id="a6c30-117">The default value is **null**.</span></span>
- <span data-ttu-id="a6c30-118">É possível especificar um valor para `constraints.regex` quando `constraints.required` é definido como **false**.</span><span class="sxs-lookup"><span data-stu-id="a6c30-118">It's possible to specify a value for `constraints.regex` when `constraints.required` is set to **false**.</span></span> <span data-ttu-id="a6c30-119">Nesse cenário, um valor não é necessário para a caixa de texto validar com êxito.</span><span class="sxs-lookup"><span data-stu-id="a6c30-119">In this scenario, a value is not required for the text box to validate successfully.</span></span> <span data-ttu-id="a6c30-120">Se um valor for especificado, ele deve corresponder ao padrão da expressão regular.</span><span class="sxs-lookup"><span data-stu-id="a6c30-120">If one is specified, it must match the regular expression pattern.</span></span>

## <a name="sample-output"></a><span data-ttu-id="a6c30-121">Saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="a6c30-121">Sample output</span></span>

```json
"foobar"
```

## <a name="next-steps"></a><span data-ttu-id="a6c30-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a6c30-122">Next steps</span></span>
* <span data-ttu-id="a6c30-123">Para obter uma introdução aos aplicativos gerenciados, consulte [Visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a6c30-123">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="a6c30-124">Para obter uma introdução à criação de definições de interface do usuário, consulte [Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a6c30-124">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="a6c30-125">Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="a6c30-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
