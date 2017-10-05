---
title: "Conexão segura a recursos de back-end a partir de um ambiente do Serviço de Aplicativo"
description: "Saiba como realizar conexão segura a recursos de back-end a partir de um ambiente do Serviço de Aplicativo."
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
ms.openlocfilehash: 0b6d3a47dc429c469b37c2c74f546cfeca580358
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="securely-connecting-to-backend-resources-from-an-app-service-environment"></a><span data-ttu-id="eab81-103">Conexão segura a recursos de back-end a partir de um ambiente do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="eab81-103">Securely Connecting to Backend Resources from an App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="eab81-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="eab81-104">Overview</span></span>
<span data-ttu-id="eab81-105">Como um Ambiente do Serviço de Aplicativo sempre é criado **ou** em uma rede virtual do Azure Resource Manager, **ou** em uma [rede virtual][virtualnetwork] do modelo de implantação clássico, as conexões de saída de um Ambiente do Serviço de Aplicativo com outros recursos de back-end podem fluir exclusivamente pela rede virtual.</span><span class="sxs-lookup"><span data-stu-id="eab81-105">Since an App Service Environment is always created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model [virtual network][virtualnetwork], outbound connections from an App Service Environment to other backend resources can flow exclusively over the virtual network.</span></span>  <span data-ttu-id="eab81-106">Com uma alteração recente feita em junho de 2016, os ASEs agora podem ser implantados nas redes virtuais que usam os intervalos de endereço público ou espaços de endereço RFC1918 (ou seja,</span><span class="sxs-lookup"><span data-stu-id="eab81-106">With a recent change made in June 2016, ASEs can also be deployed into virtual networks that use either public address ranges, or RFC1918 address spaces (i.e.</span></span> <span data-ttu-id="eab81-107">endereços privados).</span><span class="sxs-lookup"><span data-stu-id="eab81-107">private addresses).</span></span>  

<span data-ttu-id="eab81-108">Por exemplo, pode haver um SQL Server em execução em um cluster de máquinas virtuais com a porta 1433 bloqueada.</span><span class="sxs-lookup"><span data-stu-id="eab81-108">For example, there may be a SQL Server running on a cluster of virtual machines with port 1433 locked down.</span></span>  <span data-ttu-id="eab81-109">O ponto de extremidade pode ser ACLd, para permitir apenas acesso de outros recursos na mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="eab81-109">The endpoint may be ACLd to only allow access from other resources on the same virtual network.</span></span>  

<span data-ttu-id="eab81-110">Como outro exemplo, pontos de extremidade confidenciais podem ser executados localmente e conectados ao Azure via conexões [Site a Site][SiteToSite] ou do [Azure ExpressRoute][ExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="eab81-110">As another example, sensitive endpoints may run on-premises and be connected to Azure via either [Site-to-Site][SiteToSite] or [Azure ExpressRoute][ExpressRoute] connections.</span></span>  <span data-ttu-id="eab81-111">Como resultado, apenas os recursos nas redes virtuais conectadas a túneis Site a Site ou de ExpressRoute poderão acessar pontos de extremidade locais.</span><span class="sxs-lookup"><span data-stu-id="eab81-111">As a result, only resources in virtual networks connected to the Site-to-Site or ExpressRoute tunnels will be able to access on-premises endpoints.</span></span>

<span data-ttu-id="eab81-112">Para todos esses cenários, aplicativos em execução em um ambiente do serviço de aplicativo serão capazes de se conectar com segurança aos diversos servidores e recursos.</span><span class="sxs-lookup"><span data-stu-id="eab81-112">For all of these scenarios, apps running on an App Service Environment will be able to securely connect to the various servers and resources.</span></span>  <span data-ttu-id="eab81-113">Tráfego de saída de aplicativos que são executados em um ambiente do serviço de aplicativo para pontos de extremidade privados na mesma rede virtual (ou conectados à mesma rede virtual) passará apenas pela rede virtual.</span><span class="sxs-lookup"><span data-stu-id="eab81-113">Outbound traffic from apps running in an App Service Environment to private endpoints in the same virtual network (or connected to the same virtual network), will only flow over the virtual network.</span></span>  <span data-ttu-id="eab81-114">O tráfego de saída para pontos de extremidade privados não passará pela Internet pública.</span><span class="sxs-lookup"><span data-stu-id="eab81-114">Outbound traffic to private endpoints will not flow over the public Internet.</span></span>

<span data-ttu-id="eab81-115">Uma limitação se aplica ao tráfego de saída de um ambiente de Serviço de Aplicativo para pontos de extremidade em uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="eab81-115">One caveat applies to outbound traffic from an App Service Environment to endpoints within a virtual network.</span></span>  <span data-ttu-id="eab81-116">Ambientes do Serviço de Aplicativo não podem acessar pontos de extremidade de máquinas virtuais localizados na **mesma** sub-rede que o ambiente do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="eab81-116">App Service Environments cannot reach endpoints of virtual machines located in the **same** subnet as the App Service Environment.</span></span>  <span data-ttu-id="eab81-117">Isso não deve ser um problema, desde que os ambientes do Serviço de Aplicativo sejam implantados em uma sub-rede reservada para uso exclusivo pelo ambiente do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="eab81-117">This normally should not be a problem as long as App Service Environments are deployed into a subnet reserved for exclusive use by only the App Service Environment.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a><span data-ttu-id="eab81-118">Requisitos de DNS e conectividade de saída</span><span class="sxs-lookup"><span data-stu-id="eab81-118">Outbound Connectivity and DNS Requirements</span></span>
<span data-ttu-id="eab81-119">Para um Ambiente de Serviço de Aplicativo funcionar corretamente, ele requer acesso de saída a vários pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="eab81-119">For an App Service Environment to function properly, it requires outbound access to various endpoints.</span></span> <span data-ttu-id="eab81-120">Uma lista completa dos pontos de extremidade externos usado por um ASE está na seção "Conectividade de rede necessária" do artigo [Configuração de rede para o ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) .</span><span class="sxs-lookup"><span data-stu-id="eab81-120">A full list of the external endpoints used by an ASE is in the "Required Network Connectivity" section of the [Network Configuration for ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) article.</span></span>

<span data-ttu-id="eab81-121">Ambientes de Serviço de Aplicativo exigem uma infraestrutura DNS válida configurada para a rede virtual.</span><span class="sxs-lookup"><span data-stu-id="eab81-121">App Service Environments require a valid DNS infrastructure configured for the virtual network.</span></span>  <span data-ttu-id="eab81-122">Se por algum motivo, a configuração do DNS for alterada após ter sido criado um Ambiente do Serviço de Aplicativo, os desenvolvedores podem forçar um Ambiente do Serviço de Aplicativo para captar a nova configuração de DNS.</span><span class="sxs-lookup"><span data-stu-id="eab81-122">If for any reason the DNS configuration is changed after an App Service Environment has been created, developers can force an App Service Environment to pick up the new DNS configuration.</span></span>  <span data-ttu-id="eab81-123">Disparar uma reinicialização do ambiente sem interrupção usando o ícone "Reiniciar" localizado na parte superior da folha de gerenciamento do Ambiente de Serviço de Aplicativo no portal fará com que o ambiente capture a nova configuração de DNS.</span><span class="sxs-lookup"><span data-stu-id="eab81-123">Triggering a rolling environment reboot using the "Restart" icon located at the top of the App Service Environment management blade in the portal will cause the environment to pick up the new DNS configuration.</span></span>

<span data-ttu-id="eab81-124">Também é recomendável que todos os servidores DNS personalizados na rede virtual sejam configurados com antecedência antes da criação de um ambiente do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="eab81-124">It is also recommended that any custom DNS servers on the vnet be setup ahead of time prior to creating an App Service Environment.</span></span>  <span data-ttu-id="eab81-125">Se a configuração DNS de uma rede virtual for alterada enquanto um Ambiente de Serviço de Aplicativo estiver sendo criado, isso resultará em falha do processo de criação do Ambiente de Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="eab81-125">If a virtual network's DNS configuration is changed while an App Service Environment is being created, that will result in the App Service Environment creation process failing.</span></span>  <span data-ttu-id="eab81-126">Do mesmo modo, se um servidor DNS personalizado existir na outra extremidade de um gateway de VPN e estiver inacessível ou indisponível, o processo de criação do Ambiente do Serviço de Aplicativo também falhará.</span><span class="sxs-lookup"><span data-stu-id="eab81-126">In a similar vein, if a custom DNS server exists on the other end of a VPN gateway, and the DNS server is unreachable or unavailable, the App Service Environment creation process will also fail.</span></span>

## <a name="connecting-to-a-sql-server"></a><span data-ttu-id="eab81-127">Conectando-se a um SQL Server</span><span class="sxs-lookup"><span data-stu-id="eab81-127">Connecting to a SQL Server</span></span>
<span data-ttu-id="eab81-128">Uma configuração comum do SQL Server tem um ponto de extremidade escutando na porta 1433:</span><span class="sxs-lookup"><span data-stu-id="eab81-128">A common SQL Server configuration has an endpoint listening on port 1433:</span></span>

![Ponto de extremidade do SQL Server][SqlServerEndpoint]

<span data-ttu-id="eab81-130">Há duas abordagens para restringir o tráfego para esse ponto de extremidade:</span><span class="sxs-lookup"><span data-stu-id="eab81-130">There are two approaches for restricting traffic to this endpoint:</span></span>

* <span data-ttu-id="eab81-131">[Listas de controle de acesso a redes][NetworkAccessControlLists] (ACLs de rede)</span><span class="sxs-lookup"><span data-stu-id="eab81-131">[Network Access Control Lists][NetworkAccessControlLists] (Network ACLs)</span></span>
* <span data-ttu-id="eab81-132">[Grupos de segurança de rede][NetworkSecurityGroups]</span><span class="sxs-lookup"><span data-stu-id="eab81-132">[Network Security Groups][NetworkSecurityGroups]</span></span>

## <a name="restricting-access-with-a-network-acl"></a><span data-ttu-id="eab81-133">Restringindo o acesso com uma ACL de rede</span><span class="sxs-lookup"><span data-stu-id="eab81-133">Restricting Access With a Network ACL</span></span>
<span data-ttu-id="eab81-134">A porta 1433 pode ser protegida usando uma lista de controle de acesso de rede.</span><span class="sxs-lookup"><span data-stu-id="eab81-134">Port 1433 can be secured using a network access control list.</span></span>  <span data-ttu-id="eab81-135">O exemplo abaixo coloca endereços de cliente originados dentro de uma rede virtual em lista branca e bloqueia o acesso a todos os outros clientes.</span><span class="sxs-lookup"><span data-stu-id="eab81-135">The example below whitelists client addresses originating from inside of a virtual network, and blocks access to all other clients.</span></span>

![Exemplo de lista de controle de acesso de rede][NetworkAccessControlListExample]

<span data-ttu-id="eab81-137">Quaisquer aplicativos em execução no ambiente de serviço de aplicativo na mesma rede virtual que o SQL Server serão capazes de se conectarem à instância do SQL Server usando o endereço IP **VNet interno** para a máquina virtual do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="eab81-137">Any applications running in App Service Environment in the same virtual network as the SQL Server will be able to connect to the SQL Server instance using the **VNet internal** IP address for the SQL Server virtual machine.</span></span>  

<span data-ttu-id="eab81-138">A cadeia de conexão de exemplo a seguir faz referência ao SQL Server usando seu endereço IP privado.</span><span class="sxs-lookup"><span data-stu-id="eab81-138">The example connection string below references the SQL Server using its private IP address.</span></span>

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

<span data-ttu-id="eab81-139">Embora a máquina virtual também tenha um ponto de extremidade público, tentativas de conexão usando o endereço IP público serão rejeitadas devido à ACL de rede.</span><span class="sxs-lookup"><span data-stu-id="eab81-139">Although the virtual machine has a public endpoint as well, connection attempts using the public IP address will be rejected because of the network ACL.</span></span> 

## <a name="restricting-access-with-a-network-security-group"></a><span data-ttu-id="eab81-140">Restringindo o acesso com um grupo de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="eab81-140">Restricting Access With a Network Security Group</span></span>
<span data-ttu-id="eab81-141">Uma abordagem alternativa para proteger o acesso é com um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="eab81-141">An alternative approach for securing access is with a network security group.</span></span>  <span data-ttu-id="eab81-142">Grupos de segurança de rede podem ser aplicados a máquinas virtuais individuais ou a uma sub-rede que contenha as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="eab81-142">Network security groups can be applied to individual virtual machines, or to a subnet containing virtual machines.</span></span>

<span data-ttu-id="eab81-143">Primeiro é preciso criar um grupo de segurança de rede:</span><span class="sxs-lookup"><span data-stu-id="eab81-143">First a network security group needs to be created:</span></span>

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

<span data-ttu-id="eab81-144">Restringir o acesso apenas ao tráfego VNet interno é muito simples com um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="eab81-144">Restricting access to only VNet internal traffic is very simple with a network security group.</span></span>  <span data-ttu-id="eab81-145">As regras padrão em um grupo de segurança de rede somente permitem o acesso a partir de outros clientes de rede na mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="eab81-145">The default rules in a network security group only allow access from other network clients in the same virtual network.</span></span>

<span data-ttu-id="eab81-146">Como resultado, bloquear o acesso ao SQL Server é tão simples quanto a aplicação de um grupo de segurança de rede com suas regras padrão às máquinas virtuais executando o SQL Server ou então à sub-rede que contém as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="eab81-146">As a result locking down access to SQL Server is as simple as applying a network security group with its default rules to either the virtual machines running SQL Server, or the subnet containing the virtual machines.</span></span>

<span data-ttu-id="eab81-147">O exemplo a seguir aplica a um grupo de segurança de rede à sub-rede que o contém:</span><span class="sxs-lookup"><span data-stu-id="eab81-147">The sample below applies a network security group to the containing subnet:</span></span>

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

<span data-ttu-id="eab81-148">O resultado final é um conjunto de regras de segurança que bloqueiam o acesso externo, permitindo acesso interno VNet:</span><span class="sxs-lookup"><span data-stu-id="eab81-148">The end result is a set of security rules that block external access, while allowing VNet internal access:</span></span>

![Regras de segurança de rede padrão][DefaultNetworkSecurityRules]

## <a name="getting-started"></a><span data-ttu-id="eab81-150">Introdução</span><span class="sxs-lookup"><span data-stu-id="eab81-150">Getting started</span></span>
<span data-ttu-id="eab81-151">Todos os artigos e os Como fazer para Ambientes de Serviço de Aplicativo estão disponíveis no [LEIAME para Ambientes de Serviço de Aplicativo](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="eab81-151">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="eab81-152">Para começar a usar Ambientes de Serviço de Aplicativo, veja [Introdução ao ambiente de Serviço de Aplicativo][IntroToAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="eab81-152">To get started with App Service Environments, see [Introduction to App Service Environment][IntroToAppServiceEnvironment]</span></span>

<span data-ttu-id="eab81-153">Para obter detalhes sobre como controlar o tráfego de entrada para seu Ambiente do Serviço de Aplicativo, confira [Como controlar o tráfego de entrada para um Ambiente do Serviço de Aplicativo][ControlInboundASE]</span><span class="sxs-lookup"><span data-stu-id="eab81-153">For details around controlling inbound traffic to your App Service Environment, see [Controlling inbound traffic to an App Service Environment][ControlInboundASE]</span></span>

<span data-ttu-id="eab81-154">Para saber mais sobre a plataforma de Serviço de Aplicativo do Azure, veja [Serviço de Aplicativo do Azure][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="eab81-154">For more information about the Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

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
