---
title: "elemento de interface do usuário VirtualNetworkCombo de aplicativo gerenciado aaaAzure | Microsoft Docs"
description: "Descreve Olá elemento Microsoft.Network.VirtualNetworkCombo da interface do usuário para aplicativos gerenciados do Azure"
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
ms.openlocfilehash: 1b0fa5360d93306f7a814723f77e42540bdaaa9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a>Elemento de interface do usuário Microsoft.Network.VirtualNetworkCombo
Um grupo de controles para selecionar uma rede virtual nova ou existente. Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Exemplo de interface do usuário
![Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- Em wireframe superior do hello, usuário Olá separou uma nova rede virtual para que usuário Olá pode personalizar o prefixo de nome e endereço de cada sub-rede. Configurar sub-redes, nesse caso, é opcional.
- Olá inferior wireframe, usuário Olá separou uma rede virtual existente, para que o usuário Olá deve mapear cada modelo de implantação de saudação sub-rede requer tooan subrede existente. Configurar sub-redes, nesse caso, é necessário.

## <a name="schema"></a>Esquema
```json
{
  "name": "element1",
  "type": "Microsoft.Network.VirtualNetworkCombo",
  "label": {
    "virtualNetwork": "Virtual network",
    "subnets": "Subnets"
  },
  "toolTip": {
    "virtualNetwork": "",
    "subnets": ""
  },
  "defaultValue": {
    "name": "vnet01",
    "addressPrefixSize": "/16"
  },
  "constraints": {
    "minAddressPrefixSize": "/16"
  },
  "options": {
    "hideExisting": false
  },
  "subnets": {
    "subnet1": {
      "label": "First subnet",
      "defaultValue": {
        "name": "subnet-1",
        "addressPrefixSize": "/24"
      },
      "constraints": {
        "minAddressPrefixSize": "/24",
        "minAddressCount": 12,
        "requireContiguousAddresses": true
      }
    },
    "subnet2": {
      "label": "Second subnet",
      "defaultValue": {
        "name": "subnet-2",
        "addressPrefixSize": "/26"
      },
      "constraints": {
        "minAddressPrefixSize": "/26",
        "minAddressCount": 8,
        "requireContiguousAddresses": true
      }
    }
  },
  "visible": true
}
```

## <a name="remarks"></a>Comentários
- Se especificado, Olá primeiro prefixo de endereço sem sobreposição de tamanho `defaultValue.addressPrefixSize` é determinado automaticamente com base em redes virtuais existentes na assinatura saudação do usuário.
- Olá valor padrão para `defaultValue.name` e `defaultValue.addressPrefixSize` é **nulo**.
- `constraints.minAddressPrefixSize`deve ser especificado. Nenhuma rede virtual existente com um espaço de endereço menor do que o hello valor especificado não estão disponíveis para seleção.
- `subnets`deve ser especificado e `constraints.minAddressPrefixSize` deve ser especificado para cada sub-rede.
- Ao criar uma nova rede virtual, o prefixo de endereço da sub-rede cada é calculado automaticamente com base no prefixo de endereço da rede virtual hello e os respectivos `addressPrefixSize`.
- Ao usar uma rede virtual existente, todas as sub-redes menores que os respectivos `constraints.minAddressPrefixSize` ficarão indisponíveis para seleção. Além disso, se especificado, as sub-redes que não contêm pelo menos `minAddressCount` endereços disponíveis ficam indisponíveis para seleção.
valor padrão de saudação é **0**. tooensure que Olá endereços disponíveis são contíguas, especifique **true** para `requireContiguousAddresses`. valor padrão de saudação é **true**.
- Não há suporte para a criação de sub-redes em uma rede virtual existente.
- Se `options.hideExisting` é **true**, usuário Olá não é possível escolher uma rede virtual existente. valor padrão de saudação é **false**.

## <a name="sample-output"></a>Saída de exemplo
```json
{
  "name": "vnet01",
  "resourceGroup": "rg01",
  "addressPrefixes": ["10.0.0.0/16"],
  "newOrExisting": "new",
  "subnets": {
    "subnet1": {
      "name": "subnet-1",
      "addressPrefix": "10.0.0.0/24",
      "startAddress": "10.0.0.1"
    },
    "subnet2": {
      "name": "subnet-2",
      "addressPrefix": "10.0.1.0/26",
      "startAddress": "10.0.1.1"
    }
  }
}
```

## <a name="next-steps"></a>Próximas etapas
* Para aplicativos de toomanaged uma introdução, consulte [visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).
* Para definições de interface do usuário de toocreating uma introdução, consulte [guia de Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).
