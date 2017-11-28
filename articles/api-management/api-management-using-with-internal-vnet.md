---
title: aaaHow toouse gerenciamento de API do Azure com rede virtual interna | Microsoft Docs
description: Saiba como toosetup e configurar o gerenciamento de API do Azure na rede virtual interna.
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: 
ms.assetid: dac28ccf-2550-45a5-89cf-192d87369bc3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 8d25de14e0c0bebe7ba7b47ca432ea4e45dde312
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a><span data-ttu-id="cf499-103">Usar o serviço de Gerenciamento de API do Azure com rede virtual interna</span><span class="sxs-lookup"><span data-stu-id="cf499-103">Using Azure API Management service with Internal Virtual Network</span></span>
<span data-ttu-id="cf499-104">Com redes virtuais do Azure (VNETs), gerenciamento de API pode gerenciar APIs não está acessível no hello da Internet.</span><span class="sxs-lookup"><span data-stu-id="cf499-104">With Azure Virtual Networks (VNETs), API Management can manage APIs not accessible on hello Internet.</span></span> <span data-ttu-id="cf499-105">Um número de tecnologias de VPN é conexão de saudação toomake disponíveis e gerenciamento de API pode ser implantado em dois modos principais dentro Olá redes:</span><span class="sxs-lookup"><span data-stu-id="cf499-105">A number of VPN technologies are available toomake hello connection and API Management can be deployed in two main modes inside hello VNET:</span></span>
* <span data-ttu-id="cf499-106">Externo</span><span class="sxs-lookup"><span data-stu-id="cf499-106">External</span></span>
* <span data-ttu-id="cf499-107">Interna</span><span class="sxs-lookup"><span data-stu-id="cf499-107">Internal</span></span>

## <span data-ttu-id="cf499-108"><a name="overview"> </a>Visão geral</span><span class="sxs-lookup"><span data-stu-id="cf499-108"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="cf499-109">Quando o gerenciamento de API é implantado em um modo de rede interna Virtual, todos os pontos de serviço hello (gateway, portal do desenvolvedor, portal do publicador, gerenciamento direto e Git) só são visíveis dentro de uma rede Virtual que você controle o acesso ao.</span><span class="sxs-lookup"><span data-stu-id="cf499-109">When API Management is deployed in an Internal Virtual network mode, all hello service endpoints (gateway, developer portal, publisher portal, direct management and Git) are only visible inside a Virtual network that you control access to.</span></span> <span data-ttu-id="cf499-110">Nenhum dos pontos de extremidade de serviço Olá estão registrados no servidor DNS público do hello.</span><span class="sxs-lookup"><span data-stu-id="cf499-110">None of hello service endpoints are registered on hello Public DNS Server.</span></span>

<span data-ttu-id="cf499-111">Usando o gerenciamento de API no modo interno, você pode obter os seguintes cenários de saudação</span><span class="sxs-lookup"><span data-stu-id="cf499-111">Using API Management in Internal mode, you can achieve hello following scenarios</span></span>
* <span data-ttu-id="cf499-112">Torne as APIs hospedadas em seu datacenter privado seguras e acessíveis por terceiros usando as conexões de VPN Site a Site ou ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="cf499-112">Securely make APIs hosted in your private datacenter accessible by 3rd parties outside of it using Site-to-Site or ExpressRoute VPN connections.</span></span>
* <span data-ttu-id="cf499-113">Habilite cenários de nuvem híbrida, expondo as APIs baseadas em nuvem e as APIs locais por meio de um gateway comum.</span><span class="sxs-lookup"><span data-stu-id="cf499-113">Enable hybrid cloud scenarios by exposing your cloud-based APIs and on-prem APIs through a common gateway.</span></span>
* <span data-ttu-id="cf499-114">Gerencie suas APIs hospedadas em várias localizações geográficas usando um único ponto de extremidade de Gateway.</span><span class="sxs-lookup"><span data-stu-id="cf499-114">Manage your APIs hosted in multiple geographic locations using a single Gateway endpoint.</span></span> 

## <span data-ttu-id="cf499-115"><a name="enable-vpn"> </a>Criar um Gerenciamento de API na rede virtual interna</span><span class="sxs-lookup"><span data-stu-id="cf499-115"><a name="enable-vpn"> </a>Creating an API Management in Internal Virtual network</span></span>
<span data-ttu-id="cf499-116">Olá serviço de gerenciamento de API na rede interna Virtual é hospedado por trás de um Balancer(ILB) de carga interno.</span><span class="sxs-lookup"><span data-stu-id="cf499-116">hello API Management service in Internal Virtual network is hosted behind an Internal Load Balancer(ILB).</span></span> <span data-ttu-id="cf499-117">Olá endereço IP do hello ILB está em Olá [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) intervalo.</span><span class="sxs-lookup"><span data-stu-id="cf499-117">hello IP Address of hello ILB is in hello [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) range.</span></span>  

### <a name="enable-vnet-connection-using-azure-portal"></a><span data-ttu-id="cf499-118">Habilitar a conexão de VNET usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="cf499-118">Enable VNET connection using Azure portal</span></span>
<span data-ttu-id="cf499-119">Primeiro crie o serviço de gerenciamento de API Olá seguindo as etapas de saudação [serviço de gerenciamento de API criar][Create API Management service].</span><span class="sxs-lookup"><span data-stu-id="cf499-119">First create hello API Management service by following hello steps [Create API Management service][Create API Management service].</span></span> <span data-ttu-id="cf499-120">Em seguida, configurar gerenciamento de API toobe implantado dentro de uma rede Virtual.</span><span class="sxs-lookup"><span data-stu-id="cf499-120">Then set-up API Management toobe deployed inside a Virtual network.</span></span>

![Menu de configuração de APIM na rede virtual interna][api-management-using-internal-vnet-menu]

<span data-ttu-id="cf499-122">Após a implantação de saudação for bem-sucedida, você deve ver Olá endereço IP Virtual interno do serviço no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf499-122">After hello deployment succeeds, you should see hello Internal Virtual IP Address of your service on hello dashboard.</span></span>

![Painel de Gerenciamento de API com a VNET interna configurada][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a><span data-ttu-id="cf499-124">Habilitar a conexão de VNET usando cmdlets do Powershell</span><span class="sxs-lookup"><span data-stu-id="cf499-124">Enable VNET connection using Powershell cmdlets</span></span>
<span data-ttu-id="cf499-125">Você também pode habilitar a conectividade de rede virtual usando cmdlets do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="cf499-125">You can also enable VNET connectivity using hello PowerShell cmdlets.</span></span>

* <span data-ttu-id="cf499-126">**Criar um serviço de gerenciamento de API dentro de uma rede virtual**: usar o cmdlet Olá [AzureRmApiManagement novo](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate um gerenciamento de API do Azure do serviço dentro de uma rede virtual e configure-o tipo de rede virtual interna Olá toouse.</span><span class="sxs-lookup"><span data-stu-id="cf499-126">**Create an API Management service inside a VNET**: Use hello cmdlet [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate an Azure API Management service inside a VNET and configure it toouse hello Internal VNET type.</span></span>

* <span data-ttu-id="cf499-127">**Implantar um serviço de gerenciamento de API existente dentro de uma rede virtual**: usar o cmdlet Olá [AzureRmApiManagementDeployment atualização](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove um gerenciamento de API do Azure existente de serviço dentro de uma rede Virtual e configurá-lo toouse Tipo de rede virtual interno.</span><span class="sxs-lookup"><span data-stu-id="cf499-127">**Deploy an existing API Management service inside a VNET**: Use hello cmdlet [Update-AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove an existing Azure API Management service inside a Virtual network and configure it toouse Internal VNET type.</span></span>

## <span data-ttu-id="cf499-128"><a name="apim-dns-configuration"></a>Configuração de DNS</span><span class="sxs-lookup"><span data-stu-id="cf499-128"><a name="apim-dns-configuration"></a>DNS configuration</span></span>
<span data-ttu-id="cf499-129">Ao usar o Gerenciamento de API em modo de rede virtual externa, o DNS é gerenciado pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="cf499-129">When using API Management in External Virtual network mode, DNS is managed by Azure.</span></span> <span data-ttu-id="cf499-130">Para o modo de rede Virtual interna, você tem toomanage seu próprio DNS.</span><span class="sxs-lookup"><span data-stu-id="cf499-130">For Internal Virtual network mode, you have toomanage your own DNS.</span></span>

> [!NOTE]
> <span data-ttu-id="cf499-131">Serviço de gerenciamento de API não escuta toorequests provenientes de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="cf499-131">API Management service does not listen toorequests coming on IP addresses.</span></span> <span data-ttu-id="cf499-132">Ele responde apenas toorequests toohello nome de host configurado em seus pontos de extremidade de serviço (que inclui o gateway, portal do desenvolvedor, Portal do publicador, ponto de extremidade de gerenciamento direto e git).</span><span class="sxs-lookup"><span data-stu-id="cf499-132">It only responds toorequests toohello Hostname configured on its service endpoints (which includes gateway, developer portal, publisher Portal, direct management endpoint, and git).</span></span>

### <a name="access-on-default-host-names"></a><span data-ttu-id="cf499-133">Acesso em nomes de host padrão:</span><span class="sxs-lookup"><span data-stu-id="cf499-133">Access on default host names:</span></span>
<span data-ttu-id="cf499-134">Quando você cria um serviço de gerenciamento de API na nuvem do Azure pública, chamado "contoso" por exemplo, hello seguintes pontos de extremidade de serviço são configurados por padrão.</span><span class="sxs-lookup"><span data-stu-id="cf499-134">When you create an API Management service in public Azure cloud, named "contoso" for example, hello following service endpoints are configured by default.</span></span>

>   <span data-ttu-id="cf499-135">Gateway/Proxy: contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="cf499-135">Gateway / Proxy - contoso.azure-api.net</span></span>

> <span data-ttu-id="cf499-136">Portal do Editor e Portal do desenvolvedor: contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="cf499-136">Publisher Portal and Developer Portal - contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="cf499-137">Ponto de extremidade de gerenciamento direto: contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="cf499-137">Direct Management Endpoint - contoso.management.azure-api.net</span></span>

>   <span data-ttu-id="cf499-138">GIT: contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="cf499-138">GIT - contoso.scm.azure-api.net</span></span>

<span data-ttu-id="cf499-139">tooaccess esses pontos de extremidade de serviço de gerenciamento de API, você pode criar uma máquina Virtual em uma rede de Virtual toohello conectado de sub-rede em que o gerenciamento de API é implantado.</span><span class="sxs-lookup"><span data-stu-id="cf499-139">tooaccess these API Management service endpoints, you can create a Virtual Machine in a subnet connected toohello Virtual network in which API Management is deployed.</span></span> <span data-ttu-id="cf499-140">Supondo que Olá interno endereço IP Virtual para o serviço 10.0.0.5, você pode fazer Olá mapeamento de arquivo de hosts (% SystemDrive%\drivers\etc\hosts) da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="cf499-140">Assuming hello Internal Virtual IP Address for your service is 10.0.0.5, you can do hello hosts file mapping (%SystemDrive%\drivers\etc\hosts) as follows:</span></span>

> <span data-ttu-id="cf499-141">10.0.0.5    contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="cf499-141">10.0.0.5    contoso.azure-api.net</span></span>

> <span data-ttu-id="cf499-142">10.0.0.5    contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="cf499-142">10.0.0.5    contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="cf499-143">10.0.0.5    contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="cf499-143">10.0.0.5    contoso.management.azure-api.net</span></span>

> <span data-ttu-id="cf499-144">10.0.0.5    contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="cf499-144">10.0.0.5    contoso.scm.azure-api.net</span></span>

<span data-ttu-id="cf499-145">Você pode acessar todos os pontos de extremidade de serviço de saudação do hello Máquina Virtual que você criou.</span><span class="sxs-lookup"><span data-stu-id="cf499-145">You can then access all hello service endpoints from hello Virtual Machine you created.</span></span> <span data-ttu-id="cf499-146">Se usar um servidor DNS personalizado em uma rede virtual, você também pode criar registros A de DNS e acessar esses pontos de extremidade de qualquer lugar em sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="cf499-146">If using a Custom DNS server in a Virtual network, you can also create A DNS records and access these endpoints from anywhere in your Virtual network.</span></span> 

### <a name="access-on-custom-domain-names"></a><span data-ttu-id="cf499-147">Acessar em nomes de domínio personalizados:</span><span class="sxs-lookup"><span data-stu-id="cf499-147">Access on custom domain names:</span></span>
<span data-ttu-id="cf499-148">Se você não quiser Olá tooaccess serviço de gerenciamento de API com nomes de host padrão hello, você pode configurar os nomes de domínio personalizados para todos os seus pontos de extremidade serviço como abaixo</span><span class="sxs-lookup"><span data-stu-id="cf499-148">If you don’t want tooaccess hello API Management service with hello default host names, you can setup custom domain names for all your service endpoints like below</span></span>

![Configurar o domínio personalizado para Gerenciamento de API][api-management-custom-domain-name]

<span data-ttu-id="cf499-150">Em seguida, você pode criar registros em seu servidor DNS tooaccess esses pontos de extremidade que só podem ser acessados de dentro de sua rede Virtual.</span><span class="sxs-lookup"><span data-stu-id="cf499-150">Then you can create A records in your DNS Server tooaccess these endpoints which are only accessible from within your Virtual network.</span></span>

## <span data-ttu-id="cf499-151"><a name="related-content"> </a>Conteúdo relacionado</span><span class="sxs-lookup"><span data-stu-id="cf499-151"><a name="related-content"> </a>Related content</span></span>
* <span data-ttu-id="cf499-152">[Problemas comuns de configuração de rede durante a configuração de APIM na VNET][Common Network Configuration Issues]</span><span class="sxs-lookup"><span data-stu-id="cf499-152">[Common Network configuration issues while setting up APIM in VNET][Common Network Configuration Issues]</span></span>
* [<span data-ttu-id="cf499-153">Perguntas frequentes sobre rede virtual</span><span class="sxs-lookup"><span data-stu-id="cf499-153">Virtual Network faqs</span></span>](../virtual-network/virtual-networks-faq.md)
* [<span data-ttu-id="cf499-154">Criar registro A no DNS</span><span class="sxs-lookup"><span data-stu-id="cf499-154">Creating A record in DNS</span></span>](https://msdn.microsoft.com/en-us/library/bb727018.aspx)

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues
