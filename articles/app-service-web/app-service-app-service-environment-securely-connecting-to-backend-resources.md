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
# <a name="securely-connecting-toobackend-resources-from-an-app-service-environment"></a>TooBackend de conectar-se com segurança os recursos de um ambiente de serviço de aplicativo
## <a name="overview"></a>Visão geral
Como um ambiente de serviço de aplicativo é sempre criado no **ou** uma rede virtual do Azure Resource Manager, **ou** um modelo de implantação clássico [rede virtual] [ virtualnetwork], conexões de saída dos recursos de back-end de tooother ambiente de serviço de aplicativo podem fluir exclusivamente em rede virtual hello.  Com uma alteração recente feita em junho de 2016, os ASEs agora podem ser implantados nas redes virtuais que usam os intervalos de endereço público ou espaços de endereço RFC1918 (ou seja, endereços privados).  

Por exemplo, pode haver um SQL Server em execução em um cluster de máquinas virtuais com a porta 1433 bloqueada.  ponto de extremidade de saudação pode ser ACLd tooonly permitir o acesso de outros recursos na mesma rede virtual de hello.  

Como outro exemplo, pontos de extremidade confidenciais podem executados no local e ser tooAzure conectado através de um [Site a Site] [ SiteToSite] ou [Azure ExpressRoute] [ ExpressRoute] conexões.  Como resultado, somente os recursos em redes virtuais conectadas toohello Site a Site ou rota expressa túneis será tooaccess capaz de pontos de extremidade de local.

Para todos esses cenários, aplicativos executados em um ambiente de serviço de aplicativo ser capaz de toosecurely conectará toohello vários servidores e recursos.  Tráfego de saída de aplicativos executados em um ambiente de serviço de aplicativo tooprivate os pontos de extremidade no hello mesma rede virtual (ou conectado toohello mesma rede virtual), será apenas fluxo de rede virtual hello.  O tráfego de saída tooprivate pontos de extremidade de não fluirá sobre Olá Internet pública.

Uma limitação se aplica a tráfego de toooutbound de tooendpoints um ambiente de serviço de aplicativo em uma rede virtual.  Ambientes de serviço de aplicativo não pode acessar pontos de extremidade das máquinas virtuais localizadas em Olá **mesmo** sub-rede como Olá ambiente de serviço de aplicativo.  Isso normalmente não deveria um problema como ambientes de serviço de aplicativo são implantados em uma sub-rede reservada para uso exclusivo por Olá ambiente de serviço de aplicativo.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a>Requisitos de DNS e conectividade de saída
Para um ambiente de serviço de aplicativo toofunction corretamente, ele exige pontos de extremidade de toovarious de acesso de saída. É uma lista completa dos pontos de extremidade externos Olá usado por uma ASE em Olá seção "Conectividade de rede necessária" hello [configuração de rede para a rota expressa](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) artigo.

Ambientes de serviço de aplicativo exigem uma infraestrutura DNS válida configurada para a rede virtual hello.  Se para qualquer Olá motivo a configuração do DNS é alterada após ter sido criado um ambiente de serviço de aplicativo, os desenvolvedores podem forçar o toopick um ambiente de serviço de aplicativo nova configuração de DNS Olá.  Disparar uma reinicialização sem interrupção de ambiente usando hello "Reiniciar" localizado na parte superior de saudação do hello ambiente de serviço de aplicativo folha de gerenciamento no portal de saudação fará com que Olá ambiente toopick a nova configuração de DNS hello.

Também é recomendável que todos os servidores DNS personalizados Olá vnet ser configurado antes do tempo anterior toocreating um ambiente de serviço de aplicativo.  Se a configuração do DNS da rede virtual for alterada enquanto um ambiente de serviço de aplicativo está sendo criado, que resultará em falha de processo de criação de ambiente de serviço de aplicativo hello.  Do mesmo modo, se um servidor DNS personalizado existir no hello outra extremidade de um gateway de VPN e o servidor DNS Olá é Olá inacessível ou não estiver disponível, ambiente de serviço de aplicativo, o processo de criação também falharão.

## <a name="connecting-tooa-sql-server"></a>Conectar-se tooa do SQL Server
Uma configuração comum do SQL Server tem um ponto de extremidade escutando na porta 1433:

![Ponto de extremidade do SQL Server][SqlServerEndpoint]

Há duas abordagens para restringir o ponto de extremidade do tráfego toothis:

* [Listas de controle de acesso a redes][NetworkAccessControlLists] (ACLs de rede)
* [Grupos de segurança de rede][NetworkSecurityGroups]

## <a name="restricting-access-with-a-network-acl"></a>Restringindo o acesso com uma ACL de rede
A porta 1433 pode ser protegida usando uma lista de controle de acesso de rede.  exemplo Hello abaixo brancas cliente endereços provenientes de dentro de uma rede virtual e bloqueia o acesso tooall outros clientes.

![Exemplo de lista de controle de acesso de rede][NetworkAccessControlListExample]

Todos os aplicativos em execução no ambiente de serviço de aplicativo no hello mesma rede virtual como saudação do SQL Server será capaz de tooconnect instância de SQL Server de toohello usando Olá **VNet interno** endereço IP da máquina de virtual saudação do SQL Server.  

cadeia de conexão de exemplo Hello abaixo referências Olá SQL Server usando seu endereço IP privado.

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

Embora a máquina virtual de saudação tem um ponto de extremidade público, as tentativas de conexão usando o endereço IP público de saudação serão rejeitadas devido a ACL de rede hello. 

## <a name="restricting-access-with-a-network-security-group"></a>Restringindo o acesso com um grupo de segurança de rede
Uma abordagem alternativa para proteger o acesso é com um grupo de segurança de rede.  Grupos de segurança de rede podem ser aplicado tooindividual VMs ou sub-rede tooa que contêm máquinas virtuais.

Primeiro, um grupo de segurança de rede precisa toobe criado:

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

Restringir acesso tooonly tráfego interno da rede virtual é muito simple com um grupo de segurança de rede.  regras do saudação padrão em um grupo de segurança de rede somente permitem o acesso de outros clientes de rede em Olá mesma rede virtual.

Como resultado, bloqueando acesso tooSQL servidor é tão simple quanto a aplicação de um grupo de segurança de rede com seus padrão regras tooeither Olá máquinas virtuais que executam o SQL Server ou sub-rede Olá que contêm máquinas virtuais de saudação.

exemplo Hello abaixo se aplica a uma sub-rede que contém toohello de grupo rede segurança:

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

resultado final de saudação é um conjunto de regras de segurança que bloqueiam o acesso externo, permitindo o acesso de rede virtual interno:

![Regras de segurança de rede padrão][DefaultNetworkSecurityRules]

## <a name="getting-started"></a>Introdução
Todos os artigos e como-para para ambientes de serviço de aplicativo estão disponíveis no hello [Leiame para ambientes de serviço de aplicativo](../app-service/app-service-app-service-environments-readme.md).

tooget iniciado com ambientes de serviço de aplicativo, consulte [Introdução tooApp ambiente de serviço][IntroToAppServiceEnvironment]

Para obter detalhes sobre o ambiente de serviço de aplicativo tooyour de controlar o tráfego de entrada, consulte [controlando o tráfego de entrada tooan ambiente de serviço de aplicativo][ControlInboundASE]

Para obter mais informações sobre a plataforma do serviço de aplicativo do Azure hello, consulte [do serviço de aplicativo do Azure][AzureAppService].

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
