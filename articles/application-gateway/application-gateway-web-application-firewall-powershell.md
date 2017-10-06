---
title: firewall do aplicativo web aaaConfigure - Gateway de aplicativo do Azure | Microsoft Docs
description: "Este artigo fornece orientação sobre como usar toostart web firewall do aplicativo em um Gateway de aplicativo novo ou existente."
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
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: bd2a69901f0ec0d6551d633e2588b74c3ab59a71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a><span data-ttu-id="ab971-103">Configurar o firewall do aplicativo Web em um Gateway de Aplicativo novo ou existente</span><span class="sxs-lookup"><span data-stu-id="ab971-103">Configure web application firewall on a new or existing Application Gateway</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ab971-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ab971-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="ab971-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ab971-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="ab971-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="ab971-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="ab971-107">Saiba como toocreate um firewall do aplicativo web habilitado Application Gateway ou adicionar tooan de firewall do aplicativo web existente do Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="ab971-107">Learn how toocreate a web application firewall enabled Application Gateway or add web application firewall tooan existing Application Gateway.</span></span>

<span data-ttu-id="ab971-108">firewall do aplicativo web Hello (WAF) no Gateway de aplicativo do Azure protege os aplicativos da web comuns ataques baseados na web como injeção de SQL, ataques de script entre sites e sequestros de sessão.</span><span class="sxs-lookup"><span data-stu-id="ab971-108">hello web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="ab971-109">O Gateway de Aplicativo do Azure é um balanceador de carga de camada 7.</span><span class="sxs-lookup"><span data-stu-id="ab971-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="ab971-110">Ele fornece failover, o roteamento de desempenho de solicitações HTTP entre diferentes servidores, independentemente de estarem em nuvem hello ou local.</span><span class="sxs-lookup"><span data-stu-id="ab971-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="ab971-111">O Gateway de Aplicativo fornece muitos recursos do ADC (controlador de entrega de aplicativos), incluindo o balanceamento de carga de HTTP, a afinidade de sessão baseada em cookies, o descarregamento de protocolo SSL, as sondas de integridade personalizadas, suporte para vários sites e muitos outros.</span><span class="sxs-lookup"><span data-stu-id="ab971-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="ab971-112">toofind uma lista completa de recursos com suporte, visite: [visão geral do Application Gateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ab971-112">toofind a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="ab971-113">Olá artigo a seguir mostra como muito[adicionar tooan de firewall do aplicativo web existente do Application Gateway](#add-web-application-firewall-to-an-existing-application-gateway) e [criar um Gateway de aplicativo que usa o firewall do aplicativo web](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="ab971-113">hello following article shows how too[add web application firewall tooan existing Application Gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an Application Gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![imagem de cenário][scenario]

## <a name="waf-configuration-differences"></a><span data-ttu-id="ab971-115">Diferenças de configuração do WAF</span><span class="sxs-lookup"><span data-stu-id="ab971-115">WAF configuration differences</span></span>

<span data-ttu-id="ab971-116">Se você leu [criar um Gateway de aplicativos com o PowerShell](application-gateway-create-gateway-arm.md), entender Olá SKU configurações tooconfigure durante a criação de um Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="ab971-116">If you have read [Create an Application Gateway with PowerShell](application-gateway-create-gateway-arm.md), you understand hello SKU settings tooconfigure when creating an Application Gateway.</span></span> <span data-ttu-id="ab971-117">WAF fornece configurações adicionais toodefine ao configurar um Application Gateway Olá SKU.</span><span class="sxs-lookup"><span data-stu-id="ab971-117">WAF provides additional settings toodefine when configuring hello SKU on an Application Gateway.</span></span> <span data-ttu-id="ab971-118">Não há nenhuma outra alteração que você faz na Olá Application Gateway em si.</span><span class="sxs-lookup"><span data-stu-id="ab971-118">There are no additional changes that you make on hello Application Gateway itself.</span></span>

| <span data-ttu-id="ab971-119">**Configuração**</span><span class="sxs-lookup"><span data-stu-id="ab971-119">**Setting**</span></span> | <span data-ttu-id="ab971-120">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="ab971-120">**Details**</span></span>
|---|---|
|<span data-ttu-id="ab971-121">**SKU**</span><span class="sxs-lookup"><span data-stu-id="ab971-121">**SKU**</span></span> |<span data-ttu-id="ab971-122">Um Gateway de Aplicativo normal sem WAF dá suporte aos tamanhos **Standard\_Small**, **Standard\_Medium** e **Standard\_Large**.</span><span class="sxs-lookup"><span data-stu-id="ab971-122">A normal Application Gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="ab971-123">Com a introdução de saudação do WAF, há duas SKUs adicionais, **WAF\_médio** e **WAF\_grande**.</span><span class="sxs-lookup"><span data-stu-id="ab971-123">With hello introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="ab971-124">Não há suporte para WAF em Gateways de Aplicativo pequenos.</span><span class="sxs-lookup"><span data-stu-id="ab971-124">WAF is not supported on small Application Gateways.</span></span>|
|<span data-ttu-id="ab971-125">**Camada**</span><span class="sxs-lookup"><span data-stu-id="ab971-125">**Tier**</span></span> | <span data-ttu-id="ab971-126">Olá os valores disponíveis são **padrão** ou **WAF**.</span><span class="sxs-lookup"><span data-stu-id="ab971-126">hello available values are **Standard** or **WAF**.</span></span> <span data-ttu-id="ab971-127">Ao usar o firewall do aplicativo Web, **WAF** deve ser escolhido.</span><span class="sxs-lookup"><span data-stu-id="ab971-127">When using web application firewall, **WAF** must be chosen.</span></span>|
|<span data-ttu-id="ab971-128">**Modo**</span><span class="sxs-lookup"><span data-stu-id="ab971-128">**Mode**</span></span> | <span data-ttu-id="ab971-129">Essa configuração é o modo de saudação do WAF.</span><span class="sxs-lookup"><span data-stu-id="ab971-129">This setting is hello mode of WAF.</span></span> <span data-ttu-id="ab971-130">Os valores permitidos são **detecção** e **prevenção**.</span><span class="sxs-lookup"><span data-stu-id="ab971-130">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="ab971-131">Quando WAF estiver configurado no modo de detecção, todas as ameaças são armazenadas em um arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="ab971-131">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="ab971-132">No modo de prevenção, eventos ainda estão conectados, mas invasor Olá recebe uma resposta de não autorizado 403 da saudação Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="ab971-132">In prevention mode, events are still logged but hello attacker receives a 403 unauthorized response from hello Application Gateway.</span></span>|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a><span data-ttu-id="ab971-133">Adicionar tooan de firewall do aplicativo web existente do Application Gateway</span><span class="sxs-lookup"><span data-stu-id="ab971-133">Add web application firewall tooan existing Application Gateway</span></span>

<span data-ttu-id="ab971-134">Certifique-se de que você estiver usando a versão mais recente de saudação do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab971-134">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="ab971-135">Há mais informações disponíveis em [Como usar o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="ab971-135">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="ab971-136">Faça logon no tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab971-136">Log in tooyour Azure Account.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

2. <span data-ttu-id="ab971-137">Selecione Olá toouse de assinatura para esse cenário.</span><span class="sxs-lookup"><span data-stu-id="ab971-137">Select hello subscription toouse for this scenario.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. <span data-ttu-id="ab971-138">Recupere gateway Olá que você está adicionando o firewall do aplicativo web para.</span><span class="sxs-lookup"><span data-stu-id="ab971-138">Retrieve hello gateway that you are adding web application firewall to.</span></span>

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. <span data-ttu-id="ab971-139">Configure Olá web aplicativo firewall sku.</span><span class="sxs-lookup"><span data-stu-id="ab971-139">Configure hello web application firewall sku.</span></span> <span data-ttu-id="ab971-140">Olá os tamanhos disponíveis são **WAF\_grande** e **WAF\_médio**.</span><span class="sxs-lookup"><span data-stu-id="ab971-140">hello available sizes are **WAF\_Large** and **WAF\_Medium**.</span></span> <span data-ttu-id="ab971-141">Quando o firewall do aplicativo web é usada a camada de saudação deve ser **WAF**, capacidade Olá deve ser confirmada ao definir Olá sku.</span><span class="sxs-lookup"><span data-stu-id="ab971-141">When web application firewall is used hello tier must be **WAF**, hello capacity must be confirmed when setting hello sku.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. <span data-ttu-id="ab971-142">Defina configurações de saudação WAF conforme definido no hello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ab971-142">Configure hello WAF settings as defined in hello following example:</span></span>

   <span data-ttu-id="ab971-143">Para **FirewallMode**, valores disponíveis Olá são detecção e prevenção.</span><span class="sxs-lookup"><span data-stu-id="ab971-143">For **FirewallMode**, hello available values are Prevention and Detection.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. <span data-ttu-id="ab971-144">Atualize Olá Application Gateway com hello definições de saudação anterior da etapa.</span><span class="sxs-lookup"><span data-stu-id="ab971-144">Update hello Application Gateway with hello settings defined in hello preceding step.</span></span>

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

<span data-ttu-id="ab971-145">Esse comando atualiza Olá Application Gateway com o firewall do aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="ab971-145">This command updates hello Application Gateway with web application firewall.</span></span> <span data-ttu-id="ab971-146">Visite [diagnóstico do Gateway do aplicativo](application-gateway-diagnostics.md) toounderstand como tooview logs para o Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="ab971-146">Visit [Application Gateway diagnostics](application-gateway-diagnostics.md) toounderstand how tooview logs for your Application Gateway.</span></span> <span data-ttu-id="ab971-147">Devido a natureza de segurança toohello de WAF, logs necessidade toobe revisado regularmente toounderstand postura de segurança de saudação de seus aplicativos web.</span><span class="sxs-lookup"><span data-stu-id="ab971-147">Due toohello security nature of WAF, logs need toobe reviewed regularly toounderstand hello security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="ab971-148">Criar um Gateway de Aplicativo com o firewall do aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="ab971-148">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="ab971-149">Hello etapas a seguir se você através de todo o processo de tooend de início para a criação de um Gateway de aplicativos com o firewall do aplicativo web hello.</span><span class="sxs-lookup"><span data-stu-id="ab971-149">hello following steps take you through hello entire process from beginning tooend for creating an Application Gateway with web application firewall.</span></span>

<span data-ttu-id="ab971-150">Certifique-se de que você estiver usando a versão mais recente de saudação do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab971-150">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="ab971-151">Há mais informações disponíveis em [Como usar o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="ab971-151">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="ab971-152">Faça logon no tooAzure executando `Login-AzureRmAccount`, são solicitada tooauthenticate com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="ab971-152">Log in tooAzure by running `Login-AzureRmAccount`, you are prompted tooauthenticate with your credentials.</span></span>

1. <span data-ttu-id="ab971-153">Verificar assinaturas Olá conta hello, executando`Get-AzureRmSubscription`</span><span class="sxs-lookup"><span data-stu-id="ab971-153">Check hello subscriptions for hello account by running `Get-AzureRmSubscription`</span></span>

1. <span data-ttu-id="ab971-154">Escolha qual toouse suas assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab971-154">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a><span data-ttu-id="ab971-155">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="ab971-155">Create a resource group</span></span>

<span data-ttu-id="ab971-156">Crie um grupo de recursos para Olá Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="ab971-156">Create a resource group for hello Application Gateway.</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="ab971-157">O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local.</span><span class="sxs-lookup"><span data-stu-id="ab971-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="ab971-158">Esse local é usado como o local padrão de saudação para recursos desse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ab971-158">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="ab971-159">Certifique-se de que todos os comandos toocreate um Application Gateway usa Olá mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ab971-159">Make sure that all commands toocreate an Application Gateway uses hello same resource group.</span></span>

<span data-ttu-id="ab971-160">Em Olá anterior de exemplo, criamos um grupo de recursos chamado "Appgw-RG" e o local "Oeste dos EUA."</span><span class="sxs-lookup"><span data-stu-id="ab971-160">In hello preceding example, we created a resource group called "appgw-RG" and location "West US."</span></span>

> [!NOTE]
> <span data-ttu-id="ab971-161">Se você precisar tooconfigure uma investigação personalizada para o Gateway de aplicativo, consulte [criar um Gateway de aplicativos com testes personalizados usando o PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="ab971-161">If you need tooconfigure a custom probe for your Application Gateway, see [Create an Application Gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="ab971-162">Confira [investigações personalizadas e monitoramento de integridade](application-gateway-probe-overview.md) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="ab971-162">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

### <a name="configure-virtual-network"></a><span data-ttu-id="ab971-163">Configurar rede virtual</span><span class="sxs-lookup"><span data-stu-id="ab971-163">Configure virtual network</span></span>

<span data-ttu-id="ab971-164">O Gateway de Aplicativo exige sua própria sub-rede.</span><span class="sxs-lookup"><span data-stu-id="ab971-164">Application Gateway requires a subnet of its own.</span></span> <span data-ttu-id="ab971-165">Nesta etapa, você deve criar uma rede virtual com um espaço de endereço de 10.0.0.0/16 e duas sub-redes, um para Olá Application Gateway e outra para membros do pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="ab971-165">In this step, you create a virtual network with an address space of 10.0.0.0/16 and two subnets, one for hello Application Gateway and one for backend pool members.</span></span>

```powershell
# Create a subnet configuration object for hello Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in hello subnet for Application Gateway instances. With a smaller subnet, you may not be able tooadd more instance of your Application Gateway in hello future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for hello backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create hello virtual network with hello previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a><span data-ttu-id="ab971-166">Configurar o endereço IP público</span><span class="sxs-lookup"><span data-stu-id="ab971-166">Configure public IP address</span></span>

<span data-ttu-id="ab971-167">Em ordem toohandle as solicitações externas, o Application Gateway requer um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="ab971-167">In order toohandle external requests, Application Gateway requires a public IP address.</span></span> <span data-ttu-id="ab971-168">Este endereço IP público não deve ter um `DomainNameLabel` definido toobe usado pelo Olá Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="ab971-168">This public IP address must not have a `DomainNameLabel` defined toobe used by hello Application Gateway.</span></span>

```powershell
# Create a public IP address for use with hello Application Gateway. Defining hello domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-hello-application-gateway"></a><span data-ttu-id="ab971-169">Configurar Olá Application Gateway</span><span class="sxs-lookup"><span data-stu-id="ab971-169">Configure hello Application Gateway</span></span>

```powershell
# Create a IP configuration. This configures what subnet hello Application Gateway uses. When Application Gateway starts, it picks up an IP address from hello subnet configured and routes network traffic toohello IP addresses in hello back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet

# Create a backend pool toohold hello addresses or NICs for hello application that Application Gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Upload hello authenication certificate that will be used toocommunicate with hello backend servers
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path too.cer file>

# Conifugre hello backend HTTP settings toobe used toodefine how traffic is routed toohello backend pool. hello authenication certificate used in hello previous step is added toohello backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert

# Create a frontend port toobe used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443

# Create a frontend IP configuration tooassociate hello public IP address with hello Application Gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Configure hello certificate for hello Application Gateway. This certificate is used toodecrypt and re-encrypt hello traffic on hello Application Gateway.
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>

# Create hello HTTP listener for hello Application Gateway. Assign hello front-end ip configuration, port, and ssl certificate toouse.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

#Create a load balancer routing rule that configures hello load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure hello SKU of hello Application Gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Define hello SSL policy toouse
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

#Configure hello waf configuration settings.
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"

# Create hello Application Gateway utilizing all hello previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> <span data-ttu-id="ab971-170">Gateways de aplicativo criados com a configuração de firewall de aplicativo Olá web básico são configurados com CRS 3.0 para proteção.</span><span class="sxs-lookup"><span data-stu-id="ab971-170">Application Gateways created with hello basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="ab971-171">Obter nome DNS do Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="ab971-171">Get Application Gateway DNS name</span></span>

<span data-ttu-id="ab971-172">Depois de criar o gateway hello, Olá próxima etapa é tooconfigure Olá front-end para comunicação.</span><span class="sxs-lookup"><span data-stu-id="ab971-172">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="ab971-173">Ao usar um IP público, o Gateway de Aplicativo requer um nome DNS atribuído dinamicamente, o que não é amigável.</span><span class="sxs-lookup"><span data-stu-id="ab971-173">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="ab971-174">os usuários finais de tooensure pode pressionar Olá Application Gateway, um registro CNAME pode ser usado toopoint toohello pública ponto de extremidade de saudação Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="ab971-174">tooensure end users can hit hello Application Gateway, a CNAME record can be used toopoint toohello public endpoint of hello Application Gateway.</span></span> <span data-ttu-id="ab971-175">[Configurando um nome de domínio personalizado no Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ab971-175">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="ab971-176">tooconfigure um alias, recuperar detalhes da saudação Application Gateway e seu nome de IP/DNS associado usando Olá PublicIPAddress elemento anexado toohello Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="ab971-176">tooconfigure an alias, retrieve details of hello Application Gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello Application Gateway.</span></span> <span data-ttu-id="ab971-177">nome DNS do Hello Application Gateway deve ser usado toocreate um registro CNAME, qual nome DNS pontos Olá duas web aplicativos toothis.</span><span class="sxs-lookup"><span data-stu-id="ab971-177">hello Application Gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="ab971-178">uso de saudação de registros de um não é recomendável porque Olá VIP pode ser alterado na reinicialização do Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="ab971-178">hello use of A-records is not recommended since hello VIP may change on restart of Application Gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : appgw-RG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/applicationGateways/appgwtest/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="next-steps"></a><span data-ttu-id="ab971-179">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ab971-179">Next steps</span></span>

<span data-ttu-id="ab971-180">Saiba como log de diagnóstico tooconfigure, eventos de saudação toolog detectadas ou evitados com o firewall do aplicativo web visitando [diagnóstico de Gateway do aplicativo](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="ab971-180">Learn how tooconfigure diagnostic logging, toolog hello events that are detected or prevented with web application firewall by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
