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
# <a name="microsoftcommonoptionsgroup-ui-element"></a>Elemento de interface do usuário Microsoft.Common.OptionsGroup
Um controle de seleção com uma linha de opções disponíveis. Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Exemplo de interface do usuário
![Microsoft.Common.OptionsGroup](./media/managed-application-elements/microsoft.common.optionsgroup.png)

## <a name="schema"></a>Esquema
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

## <a name="remarks"></a>Comentários
- rótulo de saudação para `constraints.allowedValues` é Olá texto de exibição para um item e seu valor é o valor de saída de saudação do elemento de saudação quando selecionado.
- Se especificado, o valor de padrão de saudação deve ser um rótulo presente no `constraints.allowedValues`. Se não for especificado, Olá primeiro item na `constraints.allowedValues` é selecionada por padrão. valor padrão de saudação é **nulo**.
- `constraints.allowedValues` deve conter pelo menos um item.
- Esse elemento não oferece suporte a saudação `constraints.required` propriedade; um item deve ser selecionado toovalidate com êxito.

## <a name="sample-output"></a>Saída de exemplo
```json
"Bar"
```

## <a name="next-steps"></a>Próximas etapas
* Para aplicativos de toomanaged uma introdução, consulte [visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).
* Para definições de interface do usuário de toocreating uma introdução, consulte [guia de Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).
