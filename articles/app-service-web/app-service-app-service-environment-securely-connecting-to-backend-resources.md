---
title: "Conectando-se de aaaSecurely tooBackEnd recursos de um ambiente de serviço de aplicativo"
description: "Saiba mais sobre como toosecurely conectar toobackend recursos de um ambiente de serviço de aplicativo."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: f82eb283-a6e7-4923-a00b-4b4ccf7c4b5b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: 6311d3fc301512ea3c4ed8f14f268f75755aa415
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="securely-connecting-toobackend-resources-from-an-app-service-environment"></a><span data-ttu-id="5c4fc-103">TooBackend de conectar-se com segurança os recursos de um ambiente de serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="5c4fc-103">Securely Connecting tooBackend Resources from an App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="5c4fc-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="5c4fc-104">Overview</span></span>
<span data-ttu-id="5c4fc-105">Como um ambiente de serviço de aplicativo é sempre criado no **ou** uma rede virtual do Azure Resource Manager, **ou** um modelo de implantação clássico [rede virtual] [ virtualnetwork], conexões de saída dos recursos de back-end de tooother ambiente de serviço de aplicativo podem fluir exclusivamente em rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="5c4fc-105">Since an App Service Environment is always created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model [virtual network][virtualnetwork], outbound connections from an App Service Environment tooother backend resources can flow exclusively over hello virtual network.</span></span>  <span data-ttu-id="5c4fc-106">Com uma alteração recente feita em junho de 2016, os ASEs agora podem ser implantados nas redes virtuais que usam os intervalos de endereço público ou espaços de endereço RFC1918 (ou seja, endereços privados).</span><span class="sxs-lookup"><span data-stu-id="5c4fc-106">With a recent change made in June 2016, ASEs can also be deployed into virtual networks that use either public address ranges, or RFC1918 address spaces (i.e. private addresses).</span></span>  

<span data-ttu-id="5c4fc-107">Por exemplo, pode haver um SQL Server em execução em um cluster de máquinas virtuais com a porta 1433 bloqueada.</span><span class="sxs-lookup"><span data-stu-id="5c4fc-107">For example, there may be a SQL Server running on a cluster of virtual machines with port 1433 locked down.</span></span>  <span data-ttu-id="5c4fc-108">ponto de extremidade de saudação pode ser ACLd tooonly permitir o acesso de outros recursos na mesma rede virtual de hello.</span><span class="sxs-lookup"><span data-stu-id="5c4fc-108">hello endpoint may be ACLd tooonly allow access from other resources on hello same virtual network.</span></span>  

<span data-ttu-id="5c4fc-109">Como outro exemplo, pontos de extremidade confidenciais podem executados no local e ser tooAzure conectado através de um [Site a Site] [ SiteToSite] ou [Azure ExpressRoute] [ ExpressRoute] conexões.</span><span class="sxs-lookup"><span data-stu-id="5c4fc-109">As another example, sensitive endpoints may run on-premises and be connected tooAzure via either [Site-to-Site][SiteToSite] or [Azure ExpressRoute][ExpressRoute] connections.</span></span>  <span data-ttu-id="5c4fc-110">Como resultado, somente os recursos em redes virtuais conectadas toohello Site a Site ou rota expressa túneis será tooaccess capaz de pontos de extremidade de local.</span><span class="sxs-lookup"><span data-stu-id="5c4fc-110">As a result, only resources in virtual networks connected toohello Site-to-Site or ExpressRoute tunnels will be able tooaccess on-premises endpoints.</span></span>

<span data-ttu-id="5c4fc-111">Para todos esses cenários, aplicativos executados em um ambiente de serviço de aplicativo ser capaz de toosecurely conectará toohello vários servidores e recursos.</span><span class="sxs-lookup"><span data-stu-id="5c4fc-111">For all of these scenarios, apps running on an App Service Environment will be able toosecurely connect toohello various servers and resources.</span></span>  <span data-ttu-id="5c4fc-112">Tráfego de saída de aplicativos executados em um ambiente de serviço de aplicativo tooprivate os pontos de extremidade no hello mesma rede virtual (ou conectado toohello mesma rede virtual), será apenas fluxo de rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="5c4fc-112">Outbound traffic from apps running in an App Service Environment tooprivate endpoints in hello same virtual network (or connected toohello same virtual network), will only flow over hello virtual network.</span></span>  <span data-ttu-id="5c4fc-113">O tráfego de saída tooprivate pontos de extremidade de não fluirá sobre Olá Internet pública.</span><span class="sxs-lookup"><span data-stu-id="5c4fc-113">Outbound traffic tooprivate endpoints will not flow over hello public Internet.</span></span>

<span data-ttu-id="5c4fc-114">Uma limitação se aplica a tráfego de toooutbound de tooendpoints um ambiente de serviço de aplicativo em uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="5c4fc-114">One caveat applies toooutbound traffic from an App Service Environment tooendpoints within a virtual network.</span></span>  <span data-ttu-id="5c4fc-115">Ambientes de serviço de aplicativo não pode acessar pontos de extremidade das máquinas virtuais localizadas em Olá **mesmo** sub-rede como Olá ambiente de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5c4fc-115">App Service Environments cannot reach endpoints of virtual machines located in hello **same** subnet as hello App Service Environment.</span></span>  <span data-ttu-id="5c4fc-116">Isso normalmente não deveria um problema como ambientes de serviço de aplicativo são implantados em uma sub-rede reservada para uso exclusivo por Olá ambiente de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5c4fc-116">This normally should not be a problem as long as App Service Environments are deployed into a subnet reserved for exclusive use by only hello App Service Environment.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a><span data-ttu-id="5c4fc-117">Requisitos de DNS e conectividade de saída</span><span class="sxs-lookup"><span data-stu-id="5c4fc-117">Outbound Connectivity and DNS Requirements</span></span>
<span data-ttu-id="5c4fc-118">Para um ambiente de serviço de aplicativo toofunction corretamente, ele exige pontos de extremidade de toovarious de acesso de saída.</span><span class="sxs-lookup"><span data-stu-id="5c4fc-118">For an App Service Environment toofunction properly, it requires outbound access toovarious endpoints.</span></span> <span data-ttu-id="5c4fc-119">É uma lista completa dos pontos de extremidade externos Olá usado por uma ASE em Olá seção "Conectividade de rede necessária" hello [configuração de rede para a rota expressa](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) artigo.</span><span class="sxs-lookup"><span data-stu-id="5c4fc-119">A full list of hello external endpoints used by an ASE is in hello "Required Network Connectivity" section of hello [Network Configuration for ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) article.</span></span>

<span data-ttu-id="5c4fc-120">Ambientes de serviço de aplicativo exigem uma infraestrutura DNS válida configurada para a rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="5c4fc-120">App Service Environments require a valid DNS infrastructure configured for hello virtual network.</span></span>  <span data-ttu-id="5c4fc-121">Se para qualquer Olá motivo a configuração do DNS é alterada após ter sido criado um ambiente de serviço de aplicativo, os desenvolvedores podem forçar o toopick um ambiente de serviço de aplicativo nova configuração de DNS Olá.</span><span class="sxs-lookup"><span data-stu-id="5c4fc-121">If for any reason hello DNS configuration is changed after an App Service Environment has been created, developers can force an App Service Environment toopick up hello new DNS configuration.</span></span>  <span data-ttu-id="5c4fc-122">Disparar uma reinicialização sem interrupção de ambiente usando hello "Reiniciar" localizado na parte superior de saudação do hello ambiente de serviço de aplicativo folha de gerenciamento no portal de saudação fará com que Olá ambiente toopick a nova configuração de DNS hello.</span><span class="sxs-lookup"><span data-stu-id="5c4fc-122">Triggering a rolling environment reboot using hello "Restart" icon located at hello top of hello App Service Environment management blade in hello portal will cause hello environment toopick up hello new DNS configuration.</span></span>

<span data-ttu-id="5c4fc-123">Também é recomendável que todos os servidores DNS personalizados Olá vnet ser configurado antes do tempo anterior toocreating um ambiente de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5c4fc-123">It is also recommended that any custom DNS servers on hello vnet be setup ahead of time prior toocreating an App Service Environment.</span></span>  <span data-ttu-id="5c4fc-124">Se a configuração do DNS da rede virtual for alterada enquanto um ambiente de serviço de aplicativo está sendo criado, que resultará em falha de processo de criação de ambiente de serviço de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="5c4fc-124">If a virtual network's DNS configuration is changed while an App Service Environment is being created, that will result in hello App Service Environment creation process failing.</span></span>  <span data-ttu-id="5c4fc-125">Do mesmo modo, se um servidor DNS personalizado existir no hello outra extremidade de um gateway de VPN e o servidor DNS Olá é Olá inacessível ou não estiver disponível, ambiente de serviço de aplicativo, o processo de criação também falharão.</span><span class="sxs-lookup"><span data-stu-id="5c4fc-125">In a similar vein, if a custom DNS server exists on hello other end of a VPN gateway, and hello DNS server is unreachable or unavailable, hello App Service Environment creation process will also fail.</span></span>

## <a name="connecting-tooa-sql-server"></a><span data-ttu-id="5c4fc-126">Conectar-se tooa do SQL Server</span><span class="sxs-lookup"><span data-stu-id="5c4fc-126">Connecting tooa SQL Server</span></span>
<span data-ttu-id="5c4fc-127">Uma configuração comum do SQL Server tem um ponto de extremidade escutando na porta 1433:</span><span class="sxs-lookup"><span data-stu-id="5c4fc-127">A common SQL Server configuration has an endpoint listening on port 1433:</span></span>

![Ponto de extremidade do SQL Server][SqlServerEndpoint]

<span data-ttu-id="5c4fc-129">Há duas abordagens para restringir o ponto de extremidade do tráfego toothis:</span><span class="sxs-lookup"><span data-stu-id="5c4fc-129">There are two approaches for restricting traffic toothis endpoint:</span></span>

* <span data-ttu-id="5c4fc-130">[Listas de controle de acesso a redes][NetworkAccessControlLists] (ACLs de rede)</span><span class="sxs-lookup"><span data-stu-id="5c4fc-130">[Network Access Control Lists][NetworkAccessControlLists] (Network ACLs)</span></span>
* <span data-ttu-id="5c4fc-131">[Grupos de segurança de rede][NetworkSecurityGroups]</span><span class="sxs-lookup"><span data-stu-id="5c4fc-131">[Network Security Groups][NetworkSecurityGroups]</span></span>

## <a name="restricting-access-with-a-network-acl"></a><span data-ttu-id="5c4fc-132">Restringindo o acesso com uma ACL de rede</span><span class="sxs-lookup"><span data-stu-id="5c4fc-132">Restricting Access With a Network ACL</span></span>
<span data-ttu-id="5c4fc-133">A porta 1433 pode ser protegida usando uma lista de controle de acesso de rede.</span><span class="sxs-lookup"><span data-stu-id="5c4fc-133">Port 1433 can be secured using a network access control list.</span></span>  <span data-ttu-id="5c4fc-134">exemplo Hello abaixo brancas cliente endereços provenientes de dentro de uma rede virtual e bloqueia o acesso tooall outros clientes.</span><span class="sxs-lookup"><span data-stu-id="5c4fc-134">hello example below whitelists client addresses originating from inside of a virtual network, and blocks access tooall other clients.</span></span>

![Exemplo de lista de controle de acesso de rede][NetworkAccessControlListExample]

<span data-ttu-id="5c4fc-136">Todos os aplicativos em execução no ambiente de serviço de aplicativo no hello mesma rede virtual como saudação do SQL Server será capaz de tooconnect instância de SQL Server de toohello usando Olá **VNet interno** endereço IP da máquina de virtual saudação do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5c4fc-136">Any applications running in App Service Environment in hello same virtual network as hello SQL Server will be able tooconnect toohello SQL Server instance using hello **VNet internal** IP address for hello SQL Server virtual machine.</span></span>  

<span data-ttu-id="5c4fc-137">cadeia de conexão de exemplo Hello abaixo referências Olá SQL Server usando seu endereço IP privado.</span><span class="sxs-lookup"><span data-stu-id="5c4fc-137">hello example connection string below references hello SQL Server using its private IP address.</span></span>

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

<span data-ttu-id="5c4fc-138">Embora a máquina virtual de saudação tem um ponto de extremidade público, as tentativas de conexão usando o endereço IP público de saudação serão rejeitadas devido a ACL de rede hello.</span><span class="sxs-lookup"><span data-stu-id="5c4fc-138">Although hello virtual machine has a public endpoint as well, connection attempts using hello public IP address will be rejected because of hello network ACL.</span></span> 

## <a name="restricting-access-with-a-network-security-group"></a><span data-ttu-id="5c4fc-139">Restringindo o acesso com um grupo de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="5c4fc-139">Restricting Access With a Network Security Group</span></span>
<span data-ttu-id="5c4fc-140">Uma abordagem alternativa para proteger o acesso é com um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="5c4fc-140">An alternative approach for securing access is with a network security group.</span></span>  <span data-ttu-id="5c4fc-141">Grupos de segurança de rede podem ser aplicado tooindividual VMs ou sub-rede tooa que contêm máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="5c4fc-141">Network security groups can be applied tooindividual virtual machines, or tooa subnet containing virtual machines.</span></span>

<span data-ttu-id="5c4fc-142">Primeiro, um grupo de segurança de rede precisa toobe criado:</span><span class="sxs-lookup"><span data-stu-id="5c4fc-142">First a network security group needs toobe created:</span></span>

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

<span data-ttu-id="5c4fc-143">Restringir acesso tooonly tráfego interno da rede virtual é muito simple com um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="5c4fc-143">Restricting access tooonly VNet internal traffic is very simple with a network security group.</span></span>  <span data-ttu-id="5c4fc-144">regras do saudação padrão em um grupo de segurança de rede somente permitem o acesso de outros clientes de rede em Olá mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="5c4fc-144">hello default rules in a network security group only allow access from other network clients in hello same virtual network.</span></span>

<span data-ttu-id="5c4fc-145">Como resultado, bloqueando acesso tooSQL servidor é tão simple quanto a aplicação de um grupo de segurança de rede com seus padrão regras tooeither Olá máquinas virtuais que executam o SQL Server ou sub-rede Olá que contêm máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c4fc-145">As a result locking down access tooSQL Server is as simple as applying a network security group with its default rules tooeither hello virtual machines running SQL Server, or hello subnet containing hello virtual machines.</span></span>

<span data-ttu-id="5c4fc-146">exemplo Hello abaixo se aplica a uma sub-rede que contém toohello de grupo rede segurança:</span><span class="sxs-lookup"><span data-stu-id="5c4fc-146">hello sample below applies a network security group toohello containing subnet:</span></span>

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

<span data-ttu-id="5c4fc-147">resultado final de saudação é um conjunto de regras de segurança que bloqueiam o acesso externo, permitindo o acesso de rede virtual interno:</span><span class="sxs-lookup"><span data-stu-id="5c4fc-147">hello end result is a set of security rules that block external access, while allowing VNet internal access:</span></span>

![Regras de segurança de rede padrão][DefaultNetworkSecurityRules]

## <a name="getting-started"></a><span data-ttu-id="5c4fc-149">Introdução</span><span class="sxs-lookup"><span data-stu-id="5c4fc-149">Getting started</span></span>
<span data-ttu-id="5c4fc-150">Todos os artigos e como-para para ambientes de serviço de aplicativo estão disponíveis no hello [Leiame para ambientes de serviço de aplicativo](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="5c4fc-150">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="5c4fc-151">tooget iniciado com ambientes de serviço de aplicativo, consulte [Introdução tooApp ambiente de serviço][IntroToAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="5c4fc-151">tooget started with App Service Environments, see [Introduction tooApp Service Environment][IntroToAppServiceEnvironment]</span></span>

<span data-ttu-id="5c4fc-152">Para obter detalhes sobre o ambiente de serviço de aplicativo tooyour de controlar o tráfego de entrada, consulte [controlando o tráfego de entrada tooan ambiente de serviço de aplicativo][ControlInboundASE]</span><span class="sxs-lookup"><span data-stu-id="5c4fc-152">For details around controlling inbound traffic tooyour App Service Environment, see [Controlling inbound traffic tooan App Service Environment][ControlInboundASE]</span></span>

<span data-ttu-id="5c4fc-153">Para obter mais informações sobre a plataforma do serviço de aplicativo do Azure hello, consulte [do serviço de aplicativo do Azure][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="5c4fc-153">For more information about hello Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[ControlInboundTraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[NetworkAccessControlLists]: https://azure.microsoft.com/documentation/articles/virtual-networks-acl/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ControlInboundASE]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/ 

<!-- IMAGES -->
[SqlServerEndpoint]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/SqlServerEndpoint01.png
[NetworkAccessControlListExample]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/NetworkAcl01.png
[DefaultNetworkSecurityRules]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/DefaultNetworkSecurityRules01.png 
