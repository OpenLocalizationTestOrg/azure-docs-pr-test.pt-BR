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
# <a name="url-path-based-routing-overview"></a><span data-ttu-id="e9454-103">Visão geral do Roteamento Baseado em Caminho de URL</span><span class="sxs-lookup"><span data-stu-id="e9454-103">URL Path Based Routing overview</span></span>

<span data-ttu-id="e9454-104">URL de caminho com base em roteamento permite que você tooroute tráfego tooback ponta pools de servidores com base em caminhos de URL de solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9454-104">URL Path Based Routing allows you tooroute traffic tooback-end server pools based on URL Paths of hello request.</span></span> 

<span data-ttu-id="e9454-105">Um dos cenários de saudação é tooroute solicitações para pools de servidores de back-end de toodifferent de diferentes tipos de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="e9454-105">One of hello scenarios is tooroute requests for different content types toodifferent backend server pools.</span></span>

<span data-ttu-id="e9454-106">Em Olá exemplo a seguir, Application Gateway está servindo o tráfego para contoso.com de três pools do servidor back-end por exemplo: VideoServerPool, ImageServerPool e DefaultServerPool.</span><span class="sxs-lookup"><span data-stu-id="e9454-106">In hello following example, Application Gateway is serving traffic for contoso.com from three back-end server pools for example: VideoServerPool, ImageServerPool, and DefaultServerPool.</span></span>

![imageURLroute](./media/application-gateway-url-route-overview/figure1.png)

<span data-ttu-id="e9454-108">As solicitações para http://contoso.com/video * são roteada tooVideoServerPool e http://contoso.com/images * são roteada tooImageServerPool.</span><span class="sxs-lookup"><span data-stu-id="e9454-108">Requests for http://contoso.com/video* are routed tooVideoServerPool, and http://contoso.com/images* are routed tooImageServerPool.</span></span> <span data-ttu-id="e9454-109">DefaultServerPool será selecionada se corresponder a nenhum dos padrões de caminho hello.</span><span class="sxs-lookup"><span data-stu-id="e9454-109">DefaultServerPool is selected if none of hello path patterns match.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e9454-110">Regras são processadas na ordem Olá que estão listados no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9454-110">Rules are processed in hello order they are listed in hello portal.</span></span> <span data-ttu-id="e9454-111">É altamente recomendado tooconfigure multissite ouvintes primeiro anterior tooconfiguring um ouvinte básico.</span><span class="sxs-lookup"><span data-stu-id="e9454-111">It is highly recommended tooconfigure multi-site listeners first prior tooconfiguring a basic listener.</span></span>  <span data-ttu-id="e9454-112">Isso garante que o tráfego obtém roteados toohello volta terminar.</span><span class="sxs-lookup"><span data-stu-id="e9454-112">This ensures that traffic gets routed toohello right back end.</span></span> <span data-ttu-id="e9454-113">Se um ouvinte básico for listado primeiro e corresponder a uma solicitação de entrada, ele é processado por esse ouvinte.</span><span class="sxs-lookup"><span data-stu-id="e9454-113">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

## <a name="urlpathmap-configuration-element"></a><span data-ttu-id="e9454-114">Elemento de configuração UrlPathMap</span><span class="sxs-lookup"><span data-stu-id="e9454-114">UrlPathMap configuration element</span></span>

<span data-ttu-id="e9454-115">Olá urlPathMap é mapeamentos de pool do servidor usado toospecify padrões de caminho tooback-end.</span><span class="sxs-lookup"><span data-stu-id="e9454-115">hello urlPathMap element is used toospecify Path patterns tooback-end server pool mappings.</span></span> <span data-ttu-id="e9454-116">Olá, exemplo de código a seguir é o trecho de saudação do elemento urlPathMap do arquivo de modelo.</span><span class="sxs-lookup"><span data-stu-id="e9454-116">hello following code example is hello snippet of urlPathMap element from template file.</span></span>

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
> <span data-ttu-id="e9454-117">PathPattern: Essa configuração é uma lista de toomatch de padrões de caminho.</span><span class="sxs-lookup"><span data-stu-id="e9454-117">PathPattern: This setting is a list of path patterns toomatch.</span></span> <span data-ttu-id="e9454-118">Cada um deve começar com / e coloque-Olá somente um "*" é permitido é em Olá final após um "/".</span><span class="sxs-lookup"><span data-stu-id="e9454-118">Each must start with / and hello only place a "*" is allowed is at hello end following a "/."</span></span> <span data-ttu-id="e9454-119">cadeia de caracteres de saudação alimentada toohello correspondente de caminho não inclui qualquer texto após Olá primeiro? ou, # e os caracteres não são permitidos aqui.</span><span class="sxs-lookup"><span data-stu-id="e9454-119">hello string fed toohello path matcher does not include any text after hello first? or #, and those chars are not allowed here.</span></span>

<span data-ttu-id="e9454-120">Você pode conferir um [modelo do Resource Manager usando o roteamento baseado em URL](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="e9454-120">You can check out a [Resource Manager template using URL-based routing](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) for more information.</span></span>

## <a name="pathbasedrouting-rule"></a><span data-ttu-id="e9454-121">Regra de PathBasedRouting</span><span class="sxs-lookup"><span data-stu-id="e9454-121">PathBasedRouting rule</span></span>

<span data-ttu-id="e9454-122">RequestRoutingRule do tipo PathBasedRouting é usado toobind urlPathMap de tooa um ouvinte.</span><span class="sxs-lookup"><span data-stu-id="e9454-122">RequestRoutingRule of type PathBasedRouting is used toobind a listener tooa urlPathMap.</span></span> <span data-ttu-id="e9454-123">Todas as solicitações recebidas por este ouvinte são roteadas com base na política especificada no urlPathMap.</span><span class="sxs-lookup"><span data-stu-id="e9454-123">All requests that are received for this listener are routed based on policy specified in urlPathMap.</span></span>
<span data-ttu-id="e9454-124">Trecho de código da regra de PathBasedRouting:</span><span class="sxs-lookup"><span data-stu-id="e9454-124">Snippet of PathBasedRouting rule:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e9454-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e9454-125">Next steps</span></span>

<span data-ttu-id="e9454-126">Depois de aprendizado sobre o roteamento de conteúdo baseado em URL, ir muito[criar um gateway de aplicativo usando roteamento baseado em URL](application-gateway-create-url-route-portal.md) toocreate um application gateway com regras de roteamento de URL.</span><span class="sxs-lookup"><span data-stu-id="e9454-126">After learning about URL-based content routing, go too[create an application gateway using URL-based routing](application-gateway-create-url-route-portal.md) toocreate an application gateway with URL routing rules.</span></span>
