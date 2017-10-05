---
title: "Arquitetura de segurança em camadas com os Ambientes do Serviço de Aplicativo"
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
ms.openlocfilehash: 0fb02c13f99a8f4a46e0142c20da3b152c809b6b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="implementing-a-layered-security-architecture-with-app-service-environments"></a><span data-ttu-id="5894e-103">Implementando uma arquitetura de segurança em camadas com Ambientes do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="5894e-103">Implementing a Layered Security Architecture with App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="5894e-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="5894e-104">Overview</span></span>
<span data-ttu-id="5894e-105">Como os Ambientes do Serviço de Aplicativo fornecem um ambiente de tempo de execução isolado implantado em uma rede virtual, os desenvolvedores podem criar uma arquitetura de segurança em camadas fornecendo diferentes níveis de acesso à rede para cada camada de aplicativo físico.</span><span class="sxs-lookup"><span data-stu-id="5894e-105">Since App Service Environments provide an isolated runtime environment deployed into a virtual network, developers can create a layered security architecture providing differing levels of network access for each physical application tier.</span></span>

<span data-ttu-id="5894e-106">Um desejo comum é ocultar os back-ends de API do acesso à Internet geral e só permitir que as APIs sejam chamadas por aplicativos Web upstream.</span><span class="sxs-lookup"><span data-stu-id="5894e-106">A common desire is to hide API back-ends from general Internet access, and only allow APIs to be called by upstream web apps.</span></span>  <span data-ttu-id="5894e-107">Os [NSGs (grupos de segurança de rede)][NetworkSecurityGroups] podem ser usados em sub-redes contendo Ambientes do Serviço de Aplicativo para restringir o acesso público aos aplicativos da API.</span><span class="sxs-lookup"><span data-stu-id="5894e-107">[Network security groups (NSGs)][NetworkSecurityGroups] can be used on subnets containing App Service Environments to restrict public access to API applications.</span></span>

<span data-ttu-id="5894e-108">O diagrama abaixo mostra uma arquitetura de exemplo com um aplicativo baseado em API Web implantado em um Ambiente do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5894e-108">The diagram below shows an example architecture with a WebAPI based app deployed on an App Service Environment.</span></span>  <span data-ttu-id="5894e-109">Três instâncias de aplicativos Web separados, implantadas em três Ambientes do Serviço de Aplicativo separados, fazem chamadas de back-end para o mesmo aplicativo da API Web.</span><span class="sxs-lookup"><span data-stu-id="5894e-109">Three separate web app instances, deployed on three separate App Service Environments, make back-end calls to the same WebAPI app.</span></span>

![Arquitetura conceitual][ConceptualArchitecture] 

<span data-ttu-id="5894e-111">O sinal de adição verde indica que o grupo de segurança de rede na sub-rede contendo “apiase” permite chamadas recebidas de aplicativos Web upstream, bem como chamadas de si mesmo.</span><span class="sxs-lookup"><span data-stu-id="5894e-111">The green plus signs indicate that the network security group on the subnet containing "apiase" allows inbound calls from the upstream web apps, as well calls from itself.</span></span>  <span data-ttu-id="5894e-112">No entanto, o mesmo grupo de segurança de rede nega explicitamente o acesso ao tráfego de entrada geral da Internet.</span><span class="sxs-lookup"><span data-stu-id="5894e-112">However the same network security group explicitly denies access to general inbound traffic from the Internet.</span></span> 

<span data-ttu-id="5894e-113">O restante deste tópico explica as etapas necessárias para configurar o grupo de segurança de rede na sub-rede contendo “apiase”.</span><span class="sxs-lookup"><span data-stu-id="5894e-113">The remainder of this topic walks through the steps needed to configure the network security group on the subnet containing "apiase".</span></span>

## <a name="determining-the-network-behavior"></a><span data-ttu-id="5894e-114">Determinando o comportamento de rede</span><span class="sxs-lookup"><span data-stu-id="5894e-114">Determining the Network Behavior</span></span>
<span data-ttu-id="5894e-115">Para saber quais regras de segurança de rede são necessárias, você precisa determinar quais clientes de rede terão permissão para acessar o Ambiente do Serviço de Aplicativo que contém o aplicativo de API e quais clientes serão bloqueados.</span><span class="sxs-lookup"><span data-stu-id="5894e-115">In order to know what network security rules are needed, you need to determine which network clients will be allowed to reach the App Service Environment containing the API app, and which clients will be blocked.</span></span>

<span data-ttu-id="5894e-116">Como os [NSGs (grupos de segurança de rede)][NetworkSecurityGroups] são aplicados às sub-redes e os Ambientes do Serviço de Aplicativo são implantados em sub-redes, as regras contidas em um NSG se aplicam a **todos** os aplicativos em execução em um Ambiente do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5894e-116">Since [network security groups (NSGs)][NetworkSecurityGroups] are applied to subnets, and App Service Environments are deployed into subnets, the rules contained in an NSG apply to **all** apps running on an App Service Environment.</span></span>  <span data-ttu-id="5894e-117">Usando a arquitetura de exemplo deste artigo, depois que um grupo de segurança de rede for aplicado à sub-rede contendo “apiase”, todos os aplicativos em execução no Ambiente do Serviço de Aplicativo “apiase” estarão protegidos pelo mesmo conjunto de regras de segurança.</span><span class="sxs-lookup"><span data-stu-id="5894e-117">Using the sample architecture for this article, once a network security group is applied to the subnet containing "apiase", all apps running on the "apiase" App Service Environment will be protected by the same set of security rules.</span></span> 

* <span data-ttu-id="5894e-118">**Determine o endereço IP de saída dos autores da chamada upstream:** Qual é o endereço IP ou endereços dos autores da chamada upstream?</span><span class="sxs-lookup"><span data-stu-id="5894e-118">**Determine the outbound IP address of upstream callers:**  What is the IP address or addresses of the upstream callers?</span></span>  <span data-ttu-id="5894e-119">Esses endereços precisarão receber explicitamente a permissão de acesso no NSG.</span><span class="sxs-lookup"><span data-stu-id="5894e-119">These addresses will need to be explicitly allowed access in the NSG.</span></span>  <span data-ttu-id="5894e-120">Como as chamadas entre os Ambientes do Serviço de Aplicativo são consideradas chamadas da “Internet”, isso significa que o endereço IP de saída atribuído a cada um dos três Ambientes do Serviço de Aplicativo upstream precisa receber permissão de acesso no NSG para a sub-rede “apiase”.</span><span class="sxs-lookup"><span data-stu-id="5894e-120">Since calls between App Service Environments are considered "Internet" calls, this means the outbound IP address assigned to each of the three upstream App Service Environments needs to be allowed access in the NSG for the "apiase" subnet.</span></span>   <span data-ttu-id="5894e-121">Para obter mais detalhes sobre como determinar o endereço IP de saída para aplicativos executados em um Ambiente do Serviço de Aplicativo, confira o artigo de Visão geral da [Arquitetura de rede][NetworkArchitecture].</span><span class="sxs-lookup"><span data-stu-id="5894e-121">For more details on determining the outbound IP address for apps running in an App Service Environment see the [Network Architecture][NetworkArchitecture] Overview article.</span></span>
* <span data-ttu-id="5894e-122">**O aplicativo de API de back-end precisará chamar a si mesmo?**</span><span class="sxs-lookup"><span data-stu-id="5894e-122">**Will the back-end API app need to call itself?**</span></span>  <span data-ttu-id="5894e-123">Um ponto sutil e às vezes negligenciado é o cenário em que o aplicativo de back-end precisa chamar a si mesmo.</span><span class="sxs-lookup"><span data-stu-id="5894e-123">A sometimes overlooked and subtle point is the scenario where the back-end application needs to call itself.</span></span>  <span data-ttu-id="5894e-124">Se um aplicativo de API de back-end em um Ambiente do Serviço de Aplicativo precisar chamar a si mesmo, isso também será tratado como uma chamada da “Internet”.</span><span class="sxs-lookup"><span data-stu-id="5894e-124">If a back-end API application on an App Service Environment needs to call itself, this is also treated as an "Internet" call.</span></span>  <span data-ttu-id="5894e-125">Na arquitetura de exemplo, isso também requer a permissão de acesso do endereço IP de saída do Ambiente do Serviço de Aplicativo “apiase”.</span><span class="sxs-lookup"><span data-stu-id="5894e-125">In the sample architecture this requires allowing access from the outbound IP address of the "apiase" App Service Environment as well.</span></span>

## <a name="setting-up-the-network-security-group"></a><span data-ttu-id="5894e-126">Configurando o Grupo de Segurança de Rede</span><span class="sxs-lookup"><span data-stu-id="5894e-126">Setting up the Network Security Group</span></span>
<span data-ttu-id="5894e-127">Depois que o conjunto de endereços IP de saída forem conhecidos, a próxima etapa é criar um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="5894e-127">Once the set of outbound IP addresses are known, the next step is to construct a network security group.</span></span>  <span data-ttu-id="5894e-128">Os grupos de segurança de rede podem ser criados para as redes virtuais baseadas no Resource Manager, bem como para as redes virtuais clássicas.</span><span class="sxs-lookup"><span data-stu-id="5894e-128">Network security groups can be created for both Resource Manager based virtual networks, as well as classic virtual networks.</span></span>  <span data-ttu-id="5894e-129">Os exemplos a seguir mostram a criação e a configuração de um NSG em uma rede virtual clássica usando o Powershell.</span><span class="sxs-lookup"><span data-stu-id="5894e-129">The examples below show creating and configuring an NSG on a classic virtual network using Powershell.</span></span>

<span data-ttu-id="5894e-130">Para a arquitetura de exemplo, como os ambientes estão localizados no Centro Sul dos EUA, um NSG vazio é criado nessa região:</span><span class="sxs-lookup"><span data-stu-id="5894e-130">For the sample architecture, the environments are located in South Central US, so an empty NSG is created in that region:</span></span>

    New-AzureNetworkSecurityGroup -Name "RestrictBackendApi" -Location "South Central US" -Label "Only allow web frontend and loopback traffic"

<span data-ttu-id="5894e-131">Primeiro uma regra de permissão explícita é adicionada para a infraestrutura de gerenciamento do Azure, como observado no artigo sobre o [tráfego de entrada][InboundTraffic] dos Ambientes do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5894e-131">First an explicit allow rule is added for the Azure management infrastructure as noted in the article on [inbound traffic][InboundTraffic] for App Service Environments.</span></span>

    #Open ports for access by Azure management infrastructure
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET' -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP

<span data-ttu-id="5894e-132">Em seguida, duas regras foram adicionadas para permitir chamadas HTTP e HTTPS do primeiro Ambiente do Serviço de Aplicativo upstream (“fe1ase”).</span><span class="sxs-lookup"><span data-stu-id="5894e-132">Next, two rules are added to allow HTTP and HTTPS calls from the first upstream App Service Environment ("fe1ase").</span></span>

    #Grant access to requests from the first upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe1ase" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe1ase" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="5894e-133">Aplique e repita para o segundo e terceiro Ambientes do Serviço de Aplicativo upstream (“fe2ase” e “fe3ase”).</span><span class="sxs-lookup"><span data-stu-id="5894e-133">Rinse and repeat for the second and third upstream App Service Environments ("fe2ase"and "fe3ase").</span></span>

    #Grant access to requests from the second upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe2ase" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe2ase" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

    #Grant access to requests from the third upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe3ase" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe3ase" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="5894e-134">Por fim, conceda acesso ao endereço IP de saída do Ambiente do Serviço de Aplicativo da API de back-end para que ele possa chamar de volta a si mesmo.</span><span class="sxs-lookup"><span data-stu-id="5894e-134">Lastly, grant access to the outbound IP address of the back-end API's App Service Environment so that it can call back into itself.</span></span>

    #Allow apps on the apiase environment to call back into itself
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP apiase" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS apiase" -Type Inbound -Priority 900 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="5894e-135">Nenhuma outra regra de segurança de rede precisa ser configurada, pois cada NSG tem um conjunto de regras padrão que bloqueia o acesso de entrada da Internet por padrão.</span><span class="sxs-lookup"><span data-stu-id="5894e-135">No other network security rules need to be configured because every NSG has a set of default rules that block inbound access from the Internet by default.</span></span>

<span data-ttu-id="5894e-136">A lista completa das regras no grupo de segurança de rede é mostrada abaixo.</span><span class="sxs-lookup"><span data-stu-id="5894e-136">The full list of rules in the network security group are shown below.</span></span>  <span data-ttu-id="5894e-137">Observe como a última regra, que é realçada, bloqueia o acesso de entrada de todos os autores da chamada diferentes daqueles que receberam o acesso explicitamente.</span><span class="sxs-lookup"><span data-stu-id="5894e-137">Note how the last rule, which is highlighted, blocks inbound access from all callers other than those which have been explicitly granted access.</span></span>

![Configuração do NSG][NSGConfiguration] 

<span data-ttu-id="5894e-139">A etapa final é aplicar o NSG à sub-rede que contém o Ambiente do Serviço de Aplicativo “apiase”.</span><span class="sxs-lookup"><span data-stu-id="5894e-139">The final step is to apply the NSG to the subnet that contains the "apiase" App Service Environment.</span></span>  

     #Apply the NSG to the backend API subnet
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'yourvnetnamehere' -SubnetName 'API-ASE-Subnet'

<span data-ttu-id="5894e-140">Com o NSG aplicado à sub-rede, somente três Ambientes do Serviço de Aplicativo upstream e o Ambiente do Serviço de Aplicativo contendo o back-end da API têm permissão para realizar chamadas no ambiente de “apiase”.</span><span class="sxs-lookup"><span data-stu-id="5894e-140">With the NSG applied to the subnet, only the three upstream App Service Environments, and the App Service Environment containing the API back-end, are allowed to call into the "apiase" environment.</span></span>

## <a name="additional-links-and-information"></a><span data-ttu-id="5894e-141">Informações e links adicionais</span><span class="sxs-lookup"><span data-stu-id="5894e-141">Additional Links and Information</span></span>
<span data-ttu-id="5894e-142">Todos os artigos e instruções sobre os Ambientes do Serviço de Aplicativo estão disponíveis no [LEIAME para Ambientes do Serviço de Aplicativo](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="5894e-142">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="5894e-143">Informações sobre [grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="5894e-143">Information about [network security groups](../virtual-network/virtual-networks-nsg.md).</span></span> 

<span data-ttu-id="5894e-144">Noções básicas sobre [endereços IP de saída][NetworkArchitecture] e Ambientes do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5894e-144">Understanding [outbound IP addresses][NetworkArchitecture] and App Service Environments.</span></span>

<span data-ttu-id="5894e-145">[Portas de rede][InboundTraffic] usadas pelos Ambientes do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5894e-145">[Network ports][InboundTraffic] used by App Service Environments.</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[NetworkArchitecture]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[InboundTraffic]:  https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-control-inbound-traffic/

<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-layered-security/ConceptualArchitecture-1.png
[NSGConfiguration]:  ./media/app-service-app-service-environment-layered-security/NSGConfiguration-1.png
