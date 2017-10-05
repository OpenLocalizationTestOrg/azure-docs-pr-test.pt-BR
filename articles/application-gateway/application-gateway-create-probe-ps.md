---
title: "Criar uma investigação personalizada - Gateway de Aplicativo do Azure - PowerShell | Microsoft Docs"
description: "Saiba como criar uma investigação personalizada para o Gateway de Aplicativo usando o PowerShell no Gerenciador de Recursos"
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
ms.openlocfilehash: b54fe5267d87a41eb9e81d5d1dc9b1b16c5c5e88
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-by-using-powershell-for-azure-resource-manager"></a><span data-ttu-id="e462b-103">Criar uma investigação personalizada para o Gateway de Aplicativo do Azure usando o PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e462b-103">Create a custom probe for Azure Application Gateway by using PowerShell for Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e462b-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e462b-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="e462b-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e462b-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="e462b-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="e462b-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="e462b-107">Neste artigo, você adiciona uma investigação personalizada a um gateway de aplicativo existente com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e462b-107">In this article, you add a custom probe to an existing application gateway with PowerShell.</span></span> <span data-ttu-id="e462b-108">As investigações personalizadas são úteis para aplicativos que tenham uma página de verificação de integridade específica ou para aplicativos que não forneçam uma resposta bem-sucedida no aplicativo Web padrão.</span><span class="sxs-lookup"><span data-stu-id="e462b-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on the default web application.</span></span>

> [!NOTE]
> <span data-ttu-id="e462b-109">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e462b-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="e462b-110">Este artigo aborda usando o modelo de implantação do Gerenciador de Recursos, que a Microsoft recomenda para a maioria das novas implantações em vez de do [modelo de implantação clássico](application-gateway-create-probe-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e462b-110">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](application-gateway-create-probe-classic-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway-with-a-custom-probe"></a><span data-ttu-id="e462b-111">Criar um gateway de aplicativo com uma investigação personalizada</span><span class="sxs-lookup"><span data-stu-id="e462b-111">Create an application gateway with a custom probe</span></span>

### <a name="sign-in-and-create-resource-group"></a><span data-ttu-id="e462b-112">Entrar e criar grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="e462b-112">Sign in and create resource group</span></span>

1. <span data-ttu-id="e462b-113">Use `Login-AzureRmAccount` para autenticar.</span><span class="sxs-lookup"><span data-stu-id="e462b-113">Use `Login-AzureRmAccount` to authenticate.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

1. <span data-ttu-id="e462b-114">Obter as assinaturas da conta.</span><span class="sxs-lookup"><span data-stu-id="e462b-114">Get the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

1. <span data-ttu-id="e462b-115">Escolha quais das suas assinaturas do Azure deseja usar.</span><span class="sxs-lookup"><span data-stu-id="e462b-115">Choose which of your Azure subscriptions to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid '{subscriptionGuid}'
  ```

1. <span data-ttu-id="e462b-116">Crie um grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="e462b-116">Create a resource group.</span></span> <span data-ttu-id="e462b-117">Você pode ignorar esta etapa se tem um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="e462b-117">You can skip this step if you have an existing resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name appgw-rg -Location 'West US'
  ```

<span data-ttu-id="e462b-118">O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local.</span><span class="sxs-lookup"><span data-stu-id="e462b-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="e462b-119">Esse local é usado como o local padrão para os recursos do grupo de recursos em questão.</span><span class="sxs-lookup"><span data-stu-id="e462b-119">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="e462b-120">Verifique se todos os comandos para criar um gateway de aplicativo usam o mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e462b-120">Make sure that all commands to create an application gateway use the same resource group.</span></span>

<span data-ttu-id="e462b-121">No exemplo anterior, criamos um grupo de recursos denominado **appgw-RG** no local **Oeste dos EUA**.</span><span class="sxs-lookup"><span data-stu-id="e462b-121">In the preceding example, we created a resource group called **appgw-RG** in location **West US**.</span></span>

### <a name="create-a-virtual-network-and-a-subnet"></a><span data-ttu-id="e462b-122">Criar uma rede virtual e uma sub-rede</span><span class="sxs-lookup"><span data-stu-id="e462b-122">Create a virtual network and a subnet</span></span>

<span data-ttu-id="e462b-123">O exemplo a seguir cria uma rede virtual e uma sub-rede para o gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e462b-123">The following example creates a virtual network and a subnet for the application gateway.</span></span> <span data-ttu-id="e462b-124">O gateway de aplicativo requer sua própria sub-rede para uso.</span><span class="sxs-lookup"><span data-stu-id="e462b-124">Application gateway requires its own subnet for use.</span></span> <span data-ttu-id="e462b-125">Por esse motivo, a sub-rede criada para o gateway de aplicativo deve ser menor que o espaço de endereço do VNET para possibilitar que outras sub-redes sejam criadas e usadas.</span><span class="sxs-lookup"><span data-stu-id="e462b-125">For this reason, the subnet created for the application gateway should be smaller than the address space of the VNET to allow for other subnets to be created and used.</span></span>

```powershell
# Assign the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network named appgwvnet in resource group appgw-rg for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Assign a subnet variable for the next steps, which create an application gateway.
$subnet = $vnet.Subnets[0]
```

### <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="e462b-126">Criar um endereço IP público para a configuração de front-end</span><span class="sxs-lookup"><span data-stu-id="e462b-126">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="e462b-127">Crie um recurso IP público **publicIP01** no grupo de recursos **appgw-rg** para a região Oeste dos EUA.</span><span class="sxs-lookup"><span data-stu-id="e462b-127">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span> <span data-ttu-id="e462b-128">Este exemplo usa um endereço IP público para o endereço IP front-end do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e462b-128">This example uses a public IP address for the front-end IP address of the application gateway.</span></span>  <span data-ttu-id="e462b-129">Como o gateway de aplicativo exige que o endereço IP público tenha um nome DNS criado dinamicamente, o `-DomainNameLabel` não pode ser especificado durante a criação do endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="e462b-129">Application gateway requires the public IP address to have a dynamically created DNS name therefore the `-DomainNameLabel` cannot be specified during the creation of the public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name publicIP01 -Location 'West US' -AllocationMethod Dynamic
```

### <a name="create-an-application-gateway"></a><span data-ttu-id="e462b-130">Criar um gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="e462b-130">Create an application gateway</span></span>

<span data-ttu-id="e462b-131">Configure todos os itens de configuração antes de criar o gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e462b-131">You set up all configuration items before creating the application gateway.</span></span> <span data-ttu-id="e462b-132">O exemplo a seguir cria os itens de configuração necessários para um recurso de gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e462b-132">The following example creates the configuration items that are needed for an application gateway resource.</span></span>

| <span data-ttu-id="e462b-133">**Componente**</span><span class="sxs-lookup"><span data-stu-id="e462b-133">**Component**</span></span> | <span data-ttu-id="e462b-134">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="e462b-134">**Description**</span></span> |
|---|---|
| <span data-ttu-id="e462b-135">**Configuração de IP do gateway**</span><span class="sxs-lookup"><span data-stu-id="e462b-135">**Gateway IP configuration**</span></span> | <span data-ttu-id="e462b-136">Uma configuração de IP para um gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e462b-136">An IP configuration for an application gateway.</span></span>|
| <span data-ttu-id="e462b-137">**Pool de back-end**</span><span class="sxs-lookup"><span data-stu-id="e462b-137">**Backend pool**</span></span> | <span data-ttu-id="e462b-138">Um pool de endereços IP, FQDNs ou NICs que são para os servidores de aplicativos que hospedam o aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="e462b-138">A pool of IP addresses, FQDN's, or NICs that are to the application servers that host the web application</span></span>|
| <span data-ttu-id="e462b-139">**Investigação de integridade**</span><span class="sxs-lookup"><span data-stu-id="e462b-139">**Health probe**</span></span> | <span data-ttu-id="e462b-140">Uma investigação personalizada usada para monitorar a integridade dos membros do pool de back-end</span><span class="sxs-lookup"><span data-stu-id="e462b-140">A custom probe used to monitor the health of the backend pool members</span></span>|
| <span data-ttu-id="e462b-141">**Configurações HTTP**</span><span class="sxs-lookup"><span data-stu-id="e462b-141">**HTTP settings**</span></span> | <span data-ttu-id="e462b-142">Uma coleção de configurações, inclusive porta, protocolo, afinidade baseada em cookie, investigação e tempo limite.</span><span class="sxs-lookup"><span data-stu-id="e462b-142">A collection of settings including, port, protocol, cookie-based affinity, probe, and timeout.</span></span>  <span data-ttu-id="e462b-143">Essas configurações determinam como o tráfego é roteado para os membros do pool de back-end</span><span class="sxs-lookup"><span data-stu-id="e462b-143">These settings determine how traffic is routed to the backend pool members</span></span>|
| <span data-ttu-id="e462b-144">**Porta de front-end**</span><span class="sxs-lookup"><span data-stu-id="e462b-144">**Frontend port**</span></span> | <span data-ttu-id="e462b-145">A porta em que o gateway de aplicativo escuta tráfego</span><span class="sxs-lookup"><span data-stu-id="e462b-145">The port that the application gateway listens for traffic on</span></span>|
| <span data-ttu-id="e462b-146">**Ouvinte**</span><span class="sxs-lookup"><span data-stu-id="e462b-146">**Listener**</span></span> | <span data-ttu-id="e462b-147">Uma combinação de um protocolo, configuração de IP front-end e porta front-end.</span><span class="sxs-lookup"><span data-stu-id="e462b-147">A combination of a protocol, frontend IP configuration, and frontend port.</span></span> <span data-ttu-id="e462b-148">É o que escuta solicitações de entrada.</span><span class="sxs-lookup"><span data-stu-id="e462b-148">This is what listens for incoming requests.</span></span>
|<span data-ttu-id="e462b-149">**Regra**</span><span class="sxs-lookup"><span data-stu-id="e462b-149">**Rule**</span></span>| <span data-ttu-id="e462b-150">Roteia o tráfego para o back-end apropriado com base em configurações de HTTP.</span><span class="sxs-lookup"><span data-stu-id="e462b-150">Routes the traffic to the appropriate backend based on HTTP settings.</span></span>|

```powershell
# Creates a application gateway Frontend IP configuration named gatewayIP01
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

#Creates a back-end IP address pool named pool01 with IP addresses 134.170.185.46, 134.170.188.221, 134.170.185.50.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Creates a probe that will check health at http://contoso.com/path/path.htm
$probe = New-AzureRmApplicationGatewayProbeConfig -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/path.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Creates the backend http settings to be used. This component references the $probe created in the previous command.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 80

# Creates a frontend port for the application gateway to listen on port 80 that will be used by the listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01 -Port 80

# Creates a frontend IP configuration. This associates the $publicip variable defined previously with the front-end IP that will be used by the listener.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Creates the listener. The listener is a combination of protocol and the frontend IP configuration $fipconfig and frontend port $fp created in previous steps.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Creates the rule that routes traffic to the backend pools.  In this example we create a basic rule that uses the previous defined http settings and backend address pool.  It also associates the listener to the rule
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Sets the SKU of the application gateway, in this example we create a small standard application gateway with 2 instances.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# The final step creates the application gateway with all the previously defined components.
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location 'West US' -BackendAddressPools $pool -Probes $probe -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

## <a name="add-a-probe-to-an-existing-application-gateway"></a><span data-ttu-id="e462b-151">Adicionar uma investigação a um Application Gateway existente</span><span class="sxs-lookup"><span data-stu-id="e462b-151">Add a probe to an existing application gateway</span></span>

<span data-ttu-id="e462b-152">O trecho de código a seguir adiciona uma investigação a um gateway de aplicativo existente.</span><span class="sxs-lookup"><span data-stu-id="e462b-152">The following code snippet adds a probe to an existing application gateway.</span></span>

```powershell
# Load the application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Create the probe object that will check health at http://contoso.com/path/path.htm
$getgw = Add-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/custompath.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Set the backend HTTP settings to use the new probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 120

# Save the application gateway with the configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="remove-a-probe-from-an-existing-application-gateway"></a><span data-ttu-id="e462b-153">Remover uma investigação de um Application Gateway existente</span><span class="sxs-lookup"><span data-stu-id="e462b-153">Remove a probe from an existing application gateway</span></span>

<span data-ttu-id="e462b-154">O trecho de código a seguir remove uma investigação de um gateway de aplicativo existente.</span><span class="sxs-lookup"><span data-stu-id="e462b-154">The following code snippet removes a probe from an existing application gateway.</span></span>

```powershell
# Load the application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Remove the probe from the application gateway configuration object
$getgw = Remove-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name $getgw.Probes.name

# Set the backend HTTP settings to remove the reference to the probe. The backend http settings now use the default probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol http -CookieBasedAffinity Disabled

# Save the application gateway with the configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="e462b-155">Obter um nome DNS de gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="e462b-155">Get application gateway DNS name</span></span>

<span data-ttu-id="e462b-156">Depois de criar o gateway, a próxima etapa será configurar o front-end para comunicação.</span><span class="sxs-lookup"><span data-stu-id="e462b-156">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="e462b-157">Ao usar um IP público, o gateway de aplicativo requer um nome DNS atribuído dinamicamente, o que não é amigável.</span><span class="sxs-lookup"><span data-stu-id="e462b-157">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="e462b-158">Para garantir que os usuários finais possam alcançar o gateway de aplicativo, um registro CNAME pode ser usado para apontar para o ponto de extremidade público do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e462b-158">To ensure end users can hit the application gateway a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="e462b-159">[Configurando um nome de domínio personalizado no Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e462b-159">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="e462b-160">Para isso, recupere detalhes do Gateway de Aplicativo e seu nome DNS/IP associado usando o elemento PublicIPAddress anexado ao Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e462b-160">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="e462b-161">O nome DNS do Gateway de Aplicativo deve ser usado para criar um registro CNAME que aponta os dois aplicativos Web para esse nome DNS.</span><span class="sxs-lookup"><span data-stu-id="e462b-161">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="e462b-162">O uso de registros A não é recomendável, pois o VIP pode mudar na reinicialização do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e462b-162">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e462b-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e462b-163">Next steps</span></span>

<span data-ttu-id="e462b-164">Saiba como configurar o descarregamento de SSL ao visitar [Configurar descarregamento de SSL](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="e462b-164">Learn to configure SSL offloading by visiting: [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

