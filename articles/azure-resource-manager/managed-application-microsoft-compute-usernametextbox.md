---
title: "elemento de interface do usuário UserNameTextBox de aplicativo gerenciado aaaAzure | Microsoft Docs"
description: "Descreve Olá elemento Microsoft.Compute.UserNameTextBox da interface do usuário para aplicativos gerenciados do Azure"
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
ms.openlocfilehash: 33092014e804c4aabd56ba49144d9cd4d6a5fd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputeusernametextbox-ui-element"></a><span data-ttu-id="9151e-103">Elemento de interface do usuário Microsoft.Compute.UserNameTextBox</span><span class="sxs-lookup"><span data-stu-id="9151e-103">Microsoft.Compute.UserNameTextBox UI element</span></span>
<span data-ttu-id="9151e-104">Um controle de caixa de texto com validação interna para nomes de usuário do Windows e do Linux.</span><span class="sxs-lookup"><span data-stu-id="9151e-104">A text box control with built-in validation for Windows and Linux user names.</span></span> <span data-ttu-id="9151e-105">Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="9151e-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="9151e-106">Exemplo de interface do usuário</span><span class="sxs-lookup"><span data-stu-id="9151e-106">UI sample</span></span>
![Microsoft.Compute.UserNameTextBox](./media/managed-application-elements/microsoft.compute.usernametextbox.png)

## <a name="schema"></a><span data-ttu-id="9151e-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="9151e-108">Schema</span></span>
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
    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-30 characters long."
  },
  "osPlatform": "Windows",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="9151e-109">Comentários</span><span class="sxs-lookup"><span data-stu-id="9151e-109">Remarks</span></span>
- <span data-ttu-id="9151e-110">Se `constraints.required` está definido muito**true**, em seguida, a caixa de texto de saudação deve conter um valor toovalidate com êxito.</span><span class="sxs-lookup"><span data-stu-id="9151e-110">If `constraints.required` is set too**true**, then hello text box must contain a value toovalidate successfully.</span></span> <span data-ttu-id="9151e-111">valor padrão de saudação é **true**.</span><span class="sxs-lookup"><span data-stu-id="9151e-111">hello default value is **true**.</span></span>
- <span data-ttu-id="9151e-112">`osPlatform` deve ser especificada e pode ser **Windows** ou **Linux**.</span><span class="sxs-lookup"><span data-stu-id="9151e-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="9151e-113">`constraints.regex` é um padrão de expressão regular JavaScript.</span><span class="sxs-lookup"><span data-stu-id="9151e-113">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="9151e-114">Se especificado, em seguida, valor da caixa de texto de saudação deve corresponder saudação padrão toovalidate com êxito.</span><span class="sxs-lookup"><span data-stu-id="9151e-114">If specified, then hello text box's value must match hello pattern toovalidate successfully.</span></span> <span data-ttu-id="9151e-115">O valor padrão é **null**.</span><span class="sxs-lookup"><span data-stu-id="9151e-115">The default value is **null**.</span></span>
- <span data-ttu-id="9151e-116">`constraints.validationMessage`é uma cadeia de caracteres toodisplay quando o valor da caixa de texto de saudação Falha na validação de saudação especificada pelo `constraints.regex`.</span><span class="sxs-lookup"><span data-stu-id="9151e-116">`constraints.validationMessage` is a string toodisplay when hello text box's value fails hello validation specified by `constraints.regex`.</span></span> <span data-ttu-id="9151e-117">Se não for especificado, Olá validação interna da caixa de texto, as mensagens são usadas.</span><span class="sxs-lookup"><span data-stu-id="9151e-117">If not specified, then hello text box's built-in validation messages are used.</span></span> <span data-ttu-id="9151e-118">valor padrão de saudação é **nulo**.</span><span class="sxs-lookup"><span data-stu-id="9151e-118">hello default value is **null**.</span></span>
- <span data-ttu-id="9151e-119">Este elemento tem validação interna que é baseada no valor de saudação especificado para `osPlatform`.</span><span class="sxs-lookup"><span data-stu-id="9151e-119">This element has built-in validation that is based on hello value specified for `osPlatform`.</span></span> <span data-ttu-id="9151e-120">validação interna Olá pode ser usada junto com uma expressão regular personalizada.</span><span class="sxs-lookup"><span data-stu-id="9151e-120">hello built-in validation can be used along with a custom regular expression.</span></span>
<span data-ttu-id="9151e-121">Se um valor para `constraints.regex` for especificado, ambos Olá internas e personalizadas validações são disparadas.</span><span class="sxs-lookup"><span data-stu-id="9151e-121">If a value for `constraints.regex` is specified, then both hello built-in and custom validations are triggered.</span></span>

## <a name="sample-output"></a><span data-ttu-id="9151e-122">Saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="9151e-122">Sample output</span></span>
```json
"tabrezm"
```

## <a name="next-steps"></a><span data-ttu-id="9151e-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9151e-123">Next steps</span></span>
* <span data-ttu-id="9151e-124">Para aplicativos de toomanaged uma introdução, consulte [visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9151e-124">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="9151e-125">Para definições de interface do usuário de toocreating uma introdução, consulte [guia de Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9151e-125">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="9151e-126">Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="9151e-126">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
