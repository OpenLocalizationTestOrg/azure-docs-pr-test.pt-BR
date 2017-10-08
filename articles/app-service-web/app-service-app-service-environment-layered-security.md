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
# <a name="implementing-a-layered-security-architecture-with-app-service-environments"></a>Implementando uma arquitetura de segurança em camadas com Ambientes do Serviço de Aplicativo
## <a name="overview"></a>Visão geral
Como os Ambientes do Serviço de Aplicativo fornecem um ambiente de tempo de execução isolado implantado em uma rede virtual, os desenvolvedores podem criar uma arquitetura de segurança em camadas fornecendo diferentes níveis de acesso à rede para cada camada de aplicativo físico.

Desejo comum é toohide API back-ends de acessar a Internet geral e só permitir que APIs toobe chamado por aplicativos web upstream.  [Grupos de segurança (NSGs) de rede] [ NetworkSecurityGroups] pode ser usado em sub-redes que contém os ambientes de serviço de aplicativo toorestrict acesso público tooAPI aplicativos.

Olá diagrama a seguir mostra uma arquitetura de exemplo com um aplicativo WebAPI com base em implantado em um ambiente de serviço de aplicativo.  Três instâncias de aplicativo web separado, implantadas em três ambientes separados de serviço do aplicativo, faça chamadas de back-end toohello mesmo aplicativo WebAPI.

![Arquitetura conceitual][ConceptualArchitecture] 

Olá, sinais de mais indicar que Olá grupo de segurança de rede na sub-rede Olá contendo "apiase" permite que chamadas recebidas de saudação aplicativos web upstream, também chamadas de si mesma.  Mas Olá nega explicitamente o mesmo grupo de segurança de rede acessar toogeneral Olá Internet o tráfego de entrada. 

restante deste tópico Olá orienta por meio do grupo de segurança de rede Olá etapas necessárias tooconfigure Olá na sub-rede Olá contendo "apiase".

## <a name="determining-hello-network-behavior"></a>Determinando Olá comportamento de rede
Na ordem tooknow quais regras são necessárias, a segurança da rede é necessário toodetermine quais clientes de rede poderá ser tooreach Olá ambiente de serviço de aplicativo contendo saudação do aplicativo de API e quais clientes serão bloqueados.

Como [(NSGs) de grupos de segurança de rede] [ NetworkSecurityGroups] são aplicadas toosubnets e ambientes de serviço de aplicativo são implantados em sub-redes, regras de saudação contidas em um NSG aplicam-se muito**todas as** aplicativos executados em um ambiente de serviço de aplicativo.  Usando a arquitetura de exemplo hello neste artigo, depois que um grupo de segurança de rede é toohello aplicada sub-rede que contém "apiase", todos os aplicativos em execução no hello "apiase" ambiente de serviço de aplicativo será protegido pelo Olá mesmo conjunto de regras de segurança. 

* **Determinar o endereço IP saído Olá de chamadores upstream:** novidades Olá endereço ou endereços IP de chamadores upstream Olá?  Esses endereços precisará toobe explicitamente, o acesso é permitido em Olá NSG.  Como chamadas entre ambientes de serviço de aplicativo são consideradas chamadas de "Internet", isso significa Olá saída IP endereço atribuído tooeach de saudação três upstream ambientes de serviço de aplicativo necessidades toobe acesso Olá NSG para a sub-rede do hello "apiase".   Para obter mais detalhes sobre como determinar o endereço IP da saída Olá para aplicativos em execução em um ambiente de serviço de aplicativo, consulte Olá [arquitetura de rede] [ NetworkArchitecture] artigo de visão geral.
* **Aplicativo de API de back-end Olá precisará toocall em si?**  Um ponto, às vezes, desconsiderado e sutil é cenário Olá onde o aplicativo de back-end hello precisa toocall em si.  Se um aplicativo de API de back-end em um ambiente de serviço de aplicativo precisa toocall em si, também será tratada como uma chamada de "Internet".  Arquitetura de exemplo hello isso requer permissão de acesso de endereço IP saído de saudação do hello "apiase" ambiente de serviço de aplicativo também.

## <a name="setting-up-hello-network-security-group"></a>Configurando Olá grupo de segurança de rede
Depois que o hello conjunto de endereços IP de saída são conhecidos, Olá próxima etapa é tooconstruct um grupo de segurança de rede.  Os grupos de segurança de rede podem ser criados para as redes virtuais baseadas no Resource Manager, bem como para as redes virtuais clássicas.  exemplos de saudação abaixo mostram criando e configurando um NSG em uma rede virtual clássica usando o Powershell.

Para a arquitetura de exemplo hello, ambientes Olá estão localizados no Centro Sul dos EUA, então um NSG vazio é criado nessa região:

    New-AzureNetworkSecurityGroup -Name "RestrictBackendApi" -Location "South Central US" -Label "Only allow web frontend and loopback traffic"

Primeiro explícito permitir regra será adicionada para a infraestrutura de gerenciamento do Azure Olá descrita no artigo Olá em [o tráfego de entrada] [ InboundTraffic] para ambientes de serviço de aplicativo.

    #Open ports for access by Azure management infrastructure
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET' -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP

Em seguida, duas regras são adicionadas tooallow HTTP e HTTPS chamadas de Olá primeiro upstream aplicativo ambiente de serviço ("fe1ase").

    #Grant access toorequests from hello first upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe1ase" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe1ase" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

Aprimorá e repetir para Olá segundo e terceiro upstream aplicativo ambientes de serviço ("fe2ase" e "fe3ase").

    #Grant access toorequests from hello second upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe2ase" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe2ase" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

    #Grant access toorequests from hello third upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe3ase" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe3ase" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

Por fim, conceda acesso toohello saído endereço IP do ambiente de serviço de aplicativo da API de back-end Olá para que ele possa chamar novamente para si mesmo.

    #Allow apps on hello apiase environment toocall back into itself
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP apiase" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS apiase" -Type Inbound -Priority 900 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

Nenhuma outra regra de segurança de rede necessário toobe configurado porque cada NSG tem um conjunto de regras padrão que bloqueiam o acesso de entrada de saudação da Internet por padrão.

lista completa de saudação de regras no grupo de segurança de rede Olá são mostrados abaixo.  Observe como Olá última regra, que é realçada, bloqueia o acesso de entrada de todos os chamadores que não sejam aqueles que têm acesso.

![Configuração do NSG][NSGConfiguration] 

Olá última etapa é tooapply Olá NSG toohello sub-rede contém hello "apiase" ambiente de serviço de aplicativo.  

     #Apply hello NSG toohello backend API subnet
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'yourvnetnamehere' -SubnetName 'API-ASE-Subnet'

Olá NSG aplicada toohello sub-rede, somente hello três ambientes de serviço de aplicativo upstream e Olá Olá recipiente do ambiente de serviço de aplicativo API back-end, são permitidas toocall no ambiente de "apiase" hello.

## <a name="additional-links-and-information"></a>Informações e links adicionais
Todos os artigos e como-para para ambientes de serviço de aplicativo estão disponíveis no hello [Leiame para ambientes de serviço de aplicativo](../app-service/app-service-app-service-environments-readme.md).

Informações sobre [grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md). 

Noções básicas sobre [endereços IP de saída][NetworkArchitecture] e Ambientes do Serviço de Aplicativo.

[Portas de rede][InboundTraffic] usadas pelos Ambientes do Serviço de Aplicativo.

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[NetworkArchitecture]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[InboundTraffic]:  https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-control-inbound-traffic/

<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-layered-security/ConceptualArchitecture-1.png
[NSGConfiguration]:  ./media/app-service-app-service-environment-layered-security/NSGConfiguration-1.png
