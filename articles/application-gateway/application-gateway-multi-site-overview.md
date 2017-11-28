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
# <a name="application-gateway-multiple-site-hosting"></a><span data-ttu-id="a2e80-103">Hospedagem de vários sites do Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="a2e80-103">Application Gateway multiple site hosting</span></span>

<span data-ttu-id="a2e80-104">Várias opções de hospedagem de site permite que você tooconfigure mais de um aplicativo web em Olá mesma instância de gateway do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a2e80-104">Multiple site hosting enables you tooconfigure more than one web application on hello same application gateway instance.</span></span> <span data-ttu-id="a2e80-105">Esse recurso permite que você tooconfigure uma topologia mais eficiente para implantações com a adição de gateway de aplicativo too20 sites tooone.</span><span class="sxs-lookup"><span data-stu-id="a2e80-105">This feature allows you tooconfigure a more efficient topology for your deployments by adding up too20 websites tooone application gateway.</span></span> <span data-ttu-id="a2e80-106">Cada site pode ser direcionado tooits possui o pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="a2e80-106">Each website can be directed tooits own backend pool.</span></span> <span data-ttu-id="a2e80-107">Olá exemplo a seguir, o gateway de aplicativo é que atende ao tráfego para contoso.com e fabrikam.com de dois pools do servidor back-end chamado ContosoServerPool e FabrikamServerPool.</span><span class="sxs-lookup"><span data-stu-id="a2e80-107">In hello following example, application gateway is serving traffic for contoso.com and fabrikam.com from two back-end server pools called ContosoServerPool and FabrikamServerPool.</span></span>

![imageURLroute](./media/application-gateway-multi-site-overview/multisite.png)

> [!IMPORTANT]
> <span data-ttu-id="a2e80-109">Regras são processadas na ordem Olá que estão listados no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="a2e80-109">Rules are processed in hello order they are listed in hello portal.</span></span> <span data-ttu-id="a2e80-110">É altamente recomendado tooconfigure multissite ouvintes primeiro anterior tooconfiguring um ouvinte básico.</span><span class="sxs-lookup"><span data-stu-id="a2e80-110">It is highly recommended tooconfigure multi-site listeners first prior tooconfiguring a basic listener.</span></span>  <span data-ttu-id="a2e80-111">Isso irá garantir que o tráfego obtém roteados toohello volta terminar.</span><span class="sxs-lookup"><span data-stu-id="a2e80-111">This will ensure that traffic gets routed toohello right back end.</span></span> <span data-ttu-id="a2e80-112">Se um ouvinte básico for listado primeiro e corresponder a uma solicitação de entrada, ele é processado por esse ouvinte.</span><span class="sxs-lookup"><span data-stu-id="a2e80-112">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

<span data-ttu-id="a2e80-113">Solicitações de http://contoso.com são roteada tooContosoServerPool e http://fabrikam.com são roteada tooFabrikamServerPool.</span><span class="sxs-lookup"><span data-stu-id="a2e80-113">Requests for http://contoso.com are routed tooContosoServerPool, and http://fabrikam.com are routed tooFabrikamServerPool.</span></span>

<span data-ttu-id="a2e80-114">Da mesma forma dois subdomínios de saudação mesmo domínio pai pode ser hospedado em Olá implantação de gateway do mesmo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a2e80-114">Similarly two subdomains of hello same parent domain can be hosted on hello same application gateway deployment.</span></span> <span data-ttu-id="a2e80-115">Exemplos de uso de subdomínios podem incluir http://blog.contoso.com e http://app.contoso.com hospedado em uma implantação do gateway de aplicativo única.</span><span class="sxs-lookup"><span data-stu-id="a2e80-115">Examples of using subdomains could include http://blog.contoso.com and http://app.contoso.com hosted on a single application gateway deployment.</span></span>

## <a name="host-headers-and-server-name-indication-sni"></a><span data-ttu-id="a2e80-116">Cabeçalhos de host e SNI (Indicação de Nome de Servidor)</span><span class="sxs-lookup"><span data-stu-id="a2e80-116">Host headers and Server Name Indication (SNI)</span></span>

<span data-ttu-id="a2e80-117">Existem três mecanismos comuns para habilitar vários site hospedagem Olá mesmo infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="a2e80-117">There are three common mechanisms for enabling multiple site hosting on hello same infrastructure.</span></span>

1. <span data-ttu-id="a2e80-118">Hospede vários aplicativos Web, cada um em um endereço IP exclusivo.</span><span class="sxs-lookup"><span data-stu-id="a2e80-118">Host multiple web applications each on a unique IP address.</span></span>
2. <span data-ttu-id="a2e80-119">Nome de host de uso toohost vários aplicativos web em Olá mesmo endereço IP.</span><span class="sxs-lookup"><span data-stu-id="a2e80-119">Use host name toohost multiple web applications on hello same IP address.</span></span>
3. <span data-ttu-id="a2e80-120">Usar diferente portas toohost vários aplicativos web em Olá mesmo endereço IP.</span><span class="sxs-lookup"><span data-stu-id="a2e80-120">Use different ports toohost multiple web applications on hello same IP address.</span></span>

<span data-ttu-id="a2e80-121">No momento, um Application Gateway obtém um único endereço IP público que escuta o tráfego.</span><span class="sxs-lookup"><span data-stu-id="a2e80-121">Currently an application gateway gets a single public IP address on which it listens for traffic.</span></span> <span data-ttu-id="a2e80-122">Portanto, o suporte a vários aplicativos, cada um com seu próprio endereço IP, não tem suporte no momento.</span><span class="sxs-lookup"><span data-stu-id="a2e80-122">Therefore supporting multiple applications, each with its own IP address, is currently not supported.</span></span> <span data-ttu-id="a2e80-123">Application Gateway oferece suporte a vários aplicativos de hospedagem cada escutando nas portas diferentes, mas esse cenário requer tráfego de tooaccept aplicativos Olá em portas não padrão e geralmente não é uma configuração desejada.</span><span class="sxs-lookup"><span data-stu-id="a2e80-123">Application Gateway supports hosting multiple applications each listening on different ports but this scenario would require hello applications tooaccept traffic on non-standard ports and is often not a desired configuration.</span></span> <span data-ttu-id="a2e80-124">Application Gateway depende do HTTP 1.1 Olá de toohost de cabeçalhos de host com mais de um site da Web no mesmo endereço IP público e a porta.</span><span class="sxs-lookup"><span data-stu-id="a2e80-124">Application Gateway relies on HTTP 1.1 host headers toohost more than one website on hello same public IP address and port.</span></span> <span data-ttu-id="a2e80-125">sites de saudação hospedados no gateway do aplicativo também podem suporte ao descarregamento SSL com a extensão TLS de indicação de nome de servidor (SNI).</span><span class="sxs-lookup"><span data-stu-id="a2e80-125">hello sites hosted on application gateway can also support SSL offload with Server Name Indication (SNI) TLS extension.</span></span> <span data-ttu-id="a2e80-126">Nesse cenário significa que Olá cliente navegador e back-end da web farm deve oferecer suporte a HTTP/1.1 e extensão TLS conforme definido no RFC 6066.</span><span class="sxs-lookup"><span data-stu-id="a2e80-126">This scenario means that hello client browser and backend web farm must support HTTP/1.1 and TLS extension as defined in RFC 6066.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="a2e80-127">Elemento de configuração do ouvinte</span><span class="sxs-lookup"><span data-stu-id="a2e80-127">Listener configuration element</span></span>

<span data-ttu-id="a2e80-128">HTTPListener existente, elemento de configuração é aprimorado toosupport host nome e o servidor de nome indicação elementos, que é usada pelo pool de back-end do application gateway tooroute tráfego tooappropriate.</span><span class="sxs-lookup"><span data-stu-id="a2e80-128">Existing HTTPListener configuration element is enhanced toosupport host name and server name indication elements, which is used by application gateway tooroute traffic tooappropriate backend pool.</span></span> <span data-ttu-id="a2e80-129">Olá, exemplo de código a seguir é o trecho de saudação do elemento de HttpListeners do arquivo de modelo.</span><span class="sxs-lookup"><span data-stu-id="a2e80-129">hello following code example is hello snippet of HttpListeners element from template file.</span></span>

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

<span data-ttu-id="a2e80-130">Você pode visitar [modelo do Gerenciador de recursos usando várias opções de hospedagem de site](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) para um end tooend baseado em modelo de implantação.</span><span class="sxs-lookup"><span data-stu-id="a2e80-130">You can visit [Resource Manager template using multiple site hosting](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) for an end tooend template-based deployment.</span></span>

## <a name="routing-rule"></a><span data-ttu-id="a2e80-131">Regra de roteamento</span><span class="sxs-lookup"><span data-stu-id="a2e80-131">Routing rule</span></span>

<span data-ttu-id="a2e80-132">Não há nenhuma alteração necessária na regra de roteamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="a2e80-132">There is no change required in hello routing rule.</span></span> <span data-ttu-id="a2e80-133">Olá 'Basic' deve continuar toobe escolhido tootie Olá site apropriado ouvinte toohello correspondente back-end pool de endereços de regra de roteamento.</span><span class="sxs-lookup"><span data-stu-id="a2e80-133">hello routing rule 'Basic' should continue toobe chosen tootie hello appropriate site listener toohello corresponding backend address pool.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a2e80-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a2e80-134">Next steps</span></span>

<span data-ttu-id="a2e80-135">Depois de conhecer a hospedagem de vários sites, vá muito[criar um gateway de aplicativo usando várias opções de hospedagem de site](application-gateway-create-multisite-azureresourcemanager-powershell.md) toocreate um application gateway com capacidade toosupport mais de um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="a2e80-135">After learning about multiple site hosting, go too[create an application gateway using multiple site hosting](application-gateway-create-multisite-azureresourcemanager-powershell.md) toocreate an application gateway with ability toosupport more than one web application.</span></span>

