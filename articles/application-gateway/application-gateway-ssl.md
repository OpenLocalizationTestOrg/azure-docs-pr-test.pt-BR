---
title: "Configurar o descarregamento SSL - Gateway de Aplicativo do Azure - PowerShell clássico | Microsoft Docs"
description: "Este artigo fornece instruções para criar um Application Gateway com descarregamento de protocolo SSL usando o modelo de implantação clássica do Azure."
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
ms.openlocfilehash: 2eba6fb24c11add12ac16d04d3445e19a3486216
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-the-classic-deployment-model"></a><span data-ttu-id="0c695-103">Configurar um Application Gateway para o descarregamento SSL usando o modelo implantação clássico</span><span class="sxs-lookup"><span data-stu-id="0c695-103">Configure an application gateway for SSL offload by using the classic deployment model</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0c695-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0c695-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="0c695-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0c695-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="0c695-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="0c695-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="0c695-107">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="0c695-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="0c695-108">O Gateway de Aplicativo do Azure pode ser configurado para encerrar a sessão SSL no gateway para evitar que a onerosa tarefa de descriptografia de SSL aconteça no web farm.</span><span class="sxs-lookup"><span data-stu-id="0c695-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="0c695-109">O descarregamento SSL também simplifica a configuração do servidor front-end e o gerenciamento do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="0c695-109">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0c695-110">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="0c695-110">Before you begin</span></span>

1. <span data-ttu-id="0c695-111">Instale a versão mais recente dos cmdlets do Azure PowerShell usando o Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="0c695-111">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="0c695-112">Você pode baixar e instalar a versão mais recente da seção **Windows PowerShell** da [página Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="0c695-112">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="0c695-113">Verifique se você tem uma rede virtual em funcionamento com uma sub-rede válida.</span><span class="sxs-lookup"><span data-stu-id="0c695-113">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="0c695-114">Verifique se não há máquinas virtuais ou implantações em nuvem usando a sub-rede.</span><span class="sxs-lookup"><span data-stu-id="0c695-114">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="0c695-115">O gateway de aplicativo deve estar sozinho em uma sub-rede de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="0c695-115">The application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="0c695-116">Os servidores que você configura para usar o gateway de aplicativo devem existir ou ter seus pontos de extremidade criados na rede virtual ou com um IP/VIP público atribuído.</span><span class="sxs-lookup"><span data-stu-id="0c695-116">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="0c695-117">Para configurar o descarregamento de SSL em um Application Gateway, execute as seguintes etapas na ordem listada:</span><span class="sxs-lookup"><span data-stu-id="0c695-117">To configure SSL offload on an application gateway, do the following steps in the order listed:</span></span>

1. [<span data-ttu-id="0c695-118">Criar um Application Gateway</span><span class="sxs-lookup"><span data-stu-id="0c695-118">Create an application gateway</span></span>](#create-an-application-gateway)
2. [<span data-ttu-id="0c695-119">Carregar certificados SSL</span><span class="sxs-lookup"><span data-stu-id="0c695-119">Upload SSL certificates</span></span>](#upload-ssl-certificates)
3. [<span data-ttu-id="0c695-120">Configurar o gateway</span><span class="sxs-lookup"><span data-stu-id="0c695-120">Configure the gateway</span></span>](#configure-the-gateway)
4. [<span data-ttu-id="0c695-121">Definir a configuração do gateway</span><span class="sxs-lookup"><span data-stu-id="0c695-121">Set the gateway configuration</span></span>](#set-the-gateway-configuration)
5. [<span data-ttu-id="0c695-122">Iniciar o gateway</span><span class="sxs-lookup"><span data-stu-id="0c695-122">Start the gateway</span></span>](#start-the-gateway)
6. [<span data-ttu-id="0c695-123">Verificar o status do gateway</span><span class="sxs-lookup"><span data-stu-id="0c695-123">Verify the gateway status</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="0c695-124">Criar um Application Gateway</span><span class="sxs-lookup"><span data-stu-id="0c695-124">Create an application gateway</span></span>

<span data-ttu-id="0c695-125">Para criar o gateway, use o cmdlet `New-AzureApplicationGateway`, substituindo os valores pelos seus próprios.</span><span class="sxs-lookup"><span data-stu-id="0c695-125">To create the gateway, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="0c695-126">A cobrança pelo gateway não se inicia neste momento.</span><span class="sxs-lookup"><span data-stu-id="0c695-126">Billing for the gateway does not start at this point.</span></span> <span data-ttu-id="0c695-127">A cobrança é iniciada em uma etapa posterior, quando o gateway é iniciado com êxito.</span><span class="sxs-lookup"><span data-stu-id="0c695-127">Billing begins in a later step, when the gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="0c695-128">Para validar esse gateway que foi criado, você pode usar o cmdlet `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="0c695-128">To validate that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="0c695-129">No exemplo, *Description*, *InstanceCount* e *GatewaySize* são parâmetros opcionais.</span><span class="sxs-lookup"><span data-stu-id="0c695-129">In the sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="0c695-130">O valor padrão para *InstanceCount* é 2, com um valor máximo de 10.</span><span class="sxs-lookup"><span data-stu-id="0c695-130">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="0c695-131">O valor padrão para *GatewaySize* é Medium.</span><span class="sxs-lookup"><span data-stu-id="0c695-131">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="0c695-132">Small e Large são outros valore disponíveis.</span><span class="sxs-lookup"><span data-stu-id="0c695-132">Small and Large are other available values.</span></span> <span data-ttu-id="0c695-133">*VirtualIPs* e *DnsName* são mostrados em branco porque o gateway ainda não foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="0c695-133">*VirtualIPs* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="0c695-134">Esses valores serão criados depois que o gateway estiver em estado de execução.</span><span class="sxs-lookup"><span data-stu-id="0c695-134">These values are created once the gateway is in the running state.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a><span data-ttu-id="0c695-135">Carregar certificados SSL</span><span class="sxs-lookup"><span data-stu-id="0c695-135">Upload SSL certificates</span></span>

<span data-ttu-id="0c695-136">Use `Add-AzureApplicationGatewaySslCertificate` para carregar o certificado do servidor no formato *pfx* para o gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0c695-136">Use `Add-AzureApplicationGatewaySslCertificate` to upload the server certificate in *pfx* format to the application gateway.</span></span> <span data-ttu-id="0c695-137">O nome do certificado é um nome escolhido pelo usuário e deve ser exclusivo dentro do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0c695-137">The certificate name is a user-chosen name and must be unique within the application gateway.</span></span> <span data-ttu-id="0c695-138">Esse certificado é conhecido por esse nome em todas as operações de gerenciamento de certificado no gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0c695-138">This certificate is referred to by this name in all certificate management operations on the application gateway.</span></span>

<span data-ttu-id="0c695-139">O exemplo a seguir mostra o cmdlet. Substitua os valores no exemplo pelos seus próprios.</span><span class="sxs-lookup"><span data-stu-id="0c695-139">This following sample shows the cmdlet, replace the values in the sample with your own.</span></span>

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path to pfx file>
```

<span data-ttu-id="0c695-140">Em seguida, valide o carregamento do certificado.</span><span class="sxs-lookup"><span data-stu-id="0c695-140">Next, validate the certificate upload.</span></span> <span data-ttu-id="0c695-141">Use o cmdlet `Get-AzureApplicationGatewayCertificate` .</span><span class="sxs-lookup"><span data-stu-id="0c695-141">Use the `Get-AzureApplicationGatewayCertificate` cmdlet.</span></span>

<span data-ttu-id="0c695-142">Este exemplo mostra o cmdlet na primeira linha, seguido pela saída.</span><span class="sxs-lookup"><span data-stu-id="0c695-142">This sample shows the cmdlet on the first line, followed by the output.</span></span>

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
> <span data-ttu-id="0c695-143">A senha do certificado deve ser entre 4 a 12 caracteres, letras ou números.</span><span class="sxs-lookup"><span data-stu-id="0c695-143">The certificate password has to be between 4 to 12 characters, letters, or numbers.</span></span> <span data-ttu-id="0c695-144">Caracteres especiais não são aceitos.</span><span class="sxs-lookup"><span data-stu-id="0c695-144">Special characters are not accepted.</span></span>

## <a name="configure-the-gateway"></a><span data-ttu-id="0c695-145">Configurar o gateway</span><span class="sxs-lookup"><span data-stu-id="0c695-145">Configure the gateway</span></span>

<span data-ttu-id="0c695-146">Uma configuração de gateway de aplicativo consiste em vários valores.</span><span class="sxs-lookup"><span data-stu-id="0c695-146">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="0c695-147">Os valores podem ser vinculados para construir a configuração.</span><span class="sxs-lookup"><span data-stu-id="0c695-147">The values can be tied together to construct the configuration.</span></span>

<span data-ttu-id="0c695-148">Os valores são:</span><span class="sxs-lookup"><span data-stu-id="0c695-148">The values are:</span></span>

* <span data-ttu-id="0c695-149">**Pool de servidores back-end:** a lista de endereços IP dos servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="0c695-149">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="0c695-150">Os endereços IP listados devem pertencer à sub-rede da rede virtual ou devem ser um IP/VIP público.</span><span class="sxs-lookup"><span data-stu-id="0c695-150">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="0c695-151">**Configurações do pool de servidores back-end:** cada pool tem configurações como porta, protocolo e afinidade baseada em cookie.</span><span class="sxs-lookup"><span data-stu-id="0c695-151">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="0c695-152">Essas configurações são vinculadas a um pool e aplicadas a todos os servidores no pool.</span><span class="sxs-lookup"><span data-stu-id="0c695-152">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="0c695-153">**Porta front-end:** essa porta é a porta pública aberta no gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0c695-153">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="0c695-154">O tráfego atinge essa porta e é redirecionado para um dos servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="0c695-154">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="0c695-155">**Ouvinte:** o ouvinte tem uma porta front-end, um protocolo (HTTP ou HTTPS, esses valores diferenciam maiúsculas de minúsculas) e o nome do certificado SSL (caso esteja configurando o descarregamento SSL).</span><span class="sxs-lookup"><span data-stu-id="0c695-155">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="0c695-156">**Regra:** a regra vincula o ouvinte e o pool de servidores back-end e define à qual pool de servidores back-end o tráfego deve ser direcionado quando atinge um ouvinte específico.</span><span class="sxs-lookup"><span data-stu-id="0c695-156">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="0c695-157">Atualmente, há suporte apenas para a regra *basic* .</span><span class="sxs-lookup"><span data-stu-id="0c695-157">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="0c695-158">A regra *básica* é a distribuição de carga round robin.</span><span class="sxs-lookup"><span data-stu-id="0c695-158">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="0c695-159">**Observações adicionais sobre a configuração**</span><span class="sxs-lookup"><span data-stu-id="0c695-159">**Additional configuration notes**</span></span>

<span data-ttu-id="0c695-160">Para a configuração de certificados SSL, o protocolo em **HttpListener** deve ser alterado para *Https* (diferencia maiúsculas de minúsculas).</span><span class="sxs-lookup"><span data-stu-id="0c695-160">For SSL certificates configuration, the protocol in **HttpListener** should change to *Https* (case sensitive).</span></span> <span data-ttu-id="0c695-161">O elemento **SslCert** é adicionado a **HttpListener** com o valor definido para o mesmo nome usado no carregamento da seção de certificados SSL anterior.</span><span class="sxs-lookup"><span data-stu-id="0c695-161">The **SslCert** element is added to **HttpListener** with the value set to the same name as used in the upload of preceding SSL certificates section.</span></span> <span data-ttu-id="0c695-162">A porta front-end deve ser atualizada para 443.</span><span class="sxs-lookup"><span data-stu-id="0c695-162">The front-end port should be updated to 443.</span></span>

<span data-ttu-id="0c695-163">**Para habilitar a afinidade baseada em cookie**: um gateway de aplicativo pode ser configurado para garantir que uma solicitação de uma sessão de cliente sempre seja direcionada para a mesma VM no web farm.</span><span class="sxs-lookup"><span data-stu-id="0c695-163">**To enable cookie-based affinity**: An application gateway can be configured to ensure that a request from a client session is always directed to the same VM in the web farm.</span></span> <span data-ttu-id="0c695-164">Este cenário é concluído pela injeção de um cookie de sessão que permite que o gateway redirecione o tráfego corretamente.</span><span class="sxs-lookup"><span data-stu-id="0c695-164">This scenario is done by injection of a session cookie that allows the gateway to direct traffic appropriately.</span></span> <span data-ttu-id="0c695-165">Para habilitar a afinidade baseada em cookie, defina **CookieBasedAffinity** como *Habilitado* no elemento **BackendHttpSettings**.</span><span class="sxs-lookup"><span data-stu-id="0c695-165">To enable cookie-based affinity, set **CookieBasedAffinity** to *Enabled* in the **BackendHttpSettings** element.</span></span>

<span data-ttu-id="0c695-166">Você pode construir sua configuração criando um objeto de configuração ou usando um arquivo XML de configuração.</span><span class="sxs-lookup"><span data-stu-id="0c695-166">You can construct your configuration either by creating a configuration object or by using a configuration XML file.</span></span>
<span data-ttu-id="0c695-167">Para construir a configuração usando um arquivo XML de configuração, use o exemplo abaixo:</span><span class="sxs-lookup"><span data-stu-id="0c695-167">To construct your configuration by using a configuration XML file, use the following sample:</span></span>

<span data-ttu-id="0c695-168">**Exemplo de XML de configuração**</span><span class="sxs-lookup"><span data-stu-id="0c695-168">**Configuration XML sample**</span></span>

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

## <a name="set-the-gateway-configuration"></a><span data-ttu-id="0c695-169">Definir a configuração do gateway</span><span class="sxs-lookup"><span data-stu-id="0c695-169">Set the gateway configuration</span></span>

<span data-ttu-id="0c695-170">Em seguida, você configura o gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0c695-170">Next, you set the application gateway.</span></span> <span data-ttu-id="0c695-171">É possível usar o cmdlet `Set-AzureApplicationGatewayConfig` com um objeto de configuração ou um arquivo XML de configuração.</span><span class="sxs-lookup"><span data-stu-id="0c695-171">You can use the `Set-AzureApplicationGatewayConfig` cmdlet with either a configuration object or with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-the-gateway"></a><span data-ttu-id="0c695-172">Iniciar o gateway</span><span class="sxs-lookup"><span data-stu-id="0c695-172">Start the gateway</span></span>

<span data-ttu-id="0c695-173">Depois que o gateway tiver sido configurado, use o cmdlet `Start-AzureApplicationGateway` para iniciá-lo.</span><span class="sxs-lookup"><span data-stu-id="0c695-173">Once the gateway has been configured, use the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span></span> <span data-ttu-id="0c695-174">A cobrança por um gateway de aplicativo começa depois que o gateway tiver sido iniciado com êxito.</span><span class="sxs-lookup"><span data-stu-id="0c695-174">Billing for an application gateway begins after the gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="0c695-175">O cmdlet `Start-AzureApplicationGateway` poderá levar até 15 a 20 minutos para terminar.</span><span class="sxs-lookup"><span data-stu-id="0c695-175">The `Start-AzureApplicationGateway` cmdlet might take up to 15-20 minutes to finish.</span></span>
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-the-gateway-status"></a><span data-ttu-id="0c695-176">Verificar o status do gateway</span><span class="sxs-lookup"><span data-stu-id="0c695-176">Verify the gateway status</span></span>

<span data-ttu-id="0c695-177">Use o cmdlet `Get-AzureApplicationGateway` para verificar o status do gateway.</span><span class="sxs-lookup"><span data-stu-id="0c695-177">Use the `Get-AzureApplicationGateway` cmdlet to check the status of the gateway.</span></span> <span data-ttu-id="0c695-178">Se `Start-AzureApplicationGateway` foi bem-sucedido na etapa anterior, o item *Estado* deverá ser Em execução e *VirtualIPs* e *DnsName* deverão ter entradas válidas.</span><span class="sxs-lookup"><span data-stu-id="0c695-178">If `Start-AzureApplicationGateway` succeeded in the previous step, *State* should be Running, and *VirtualIPs* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="0c695-179">Este exemplo mostra um Application Gateway que está ativo, em execução e pronto para receber tráfego.</span><span class="sxs-lookup"><span data-stu-id="0c695-179">This sample shows an application gateway that is up, running, and is ready to take traffic.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0c695-180">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0c695-180">Next steps</span></span>

<span data-ttu-id="0c695-181">Se deseja obter mais informações sobre as opções de balanceamento de carga no geral, consulte:</span><span class="sxs-lookup"><span data-stu-id="0c695-181">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="0c695-182">Balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="0c695-182">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="0c695-183">Gerenciador de Tráfego do Azure</span><span class="sxs-lookup"><span data-stu-id="0c695-183">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

