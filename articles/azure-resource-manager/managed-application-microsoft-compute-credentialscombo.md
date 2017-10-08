---
title: "elemento de interface do usuário CredentialsCombo de aplicativo gerenciado aaaAzure | Microsoft Docs"
description: "Descreve Olá elemento Microsoft.Compute.CredentialsCombo da interface do usuário para aplicativos gerenciados do Azure"
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
ms.openlocfilehash: d44a3929ebb7a5ff78b72f9eaeb6e52b098e266f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputecredentialscombo-ui-element"></a>Elemento de interface do usuário Microsoft.Compute.CredentialsCombo
Um grupo de controles com validação interna para chaves públicas SSH e senhas Windows e Linux. Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Exemplo de interface do usuário
![Microsoft.Compute.CredentialsCombo](./media/managed-application-elements/microsoft.compute.credentialscombo.png)

## <a name="schema"></a>Esquema
Se `osPlatform` é **Windows**, hello esquema a seguir será usada:
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.CredentialsCombo",
  "label": {
    "password": "Password",
    "confirmPassword": "Confirm password"
  },
  "toolTip": {
    "password": ""
  },
  "constraints": {
    "required": true,
    "customPasswordRegex": "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
    "customValidationMessage": "hello password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false
  },
  "osPlatform": "Windows",
  "visible": true
}
```

Se `osPlatform` é **Linux**, hello esquema a seguir será usada:
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.CredentialsCombo",
  "label": {
    "authenticationType": "Authentication type",
    "password": "Password",
    "confirmPassword": "Confirm password",
    "sshPublicKey": "SSH public key"
  },
  "toolTip": {
    "authenticationType": "",
    "password": "",
    "sshPublicKey": ""
  },
  "constraints": {
    "required": true,
    "customPasswordRegex": "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
    "customValidationMessage": "hello password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false,
    "hidePassword": false
  },
  "osPlatform": "Linux",
  "visible": true
}
```

## <a name="remarks"></a>Comentários
- `osPlatform` deve ser especificada e pode ser **Windows** ou **Linux**.
- Se `constraints.required` está definido muito**true**, Olá, em seguida, a senha ou caixas de texto de chave pública de SSH devem conter valores toovalidate com êxito. valor padrão de saudação é **true**.
- Se `options.hideConfirmation` está definido muito**true**, em seguida, a segunda caixa de texto Olá para confirmar a senha do usuário hello está oculto. valor padrão de saudação é **false**.
- Se `options.hidePassword` está definido muito**true**, e a autenticação de senha Olá opção toouse está oculto. Ele pode ser usado apenas quando `osPlatform` é **Linux**. O valor padrão é **false**.
- Restrições adicionais sobre Olá permitidas senhas podem ser implementadas usando Olá `customPasswordRegex` propriedade. Olá a cadeia de caracteres em `customValidationMessage` é exibida quando uma senha falha a validação personalizada. Olá valor padrão para as duas propriedades é **nulo**.

## <a name="sample-output"></a>Saída de exemplo
Se `osPlatform` é **Windows**, ou uma senha em vez de uma chave pública SSH fornecido pelo usuário de hello, hello seguinte saída é esperada:

```json
{
  "authenticationType": "password",
  "password": "p4ssw0rd",
}
```

Se o usuário Olá fornecido uma chave pública SSH, em seguida, hello saída a seguir é esperada:
```json
{
  "authenticationType": "sshPublicKey",
  "sshPublicKey": "AAAAB3NzaC1yc2EAAAABIwAAAIEA1on8gxCGJJWSRT4uOrR13mUaUk0hRf4RzxSZ1zRbYYFw8pfGesIFoEuVth4HKyF8k1y4mRUnYHP1XNMNMJl1JcEArC2asV8sHf6zSPVffozZ5TT4SfsUu/iKy9lUcCfXzwre4WWZSXXcPff+EHtWshahu3WzBdnGxm5Xoi89zcE=",
}
```

## <a name="next-steps"></a>Próximas etapas
* Para aplicativos de toomanaged uma introdução, consulte [visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).
* Para definições de interface do usuário de toocreating uma introdução, consulte [guia de Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).
