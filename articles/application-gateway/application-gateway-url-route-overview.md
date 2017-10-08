---
title: "com base em aaaURL conteúdo visão geral do roteamento | Microsoft Docs"
description: "Esta página fornece uma visão geral de saudação URL do aplicativo Gateway de roteamento baseado em conteúdo, configuração de UrlPathMap e PathBasedRouting regra."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.assetid: 4409159b-e22d-4c9a-a103-f5d32465d163
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: gwallace
ms.openlocfilehash: 5094b42625baffeb395beace68db0d269e46080c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="url-path-based-routing-overview"></a>Visão geral do Roteamento Baseado em Caminho de URL

URL de caminho com base em roteamento permite que você tooroute tráfego tooback ponta pools de servidores com base em caminhos de URL de solicitação de saudação. 

Um dos cenários de saudação é tooroute solicitações para pools de servidores de back-end de toodifferent de diferentes tipos de conteúdo.

Em Olá exemplo a seguir, Application Gateway está servindo o tráfego para contoso.com de três pools do servidor back-end por exemplo: VideoServerPool, ImageServerPool e DefaultServerPool.

![imageURLroute](./media/application-gateway-url-route-overview/figure1.png)

As solicitações para http://contoso.com/video * são roteada tooVideoServerPool e http://contoso.com/images * são roteada tooImageServerPool. DefaultServerPool será selecionada se corresponder a nenhum dos padrões de caminho hello.

> [!IMPORTANT]
> Regras são processadas na ordem Olá que estão listados no portal de saudação. É altamente recomendado tooconfigure multissite ouvintes primeiro anterior tooconfiguring um ouvinte básico.  Isso garante que o tráfego obtém roteados toohello volta terminar. Se um ouvinte básico for listado primeiro e corresponder a uma solicitação de entrada, ele é processado por esse ouvinte.

## <a name="urlpathmap-configuration-element"></a>Elemento de configuração UrlPathMap

Olá urlPathMap é mapeamentos de pool do servidor usado toospecify padrões de caminho tooback-end. Olá, exemplo de código a seguir é o trecho de saudação do elemento urlPathMap do arquivo de modelo.

```json
"urlPathMaps": [{
    "name": "{urlpathMapName}",
    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/urlPathMaps/{urlpathMapName}",
    "properties": {
        "defaultBackendAddressPool": {
            "id": "/subscriptions/    {subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendAddressPools/{poolName1}"
        },
        "defaultBackendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendHttpSettingsList/{settingname1}"
        },
        "pathRules": [{
            "name": "{pathRuleName}",
            "properties": {
                "paths": [
                    "{pathPattern}"
                ],
                "backendAddressPool": {
                    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendAddressPools/{poolName2}"
                },
                "backendHttpsettings": {
                    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendHttpsettingsList/{settingName2}"
                }
            }
        }]
    }
}]
```

> [!NOTE]
> PathPattern: Essa configuração é uma lista de toomatch de padrões de caminho. Cada um deve começar com / e coloque-Olá somente um "*" é permitido é em Olá final após um "/". cadeia de caracteres de saudação alimentada toohello correspondente de caminho não inclui qualquer texto após Olá primeiro? ou, # e os caracteres não são permitidos aqui.

Você pode conferir um [modelo do Resource Manager usando o roteamento baseado em URL](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) para obter mais informações.

## <a name="pathbasedrouting-rule"></a>Regra de PathBasedRouting

RequestRoutingRule do tipo PathBasedRouting é usado toobind urlPathMap de tooa um ouvinte. Todas as solicitações recebidas por este ouvinte são roteadas com base na política especificada no urlPathMap.
Trecho de código da regra de PathBasedRouting:

```json
"requestRoutingRules": [
    {

"name": "{ruleName}",
"id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/requestRoutingRules/{ruleName}",
"properties": {
    "ruleType": "PathBasedRouting",
    "httpListener": {
        "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/httpListeners/<listenerName>"
    },
    "urlPathMap": {
        "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/ urlPathMaps/{urlpathMapName}"
    },

}
    }
]
```

## <a name="next-steps"></a>Próximas etapas

Depois de aprendizado sobre o roteamento de conteúdo baseado em URL, ir muito[criar um gateway de aplicativo usando roteamento baseado em URL](application-gateway-create-url-route-portal.md) toocreate um application gateway com regras de roteamento de URL.
