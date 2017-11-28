---
title: aaaCreate e gerenciar um Gateway de aplicativo do Azure - PowerShell | Microsoft Docs
description: "Esta página fornece instruções toocreate, configurar, iniciar e excluir um gateway de aplicativo do Azure usando o Gerenciador de recursos do Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: ab98d5f9aa0dc309f8353b7f72591359e1121849
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-by-using-azure-resource-manager"></a><span data-ttu-id="44991-103">Criar, iniciar ou excluir um gateway de aplicativo usando o Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="44991-103">Create, start, or delete an application gateway by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="44991-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="44991-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="44991-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="44991-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="44991-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="44991-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="44991-107">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="44991-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="44991-108">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="44991-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="44991-109">O Gateway de Aplicativo do Azure é um balanceador de carga de camada 7.</span><span class="sxs-lookup"><span data-stu-id="44991-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="44991-110">Ele fornece failover e roteamento de desempenho de solicitações HTTP entre diferentes servidores, independentemente de estarem em nuvem hello ou local.</span><span class="sxs-lookup"><span data-stu-id="44991-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="44991-111">O Gateway de Aplicativo fornece muitos recursos do ADC (Controlador de entrega de aplicativos), incluindo o balanceamento de carga de HTTP, a afinidade de sessão baseada em cookies, o descarregamento de protocolo SSL (Secure Sockets Layer), as sondas de integridade personalizadas, suporte para vários sites e muitos outros.</span><span class="sxs-lookup"><span data-stu-id="44991-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="44991-112">toofind uma lista completa de recursos com suporte, visite [visão geral do Application Gateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="44991-112">toofind a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md).</span></span>

<span data-ttu-id="44991-113">Este artigo orienta Olá etapas toocreate, configurar, iniciar e excluir um application gateway.</span><span class="sxs-lookup"><span data-stu-id="44991-113">This article walks you through hello steps toocreate, configure, start, and delete an application gateway.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44991-114">Antes de trabalhar com recursos do Azure, é importante toounderstand que o Azure atualmente tem dois modelos de implantação: Gerenciador de recursos e clássico.</span><span class="sxs-lookup"><span data-stu-id="44991-114">Before you work with Azure resources, it is important toounderstand that Azure currently has two deployment models: Resource Manager and classic.</span></span> <span data-ttu-id="44991-115">Verifique se você entendeu [os modelos e as ferramentas de implantação](../azure-classic-rm.md) antes de trabalhar com qualquer recurso do Azure.</span><span class="sxs-lookup"><span data-stu-id="44991-115">Make sure that you understand [deployment models and tools](../azure-classic-rm.md) before working with any Azure resource.</span></span> <span data-ttu-id="44991-116">Você pode exibir a documentação de saudação para diferentes ferramentas clicando Olá guias na parte superior da saudação deste artigo.</span><span class="sxs-lookup"><span data-stu-id="44991-116">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="44991-117">Este documento aborda a criação de um gateway de aplicativo usando o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="44991-117">This document covers creating an application gateway by using Azure Resource Manager.</span></span> <span data-ttu-id="44991-118">versão clássica do toouse hello, ir muito[criar um gateway clássico a implantação usando o PowerShell](application-gateway-create-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="44991-118">toouse hello classic version, go too[Create an application gateway classic deployment by using PowerShell](application-gateway-create-gateway.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="44991-119">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="44991-119">Before you begin</span></span>

1. <span data-ttu-id="44991-120">Instale a versão mais recente Olá Olá Azure de cmdlets do PowerShell usando Olá Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="44991-120">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="44991-121">Você pode baixar e instalar a versão mais recente de saudação do hello **do Windows PowerShell** seção Olá [página de Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="44991-121">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
1. <span data-ttu-id="44991-122">Se você tiver uma rede virtual existente, selecione uma sub-rede vazia existente ou crie uma sub-rede na rede virtual existente unicamente para uso pelo gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="44991-122">If you have an existing virtual network, either select an existing empty subnet or create a subnet in your existing virtual network solely for use by hello application gateway.</span></span> <span data-ttu-id="44991-123">Não é possível implantar Olá application gateway tooa rede virtual diferente de recursos de saudação pretende toodeploy por trás do gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="44991-123">You cannot deploy hello application gateway tooa different virtual network than hello resources you intend toodeploy behind hello application gateway.</span></span>
1. <span data-ttu-id="44991-124">servidores de saudação que você configure o gateway de aplicativo hello toouse devem existir ou seus pontos de extremidade criados na rede virtual hello ou com um IP público/VIP atribuídos.</span><span class="sxs-lookup"><span data-stu-id="44991-124">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="44991-125">O que é necessário toocreate um application gateway?</span><span class="sxs-lookup"><span data-stu-id="44991-125">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="44991-126">**Pool de servidores de back-end:** lista de saudação de placas de rede de servidores de back-end de saudação, FQDNs ou endereços IP.</span><span class="sxs-lookup"><span data-stu-id="44991-126">**Backend server pool:** hello list of IP addresses, FQDNs, or NICs of hello backend servers.</span></span> <span data-ttu-id="44991-127">Se os endereços IP são usados, eles ou devem pertencer a sub-rede da rede virtual toohello ou devem ser um IP público/VIP.</span><span class="sxs-lookup"><span data-stu-id="44991-127">If IP addresses are used, they should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="44991-128">**Configurações do pool de servidores back-end:** cada pool tem configurações como porta, protocolo e afinidade baseada em cookies.</span><span class="sxs-lookup"><span data-stu-id="44991-128">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="44991-129">Essas configurações são tooa empatado pool e são aplicados tooall servidores no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="44991-129">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="44991-130">**porta de front-end:** essa porta é a porta pública de saudação que é aberta no gateway do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="44991-130">**frontend port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="44991-131">Tráfego atinge a essa porta e, em seguida, obtém tooone redirecionado de servidores de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="44991-131">Traffic hits this port, and then gets redirected tooone of hello backend servers.</span></span>
* <span data-ttu-id="44991-132">**Ouvinte:** ouvinte Olá tem uma porta de front-end, um protocolo (Http ou Https, esses valores diferenciam maiusculas de minúsculas) e o nome do certificado SSL de saudação (se a configuração de SSL de descarregamento).</span><span class="sxs-lookup"><span data-stu-id="44991-132">**Listener:** hello listener has a frontend port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="44991-133">**Regra:** regra Olá associa ouvinte hello, pool de servidores de back-end hello e define qual tráfego Olá pool do servidor de back-end deve ser direcionado toowhen que ele atinja um ouvinte específico.</span><span class="sxs-lookup"><span data-stu-id="44991-133">**Rule:** hello rule binds hello listener, hello backend server pool and defines which backend server pool hello traffic should be directed toowhen it hits a particular listener.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="44991-134">Criar um grupo de recursos para o Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="44991-134">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="44991-135">Certifique-se de que você estiver usando a versão mais recente de saudação do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="44991-135">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="44991-136">Há mais informações disponíveis em [Como usar o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="44991-136">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="44991-137">Faça logon no tooAzure e insira suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="44991-137">Log in tooAzure and enter your credentials.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="44991-138">Verificar as assinaturas de saudação para conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="44991-138">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

3. <span data-ttu-id="44991-139">Escolha qual toouse suas assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="44991-139">Choose which of your Azure subscriptions toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
  ```

4. <span data-ttu-id="44991-140">Crie um grupo de recursos (ignore esta etapa se você estiver usando um grupo de recursos existente).</span><span class="sxs-lookup"><span data-stu-id="44991-140">Create a resource group (skip this step if you're using an existing resource group).</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name ContosoRG -Location "West US"
  ```

<span data-ttu-id="44991-141">O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local.</span><span class="sxs-lookup"><span data-stu-id="44991-141">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="44991-142">Esse local é usado como o local padrão de saudação para recursos desse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="44991-142">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="44991-143">Certifique-se de que todos os toocreate de comandos usa um application gateway Olá mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="44991-143">Make sure that all commands toocreate an application gateway uses hello same resource group.</span></span>

<span data-ttu-id="44991-144">O exemplo hello acima, criamos um grupo de recursos chamado **ContosoRG** e local **Leste dos EUA**.</span><span class="sxs-lookup"><span data-stu-id="44991-144">In hello example above, we created a resource group called **ContosoRG** and location **East US**.</span></span>

> [!NOTE]
> <span data-ttu-id="44991-145">Se você precisar tooconfigure uma investigação personalizada para o gateway de aplicativo, visite: [criar um gateway de aplicativos com testes personalizados usando o PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="44991-145">If you need tooconfigure a custom probe for your application gateway, visit: [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="44991-146">Confira [investigações personalizadas e monitoramento de integridade](application-gateway-probe-overview.md) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="44991-146">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>


## <a name="create-hello-application-gateway-configuration-objects"></a><span data-ttu-id="44991-147">Criar objetos de configuração de gateway do aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="44991-147">Create hello application gateway configuration objects</span></span>

<span data-ttu-id="44991-148">Todos os itens de configuração devem ser configurados antes de criar o gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="44991-148">All configuration items must be set up before creating hello application gateway.</span></span> <span data-ttu-id="44991-149">Olá etapas a seguir criam Olá itens de configuração que são necessárias para um recurso do application gateway.</span><span class="sxs-lookup"><span data-stu-id="44991-149">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

```powershell
# Create a subnet and assign hello address space of 10.0.0.0/24
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network with hello address space of 10.0.0.0/16 and add hello subnet
$vnet = New-AzureRmVirtualNetwork -Name ContosoVNET -ResourceGroupName ContosoRG -Location "East US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Retrieve hello newly created subnet
$subnet=$vnet.Subnets[0]

# Create a public IP address that is used tooconnect toohello application gateway. Application Gateway does not support custom DNS names on public IP addresses.  If a custom name is required for hello public endpoint, a CNAME record should be created toopoint toohello automatically generated DNS name for hello public IP address.
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -name publicIP01 -location "East US" -AllocationMethod Dynamic

# Create a gateway IP configuration. hello gateway picks up an IP addressfrom hello configured subnet and routes network traffic toohello IP addresses in hello backend IP pool. Keep in mind that each instance takes one IP address.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

# Configure a backend pool with hello addresses of your web servers. These backend pool members are all validated toobe healthy by probes, whether they are basic probes or custom probes.  Traffic is then routed toothem when requests come into hello application gateway. Backend pools can be used by multiple rules within hello application gateway, which means one backend pool could be used for multiple web applications that reside on hello same host.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Configure backend http settings toodetermine hello protocol and port that is used when sending traffic toohello backend servers. Cookie-based sessions are also determined by hello backend HTTP settings.  If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

# Configure a frontend port that is used tooconnect toohello application gateway through hello public IP address
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80

# Configure hello frontend IP configuration with hello public IP address created earlier.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Configure hello listener.  hello listener is a combination of hello front end IP configuration, protocol, and port and is used tooreceive incoming network traffic. 
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Configure a basic rule that is used tooroute traffic toohello backend servers. hello backend pool settings, listener, and backend pool created in hello previous steps make up hello rule. Based on hello criteria defined traffic is routed toohello appropriate backend.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure hello SKU for hello application gateway, this determines hello size and whether or not WAF is used.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# Create hello application gateway
$appgw = New-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Location "East US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="44991-150">Ao concluir, recupere detalhes DNS e o VIP do gateway de aplicativo hello do gateway Olá pública IP recursos anexado toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="44991-150">When complete, retrieve DNS and VIP details of hello application gateway from hello public IP resource attached toohello application gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name publicIP01 -ResourceGroupName ContosoRG
```

## <a name="delete-hello-application-gateway"></a><span data-ttu-id="44991-151">Excluir o hello application gateway</span><span class="sxs-lookup"><span data-stu-id="44991-151">Delete hello application gateway</span></span>

<span data-ttu-id="44991-152">Olá, exemplo a seguir exclui o gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="44991-152">hello following example deletes hello application gateway.</span></span>

```powershell
# Retrieve hello application gateway
$gw = Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG

# Stops hello application gateway
Stop-AzureRmApplicationGateway -ApplicationGateway $gw

# Once hello application gateway is in a stopped state, use hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello service.
Remove-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Force
```

> [!NOTE]
> <span data-ttu-id="44991-153">Olá **-force** switch pode ser uma mensagem de confirmação de remoção toosuppress usado Olá.</span><span class="sxs-lookup"><span data-stu-id="44991-153">hello **-force** switch can be used toosuppress hello remove confirmation message.</span></span>

<span data-ttu-id="44991-154">tooverify que Olá serviço foi removido, você pode usar o hello `Get-AzureRmApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="44991-154">tooverify that hello service has been removed, you can use hello `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="44991-155">Essa etapa não é necessária.</span><span class="sxs-lookup"><span data-stu-id="44991-155">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="44991-156">Obter um nome DNS de Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="44991-156">Get application gateway DNS name</span></span>

<span data-ttu-id="44991-157">Depois de criar o gateway hello, Olá próxima etapa é tooconfigure Olá front-end para comunicação.</span><span class="sxs-lookup"><span data-stu-id="44991-157">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="44991-158">Ao usar um IP público, o gateway de aplicativo requer um nome DNS atribuído dinamicamente, o que não é amigável.</span><span class="sxs-lookup"><span data-stu-id="44991-158">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="44991-159">os usuários finais de tooensure pode pressionar o gateway de aplicativo hello, um registro CNAME pode ser usado toopoint toohello ponto de extremidade público do gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="44991-159">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="44991-160">toodo, detalhes de recuperar de gateway de aplicativo hello e seu nome de IP/DNS associado usando Olá PublicIPAddress elemento toohello anexado application gateway.</span><span class="sxs-lookup"><span data-stu-id="44991-160">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="44991-161">Isso pode ser feito com o DNS do Azure ou outros provedores DNS, por criar um registro CNAME que aponte toohello [endereço IP público](../dns/dns-custom-domain.md#public-ip-address).</span><span class="sxs-lookup"><span data-stu-id="44991-161">This can be done with Azure DNS or other DNS providers, by creating a CNAME record that points toohello [public IP address](../dns/dns-custom-domain.md#public-ip-address).</span></span> <span data-ttu-id="44991-162">uso de saudação de registros de um não é recomendável porque Olá VIP pode ser alterado na reinicialização do application gateway.</span><span class="sxs-lookup"><span data-stu-id="44991-162">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="44991-163">Um endereço IP é atribuído gateway de aplicativo toohello quando Olá serviço é iniciado.</span><span class="sxs-lookup"><span data-stu-id="44991-163">An IP address is assigned toohello application gateway when hello service starts.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : ContosoRG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/ContosoRG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/ContosoAppGateway/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="delete-all-resources"></a><span data-ttu-id="44991-164">Excluir todos os recursos</span><span class="sxs-lookup"><span data-stu-id="44991-164">Delete all resources</span></span>

<span data-ttu-id="44991-165">toodelete todos os recursos criados neste artigo, Olá completa etapa a seguir:</span><span class="sxs-lookup"><span data-stu-id="44991-165">toodelete all resources created in this article, complete hello following step:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name ContosoRG
```

## <a name="next-steps"></a><span data-ttu-id="44991-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="44991-166">Next steps</span></span>

<span data-ttu-id="44991-167">Se você quiser tooconfigure descarregamento de SSL, visite: [Configure um gateway de aplicativo para descarregamento SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="44991-167">If you want tooconfigure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="44991-168">Se você quiser tooconfigure um toouse de gateway do aplicativo com um balanceador de carga interno, visite: [criar um gateway de aplicativo com um balanceador de carga interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="44991-168">If you want tooconfigure an application gateway toouse with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="44991-169">Se deseja saber mais sobre as opções de balanceamento de carga no geral, visite:</span><span class="sxs-lookup"><span data-stu-id="44991-169">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="44991-170">Balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="44991-170">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="44991-171">Gerenciador de Tráfego do Azure</span><span class="sxs-lookup"><span data-stu-id="44991-171">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)
