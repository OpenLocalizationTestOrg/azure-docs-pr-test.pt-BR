---
title: "Hospedagem de vários sites no Gateway de Aplicativo do Azure | Microsoft Docs"
description: "Esta página fornece uma visão geral do suporte a vários sites do Gateway de Aplicativo."
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
ms.openlocfilehash: 645f68d836babf11f32fc391e6dacc9430f0070c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="application-gateway-multiple-site-hosting"></a><span data-ttu-id="1ed06-103">Hospedagem de vários sites do Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="1ed06-103">Application Gateway multiple site hosting</span></span>

<span data-ttu-id="1ed06-104">A hospedagem de vários sites permite que você configure mais de um aplicativo Web na mesma instância do Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="1ed06-104">Multiple site hosting enables you to configure more than one web application on the same application gateway instance.</span></span> <span data-ttu-id="1ed06-105">Esse recurso permite que você configure a topologia mais eficiente para suas implantações adicionando até 20 sites a um Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1ed06-105">This feature allows you to configure a more efficient topology for your deployments by adding up to 20 websites to one application gateway.</span></span> <span data-ttu-id="1ed06-106">Cada site pode ser direcionado para seu próprio pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="1ed06-106">Each website can be directed to its own backend pool.</span></span> <span data-ttu-id="1ed06-107">No exemplo a seguir, o Application Gateway está fornecendo o tráfego para contoso.com e fabrikam.com de dois pools de servidores de back-end chamados ContosoServerPool e FabrikamServerPool.</span><span class="sxs-lookup"><span data-stu-id="1ed06-107">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com from two back-end server pools called ContosoServerPool and FabrikamServerPool.</span></span>

![imageURLroute](./media/application-gateway-multi-site-overview/multisite.png)

> [!IMPORTANT]
> <span data-ttu-id="1ed06-109">As regras são processadas na ordem em que elas são listadas no portal.</span><span class="sxs-lookup"><span data-stu-id="1ed06-109">Rules are processed in the order they are listed in the portal.</span></span> <span data-ttu-id="1ed06-110">É altamente recomendável configurar primeiro os ouvintes de vários locais para configurar um ouvinte básico.</span><span class="sxs-lookup"><span data-stu-id="1ed06-110">It is highly recommended to configure multi-site listeners first prior to configuring a basic listener.</span></span>  <span data-ttu-id="1ed06-111">Isso irá garantir que o tráfego seja roteado para o back-end correto.</span><span class="sxs-lookup"><span data-stu-id="1ed06-111">This will ensure that traffic gets routed to the right back end.</span></span> <span data-ttu-id="1ed06-112">Se um ouvinte básico for listado primeiro e corresponder a uma solicitação de entrada, ele é processado por esse ouvinte.</span><span class="sxs-lookup"><span data-stu-id="1ed06-112">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

<span data-ttu-id="1ed06-113">As solicitações de http://contoso.com são roteadas para ContosoServerPool e as de http://fabrikam.com são roteadas para FabrikamServerPool.</span><span class="sxs-lookup"><span data-stu-id="1ed06-113">Requests for http://contoso.com are routed to ContosoServerPool, and http://fabrikam.com are routed to FabrikamServerPool.</span></span>

<span data-ttu-id="1ed06-114">Da mesma forma, dois subdomínios do mesmo domínio pai podem ser hospedados na mesma implantação do Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1ed06-114">Similarly two subdomains of the same parent domain can be hosted on the same application gateway deployment.</span></span> <span data-ttu-id="1ed06-115">Exemplos de uso de subdomínios podem incluir http://blog.contoso.com e http://app.contoso.com hospedado em uma implantação do gateway de aplicativo única.</span><span class="sxs-lookup"><span data-stu-id="1ed06-115">Examples of using subdomains could include http://blog.contoso.com and http://app.contoso.com hosted on a single application gateway deployment.</span></span>

## <a name="host-headers-and-server-name-indication-sni"></a><span data-ttu-id="1ed06-116">Cabeçalhos de host e SNI (Indicação de Nome de Servidor)</span><span class="sxs-lookup"><span data-stu-id="1ed06-116">Host headers and Server Name Indication (SNI)</span></span>

<span data-ttu-id="1ed06-117">Existem três mecanismos comuns para habilitar a hospedagem de vários sites na mesma infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="1ed06-117">There are three common mechanisms for enabling multiple site hosting on the same infrastructure.</span></span>

1. <span data-ttu-id="1ed06-118">Hospede vários aplicativos Web, cada um em um endereço IP exclusivo.</span><span class="sxs-lookup"><span data-stu-id="1ed06-118">Host multiple web applications each on a unique IP address.</span></span>
2. <span data-ttu-id="1ed06-119">Use o nome de host para hospedar vários aplicativos Web no mesmo endereço IP.</span><span class="sxs-lookup"><span data-stu-id="1ed06-119">Use host name to host multiple web applications on the same IP address.</span></span>
3. <span data-ttu-id="1ed06-120">Use portas diferentes para hospedar vários aplicativos Web no mesmo endereço IP.</span><span class="sxs-lookup"><span data-stu-id="1ed06-120">Use different ports to host multiple web applications on the same IP address.</span></span>

<span data-ttu-id="1ed06-121">No momento, um Application Gateway obtém um único endereço IP público que escuta o tráfego.</span><span class="sxs-lookup"><span data-stu-id="1ed06-121">Currently an application gateway gets a single public IP address on which it listens for traffic.</span></span> <span data-ttu-id="1ed06-122">Portanto, o suporte a vários aplicativos, cada um com seu próprio endereço IP, não tem suporte no momento.</span><span class="sxs-lookup"><span data-stu-id="1ed06-122">Therefore supporting multiple applications, each with its own IP address, is currently not supported.</span></span> <span data-ttu-id="1ed06-123">O Gateway de Aplicativo dá suporte à hospedagem de vários aplicativos, cada um ouvindo em portas diferentes, mas esse cenário exige que os aplicativos aceitem o tráfego em portas não padrão e normalmente não é uma configuração desejada.</span><span class="sxs-lookup"><span data-stu-id="1ed06-123">Application Gateway supports hosting multiple applications each listening on different ports but this scenario would require the applications to accept traffic on non-standard ports and is often not a desired configuration.</span></span> <span data-ttu-id="1ed06-124">O Gateway de Aplicativo depende de cabeçalhos de host HTTP 1.1 para hospedar mais de um site na mesma porta e endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="1ed06-124">Application Gateway relies on HTTP 1.1 host headers to host more than one website on the same public IP address and port.</span></span> <span data-ttu-id="1ed06-125">Os sites hospedados no Application Gateway também podem dar suporte ao descarregamento SSL com a extensão TLS de SNI (Indicação de Nome de Servidor).</span><span class="sxs-lookup"><span data-stu-id="1ed06-125">The sites hosted on application gateway can also support SSL offload with Server Name Indication (SNI) TLS extension.</span></span> <span data-ttu-id="1ed06-126">Esse cenário significa que o farm da Web de back-end e o navegador cliente devem dar suporte à extensão TLS e HTTP/1.1 conforme definido no RFC 6066.</span><span class="sxs-lookup"><span data-stu-id="1ed06-126">This scenario means that the client browser and backend web farm must support HTTP/1.1 and TLS extension as defined in RFC 6066.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="1ed06-127">Elemento de configuração do ouvinte</span><span class="sxs-lookup"><span data-stu-id="1ed06-127">Listener configuration element</span></span>

<span data-ttu-id="1ed06-128">O elemento de configuração HTTPListener existente é aprimorado para dar suporte aos elementos de indicação de nome de servidor e nome de host que são usados pelo Gateway de Aplicativo para rotear o tráfego para o pool de back-end adequado.</span><span class="sxs-lookup"><span data-stu-id="1ed06-128">Existing HTTPListener configuration element is enhanced to support host name and server name indication elements, which is used by application gateway to route traffic to appropriate backend pool.</span></span> <span data-ttu-id="1ed06-129">O exemplo de código a seguir é o trecho de código do elemento HttpListeners do arquivo de modelo.</span><span class="sxs-lookup"><span data-stu-id="1ed06-129">The following code example is the snippet of HttpListeners element from template file.</span></span>

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

<span data-ttu-id="1ed06-130">Você pode visitar [Modelo do Resource Manager usando a hospedagem de vários sites](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) para encontrar uma implantação baseada em modelo de ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="1ed06-130">You can visit [Resource Manager template using multiple site hosting](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) for an end to end template-based deployment.</span></span>

## <a name="routing-rule"></a><span data-ttu-id="1ed06-131">Regra de roteamento</span><span class="sxs-lookup"><span data-stu-id="1ed06-131">Routing rule</span></span>

<span data-ttu-id="1ed06-132">Não há nenhuma alteração necessária na regra de roteamento.</span><span class="sxs-lookup"><span data-stu-id="1ed06-132">There is no change required in the routing rule.</span></span> <span data-ttu-id="1ed06-133">A regra de roteamento 'Básica' deve continuar a ser escolhido para ligar o ouvinte do site apropriado ao pool de endereços de back-end correspondente.</span><span class="sxs-lookup"><span data-stu-id="1ed06-133">The routing rule 'Basic' should continue to be chosen to tie the appropriate site listener to the corresponding backend address pool.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="1ed06-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1ed06-134">Next steps</span></span>

<span data-ttu-id="1ed06-135">Depois de conhecer várias opções de hospedagem de site, vá para [criar um Application Gateway usando a hospedagem de vários sites](application-gateway-create-multisite-azureresourcemanager-powershell.md) para criar um Application Gateway com capacidade de dar suporte a mais de um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="1ed06-135">After learning about multiple site hosting, go to [create an application gateway using multiple site hosting](application-gateway-create-multisite-azureresourcemanager-powershell.md) to create an application gateway with ability to support more than one web application.</span></span>

