---
title: Criar um gateway de aplicativo usando as regras de roteamento de URL | Microsoft Docs
description: "Esta página oferece instruções para criar, configurar um gateway de aplicativo do Azure usando as regras de roteamento de URL"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d141cfbb-320a-4fc9-9125-10001c6fa4cf
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: ba756d3262b9780c5701e69faad860ba32bba08b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-gateway-using-path-based-routing"></a><span data-ttu-id="77828-103">Criar um gateway de aplicativo usando roteamento com base em caminho</span><span class="sxs-lookup"><span data-stu-id="77828-103">Create an application gateway using Path-based routing</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="77828-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="77828-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="77828-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="77828-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="77828-106">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="77828-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="77828-107">O roteamento com base em caminho de URL permite que você associe rotas com base no caminho de URL de uma solicitação Http.</span><span class="sxs-lookup"><span data-stu-id="77828-107">URL Path-based routing enables you to associate routes based on the URL path of an Http request.</span></span> <span data-ttu-id="77828-108">Ele verifica se há uma rota para um pool de back-end configurado para a URL apresentada no Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77828-108">It checks if there is a route to a back-end pool configured for the URL presented in the Application Gateway.</span></span> <span data-ttu-id="77828-109">Em seguida, ele envia o tráfego de rede para o pool de back-end definido.</span><span class="sxs-lookup"><span data-stu-id="77828-109">It then sends the network traffic to the defined back-end pool.</span></span> <span data-ttu-id="77828-110">Um uso comum para o roteamento com base em URL é balancear a carga das solicitações para tipos de conteúdo diferentes para pools de servidores back-end diferentes.</span><span class="sxs-lookup"><span data-stu-id="77828-110">A common use for URL-based routing is to load balance requests for different content types to different back-end server pools.</span></span>

<span data-ttu-id="77828-111">O roteamento com base em URL apresenta um novo tipo de regra ao gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77828-111">URL-based routing introduces a new rule type to application gateway.</span></span> <span data-ttu-id="77828-112">O gateway de aplicativo tem dois tipos de regra: básica e PathBasedRouting.</span><span class="sxs-lookup"><span data-stu-id="77828-112">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="77828-113">O tipo de regra básica fornece o serviço de round robin para os pools de back-end, enquanto o PathBasedRouting também leva em consideração, além de distribuição round robin, o padrão de caminho da URL da solicitação ao escolher o pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="77828-113">Basic rule type provides round-robin service for the back-end pools while PathBasedRouting in addition to round robin distribution, also takes path pattern of the request URL into account while choosing the backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="77828-114">Cenário</span><span class="sxs-lookup"><span data-stu-id="77828-114">Scenario</span></span>

<span data-ttu-id="77828-115">No exemplo a seguir, o Gateway de Aplicativo está fornecendo o tráfego para contoso.com com dois pools de servidor back-end: o pool de servidores de vídeo e o pool de servidores de imagem.</span><span class="sxs-lookup"><span data-stu-id="77828-115">In the following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: video server pool and image server pool.</span></span>

<span data-ttu-id="77828-116">As solicitações de http://contoso.com/image* são roteadas para o pool de servidores de imagem (pool1) e as de http://contoso.com/video* são roteadas para o pool de servidores de vídeo (pool2).</span><span class="sxs-lookup"><span data-stu-id="77828-116">Requests for http://contoso.com/image* are routed to image server pool (pool1), and http://contoso.com/video* are routed to video server pool (pool2).</span></span> <span data-ttu-id="77828-117">Um pool de servidores padrão (pool1) será selecionado se nenhum dos padrões de caminho corresponderem.</span><span class="sxs-lookup"><span data-stu-id="77828-117">if none of the path patterns match, a default server pool (pool1) is selected.</span></span>

![roteamento de url](./media/application-gateway-create-url-route-arm-ps/figure1.png)

## <a name="before-you-begin"></a><span data-ttu-id="77828-119">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="77828-119">Before you begin</span></span>

1. <span data-ttu-id="77828-120">Instale a versão mais recente dos cmdlets do Azure PowerShell usando o Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="77828-120">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="77828-121">Você pode baixar e instalar a versão mais recente na seção **Windows PowerShell** da [página Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="77828-121">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="77828-122">Você cria uma rede virtual e uma sub-rede para o Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77828-122">You create a virtual network and subnet for Application Gateway.</span></span> <span data-ttu-id="77828-123">Verifique se não há máquinas virtuais ou implantações em nuvem usando a sub-rede.</span><span class="sxs-lookup"><span data-stu-id="77828-123">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="77828-124">O gateway de aplicativo deve estar sozinho em uma sub-rede de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="77828-124">The application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="77828-125">Os servidores adicionados ao pool de back-end a fim de usar o gateway de aplicativo deve existir ou ter seus pontos de extremidade na rede virtual ou com um IP/VIP público atribuído.</span><span class="sxs-lookup"><span data-stu-id="77828-125">The servers added to the back-end pool to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="77828-126">O que é necessário para criar um gateway de aplicativo?</span><span class="sxs-lookup"><span data-stu-id="77828-126">What is required to create an application gateway?</span></span>

* <span data-ttu-id="77828-127">**Pool de servidores back-end:** a lista de endereços IP dos servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="77828-127">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="77828-128">Os endereços IP listados devem pertencer à sub-rede da rede virtual ou devem ser um IP/VIP público.</span><span class="sxs-lookup"><span data-stu-id="77828-128">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="77828-129">**Configurações do pool de servidores back-end:** cada pool tem configurações como porta, protocolo e afinidade baseada em cookie.</span><span class="sxs-lookup"><span data-stu-id="77828-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="77828-130">Essas configurações são vinculadas a um pool e aplicadas a todos os servidores no pool.</span><span class="sxs-lookup"><span data-stu-id="77828-130">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="77828-131">**Porta front-end:** essa porta é a porta pública aberta no gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77828-131">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="77828-132">O tráfego atinge essa porta e é redirecionado para um dos servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="77828-132">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="77828-133">**Ouvinte:** o ouvinte tem uma porta front-end, um protocolo (HTTP ou HTTPS, esses valores diferenciam maiúsculas de minúsculas) e o nome do certificado SSL (caso esteja configurando o descarregamento SSL).</span><span class="sxs-lookup"><span data-stu-id="77828-133">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="77828-134">**Regra:** a regra vincula o ouvinte e o pool de servidores back-end e define a qual pool de servidores back-end o tráfego deve ser direcionado ao atingir um ouvinte específico.</span><span class="sxs-lookup"><span data-stu-id="77828-134">**Rule:** The rule binds the listener, the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="77828-135">Criar um Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="77828-135">Create an application gateway</span></span>

<span data-ttu-id="77828-136">A diferença entre usar o Azure Classic e o Azure Resource Manager é a ordem em que você cria o gateway de aplicativo e os itens que precisam ser configurados.</span><span class="sxs-lookup"><span data-stu-id="77828-136">The difference between using Azure Classic and Azure Resource Manager is the order in which you create the application gateway and the items that need to be configured.</span></span>

<span data-ttu-id="77828-137">Com o Gerenciador de Recursos, todos os itens que compõem um gateway de aplicativo serão configurados individualmente e, em seguida, reunidos para criar o recurso do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77828-137">With Resource Manager, all items that make an application gateway are configured individually and then put together to create the application gateway resource.</span></span>

<span data-ttu-id="77828-138">A seguir, as etapas necessárias para criar um gateway de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="77828-138">Here are the steps that are needed to create an application gateway:</span></span>

1. <span data-ttu-id="77828-139">Criar um grupo de recursos para o Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="77828-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="77828-140">Criar uma rede virtual, uma sub-rede e um IP público para o gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77828-140">Create a virtual network, subnet, and public IP for the application gateway.</span></span>
3. <span data-ttu-id="77828-141">Criar um objeto de configuração do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77828-141">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="77828-142">Criar um recurso de gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77828-142">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="77828-143">Criar um grupo de recursos para o Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="77828-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="77828-144">Use a versão mais recente do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="77828-144">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="77828-145">Há mais informações disponíveis em [Como usar o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="77828-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="77828-146">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="77828-146">Step 1</span></span>

<span data-ttu-id="77828-147">Fazer logon no Azure</span><span class="sxs-lookup"><span data-stu-id="77828-147">Log in to Azure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="77828-148">Você deve se autenticar com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="77828-148">You are prompted to authenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="77828-149">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="77828-149">Step 2</span></span>

<span data-ttu-id="77828-150">Verificar as assinaturas da conta.</span><span class="sxs-lookup"><span data-stu-id="77828-150">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="77828-151">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="77828-151">Step 3</span></span>

<span data-ttu-id="77828-152">Escolha quais das suas assinaturas do Azure deseja usar.</span><span class="sxs-lookup"><span data-stu-id="77828-152">Choose which of your Azure subscriptions to use.</span></span> <BR>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="77828-153">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="77828-153">Step 4</span></span>

<span data-ttu-id="77828-154">Crie um grupo de recursos (ignore esta etapa se você estiver usando um grupo de recursos existente).</span><span class="sxs-lookup"><span data-stu-id="77828-154">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US"
```

<span data-ttu-id="77828-155">Como alternativa, também é possível pode criar marcas para um grupo de recursos para o gateway de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="77828-155">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway URL routing"} 
```

<span data-ttu-id="77828-156">O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local.</span><span class="sxs-lookup"><span data-stu-id="77828-156">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="77828-157">Esse grupo de recursos é usado como o local padrão para os recursos do grupo de recursos em questão.</span><span class="sxs-lookup"><span data-stu-id="77828-157">This resource group is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="77828-158">Verifique se todos os comandos para criar um Gateway de Aplicativo usam o mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="77828-158">Make sure that all commands to create an application gateway use the same resource group.</span></span>

<span data-ttu-id="77828-159">No exemplo anterior, criamos um grupo de recursos denominado "appgw-RG" e o local "Oeste dos EUA".</span><span class="sxs-lookup"><span data-stu-id="77828-159">In the example above, we created a resource group called "appgw-RG" and location "West US".</span></span>

> [!NOTE]
> <span data-ttu-id="77828-160">Se você precisar configurar uma investigação personalizada para o gateway de aplicativo, veja [Criar um gateway de aplicativo com investigações personalizadas usando o PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="77828-160">If you need to configure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="77828-161">Confira [investigações personalizadas e monitoramento de integridade](application-gateway-probe-overview.md) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="77828-161">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>
> 
> 

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="77828-162">Criar uma rede virtual e uma sub-rede para o gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="77828-162">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="77828-163">O exemplo a seguir mostra como criar uma rede virtual usando o Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="77828-163">The following example shows how to create a virtual network by using Resource Manager.</span></span> <span data-ttu-id="77828-164">Este exemplo cria uma VNET para o Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77828-164">This example creates a VNET for the Application Gateway.</span></span> <span data-ttu-id="77828-165">O Gateway de Aplicativo requer sua própria sub-rede e é por esse motivo que a sub-rede criada para o Gateway de Aplicativo é menor do que o espaço de endereço da VNET.</span><span class="sxs-lookup"><span data-stu-id="77828-165">Application Gateway requires its own subnet, for this reason the subnet created for the Application Gateway is smaller than the VNET address space.</span></span> <span data-ttu-id="77828-166">Isso permite outros recursos, incluindo, dentre outras coisas, que servidores Web sejam configurados na mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="77828-166">This allows for other resources, including but not limited to web servers to be configured in the same VNET.</span></span>

### <a name="step-1"></a><span data-ttu-id="77828-167">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="77828-167">Step 1</span></span>

<span data-ttu-id="77828-168">Atribua o intervalo de endereços 10.0.0.0/24 à variável de sub-rede a ser usada para criar uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="77828-168">Assign the address range 10.0.0.0/24 to the subnet variable to be used to create a virtual network.</span></span>  <span data-ttu-id="77828-169">Isso cria o objeto de configuração de sub-rede para o Gateway de Aplicativo que é usado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="77828-169">This creates the subnet configuration object for the Application Gateway, which is used in the next example.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

### <a name="step-2"></a><span data-ttu-id="77828-170">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="77828-170">Step 2</span></span>

<span data-ttu-id="77828-171">Crie uma rede virtual chamada **appgwvnet** no grupo de recursos **appgw-rg** para a região Oeste dos EUA usando o prefixo 10.0.0.0/16 com a sub-rede 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="77828-171">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span> <span data-ttu-id="77828-172">Isso conclui a configuração da rede virtual com uma única sub-rede em que o Gateway de Aplicativo deve residir.</span><span class="sxs-lookup"><span data-stu-id="77828-172">This completes the configuration of the VNET with a single subnet for the Application Gateway to reside.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

### <a name="step-3"></a><span data-ttu-id="77828-173">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="77828-173">Step 3</span></span>

<span data-ttu-id="77828-174">Atribua a variável de sub-rede para as próximas etapas, a qual será passada para o cmdlet `New-AzureRMApplicationGateway` em uma etapa futura.</span><span class="sxs-lookup"><span data-stu-id="77828-174">Assign the subnet variable for the next steps, this is passed to the `New-AzureRMApplicationGateway` cmdlet in a future step.</span></span>

```powershell
$subnet=$vnet.Subnets[0]
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="77828-175">Criar um endereço IP público para a configuração de front-end</span><span class="sxs-lookup"><span data-stu-id="77828-175">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="77828-176">Crie um recurso IP público **publicIP01** no grupo de recursos **appgw-rg** para a região Oeste dos EUA.</span><span class="sxs-lookup"><span data-stu-id="77828-176">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span> <span data-ttu-id="77828-177">O Gateway de Aplicativo pode usar um endereço IP público, interno ou de ambos os tipos para receber solicitações de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="77828-177">Application Gateway can use a public IP address, internal IP address or both to receive requests for load balancing.</span></span>  <span data-ttu-id="77828-178">Este exemplo usa apenas um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="77828-178">This example only uses a public IP address.</span></span> <span data-ttu-id="77828-179">No exemplo a seguir, nenhum nome DNS é configurado para criar o endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="77828-179">In the following example, no DNS name is configured for creating the Public IP address.</span></span>  <span data-ttu-id="77828-180">O Gateway de Aplicativo não dá suporte a nomes DNS personalizados em endereços IP públicos.</span><span class="sxs-lookup"><span data-stu-id="77828-180">Application Gateway does not support custom DNS names on public IP addresses.</span></span>  <span data-ttu-id="77828-181">Se um nome personalizado for exigido para o ponto de extremidade público, um registro CNAME deve ser criado a fim de apontar para o nome DNS gerado automaticamente para o endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="77828-181">If a custom name is required for the public endpoint, a CNAME record should be created to point to the automatically generated DNS name for the public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="77828-182">Um endereço IP é atribuído ao gateway de aplicativo quando o serviço é iniciado.</span><span class="sxs-lookup"><span data-stu-id="77828-182">An IP address is assigned to the application gateway when the service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="77828-183">Criar uma configuração do gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="77828-183">Create application gateway configuration</span></span>

<span data-ttu-id="77828-184">Todos os itens de configuração devem estar configurados antes de criar o gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77828-184">All configuration items must be set up before creating the application gateway.</span></span> <span data-ttu-id="77828-185">As etapas a seguir criam os itens de configuração necessários para um recurso de gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77828-185">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="77828-186">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="77828-186">Step 1</span></span>

<span data-ttu-id="77828-187">Crie uma configuração de IP do gateway de aplicativo chamada **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="77828-187">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="77828-188">Quando o Gateway de Aplicativo é iniciado, ele escolhe um endereço IP na sub-rede configurada e no tráfego de rede da rota para os endereços IP no pool de IPs de back-end.</span><span class="sxs-lookup"><span data-stu-id="77828-188">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="77828-189">Tenha em mente que cada instância usa um endereço IP.</span><span class="sxs-lookup"><span data-stu-id="77828-189">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

### <a name="step-2"></a><span data-ttu-id="77828-190">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="77828-190">Step 2</span></span>

<span data-ttu-id="77828-191">Configure o pool de endereços IP de back-end denominado **pool01** e **pool2** com os endereços IP para o **pool1** e **pool2**.</span><span class="sxs-lookup"><span data-stu-id="77828-191">Configure the back-end IP address pool named **pool01** and **pool2** with IP addresses for **pool1** and **pool2**.</span></span> <span data-ttu-id="77828-192">Esses endereços IP são os endereços IP dos recursos que estão hospedando o aplicativo Web que será protegido pelo Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77828-192">These IP addresses are the IP addresses of the resources that are hosting the web application to be protected by the application gateway.</span></span> <span data-ttu-id="77828-193">A integridade desses membros do pool de back-end é validada por investigações, sejam básicas ou personalizadas.</span><span class="sxs-lookup"><span data-stu-id="77828-193">These backend pool members are all validated to be healthy by probes whether they are basic probes or custom probes.</span></span>  <span data-ttu-id="77828-194">O tráfego é encaminhado para eles quando a solicitação chega no gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77828-194">Traffic is then routed to them when requests come into the application gateway.</span></span> <span data-ttu-id="77828-195">Os pools de back-end podem ser usados por várias regras dentro do gateway de aplicativo, o que significa que um pool de back-end pode ser usado para vários aplicativos Web que residem no mesmo host.</span><span class="sxs-lookup"><span data-stu-id="77828-195">Backend pools can be used by multiple rules within the application gateway, which means one backend pool could be used for multiple web applications that reside on the same host.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 134.170.186.47, 134.170.189.222, 134.170.186.51
```

<span data-ttu-id="77828-196">Neste exemplo, haverá dois pools de back-end para rotear o tráfego de rede com base no caminho da URL.</span><span class="sxs-lookup"><span data-stu-id="77828-196">In this example, there are two back-end pools to route network traffic based on the URL path.</span></span> <span data-ttu-id="77828-197">Um pool recebe o tráfego do caminho de URL "/video", e o outro pool recebe o tráfego do caminho "/image".</span><span class="sxs-lookup"><span data-stu-id="77828-197">One pool receives traffic from URL path "/video" and other pool receive traffic from path "/image".</span></span> <span data-ttu-id="77828-198">Substitua os endereços IP anteriores para adicionar seus próprios pontos de extremidade de endereço IP do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77828-198">Replace the preceding IP addresses to add your own application IP address endpoints.</span></span> 

### <a name="step-3"></a><span data-ttu-id="77828-199">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="77828-199">Step 3</span></span>

<span data-ttu-id="77828-200">Defina as configurações de **poolsetting01** e **poolsetting02** do gateway de aplicativo para o tráfego de rede com carga balanceada no pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="77828-200">Configure application gateway setting **poolsetting01** and **poolsetting02** for the load-balanced network traffic in the back-end pool.</span></span> <span data-ttu-id="77828-201">Neste exemplo, defina as configurações diferentes de pool de back-end para os pools de back-end.</span><span class="sxs-lookup"><span data-stu-id="77828-201">In this example, you configure different back-end pool settings for the back-end pools.</span></span> <span data-ttu-id="77828-202">Cada pool de back-end pode ter sua própria configuração de pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="77828-202">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="77828-203">As configurações HTTP de back-end são usadas pelas regras para rotear o tráfego para os membros do pool de back-end corretos.</span><span class="sxs-lookup"><span data-stu-id="77828-203">Backend HTTP settings are used by rules to route traffic to the correct backend pool members.</span></span> <span data-ttu-id="77828-204">Isso determina o protocolo e a porta usados ao enviar tráfego para os membros do pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="77828-204">This determines the protocol and port that is used when sending traffic to the backend pool members.</span></span> <span data-ttu-id="77828-205">As sessões baseadas em cookies também são determinadas pelas configurações HTTP de back-end.</span><span class="sxs-lookup"><span data-stu-id="77828-205">Cookie-based sessions are also determined by the backend HTTP settings.</span></span>  <span data-ttu-id="77828-206">Se habilitada, a afinidade de sessão baseada em cookies envia o tráfego para o mesmo back-end das solicitações anteriores para cada pacote.</span><span class="sxs-lookup"><span data-stu-id="77828-206">If enabled, cookie-based session affinity sends traffic to the same backend as previous requests for each packet.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="77828-207">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="77828-207">Step 4</span></span>

<span data-ttu-id="77828-208">Configure o IP front-end com o ponto de extremidade IP público.</span><span class="sxs-lookup"><span data-stu-id="77828-208">Configure the front-end IP with public IP endpoint.</span></span> <span data-ttu-id="77828-209">O objeto de configuração de IP front-end é usado por um ouvinte para relacionar o endereço IP voltado para fora com o ouvinte.</span><span class="sxs-lookup"><span data-stu-id="77828-209">The front-end IP configuration object is used by a listener to relate the outward facing IP address with the listener.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="77828-210">Etapa 5</span><span class="sxs-lookup"><span data-stu-id="77828-210">Step 5</span></span>

<span data-ttu-id="77828-211">Configure a porta front-end para um gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77828-211">Configure the front-end port for an application gateway.</span></span> <span data-ttu-id="77828-212">O objeto de configuração de porta front-end é usado por um ouvinte para definir a porta cujo tráfego deve ser ouvido pelo Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77828-212">The front-end port configuration object is used by a listener to define what port the Application Gateway listens for traffic on the listener.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 80
```

### <a name="step-6"></a><span data-ttu-id="77828-213">Etapa 6</span><span class="sxs-lookup"><span data-stu-id="77828-213">Step 6</span></span>

<span data-ttu-id="77828-214">Crie o ouvinte.</span><span class="sxs-lookup"><span data-stu-id="77828-214">Configure the listener.</span></span> <span data-ttu-id="77828-215">Esta etapa configura o ouvinte para o endereço IP público, e a porta usada para receber o tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="77828-215">This step configures the listener for the public IP address and port used to receive incoming network traffic.</span></span> <span data-ttu-id="77828-216">O exemplo a seguir usa a configuração de IP de front-end definida anteriormente, uma configuração de porta front-end e um protocolo (http ou https) e configura o ouvinte.</span><span class="sxs-lookup"><span data-stu-id="77828-216">The following example takes the previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures the listener.</span></span> <span data-ttu-id="77828-217">Neste exemplo, o ouvinte ouve o tráfego HTTP na porta 80 no endereço IP público que foi criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="77828-217">In this example, the listener listens to HTTP traffic on port 80 on the public IP address that was created earlier.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Http -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01
```

### <a name="step-7"></a><span data-ttu-id="77828-218">Etapa 7</span><span class="sxs-lookup"><span data-stu-id="77828-218">Step 7</span></span>

<span data-ttu-id="77828-219">Configure os caminhos de regra de URL para os pools de back-end.</span><span class="sxs-lookup"><span data-stu-id="77828-219">Configure URL rule paths for the back-end pools.</span></span> <span data-ttu-id="77828-220">Esta etapa configura o caminho relativo usado pelo Gateway de Aplicativo e define o mapeamento entre o caminho da URL e o pool de back-end que será atribuído para lidar com o tráfego de entrada.</span><span class="sxs-lookup"><span data-stu-id="77828-220">This step configures the relative path used by application gateway and defines the mapping between the URL path and the back-end pool that is assigned to handle the incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77828-221">Cada caminho deve começar com /, sendo que o único lugar no qual um "\*" é permitido é no final.</span><span class="sxs-lookup"><span data-stu-id="77828-221">Each path must start with / and the only place a "\*" is allowed, is at the end.</span></span> <span data-ttu-id="77828-222">Exemplos válidos são /xyz, /xyz* ou /xyz/*.</span><span class="sxs-lookup"><span data-stu-id="77828-222">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="77828-223">A cadeia de caracteres inserida no correspondente de caminho não inclui qualquer texto após o primeiro “?” ou “#”, e esses caracteres não são permitidos.</span><span class="sxs-lookup"><span data-stu-id="77828-223">The string fed to the path matcher does not include any text after the first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="77828-224">O exemplo a seguir cria duas regras: uma para o tráfego do caminho de roteamento "/imagem/" para o back-end "pool1" e outra para o tráfego do caminho de roteamento "/video/" para o back-end "pool2".</span><span class="sxs-lookup"><span data-stu-id="77828-224">The following example creates two rules: one for "/image/" path routing traffic to back-end "pool1" and another one for "/video/" path routing traffic to back-end "pool2."</span></span> <span data-ttu-id="77828-225">Essas regras garantem que o tráfego para cada conjunto de URLs seja roteado para o back-end.</span><span class="sxs-lookup"><span data-stu-id="77828-225">These rules ensure that traffic for each set of urls is routed to the backend.</span></span> <span data-ttu-id="77828-226">Por exemplo, http://contoso.com/image/figure1.jpg vai para o pool1 e http://contoso.com/video/example.mp4 vai para o pool2.</span><span class="sxs-lookup"><span data-stu-id="77828-226">For example, http://contoso.com/image/figure1.jpg goes to pool1 and http://contoso.com/video/example.mp4 goes to pool2.</span></span>

```powershell
$imagePathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule1" -Paths "/image/*" -BackendAddressPool $pool1 -BackendHttpSettings $poolSetting01

$videoPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule2" -Paths "/video/*" -BackendAddressPool $pool2 -BackendHttpSettings $poolSetting02
```

<span data-ttu-id="77828-227">A configuração de mapa do caminho de regra também configurará um pool de endereços de back-end padrão se o caminho não corresponder a nenhuma das regras de caminho predefinidas.</span><span class="sxs-lookup"><span data-stu-id="77828-227">If the path doesn't match any of the pre-defined path rules, the rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="77828-228">Por exemplo, http://contoso.com/shoppingcart/test.html vai para o pool1, já que ele está definido como o pool padrão para tráfego sem correspondência.</span><span class="sxs-lookup"><span data-stu-id="77828-228">For example, http://contoso.com/shoppingcart/test.html goes to pool1 as it is defined as the default pool for unmatched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $videoPathRule, $imagePathRule -DefaultBackendAddressPool $pool1 -DefaultBackendHttpSettings $poolSetting02
```

### <a name="step-8"></a><span data-ttu-id="77828-229">Etapa 8</span><span class="sxs-lookup"><span data-stu-id="77828-229">Step 8</span></span>

<span data-ttu-id="77828-230">Crie uma configuração de regra.</span><span class="sxs-lookup"><span data-stu-id="77828-230">Create a rule setting.</span></span> <span data-ttu-id="77828-231">Esta etapa configura o gateway de aplicativo a fim de usar o roteamento de com base no caminho de URL.</span><span class="sxs-lookup"><span data-stu-id="77828-231">This step configures the application gateway to use URL path-based routing.</span></span> <span data-ttu-id="77828-232">A variável `$urlPathMap` definida na etapa anterior é usada agora para criar a regra com base no caminho.</span><span class="sxs-lookup"><span data-stu-id="77828-232">The `$urlPathMap` variable defined in the earlier step is now used to create the path-based rule.</span></span> <span data-ttu-id="77828-233">Nesta etapa, associe a regra com um ouvinte e o mapeamento de caminho de URL criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="77828-233">In this step, we associate the rule with a listener and the url path mapping created earlier.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-9"></a><span data-ttu-id="77828-234">Etapa 9</span><span class="sxs-lookup"><span data-stu-id="77828-234">Step 9</span></span>

<span data-ttu-id="77828-235">Configure o número de instâncias e o tamanho do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77828-235">Configure the number of instances and size for the application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Small" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="77828-236">Criar um Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="77828-236">Create Application Gateway</span></span>

<span data-ttu-id="77828-237">Crie um gateway de aplicativo com todos os objetos de configuração das etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="77828-237">Create an application gateway with all configuration objects from the preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="77828-238">Obter um nome DNS de Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="77828-238">Get application gateway DNS name</span></span>

<span data-ttu-id="77828-239">Depois de criar o gateway, a próxima etapa será configurar o front-end para comunicação.</span><span class="sxs-lookup"><span data-stu-id="77828-239">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="77828-240">Ao usar um IP público, o gateway de aplicativo requer um nome DNS atribuído dinamicamente, o que não é amigável.</span><span class="sxs-lookup"><span data-stu-id="77828-240">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="77828-241">Para garantir que os usuários finais possam alcançar o gateway de aplicativo, um registro CNAME pode ser usado para apontar para o ponto de extremidade público do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77828-241">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="77828-242">[Configurando um nome de domínio personalizado no Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="77828-242">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="77828-243">Para configurar o registro CNAME de IP de front-end, recupere detalhes do Gateway de Aplicativo e seu nome DNS/IP associado usando o elemento PublicIPAddress anexado ao Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77828-243">To configure the frontend IP CNAME record, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="77828-244">O nome DNS do Gateway de Aplicativo deve ser usado para criar um registro CNAME.</span><span class="sxs-lookup"><span data-stu-id="77828-244">The application gateway's DNS name should be used to create a CNAME record.</span></span> <span data-ttu-id="77828-245">O uso de registros A não é recomendável, pois o VIP pode mudar na reinicialização do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77828-245">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="77828-246">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="77828-246">Next steps</span></span>

<span data-ttu-id="77828-247">Se você quiser aprender sobre o descarregamento de protocolo SSL, consulte [Configurar um Gateway de Aplicativo para o descarregamento SSL](application-gateway-ssl-arm.md).</span><span class="sxs-lookup"><span data-stu-id="77828-247">If you want to learn Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-arm.md).</span></span>

