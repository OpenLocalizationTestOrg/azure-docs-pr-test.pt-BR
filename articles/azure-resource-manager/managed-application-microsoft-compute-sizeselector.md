---
title: "elemento de interface do usuário SizeSelector de aplicativo gerenciado aaaAzure | Microsoft Docs"
description: "Descreve Olá elemento Microsoft.Compute.SizeSelector da interface do usuário para aplicativos gerenciados do Azure"
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
ms.openlocfilehash: d93306135d9c6f9a83692766ce1ca7ea2b688086
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputesizeselector-ui-element"></a>Elemento de interface do usuário Microsoft.Compute.SizeSelector
Um controle para selecionar um tamanho de uma ou mais instâncias de máquina virtual. Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Exemplo de interface do usuário
![Microsoft.Compute.SizeSelector](./media/managed-application-elements/microsoft.compute.sizeselector.png)

## <a name="schema"></a>Esquema
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.SizeSelector",
  "label": "Size",
  "toolTip": "",
  "recommendedSizes": [
    "Standard_D1",
    "Standard_D2",
    "Standard_D3"
  ],
  "constraints": {
    "allowedSizes": [],
    "excludedSizes": []
  },
  "osPlatform": "Windows",
  "imageReference": {
    "publisher": "MicrosoftWindowsServer",
    "offer": "WindowsServer",
    "sku": "2012-R2-Datacenter"
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a>Comentários
- `recommendedSizes` deve conter pelo menos um tamanho. Olá recomendado primeiro tamanho é usado como padrão de saudação.
- Se um tamanho recomendado não está disponível no local de saudação selecionada, o tamanho de saudação automaticamente será ignorado. Em vez disso, hello próximo tamanho recomendado é usado.
- Qualquer tamanho não está especificado no hello `constraints.allowedSizes` estiver oculto e qualquer tamanho não é especificado em `constraints.excludedSizes` é mostrado.
`constraints.allowedSizes` e `constraints.excludedSizes` são opcionais, mas não podem ser usados simultaneamente. lista de saudação de tamanhos disponíveis pode ser determinada chamando [lista tamanhos de máquina virtual disponível para uma assinatura](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).
- `osPlatform` deve ser especificada e pode ser **Windows** ou **Linux**. Ele usou os custos de hardware de saudação toodetermine de máquinas virtuais de saudação.
- `imageReference` é omitida para imagens próprias, mas fornecida para imagens de terceiros. Ele usou os custos de software de saudação toodetermine de máquinas virtuais de saudação.
- `count`é usado tooset Olá apropriado multiplicador para o elemento de saudação. Ele dá suporte a um valor estático, como **2**, ou a um valor dinâmico de outro elemento, como `[steps('step1').vmCount]`. valor padrão de saudação é **1**.

## <a name="sample-output"></a>Saída de exemplo
```json
"Standard_D1"
```

## <a name="next-steps"></a>Próximas etapas
* Para aplicativos de toomanaged uma introdução, consulte [visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).
* Para definições de interface do usuário de toocreating uma introdução, consulte [guia de Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).
