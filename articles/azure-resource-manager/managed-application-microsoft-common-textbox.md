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
# <a name="microsoftcommontextbox-ui-element"></a>Elemento de interface do usuário Microsoft.Common.TextBox
Um controle que pode ser usado tooedit texto sem formatação. Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Exemplo de interface do usuário
![Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a>Esquema
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

## <a name="remarks"></a>Comentários
- Se `constraints.required` está definido muito**true**, em seguida, a caixa de texto de saudação deve conter um valor toovalidate com êxito. valor padrão de saudação é **false**.
- `constraints.regex` é um padrão de expressão regular JavaScript. Se especificado, em seguida, valor da caixa de texto de saudação deve corresponder saudação padrão toovalidate com êxito. O valor padrão é **null**.
- `constraints.validationMessage`é uma cadeia de caracteres toodisplay quando o valor da caixa de texto de saudação Falha na validação. Se não for especificado, Olá validação interna da caixa de texto, as mensagens são usadas. valor padrão de saudação é **nulo**.
- Toospecify possíveis de é um valor para `constraints.regex` quando `constraints.required` está definido muito**false**. Nesse cenário, um valor não é necessário para toovalidate de caixa de texto de saudação com êxito. Se um for especificado, o padrão de expressão regular Olá deve corresponder.

## <a name="sample-output"></a>Saída de exemplo

```json
"foobar"
```

## <a name="next-steps"></a>Próximas etapas
* Para aplicativos de toomanaged uma introdução, consulte [visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).
* Para definições de interface do usuário de toocreating uma introdução, consulte [guia de Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).
