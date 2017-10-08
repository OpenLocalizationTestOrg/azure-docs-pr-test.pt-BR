---
title: "elemento de interface do usuário suspensa de aplicativo gerenciado aaaAzure | Microsoft Docs"
description: "Descreve Olá elemento Microsoft.Common.DropDown da interface do usuário para aplicativos gerenciados do Azure"
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
ms.openlocfilehash: 1c07a48ad66b8e8b7fd8f59561776ecb1fc6224f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommondropdown-ui-element"></a>Elemento de interface do usuário Microsoft.Common.DropDown
Um controle de seleção com uma lista suspensa. Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Exemplo de interface do usuário
![Microsoft.Common.DropDown](./media/managed-application-elements/microsoft.common.dropdown.png)

## <a name="schema"></a>Esquema
```json
{
  "name": "element1",
  "type": "Microsoft.Common.DropDown",
  "label": "Some drop down",
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
- Se especificado, o valor de padrão de saudação deve ser um rótulo presente no `constraints.allowedValues`. Se não for especificado, Olá primeiro item na `constraints.allowedValues` está selecionado. valor padrão de saudação é **nulo**.
- `constraints.allowedValues` deve conter pelo menos um item.
- Esse elemento não oferece suporte a saudação `constraints.required` propriedade. tooemulate esse comportamento, adicione um item com um rótulo e um valor de `""` (cadeia de caracteres vazia) muito`constraints.allowedValues`.

## <a name="sample-output"></a>Saída de exemplo
```json
"Bar"
```

## <a name="next-steps"></a>Próximas etapas
* Para aplicativos de toomanaged uma introdução, consulte [visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).
* Para definições de interface do usuário de toocreating uma introdução, consulte [guia de Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).
