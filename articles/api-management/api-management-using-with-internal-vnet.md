---
title: Como usar o Gerenciamento de API do Azure com redes virtuais internas | Microsoft Docs
description: Saiba como instalar e configurar o Gerenciamento de API do Azure na rede virtual interna.
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
ms.openlocfilehash: 55248387c7e78d05c1cf1afd615b7b921e9669d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a><span data-ttu-id="0d7d7-103">Usar o serviço de Gerenciamento de API do Azure com rede virtual interna</span><span class="sxs-lookup"><span data-stu-id="0d7d7-103">Using Azure API Management service with Internal Virtual Network</span></span>
<span data-ttu-id="0d7d7-104">Com as Redes virtuais (VNETs) do Azure, o Gerenciamento de API pode administrar as APIs que não estão acessíveis pela Internet.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-104">With Azure Virtual Networks (VNETs), API Management can manage APIs not accessible on the Internet.</span></span> <span data-ttu-id="0d7d7-105">Várias tecnologias de VPN estão disponíveis para fazer a conexão e o Gerenciamento de API pode ser implantado em dois modos principais dentro da VNET:</span><span class="sxs-lookup"><span data-stu-id="0d7d7-105">A number of VPN technologies are available to make the connection and API Management can be deployed in two main modes inside the VNET:</span></span>
* <span data-ttu-id="0d7d7-106">Externo</span><span class="sxs-lookup"><span data-stu-id="0d7d7-106">External</span></span>
* <span data-ttu-id="0d7d7-107">Interna</span><span class="sxs-lookup"><span data-stu-id="0d7d7-107">Internal</span></span>

## <span data-ttu-id="0d7d7-108"><a name="overview"> </a>Visão geral</span><span class="sxs-lookup"><span data-stu-id="0d7d7-108"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="0d7d7-109">Quando o Gerenciamento de API é implantado em um modo de rede virtual interna, todos os pontos de extremidade de serviço (gateway, portal do desenvolvedor, portal do editor, gerenciamento direto e Git) ficam visíveis apenas de dentro de uma rede virtual à qual você controla o acesso.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-109">When API Management is deployed in an Internal Virtual network mode, all the service endpoints (gateway, developer portal, publisher portal, direct management and Git) are only visible inside a Virtual network that you control access to.</span></span> <span data-ttu-id="0d7d7-110">Nenhum ponto de extremidade de serviço é registrado no servidor DNS público.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-110">None of the service endpoints are registered on the Public DNS Server.</span></span>

<span data-ttu-id="0d7d7-111">Usando o Gerenciamento de API no modo interno, você pode chegar aos seguintes cenários</span><span class="sxs-lookup"><span data-stu-id="0d7d7-111">Using API Management in Internal mode, you can achieve the following scenarios</span></span>
* <span data-ttu-id="0d7d7-112">Torne as APIs hospedadas em seu datacenter privado seguras e acessíveis por terceiros usando as conexões de VPN Site a Site ou ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-112">Securely make APIs hosted in your private datacenter accessible by 3rd parties outside of it using Site-to-Site or ExpressRoute VPN connections.</span></span>
* <span data-ttu-id="0d7d7-113">Habilite cenários de nuvem híbrida, expondo as APIs baseadas em nuvem e as APIs locais por meio de um gateway comum.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-113">Enable hybrid cloud scenarios by exposing your cloud-based APIs and on-prem APIs through a common gateway.</span></span>
* <span data-ttu-id="0d7d7-114">Gerencie suas APIs hospedadas em várias localizações geográficas usando um único ponto de extremidade de Gateway.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-114">Manage your APIs hosted in multiple geographic locations using a single Gateway endpoint.</span></span> 

## <span data-ttu-id="0d7d7-115"><a name="enable-vpn"> </a>Criar um Gerenciamento de API na rede virtual interna</span><span class="sxs-lookup"><span data-stu-id="0d7d7-115"><a name="enable-vpn"> </a>Creating an API Management in Internal Virtual network</span></span>
<span data-ttu-id="0d7d7-116">O serviço de Gerenciamento de API na rede virtual interna é hospedado por trás de um Balanceador de Carga Interno (ILB).</span><span class="sxs-lookup"><span data-stu-id="0d7d7-116">The API Management service in Internal Virtual network is hosted behind an Internal Load Balancer(ILB).</span></span> <span data-ttu-id="0d7d7-117">O endereço IP do ILB está no intervalo [RFC1918](http://www.faqs.org/rfcs/rfc1918.html).</span><span class="sxs-lookup"><span data-stu-id="0d7d7-117">The IP Address of the ILB is in the [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) range.</span></span>  

### <a name="enable-vnet-connection-using-azure-portal"></a><span data-ttu-id="0d7d7-118">Habilitar a conexão de VNET usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0d7d7-118">Enable VNET connection using Azure portal</span></span>
<span data-ttu-id="0d7d7-119">Primeiro, crie o serviço de Gerenciamento de API seguindo as etapas em [Criar serviço de Gerenciamento de API][Create API Management service].</span><span class="sxs-lookup"><span data-stu-id="0d7d7-119">First create the API Management service by following the steps [Create API Management service][Create API Management service].</span></span> <span data-ttu-id="0d7d7-120">Em seguida, configure o Gerenciamento de API a ser implantado dentro de uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-120">Then set-up API Management to be deployed inside a Virtual network.</span></span>

![Menu de configuração de APIM na rede virtual interna][api-management-using-internal-vnet-menu]

<span data-ttu-id="0d7d7-122">Após a implantação bem-sucedida, você deve ver o endereço IP virtual interno do serviço no painel.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-122">After the deployment succeeds, you should see the Internal Virtual IP Address of your service on the dashboard.</span></span>

![Painel de Gerenciamento de API com a VNET interna configurada][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a><span data-ttu-id="0d7d7-124">Habilitar a conexão de VNET usando cmdlets do Powershell</span><span class="sxs-lookup"><span data-stu-id="0d7d7-124">Enable VNET connection using Powershell cmdlets</span></span>
<span data-ttu-id="0d7d7-125">Você também pode habilitar a conectividade de VNET usando os cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-125">You can also enable VNET connectivity using the PowerShell cmdlets.</span></span>

* <span data-ttu-id="0d7d7-126">**Criar um serviço de Gerenciamento de API dentro de uma VNET**: use o cmdlet [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) para criar um serviço de Gerenciamento de API do Azure dentro de uma VNET e configurá-lo para usar o tipo de VNET interna.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-126">**Create an API Management service inside a VNET**: Use the cmdlet [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) to create an Azure API Management service inside a VNET and configure it to use the Internal VNET type.</span></span>

* <span data-ttu-id="0d7d7-127">**Implantar um serviço de Gerenciamento de API existente dentro de uma VNET**: use o cmdlet [Update-AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) para mover um serviço de Gerenciamento de API do Azure existente para uma rede virtual e configurá-lo para usar o tipo de VNET interna.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-127">**Deploy an existing API Management service inside a VNET**: Use the cmdlet [Update-AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) to move an existing Azure API Management service inside a Virtual network and configure it to use Internal VNET type.</span></span>

## <span data-ttu-id="0d7d7-128"><a name="apim-dns-configuration"></a>Configuração de DNS</span><span class="sxs-lookup"><span data-stu-id="0d7d7-128"><a name="apim-dns-configuration"></a>DNS configuration</span></span>
<span data-ttu-id="0d7d7-129">Ao usar o Gerenciamento de API em modo de rede virtual externa, o DNS é gerenciado pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-129">When using API Management in External Virtual network mode, DNS is managed by Azure.</span></span> <span data-ttu-id="0d7d7-130">Para o modo de rede virtual interna, você precisa gerenciar o seu próprio DNS.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-130">For Internal Virtual network mode, you have to manage your own DNS.</span></span>

> [!NOTE]
> <span data-ttu-id="0d7d7-131">O serviço de Gerenciamento de API não escuta as solicitações que chegam de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-131">API Management service does not listen to requests coming on IP addresses.</span></span> <span data-ttu-id="0d7d7-132">Ele responde apenas às solicitações do nome de host configurado em seus pontos de extremidade de serviço (que inclui o gateway, o portal do desenvolvedor, o portal do editor, o ponto de extremidade de gerenciamento direto e git).</span><span class="sxs-lookup"><span data-stu-id="0d7d7-132">It only responds to requests to the Hostname configured on its service endpoints (which includes gateway, developer portal, publisher Portal, direct management endpoint, and git).</span></span>

### <a name="access-on-default-host-names"></a><span data-ttu-id="0d7d7-133">Acesso em nomes de host padrão:</span><span class="sxs-lookup"><span data-stu-id="0d7d7-133">Access on default host names:</span></span>
<span data-ttu-id="0d7d7-134">Ao criar um serviço de Gerenciamento de API na nuvem pública do Azure, chamado "contoso" por exemplo, os seguintes pontos de extremidade de serviço são configurados por padrão.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-134">When you create an API Management service in public Azure cloud, named "contoso" for example, the following service endpoints are configured by default.</span></span>

>   <span data-ttu-id="0d7d7-135">Gateway/Proxy: contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="0d7d7-135">Gateway / Proxy - contoso.azure-api.net</span></span>

> <span data-ttu-id="0d7d7-136">Portal do Editor e Portal do desenvolvedor: contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="0d7d7-136">Publisher Portal and Developer Portal - contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="0d7d7-137">Ponto de extremidade de gerenciamento direto: contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="0d7d7-137">Direct Management Endpoint - contoso.management.azure-api.net</span></span>

>   <span data-ttu-id="0d7d7-138">GIT: contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="0d7d7-138">GIT - contoso.scm.azure-api.net</span></span>

<span data-ttu-id="0d7d7-139">Para acessar esses pontos de extremidade do serviço de Gerenciamento de API, você pode criar uma máquina virtual em uma sub-rede conectada à rede virtual na qual o Gerenciamento de API é implantado.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-139">To access these API Management service endpoints, you can create a Virtual Machine in a subnet connected to the Virtual network in which API Management is deployed.</span></span> <span data-ttu-id="0d7d7-140">Supondo que o endereço IP virtual interno para seu serviço seja 10.0.0.5, você pode fazer o mapeamento dos arquivos de hosts (%UnidadeDoSistema%\drivers\etc\hosts) como se segue:</span><span class="sxs-lookup"><span data-stu-id="0d7d7-140">Assuming the Internal Virtual IP Address for your service is 10.0.0.5, you can do the hosts file mapping (%SystemDrive%\drivers\etc\hosts) as follows:</span></span>

> <span data-ttu-id="0d7d7-141">10.0.0.5    contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="0d7d7-141">10.0.0.5    contoso.azure-api.net</span></span>

> <span data-ttu-id="0d7d7-142">10.0.0.5    contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="0d7d7-142">10.0.0.5    contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="0d7d7-143">10.0.0.5    contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="0d7d7-143">10.0.0.5    contoso.management.azure-api.net</span></span>

> <span data-ttu-id="0d7d7-144">10.0.0.5    contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="0d7d7-144">10.0.0.5    contoso.scm.azure-api.net</span></span>

<span data-ttu-id="0d7d7-145">Em seguida pode acessar todos os pontos de extremidade do serviço da máquina virtual criada.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-145">You can then access all the service endpoints from the Virtual Machine you created.</span></span> <span data-ttu-id="0d7d7-146">Se usar um servidor DNS personalizado em uma rede virtual, você também pode criar registros A de DNS e acessar esses pontos de extremidade de qualquer lugar em sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-146">If using a Custom DNS server in a Virtual network, you can also create A DNS records and access these endpoints from anywhere in your Virtual network.</span></span> 

### <a name="access-on-custom-domain-names"></a><span data-ttu-id="0d7d7-147">Acessar em nomes de domínio personalizados:</span><span class="sxs-lookup"><span data-stu-id="0d7d7-147">Access on custom domain names:</span></span>
<span data-ttu-id="0d7d7-148">Se você não quiser acessar o serviço de Gerenciamento de API com os nomes de host padrão, pode configurar nomes de domínio personalizados para todos os seus pontos de extremidade de serviço como abaixo</span><span class="sxs-lookup"><span data-stu-id="0d7d7-148">If you don’t want to access the API Management service with the default host names, you can setup custom domain names for all your service endpoints like below</span></span>

![Configurar o domínio personalizado para Gerenciamento de API][api-management-custom-domain-name]

<span data-ttu-id="0d7d7-150">Em seguida, você pode criar registros A no seu servidor DNS para acessar esses pontos de extremidade que só são acessíveis a partir da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-150">Then you can create A records in your DNS Server to access these endpoints which are only accessible from within your Virtual network.</span></span>

## <span data-ttu-id="0d7d7-151"><a name="related-content"> </a>Conteúdo relacionado</span><span class="sxs-lookup"><span data-stu-id="0d7d7-151"><a name="related-content"> </a>Related content</span></span>
* <span data-ttu-id="0d7d7-152">[Problemas comuns de configuração de rede durante a configuração de APIM na VNET][Common Network Configuration Issues]</span><span class="sxs-lookup"><span data-stu-id="0d7d7-152">[Common Network configuration issues while setting up APIM in VNET][Common Network Configuration Issues]</span></span>
* [<span data-ttu-id="0d7d7-153">Perguntas frequentes sobre rede virtual</span><span class="sxs-lookup"><span data-stu-id="0d7d7-153">Virtual Network faqs</span></span>](../virtual-network/virtual-networks-faq.md)
* [<span data-ttu-id="0d7d7-154">Criar registro A no DNS</span><span class="sxs-lookup"><span data-stu-id="0d7d7-154">Creating A record in DNS</span></span>](https://msdn.microsoft.com/en-us/library/bb727018.aspx)

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues
