---
title: "elemento de interface do usuário PasswordBox de aplicativo gerenciado aaaAzure | Microsoft Docs"
description: "Descreve Olá elemento Microsoft.Common.PasswordBox da interface do usuário para aplicativos gerenciados do Azure"
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
ms.openlocfilehash: bcb1f54c0bee464075ed732ead9aa3f88697f49e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonpasswordbox-ui-element"></a><span data-ttu-id="a303d-103">Elemento de interface do usuário Microsoft.Common.PasswordBox</span><span class="sxs-lookup"><span data-stu-id="a303d-103">Microsoft.Common.PasswordBox UI element</span></span>
<span data-ttu-id="a303d-104">Um controle que pode ser usado tooprovide e confirme uma senha.</span><span class="sxs-lookup"><span data-stu-id="a303d-104">A control that can be used tooprovide and confirm a password.</span></span> <span data-ttu-id="a303d-105">Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="a303d-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="a303d-106">Exemplo de interface do usuário</span><span class="sxs-lookup"><span data-stu-id="a303d-106">UI sample</span></span>
![Microsoft.Common.PasswordBox](./media/managed-application-elements/microsoft.common.passwordbox.png)

## <a name="schema"></a><span data-ttu-id="a303d-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="a303d-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="a303d-109">Comentários</span><span class="sxs-lookup"><span data-stu-id="a303d-109">Remarks</span></span>
- <span data-ttu-id="a303d-110">Esse elemento não oferece suporte a saudação `defaultValue` propriedade.</span><span class="sxs-lookup"><span data-stu-id="a303d-110">This element doesn't support hello `defaultValue` property.</span></span>
- <span data-ttu-id="a303d-111">Para obter detalhes sobre a implementação de `constraints`, consulte [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span><span class="sxs-lookup"><span data-stu-id="a303d-111">For implementation details of `constraints`, see [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span></span>
- <span data-ttu-id="a303d-112">Se `options.hideConfirmation` está definido muito**true**, segunda caixa de texto Olá para confirmar a senha do usuário hello está oculto.</span><span class="sxs-lookup"><span data-stu-id="a303d-112">If `options.hideConfirmation` is set too**true**, hello second text box for confirming hello user's password is hidden.</span></span> <span data-ttu-id="a303d-113">valor padrão de saudação é **false**.</span><span class="sxs-lookup"><span data-stu-id="a303d-113">hello default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="a303d-114">Saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="a303d-114">Sample output</span></span>
```json
"p4ssw0rd"
```

## <a name="next-steps"></a><span data-ttu-id="a303d-115">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a303d-115">Next steps</span></span>
* <span data-ttu-id="a303d-116">Para aplicativos de toomanaged uma introdução, consulte [visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a303d-116">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="a303d-117">Para definições de interface do usuário de toocreating uma introdução, consulte [guia de Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a303d-117">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="a303d-118">Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="a303d-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
