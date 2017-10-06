---
title: "aaaHosting vários sites no Gateway de aplicativo do Azure | Microsoft Docs"
description: "Esta página fornece uma visão geral da saudação suporte de vários local do Application Gateway."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: 
ms.assetid: 49993fd2-87e5-4a66-b386-8d22056a616d
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: 4ab6faa97f1891d7525affdaa36463681bf99e9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-multiple-site-hosting"></a>Hospedagem de vários sites do Gateway de Aplicativo

Várias opções de hospedagem de site permite que você tooconfigure mais de um aplicativo web em Olá mesma instância de gateway do aplicativo. Esse recurso permite que você tooconfigure uma topologia mais eficiente para implantações com a adição de gateway de aplicativo too20 sites tooone. Cada site pode ser direcionado tooits possui o pool de back-end. Olá exemplo a seguir, o gateway de aplicativo é que atende ao tráfego para contoso.com e fabrikam.com de dois pools do servidor back-end chamado ContosoServerPool e FabrikamServerPool.

![imageURLroute](./media/application-gateway-multi-site-overview/multisite.png)

> [!IMPORTANT]
> Regras são processadas na ordem Olá que estão listados no portal de saudação. É altamente recomendado tooconfigure multissite ouvintes primeiro anterior tooconfiguring um ouvinte básico.  Isso irá garantir que o tráfego obtém roteados toohello volta terminar. Se um ouvinte básico for listado primeiro e corresponder a uma solicitação de entrada, ele é processado por esse ouvinte.

Solicitações de http://contoso.com são roteada tooContosoServerPool e http://fabrikam.com são roteada tooFabrikamServerPool.

Da mesma forma dois subdomínios de saudação mesmo domínio pai pode ser hospedado em Olá implantação de gateway do mesmo aplicativo. Exemplos de uso de subdomínios podem incluir http://blog.contoso.com e http://app.contoso.com hospedado em uma implantação do gateway de aplicativo única.

## <a name="host-headers-and-server-name-indication-sni"></a>Cabeçalhos de host e SNI (Indicação de Nome de Servidor)

Existem três mecanismos comuns para habilitar vários site hospedagem Olá mesmo infraestrutura.

1. Hospede vários aplicativos Web, cada um em um endereço IP exclusivo.
2. Nome de host de uso toohost vários aplicativos web em Olá mesmo endereço IP.
3. Usar diferente portas toohost vários aplicativos web em Olá mesmo endereço IP.

No momento, um Application Gateway obtém um único endereço IP público que escuta o tráfego. Portanto, o suporte a vários aplicativos, cada um com seu próprio endereço IP, não tem suporte no momento. Application Gateway oferece suporte a vários aplicativos de hospedagem cada escutando nas portas diferentes, mas esse cenário requer tráfego de tooaccept aplicativos Olá em portas não padrão e geralmente não é uma configuração desejada. Application Gateway depende do HTTP 1.1 Olá de toohost de cabeçalhos de host com mais de um site da Web no mesmo endereço IP público e a porta. sites de saudação hospedados no gateway do aplicativo também podem suporte ao descarregamento SSL com a extensão TLS de indicação de nome de servidor (SNI). Nesse cenário significa que Olá cliente navegador e back-end da web farm deve oferecer suporte a HTTP/1.1 e extensão TLS conforme definido no RFC 6066.

## <a name="listener-configuration-element"></a>Elemento de configuração do ouvinte

HTTPListener existente, elemento de configuração é aprimorado toosupport host nome e o servidor de nome indicação elementos, que é usada pelo pool de back-end do application gateway tooroute tráfego tooappropriate. Olá, exemplo de código a seguir é o trecho de saudação do elemento de HttpListeners do arquivo de modelo.

```json
"httpListeners": [
    {
        "name": "appGatewayHttpsListener1",
        "properties": {
            "FrontendIPConfiguration": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendIPConfigurations/DefaultFrontendPublicIP"
            },
            "FrontendPort": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendPorts/appGatewayFrontendPort443'"
            },
            "Protocol": "Https",
            "SslCertificate": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/sslCertificates/appGatewaySslCert1'"
            },
            "HostName": "contoso.com",
            "RequireServerNameIndication": "true"
        }
    },
    {
        "name": "appGatewayHttpListener2",
        "properties": {
            "FrontendIPConfiguration": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendIPConfigurations/appGatewayFrontendIP'"
            },
            "FrontendPort": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendPorts/appGatewayFrontendPort80'"
            },
            "Protocol": "Http",
            "HostName": "fabrikam.com",
            "RequireServerNameIndication": "false"
        }
    }
],
```

Você pode visitar [modelo do Gerenciador de recursos usando várias opções de hospedagem de site](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) para um end tooend baseado em modelo de implantação.

## <a name="routing-rule"></a>Regra de roteamento

Não há nenhuma alteração necessária na regra de roteamento de saudação. Olá 'Basic' deve continuar toobe escolhido tootie Olá site apropriado ouvinte toohello correspondente back-end pool de endereços de regra de roteamento.

```json
"requestRoutingRules": [
{
    "name": "<ruleName1>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/httpListeners/appGatewayHttpsListener1')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

},
{
    "name": "<ruleName2>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/httpListeners/appGatewayHttpListener2')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/FabrikamServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

}
]
```

## <a name="next-steps"></a>Próximas etapas

Depois de conhecer a hospedagem de vários sites, vá muito[criar um gateway de aplicativo usando várias opções de hospedagem de site](application-gateway-create-multisite-azureresourcemanager-powershell.md) toocreate um application gateway com capacidade toosupport mais de um aplicativo web.

