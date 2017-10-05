---
title: Configurar o firewall do aplicativo Web - Gateway de Aplicativo do Azure | Microsoft Docs
description: "Este artigo oferece orientação sobre como começar a usar o firewall do aplicativo Web em um gateway de aplicativo novo ou existente."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: gwallace
ms.openlocfilehash: ac6c629ceaf1a8036643f593ce3d7ef9ea096ef8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway-with-azure-cli"></a><span data-ttu-id="a521e-103">Configurar o firewall do aplicativo Web em um Gateway de Aplicativo novo ou existente com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="a521e-103">Configure web application firewall on a new or existing Application Gateway with Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a521e-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a521e-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="a521e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a521e-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="a521e-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="a521e-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="a521e-107">Saiba como criar um gateway de aplicativo habilitado para firewall de aplicativo Web ou adicionar um firewall do aplicativo Web a um gateway de aplicativo existente.</span><span class="sxs-lookup"><span data-stu-id="a521e-107">Learn how to create a web application firewall enabled application gateway or add web application firewall to an existing application gateway.</span></span>

<span data-ttu-id="a521e-108">O firewall de aplicativo Web (WAF) no Gateway de Aplicativo do Azure protege os aplicativos Web contra ataques comuns baseados na Web, como injeção de SQL, ataques de scripts entre sites e sequestros de sessão.</span><span class="sxs-lookup"><span data-stu-id="a521e-108">The web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="a521e-109">O Gateway de Aplicativo do Azure é um balanceador de carga de camada 7.</span><span class="sxs-lookup"><span data-stu-id="a521e-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="a521e-110">Ele fornece o failover e solicitações HTTP de roteamento de desempenho entre diferentes servidores, estejam eles na nuvem ou no local.</span><span class="sxs-lookup"><span data-stu-id="a521e-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="a521e-111">O Gateway de Aplicativo fornece muitos recursos do ADC (controlador de entrega de aplicativos), incluindo o balanceamento de carga de HTTP, a afinidade de sessão baseada em cookies, o descarregamento de protocolo SSL, as sondas de integridade personalizadas, suporte para vários sites e muitos outros.</span><span class="sxs-lookup"><span data-stu-id="a521e-111">Application gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="a521e-112">Para uma lista completa dos recursos com suporte, visite [Visão geral do Gateway de Aplicativo](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a521e-112">To find a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="a521e-113">O artigo a seguir mostra como [adicionar um firewall do aplicativo Web a um gateway de aplicativo existente](#add-web-application-firewall-to-an-existing-application-gateway) e como [criar um gateway de aplicativo que use o firewall do aplicativo Web](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="a521e-113">The following article shows how to [add web application firewall to an existing application gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an application gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![imagem de cenário][scenario]

## <a name="prerequisite-install-the-azure-cli-20"></a><span data-ttu-id="a521e-115">Pré-requisito: instalar a CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="a521e-115">Prerequisite: Install the Azure CLI 2.0</span></span>

<span data-ttu-id="a521e-116">Para executar as etapas deste artigo, será necessário [instalar a Interface de Linha de Comando do Azure para Mac, Linux e Windows (CLI do Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="a521e-116">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="waf-configuration-differences"></a><span data-ttu-id="a521e-117">Diferenças de configuração do WAF</span><span class="sxs-lookup"><span data-stu-id="a521e-117">WAF configuration differences</span></span>

<span data-ttu-id="a521e-118">Se você tiver lido [Criar um Gateway de Aplicativo com a CLI do Azure](application-gateway-create-gateway-cli.md), você compreenderá as configurações de SKU a serem definidas durante a criação de um Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a521e-118">If you have read [Create an Application Gateway with Azure CLI](application-gateway-create-gateway-cli.md), you understand the SKU settings to configure when creating an application gateway.</span></span> <span data-ttu-id="a521e-119">O WAF fornece configurações adicionais para definir ao configurar a SKU em um gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a521e-119">WAF provides additional settings to define when configuring the SKU on an application gateway.</span></span> <span data-ttu-id="a521e-120">Não há nenhuma alteração adicional feita no gateway de aplicativo em si.</span><span class="sxs-lookup"><span data-stu-id="a521e-120">There are no additional changes that you make on the application gateway itself.</span></span>

| <span data-ttu-id="a521e-121">**Configuração**</span><span class="sxs-lookup"><span data-stu-id="a521e-121">**Setting**</span></span> | <span data-ttu-id="a521e-122">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="a521e-122">**Details**</span></span>
|---|---|
|<span data-ttu-id="a521e-123">**SKU**</span><span class="sxs-lookup"><span data-stu-id="a521e-123">**SKU**</span></span> |<span data-ttu-id="a521e-124">Um gateway de aplicativo normal sem WAF dá suporte aos tamanhos **Standard\_Small**, **Standard\_Medium** e **Standard\_Large**.</span><span class="sxs-lookup"><span data-stu-id="a521e-124">A normal application gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="a521e-125">Com a introdução do WAF, há duas SKUs adicionais, **WAF\_Medium** e **WAF\_Large**.</span><span class="sxs-lookup"><span data-stu-id="a521e-125">With the introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="a521e-126">Não há suporte para WAF em gateways de aplicativo pequenos.</span><span class="sxs-lookup"><span data-stu-id="a521e-126">WAF is not supported on small application gateways.</span></span>|
|<span data-ttu-id="a521e-127">**Modo**</span><span class="sxs-lookup"><span data-stu-id="a521e-127">**Mode**</span></span> | <span data-ttu-id="a521e-128">Essa configuração é o modo de WAF.</span><span class="sxs-lookup"><span data-stu-id="a521e-128">This setting is the mode of WAF.</span></span> <span data-ttu-id="a521e-129">Os valores permitidos são **detecção** e **prevenção**.</span><span class="sxs-lookup"><span data-stu-id="a521e-129">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="a521e-130">Quando WAF estiver configurado no modo de detecção, todas as ameaças são armazenadas em um arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="a521e-130">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="a521e-131">No modo de prevenção, os eventos ainda estão conectados, mas o invasor recebe uma resposta 403 não autorizado do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a521e-131">In prevention mode, events are still logged but the attacker receives a 403 unauthorized response from the application gateway.</span></span>|

## <a name="add-web-application-firewall-to-an-existing-application-gateway"></a><span data-ttu-id="a521e-132">Adicionar o firewall do aplicativo Web a um gateway de aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="a521e-132">Add web application firewall to an existing application gateway</span></span>

<span data-ttu-id="a521e-133">O comando a seguir altera um Gateway de Aplicativo padrão existente para um Gateway de Aplicativo com WAF habilitado.</span><span class="sxs-lookup"><span data-stu-id="a521e-133">The follow command changes an existing standard application gateway to a WAF enabled application gateway.</span></span>

```azurecli-interactive
#!/bin/bash

az network application-gateway waf-config set \
  --enabled true \
  --firewall-mode Prevention \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"
```

<span data-ttu-id="a521e-134">Este comando atualiza o gateway de aplicativo com o firewall do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="a521e-134">This command updates the application gateway with web application firewall.</span></span> <span data-ttu-id="a521e-135">Visite [Diagnósticos do Gateway de Aplicativo](application-gateway-diagnostics.md) para entender como exibir os logs do seu Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a521e-135">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) to understand how to view logs for your application gateway.</span></span> <span data-ttu-id="a521e-136">Devido à natureza de segurança do WAF, será necessário examinar regularmente os logs para compreender a postura de segurança de seus aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="a521e-136">Due to the security nature of WAF, logs need to be reviewed regularly to understand the security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="a521e-137">Criar um Gateway de Aplicativo com o firewall do aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="a521e-137">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="a521e-138">O comando a seguir cria um Gateway de Aplicativo com o firewall do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="a521e-138">The following command creates an Application Gateway with web application firewall.</span></span>

```azurecli-interactive
#!/bin/bash

az network application-gateway create \
  --name "AdatumAppGateway2" \
  --location "eastus" \
  --resource-group "AdatumAppGatewayRG" \
  --vnet-name "AdatumAppGatewayVNET2" \
  --vnet-address-prefix "10.0.0.0/16" \
  --subnet "Appgatewaysubnet2" \
  --subnet-address-prefix "10.0.0.0/28" \
 --servers "10.0.0.5 10.0.0.4" \
  --capacity 2 
  --sku "WAF_Medium" \
  --http-settings-cookie-based-affinity "Enabled" \
  --http-settings-protocol "Http" \
  --frontend-port "80" \
  --routing-rule-type "Basic" \
  --http-settings-port "80" \
  --public-ip-address "pip2" \
  --public-ip-address-allocation "dynamic" \
  --tags "cli[2] owner[administrator]"
```

> [!NOTE]
> <span data-ttu-id="a521e-139">Os gateways de aplicativo criados com a configuração básica do firewall do aplicativo Web são configurados com o CRS 3.0 para proteções.</span><span class="sxs-lookup"><span data-stu-id="a521e-139">Application gateways created with the basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="a521e-140">Obter um nome DNS de Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="a521e-140">Get application gateway DNS name</span></span>

<span data-ttu-id="a521e-141">Depois de criar o gateway, a próxima etapa será configurar o front-end para comunicação.</span><span class="sxs-lookup"><span data-stu-id="a521e-141">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="a521e-142">Ao usar um IP público, o gateway de aplicativo requer um nome DNS atribuído dinamicamente, o que não é amigável.</span><span class="sxs-lookup"><span data-stu-id="a521e-142">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="a521e-143">Para garantir que os usuários finais possam alcançar o gateway de aplicativo, um registro CNAME pode ser usado para apontar para o ponto de extremidade público do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a521e-143">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="a521e-144">[Configurando um nome de domínio personalizado no Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a521e-144">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="a521e-145">Para configurar um registro CNAME, recupere detalhes do Gateway de Aplicativo e seu nome DNS/IP associado usando o elemento PublicIPAddress anexado ao Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a521e-145">To configure a CNAME record, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="a521e-146">O nome DNS do Gateway de Aplicativo deve ser usado para criar um registro CNAME que aponta os dois aplicativos Web para esse nome DNS.</span><span class="sxs-lookup"><span data-stu-id="a521e-146">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="a521e-147">O uso de registros A não é recomendável, pois o VIP pode mudar na reinicialização do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a521e-147">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

```azurecli-interactive
#!/bin/bash

az network public-ip show \
  --name pip2 \
  --resource-group "AdatumAppGatewayRG"
```

```
{
  "dnsSettings": {
    "domainNameLabel": null,
    "fqdn": "8c786058-96d4-4f3e-bb41-660860ceae4c.cloudapp.net",
    "reverseFqdn": null
  },
  "etag": "W/\"3b0ac031-01f0-4860-b572-e3c25e0c57ad\"",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/publicIPAddresses/pip2",
  "idleTimeoutInMinutes": 4,
  "ipAddress": "40.121.167.250",
  "ipConfiguration": {
    "etag": null,
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/applicationGateways/AdatumAppGateway2/frontendIPConfigurations/appGatewayFrontendIP",
    "name": null,
    "privateIpAddress": null,
    "privateIpAllocationMethod": null,
    "provisioningState": null,
    "publicIpAddress": null,
    "resourceGroup": "AdatumAppGatewayRG",
    "subnet": null
  },
  "location": "eastus",
  "name": "pip2",
  "provisioningState": "Succeeded",
  "publicIpAddressVersion": "IPv4",
  "publicIpAllocationMethod": "Dynamic",
  "resourceGroup": "AdatumAppGatewayRG",
  "resourceGuid": "3c30d310-c543-4e9d-9c72-bbacd7fe9b05",
  "tags": {
    "cli[2] owner[administrator]": ""
  },
  "type": "Microsoft.Network/publicIPAddresses"
}
```

## <a name="next-steps"></a><span data-ttu-id="a521e-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a521e-148">Next steps</span></span>

<span data-ttu-id="a521e-149">Saiba como personalizar regras de WAF visitando: [Personalizar as regras de firewall de aplicativo Web por meio da CLI do Azure 2.0](application-gateway-customize-waf-rules-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a521e-149">Learn how to customize WAF rules by visiting: [Customize web application firewall rules through the Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md).</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-cli/scenario.png
