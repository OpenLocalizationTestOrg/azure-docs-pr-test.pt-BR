---
title: Configurar o descarregamento SSL - Gateway de Aplicativo do Azure - PowerShell | Microsoft Docs
description: "Esta página fornece instruções para criar um gateway de aplicativo com descarregamento SSL usando o Gerenciador de Recursos do Azure"
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
ms.openlocfilehash: ededabc7c665d6bb05b91e4d21d01fb1379add32
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a><span data-ttu-id="864c9-103">Configurar um gateway de aplicativo para descarregamento SSL usando o Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="864c9-103">Configure an application gateway for SSL offload by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="864c9-104">portal do Azure</span><span class="sxs-lookup"><span data-stu-id="864c9-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="864c9-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="864c9-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="864c9-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="864c9-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="864c9-107">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="864c9-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="864c9-108">O Gateway de Aplicativo do Azure pode ser configurado para encerrar a sessão SSL no gateway para evitar que a onerosa tarefa de descriptografia de SSL aconteça no web farm.</span><span class="sxs-lookup"><span data-stu-id="864c9-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="864c9-109">O descarregamento SSL também simplifica a configuração do servidor front-end e o gerenciamento do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="864c9-109">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="864c9-110">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="864c9-110">Before you begin</span></span>

1. <span data-ttu-id="864c9-111">Instale a versão mais recente dos cmdlets do Azure PowerShell usando o Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="864c9-111">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="864c9-112">Você pode baixar e instalar a versão mais recente na seção **Windows PowerShell** da [página Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="864c9-112">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="864c9-113">Você cria uma rede virtual e uma sub-rede para o gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="864c9-113">You create a virtual network and a subnet for the application gateway.</span></span> <span data-ttu-id="864c9-114">Verifique se não há máquinas virtuais ou implantações em nuvem usando a sub-rede.</span><span class="sxs-lookup"><span data-stu-id="864c9-114">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="864c9-115">O Gateway de Aplicativo deve estar sozinho em uma sub-rede de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="864c9-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="864c9-116">Os servidores que você configura para usar o gateway de aplicativo devem existir ou ter seus pontos de extremidade criados na rede virtual ou com um IP/VIP público atribuído.</span><span class="sxs-lookup"><span data-stu-id="864c9-116">The servers you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="864c9-117">O que é necessário para criar um gateway de aplicativo?</span><span class="sxs-lookup"><span data-stu-id="864c9-117">What is required to create an application gateway?</span></span>

* <span data-ttu-id="864c9-118">**Pool de servidores back-end:** a lista de endereços IP dos servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="864c9-118">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="864c9-119">Os endereços IP listados devem pertencer à sub-rede da rede virtual ou devem ser um IP/VIP público.</span><span class="sxs-lookup"><span data-stu-id="864c9-119">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="864c9-120">**Configurações do pool de servidores back-end:** cada pool tem configurações como porta, protocolo e afinidade baseada em cookie.</span><span class="sxs-lookup"><span data-stu-id="864c9-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="864c9-121">Essas configurações são vinculadas a um pool e aplicadas a todos os servidores no pool.</span><span class="sxs-lookup"><span data-stu-id="864c9-121">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="864c9-122">**Porta front-end:** essa porta é a porta pública aberta no gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="864c9-122">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="864c9-123">O tráfego atinge essa porta e é redirecionado para um dos servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="864c9-123">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="864c9-124">**Ouvinte:** o ouvinte tem uma porta front-end, um protocolo (HTTP ou HTTPS; essas configurações diferenciam maiúsculas de minúsculas) e o nome do certificado SSL (se estiver configurando o descarregamento SSL).</span><span class="sxs-lookup"><span data-stu-id="864c9-124">**Listener:** The listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="864c9-125">**Regra:** a regra vincula o ouvinte e o pool de servidores back-end e define à qual pool de servidores back-end o tráfego deve ser direcionado quando atinge um ouvinte específico.</span><span class="sxs-lookup"><span data-stu-id="864c9-125">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="864c9-126">Atualmente, há suporte apenas para a regra *basic* .</span><span class="sxs-lookup"><span data-stu-id="864c9-126">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="864c9-127">A regra *básica* é a distribuição de carga round robin.</span><span class="sxs-lookup"><span data-stu-id="864c9-127">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="864c9-128">**Observações adicionais sobre a configuração**</span><span class="sxs-lookup"><span data-stu-id="864c9-128">**Additional configuration notes**</span></span>

<span data-ttu-id="864c9-129">Para a configuração de certificados SSL, o protocolo em **HttpListener** deve ser alterado para *Https* (diferencia maiúsculas de minúsculas).</span><span class="sxs-lookup"><span data-stu-id="864c9-129">For SSL certificates configuration, the protocol in **HttpListener** should change to *Https* (case sensitive).</span></span> <span data-ttu-id="864c9-130">O elemento **SslCertificate** é adicionado ao **HttpListener** com o valor da variável configurado para o certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="864c9-130">The **SslCertificate** element is added to **HttpListener** with the variable value configured for the SSL certificate.</span></span> <span data-ttu-id="864c9-131">A porta front-end deve ser atualizada para 443.</span><span class="sxs-lookup"><span data-stu-id="864c9-131">The front-end port should be updated to 443.</span></span>

<span data-ttu-id="864c9-132">**Para habilitar a afinidade baseada em cookie**: um gateway de aplicativo pode ser configurado para garantir que uma solicitação de uma sessão de cliente sempre seja direcionada para a mesma VM no web farm.</span><span class="sxs-lookup"><span data-stu-id="864c9-132">**To enable cookie-based affinity**: An application gateway can be configured to ensure that a request from a client session is always directed to the same VM in the web farm.</span></span> <span data-ttu-id="864c9-133">Este cenário é concluído pela injeção de um cookie de sessão que permite que o gateway redirecione o tráfego corretamente.</span><span class="sxs-lookup"><span data-stu-id="864c9-133">This scenario is done by injection of a session cookie that allows the gateway to direct traffic appropriately.</span></span> <span data-ttu-id="864c9-134">Para habilitar a afinidade baseada em cookie, defina **CookieBasedAffinity** como *Habilitado* no elemento **BackendHttpSettings**.</span><span class="sxs-lookup"><span data-stu-id="864c9-134">To enable cookie-based affinity, set **CookieBasedAffinity** to *Enabled* in the **BackendHttpSettings** element.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="864c9-135">Criar um Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="864c9-135">Create an application gateway</span></span>

<span data-ttu-id="864c9-136">A diferença entre usar o modelo de implantação Clássico do Azure e o Azure Resource Manager é a ordem em que você cria o gateway de aplicativo e os itens que precisam ser configurados.</span><span class="sxs-lookup"><span data-stu-id="864c9-136">The difference between using the Azure Classic deployment model and Azure Resource Manager is the order that you create an application gateway and the items that need to be configured.</span></span>

<span data-ttu-id="864c9-137">Com o Gerenciador de Recursos, todos os componentes de um gateway de aplicativo são configurados individualmente e reunidos para criar um recurso do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="864c9-137">With Resource Manager, all components of an application gateway are configured individually and then put together to create an application gateway resource.</span></span>

<span data-ttu-id="864c9-138">A seguir, as etapas necessárias para criar um gateway de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="864c9-138">Here are the steps needed to create an application gateway:</span></span>

1. <span data-ttu-id="864c9-139">Criar um grupo de recursos para o Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="864c9-139">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="864c9-140">Criar uma rede virtual, uma sub-rede e um IP público para o gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="864c9-140">Create virtual network, subnet, and public IP for the application gateway</span></span>
3. <span data-ttu-id="864c9-141">Criar um objeto de configuração do gateway do aplicativo</span><span class="sxs-lookup"><span data-stu-id="864c9-141">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="864c9-142">Criar um recurso do gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="864c9-142">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="864c9-143">Criar um grupo de recursos para o Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="864c9-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="864c9-144">Alterne para o modo PowerShell para usar os cmdlets do Gerenciador de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="864c9-144">Make sure that you switch PowerShell mode to use the Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="864c9-145">Mais informações estão disponíveis em [Usando o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="864c9-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="864c9-146">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="864c9-146">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="864c9-147">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="864c9-147">Step 2</span></span>

<span data-ttu-id="864c9-148">Verificar as assinaturas da conta.</span><span class="sxs-lookup"><span data-stu-id="864c9-148">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="864c9-149">Você deve se autenticar com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="864c9-149">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="864c9-150">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="864c9-150">Step 3</span></span>

<span data-ttu-id="864c9-151">Escolha quais das suas assinaturas do Azure deseja usar.</span><span class="sxs-lookup"><span data-stu-id="864c9-151">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="864c9-152">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="864c9-152">Step 4</span></span>

<span data-ttu-id="864c9-153">Crie um grupo de recursos (ignore esta etapa se você estiver usando um grupo de recursos existente).</span><span class="sxs-lookup"><span data-stu-id="864c9-153">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="864c9-154">O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local.</span><span class="sxs-lookup"><span data-stu-id="864c9-154">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="864c9-155">Essa configuração é usada como o local padrão para os recursos do grupo de recursos em questão.</span><span class="sxs-lookup"><span data-stu-id="864c9-155">This setting is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="864c9-156">Verifique se todos os comandos para criar um gateway de aplicativo usam o mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="864c9-156">Make sure that all commands to create an application gateway uses the same resource group.</span></span>

<span data-ttu-id="864c9-157">No exemplo anterior, criamos um grupo de recursos denominado **appgw-RG** e a localização **Oeste dos EUA**.</span><span class="sxs-lookup"><span data-stu-id="864c9-157">In the example above, we created a resource group called **appgw-RG** and location **West US**.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="864c9-158">Criar uma rede virtual e uma sub-rede para o gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="864c9-158">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="864c9-159">O exemplo a seguir mostra como criar uma rede virtual usando o Gerenciador de Recursos:</span><span class="sxs-lookup"><span data-stu-id="864c9-159">The following example shows how to create a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="864c9-160">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="864c9-160">Step 1</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="864c9-161">Esta amostra atribui o intervalo de endereços 10.0.0.0/24 a uma variável de sub-rede a ser usada para criar uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="864c9-161">This sample assigns the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="864c9-162">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="864c9-162">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

<span data-ttu-id="864c9-163">Esta amostra cria uma rede virtual chamada **appgwvnet** no grupo de recursos **appgw-rg** para a região Oeste dos EUA usando o prefixo 10.0.0.0/16 com a sub-rede 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="864c9-163">This sample creates a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="864c9-164">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="864c9-164">Step 3</span></span>

```powershell
$subnet = $vnet.Subnets[0]
```

<span data-ttu-id="864c9-165">Esta amostra atribui o objeto de sub-rede à variável $subnet para as próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="864c9-165">This sample assigns the subnet object to variable $subnet for the next steps.</span></span>

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="864c9-166">Criar um endereço IP público para a configuração de front-end</span><span class="sxs-lookup"><span data-stu-id="864c9-166">Create a public IP address for the front-end configuration</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="864c9-167">Esta amostra cria um recurso de IP público **publicIP01** no grupo de recursos **appgw-rg** para a região Oeste dos EUA.</span><span class="sxs-lookup"><span data-stu-id="864c9-167">This sample creates a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="864c9-168">Criar um objeto de configuração do gateway do aplicativo</span><span class="sxs-lookup"><span data-stu-id="864c9-168">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="864c9-169">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="864c9-169">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="864c9-170">Esta amostra cria uma configuração de IP do gateway de aplicativo chamada **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="864c9-170">This sample creates an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="864c9-171">Quando o Gateway de Aplicativo é iniciado, ele escolhe um endereço IP na sub-rede configurada e no tráfego de rede da rota para os endereços IP no pool de IPs de back-end.</span><span class="sxs-lookup"><span data-stu-id="864c9-171">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="864c9-172">Tenha em mente que cada instância usa um endereço IP.</span><span class="sxs-lookup"><span data-stu-id="864c9-172">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="864c9-173">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="864c9-173">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

<span data-ttu-id="864c9-174">Esta amostra configura o pool de endereços IP de back-end denominado **pool01** com os endereços IP **134.170.185.46**, **134.170.188.221**, **134.170.185.50**.</span><span class="sxs-lookup"><span data-stu-id="864c9-174">This sample configures the back-end IP address pool named **pool01** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50**.</span></span> <span data-ttu-id="864c9-175">Esses valores são os endereços IP que receberão o tráfego de rede proveniente do ponto de extremidade do IP de front-end.</span><span class="sxs-lookup"><span data-stu-id="864c9-175">Those values are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span></span> <span data-ttu-id="864c9-176">Substitua os endereços IP do exemplo anterior pelos endereços IP dos pontos de extremidade do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="864c9-176">Replace the IP addresses from the preceding example with the IP addresses of your web application endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="864c9-177">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="864c9-177">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

<span data-ttu-id="864c9-178">Esta amostra define a configuração **poolsetting01** do gateway de aplicativo para o tráfego de rede com carga balanceada no pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="864c9-178">This sample configures application gateway setting **poolsetting01** to load-balanced network traffic in the back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="864c9-179">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="864c9-179">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

<span data-ttu-id="864c9-180">Esta amostra configura a porta do IP de front-end denominada **frontendport01** para o ponto de extremidade do IP público.</span><span class="sxs-lookup"><span data-stu-id="864c9-180">This sample configures the front-end IP port named **frontendport01** for the public IP endpoint.</span></span>

### <a name="step-5"></a><span data-ttu-id="864c9-181">Etapa 5</span><span class="sxs-lookup"><span data-stu-id="864c9-181">Step 5</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

<span data-ttu-id="864c9-182">Esta amostra configura o certificado usado para a conexão SSL.</span><span class="sxs-lookup"><span data-stu-id="864c9-182">This sample configures the certificate used for SSL connection.</span></span> <span data-ttu-id="864c9-183">O certificado deve estar no formato .pfx e a senha deve ter entre 4 e 12 caracteres.</span><span class="sxs-lookup"><span data-stu-id="864c9-183">The certificate needs to be in .pfx format, and the password must be between 4 to 12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="864c9-184">Etapa 6</span><span class="sxs-lookup"><span data-stu-id="864c9-184">Step 6</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

<span data-ttu-id="864c9-185">Esta amostra cria a configuração de IP de front-end chamada **fipconfig01** e associa o endereço IP público à configuração de IP de front-end.</span><span class="sxs-lookup"><span data-stu-id="864c9-185">This sample creates the front-end IP configuration named **fipconfig01** and associates the public IP address with the front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="864c9-186">Etapa 7</span><span class="sxs-lookup"><span data-stu-id="864c9-186">Step 7</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

<span data-ttu-id="864c9-187">Esta amostra cria o ouvinte de nome **listener01** e associa a porta de front-end à configuração de IP e ao certificado do front-end.</span><span class="sxs-lookup"><span data-stu-id="864c9-187">This sample creates the listener name **listener01** and associates the front-end port to the front-end IP configuration and certificate.</span></span>

### <a name="step-8"></a><span data-ttu-id="864c9-188">Etapa 8</span><span class="sxs-lookup"><span data-stu-id="864c9-188">Step 8</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="864c9-189">Esta amostra cria a regra de roteamento do balanceador de carga chamada **rule01**, que configura o comportamento do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="864c9-189">This sample creates the load balancer routing rule named **rule01** that configures the load balancer behavior.</span></span>

### <a name="step-9"></a><span data-ttu-id="864c9-190">Etapa 9</span><span class="sxs-lookup"><span data-stu-id="864c9-190">Step 9</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="864c9-191">Esta amostra configura o tamanho da instância do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="864c9-191">This sample configures the instance size of the application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="864c9-192">O valor padrão para *InstanceCount* é 2, com um valor máximo de 10.</span><span class="sxs-lookup"><span data-stu-id="864c9-192">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="864c9-193">O valor padrão para *GatewaySize* é Medium.</span><span class="sxs-lookup"><span data-stu-id="864c9-193">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="864c9-194">Você pode escolher entre Standard_Small, Standard_Medium e Standard_Large.</span><span class="sxs-lookup"><span data-stu-id="864c9-194">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

### <a name="step-10"></a><span data-ttu-id="864c9-195">Etapa 10</span><span class="sxs-lookup"><span data-stu-id="864c9-195">Step 10</span></span>

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

<span data-ttu-id="864c9-196">Esta etapa define a política SSL para usar no gateway do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="864c9-196">This step defines the SSL policy to use on the application gateway.</span></span> <span data-ttu-id="864c9-197">Visite [versões de política de configurar SSL e conjuntos de codificação no Gateway de Aplicativo](application-gateway-configure-ssl-policy-powershell.md) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="864c9-197">Visit [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) to learn more.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="864c9-198">Criar um gateway de aplicativo usando New-AzureApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="864c9-198">Create an application gateway by using New-AzureApplicationGateway</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

<span data-ttu-id="864c9-199">Esta amostra cria um gateway de aplicativo com todos os itens de configuração das etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="864c9-199">This sample creates an application gateway with all configuration items from the preceding steps.</span></span> <span data-ttu-id="864c9-200">No exemplo, o gateway de aplicativo se chama **appgwtest**.</span><span class="sxs-lookup"><span data-stu-id="864c9-200">In the example, the application gateway is called **appgwtest**.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="864c9-201">Obter um nome DNS de Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="864c9-201">Get application gateway DNS name</span></span>

<span data-ttu-id="864c9-202">Depois de criar o gateway, a próxima etapa será configurar o front-end para comunicação.</span><span class="sxs-lookup"><span data-stu-id="864c9-202">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="864c9-203">Ao usar um IP público, o gateway de aplicativo requer um nome DNS atribuído dinamicamente, o que não é amigável.</span><span class="sxs-lookup"><span data-stu-id="864c9-203">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="864c9-204">Para garantir que os usuários finais possam alcançar o gateway de aplicativo, um registro CNAME pode ser usado para apontar para o ponto de extremidade público do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="864c9-204">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="864c9-205">[Configurando um nome de domínio personalizado no Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="864c9-205">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="864c9-206">Para isso, recupere detalhes do Gateway de Aplicativo e seu nome DNS/IP associado usando o elemento PublicIPAddress anexado ao Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="864c9-206">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="864c9-207">O nome DNS do Gateway de Aplicativo deve ser usado para criar um registro CNAME que aponta os dois aplicativos Web para esse nome DNS.</span><span class="sxs-lookup"><span data-stu-id="864c9-207">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="864c9-208">O uso de registros A não é recomendável, pois o VIP pode mudar na reinicialização do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="864c9-208">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>


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

## <a name="next-steps"></a><span data-ttu-id="864c9-209">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="864c9-209">Next steps</span></span>

<span data-ttu-id="864c9-210">Se desejar configurar um gateway de aplicativo para usar com um balanceador de carga interno (ILB), veja [Criar um gateway de aplicativo com um ILB (balanceador de carga interno)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="864c9-210">If you want to configure an application gateway to use with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="864c9-211">Se deseja obter mais informações sobre as opções de balanceamento de carga no geral, consulte:</span><span class="sxs-lookup"><span data-stu-id="864c9-211">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="864c9-212">Balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="864c9-212">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="864c9-213">Gerenciador de Tráfego do Azure</span><span class="sxs-lookup"><span data-stu-id="864c9-213">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

