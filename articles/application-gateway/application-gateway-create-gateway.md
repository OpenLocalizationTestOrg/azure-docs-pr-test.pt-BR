---
title: Criar, iniciar ou excluir um gateway de aplicativo | Microsoft Docs
description: "Esta página oferece instruções para criar, configurar, iniciar e excluir um gateway de aplicativo do Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 577054ca-8368-4fbf-8d53-a813f29dc3bc
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: c4932096229b1941e0966e7f3e97de39c6931392
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-start-or-delete-an-application-gateway-with-powershell"></a><span data-ttu-id="70bf6-103">Criar, iniciar ou excluir um gateway de aplicativo com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="70bf6-103">Create, start, or delete an application gateway with PowerShell</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="70bf6-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="70bf6-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="70bf6-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="70bf6-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="70bf6-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="70bf6-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="70bf6-107">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="70bf6-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="70bf6-108">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="70bf6-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="70bf6-109">O Gateway de Aplicativo do Azure é um balanceador de carga de camada 7.</span><span class="sxs-lookup"><span data-stu-id="70bf6-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="70bf6-110">Ele fornece o failover e solicitações HTTP de roteamento de desempenho entre diferentes servidores, estejam eles na nuvem ou no local.</span><span class="sxs-lookup"><span data-stu-id="70bf6-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="70bf6-111">O Gateway de Aplicativo fornece muitos recursos do ADC (Controlador de Entrega de Aplicativos), incluindo o balanceamento de carga de HTTP, a afinidade de sessão baseada em cookies, o descarregamento de SSL (Secure Sockets Layer), as sondas de integridade personalizadas, suporte para vários sites e muitos outros.</span><span class="sxs-lookup"><span data-stu-id="70bf6-111">Application Gateway provides many Application Delivery Controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="70bf6-112">Para localizar uma lista completa dos recursos com suporte, visite [Visão geral do Gateway de Aplicativo](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="70bf6-112">To find a complete list of supported features, visit [Application Gateway Overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="70bf6-113">Este artigo orienta você pelas etapas para criar, configurar, iniciar e excluir um gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="70bf6-113">This article walks you through the steps to create, configure, start, and delete an application gateway.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="70bf6-114">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="70bf6-114">Before you begin</span></span>

1. <span data-ttu-id="70bf6-115">Instale a versão mais recente dos cmdlets do Azure PowerShell usando o Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="70bf6-115">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="70bf6-116">Você pode baixar e instalar a versão mais recente na seção **Windows PowerShell** da [página Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="70bf6-116">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="70bf6-117">Se você tiver uma rede virtual existente, selecione uma sub-rede vazia existente ou crie uma nova sub-rede na rede virtual existente unicamente para uso pelo gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="70bf6-117">If you have an existing virtual network, either select an existing empty subnet or create a new subnet in your existing virtual network solely for use by the application gateway.</span></span> <span data-ttu-id="70bf6-118">Você não pode implantar o gateway de aplicativo para uma rede virtual diferente dos recursos que pretende implantar por trás do gateway de aplicativo, a não ser que use emparelhamento de Vnet.</span><span class="sxs-lookup"><span data-stu-id="70bf6-118">You cannot deploy the application gateway to a different virtual network than the resources you intend to deploy behind the application gateway unless vnet peering is used.</span></span> <span data-ttu-id="70bf6-119">Para saber mais, acesse [Emparelhamento de VNet](../virtual-network/virtual-network-peering-overview.md)</span><span class="sxs-lookup"><span data-stu-id="70bf6-119">To learn more visit [Vnet Peering](../virtual-network/virtual-network-peering-overview.md)</span></span>
3. <span data-ttu-id="70bf6-120">Verifique se você tem uma rede virtual em funcionamento com uma sub-rede válida.</span><span class="sxs-lookup"><span data-stu-id="70bf6-120">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="70bf6-121">Verifique se não há máquinas virtuais ou implantações em nuvem usando a sub-rede.</span><span class="sxs-lookup"><span data-stu-id="70bf6-121">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="70bf6-122">O gateway de aplicativo deve estar sozinho em uma sub-rede de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="70bf6-122">The application gateway must be by itself in a virtual network subnet.</span></span>
4. <span data-ttu-id="70bf6-123">Os servidores que você configura para usar o gateway de aplicativo devem existir ou ter seus pontos de extremidade criados na rede virtual ou com um IP/VIP público atribuído.</span><span class="sxs-lookup"><span data-stu-id="70bf6-123">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="70bf6-124">O que é necessário para criar um gateway de aplicativo?</span><span class="sxs-lookup"><span data-stu-id="70bf6-124">What is required to create an application gateway?</span></span>

<span data-ttu-id="70bf6-125">Quando você usa o comando `New-AzureApplicationGateway` para criar o gateway de aplicativo, nenhuma configuração é definida nesse ponto e o recurso recém-criado é configurado usando um objeto de configuração ou usando XML.</span><span class="sxs-lookup"><span data-stu-id="70bf6-125">When you use the `New-AzureApplicationGateway` command to create the application gateway, no configuration is set at this point and the newly created resource are configured either by using XML or a configuration object.</span></span>

<span data-ttu-id="70bf6-126">Os valores são:</span><span class="sxs-lookup"><span data-stu-id="70bf6-126">The values are:</span></span>

* <span data-ttu-id="70bf6-127">**Pool de servidores back-end:** a lista de endereços IP dos servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="70bf6-127">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="70bf6-128">Os endereços IP listados devem pertencer à sub-rede da rede virtual ou devem ser um IP/VIP público.</span><span class="sxs-lookup"><span data-stu-id="70bf6-128">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="70bf6-129">**Configurações do pool de servidores back-end:** cada pool tem configurações como porta, protocolo e afinidade baseada em cookie.</span><span class="sxs-lookup"><span data-stu-id="70bf6-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="70bf6-130">Essas configurações são vinculadas a um pool e aplicadas a todos os servidores no pool.</span><span class="sxs-lookup"><span data-stu-id="70bf6-130">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="70bf6-131">**Porta front-end:** essa porta é a porta pública aberta no gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="70bf6-131">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="70bf6-132">O tráfego atinge essa porta e é redirecionado para um dos servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="70bf6-132">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="70bf6-133">**Ouvinte:** o ouvinte tem uma porta front-end, um protocolo (HTTP ou HTTPS, esses valores diferenciam maiúsculas de minúsculas) e o nome do certificado SSL (caso esteja configurando o descarregamento SSL).</span><span class="sxs-lookup"><span data-stu-id="70bf6-133">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="70bf6-134">**Regra:** a regra vincula o ouvinte e o pool de servidores back-end e define à qual pool de servidores back-end o tráfego deve ser direcionado quando atinge um ouvinte específico.</span><span class="sxs-lookup"><span data-stu-id="70bf6-134">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="70bf6-135">Criar um Application Gateway</span><span class="sxs-lookup"><span data-stu-id="70bf6-135">Create an application gateway</span></span>

<span data-ttu-id="70bf6-136">Para criar um Application Gateway:</span><span class="sxs-lookup"><span data-stu-id="70bf6-136">To create an application gateway:</span></span>

1. <span data-ttu-id="70bf6-137">Criar um recurso de gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="70bf6-137">Create an application gateway resource.</span></span>
2. <span data-ttu-id="70bf6-138">Crie um arquivo XML de configuração ou um objeto de configuração.</span><span class="sxs-lookup"><span data-stu-id="70bf6-138">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="70bf6-139">Confirme a configuração do recurso de gateway de aplicativo recém-criado.</span><span class="sxs-lookup"><span data-stu-id="70bf6-139">Commit the configuration to the newly created application gateway resource.</span></span>

> [!NOTE]
> <span data-ttu-id="70bf6-140">Se você precisar configurar uma investigação personalizada para o gateway de aplicativo, veja [Criar um gateway de aplicativo com investigações personalizadas usando o PowerShell](application-gateway-create-probe-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="70bf6-140">If you need to configure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-classic-ps.md).</span></span> <span data-ttu-id="70bf6-141">Confira [investigações personalizadas e monitoramento de integridade](application-gateway-probe-overview.md) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="70bf6-141">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

![Cenário de exemplo][scenario]

### <a name="create-an-application-gateway-resource"></a><span data-ttu-id="70bf6-143">Criar um recurso de Application Gateway</span><span class="sxs-lookup"><span data-stu-id="70bf6-143">Create an application gateway resource</span></span>

<span data-ttu-id="70bf6-144">Para criar o gateway, use o cmdlet `New-AzureApplicationGateway`, substituindo os valores pelos seus próprios.</span><span class="sxs-lookup"><span data-stu-id="70bf6-144">To create the gateway, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="70bf6-145">A cobrança pelo gateway não se inicia neste momento.</span><span class="sxs-lookup"><span data-stu-id="70bf6-145">Billing for the gateway does not start at this point.</span></span> <span data-ttu-id="70bf6-146">A cobrança é iniciada em uma etapa posterior, quando o gateway é iniciado com êxito.</span><span class="sxs-lookup"><span data-stu-id="70bf6-146">Billing begins in a later step, when the gateway is successfully started.</span></span>

<span data-ttu-id="70bf6-147">O exemplo a seguir cria um novo Application Gateway usando uma rede virtual chamada "testvnet1" e uma sub-rede chamada "subnet-1":</span><span class="sxs-lookup"><span data-stu-id="70bf6-147">The following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1":</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="70bf6-148">*Description*, *InstanceCount* e *GatewaySize* são parâmetros opcionais.</span><span class="sxs-lookup"><span data-stu-id="70bf6-148">*Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span>

<span data-ttu-id="70bf6-149">Para validar esse gateway que foi criado, você pode usar o cmdlet `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="70bf6-149">To validate that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Stopped
VirtualIPs    : {}
DnsName       :
```

> [!NOTE]
> <span data-ttu-id="70bf6-150">O valor padrão para *InstanceCount* é 2, com um valor máximo de 10.</span><span class="sxs-lookup"><span data-stu-id="70bf6-150">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="70bf6-151">O valor padrão para *GatewaySize* é Medium.</span><span class="sxs-lookup"><span data-stu-id="70bf6-151">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="70bf6-152">Você pode escolher entre Small, Medium e Large.</span><span class="sxs-lookup"><span data-stu-id="70bf6-152">You can choose between Small, Medium and Large.</span></span>

<span data-ttu-id="70bf6-153">*VirtualIPs* e *DnsName* são mostrados em branco porque o gateway ainda não foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="70bf6-153">*VirtualIPs* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="70bf6-154">Eles serão criados depois que o gateway estiver em estado de execução.</span><span class="sxs-lookup"><span data-stu-id="70bf6-154">These are created once the gateway is in the running state.</span></span>

## <a name="configure-the-application-gateway"></a><span data-ttu-id="70bf6-155">Configurar o gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="70bf6-155">Configure the application gateway</span></span>

<span data-ttu-id="70bf6-156">Você pode configurar o gateway de aplicativo usando XML ou um objeto de configuração.</span><span class="sxs-lookup"><span data-stu-id="70bf6-156">You can configure the application gateway by using XML or a configuration object.</span></span>

### <a name="configure-the-application-gateway-by-using-xml"></a><span data-ttu-id="70bf6-157">Configurar o gateway de aplicativo usando XML</span><span class="sxs-lookup"><span data-stu-id="70bf6-157">Configure the application gateway by using XML</span></span>

<span data-ttu-id="70bf6-158">No exemplo a seguir, você usará um arquivo XML para definir todas as configurações do Application Gateway e confirmá-las para o recurso do Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="70bf6-158">In the following example, you use an XML file to configure all application gateway settings and commit them to the application gateway resource.</span></span>  

#### <a name="step-1"></a><span data-ttu-id="70bf6-159">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="70bf6-159">Step 1</span></span>

<span data-ttu-id="70bf6-160">Copie o seguinte texto no bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="70bf6-160">Copy the following text to Notepad.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>(name-of-your-frontend-port)</Name>
            <Port>(port number)</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>(name-of-your-backend-pool)</Name>
            <IPAddresses>
                <IPAddress>(your-IP-address-for-backend-pool)</IPAddress>
                <IPAddress>(your-second-IP-address-for-backend-pool)</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>(backend-setting-name-to-configure-rule)</Name>
            <Port>80</Port>
            <Protocol>[Http|Https]</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>(name-of-the-listener)</Name>
            <FrontendPort>(name-of-your-frontend-port)</FrontendPort>
            <Protocol>[Http|Https]</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>(name-of-load-balancing-rule)</Name>
            <Type>basic</Type>
            <BackendHttpSettings>(backend-setting-name-to-configure-rule)</BackendHttpSettings>
            <Listener>(name-of-the-listener)</Listener>
            <BackendAddressPool>(name-of-your-backend-pool)</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

<span data-ttu-id="70bf6-161">Edite os valores entre parênteses para os itens de configuração.</span><span class="sxs-lookup"><span data-stu-id="70bf6-161">Edit the values between the parentheses for the configuration items.</span></span> <span data-ttu-id="70bf6-162">Salve o arquivo com a extensão .xml.</span><span class="sxs-lookup"><span data-stu-id="70bf6-162">Save the file with extension .xml.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="70bf6-163">O item de protocolo Http ou Https diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="70bf6-163">The protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="70bf6-164">O exemplo a seguir mostra como usar um arquivo de configuração para configurar o gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="70bf6-164">The following example shows how to use a configuration file to set up the application gateway.</span></span> <span data-ttu-id="70bf6-165">A carga de exemplo equilibra o tráfego HTTP na porta pública 80 e envia o tráfego de rede para a porta 80 do back-end entre dois endereços IP.</span><span class="sxs-lookup"><span data-stu-id="70bf6-165">The example load balances HTTP traffic on public port 80 and sends network traffic to back-end port 80 between two IP addresses.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>80</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>BackendPool1</Name>
            <IPAddresses>
                <IPAddress>10.0.0.1</IPAddress>
                <IPAddress>10.0.0.2</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>BackendSetting1</Name>
            <Port>80</Port>
            <Protocol>Http</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>HTTPListener1</Name>
            <FrontendPort>FrontendPort1</FrontendPort>
            <Protocol>Http</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>HttpLBRule1</Name>
            <Type>basic</Type>
            <BackendHttpSettings>BackendSetting1</BackendHttpSettings>
            <Listener>HTTPListener1</Listener>
            <BackendAddressPool>BackendPool1</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

#### <a name="step-2"></a><span data-ttu-id="70bf6-166">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="70bf6-166">Step 2</span></span>

<span data-ttu-id="70bf6-167">Em seguida, defina o gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="70bf6-167">Next, set the application gateway.</span></span> <span data-ttu-id="70bf6-168">Use o cmdlet `Set-AzureApplicationGatewayConfig` com um arquivo XML de configuração.</span><span class="sxs-lookup"><span data-stu-id="70bf6-168">Use the `Set-AzureApplicationGatewayConfig` cmdlet with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile "D:\config.xml"
```

### <a name="configure-the-application-gateway-by-using-a-configuration-object"></a><span data-ttu-id="70bf6-169">Configurar o gateway de aplicativo usando um objeto de configuração</span><span class="sxs-lookup"><span data-stu-id="70bf6-169">Configure the application gateway by using a configuration object</span></span>

<span data-ttu-id="70bf6-170">O exemplo a seguir mostra como configurar o gateway de aplicativo usando objetos de configuração.</span><span class="sxs-lookup"><span data-stu-id="70bf6-170">The following example shows how to configure the application gateway by using configuration objects.</span></span> <span data-ttu-id="70bf6-171">Todos os itens de configuração devem ser configurados individualmente e, em seguida, adicionados a um objeto de configuração do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="70bf6-171">All configuration items must be configured individually and then added to an application gateway configuration object.</span></span> <span data-ttu-id="70bf6-172">Depois de criar o objeto de configuração, você usa o comando `Set-AzureApplicationGateway` para confirmar a configuração para o recurso do gateway de aplicativo criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="70bf6-172">After creating the configuration object, you use the `Set-AzureApplicationGateway` command to commit the configuration to the previously created application gateway resource.</span></span>

> [!NOTE]
> <span data-ttu-id="70bf6-173">Antes de atribuir um valor a cada objeto de configuração, você precisa declarar que tipo de objeto do PowerShell vai armazená-lo.</span><span class="sxs-lookup"><span data-stu-id="70bf6-173">Before assigning a value to each configuration object, you need to declare what kind of object PowerShell uses for storage.</span></span> <span data-ttu-id="70bf6-174">A primeira linha para criar os itens individuais define quais `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` serão usados.</span><span class="sxs-lookup"><span data-stu-id="70bf6-174">The first line to create the individual items defines what `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` are used.</span></span>

#### <a name="step-1"></a><span data-ttu-id="70bf6-175">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="70bf6-175">Step 1</span></span>

<span data-ttu-id="70bf6-176">Crie todos os itens de configuração individuais.</span><span class="sxs-lookup"><span data-stu-id="70bf6-176">Create all individual configuration items.</span></span>

<span data-ttu-id="70bf6-177">Crie o IP front-end, como mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="70bf6-177">Create the front-end IP as shown in the following example.</span></span>

```powershell
$fip = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration
$fip.Name = "fip1"
$fip.Type = "Private"
$fip.StaticIPAddress = "10.0.0.5"
```

<span data-ttu-id="70bf6-178">Crie a porta front-end, como mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="70bf6-178">Create the front-end port as shown in the following example.</span></span>

```powershell
$fep = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort
$fep.Name = "fep1"
$fep.Port = 80
```

<span data-ttu-id="70bf6-179">Crie o pool de servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="70bf6-179">Create the back-end server pool.</span></span>

<span data-ttu-id="70bf6-180">Defina os endereços IP que são adicionados ao pool de servidores back-end conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="70bf6-180">Define the IP addresses that are added to the back-end server pool as shown in the next example.</span></span>

```powershell
$servers = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendServerCollection
$servers.Add("10.0.0.1")
$servers.Add("10.0.0.2")
```

<span data-ttu-id="70bf6-181">Use o objeto $server para adicionar os valores ao objeto do pool de back-end ($pool).</span><span class="sxs-lookup"><span data-stu-id="70bf6-181">Use the $server object to add the values to the back-end pool object ($pool).</span></span>

```powershell
$pool = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool
$pool.BackendServers = $servers
$pool.Name = "pool1"
```

<span data-ttu-id="70bf6-182">Crie a configuração do pool de servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="70bf6-182">Create the back-end server pool setting.</span></span>

```powershell
$setting = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings
$setting.Name = "setting1"
$setting.CookieBasedAffinity = "enabled"
$setting.Port = 80
$setting.Protocol = "http"
```

<span data-ttu-id="70bf6-183">Crie o ouvinte.</span><span class="sxs-lookup"><span data-stu-id="70bf6-183">Create the listener.</span></span>

```powershell
$listener = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener
$listener.Name = "listener1"
$listener.FrontendPort = "fep1"
$listener.FrontendIP = "fip1"
$listener.Protocol = "http"
$listener.SslCert = ""
```

<span data-ttu-id="70bf6-184">Crie a regra.</span><span class="sxs-lookup"><span data-stu-id="70bf6-184">Create the rule.</span></span>

```powershell
$rule = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule
$rule.Name = "rule1"
$rule.Type = "basic"
$rule.BackendHttpSettings = "setting1"
$rule.Listener = "listener1"
$rule.BackendAddressPool = "pool1"
```

#### <a name="step-2"></a><span data-ttu-id="70bf6-185">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="70bf6-185">Step 2</span></span>

<span data-ttu-id="70bf6-186">Atribua todos os itens de configuração individuais a um objeto de configuração do gateway de aplicativo ($appgwconfig):</span><span class="sxs-lookup"><span data-stu-id="70bf6-186">Assign all individual configuration items to an application gateway configuration object ($appgwconfig).</span></span>

<span data-ttu-id="70bf6-187">Adicione o IP front-end à configuração.</span><span class="sxs-lookup"><span data-stu-id="70bf6-187">Add the front-end IP to the configuration.</span></span>

```powershell
$appgwconfig = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.ApplicationGatewayConfiguration
$appgwconfig.FrontendIPConfigurations = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration]"
$appgwconfig.FrontendIPConfigurations.Add($fip)
```

<span data-ttu-id="70bf6-188">Adicione a porta front-end à configuração.</span><span class="sxs-lookup"><span data-stu-id="70bf6-188">Add the front-end port to the configuration.</span></span>

```powershell
$appgwconfig.FrontendPorts = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort]"
$appgwconfig.FrontendPorts.Add($fep)
```
<span data-ttu-id="70bf6-189">Adicione o pool de servidores back-end à configuração.</span><span class="sxs-lookup"><span data-stu-id="70bf6-189">Add the back-end server pool to the configuration.</span></span>

```powershell
$appgwconfig.BackendAddressPools = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool]"
$appgwconfig.BackendAddressPools.Add($pool)
```

<span data-ttu-id="70bf6-190">Adicione a configuração do pool back-end à configuração.</span><span class="sxs-lookup"><span data-stu-id="70bf6-190">Add the back-end pool setting to the configuration.</span></span>

```powershell
$appgwconfig.BackendHttpSettingsList = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings]"
$appgwconfig.BackendHttpSettingsList.Add($setting)
```

<span data-ttu-id="70bf6-191">Adicione o ouvinte à configuração.</span><span class="sxs-lookup"><span data-stu-id="70bf6-191">Add the listener to the configuration.</span></span>

```powershell
$appgwconfig.HttpListeners = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener]"
$appgwconfig.HttpListeners.Add($listener)
```

<span data-ttu-id="70bf6-192">Adicione a regra à configuração.</span><span class="sxs-lookup"><span data-stu-id="70bf6-192">Add the rule to the configuration.</span></span>

```powershell
$appgwconfig.HttpLoadBalancingRules = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule]"
$appgwconfig.HttpLoadBalancingRules.Add($rule)
```

### <a name="step-3"></a><span data-ttu-id="70bf6-193">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="70bf6-193">Step 3</span></span>
<span data-ttu-id="70bf6-194">Confirme o objeto de configuração do recurso do gateway de aplicativo usando `Set-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="70bf6-194">Commit the configuration object to the application gateway resource by using `Set-AzureApplicationGatewayConfig`.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -Config $appgwconfig
```

## <a name="start-the-gateway"></a><span data-ttu-id="70bf6-195">Iniciar o gateway</span><span class="sxs-lookup"><span data-stu-id="70bf6-195">Start the gateway</span></span>

<span data-ttu-id="70bf6-196">Depois que o gateway tiver sido configurado, use o cmdlet `Start-AzureApplicationGateway` para iniciá-lo.</span><span class="sxs-lookup"><span data-stu-id="70bf6-196">Once the gateway has been configured, use the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span></span> <span data-ttu-id="70bf6-197">A cobrança por um gateway de aplicativo começa depois que o gateway tiver sido iniciado com êxito.</span><span class="sxs-lookup"><span data-stu-id="70bf6-197">Billing for an application gateway begins after the gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="70bf6-198">O cmdlet `Start-AzureApplicationGateway` poderá levar até 15 a 20 minutos para terminar.</span><span class="sxs-lookup"><span data-stu-id="70bf6-198">The `Start-AzureApplicationGateway` cmdlet might take up to 15-20 minutes to finish.</span></span>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-the-gateway-status"></a><span data-ttu-id="70bf6-199">Verificar o status do gateway</span><span class="sxs-lookup"><span data-stu-id="70bf6-199">Verify the gateway status</span></span>

<span data-ttu-id="70bf6-200">Use o cmdlet `Get-AzureApplicationGateway` para verificar o status do gateway.</span><span class="sxs-lookup"><span data-stu-id="70bf6-200">Use the `Get-AzureApplicationGateway` cmdlet to check the status of the gateway.</span></span> <span data-ttu-id="70bf6-201">Se `Start-AzureApplicationGateway` tiver sido bem-sucedido na etapa anterior, o item *Estado* deverá estar Em execução e *Vip* e *DnsName* deverão ter entradas válidas.</span><span class="sxs-lookup"><span data-stu-id="70bf6-201">If `Start-AzureApplicationGateway` succeeded in the previous step, *State* should be Running, and *Vip* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="70bf6-202">Este exemplo mostra um gateway de aplicativo que está ativo, em execução e pronto para assumir o tráfego destinado a `http://<generated-dns-name>.cloudapp.net`.</span><span class="sxs-lookup"><span data-stu-id="70bf6-202">The following example shows an application gateway that is up, running, and ready to take traffic destined for `http://<generated-dns-name>.cloudapp.net`.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 8:09:28 PM - Begin Operation: Get-AzureApplicationGateway
VERBOSE: 8:09:30 PM - Completed Operation: Get-AzureApplicationGateway
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
Vip           : 138.91.170.26
DnsName       : appgw-1b8402e8-3e0d-428d-b661-289c16c82101.cloudapp.net
```

## <a name="delete-the-application-gateway"></a><span data-ttu-id="70bf6-203">Excluir o gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="70bf6-203">Delete the application gateway</span></span>

<span data-ttu-id="70bf6-204">Para excluir o gateway de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="70bf6-204">To delete the application gateway:</span></span>

1. <span data-ttu-id="70bf6-205">Use o cmdlet `Stop-AzureApplicationGateway` para parar o gateway.</span><span class="sxs-lookup"><span data-stu-id="70bf6-205">Use the `Stop-AzureApplicationGateway` cmdlet to stop the gateway.</span></span>
2. <span data-ttu-id="70bf6-206">Use o cmdlet `Remove-AzureApplicationGateway` para remover o gateway.</span><span class="sxs-lookup"><span data-stu-id="70bf6-206">Use the `Remove-AzureApplicationGateway` cmdlet to remove the gateway.</span></span>
3. <span data-ttu-id="70bf6-207">Verifique se o gateway foi removido usando o cmdlet `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="70bf6-207">Verify that the gateway has been removed by using the `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="70bf6-208">O exemplo a seguir mostra o cmdlet `Stop-AzureApplicationGateway` na primeira linha, seguido pela saída.</span><span class="sxs-lookup"><span data-stu-id="70bf6-208">The following example shows the `Stop-AzureApplicationGateway` cmdlet on the first line, followed by the output.</span></span>

```powershell
Stop-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

<span data-ttu-id="70bf6-209">Depois que o gateway de aplicativo estiver em um estado parado, use o cmdlet `Remove-AzureApplicationGateway` para remover o serviço.</span><span class="sxs-lookup"><span data-stu-id="70bf6-209">Once the application gateway is in a stopped state, use the `Remove-AzureApplicationGateway` cmdlet to remove the service.</span></span>

```powershell
Remove-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

<span data-ttu-id="70bf6-210">Para verificar se o serviço foi removido, você pode usar o cmdlet `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="70bf6-210">To verify that the service has been removed, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span> <span data-ttu-id="70bf6-211">Essa etapa não é necessária.</span><span class="sxs-lookup"><span data-stu-id="70bf6-211">This step is not required.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: The gateway does not exist.
.....
```

## <a name="next-steps"></a><span data-ttu-id="70bf6-212">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="70bf6-212">Next steps</span></span>

<span data-ttu-id="70bf6-213">Se desejar configurar o descarregamento SSL, confira [Configurar um application gateway para descarregamento SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="70bf6-213">If you want to configure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="70bf6-214">Para configurar um gateway de aplicativo para usar com um balanceador de carga interno, confira [Criar um gateway de aplicativo com um ILB (balanceador de carga interno)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="70bf6-214">If you want to configure an application gateway to use with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="70bf6-215">Se deseja obter mais informações sobre as opções de balanceamento de carga no geral, consulte:</span><span class="sxs-lookup"><span data-stu-id="70bf6-215">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="70bf6-216">Balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="70bf6-216">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="70bf6-217">Gerenciador de Tráfego do Azure</span><span class="sxs-lookup"><span data-stu-id="70bf6-217">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

[scenario]: ./media/application-gateway-create-gateway/scenario.png
