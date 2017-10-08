---
title: "aaaLayered arquitetura de segurança com os ambientes de serviço de aplicativo"
description: "Implementando uma arquitetura de segurança em camadas com Ambientes do Serviço de Aplicativo."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 73ce0213-bd3e-4876-b1ed-5ecad4ad5601
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: stefsch
ms.openlocfilehash: 0627ba6fa849908506fe62c451c888c147cabc03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="implementing-a-layered-security-architecture-with-app-service-environments"></a><span data-ttu-id="91cec-103">Implementando uma arquitetura de segurança em camadas com Ambientes do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="91cec-103">Implementing a Layered Security Architecture with App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="91cec-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="91cec-104">Overview</span></span>
<span data-ttu-id="91cec-105">Como os Ambientes do Serviço de Aplicativo fornecem um ambiente de tempo de execução isolado implantado em uma rede virtual, os desenvolvedores podem criar uma arquitetura de segurança em camadas fornecendo diferentes níveis de acesso à rede para cada camada de aplicativo físico.</span><span class="sxs-lookup"><span data-stu-id="91cec-105">Since App Service Environments provide an isolated runtime environment deployed into a virtual network, developers can create a layered security architecture providing differing levels of network access for each physical application tier.</span></span>

<span data-ttu-id="91cec-106">Desejo comum é toohide API back-ends de acessar a Internet geral e só permitir que APIs toobe chamado por aplicativos web upstream.</span><span class="sxs-lookup"><span data-stu-id="91cec-106">A common desire is toohide API back-ends from general Internet access, and only allow APIs toobe called by upstream web apps.</span></span>  <span data-ttu-id="91cec-107">[Grupos de segurança (NSGs) de rede] [ NetworkSecurityGroups] pode ser usado em sub-redes que contém os ambientes de serviço de aplicativo toorestrict acesso público tooAPI aplicativos.</span><span class="sxs-lookup"><span data-stu-id="91cec-107">[Network security groups (NSGs)][NetworkSecurityGroups] can be used on subnets containing App Service Environments toorestrict public access tooAPI applications.</span></span>

<span data-ttu-id="91cec-108">Olá diagrama a seguir mostra uma arquitetura de exemplo com um aplicativo WebAPI com base em implantado em um ambiente de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91cec-108">hello diagram below shows an example architecture with a WebAPI based app deployed on an App Service Environment.</span></span>  <span data-ttu-id="91cec-109">Três instâncias de aplicativo web separado, implantadas em três ambientes separados de serviço do aplicativo, faça chamadas de back-end toohello mesmo aplicativo WebAPI.</span><span class="sxs-lookup"><span data-stu-id="91cec-109">Three separate web app instances, deployed on three separate App Service Environments, make back-end calls toohello same WebAPI app.</span></span>

![Arquitetura conceitual][ConceptualArchitecture] 

<span data-ttu-id="91cec-111">Olá, sinais de mais indicar que Olá grupo de segurança de rede na sub-rede Olá contendo "apiase" permite que chamadas recebidas de saudação aplicativos web upstream, também chamadas de si mesma.</span><span class="sxs-lookup"><span data-stu-id="91cec-111">hello green plus signs indicate that hello network security group on hello subnet containing "apiase" allows inbound calls from hello upstream web apps, as well calls from itself.</span></span>  <span data-ttu-id="91cec-112">Mas Olá nega explicitamente o mesmo grupo de segurança de rede acessar toogeneral Olá Internet o tráfego de entrada.</span><span class="sxs-lookup"><span data-stu-id="91cec-112">However hello same network security group explicitly denies access toogeneral inbound traffic from hello Internet.</span></span> 

<span data-ttu-id="91cec-113">restante deste tópico Olá orienta por meio do grupo de segurança de rede Olá etapas necessárias tooconfigure Olá na sub-rede Olá contendo "apiase".</span><span class="sxs-lookup"><span data-stu-id="91cec-113">hello remainder of this topic walks through hello steps needed tooconfigure hello network security group on hello subnet containing "apiase".</span></span>

## <a name="determining-hello-network-behavior"></a><span data-ttu-id="91cec-114">Determinando Olá comportamento de rede</span><span class="sxs-lookup"><span data-stu-id="91cec-114">Determining hello Network Behavior</span></span>
<span data-ttu-id="91cec-115">Na ordem tooknow quais regras são necessárias, a segurança da rede é necessário toodetermine quais clientes de rede poderá ser tooreach Olá ambiente de serviço de aplicativo contendo saudação do aplicativo de API e quais clientes serão bloqueados.</span><span class="sxs-lookup"><span data-stu-id="91cec-115">In order tooknow what network security rules are needed, you need toodetermine which network clients will be allowed tooreach hello App Service Environment containing hello API app, and which clients will be blocked.</span></span>

<span data-ttu-id="91cec-116">Como [(NSGs) de grupos de segurança de rede] [ NetworkSecurityGroups] são aplicadas toosubnets e ambientes de serviço de aplicativo são implantados em sub-redes, regras de saudação contidas em um NSG aplicam-se muito**todas as** aplicativos executados em um ambiente de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91cec-116">Since [network security groups (NSGs)][NetworkSecurityGroups] are applied toosubnets, and App Service Environments are deployed into subnets, hello rules contained in an NSG apply too**all** apps running on an App Service Environment.</span></span>  <span data-ttu-id="91cec-117">Usando a arquitetura de exemplo hello neste artigo, depois que um grupo de segurança de rede é toohello aplicada sub-rede que contém "apiase", todos os aplicativos em execução no hello "apiase" ambiente de serviço de aplicativo será protegido pelo Olá mesmo conjunto de regras de segurança.</span><span class="sxs-lookup"><span data-stu-id="91cec-117">Using hello sample architecture for this article, once a network security group is applied toohello subnet containing "apiase", all apps running on hello "apiase" App Service Environment will be protected by hello same set of security rules.</span></span> 

* <span data-ttu-id="91cec-118">**Determinar o endereço IP saído Olá de chamadores upstream:** novidades Olá endereço ou endereços IP de chamadores upstream Olá?</span><span class="sxs-lookup"><span data-stu-id="91cec-118">**Determine hello outbound IP address of upstream callers:**  What is hello IP address or addresses of hello upstream callers?</span></span>  <span data-ttu-id="91cec-119">Esses endereços precisará toobe explicitamente, o acesso é permitido em Olá NSG.</span><span class="sxs-lookup"><span data-stu-id="91cec-119">These addresses will need toobe explicitly allowed access in hello NSG.</span></span>  <span data-ttu-id="91cec-120">Como chamadas entre ambientes de serviço de aplicativo são consideradas chamadas de "Internet", isso significa Olá saída IP endereço atribuído tooeach de saudação três upstream ambientes de serviço de aplicativo necessidades toobe acesso Olá NSG para a sub-rede do hello "apiase".</span><span class="sxs-lookup"><span data-stu-id="91cec-120">Since calls between App Service Environments are considered "Internet" calls, this means hello outbound IP address assigned tooeach of hello three upstream App Service Environments needs toobe allowed access in hello NSG for hello "apiase" subnet.</span></span>   <span data-ttu-id="91cec-121">Para obter mais detalhes sobre como determinar o endereço IP da saída Olá para aplicativos em execução em um ambiente de serviço de aplicativo, consulte Olá [arquitetura de rede] [ NetworkArchitecture] artigo de visão geral.</span><span class="sxs-lookup"><span data-stu-id="91cec-121">For more details on determining hello outbound IP address for apps running in an App Service Environment see hello [Network Architecture][NetworkArchitecture] Overview article.</span></span>
* <span data-ttu-id="91cec-122">**Aplicativo de API de back-end Olá precisará toocall em si?**</span><span class="sxs-lookup"><span data-stu-id="91cec-122">**Will hello back-end API app need toocall itself?**</span></span>  <span data-ttu-id="91cec-123">Um ponto, às vezes, desconsiderado e sutil é cenário Olá onde o aplicativo de back-end hello precisa toocall em si.</span><span class="sxs-lookup"><span data-stu-id="91cec-123">A sometimes overlooked and subtle point is hello scenario where hello back-end application needs toocall itself.</span></span>  <span data-ttu-id="91cec-124">Se um aplicativo de API de back-end em um ambiente de serviço de aplicativo precisa toocall em si, também será tratada como uma chamada de "Internet".</span><span class="sxs-lookup"><span data-stu-id="91cec-124">If a back-end API application on an App Service Environment needs toocall itself, this is also treated as an "Internet" call.</span></span>  <span data-ttu-id="91cec-125">Arquitetura de exemplo hello isso requer permissão de acesso de endereço IP saído de saudação do hello "apiase" ambiente de serviço de aplicativo também.</span><span class="sxs-lookup"><span data-stu-id="91cec-125">In hello sample architecture this requires allowing access from hello outbound IP address of hello "apiase" App Service Environment as well.</span></span>

## <a name="setting-up-hello-network-security-group"></a><span data-ttu-id="91cec-126">Configurando Olá grupo de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="91cec-126">Setting up hello Network Security Group</span></span>
<span data-ttu-id="91cec-127">Depois que o hello conjunto de endereços IP de saída são conhecidos, Olá próxima etapa é tooconstruct um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="91cec-127">Once hello set of outbound IP addresses are known, hello next step is tooconstruct a network security group.</span></span>  <span data-ttu-id="91cec-128">Os grupos de segurança de rede podem ser criados para as redes virtuais baseadas no Resource Manager, bem como para as redes virtuais clássicas.</span><span class="sxs-lookup"><span data-stu-id="91cec-128">Network security groups can be created for both Resource Manager based virtual networks, as well as classic virtual networks.</span></span>  <span data-ttu-id="91cec-129">exemplos de saudação abaixo mostram criando e configurando um NSG em uma rede virtual clássica usando o Powershell.</span><span class="sxs-lookup"><span data-stu-id="91cec-129">hello examples below show creating and configuring an NSG on a classic virtual network using Powershell.</span></span>

<span data-ttu-id="91cec-130">Para a arquitetura de exemplo hello, ambientes Olá estão localizados no Centro Sul dos EUA, então um NSG vazio é criado nessa região:</span><span class="sxs-lookup"><span data-stu-id="91cec-130">For hello sample architecture, hello environments are located in South Central US, so an empty NSG is created in that region:</span></span>

    New-AzureNetworkSecurityGroup -Name "RestrictBackendApi" -Location "South Central US" -Label "Only allow web frontend and loopback traffic"

<span data-ttu-id="91cec-131">Primeiro explícito permitir regra será adicionada para a infraestrutura de gerenciamento do Azure Olá descrita no artigo Olá em [o tráfego de entrada] [ InboundTraffic] para ambientes de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91cec-131">First an explicit allow rule is added for hello Azure management infrastructure as noted in hello article on [inbound traffic][InboundTraffic] for App Service Environments.</span></span>

    #Open ports for access by Azure management infrastructure
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET' -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP

<span data-ttu-id="91cec-132">Em seguida, duas regras são adicionadas tooallow HTTP e HTTPS chamadas de Olá primeiro upstream aplicativo ambiente de serviço ("fe1ase").</span><span class="sxs-lookup"><span data-stu-id="91cec-132">Next, two rules are added tooallow HTTP and HTTPS calls from hello first upstream App Service Environment ("fe1ase").</span></span>

    #Grant access toorequests from hello first upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe1ase" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe1ase" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="91cec-133">Aprimorá e repetir para Olá segundo e terceiro upstream aplicativo ambientes de serviço ("fe2ase" e "fe3ase").</span><span class="sxs-lookup"><span data-stu-id="91cec-133">Rinse and repeat for hello second and third upstream App Service Environments ("fe2ase"and "fe3ase").</span></span>

    #Grant access toorequests from hello second upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe2ase" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe2ase" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

    #Grant access toorequests from hello third upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe3ase" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe3ase" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="91cec-134">Por fim, conceda acesso toohello saído endereço IP do ambiente de serviço de aplicativo da API de back-end Olá para que ele possa chamar novamente para si mesmo.</span><span class="sxs-lookup"><span data-stu-id="91cec-134">Lastly, grant access toohello outbound IP address of hello back-end API's App Service Environment so that it can call back into itself.</span></span>

    #Allow apps on hello apiase environment toocall back into itself
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP apiase" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS apiase" -Type Inbound -Priority 900 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="91cec-135">Nenhuma outra regra de segurança de rede necessário toobe configurado porque cada NSG tem um conjunto de regras padrão que bloqueiam o acesso de entrada de saudação da Internet por padrão.</span><span class="sxs-lookup"><span data-stu-id="91cec-135">No other network security rules need toobe configured because every NSG has a set of default rules that block inbound access from hello Internet by default.</span></span>

<span data-ttu-id="91cec-136">lista completa de saudação de regras no grupo de segurança de rede Olá são mostrados abaixo.</span><span class="sxs-lookup"><span data-stu-id="91cec-136">hello full list of rules in hello network security group are shown below.</span></span>  <span data-ttu-id="91cec-137">Observe como Olá última regra, que é realçada, bloqueia o acesso de entrada de todos os chamadores que não sejam aqueles que têm acesso.</span><span class="sxs-lookup"><span data-stu-id="91cec-137">Note how hello last rule, which is highlighted, blocks inbound access from all callers other than those which have been explicitly granted access.</span></span>

![Configuração do NSG][NSGConfiguration] 

<span data-ttu-id="91cec-139">Olá última etapa é tooapply Olá NSG toohello sub-rede contém hello "apiase" ambiente de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91cec-139">hello final step is tooapply hello NSG toohello subnet that contains hello "apiase" App Service Environment.</span></span>  

     #Apply hello NSG toohello backend API subnet
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'yourvnetnamehere' -SubnetName 'API-ASE-Subnet'

<span data-ttu-id="91cec-140">Olá NSG aplicada toohello sub-rede, somente hello três ambientes de serviço de aplicativo upstream e Olá Olá recipiente do ambiente de serviço de aplicativo API back-end, são permitidas toocall no ambiente de "apiase" hello.</span><span class="sxs-lookup"><span data-stu-id="91cec-140">With hello NSG applied toohello subnet, only hello three upstream App Service Environments, and hello App Service Environment containing hello API back-end, are allowed toocall into hello "apiase" environment.</span></span>

## <a name="additional-links-and-information"></a><span data-ttu-id="91cec-141">Informações e links adicionais</span><span class="sxs-lookup"><span data-stu-id="91cec-141">Additional Links and Information</span></span>
<span data-ttu-id="91cec-142">Todos os artigos e como-para para ambientes de serviço de aplicativo estão disponíveis no hello [Leiame para ambientes de serviço de aplicativo](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="91cec-142">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="91cec-143">Informações sobre [grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="91cec-143">Information about [network security groups](../virtual-network/virtual-networks-nsg.md).</span></span> 

<span data-ttu-id="91cec-144">Noções básicas sobre [endereços IP de saída][NetworkArchitecture] e Ambientes do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91cec-144">Understanding [outbound IP addresses][NetworkArchitecture] and App Service Environments.</span></span>

<span data-ttu-id="91cec-145">[Portas de rede][InboundTraffic] usadas pelos Ambientes do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91cec-145">[Network ports][InboundTraffic] used by App Service Environments.</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[NetworkArchitecture]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[InboundTraffic]:  https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-control-inbound-traffic/

<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-layered-security/ConceptualArchitecture-1.png
[NSGConfiguration]:  ./media/app-service-app-service-environment-layered-security/NSGConfiguration-1.png
