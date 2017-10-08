---
title: "elemento de interface do usuário PublicIpAddressCombo de aplicativo gerenciado aaaAzure | Microsoft Docs"
description: "Descreve Olá elemento Microsoft.Network.PublicIpAddressCombo da interface do usuário para aplicativos gerenciados do Azure"
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
ms.openlocfilehash: 8ba689005c0eccda0a57bf628de4b5197886a950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a>Elemento de interface do usuário Microsoft.Network.PublicIpAddressCombo
Um grupo de controles para selecionar um endereço IP público novo ou existente. Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Exemplo de interface do usuário
![Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- Se o usuário Olá seleciona 'Nenhum' para o endereço IP público, caixa de texto rótulo do nome de domínio hello está oculto.
- Se o usuário Olá seleciona um endereço IP público existente, a caixa de texto rótulo do nome de domínio Olá está desabilitada. Seu valor é o rótulo de nome de domínio de saudação do endereço IP de saudação selecionado.
- Olá domínio nome sufixo (por exemplo, westus.cloudapp.azure.com) atualizações automaticamente com base na localização de saudação selecionada.

## <a name="schema"></a>Esquema
```json
{
  "name": "element1",
  "type": "Microsoft.Network.PublicIpAddressCombo",
  "label": {
    "publicIpAddress": "Public IP address",
    "domainNameLabel": "Domain name label"
  },
  "toolTip": {
    "publicIpAddress": "",
    "domainNameLabel": ""
  },
  "defaultValue": {
    "publicIpAddressName": "ip01",
    "domainNameLabel": "foobar"
  },
  "constraints": {
    "required": {
      "domainNameLabel": true
    }
  },
  "options": {
    "hideNone": false,
    "hideDomainNameLabel": false,
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a>Comentários
- Se `constraints.required.domainNameLabel` está definido muito**true**, usuário Olá deve fornecer um rótulo de nome de domínio ao criar um novo endereço IP público. Endereços IP públicos existentes sem um rótulo não ficam disponíveis para seleção.
- Se `options.hideNone` está definido muito**true**, Olá, em seguida, a opção tooselect **nenhum** para o IP público Olá endereço está oculto. valor padrão de saudação é **false**.
- Se `options.hideDomainNameLabel` está definido muito**true**, em seguida, a caixa de texto de saudação do rótulo de nome de domínio está oculto. valor padrão de saudação é **false**.
- Se `options.hideExisting` for true, o usuário Olá não é capaz de toochoose um endereço IP público existente. valor padrão de saudação é **false**.

## <a name="sample-output"></a>Saída de exemplo
Se o usuário Olá não seleciona Nenhum endereço IP público, hello seguinte saída é esperada:
```json
{
  "newOrExistingOrNone": "none"
}
```

Se o usuário Olá seleciona um endereço IP novo ou existente, hello seguinte saída é esperada:
```json
{
  "name": "ip01",
  "resourceGroup": "rg01",
  "domainNameLabel": "foobar",
  "newOrExistingOrNone": "new"
}
```
- Quando `options.hideNone` for especificado, `newOrExistingOrNone` sempre retornará **none**.
- Quando `options.hideDomainNameLabel` for especificado, `domainNameLabel` não será declarado.

## <a name="next-steps"></a>Próximas etapas
* Para aplicativos de toomanaged uma introdução, consulte [visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).
* Para definições de interface do usuário de toocreating uma introdução, consulte [guia de Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).
