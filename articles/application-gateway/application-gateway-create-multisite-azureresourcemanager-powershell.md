---
title: "aaaCreate um application gateway para hospedar vários sites | Microsoft Docs"
description: "Esta página fornece instruções toocreate, configure um gateway de aplicativo do Azure para hospedar vários aplicativos web em Olá mesmo gateway."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: b107d647-c9be-499f-8b55-809c4310c783
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/12/2016
ms.author: amsriva
ms.openlocfilehash: bad9a76be0a73a7026a770630fa7156f6e5940c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="bf773-103">Criar um gateway de aplicativo para hospedar vários aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="bf773-103">Create an application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bf773-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bf773-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="bf773-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bf773-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)

<span data-ttu-id="bf773-106">Várias opções de hospedagem de site permite que você toodeploy mais de um aplicativo web em Olá mesmo gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bf773-106">Multiple site hosting allows you toodeploy more than one web application on hello same application gateway.</span></span> <span data-ttu-id="bf773-107">Ele depende da presença do cabeçalho de host na solicitação HTTP entrada hello, toodetermine o ouvinte deve receber tráfego.</span><span class="sxs-lookup"><span data-stu-id="bf773-107">It relies on presence of host header in hello incoming HTTP request, toodetermine which listener would receive traffic.</span></span> <span data-ttu-id="bf773-108">ouvinte de Hello, em seguida, direciona o pool de back-end do tráfego tooappropriate conforme configurado na definição de regras de saudação do gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf773-108">hello listener then directs traffic tooappropriate backend pool as configured in hello rules definition of hello gateway.</span></span> <span data-ttu-id="bf773-109">Em aplicativos da web SSL habilitado, o gateway de aplicativo depende Olá indicação de nome de servidor (SNI) extensão toochoose Olá correto ouvinte para o tráfego da web hello.</span><span class="sxs-lookup"><span data-stu-id="bf773-109">In SSL enabled web applications, application gateway relies on hello Server Name Indication (SNI) extension toochoose hello correct listener for hello web traffic.</span></span> <span data-ttu-id="bf773-110">Um uso comum para várias opções de hospedagem de site é equilibrar solicitações de tooload para pools de servidor back-end da web diferentes domínios toodifferent.</span><span class="sxs-lookup"><span data-stu-id="bf773-110">A common use for multiple site hosting is tooload balance requests for different web domains toodifferent back-end server pools.</span></span> <span data-ttu-id="bf773-111">Da mesma forma diversos subdomínios de saudação mesmo domínio raiz também pode ser hospedado em Olá mesmo gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bf773-111">Similarly multiple subdomains of hello same root domain could also be hosted on hello same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="bf773-112">Cenário</span><span class="sxs-lookup"><span data-stu-id="bf773-112">Scenario</span></span>

<span data-ttu-id="bf773-113">Em Olá exemplo a seguir, o gateway de aplicativo está servindo tráfego para contoso.com e fabrikam.com com dois grupos de servidor back-end: contoso pool de servidores e pool de servidores da fabrikam.</span><span class="sxs-lookup"><span data-stu-id="bf773-113">In hello following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="bf773-114">Configuração semelhante pode ser usado toohost subdomínios como app.contoso.com e blog.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="bf773-114">Similar setup could be used toohost subdomains like app.contoso.com and blog.contoso.com.</span></span>

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a><span data-ttu-id="bf773-116">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="bf773-116">Before you begin</span></span>

1. <span data-ttu-id="bf773-117">Instale a versão mais recente Olá Olá Azure de cmdlets do PowerShell usando Olá Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="bf773-117">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="bf773-118">Você pode baixar e instalar a versão mais recente de saudação do hello **do Windows PowerShell** seção Olá [página de Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="bf773-118">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="bf773-119">servidores de saudação adicionados gateway de aplicativo toohello pool de back-end toouse Olá deve existir ou tiveram seus pontos de extremidade criado na rede virtual de saudação em uma sub-rede separada ou com um IP público/VIP atribuído.</span><span class="sxs-lookup"><span data-stu-id="bf773-119">hello servers added toohello back-end pool toouse hello application gateway must exist or have their endpoints created either in hello virtual network in a separate subnet or with a public IP/VIP assigned.</span></span>

## <a name="requirements"></a><span data-ttu-id="bf773-120">Requisitos</span><span class="sxs-lookup"><span data-stu-id="bf773-120">Requirements</span></span>

* <span data-ttu-id="bf773-121">**Pool de servidores de back-end:** lista de saudação de endereços IP dos servidores de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf773-121">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="bf773-122">endereços IP Hello listado ou devem pertencer a sub-rede da rede virtual toohello ou devem ser um IP público/VIP.</span><span class="sxs-lookup"><span data-stu-id="bf773-122">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="bf773-123">O FQDN também pode ser usado.</span><span class="sxs-lookup"><span data-stu-id="bf773-123">FQDN can also be used.</span></span>
* <span data-ttu-id="bf773-124">**Configurações do pool de servidores back-end:** cada pool tem configurações como porta, protocolo e afinidade baseada em cookie.</span><span class="sxs-lookup"><span data-stu-id="bf773-124">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="bf773-125">Essas configurações são tooa empatado pool e são aplicados tooall servidores no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf773-125">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="bf773-126">**Porta de front-end:** essa porta é a porta pública de saudação que é aberta no gateway do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="bf773-126">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="bf773-127">Tráfego atinge essa porta e, em seguida, obtém redirecionado tooone de servidores de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf773-127">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="bf773-128">**Ouvinte:** ouvinte Olá tem uma porta de front-end, um protocolo (Http ou Https, esses valores diferenciam maiusculas de minúsculas) e o nome do certificado SSL de saudação (se a configuração de SSL de descarregamento).</span><span class="sxs-lookup"><span data-stu-id="bf773-128">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="bf773-129">Para Application Gateways habilitados para vários sites, os indicadores de SNI e nome do host também são adicionados.</span><span class="sxs-lookup"><span data-stu-id="bf773-129">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="bf773-130">**Regra:** regra Olá associa ouvinte hello, pool de servidores de back-end hello e define o tráfego de saudação do pool de servidor back-end deve ser direcionado toowhen que ele atinja um ouvinte específico.</span><span class="sxs-lookup"><span data-stu-id="bf773-130">**Rule:** hello rule binds hello listener, hello back-end server pool, and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="bf773-131">As regras são processadas na ordem Olá que estão listados e o tráfego será direcionado por meio de saudação primeira regra correspondente, independentemente de especificidade.</span><span class="sxs-lookup"><span data-stu-id="bf773-131">Rules are processed in hello order they are listed, and traffic will be directed via hello first rule that matches regardless of specificity.</span></span> <span data-ttu-id="bf773-132">Por exemplo, se você tiver uma regra usando um ouvinte básico e uma regra usando um ouvinte de multissite ambos em Olá mesma regra de porta, Olá com ouvinte de multissite Olá deverá ser listada antes regra Olá com o ouvinte de saudação básica em ordem para Olá multissite regra toofunction como esperado.</span><span class="sxs-lookup"><span data-stu-id="bf773-132">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on hello same port, hello rule with hello multi-site listener must be listed before hello rule with hello basic listener in order for hello multi-site rule toofunction as expected.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="bf773-133">Criar um Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="bf773-133">Create an application gateway</span></span>

<span data-ttu-id="bf773-134">Olá seguem etapas Olá necessário toocreate um application gateway:</span><span class="sxs-lookup"><span data-stu-id="bf773-134">hello following are hello steps needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="bf773-135">Criar um grupo de recursos para o Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="bf773-135">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="bf773-136">Crie uma rede virtual e sub-redes IP público para o gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="bf773-136">Create a virtual network, subnets, and public IP for hello application gateway.</span></span>
3. <span data-ttu-id="bf773-137">Criar um objeto de configuração do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bf773-137">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="bf773-138">Criar um recurso de gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bf773-138">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="bf773-139">Criar um grupo de recursos para o Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="bf773-139">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="bf773-140">Certifique-se de que você estiver usando a versão mais recente de saudação do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf773-140">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="bf773-141">Há mais informações disponíveis em [Usando o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="bf773-141">More information is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="bf773-142">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="bf773-142">Step 1</span></span>

<span data-ttu-id="bf773-143">Faça logon no tooAzure</span><span class="sxs-lookup"><span data-stu-id="bf773-143">Log in tooAzure</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="bf773-144">Você está tooauthenticate solicitado com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="bf773-144">You are prompted tooauthenticate with your credentials.</span></span>

### <a name="step-2"></a><span data-ttu-id="bf773-145">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="bf773-145">Step 2</span></span>

<span data-ttu-id="bf773-146">Verificar as assinaturas de saudação para conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf773-146">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="bf773-147">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="bf773-147">Step 3</span></span>

<span data-ttu-id="bf773-148">Escolha qual toouse suas assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf773-148">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="bf773-149">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="bf773-149">Step 4</span></span>

<span data-ttu-id="bf773-150">Crie um grupo de recursos (ignore esta etapa se você estiver usando um grupo de recursos existente).</span><span class="sxs-lookup"><span data-stu-id="bf773-150">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

<span data-ttu-id="bf773-151">Como alternativa, também é possível pode criar marcas para um grupo de recursos para o gateway de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="bf773-151">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

<span data-ttu-id="bf773-152">O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local.</span><span class="sxs-lookup"><span data-stu-id="bf773-152">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="bf773-153">Esse local é usado como o local padrão de saudação para recursos desse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="bf773-153">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="bf773-154">Certifique-se de que todos os comandos toocreate uma saudação de uso de gateway de aplicativo mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="bf773-154">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

<span data-ttu-id="bf773-155">O exemplo hello acima, criamos um grupo de recursos chamado **appgw RG** com um local de **Oeste dos EUA**.</span><span class="sxs-lookup"><span data-stu-id="bf773-155">In hello example above, we created a resource group called **appgw-RG** with a location of **West US**.</span></span>

> [!NOTE]
> <span data-ttu-id="bf773-156">Se você precisar tooconfigure uma investigação personalizada para o gateway de aplicativo, consulte [criar um gateway de aplicativos com testes personalizados usando o PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="bf773-156">If you need tooconfigure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="bf773-157">Confira [investigações personalizadas e monitoramento de integridade](application-gateway-probe-overview.md) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="bf773-157">Visit [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

## <a name="create-a-virtual-network-and-subnets"></a><span data-ttu-id="bf773-158">Crie a rede virtual e as sub-redes</span><span class="sxs-lookup"><span data-stu-id="bf773-158">Create a virtual network and subnets</span></span>

<span data-ttu-id="bf773-159">Olá mostrado no exemplo a seguir como toocreate uma rede virtual usando o Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="bf773-159">hello following example shows how toocreate a virtual network by using Resource Manager.</span></span> <span data-ttu-id="bf773-160">Duas sub-redes são criadas nesta etapa.</span><span class="sxs-lookup"><span data-stu-id="bf773-160">Two subnets are created in this step.</span></span> <span data-ttu-id="bf773-161">primeira sub-rede de saudação é para o próprio gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="bf773-161">hello first subnet is for hello application gateway itself.</span></span> <span data-ttu-id="bf773-162">Gateway de aplicativo requer seu próprio toohold sub-rede suas instâncias.</span><span class="sxs-lookup"><span data-stu-id="bf773-162">Application gateway requires its own subnet toohold its instances.</span></span> <span data-ttu-id="bf773-163">Somente outros gateways de aplicativo podem ser implantados na sub-rede.</span><span class="sxs-lookup"><span data-stu-id="bf773-163">Only other application gateways can be deployed in that subnet.</span></span> <span data-ttu-id="bf773-164">subrede segundo Olá é servidores de back-end de aplicativo usados toohold Olá.</span><span class="sxs-lookup"><span data-stu-id="bf773-164">hello second subnet is used toohold hello application backend servers.</span></span>

### <a name="step-1"></a><span data-ttu-id="bf773-165">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="bf773-165">Step 1</span></span>

<span data-ttu-id="bf773-166">Atribua Olá endereço intervalo 10.0.0.0/24 toohello sub-rede toobe variável toohold usado Olá application gateway.</span><span class="sxs-lookup"><span data-stu-id="bf773-166">Assign hello address range 10.0.0.0/24 toohello subnet variable toobe used toohold hello application gateway.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a><span data-ttu-id="bf773-167">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="bf773-167">Step 2</span></span>

<span data-ttu-id="bf773-168">Atribua subnet2 Olá endereço intervalo 10.0.1.0/24 toohello variável toobe usado para pools de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf773-168">Assign hello address range 10.0.1.0/24 toohello subnet2 variable toobe used for hello backend pools.</span></span>

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a><span data-ttu-id="bf773-169">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="bf773-169">Step 3</span></span>

<span data-ttu-id="bf773-170">Criar uma rede virtual denominada **appgwvnet** no grupo de recursos **appgw rg** para a região do hello Oeste dos EUA com hello prefixo 10.0.0.0/16 sub-rede 10.0.0.0/24 e 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="bf773-170">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24, and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a><span data-ttu-id="bf773-171">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="bf773-171">Step 4</span></span>

<span data-ttu-id="bf773-172">Atribua uma variável de sub-rede para as próximas etapas hello, que cria um application gateway.</span><span class="sxs-lookup"><span data-stu-id="bf773-172">Assign a subnet variable for hello next steps, which creates an application gateway.</span></span>

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="bf773-173">Criar um endereço IP público para a configuração de front-end Olá</span><span class="sxs-lookup"><span data-stu-id="bf773-173">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="bf773-174">Criar um recurso IP público **publicIP01** no grupo de recursos **appgw rg** para região Oeste dos EUA de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf773-174">Create a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="bf773-175">Um endereço IP é atribuído gateway de aplicativo toohello quando Olá serviço é iniciado.</span><span class="sxs-lookup"><span data-stu-id="bf773-175">An IP address is assigned toohello application gateway when hello service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="bf773-176">Criar uma configuração do gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="bf773-176">Create application gateway configuration</span></span>

<span data-ttu-id="bf773-177">Você tem tooset todos os itens de configuração antes de criar o gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="bf773-177">You have tooset up all configuration items before creating hello application gateway.</span></span> <span data-ttu-id="bf773-178">Olá etapas a seguir criam Olá itens de configuração que são necessárias para um recurso do application gateway.</span><span class="sxs-lookup"><span data-stu-id="bf773-178">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="bf773-179">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="bf773-179">Step 1</span></span>

<span data-ttu-id="bf773-180">Crie uma configuração de IP do gateway de aplicativo chamada **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="bf773-180">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="bf773-181">Quando o gateway de aplicativo é iniciado, ele pega um endereço IP da sub-rede de saudação configurado e rotear os endereços IP de toohello de tráfego de rede no pool IP de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf773-181">When application gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="bf773-182">Tenha em mente que cada instância usa um endereço IP.</span><span class="sxs-lookup"><span data-stu-id="bf773-182">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a><span data-ttu-id="bf773-183">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="bf773-183">Step 2</span></span>

<span data-ttu-id="bf773-184">Configurar as pool de endereços IP back-end Olá denominada **pool01** e **pool2** com endereços IP **134.170.185.46**, **134.170.188.221**, **134.170.185.50** para **pool1** e **134.170.186.46**, **134.170.189.221**, **134.170.186.50**  para **pool2**.</span><span class="sxs-lookup"><span data-stu-id="bf773-184">Configure hello back-end IP address pool named **pool01** and **pool2** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50** for **pool1** and **134.170.186.46**, **134.170.189.221**, **134.170.186.50** for **pool2**.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

<span data-ttu-id="bf773-185">Neste exemplo, há dois pools de back-end tooroute tráfego, com base no site solicitado hello.</span><span class="sxs-lookup"><span data-stu-id="bf773-185">In this example, there are two back-end pools tooroute network traffic based on hello requested site.</span></span> <span data-ttu-id="bf773-186">Um pool recebe o tráfego do site "contoso.com" e outro pool recebe o tráfego do site "fabrikam.com".</span><span class="sxs-lookup"><span data-stu-id="bf773-186">One pool receives traffic from site "contoso.com" and other pool receives traffic from site "fabrikam.com".</span></span> <span data-ttu-id="bf773-187">Você tem Olá tooreplace anterior tooadd de endereços IP seus próprios pontos de extremidade do endereço IP do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bf773-187">You have tooreplace hello preceding IP addresses tooadd your own application IP address endpoints.</span></span> <span data-ttu-id="bf773-188">Em vez de endereços IP internos, você também pode usar endereços IP públicos, FQDN ou NIC da VM para instâncias de back-end.</span><span class="sxs-lookup"><span data-stu-id="bf773-188">In place of internal IP addresses, you could also use public IP addresses, FQDN, or a VM's NIC for backend instances.</span></span> <span data-ttu-id="bf773-189">toospecify FQDNs em vez de IPs no PowerShell, use "-BackendFQDNs" parâmetro.</span><span class="sxs-lookup"><span data-stu-id="bf773-189">toospecify FQDNs instead of IPs in PowerShell use "-BackendFQDNs" parameter.</span></span>

### <a name="step-3"></a><span data-ttu-id="bf773-190">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="bf773-190">Step 3</span></span>

<span data-ttu-id="bf773-191">Definir configuração de gateway do aplicativo **poolsetting01** e **poolsetting02** Olá com balanceamento de carga de tráfego de rede no pool de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf773-191">Configure application gateway setting **poolsetting01** and **poolsetting02** for hello load-balanced network traffic in hello back-end pool.</span></span> <span data-ttu-id="bf773-192">Neste exemplo, você definir as configurações de pool de back-end diferente para pools de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf773-192">In this example, you configure different back-end pool settings for hello back-end pools.</span></span> <span data-ttu-id="bf773-193">Cada pool de back-end pode ter sua própria configuração de pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="bf773-193">Each back-end pool can have its own back-end pool setting.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="bf773-194">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="bf773-194">Step 4</span></span>

<span data-ttu-id="bf773-195">Configure Olá IP de front-end com o ponto de extremidade IP público.</span><span class="sxs-lookup"><span data-stu-id="bf773-195">Configure hello front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="bf773-196">Etapa 5</span><span class="sxs-lookup"><span data-stu-id="bf773-196">Step 5</span></span>

<span data-ttu-id="bf773-197">Configure portas de front-end Olá para o application gateway.</span><span class="sxs-lookup"><span data-stu-id="bf773-197">Configure hello front-end port for an application gateway.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a><span data-ttu-id="bf773-198">Etapa 6</span><span class="sxs-lookup"><span data-stu-id="bf773-198">Step 6</span></span>

<span data-ttu-id="bf773-199">Configurar dois certificados SSL para Olá dois sites, vamos toosupport neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="bf773-199">Configure two SSL certificates for hello two websites we are going toosupport in this example.</span></span> <span data-ttu-id="bf773-200">Um certificado é para o tráfego de contoso.com e Olá outro é para o tráfego de fabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="bf773-200">One certificate is for contoso.com traffic and hello other is for fabrikam.com traffic.</span></span> <span data-ttu-id="bf773-201">Esses certificados devem ser certificados emitidos por uma Autoridade de Certificação para seus sites.</span><span class="sxs-lookup"><span data-stu-id="bf773-201">These certificates should be a Certificate Authority issued certificates for your websites.</span></span> <span data-ttu-id="bf773-202">Os certificados autoassinados têm suporte, mas não são recomendados para o tráfego de produção.</span><span class="sxs-lookup"><span data-stu-id="bf773-202">Self-signed certificates are supported but not recommended for production traffic.</span></span>

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a><span data-ttu-id="bf773-203">Etapa 7</span><span class="sxs-lookup"><span data-stu-id="bf773-203">Step 7</span></span>

<span data-ttu-id="bf773-204">Configure dois ouvintes para dois sites Olá neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="bf773-204">Configure two listeners for hello two web sites in this example.</span></span> <span data-ttu-id="bf773-205">Esta etapa configura ouvintes Olá para endereço IP público, porta e host usado tooreceive o tráfego de entrada.</span><span class="sxs-lookup"><span data-stu-id="bf773-205">This step configures hello listeners for public IP address, port, and host used tooreceive incoming traffic.</span></span> <span data-ttu-id="bf773-206">Parâmetro de nome de host é necessário para suporte a vários sites e deve ser o conjunto toohello site apropriado para o qual Olá tráfego é recebido.</span><span class="sxs-lookup"><span data-stu-id="bf773-206">HostName parameter is required for multiple site support and should be set toohello appropriate website for which hello traffic is received.</span></span> <span data-ttu-id="bf773-207">Parâmetro RequireServerNameIndication deve ser definido tootrue para que precisam de suporte para SSL em um cenário de host de vários sites.</span><span class="sxs-lookup"><span data-stu-id="bf773-207">RequireServerNameIndication parameter should be set tootrue for websites that need support for SSL in a multiple host scenario.</span></span> <span data-ttu-id="bf773-208">Suporte a SSL é necessário, também é necessário toospecify Olá SSL certificado que é usado toosecure tráfego para o aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="bf773-208">If SSL support is required, you also need toospecify hello SSL certificate that is used toosecure traffic for that web application.</span></span> <span data-ttu-id="bf773-209">combinação de saudação de FrontendIPConfiguration, FrontendPort e nome de host deve ser exclusivo tooa ouvinte.</span><span class="sxs-lookup"><span data-stu-id="bf773-209">hello combination of FrontendIPConfiguration, FrontendPort, and HostName must be unique tooa listener.</span></span> <span data-ttu-id="bf773-210">Cada ouvinte pode dar suporte a um certificado.</span><span class="sxs-lookup"><span data-stu-id="bf773-210">Each listener can support one certificate.</span></span>

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a><span data-ttu-id="bf773-211">Etapa 8</span><span class="sxs-lookup"><span data-stu-id="bf773-211">Step 8</span></span>

<span data-ttu-id="bf773-212">Crie regra de dois definindo para Olá dois aplicativos web neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="bf773-212">Create two rule setting for hello two web applications in this example.</span></span> <span data-ttu-id="bf773-213">Uma regra vincula ouvintes, pools de back-end e as configurações de http.</span><span class="sxs-lookup"><span data-stu-id="bf773-213">A rule ties together listeners, backend pools and http settings.</span></span> <span data-ttu-id="bf773-214">Esta etapa configura Olá application gateway toouse básica regra de roteamento, uma para cada site.</span><span class="sxs-lookup"><span data-stu-id="bf773-214">This step configures hello application gateway toouse Basic routing rule, one for each website.</span></span> <span data-ttu-id="bf773-215">Tráfego tooeach site é recebida pelo seu ouvinte configurado e, em seguida, é direcionado tooits configurados de pool de back-end, usando as propriedades de saudação especificadas no hello BackendHttpSettings.</span><span class="sxs-lookup"><span data-stu-id="bf773-215">Traffic tooeach website is received by its configured listener, and is then directed tooits configured backend pool, using hello properties specified in hello BackendHttpSettings.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a><span data-ttu-id="bf773-216">Etapa 9</span><span class="sxs-lookup"><span data-stu-id="bf773-216">Step 9</span></span>

<span data-ttu-id="bf773-217">Configure o número de saudação de instâncias e o tamanho para o gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="bf773-217">Configure hello number of instances and size for hello application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="bf773-218">Criar um gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="bf773-218">Create application gateway</span></span>

<span data-ttu-id="bf773-219">Crie um gateway de aplicativos com todos os objetos de configuração da saudação etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="bf773-219">Create an application gateway with all configuration objects from hello preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> <span data-ttu-id="bf773-220">Provisionamento do Gateway de aplicativos é uma operação demorada e pode levar algum tempo toocomplete.</span><span class="sxs-lookup"><span data-stu-id="bf773-220">Application Gateway provisioning is a long running operation and may take some time toocomplete.</span></span>
> 
> 

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="bf773-221">Obter um nome DNS de Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="bf773-221">Get application gateway DNS name</span></span>

<span data-ttu-id="bf773-222">Depois de criar o gateway hello, Olá próxima etapa é tooconfigure Olá front-end para comunicação.</span><span class="sxs-lookup"><span data-stu-id="bf773-222">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="bf773-223">Ao usar um IP público, o gateway de aplicativo requer um nome DNS atribuído dinamicamente, o que não é amigável.</span><span class="sxs-lookup"><span data-stu-id="bf773-223">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="bf773-224">os usuários finais de tooensure pode pressionar o gateway de aplicativo hello, um registro CNAME pode ser usado toopoint toohello ponto de extremidade público do gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="bf773-224">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="bf773-225">[Configurando um nome de domínio personalizado no Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bf773-225">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="bf773-226">toodo, detalhes de recuperar de gateway de aplicativo hello e seu nome de IP/DNS associado usando Olá PublicIPAddress elemento toohello anexado application gateway.</span><span class="sxs-lookup"><span data-stu-id="bf773-226">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="bf773-227">nome DNS do gateway do aplicativo Hello deve ser usado toocreate um registro CNAME, qual nome DNS pontos Olá duas web aplicativos toothis.</span><span class="sxs-lookup"><span data-stu-id="bf773-227">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="bf773-228">uso de saudação de registros de um não é recomendável porque Olá VIP pode ser alterado na reinicialização do application gateway.</span><span class="sxs-lookup"><span data-stu-id="bf773-228">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="bf773-229">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bf773-229">Next steps</span></span>

<span data-ttu-id="bf773-230">Saiba como tooprotect seus sites com [Application Gateway - Firewall do aplicativo Web](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="bf773-230">Learn how tooprotect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

