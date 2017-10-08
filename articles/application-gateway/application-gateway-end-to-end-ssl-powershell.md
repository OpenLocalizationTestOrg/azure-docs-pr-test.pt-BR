---
title: aaaConfigure final tooend SSL com o Gateway de aplicativo do Azure | Microsoft Docs
description: Este artigo descreve como tooconfigure encerrar tooend SSL com o Application Gateway usando o PowerShell do Gerenciador de recursos do Azure
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: e6d80a33-4047-4538-8c83-e88876c8834e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: 7c280478e143d309e7665219441cbee8c81d9a80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-end-tooend-ssl-with-application-gateway-using-powershell"></a><span data-ttu-id="99684-103">Configurar final tooend SSL com o Application Gateway usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="99684-103">Configure end tooend SSL with Application Gateway using PowerShell</span></span>

## <a name="overview"></a><span data-ttu-id="99684-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="99684-104">Overview</span></span>

<span data-ttu-id="99684-105">Oferece suporte ao Gateway de aplicativo final tooend criptografia de tráfego.</span><span class="sxs-lookup"><span data-stu-id="99684-105">Application Gateway supports end tooend encryption of traffic.</span></span> <span data-ttu-id="99684-106">Application Gateway faz isso encerrando a conexão de SSL Olá no gateway do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="99684-106">Application Gateway does this by terminating hello SSL connection at hello application gateway.</span></span> <span data-ttu-id="99684-107">gateway de Hello, em seguida, aplica regras de roteamento de saudação toohello tráfego, criptografa novamente o pacote de saudação e encaminha Olá pacote toohello apropriado back-end com base nas regras de roteamento Olá definidas.</span><span class="sxs-lookup"><span data-stu-id="99684-107">hello gateway then applies hello routing rules toohello traffic, re-encrypts hello packet, and forwards hello packet toohello appropriate backend based on hello routing rules defined.</span></span> <span data-ttu-id="99684-108">Qualquer resposta do servidor de web hello atravessa Olá mesmo processo toohello back end usuário.</span><span class="sxs-lookup"><span data-stu-id="99684-108">Any response from hello web server goes through hello same process back toohello end user.</span></span>

<span data-ttu-id="99684-109">Outro recurso ao qual o gateway de aplicativo dá suporte para definir opções personalizadas de SSL.</span><span class="sxs-lookup"><span data-stu-id="99684-109">Another feature that application gateway supports defining custom SSL options.</span></span> <span data-ttu-id="99684-110">Application Gateway oferece suporte à desabilitação Olá após a versão do protocolo; **TLSv1.0**, **TLSv1.1**, e **TLSv1.2** também definindo Olá que cipher suites toouse e Olá a ordem de preferência.</span><span class="sxs-lookup"><span data-stu-id="99684-110">Application Gateway supports disabling hello following protocol version; **TLSv1.0**, **TLSv1.1**, and **TLSv1.2** as well defining hello which cipher suites toouse and hello order of preference.</span></span>  <span data-ttu-id="99684-111">toolearn mais sobre as opções configuráveis de SSL, visite [visão geral da política de SSL](application-gateway-SSL-policy-overview.md).</span><span class="sxs-lookup"><span data-stu-id="99684-111">toolearn more about configurable SSL options, visit [SSL Policy overview](application-gateway-SSL-policy-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="99684-112">O SSL 2.0 e o SSL 3.0 estão desabilitados por padrão e não podem ser habilitados.</span><span class="sxs-lookup"><span data-stu-id="99684-112">SSL 2.0 and SSL 3.0 are disabled by default and cannot be enabled.</span></span> <span data-ttu-id="99684-113">Elas são consideradas inseguras e não são capaz toobe usado com o Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="99684-113">They are considered unsecure and are not able toobe used with Application Gateway.</span></span>

![imagem de cenário][scenario]

## <a name="scenario"></a><span data-ttu-id="99684-115">Cenário</span><span class="sxs-lookup"><span data-stu-id="99684-115">Scenario</span></span>

<span data-ttu-id="99684-116">Nesse cenário, você aprenderá como toocreate um gateway de aplicativo usando encerrar tooend SSL usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="99684-116">In this scenario, you learn how toocreate an application gateway using end tooend SSL using PowerShell.</span></span>

<span data-ttu-id="99684-117">Este cenário:</span><span class="sxs-lookup"><span data-stu-id="99684-117">This scenario will:</span></span>

* <span data-ttu-id="99684-118">Criar um grupo de recursos denominado **appgw-rg**</span><span class="sxs-lookup"><span data-stu-id="99684-118">Create a resource group named **appgw-rg**</span></span>
* <span data-ttu-id="99684-119">Criar uma rede virtual denominada **appgwvnet** com um espaço de endereço de 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="99684-119">Create a virtual network named **appgwvnet** with an address space of 10.0.0.0/16.</span></span>
* <span data-ttu-id="99684-120">Crie duas sub-redes chamadas **appgwsubnet** e **appsubnet**.</span><span class="sxs-lookup"><span data-stu-id="99684-120">Create two subnets called **appgwsubnet** and **appsubnet**.</span></span>
* <span data-ttu-id="99684-121">Crie uma pequeno aplicativo gateway suporte final tooend criptografia SSL que versões de protocolos SSL limites e o conjunto de codificação.</span><span class="sxs-lookup"><span data-stu-id="99684-121">Create a small application gateway supporting end tooend SSL encryption that limits SSL protocols versions and cipher suites.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="99684-122">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="99684-122">Before you begin</span></span>

<span data-ttu-id="99684-123">tooconfigure final tooend SSL com um gateway de aplicativo, um certificado é necessário para o gateway de saudação e são necessários certificados para servidores de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="99684-123">tooconfigure end tooend SSL with an application gateway, a certificate is required for hello gateway and certificates are required for hello backend servers.</span></span> <span data-ttu-id="99684-124">certificado de gateway de saudação é usado tooencrypt e descriptografar Olá tráfego enviado tooit usando SSL.</span><span class="sxs-lookup"><span data-stu-id="99684-124">hello gateway certificate is used tooencrypt and decrypt hello traffic sent tooit using SSL.</span></span> <span data-ttu-id="99684-125">certificado de gateway Olá precisa toobe no formato de troca de informações pessoais (pfx).</span><span class="sxs-lookup"><span data-stu-id="99684-125">hello gateway certificate needs toobe in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="99684-126">Esse formato de arquivo permite Olá privada toobe chave exportado que é exigido pelo Olá application gateway tooperform Olá criptografia e a descriptografia de tráfego.</span><span class="sxs-lookup"><span data-stu-id="99684-126">This file format allows for hello private key toobe exported which is required by hello application gateway tooperform hello encryption and decryption of traffic.</span></span>

<span data-ttu-id="99684-127">Para final tooend SSL criptografia Olá back-end deve estar na lista de permissões com o application gateway.</span><span class="sxs-lookup"><span data-stu-id="99684-127">For end tooend SSL encryption hello backend must be whitelisted with application gateway.</span></span> <span data-ttu-id="99684-128">Isso é feito por carregar certificado público de saudação do gateway de aplicativo hello back-ends toohello.</span><span class="sxs-lookup"><span data-stu-id="99684-128">This is done by uploading hello public certificate of hello backends toohello application gateway.</span></span> <span data-ttu-id="99684-129">Isso garante que o gateway Olá aplicativo se comunica somente com instâncias de back-end conhecidos.</span><span class="sxs-lookup"><span data-stu-id="99684-129">This ensures that hello application gateway only communicates with known backend instances.</span></span> <span data-ttu-id="99684-130">Isso ainda mais protege a comunicação de tooend de término hello.</span><span class="sxs-lookup"><span data-stu-id="99684-130">This further secures hello end tooend communication.</span></span>

<span data-ttu-id="99684-131">Esse processo é descrito em Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="99684-131">This process is described in hello following steps:</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="99684-132">Criar hello grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="99684-132">Create hello Resource Group</span></span>

<span data-ttu-id="99684-133">Esta seção orienta você pelo processo de criação de um grupo de recursos, que contém o gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="99684-133">This section walks you through creating a resource group, that contains hello application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="99684-134">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="99684-134">Step 1</span></span>

<span data-ttu-id="99684-135">Faça logon no tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="99684-135">Log in tooyour Azure Account.</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="99684-136">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="99684-136">Step 2</span></span>

<span data-ttu-id="99684-137">Selecione Olá toouse de assinatura para esse cenário.</span><span class="sxs-lookup"><span data-stu-id="99684-137">Select hello subscription toouse for this scenario.</span></span>

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a><span data-ttu-id="99684-138">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="99684-138">Step 3</span></span>

<span data-ttu-id="99684-139">Crie um grupo de recursos (ignore esta etapa se você estiver usando um grupo de recursos existente).</span><span class="sxs-lookup"><span data-stu-id="99684-139">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="99684-140">Criar uma rede virtual e uma sub-rede para o gateway de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="99684-140">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="99684-141">Olá exemplo a seguir cria uma rede virtual e duas sub-redes.</span><span class="sxs-lookup"><span data-stu-id="99684-141">hello following example creates a virtual network and two subnets.</span></span> <span data-ttu-id="99684-142">Uma sub-rede é um gateway de aplicativo hello toohold usado.</span><span class="sxs-lookup"><span data-stu-id="99684-142">One subnet is used toohold hello application gateway.</span></span> <span data-ttu-id="99684-143">Olá outra sub-rede é usado para aplicativo web de saudação hospedagem hello back-ends.</span><span class="sxs-lookup"><span data-stu-id="99684-143">hello other subnet is used for hello backends hosting hello web application.</span></span>

### <a name="step-1"></a><span data-ttu-id="99684-144">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="99684-144">Step 1</span></span>

<span data-ttu-id="99684-145">Atribua um intervalo de endereços para sub-rede Olá ser usada para Olá Application Gateway em si.</span><span class="sxs-lookup"><span data-stu-id="99684-145">Assign an address range for hello subnet be used for hello Application Gateway itself.</span></span>

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> <span data-ttu-id="99684-146">As sub-redes configuradas para o gateway de aplicativo devem ser dimensionadas corretamente.</span><span class="sxs-lookup"><span data-stu-id="99684-146">Subnets configured for application gateway should be properly sized.</span></span> <span data-ttu-id="99684-147">O application gateway pode ser configurado para instâncias de too10.</span><span class="sxs-lookup"><span data-stu-id="99684-147">An application gateway can be configured for up too10 instances.</span></span> <span data-ttu-id="99684-148">Cada instância usa um endereço IP da sub-rede hello.</span><span class="sxs-lookup"><span data-stu-id="99684-148">Each instance takes one IP address from hello subnet.</span></span> <span data-ttu-id="99684-149">Uma sub-rede muito pequena pode afetar de forma adversa a ampliação de um gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="99684-149">Too small of a subnet can adversely affect scaling out an application gateway.</span></span>
> 
> 

### <a name="step-2"></a><span data-ttu-id="99684-150">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="99684-150">Step 2</span></span>

<span data-ttu-id="99684-151">Atribua um toobe de intervalo de endereço usado para Olá pool de endereços de back-end.</span><span class="sxs-lookup"><span data-stu-id="99684-151">Assign an address range toobe used for hello Backend address pool.</span></span>

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a><span data-ttu-id="99684-152">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="99684-152">Step 3</span></span>

<span data-ttu-id="99684-153">Crie uma rede virtual com sub-redes Olá definidos no hello etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="99684-153">Create a virtual network with hello subnets defined in hello preceding steps.</span></span>

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a><span data-ttu-id="99684-154">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="99684-154">Step 4</span></span>

<span data-ttu-id="99684-155">Recupere Olá rede virtual recursos e a sub-rede recursos toobe usado em Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="99684-155">Retrieve hello virtual network resource and subnet resources toobe used in hello following steps:</span></span>

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="99684-156">Criar um endereço IP público para a configuração de front-end Olá</span><span class="sxs-lookup"><span data-stu-id="99684-156">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="99684-157">Crie um toobe de recurso IP público usado para o gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="99684-157">Create a public IP resource toobe used for hello application gateway.</span></span> <span data-ttu-id="99684-158">Este endereço IP público será usado em uma etapa seguinte.</span><span class="sxs-lookup"><span data-stu-id="99684-158">This public IP address is used a following step.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> <span data-ttu-id="99684-159">Application Gateway não suporta o uso de saudação de um endereço IP público criado com um rótulo de domínio definido.</span><span class="sxs-lookup"><span data-stu-id="99684-159">Application Gateway does not support hello use of a public IP address created with a domain label defined.</span></span> <span data-ttu-id="99684-160">Há suporte para apenas para um endereço IP público com um rótulo de domínio criado dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="99684-160">Only a public IP address with a dynamically created domain label is supported.</span></span> <span data-ttu-id="99684-161">Se você precisar de um nome amigável de dns para o gateway de aplicativo hello, é recomendável toouse um CNAME registrar como um alias.</span><span class="sxs-lookup"><span data-stu-id="99684-161">If you require a friendly dns name for hello application gateway, it is recommended toouse a CNAME record as an alias.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="99684-162">Criar um objeto de configuração do gateway do aplicativo</span><span class="sxs-lookup"><span data-stu-id="99684-162">Create an application gateway configuration object</span></span>

<span data-ttu-id="99684-163">Todos os itens de configuração são definidos antes de criar o gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="99684-163">All configuration items are set before creating hello application gateway.</span></span> <span data-ttu-id="99684-164">Olá etapas a seguir criam Olá itens de configuração que são necessárias para um recurso do application gateway.</span><span class="sxs-lookup"><span data-stu-id="99684-164">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="99684-165">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="99684-165">Step 1</span></span>

<span data-ttu-id="99684-166">Criar uma configuração de IP de gateway do aplicativo, essa configuração define quais sub-rede Olá aplicativo gateway usa.</span><span class="sxs-lookup"><span data-stu-id="99684-166">Create an application gateway IP configuration, this setting configures what subnet hello application gateway uses.</span></span> <span data-ttu-id="99684-167">Quando o gateway de aplicativo é iniciado, ele pega um endereço IP da sub-rede de saudação configurado e encaminha os endereços IP de toohello de tráfego de rede no pool IP de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="99684-167">When application gateway starts, it picks up an IP address from hello subnet configured and routes network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="99684-168">Tenha em mente que cada instância usa um endereço IP.</span><span class="sxs-lookup"><span data-stu-id="99684-168">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a><span data-ttu-id="99684-169">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="99684-169">Step 2</span></span>

<span data-ttu-id="99684-170">Criar uma configuração de IP de front-end, essa configuração mapeia um ip público ou privado endereço toohello front-end do gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="99684-170">Create a front-end IP configuration, this setting maps a private or public ip address toohello front end of hello application gateway.</span></span> <span data-ttu-id="99684-171">Olá etapa a seguir associa o endereço IP público de saudação em Olá anterior etapa com configuração de IP de front-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="99684-171">hello following step associates hello public IP address in hello preceding step with hello front-end IP configuration.</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a><span data-ttu-id="99684-172">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="99684-172">Step 3</span></span>

<span data-ttu-id="99684-173">Configure o pool de endereços IP de back-end Olá com endereços IP de Olá dos servidores de web de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="99684-173">Configure hello back-end IP address pool with hello IP addresses of hello backend web servers.</span></span> <span data-ttu-id="99684-174">Esses endereços IP são endereços IP hello que recebem o tráfego de rede hello proveniente de um ponto de extremidade IP de front-end hello.</span><span class="sxs-lookup"><span data-stu-id="99684-174">These IP addresses are hello IP addresses that receive hello network traffic that comes from hello front-end IP endpoint.</span></span> <span data-ttu-id="99684-175">Substituir saudação tooadd de endereços IP a seguir seus próprios pontos de extremidade do endereço IP do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="99684-175">You replace hello following IP addresses tooadd your own application IP address endpoints.</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> <span data-ttu-id="99684-176">Um nome de domínio totalmente qualificado (FQDN) também é um valor válido no lugar de um endereço ip para servidores de back-end hello usando Olá - BackendFqdns switch.</span><span class="sxs-lookup"><span data-stu-id="99684-176">A fully qualified domain name (FQDN) is also a valid value in place of an ip address for hello backend servers by using hello -BackendFqdns switch.</span></span> 

### <a name="step-4"></a><span data-ttu-id="99684-177">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="99684-177">Step 4</span></span>

<span data-ttu-id="99684-178">Configure porta IP front-end de Olá para o ponto de extremidade de IP público hello.</span><span class="sxs-lookup"><span data-stu-id="99684-178">Configure hello front-end IP port for hello public IP endpoint.</span></span> <span data-ttu-id="99684-179">Esta porta é Olá que os usuários finais se conectem.</span><span class="sxs-lookup"><span data-stu-id="99684-179">This port is hello port that end users connect to.</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a><span data-ttu-id="99684-180">Etapa 5</span><span class="sxs-lookup"><span data-stu-id="99684-180">Step 5</span></span>

<span data-ttu-id="99684-181">Configure certificado Olá para o gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="99684-181">Configure hello certificate for hello application gateway.</span></span> <span data-ttu-id="99684-182">Esse certificado é usado toodecrypt e criptografar novamente o tráfego no gateway do aplicativo hello hello.</span><span class="sxs-lookup"><span data-stu-id="99684-182">This certificate is used toodecrypt and re-encrypt hello traffic on hello application gateway.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

> [!NOTE]
> <span data-ttu-id="99684-183">Este exemplo configura o certificado de saudação usado para a conexão SSL.</span><span class="sxs-lookup"><span data-stu-id="99684-183">This sample configures hello certificate used for SSL connection.</span></span> <span data-ttu-id="99684-184">certificado Olá precisa toobe no formato. pfx e senha Olá deve estar entre 4 too12 caracteres.</span><span class="sxs-lookup"><span data-stu-id="99684-184">hello certificate needs toobe in .pfx format, and hello password must be between 4 too12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="99684-185">Etapa 6</span><span class="sxs-lookup"><span data-stu-id="99684-185">Step 6</span></span>

<span data-ttu-id="99684-186">Crie ouvinte HTTP Olá para o gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="99684-186">Create hello HTTP listener for hello application gateway.</span></span> <span data-ttu-id="99684-187">Atribua a configuração de ip de front-end hello, porta e toouse do certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="99684-187">Assign hello front-end ip configuration, port, and SSL certificate toouse.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a><span data-ttu-id="99684-188">Etapa 7</span><span class="sxs-lookup"><span data-stu-id="99684-188">Step 7</span></span>

<span data-ttu-id="99684-189">Carregar certificado Olá toobe usado em Olá SSL habilitado recursos do pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="99684-189">Upload hello certificate toobe used on hello SSL enabled backend pool resources.</span></span>

> [!NOTE]
> <span data-ttu-id="99684-190">investigação de padrão de saudação obtém a chave pública de saudação do hello **padrão** associação SSL no endereço IP do hello back-end e compara Olá valor da chave pública recebe toohello valor da chave pública fornecidos aqui.</span><span class="sxs-lookup"><span data-stu-id="99684-190">hello default probe gets hello public key from hello **default** SSL binding on hello back-end's IP address and compares hello public key value it receives toohello public key value you provide here.</span></span> <span data-ttu-id="99684-191">Hello recuperados de chave pública não ser necessariamente fluxos de tráfego Olá pretendido site toowhich **se** você estiver usando cabeçalhos de host e SNI Olá back-end.</span><span class="sxs-lookup"><span data-stu-id="99684-191">hello retrieved public key may not necessarily be hello intended site toowhich traffic flows **if** you are using host headers and SNI on hello back-end.</span></span> <span data-ttu-id="99684-192">Em caso de dúvida, visite https://127.0.0.1/ tooconfirm de back-ends Olá qual certificado será usado para Olá **padrão** associação SSL.</span><span class="sxs-lookup"><span data-stu-id="99684-192">If in doubt, visit https://127.0.0.1/ on hello back-ends tooconfirm which certificate is used for hello **default** SSL binding.</span></span> <span data-ttu-id="99684-193">Use a chave pública de saudação do que a solicitação nesta seção.</span><span class="sxs-lookup"><span data-stu-id="99684-193">Use hello public key from that request in this section.</span></span> <span data-ttu-id="99684-194">Se você estiver usando cabeçalhos de host e SNI em associações de HTTPS e você não receber uma resposta e o certificado de um navegador manual solicitação toohttps://127.0.0.1/ em Olá back-ends, você deve configurar uma associação de SSL padrão em Olá back-ends.</span><span class="sxs-lookup"><span data-stu-id="99684-194">If you are using host-headers and SNI on HTTPS bindings and you do not receive a response and certificate from a manual browser request toohttps://127.0.0.1/ on hello back-ends, you must set up a default SSL binding on hello back-ends.</span></span> <span data-ttu-id="99684-195">Se você não fizer isso, a falha de testes e Olá back-end não está autorizado.</span><span class="sxs-lookup"><span data-stu-id="99684-195">If you do not do so, probes fail and hello back-end is not whitelisted.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> <span data-ttu-id="99684-196">certificado de saudação fornecido nesta etapa deve ser a chave pública de saudação do cert. pfx Olá presente no back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="99684-196">hello certificate provided in this step should be hello public key of hello pfx cert present on hello backend.</span></span> <span data-ttu-id="99684-197">Exporte o certificado de saudação (não o certificado raiz de saudação) instalado no servidor de back-end Olá no. CER Formatar e usá-lo nesta etapa.</span><span class="sxs-lookup"><span data-stu-id="99684-197">Export hello certificate (not hello root certificate) installed on hello backend server in .CER format and use it in this step.</span></span> <span data-ttu-id="99684-198">Esta etapa brancas Olá back-end com o gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="99684-198">This step whitelists hello backend with hello application gateway.</span></span>

### <a name="step-8"></a><span data-ttu-id="99684-199">Etapa 8</span><span class="sxs-lookup"><span data-stu-id="99684-199">Step 8</span></span>

<span data-ttu-id="99684-200">Defina configurações de http de back-end do gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="99684-200">Configure hello application gateway back-end http settings.</span></span> <span data-ttu-id="99684-201">Atribua Olá certificado carregado no hello anterior etapa toohello http configurações.</span><span class="sxs-lookup"><span data-stu-id="99684-201">Assign hello certificate uploaded in hello preceding step toohello http settings.</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a><span data-ttu-id="99684-202">Etapa 9</span><span class="sxs-lookup"><span data-stu-id="99684-202">Step 9</span></span>

<span data-ttu-id="99684-203">Crie uma regra de roteamento de Balanceador de carga que configura o comportamento de Balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="99684-203">Create a load balancer routing rule that configures hello load balancer behavior.</span></span> <span data-ttu-id="99684-204">Neste exemplo, é criada uma regra básica de round robin.</span><span class="sxs-lookup"><span data-stu-id="99684-204">In this example, a basic round robin rule is created.</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a><span data-ttu-id="99684-205">Etapa 10</span><span class="sxs-lookup"><span data-stu-id="99684-205">Step 10</span></span>

<span data-ttu-id="99684-206">Configure o tamanho de instância de saudação do gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="99684-206">Configure hello instance size of hello application gateway.</span></span>  <span data-ttu-id="99684-207">Olá os tamanhos disponíveis são **padrão\_pequeno**, **padrão\_médio**, e **padrão\_grande**.</span><span class="sxs-lookup"><span data-stu-id="99684-207">hello available sizes are **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large**.</span></span>  <span data-ttu-id="99684-208">Capacidade, valores disponíveis Olá variam de 1 a 10.</span><span class="sxs-lookup"><span data-stu-id="99684-208">For capacity, hello available values are 1 through 10.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> <span data-ttu-id="99684-209">É possível escolher uma contagem de instâncias de 1 para fins de teste.</span><span class="sxs-lookup"><span data-stu-id="99684-209">An instance count of 1 can be chosen for testing purposes.</span></span> <span data-ttu-id="99684-210">É importante tooknow qualquer instância de contagem em duas instâncias não é coberto por Olá SLA e, portanto, não recomendável.</span><span class="sxs-lookup"><span data-stu-id="99684-210">It is important tooknow that any instance count under two instances is not covered by hello SLA and are therefore not recommended.</span></span> <span data-ttu-id="99684-211">Os gateways pequenos são toobe usado para desenvolvimento de teste e não para fins de produção.</span><span class="sxs-lookup"><span data-stu-id="99684-211">Small gateways are toobe used for dev test and not for production purposes.</span></span>

### <a name="step-11"></a><span data-ttu-id="99684-212">Etapa 11</span><span class="sxs-lookup"><span data-stu-id="99684-212">Step 11</span></span>

<span data-ttu-id="99684-213">Configure Olá toobe de política SSL usado em Olá Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="99684-213">Configure hello SSL policy toobe used on hello Application Gateway.</span></span> <span data-ttu-id="99684-214">Application Gateway oferece suporte a saudação capacidade tooset uma versão mínima para versões do protocolo SSL.</span><span class="sxs-lookup"><span data-stu-id="99684-214">Application Gateway supports hello ability tooset a minimum version for SSL protocol versions.</span></span>

<span data-ttu-id="99684-215">Hello valores a seguir estão uma lista das versões de protocolo que podem ser definidas.</span><span class="sxs-lookup"><span data-stu-id="99684-215">hello following values are a list of protocol versions that can be defined.</span></span>

* <span data-ttu-id="99684-216">**TLSv1_0**</span><span class="sxs-lookup"><span data-stu-id="99684-216">**TLSv1_0**</span></span>
* <span data-ttu-id="99684-217">**TLSv1_1**</span><span class="sxs-lookup"><span data-stu-id="99684-217">**TLSv1_1**</span></span>
* <span data-ttu-id="99684-218">**TLSv1_2**</span><span class="sxs-lookup"><span data-stu-id="99684-218">**TLSv1_2**</span></span>

<span data-ttu-id="99684-219">Conjuntos de Olá versão mínima do protocolo muito**TLSv1_2** e permite **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_ SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**e **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** somente.</span><span class="sxs-lookup"><span data-stu-id="99684-219">Sets hello minimum protocol version too**TLSv1_2** and enables **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** only.</span></span>

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="99684-220">Criar hello Application Gateway</span><span class="sxs-lookup"><span data-stu-id="99684-220">Create hello Application Gateway</span></span>

<span data-ttu-id="99684-221">Usando Olá todas as etapas anteriores, crie Olá Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="99684-221">Using all hello preceding steps, create hello Application Gateway.</span></span> <span data-ttu-id="99684-222">criação de saudação do gateway de saudação é um processo de execução longa.</span><span class="sxs-lookup"><span data-stu-id="99684-222">hello creation of hello gateway is a long running process.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a><span data-ttu-id="99684-223">Limitar as versões de protocolo SSL em um Gateway de Aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="99684-223">Limit SSL protocol versions on an existing Application Gateway</span></span>

<span data-ttu-id="99684-224">Olá etapas anteriores levá-lo por meio de criar um aplicativo com final tooend SSL e desabilitando determinadas versões do protocolo SSL.</span><span class="sxs-lookup"><span data-stu-id="99684-224">hello preceding steps take you through creating an application with end tooend SSL and disabling certain SSL protocol versions.</span></span> <span data-ttu-id="99684-225">Olá, exemplo a seguir desabilita certas políticas SSL em um gateway existente do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="99684-225">hello following example disables certain SSL policies on an existing application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="99684-226">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="99684-226">Step 1</span></span>

<span data-ttu-id="99684-227">Recupere Olá tooupdate de gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="99684-227">Retrieve hello application gateway tooupdate.</span></span>

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a><span data-ttu-id="99684-228">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="99684-228">Step 2</span></span>

<span data-ttu-id="99684-229">Defina uma política de SSL.</span><span class="sxs-lookup"><span data-stu-id="99684-229">Define an SSL policy.</span></span> <span data-ttu-id="99684-230">Saudação de exemplo a seguir, TLSv1.0 e TLSv1.1 são desabilitados e Olá conjuntos de codificação **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256** , **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, e  **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** é Olá únicos permitidos.</span><span class="sxs-lookup"><span data-stu-id="99684-230">In hello following example, TLSv1.0 and TLSv1.1 are disabled and hello cipher suites **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** are hello only ones allowed.</span></span>

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a><span data-ttu-id="99684-231">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="99684-231">Step 3</span></span>

<span data-ttu-id="99684-232">Por fim, atualize o gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="99684-232">Finally, update hello gateway.</span></span> <span data-ttu-id="99684-233">É importante toonote nesta última etapa é uma tarefa demorada.</span><span class="sxs-lookup"><span data-stu-id="99684-233">It is important toonote that this last step is a long running task.</span></span> <span data-ttu-id="99684-234">Quando estiver pronto, tooend final SSL é configurada no gateway do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="99684-234">When it is done, end tooend SSL is configured on hello application gateway.</span></span>

```powershell
$gw | Set-AzureRmApplicationGateway
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="99684-235">Obter um nome DNS de Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="99684-235">Get application gateway DNS name</span></span>

<span data-ttu-id="99684-236">Depois de criar o gateway hello, Olá próxima etapa é tooconfigure Olá front-end para comunicação.</span><span class="sxs-lookup"><span data-stu-id="99684-236">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="99684-237">Ao usar um IP público, o gateway de aplicativo requer um nome DNS atribuído dinamicamente, o que não é amigável.</span><span class="sxs-lookup"><span data-stu-id="99684-237">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="99684-238">os usuários finais de tooensure pode pressionar o gateway de aplicativo hello, um registro CNAME pode ser usado toopoint toohello ponto de extremidade público do gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="99684-238">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="99684-239">[Configurando um nome de domínio personalizado no Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="99684-239">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="99684-240">toodo, detalhes de recuperar de gateway de aplicativo hello e seu nome de IP/DNS associado usando Olá PublicIPAddress elemento toohello anexado application gateway.</span><span class="sxs-lookup"><span data-stu-id="99684-240">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="99684-241">nome DNS do gateway do aplicativo Hello deve ser usado toocreate um registro CNAME, qual nome DNS pontos Olá duas web aplicativos toothis.</span><span class="sxs-lookup"><span data-stu-id="99684-241">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="99684-242">uso de saudação de registros de um não é recomendável porque Olá VIP pode ser alterado na reinicialização do application gateway.</span><span class="sxs-lookup"><span data-stu-id="99684-242">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="99684-243">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="99684-243">Next steps</span></span>

<span data-ttu-id="99684-244">Saiba mais sobre a proteção de segurança de saudação de seus aplicativos web com o Firewall do aplicativo Web por meio do Application Gateway visitando [visão geral do Firewall de aplicativo Web](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="99684-244">Learn about hardening hello security of your web applications with Web Application Firewall through Application Gateway by visiting [Web Application Firewall Overview](application-gateway-webapplicationfirewall-overview.md)</span></span>

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
