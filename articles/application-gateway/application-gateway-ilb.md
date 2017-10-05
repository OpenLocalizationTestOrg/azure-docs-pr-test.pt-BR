---
title: Usando o Gateway de Aplicativo do Azure com o balanceador de carga interno | Microsoft Docs
description: "Esta página fornece instruções para configurar um Gateway de Aplicativo do Azure com um ponto de extremidade do Balanceador de Carga Interno"
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
ms.openlocfilehash: d6f3af61934c8c645be1f2c6b4c056fc7ee2e3aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a><span data-ttu-id="12065-103">Criar um Gateway de Aplicativo com um ILB (Balanceador de Carga Interno)</span><span class="sxs-lookup"><span data-stu-id="12065-103">Create an Application Gateway with an Internal Load Balancer (ILB)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="12065-104">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="12065-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="12065-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="12065-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="12065-106">O Gateway de Aplicativo pode ser configurado com um IP virtual voltado para a Internet ou com um ponto de extremidade interno não exposto à Internet, também conhecido como ponto de extremidade ILB (Balanceador de Carga Interno).</span><span class="sxs-lookup"><span data-stu-id="12065-106">Application Gateway can be configured with an internet facing virtual IP or with an internal end-point not exposed to the internet, also known as Internal Load Balancer (ILB) endpoint.</span></span> <span data-ttu-id="12065-107">Configurar o gateway como um ILB é útil para aplicativos de linha de negócios internos não expostos à Internet.</span><span class="sxs-lookup"><span data-stu-id="12065-107">Configuring the gateway with an ILB is useful for internal line-of-business applications not exposed to internet.</span></span> <span data-ttu-id="12065-108">Isso também é útil para serviços/camadas em um aplicativo multicamada que reside em um limite de segurança não exposto à Internet, mas que ainda exige distribuição de carga round robin, adesão da sessão ou terminação SSL.</span><span class="sxs-lookup"><span data-stu-id="12065-108">It's also useful for services/tiers within a multi-tier application, which sits in a security boundary not exposed to internet, but still require round robin load distribution, session stickiness, or SSL termination.</span></span> <span data-ttu-id="12065-109">Este artigo o orienta ao longo das etapas para configurar um Application Gateway com um ILB.</span><span class="sxs-lookup"><span data-stu-id="12065-109">This article walks you through the steps to configure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="12065-110">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="12065-110">Before you begin</span></span>

1. <span data-ttu-id="12065-111">Instale a versão mais recente dos cmdlets do Azure PowerShell usando o Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="12065-111">Install latest version of the Azure PowerShell cmdlets using the Web Platform Installer.</span></span> <span data-ttu-id="12065-112">Você pode baixar e instalar a versão mais recente na seção **Windows PowerShell** da [página de download](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="12065-112">You can download and install the latest version from the **Windows PowerShell** section of the [Download page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="12065-113">Verifique se você tem uma rede virtual em funcionamento com uma sub-rede válida.</span><span class="sxs-lookup"><span data-stu-id="12065-113">Verify that you have a working virtual network with valid subnet.</span></span>
3. <span data-ttu-id="12065-114">Verifique se você tem servidores back-end na rede virtual ou com um IP/VIP público atribuído.</span><span class="sxs-lookup"><span data-stu-id="12065-114">Verify that you have backend servers either in the virtual network, or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="12065-115">Para criar um Application Gateway, execute as etapas a seguir na ordem listada.</span><span class="sxs-lookup"><span data-stu-id="12065-115">To create an application gateway, perform the following steps in the order listed.</span></span> 

1. [<span data-ttu-id="12065-116">Criar um Application Gateway</span><span class="sxs-lookup"><span data-stu-id="12065-116">Create an application gateway</span></span>](#create-a-new-application-gateway)
2. [<span data-ttu-id="12065-117">Configurar o gateway</span><span class="sxs-lookup"><span data-stu-id="12065-117">Configure the gateway</span></span>](#configure-the-gateway)
3. [<span data-ttu-id="12065-118">Definir a configuração do gateway</span><span class="sxs-lookup"><span data-stu-id="12065-118">Set the gateway configuration</span></span>](#set-the-gateway-configuration)
4. [<span data-ttu-id="12065-119">Iniciar o gateway</span><span class="sxs-lookup"><span data-stu-id="12065-119">Start the gateway</span></span>](#start-the-gateway)
5. [<span data-ttu-id="12065-120">Verificar o gateway</span><span class="sxs-lookup"><span data-stu-id="12065-120">Verify the gateway</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="12065-121">Criar um Application Gateway:</span><span class="sxs-lookup"><span data-stu-id="12065-121">Create an application gateway:</span></span>

<span data-ttu-id="12065-122">**Para criar o gateway**, use o cmdlet `New-AzureApplicationGateway`, substituindo os valores pelos seus próprios.</span><span class="sxs-lookup"><span data-stu-id="12065-122">**To create the gateway**, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="12065-123">Observe que a cobrança pelo gateway não se inicia neste momento.</span><span class="sxs-lookup"><span data-stu-id="12065-123">Note that billing for the gateway does not start at this point.</span></span> <span data-ttu-id="12065-124">A cobrança é iniciada em uma etapa posterior, quando o gateway é iniciado com êxito.</span><span class="sxs-lookup"><span data-stu-id="12065-124">Billing begins in a later step, when the gateway is successfully started.</span></span>

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

<span data-ttu-id="12065-125">**Para validar** esse gateway que foi criado, você pode usar o cmdlet `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="12065-125">**To validate** that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span> 

<span data-ttu-id="12065-126">No exemplo, *Description*, *InstanceCount* e *GatewaySize* são parâmetros opcionais.</span><span class="sxs-lookup"><span data-stu-id="12065-126">In the sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="12065-127">O valor padrão para *InstanceCount* é 2, com um valor máximo de 10.</span><span class="sxs-lookup"><span data-stu-id="12065-127">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="12065-128">O valor padrão para *GatewaySize* é Medium.</span><span class="sxs-lookup"><span data-stu-id="12065-128">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="12065-129">Small e Large são outros valore disponíveis.</span><span class="sxs-lookup"><span data-stu-id="12065-129">Small and Large are other available values.</span></span> <span data-ttu-id="12065-130">*Vip* e *DnsName* são mostrados em branco porque o gateway ainda não foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="12065-130">*Vip* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="12065-131">Eles serão criados depois que o gateway estiver em estado de execução.</span><span class="sxs-lookup"><span data-stu-id="12065-131">These are created once the gateway is in the running state.</span></span> 

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

## <a name="configure-the-gateway"></a><span data-ttu-id="12065-132">Configurar o gateway</span><span class="sxs-lookup"><span data-stu-id="12065-132">Configure the gateway</span></span>
<span data-ttu-id="12065-133">Uma configuração de gateway de aplicativo consiste em vários valores.</span><span class="sxs-lookup"><span data-stu-id="12065-133">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="12065-134">Os valores podem ser vinculados para construir a configuração.</span><span class="sxs-lookup"><span data-stu-id="12065-134">The values can be tied together to construct the configuration.</span></span>

<span data-ttu-id="12065-135">Os valores são:</span><span class="sxs-lookup"><span data-stu-id="12065-135">The values are:</span></span>

* <span data-ttu-id="12065-136">**Pool de servidores de back-end:** a lista de endereços IP dos servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="12065-136">**Backend server pool:** The list of IP addresses of the backend servers.</span></span> <span data-ttu-id="12065-137">Os endereços IP listados ou devem pertencer à sub-rede da VNet, ou devem ser um IP/VIP público.</span><span class="sxs-lookup"><span data-stu-id="12065-137">The IP addresses listed should either belong to the VNet subnet, or should be a public IP/VIP.</span></span> 
* <span data-ttu-id="12065-138">**Configurações do pool de servidores back-end:** cada pool tem configurações como porta, protocolo e afinidade baseada em cookies.</span><span class="sxs-lookup"><span data-stu-id="12065-138">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="12065-139">Essas configurações são vinculadas a um pool e aplicadas a todos os servidores no pool.</span><span class="sxs-lookup"><span data-stu-id="12065-139">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="12065-140">**Porta front-end:** essa porta é a porta pública aberta no gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="12065-140">**Frontend Port:** This port is the public port opened on the application gateway.</span></span> <span data-ttu-id="12065-141">O tráfego atinge essa porta e é redirecionado para um dos servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="12065-141">Traffic hits this port, and then gets redirected to one of the backend servers.</span></span>
* <span data-ttu-id="12065-142">**Ouvinte:** o ouvinte tem uma porta front-end, um protocolo (Http ou Https, que diferencia maiúsculas de minúsculas) e o nome do certificado SSL (se estiver configurando o descarregamento SSL).</span><span class="sxs-lookup"><span data-stu-id="12065-142">**Listener:** The listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> 
* <span data-ttu-id="12065-143">**Regra:** a regra vincula o ouvinte e o pool de servidores back-end e define à qual pool de servidores back-end o tráfego deve ser direcionado quando atinge um ouvinte específico.</span><span class="sxs-lookup"><span data-stu-id="12065-143">**Rule:** The rule binds the listener and the backend server pool and defines which backend server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="12065-144">Atualmente, há suporte apenas para a regra *basic* .</span><span class="sxs-lookup"><span data-stu-id="12065-144">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="12065-145">A regra *basic* é a distribuição de carga round robin.</span><span class="sxs-lookup"><span data-stu-id="12065-145">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="12065-146">Você pode construir sua configuração criando um objeto de configuração ou usando um arquivo XML de configuração.</span><span class="sxs-lookup"><span data-stu-id="12065-146">You can construct your configuration either by creating a configuration object, or by using a configuration XML file.</span></span> <span data-ttu-id="12065-147">Para construir a configuração usando um arquivo XML de configuração, use o exemplo abaixo.</span><span class="sxs-lookup"><span data-stu-id="12065-147">To construct your configuration by using a configuration XML file, use the sample below.</span></span>

<span data-ttu-id="12065-148">Observe o seguinte:</span><span class="sxs-lookup"><span data-stu-id="12065-148">Note the following:</span></span>

* <span data-ttu-id="12065-149">O elemento *FrontendIPConfigurations* descreve os detalhes do ILB relevantes para configurar o Gateway de Aplicativo com ILB.</span><span class="sxs-lookup"><span data-stu-id="12065-149">The *FrontendIPConfigurations* element describes the ILB details relevant for configuring Application Gateway with an ILB.</span></span> 
* <span data-ttu-id="12065-150">O *Tipo* de IP front-end deve ser definido como ‘Privado’.</span><span class="sxs-lookup"><span data-stu-id="12065-150">The Frontend IP *Type* should be set to 'Private'</span></span>
* <span data-ttu-id="12065-151">O *StaticIPAddress* deve ser definido para o IP interno desejado no qual o gateway recebe o tráfego.</span><span class="sxs-lookup"><span data-stu-id="12065-151">The *StaticIPAddress* should be set to the desired internal IP on which the gateway receives traffic.</span></span> <span data-ttu-id="12065-152">Observe que o elemento *StaticIPAddress* é opcional.</span><span class="sxs-lookup"><span data-stu-id="12065-152">Note that the *StaticIPAddress* element is optional.</span></span> <span data-ttu-id="12065-153">Se não for definido, será escolhido um IP interno disponível na sub-rede implantada.</span><span class="sxs-lookup"><span data-stu-id="12065-153">If not set, an available internal IP from the deployed subnet is chosen.</span></span> 
* <span data-ttu-id="12065-154">O valor do elemento *Name* especificado em *FrontendIPConfiguration* deve ser usado no elemento *FrontendIP* de HTTPListener para fazer referência a FrontendIPConfiguration.</span><span class="sxs-lookup"><span data-stu-id="12065-154">The value of the *Name* element specified in *FrontendIPConfiguration* should be used in the HTTPListener's *FrontendIP* element to refer to the FrontendIPConfiguration.</span></span>
  
  <span data-ttu-id="12065-155">**Exemplo de XML de configuração**</span><span class="sxs-lookup"><span data-stu-id="12065-155">**Configuration XML sample**</span></span>
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


## <a name="set-the-gateway-configuration"></a><span data-ttu-id="12065-156">Definir a configuração do gateway</span><span class="sxs-lookup"><span data-stu-id="12065-156">Set the gateway configuration</span></span>
<span data-ttu-id="12065-157">Em seguida, você vai configurar o gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="12065-157">Next, you'll set the application gateway.</span></span> <span data-ttu-id="12065-158">É possível usar o cmdlet `Set-AzureApplicationGatewayConfig` com um objeto de configuração ou com um arquivo XML de configuração.</span><span class="sxs-lookup"><span data-stu-id="12065-158">You can use the `Set-AzureApplicationGatewayConfig` cmdlet with a configuration object, or with a configuration XML file.</span></span> 

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

## <a name="start-the-gateway"></a><span data-ttu-id="12065-159">Iniciar o gateway</span><span class="sxs-lookup"><span data-stu-id="12065-159">Start the gateway</span></span>

<span data-ttu-id="12065-160">Depois que o gateway tiver sido configurado, use o cmdlet `Start-AzureApplicationGateway` para iniciá-lo.</span><span class="sxs-lookup"><span data-stu-id="12065-160">Once the gateway has been configured, use the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span></span> <span data-ttu-id="12065-161">A cobrança por um gateway de aplicativo começa depois que o gateway tiver sido iniciado com êxito.</span><span class="sxs-lookup"><span data-stu-id="12065-161">Billing for an application gateway begins after the gateway has been successfully started.</span></span> 

> [!NOTE]
> <span data-ttu-id="12065-162">A regra `Start-AzureApplicationGateway` pode levar até 15 a 20 minutos para ser concluído.</span><span class="sxs-lookup"><span data-stu-id="12065-162">The `Start-AzureApplicationGateway` cmdlet might take up to 15-20 minutes to complete.</span></span> 
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

## <a name="verify-the-gateway-status"></a><span data-ttu-id="12065-163">Verificar o status do gateway</span><span class="sxs-lookup"><span data-stu-id="12065-163">Verify the gateway status</span></span>

<span data-ttu-id="12065-164">Use o cmdlet `Get-AzureApplicationGateway` para verificar o status do gateway.</span><span class="sxs-lookup"><span data-stu-id="12065-164">Use the `Get-AzureApplicationGateway` cmdlet to check the status of gateway.</span></span> <span data-ttu-id="12065-165">Se `Start-AzureApplicationGateway` tiver sido bem-sucedido na etapa anterior, o Estado deverá ser *Em execução* e Vip e DnsName deverão ter entradas válidas.</span><span class="sxs-lookup"><span data-stu-id="12065-165">If `Start-AzureApplicationGateway` succeeded in the previous step, the State should be *Running*, and the Vip and DnsName should have valid entries.</span></span> <span data-ttu-id="12065-166">Este exemplo mostra o cmdlet na primeira linha, seguido pela saída.</span><span class="sxs-lookup"><span data-stu-id="12065-166">This sample shows the cmdlet on the first line, followed by the output.</span></span> <span data-ttu-id="12065-167">Neste exemplo, o gateway está em execução e pronto para assumir o tráfego.</span><span class="sxs-lookup"><span data-stu-id="12065-167">In this sample, the gateway is running, and is ready to take traffic.</span></span> 

> [!NOTE]
> <span data-ttu-id="12065-168">Neste exemplo, o Application Gateway está configurado para aceitar o tráfego no ponto de extremidade ILB configurado de 10.0.0.10.</span><span class="sxs-lookup"><span data-stu-id="12065-168">The application gateway is configured to accept traffic at the configured ILB endpoint of 10.0.0.10 in this example.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="12065-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="12065-169">Next steps</span></span>
<span data-ttu-id="12065-170">Se deseja obter mais informações sobre as opções de balanceamento de carga no geral, consulte:</span><span class="sxs-lookup"><span data-stu-id="12065-170">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="12065-171">Balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="12065-171">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="12065-172">Gerenciador de Tráfego do Azure</span><span class="sxs-lookup"><span data-stu-id="12065-172">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

