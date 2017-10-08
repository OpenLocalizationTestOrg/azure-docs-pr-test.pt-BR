---
title: aaaConfigure SSL descarregar - Gateway de aplicativo do Azure - PowerShell | Microsoft Docs
description: "Esta página fornece instruções toocreate descarregar um application gateway com SSL usando o Gerenciador de recursos do Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 3c3681e0-f928-4682-9d97-567f8e278e13
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: c2855d8d3caaa97ec05475c67ff0f8dce72ef2a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a><span data-ttu-id="74a24-103">Configurar um gateway de aplicativo para descarregamento SSL usando o Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="74a24-103">Configure an application gateway for SSL offload by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="74a24-104">portal do Azure</span><span class="sxs-lookup"><span data-stu-id="74a24-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="74a24-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="74a24-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="74a24-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="74a24-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="74a24-107">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="74a24-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="74a24-108">Gateway de aplicativo do Azure pode ser configurado tooterminate Olá Secure Sockets Layer (SSL) sessão Olá gateway tooavoid cara SSL descriptografia tarefas toohappen no farm de web hello.</span><span class="sxs-lookup"><span data-stu-id="74a24-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="74a24-109">Descarregamento SSL também simplifica a configuração de servidor front-end do hello e gerenciamento de aplicativo da web hello.</span><span class="sxs-lookup"><span data-stu-id="74a24-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="74a24-110">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="74a24-110">Before you begin</span></span>

1. <span data-ttu-id="74a24-111">Instale a versão mais recente Olá Olá Azure de cmdlets do PowerShell usando Olá Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="74a24-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="74a24-112">Você pode baixar e instalar a versão mais recente de saudação do hello **do Windows PowerShell** seção Olá [página de Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="74a24-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="74a24-113">Crie uma rede virtual e uma sub-rede para o gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="74a24-113">You create a virtual network and a subnet for hello application gateway.</span></span> <span data-ttu-id="74a24-114">Certifique-se de que não há máquinas ou implantações de nuvem usando sub-rede hello.</span><span class="sxs-lookup"><span data-stu-id="74a24-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="74a24-115">O Gateway de Aplicativo deve estar sozinho em uma sub-rede de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="74a24-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="74a24-116">servidores Olá configurar o gateway de aplicativo hello toouse devem existir ou tem seus pontos de extremidade criado na rede virtual hello ou com um IP público/VIP atribuído.</span><span class="sxs-lookup"><span data-stu-id="74a24-116">hello servers you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="74a24-117">O que é necessário toocreate um application gateway?</span><span class="sxs-lookup"><span data-stu-id="74a24-117">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="74a24-118">**Pool de servidores de back-end:** lista de saudação de endereços IP dos servidores de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="74a24-118">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="74a24-119">endereços IP Hello listado ou devem pertencer a sub-rede da rede virtual toohello ou devem ser um IP público/VIP.</span><span class="sxs-lookup"><span data-stu-id="74a24-119">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="74a24-120">**Configurações do pool de servidores back-end:** cada pool tem configurações como porta, protocolo e afinidade baseada em cookie.</span><span class="sxs-lookup"><span data-stu-id="74a24-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="74a24-121">Essas configurações são tooa empatado pool e são aplicados tooall servidores no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="74a24-121">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="74a24-122">**Porta de front-end:** essa porta é a porta pública de saudação que é aberta no gateway do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="74a24-122">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="74a24-123">Tráfego atinge essa porta e, em seguida, obtém redirecionado tooone de servidores de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="74a24-123">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="74a24-124">**Ouvinte:** ouvinte Olá tem uma porta de front-end, um protocolo (Http ou Https, essas configurações diferenciam maiusculas de minúsculas) e o nome do certificado SSL de saudação (se a configuração de SSL de descarregamento).</span><span class="sxs-lookup"><span data-stu-id="74a24-124">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="74a24-125">**Regra:** regra Olá associa ouvinte hello e pool de saudação do servidor de back-end e define o tráfego de saudação do pool de servidor back-end deve ser direcionado toowhen que ele atinja um ouvinte específico.</span><span class="sxs-lookup"><span data-stu-id="74a24-125">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="74a24-126">Atualmente, apenas Olá *básica* regra tem suporte.</span><span class="sxs-lookup"><span data-stu-id="74a24-126">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="74a24-127">Olá *básica* regra é a distribuição de carga de round-robin.</span><span class="sxs-lookup"><span data-stu-id="74a24-127">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="74a24-128">**Observações adicionais sobre a configuração**</span><span class="sxs-lookup"><span data-stu-id="74a24-128">**Additional configuration notes**</span></span>

<span data-ttu-id="74a24-129">Para a configuração de certificados SSL, Olá protocolo em **HttpListener** devem alterar muito*Https* (com distinção entre maiusculas e minúsculas).</span><span class="sxs-lookup"><span data-stu-id="74a24-129">For SSL certificates configuration, hello protocol in **HttpListener** should change too*Https* (case sensitive).</span></span> <span data-ttu-id="74a24-130">Olá **SslCertificate** elemento é adicionado muito**HttpListener** com valor de variável Olá configurado para o certificado SSL da saudação.</span><span class="sxs-lookup"><span data-stu-id="74a24-130">hello **SslCertificate** element is added too**HttpListener** with hello variable value configured for hello SSL certificate.</span></span> <span data-ttu-id="74a24-131">porta de front-end Olá deve ser atualizado too443.</span><span class="sxs-lookup"><span data-stu-id="74a24-131">hello front-end port should be updated too443.</span></span>

<span data-ttu-id="74a24-132">**afinidade de baseada em cookie tooenable**: um application gateway pode ser configurado tooensure que uma solicitação de uma sessão de cliente é sempre toohello direcionado mesma VM no farm de web hello.</span><span class="sxs-lookup"><span data-stu-id="74a24-132">**tooenable cookie-based affinity**: An application gateway can be configured tooensure that a request from a client session is always directed toohello same VM in hello web farm.</span></span> <span data-ttu-id="74a24-133">Este cenário é feito pela inclusão de um cookie de sessão que permite que o tráfego de toodirect gateway Olá adequadamente.</span><span class="sxs-lookup"><span data-stu-id="74a24-133">This scenario is done by injection of a session cookie that allows hello gateway toodirect traffic appropriately.</span></span> <span data-ttu-id="74a24-134">Definir afinidade baseada em cookie tooenable, **CookieBasedAffinity** muito*habilitado* em Olá **BackendHttpSettings** elemento.</span><span class="sxs-lookup"><span data-stu-id="74a24-134">tooenable cookie-based affinity, set **CookieBasedAffinity** too*Enabled* in hello **BackendHttpSettings** element.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="74a24-135">Criar um Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="74a24-135">Create an application gateway</span></span>

<span data-ttu-id="74a24-136">diferença de saudação entre usar o modelo de implantação clássico do Azure hello e Gerenciador de recursos do Azure é a ordem de saudação que você criar um aplicativo gateway e Olá itens que precisam toobe configurado.</span><span class="sxs-lookup"><span data-stu-id="74a24-136">hello difference between using hello Azure Classic deployment model and Azure Resource Manager is hello order that you create an application gateway and hello items that need toobe configured.</span></span>

<span data-ttu-id="74a24-137">Com o Gerenciador de recursos, todos os componentes de um application gateway são configurados individualmente e, em seguida, coloque junto toocreate um recurso do application gateway.</span><span class="sxs-lookup"><span data-stu-id="74a24-137">With Resource Manager, all components of an application gateway are configured individually and then put together toocreate an application gateway resource.</span></span>

<span data-ttu-id="74a24-138">Aqui está Olá etapas necessárias toocreate um application gateway:</span><span class="sxs-lookup"><span data-stu-id="74a24-138">Here are hello steps needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="74a24-139">Criar um grupo de recursos para o Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="74a24-139">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="74a24-140">Criar rede virtual, sub-rede e IP público para o gateway de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="74a24-140">Create virtual network, subnet, and public IP for hello application gateway</span></span>
3. <span data-ttu-id="74a24-141">Criar um objeto de configuração do gateway do aplicativo</span><span class="sxs-lookup"><span data-stu-id="74a24-141">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="74a24-142">Criar um recurso do gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="74a24-142">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="74a24-143">Criar um grupo de recursos para o Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="74a24-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="74a24-144">Certifique-se de que você alterne os cmdlets do PowerShell modo toouse hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="74a24-144">Make sure that you switch PowerShell mode toouse hello Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="74a24-145">Há mais informações disponíveis em [Como usar o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="74a24-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="74a24-146">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="74a24-146">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="74a24-147">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="74a24-147">Step 2</span></span>

<span data-ttu-id="74a24-148">Verificar as assinaturas de saudação para conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="74a24-148">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="74a24-149">Você está tooauthenticate solicitado com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="74a24-149">You are prompted tooauthenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="74a24-150">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="74a24-150">Step 3</span></span>

<span data-ttu-id="74a24-151">Escolha qual toouse suas assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="74a24-151">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="74a24-152">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="74a24-152">Step 4</span></span>

<span data-ttu-id="74a24-153">Crie um grupo de recursos (ignore esta etapa se você estiver usando um grupo de recursos existente).</span><span class="sxs-lookup"><span data-stu-id="74a24-153">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="74a24-154">O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local.</span><span class="sxs-lookup"><span data-stu-id="74a24-154">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="74a24-155">Essa configuração é usada como o local padrão de saudação para recursos desse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="74a24-155">This setting is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="74a24-156">Certifique-se de que todos os toocreate de comandos usa um application gateway Olá mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="74a24-156">Make sure that all commands toocreate an application gateway uses hello same resource group.</span></span>

<span data-ttu-id="74a24-157">O exemplo hello acima, criamos um grupo de recursos chamado **appgw RG** e local **Oeste dos EUA**.</span><span class="sxs-lookup"><span data-stu-id="74a24-157">In hello example above, we created a resource group called **appgw-RG** and location **West US**.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="74a24-158">Criar uma rede virtual e uma sub-rede para o gateway de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="74a24-158">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="74a24-159">Olá mostrado no exemplo a seguir como toocreate uma rede virtual usando o Gerenciador de recursos:</span><span class="sxs-lookup"><span data-stu-id="74a24-159">hello following example shows how toocreate a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="74a24-160">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="74a24-160">Step 1</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="74a24-161">Este exemplo atribui o intervalo de endereço Olá 10.0.0.0/24 tooa sub-rede toobe variável usada toocreate uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="74a24-161">This sample assigns hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="74a24-162">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="74a24-162">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

<span data-ttu-id="74a24-163">Este exemplo cria uma rede virtual denominada **appgwvnet** no grupo de recursos **appgw rg** para a região do hello Oeste dos EUA com hello prefixo 10.0.0.0/16 10.0.0.0/24 sub-rede.</span><span class="sxs-lookup"><span data-stu-id="74a24-163">This sample creates a virtual network named **appgwvnet** in resource group **appgw-rg** for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="74a24-164">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="74a24-164">Step 3</span></span>

```powershell
$subnet = $vnet.Subnets[0]
```

<span data-ttu-id="74a24-165">Este exemplo atribui Olá sub-rede objeto toovariable $subnet para as próximas etapas hello.</span><span class="sxs-lookup"><span data-stu-id="74a24-165">This sample assigns hello subnet object toovariable $subnet for hello next steps.</span></span>

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="74a24-166">Criar um endereço IP público para a configuração de front-end Olá</span><span class="sxs-lookup"><span data-stu-id="74a24-166">Create a public IP address for hello front-end configuration</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="74a24-167">Este exemplo cria um recurso IP público **publicIP01** no grupo de recursos **appgw rg** para região Oeste dos EUA de saudação.</span><span class="sxs-lookup"><span data-stu-id="74a24-167">This sample creates a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="74a24-168">Criar um objeto de configuração do gateway do aplicativo</span><span class="sxs-lookup"><span data-stu-id="74a24-168">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="74a24-169">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="74a24-169">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="74a24-170">Esta amostra cria uma configuração de IP do gateway de aplicativo chamada **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="74a24-170">This sample creates an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="74a24-171">Quando Application Gateway iniciado, ele seleciona um endereço IP da sub-rede de saudação configurado e rotear os endereços IP de toohello de tráfego de rede no pool IP de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="74a24-171">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="74a24-172">Tenha em mente que cada instância usa um endereço IP.</span><span class="sxs-lookup"><span data-stu-id="74a24-172">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="74a24-173">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="74a24-173">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

<span data-ttu-id="74a24-174">Este exemplo configura o pool de endereços do hello back-end IP denominado **pool01** com endereços IP **134.170.185.46**, **134.170.188.221**, **134.170.185.50** .</span><span class="sxs-lookup"><span data-stu-id="74a24-174">This sample configures hello back-end IP address pool named **pool01** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50**.</span></span> <span data-ttu-id="74a24-175">Esses valores são endereços IP hello que recebem o tráfego de rede hello proveniente de um ponto de extremidade IP de front-end hello.</span><span class="sxs-lookup"><span data-stu-id="74a24-175">Those values are hello IP addresses that receive hello network traffic that comes from hello front-end IP endpoint.</span></span> <span data-ttu-id="74a24-176">Substitua os endereços IP de saudação da saudação anterior exemplo com endereços IP de saudação de seus pontos de extremidade do aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="74a24-176">Replace hello IP addresses from hello preceding example with hello IP addresses of your web application endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="74a24-177">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="74a24-177">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

<span data-ttu-id="74a24-178">Este exemplo configura a configuração de gateway do aplicativo **poolsetting01** tooload balanceada de tráfego de rede no pool de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="74a24-178">This sample configures application gateway setting **poolsetting01** tooload-balanced network traffic in hello back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="74a24-179">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="74a24-179">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

<span data-ttu-id="74a24-180">Este exemplo configura a porta IP front-end Olá chamada **frontendport01** ponto de extremidade IP pública hello.</span><span class="sxs-lookup"><span data-stu-id="74a24-180">This sample configures hello front-end IP port named **frontendport01** for hello public IP endpoint.</span></span>

### <a name="step-5"></a><span data-ttu-id="74a24-181">Etapa 5</span><span class="sxs-lookup"><span data-stu-id="74a24-181">Step 5</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

<span data-ttu-id="74a24-182">Este exemplo configura o certificado de saudação usado para a conexão SSL.</span><span class="sxs-lookup"><span data-stu-id="74a24-182">This sample configures hello certificate used for SSL connection.</span></span> <span data-ttu-id="74a24-183">certificado Olá precisa toobe no formato. pfx e senha Olá deve estar entre 4 too12 caracteres.</span><span class="sxs-lookup"><span data-stu-id="74a24-183">hello certificate needs toobe in .pfx format, and hello password must be between 4 too12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="74a24-184">Etapa 6</span><span class="sxs-lookup"><span data-stu-id="74a24-184">Step 6</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

<span data-ttu-id="74a24-185">Este exemplo cria a configuração de IP front-end Olá nomeada **fipconfig01** e associa Olá endereço IP público com configuração de IP de front-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="74a24-185">This sample creates hello front-end IP configuration named **fipconfig01** and associates hello public IP address with hello front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="74a24-186">Etapa 7</span><span class="sxs-lookup"><span data-stu-id="74a24-186">Step 7</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

<span data-ttu-id="74a24-187">Este exemplo cria o nome do ouvinte Olá **listener01** e associa Olá certificado e configuração de IP de front-end da toohello de porta de front-end.</span><span class="sxs-lookup"><span data-stu-id="74a24-187">This sample creates hello listener name **listener01** and associates hello front-end port toohello front-end IP configuration and certificate.</span></span>

### <a name="step-8"></a><span data-ttu-id="74a24-188">Etapa 8</span><span class="sxs-lookup"><span data-stu-id="74a24-188">Step 8</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="74a24-189">Este exemplo cria Olá regra balanceador de carga roteamento denominada **rule01** que define o comportamento de Balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="74a24-189">This sample creates hello load balancer routing rule named **rule01** that configures hello load balancer behavior.</span></span>

### <a name="step-9"></a><span data-ttu-id="74a24-190">Etapa 9</span><span class="sxs-lookup"><span data-stu-id="74a24-190">Step 9</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="74a24-191">Este exemplo configura o tamanho de instância de saudação do gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="74a24-191">This sample configures hello instance size of hello application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="74a24-192">Olá valor padrão para *InstanceCount* é 2, com um valor máximo de 10.</span><span class="sxs-lookup"><span data-stu-id="74a24-192">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="74a24-193">Olá valor padrão para *GatewaySize* é médio.</span><span class="sxs-lookup"><span data-stu-id="74a24-193">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="74a24-194">Você pode escolher entre Standard_Small, Standard_Medium e Standard_Large.</span><span class="sxs-lookup"><span data-stu-id="74a24-194">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

### <a name="step-10"></a><span data-ttu-id="74a24-195">Etapa 10</span><span class="sxs-lookup"><span data-stu-id="74a24-195">Step 10</span></span>

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

<span data-ttu-id="74a24-196">Esta etapa define Olá toouse de política SSL no gateway do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="74a24-196">This step defines hello SSL policy toouse on hello application gateway.</span></span> <span data-ttu-id="74a24-197">Visite [versões de política de configurar SSL e conjuntos de codificação no Application Gateway](application-gateway-configure-ssl-policy-powershell.md) toolearn mais.</span><span class="sxs-lookup"><span data-stu-id="74a24-197">Visit [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) toolearn more.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="74a24-198">Criar um gateway de aplicativo usando New-AzureApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="74a24-198">Create an application gateway by using New-AzureApplicationGateway</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

<span data-ttu-id="74a24-199">Este exemplo cria um application gateway com todos os itens de configuração do hello etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="74a24-199">This sample creates an application gateway with all configuration items from hello preceding steps.</span></span> <span data-ttu-id="74a24-200">No exemplo hello, o gateway de aplicativo hello é chamado **appgwtest**.</span><span class="sxs-lookup"><span data-stu-id="74a24-200">In hello example, hello application gateway is called **appgwtest**.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="74a24-201">Obter um nome DNS de Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="74a24-201">Get application gateway DNS name</span></span>

<span data-ttu-id="74a24-202">Depois de criar o gateway hello, Olá próxima etapa é tooconfigure Olá front-end para comunicação.</span><span class="sxs-lookup"><span data-stu-id="74a24-202">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="74a24-203">Ao usar um IP público, o gateway de aplicativo requer um nome DNS atribuído dinamicamente, o que não é amigável.</span><span class="sxs-lookup"><span data-stu-id="74a24-203">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="74a24-204">os usuários finais de tooensure pode pressionar o gateway de aplicativo hello, um registro CNAME pode ser usado toopoint toohello ponto de extremidade público do gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="74a24-204">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="74a24-205">[Configurando um nome de domínio personalizado no Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="74a24-205">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="74a24-206">toodo, detalhes de recuperar de gateway de aplicativo hello e seu nome de IP/DNS associado usando Olá PublicIPAddress elemento toohello anexado application gateway.</span><span class="sxs-lookup"><span data-stu-id="74a24-206">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="74a24-207">nome DNS do gateway do aplicativo Hello deve ser usado toocreate um registro CNAME, qual nome DNS pontos Olá duas web aplicativos toothis.</span><span class="sxs-lookup"><span data-stu-id="74a24-207">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="74a24-208">uso de saudação de registros de um não é recomendável porque Olá VIP pode ser alterado na reinicialização do application gateway.</span><span class="sxs-lookup"><span data-stu-id="74a24-208">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>


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

## <a name="next-steps"></a><span data-ttu-id="74a24-209">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="74a24-209">Next steps</span></span>

<span data-ttu-id="74a24-210">Se você quiser tooconfigure um toouse de gateway do aplicativo com um balanceador de carga interno (ILB), consulte [criar um gateway de aplicativo com um balanceador de carga interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="74a24-210">If you want tooconfigure an application gateway toouse with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="74a24-211">Se deseja obter mais informações sobre as opções de balanceamento de carga no geral, consulte:</span><span class="sxs-lookup"><span data-stu-id="74a24-211">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="74a24-212">Balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="74a24-212">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="74a24-213">Gerenciador de Tráfego do Azure</span><span class="sxs-lookup"><span data-stu-id="74a24-213">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

