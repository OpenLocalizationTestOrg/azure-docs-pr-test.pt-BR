---
title: "escala de aaaAutomatically unidades de taxa de transferência de Hubs de eventos do Azure | Microsoft Docs"
description: "Habilitar aumentar automaticamente em uma escala de tooautomatically namespace unidades de taxa de transferência"
services: event-hubs
documentationcenter: na
author: ShubhaVijayasarathy
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: shvija;sethm
ms.openlocfilehash: 0f5216bcd619ccddc1fd4063a2f0131bfa36c7d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a>Escalar verticalmente automaticamente unidade de produtividade do Hub de Eventos do Azure

## <a name="overview"></a>Visão geral

Hubs de Eventos do Azure é uma plataforma de streaming de dados altamente escalonável. Dessa forma, os clientes de Hubs de eventos geralmente aumentam seu uso depois integração toohello serviço. Esses aumentos exigem crescentes Olá predeterminado taxa de transferência unidades (elas) tooscale Hubs de eventos e lidar com taxas de transferência maior. Olá *aumentar automaticamente* recurso dos Hubs de eventos dimensiona automaticamente número de saudação de necessidades de uso de toomeet elas. O aumento de TUs evita cenários com limitação, nos quais:

* As taxas de entrada de dados excedem as TUs definidas.
* As taxas de solicitação de saída de dados excedem as TUs definidas.

## <a name="how-auto-inflate-works"></a>Como o Inflar automaticamente funciona

O tráfego dos Hubs de Eventos é controlado por unidades de produtividade. Uma única TU permite o ingresso de 1 MB/s ou saída com duas vezes essa quantidade. Hubs de Evento Standard podem ser configurados com 1-20 unidades de produtividade. Aumentar automaticamente habilita toostart pequeno com unidades de taxa de transferência mínima necessária de saudação. recurso Olá expande automaticamente toohello o limite máximo de unidades de taxa de transferência que precisar, dependendo de aumento de saudação de seu tráfego. Aumentar automaticamente fornece Olá benefícios a seguir:

- Um eficiente toostart mecanismo escala pequena e a escala se você aumentam.
- Dimensione automaticamente o limite superior especificado em toohello sem problemas de limitação.
- Mais controle sobre o dimensionamento, como controlar quando e quanto tooscale.

## <a name="enable-auto-inflate-on-a-namespace"></a>Habilitar o Inflar automaticamente em um namespace

Você pode habilitar ou desabilitar a aumentar automaticamente em um namespace usando qualquer um dos métodos a seguir de saudação:

1. Olá [portal do Azure](https://portal.azure.com).
2. Um modelo do Azure Resource Manager.

### <a name="enable-auto-inflate-through-hello-portal"></a>Habilitar aumentar automaticamente por meio do portal Olá

Você pode habilitar o recurso de aumentar automaticamente de saudação em um namespace durante a criação de um namespace de Hubs de eventos:
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

Com essa opção habilitada, você pode começar pequeno em suas unidades de produtividade e escalar verticalmente à medida que suas necessidades de seu uso aumentam. Hello limite superior para inflação não afeta os preços, que depende de vários Olá elas usada por hora.

Você também pode habilitar inflar automática usando Olá **escala** opção na folha de configurações de saudação no portal de saudação:
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a>Habilitar Inflar automaticamente usando um modelo do Azure Resource Manager

Você pode habilitar o Inflar automaticamente durante uma implantação de modelo do Azure Resource Manager. Por exemplo, o conjunto Olá `isAutoInflateEnabled` propriedade muito**true** e defina `maximumThroughputUnits` too10.

```json
"resources": [
        {
            "apiVersion": "2017-04-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "properties": {
                "isAutoInflateEnabled": true,
                "maximumThroughputUnits": 10
            },
            "resources": [
                {
                    "apiVersion": "2017-04-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {},
                    "resources": [
                        {
                            "apiVersion": "2017-04-01",
                            "name": "[parameters('consumerGroupName')]",
                            "type": "ConsumerGroups",
                            "dependsOn": [
                                "[parameters('eventHubName')]"
                            ],
                            "properties": {}
                        }
                    ]
                }
            ]
        }
    ]
```

Para o modelo completo de Olá, consulte Olá [namespace criar Hubs de eventos e habilitar inflar](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) modelo no GitHub.

## <a name="next-steps"></a>Próximas etapas

Você pode aprender mais sobre os Hubs de eventos visitando Olá links a seguir:

* [Visão Geral dos Hubs de Eventos](event-hubs-what-is-event-hubs.md)
* [Criar um Hub de Eventos](event-hubs-create.md)
