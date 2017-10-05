---
title: Configurar o firewall do aplicativo Web - Gateway de Aplicativo do Azure | Microsoft Docs
description: "Este artigo oferece orientação sobre como começar a usar o firewall do aplicativo Web em um Gateway de Aplicativo novo ou existente."
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
ms.openlocfilehash: dab489a1c9fb7d4a51b9ccbce543b209bec23575
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a><span data-ttu-id="8ed9b-103">Configurar o firewall do aplicativo Web em um Gateway de Aplicativo novo ou existente</span><span class="sxs-lookup"><span data-stu-id="8ed9b-103">Configure web application firewall on a new or existing Application Gateway</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8ed9b-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8ed9b-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="8ed9b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ed9b-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="8ed9b-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="8ed9b-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="8ed9b-107">Saiba como criar um Gateway de Aplicativo habilitado para firewall de aplicativo Web ou adicionar um firewall do aplicativo Web a um Gateway de Aplicativo existente.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-107">Learn how to create a web application firewall enabled Application Gateway or add web application firewall to an existing Application Gateway.</span></span>

<span data-ttu-id="8ed9b-108">O firewall de aplicativo Web (WAF) no Gateway de Aplicativo do Azure protege os aplicativos Web contra ataques comuns baseados na Web, como injeção de SQL, ataques de scripts entre sites e sequestros de sessão.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-108">The web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="8ed9b-109">O Gateway de Aplicativo do Azure é um balanceador de carga de camada 7.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="8ed9b-110">Ele fornece o failover e solicitações HTTP de roteamento de desempenho entre diferentes servidores, estejam eles na nuvem ou no local.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="8ed9b-111">O Gateway de Aplicativo fornece muitos recursos do ADC (controlador de entrega de aplicativos), incluindo o balanceamento de carga de HTTP, a afinidade de sessão baseada em cookies, o descarregamento de protocolo SSL, as sondas de integridade personalizadas, suporte para vários sites e muitos outros.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="8ed9b-112">Para uma lista completa dos recursos com suporte, visite [Visão geral do Gateway de Aplicativo](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8ed9b-112">To find a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="8ed9b-113">O artigo a seguir mostra como [adicionar um firewall do aplicativo Web a um Gateway de Aplicativo existente](#add-web-application-firewall-to-an-existing-application-gateway) e como [criar um Gateway de Aplicativo que use o firewall do aplicativo Web](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="8ed9b-113">The following article shows how to [add web application firewall to an existing Application Gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an Application Gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![imagem de cenário][scenario]

## <a name="waf-configuration-differences"></a><span data-ttu-id="8ed9b-115">Diferenças de configuração do WAF</span><span class="sxs-lookup"><span data-stu-id="8ed9b-115">WAF configuration differences</span></span>

<span data-ttu-id="8ed9b-116">Se você tiver lido [Criar um Gateway de Aplicativo com o PowerShell](application-gateway-create-gateway-arm.md), compreende as configurações de SKU a serem definidas durante a criação de um Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-116">If you have read [Create an Application Gateway with PowerShell](application-gateway-create-gateway-arm.md), you understand the SKU settings to configure when creating an Application Gateway.</span></span> <span data-ttu-id="8ed9b-117">O WAF fornece configurações adicionais para definir ao configurar a SKU em um Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-117">WAF provides additional settings to define when configuring the SKU on an Application Gateway.</span></span> <span data-ttu-id="8ed9b-118">Não há nenhuma alteração adicional feita no Gateway de Aplicativo em si.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-118">There are no additional changes that you make on the Application Gateway itself.</span></span>

| <span data-ttu-id="8ed9b-119">**Configuração**</span><span class="sxs-lookup"><span data-stu-id="8ed9b-119">**Setting**</span></span> | <span data-ttu-id="8ed9b-120">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="8ed9b-120">**Details**</span></span>
|---|---|
|<span data-ttu-id="8ed9b-121">**SKU**</span><span class="sxs-lookup"><span data-stu-id="8ed9b-121">**SKU**</span></span> |<span data-ttu-id="8ed9b-122">Um Gateway de Aplicativo normal sem WAF dá suporte aos tamanhos **Standard\_Small**, **Standard\_Medium** e **Standard\_Large**.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-122">A normal Application Gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="8ed9b-123">Com a introdução do WAF, há duas SKUs adicionais, **WAF\_Medium** e **WAF\_Large**.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-123">With the introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="8ed9b-124">Não há suporte para WAF em Gateways de Aplicativo pequenos.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-124">WAF is not supported on small Application Gateways.</span></span>|
|<span data-ttu-id="8ed9b-125">**Camada**</span><span class="sxs-lookup"><span data-stu-id="8ed9b-125">**Tier**</span></span> | <span data-ttu-id="8ed9b-126">Os valores disponíveis são **Standard** ou **WAF**.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-126">The available values are **Standard** or **WAF**.</span></span> <span data-ttu-id="8ed9b-127">Ao usar o firewall do aplicativo Web, **WAF** deve ser escolhido.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-127">When using web application firewall, **WAF** must be chosen.</span></span>|
|<span data-ttu-id="8ed9b-128">**Modo**</span><span class="sxs-lookup"><span data-stu-id="8ed9b-128">**Mode**</span></span> | <span data-ttu-id="8ed9b-129">Essa configuração é o modo de WAF.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-129">This setting is the mode of WAF.</span></span> <span data-ttu-id="8ed9b-130">Os valores permitidos são **detecção** e **prevenção**.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-130">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="8ed9b-131">Quando WAF estiver configurado no modo de detecção, todas as ameaças são armazenadas em um arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-131">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="8ed9b-132">No modo de prevenção, os eventos ainda estão conectados, mas o invasor recebe uma resposta 403 não autorizado do Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-132">In prevention mode, events are still logged but the attacker receives a 403 unauthorized response from the Application Gateway.</span></span>|

## <a name="add-web-application-firewall-to-an-existing-application-gateway"></a><span data-ttu-id="8ed9b-133">Adicionar o firewall do aplicativo Web a um Gateway de Aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="8ed9b-133">Add web application firewall to an existing Application Gateway</span></span>

<span data-ttu-id="8ed9b-134">Use a versão mais recente do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-134">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="8ed9b-135">Há mais informações disponíveis em [Como usar o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="8ed9b-135">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="8ed9b-136">Faça logon na sua Conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-136">Log in to your Azure Account.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

2. <span data-ttu-id="8ed9b-137">Selecione a assinatura a ser usada nesse cenário.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-137">Select the subscription to use for this scenario.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. <span data-ttu-id="8ed9b-138">Recupere o gateway ao qual você está adicionando o firewall do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-138">Retrieve the gateway that you are adding web application firewall to.</span></span>

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. <span data-ttu-id="8ed9b-139">Configure a sku do firewall do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-139">Configure the web application firewall sku.</span></span> <span data-ttu-id="8ed9b-140">Os tamanhos disponíveis são **WAF\_Large** e **WAF\_Medium**.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-140">The available sizes are **WAF\_Large** and **WAF\_Medium**.</span></span> <span data-ttu-id="8ed9b-141">Quando o firewall do aplicativo Web é usado, a camada deve ser **WAF**. A capacidade deve ser confirmada ao definir o SKU.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-141">When web application firewall is used the tier must be **WAF**, the capacity must be confirmed when setting the sku.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. <span data-ttu-id="8ed9b-142">Defina as configurações de WAF, conforme definido no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="8ed9b-142">Configure the WAF settings as defined in the following example:</span></span>

   <span data-ttu-id="8ed9b-143">Para a configuração **FirewallMode**, os valores disponíveis são Prevenção e Detecção.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-143">For **FirewallMode**, the available values are Prevention and Detection.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. <span data-ttu-id="8ed9b-144">Atualize o Gateway de Aplicativo com as configurações definidas na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-144">Update the Application Gateway with the settings defined in the preceding step.</span></span>

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

<span data-ttu-id="8ed9b-145">Este comando atualiza o Gateway de Aplicativo com o firewall do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-145">This command updates the Application Gateway with web application firewall.</span></span> <span data-ttu-id="8ed9b-146">Visite [Diagnósticos do Gateway de Aplicativo](application-gateway-diagnostics.md) para entender como exibir os logs do seu Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-146">Visit [Application Gateway diagnostics](application-gateway-diagnostics.md) to understand how to view logs for your Application Gateway.</span></span> <span data-ttu-id="8ed9b-147">Devido à natureza de segurança do WAF, será necessário examinar regularmente os logs para compreender a postura de segurança de seus aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-147">Due to the security nature of WAF, logs need to be reviewed regularly to understand the security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="8ed9b-148">Criar um Gateway de Aplicativo com o firewall do aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="8ed9b-148">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="8ed9b-149">As etapas a seguir guiarão você do início ao fim do processo para criar um Gateway de Aplicativo com o firewall do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-149">The following steps take you through the entire process from beginning to end for creating an Application Gateway with web application firewall.</span></span>

<span data-ttu-id="8ed9b-150">Use a versão mais recente do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-150">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="8ed9b-151">Há mais informações disponíveis em [Como usar o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="8ed9b-151">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="8ed9b-152">Faça logon no Azure executando `Login-AzureRmAccount`, será então solicitado que você se autentique com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-152">Log in to Azure by running `Login-AzureRmAccount`, you are prompted to authenticate with your credentials.</span></span>

1. <span data-ttu-id="8ed9b-153">Verificar as assinaturas da conta executando `Get-AzureRmSubscription`</span><span class="sxs-lookup"><span data-stu-id="8ed9b-153">Check the subscriptions for the account by running `Get-AzureRmSubscription`</span></span>

1. <span data-ttu-id="8ed9b-154">Escolha quais das suas assinaturas do Azure deseja usar.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-154">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a><span data-ttu-id="8ed9b-155">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="8ed9b-155">Create a resource group</span></span>

<span data-ttu-id="8ed9b-156">Crie um grupo de recursos para o Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-156">Create a resource group for the Application Gateway.</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="8ed9b-157">O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="8ed9b-158">Esse local é usado como o local padrão para os recursos do grupo de recursos em questão.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-158">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="8ed9b-159">Verifique se todos os comandos para criar um Gateway de Aplicativo usam o mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-159">Make sure that all commands to create an Application Gateway uses the same resource group.</span></span>

<span data-ttu-id="8ed9b-160">No exemplo anterior, criamos um grupo de recursos denominado "appgw-RG" e o local "Oeste dos EUA".</span><span class="sxs-lookup"><span data-stu-id="8ed9b-160">In the preceding example, we created a resource group called "appgw-RG" and location "West US."</span></span>

> [!NOTE]
> <span data-ttu-id="8ed9b-161">Se você precisar configurar uma investigação personalizada para o Gateway de Aplicativo, veja [Criar um Gateway de Aplicativo com investigações personalizadas usando o PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="8ed9b-161">If you need to configure a custom probe for your Application Gateway, see [Create an Application Gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="8ed9b-162">Confira [investigações personalizadas e monitoramento de integridade](application-gateway-probe-overview.md) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-162">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

### <a name="configure-virtual-network"></a><span data-ttu-id="8ed9b-163">Configurar rede virtual</span><span class="sxs-lookup"><span data-stu-id="8ed9b-163">Configure virtual network</span></span>

<span data-ttu-id="8ed9b-164">O Gateway de Aplicativo exige sua própria sub-rede.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-164">Application Gateway requires a subnet of its own.</span></span> <span data-ttu-id="8ed9b-165">Nesta etapa, você cria uma rede virtual com um espaço de endereço de 10.0.0.0/16 e duas sub-redes, uma para o Gateway de Aplicativo e outra para os membros do pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-165">In this step, you create a virtual network with an address space of 10.0.0.0/16 and two subnets, one for the Application Gateway and one for backend pool members.</span></span>

```powershell
# Create a subnet configuration object for the Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in the subnet for Application Gateway instances. With a smaller subnet, you may not be able to add more instance of your Application Gateway in the future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for the backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create the virtual network with the previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a><span data-ttu-id="8ed9b-166">Configurar o endereço IP público</span><span class="sxs-lookup"><span data-stu-id="8ed9b-166">Configure public IP address</span></span>

<span data-ttu-id="8ed9b-167">Para tratar as solicitações externas, o Gateway de Aplicativo requer um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-167">In order to handle external requests, Application Gateway requires a public IP address.</span></span> <span data-ttu-id="8ed9b-168">Esse endereço IP público não deve ter um `DomainNameLabel` definido para ser usado pelo Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-168">This public IP address must not have a `DomainNameLabel` defined to be used by the Application Gateway.</span></span>

```powershell
# Create a public IP address for use with the Application Gateway. Defining the domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-the-application-gateway"></a><span data-ttu-id="8ed9b-169">Configurar o Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="8ed9b-169">Configure the Application Gateway</span></span>

```powershell
# Create a IP configuration. This configures what subnet the Application Gateway uses. When Application Gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet

# Create a backend pool to hold the addresses or NICs for the application that Application Gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Upload the authenication certificate that will be used to communicate with the backend servers
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path to .cer file>

# Conifugre the backend HTTP settings to be used to define how traffic is routed to the backend pool. The authenication certificate used in the previous step is added to the backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert

# Create a frontend port to be used by the listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443

# Create a frontend IP configuration to associate the public IP address with the Application Gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Configure the certificate for the Application Gateway. This certificate is used to decrypt and re-encrypt the traffic on the Application Gateway.
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path to .pfx file> -Password <password for certificate file>

# Create the HTTP listener for the Application Gateway. Assign the front-end ip configuration, port, and ssl certificate to use.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

#Create a load balancer routing rule that configures the load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure the SKU of the Application Gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Define the SSL policy to use
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

#Configure the waf configuration settings.
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"

# Create the Application Gateway utilizing all the previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> <span data-ttu-id="8ed9b-170">Os Gateways de Aplicativo criados com a configuração básica do firewall do aplicativo Web são configurados com o CRS 3.0 para proteções.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-170">Application Gateways created with the basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="8ed9b-171">Obter nome DNS do Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="8ed9b-171">Get Application Gateway DNS name</span></span>

<span data-ttu-id="8ed9b-172">Depois de criar o gateway, a próxima etapa será configurar o front-end para comunicação.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-172">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="8ed9b-173">Ao usar um IP público, o Gateway de Aplicativo requer um nome DNS atribuído dinamicamente, o que não é amigável.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-173">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="8ed9b-174">Para garantir que os usuários finais possam alcançar o Gateway de Aplicativo, um registro CNAME pode ser usado para apontar para o ponto de extremidade público do Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-174">To ensure end users can hit the Application Gateway, a CNAME record can be used to point to the public endpoint of the Application Gateway.</span></span> <span data-ttu-id="8ed9b-175">[Configurando um nome de domínio personalizado no Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8ed9b-175">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="8ed9b-176">Para configurar um alias, recupere os detalhes do Gateway de Aplicativo e seu nome DNS/IP associado usando o elemento PublicIPAddress anexado ao Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-176">To configure an alias, retrieve details of the Application Gateway and its associated IP/DNS name using the PublicIPAddress element attached to the Application Gateway.</span></span> <span data-ttu-id="8ed9b-177">O nome DNS do Gateway de Aplicativo deve ser usado para criar um registro CNAME que aponta os dois aplicativos Web para esse nome DNS.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-177">The Application Gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="8ed9b-178">O uso de registros A não é recomendável, pois o VIP pode mudar na reinicialização do Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8ed9b-178">The use of A-records is not recommended since the VIP may change on restart of Application Gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8ed9b-179">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8ed9b-179">Next steps</span></span>

<span data-ttu-id="8ed9b-180">Saiba como configurar o log de diagnóstico para registrar os eventos detectados ou impedidos pelo firewall do aplicativo Web ao visitar o [Diagnóstico do Gateway de Aplicativo](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="8ed9b-180">Learn how to configure diagnostic logging, to log the events that are detected or prevented with web application firewall by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
