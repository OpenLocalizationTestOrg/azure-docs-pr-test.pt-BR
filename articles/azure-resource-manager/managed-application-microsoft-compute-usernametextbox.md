---
title: "Elemento de interface do usuário UserNameTextBox de aplicativo gerenciado do Azure | Microsoft Docs"
description: "Descreve o elemento Microsoft.Common.UserNameTextBox da interface do usuário para aplicativos gerenciados do Azure"
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
ms.openlocfilehash: c90be5a0ed3aadda81d7ec9b5388a96472f69af0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcomputeusernametextbox-ui-element"></a><span data-ttu-id="424c2-103">Elemento de interface do usuário Microsoft.Compute.UserNameTextBox</span><span class="sxs-lookup"><span data-stu-id="424c2-103">Microsoft.Compute.UserNameTextBox UI element</span></span>
<span data-ttu-id="424c2-104">Um controle de caixa de texto com validação interna para nomes de usuário do Windows e do Linux.</span><span class="sxs-lookup"><span data-stu-id="424c2-104">A text box control with built-in validation for Windows and Linux user names.</span></span> <span data-ttu-id="424c2-105">Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="424c2-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="424c2-106">Exemplo de interface do usuário</span><span class="sxs-lookup"><span data-stu-id="424c2-106">UI sample</span></span>
![Microsoft.Compute.UserNameTextBox](./media/managed-application-elements/microsoft.compute.usernametextbox.png)

## <a name="schema"></a><span data-ttu-id="424c2-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="424c2-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.UserNameTextBox",
  "label": "User name",
  "defaultValue": "",
  "toolTip": "",
  "constraints": {
    "required": true,
    "regex": "^[a-z0-9A-Z]{1,30}$",
    "validationMessage": "Only alphanumeric characters are allowed, and the value must be 1-30 characters long."
  },
  "osPlatform": "Windows",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="424c2-109">Comentários</span><span class="sxs-lookup"><span data-stu-id="424c2-109">Remarks</span></span>
- <span data-ttu-id="424c2-110">Se `constraints.required` é definido como **true**, a caixa de texto deve conter um valor a ser validado com êxito.</span><span class="sxs-lookup"><span data-stu-id="424c2-110">If `constraints.required` is set to **true**, then the text box must contain a value to validate successfully.</span></span> <span data-ttu-id="424c2-111">O valor padrão é **true**.</span><span class="sxs-lookup"><span data-stu-id="424c2-111">The default value is **true**.</span></span>
- <span data-ttu-id="424c2-112">`osPlatform` deve ser especificada e pode ser **Windows** ou **Linux**.</span><span class="sxs-lookup"><span data-stu-id="424c2-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="424c2-113">`constraints.regex` é um padrão de expressão regular JavaScript.</span><span class="sxs-lookup"><span data-stu-id="424c2-113">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="424c2-114">Se especificado, o valor da caixa de texto deve corresponder ao padrão para validar com êxito.</span><span class="sxs-lookup"><span data-stu-id="424c2-114">If specified, then the text box's value must match the pattern to validate successfully.</span></span> <span data-ttu-id="424c2-115">O valor padrão é **null**.</span><span class="sxs-lookup"><span data-stu-id="424c2-115">The default value is **null**.</span></span>
- <span data-ttu-id="424c2-116">`constraints.validationMessage` é uma cadeia de caracteres a ser exibida quando o valor da caixa de texto falha a validação especificada por `constraints.regex`.</span><span class="sxs-lookup"><span data-stu-id="424c2-116">`constraints.validationMessage` is a string to display when the text box's value fails the validation specified by `constraints.regex`.</span></span> <span data-ttu-id="424c2-117">Se não for especificado, as mensagens de validação internas da caixa de texto serão usadas.</span><span class="sxs-lookup"><span data-stu-id="424c2-117">If not specified, then the text box's built-in validation messages are used.</span></span> <span data-ttu-id="424c2-118">O valor padrão é **null**.</span><span class="sxs-lookup"><span data-stu-id="424c2-118">The default value is **null**.</span></span>
- <span data-ttu-id="424c2-119">Este elemento tem validação interna com base no valor especificado para `osPlatform`.</span><span class="sxs-lookup"><span data-stu-id="424c2-119">This element has built-in validation that is based on the value specified for `osPlatform`.</span></span> <span data-ttu-id="424c2-120">A validação interna pode ser usada juntamente com uma expressão regular personalizada.</span><span class="sxs-lookup"><span data-stu-id="424c2-120">The built-in validation can be used along with a custom regular expression.</span></span>
<span data-ttu-id="424c2-121">Se um valor para `constraints.regex` for especificado, as validações internas e personalizadas serão disparadas.</span><span class="sxs-lookup"><span data-stu-id="424c2-121">If a value for `constraints.regex` is specified, then both the built-in and custom validations are triggered.</span></span>

## <a name="sample-output"></a><span data-ttu-id="424c2-122">Saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="424c2-122">Sample output</span></span>
```json
"tabrezm"
```

## <a name="next-steps"></a><span data-ttu-id="424c2-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="424c2-123">Next steps</span></span>
* <span data-ttu-id="424c2-124">Para obter uma introdução aos aplicativos gerenciados, consulte [Visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="424c2-124">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="424c2-125">Para obter uma introdução à criação de definições de interface do usuário, consulte [Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="424c2-125">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="424c2-126">Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="424c2-126">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
