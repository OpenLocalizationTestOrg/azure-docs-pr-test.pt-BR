---
title: "Visão geral do roteamento de conteúdo baseado em URL | Microsoft Docs"
description: "Esta página fornece uma visão geral do roteamento de conteúdo baseado em URL do Gateway de Aplicativo, da configuração de UrlPathMap e da regra de PathBasedRouting."
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
ms.openlocfilehash: 75c3279d2d02cb3c6e949d191c88a1eb18b58a27
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="url-path-based-routing-overview"></a><span data-ttu-id="d73fb-103">Visão geral do Roteamento Baseado em Caminho de URL</span><span class="sxs-lookup"><span data-stu-id="d73fb-103">URL Path Based Routing overview</span></span>

<span data-ttu-id="d73fb-104">O Roteamento Baseado em Caminho de URL permite rotear o tráfego para pools do servidor de back-end com base nos Caminhos de URL da solicitação.</span><span class="sxs-lookup"><span data-stu-id="d73fb-104">URL Path Based Routing allows you to route traffic to back-end server pools based on URL Paths of the request.</span></span> 

<span data-ttu-id="d73fb-105">Um dos cenários possíveis é rotear as solicitações de tipos de conteúdo diferentes para pools de servidores de back-end diferentes.</span><span class="sxs-lookup"><span data-stu-id="d73fb-105">One of the scenarios is to route requests for different content types to different backend server pools.</span></span>

<span data-ttu-id="d73fb-106">No exemplo a seguir, o Gateway de Aplicativo está fornecendo tráfego para contoso.com de três pools de servidor de back-end, como por exemplo: VideoServerPool, ImageServerPool e DefaultServerPool.</span><span class="sxs-lookup"><span data-stu-id="d73fb-106">In the following example, Application Gateway is serving traffic for contoso.com from three back-end server pools for example: VideoServerPool, ImageServerPool, and DefaultServerPool.</span></span>

![imageURLroute](./media/application-gateway-url-route-overview/figure1.png)

<span data-ttu-id="d73fb-108">As solicitações de http://contoso.com/video* são roteadas para VideoServerPool e as de http://contoso.com/images* são roteadas para ImageServerPool.</span><span class="sxs-lookup"><span data-stu-id="d73fb-108">Requests for http://contoso.com/video* are routed to VideoServerPool, and http://contoso.com/images* are routed to ImageServerPool.</span></span> <span data-ttu-id="d73fb-109">O DefaultServerPool será selecionado se nenhum dos padrões de caminho forem compatíveis.</span><span class="sxs-lookup"><span data-stu-id="d73fb-109">DefaultServerPool is selected if none of the path patterns match.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d73fb-110">As regras são processadas na ordem em que elas são listadas no portal.</span><span class="sxs-lookup"><span data-stu-id="d73fb-110">Rules are processed in the order they are listed in the portal.</span></span> <span data-ttu-id="d73fb-111">É altamente recomendável configurar primeiro os ouvintes de vários locais para configurar um ouvinte básico.</span><span class="sxs-lookup"><span data-stu-id="d73fb-111">It is highly recommended to configure multi-site listeners first prior to configuring a basic listener.</span></span>  <span data-ttu-id="d73fb-112">Isso garante que o tráfego seja roteado para o back-end correto.</span><span class="sxs-lookup"><span data-stu-id="d73fb-112">This ensures that traffic gets routed to the right back end.</span></span> <span data-ttu-id="d73fb-113">Se um ouvinte básico for listado primeiro e corresponder a uma solicitação de entrada, ele é processado por esse ouvinte.</span><span class="sxs-lookup"><span data-stu-id="d73fb-113">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

## <a name="urlpathmap-configuration-element"></a><span data-ttu-id="d73fb-114">Elemento de configuração UrlPathMap</span><span class="sxs-lookup"><span data-stu-id="d73fb-114">UrlPathMap configuration element</span></span>

<span data-ttu-id="d73fb-115">O elemento urlPathMap é usado para especificar padrões de Caminho para mapeamentos de pool do servidor de back-end.</span><span class="sxs-lookup"><span data-stu-id="d73fb-115">The urlPathMap element is used to specify Path patterns to back-end server pool mappings.</span></span> <span data-ttu-id="d73fb-116">O seguinte é o trecho do elemento urlPathMap do arquivo de modelo.</span><span class="sxs-lookup"><span data-stu-id="d73fb-116">The following code example is the snippet of urlPathMap element from template file.</span></span>

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
> <span data-ttu-id="d73fb-117">PathPattern: essa configuração é uma lista de padrões de caminho para correspondência.</span><span class="sxs-lookup"><span data-stu-id="d73fb-117">PathPattern: This setting is a list of path patterns to match.</span></span> <span data-ttu-id="d73fb-118">Cada um deve começar com / e o único lugar onde um "*" é permitido é no final após um "/".</span><span class="sxs-lookup"><span data-stu-id="d73fb-118">Each must start with / and the only place a "*" is allowed is at the end following a "/."</span></span> <span data-ttu-id="d73fb-119">A cadeia de caracteres inserida no correspondente de caminho não inclui nenhum texto após o primeiro ? ou #, e esses caracteres não são permitidos aqui.</span><span class="sxs-lookup"><span data-stu-id="d73fb-119">The string fed to the path matcher does not include any text after the first? or #, and those chars are not allowed here.</span></span>

<span data-ttu-id="d73fb-120">Você pode conferir um [modelo do Resource Manager usando o roteamento baseado em URL](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="d73fb-120">You can check out a [Resource Manager template using URL-based routing](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) for more information.</span></span>

## <a name="pathbasedrouting-rule"></a><span data-ttu-id="d73fb-121">Regra de PathBasedRouting</span><span class="sxs-lookup"><span data-stu-id="d73fb-121">PathBasedRouting rule</span></span>

<span data-ttu-id="d73fb-122">RequestRoutingRule do tipo PathBasedRouting é usada para associar um ouvinte a um urlPathMap.</span><span class="sxs-lookup"><span data-stu-id="d73fb-122">RequestRoutingRule of type PathBasedRouting is used to bind a listener to a urlPathMap.</span></span> <span data-ttu-id="d73fb-123">Todas as solicitações recebidas por este ouvinte são roteadas com base na política especificada no urlPathMap.</span><span class="sxs-lookup"><span data-stu-id="d73fb-123">All requests that are received for this listener are routed based on policy specified in urlPathMap.</span></span>
<span data-ttu-id="d73fb-124">Trecho de código da regra de PathBasedRouting:</span><span class="sxs-lookup"><span data-stu-id="d73fb-124">Snippet of PathBasedRouting rule:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d73fb-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d73fb-125">Next steps</span></span>

<span data-ttu-id="d73fb-126">Depois de conhecer o roteamento de conteúdo baseado em URL, acesse [criar um application gateway usando o roteamento baseado em URL](application-gateway-create-url-route-portal.md) para criar um application gateway com as regras de roteamento de URL.</span><span class="sxs-lookup"><span data-stu-id="d73fb-126">After learning about URL-based content routing, go to [create an application gateway using URL-based routing](application-gateway-create-url-route-portal.md) to create an application gateway with URL routing rules.</span></span>
