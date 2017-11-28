---
title: aaaCreate, iniciar ou excluir um application gateway | Microsoft Docs
description: "Esta página fornece instruções toocreate, configurar, iniciar e excluir um gateway de aplicativo do Azure"
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
ms.openlocfilehash: 3efef5b49880c9efdafad8b88d4bce5b749b82af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-with-powershell"></a><span data-ttu-id="70b27-103">Criar, iniciar ou excluir um gateway de aplicativo com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="70b27-103">Create, start, or delete an application gateway with PowerShell</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="70b27-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="70b27-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="70b27-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="70b27-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="70b27-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="70b27-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="70b27-107">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="70b27-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="70b27-108">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="70b27-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="70b27-109">O Gateway de Aplicativo do Azure é um balanceador de carga de camada 7.</span><span class="sxs-lookup"><span data-stu-id="70b27-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="70b27-110">Ele fornece failover, o roteamento de desempenho de solicitações HTTP entre diferentes servidores, independentemente de estarem em nuvem hello ou local.</span><span class="sxs-lookup"><span data-stu-id="70b27-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="70b27-111">O Gateway de Aplicativo fornece muitos recursos do ADC (Controlador de Entrega de Aplicativos), incluindo o balanceamento de carga de HTTP, a afinidade de sessão baseada em cookies, o descarregamento de SSL (Secure Sockets Layer), as sondas de integridade personalizadas, suporte para vários sites e muitos outros.</span><span class="sxs-lookup"><span data-stu-id="70b27-111">Application Gateway provides many Application Delivery Controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="70b27-112">toofind uma lista completa de recursos com suporte, visite [visão geral do Application Gateway](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="70b27-112">toofind a complete list of supported features, visit [Application Gateway Overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="70b27-113">Este artigo orienta Olá etapas toocreate, configurar, iniciar e excluir um application gateway.</span><span class="sxs-lookup"><span data-stu-id="70b27-113">This article walks you through hello steps toocreate, configure, start, and delete an application gateway.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="70b27-114">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="70b27-114">Before you begin</span></span>

1. <span data-ttu-id="70b27-115">Instale a versão mais recente Olá Olá Azure de cmdlets do PowerShell usando Olá Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="70b27-115">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="70b27-116">Você pode baixar e instalar a versão mais recente de saudação do hello **do Windows PowerShell** seção Olá [página de Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="70b27-116">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="70b27-117">Se você tiver uma rede virtual existente, selecione uma sub-rede vazia existente ou criar uma nova sub-rede na rede virtual existente unicamente para uso pelo gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="70b27-117">If you have an existing virtual network, either select an existing empty subnet or create a new subnet in your existing virtual network solely for use by hello application gateway.</span></span> <span data-ttu-id="70b27-118">Não é possível implantar Olá application gateway tooa rede virtual diferente de recursos de saudação pretende toodeploy por trás do gateway de aplicativo hello, a menos que o emparelhamento de rede virtual é usado.</span><span class="sxs-lookup"><span data-stu-id="70b27-118">You cannot deploy hello application gateway tooa different virtual network than hello resources you intend toodeploy behind hello application gateway unless vnet peering is used.</span></span> <span data-ttu-id="70b27-119">toolearn mais visitar [emparelhamento de rede virtual](../virtual-network/virtual-network-peering-overview.md)</span><span class="sxs-lookup"><span data-stu-id="70b27-119">toolearn more visit [Vnet Peering](../virtual-network/virtual-network-peering-overview.md)</span></span>
3. <span data-ttu-id="70b27-120">Verifique se você tem uma rede virtual em funcionamento com uma sub-rede válida.</span><span class="sxs-lookup"><span data-stu-id="70b27-120">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="70b27-121">Certifique-se de que não há máquinas ou implantações de nuvem usando sub-rede hello.</span><span class="sxs-lookup"><span data-stu-id="70b27-121">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="70b27-122">gateway de aplicativo Hello deve ser sozinho em uma sub-rede de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="70b27-122">hello application gateway must be by itself in a virtual network subnet.</span></span>
4. <span data-ttu-id="70b27-123">servidores de saudação que você configure o gateway de aplicativo hello toouse devem existir ou seus pontos de extremidade criados na rede virtual hello ou com um IP público/VIP atribuídos.</span><span class="sxs-lookup"><span data-stu-id="70b27-123">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="70b27-124">O que é necessário toocreate um application gateway?</span><span class="sxs-lookup"><span data-stu-id="70b27-124">What is required toocreate an application gateway?</span></span>

<span data-ttu-id="70b27-125">Quando você usa Olá `New-AzureApplicationGateway` gateway de aplicativo do comando toocreate hello, nenhuma configuração é definida neste momento e recurso Olá recém-criado são configuradas usando XML ou um objeto de configuração.</span><span class="sxs-lookup"><span data-stu-id="70b27-125">When you use hello `New-AzureApplicationGateway` command toocreate hello application gateway, no configuration is set at this point and hello newly created resource are configured either by using XML or a configuration object.</span></span>

<span data-ttu-id="70b27-126">Olá valores são:</span><span class="sxs-lookup"><span data-stu-id="70b27-126">hello values are:</span></span>

* <span data-ttu-id="70b27-127">**Pool de servidores de back-end:** lista de saudação de endereços IP dos servidores de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="70b27-127">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="70b27-128">endereços IP Hello listado ou devem pertencer a sub-rede da rede virtual toohello ou devem ser um IP público/VIP.</span><span class="sxs-lookup"><span data-stu-id="70b27-128">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="70b27-129">**Configurações do pool de servidores back-end:** cada pool tem configurações como porta, protocolo e afinidade baseada em cookie.</span><span class="sxs-lookup"><span data-stu-id="70b27-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="70b27-130">Essas configurações são tooa empatado pool e são aplicados tooall servidores no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="70b27-130">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="70b27-131">**Porta de front-end:** essa porta é a porta pública de saudação que é aberta no gateway do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="70b27-131">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="70b27-132">Tráfego atinge essa porta e, em seguida, obtém redirecionado tooone de servidores de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="70b27-132">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="70b27-133">**Ouvinte:** ouvinte Olá tem uma porta de front-end, um protocolo (Http ou Https, esses valores diferenciam maiusculas de minúsculas) e o nome do certificado SSL de saudação (se a configuração de SSL de descarregamento).</span><span class="sxs-lookup"><span data-stu-id="70b27-133">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="70b27-134">**Regra:** regra Olá associa ouvinte hello e pool de saudação do servidor de back-end e define o tráfego de saudação do pool de servidor back-end deve ser direcionado toowhen que ele atinja um ouvinte específico.</span><span class="sxs-lookup"><span data-stu-id="70b27-134">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="70b27-135">Criar um Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="70b27-135">Create an application gateway</span></span>

<span data-ttu-id="70b27-136">toocreate um application gateway:</span><span class="sxs-lookup"><span data-stu-id="70b27-136">toocreate an application gateway:</span></span>

1. <span data-ttu-id="70b27-137">Criar um recurso de gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="70b27-137">Create an application gateway resource.</span></span>
2. <span data-ttu-id="70b27-138">Crie um arquivo XML de configuração ou um objeto de configuração.</span><span class="sxs-lookup"><span data-stu-id="70b27-138">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="70b27-139">Confirme Olá configuração toohello recém-criados em recursos de gateway do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="70b27-139">Commit hello configuration toohello newly created application gateway resource.</span></span>

> [!NOTE]
> <span data-ttu-id="70b27-140">Se você precisar tooconfigure uma investigação personalizada para o gateway de aplicativo, consulte [criar um gateway de aplicativos com testes personalizados usando o PowerShell](application-gateway-create-probe-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="70b27-140">If you need tooconfigure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-classic-ps.md).</span></span> <span data-ttu-id="70b27-141">Confira [investigações personalizadas e monitoramento de integridade](application-gateway-probe-overview.md) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="70b27-141">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

![Cenário de exemplo][scenario]

### <a name="create-an-application-gateway-resource"></a><span data-ttu-id="70b27-143">Criar um recurso do gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="70b27-143">Create an application gateway resource</span></span>

<span data-ttu-id="70b27-144">gateway toocreate Olá Olá use `New-AzureApplicationGateway` cmdlet, substituindo os valores hello com seus próprios.</span><span class="sxs-lookup"><span data-stu-id="70b27-144">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="70b27-145">Cobrança para o gateway de saudação não funciona neste momento.</span><span class="sxs-lookup"><span data-stu-id="70b27-145">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="70b27-146">A cobrança começa em uma etapa posterior, quando o gateway Olá foi iniciado com êxito.</span><span class="sxs-lookup"><span data-stu-id="70b27-146">Billing begins in a later step, when hello gateway is successfully started.</span></span>

<span data-ttu-id="70b27-147">Olá exemplo a seguir cria um application gateway usando uma rede virtual chamada "testvnet1" e uma sub-rede denominada "subnet-1":</span><span class="sxs-lookup"><span data-stu-id="70b27-147">hello following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1":</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="70b27-148">*Description*, *InstanceCount* e *GatewaySize* são parâmetros opcionais.</span><span class="sxs-lookup"><span data-stu-id="70b27-148">*Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span>

<span data-ttu-id="70b27-149">toovalidate que Olá gateway foi criado, você pode usar o hello `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="70b27-149">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

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
> <span data-ttu-id="70b27-150">Olá valor padrão para *InstanceCount* é 2, com um valor máximo de 10.</span><span class="sxs-lookup"><span data-stu-id="70b27-150">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="70b27-151">Olá valor padrão para *GatewaySize* é médio.</span><span class="sxs-lookup"><span data-stu-id="70b27-151">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="70b27-152">Você pode escolher entre Small, Medium e Large.</span><span class="sxs-lookup"><span data-stu-id="70b27-152">You can choose between Small, Medium and Large.</span></span>

<span data-ttu-id="70b27-153">*VirtualIPs* e *DnsName* são mostrados como em branco porque o gateway Olá ainda não foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="70b27-153">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="70b27-154">Eles são criados depois que o gateway de hello está em estado de execução de saudação.</span><span class="sxs-lookup"><span data-stu-id="70b27-154">These are created once hello gateway is in hello running state.</span></span>

## <a name="configure-hello-application-gateway"></a><span data-ttu-id="70b27-155">Configurar o gateway de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="70b27-155">Configure hello application gateway</span></span>

<span data-ttu-id="70b27-156">Você pode configurar o gateway de aplicativo hello usando XML ou um objeto de configuração.</span><span class="sxs-lookup"><span data-stu-id="70b27-156">You can configure hello application gateway by using XML or a configuration object.</span></span>

### <a name="configure-hello-application-gateway-by-using-xml"></a><span data-ttu-id="70b27-157">Configurar o gateway de aplicativo hello usando XML</span><span class="sxs-lookup"><span data-stu-id="70b27-157">Configure hello application gateway by using XML</span></span>

<span data-ttu-id="70b27-158">Em Olá exemplo a seguir, use um tooconfigure do arquivo XML todas as configurações de gateway do aplicativo e confirmá-las toohello recursos de gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="70b27-158">In hello following example, you use an XML file tooconfigure all application gateway settings and commit them toohello application gateway resource.</span></span>  

#### <a name="step-1"></a><span data-ttu-id="70b27-159">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="70b27-159">Step 1</span></span>

<span data-ttu-id="70b27-160">Saudação de cópia tooNotepad de texto a seguir.</span><span class="sxs-lookup"><span data-stu-id="70b27-160">Copy hello following text tooNotepad.</span></span>

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

<span data-ttu-id="70b27-161">Edite valores de saudação entre parênteses Olá Olá para itens de configuração.</span><span class="sxs-lookup"><span data-stu-id="70b27-161">Edit hello values between hello parentheses for hello configuration items.</span></span> <span data-ttu-id="70b27-162">Salve o arquivo de saudação com extensão. XML.</span><span class="sxs-lookup"><span data-stu-id="70b27-162">Save hello file with extension .xml.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="70b27-163">item de protocolo Hello Http ou Https diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="70b27-163">hello protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="70b27-164">saudação de exemplo a seguir mostra como toouse uma configuração de arquivo tooset o gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="70b27-164">hello following example shows how toouse a configuration file tooset up hello application gateway.</span></span> <span data-ttu-id="70b27-165">carga de exemplo Hello balanceia o tráfego HTTP na porta pública 80 e envia o tráfego de rede a porta 80 tooback ponta entre dois endereços IP.</span><span class="sxs-lookup"><span data-stu-id="70b27-165">hello example load balances HTTP traffic on public port 80 and sends network traffic tooback-end port 80 between two IP addresses.</span></span>

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

#### <a name="step-2"></a><span data-ttu-id="70b27-166">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="70b27-166">Step 2</span></span>

<span data-ttu-id="70b27-167">Em seguida, configure o gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="70b27-167">Next, set hello application gateway.</span></span> <span data-ttu-id="70b27-168">Saudação de uso `Set-AzureApplicationGatewayConfig` cmdlet com um arquivo XML de configuração.</span><span class="sxs-lookup"><span data-stu-id="70b27-168">Use hello `Set-AzureApplicationGatewayConfig` cmdlet with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile "D:\config.xml"
```

### <a name="configure-hello-application-gateway-by-using-a-configuration-object"></a><span data-ttu-id="70b27-169">Configurar o gateway de aplicativo hello usando um objeto de configuração</span><span class="sxs-lookup"><span data-stu-id="70b27-169">Configure hello application gateway by using a configuration object</span></span>

<span data-ttu-id="70b27-170">saudação de exemplo a seguir mostra como tooconfigure Olá gateway de aplicativo por meio de objetos de configuração.</span><span class="sxs-lookup"><span data-stu-id="70b27-170">hello following example shows how tooconfigure hello application gateway by using configuration objects.</span></span> <span data-ttu-id="70b27-171">Todos os itens de configuração devem ser configurados individualmente e, em seguida, adicionar objeto de configuração do tooan application gateway.</span><span class="sxs-lookup"><span data-stu-id="70b27-171">All configuration items must be configured individually and then added tooan application gateway configuration object.</span></span> <span data-ttu-id="70b27-172">Depois de criar o objeto de configuração hello, você usar Olá `Set-AzureApplicationGateway` comando toocommit Olá configuração toohello criado anteriormente o recurso do application gateway.</span><span class="sxs-lookup"><span data-stu-id="70b27-172">After creating hello configuration object, you use hello `Set-AzureApplicationGateway` command toocommit hello configuration toohello previously created application gateway resource.</span></span>

> [!NOTE]
> <span data-ttu-id="70b27-173">Antes de atribuir um objeto de configuração do valor tooeach, é necessário toodeclare que tipo de objeto PowerShell usa para armazenamento.</span><span class="sxs-lookup"><span data-stu-id="70b27-173">Before assigning a value tooeach configuration object, you need toodeclare what kind of object PowerShell uses for storage.</span></span> <span data-ttu-id="70b27-174">itens individuais do Hello primeira linha toocreate Olá define quais `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` são usados.</span><span class="sxs-lookup"><span data-stu-id="70b27-174">hello first line toocreate hello individual items defines what `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` are used.</span></span>

#### <a name="step-1"></a><span data-ttu-id="70b27-175">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="70b27-175">Step 1</span></span>

<span data-ttu-id="70b27-176">Crie todos os itens de configuração individuais.</span><span class="sxs-lookup"><span data-stu-id="70b27-176">Create all individual configuration items.</span></span>

<span data-ttu-id="70b27-177">Crie IP de front-end hello, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="70b27-177">Create hello front-end IP as shown in hello following example.</span></span>

```powershell
$fip = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration
$fip.Name = "fip1"
$fip.Type = "Private"
$fip.StaticIPAddress = "10.0.0.5"
```

<span data-ttu-id="70b27-178">Crie a porta de front-end Olá conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="70b27-178">Create hello front-end port as shown in hello following example.</span></span>

```powershell
$fep = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort
$fep.Name = "fep1"
$fep.Port = 80
```

<span data-ttu-id="70b27-179">Crie pool de saudação do servidor de back-end.</span><span class="sxs-lookup"><span data-stu-id="70b27-179">Create hello back-end server pool.</span></span>

<span data-ttu-id="70b27-180">Defina Olá endereços IP que são adicionados o pool de servidores de back-end do toohello conforme mostrado no exemplo a seguir hello.</span><span class="sxs-lookup"><span data-stu-id="70b27-180">Define hello IP addresses that are added toohello back-end server pool as shown in hello next example.</span></span>

```powershell
$servers = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendServerCollection
$servers.Add("10.0.0.1")
$servers.Add("10.0.0.2")
```

<span data-ttu-id="70b27-181">Use Olá $server tooadd Olá valores toohello pool de back-end de objeto ($pool).</span><span class="sxs-lookup"><span data-stu-id="70b27-181">Use hello $server object tooadd hello values toohello back-end pool object ($pool).</span></span>

```powershell
$pool = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool
$pool.BackendServers = $servers
$pool.Name = "pool1"
```

<span data-ttu-id="70b27-182">Crie a configuração de pool do servidor back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="70b27-182">Create hello back-end server pool setting.</span></span>

```powershell
$setting = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings
$setting.Name = "setting1"
$setting.CookieBasedAffinity = "enabled"
$setting.Port = 80
$setting.Protocol = "http"
```

<span data-ttu-id="70b27-183">Crie um ouvinte de saudação.</span><span class="sxs-lookup"><span data-stu-id="70b27-183">Create hello listener.</span></span>

```powershell
$listener = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener
$listener.Name = "listener1"
$listener.FrontendPort = "fep1"
$listener.FrontendIP = "fip1"
$listener.Protocol = "http"
$listener.SslCert = ""
```

<span data-ttu-id="70b27-184">Crie regra de saudação.</span><span class="sxs-lookup"><span data-stu-id="70b27-184">Create hello rule.</span></span>

```powershell
$rule = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule
$rule.Name = "rule1"
$rule.Type = "basic"
$rule.BackendHttpSettings = "setting1"
$rule.Listener = "listener1"
$rule.BackendAddressPool = "pool1"
```

#### <a name="step-2"></a><span data-ttu-id="70b27-185">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="70b27-185">Step 2</span></span>

<span data-ttu-id="70b27-186">Atribua todas as configuração individual itens tooan aplicativo gateway configuração objeto ($appgwconfig).</span><span class="sxs-lookup"><span data-stu-id="70b27-186">Assign all individual configuration items tooan application gateway configuration object ($appgwconfig).</span></span>

<span data-ttu-id="70b27-187">Adicione configuração de toohello IP de front-end hello.</span><span class="sxs-lookup"><span data-stu-id="70b27-187">Add hello front-end IP toohello configuration.</span></span>

```powershell
$appgwconfig = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.ApplicationGatewayConfiguration
$appgwconfig.FrontendIPConfigurations = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration]"
$appgwconfig.FrontendIPConfigurations.Add($fip)
```

<span data-ttu-id="70b27-188">Adicione configuração de toohello de porta de front-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="70b27-188">Add hello front-end port toohello configuration.</span></span>

```powershell
$appgwconfig.FrontendPorts = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort]"
$appgwconfig.FrontendPorts.Add($fep)
```
<span data-ttu-id="70b27-189">Adicione configuração de toohello do pool de servidor back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="70b27-189">Add hello back-end server pool toohello configuration.</span></span>

```powershell
$appgwconfig.BackendAddressPools = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool]"
$appgwconfig.BackendAddressPools.Add($pool)
```

<span data-ttu-id="70b27-190">Adicione toohello configuração de pool de back-end do hello.</span><span class="sxs-lookup"><span data-stu-id="70b27-190">Add hello back-end pool setting toohello configuration.</span></span>

```powershell
$appgwconfig.BackendHttpSettingsList = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings]"
$appgwconfig.BackendHttpSettingsList.Add($setting)
```

<span data-ttu-id="70b27-191">Adicione configuração de toohello Olá ouvinte.</span><span class="sxs-lookup"><span data-stu-id="70b27-191">Add hello listener toohello configuration.</span></span>

```powershell
$appgwconfig.HttpListeners = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener]"
$appgwconfig.HttpListeners.Add($listener)
```

<span data-ttu-id="70b27-192">Adicione configuração da regra de saudação toohello.</span><span class="sxs-lookup"><span data-stu-id="70b27-192">Add hello rule toohello configuration.</span></span>

```powershell
$appgwconfig.HttpLoadBalancingRules = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule]"
$appgwconfig.HttpLoadBalancingRules.Add($rule)
```

### <a name="step-3"></a><span data-ttu-id="70b27-193">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="70b27-193">Step 3</span></span>
<span data-ttu-id="70b27-194">Confirme o recurso de gateway de aplicativo hello configuração objeto toohello usando `Set-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="70b27-194">Commit hello configuration object toohello application gateway resource by using `Set-AzureApplicationGatewayConfig`.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -Config $appgwconfig
```

## <a name="start-hello-gateway"></a><span data-ttu-id="70b27-195">Gateway de saudação inicial</span><span class="sxs-lookup"><span data-stu-id="70b27-195">Start hello gateway</span></span>

<span data-ttu-id="70b27-196">Uma vez configurado o gateway hello, use Olá `Start-AzureApplicationGateway` gateway de saudação do cmdlet toostart.</span><span class="sxs-lookup"><span data-stu-id="70b27-196">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="70b27-197">A cobrança por um application gateway iniciado após a saudação gateway foi iniciado com êxito.</span><span class="sxs-lookup"><span data-stu-id="70b27-197">Billing for an application gateway begins after hello gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="70b27-198">Olá `Start-AzureApplicationGateway` cmdlet pode levar até toofinish too15 a 20 minutos.</span><span class="sxs-lookup"><span data-stu-id="70b27-198">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toofinish.</span></span>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="70b27-199">Verificar status do gateway Olá</span><span class="sxs-lookup"><span data-stu-id="70b27-199">Verify hello gateway status</span></span>

<span data-ttu-id="70b27-200">Saudação de uso `Get-AzureApplicationGateway` status de saudação do cmdlet toocheck do gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="70b27-200">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of hello gateway.</span></span> <span data-ttu-id="70b27-201">Se `Start-AzureApplicationGateway` com êxito na etapa anterior de saudação, *estado* devem estar em execução, e *Vip* e *DnsName* devem ter entradas válidas.</span><span class="sxs-lookup"><span data-stu-id="70b27-201">If `Start-AzureApplicationGateway` succeeded in hello previous step, *State* should be Running, and *Vip* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="70b27-202">Olá, exemplo a seguir mostra um application gateway é para cima, em execução, e tootake pronto tráfego destinado a `http://<generated-dns-name>.cloudapp.net`.</span><span class="sxs-lookup"><span data-stu-id="70b27-202">hello following example shows an application gateway that is up, running, and ready tootake traffic destined for `http://<generated-dns-name>.cloudapp.net`.</span></span>

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

## <a name="delete-hello-application-gateway"></a><span data-ttu-id="70b27-203">Excluir o hello application gateway</span><span class="sxs-lookup"><span data-stu-id="70b27-203">Delete hello application gateway</span></span>

<span data-ttu-id="70b27-204">gateway de aplicativo hello toodelete:</span><span class="sxs-lookup"><span data-stu-id="70b27-204">toodelete hello application gateway:</span></span>

1. <span data-ttu-id="70b27-205">Saudação de uso `Stop-AzureApplicationGateway` gateway de saudação do cmdlet toostop.</span><span class="sxs-lookup"><span data-stu-id="70b27-205">Use hello `Stop-AzureApplicationGateway` cmdlet toostop hello gateway.</span></span>
2. <span data-ttu-id="70b27-206">Saudação de uso `Remove-AzureApplicationGateway` gateway de saudação do cmdlet tooremove.</span><span class="sxs-lookup"><span data-stu-id="70b27-206">Use hello `Remove-AzureApplicationGateway` cmdlet tooremove hello gateway.</span></span>
3. <span data-ttu-id="70b27-207">Verificar gateway Olá foi removido usando Olá `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="70b27-207">Verify that hello gateway has been removed by using hello `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="70b27-208">Olá, exemplo a seguir mostra Olá `Stop-AzureApplicationGateway` cmdlet na primeira linha de saudação, seguido pela saída de hello.</span><span class="sxs-lookup"><span data-stu-id="70b27-208">hello following example shows hello `Stop-AzureApplicationGateway` cmdlet on hello first line, followed by hello output.</span></span>

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

<span data-ttu-id="70b27-209">Depois que o gateway de aplicativo hello está em um estado parado, use Olá `Remove-AzureApplicationGateway` serviço de saudação do cmdlet tooremove.</span><span class="sxs-lookup"><span data-stu-id="70b27-209">Once hello application gateway is in a stopped state, use hello `Remove-AzureApplicationGateway` cmdlet tooremove hello service.</span></span>

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

<span data-ttu-id="70b27-210">tooverify que Olá serviço foi removido, você pode usar o hello `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="70b27-210">tooverify that hello service has been removed, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span> <span data-ttu-id="70b27-211">Essa etapa não é necessária.</span><span class="sxs-lookup"><span data-stu-id="70b27-211">This step is not required.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
.....
```

## <a name="next-steps"></a><span data-ttu-id="70b27-212">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="70b27-212">Next steps</span></span>

<span data-ttu-id="70b27-213">Se você quiser tooconfigure descarregamento de SSL, consulte [Configure um gateway de aplicativo para descarregamento SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="70b27-213">If you want tooconfigure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="70b27-214">Se você quiser tooconfigure um toouse de gateway do aplicativo com um balanceador de carga interno, consulte [criar um gateway de aplicativo com um balanceador de carga interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="70b27-214">If you want tooconfigure an application gateway toouse with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="70b27-215">Se deseja obter mais informações sobre as opções de balanceamento de carga no geral, consulte:</span><span class="sxs-lookup"><span data-stu-id="70b27-215">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="70b27-216">Balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="70b27-216">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="70b27-217">Gerenciador de Tráfego do Azure</span><span class="sxs-lookup"><span data-stu-id="70b27-217">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

[scenario]: ./media/application-gateway-create-gateway/scenario.png
