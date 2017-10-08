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
# <a name="overview-of-websocket-support-in-application-gateway"></a>Visão geral do suporte para WebSocket no Gateway de Aplicativo

O Gateway de Aplicativo fornece suporte nativo a WebSocket em todos os tamanhos de gateway. Não há nenhuma configuração configurável pelo usuário tooselectively habilitar ou desabilitar o suporte para WebSocket. 

O protocolo WebSocket padronizado na [RFC6455](https://tools.ietf.org/html/rfc6455) permite uma comunicação full-duplex entre um servidor e um cliente em uma conexão TCP de execução longa. Esse recurso permite para uma mais interativa comunicação entre o servidor de web hello e cliente hello, que pode ser bidirecional sem necessidade de saudação de sondagem como necessário em implementações baseadas em HTTP. WebSocket tem baixa sobrecarga ao contrário de HTTP e pode reutilizar Olá mesma conexão TCP de vários/respostas de solicitação resultando em uma utilização mais eficiente de recursos. Protocolos de WebSocket são projetada toowork sobre as portas HTTP tradicionais de 80 e 443.

Você pode continuar usando um ouvinte HTTP padrão na porta 80 ou 443 tooreceive tráfego WebSocket. Tráfego de WebSocket é direcionado toohello WebSocket habilitada usando o pool de back-end apropriado Olá conforme especificado nas regras de gateway do aplicativo de servidor de back-end. servidor de back-end Olá deve responder toohello aplicativo gateway investigações que são descritas em Olá [visão geral de investigação de integridade](application-gateway-probe-overview.md) seção. As investigações de integridade do gateway de aplicativo se destinam apenas a HTTP/HTTPS. Cada servidor de back-end deve responder investigações tooHTTP aplicativo servidor de gateway tooroute WebSocket tráfego toohello.

## <a name="listener-configuration-element"></a>Elemento de configuração do ouvinte

Um ouvinte HTTP existente pode ser usado toosupport tráfego WebSocket. a seguir Hello está um trecho de um elemento de httpListeners de um arquivo de modelo de exemplo. Você precisa de HTTP e HTTPS ouvintes toosupport WebSocket e proteger o tráfego de WebSocket. Da mesma forma, você pode usar Olá [portal](application-gateway-create-gateway-portal.md) ou [PowerShell](application-gateway-create-gateway-arm.md) toocreate um application gateway com ouvintes na porta 80/443 toosupport WebSocket tráfego.

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

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a>Configuração de regra BackendAddressPool, BackendHttpSetting e Routing

Um BackendAddressPool é toodefine usado um pool de back-end com servidores do WebSocket habilitado. Olá backendHttpSetting é definida com uma back-end a porta 80 e 443. Olá propriedades com base no cookie de afinidade e requestTimeouts não estão tráfego tooWebSocket relevantes. Não há nenhuma alteração necessária na regra de roteamento de saudação, 'Basic' é usado tootie Olá ouvinte apropriado toohello correspondente do pool de endereços de back-end. 

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

## <a name="websocket-enabled-backend"></a>Back-end habilitado para WebSocket

O back-end deve ter um servidor de web HTTP/HTTPS com hello configurado do WebSocket toowork porta (normalmente, 80/443). Esse requisito é porque o protocolo WebSocket exige Olá handshake inicial toobe HTTP com o protocolo de atualização tooWebSocket como um campo de cabeçalho. Olá seguinte é um exemplo de um cabeçalho de:

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

Outro motivo é que a investigação de integridade de back-end do gateway de aplicativo dá suporte apenas aos protocolos HTTP e HTTPS. Se o servidor de back-end de saudação não responder tooHTTP ou investigações HTTPS, ela é considerada fora do pool de back-end.

## <a name="next-steps"></a>Próximas etapas

Depois de aprendizado sobre o suporte do WebSocket, ir muito[criar um application gateway](application-gateway-create-gateway.md) aplicativos web habilitados para tooget iniciada com um WebSocket.

