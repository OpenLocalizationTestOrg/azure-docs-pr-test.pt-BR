---
title: "elemento de interface do usuário TextBox de aplicativo gerenciado aaaAzure | Microsoft Docs"
description: "Descreve Olá elemento Microsoft.Common.TextBox da interface do usuário para aplicativos gerenciados do Azure"
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
ms.openlocfilehash: 11771cd1d689b720384df98b8d1465703068af37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommontextbox-ui-element"></a><span data-ttu-id="cd4b9-103">Elemento de interface do usuário Microsoft.Common.TextBox</span><span class="sxs-lookup"><span data-stu-id="cd4b9-103">Microsoft.Common.TextBox UI element</span></span>
<span data-ttu-id="cd4b9-104">Um controle que pode ser usado tooedit texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="cd4b9-104">A control that can be used tooedit unformatted text.</span></span> <span data-ttu-id="cd4b9-105">Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="cd4b9-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="cd4b9-106">Exemplo de interface do usuário</span><span class="sxs-lookup"><span data-stu-id="cd4b9-106">UI sample</span></span>
![Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a><span data-ttu-id="cd4b9-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="cd4b9-108">Schema</span></span>
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
    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-30 characters long."
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="cd4b9-109">Comentários</span><span class="sxs-lookup"><span data-stu-id="cd4b9-109">Remarks</span></span>
- <span data-ttu-id="cd4b9-110">Se `constraints.required` está definido muito**true**, em seguida, a caixa de texto de saudação deve conter um valor toovalidate com êxito.</span><span class="sxs-lookup"><span data-stu-id="cd4b9-110">If `constraints.required` is set too**true**, then hello text box must contain a value toovalidate successfully.</span></span> <span data-ttu-id="cd4b9-111">valor padrão de saudação é **false**.</span><span class="sxs-lookup"><span data-stu-id="cd4b9-111">hello default value is **false**.</span></span>
- <span data-ttu-id="cd4b9-112">`constraints.regex` é um padrão de expressão regular JavaScript.</span><span class="sxs-lookup"><span data-stu-id="cd4b9-112">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="cd4b9-113">Se especificado, em seguida, valor da caixa de texto de saudação deve corresponder saudação padrão toovalidate com êxito.</span><span class="sxs-lookup"><span data-stu-id="cd4b9-113">If specified, then hello text box's value must match hello pattern toovalidate successfully.</span></span> <span data-ttu-id="cd4b9-114">O valor padrão é **null**.</span><span class="sxs-lookup"><span data-stu-id="cd4b9-114">The default value is **null**.</span></span>
- <span data-ttu-id="cd4b9-115">`constraints.validationMessage`é uma cadeia de caracteres toodisplay quando o valor da caixa de texto de saudação Falha na validação.</span><span class="sxs-lookup"><span data-stu-id="cd4b9-115">`constraints.validationMessage` is a string toodisplay when hello text box's value fails validation.</span></span> <span data-ttu-id="cd4b9-116">Se não for especificado, Olá validação interna da caixa de texto, as mensagens são usadas.</span><span class="sxs-lookup"><span data-stu-id="cd4b9-116">If not specified, then hello text box's built-in validation messages are used.</span></span> <span data-ttu-id="cd4b9-117">valor padrão de saudação é **nulo**.</span><span class="sxs-lookup"><span data-stu-id="cd4b9-117">hello default value is **null**.</span></span>
- <span data-ttu-id="cd4b9-118">Toospecify possíveis de é um valor para `constraints.regex` quando `constraints.required` está definido muito**false**.</span><span class="sxs-lookup"><span data-stu-id="cd4b9-118">It's possible toospecify a value for `constraints.regex` when `constraints.required` is set too**false**.</span></span> <span data-ttu-id="cd4b9-119">Nesse cenário, um valor não é necessário para toovalidate de caixa de texto de saudação com êxito.</span><span class="sxs-lookup"><span data-stu-id="cd4b9-119">In this scenario, a value is not required for hello text box toovalidate successfully.</span></span> <span data-ttu-id="cd4b9-120">Se um for especificado, o padrão de expressão regular Olá deve corresponder.</span><span class="sxs-lookup"><span data-stu-id="cd4b9-120">If one is specified, it must match hello regular expression pattern.</span></span>

## <a name="sample-output"></a><span data-ttu-id="cd4b9-121">Saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="cd4b9-121">Sample output</span></span>

```json
"foobar"
```

## <a name="next-steps"></a><span data-ttu-id="cd4b9-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cd4b9-122">Next steps</span></span>
* <span data-ttu-id="cd4b9-123">Para aplicativos de toomanaged uma introdução, consulte [visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cd4b9-123">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="cd4b9-124">Para definições de interface do usuário de toocreating uma introdução, consulte [guia de Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cd4b9-124">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="cd4b9-125">Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="cd4b9-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
