---
title: "elemento de interface do usuário seção de aplicativo gerenciado aaaAzure | Microsoft Docs"
description: "Descreve Olá elemento Microsoft.Common.Section da interface do usuário para aplicativos gerenciados do Azure"
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
ms.openlocfilehash: d20b365b12fab66177e1a12db2ebbeefe507212e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonsection-ui-element"></a><span data-ttu-id="0b917-103">Elemento de interface do usuário Microsoft.Common.Section</span><span class="sxs-lookup"><span data-stu-id="0b917-103">Microsoft.Common.Section UI element</span></span>
<span data-ttu-id="0b917-104">Um controle que agrupa um ou mais elementos em um título.</span><span class="sxs-lookup"><span data-stu-id="0b917-104">A control that groups one or more elements under a heading.</span></span> <span data-ttu-id="0b917-105">Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="0b917-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="0b917-106">Exemplo de interface do usuário</span><span class="sxs-lookup"><span data-stu-id="0b917-106">UI sample</span></span>
![Microsoft.Common.Section](./media/managed-application-elements/microsoft.common.section.png)

## <a name="schema"></a><span data-ttu-id="0b917-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="0b917-108">Schema</span></span>
```json
{
  "name": "section1",
  "type": "Microsoft.Common.Section",
  "label": "Some section",
  "elements": [
    {
      "name": "element1",
      "type": "Microsoft.Common.TextBox",
      "label": "Some text box 1"
    },
    {
      "name": "element2",
      "type": "Microsoft.Common.TextBox",
      "label": "Some text box 2"
    }
  ],
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="0b917-109">Comentários</span><span class="sxs-lookup"><span data-stu-id="0b917-109">Remarks</span></span>
- <span data-ttu-id="0b917-110">`elements` deve conter pelo menos um elemento e pode conter todos os tipos de elemento exceto `Microsoft.Common.Section`.</span><span class="sxs-lookup"><span data-stu-id="0b917-110">`elements` must contain at least one element, and can contain all element types except `Microsoft.Common.Section`.</span></span>
- <span data-ttu-id="0b917-111">Esse elemento não oferece suporte a saudação `toolTip` propriedade.</span><span class="sxs-lookup"><span data-stu-id="0b917-111">This element doesn't support hello `toolTip` property.</span></span>

## <a name="sample-output"></a><span data-ttu-id="0b917-112">Saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="0b917-112">Sample output</span></span>
<span data-ttu-id="0b917-113">Olá tooaccess valores de saída dos elementos no `elements`, use Olá [basics()](managed-application-createuidefinition-functions.md#basics) ou [steps()](managed-application-createuidefinition-functions.md#steps) funções e a notação de ponto:</span><span class="sxs-lookup"><span data-stu-id="0b917-113">tooaccess hello output values of elements in `elements`, use hello [basics()](managed-application-createuidefinition-functions.md#basics) or [steps()](managed-application-createuidefinition-functions.md#steps) functions and dot notation:</span></span>

```json
basics('section1').element1
```

<span data-ttu-id="0b917-114">Elementos do tipo `Microsoft.Common.Section` não têm nenhum valor de saída próprio.</span><span class="sxs-lookup"><span data-stu-id="0b917-114">Elements of type `Microsoft.Common.Section` have no output values themselves.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b917-115">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0b917-115">Next steps</span></span>
* <span data-ttu-id="0b917-116">Para aplicativos de toomanaged uma introdução, consulte [visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0b917-116">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="0b917-117">Para definições de interface do usuário de toocreating uma introdução, consulte [guia de Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0b917-117">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="0b917-118">Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="0b917-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
