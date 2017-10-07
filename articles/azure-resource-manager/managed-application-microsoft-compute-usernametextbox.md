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
# <a name="microsoftcomputeusernametextbox-ui-element"></a>Elemento de interface do usuário Microsoft.Compute.UserNameTextBox
Um controle de caixa de texto com validação interna para nomes de usuário do Windows e do Linux. Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Exemplo de interface do usuário
![Microsoft.Compute.UserNameTextBox](./media/managed-application-elements/microsoft.compute.usernametextbox.png)

## <a name="schema"></a>Esquema
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

## <a name="remarks"></a>Comentários
- Se `constraints.required` está definido muito**true**, em seguida, a caixa de texto de saudação deve conter um valor toovalidate com êxito. valor padrão de saudação é **true**.
- `osPlatform` deve ser especificada e pode ser **Windows** ou **Linux**.
- `constraints.regex` é um padrão de expressão regular JavaScript. Se especificado, em seguida, valor da caixa de texto de saudação deve corresponder saudação padrão toovalidate com êxito. O valor padrão é **null**.
- `constraints.validationMessage`é uma cadeia de caracteres toodisplay quando o valor da caixa de texto de saudação Falha na validação de saudação especificada pelo `constraints.regex`. Se não for especificado, Olá validação interna da caixa de texto, as mensagens são usadas. valor padrão de saudação é **nulo**.
- Este elemento tem validação interna que é baseada no valor de saudação especificado para `osPlatform`. validação interna Olá pode ser usada junto com uma expressão regular personalizada.
Se um valor para `constraints.regex` for especificado, ambos Olá internas e personalizadas validações são disparadas.

## <a name="sample-output"></a>Saída de exemplo
```json
"tabrezm"
```

## <a name="next-steps"></a>Próximas etapas
* Para aplicativos de toomanaged uma introdução, consulte [visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).
* Para definições de interface do usuário de toocreating uma introdução, consulte [guia de Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).
