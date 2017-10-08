---
title: aaaHow toouse gerenciamento de API do Azure na rede Virtual com o Application Gateway | Microsoft Docs
description: Saiba como toosetup e configurar o gerenciamento de API do Azure na rede interna Virtual com o Application Gateway (WAF) como front-end
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: antonba
ms.assetid: a8c982b2-bca5-4312-9367-4a0bbc1082b1
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2017
ms.author: sasolank
ms.openlocfilehash: 74303a2ee8a10db633ab1740ec7267728eacb473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a><span data-ttu-id="cf6cf-103">Como integrar o gerenciamento de API em uma VNET interna com o gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="cf6cf-103">Integrate API Management in an internal VNET with Application Gateway</span></span> 

##<span data-ttu-id="cf6cf-104"><a name="overview"> </a> Visão geral</span><span class="sxs-lookup"><span data-stu-id="cf6cf-104"><a name="overview"> </a> Overview</span></span>
 
<span data-ttu-id="cf6cf-105">Olá serviço de gerenciamento de API pode ser configurado em uma rede Virtual no modo interno que é acessível somente dentro Olá rede Virtual.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-105">hello API Management service can be configured in a Virtual Network in internal mode which makes it accessible only from within hello Virtual Network.</span></span> <span data-ttu-id="cf6cf-106">O Gateway de Aplicativo do Azure é um Serviço PAAS que fornece um balanceador de carga de Camada 7.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-106">Azure Application Gateway is a PAAS Service which provides a Layer-7 load balancer.</span></span> <span data-ttu-id="cf6cf-107">Ele atua como um serviço de proxy reverso e fornece também um firewall do aplicativo Web (WAF).</span><span class="sxs-lookup"><span data-stu-id="cf6cf-107">It acts as a reverse-proxy service and provides among its offering a Web Application Firewall (WAF).</span></span>

<span data-ttu-id="cf6cf-108">Combinar provisionado em uma rede virtual interna com front-end Olá Application Gateway de gerenciamento de API permite Olá os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="cf6cf-108">Combining API Management provisioned in an internal VNET with hello Application Gateway frontend enables hello following scenarios:</span></span>

* <span data-ttu-id="cf6cf-109">Use Olá mesmo recurso de gerenciamento de API para consumo por clientes internos e externos consumidores.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-109">Use hello same API Management resource for consumption by both internal consumers and external consumers.</span></span>
* <span data-ttu-id="cf6cf-110">Usar um único recurso de Gerenciamento de API e ter uma sub-rede de APIs definida no Gerenciamento de API disponível para consumidores externos.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-110">Use a single API Management resource and have a subset of APIs defined in API Management available for external consumers.</span></span>
* <span data-ttu-id="cf6cf-111">Fornecem uma maneira de turnkey tooswitch acesso tooAPI gerenciamento de saudação Internet pública e desativar.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-111">Provide a turn-key way tooswitch access tooAPI Management from hello public Internet on and off.</span></span> 

##<span data-ttu-id="cf6cf-112"><a name="scenario"> </a> Cenário</span><span class="sxs-lookup"><span data-stu-id="cf6cf-112"><a name="scenario"> </a> Scenario</span></span>
<span data-ttu-id="cf6cf-113">Este artigo aborda como toouse uma única API de gerenciamento de serviço para clientes internos e externos e torná-la atuar como um único front-end para ambos os locais e APIs de nuvem.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-113">This article will cover how toouse a single API Management service for both internal and external consumers and make it act as a single frontend for both on-prem and cloud APIs.</span></span> <span data-ttu-id="cf6cf-114">Você também verá como tooexpose apenas um subconjunto de suas APIs (por exemplo hello realçados em verde) para consumo externo usando a funcionalidade de PathBasedRouting Olá disponível no Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-114">You will also see how tooexpose only a subset of your APIs (in hello example they are highlighted in green) for External Consumption using hello PathBasedRouting functionality available in Application Gateway.</span></span>

<span data-ttu-id="cf6cf-115">No primeiro exemplo hello todas as suas APIs são gerenciados somente de dentro de sua rede Virtual.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-115">In hello first setup example all your APIs are managed only from within your Virtual Network.</span></span> <span data-ttu-id="cf6cf-116">Os consumidores internos (destacados em laranja) podem acessar todas as APIs internas e externas.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-116">Internal consumers (highlighted in orange) can access all your internal and external APIs.</span></span> <span data-ttu-id="cf6cf-117">Tráfego nunca sai tooInternet que um alto desempenho é fornecido por meio de circuitos de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-117">Traffic never goes out tooInternet a high performance is delivered via Express Route circuits.</span></span>

![roteamento de url](./media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <span data-ttu-id="cf6cf-119"><a name="before-you-begin"> </a> Antes de começar</span><span class="sxs-lookup"><span data-stu-id="cf6cf-119"><a name="before-you-begin"> </a> Before you begin</span></span>

1. <span data-ttu-id="cf6cf-120">Instale a versão mais recente Olá Olá Azure de cmdlets do PowerShell usando Olá Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-120">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="cf6cf-121">Você pode baixar e instalar a versão mais recente de saudação do hello **do Windows PowerShell** seção Olá [página de Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="cf6cf-121">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="cf6cf-122">Crie uma rede virtual e sub-redes separadas para o gerenciamento de API e o gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-122">Create a Virtual Network and create separate subnets for API Management and Application Gateway.</span></span> 
3. <span data-ttu-id="cf6cf-123">Se você pretende toocreate um servidor DNS personalizado para Olá rede Virtual, você deve fazer isso antes de iniciar a implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-123">If you intend toocreate a custom DNS server for hello Virtual Network, do so before starting hello deployment.</span></span> <span data-ttu-id="cf6cf-124">Verifique que ele funciona, garantindo uma máquina virtual criada em uma nova sub-rede na rede Virtual de saudação pode resolver e acessar todos os pontos de extremidade de serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-124">Double check it works by ensuring a virtual machine created in a new subnet in hello Virtual Network can resolve and access all Azure service endpoints.</span></span>

## <a name="what-is-required-toocreate-an-integration-between-api-management-and-application-gateway"></a><span data-ttu-id="cf6cf-125">O que é necessário toocreate uma integração entre o gerenciamento de API e o Application Gateway?</span><span class="sxs-lookup"><span data-stu-id="cf6cf-125">What is required toocreate an integration between API Management and Application Gateway?</span></span>

* <span data-ttu-id="cf6cf-126">**Pool de servidores de back-end:** trata Olá virtual endereço IP interno do hello serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-126">**Back-end server pool:** This is hello internal virtual IP address of hello API Management service.</span></span>
* <span data-ttu-id="cf6cf-127">**Configurações do pool de servidores back-end:** cada pool tem configurações como porta, protocolo e afinidade baseada em cookie.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-127">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="cf6cf-128">Essas configurações são aplicadas tooall servidores no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-128">These settings are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="cf6cf-129">**Porta de front-end:** é Olá porta pública que é aberta no gateway do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-129">**Front-end port:** This is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="cf6cf-130">Tráfego atingi-lo obtém tooone redirecionado de saudação servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-130">Traffic hitting it gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="cf6cf-131">**Ouvinte:** ouvinte Olá tem uma porta de front-end, um protocolo (Http ou Https, esses valores diferenciam maiusculas de minúsculas) e o nome do certificado SSL de saudação (se a configuração de SSL de descarregamento).</span><span class="sxs-lookup"><span data-stu-id="cf6cf-131">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="cf6cf-132">**Regra:** regra Olá associa um pool de servidores de back-end de tooa de ouvinte.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-132">**Rule:** hello rule binds a listener tooa back-end server pool.</span></span>
* <span data-ttu-id="cf6cf-133">**Investigação de integridade personalizada:** Application Gateway, por padrão, usa toofigure de testes com base em endereços IP quais servidores de saudação BackendAddressPool estão ativos.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-133">**Custom Health Probe:** Application Gateway, by default, uses IP address based probes toofigure out which servers in hello BackendAddressPool are active.</span></span> <span data-ttu-id="cf6cf-134">Olá serviço de gerenciamento de API responde apenas toorequests que têm o cabeçalho de host correto hello, portanto, investigações de padrão de saudação falharem.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-134">hello API Management service only responds toorequests which have hello correct host header, hence hello default probes fail.</span></span> <span data-ttu-id="cf6cf-135">Precisa de um teste de integridade personalizado toobe definido pelo gateway de aplicativo toohelp determinar que serviço hello está ativo e encaminhar solicitações.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-135">A custom health probe needs toobe defined toohelp application gateway determine that hello service is alive and it should forward requests.</span></span>
* <span data-ttu-id="cf6cf-136">**Certificado de domínio personalizado:** tooaccess gerenciamento de API de saudação à internet, você precisa toocreate um mapeamento CNAME de seu nome DNS front-end do nome de host toohello Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-136">**Custom domain certificate:** tooaccess API Management from hello internet you need toocreate a CNAME mapping of its hostname toohello Application Gateway front-end DNS name.</span></span> <span data-ttu-id="cf6cf-137">Isso garante que Olá hostname cabeçalho e um certificado enviado tooApplication Gateway é encaminhado tooAPI gerenciamento um que APIM possa reconhecer como válido.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-137">This ensures that hello hostname header and certificate sent tooApplication Gateway that is forwarded tooAPI Management is one APIM can recognize as valid.</span></span>

## <span data-ttu-id="cf6cf-138"><a name="overview-steps"> </a> Etapas necessárias para integrar o Gerenciamento de API e o Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="cf6cf-138"><a name="overview-steps"> </a> Steps required for integrating API Management and Application Gateway</span></span> 

1. <span data-ttu-id="cf6cf-139">Criar um grupo de recursos para o Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="cf6cf-140">Crie uma rede Virtual, sub-rede e IP público para Olá Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-140">Create a Virtual Network, subnet, and public IP for hello Application Gateway.</span></span> <span data-ttu-id="cf6cf-141">Crie outra sub-rede para o gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-141">Create another subnet for API Management.</span></span>
3. <span data-ttu-id="cf6cf-142">Criar um serviço de gerenciamento de API dentro da sub-rede de rede virtual Olá criado acima e certifique-se de que você usa o modo de saudação interno.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-142">Create an API Management service inside hello VNET subnet created above and ensure you use hello Internal mode.</span></span>
4. <span data-ttu-id="cf6cf-143">Configure o nome de domínio personalizado de saudação em Olá serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-143">Setup hello custom domain name in hello API Management service.</span></span>
5. <span data-ttu-id="cf6cf-144">Crie um objeto de configuração do Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-144">Create an Application Gateway configuration object.</span></span>
6. <span data-ttu-id="cf6cf-145">Crie um recurso de Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-145">Create an Application Gateway resource.</span></span>
7. <span data-ttu-id="cf6cf-146">Crie um CNAME do nome DNS público de saudação do host de proxy Olá Application Gateway toohello gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-146">Create a CNAME from hello public DNS name of hello Application Gateway toohello API Management proxy hostname.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="cf6cf-147">Criar um grupo de recursos para o Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="cf6cf-147">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="cf6cf-148">Certifique-se de que você estiver usando a versão mais recente de saudação do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-148">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="cf6cf-149">Há mais informações disponíveis em [Como usar o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="cf6cf-149">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="cf6cf-150">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="cf6cf-150">Step 1</span></span>

<span data-ttu-id="cf6cf-151">Faça logon no tooAzure</span><span class="sxs-lookup"><span data-stu-id="cf6cf-151">Log in tooAzure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="cf6cf-152">Como autenticar com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-152">Authenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="cf6cf-153">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="cf6cf-153">Step 2</span></span>

<span data-ttu-id="cf6cf-154">Verificar as assinaturas de saudação conta hello e selecioná-lo.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-154">Check hello subscriptions for hello account and select it.</span></span>

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="cf6cf-155">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="cf6cf-155">Step 3</span></span>

<span data-ttu-id="cf6cf-156">Crie um grupo de recursos (ignore esta etapa se você estiver usando um grupo de recursos existente).</span><span class="sxs-lookup"><span data-stu-id="cf6cf-156">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
<span data-ttu-id="cf6cf-157">O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="cf6cf-158">Isso é usado como o local padrão de saudação para recursos desse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-158">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="cf6cf-159">Certifique-se de que todos os comandos toocreate uma saudação de uso de gateway de aplicativo mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-159">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="cf6cf-160">Criar uma rede Virtual e uma sub-rede para o gateway de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="cf6cf-160">Create a Virtual Network and a subnet for hello application gateway</span></span>

<span data-ttu-id="cf6cf-161">saudação de exemplo a seguir mostra como toocreate usando uma rede Virtual Olá Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-161">hello following example shows how toocreate a Virtual Network using hello resource manager.</span></span>

### <a name="step-1"></a><span data-ttu-id="cf6cf-162">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="cf6cf-162">Step 1</span></span>

<span data-ttu-id="cf6cf-163">Atribua a sub-rede Olá endereço intervalo 10.0.0.0/24 toohello variável toobe usada para o Gateway de aplicativo durante a criação de uma rede Virtual.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-163">Assign hello address range 10.0.0.0/24 toohello subnet variable toobe used for Application Gateway while creating a Virtual Network.</span></span>

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a><span data-ttu-id="cf6cf-164">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="cf6cf-164">Step 2</span></span>

<span data-ttu-id="cf6cf-165">Atribua a sub-rede Olá endereço intervalo 10.0.1.0/24 toohello variável toobe usado para gerenciamento de API durante a criação de uma rede Virtual.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-165">Assign hello address range 10.0.1.0/24 toohello subnet variable toobe used for API Management while creating a Virtual Network.</span></span>

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a><span data-ttu-id="cf6cf-166">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="cf6cf-166">Step 3</span></span>

<span data-ttu-id="cf6cf-167">Criar uma rede Virtual denominado **appgwvnet** no grupo de recursos **apim-appGw-RG** para a região Oeste dos EUA de hello usando Olá prefixo 10.0.0.0/16 com sub-redes 10.0.0.0/24 e 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-167">Create a Virtual Network named **appgwvnet** in resource group **apim-appGw-RG** for hello West US region using hello prefix 10.0.0.0/16 with subnets 10.0.0.0/24 and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a><span data-ttu-id="cf6cf-168">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="cf6cf-168">Step 4</span></span>

<span data-ttu-id="cf6cf-169">Atribuir uma variável de sub-rede para as próximas etapas Olá</span><span class="sxs-lookup"><span data-stu-id="cf6cf-169">Assign a subnet variable for hello next steps</span></span>

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a><span data-ttu-id="cf6cf-170">Crie um serviço de Gerenciamento de API dentro de uma Vnet configurada no modo interno</span><span class="sxs-lookup"><span data-stu-id="cf6cf-170">Create an API Management service inside a VNET configured in internal mode</span></span>

<span data-ttu-id="cf6cf-171">Olá exemplo a seguir mostra como toocreate um serviço de gerenciamento de API em uma rede virtual configurado para acesso interno apenas.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-171">hello following example shows how toocreate an API Management service in a VNET configured for internal access only.</span></span>

### <a name="step-1"></a><span data-ttu-id="cf6cf-172">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="cf6cf-172">Step 1</span></span>
<span data-ttu-id="cf6cf-173">Crie um objeto de rede Virtual de gerenciamento de API usando Olá sub-rede $apimsubnetdata criado acima.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-173">Create an API Management Virtual Network object using hello subnet $apimsubnetdata created above.</span></span>

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a><span data-ttu-id="cf6cf-174">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="cf6cf-174">Step 2</span></span>
<span data-ttu-id="cf6cf-175">Crie um serviço de gerenciamento de API dentro Olá rede Virtual.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-175">Create an API Management service inside hello Virtual Network.</span></span>

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Developer"
```
<span data-ttu-id="cf6cf-176">Após o êxito de saudação acima comando Consulte muito[tooaccess interno serviço de gerenciamento de API de rede virtual necessária a configuração de DNS](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess-lo.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-176">After hello above command succeeds refer too[DNS Configuration required tooaccess internal VNET API Management service](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess it.</span></span>

## <a name="set-up-a-custom-domain-name-in-api-management"></a><span data-ttu-id="cf6cf-177">Configure um nome de domínio personalizado no Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="cf6cf-177">Set-up a custom domain name in API Management</span></span>

### <a name="step-1"></a><span data-ttu-id="cf6cf-178">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="cf6cf-178">Step 1</span></span>
<span data-ttu-id="cf6cf-179">Carregar certificado de saudação com chave privada para o domínio de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-179">Upload hello certificate with private key for hello domain.</span></span> <span data-ttu-id="cf6cf-180">Para este exemplo será `*.contoso.net`.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-180">For this example it will be `*.contoso.net`.</span></span> 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path too.pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a><span data-ttu-id="cf6cf-181">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="cf6cf-181">Step 2</span></span>
<span data-ttu-id="cf6cf-182">Depois que o certificado Olá é carregado, criar um objeto de configuração de nome de host para o proxy de saudação com um nome de host `api.contoso.net`, como certificado de exemplo hello fornece autoridade para Olá `*.contoso.net` domínio.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-182">Once hello certificate is uploaded, create a hostname configuration object for hello proxy with a hostname of `api.contoso.net`, as hello example certificate provides authority for hello  `*.contoso.net` domain.</span></span> 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="cf6cf-183">Criar um endereço IP público para a configuração de front-end Olá</span><span class="sxs-lookup"><span data-stu-id="cf6cf-183">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="cf6cf-184">Criar um recurso IP público **publicIP01** no grupo de recursos **apim-appGw-RG** para região Oeste dos EUA de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-184">Create a public IP resource **publicIP01** in resource group **apim-appGw-RG** for hello West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="cf6cf-185">Um endereço IP é atribuído gateway de aplicativo toohello quando Olá serviço é iniciado.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-185">An IP address is assigned toohello application gateway when hello service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="cf6cf-186">Criar uma configuração do gateway de aplicativo</span><span class="sxs-lookup"><span data-stu-id="cf6cf-186">Create application gateway configuration</span></span>

<span data-ttu-id="cf6cf-187">Todos os itens de configuração devem ser configurados antes de criar o gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-187">All configuration items must be set up before creating hello application gateway.</span></span> <span data-ttu-id="cf6cf-188">Olá etapas a seguir criam Olá itens de configuração que são necessárias para um recurso do application gateway.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-188">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="cf6cf-189">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="cf6cf-189">Step 1</span></span>

<span data-ttu-id="cf6cf-190">Crie uma configuração de IP do gateway de aplicativo chamada **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-190">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="cf6cf-191">Quando Application Gateway iniciado, ele seleciona um endereço IP da sub-rede de saudação configurado e rotear os endereços IP de toohello de tráfego de rede no pool IP de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-191">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="cf6cf-192">Tenha em mente que cada instância usa um endereço IP.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-192">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a><span data-ttu-id="cf6cf-193">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="cf6cf-193">Step 2</span></span>

<span data-ttu-id="cf6cf-194">Configure porta IP front-end de Olá para o ponto de extremidade de IP público hello.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-194">Configure hello front-end IP port for hello public IP endpoint.</span></span> <span data-ttu-id="cf6cf-195">Esta porta é Olá que os usuários finais se conectem.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-195">This port is hello port that end users connect to.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a><span data-ttu-id="cf6cf-196">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="cf6cf-196">Step 3</span></span>

<span data-ttu-id="cf6cf-197">Configure Olá IP de front-end com o ponto de extremidade IP público.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-197">Configure hello front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a><span data-ttu-id="cf6cf-198">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="cf6cf-198">Step 4</span></span>

<span data-ttu-id="cf6cf-199">Configurar certificado Olá para Application Gateway hello usado toodecrypt e criptografe novamente o tráfego de saudação passando.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-199">Configure hello certificate for hello Application Gateway, used toodecrypt and re-encrypt hello traffic passing through.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a><span data-ttu-id="cf6cf-200">Etapa 5</span><span class="sxs-lookup"><span data-stu-id="cf6cf-200">Step 5</span></span>

<span data-ttu-id="cf6cf-201">Crie o ouvinte HTTP Olá Olá Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-201">Create hello HTTP listener for hello Application Gateway.</span></span> <span data-ttu-id="cf6cf-202">Atribua a configuração de IP de front-end de hello, porta e tooit do certificado ssl.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-202">Assign hello front-end IP configuration, port, and ssl certificate tooit.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a><span data-ttu-id="cf6cf-203">Etapa 6</span><span class="sxs-lookup"><span data-stu-id="cf6cf-203">Step 6</span></span>

<span data-ttu-id="cf6cf-204">Criar um serviço de gerenciamento de API do toohello de investigação personalizada `ContosoApi` ponto de extremidade do proxy domínio.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-204">Create a custom probe toohello API Management service `ContosoApi` proxy domain endpoint.</span></span> <span data-ttu-id="cf6cf-205">caminho de saudação `/status-0123456789abcdef` é um ponto de extremidade de integridade padrão hospedado em todos os serviços de gerenciamento de API de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-205">hello path `/status-0123456789abcdef` is a default health endpoint hosted on all hello API Management services.</span></span> <span data-ttu-id="cf6cf-206">Definir `api.contoso.net` como um toosecure de nome de host de investigação personalizada com o certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-206">Set `api.contoso.net` as a custom probe hostname toosecure it with SSL certificate.</span></span>

> [!NOTE]
> <span data-ttu-id="cf6cf-207">Olá hostname `contosoapi.azure-api.net` nome do host proxy saudação padrão é configurado quando um serviço chamado `contosoapi` é criado no Azure público.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-207">hello hostname `contosoapi.azure-api.net` is hello default proxy hostname configured when a service named `contosoapi` is created in public Azure.</span></span> 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a><span data-ttu-id="cf6cf-208">Etapa 7</span><span class="sxs-lookup"><span data-stu-id="cf6cf-208">Step 7</span></span>

<span data-ttu-id="cf6cf-209">Carregar certificado Olá toobe usado em recursos do pool de back-end habilitado para SSL hello.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-209">Upload hello certificate toobe used on hello SSL-enabled backend pool resources.</span></span> <span data-ttu-id="cf6cf-210">Isso é hello mesmo certificado que você forneceu na etapa 4 acima.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-210">This is hello same certificate which you provided in Step 4 above.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path too.cer file>
```

### <a name="step-8"></a><span data-ttu-id="cf6cf-211">Etapa 8</span><span class="sxs-lookup"><span data-stu-id="cf6cf-211">Step 8</span></span>

<span data-ttu-id="cf6cf-212">Defina configurações de back-end HTTP para Olá Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-212">Configure HTTP backend settings for hello Application Gateway.</span></span> <span data-ttu-id="cf6cf-213">Isso inclui a definição de um tempo limite para solicitação de back-end após o qual elas serão canceladas.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-213">This includes setting a time-out limit for backend request after which they are cancelled.</span></span> <span data-ttu-id="cf6cf-214">Esse valor é diferente do tempo limite de investigação de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-214">This value is different from hello probe time-out.</span></span>

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a><span data-ttu-id="cf6cf-215">Etapa 9</span><span class="sxs-lookup"><span data-stu-id="cf6cf-215">Step 9</span></span>

<span data-ttu-id="cf6cf-216">Configurar um pool de endereços IP de back-end denominado **apimbackend** com endereço IP virtual interno Olá endereço de serviço de gerenciamento de API do hello criado acima.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-216">Configure a back-end IP address pool named **apimbackend**  with hello internal virtual IP address of hello API Management service created above.</span></span>

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a><span data-ttu-id="cf6cf-217">Etapa 10</span><span class="sxs-lookup"><span data-stu-id="cf6cf-217">Step 10</span></span>

<span data-ttu-id="cf6cf-218">Crie configurações para um back-end fictício (inexistente).</span><span class="sxs-lookup"><span data-stu-id="cf6cf-218">Create settings for a dummy (non-existent) backend.</span></span> <span data-ttu-id="cf6cf-219">Caminhos de tooAPI de solicitações que não queremos tooexpose do gerenciamento de API por meio do Gateway do aplicativo será atingido esse back-end e retornar 404.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-219">Requests tooAPI paths that we do not want tooexpose from API Management via Application Gateway will hit this backend and return 404.</span></span>

<span data-ttu-id="cf6cf-220">Defina configurações de HTTP de back-end de saudação fictício.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-220">Configure HTTP settings for hello dummy backend.</span></span>

```powershell
$dummyBackendSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "dummySetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="cf6cf-221">Configurar um back-end fictício **dummyBackendPool**, que aponta o endereço FQDN que tooa **dummybackend.com**. Esse endereço FQDN não existe na rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-221">Configure a dummy backend **dummyBackendPool**, which points tooa FQDN address **dummybackend.com**. This FQDN address does not exist in hello virtual network.</span></span>

```powershell
$dummyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "dummyBackendPool" -BackendFqdns "dummybackend.com"
```

<span data-ttu-id="cf6cf-222">Criar uma regra de configuração que Olá Application Gateway usará por padrão que aponta o back-end do toohello inexistente **dummybackend.com** em Olá rede Virtual.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-222">Create a rule setting that hello Application Gateway will use by default which points toohello non-existent backend **dummybackend.com** in hello Virtual Network.</span></span>

```powershell
$dummyPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "nonexistentapis" -Paths "/*" -BackendAddressPool $dummyBackendPool -BackendHttpSettings $dummyBackendSetting
```

### <a name="step-11"></a><span data-ttu-id="cf6cf-223">Etapa 11</span><span class="sxs-lookup"><span data-stu-id="cf6cf-223">Step 11</span></span>

<span data-ttu-id="cf6cf-224">Configure caminhos de regra de URL para pools de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-224">Configure URL rule paths for hello back-end pools.</span></span> <span data-ttu-id="cf6cf-225">Isso permite a seleção de apenas algumas das APIs de gerenciamento de API de saudação do que está sendo exposto toohello público.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-225">This enables selecting only some of hello APIs from API Management for being exposed toohello public.</span></span> <span data-ttu-id="cf6cf-226">Por exemplo, se houver `Echo API` (/echo/), `Calculator API` (/calc/) etc., deixe somente `Echo API` acessível na Internet.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-226">For example, if there are `Echo API` (/echo/), `Calculator API` (/calc/) etc. make only `Echo API` accessible from Internet).</span></span> 

<span data-ttu-id="cf6cf-227">Olá, exemplo a seguir cria uma regra simples para hello "echo /" caminho roteamento tráfego toohello back-end "apimProxyBackendPool".</span><span class="sxs-lookup"><span data-stu-id="cf6cf-227">hello following example creates a simple rule for hello "/echo/" path routing traffic toohello back-end "apimProxyBackendPool".</span></span>

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting
```

<span data-ttu-id="cf6cf-228">Se o caminho de saudação não corresponder caminho Olá regras queremos tooenable do gerenciamento de API, regra Olá caminho de configuração de mapa também configura um pool de endereços de back-end do padrão chamado **dummyBackendPool**.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-228">If hello path doesn't match hello path rules we want tooenable from API Management, hello rule path map configuration also configures a default back-end address pool named **dummyBackendPool**.</span></span> <span data-ttu-id="cf6cf-229">Por exemplo, http://api.contoso.net/calc/ * vai muito**dummyBackendPool** conforme ele é definido como o pool padrão de saudação para tráfego não correspondente.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-229">For example, http://api.contoso.net/calc/* goes too**dummyBackendPool** as it is defined as hello default pool for un-matched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule, $dummyPathRule -DefaultBackendAddressPool $dummyBackendPool -DefaultBackendHttpSettings $dummyBackendSetting
```

<span data-ttu-id="cf6cf-230">Olá acima etapa garante que somente as solicitações de caminho hello "/ echo" são permitidos por meio de saudação Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-230">hello above step ensures that only requests for hello path "/echo" are allowed through hello Application Gateway.</span></span> <span data-ttu-id="cf6cf-231">Solicitações tooother que APIs configurados no gerenciamento de API gerará 404 erros do Application Gateway quando acessados de saudação à Internet.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-231">Requests tooother APIs configured in API Management will throw 404 errors from Application Gateway when accessed from hello Internet.</span></span> 

### <a name="step-12"></a><span data-ttu-id="cf6cf-232">Etapa 12</span><span class="sxs-lookup"><span data-stu-id="cf6cf-232">Step 12</span></span>

<span data-ttu-id="cf6cf-233">Crie uma configuração de regra para Olá Application Gateway toouse URL baseada no caminho de roteamento.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-233">Create a rule setting for hello Application Gateway toouse URL path-based routing.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-13"></a><span data-ttu-id="cf6cf-234">Etapa 13</span><span class="sxs-lookup"><span data-stu-id="cf6cf-234">Step 13</span></span>

<span data-ttu-id="cf6cf-235">Configure o número de saudação de instâncias e o tamanho de saudação Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-235">Configure hello number of instances and size for hello Application Gateway.</span></span> <span data-ttu-id="cf6cf-236">Aqui, estamos usando Olá [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) para aumentar a segurança de saudação recursos de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-236">Here we are using hello [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) for increased security of hello API Management resource.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-14"></a><span data-ttu-id="cf6cf-237">Etapa 14</span><span class="sxs-lookup"><span data-stu-id="cf6cf-237">Step 14</span></span>

<span data-ttu-id="cf6cf-238">Configure WAF toobe no modo de "Prevenção".</span><span class="sxs-lookup"><span data-stu-id="cf6cf-238">Configure WAF toobe in "Prevention" mode.</span></span>
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a><span data-ttu-id="cf6cf-239">Criar um Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="cf6cf-239">Create Application Gateway</span></span>

<span data-ttu-id="cf6cf-240">Crie um Gateway de aplicativos com todos os objetos de configuração de saudação da saudação etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-240">Create an Application Gateway with all hello configuration objects from hello preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName  -Location $location -BackendAddressPools $apimProxyBackendPool, $dummyBackendPool -BackendHttpSettingsCollection $apimPoolSetting, $dummyBackendSetting  -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-hello-api-management-proxy-hostname-toohello-public-dns-name-of-hello-application-gateway-resource"></a><span data-ttu-id="cf6cf-241">CNAME Olá API de gerenciamento proxy hostname toohello nome DNS público do hello recurso do Application Gateway</span><span class="sxs-lookup"><span data-stu-id="cf6cf-241">CNAME hello API Management proxy hostname toohello public DNS name of hello Application Gateway resource</span></span>

<span data-ttu-id="cf6cf-242">Depois de criar o gateway hello, Olá próxima etapa é tooconfigure Olá front-end para comunicação.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-242">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="cf6cf-243">Ao usar um IP público, o Application Gateway requer um nome DNS atribuído dinamicamente, o que pode não ser fácil toouse.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-243">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which may not be easy toouse.</span></span> 

<span data-ttu-id="cf6cf-244">Hello nome DNS do Application Gateway deve ser usado toocreate um registro CNAME que aponte o nome de host de proxy Olá APIM (por exemplo, `api.contoso.net` nos exemplos de saudação acima) toothis nome DNS.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-244">hello Application Gateway's DNS name should be used toocreate a CNAME record which points hello APIM proxy host name (e.g. `api.contoso.net` in hello examples above) toothis DNS name.</span></span> <span data-ttu-id="cf6cf-245">tooconfigure Olá front-end registro CNAME de IP, recuperar detalhes de saudação do hello Application Gateway e seu nome de IP/DNS associado usando Olá PublicIPAddress elemento.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-245">tooconfigure hello frontend IP CNAME record, retrieve hello details of hello Application Gateway and its associated IP/DNS name using hello PublicIPAddress element.</span></span> <span data-ttu-id="cf6cf-246">uso de saudação de registros de um não é recomendável porque Olá VIP pode ser alterado na reinicialização do gateway.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-246">hello use of A-records is not recommended since hello VIP may change on restart of gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<span data-ttu-id="cf6cf-247"><a name="summary"> </a> Resumo</span><span class="sxs-lookup"><span data-stu-id="cf6cf-247"><a name="summary"> </a> Summary</span></span>
<span data-ttu-id="cf6cf-248">Gerenciamento de API do Azure configurado em uma rede virtual fornece uma interface de único gateway para todas as APIs configuradas, se estiverem hospedados no local ou na nuvem de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-248">Azure API Management configured in a VNET provides a single gateway interface for all configured APIs, whether they are hosted on-prem or in hello cloud.</span></span> <span data-ttu-id="cf6cf-249">Integrando Application Gateway de gerenciamento de API fornece flexibilidade de saudação do seletivamente habilitar específico toobe APIs acessível na Internet de saudação, bem como fornecer um Firewall do aplicativo Web como uma instância de gerenciamento de API de tooyour de front-end.</span><span class="sxs-lookup"><span data-stu-id="cf6cf-249">Integrating Application Gateway with API Management provides hello flexibility of selectively enabling particular APIs toobe accessible on hello Internet, as well as providing a Web Application Firewall as a frontend tooyour API Management instance.</span></span>

##<span data-ttu-id="cf6cf-250"><a name="next-steps"> </a> Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cf6cf-250"><a name="next-steps"> </a> Next steps</span></span>
* <span data-ttu-id="cf6cf-251">Saiba mais sobre o Gateway de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="cf6cf-251">Learn more about Azure Application Gateway</span></span>
  * [<span data-ttu-id="cf6cf-252">Visão geral do Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="cf6cf-252">Application Gateway Overview</span></span>](../application-gateway/application-gateway-introduction.md)
  * [<span data-ttu-id="cf6cf-253">Firewall do Aplicativo Web do Gateway de Aplicativo (visualização)</span><span class="sxs-lookup"><span data-stu-id="cf6cf-253">Application Gateway Web Application Firewall</span></span>](../application-gateway/application-gateway-webapplicationfirewall-overview.md)
  * [<span data-ttu-id="cf6cf-254">Gateway de Aplicativo usando Roteamento com base em Caminho</span><span class="sxs-lookup"><span data-stu-id="cf6cf-254">Application Gateway using Path-based Routing</span></span>](../application-gateway/application-gateway-create-url-route-arm-ps.md)
* <span data-ttu-id="cf6cf-255">Saiba mais sobre o gerenciamento de API nas VNETs</span><span class="sxs-lookup"><span data-stu-id="cf6cf-255">Learn more about API Management and VNETs</span></span>
  * [<span data-ttu-id="cf6cf-256">Usando a API de gerenciamento disponíveis apenas no hello VNET</span><span class="sxs-lookup"><span data-stu-id="cf6cf-256">Using API Management available only within hello VNET</span></span>](api-management-using-with-internal-vnet.md)
  * [<span data-ttu-id="cf6cf-257">Uso do Gerenciamento de API na rede virtual</span><span class="sxs-lookup"><span data-stu-id="cf6cf-257">Using API Management in VNET</span></span>](api-management-using-with-vnet.md)
