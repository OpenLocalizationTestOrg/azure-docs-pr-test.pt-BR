---
title: Suporte para WebSocket no Gateway de Aplicativo do Azure | Microsoft Docs
description: "Esta página oferece uma visão geral do suporte ao WebSocket do Gateway de Aplicativo."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 8968dac1-e9bc-4fa1-8415-96decacab83f
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: amsriva
ms.openlocfilehash: 75b06ddd02da231b7813c609c848c75e42116da5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-websocket-support-in-application-gateway"></a><span data-ttu-id="782ea-103">Visão geral do suporte para WebSocket no Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="782ea-103">Overview of WebSocket support in Application Gateway</span></span>

<span data-ttu-id="782ea-104">O Gateway de Aplicativo fornece suporte nativo a WebSocket em todos os tamanhos de gateway.</span><span class="sxs-lookup"><span data-stu-id="782ea-104">Application Gateway provides native support for WebSocket across all gateway sizes.</span></span> <span data-ttu-id="782ea-105">Não há nenhuma configuração configurada pelo usuário para habilitar ou desabilitar seletivamente o suporte ao WebSocket.</span><span class="sxs-lookup"><span data-stu-id="782ea-105">There is no user-configurable setting to selectively enable or disable WebSocket support.</span></span> 

<span data-ttu-id="782ea-106">O protocolo WebSocket padronizado na [RFC6455](https://tools.ietf.org/html/rfc6455) permite uma comunicação full-duplex entre um servidor e um cliente em uma conexão TCP de execução longa.</span><span class="sxs-lookup"><span data-stu-id="782ea-106">WebSocket protocol standardized in [RFC6455](https://tools.ietf.org/html/rfc6455) enables a full duplex communication between a server and a client over a long running TCP connection.</span></span> <span data-ttu-id="782ea-107">Esse recurso permite uma comunicação mais interativa entre o servidor Web e o cliente, que pode ser bidirecional sem a necessidade de sondagem, necessária nas implementações baseadas em HTTP.</span><span class="sxs-lookup"><span data-stu-id="782ea-107">This feature allows for a more interactive communication between the web server and the client, which can be bidirectional without the need for polling as required in HTTP-based implementations.</span></span> <span data-ttu-id="782ea-108">O WebSocket tem baixa sobrecarga, ao contrário do HTTP e pode reutilizar a mesma conexão TCP para várias solicitações/respostas, resultando em uma utilização mais eficiente de recursos.</span><span class="sxs-lookup"><span data-stu-id="782ea-108">WebSocket has low overhead unlike HTTP and can reuse the same TCP connection for multiple request/responses resulting in a more efficient utilization of resources.</span></span> <span data-ttu-id="782ea-109">Os protocolos WebSocket são projetados para funcionar em portas HTTP tradicionais de 80 e 443.</span><span class="sxs-lookup"><span data-stu-id="782ea-109">WebSocket protocols are designed to work over traditional HTTP ports of 80 and 443.</span></span>

<span data-ttu-id="782ea-110">Você pode continuar usando um ouvinte HTTP padrão na porta 80 ou 443 para receber o tráfego do WebSocket.</span><span class="sxs-lookup"><span data-stu-id="782ea-110">You can continue using a standard HTTP listener on port 80 or 443 to receive WebSocket traffic.</span></span> <span data-ttu-id="782ea-111">O tráfego WebSocket será direcionado para o servidor de back-end habilitado para WebSocket usando o pool de back-end apropriado conforme especificado nas regras do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="782ea-111">WebSocket traffic is then directed to the WebSocket enabled backend server using the appropriate backend pool as specified in application gateway rules.</span></span> <span data-ttu-id="782ea-112">O servidor back-end deve responder às investigações do gateway de aplicativo, descritas na seção [Visão geral da investigação de integridade](application-gateway-probe-overview.md).</span><span class="sxs-lookup"><span data-stu-id="782ea-112">The backend server must respond to the application gateway probes, which are described in the [health probe overview](application-gateway-probe-overview.md) section.</span></span> <span data-ttu-id="782ea-113">As investigações de integridade do gateway de aplicativo se destinam apenas a HTTP/HTTPS.</span><span class="sxs-lookup"><span data-stu-id="782ea-113">Application gateway health probes are HTTP/HTTPS only.</span></span> <span data-ttu-id="782ea-114">Cada servidor back-end deve responder às investigações de HTTP do gateway de aplicativo para encaminhar o tráfego do WebSocket para o servidor.</span><span class="sxs-lookup"><span data-stu-id="782ea-114">Each backend server must respond to HTTP probes for application gateway to route WebSocket traffic to the server.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="782ea-115">Elemento de configuração do ouvinte</span><span class="sxs-lookup"><span data-stu-id="782ea-115">Listener configuration element</span></span>

<span data-ttu-id="782ea-116">Um ouvinte HTTP existente pode ser usado para dar suporte ao tráfego do WebSocket.</span><span class="sxs-lookup"><span data-stu-id="782ea-116">An existing HTTP listener can be used to support WebSocket traffic.</span></span> <span data-ttu-id="782ea-117">A seguir, veja um trecho de um elemento httpListeners de um arquivo de modelo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="782ea-117">The following is a snippet of an httpListeners element from a sample template file.</span></span> <span data-ttu-id="782ea-118">Você precisaria de ouvintes HTTP e HTTPS para oferecer suporte a tráfego WebSocket e WebSocket seguro.</span><span class="sxs-lookup"><span data-stu-id="782ea-118">You would need both HTTP and HTTPS listeners to support WebSocket and secure WebSocket traffic.</span></span> <span data-ttu-id="782ea-119">Da mesma forma, você pode usar o [portal](application-gateway-create-gateway-portal.md) ou o [PowerShell](application-gateway-create-gateway-arm.md) para criar um gateway de aplicativo com ouvintes na porta 80/443 para dar suporte ao tráfego WebSocket.</span><span class="sxs-lookup"><span data-stu-id="782ea-119">Similarly you can use the [portal](application-gateway-create-gateway-portal.md) or [PowerShell](application-gateway-create-gateway-arm.md) to create an application gateway with listeners on port 80/443 to support WebSocket traffic.</span></span>

```json
"httpListeners": [
        {
            "name": "appGatewayHttpsListener",
            "properties": {
                "FrontendIPConfiguration": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendIPConfigurations/DefaultFrontendPublicIP"
                },
                "FrontendPort": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendPorts/appGatewayFrontendPort443'"
                },
                "Protocol": "Https",
                "SslCertificate": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/sslCertificates/appGatewaySslCert1'"
                },
            }
        },
        {
            "name": "appGatewayHttpListener",
            "properties": {
                "FrontendIPConfiguration": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendIPConfigurations/appGatewayFrontendIP'"
                },
                "FrontendPort": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendPorts/appGatewayFrontendPort80'"
                },
                "Protocol": "Http",
            }
        }
    ],
```

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a><span data-ttu-id="782ea-120">Configuração de regra BackendAddressPool, BackendHttpSetting e Routing</span><span class="sxs-lookup"><span data-stu-id="782ea-120">BackendAddressPool, BackendHttpSetting, and Routing rule configuration</span></span>

<span data-ttu-id="782ea-121">Um BackendAddressPool é usado para definir um pool de back-end com servidores habilitados para WebSocket.</span><span class="sxs-lookup"><span data-stu-id="782ea-121">A BackendAddressPool is used to define a backend pool with WebSocket enabled servers.</span></span> <span data-ttu-id="782ea-122">A backendHttpSetting é definida com uma porta de back-end 80 e 443.</span><span class="sxs-lookup"><span data-stu-id="782ea-122">The backendHttpSetting is defined with a backend port 80 and 443.</span></span> <span data-ttu-id="782ea-123">As propriedades de afinidade baseada em cookie e requestTimeouts não são relevantes para o tráfego do WebSocket.</span><span class="sxs-lookup"><span data-stu-id="782ea-123">The properties for cookie-based affinity and requestTimeouts are not relevant to WebSocket traffic.</span></span> <span data-ttu-id="782ea-124">Nenhuma alteração é necessária na regra de roteamento; “Básico” é usado para vincular o ouvinte apropriado ao pool de endereços de back-end correspondente.</span><span class="sxs-lookup"><span data-stu-id="782ea-124">There is no change required in the routing rule, 'Basic' is used to tie the appropriate listener to the corresponding backend address pool.</span></span> 

```json
"requestRoutingRules": [{
    "name": "<ruleName1>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/httpListeners/appGatewayHttpsListener')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

}, {
    "name": "<ruleName2>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/httpListeners/appGatewayHttpListener')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }

    }
}]
```

## <a name="websocket-enabled-backend"></a><span data-ttu-id="782ea-125">Back-end habilitado para WebSocket</span><span class="sxs-lookup"><span data-stu-id="782ea-125">WebSocket enabled backend</span></span>

<span data-ttu-id="782ea-126">O back-end deve ter um servidor Web HTTP/HTTPS em execução na porta configurada (normalmente 80/443) para que o WebSocket funcione.</span><span class="sxs-lookup"><span data-stu-id="782ea-126">Your backend must have a HTTP/HTTPS web server running on the configured port (usually 80/443) for WebSocket to work.</span></span> <span data-ttu-id="782ea-127">Esse requisito existe porque o protocolo WebSocket exige que o handshake inicial seja HTTP com atualização para o protocolo WebSocket como um campo de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="782ea-127">This requirement is because WebSocket protocol requires the initial handshake to be HTTP with upgrade to WebSocket protocol as a header field.</span></span> <span data-ttu-id="782ea-128">Segue um exemplo de um cabeçalho:</span><span class="sxs-lookup"><span data-stu-id="782ea-128">The following is an example of a header:</span></span>

```
    GET /chat HTTP/1.1
    Host: server.example.com
    Upgrade: websocket
    Connection: Upgrade
    Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==
    Origin: http://example.com
    Sec-WebSocket-Protocol: chat, superchat
    Sec-WebSocket-Version: 13
```

<span data-ttu-id="782ea-129">Outro motivo é que a investigação de integridade de back-end do gateway de aplicativo dá suporte apenas aos protocolos HTTP e HTTPS.</span><span class="sxs-lookup"><span data-stu-id="782ea-129">Another reason for this is that application gateway backend health probe supports HTTP and HTTPS protocols only.</span></span> <span data-ttu-id="782ea-130">Se o servidor back-end não responder às investigações de HTTP ou HTTPS, ele será retirado do pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="782ea-130">If the backend server does not respond to HTTP or HTTPS probes, it is taken out of backend pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="782ea-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="782ea-131">Next steps</span></span>

<span data-ttu-id="782ea-132">Depois de aprender sobre o suporte ao WebSocket, vá para [criar um gateway de aplicativo](application-gateway-create-gateway.md) para começar a usar um aplicativo Web habilitado para WebSocket.</span><span class="sxs-lookup"><span data-stu-id="782ea-132">After learning about WebSocket support, go to [create an application gateway](application-gateway-create-gateway.md) to get started with a WebSocket enabled web application.</span></span>

