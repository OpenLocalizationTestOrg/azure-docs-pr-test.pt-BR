---
title: "aaaConfigure SSL descarregar clássico - Gateway de aplicativo do Azure - PowerShell | Microsoft Docs"
description: "Este artigo fornece instruções toocreate descarregar um application gateway com SSL usando Olá modelo de implantação clássico do Azure."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 63f28d96-9c47-410e-97dd-f5ca1ad1b8a4
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 5cb128015747ed4b71802cf751c80b60634601a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-classic-deployment-model"></a><span data-ttu-id="fc46d-103">Configure um gateway de aplicativo para descarregamento SSL usando o modelo de implantação clássico Olá</span><span class="sxs-lookup"><span data-stu-id="fc46d-103">Configure an application gateway for SSL offload by using hello classic deployment model</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="fc46d-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="fc46d-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="fc46d-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fc46d-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="fc46d-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="fc46d-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="fc46d-107">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="fc46d-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="fc46d-108">Gateway de aplicativo do Azure pode ser configurado tooterminate Olá Secure Sockets Layer (SSL) sessão Olá gateway tooavoid cara SSL descriptografia tarefas toohappen no farm de web hello.</span><span class="sxs-lookup"><span data-stu-id="fc46d-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="fc46d-109">Descarregamento SSL também simplifica a configuração de servidor front-end do hello e gerenciamento de aplicativo da web hello.</span><span class="sxs-lookup"><span data-stu-id="fc46d-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="fc46d-110">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="fc46d-110">Before you begin</span></span>

1. <span data-ttu-id="fc46d-111">Instale a versão mais recente Olá Olá Azure de cmdlets do PowerShell usando Olá Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="fc46d-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="fc46d-112">Você pode baixar e instalar a versão mais recente de saudação do hello **do Windows PowerShell** seção Olá [página de Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="fc46d-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="fc46d-113">Verifique se você tem uma rede virtual em funcionamento com uma sub-rede válida.</span><span class="sxs-lookup"><span data-stu-id="fc46d-113">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="fc46d-114">Certifique-se de que não há máquinas ou implantações de nuvem usando sub-rede hello.</span><span class="sxs-lookup"><span data-stu-id="fc46d-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="fc46d-115">gateway de aplicativo Hello deve ser sozinho em uma sub-rede de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="fc46d-115">hello application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="fc46d-116">servidores de saudação que você configure o gateway de aplicativo hello toouse devem existir ou seus pontos de extremidade criados na rede virtual hello ou com um IP público/VIP atribuídos.</span><span class="sxs-lookup"><span data-stu-id="fc46d-116">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="fc46d-117">tooconfigure SSL descarregar em um gateway de aplicativo, Olá etapas na ordem Olá listados a seguir:</span><span class="sxs-lookup"><span data-stu-id="fc46d-117">tooconfigure SSL offload on an application gateway, do hello following steps in hello order listed:</span></span>

1. [<span data-ttu-id="fc46d-118">Criar um Application Gateway</span><span class="sxs-lookup"><span data-stu-id="fc46d-118">Create an application gateway</span></span>](#create-an-application-gateway)
2. [<span data-ttu-id="fc46d-119">Carregar certificados SSL</span><span class="sxs-lookup"><span data-stu-id="fc46d-119">Upload SSL certificates</span></span>](#upload-ssl-certificates)
3. [<span data-ttu-id="fc46d-120">Configurar o gateway de saudação</span><span class="sxs-lookup"><span data-stu-id="fc46d-120">Configure hello gateway</span></span>](#configure-the-gateway)
4. [<span data-ttu-id="fc46d-121">Configuração de gateway de saudação do conjunto</span><span class="sxs-lookup"><span data-stu-id="fc46d-121">Set hello gateway configuration</span></span>](#set-the-gateway-configuration)
5. [<span data-ttu-id="fc46d-122">Gateway de saudação inicial</span><span class="sxs-lookup"><span data-stu-id="fc46d-122">Start hello gateway</span></span>](#start-the-gateway)
6. [<span data-ttu-id="fc46d-123">Verificar status do gateway Olá</span><span class="sxs-lookup"><span data-stu-id="fc46d-123">Verify hello gateway status</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="fc46d-124">Criar um Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="fc46d-124">Create an application gateway</span></span>

<span data-ttu-id="fc46d-125">gateway toocreate Olá Olá use `New-AzureApplicationGateway` cmdlet, substituindo os valores hello com seus próprios.</span><span class="sxs-lookup"><span data-stu-id="fc46d-125">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="fc46d-126">Cobrança para o gateway de saudação não funciona neste momento.</span><span class="sxs-lookup"><span data-stu-id="fc46d-126">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="fc46d-127">A cobrança começa em uma etapa posterior, quando o gateway Olá foi iniciado com êxito.</span><span class="sxs-lookup"><span data-stu-id="fc46d-127">Billing begins in a later step, when hello gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="fc46d-128">toovalidate que Olá gateway foi criado, você pode usar o hello `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="fc46d-128">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="fc46d-129">No exemplo hello, *descrição*, *InstanceCount*, e *GatewaySize* são parâmetros opcionais.</span><span class="sxs-lookup"><span data-stu-id="fc46d-129">In hello sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="fc46d-130">Olá valor padrão para *InstanceCount* é 2, com um valor máximo de 10.</span><span class="sxs-lookup"><span data-stu-id="fc46d-130">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="fc46d-131">Olá valor padrão para *GatewaySize* é médio.</span><span class="sxs-lookup"><span data-stu-id="fc46d-131">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="fc46d-132">Small e Large são outros valore disponíveis.</span><span class="sxs-lookup"><span data-stu-id="fc46d-132">Small and Large are other available values.</span></span> <span data-ttu-id="fc46d-133">*VirtualIPs* e *DnsName* são mostrados como em branco porque o gateway Olá ainda não foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="fc46d-133">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="fc46d-134">Esses valores são criados depois que o gateway de hello está em estado de execução de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc46d-134">These values are created once hello gateway is in hello running state.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a><span data-ttu-id="fc46d-135">Carregar certificados SSL</span><span class="sxs-lookup"><span data-stu-id="fc46d-135">Upload SSL certificates</span></span>

<span data-ttu-id="fc46d-136">Use `Add-AzureApplicationGatewaySslCertificate` certificado do servidor de saudação tooupload no *pfx* gateway de formato de aplicativo toohello.</span><span class="sxs-lookup"><span data-stu-id="fc46d-136">Use `Add-AzureApplicationGatewaySslCertificate` tooupload hello server certificate in *pfx* format toohello application gateway.</span></span> <span data-ttu-id="fc46d-137">nome do certificado Olá é um nome de usuário escolhido e deve ser exclusivo no gateway do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="fc46d-137">hello certificate name is a user-chosen name and must be unique within hello application gateway.</span></span> <span data-ttu-id="fc46d-138">Esse certificado é chamado tooby esse nome em todas as operações de gerenciamento de certificado no gateway do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="fc46d-138">This certificate is referred tooby this name in all certificate management operations on hello application gateway.</span></span>

<span data-ttu-id="fc46d-139">Este exemplo a seguir mostra o cmdlet hello, substitua valores de saudação no exemplo hello com seus próprios.</span><span class="sxs-lookup"><span data-stu-id="fc46d-139">This following sample shows hello cmdlet, replace hello values in hello sample with your own.</span></span>

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path toopfx file>
```

<span data-ttu-id="fc46d-140">Em seguida, valide o carregamento do certificado hello.</span><span class="sxs-lookup"><span data-stu-id="fc46d-140">Next, validate hello certificate upload.</span></span> <span data-ttu-id="fc46d-141">Saudação de uso `Get-AzureApplicationGatewayCertificate` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="fc46d-141">Use hello `Get-AzureApplicationGatewayCertificate` cmdlet.</span></span>

<span data-ttu-id="fc46d-142">Isso exemplo mostra Olá cmdlet na primeira linha de saudação, seguido de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="fc46d-142">This sample shows hello cmdlet on hello first line, followed by hello output.</span></span>

```powershell
Get-AzureApplicationGatewaySslCertificate AppGwTest
```

```
VERBOSE: 5:07:54 PM - Begin Operation: Get-AzureApplicationGatewaySslCertificate
VERBOSE: 5:07:55 PM - Completed Operation: Get-AzureApplicationGatewaySslCertificate
Name           : SslCert
SubjectName    : CN=gwcert.app.test.contoso.com
Thumbprint     : AF5ADD77E160A01A6......EE48D1A
ThumbprintAlgo : sha1RSA
State..........: Provisioned
```

> [!NOTE]
> <span data-ttu-id="fc46d-143">senha do certificado Olá tem toobe entre 4 too12 caracteres, letras ou números.</span><span class="sxs-lookup"><span data-stu-id="fc46d-143">hello certificate password has toobe between 4 too12 characters, letters, or numbers.</span></span> <span data-ttu-id="fc46d-144">Caracteres especiais não são aceitos.</span><span class="sxs-lookup"><span data-stu-id="fc46d-144">Special characters are not accepted.</span></span>

## <a name="configure-hello-gateway"></a><span data-ttu-id="fc46d-145">Configurar o gateway de saudação</span><span class="sxs-lookup"><span data-stu-id="fc46d-145">Configure hello gateway</span></span>

<span data-ttu-id="fc46d-146">Uma configuração de gateway de aplicativo consiste em vários valores.</span><span class="sxs-lookup"><span data-stu-id="fc46d-146">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="fc46d-147">valores Hello podem ser restritos a configuração de saudação tooconstruct juntos.</span><span class="sxs-lookup"><span data-stu-id="fc46d-147">hello values can be tied together tooconstruct hello configuration.</span></span>

<span data-ttu-id="fc46d-148">Olá valores são:</span><span class="sxs-lookup"><span data-stu-id="fc46d-148">hello values are:</span></span>

* <span data-ttu-id="fc46d-149">**Pool de servidores de back-end:** lista de saudação de endereços IP dos servidores de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc46d-149">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="fc46d-150">endereços IP Hello listado ou devem pertencer a sub-rede da rede virtual toohello ou devem ser um IP público/VIP.</span><span class="sxs-lookup"><span data-stu-id="fc46d-150">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="fc46d-151">**Configurações do pool de servidores back-end:** cada pool tem configurações como porta, protocolo e afinidade baseada em cookie.</span><span class="sxs-lookup"><span data-stu-id="fc46d-151">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="fc46d-152">Essas configurações são tooa empatado pool e são aplicados tooall servidores no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc46d-152">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="fc46d-153">**Porta de front-end:** essa porta é a porta pública de saudação que é aberta no gateway do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="fc46d-153">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="fc46d-154">Tráfego atinge essa porta e, em seguida, obtém redirecionado tooone de servidores de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc46d-154">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="fc46d-155">**Ouvinte:** ouvinte Olá tem uma porta de front-end, um protocolo (Http ou Https, esses valores diferenciam maiusculas de minúsculas) e o nome do certificado SSL de saudação (se a configuração de SSL de descarregamento).</span><span class="sxs-lookup"><span data-stu-id="fc46d-155">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="fc46d-156">**Regra:** regra Olá associa ouvinte hello e pool de saudação do servidor de back-end e define o tráfego de saudação do pool de servidor back-end deve ser direcionado toowhen que ele atinja um ouvinte específico.</span><span class="sxs-lookup"><span data-stu-id="fc46d-156">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="fc46d-157">Atualmente, apenas Olá *básica* regra tem suporte.</span><span class="sxs-lookup"><span data-stu-id="fc46d-157">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="fc46d-158">Olá *básica* regra é a distribuição de carga de round-robin.</span><span class="sxs-lookup"><span data-stu-id="fc46d-158">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="fc46d-159">**Observações adicionais sobre a configuração**</span><span class="sxs-lookup"><span data-stu-id="fc46d-159">**Additional configuration notes**</span></span>

<span data-ttu-id="fc46d-160">Para a configuração de certificados SSL, Olá protocolo em **HttpListener** devem alterar muito*Https* (com distinção entre maiusculas e minúsculas).</span><span class="sxs-lookup"><span data-stu-id="fc46d-160">For SSL certificates configuration, hello protocol in **HttpListener** should change too*Https* (case sensitive).</span></span> <span data-ttu-id="fc46d-161">Olá **SslCert** elemento é adicionado muito**HttpListener** com hello valor definido toohello mesmo nome como usado no carregamento de saudação das anteriores a seção de certificados SSL.</span><span class="sxs-lookup"><span data-stu-id="fc46d-161">hello **SslCert** element is added too**HttpListener** with hello value set toohello same name as used in hello upload of preceding SSL certificates section.</span></span> <span data-ttu-id="fc46d-162">porta de front-end Olá deve ser atualizado too443.</span><span class="sxs-lookup"><span data-stu-id="fc46d-162">hello front-end port should be updated too443.</span></span>

<span data-ttu-id="fc46d-163">**afinidade de baseada em cookie tooenable**: um application gateway pode ser configurado tooensure que uma solicitação de uma sessão de cliente é sempre toohello direcionado mesma VM no farm de web hello.</span><span class="sxs-lookup"><span data-stu-id="fc46d-163">**tooenable cookie-based affinity**: An application gateway can be configured tooensure that a request from a client session is always directed toohello same VM in hello web farm.</span></span> <span data-ttu-id="fc46d-164">Este cenário é feito pela inclusão de um cookie de sessão que permite que o tráfego de toodirect gateway Olá adequadamente.</span><span class="sxs-lookup"><span data-stu-id="fc46d-164">This scenario is done by injection of a session cookie that allows hello gateway toodirect traffic appropriately.</span></span> <span data-ttu-id="fc46d-165">Definir afinidade baseada em cookie tooenable, **CookieBasedAffinity** muito*habilitado* em Olá **BackendHttpSettings** elemento.</span><span class="sxs-lookup"><span data-stu-id="fc46d-165">tooenable cookie-based affinity, set **CookieBasedAffinity** too*Enabled* in hello **BackendHttpSettings** element.</span></span>

<span data-ttu-id="fc46d-166">Você pode construir sua configuração criando um objeto de configuração ou usando um arquivo XML de configuração.</span><span class="sxs-lookup"><span data-stu-id="fc46d-166">You can construct your configuration either by creating a configuration object or by using a configuration XML file.</span></span>
<span data-ttu-id="fc46d-167">tooconstruct sua configuração por meio de uma configuração de arquivo XML, use Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="fc46d-167">tooconstruct your configuration by using a configuration XML file, use hello following sample:</span></span>

<span data-ttu-id="fc46d-168">**Exemplo de XML de configuração**</span><span class="sxs-lookup"><span data-stu-id="fc46d-168">**Configuration XML sample**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations />
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>443</Port>
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
            <Protocol>Https</Protocol>
            <SslCert>GWCert</SslCert>
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

## <a name="set-hello-gateway-configuration"></a><span data-ttu-id="fc46d-169">Configuração de gateway de saudação do conjunto</span><span class="sxs-lookup"><span data-stu-id="fc46d-169">Set hello gateway configuration</span></span>

<span data-ttu-id="fc46d-170">Em seguida, defina o gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="fc46d-170">Next, you set hello application gateway.</span></span> <span data-ttu-id="fc46d-171">Você pode usar o hello `Set-AzureApplicationGatewayConfig` cmdlet com um objeto de configuração ou com um arquivo XML de configuração.</span><span class="sxs-lookup"><span data-stu-id="fc46d-171">You can use hello `Set-AzureApplicationGatewayConfig` cmdlet with either a configuration object or with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-hello-gateway"></a><span data-ttu-id="fc46d-172">Gateway de saudação inicial</span><span class="sxs-lookup"><span data-stu-id="fc46d-172">Start hello gateway</span></span>

<span data-ttu-id="fc46d-173">Uma vez configurado o gateway hello, use Olá `Start-AzureApplicationGateway` gateway de saudação do cmdlet toostart.</span><span class="sxs-lookup"><span data-stu-id="fc46d-173">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="fc46d-174">A cobrança por um application gateway iniciado após a saudação gateway foi iniciado com êxito.</span><span class="sxs-lookup"><span data-stu-id="fc46d-174">Billing for an application gateway begins after hello gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="fc46d-175">Olá `Start-AzureApplicationGateway` cmdlet pode levar até toofinish too15 a 20 minutos.</span><span class="sxs-lookup"><span data-stu-id="fc46d-175">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toofinish.</span></span>
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="fc46d-176">Verificar status do gateway Olá</span><span class="sxs-lookup"><span data-stu-id="fc46d-176">Verify hello gateway status</span></span>

<span data-ttu-id="fc46d-177">Saudação de uso `Get-AzureApplicationGateway` status de saudação do cmdlet toocheck do gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc46d-177">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of hello gateway.</span></span> <span data-ttu-id="fc46d-178">Se `Start-AzureApplicationGateway` com êxito na etapa anterior de saudação, *estado* devem estar em execução, e *VirtualIPs* e *DnsName* devem ter entradas válidas.</span><span class="sxs-lookup"><span data-stu-id="fc46d-178">If `Start-AzureApplicationGateway` succeeded in hello previous step, *State* should be Running, and *VirtualIPs* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="fc46d-179">Este exemplo mostra um application gateway, em execução, e o tráfego tootake pronto.</span><span class="sxs-lookup"><span data-stu-id="fc46d-179">This sample shows an application gateway that is up, running, and is ready tootake traffic.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest2
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {23.96.22.241}
DnsName       : appgw-4c960426-d1e6-4aae-8670-81fd7a519a43.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="fc46d-180">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fc46d-180">Next steps</span></span>

<span data-ttu-id="fc46d-181">Se deseja obter mais informações sobre as opções de balanceamento de carga no geral, consulte:</span><span class="sxs-lookup"><span data-stu-id="fc46d-181">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="fc46d-182">Balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="fc46d-182">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="fc46d-183">Gerenciador de Tráfego do Azure</span><span class="sxs-lookup"><span data-stu-id="fc46d-183">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

