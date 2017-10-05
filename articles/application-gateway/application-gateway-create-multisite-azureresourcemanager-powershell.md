---
title: "Criar um gateway de aplicativo para hospedar vários sites | Microsoft Docs"
description: "Esta página fornece instruções para criar e configurar um Gateway de Aplicativo do Azure para hospedar vários aplicativos Web no mesmo gateway."
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
ms.openlocfilehash: d42efa7d359f5c87c14afbfd138328b37c8ae6c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="80d03-103">Criar um gateway de aplicativo para hospedar vários aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="80d03-103">Create an application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="80d03-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="80d03-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="80d03-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="80d03-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)

<span data-ttu-id="80d03-106">A hospedagem de vários sites permite que você implante mais de um aplicativo Web no mesmo gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="80d03-106">Multiple site hosting allows you to deploy more than one web application on the same application gateway.</span></span> <span data-ttu-id="80d03-107">Ela depende da presença do cabeçalho de host na solicitação HTTP de entrada, para determinar quais ouvintes devem receber tráfego.</span><span class="sxs-lookup"><span data-stu-id="80d03-107">It relies on presence of host header in the incoming HTTP request, to determine which listener would receive traffic.</span></span> <span data-ttu-id="80d03-108">O ouvinte, em seguida, direciona o tráfego ao pool de back-end apropriado conforme configurado na definição de regras do gateway.</span><span class="sxs-lookup"><span data-stu-id="80d03-108">The listener then directs traffic to appropriate backend pool as configured in the rules definition of the gateway.</span></span> <span data-ttu-id="80d03-109">No caso de aplicativos Web habilitados com SSL, o gateway de aplicativo depende da extensão de SNI (Indicação de Nome de Servidor) para escolher o ouvinte correto para o tráfego da Web.</span><span class="sxs-lookup"><span data-stu-id="80d03-109">In SSL enabled web applications, application gateway relies on the Server Name Indication (SNI) extension to choose the correct listener for the web traffic.</span></span> <span data-ttu-id="80d03-110">Um uso comum para a hospedagem de vários sites é balancear a carga das solicitações para domínios da Web diferentes para pools de servidor back-end diferentes.</span><span class="sxs-lookup"><span data-stu-id="80d03-110">A common use for multiple site hosting is to load balance requests for different web domains to different back-end server pools.</span></span> <span data-ttu-id="80d03-111">Da mesma forma, vários subdomínios do mesmo domínio raiz também podem ser hospedados no mesmo Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="80d03-111">Similarly multiple subdomains of the same root domain could also be hosted on the same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="80d03-112">Cenário</span><span class="sxs-lookup"><span data-stu-id="80d03-112">Scenario</span></span>

<span data-ttu-id="80d03-113">No exemplo a seguir, o gateway de aplicativo está fornecendo o tráfego para contoso.com e fabrikam.com com dois pools de servidor back-end: o pool de servidores contoso e o pool de servidores fabrikam.</span><span class="sxs-lookup"><span data-stu-id="80d03-113">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="80d03-114">É possível usar uma configuração semelhante para hospedar subdomínios, como app.contoso.com e blog.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="80d03-114">Similar setup could be used to host subdomains like app.contoso.com and blog.contoso.com.</span></span>

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a><span data-ttu-id="80d03-116">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="80d03-116">Before you begin</span></span>

1. <span data-ttu-id="80d03-117">Instale a versão mais recente dos cmdlets do Azure PowerShell usando o Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="80d03-117">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="80d03-118">Você pode baixar e instalar a versão mais recente da seção **Windows PowerShell** da [página Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="80d03-118">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="80d03-119">Os servidores adicionados ao pool de back-end a fim de usar o gateway de aplicativo devem existir ou ter seus pontos de extremidade criados na rede virtual em uma sub-rede separada ou com um IP/VIP público atribuído.</span><span class="sxs-lookup"><span data-stu-id="80d03-119">The servers added to the back-end pool to use the application gateway must exist or have their endpoints created either in the virtual network in a separate subnet or with a public IP/VIP assigned.</span></span>

## <a name="requirements"></a><span data-ttu-id="80d03-120">Requisitos</span><span class="sxs-lookup"><span data-stu-id="80d03-120">Requirements</span></span>

* <span data-ttu-id="80d03-121">**Pool de servidores back-end:** a lista de endereços IP dos servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="80d03-121">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="80d03-122">Os endereços IP listados devem pertencer à sub-rede da rede virtual ou devem ser um IP/VIP público.</span><span class="sxs-lookup"><span data-stu-id="80d03-122">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="80d03-123">O FQDN também pode ser usado.</span><span class="sxs-lookup"><span data-stu-id="80d03-123">FQDN can also be used.</span></span>
* <span data-ttu-id="80d03-124">**Configurações do pool de servidores back-end:** cada pool tem configurações como porta, protocolo e afinidade baseada em cookie.</span><span class="sxs-lookup"><span data-stu-id="80d03-124">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="80d03-125">Essas configurações são vinculadas a um pool e aplicadas a todos os servidores no pool.</span><span class="sxs-lookup"><span data-stu-id="80d03-125">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="80d03-126">**Porta front-end:** essa porta é a porta pública aberta no gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="80d03-126">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="80d03-127">O tráfego atinge essa porta e é redirecionado para um dos servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="80d03-127">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="80d03-128">**Ouvinte:** o ouvinte tem uma porta front-end, um protocolo (HTTP ou HTTPS, esses valores diferenciam maiúsculas de minúsculas) e o nome do certificado SSL (caso esteja configurando o descarregamento SSL).</span><span class="sxs-lookup"><span data-stu-id="80d03-128">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="80d03-129">Para Application Gateways habilitados para vários sites, os indicadores de SNI e nome do host também são adicionados.</span><span class="sxs-lookup"><span data-stu-id="80d03-129">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="80d03-130">**Regra:** a regra vincula o ouvinte e o pool de servidores back-end e define a qual pool de servidores back-end o tráfego deve ser direcionado ao atingir um ouvinte específico.</span><span class="sxs-lookup"><span data-stu-id="80d03-130">**Rule:** The rule binds the listener, the back-end server pool, and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="80d03-131">As regras são processadas na ordem em que são listadas e o tráfego será direcionado por meio da primeira regra correspondente, independentemente de especificidade.</span><span class="sxs-lookup"><span data-stu-id="80d03-131">Rules are processed in the order they are listed, and traffic will be directed via the first rule that matches regardless of specificity.</span></span> <span data-ttu-id="80d03-132">Por exemplo, se você tiver uma regra usando um ouvinte básico e outra usando um ouvinte multissite, ambas na mesma porta, a regra com o ouvinte multissite deverá ser listada antes daquela com o ouvinte básico, para que a função multissite funcione conforme esperado.</span><span class="sxs-lookup"><span data-stu-id="80d03-132">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on the same port, the rule with the multi-site listener must be listed before the rule with the basic listener in order for the multi-site rule to function as expected.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="80d03-133">Criar um gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="80d03-133">Create an application gateway</span></span>

<span data-ttu-id="80d03-134">A seguir estão as etapas necessárias para criar um gateway de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="80d03-134">The following are the steps needed to create an application gateway:</span></span>

1. <span data-ttu-id="80d03-135">Criar um grupo de recursos para o Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="80d03-135">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="80d03-136">Criar uma rede virtual, uma sub-rede e um IP público para o gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="80d03-136">Create a virtual network, subnets, and public IP for the application gateway.</span></span>
3. <span data-ttu-id="80d03-137">Criar um objeto de configuração do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="80d03-137">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="80d03-138">Criar um recurso de gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="80d03-138">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="80d03-139">Criar um grupo de recursos para o Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="80d03-139">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="80d03-140">Use a versão mais recente do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="80d03-140">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="80d03-141">Há mais informações disponíveis em [Usando o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="80d03-141">More information is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="80d03-142">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="80d03-142">Step 1</span></span>

<span data-ttu-id="80d03-143">Fazer logon no Azure</span><span class="sxs-lookup"><span data-stu-id="80d03-143">Log in to Azure</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="80d03-144">Você deve se autenticar com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="80d03-144">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-2"></a><span data-ttu-id="80d03-145">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="80d03-145">Step 2</span></span>

<span data-ttu-id="80d03-146">Verificar as assinaturas da conta.</span><span class="sxs-lookup"><span data-stu-id="80d03-146">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="80d03-147">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="80d03-147">Step 3</span></span>

<span data-ttu-id="80d03-148">Escolha quais das suas assinaturas do Azure deseja usar.</span><span class="sxs-lookup"><span data-stu-id="80d03-148">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="80d03-149">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="80d03-149">Step 4</span></span>

<span data-ttu-id="80d03-150">Crie um grupo de recursos (ignore esta etapa se você estiver usando um grupo de recursos existente).</span><span class="sxs-lookup"><span data-stu-id="80d03-150">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

<span data-ttu-id="80d03-151">Como alternativa, também é possível pode criar marcas para um grupo de recursos para o gateway de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="80d03-151">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

<span data-ttu-id="80d03-152">O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local.</span><span class="sxs-lookup"><span data-stu-id="80d03-152">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="80d03-153">Esse local é usado como o local padrão para os recursos do grupo de recursos em questão.</span><span class="sxs-lookup"><span data-stu-id="80d03-153">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="80d03-154">Verifique se todos os comandos para criar um gateway de aplicativo usam o mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="80d03-154">Make sure that all commands to create an application gateway use the same resource group.</span></span>

<span data-ttu-id="80d03-155">No exemplo acima, criamos um grupo de recursos denominado **appgw-RG** com o local **Oeste dos EUA**.</span><span class="sxs-lookup"><span data-stu-id="80d03-155">In the example above, we created a resource group called **appgw-RG** with a location of **West US**.</span></span>

> [!NOTE]
> <span data-ttu-id="80d03-156">Se você precisar configurar uma investigação personalizada para o gateway de aplicativo, veja [Criar um gateway de aplicativo com investigações personalizadas usando o PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="80d03-156">If you need to configure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="80d03-157">Confira [investigações personalizadas e monitoramento de integridade](application-gateway-probe-overview.md) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="80d03-157">Visit [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

## <a name="create-a-virtual-network-and-subnets"></a><span data-ttu-id="80d03-158">Crie a rede virtual e as sub-redes</span><span class="sxs-lookup"><span data-stu-id="80d03-158">Create a virtual network and subnets</span></span>

<span data-ttu-id="80d03-159">O exemplo a seguir mostra como criar uma rede virtual usando o Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="80d03-159">The following example shows how to create a virtual network by using Resource Manager.</span></span> <span data-ttu-id="80d03-160">Duas sub-redes são criadas nesta etapa.</span><span class="sxs-lookup"><span data-stu-id="80d03-160">Two subnets are created in this step.</span></span> <span data-ttu-id="80d03-161">A primeira sub-rede é para o próprio gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="80d03-161">The first subnet is for the application gateway itself.</span></span> <span data-ttu-id="80d03-162">O gateway de aplicativo requer sua própria sub-rede para armazenar suas instâncias.</span><span class="sxs-lookup"><span data-stu-id="80d03-162">Application gateway requires its own subnet to hold its instances.</span></span> <span data-ttu-id="80d03-163">Somente outros gateways de aplicativo podem ser implantados na sub-rede.</span><span class="sxs-lookup"><span data-stu-id="80d03-163">Only other application gateways can be deployed in that subnet.</span></span> <span data-ttu-id="80d03-164">A segunda sub-rede é usada para manter os servidores back-end de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="80d03-164">The second subnet is used to hold the application backend servers.</span></span>

### <a name="step-1"></a><span data-ttu-id="80d03-165">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="80d03-165">Step 1</span></span>

<span data-ttu-id="80d03-166">Atribua o intervalo de endereços 10.0.0.0/24 à variável de sub-rede a ser usada para manter a gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="80d03-166">Assign the address range 10.0.0.0/24 to the subnet variable to be used to hold the application gateway.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a><span data-ttu-id="80d03-167">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="80d03-167">Step 2</span></span>

<span data-ttu-id="80d03-168">Atribua o intervalo de endereços 10.0.1.0/24 à variável de sub-rede 2 a ser usada para os pools de back-end.</span><span class="sxs-lookup"><span data-stu-id="80d03-168">Assign the address range 10.0.1.0/24 to the subnet2 variable to be used for the backend pools.</span></span>

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a><span data-ttu-id="80d03-169">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="80d03-169">Step 3</span></span>

<span data-ttu-id="80d03-170">Crie uma rede virtual chamada **appgwvnet** no grupo de recursos **appgw-rg** para a região Oeste dos EUA usando o prefixo 10.0.0.0/16 com a sub-rede 10.0.0.0/24 e 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="80d03-170">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24, and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a><span data-ttu-id="80d03-171">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="80d03-171">Step 4</span></span>

<span data-ttu-id="80d03-172">Atribua uma variável de sub-rede para as próximas etapas, o que criará um gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="80d03-172">Assign a subnet variable for the next steps, which creates an application gateway.</span></span>

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="80d03-173">Criar um endereço IP público para a configuração de front-end</span><span class="sxs-lookup"><span data-stu-id="80d03-173">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="80d03-174">Crie um recurso IP público **publicIP01** no grupo de recursos **appgw-rg** para a região Oeste dos EUA.</span><span class="sxs-lookup"><span data-stu-id="80d03-174">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="80d03-175">Um endereço IP é atribuído ao gateway de aplicativo quando o serviço é iniciado.</span><span class="sxs-lookup"><span data-stu-id="80d03-175">An IP address is assigned to the application gateway when the service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="80d03-176">Criar uma configuração do gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="80d03-176">Create application gateway configuration</span></span>

<span data-ttu-id="80d03-177">Você precisa configurar todos os itens de configuração antes de criar o gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="80d03-177">You have to set up all configuration items before creating the application gateway.</span></span> <span data-ttu-id="80d03-178">As etapas a seguir criam os itens de configuração necessários para um recurso de gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="80d03-178">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="80d03-179">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="80d03-179">Step 1</span></span>

<span data-ttu-id="80d03-180">Crie uma configuração de IP do gateway de aplicativo chamada **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="80d03-180">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="80d03-181">Quando o Gateway de Aplicativo é iniciado, ele escolhe um endereço IP na sub-rede configurada e no tráfego de rede da rota para os endereços IP no pool de IPs de back-end.</span><span class="sxs-lookup"><span data-stu-id="80d03-181">When application gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="80d03-182">Tenha em mente que cada instância usa um endereço IP.</span><span class="sxs-lookup"><span data-stu-id="80d03-182">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a><span data-ttu-id="80d03-183">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="80d03-183">Step 2</span></span>

<span data-ttu-id="80d03-184">Configure o pool de endereços IP de back-end denominado **pool01** e **pool2** com os endereços IP **134.170.185.46**, **134.170.188.221**, **134.170.185.50** para o **pool1** e **134.170.186.46**, **134.170.189.221**, **134.170.186.50** para o **pool2**.</span><span class="sxs-lookup"><span data-stu-id="80d03-184">Configure the back-end IP address pool named **pool01** and **pool2** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50** for **pool1** and **134.170.186.46**, **134.170.189.221**, **134.170.186.50** for **pool2**.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

<span data-ttu-id="80d03-185">Neste exemplo, haverá dois pools de back-end para rotear o tráfego de rede com base no site solicitado.</span><span class="sxs-lookup"><span data-stu-id="80d03-185">In this example, there are two back-end pools to route network traffic based on the requested site.</span></span> <span data-ttu-id="80d03-186">Um pool recebe o tráfego do site "contoso.com" e outro pool recebe o tráfego do site "fabrikam.com".</span><span class="sxs-lookup"><span data-stu-id="80d03-186">One pool receives traffic from site "contoso.com" and other pool receives traffic from site "fabrikam.com".</span></span> <span data-ttu-id="80d03-187">Você precisa substituir os endereços IP anteriores para adicionar seus próprios pontos de extremidade de endereço IP do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="80d03-187">You have to replace the preceding IP addresses to add your own application IP address endpoints.</span></span> <span data-ttu-id="80d03-188">Em vez de endereços IP internos, você também pode usar endereços IP públicos, FQDN ou NIC da VM para instâncias de back-end.</span><span class="sxs-lookup"><span data-stu-id="80d03-188">In place of internal IP addresses, you could also use public IP addresses, FQDN, or a VM's NIC for backend instances.</span></span> <span data-ttu-id="80d03-189">Para especificar FQDNs em vez de IPs no PowerShell, use o parâmetro "-BackendFQDNs".</span><span class="sxs-lookup"><span data-stu-id="80d03-189">To specify FQDNs instead of IPs in PowerShell use "-BackendFQDNs" parameter.</span></span>

### <a name="step-3"></a><span data-ttu-id="80d03-190">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="80d03-190">Step 3</span></span>

<span data-ttu-id="80d03-191">Defina as configurações de **poolsetting01** e **poolsetting02** do gateway de aplicativo para o tráfego de rede com carga balanceada no pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="80d03-191">Configure application gateway setting **poolsetting01** and **poolsetting02** for the load-balanced network traffic in the back-end pool.</span></span> <span data-ttu-id="80d03-192">Neste exemplo, defina as configurações diferentes de pool de back-end para os pools de back-end.</span><span class="sxs-lookup"><span data-stu-id="80d03-192">In this example, you configure different back-end pool settings for the back-end pools.</span></span> <span data-ttu-id="80d03-193">Cada pool de back-end pode ter sua própria configuração de pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="80d03-193">Each back-end pool can have its own back-end pool setting.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="80d03-194">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="80d03-194">Step 4</span></span>

<span data-ttu-id="80d03-195">Configure o IP front-end com o ponto de extremidade IP público.</span><span class="sxs-lookup"><span data-stu-id="80d03-195">Configure the front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="80d03-196">Etapa 5</span><span class="sxs-lookup"><span data-stu-id="80d03-196">Step 5</span></span>

<span data-ttu-id="80d03-197">Configure a porta front-end para um gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="80d03-197">Configure the front-end port for an application gateway.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a><span data-ttu-id="80d03-198">Etapa 6</span><span class="sxs-lookup"><span data-stu-id="80d03-198">Step 6</span></span>

<span data-ttu-id="80d03-199">Configure dois certificados SSL para os dois sites para os quais daremos suporte nesse exemplo.</span><span class="sxs-lookup"><span data-stu-id="80d03-199">Configure two SSL certificates for the two websites we are going to support in this example.</span></span> <span data-ttu-id="80d03-200">Um certificado é para tráfego de contoso.com e o outro é para o tráfego de fabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="80d03-200">One certificate is for contoso.com traffic and the other is for fabrikam.com traffic.</span></span> <span data-ttu-id="80d03-201">Esses certificados devem ser certificados emitidos por uma Autoridade de Certificação para seus sites.</span><span class="sxs-lookup"><span data-stu-id="80d03-201">These certificates should be a Certificate Authority issued certificates for your websites.</span></span> <span data-ttu-id="80d03-202">Os certificados autoassinados têm suporte, mas não são recomendados para o tráfego de produção.</span><span class="sxs-lookup"><span data-stu-id="80d03-202">Self-signed certificates are supported but not recommended for production traffic.</span></span>

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a><span data-ttu-id="80d03-203">Etapa 7</span><span class="sxs-lookup"><span data-stu-id="80d03-203">Step 7</span></span>

<span data-ttu-id="80d03-204">Configure dois ouvintes para os dois sites neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="80d03-204">Configure two listeners for the two web sites in this example.</span></span> <span data-ttu-id="80d03-205">Esta etapa configura os ouvintes para o endereço IP público, a porta e o host usados para receber o tráfego de entrada.</span><span class="sxs-lookup"><span data-stu-id="80d03-205">This step configures the listeners for public IP address, port, and host used to receive incoming traffic.</span></span> <span data-ttu-id="80d03-206">O parâmetro HostName é necessário para o suporte a vários sites e deve ser definido para o site apropriado no qual o tráfego é recebido.</span><span class="sxs-lookup"><span data-stu-id="80d03-206">HostName parameter is required for multiple site support and should be set to the appropriate website for which the traffic is received.</span></span> <span data-ttu-id="80d03-207">O parâmetro RequireServerNameIndication deve ser definido como true para sites que precisam de suporte para SSL em um cenário de vários hosts.</span><span class="sxs-lookup"><span data-stu-id="80d03-207">RequireServerNameIndication parameter should be set to true for websites that need support for SSL in a multiple host scenario.</span></span> <span data-ttu-id="80d03-208">Se o suporte a SSL for necessário, você também precisará especificar o certificado SSL que é usado para proteger o tráfego para aquele aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="80d03-208">If SSL support is required, you also need to specify the SSL certificate that is used to secure traffic for that web application.</span></span> <span data-ttu-id="80d03-209">A combinação de FrontendIPConfiguration, FrontendPort e HostName deve ser exclusiva para um ouvinte.</span><span class="sxs-lookup"><span data-stu-id="80d03-209">The combination of FrontendIPConfiguration, FrontendPort, and HostName must be unique to a listener.</span></span> <span data-ttu-id="80d03-210">Cada ouvinte pode dar suporte a um certificado.</span><span class="sxs-lookup"><span data-stu-id="80d03-210">Each listener can support one certificate.</span></span>

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a><span data-ttu-id="80d03-211">Etapa 8</span><span class="sxs-lookup"><span data-stu-id="80d03-211">Step 8</span></span>

<span data-ttu-id="80d03-212">Crie duas configurações de regra para os dois aplicativos Web nesse exemplo.</span><span class="sxs-lookup"><span data-stu-id="80d03-212">Create two rule setting for the two web applications in this example.</span></span> <span data-ttu-id="80d03-213">Uma regra vincula ouvintes, pools de back-end e as configurações de http.</span><span class="sxs-lookup"><span data-stu-id="80d03-213">A rule ties together listeners, backend pools and http settings.</span></span> <span data-ttu-id="80d03-214">Esta etapa configura o gateway de aplicativo para usar a regra de roteamento Básica, uma para cada site.</span><span class="sxs-lookup"><span data-stu-id="80d03-214">This step configures the application gateway to use Basic routing rule, one for each website.</span></span> <span data-ttu-id="80d03-215">O tráfego para cada site é recebido pelo seu ouvinte configurado e é direcionado para seu pool de back-end configurado, usando as propriedades especificadas no BackendHttpSettings.</span><span class="sxs-lookup"><span data-stu-id="80d03-215">Traffic to each website is received by its configured listener, and is then directed to its configured backend pool, using the properties specified in the BackendHttpSettings.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a><span data-ttu-id="80d03-216">Etapa 9</span><span class="sxs-lookup"><span data-stu-id="80d03-216">Step 9</span></span>

<span data-ttu-id="80d03-217">Configure o número de instâncias e o tamanho do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="80d03-217">Configure the number of instances and size for the application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="80d03-218">Criar um gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="80d03-218">Create application gateway</span></span>

<span data-ttu-id="80d03-219">Crie um gateway de aplicativo com todos os objetos de configuração das etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="80d03-219">Create an application gateway with all configuration objects from the preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> <span data-ttu-id="80d03-220">O provisionamento do Gateway de Aplicativo é uma operação demorada e pode levar algum tempo para ser concluída.</span><span class="sxs-lookup"><span data-stu-id="80d03-220">Application Gateway provisioning is a long running operation and may take some time to complete.</span></span>
> 
> 

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="80d03-221">Obter um nome DNS de gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="80d03-221">Get application gateway DNS name</span></span>

<span data-ttu-id="80d03-222">Depois de criar o gateway, a próxima etapa será configurar o front-end para comunicação.</span><span class="sxs-lookup"><span data-stu-id="80d03-222">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="80d03-223">Ao usar um IP público, o gateway de aplicativo requer um nome DNS atribuído dinamicamente, o que não é amigável.</span><span class="sxs-lookup"><span data-stu-id="80d03-223">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="80d03-224">Para garantir que os usuários finais possam alcançar o gateway de aplicativo, um registro CNAME pode ser usado para apontar para o ponto de extremidade público do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="80d03-224">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="80d03-225">[Configurando um nome de domínio personalizado no Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="80d03-225">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="80d03-226">Para isso, recupere detalhes do Gateway de Aplicativo e seu nome DNS/IP associado usando o elemento PublicIPAddress anexado ao Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="80d03-226">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="80d03-227">O nome DNS do Gateway de Aplicativo deve ser usado para criar um registro CNAME que aponta os dois aplicativos Web para esse nome DNS.</span><span class="sxs-lookup"><span data-stu-id="80d03-227">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="80d03-228">O uso de registros A não é recomendável, pois o VIP pode mudar na reinicialização do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="80d03-228">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="80d03-229">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="80d03-229">Next steps</span></span>

<span data-ttu-id="80d03-230">Saiba como proteger seus sites com o [Gateway de Aplicativo - Firewall de Aplicativo Web](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="80d03-230">Learn how to protect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

