---
title: aaaCreate regras de um gateway de aplicativo usando o roteamento de URL | Microsoft Docs
description: "Esta página fornece instruções toocreate, configure um gateway de aplicativo do Azure usando regras de roteamento de URL"
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
ms.openlocfilehash: 54fcccc39e48a933576968ce3d8160518c0d0b7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing"></a><span data-ttu-id="2c0d6-103">Criar um gateway de aplicativo usando roteamento com base em caminho</span><span class="sxs-lookup"><span data-stu-id="2c0d6-103">Create an application gateway using Path-based routing</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2c0d6-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2c0d6-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="2c0d6-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2c0d6-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="2c0d6-106">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="2c0d6-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="2c0d6-107">Roteamento baseado no caminho de URL permite que você tooassociate rotas com base no caminho de URL de saudação de uma solicitação Http.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-107">URL Path-based routing enables you tooassociate routes based on hello URL path of an Http request.</span></span> <span data-ttu-id="2c0d6-108">Ele verifica se há um pool de back-end de tooa rota configurado para a URL de saudação apresentado em Olá Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-108">It checks if there is a route tooa back-end pool configured for hello URL presented in hello Application Gateway.</span></span> <span data-ttu-id="2c0d6-109">Em seguida, envia Olá toohello de tráfego de rede definida pelo pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-109">It then sends hello network traffic toohello defined back-end pool.</span></span> <span data-ttu-id="2c0d6-110">Um uso comum para roteamento baseado em URL é equilibrar solicitações de tooload para pools de toodifferent de diferentes tipos de conteúdo do servidor de back-end.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-110">A common use for URL-based routing is tooload balance requests for different content types toodifferent back-end server pools.</span></span>

<span data-ttu-id="2c0d6-111">Roteamento baseado em URL apresenta um novo gateway de tooapplication do tipo de regra.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-111">URL-based routing introduces a new rule type tooapplication gateway.</span></span> <span data-ttu-id="2c0d6-112">O gateway de aplicativo tem dois tipos de regra: básica e PathBasedRouting.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-112">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="2c0d6-113">Tipo de regra básica fornece serviço de round-robin para Olá back-end pools ao PathBasedRouting distribuição de rodízio tooround Além disso, também leva padrão de caminho da URL de solicitação de saudação em consideração ao escolher o pool de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-113">Basic rule type provides round-robin service for hello back-end pools while PathBasedRouting in addition tooround robin distribution, also takes path pattern of hello request URL into account while choosing hello backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="2c0d6-114">Cenário</span><span class="sxs-lookup"><span data-stu-id="2c0d6-114">Scenario</span></span>

<span data-ttu-id="2c0d6-115">Em Olá exemplo a seguir, o Application Gateway está servindo tráfego para contoso.com com dois grupos de servidor back-end: pool de servidores de vídeo e pool de servidores de imagem.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-115">In hello following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: video server pool and image server pool.</span></span>

<span data-ttu-id="2c0d6-116">As solicitações de http://contoso.com/image * são roteadas pool de servidores tooimage (pool1) e http://contoso.com/video * são roteadas pool de servidores toovideo (pool2).</span><span class="sxs-lookup"><span data-stu-id="2c0d6-116">Requests for http://contoso.com/image* are routed tooimage server pool (pool1), and http://contoso.com/video* are routed toovideo server pool (pool2).</span></span> <span data-ttu-id="2c0d6-117">Se nenhum dos padrões de caminho Olá corresponder, um pool de servidores padrão (pool1) é selecionado.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-117">if none of hello path patterns match, a default server pool (pool1) is selected.</span></span>

![roteamento de url](./media/application-gateway-create-url-route-arm-ps/figure1.png)

## <a name="before-you-begin"></a><span data-ttu-id="2c0d6-119">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="2c0d6-119">Before you begin</span></span>

1. <span data-ttu-id="2c0d6-120">Instale a versão mais recente Olá Olá Azure de cmdlets do PowerShell usando Olá Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-120">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="2c0d6-121">Você pode baixar e instalar a versão mais recente de saudação do hello **do Windows PowerShell** seção Olá [página de Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="2c0d6-121">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="2c0d6-122">Você cria uma rede virtual e uma sub-rede para o Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-122">You create a virtual network and subnet for Application Gateway.</span></span> <span data-ttu-id="2c0d6-123">Certifique-se de que não há máquinas ou implantações de nuvem usando sub-rede hello.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-123">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="2c0d6-124">gateway de aplicativo Hello deve ser sozinho em uma sub-rede de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-124">hello application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="2c0d6-125">servidores de saudação adicionados gateway de aplicativo toohello pool de back-end toouse Olá deve existir ou tiveram seus pontos de extremidade criado na rede virtual hello ou com um IP público/VIP atribuído.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-125">hello servers added toohello back-end pool toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="2c0d6-126">O que é necessário toocreate um application gateway?</span><span class="sxs-lookup"><span data-stu-id="2c0d6-126">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="2c0d6-127">**Pool de servidores de back-end:** lista de saudação de endereços IP dos servidores de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-127">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="2c0d6-128">endereços IP Hello listado ou devem pertencer a sub-rede da rede virtual toohello ou devem ser um IP público/VIP.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-128">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="2c0d6-129">**Configurações do pool de servidores back-end:** cada pool tem configurações como porta, protocolo e afinidade baseada em cookie.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="2c0d6-130">Essas configurações são tooa empatado pool e são aplicados tooall servidores no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-130">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="2c0d6-131">**Porta de front-end:** essa porta é a porta pública de saudação que é aberta no gateway do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-131">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="2c0d6-132">Tráfego atinge essa porta e, em seguida, obtém redirecionado tooone de servidores de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-132">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="2c0d6-133">**Ouvinte:** ouvinte Olá tem uma porta de front-end, um protocolo (Http ou Https, esses valores diferenciam maiusculas de minúsculas) e o nome do certificado SSL de saudação (se a configuração de SSL de descarregamento).</span><span class="sxs-lookup"><span data-stu-id="2c0d6-133">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="2c0d6-134">**Regra:** regra Olá associa ouvinte hello, pool de saudação do servidor de back-end e define o tráfego de saudação do pool de servidor back-end deve ser direcionado toowhen que ele atinja um ouvinte específico.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-134">**Rule:** hello rule binds hello listener, hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="2c0d6-135">Criar um Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="2c0d6-135">Create an application gateway</span></span>

<span data-ttu-id="2c0d6-136">diferença de saudação entre usar clássico do Azure e o Azure Resource Manager é a ordem de saudação no qual criar gateway de aplicativo hello e itens de saudação que precisam toobe configurado.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-136">hello difference between using Azure Classic and Azure Resource Manager is hello order in which you create hello application gateway and hello items that need toobe configured.</span></span>

<span data-ttu-id="2c0d6-137">Com o Gerenciador de recursos, todos os itens que compõem um application gateway são configurados individualmente e, em seguida, juntar toocreate recurso de gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-137">With Resource Manager, all items that make an application gateway are configured individually and then put together toocreate hello application gateway resource.</span></span>

<span data-ttu-id="2c0d6-138">Aqui estão as etapas de saudação que são necessária toocreate um application gateway:</span><span class="sxs-lookup"><span data-stu-id="2c0d6-138">Here are hello steps that are needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="2c0d6-139">Criar um grupo de recursos para o Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="2c0d6-140">Crie uma rede virtual, sub-rede e IP público para o gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-140">Create a virtual network, subnet, and public IP for hello application gateway.</span></span>
3. <span data-ttu-id="2c0d6-141">Criar um objeto de configuração do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-141">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="2c0d6-142">Criar um recurso de gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-142">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="2c0d6-143">Criar um grupo de recursos para o Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="2c0d6-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="2c0d6-144">Certifique-se de que você estiver usando a versão mais recente de saudação do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-144">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="2c0d6-145">Há mais informações disponíveis em [Como usar o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="2c0d6-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="2c0d6-146">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="2c0d6-146">Step 1</span></span>

<span data-ttu-id="2c0d6-147">Faça logon no tooAzure</span><span class="sxs-lookup"><span data-stu-id="2c0d6-147">Log in tooAzure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="2c0d6-148">Você está tooauthenticate solicitado com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-148">You are prompted tooauthenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="2c0d6-149">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="2c0d6-149">Step 2</span></span>

<span data-ttu-id="2c0d6-150">Verificar as assinaturas de saudação para conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-150">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="2c0d6-151">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="2c0d6-151">Step 3</span></span>

<span data-ttu-id="2c0d6-152">Escolha qual toouse suas assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-152">Choose which of your Azure subscriptions toouse.</span></span> <BR>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="2c0d6-153">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="2c0d6-153">Step 4</span></span>

<span data-ttu-id="2c0d6-154">Crie um grupo de recursos (ignore esta etapa se você estiver usando um grupo de recursos existente).</span><span class="sxs-lookup"><span data-stu-id="2c0d6-154">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US"
```

<span data-ttu-id="2c0d6-155">Como alternativa, também é possível pode criar marcas para um grupo de recursos para o gateway de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="2c0d6-155">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway URL routing"} 
```

<span data-ttu-id="2c0d6-156">O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-156">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="2c0d6-157">Este grupo de recursos é usado como o local padrão de saudação para recursos desse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-157">This resource group is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="2c0d6-158">Certifique-se de que todos os comandos toocreate uma saudação de uso de gateway de aplicativo mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-158">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

<span data-ttu-id="2c0d6-159">O exemplo hello acima, criamos um grupo de recursos chamado "appgw-RG" e o local "Oeste US".</span><span class="sxs-lookup"><span data-stu-id="2c0d6-159">In hello example above, we created a resource group called "appgw-RG" and location "West US".</span></span>

> [!NOTE]
> <span data-ttu-id="2c0d6-160">Se você precisar tooconfigure uma investigação personalizada para o gateway de aplicativo, consulte [criar um gateway de aplicativos com testes personalizados usando o PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="2c0d6-160">If you need tooconfigure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="2c0d6-161">Confira [investigações personalizadas e monitoramento de integridade](application-gateway-probe-overview.md) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-161">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>
> 
> 

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="2c0d6-162">Criar uma rede virtual e uma sub-rede para o gateway de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="2c0d6-162">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="2c0d6-163">Olá mostrado no exemplo a seguir como toocreate uma rede virtual usando o Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-163">hello following example shows how toocreate a virtual network by using Resource Manager.</span></span> <span data-ttu-id="2c0d6-164">Este exemplo cria uma rede virtual para Olá Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-164">This example creates a VNET for hello Application Gateway.</span></span> <span data-ttu-id="2c0d6-165">Application Gateway requer seu próprio sub-rede, por esse motivo, sub-rede Olá criado para Olá Application Gateway é menor do que Olá espaço de endereço de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-165">Application Gateway requires its own subnet, for this reason hello subnet created for hello Application Gateway is smaller than hello VNET address space.</span></span> <span data-ttu-id="2c0d6-166">Isso permite que outros recursos, incluindo, mas não limitado tooweb servidores toobe configurado no hello mesmo VNET.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-166">This allows for other resources, including but not limited tooweb servers toobe configured in hello same VNET.</span></span>

### <a name="step-1"></a><span data-ttu-id="2c0d6-167">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="2c0d6-167">Step 1</span></span>

<span data-ttu-id="2c0d6-168">Atribua o intervalo de endereço Olá 10.0.0.0/24 toohello sub-rede toobe variável usada toocreate uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-168">Assign hello address range 10.0.0.0/24 toohello subnet variable toobe used toocreate a virtual network.</span></span>  <span data-ttu-id="2c0d6-169">Isso cria um objeto de configuração de sub-rede Olá para Olá Application Gateway, que é usada no exemplo a seguir hello.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-169">This creates hello subnet configuration object for hello Application Gateway, which is used in hello next example.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

### <a name="step-2"></a><span data-ttu-id="2c0d6-170">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="2c0d6-170">Step 2</span></span>

<span data-ttu-id="2c0d6-171">Criar uma rede virtual denominada **appgwvnet** no grupo de recursos **appgw rg** para a região do hello Oeste dos EUA com hello prefixo 10.0.0.0/16 10.0.0.0/24 sub-rede.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-171">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span> <span data-ttu-id="2c0d6-172">Isso conclui a configuração de saudação da saudação VNET com uma única sub-rede para Olá Application Gateway tooreside.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-172">This completes hello configuration of hello VNET with a single subnet for hello Application Gateway tooreside.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

### <a name="step-3"></a><span data-ttu-id="2c0d6-173">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="2c0d6-173">Step 3</span></span>

<span data-ttu-id="2c0d6-174">Atribuir a variável de sub-rede Olá para Olá próximas etapas, isso é passado toohello `New-AzureRMApplicationGateway` cmdlet em uma etapa futura.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-174">Assign hello subnet variable for hello next steps, this is passed toohello `New-AzureRMApplicationGateway` cmdlet in a future step.</span></span>

```powershell
$subnet=$vnet.Subnets[0]
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="2c0d6-175">Criar um endereço IP público para a configuração de front-end Olá</span><span class="sxs-lookup"><span data-stu-id="2c0d6-175">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="2c0d6-176">Criar um recurso IP público **publicIP01** no grupo de recursos **appgw rg** para região Oeste dos EUA de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-176">Create a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span> <span data-ttu-id="2c0d6-177">Gateway de aplicativo pode usar um endereço IP público, o endereço IP interno ou ambas as solicitações de tooreceive para balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-177">Application Gateway can use a public IP address, internal IP address or both tooreceive requests for load balancing.</span></span>  <span data-ttu-id="2c0d6-178">Este exemplo usa apenas um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-178">This example only uses a public IP address.</span></span> <span data-ttu-id="2c0d6-179">No hello exemplo a seguir, nenhum nome DNS é configurado para a criação de endereço IP público de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-179">In hello following example, no DNS name is configured for creating hello Public IP address.</span></span>  <span data-ttu-id="2c0d6-180">O Gateway de Aplicativo não dá suporte a nomes DNS personalizados em endereços IP públicos.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-180">Application Gateway does not support custom DNS names on public IP addresses.</span></span>  <span data-ttu-id="2c0d6-181">Se um nome personalizado é necessário para o ponto de extremidade público hello, um registro CNAME deve ser criado para nome DNS toopoint toohello gerado automaticamente para o endereço IP público de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-181">If a custom name is required for hello public endpoint, a CNAME record should be created toopoint toohello automatically generated DNS name for hello public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="2c0d6-182">Um endereço IP é atribuído gateway de aplicativo toohello quando Olá serviço é iniciado.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-182">An IP address is assigned toohello application gateway when hello service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="2c0d6-183">Criar uma configuração do gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="2c0d6-183">Create application gateway configuration</span></span>

<span data-ttu-id="2c0d6-184">Todos os itens de configuração devem ser configurados antes de criar o gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-184">All configuration items must be set up before creating hello application gateway.</span></span> <span data-ttu-id="2c0d6-185">Olá etapas a seguir criam Olá itens de configuração que são necessárias para um recurso do application gateway.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-185">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="2c0d6-186">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="2c0d6-186">Step 1</span></span>

<span data-ttu-id="2c0d6-187">Crie uma configuração de IP do gateway de aplicativo chamada **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-187">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="2c0d6-188">Quando Application Gateway iniciado, ele seleciona um endereço IP da sub-rede de saudação configurado e rotear os endereços IP de toohello de tráfego de rede no pool IP de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-188">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="2c0d6-189">Tenha em mente que cada instância usa um endereço IP.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-189">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

### <a name="step-2"></a><span data-ttu-id="2c0d6-190">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="2c0d6-190">Step 2</span></span>

<span data-ttu-id="2c0d6-191">Configurar as pool de endereços IP back-end Olá denominada **pool01** e **pool2** com endereços IP para **pool1** e **pool2**.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-191">Configure hello back-end IP address pool named **pool01** and **pool2** with IP addresses for **pool1** and **pool2**.</span></span> <span data-ttu-id="2c0d6-192">Esses endereços IP são endereços IP de saudação de recursos de saudação que estão hospedando Olá toobe de aplicativo de web protegido pelo gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-192">These IP addresses are hello IP addresses of hello resources that are hosting hello web application toobe protected by hello application gateway.</span></span> <span data-ttu-id="2c0d6-193">Esses membros do pool de back-end são todos os toobe validado Íntegro por testes sejam investigações básicas ou personalizadas investigações.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-193">These backend pool members are all validated toobe healthy by probes whether they are basic probes or custom probes.</span></span>  <span data-ttu-id="2c0d6-194">O tráfego é roteado, em seguida, toothem quando a solicitação chega no gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-194">Traffic is then routed toothem when requests come into hello application gateway.</span></span> <span data-ttu-id="2c0d6-195">Pools de back-end podem ser usados por várias regras no gateway de aplicativo hello, que significa que um pool de back-end pode ser usado para vários aplicativos web que residem em Olá mesmo host.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-195">Backend pools can be used by multiple rules within hello application gateway, which means one backend pool could be used for multiple web applications that reside on hello same host.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 134.170.186.47, 134.170.189.222, 134.170.186.51
```

<span data-ttu-id="2c0d6-196">Neste exemplo, há dois pools de back-end tooroute o tráfego com base no caminho de URL hello.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-196">In this example, there are two back-end pools tooroute network traffic based on hello URL path.</span></span> <span data-ttu-id="2c0d6-197">Um pool recebe o tráfego do caminho de URL "/video", e o outro pool recebe o tráfego do caminho "/image".</span><span class="sxs-lookup"><span data-stu-id="2c0d6-197">One pool receives traffic from URL path "/video" and other pool receive traffic from path "/image".</span></span> <span data-ttu-id="2c0d6-198">Substitua saudação anterior tooadd de endereços IP seus próprios pontos de extremidade do endereço IP do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-198">Replace hello preceding IP addresses tooadd your own application IP address endpoints.</span></span> 

### <a name="step-3"></a><span data-ttu-id="2c0d6-199">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="2c0d6-199">Step 3</span></span>

<span data-ttu-id="2c0d6-200">Definir configuração de gateway do aplicativo **poolsetting01** e **poolsetting02** Olá com balanceamento de carga de tráfego de rede no pool de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-200">Configure application gateway setting **poolsetting01** and **poolsetting02** for hello load-balanced network traffic in hello back-end pool.</span></span> <span data-ttu-id="2c0d6-201">Neste exemplo, você definir as configurações de pool de back-end diferente para pools de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-201">In this example, you configure different back-end pool settings for hello back-end pools.</span></span> <span data-ttu-id="2c0d6-202">Cada pool de back-end pode ter sua própria configuração de pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-202">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="2c0d6-203">Configurações de HTTP de back-end são usadas por membros do pool regras tooroute tráfego toohello correto de back-end.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-203">Backend HTTP settings are used by rules tooroute traffic toohello correct backend pool members.</span></span> <span data-ttu-id="2c0d6-204">Isso determina o protocolo de saudação e a porta que é usada ao enviar tráfego toohello membros do pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-204">This determines hello protocol and port that is used when sending traffic toohello backend pool members.</span></span> <span data-ttu-id="2c0d6-205">Sessões baseada em cookie também são determinadas pelas configurações de HTTP de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-205">Cookie-based sessions are also determined by hello backend HTTP settings.</span></span>  <span data-ttu-id="2c0d6-206">Se habilitada, a afinidade de sessão baseada em cookie envia tráfego toohello mesmo back-end como solicitações anteriores para cada pacote.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-206">If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="2c0d6-207">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="2c0d6-207">Step 4</span></span>

<span data-ttu-id="2c0d6-208">Configure Olá IP de front-end com o ponto de extremidade IP público.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-208">Configure hello front-end IP with public IP endpoint.</span></span> <span data-ttu-id="2c0d6-209">objeto de configuração de IP de front-end Olá é usado por uma saudação toorelate de ouvinte para fora de voltada para o endereço IP com o ouvinte de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-209">hello front-end IP configuration object is used by a listener toorelate hello outward facing IP address with hello listener.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="2c0d6-210">Etapa 5</span><span class="sxs-lookup"><span data-stu-id="2c0d6-210">Step 5</span></span>

<span data-ttu-id="2c0d6-211">Configure portas de front-end Olá para o application gateway.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-211">Configure hello front-end port for an application gateway.</span></span> <span data-ttu-id="2c0d6-212">objeto de configuração de porta de front-end de saudação é usado por um ouvinte toodefine qual porta Olá Application Gateway escuta para o tráfego no ouvinte Olá.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-212">hello front-end port configuration object is used by a listener toodefine what port hello Application Gateway listens for traffic on hello listener.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 80
```

### <a name="step-6"></a><span data-ttu-id="2c0d6-213">Etapa 6</span><span class="sxs-lookup"><span data-stu-id="2c0d6-213">Step 6</span></span>

<span data-ttu-id="2c0d6-214">Configure o ouvinte de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-214">Configure hello listener.</span></span> <span data-ttu-id="2c0d6-215">Esta etapa configura um ouvinte de Olá para o endereço IP público de saudação e a porta usada tooreceive tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-215">This step configures hello listener for hello public IP address and port used tooreceive incoming network traffic.</span></span> <span data-ttu-id="2c0d6-216">saudação de exemplo a seguir usa a configuração de IP de front-end de Olá configurado anteriormente, a configuração de porta de front-end e um protocolo (http ou https) e configura o ouvinte hello.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-216">hello following example takes hello previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures hello listener.</span></span> <span data-ttu-id="2c0d6-217">Neste exemplo, o ouvinte de saudação escuta tooHTTP tráfego na porta 80 no endereço IP público Olá criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-217">In this example, hello listener listens tooHTTP traffic on port 80 on hello public IP address that was created earlier.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Http -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01
```

### <a name="step-7"></a><span data-ttu-id="2c0d6-218">Etapa 7</span><span class="sxs-lookup"><span data-stu-id="2c0d6-218">Step 7</span></span>

<span data-ttu-id="2c0d6-219">Configure caminhos de regra de URL para pools de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-219">Configure URL rule paths for hello back-end pools.</span></span> <span data-ttu-id="2c0d6-220">Esta etapa configura o caminho relativo do hello usado pelo gateway de aplicativo e define Olá mapeamento entre o caminho da URL hello e pool de back-end de saudação que recebe o tráfego de entrada hello toohandle.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-220">This step configures hello relative path used by application gateway and defines hello mapping between hello URL path and hello back-end pool that is assigned toohandle hello incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2c0d6-221">Cada caminho deve começar com / e coloque-Olá somente um "\*" é permitido, está na extremidade hello.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-221">Each path must start with / and hello only place a "\*" is allowed, is at hello end.</span></span> <span data-ttu-id="2c0d6-222">Exemplos válidos são /xyz, /xyz* ou /xyz/*.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-222">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="2c0d6-223">Olá alimentada correspondente do caminho toohello de cadeia de caracteres não inclui qualquer texto após Olá primeiro "?" ou "#" e os caracteres não são permitidos.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-223">hello string fed toohello path matcher does not include any text after hello first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="2c0d6-224">Olá, exemplo a seguir cria duas regras: um para "imagem /" caminho de roteamento de tráfego tooback-end "pool1" e outra para "vídeo /" caminho de roteamento de tráfego tooback-end "pool2".</span><span class="sxs-lookup"><span data-stu-id="2c0d6-224">hello following example creates two rules: one for "/image/" path routing traffic tooback-end "pool1" and another one for "/video/" path routing traffic tooback-end "pool2."</span></span> <span data-ttu-id="2c0d6-225">Essas regras Certifique-se de que o tráfego para cada conjunto de urls é roteado toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-225">These rules ensure that traffic for each set of urls is routed toohello backend.</span></span> <span data-ttu-id="2c0d6-226">Por exemplo, http://contoso.com/image/figure1.jpg vai toopool1 e http://contoso.com/video/example.mp4 vai toopool2.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-226">For example, http://contoso.com/image/figure1.jpg goes toopool1 and http://contoso.com/video/example.mp4 goes toopool2.</span></span>

```powershell
$imagePathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule1" -Paths "/image/*" -BackendAddressPool $pool1 -BackendHttpSettings $poolSetting01

$videoPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule2" -Paths "/video/*" -BackendAddressPool $pool2 -BackendHttpSettings $poolSetting02
```

<span data-ttu-id="2c0d6-227">Se o caminho Olá não corresponde a qualquer uma das regras de caminho predefinido Olá, configuração de mapa de caminho de regra Olá também configura um pool de endereços de back-end do padrão.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-227">If hello path doesn't match any of hello pre-defined path rules, hello rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="2c0d6-228">Por exemplo, http://contoso.com/shoppingcart/test.html irá toopool1 conforme ele é definido como o pool padrão de saudação para tráfego não correspondente.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-228">For example, http://contoso.com/shoppingcart/test.html goes toopool1 as it is defined as hello default pool for unmatched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $videoPathRule, $imagePathRule -DefaultBackendAddressPool $pool1 -DefaultBackendHttpSettings $poolSetting02
```

### <a name="step-8"></a><span data-ttu-id="2c0d6-229">Etapa 8</span><span class="sxs-lookup"><span data-stu-id="2c0d6-229">Step 8</span></span>

<span data-ttu-id="2c0d6-230">Crie uma configuração de regra.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-230">Create a rule setting.</span></span> <span data-ttu-id="2c0d6-231">Esta etapa configura Olá application gateway toouse baseadas em caminhos roteamento de URL.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-231">This step configures hello application gateway toouse URL path-based routing.</span></span> <span data-ttu-id="2c0d6-232">Olá `$urlPathMap` variável definida em Olá etapa anterior é baseado no caminho regra de saudação de toocreate usado agora.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-232">hello `$urlPathMap` variable defined in hello earlier step is now used toocreate hello path-based rule.</span></span> <span data-ttu-id="2c0d6-233">Nesta etapa, associamos regra Olá com um ouvinte e mapeamento de caminho de url Olá criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-233">In this step, we associate hello rule with a listener and hello url path mapping created earlier.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-9"></a><span data-ttu-id="2c0d6-234">Etapa 9</span><span class="sxs-lookup"><span data-stu-id="2c0d6-234">Step 9</span></span>

<span data-ttu-id="2c0d6-235">Configure o número de saudação de instâncias e o tamanho para o gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-235">Configure hello number of instances and size for hello application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Small" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="2c0d6-236">Criar um Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="2c0d6-236">Create Application Gateway</span></span>

<span data-ttu-id="2c0d6-237">Crie um gateway de aplicativos com todos os objetos de configuração da saudação etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-237">Create an application gateway with all configuration objects from hello preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="2c0d6-238">Obter um nome DNS de Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="2c0d6-238">Get application gateway DNS name</span></span>

<span data-ttu-id="2c0d6-239">Depois de criar o gateway hello, Olá próxima etapa é tooconfigure Olá front-end para comunicação.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-239">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="2c0d6-240">Ao usar um IP público, o gateway de aplicativo requer um nome DNS atribuído dinamicamente, o que não é amigável.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-240">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="2c0d6-241">os usuários finais de tooensure pode pressionar o gateway de aplicativo hello, um registro CNAME pode ser usado toopoint toohello ponto de extremidade público do gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-241">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="2c0d6-242">[Configurando um nome de domínio personalizado no Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2c0d6-242">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="2c0d6-243">tooconfigure Olá front-end registro CNAME de IP, recuperar detalhes do gateway de aplicativo hello e seu nome de IP/DNS associado usando Olá PublicIPAddress elemento toohello anexado application gateway.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-243">tooconfigure hello frontend IP CNAME record, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="2c0d6-244">nome DNS do gateway do aplicativo Hello deve ser usado toocreate um registro CNAME.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-244">hello application gateway's DNS name should be used toocreate a CNAME record.</span></span> <span data-ttu-id="2c0d6-245">uso de saudação de registros de um não é recomendável porque Olá VIP pode ser alterado na reinicialização do application gateway.</span><span class="sxs-lookup"><span data-stu-id="2c0d6-245">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2c0d6-246">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2c0d6-246">Next steps</span></span>

<span data-ttu-id="2c0d6-247">Se você quiser toolearn descarregamento de SSL Secure Sockets Layer (), consulte [Configure um gateway de aplicativo para descarregamento SSL](application-gateway-ssl-arm.md).</span><span class="sxs-lookup"><span data-stu-id="2c0d6-247">If you want toolearn Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-arm.md).</span></span>

