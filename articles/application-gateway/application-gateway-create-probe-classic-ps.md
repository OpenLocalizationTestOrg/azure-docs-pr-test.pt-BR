---
title: "aaaCreate clássico de PowerShell uma investigação personalizada - Gateway de aplicativo do Azure - | Microsoft Docs"
description: "Saiba como toocreate um personalizado teste para o Application Gateway usando o PowerShell no modelo de implantação clássico Olá"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 338a7be1-835c-48e9-a072-95662dc30f5e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 68332367c99328bd6456b0c339923765637be986
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a><span data-ttu-id="31997-103">Criar uma investigação personalizada para o Gateway de Aplicativo (clássico) pelo uso do PowerShell</span><span class="sxs-lookup"><span data-stu-id="31997-103">Create a custom probe for Azure Application Gateway (classic) by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="31997-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="31997-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="31997-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="31997-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="31997-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="31997-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="31997-107">Neste artigo, você deve adicionar um gateway de aplicativo existente do investigação personalizada tooan com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31997-107">In this article, you add a custom probe tooan existing application gateway with PowerShell.</span></span> <span data-ttu-id="31997-108">Testes personalizados são úteis para aplicativos que têm uma página de verificação de integridade específicas ou para aplicativos que não fornecem uma resposta bem-sucedida no aplicativo de web saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="31997-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on hello default web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="31997-109">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="31997-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="31997-110">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="31997-110">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="31997-111">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="31997-111">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="31997-112">Saiba como muito[executar essas etapas usando o modelo do Gerenciador de recursos de saudação](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="31997-112">Learn how too[perform these steps using hello Resource Manager model](application-gateway-create-probe-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a><span data-ttu-id="31997-113">Criar um Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="31997-113">Create an application gateway</span></span>

<span data-ttu-id="31997-114">toocreate um application gateway:</span><span class="sxs-lookup"><span data-stu-id="31997-114">toocreate an application gateway:</span></span>

1. <span data-ttu-id="31997-115">Criar um recurso de gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="31997-115">Create an application gateway resource.</span></span>
2. <span data-ttu-id="31997-116">Crie um arquivo XML de configuração ou um objeto de configuração.</span><span class="sxs-lookup"><span data-stu-id="31997-116">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="31997-117">Confirme Olá configuração toohello recém-criados em recursos de gateway do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="31997-117">Commit hello configuration toohello newly created application gateway resource.</span></span>

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a><span data-ttu-id="31997-118">Criar um recurso de gateway de aplicativo com uma investigação personalizada</span><span class="sxs-lookup"><span data-stu-id="31997-118">Create an application gateway resource with a custom probe</span></span>

<span data-ttu-id="31997-119">gateway toocreate Olá Olá use `New-AzureApplicationGateway` cmdlet, substituindo os valores hello com seus próprios.</span><span class="sxs-lookup"><span data-stu-id="31997-119">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="31997-120">Cobrança para o gateway de saudação não funciona neste momento.</span><span class="sxs-lookup"><span data-stu-id="31997-120">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="31997-121">A cobrança começa em uma etapa posterior, quando o gateway Olá foi iniciado com êxito.</span><span class="sxs-lookup"><span data-stu-id="31997-121">Billing begins in a later step, when hello gateway is successfully started.</span></span>

<span data-ttu-id="31997-122">Olá exemplo a seguir cria um application gateway usando uma rede virtual chamada "testvnet1" e uma sub-rede denominada "subnet-1".</span><span class="sxs-lookup"><span data-stu-id="31997-122">hello following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1".</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="31997-123">toovalidate que Olá gateway foi criado, você pode usar o hello `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="31997-123">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> <span data-ttu-id="31997-124">Olá valor padrão para *InstanceCount* é 2, com um valor máximo de 10.</span><span class="sxs-lookup"><span data-stu-id="31997-124">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="31997-125">Olá valor padrão para *GatewaySize* é médio.</span><span class="sxs-lookup"><span data-stu-id="31997-125">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="31997-126">Você pode escolher entre Small, Medium e Large.</span><span class="sxs-lookup"><span data-stu-id="31997-126">You can choose between Small, Medium, and Large.</span></span>
> 
> 

<span data-ttu-id="31997-127">*VirtualIPs* e *DnsName* são mostrados como em branco porque o gateway Olá ainda não foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="31997-127">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="31997-128">Esses valores são criados depois que o gateway de hello está em estado de execução de saudação.</span><span class="sxs-lookup"><span data-stu-id="31997-128">These values are created once hello gateway is in hello running state.</span></span>

### <a name="configure-an-application-gateway-by-using-xml"></a><span data-ttu-id="31997-129">Configurar um Application Gateway usando XML</span><span class="sxs-lookup"><span data-stu-id="31997-129">Configure an application gateway by using XML</span></span>

<span data-ttu-id="31997-130">Em Olá exemplo a seguir, use um tooconfigure do arquivo XML todas as configurações de gateway do aplicativo e confirmá-las toohello recursos de gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="31997-130">In hello following example, you use an XML file tooconfigure all application gateway settings and commit them toohello application gateway resource.</span></span>  

<span data-ttu-id="31997-131">Saudação de cópia tooNotepad de texto a seguir.</span><span class="sxs-lookup"><span data-stu-id="31997-131">Copy hello following text tooNotepad.</span></span>

```xml
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
<FrontendIPConfigurations>
    <FrontendIPConfiguration>
        <Name>fip1</Name>
        <Type>Private</Type>
    </FrontendIPConfiguration>
</FrontendIPConfigurations>
<FrontendPorts>
    <FrontendPort>
        <Name>port1</Name>
        <Port>80</Port>
    </FrontendPort>
</FrontendPorts>
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
    </Probes>
    <BackendAddressPools>
    <BackendAddressPool>
        <Name>pool1</Name>
        <IPAddresses>
            <IPAddress>1.1.1.1</IPAddress>
            <IPAddress>2.2.2.2</IPAddress>
        </IPAddresses>
    </BackendAddressPool>
</BackendAddressPools>
<BackendHttpSettingsList>
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
</BackendHttpSettingsList>
<HttpListeners>
    <HttpListener>
        <Name>listener1</Name>
        <FrontendIP>fip1</FrontendIP>
    <FrontendPort>port1</FrontendPort>
        <Protocol>Http</Protocol>
    </HttpListener>
</HttpListeners>
<HttpLoadBalancingRules>
    <HttpLoadBalancingRule>
        <Name>lbrule1</Name>
        <Type>basic</Type>
        <BackendHttpSettings>setting1</BackendHttpSettings>
        <Listener>listener1</Listener>
        <BackendAddressPool>pool1</BackendAddressPool>
    </HttpLoadBalancingRule>
</HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

<span data-ttu-id="31997-132">Edite valores de saudação entre parênteses Olá Olá para itens de configuração.</span><span class="sxs-lookup"><span data-stu-id="31997-132">Edit hello values between hello parentheses for hello configuration items.</span></span> <span data-ttu-id="31997-133">Salve o arquivo de saudação com extensão. XML.</span><span class="sxs-lookup"><span data-stu-id="31997-133">Save hello file with extension .xml.</span></span>

<span data-ttu-id="31997-134">Olá exemplo a seguir mostra como toouse um tooset do arquivo de configuração o tooload de gateway do aplicativo hello equilibrar o tráfego HTTP na porta pública 80 e enviar tráfego de rede a porta 80 tooback ponta entre dois endereços IP por meio de uma investigação personalizada.</span><span class="sxs-lookup"><span data-stu-id="31997-134">hello following example shows how toouse a configuration file tooset up hello application gateway tooload balance HTTP traffic on public port 80 and send network traffic tooback-end port 80 between two IP addresses by using a custom probe.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="31997-135">item de protocolo Hello Http ou Https diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="31997-135">hello protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="31997-136">Um novo item de configuração \<investigação\> é adicionado investigações de tooconfigure personalizado.</span><span class="sxs-lookup"><span data-stu-id="31997-136">A new configuration item \<Probe\> is added tooconfigure custom probes.</span></span>

<span data-ttu-id="31997-137">parâmetros de configuração de saudação são:</span><span class="sxs-lookup"><span data-stu-id="31997-137">hello configuration parameters are:</span></span>

|<span data-ttu-id="31997-138">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="31997-138">Parameter</span></span>|<span data-ttu-id="31997-139">Descrição</span><span class="sxs-lookup"><span data-stu-id="31997-139">Description</span></span>|
|---|---|
|<span data-ttu-id="31997-140">**Nome**</span><span class="sxs-lookup"><span data-stu-id="31997-140">**Name**</span></span> |<span data-ttu-id="31997-141">Nome de referência da investigação personalizada.</span><span class="sxs-lookup"><span data-stu-id="31997-141">Reference name for custom probe.</span></span> |
<span data-ttu-id="31997-142">* **Protocolo**</span><span class="sxs-lookup"><span data-stu-id="31997-142">* **Protocol**</span></span> | <span data-ttu-id="31997-143">Protocolo usado (os valores possíveis são HTTP ou HTTPS).</span><span class="sxs-lookup"><span data-stu-id="31997-143">Protocol used (possible values are HTTP or HTTPS).</span></span>|
| <span data-ttu-id="31997-144">**Host** e **Path**</span><span class="sxs-lookup"><span data-stu-id="31997-144">**Host** and **Path**</span></span> | <span data-ttu-id="31997-145">Caminho completo do URL que é invocado com a integridade de Olá Olá aplicativos gateway toodetermine da instância de saudação.</span><span class="sxs-lookup"><span data-stu-id="31997-145">Complete URL path that is invoked by hello application gateway toodetermine hello health of hello instance.</span></span> <span data-ttu-id="31997-146">Por exemplo, se você tiver http://contoso.com/ um site, e a investigação personalizada Olá pode ser configurada para "http://contoso.com/path/custompath.htm" para teste verifica toohave uma resposta HTTP bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="31997-146">For example, if you have a website http://contoso.com/, then hello custom probe can be configured for "http://contoso.com/path/custompath.htm" for probe checks toohave a successful HTTP response.</span></span>|
| <span data-ttu-id="31997-147">**Intervalo**</span><span class="sxs-lookup"><span data-stu-id="31997-147">**Interval**</span></span> | <span data-ttu-id="31997-148">Configura as verificações de intervalo de investigação de saudação em segundos.</span><span class="sxs-lookup"><span data-stu-id="31997-148">Configures hello probe interval checks in seconds.</span></span>|
| <span data-ttu-id="31997-149">**Tempo limite**</span><span class="sxs-lookup"><span data-stu-id="31997-149">**Timeout**</span></span> | <span data-ttu-id="31997-150">Define o tempo limite de investigação de saudação para uma verificação de resposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="31997-150">Defines hello probe time-out for an HTTP response check.</span></span>|
| <span data-ttu-id="31997-151">**UnhealthyThreshold**</span><span class="sxs-lookup"><span data-stu-id="31997-151">**UnhealthyThreshold**</span></span> | <span data-ttu-id="31997-152">Olá o número de respostas HTTP com falha necessário tooflag Olá back-end a instância como *Íntegro*.</span><span class="sxs-lookup"><span data-stu-id="31997-152">hello number of failed HTTP responses needed tooflag hello back-end instance as *unhealthy*.</span></span>|

<span data-ttu-id="31997-153">nome do teste Olá é referenciado em Olá \<BackendHttpSettings\> tooassign configuração qual pool de back-end usa configurações de investigação personalizada.</span><span class="sxs-lookup"><span data-stu-id="31997-153">hello probe name is referenced in hello \<BackendHttpSettings\> configuration tooassign which back-end pool uses custom probe settings.</span></span>

## <a name="add-a-custom-probe-tooan-existing-application-gateway"></a><span data-ttu-id="31997-154">Adicionar um gateway de aplicativo investigação personalizada tooan existente</span><span class="sxs-lookup"><span data-stu-id="31997-154">Add a custom probe tooan existing application gateway</span></span>

<span data-ttu-id="31997-155">Alteração da configuração atual Olá de um gateway de aplicativo requer três etapas: obter o arquivo de configuração XML atual hello, modificar toohave uma investigação personalizada e configurar o gateway de aplicativo hello com novas configurações de XML hello.</span><span class="sxs-lookup"><span data-stu-id="31997-155">Changing hello current configuration of an application gateway requires three steps: Get hello current XML configuration file, modify toohave a custom probe, and configure hello application gateway with hello new XML settings.</span></span>

1. <span data-ttu-id="31997-156">Obter o arquivo XML de saudação usando `Get-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="31997-156">Get hello XML file by using `Get-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="31997-157">Esse cmdlet exporta Olá configuração XML toobe modificado tooadd uma configuração de teste.</span><span class="sxs-lookup"><span data-stu-id="31997-157">This cmdlet exports hello configuration XML toobe modified tooadd a probe setting.</span></span>

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path toofile>"
  ```

1. <span data-ttu-id="31997-158">Abra o arquivo XML de saudação em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="31997-158">Open hello XML file in a text editor.</span></span> <span data-ttu-id="31997-159">Adicione uma seção `<probe>` após `<frontendport>`.</span><span class="sxs-lookup"><span data-stu-id="31997-159">Add a `<probe>` section after `<frontendport>`.</span></span>

  ```xml
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
</Probes>
  ```

  <span data-ttu-id="31997-160">Na seção de backendHttpSettings de saudação da saudação XML, adicione o nome de investigação de saudação conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="31997-160">In hello backendHttpSettings section of hello XML, add hello probe name as shown in hello following example:</span></span>

  ```xml
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
  ```

  <span data-ttu-id="31997-161">Salve o arquivo XML de saudação.</span><span class="sxs-lookup"><span data-stu-id="31997-161">Save hello XML file.</span></span>

1. <span data-ttu-id="31997-162">Configuração do gateway atualização Olá aplicativo com o novo arquivo XML hello usando `Set-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="31997-162">Update hello application gateway configuration with hello new XML file by using `Set-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="31997-163">Esse cmdlet atualiza seu gateway de aplicativo com a nova configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="31997-163">This cmdlet updates your application gateway with hello new configuration.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path toofile>"
```

## <a name="next-steps"></a><span data-ttu-id="31997-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="31997-164">Next steps</span></span>

<span data-ttu-id="31997-165">Se você quiser tooconfigure descarregamento de SSL Secure Sockets Layer (), consulte [Configure um gateway de aplicativo para descarregamento SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="31997-165">If you want tooconfigure Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="31997-166">Se você quiser tooconfigure um toouse de gateway do aplicativo com um balanceador de carga interno, consulte [criar um gateway de aplicativo com um balanceador de carga interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="31997-166">If you want tooconfigure an application gateway toouse with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

