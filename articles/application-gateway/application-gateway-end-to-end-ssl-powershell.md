---
title: Configurar o SSL de ponta a ponta no Gateway de Aplicativo do Azure | Microsoft Docs
description: Este artigo descreve como configurar o SSL de ponta a ponta com o Gateway de Aplicativo usando o Azure PowerShell Resource Manager
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
ms.openlocfilehash: 6d969d6a0c649c263e1d5bb99bdbceec484cb9a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-end-to-end-ssl-with-application-gateway-using-powershell"></a><span data-ttu-id="101c1-103">Configurar o SSL de ponta a ponta com o Gateway de Aplicativo usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="101c1-103">Configure end to end SSL with Application Gateway using PowerShell</span></span>

## <a name="overview"></a><span data-ttu-id="101c1-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="101c1-104">Overview</span></span>

<span data-ttu-id="101c1-105">O Gateway de Aplicativo oferece suporte à criptografia de tráfego de ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="101c1-105">Application Gateway supports end to end encryption of traffic.</span></span> <span data-ttu-id="101c1-106">O Gateway de Aplicativo faz isso ao encerrar a conexão SSL no gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="101c1-106">Application Gateway does this by terminating the SSL connection at the application gateway.</span></span> <span data-ttu-id="101c1-107">O gateway, em seguida, aplica as regras de roteamento ao tráfego, criptografa o pacote novamente e encaminha o pacote para o back-end apropriado com base nas regras de roteamento definidas.</span><span class="sxs-lookup"><span data-stu-id="101c1-107">The gateway then applies the routing rules to the traffic, re-encrypts the packet, and forwards the packet to the appropriate backend based on the routing rules defined.</span></span> <span data-ttu-id="101c1-108">Qualquer resposta do servidor Web passa pelo mesmo processo de volta para o usuário final.</span><span class="sxs-lookup"><span data-stu-id="101c1-108">Any response from the web server goes through the same process back to the end user.</span></span>

<span data-ttu-id="101c1-109">Outro recurso ao qual o gateway de aplicativo dá suporte para definir opções personalizadas de SSL.</span><span class="sxs-lookup"><span data-stu-id="101c1-109">Another feature that application gateway supports defining custom SSL options.</span></span> <span data-ttu-id="101c1-110">O Gateway de Aplicativo oferece suporte a desabilitar a seguinte versão de protocolo; **TLSv1.0**, **TLSv1.1**, e **TLSv1.2** como também define quais conjuntos de uso e a ordem de preferência de criptografia.</span><span class="sxs-lookup"><span data-stu-id="101c1-110">Application Gateway supports disabling the following protocol version; **TLSv1.0**, **TLSv1.1**, and **TLSv1.2** as well defining the which cipher suites to use and the order of preference.</span></span>  <span data-ttu-id="101c1-111">Para saber mais sobre as opções configuráveis de SSL, visite [visão geral da política de SSL](application-gateway-SSL-policy-overview.md).</span><span class="sxs-lookup"><span data-stu-id="101c1-111">To learn more about configurable SSL options, visit [SSL Policy overview](application-gateway-SSL-policy-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="101c1-112">O SSL 2.0 e o SSL 3.0 estão desabilitados por padrão e não podem ser habilitados.</span><span class="sxs-lookup"><span data-stu-id="101c1-112">SSL 2.0 and SSL 3.0 are disabled by default and cannot be enabled.</span></span> <span data-ttu-id="101c1-113">Eles são considerados não seguras e não podem ser usados com o Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="101c1-113">They are considered unsecure and are not able to be used with Application Gateway.</span></span>

![imagem de cenário][scenario]

## <a name="scenario"></a><span data-ttu-id="101c1-115">Cenário</span><span class="sxs-lookup"><span data-stu-id="101c1-115">Scenario</span></span>

<span data-ttu-id="101c1-116">Neste cenário, você aprenderá a criar um gateway de aplicativo usando o SSL de ponta a ponta usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="101c1-116">In this scenario, you learn how to create an application gateway using end to end SSL using PowerShell.</span></span>

<span data-ttu-id="101c1-117">Este cenário:</span><span class="sxs-lookup"><span data-stu-id="101c1-117">This scenario will:</span></span>

* <span data-ttu-id="101c1-118">Criar um grupo de recursos denominado **appgw-rg**</span><span class="sxs-lookup"><span data-stu-id="101c1-118">Create a resource group named **appgw-rg**</span></span>
* <span data-ttu-id="101c1-119">Criar uma rede virtual denominada **appgwvnet** com um espaço de endereço de 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="101c1-119">Create a virtual network named **appgwvnet** with an address space of 10.0.0.0/16.</span></span>
* <span data-ttu-id="101c1-120">Crie duas sub-redes chamadas **appgwsubnet** e **appsubnet**.</span><span class="sxs-lookup"><span data-stu-id="101c1-120">Create two subnets called **appgwsubnet** and **appsubnet**.</span></span>
* <span data-ttu-id="101c1-121">Crie um gateway de aplicativo pequeno que oferece suporte à criptografia de SSL de ponta a ponta que versões de protocolos SSL limites e conjuntos de codificação.</span><span class="sxs-lookup"><span data-stu-id="101c1-121">Create a small application gateway supporting end to end SSL encryption that limits SSL protocols versions and cipher suites.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="101c1-122">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="101c1-122">Before you begin</span></span>

<span data-ttu-id="101c1-123">Para configurar o SSL de ponta a ponta com um gateway de aplicativo, um certificado é necessário para o gateway e são necessários certificados para os servidores de back-end.</span><span class="sxs-lookup"><span data-stu-id="101c1-123">To configure end to end SSL with an application gateway, a certificate is required for the gateway and certificates are required for the backend servers.</span></span> <span data-ttu-id="101c1-124">O certificado de gateway é usado para criptografar e descriptografar o tráfego enviado para ele usando SSL.</span><span class="sxs-lookup"><span data-stu-id="101c1-124">The gateway certificate is used to encrypt and decrypt the traffic sent to it using SSL.</span></span> <span data-ttu-id="101c1-125">O certificado do gateway precisa estar no formato pfx (Troca de Informações Pessoais).</span><span class="sxs-lookup"><span data-stu-id="101c1-125">The gateway certificate needs to be in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="101c1-126">Esse formato de arquivo permite que a chave privada seja exportada, o que é exigido pelo Gateway de Aplicativo para executar criptografia e descriptografia de tráfego.</span><span class="sxs-lookup"><span data-stu-id="101c1-126">This file format allows for the private key to be exported which is required by the application gateway to perform the encryption and decryption of traffic.</span></span>

<span data-ttu-id="101c1-127">Para criptografia SSL de ponta a ponta, o back-end deve estar na lista branca do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="101c1-127">For end to end SSL encryption the backend must be whitelisted with application gateway.</span></span> <span data-ttu-id="101c1-128">Isso é feito por meio do upload do certificado público dos back-ends para o gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="101c1-128">This is done by uploading the public certificate of the backends to the application gateway.</span></span> <span data-ttu-id="101c1-129">Isso garante que o gateway de aplicativo se comunique somente com instâncias de back-end conhecidas.</span><span class="sxs-lookup"><span data-stu-id="101c1-129">This ensures that the application gateway only communicates with known backend instances.</span></span> <span data-ttu-id="101c1-130">Isso protege ainda mais a comunicação de ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="101c1-130">This further secures the end to end communication.</span></span>

<span data-ttu-id="101c1-131">Cada atributo é descrito nas etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="101c1-131">This process is described in the following steps:</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="101c1-132">Criar o Grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="101c1-132">Create the Resource Group</span></span>

<span data-ttu-id="101c1-133">Esta seção orienta você pela criação de um grupo de recursos que contenha o gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="101c1-133">This section walks you through creating a resource group, that contains the application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="101c1-134">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="101c1-134">Step 1</span></span>

<span data-ttu-id="101c1-135">Faça logon na sua Conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="101c1-135">Log in to your Azure Account.</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="101c1-136">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="101c1-136">Step 2</span></span>

<span data-ttu-id="101c1-137">Selecione a assinatura a ser usada nesse cenário.</span><span class="sxs-lookup"><span data-stu-id="101c1-137">Select the subscription to use for this scenario.</span></span>

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a><span data-ttu-id="101c1-138">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="101c1-138">Step 3</span></span>

<span data-ttu-id="101c1-139">Crie um grupo de recursos (ignore esta etapa se você estiver usando um grupo de recursos existente).</span><span class="sxs-lookup"><span data-stu-id="101c1-139">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="101c1-140">Criar uma rede virtual e uma sub-rede para o gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="101c1-140">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="101c1-141">O exemplo a seguir cria uma rede virtual e duas sub-redes.</span><span class="sxs-lookup"><span data-stu-id="101c1-141">The following example creates a virtual network and two subnets.</span></span> <span data-ttu-id="101c1-142">Uma sub-rede é usada para armazenar o gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="101c1-142">One subnet is used to hold the application gateway.</span></span> <span data-ttu-id="101c1-143">A outra sub-rede é usada para os back-ends que hospedam o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="101c1-143">The other subnet is used for the backends hosting the web application.</span></span>

### <a name="step-1"></a><span data-ttu-id="101c1-144">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="101c1-144">Step 1</span></span>

<span data-ttu-id="101c1-145">Atribua um intervalo de endereços para que a sub-rede seja usada para o próprio Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="101c1-145">Assign an address range for the subnet be used for the Application Gateway itself.</span></span>

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> <span data-ttu-id="101c1-146">As sub-redes configuradas para o gateway de aplicativo devem ser dimensionadas corretamente.</span><span class="sxs-lookup"><span data-stu-id="101c1-146">Subnets configured for application gateway should be properly sized.</span></span> <span data-ttu-id="101c1-147">Um gateway de aplicativo pode ser configurado para até 10 instâncias.</span><span class="sxs-lookup"><span data-stu-id="101c1-147">An application gateway can be configured for up to 10 instances.</span></span> <span data-ttu-id="101c1-148">Cada instância usa um endereço IP da sub-rede.</span><span class="sxs-lookup"><span data-stu-id="101c1-148">Each instance takes one IP address from the subnet.</span></span> <span data-ttu-id="101c1-149">Uma sub-rede muito pequena pode afetar de forma adversa a ampliação de um gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="101c1-149">Too small of a subnet can adversely affect scaling out an application gateway.</span></span>
> 
> 

### <a name="step-2"></a><span data-ttu-id="101c1-150">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="101c1-150">Step 2</span></span>

<span data-ttu-id="101c1-151">Atribua um intervalo de endereços a ser usado para o pool de endereços do Back-end.</span><span class="sxs-lookup"><span data-stu-id="101c1-151">Assign an address range to be used for the Backend address pool.</span></span>

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a><span data-ttu-id="101c1-152">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="101c1-152">Step 3</span></span>

<span data-ttu-id="101c1-153">Crie uma rede virtual com as sub-redes definidas nas etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="101c1-153">Create a virtual network with the subnets defined in the preceding steps.</span></span>

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a><span data-ttu-id="101c1-154">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="101c1-154">Step 4</span></span>

<span data-ttu-id="101c1-155">Recupere o recurso de rede virtual e os recursos de sub-rede a serem usados nestas etapas:</span><span class="sxs-lookup"><span data-stu-id="101c1-155">Retrieve the virtual network resource and subnet resources to be used in the following steps:</span></span>

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="101c1-156">Criar um endereço IP público para a configuração de front-end</span><span class="sxs-lookup"><span data-stu-id="101c1-156">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="101c1-157">Crie um recurso IP público a ser usado para o gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="101c1-157">Create a public IP resource to be used for the application gateway.</span></span> <span data-ttu-id="101c1-158">Este endereço IP público será usado em uma etapa seguinte.</span><span class="sxs-lookup"><span data-stu-id="101c1-158">This public IP address is used a following step.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> <span data-ttu-id="101c1-159">O Gateway de Aplicativo não dá suporte ao uso de um endereço IP público criado com um rótulo de domínio definido.</span><span class="sxs-lookup"><span data-stu-id="101c1-159">Application Gateway does not support the use of a public IP address created with a domain label defined.</span></span> <span data-ttu-id="101c1-160">Há suporte para apenas para um endereço IP público com um rótulo de domínio criado dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="101c1-160">Only a public IP address with a dynamically created domain label is supported.</span></span> <span data-ttu-id="101c1-161">Se você precisar de um nome amigável de dns para o gateway de aplicativo, é recomendável usar um registro CNAME como alias.</span><span class="sxs-lookup"><span data-stu-id="101c1-161">If you require a friendly dns name for the application gateway, it is recommended to use a CNAME record as an alias.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="101c1-162">Criar um objeto de configuração do gateway do aplicativo</span><span class="sxs-lookup"><span data-stu-id="101c1-162">Create an application gateway configuration object</span></span>

<span data-ttu-id="101c1-163">Todos os itens de configuração são definidos antes da criação do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="101c1-163">All configuration items are set before creating the application gateway.</span></span> <span data-ttu-id="101c1-164">As etapas a seguir criam os itens de configuração necessários para um recurso de gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="101c1-164">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="101c1-165">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="101c1-165">Step 1</span></span>

<span data-ttu-id="101c1-166">Crie uma configuração de IP do gateway de aplicativo para configurar qual sub-rede será usada pelo gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="101c1-166">Create an application gateway IP configuration, this setting configures what subnet the application gateway uses.</span></span> <span data-ttu-id="101c1-167">Quando o Gateway de Aplicativo é iniciado, ele escolhe um endereço IP na sub-rede configurada e encaminha o tráfego de rede para os endereços IP no pool de IPs de back-end.</span><span class="sxs-lookup"><span data-stu-id="101c1-167">When application gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="101c1-168">Tenha em mente que cada instância usa um endereço IP.</span><span class="sxs-lookup"><span data-stu-id="101c1-168">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a><span data-ttu-id="101c1-169">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="101c1-169">Step 2</span></span>

<span data-ttu-id="101c1-170">Crie uma configuração de IP de front-end para mapear um endereço ip público ou privado para o front-end do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="101c1-170">Create a front-end IP configuration, this setting maps a private or public ip address to the front end of the application gateway.</span></span> <span data-ttu-id="101c1-171">A etapa a seguir associa o endereço IP público da etapa anterior à configuração de IP do front-end.</span><span class="sxs-lookup"><span data-stu-id="101c1-171">The following step associates the public IP address in the preceding step with the front-end IP configuration.</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a><span data-ttu-id="101c1-172">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="101c1-172">Step 3</span></span>

<span data-ttu-id="101c1-173">Configure o pool de endereços IP do back-end com os endereços IP dos servidores Web de back-end.</span><span class="sxs-lookup"><span data-stu-id="101c1-173">Configure the back-end IP address pool with the IP addresses of the backend web servers.</span></span> <span data-ttu-id="101c1-174">Esses endereços IP são os que receberão o tráfego de rede proveniente do ponto de extremidade do IP de front-end.</span><span class="sxs-lookup"><span data-stu-id="101c1-174">These IP addresses are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span></span> <span data-ttu-id="101c1-175">Você substitui os endereços IP a seguir para adicionar seus próprios pontos de extremidade de endereço IP do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="101c1-175">You replace the following IP addresses to add your own application IP address endpoints.</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> <span data-ttu-id="101c1-176">Um nome de domínio totalmente qualificado (FQDN) também é um valor válido no lugar de um endereço ip para os servidores de back-end usando a opção -BackendFqdns.</span><span class="sxs-lookup"><span data-stu-id="101c1-176">A fully qualified domain name (FQDN) is also a valid value in place of an ip address for the backend servers by using the -BackendFqdns switch.</span></span> 

### <a name="step-4"></a><span data-ttu-id="101c1-177">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="101c1-177">Step 4</span></span>

<span data-ttu-id="101c1-178">Configure a porta IP front-end para o ponto de extremidade IP público.</span><span class="sxs-lookup"><span data-stu-id="101c1-178">Configure the front-end IP port for the public IP endpoint.</span></span> <span data-ttu-id="101c1-179">Essa porta é a porta à qual os usuários finais se conectam.</span><span class="sxs-lookup"><span data-stu-id="101c1-179">This port is the port that end users connect to.</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a><span data-ttu-id="101c1-180">Etapa 5</span><span class="sxs-lookup"><span data-stu-id="101c1-180">Step 5</span></span>

<span data-ttu-id="101c1-181">Configure o certificado para o gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="101c1-181">Configure the certificate for the application gateway.</span></span> <span data-ttu-id="101c1-182">Esse certificado é usado para descriptografar e criptografar novamente o tráfego no gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="101c1-182">This certificate is used to decrypt and re-encrypt the traffic on the application gateway.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path to .pfx file> -Password <password for certificate file>
```

> [!NOTE]
> <span data-ttu-id="101c1-183">Esta amostra configura o certificado usado para a conexão SSL.</span><span class="sxs-lookup"><span data-stu-id="101c1-183">This sample configures the certificate used for SSL connection.</span></span> <span data-ttu-id="101c1-184">O certificado deve estar no formato .pfx e a senha deve ter entre 4 e 12 caracteres.</span><span class="sxs-lookup"><span data-stu-id="101c1-184">The certificate needs to be in .pfx format, and the password must be between 4 to 12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="101c1-185">Etapa 6</span><span class="sxs-lookup"><span data-stu-id="101c1-185">Step 6</span></span>

<span data-ttu-id="101c1-186">Crie o ouvinte HTTP para o gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="101c1-186">Create the HTTP listener for the application gateway.</span></span> <span data-ttu-id="101c1-187">Atribua a configuração do ip, a porta e o certificado ssl do front-end a ser usado.</span><span class="sxs-lookup"><span data-stu-id="101c1-187">Assign the front-end ip configuration, port, and SSL certificate to use.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a><span data-ttu-id="101c1-188">Etapa 7</span><span class="sxs-lookup"><span data-stu-id="101c1-188">Step 7</span></span>

<span data-ttu-id="101c1-189">Carregue o certificado a ser usado nos recursos do pool de back-end habilitado para SSL.</span><span class="sxs-lookup"><span data-stu-id="101c1-189">Upload the certificate to be used on the SSL enabled backend pool resources.</span></span>

> [!NOTE]
> <span data-ttu-id="101c1-190">A investigação padrão obtém a chave pública a associação SSL **padrão** no endereço IP do back-end e compara o valor da chave pública que recebe ao valor da chave pública fornecida aqui.</span><span class="sxs-lookup"><span data-stu-id="101c1-190">The default probe gets the public key from the **default** SSL binding on the back-end's IP address and compares the public key value it receives to the public key value you provide here.</span></span> <span data-ttu-id="101c1-191">A chave pública recuperada pode não ser necessariamente o local desejado para o qual o tráfego fluirá **se** você estiver usando cabeçalhos de host e SNI no back-end.</span><span class="sxs-lookup"><span data-stu-id="101c1-191">The retrieved public key may not necessarily be the intended site to which traffic flows **if** you are using host headers and SNI on the back-end.</span></span> <span data-ttu-id="101c1-192">Em caso de dúvida, visite https://127.0.0.1/ nos back-ends para confirmar qual certificado será usado para a associação SSL **padrão**.</span><span class="sxs-lookup"><span data-stu-id="101c1-192">If in doubt, visit https://127.0.0.1/ on the back-ends to confirm which certificate is used for the **default** SSL binding.</span></span> <span data-ttu-id="101c1-193">Use a chave pública dessa solicitação nesta seção.</span><span class="sxs-lookup"><span data-stu-id="101c1-193">Use the public key from that request in this section.</span></span> <span data-ttu-id="101c1-194">Se você estiver usando cabeçalhos de host e SNI em associações HTTPS e você não receberá uma resposta e um certificado de uma solicitação de navegador manual para https://127.0.0.1/ em back-ends, deverá configurar uma associação SSL padrão nos back-ends.</span><span class="sxs-lookup"><span data-stu-id="101c1-194">If you are using host-headers and SNI on HTTPS bindings and you do not receive a response and certificate from a manual browser request to https://127.0.0.1/ on the back-ends, you must set up a default SSL binding on the back-ends.</span></span> <span data-ttu-id="101c1-195">Se você não fizer isso, as investigações falharão e o back-end não estará na lista branca.</span><span class="sxs-lookup"><span data-stu-id="101c1-195">If you do not do so, probes fail and the back-end is not whitelisted.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> <span data-ttu-id="101c1-196">O certificado fornecido nesta etapa deve ser a chave pública do certificado pfx presente no back-end.</span><span class="sxs-lookup"><span data-stu-id="101c1-196">The certificate provided in this step should be the public key of the pfx cert present on the backend.</span></span> <span data-ttu-id="101c1-197">Exporte o certificado (não o certificado raiz) instalado no servidor de back-end no formato .CER e use-o nesta etapa.</span><span class="sxs-lookup"><span data-stu-id="101c1-197">Export the certificate (not the root certificate) installed on the backend server in .CER format and use it in this step.</span></span> <span data-ttu-id="101c1-198">Esta etapa coloca o back-end na lista branca do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="101c1-198">This step whitelists the backend with the application gateway.</span></span>

### <a name="step-8"></a><span data-ttu-id="101c1-199">Etapa 8</span><span class="sxs-lookup"><span data-stu-id="101c1-199">Step 8</span></span>

<span data-ttu-id="101c1-200">Defina as configurações de http de back-end do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="101c1-200">Configure the application gateway back-end http settings.</span></span> <span data-ttu-id="101c1-201">Atribua o certificado carregado na etapa anterior às configurações de http.</span><span class="sxs-lookup"><span data-stu-id="101c1-201">Assign the certificate uploaded in the preceding step to the http settings.</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a><span data-ttu-id="101c1-202">Etapa 9</span><span class="sxs-lookup"><span data-stu-id="101c1-202">Step 9</span></span>

<span data-ttu-id="101c1-203">Crie uma regra de roteamento do balanceador de carga que configure o comportamento do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="101c1-203">Create a load balancer routing rule that configures the load balancer behavior.</span></span> <span data-ttu-id="101c1-204">Neste exemplo, é criada uma regra básica de round robin.</span><span class="sxs-lookup"><span data-stu-id="101c1-204">In this example, a basic round robin rule is created.</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a><span data-ttu-id="101c1-205">Etapa 10</span><span class="sxs-lookup"><span data-stu-id="101c1-205">Step 10</span></span>

<span data-ttu-id="101c1-206">Configure o tamanho da instância do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="101c1-206">Configure the instance size of the application gateway.</span></span>  <span data-ttu-id="101c1-207">Os tamanhos disponíveis são **Standard\_Small**, **Standard\_Medium** e **Standard\_Large**.</span><span class="sxs-lookup"><span data-stu-id="101c1-207">The available sizes are **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large**.</span></span>  <span data-ttu-id="101c1-208">Para a capacidade e os valores disponíveis são 1 a 10.</span><span class="sxs-lookup"><span data-stu-id="101c1-208">For capacity, the available values are 1 through 10.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> <span data-ttu-id="101c1-209">É possível escolher uma contagem de instâncias de 1 para fins de teste.</span><span class="sxs-lookup"><span data-stu-id="101c1-209">An instance count of 1 can be chosen for testing purposes.</span></span> <span data-ttu-id="101c1-210">É importante saber que qualquer contagem de instâncias em duas instâncias não é coberta por um SLA e, portanto, não são recomendadas.</span><span class="sxs-lookup"><span data-stu-id="101c1-210">It is important to know that any instance count under two instances is not covered by the SLA and are therefore not recommended.</span></span> <span data-ttu-id="101c1-211">Gateways pequenos devem ser usados para teste de desenvolvimento e não para fins de produção.</span><span class="sxs-lookup"><span data-stu-id="101c1-211">Small gateways are to be used for dev test and not for production purposes.</span></span>

### <a name="step-11"></a><span data-ttu-id="101c1-212">Etapa 11</span><span class="sxs-lookup"><span data-stu-id="101c1-212">Step 11</span></span>

<span data-ttu-id="101c1-213">Configure a política SSL a ser usada no Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="101c1-213">Configure the SSL policy to be used on the Application Gateway.</span></span> <span data-ttu-id="101c1-214">O Gateway de Aplicativo oferece suporte a capacidade de definir uma versão mínima para versões de protocolo SSL.</span><span class="sxs-lookup"><span data-stu-id="101c1-214">Application Gateway supports the ability to set a minimum version for SSL protocol versions.</span></span>

<span data-ttu-id="101c1-215">Os valores a seguir são uma lista de versões do protocolo que podem ser definidas.</span><span class="sxs-lookup"><span data-stu-id="101c1-215">The following values are a list of protocol versions that can be defined.</span></span>

* <span data-ttu-id="101c1-216">**TLSv1_0**</span><span class="sxs-lookup"><span data-stu-id="101c1-216">**TLSv1_0**</span></span>
* <span data-ttu-id="101c1-217">**TLSv1_1**</span><span class="sxs-lookup"><span data-stu-id="101c1-217">**TLSv1_1**</span></span>
* <span data-ttu-id="101c1-218">**TLSv1_2**</span><span class="sxs-lookup"><span data-stu-id="101c1-218">**TLSv1_2**</span></span>

<span data-ttu-id="101c1-219">Define a versão mínima do protocolo para **TLSv1_2** e permita **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, e **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** somente.</span><span class="sxs-lookup"><span data-stu-id="101c1-219">Sets the minimum protocol version to **TLSv1_2** and enables **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** only.</span></span>

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-the-application-gateway"></a><span data-ttu-id="101c1-220">Criar o Application Gateway</span><span class="sxs-lookup"><span data-stu-id="101c1-220">Create the Application Gateway</span></span>

<span data-ttu-id="101c1-221">Usando todas as etapas anteriores, crie o Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="101c1-221">Using all the preceding steps, create the Application Gateway.</span></span> <span data-ttu-id="101c1-222">A criação do gateway é um processo de execução demorada.</span><span class="sxs-lookup"><span data-stu-id="101c1-222">The creation of the gateway is a long running process.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a><span data-ttu-id="101c1-223">Limitar as versões de protocolo SSL em um Gateway de Aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="101c1-223">Limit SSL protocol versions on an existing Application Gateway</span></span>

<span data-ttu-id="101c1-224">As etapas anteriores levam você a criar um aplicativo com ssl de ponta a ponta e a desabilitar determinadas versões do protocolo SSL.</span><span class="sxs-lookup"><span data-stu-id="101c1-224">The preceding steps take you through creating an application with end to end SSL and disabling certain SSL protocol versions.</span></span> <span data-ttu-id="101c1-225">O exemplo a seguir desabilita determinadas políticas de SSL em um gateway de aplicativo existente.</span><span class="sxs-lookup"><span data-stu-id="101c1-225">The following example disables certain SSL policies on an existing application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="101c1-226">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="101c1-226">Step 1</span></span>

<span data-ttu-id="101c1-227">Recupere o gateway de aplicativo para atualizar.</span><span class="sxs-lookup"><span data-stu-id="101c1-227">Retrieve the application gateway to update.</span></span>

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a><span data-ttu-id="101c1-228">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="101c1-228">Step 2</span></span>

<span data-ttu-id="101c1-229">Defina uma política de SSL.</span><span class="sxs-lookup"><span data-stu-id="101c1-229">Define an SSL policy.</span></span> <span data-ttu-id="101c1-230">No exemplo a seguir, TLSv1.0 e TLSv1.1 estão desabilitadas e os conjuntos de codificação **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, e **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** são os únicos permitidos.</span><span class="sxs-lookup"><span data-stu-id="101c1-230">In the following example, TLSv1.0 and TLSv1.1 are disabled and the cipher suites **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** are the only ones allowed.</span></span>

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a><span data-ttu-id="101c1-231">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="101c1-231">Step 3</span></span>

<span data-ttu-id="101c1-232">Por fim, atualize o gateway.</span><span class="sxs-lookup"><span data-stu-id="101c1-232">Finally, update the gateway.</span></span> <span data-ttu-id="101c1-233">É importante observar que essa última etapa é uma tarefa de execução demorada.</span><span class="sxs-lookup"><span data-stu-id="101c1-233">It is important to note that this last step is a long running task.</span></span> <span data-ttu-id="101c1-234">Quando estiver pronto, o SSL de ponta a ponta será configurado no gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="101c1-234">When it is done, end to end SSL is configured on the application gateway.</span></span>

```powershell
$gw | Set-AzureRmApplicationGateway
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="101c1-235">Obter um nome DNS de Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="101c1-235">Get application gateway DNS name</span></span>

<span data-ttu-id="101c1-236">Depois de criar o gateway, a próxima etapa será configurar o front-end para comunicação.</span><span class="sxs-lookup"><span data-stu-id="101c1-236">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="101c1-237">Ao usar um IP público, o gateway de aplicativo requer um nome DNS atribuído dinamicamente, o que não é amigável.</span><span class="sxs-lookup"><span data-stu-id="101c1-237">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="101c1-238">Para garantir que os usuários finais possam alcançar o gateway de aplicativo, um registro CNAME pode ser usado para apontar para o ponto de extremidade público do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="101c1-238">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="101c1-239">[Configurando um nome de domínio personalizado no Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="101c1-239">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="101c1-240">Para isso, recupere detalhes do Gateway de Aplicativo e seu nome DNS/IP associado usando o elemento PublicIPAddress anexado ao Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="101c1-240">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="101c1-241">O nome DNS do Gateway de Aplicativo deve ser usado para criar um registro CNAME que aponta os dois aplicativos Web para esse nome DNS.</span><span class="sxs-lookup"><span data-stu-id="101c1-241">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="101c1-242">O uso de registros A não é recomendável, pois o VIP pode mudar na reinicialização do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="101c1-242">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="101c1-243">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="101c1-243">Next steps</span></span>

<span data-ttu-id="101c1-244">Saiba mais sobre como otimizar a segurança dos seus aplicativos Web com o Firewall do Aplicativo Web por meio do Gateway de Aplicativo ao visitar [Visão geral do Firewall de Aplicativo Web](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="101c1-244">Learn about hardening the security of your web applications with Web Application Firewall through Application Gateway by visiting [Web Application Firewall Overview](application-gateway-webapplicationfirewall-overview.md)</span></span>

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
