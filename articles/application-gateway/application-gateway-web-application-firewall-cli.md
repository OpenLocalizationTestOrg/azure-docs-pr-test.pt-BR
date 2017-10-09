---
title: firewall do aplicativo web aaaConfigure - Gateway de aplicativo do Azure | Microsoft Docs
description: "Este artigo fornece orientação sobre como usar toostart web firewall do aplicativo em um gateway de aplicativo novo ou existente."
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
ms.openlocfilehash: d5354984760ceab12ed49efa9e18836e9f1d3c96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway-with-azure-cli"></a><span data-ttu-id="f1133-103">Configurar o firewall do aplicativo Web em um Gateway de Aplicativo novo ou existente com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="f1133-103">Configure web application firewall on a new or existing Application Gateway with Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f1133-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f1133-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="f1133-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1133-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="f1133-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="f1133-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="f1133-107">Saiba como toocreate um firewall do aplicativo web habilitado gateway de aplicativo ou adicionar web aplicativo firewall tooan aplicativo gateway existente.</span><span class="sxs-lookup"><span data-stu-id="f1133-107">Learn how toocreate a web application firewall enabled application gateway or add web application firewall tooan existing application gateway.</span></span>

<span data-ttu-id="f1133-108">firewall do aplicativo web Hello (WAF) no Gateway de aplicativo do Azure protege os aplicativos da web comuns ataques baseados na web como injeção de SQL, ataques de script entre sites e sequestros de sessão.</span><span class="sxs-lookup"><span data-stu-id="f1133-108">hello web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="f1133-109">O Gateway de Aplicativo do Azure é um balanceador de carga de camada 7.</span><span class="sxs-lookup"><span data-stu-id="f1133-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="f1133-110">Ele fornece failover, o roteamento de desempenho de solicitações HTTP entre diferentes servidores, independentemente de estarem em nuvem hello ou local.</span><span class="sxs-lookup"><span data-stu-id="f1133-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="f1133-111">O Gateway de Aplicativo fornece muitos recursos do ADC (controlador de entrega de aplicativos), incluindo o balanceamento de carga de HTTP, a afinidade de sessão baseada em cookies, o descarregamento de protocolo SSL, as sondas de integridade personalizadas, suporte para vários sites e muitos outros.</span><span class="sxs-lookup"><span data-stu-id="f1133-111">Application gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="f1133-112">toofind uma lista completa de recursos com suporte, visite: [visão geral do Application Gateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f1133-112">toofind a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="f1133-113">Olá artigo a seguir mostra como muito[adicionar web aplicativo firewall tooan aplicativo gateway existente](#add-web-application-firewall-to-an-existing-application-gateway) e [criar um gateway de aplicativo que usa o firewall do aplicativo web](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="f1133-113">hello following article shows how too[add web application firewall tooan existing application gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an application gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![imagem de cenário][scenario]

## <a name="prerequisite-install-hello-azure-cli-20"></a><span data-ttu-id="f1133-115">Pré-requisito: Instale Olá 2.0 do CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="f1133-115">Prerequisite: Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="f1133-116">Olá tooperform as etapas neste artigo, é necessário muito[instalar Olá Interface de linha de comando do Azure para Mac, Linux e Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="f1133-116">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="waf-configuration-differences"></a><span data-ttu-id="f1133-117">Diferenças de configuração do WAF</span><span class="sxs-lookup"><span data-stu-id="f1133-117">WAF configuration differences</span></span>

<span data-ttu-id="f1133-118">Se você leu [criar um Gateway de aplicativo com a CLI do Azure](application-gateway-create-gateway-cli.md), entender Olá SKU configurações tooconfigure durante a criação de um application gateway.</span><span class="sxs-lookup"><span data-stu-id="f1133-118">If you have read [Create an Application Gateway with Azure CLI](application-gateway-create-gateway-cli.md), you understand hello SKU settings tooconfigure when creating an application gateway.</span></span> <span data-ttu-id="f1133-119">WAF fornece configurações adicionais toodefine ao configurar um application gateway Olá SKU.</span><span class="sxs-lookup"><span data-stu-id="f1133-119">WAF provides additional settings toodefine when configuring hello SKU on an application gateway.</span></span> <span data-ttu-id="f1133-120">Não há nenhuma outra alteração que você fizer no próprio gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="f1133-120">There are no additional changes that you make on hello application gateway itself.</span></span>

| <span data-ttu-id="f1133-121">**Configuração**</span><span class="sxs-lookup"><span data-stu-id="f1133-121">**Setting**</span></span> | <span data-ttu-id="f1133-122">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="f1133-122">**Details**</span></span>
|---|---|
|<span data-ttu-id="f1133-123">**SKU**</span><span class="sxs-lookup"><span data-stu-id="f1133-123">**SKU**</span></span> |<span data-ttu-id="f1133-124">Um gateway de aplicativo normal sem WAF dá suporte aos tamanhos **Standard\_Small**, **Standard\_Medium** e **Standard\_Large**.</span><span class="sxs-lookup"><span data-stu-id="f1133-124">A normal application gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="f1133-125">Com a introdução de saudação do WAF, há duas SKUs adicionais, **WAF\_médio** e **WAF\_grande**.</span><span class="sxs-lookup"><span data-stu-id="f1133-125">With hello introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="f1133-126">Não há suporte para WAF em gateways de aplicativo pequenos.</span><span class="sxs-lookup"><span data-stu-id="f1133-126">WAF is not supported on small application gateways.</span></span>|
|<span data-ttu-id="f1133-127">**Modo**</span><span class="sxs-lookup"><span data-stu-id="f1133-127">**Mode**</span></span> | <span data-ttu-id="f1133-128">Essa configuração é o modo de saudação do WAF.</span><span class="sxs-lookup"><span data-stu-id="f1133-128">This setting is hello mode of WAF.</span></span> <span data-ttu-id="f1133-129">Os valores permitidos são **detecção** e **prevenção**.</span><span class="sxs-lookup"><span data-stu-id="f1133-129">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="f1133-130">Quando WAF estiver configurado no modo de detecção, todas as ameaças são armazenadas em um arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="f1133-130">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="f1133-131">No modo de prevenção, eventos ainda estão conectados, mas invasor Olá recebe uma resposta de não autorizado 403 do gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="f1133-131">In prevention mode, events are still logged but hello attacker receives a 403 unauthorized response from hello application gateway.</span></span>|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a><span data-ttu-id="f1133-132">Adicionar web aplicativo firewall tooan aplicativo gateway existente</span><span class="sxs-lookup"><span data-stu-id="f1133-132">Add web application firewall tooan existing application gateway</span></span>

<span data-ttu-id="f1133-133">Olá siga alterações de comando de um gateway de aplicativo habilitado do tooa WAF de gateway padrão de aplicativo existente.</span><span class="sxs-lookup"><span data-stu-id="f1133-133">hello follow command changes an existing standard application gateway tooa WAF enabled application gateway.</span></span>

```azurecli-interactive
#!/bin/bash

az network application-gateway waf-config set \
  --enabled true \
  --firewall-mode Prevention \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"
```

<span data-ttu-id="f1133-134">Esse comando atualiza o gateway de aplicativo hello com o firewall do aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="f1133-134">This command updates hello application gateway with web application firewall.</span></span> <span data-ttu-id="f1133-135">Visite [Application Gateway Diagnostics](application-gateway-diagnostics.md) toounderstand como tooview logs para o gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f1133-135">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) toounderstand how tooview logs for your application gateway.</span></span> <span data-ttu-id="f1133-136">Devido a natureza de segurança toohello de WAF, logs necessidade toobe revisado regularmente toounderstand postura de segurança de saudação de seus aplicativos web.</span><span class="sxs-lookup"><span data-stu-id="f1133-136">Due toohello security nature of WAF, logs need toobe reviewed regularly toounderstand hello security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="f1133-137">Criar um Gateway de Aplicativo com o firewall do aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="f1133-137">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="f1133-138">saudação de comando a seguir cria um Application Gateway com o firewall do aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="f1133-138">hello following command creates an Application Gateway with web application firewall.</span></span>

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
> <span data-ttu-id="f1133-139">Gateways de aplicativo criados com a configuração de firewall de aplicativo Olá web básico são configurados com CRS 3.0 para proteção.</span><span class="sxs-lookup"><span data-stu-id="f1133-139">Application gateways created with hello basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="f1133-140">Obter um nome DNS de Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="f1133-140">Get application gateway DNS name</span></span>

<span data-ttu-id="f1133-141">Depois de criar o gateway hello, Olá próxima etapa é tooconfigure Olá front-end para comunicação.</span><span class="sxs-lookup"><span data-stu-id="f1133-141">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="f1133-142">Ao usar um IP público, o gateway de aplicativo requer um nome DNS atribuído dinamicamente, o que não é amigável.</span><span class="sxs-lookup"><span data-stu-id="f1133-142">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="f1133-143">os usuários finais de tooensure pode pressionar o gateway de aplicativo hello, um registro CNAME pode ser usado toopoint toohello ponto de extremidade público do gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="f1133-143">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="f1133-144">[Configurando um nome de domínio personalizado no Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f1133-144">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="f1133-145">tooconfigure um registro CNAME, recuperar detalhes do gateway de aplicativo hello e seu nome de IP/DNS associado usando Olá PublicIPAddress elemento toohello anexado application gateway.</span><span class="sxs-lookup"><span data-stu-id="f1133-145">tooconfigure a CNAME record, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="f1133-146">nome DNS do gateway do aplicativo Hello deve ser usado toocreate um registro CNAME, qual nome DNS pontos Olá duas web aplicativos toothis.</span><span class="sxs-lookup"><span data-stu-id="f1133-146">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="f1133-147">uso de saudação de registros de um não é recomendável porque Olá VIP pode ser alterado na reinicialização do application gateway.</span><span class="sxs-lookup"><span data-stu-id="f1133-147">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f1133-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f1133-148">Next steps</span></span>

<span data-ttu-id="f1133-149">Saiba como as regras de toocustomize WAF visitando: [personalizar regras de firewall do aplicativo web por meio de hello Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md).</span><span class="sxs-lookup"><span data-stu-id="f1133-149">Learn how toocustomize WAF rules by visiting: [Customize web application firewall rules through hello Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md).</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-cli/scenario.png
