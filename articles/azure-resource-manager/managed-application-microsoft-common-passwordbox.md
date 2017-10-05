---
title: "Elemento de interface do usuário PasswordBox de aplicativo gerenciado do Azure | Microsoft Docs"
description: "Descreve o elemento de interface do usuário Microsoft.Common.PasswordBox para aplicativos gerenciados do Azure"
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
ms.openlocfilehash: 196a4b8f77145f83e46b4b23e148bb3a9dffc1b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonpasswordbox-ui-element"></a><span data-ttu-id="0ebde-103">Elemento de interface do usuário Microsoft.Common.PasswordBox</span><span class="sxs-lookup"><span data-stu-id="0ebde-103">Microsoft.Common.PasswordBox UI element</span></span>
<span data-ttu-id="0ebde-104">Um controle que pode ser usado para fornecer e confirmar uma senha.</span><span class="sxs-lookup"><span data-stu-id="0ebde-104">A control that can be used to provide and confirm a password.</span></span> <span data-ttu-id="0ebde-105">Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="0ebde-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="0ebde-106">Exemplo de interface do usuário</span><span class="sxs-lookup"><span data-stu-id="0ebde-106">UI sample</span></span>
![Microsoft.Common.PasswordBox](./media/managed-application-elements/microsoft.common.passwordbox.png)

## <a name="schema"></a><span data-ttu-id="0ebde-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="0ebde-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.PasswordBox",
  "label": {
    "password": "Password",
    "confirmPassword": "Confirm password"
  },
  "toolTip": "",
  "constraints": {
    "required": true,
    "regex": "",
    "validationMessage": ""
  },
  "options": {
    "hideConfirmation": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="0ebde-109">Comentários</span><span class="sxs-lookup"><span data-stu-id="0ebde-109">Remarks</span></span>
- <span data-ttu-id="0ebde-110">Esse elemento não dá suporte à propriedade `defaultValue`.</span><span class="sxs-lookup"><span data-stu-id="0ebde-110">This element doesn't support the `defaultValue` property.</span></span>
- <span data-ttu-id="0ebde-111">Para obter detalhes sobre a implementação de `constraints`, consulte [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span><span class="sxs-lookup"><span data-stu-id="0ebde-111">For implementation details of `constraints`, see [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span></span>
- <span data-ttu-id="0ebde-112">Se `options.hideConfirmation` for definido como **true**, a segunda caixa de texto para confirmar a senha do usuário ficará oculta.</span><span class="sxs-lookup"><span data-stu-id="0ebde-112">If `options.hideConfirmation` is set to **true**, the second text box for confirming the user's password is hidden.</span></span> <span data-ttu-id="0ebde-113">O valor padrão é **false**.</span><span class="sxs-lookup"><span data-stu-id="0ebde-113">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="0ebde-114">Saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="0ebde-114">Sample output</span></span>
```json
"p4ssw0rd"
```

## <a name="next-steps"></a><span data-ttu-id="0ebde-115">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0ebde-115">Next steps</span></span>
* <span data-ttu-id="0ebde-116">Para obter uma introdução aos aplicativos gerenciados, consulte [Visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0ebde-116">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="0ebde-117">Para obter uma introdução à criação de definições de interface do usuário, consulte [Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0ebde-117">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="0ebde-118">Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="0ebde-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
