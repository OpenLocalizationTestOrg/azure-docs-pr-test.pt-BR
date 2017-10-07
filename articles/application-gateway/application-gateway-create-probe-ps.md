---
title: "aaaCreate um personalizado investigação - Gateway de aplicativo do Azure - PowerShell | Microsoft Docs"
description: Saiba como toocreate um personalizado teste para o Application Gateway usando o PowerShell no Gerenciador de recursos
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68feb660-7fa4-4f69-a7e4-bdd7bdc474db
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 44c9ffa75401d6d0db023e66fa82c701fb0cf8bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-by-using-powershell-for-azure-resource-manager"></a><span data-ttu-id="e5151-103">Criar uma investigação personalizada para o Gateway de Aplicativo do Azure usando o PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e5151-103">Create a custom probe for Azure Application Gateway by using PowerShell for Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e5151-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e5151-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="e5151-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e5151-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="e5151-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="e5151-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="e5151-107">Neste artigo, você deve adicionar um gateway de aplicativo existente do investigação personalizada tooan com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e5151-107">In this article, you add a custom probe tooan existing application gateway with PowerShell.</span></span> <span data-ttu-id="e5151-108">Testes personalizados são úteis para aplicativos que têm uma página de verificação de integridade específicas ou para aplicativos que não fornecem uma resposta bem-sucedida no aplicativo de web saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="e5151-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on hello default web application.</span></span>

> [!NOTE]
> <span data-ttu-id="e5151-109">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e5151-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="e5151-110">Este artigo aborda usando o modelo de implantação do hello Gerenciador de recursos, a Microsoft recomenda para a maioria das novas implantações em vez da saudação [modelo de implantação clássico](application-gateway-create-probe-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e5151-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](application-gateway-create-probe-classic-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway-with-a-custom-probe"></a><span data-ttu-id="e5151-111">Criar um gateway de aplicativo com uma investigação personalizada</span><span class="sxs-lookup"><span data-stu-id="e5151-111">Create an application gateway with a custom probe</span></span>

### <a name="sign-in-and-create-resource-group"></a><span data-ttu-id="e5151-112">Entrar e criar grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="e5151-112">Sign in and create resource group</span></span>

1. <span data-ttu-id="e5151-113">Use `Login-AzureRmAccount` tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="e5151-113">Use `Login-AzureRmAccount` tooauthenticate.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

1. <span data-ttu-id="e5151-114">Obter assinaturas Olá para conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="e5151-114">Get hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

1. <span data-ttu-id="e5151-115">Escolha qual toouse suas assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5151-115">Choose which of your Azure subscriptions toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid '{subscriptionGuid}'
  ```

1. <span data-ttu-id="e5151-116">Crie um grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="e5151-116">Create a resource group.</span></span> <span data-ttu-id="e5151-117">Você pode ignorar esta etapa se tem um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="e5151-117">You can skip this step if you have an existing resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name appgw-rg -Location 'West US'
  ```

<span data-ttu-id="e5151-118">O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local.</span><span class="sxs-lookup"><span data-stu-id="e5151-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="e5151-119">Esse local é usado como o local padrão de saudação para recursos desse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e5151-119">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="e5151-120">Certifique-se de que todos os comandos toocreate uma saudação de uso de gateway de aplicativo mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e5151-120">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

<span data-ttu-id="e5151-121">Em Olá anterior de exemplo, criamos um grupo de recursos chamado **appgw RG** no local **Oeste dos EUA**.</span><span class="sxs-lookup"><span data-stu-id="e5151-121">In hello preceding example, we created a resource group called **appgw-RG** in location **West US**.</span></span>

### <a name="create-a-virtual-network-and-a-subnet"></a><span data-ttu-id="e5151-122">Criar uma rede virtual e uma sub-rede</span><span class="sxs-lookup"><span data-stu-id="e5151-122">Create a virtual network and a subnet</span></span>

<span data-ttu-id="e5151-123">Olá exemplo a seguir cria uma rede virtual e uma sub-rede para o gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="e5151-123">hello following example creates a virtual network and a subnet for hello application gateway.</span></span> <span data-ttu-id="e5151-124">O gateway de aplicativo requer sua própria sub-rede para uso.</span><span class="sxs-lookup"><span data-stu-id="e5151-124">Application gateway requires its own subnet for use.</span></span> <span data-ttu-id="e5151-125">Por esse motivo, sub-rede Olá criado para o gateway de aplicativo hello deve ser menor que o espaço de endereço de saudação do hello VNET tooallow para toobe outras sub-redes criado e usado.</span><span class="sxs-lookup"><span data-stu-id="e5151-125">For this reason, hello subnet created for hello application gateway should be smaller than hello address space of hello VNET tooallow for other subnets toobe created and used.</span></span>

```powershell
# Assign hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network named appgwvnet in resource group appgw-rg for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Assign a subnet variable for hello next steps, which create an application gateway.
$subnet = $vnet.Subnets[0]
```

### <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="e5151-126">Criar um endereço IP público para a configuração de front-end Olá</span><span class="sxs-lookup"><span data-stu-id="e5151-126">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="e5151-127">Criar um recurso IP público **publicIP01** no grupo de recursos **appgw rg** para região Oeste dos EUA de saudação.</span><span class="sxs-lookup"><span data-stu-id="e5151-127">Create a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span> <span data-ttu-id="e5151-128">Este exemplo usa um endereço IP público para o endereço IP front-end de saudação do gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="e5151-128">This example uses a public IP address for hello front-end IP address of hello application gateway.</span></span>  <span data-ttu-id="e5151-129">Gateway de aplicativo requer Olá pública IP endereço toohave um nome DNS criado dinamicamente, portanto, Olá `-DomainNameLabel` não pode ser especificado durante a criação de saudação do endereço IP público de saudação.</span><span class="sxs-lookup"><span data-stu-id="e5151-129">Application gateway requires hello public IP address toohave a dynamically created DNS name therefore hello `-DomainNameLabel` cannot be specified during hello creation of hello public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name publicIP01 -Location 'West US' -AllocationMethod Dynamic
```

### <a name="create-an-application-gateway"></a><span data-ttu-id="e5151-130">Criar um Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="e5151-130">Create an application gateway</span></span>

<span data-ttu-id="e5151-131">Você pode configurar todos os itens de configuração antes de criar o gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="e5151-131">You set up all configuration items before creating hello application gateway.</span></span> <span data-ttu-id="e5151-132">Olá exemplo a seguir cria Olá itens de configuração que são necessárias para um recurso do application gateway.</span><span class="sxs-lookup"><span data-stu-id="e5151-132">hello following example creates hello configuration items that are needed for an application gateway resource.</span></span>

| <span data-ttu-id="e5151-133">**Componente**</span><span class="sxs-lookup"><span data-stu-id="e5151-133">**Component**</span></span> | <span data-ttu-id="e5151-134">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="e5151-134">**Description**</span></span> |
|---|---|
| <span data-ttu-id="e5151-135">**Configuração de IP do gateway**</span><span class="sxs-lookup"><span data-stu-id="e5151-135">**Gateway IP configuration**</span></span> | <span data-ttu-id="e5151-136">Uma configuração de IP para um gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e5151-136">An IP configuration for an application gateway.</span></span>|
| <span data-ttu-id="e5151-137">**Pool de back-end**</span><span class="sxs-lookup"><span data-stu-id="e5151-137">**Backend pool**</span></span> | <span data-ttu-id="e5151-138">Um pool de endereços IP, FQDN ou NICs toohello servidores de aplicativos que hospedam o aplicativo da web hello</span><span class="sxs-lookup"><span data-stu-id="e5151-138">A pool of IP addresses, FQDN's, or NICs that are toohello application servers that host hello web application</span></span>|
| <span data-ttu-id="e5151-139">**Investigação de integridade**</span><span class="sxs-lookup"><span data-stu-id="e5151-139">**Health probe**</span></span> | <span data-ttu-id="e5151-140">Uma investigação personalizada usada toomonitor integridade de saudação de membros do pool de back-end Olá</span><span class="sxs-lookup"><span data-stu-id="e5151-140">A custom probe used toomonitor hello health of hello backend pool members</span></span>|
| <span data-ttu-id="e5151-141">**Configurações HTTP**</span><span class="sxs-lookup"><span data-stu-id="e5151-141">**HTTP settings**</span></span> | <span data-ttu-id="e5151-142">Uma coleção de configurações, inclusive porta, protocolo, afinidade baseada em cookie, investigação e tempo limite.</span><span class="sxs-lookup"><span data-stu-id="e5151-142">A collection of settings including, port, protocol, cookie-based affinity, probe, and timeout.</span></span>  <span data-ttu-id="e5151-143">Essas configurações determinam como o tráfego é roteado toohello membros do pool de back-end</span><span class="sxs-lookup"><span data-stu-id="e5151-143">These settings determine how traffic is routed toohello backend pool members</span></span>|
| <span data-ttu-id="e5151-144">**Porta de front-end**</span><span class="sxs-lookup"><span data-stu-id="e5151-144">**Frontend port**</span></span> | <span data-ttu-id="e5151-145">porta Olá Olá gateway aplicativo ouve o tráfego em</span><span class="sxs-lookup"><span data-stu-id="e5151-145">hello port that hello application gateway listens for traffic on</span></span>|
| <span data-ttu-id="e5151-146">**Ouvinte**</span><span class="sxs-lookup"><span data-stu-id="e5151-146">**Listener**</span></span> | <span data-ttu-id="e5151-147">Uma combinação de um protocolo, configuração de IP front-end e porta front-end.</span><span class="sxs-lookup"><span data-stu-id="e5151-147">A combination of a protocol, frontend IP configuration, and frontend port.</span></span> <span data-ttu-id="e5151-148">É o que escuta solicitações de entrada.</span><span class="sxs-lookup"><span data-stu-id="e5151-148">This is what listens for incoming requests.</span></span>
|<span data-ttu-id="e5151-149">**Regra**</span><span class="sxs-lookup"><span data-stu-id="e5151-149">**Rule**</span></span>| <span data-ttu-id="e5151-150">Rotas Olá tráfego toohello apropriado back-end com base nas configurações de HTTP.</span><span class="sxs-lookup"><span data-stu-id="e5151-150">Routes hello traffic toohello appropriate backend based on HTTP settings.</span></span>|

```powershell
# Creates a application gateway Frontend IP configuration named gatewayIP01
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

#Creates a back-end IP address pool named pool01 with IP addresses 134.170.185.46, 134.170.188.221, 134.170.185.50.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Creates a probe that will check health at http://contoso.com/path/path.htm
$probe = New-AzureRmApplicationGatewayProbeConfig -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/path.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Creates hello backend http settings toobe used. This component references hello $probe created in hello previous command.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 80

# Creates a frontend port for hello application gateway toolisten on port 80 that will be used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01 -Port 80

# Creates a frontend IP configuration. This associates hello $publicip variable defined previously with hello front-end IP that will be used by hello listener.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Creates hello listener. hello listener is a combination of protocol and hello frontend IP configuration $fipconfig and frontend port $fp created in previous steps.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Creates hello rule that routes traffic toohello backend pools.  In this example we create a basic rule that uses hello previous defined http settings and backend address pool.  It also associates hello listener toohello rule
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Sets hello SKU of hello application gateway, in this example we create a small standard application gateway with 2 instances.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# hello final step creates hello application gateway with all hello previously defined components.
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location 'West US' -BackendAddressPools $pool -Probes $probe -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

## <a name="add-a-probe-tooan-existing-application-gateway"></a><span data-ttu-id="e5151-151">Adicionar um gateway de aplicativo existente do teste tooan</span><span class="sxs-lookup"><span data-stu-id="e5151-151">Add a probe tooan existing application gateway</span></span>

<span data-ttu-id="e5151-152">Olá trecho de código a seguir adiciona um gateway de aplicativo investigação tooan existente.</span><span class="sxs-lookup"><span data-stu-id="e5151-152">hello following code snippet adds a probe tooan existing application gateway.</span></span>

```powershell
# Load hello application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Create hello probe object that will check health at http://contoso.com/path/path.htm
$getgw = Add-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/custompath.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Set hello backend HTTP settings toouse hello new probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 120

# Save hello application gateway with hello configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="remove-a-probe-from-an-existing-application-gateway"></a><span data-ttu-id="e5151-153">Remover uma investigação de um Application Gateway existente</span><span class="sxs-lookup"><span data-stu-id="e5151-153">Remove a probe from an existing application gateway</span></span>

<span data-ttu-id="e5151-154">Olá trecho de código a seguir remove um teste de um gateway existente do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e5151-154">hello following code snippet removes a probe from an existing application gateway.</span></span>

```powershell
# Load hello application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Remove hello probe from hello application gateway configuration object
$getgw = Remove-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name $getgw.Probes.name

# Set hello backend HTTP settings tooremove hello reference toohello probe. hello backend http settings now use hello default probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol http -CookieBasedAffinity Disabled

# Save hello application gateway with hello configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="e5151-155">Obter um nome DNS de Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="e5151-155">Get application gateway DNS name</span></span>

<span data-ttu-id="e5151-156">Depois de criar o gateway hello, Olá próxima etapa é tooconfigure Olá front-end para comunicação.</span><span class="sxs-lookup"><span data-stu-id="e5151-156">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="e5151-157">Ao usar um IP público, o gateway de aplicativo requer um nome DNS atribuído dinamicamente, o que não é amigável.</span><span class="sxs-lookup"><span data-stu-id="e5151-157">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="e5151-158">os usuários finais de tooensure pode pressionar o gateway de aplicativo hello pode ser usado um registro CNAME toopoint toohello ponto de extremidade público do gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="e5151-158">tooensure end users can hit hello application gateway a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="e5151-159">[Configurando um nome de domínio personalizado no Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e5151-159">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="e5151-160">toodo, detalhes de recuperar de gateway de aplicativo hello e seu nome de IP/DNS associado usando Olá PublicIPAddress elemento toohello anexado application gateway.</span><span class="sxs-lookup"><span data-stu-id="e5151-160">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="e5151-161">nome DNS do gateway do aplicativo Hello deve ser usado toocreate um registro CNAME, qual nome DNS pontos Olá duas web aplicativos toothis.</span><span class="sxs-lookup"><span data-stu-id="e5151-161">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="e5151-162">uso de saudação de registros de um não é recomendável porque Olá VIP pode ser alterado na reinicialização do application gateway.</span><span class="sxs-lookup"><span data-stu-id="e5151-162">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e5151-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e5151-163">Next steps</span></span>

<span data-ttu-id="e5151-164">Saiba o descarregamento de SSL tooconfigure visitando: [configurar descarregamento de SSL](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="e5151-164">Learn tooconfigure SSL offloading by visiting: [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

