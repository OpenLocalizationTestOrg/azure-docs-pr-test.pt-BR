---
title: Gateway de aplicativo do Azure com o balanceador de carga interno de aaaUsing | Microsoft Docs
description: "Esta página fornece instruções tooconfigure um Gateway de aplicativo do Azure com um ponto de extremidade com balanceamento de carga interno"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 7403d28e-909f-46a2-b282-43a8e942f53c
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 272ef84a02f92a8521c35aad6f1d9f9bf1675718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a><span data-ttu-id="1523f-103">Criar um Gateway de Aplicativo com um ILB (Balanceador de Carga Interno)</span><span class="sxs-lookup"><span data-stu-id="1523f-103">Create an Application Gateway with an Internal Load Balancer (ILB)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1523f-104">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="1523f-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="1523f-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1523f-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="1523f-106">Application Gateway pode ser configurado com um IP virtual da internet ou com um toohello de ponto de extremidade interno não exposto à internet, também conhecido como ponto de extremidade de Balanceador de carga interno (ILB).</span><span class="sxs-lookup"><span data-stu-id="1523f-106">Application Gateway can be configured with an internet facing virtual IP or with an internal end-point not exposed toohello internet, also known as Internal Load Balancer (ILB) endpoint.</span></span> <span data-ttu-id="1523f-107">Configurar gateway Olá com um ILB é útil para aplicativos de linha de negócios internos não expostos toointernet.</span><span class="sxs-lookup"><span data-stu-id="1523f-107">Configuring hello gateway with an ILB is useful for internal line-of-business applications not exposed toointernet.</span></span> <span data-ttu-id="1523f-108">Também é útil para camadas de serviço/dentro de um aplicativo de várias camada, que se encontra em um toointernet de limite não exposta de segurança, mas ainda requerem a distribuição de carga de round robin, persistência de sessão ou terminação SSL.</span><span class="sxs-lookup"><span data-stu-id="1523f-108">It's also useful for services/tiers within a multi-tier application, which sits in a security boundary not exposed toointernet, but still require round robin load distribution, session stickiness, or SSL termination.</span></span> <span data-ttu-id="1523f-109">Este artigo orienta Olá etapas tooconfigure um application gateway com um ILB.</span><span class="sxs-lookup"><span data-stu-id="1523f-109">This article walks you through hello steps tooconfigure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1523f-110">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="1523f-110">Before you begin</span></span>

1. <span data-ttu-id="1523f-111">Instale a versão mais recente dos cmdlets do PowerShell do Azure hello usando Olá Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="1523f-111">Install latest version of hello Azure PowerShell cmdlets using hello Web Platform Installer.</span></span> <span data-ttu-id="1523f-112">Você pode baixar e instalar a versão mais recente de saudação do hello **do Windows PowerShell** seção Olá [página de Download](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="1523f-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Download page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="1523f-113">Verifique se você tem uma rede virtual em funcionamento com uma sub-rede válida.</span><span class="sxs-lookup"><span data-stu-id="1523f-113">Verify that you have a working virtual network with valid subnet.</span></span>
3. <span data-ttu-id="1523f-114">Verifique se você tem servidores de back-end na rede virtual hello, ou com um IP público/VIP atribuído.</span><span class="sxs-lookup"><span data-stu-id="1523f-114">Verify that you have backend servers either in hello virtual network, or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="1523f-115">toocreate um application gateway, execute Olá etapas na ordem Olá listados a seguir.</span><span class="sxs-lookup"><span data-stu-id="1523f-115">toocreate an application gateway, perform hello following steps in hello order listed.</span></span> 

1. [<span data-ttu-id="1523f-116">Criar um Application Gateway</span><span class="sxs-lookup"><span data-stu-id="1523f-116">Create an application gateway</span></span>](#create-a-new-application-gateway)
2. [<span data-ttu-id="1523f-117">Configurar o gateway de saudação</span><span class="sxs-lookup"><span data-stu-id="1523f-117">Configure hello gateway</span></span>](#configure-the-gateway)
3. [<span data-ttu-id="1523f-118">Configuração de gateway de saudação do conjunto</span><span class="sxs-lookup"><span data-stu-id="1523f-118">Set hello gateway configuration</span></span>](#set-the-gateway-configuration)
4. [<span data-ttu-id="1523f-119">Gateway de saudação inicial</span><span class="sxs-lookup"><span data-stu-id="1523f-119">Start hello gateway</span></span>](#start-the-gateway)
5. [<span data-ttu-id="1523f-120">Verifique se o gateway de saudação</span><span class="sxs-lookup"><span data-stu-id="1523f-120">Verify hello gateway</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="1523f-121">Criar um Application Gateway:</span><span class="sxs-lookup"><span data-stu-id="1523f-121">Create an application gateway:</span></span>

<span data-ttu-id="1523f-122">**gateway de saudação toocreate**, use Olá `New-AzureApplicationGateway` cmdlet, substituindo os valores hello com seus próprios.</span><span class="sxs-lookup"><span data-stu-id="1523f-122">**toocreate hello gateway**, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="1523f-123">Observe que a cobrança por gateway Olá não iniciam neste momento.</span><span class="sxs-lookup"><span data-stu-id="1523f-123">Note that billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="1523f-124">A cobrança começa em uma etapa posterior, quando o gateway Olá foi iniciado com êxito.</span><span class="sxs-lookup"><span data-stu-id="1523f-124">Billing begins in a later step, when hello gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

```
VERBOSE: 4:31:35 PM - Begin Operation: New-AzureApplicationGateway 
VERBOSE: 4:32:37 PM - Completed Operation: New-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   55ef0460-825d-2981-ad20-b9a8af41b399
```

<span data-ttu-id="1523f-125">**toovalidate** que Olá gateway foi criado, você pode usar o hello `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1523f-125">**toovalidate** that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span> 

<span data-ttu-id="1523f-126">No exemplo hello, *descrição*, *InstanceCount*, e *GatewaySize* são parâmetros opcionais.</span><span class="sxs-lookup"><span data-stu-id="1523f-126">In hello sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="1523f-127">Olá valor padrão para *InstanceCount* é 2, com um valor máximo de 10.</span><span class="sxs-lookup"><span data-stu-id="1523f-127">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="1523f-128">Olá valor padrão para *GatewaySize* é médio.</span><span class="sxs-lookup"><span data-stu-id="1523f-128">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="1523f-129">Small e Large são outros valore disponíveis.</span><span class="sxs-lookup"><span data-stu-id="1523f-129">Small and Large are other available values.</span></span> <span data-ttu-id="1523f-130">*VIP* e *DnsName* são mostrados como em branco porque o gateway Olá ainda não foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="1523f-130">*Vip* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="1523f-131">Eles são criados depois que o gateway de hello está em estado de execução de saudação.</span><span class="sxs-lookup"><span data-stu-id="1523f-131">These are created once hello gateway is in hello running state.</span></span> 

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 4:39:39 PM - Begin Operation:
Get-AzureApplicationGateway VERBOSE: 4:39:40 PM - Completed 
Operation: Get-AzureApplicationGateway
Name: AppGwTest    
Description: 
VnetName: testvnet1 
Subnets: {Subnet-1} 
InstanceCount: 2 
GatewaySize: Medium 
State: Stopped 
VirtualIPs: 
DnsName:
```

## <a name="configure-hello-gateway"></a><span data-ttu-id="1523f-132">Configurar o gateway de saudação</span><span class="sxs-lookup"><span data-stu-id="1523f-132">Configure hello gateway</span></span>
<span data-ttu-id="1523f-133">Uma configuração de gateway de aplicativo consiste em vários valores.</span><span class="sxs-lookup"><span data-stu-id="1523f-133">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="1523f-134">valores Hello podem ser restritos a configuração de saudação tooconstruct juntos.</span><span class="sxs-lookup"><span data-stu-id="1523f-134">hello values can be tied together tooconstruct hello configuration.</span></span>

<span data-ttu-id="1523f-135">Olá valores são:</span><span class="sxs-lookup"><span data-stu-id="1523f-135">hello values are:</span></span>

* <span data-ttu-id="1523f-136">**Pool de servidores de back-end:** lista de saudação de endereços IP dos servidores de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="1523f-136">**Backend server pool:** hello list of IP addresses of hello backend servers.</span></span> <span data-ttu-id="1523f-137">endereços IP Hello listado ou devem pertencer a sub-rede de rede virtual toohello ou devem ser um IP público/VIP.</span><span class="sxs-lookup"><span data-stu-id="1523f-137">hello IP addresses listed should either belong toohello VNet subnet, or should be a public IP/VIP.</span></span> 
* <span data-ttu-id="1523f-138">**Configurações do pool de servidores back-end:** cada pool tem configurações como porta, protocolo e afinidade baseada em cookies.</span><span class="sxs-lookup"><span data-stu-id="1523f-138">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="1523f-139">Essas configurações são tooa empatado pool e são aplicados tooall servidores no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="1523f-139">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="1523f-140">**Porta de front-end:** essa porta é a porta pública de saudação aberta no gateway do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="1523f-140">**Frontend Port:** This port is hello public port opened on hello application gateway.</span></span> <span data-ttu-id="1523f-141">Tráfego atinge a essa porta e, em seguida, obtém tooone redirecionado de servidores de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="1523f-141">Traffic hits this port, and then gets redirected tooone of hello backend servers.</span></span>
* <span data-ttu-id="1523f-142">**Ouvinte:** ouvinte Olá tem uma porta de front-end, um protocolo (Http ou Https, eles diferenciam maiusculas de minúsculas) e o nome do certificado SSL de saudação (se a configuração de SSL de descarregamento).</span><span class="sxs-lookup"><span data-stu-id="1523f-142">**Listener:** hello listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span> 
* <span data-ttu-id="1523f-143">**Regra:** regra Olá associa ouvinte hello e pool de servidores de back-end hello e define qual tráfego Olá pool do servidor de back-end deve ser direcionado toowhen que ele atinja um ouvinte específico.</span><span class="sxs-lookup"><span data-stu-id="1523f-143">**Rule:** hello rule binds hello listener and hello backend server pool and defines which backend server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="1523f-144">Atualmente, apenas Olá *básica* regra tem suporte.</span><span class="sxs-lookup"><span data-stu-id="1523f-144">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="1523f-145">Olá *básica* regra é a distribuição de carga de round-robin.</span><span class="sxs-lookup"><span data-stu-id="1523f-145">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="1523f-146">Você pode construir sua configuração criando um objeto de configuração ou usando um arquivo XML de configuração.</span><span class="sxs-lookup"><span data-stu-id="1523f-146">You can construct your configuration either by creating a configuration object, or by using a configuration XML file.</span></span> <span data-ttu-id="1523f-147">tooconstruct de sua configuração por meio de um arquivo XML de configuração, use Olá exemplo abaixo.</span><span class="sxs-lookup"><span data-stu-id="1523f-147">tooconstruct your configuration by using a configuration XML file, use hello sample below.</span></span>

<span data-ttu-id="1523f-148">Observe o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="1523f-148">Note hello following:</span></span>

* <span data-ttu-id="1523f-149">Olá *FrontendIPConfigurations* elemento descreve Olá ILB detalhes relevantes para configurar o Application Gateway com um ILB.</span><span class="sxs-lookup"><span data-stu-id="1523f-149">hello *FrontendIPConfigurations* element describes hello ILB details relevant for configuring Application Gateway with an ILB.</span></span> 
* <span data-ttu-id="1523f-150">IP de front-end Hello *tipo* deve ser definido too'Private'</span><span class="sxs-lookup"><span data-stu-id="1523f-150">hello Frontend IP *Type* should be set too'Private'</span></span>
* <span data-ttu-id="1523f-151">Olá *StaticIPAddress* devem ser definidos no qual Olá gateway recebe o tráfego IP interno do toohello desejado.</span><span class="sxs-lookup"><span data-stu-id="1523f-151">hello *StaticIPAddress* should be set toohello desired internal IP on which hello gateway receives traffic.</span></span> <span data-ttu-id="1523f-152">Observe que Olá *StaticIPAddress* elemento é opcional.</span><span class="sxs-lookup"><span data-stu-id="1523f-152">Note that hello *StaticIPAddress* element is optional.</span></span> <span data-ttu-id="1523f-153">Se não for definido, um IP interno disponível da sub-rede Olá implantado é escolhido.</span><span class="sxs-lookup"><span data-stu-id="1523f-153">If not set, an available internal IP from hello deployed subnet is chosen.</span></span> 
* <span data-ttu-id="1523f-154">Olá valor Olá *nome* elemento especificado no *FrontendIPConfiguration* devem ser usadas em Olá HTTPListener *FrontendIP* elemento toorefer toohello FrontendIPConfiguration.</span><span class="sxs-lookup"><span data-stu-id="1523f-154">hello value of hello *Name* element specified in *FrontendIPConfiguration* should be used in hello HTTPListener's *FrontendIP* element toorefer toohello FrontendIPConfiguration.</span></span>
  
  <span data-ttu-id="1523f-155">**Exemplo de XML de configuração**</span><span class="sxs-lookup"><span data-stu-id="1523f-155">**Configuration XML sample**</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations>
        <FrontendIPConfiguration>
            <Name>fip1</Name> 
            <Type>Private</Type> 
            <StaticIPAddress>10.0.0.10</StaticIPAddress> 
        </FrontendIPConfiguration>
    </FrontendIPConfigurations>
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
            <FrontendIP>fip1</FrontendIP>
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


## <a name="set-hello-gateway-configuration"></a><span data-ttu-id="1523f-156">Configuração de gateway de saudação do conjunto</span><span class="sxs-lookup"><span data-stu-id="1523f-156">Set hello gateway configuration</span></span>
<span data-ttu-id="1523f-157">Em seguida, você configurará o gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="1523f-157">Next, you'll set hello application gateway.</span></span> <span data-ttu-id="1523f-158">Você pode usar o hello `Set-AzureApplicationGatewayConfig` cmdlet com um objeto de configuração ou com um arquivo XML de configuração.</span><span class="sxs-lookup"><span data-stu-id="1523f-158">You can use hello `Set-AzureApplicationGatewayConfig` cmdlet with a configuration object, or with a configuration XML file.</span></span> 

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

```
VERBOSE: 7:54:59 PM - Begin Operation: Set-AzureApplicationGatewayConfig 
VERBOSE: 7:55:32 PM - Completed Operation: Set-AzureApplicationGatewayConfig
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   9b995a09-66fe-2944-8b67-9bb04fcccb9d
```

## <a name="start-hello-gateway"></a><span data-ttu-id="1523f-159">Gateway de saudação inicial</span><span class="sxs-lookup"><span data-stu-id="1523f-159">Start hello gateway</span></span>

<span data-ttu-id="1523f-160">Uma vez configurado o gateway hello, use Olá `Start-AzureApplicationGateway` gateway de saudação do cmdlet toostart.</span><span class="sxs-lookup"><span data-stu-id="1523f-160">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="1523f-161">A cobrança por um application gateway iniciado após a saudação gateway foi iniciado com êxito.</span><span class="sxs-lookup"><span data-stu-id="1523f-161">Billing for an application gateway begins after hello gateway has been successfully started.</span></span> 

> [!NOTE]
> <span data-ttu-id="1523f-162">Olá `Start-AzureApplicationGateway` cmdlet pode levar até toocomplete too15 a 20 minutos.</span><span class="sxs-lookup"><span data-stu-id="1523f-162">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toocomplete.</span></span> 
> 
> 

```powershell
Start-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 7:59:16 PM - Begin Operation: Start-AzureApplicationGateway 
VERBOSE: 8:05:52 PM - Completed Operation: Start-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   fc592db8-4c58-2c8e-9a1d-1c97880f0b9b
```

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="1523f-163">Verificar status do gateway Olá</span><span class="sxs-lookup"><span data-stu-id="1523f-163">Verify hello gateway status</span></span>

<span data-ttu-id="1523f-164">Saudação de uso `Get-AzureApplicationGateway` status de saudação do cmdlet toocheck do gateway.</span><span class="sxs-lookup"><span data-stu-id="1523f-164">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of gateway.</span></span> <span data-ttu-id="1523f-165">Se `Start-AzureApplicationGateway` com êxito na etapa anterior hello, Olá estado deve ser *executando*, Olá Vip e DnsName deve ter entradas válidas.</span><span class="sxs-lookup"><span data-stu-id="1523f-165">If `Start-AzureApplicationGateway` succeeded in hello previous step, hello State should be *Running*, and hello Vip and DnsName should have valid entries.</span></span> <span data-ttu-id="1523f-166">Isso exemplo mostra Olá cmdlet na primeira linha de saudação, seguido de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="1523f-166">This sample shows hello cmdlet on hello first line, followed by hello output.</span></span> <span data-ttu-id="1523f-167">Neste exemplo, gateway hello está em execução e o tráfego tootake pronto.</span><span class="sxs-lookup"><span data-stu-id="1523f-167">In this sample, hello gateway is running, and is ready tootake traffic.</span></span> 

> [!NOTE]
> <span data-ttu-id="1523f-168">Olá application gateway configurado tooaccept tráfego em Olá configurou o ponto de extremidade ILB de 10.0.0.10 neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="1523f-168">hello application gateway is configured tooaccept traffic at hello configured ILB endpoint of 10.0.0.10 in this example.</span></span>

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
VirtualIPs    : {10.0.0.10}
DnsName       : appgw-b2a11563-2b3a-4172-a4aa-226ee4c23eed.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="1523f-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1523f-169">Next steps</span></span>
<span data-ttu-id="1523f-170">Se deseja obter mais informações sobre as opções de balanceamento de carga no geral, consulte:</span><span class="sxs-lookup"><span data-stu-id="1523f-170">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="1523f-171">Balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="1523f-171">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="1523f-172">Gerenciador de Tráfego do Azure</span><span class="sxs-lookup"><span data-stu-id="1523f-172">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

