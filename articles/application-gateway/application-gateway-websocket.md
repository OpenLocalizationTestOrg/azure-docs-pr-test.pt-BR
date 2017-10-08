---
title: suporte a aaaWebSocket no Gateway de aplicativo do Azure | Microsoft Docs
description: "Esta página fornece uma visão geral da saudação suporte para WebSocket de Gateway do aplicativo."
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
ms.openlocfilehash: 3776117803e8559ad243c2d4c3dd661199c1e48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-websocket-support-in-application-gateway"></a><span data-ttu-id="02ce7-103">Visão geral do suporte para WebSocket no Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="02ce7-103">Overview of WebSocket support in Application Gateway</span></span>

<span data-ttu-id="02ce7-104">O Gateway de Aplicativo fornece suporte nativo a WebSocket em todos os tamanhos de gateway.</span><span class="sxs-lookup"><span data-stu-id="02ce7-104">Application Gateway provides native support for WebSocket across all gateway sizes.</span></span> <span data-ttu-id="02ce7-105">Não há nenhuma configuração configurável pelo usuário tooselectively habilitar ou desabilitar o suporte para WebSocket.</span><span class="sxs-lookup"><span data-stu-id="02ce7-105">There is no user-configurable setting tooselectively enable or disable WebSocket support.</span></span> 

<span data-ttu-id="02ce7-106">O protocolo WebSocket padronizado na [RFC6455](https://tools.ietf.org/html/rfc6455) permite uma comunicação full-duplex entre um servidor e um cliente em uma conexão TCP de execução longa.</span><span class="sxs-lookup"><span data-stu-id="02ce7-106">WebSocket protocol standardized in [RFC6455](https://tools.ietf.org/html/rfc6455) enables a full duplex communication between a server and a client over a long running TCP connection.</span></span> <span data-ttu-id="02ce7-107">Esse recurso permite para uma mais interativa comunicação entre o servidor de web hello e cliente hello, que pode ser bidirecional sem necessidade de saudação de sondagem como necessário em implementações baseadas em HTTP.</span><span class="sxs-lookup"><span data-stu-id="02ce7-107">This feature allows for a more interactive communication between hello web server and hello client, which can be bidirectional without hello need for polling as required in HTTP-based implementations.</span></span> <span data-ttu-id="02ce7-108">WebSocket tem baixa sobrecarga ao contrário de HTTP e pode reutilizar Olá mesma conexão TCP de vários/respostas de solicitação resultando em uma utilização mais eficiente de recursos.</span><span class="sxs-lookup"><span data-stu-id="02ce7-108">WebSocket has low overhead unlike HTTP and can reuse hello same TCP connection for multiple request/responses resulting in a more efficient utilization of resources.</span></span> <span data-ttu-id="02ce7-109">Protocolos de WebSocket são projetada toowork sobre as portas HTTP tradicionais de 80 e 443.</span><span class="sxs-lookup"><span data-stu-id="02ce7-109">WebSocket protocols are designed toowork over traditional HTTP ports of 80 and 443.</span></span>

<span data-ttu-id="02ce7-110">Você pode continuar usando um ouvinte HTTP padrão na porta 80 ou 443 tooreceive tráfego WebSocket.</span><span class="sxs-lookup"><span data-stu-id="02ce7-110">You can continue using a standard HTTP listener on port 80 or 443 tooreceive WebSocket traffic.</span></span> <span data-ttu-id="02ce7-111">Tráfego de WebSocket é direcionado toohello WebSocket habilitada usando o pool de back-end apropriado Olá conforme especificado nas regras de gateway do aplicativo de servidor de back-end.</span><span class="sxs-lookup"><span data-stu-id="02ce7-111">WebSocket traffic is then directed toohello WebSocket enabled backend server using hello appropriate backend pool as specified in application gateway rules.</span></span> <span data-ttu-id="02ce7-112">servidor de back-end Olá deve responder toohello aplicativo gateway investigações que são descritas em Olá [visão geral de investigação de integridade](application-gateway-probe-overview.md) seção.</span><span class="sxs-lookup"><span data-stu-id="02ce7-112">hello backend server must respond toohello application gateway probes, which are described in hello [health probe overview](application-gateway-probe-overview.md) section.</span></span> <span data-ttu-id="02ce7-113">As investigações de integridade do gateway de aplicativo se destinam apenas a HTTP/HTTPS.</span><span class="sxs-lookup"><span data-stu-id="02ce7-113">Application gateway health probes are HTTP/HTTPS only.</span></span> <span data-ttu-id="02ce7-114">Cada servidor de back-end deve responder investigações tooHTTP aplicativo servidor de gateway tooroute WebSocket tráfego toohello.</span><span class="sxs-lookup"><span data-stu-id="02ce7-114">Each backend server must respond tooHTTP probes for application gateway tooroute WebSocket traffic toohello server.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="02ce7-115">Elemento de configuração do ouvinte</span><span class="sxs-lookup"><span data-stu-id="02ce7-115">Listener configuration element</span></span>

<span data-ttu-id="02ce7-116">Um ouvinte HTTP existente pode ser usado toosupport tráfego WebSocket.</span><span class="sxs-lookup"><span data-stu-id="02ce7-116">An existing HTTP listener can be used toosupport WebSocket traffic.</span></span> <span data-ttu-id="02ce7-117">a seguir Hello está um trecho de um elemento de httpListeners de um arquivo de modelo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="02ce7-117">hello following is a snippet of an httpListeners element from a sample template file.</span></span> <span data-ttu-id="02ce7-118">Você precisa de HTTP e HTTPS ouvintes toosupport WebSocket e proteger o tráfego de WebSocket.</span><span class="sxs-lookup"><span data-stu-id="02ce7-118">You would need both HTTP and HTTPS listeners toosupport WebSocket and secure WebSocket traffic.</span></span> <span data-ttu-id="02ce7-119">Da mesma forma, você pode usar Olá [portal](application-gateway-create-gateway-portal.md) ou [PowerShell](application-gateway-create-gateway-arm.md) toocreate um application gateway com ouvintes na porta 80/443 toosupport WebSocket tráfego.</span><span class="sxs-lookup"><span data-stu-id="02ce7-119">Similarly you can use hello [portal](application-gateway-create-gateway-portal.md) or [PowerShell](application-gateway-create-gateway-arm.md) toocreate an application gateway with listeners on port 80/443 toosupport WebSocket traffic.</span></span>

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

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a><span data-ttu-id="02ce7-120">Configuração de regra BackendAddressPool, BackendHttpSetting e Routing</span><span class="sxs-lookup"><span data-stu-id="02ce7-120">BackendAddressPool, BackendHttpSetting, and Routing rule configuration</span></span>

<span data-ttu-id="02ce7-121">Um BackendAddressPool é toodefine usado um pool de back-end com servidores do WebSocket habilitado.</span><span class="sxs-lookup"><span data-stu-id="02ce7-121">A BackendAddressPool is used toodefine a backend pool with WebSocket enabled servers.</span></span> <span data-ttu-id="02ce7-122">Olá backendHttpSetting é definida com uma back-end a porta 80 e 443.</span><span class="sxs-lookup"><span data-stu-id="02ce7-122">hello backendHttpSetting is defined with a backend port 80 and 443.</span></span> <span data-ttu-id="02ce7-123">Olá propriedades com base no cookie de afinidade e requestTimeouts não estão tráfego tooWebSocket relevantes.</span><span class="sxs-lookup"><span data-stu-id="02ce7-123">hello properties for cookie-based affinity and requestTimeouts are not relevant tooWebSocket traffic.</span></span> <span data-ttu-id="02ce7-124">Não há nenhuma alteração necessária na regra de roteamento de saudação, 'Basic' é usado tootie Olá ouvinte apropriado toohello correspondente do pool de endereços de back-end.</span><span class="sxs-lookup"><span data-stu-id="02ce7-124">There is no change required in hello routing rule, 'Basic' is used tootie hello appropriate listener toohello corresponding backend address pool.</span></span> 

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

## <a name="websocket-enabled-backend"></a><span data-ttu-id="02ce7-125">Back-end habilitado para WebSocket</span><span class="sxs-lookup"><span data-stu-id="02ce7-125">WebSocket enabled backend</span></span>

<span data-ttu-id="02ce7-126">O back-end deve ter um servidor de web HTTP/HTTPS com hello configurado do WebSocket toowork porta (normalmente, 80/443).</span><span class="sxs-lookup"><span data-stu-id="02ce7-126">Your backend must have a HTTP/HTTPS web server running on hello configured port (usually 80/443) for WebSocket toowork.</span></span> <span data-ttu-id="02ce7-127">Esse requisito é porque o protocolo WebSocket exige Olá handshake inicial toobe HTTP com o protocolo de atualização tooWebSocket como um campo de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="02ce7-127">This requirement is because WebSocket protocol requires hello initial handshake toobe HTTP with upgrade tooWebSocket protocol as a header field.</span></span> <span data-ttu-id="02ce7-128">Olá seguinte é um exemplo de um cabeçalho de:</span><span class="sxs-lookup"><span data-stu-id="02ce7-128">hello following is an example of a header:</span></span>

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

<span data-ttu-id="02ce7-129">Outro motivo é que a investigação de integridade de back-end do gateway de aplicativo dá suporte apenas aos protocolos HTTP e HTTPS.</span><span class="sxs-lookup"><span data-stu-id="02ce7-129">Another reason for this is that application gateway backend health probe supports HTTP and HTTPS protocols only.</span></span> <span data-ttu-id="02ce7-130">Se o servidor de back-end de saudação não responder tooHTTP ou investigações HTTPS, ela é considerada fora do pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="02ce7-130">If hello backend server does not respond tooHTTP or HTTPS probes, it is taken out of backend pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02ce7-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="02ce7-131">Next steps</span></span>

<span data-ttu-id="02ce7-132">Depois de aprendizado sobre o suporte do WebSocket, ir muito[criar um application gateway](application-gateway-create-gateway.md) aplicativos web habilitados para tooget iniciada com um WebSocket.</span><span class="sxs-lookup"><span data-stu-id="02ce7-132">After learning about WebSocket support, go too[create an application gateway](application-gateway-create-gateway.md) tooget started with a WebSocket enabled web application.</span></span>

