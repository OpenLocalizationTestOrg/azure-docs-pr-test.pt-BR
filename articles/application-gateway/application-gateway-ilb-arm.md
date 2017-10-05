---
title: Usando o Gateway de Aplicativo do Azure com o balanceador de carga interno - PowerShell | Microsoft Docs
description: "Esta página oferece instruções para criar, configurar, iniciar e excluir um gateway de aplicativo do Azure com um ILB (balanceador de carga interno) usando o Gerenciador de Recursos do Azure"
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
ms.openlocfilehash: d218eab7e9f124e4825a8a781b4eeb0dcca58b4a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb-by-using-azure-resource-manager"></a><span data-ttu-id="f40b1-103">Criar um gateway de aplicativo com um ILB (balanceador de carga interno) usando o Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="f40b1-103">Create an application gateway with an internal load balancer (ILB) by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f40b1-104">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="f40b1-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="f40b1-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f40b1-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="f40b1-106">O Gateway de Aplicativo do Azure pode ser configurado com um VIP voltado para a Internet ou com um ponto de extremidade interno não exposto à Internet, também conhecido como um ponto de extremidade ILB (balanceador de carga interno).</span><span class="sxs-lookup"><span data-stu-id="f40b1-106">Azure Application Gateway can be configured with an Internet-facing VIP or with an internal endpoint that is not exposed to the Internet, also known as an internal load balancer (ILB) endpoint.</span></span> <span data-ttu-id="f40b1-107">Configurar o gateway como um ILB é útil para aplicativos de linha de negócios internos não expostos à Internet.</span><span class="sxs-lookup"><span data-stu-id="f40b1-107">Configuring the gateway with an ILB is useful for internal line-of-business applications that are not exposed to the Internet.</span></span> <span data-ttu-id="f40b1-108">Isso também é útil para serviços e camadas em um aplicativo multicamada que reside em um limite de segurança não exposto à Internet, mas que ainda exige distribuição de carga round robin, adesão da sessão ou terminação SSL.</span><span class="sxs-lookup"><span data-stu-id="f40b1-108">It's also useful for services and tiers within a multi-tier application that sit in a security boundary that is not exposed to the Internet but still require round-robin load distribution, session stickiness, or Secure Sockets Layer (SSL) termination.</span></span>

<span data-ttu-id="f40b1-109">Este artigo o orienta ao longo das etapas para configurar um gateway de aplicativo com um ILB.</span><span class="sxs-lookup"><span data-stu-id="f40b1-109">This article walks you through the steps to configure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f40b1-110">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="f40b1-110">Before you begin</span></span>

1. <span data-ttu-id="f40b1-111">Instale a versão mais recente dos cmdlets do Azure PowerShell usando o Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="f40b1-111">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="f40b1-112">Você pode baixar e instalar a versão mais recente da seção **Windows PowerShell** da [página Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="f40b1-112">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="f40b1-113">Você cria uma rede virtual e uma sub-rede para o Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f40b1-113">You create a virtual network and a subnet for Application Gateway.</span></span> <span data-ttu-id="f40b1-114">Verifique se não há máquinas virtuais ou implantações em nuvem usando a sub-rede.</span><span class="sxs-lookup"><span data-stu-id="f40b1-114">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="f40b1-115">O Gateway de Aplicativo deve estar sozinho em uma sub-rede de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="f40b1-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="f40b1-116">Os servidores que você configura para usar o gateway de aplicativo devem existir ou ter seus pontos de extremidade criados na rede virtual ou com um IP/VIP público atribuído.</span><span class="sxs-lookup"><span data-stu-id="f40b1-116">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="f40b1-117">O que é necessário para criar um gateway de aplicativo?</span><span class="sxs-lookup"><span data-stu-id="f40b1-117">What is required to create an application gateway?</span></span>

* <span data-ttu-id="f40b1-118">**Pool de servidores back-end:** a lista de endereços IP dos servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="f40b1-118">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="f40b1-119">Os endereços IP listados devem pertencer à rede virtual, mas em uma sub-rede diferente para o gateway de aplicativo, ou devem ser um IP/VIP público.</span><span class="sxs-lookup"><span data-stu-id="f40b1-119">The IP addresses listed should either belong to the virtual network but in a different subnet for the application gateway or should be a public IP/VIP.</span></span>
* <span data-ttu-id="f40b1-120">**Configurações do pool de servidores back-end:** cada pool tem configurações como porta, protocolo e afinidade baseada em cookie.</span><span class="sxs-lookup"><span data-stu-id="f40b1-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="f40b1-121">Essas configurações são vinculadas a um pool e aplicadas a todos os servidores no pool.</span><span class="sxs-lookup"><span data-stu-id="f40b1-121">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="f40b1-122">**Porta front-end:** essa porta é a porta pública aberta no gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f40b1-122">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="f40b1-123">O tráfego atinge essa porta e é redirecionado para um dos servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="f40b1-123">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="f40b1-124">**Ouvinte:** o ouvinte tem uma porta front-end, um protocolo (HTTP ou HTTPS, que diferencia maiúsculas de minúsculas) e o nome do certificado SSL (caso esteja configurando o descarregamento SSL).</span><span class="sxs-lookup"><span data-stu-id="f40b1-124">**Listener:** The listener has a front-end port, a protocol (Http or Https, these are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="f40b1-125">**Regra:** a regra vincula o ouvinte e o pool de servidores back-end e define à qual pool de servidores back-end o tráfego deve ser direcionado quando atinge um ouvinte específico.</span><span class="sxs-lookup"><span data-stu-id="f40b1-125">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="f40b1-126">Atualmente, há suporte apenas para a regra *basic* .</span><span class="sxs-lookup"><span data-stu-id="f40b1-126">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="f40b1-127">A regra *básica* é a distribuição de carga round robin.</span><span class="sxs-lookup"><span data-stu-id="f40b1-127">The *basic* rule is round-robin load distribution.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="f40b1-128">Criar um Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="f40b1-128">Create an application gateway</span></span>

<span data-ttu-id="f40b1-129">A diferença entre usar o Azure Classic e o Azure Resource Manager é a ordem em que você cria o gateway de aplicativo e os itens que precisam ser configurados.</span><span class="sxs-lookup"><span data-stu-id="f40b1-129">The difference between using Azure Classic and Azure Resource Manager is the order in which you create the application gateway and the items that need to be configured.</span></span>
<span data-ttu-id="f40b1-130">Com o Gerenciador de Recursos, todos os itens que compõem um gateway de aplicativo são configurados individualmente e, em seguida, reunidos para criar o recurso do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f40b1-130">With Resource Manager, all items that make an application gateway is configured individually and then put together to create the application gateway resource.</span></span>

<span data-ttu-id="f40b1-131">A seguir, as etapas necessárias para criar um gateway de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="f40b1-131">Here are the steps that are needed to create an application gateway:</span></span>

1. <span data-ttu-id="f40b1-132">Criar um grupo de recursos para o Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="f40b1-132">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="f40b1-133">Criar uma rede virtual e uma sub-rede para o gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="f40b1-133">Create a virtual network and a subnet for the application gateway</span></span>
3. <span data-ttu-id="f40b1-134">Criar um objeto de configuração do gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="f40b1-134">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="f40b1-135">Criar um recurso do gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="f40b1-135">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="f40b1-136">Criar um grupo de recursos para o Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="f40b1-136">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="f40b1-137">Alterne para o modo PowerShell para usar os cmdlets do Gerenciador de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="f40b1-137">Make sure that you switch PowerShell mode to use the Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="f40b1-138">Mais informações estão disponíveis em [Usando o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f40b1-138">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="f40b1-139">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="f40b1-139">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="f40b1-140">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="f40b1-140">Step 2</span></span>

<span data-ttu-id="f40b1-141">Verificar as assinaturas da conta.</span><span class="sxs-lookup"><span data-stu-id="f40b1-141">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="f40b1-142">Você deve se autenticar com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="f40b1-142">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="f40b1-143">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="f40b1-143">Step 3</span></span>

<span data-ttu-id="f40b1-144">Escolha quais das suas assinaturas do Azure deseja usar.</span><span class="sxs-lookup"><span data-stu-id="f40b1-144">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="f40b1-145">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="f40b1-145">Step 4</span></span>

<span data-ttu-id="f40b1-146">Crie um novo grupo de recursos (ignore esta etapa se você estiver usando um grupo de recursos existente).</span><span class="sxs-lookup"><span data-stu-id="f40b1-146">Create a new resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -location "West US"
```

<span data-ttu-id="f40b1-147">O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local.</span><span class="sxs-lookup"><span data-stu-id="f40b1-147">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="f40b1-148">Ele é usado como o local padrão para os recursos do grupo de recursos em questão.</span><span class="sxs-lookup"><span data-stu-id="f40b1-148">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="f40b1-149">Verifique se todos os comandos para criar um gateway de aplicativo usam o mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f40b1-149">Make sure that all commands to create an application gateway uses the same resource group.</span></span>

<span data-ttu-id="f40b1-150">No exemplo anterior, criamos um grupo de recursos denominado "appgw-rg" e o local "Oeste dos EUA".</span><span class="sxs-lookup"><span data-stu-id="f40b1-150">In the preceding example, we created a resource group called "appgw-rg" and location "West US".</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="f40b1-151">Criar uma rede virtual e uma sub-rede para o gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="f40b1-151">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="f40b1-152">O exemplo a seguir mostra como criar uma rede virtual usando o Gerenciador de Recursos:</span><span class="sxs-lookup"><span data-stu-id="f40b1-152">The following example shows how to create a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="f40b1-153">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="f40b1-153">Step 1</span></span>

```powershell
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="f40b1-154">Essa etapa atribui o intervalo de endereços 10.0.0.0/24 a uma variável de sub-rede a ser usada para criar uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="f40b1-154">This step assigns the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="f40b1-155">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="f40b1-155">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnetconfig
```

<span data-ttu-id="f40b1-156">Essa etapa cria uma rede virtual chamada "appgwvnet" no grupo de recursos "appgw-rg" para a região Oeste dos EUA usando o prefixo 10.0.0.0/16 com a sub-rede 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="f40b1-156">This step creates a virtual network named "appgwvnet" in resource group "appgw-rg" for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="f40b1-157">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="f40b1-157">Step 3</span></span>

```powershell
$subnet = $vnet.subnets[0]
```

<span data-ttu-id="f40b1-158">Essa etapa atribui o objeto de sub-rede à variável $subnet para as próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="f40b1-158">This step assigns the subnet object to variable $subnet for the next steps.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="f40b1-159">Criar um objeto de configuração do gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="f40b1-159">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="f40b1-160">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="f40b1-160">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="f40b1-161">Essa etapa cria uma configuração de IP do gateway de aplicativo chamada "gatewayIP01".</span><span class="sxs-lookup"><span data-stu-id="f40b1-161">This step creates an application gateway IP configuration named "gatewayIP01".</span></span> <span data-ttu-id="f40b1-162">Quando o Gateway de Aplicativo é iniciado, ele escolhe um endereço IP na sub-rede configurada e no tráfego de rede da rota para os endereços IP no pool de IPs de back-end.</span><span class="sxs-lookup"><span data-stu-id="f40b1-162">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="f40b1-163">Tenha em mente que cada instância usa um endereço IP.</span><span class="sxs-lookup"><span data-stu-id="f40b1-163">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="f40b1-164">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="f40b1-164">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.1.1.8,10.1.1.9,10.1.1.10
```

<span data-ttu-id="f40b1-165">Essa etapa configura o pool de endereços IP de back-end denominado "pool01" com os endereços IP "10.1.1.8, 10.1.1.9, 10.1.1.10".</span><span class="sxs-lookup"><span data-stu-id="f40b1-165">This step configures the back-end IP address pool named "pool01" with IP addresses "10.1.1.8, 10.1.1.9, 10.1.1.10".</span></span> <span data-ttu-id="f40b1-166">Esses são os endereços IP que receberão o tráfego de rede proveniente do ponto de extremidade do IP de front-end.</span><span class="sxs-lookup"><span data-stu-id="f40b1-166">Those are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span></span> <span data-ttu-id="f40b1-167">Você substitui os endereços IP anteriores para adicionar seus próprios pontos de extremidade de endereço IP do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f40b1-167">You replace the preceding IP addresses to add your own application IP address endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="f40b1-168">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="f40b1-168">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="f40b1-169">Essa etapa define a configuração "poolsetting01" do gateway de aplicativo para o tráfego de rede com carga balanceada no pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="f40b1-169">This step configures application gateway setting "poolsetting01" for the load balanced network traffic in the back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="f40b1-170">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="f40b1-170">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80
```

<span data-ttu-id="f40b1-171">Essa etapa configura a porta do IP de front-end denominada "frontendport01" para o ILB.</span><span class="sxs-lookup"><span data-stu-id="f40b1-171">This step configures the front-end IP port named "frontendport01" for the ILB.</span></span>

### <a name="step-5"></a><span data-ttu-id="f40b1-172">Etapa 5</span><span class="sxs-lookup"><span data-stu-id="f40b1-172">Step 5</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -Subnet $subnet
```

<span data-ttu-id="f40b1-173">Essa etapa cria a configuração de IP de front-end chamada "fipconfig01" e a associa a um IP privado da sub-rede da rede virtual atual.</span><span class="sxs-lookup"><span data-stu-id="f40b1-173">This step creates the front-end IP configuration called "fipconfig01" and associates it with a private IP from the current virtual network subnet.</span></span>

### <a name="step-6"></a><span data-ttu-id="f40b1-174">Etapa 6</span><span class="sxs-lookup"><span data-stu-id="f40b1-174">Step 6</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp
```

<span data-ttu-id="f40b1-175">Essa etapa cria o ouvinte chamado "listener01" e associa a porta de front-end à configuração de IP de front-end.</span><span class="sxs-lookup"><span data-stu-id="f40b1-175">This step creates the listener called "listener01" and associates the front-end port to the front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="f40b1-176">Etapa 7</span><span class="sxs-lookup"><span data-stu-id="f40b1-176">Step 7</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="f40b1-177">Essa etapa cria a regra de roteamento do balanceador de carga chamada "rule01", configurando o comportamento do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="f40b1-177">This step creates the load balancer routing rule called "rule01" that configures the load balancer behavior.</span></span>

### <a name="step-8"></a><span data-ttu-id="f40b1-178">Etapa 8</span><span class="sxs-lookup"><span data-stu-id="f40b1-178">Step 8</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="f40b1-179">Essa etapa configura o tamanho da instância do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f40b1-179">This step configures the instance size of the application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="f40b1-180">O valor padrão para *InstanceCount* é 2, com um valor máximo de 10.</span><span class="sxs-lookup"><span data-stu-id="f40b1-180">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="f40b1-181">O valor padrão para *GatewaySize* é Medium.</span><span class="sxs-lookup"><span data-stu-id="f40b1-181">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="f40b1-182">Você pode escolher entre Standard_Small, Standard_Medium e Standard_Large.</span><span class="sxs-lookup"><span data-stu-id="f40b1-182">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="f40b1-183">Criar um gateway de aplicativo usando New-AzureApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="f40b1-183">Create an application gateway by using New-AzureApplicationGateway</span></span>

<span data-ttu-id="f40b1-184">Cria um gateway de aplicativo com todos os itens de configuração das etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="f40b1-184">Creates an application gateway with all configuration items from the preceding steps.</span></span> <span data-ttu-id="f40b1-185">Neste exemplo, o gateway de aplicativo é chamado de "appgwtest".</span><span class="sxs-lookup"><span data-stu-id="f40b1-185">In this example, the application gateway is called "appgwtest".</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="f40b1-186">Essa etapa cria um gateway de aplicativo com todos os itens de configuração das etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="f40b1-186">This step creates an application gateway with all configuration items from the preceding steps.</span></span> <span data-ttu-id="f40b1-187">No exemplo, o gateway de aplicativo se chama "appgwtest".</span><span class="sxs-lookup"><span data-stu-id="f40b1-187">In the example, the application gateway is called "appgwtest".</span></span>

## <a name="delete-an-application-gateway"></a><span data-ttu-id="f40b1-188">Excluir um gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="f40b1-188">Delete an application gateway</span></span>

<span data-ttu-id="f40b1-189">Para excluir um gateway de aplicativo, você precisa seguir estas etapas em ordem:</span><span class="sxs-lookup"><span data-stu-id="f40b1-189">To delete an application gateway, you need to do the following steps in order:</span></span>

1. <span data-ttu-id="f40b1-190">Use o cmdlet `Stop-AzureRmApplicationGateway` para parar o gateway.</span><span class="sxs-lookup"><span data-stu-id="f40b1-190">Use the `Stop-AzureRmApplicationGateway` cmdlet to stop the gateway.</span></span>
2. <span data-ttu-id="f40b1-191">Use o cmdlet `Remove-AzureRmApplicationGateway` para remover o gateway.</span><span class="sxs-lookup"><span data-stu-id="f40b1-191">Use the `Remove-AzureRmApplicationGateway` cmdlet to remove the gateway.</span></span>
3. <span data-ttu-id="f40b1-192">Verifique se o gateway foi removido usando o cmdlet `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="f40b1-192">Verify that the gateway has been removed by using the `Get-AzureApplicationGateway` cmdlet.</span></span>

### <a name="step-1"></a><span data-ttu-id="f40b1-193">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="f40b1-193">Step 1</span></span>

<span data-ttu-id="f40b1-194">Obtenha o objeto do gateway de aplicativo e associe-o a uma variável "$getgw".</span><span class="sxs-lookup"><span data-stu-id="f40b1-194">Get the application gateway object and associate it to a variable "$getgw".</span></span>

```powershell
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

### <a name="step-2"></a><span data-ttu-id="f40b1-195">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="f40b1-195">Step 2</span></span>

<span data-ttu-id="f40b1-196">Use o `Stop-AzureRmApplicationGateway` para parar o gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f40b1-196">Use `Stop-AzureRmApplicationGateway` to stop the application gateway.</span></span> <span data-ttu-id="f40b1-197">Este exemplo mostra o cmdlet `Stop-AzureRmApplicationGateway` na primeira linha, seguido pela saída.</span><span class="sxs-lookup"><span data-stu-id="f40b1-197">This sample shows the `Stop-AzureRmApplicationGateway` cmdlet on the first line, followed by the output.</span></span>

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

<span data-ttu-id="f40b1-198">Depois que o gateway de aplicativo estiver em um estado parado, use o cmdlet `Remove-AzureRmApplicationGateway` para remover o serviço.</span><span class="sxs-lookup"><span data-stu-id="f40b1-198">Once the application gateway is in a stopped state, use the `Remove-AzureRmApplicationGateway` cmdlet to remove the service.</span></span>

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
> <span data-ttu-id="f40b1-199">A opção **-force** pode ser usada para suprimir a mensagem de confirmação da remoção.</span><span class="sxs-lookup"><span data-stu-id="f40b1-199">The **-force** switch can be used to suppress the remove confirmation message.</span></span>

<span data-ttu-id="f40b1-200">Para verificar se o serviço foi removido, você pode usar o cmdlet `Get-AzureRmApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="f40b1-200">To verify that the service has been removed, you can use the `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="f40b1-201">Essa etapa não é necessária.</span><span class="sxs-lookup"><span data-stu-id="f40b1-201">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: The gateway does not exist.
```

## <a name="next-steps"></a><span data-ttu-id="f40b1-202">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f40b1-202">Next steps</span></span>

<span data-ttu-id="f40b1-203">Se desejar configurar o descarregamento SSL, confira [Configurar um gateway de aplicativo para descarregamento SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="f40b1-203">If you want to configure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="f40b1-204">Se desejar configurar um Gateway de Aplicativo para usar com um ILB, veja [Criar um gateway de aplicativo com um ILB (balanceador de carga interno)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="f40b1-204">If you want to configure an application gateway to use with an ILB, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="f40b1-205">Se deseja obter mais informações sobre as opções de balanceamento de carga no geral, consulte:</span><span class="sxs-lookup"><span data-stu-id="f40b1-205">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="f40b1-206">Balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="f40b1-206">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="f40b1-207">Gerenciador de Tráfego do Azure</span><span class="sxs-lookup"><span data-stu-id="f40b1-207">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

