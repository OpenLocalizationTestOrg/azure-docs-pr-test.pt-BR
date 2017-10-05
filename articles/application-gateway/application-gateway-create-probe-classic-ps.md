---
title: "Criar uma investigação personalizada - Gateway de Aplicativo do Azure - PowerShell clássico | Microsoft Docs"
description: "Saiba como criar uma investigação personalizada para o Gateway de Aplicativo usando o PowerShell no modelo de implantação clássico"
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
ms.openlocfilehash: bf190741b10c10e885d927ad21a9f2b25107943f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a><span data-ttu-id="3de85-103">Criar uma investigação personalizada para o Gateway de Aplicativo (clássico) pelo uso do PowerShell</span><span class="sxs-lookup"><span data-stu-id="3de85-103">Create a custom probe for Azure Application Gateway (classic) by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3de85-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3de85-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="3de85-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3de85-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="3de85-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="3de85-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="3de85-107">Neste artigo, você adiciona uma investigação personalizada a um gateway de aplicativo existente com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3de85-107">In this article, you add a custom probe to an existing application gateway with PowerShell.</span></span> <span data-ttu-id="3de85-108">As investigações personalizadas são úteis para aplicativos que tenham uma página de verificação de integridade específica ou para aplicativos que não forneçam uma resposta bem-sucedida no aplicativo Web padrão.</span><span class="sxs-lookup"><span data-stu-id="3de85-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on the default web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3de85-109">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3de85-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3de85-110">Este artigo aborda o uso do modelo de implantação Clássica.</span><span class="sxs-lookup"><span data-stu-id="3de85-110">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="3de85-111">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="3de85-111">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="3de85-112">Saiba como [executar estas etapas usando o modelo do Resource Manager](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="3de85-112">Learn how to [perform these steps using the Resource Manager model](application-gateway-create-probe-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a><span data-ttu-id="3de85-113">Criar um Application Gateway</span><span class="sxs-lookup"><span data-stu-id="3de85-113">Create an application gateway</span></span>

<span data-ttu-id="3de85-114">Para criar um Application Gateway:</span><span class="sxs-lookup"><span data-stu-id="3de85-114">To create an application gateway:</span></span>

1. <span data-ttu-id="3de85-115">Criar um recurso de gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3de85-115">Create an application gateway resource.</span></span>
2. <span data-ttu-id="3de85-116">Crie um arquivo XML de configuração ou um objeto de configuração.</span><span class="sxs-lookup"><span data-stu-id="3de85-116">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="3de85-117">Confirme a configuração do recurso de gateway de aplicativo recém-criado.</span><span class="sxs-lookup"><span data-stu-id="3de85-117">Commit the configuration to the newly created application gateway resource.</span></span>

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a><span data-ttu-id="3de85-118">Criar um recurso de gateway de aplicativo com uma investigação personalizada</span><span class="sxs-lookup"><span data-stu-id="3de85-118">Create an application gateway resource with a custom probe</span></span>

<span data-ttu-id="3de85-119">Para criar o gateway, use o cmdlet `New-AzureApplicationGateway`, substituindo os valores pelos seus próprios.</span><span class="sxs-lookup"><span data-stu-id="3de85-119">To create the gateway, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="3de85-120">A cobrança pelo gateway não se inicia neste momento.</span><span class="sxs-lookup"><span data-stu-id="3de85-120">Billing for the gateway does not start at this point.</span></span> <span data-ttu-id="3de85-121">A cobrança é iniciada em uma etapa posterior, quando o gateway é iniciado com êxito.</span><span class="sxs-lookup"><span data-stu-id="3de85-121">Billing begins in a later step, when the gateway is successfully started.</span></span>

<span data-ttu-id="3de85-122">O exemplo a seguir cria um novo Application Gateway usando uma rede virtual chamada "testvnet1" e uma sub-rede chamada "subnet-1".</span><span class="sxs-lookup"><span data-stu-id="3de85-122">The following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1".</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="3de85-123">Para validar esse gateway que foi criado, você pode usar o cmdlet `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="3de85-123">To validate that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> <span data-ttu-id="3de85-124">O valor padrão para *InstanceCount* é 2, com um valor máximo de 10.</span><span class="sxs-lookup"><span data-stu-id="3de85-124">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="3de85-125">O valor padrão para *GatewaySize* é Medium.</span><span class="sxs-lookup"><span data-stu-id="3de85-125">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="3de85-126">Você pode escolher entre Small, Medium e Large.</span><span class="sxs-lookup"><span data-stu-id="3de85-126">You can choose between Small, Medium, and Large.</span></span>
> 
> 

<span data-ttu-id="3de85-127">*VirtualIPs* e *DnsName* são mostrados em branco porque o gateway ainda não foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="3de85-127">*VirtualIPs* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="3de85-128">Esses valores serão criados depois que o gateway estiver em estado de execução.</span><span class="sxs-lookup"><span data-stu-id="3de85-128">These values are created once the gateway is in the running state.</span></span>

### <a name="configure-an-application-gateway-by-using-xml"></a><span data-ttu-id="3de85-129">Configurar um Application Gateway usando XML</span><span class="sxs-lookup"><span data-stu-id="3de85-129">Configure an application gateway by using XML</span></span>

<span data-ttu-id="3de85-130">No exemplo a seguir, você usará um arquivo XML para definir todas as configurações do Application Gateway e confirmá-las para o recurso do Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="3de85-130">In the following example, you use an XML file to configure all application gateway settings and commit them to the application gateway resource.</span></span>  

<span data-ttu-id="3de85-131">Copie o seguinte texto no bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="3de85-131">Copy the following text to Notepad.</span></span>

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

<span data-ttu-id="3de85-132">Edite os valores entre parênteses para os itens de configuração.</span><span class="sxs-lookup"><span data-stu-id="3de85-132">Edit the values between the parentheses for the configuration items.</span></span> <span data-ttu-id="3de85-133">Salve o arquivo com a extensão .xml.</span><span class="sxs-lookup"><span data-stu-id="3de85-133">Save the file with extension .xml.</span></span>

<span data-ttu-id="3de85-134">O exemplo a seguir mostra como usar um arquivo de configuração configurando o Application Gateway para balancear a carga do tráfego HTTP na porta pública 80 e enviando o tráfego de rede para a porta 80 do back-end entre dois endereços IP pelo uso de uma investigação personalizada.</span><span class="sxs-lookup"><span data-stu-id="3de85-134">The following example shows how to use a configuration file to set up the application gateway to load balance HTTP traffic on public port 80 and send network traffic to back-end port 80 between two IP addresses by using a custom probe.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3de85-135">O item de protocolo Http ou Https diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="3de85-135">The protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="3de85-136">Um novo item de configuração \<Probe\> é adicionado para configurar investigações personalizadas.</span><span class="sxs-lookup"><span data-stu-id="3de85-136">A new configuration item \<Probe\> is added to configure custom probes.</span></span>

<span data-ttu-id="3de85-137">Os parâmetros de configuração são:</span><span class="sxs-lookup"><span data-stu-id="3de85-137">The configuration parameters are:</span></span>

|<span data-ttu-id="3de85-138">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="3de85-138">Parameter</span></span>|<span data-ttu-id="3de85-139">Descrição</span><span class="sxs-lookup"><span data-stu-id="3de85-139">Description</span></span>|
|---|---|
|<span data-ttu-id="3de85-140">**Nome**</span><span class="sxs-lookup"><span data-stu-id="3de85-140">**Name**</span></span> |<span data-ttu-id="3de85-141">Nome de referência da investigação personalizada.</span><span class="sxs-lookup"><span data-stu-id="3de85-141">Reference name for custom probe.</span></span> |
<span data-ttu-id="3de85-142">* **Protocolo**</span><span class="sxs-lookup"><span data-stu-id="3de85-142">* **Protocol**</span></span> | <span data-ttu-id="3de85-143">Protocolo usado (os valores possíveis são HTTP ou HTTPS).</span><span class="sxs-lookup"><span data-stu-id="3de85-143">Protocol used (possible values are HTTP or HTTPS).</span></span>|
| <span data-ttu-id="3de85-144">**Host** e **Path**</span><span class="sxs-lookup"><span data-stu-id="3de85-144">**Host** and **Path**</span></span> | <span data-ttu-id="3de85-145">Caminho de URL completo que é invocado pelo Gateway de Aplicativo para determinar a integridade da instância.</span><span class="sxs-lookup"><span data-stu-id="3de85-145">Complete URL path that is invoked by the application gateway to determine the health of the instance.</span></span> <span data-ttu-id="3de85-146">Por exemplo, se você tiver um site http://contoso.com/, a investigação personalizada poderá ser configurada para "http://contoso.com/path/custompath.htm" para verificações de investigação com uma resposta HTTP bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="3de85-146">For example, if you have a website http://contoso.com/, then the custom probe can be configured for "http://contoso.com/path/custompath.htm" for probe checks to have a successful HTTP response.</span></span>|
| <span data-ttu-id="3de85-147">**Intervalo**</span><span class="sxs-lookup"><span data-stu-id="3de85-147">**Interval**</span></span> | <span data-ttu-id="3de85-148">Configura as verificações de intervalo de investigação em segundos.</span><span class="sxs-lookup"><span data-stu-id="3de85-148">Configures the probe interval checks in seconds.</span></span>|
| <span data-ttu-id="3de85-149">**Tempo limite**</span><span class="sxs-lookup"><span data-stu-id="3de85-149">**Timeout**</span></span> | <span data-ttu-id="3de85-150">Define o tempo limite da investigação para uma verificação de resposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="3de85-150">Defines the probe time-out for an HTTP response check.</span></span>|
| <span data-ttu-id="3de85-151">**UnhealthyThreshold**</span><span class="sxs-lookup"><span data-stu-id="3de85-151">**UnhealthyThreshold**</span></span> | <span data-ttu-id="3de85-152">O número de respostas HTTP com falha necessárias para sinalizar a instância de back-end como *unhealthy*.</span><span class="sxs-lookup"><span data-stu-id="3de85-152">The number of failed HTTP responses needed to flag the back-end instance as *unhealthy*.</span></span>|

<span data-ttu-id="3de85-153">O nome da investigação é referenciado na configuração \<BackendHttpSettings\> para atribuir qual pool de back-end usa as configurações da investigação personalizada.</span><span class="sxs-lookup"><span data-stu-id="3de85-153">The probe name is referenced in the \<BackendHttpSettings\> configuration to assign which back-end pool uses custom probe settings.</span></span>

## <a name="add-a-custom-probe-to-an-existing-application-gateway"></a><span data-ttu-id="3de85-154">Adicionar uma investigação personalizada a um gateway de aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="3de85-154">Add a custom probe to an existing application gateway</span></span>

<span data-ttu-id="3de85-155">Alterar a configuração atual de um Application Gateway exige três etapas: obter o arquivo de configuração XML atual, modificar para ter uma investigação personalizada e configurar o Application Gateway com as novas configurações de XML.</span><span class="sxs-lookup"><span data-stu-id="3de85-155">Changing the current configuration of an application gateway requires three steps: Get the current XML configuration file, modify to have a custom probe, and configure the application gateway with the new XML settings.</span></span>

1. <span data-ttu-id="3de85-156">Obtenha o arquivo XML usando `Get-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="3de85-156">Get the XML file by using `Get-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="3de85-157">Este cmdlet exporta o XML de configuração a ser modificado para adicionar uma configuração de investigação.</span><span class="sxs-lookup"><span data-stu-id="3de85-157">This cmdlet exports the configuration XML to be modified to add a probe setting.</span></span>

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path to file>"
  ```

1. <span data-ttu-id="3de85-158">Abra o arquivo XML em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="3de85-158">Open the XML file in a text editor.</span></span> <span data-ttu-id="3de85-159">Adicione uma seção `<probe>` após `<frontendport>`.</span><span class="sxs-lookup"><span data-stu-id="3de85-159">Add a `<probe>` section after `<frontendport>`.</span></span>

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

  <span data-ttu-id="3de85-160">Na seção backendHttpSettings do XML, adicione o nome da investigação como mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="3de85-160">In the backendHttpSettings section of the XML, add the probe name as shown in the following example:</span></span>

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

  <span data-ttu-id="3de85-161">Salve o arquivo XML.</span><span class="sxs-lookup"><span data-stu-id="3de85-161">Save the XML file.</span></span>

1. <span data-ttu-id="3de85-162">Atualize a configuração do Gateway de Aplicativo com o novo arquivo XML usando `Set-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="3de85-162">Update the application gateway configuration with the new XML file by using `Set-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="3de85-163">Este cmdlet atualiza seu Gateway de Aplicativo com a nova configuração.</span><span class="sxs-lookup"><span data-stu-id="3de85-163">This cmdlet updates your application gateway with the new configuration.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path to file>"
```

## <a name="next-steps"></a><span data-ttu-id="3de85-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3de85-164">Next steps</span></span>

<span data-ttu-id="3de85-165">Se você quiser configurar o descarregamento de protocolo SSL, consulte [Configurar um Application Gateway para o descarregamento SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="3de85-165">If you want to configure Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="3de85-166">Para configurar um gateway de aplicativo para usar com um balanceador de carga interno, confira [Criar um gateway de aplicativo com um ILB (balanceador de carga interno)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="3de85-166">If you want to configure an application gateway to use with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

