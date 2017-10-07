---
title: "política de SSL aaaConfigure no Gateway do aplicativo do Azure - PowerShell | Microsoft Docs"
description: "Esta página fornece instruções tooconfigure política de SSL no Gateway de aplicativo do Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: 7802ad3d3191a2fe9d88dddcb7c65bc4a70a419c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ssl-policy-versions-and-cipher-suites-on-application-gateway"></a><span data-ttu-id="42f5a-103">Configurar versões de política SSL e conjuntos de codificação no Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="42f5a-103">Configure SSL policy versions and cipher suites on Application Gateway</span></span>

<span data-ttu-id="42f5a-104">Saiba como versões de política SSL tooconfigure e cipher suites no Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="42f5a-104">Learn how tooconfigure SSL policy versions and cipher suites on Application Gateway.</span></span> <span data-ttu-id="42f5a-105">Você pode selecionar um [lista de políticas predefinidas](#predefined-ssl-policies) que contêm configurações diferentes de versões de política SSL e habilitado os conjuntos de codificação.</span><span class="sxs-lookup"><span data-stu-id="42f5a-105">You can select from a [list of predefined policies](#predefined-ssl-policies) that contain different configurations of SSL policy versions and enabled cipher suites.</span></span> <span data-ttu-id="42f5a-106">Você também tem Olá capacidade toodefine um [política personalizada do SSL](#configure-a-custom-ssl-policy) com base em suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="42f5a-106">You also have hello ability toodefine a [custom SSL policy](#configure-a-custom-ssl-policy) based on your requirements.</span></span>

## <a name="get-available-ssl-options"></a><span data-ttu-id="42f5a-107">Obter as opções de SSL disponíveis</span><span class="sxs-lookup"><span data-stu-id="42f5a-107">Get available SSL options</span></span>

<span data-ttu-id="42f5a-108">Olá `Get-AzureRMApplicationGatewayAvailableSslOptions` cmdlet fornece uma lista de políticas predefinidas disponíveis, conjuntos de codificação disponíveis e versões de protocolo que podem ser configuradas.</span><span class="sxs-lookup"><span data-stu-id="42f5a-108">hello `Get-AzureRMApplicationGatewayAvailableSslOptions` cmdlet provides a listing of available pre-defined policies, available cipher suites, and protocol versions that can be configured.</span></span> <span data-ttu-id="42f5a-109">Olá, exemplo a seguir mostra um exemplo de saída da execução do cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="42f5a-109">hello following example shows an example output from running hello cmdlet.</span></span>

```
DefaultPolicy: AppGwSslPolicy20150501
PredefinedPolicies:
    /subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups//providers/Microsoft.Network/ApplicationGatewayAvailableSslOptions/default/Applic
ationGatewaySslPredefinedPolicy/AppGwSslPolicy20150501
    /subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups//providers/Microsoft.Network/ApplicationGatewayAvailableSslOptions/default/Applic
ationGatewaySslPredefinedPolicy/AppGwSslPolicy20170401
    /subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups//providers/Microsoft.Network/ApplicationGatewayAvailableSslOptions/default/Applic
ationGatewaySslPredefinedPolicy/AppGwSslPolicy20170401S

AvailableCipherSuites:
    TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
    TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
    TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
    TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
    TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
    TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
    TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
    TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
    TLS_DHE_RSA_WITH_AES_256_CBC_SHA
    TLS_DHE_RSA_WITH_AES_128_CBC_SHA
    TLS_RSA_WITH_AES_256_GCM_SHA384
    TLS_RSA_WITH_AES_128_GCM_SHA256
    TLS_RSA_WITH_AES_256_CBC_SHA256
    TLS_RSA_WITH_AES_128_CBC_SHA256
    TLS_RSA_WITH_AES_256_CBC_SHA
    TLS_RSA_WITH_AES_128_CBC_SHA
    TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
    TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
    TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
    TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
    TLS_DHE_DSS_WITH_AES_256_CBC_SHA256
    TLS_DHE_DSS_WITH_AES_128_CBC_SHA256
    TLS_DHE_DSS_WITH_AES_256_CBC_SHA
    TLS_DHE_DSS_WITH_AES_128_CBC_SHA
    TLS_RSA_WITH_3DES_EDE_CBC_SHA
    TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA

AvailableProtocols:
    TLSv1_0
    TLSv1_1
    TLSv1_2
```

## <a name="list-pre-defined-ssl-policies"></a><span data-ttu-id="42f5a-110">Lista de políticas predefinidas de SSL</span><span class="sxs-lookup"><span data-stu-id="42f5a-110">List pre-defined SSL Policies</span></span>

<span data-ttu-id="42f5a-111">O gateway de aplicativo vem com três políticas predefinidas que podem ser usadas.</span><span class="sxs-lookup"><span data-stu-id="42f5a-111">Application gateway comes with 3 pre-defined policies that can be used.</span></span> <span data-ttu-id="42f5a-112">Olá `Get-AzureRmApplicationGatewaySslPredefinedPolicy` cmdlet recupera essas políticas.</span><span class="sxs-lookup"><span data-stu-id="42f5a-112">hello `Get-AzureRmApplicationGatewaySslPredefinedPolicy` cmdlet retrieves these policies.</span></span> <span data-ttu-id="42f5a-113">Cada política tem versões de protocolo diferente e conjuntos de codificação habilitados.</span><span class="sxs-lookup"><span data-stu-id="42f5a-113">Each policy has different protocol versions and cipher suites enabled.</span></span> <span data-ttu-id="42f5a-114">Essas políticas predefinidas podem ser usadas tooquickly configurar uma política SSL no seu gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="42f5a-114">These pre-defined policies can be used tooquickly configure an SSL policy on your application gateway.</span></span> <span data-ttu-id="42f5a-115">Por padrão **AppGwSslPolicy20170401** será selecionada se nenhuma política SSL específica é definida.</span><span class="sxs-lookup"><span data-stu-id="42f5a-115">By default **AppGwSslPolicy20170401** is selected if no specific SSL policy is defined.</span></span>

<span data-ttu-id="42f5a-116">Olá, a seguir é um exemplo de execução `Get-AzureRmApplicationGatewaySslPredefinedPolicy`.</span><span class="sxs-lookup"><span data-stu-id="42f5a-116">hello following is an example of running `Get-AzureRmApplicationGatewaySslPredefinedPolicy`.</span></span>

```
Name: AppGwSslPolicy20150501
MinProtocolVersion: TLSv1_0
CipherSuites:
    TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
    TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
    TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
    TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
    TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
    TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
    TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
    TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
    TLS_DHE_RSA_WITH_AES_256_CBC_SHA
    TLS_DHE_RSA_WITH_AES_128_CBC_SHA
    TLS_RSA_WITH_AES_256_GCM_SHA384
 ...
Name: AppGwSslPolicy20170401
MinProtocolVersion: TLSv1_1
CipherSuites:
    TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
    TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
    TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
    TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
    TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
...
```

## <a name="configure-a-custom-ssl-policy"></a><span data-ttu-id="42f5a-117">Configurar uma política de SSL personalizada</span><span class="sxs-lookup"><span data-stu-id="42f5a-117">Configure a custom SSL policy</span></span>

<span data-ttu-id="42f5a-118">saudação de exemplo a seguir define uma política personalizada do SSL em um gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="42f5a-118">hello following example sets a custom SSL policy on an application gateway.</span></span> <span data-ttu-id="42f5a-119">Ele define a versão de protocolo mínimo Olá muito`TLSv1_1` e habilita Olá conjuntos de codificação a seguir:</span><span class="sxs-lookup"><span data-stu-id="42f5a-119">It sets hello minimum protocol version too`TLSv1_1` and enables hello following cipher suites:</span></span>

* <span data-ttu-id="42f5a-120">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="42f5a-120">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span></span>
* <span data-ttu-id="42f5a-121">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="42f5a-121">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span></span>

> [!IMPORTANT]
> <span data-ttu-id="42f5a-122">Conjunto de pelo menos uma codificação de saudação lista a seguir deve ser selecionado ao configurar uma política personalizada do SSL.</span><span class="sxs-lookup"><span data-stu-id="42f5a-122">At least one cipher suite from hello following list must be selected when configuring a custom SSL policy.</span></span> <span data-ttu-id="42f5a-123">O gateway de aplicativo usa conjuntos de criptografia RSA SHA256 para gerenciamento de back-end.</span><span class="sxs-lookup"><span data-stu-id="42f5a-123">Application gateway uses RSA SHA256 cipher suites for backend management.</span></span>
> * <span data-ttu-id="42f5a-124">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="42f5a-124">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span></span> 
> * <span data-ttu-id="42f5a-125">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="42f5a-125">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
> * <span data-ttu-id="42f5a-126">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="42f5a-126">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
> * <span data-ttu-id="42f5a-127">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="42f5a-127">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
> * <span data-ttu-id="42f5a-128">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="42f5a-128">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
> * <span data-ttu-id="42f5a-129">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="42f5a-129">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>

```powershell
# get an application gateway resource
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroup AdatumAppGatewayRG

# set hello SSL policy on hello application gateway
Set-AzureRmApplicationGatewaySslPolicy -ApplicationGateway $gw -PolicyType Custom -MinProtocolVersion TLSv1_1 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-an-application-gateway-with-a-pre-defined-ssl-policy"></a><span data-ttu-id="42f5a-130">Criar um gateway de aplicativo com uma política de SSL predefinida</span><span class="sxs-lookup"><span data-stu-id="42f5a-130">Create an application gateway with a pre-defined SSL policy</span></span>

<span data-ttu-id="42f5a-131">Olá exemplo a seguir cria um novo gateway de aplicativo com uma política SSL predefinida.</span><span class="sxs-lookup"><span data-stu-id="42f5a-131">hello following example creates a new application gateway with a pre-defined SSL policy.</span></span>

```powershell
# Create a resource group
$rg = New-AzureRmResourceGroup -Name ContosoRG -Location "East US"
# Create a subnet for hello application gateway
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
# Create a virtual network with a 10.0.0.0/16 address space
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName $rg.ResourceGroupName -Location "East US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
# Retrieve hello subnet object for later use
$subnet = $vnet.Subnets[0]
# Create a public IP address
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName $rg.ResourceGroupName -name publicIP01 -location "East US" -AllocationMethod Dynamic
# Create a ip configuration object
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
# Create a backend pool for backend web servers
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
# Define hello backend http settings toobe used.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
# Create a new port for SSL
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
# Upload an existing pfx certificate for SSL offload
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile C:\folder\contoso.pfx -Password "P@ssw0rd"
# Create a frontend IP configuration for hello public IP address
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
# Create a new listener with hello certificate, port, and frontend ip.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
# Create a new rule for backend traffic routing
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
# Define hello size of hello application gateway
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
# Configure hello SSL policy toouse a different pre-defined policy
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
# Create hello application gateway.
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName $rg.ResourceGroupName -Location "East US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

## <a name="next-steps"></a><span data-ttu-id="42f5a-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="42f5a-132">Next steps</span></span>

<span data-ttu-id="42f5a-133">Visite [visão geral de redirecionamento do Application Gateway](application-gateway-redirect-overview.md) toolearn como tooredirect HTTP tráfego tooa ponto de extremidade HTTPS.</span><span class="sxs-lookup"><span data-stu-id="42f5a-133">Visit [Application Gateway redirect overview](application-gateway-redirect-overview.md) toolearn how tooredirect HTTP traffic tooa HTTPS endpoint.</span></span>
