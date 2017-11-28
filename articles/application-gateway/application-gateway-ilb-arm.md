---
title: aaaUsing Gateway de aplicativo do Azure com o balanceador de carga interno - PowerShell | Microsoft Docs
description: "Esta página fornece instruções toocreate, configurar, iniciar e excluir um gateway de aplicativo do Azure com o balanceador de carga interno (ILB) para o Gerenciador de recursos do Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 75cfd5a2-e378-4365-99ee-a2b2abda2e0d
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: dd0d7e954b1fa219ae6ebe42cb4b479dbcf08653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb-by-using-azure-resource-manager"></a><span data-ttu-id="20299-103">Criar um gateway de aplicativo com um ILB (balanceador de carga interno) usando o Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="20299-103">Create an application gateway with an internal load balancer (ILB) by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="20299-104">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="20299-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="20299-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="20299-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="20299-106">Gateway de aplicativo do Azure pode ser configurado com um VIP da Internet ou com um ponto de extremidade interno não é toohello exposto à Internet, também conhecido como um ponto final (ILB) do balanceador de carga interno.</span><span class="sxs-lookup"><span data-stu-id="20299-106">Azure Application Gateway can be configured with an Internet-facing VIP or with an internal endpoint that is not exposed toohello Internet, also known as an internal load balancer (ILB) endpoint.</span></span> <span data-ttu-id="20299-107">Configurando o gateway Olá com um ILB é útil para aplicativos de linha de negócios internos que não são toohello exposto à Internet.</span><span class="sxs-lookup"><span data-stu-id="20299-107">Configuring hello gateway with an ILB is useful for internal line-of-business applications that are not exposed toohello Internet.</span></span> <span data-ttu-id="20299-108">Também é útil para serviços e níveis dentro de um aplicativo de várias camado que ficam em um limite de segurança que não seja toohello exposto à Internet, mas ainda precisam de round-robin carregam distribuição, persistência de sessão ou encerramento do Secure Sockets Layer (SSL).</span><span class="sxs-lookup"><span data-stu-id="20299-108">It's also useful for services and tiers within a multi-tier application that sit in a security boundary that is not exposed toohello Internet but still require round-robin load distribution, session stickiness, or Secure Sockets Layer (SSL) termination.</span></span>

<span data-ttu-id="20299-109">Este artigo orienta Olá etapas tooconfigure um application gateway com um ILB.</span><span class="sxs-lookup"><span data-stu-id="20299-109">This article walks you through hello steps tooconfigure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="20299-110">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="20299-110">Before you begin</span></span>

1. <span data-ttu-id="20299-111">Instale a versão mais recente Olá Olá Azure de cmdlets do PowerShell usando Olá Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="20299-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="20299-112">Você pode baixar e instalar a versão mais recente de saudação do hello **do Windows PowerShell** seção Olá [página de Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="20299-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="20299-113">Você cria uma rede virtual e uma sub-rede para o Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="20299-113">You create a virtual network and a subnet for Application Gateway.</span></span> <span data-ttu-id="20299-114">Certifique-se de que não há máquinas ou implantações de nuvem usando sub-rede hello.</span><span class="sxs-lookup"><span data-stu-id="20299-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="20299-115">O Gateway de Aplicativo deve estar sozinho em uma sub-rede de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="20299-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="20299-116">servidores de saudação que você configure o gateway de aplicativo hello toouse devem existir ou seus pontos de extremidade criados na rede virtual hello ou com um IP público/VIP atribuídos.</span><span class="sxs-lookup"><span data-stu-id="20299-116">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="20299-117">O que é necessário toocreate um application gateway?</span><span class="sxs-lookup"><span data-stu-id="20299-117">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="20299-118">**Pool de servidores de back-end:** lista de saudação de endereços IP dos servidores de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="20299-118">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="20299-119">Olá endereços IP listados devem ou pertencer rede virtual toohello, mas em uma sub-rede diferente para o gateway de aplicativo hello ou deve ser um IP público/VIP.</span><span class="sxs-lookup"><span data-stu-id="20299-119">hello IP addresses listed should either belong toohello virtual network but in a different subnet for hello application gateway or should be a public IP/VIP.</span></span>
* <span data-ttu-id="20299-120">**Configurações do pool de servidores back-end:** cada pool tem configurações como porta, protocolo e afinidade baseada em cookie.</span><span class="sxs-lookup"><span data-stu-id="20299-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="20299-121">Essas configurações são tooa empatado pool e são aplicados tooall servidores no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="20299-121">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="20299-122">**Porta de front-end:** essa porta é a porta pública de saudação que é aberta no gateway do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="20299-122">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="20299-123">Tráfego atinge essa porta e, em seguida, obtém redirecionado tooone de servidores de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="20299-123">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="20299-124">**Ouvinte:** ouvinte Olá tem uma porta de front-end, um protocolo (Http ou Https, eles diferenciam maiusculas de minúsculas) e o nome do certificado SSL de saudação (se a configuração de SSL de descarregamento).</span><span class="sxs-lookup"><span data-stu-id="20299-124">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="20299-125">**Regra:** regra Olá associa ouvinte hello e pool de saudação do servidor de back-end e define o tráfego de saudação do pool de servidor back-end deve ser direcionado toowhen que ele atinja um ouvinte específico.</span><span class="sxs-lookup"><span data-stu-id="20299-125">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="20299-126">Atualmente, apenas Olá *básica* regra tem suporte.</span><span class="sxs-lookup"><span data-stu-id="20299-126">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="20299-127">Olá *básica* regra é a distribuição de carga de round-robin.</span><span class="sxs-lookup"><span data-stu-id="20299-127">hello *basic* rule is round-robin load distribution.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="20299-128">Criar um Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="20299-128">Create an application gateway</span></span>

<span data-ttu-id="20299-129">diferença de saudação entre usar clássico do Azure e o Azure Resource Manager é a ordem de saudação no qual criar gateway de aplicativo hello e itens de saudação que precisam toobe configurado.</span><span class="sxs-lookup"><span data-stu-id="20299-129">hello difference between using Azure Classic and Azure Resource Manager is hello order in which you create hello application gateway and hello items that need toobe configured.</span></span>
<span data-ttu-id="20299-130">Com o Gerenciador de recursos, todos os itens que compõem um application gateway é configurada individualmente e, em seguida, juntar toocreate recurso de gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="20299-130">With Resource Manager, all items that make an application gateway is configured individually and then put together toocreate hello application gateway resource.</span></span>

<span data-ttu-id="20299-131">Aqui estão as etapas de saudação que são necessária toocreate um application gateway:</span><span class="sxs-lookup"><span data-stu-id="20299-131">Here are hello steps that are needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="20299-132">Criar um grupo de recursos para o Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="20299-132">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="20299-133">Criar uma rede virtual e uma sub-rede para o gateway de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="20299-133">Create a virtual network and a subnet for hello application gateway</span></span>
3. <span data-ttu-id="20299-134">Criar um objeto de configuração do gateway do aplicativo</span><span class="sxs-lookup"><span data-stu-id="20299-134">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="20299-135">Criar um recurso do gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="20299-135">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="20299-136">Criar um grupo de recursos para o Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="20299-136">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="20299-137">Certifique-se de que você alterne os cmdlets do PowerShell modo toouse hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="20299-137">Make sure that you switch PowerShell mode toouse hello Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="20299-138">Há mais informações disponíveis em [Como usar o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="20299-138">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="20299-139">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="20299-139">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="20299-140">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="20299-140">Step 2</span></span>

<span data-ttu-id="20299-141">Verificar as assinaturas de saudação para conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="20299-141">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="20299-142">Você está tooauthenticate solicitado com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="20299-142">You are prompted tooauthenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="20299-143">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="20299-143">Step 3</span></span>

<span data-ttu-id="20299-144">Escolha qual toouse suas assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="20299-144">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="20299-145">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="20299-145">Step 4</span></span>

<span data-ttu-id="20299-146">Crie um novo grupo de recursos (ignore esta etapa se você estiver usando um grupo de recursos existente).</span><span class="sxs-lookup"><span data-stu-id="20299-146">Create a new resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -location "West US"
```

<span data-ttu-id="20299-147">O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local.</span><span class="sxs-lookup"><span data-stu-id="20299-147">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="20299-148">Isso é usado como o local padrão de saudação para recursos desse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="20299-148">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="20299-149">Certifique-se de que todos os toocreate de comandos usa um application gateway Olá mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="20299-149">Make sure that all commands toocreate an application gateway uses hello same resource group.</span></span>

<span data-ttu-id="20299-150">Olá anterior de exemplo, criamos um grupo de recursos chamado "Appgw-rg" e o local "Oeste dos EUA".</span><span class="sxs-lookup"><span data-stu-id="20299-150">In hello preceding example, we created a resource group called "appgw-rg" and location "West US".</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="20299-151">Criar uma rede virtual e uma sub-rede para o gateway de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="20299-151">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="20299-152">Olá mostrado no exemplo a seguir como toocreate uma rede virtual usando o Gerenciador de recursos:</span><span class="sxs-lookup"><span data-stu-id="20299-152">hello following example shows how toocreate a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="20299-153">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="20299-153">Step 1</span></span>

```powershell
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="20299-154">Esta etapa atribui o intervalo de endereço Olá 10.0.0.0/24 tooa sub-rede toobe variável usada toocreate uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="20299-154">This step assigns hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="20299-155">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="20299-155">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnetconfig
```

<span data-ttu-id="20299-156">Esta etapa cria uma rede virtual chamada "appgwvnet" no recurso grupo "appgw-rg" para a região do hello Oeste dos EUA com hello prefixo 10.0.0.0/16 10.0.0.0/24 sub-rede.</span><span class="sxs-lookup"><span data-stu-id="20299-156">This step creates a virtual network named "appgwvnet" in resource group "appgw-rg" for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="20299-157">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="20299-157">Step 3</span></span>

```powershell
$subnet = $vnet.subnets[0]
```

<span data-ttu-id="20299-158">Esta etapa atribui Olá sub-rede objeto toovariable $subnet para as próximas etapas hello.</span><span class="sxs-lookup"><span data-stu-id="20299-158">This step assigns hello subnet object toovariable $subnet for hello next steps.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="20299-159">Criar um objeto de configuração do gateway do aplicativo</span><span class="sxs-lookup"><span data-stu-id="20299-159">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="20299-160">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="20299-160">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="20299-161">Essa etapa cria uma configuração de IP do gateway de aplicativo chamada "gatewayIP01".</span><span class="sxs-lookup"><span data-stu-id="20299-161">This step creates an application gateway IP configuration named "gatewayIP01".</span></span> <span data-ttu-id="20299-162">Quando Application Gateway iniciado, ele seleciona um endereço IP da sub-rede de saudação configurado e rotear os endereços IP de toohello de tráfego de rede no pool IP de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="20299-162">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="20299-163">Tenha em mente que cada instância usa um endereço IP.</span><span class="sxs-lookup"><span data-stu-id="20299-163">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="20299-164">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="20299-164">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.1.1.8,10.1.1.9,10.1.1.10
```

<span data-ttu-id="20299-165">Esta etapa configura as pool de endereços IP back-end Olá denominada "pool01" com o IP endereços "10.1.1.8, 10.1.1.9, 10.1.1.10".</span><span class="sxs-lookup"><span data-stu-id="20299-165">This step configures hello back-end IP address pool named "pool01" with IP addresses "10.1.1.8, 10.1.1.9, 10.1.1.10".</span></span> <span data-ttu-id="20299-166">Esses são endereços IP hello que recebem o tráfego de rede hello proveniente de um ponto de extremidade IP de front-end hello.</span><span class="sxs-lookup"><span data-stu-id="20299-166">Those are hello IP addresses that receive hello network traffic that comes from hello front-end IP endpoint.</span></span> <span data-ttu-id="20299-167">Substituir saudação anterior tooadd de endereços IP seus próprios pontos de extremidade do endereço IP do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="20299-167">You replace hello preceding IP addresses tooadd your own application IP address endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="20299-168">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="20299-168">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="20299-169">Esta etapa configura o tráfego de rede do gateway configuração "poolsetting01" para a carga de saudação com balanceamento de aplicativo no pool de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="20299-169">This step configures application gateway setting "poolsetting01" for hello load balanced network traffic in hello back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="20299-170">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="20299-170">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80
```

<span data-ttu-id="20299-171">Esta etapa configura porta IP front-end Olá denominada "frontendport01" para Olá ILB.</span><span class="sxs-lookup"><span data-stu-id="20299-171">This step configures hello front-end IP port named "frontendport01" for hello ILB.</span></span>

### <a name="step-5"></a><span data-ttu-id="20299-172">Etapa 5</span><span class="sxs-lookup"><span data-stu-id="20299-172">Step 5</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -Subnet $subnet
```

<span data-ttu-id="20299-173">Esta etapa cria a configuração de IP front-end Olá chamada "fipconfig01" e associa um IP privado da sub-rede da rede virtual atual hello.</span><span class="sxs-lookup"><span data-stu-id="20299-173">This step creates hello front-end IP configuration called "fipconfig01" and associates it with a private IP from hello current virtual network subnet.</span></span>

### <a name="step-6"></a><span data-ttu-id="20299-174">Etapa 6</span><span class="sxs-lookup"><span data-stu-id="20299-174">Step 6</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp
```

<span data-ttu-id="20299-175">Esta etapa cria um ouvinte Olá chamado "listener01" e associa a configuração de IP front-end do hello porta de front-end toohello.</span><span class="sxs-lookup"><span data-stu-id="20299-175">This step creates hello listener called "listener01" and associates hello front-end port toohello front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="20299-176">Etapa 7</span><span class="sxs-lookup"><span data-stu-id="20299-176">Step 7</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="20299-177">Esta etapa cria Olá regra balanceador de carga roteamento chamada "rule01" que define o comportamento de Balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="20299-177">This step creates hello load balancer routing rule called "rule01" that configures hello load balancer behavior.</span></span>

### <a name="step-8"></a><span data-ttu-id="20299-178">Etapa 8</span><span class="sxs-lookup"><span data-stu-id="20299-178">Step 8</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="20299-179">Esta etapa configura o tamanho de instância de saudação do gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="20299-179">This step configures hello instance size of hello application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="20299-180">Olá valor padrão para *InstanceCount* é 2, com um valor máximo de 10.</span><span class="sxs-lookup"><span data-stu-id="20299-180">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="20299-181">Olá valor padrão para *GatewaySize* é médio.</span><span class="sxs-lookup"><span data-stu-id="20299-181">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="20299-182">Você pode escolher entre Standard_Small, Standard_Medium e Standard_Large.</span><span class="sxs-lookup"><span data-stu-id="20299-182">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="20299-183">Criar um gateway de aplicativo usando New-AzureApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="20299-183">Create an application gateway by using New-AzureApplicationGateway</span></span>

<span data-ttu-id="20299-184">Cria um application gateway com todos os itens de configuração do hello etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="20299-184">Creates an application gateway with all configuration items from hello preceding steps.</span></span> <span data-ttu-id="20299-185">Neste exemplo, o gateway de aplicativo hello é chamado "appgwtest".</span><span class="sxs-lookup"><span data-stu-id="20299-185">In this example, hello application gateway is called "appgwtest".</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="20299-186">Esta etapa cria um application gateway com todos os itens de configuração do hello etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="20299-186">This step creates an application gateway with all configuration items from hello preceding steps.</span></span> <span data-ttu-id="20299-187">No exemplo hello, o gateway de aplicativo hello é chamado "appgwtest".</span><span class="sxs-lookup"><span data-stu-id="20299-187">In hello example, hello application gateway is called "appgwtest".</span></span>

## <a name="delete-an-application-gateway"></a><span data-ttu-id="20299-188">Excluir um gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="20299-188">Delete an application gateway</span></span>

<span data-ttu-id="20299-189">toodelete um application gateway, você precisa Olá toodo etapas na ordem a seguir:</span><span class="sxs-lookup"><span data-stu-id="20299-189">toodelete an application gateway, you need toodo hello following steps in order:</span></span>

1. <span data-ttu-id="20299-190">Saudação de uso `Stop-AzureRmApplicationGateway` gateway de saudação do cmdlet toostop.</span><span class="sxs-lookup"><span data-stu-id="20299-190">Use hello `Stop-AzureRmApplicationGateway` cmdlet toostop hello gateway.</span></span>
2. <span data-ttu-id="20299-191">Saudação de uso `Remove-AzureRmApplicationGateway` gateway de saudação do cmdlet tooremove.</span><span class="sxs-lookup"><span data-stu-id="20299-191">Use hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello gateway.</span></span>
3. <span data-ttu-id="20299-192">Verificar gateway Olá foi removido usando Olá `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="20299-192">Verify that hello gateway has been removed by using hello `Get-AzureApplicationGateway` cmdlet.</span></span>

### <a name="step-1"></a><span data-ttu-id="20299-193">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="20299-193">Step 1</span></span>

<span data-ttu-id="20299-194">Obter o objeto de gateway do aplicativo hello e associá-lo a variável tooa "$getgw".</span><span class="sxs-lookup"><span data-stu-id="20299-194">Get hello application gateway object and associate it tooa variable "$getgw".</span></span>

```powershell
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

### <a name="step-2"></a><span data-ttu-id="20299-195">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="20299-195">Step 2</span></span>

<span data-ttu-id="20299-196">Use `Stop-AzureRmApplicationGateway` gateway de aplicativo hello toostop.</span><span class="sxs-lookup"><span data-stu-id="20299-196">Use `Stop-AzureRmApplicationGateway` toostop hello application gateway.</span></span> <span data-ttu-id="20299-197">Este exemplo mostra Olá `Stop-AzureRmApplicationGateway` cmdlet na primeira linha de saudação, seguido pela saída de hello.</span><span class="sxs-lookup"><span data-stu-id="20299-197">This sample shows hello `Stop-AzureRmApplicationGateway` cmdlet on hello first line, followed by hello output.</span></span>

```powershell
Stop-AzureRmApplicationGateway -ApplicationGateway $getgw  
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

<span data-ttu-id="20299-198">Depois que o gateway de aplicativo hello está em um estado parado, use Olá `Remove-AzureRmApplicationGateway` serviço de saudação do cmdlet tooremove.</span><span class="sxs-lookup"><span data-stu-id="20299-198">Once hello application gateway is in a stopped state, use hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello service.</span></span>

```powershell
Remove-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Force
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

> [!NOTE]
> <span data-ttu-id="20299-199">Olá **-force** switch pode ser uma mensagem de confirmação de remoção toosuppress usado Olá.</span><span class="sxs-lookup"><span data-stu-id="20299-199">hello **-force** switch can be used toosuppress hello remove confirmation message.</span></span>

<span data-ttu-id="20299-200">tooverify que Olá serviço foi removido, você pode usar o hello `Get-AzureRmApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="20299-200">tooverify that hello service has been removed, you can use hello `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="20299-201">Essa etapa não é necessária.</span><span class="sxs-lookup"><span data-stu-id="20299-201">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
```

## <a name="next-steps"></a><span data-ttu-id="20299-202">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="20299-202">Next steps</span></span>

<span data-ttu-id="20299-203">Se você quiser tooconfigure descarregamento de SSL, consulte [Configure um gateway de aplicativo para descarregamento SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="20299-203">If you want tooconfigure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="20299-204">Se você quiser tooconfigure um toouse de gateway do aplicativo com um ILB, consulte [criar um gateway de aplicativo com um balanceador de carga interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="20299-204">If you want tooconfigure an application gateway toouse with an ILB, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="20299-205">Se deseja obter mais informações sobre as opções de balanceamento de carga no geral, consulte:</span><span class="sxs-lookup"><span data-stu-id="20299-205">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="20299-206">Balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="20299-206">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="20299-207">Gerenciador de Tráfego do Azure</span><span class="sxs-lookup"><span data-stu-id="20299-207">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

