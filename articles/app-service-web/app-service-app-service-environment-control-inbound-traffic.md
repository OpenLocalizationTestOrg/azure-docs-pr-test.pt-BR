---
title: "aaaHow tooControl o tráfego de entrada tooan ambiente de serviço de aplicativo"
description: "Saiba mais sobre como o tráfego tooan ambiente de serviço de aplicativo de entrada tooconfigure toocontrol de regras de segurança de rede."
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: 
ms.assetid: 4cc82439-8791-48a4-9485-de6d8e1d1a08
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: stefsch
ms.openlocfilehash: e7c6e6201db6a1ea77f7a2eee29a3b5445175495
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocontrol-inbound-traffic-tooan-app-service-environment"></a>Como o tráfego de entrada de tooControl tooan ambiente de serviço de aplicativo
## <a name="overview"></a>Visão geral
Um Ambiente de Serviço de Aplicativo pode ser criado **tanto** em uma rede virtual do Azure Resource Manager, **quanto** em uma [rede virtual][virtualnetwork] de modelo de implantação clássico.  Uma nova rede virtual e uma nova sub-rede podem ser definidos no momento de saudação que um ambiente de serviço de aplicativo é criado.  Como alternativa, um Ambiente de Serviço de Aplicativo pode ser criado em uma rede virtual e uma sub-rede existentes.  Com uma alteração recente feita em junho de 2016, os ASEs agora podem ser implantados nas redes virtuais que usam os intervalos de endereço público ou espaços de endereço RFC1918 (ou seja, endereços privados).  Para obter mais detalhes sobre a criação de um ambiente de serviço de aplicativo, consulte [como um ambiente de serviço de aplicativo de tooCreate][HowToCreateAnAppServiceEnvironment].

Um ambiente de serviço de aplicativo deve sempre ser criado em uma sub-rede porque uma sub-rede fornece um limite de rede que pode ser usado toolock para baixo tráfego de entrada por trás de upstream dispositivos e serviços, de forma que o tráfego HTTP e HTTPS só é aceito na específico upstream Endereços IP.

O tráfego de rede de entrada e saída em uma sub-rede é controlado usando um [grupo de segurança de rede][NetworkSecurityGroups]. Controlar o tráfego de entrada requer a criação de regras de segurança de rede em um grupo de segurança de rede e, em seguida, atribuir Olá rede segurança grupo Olá sub-rede contendo Olá ambiente de serviço de aplicativo.

Quando um grupo de segurança de rede é atribuído a sub-rede tooa, o tooapps de tráfego de entrada em Olá que ambiente de serviço de aplicativo é permitido/bloqueado com base em Olá permitir e negar as regras definidas no grupo de segurança de rede hello.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="inbound-network-ports-used-in-an-app-service-environment"></a>Portas de entrada de rede usadas em um Ambiente de Serviço de Aplicativo
Antes de bloquear o tráfego de rede com um grupo de segurança de rede, é importante tooknow Olá conjunto de portas de rede necessários e opcionais usadas por um ambiente de serviço de aplicativo.  Fechar acidentalmente portas toosome de tráfego pode resultar em perda de funcionalidade em um ambiente de serviço de aplicativo.

a seguir Olá é uma lista de portas usadas por um ambiente de serviço de aplicativo. Todas as portas são **TCP**, a menos que indicado o claramente contrário:

* 454: **Porta requerida** usada pela infraestrutura do Azure para gerenciamento e manutenção de Ambientes de Serviço de Aplicativo via SSL.  Não bloquear o tráfego pela porta toothis.  Essa porta é sempre associada toohello o VIP público de um ASE.
* 455: **Porta requerida** usada pela infraestrutura do Azure para gerenciamento e manutenção de Ambientes de Serviço de Aplicativo via SSL.  Não bloquear o tráfego pela porta toothis.  Essa porta é sempre associada toohello o VIP público de um ASE.
* 80: porta de entrada tooapps de tráfego HTTP em execução em planos de serviço de aplicativo em um ambiente de serviço de aplicativo padrão.  Em uma ASE ILB habilitado, essa porta é associada toohello ILB endereço Olá ASE.
* 443: porta de entrada tooapps de tráfego do SSL em execução em planos de serviço de aplicativo em um ambiente de serviço de aplicativo padrão.  Em uma ASE ILB habilitado, essa porta é associada toohello ILB endereço Olá ASE.
* 21: canal de controle para FTP.  Essa porta pode ser bloqueada com segurança se o FTP não está sendo usado.  Em uma ASE ILB habilitado, essa porta pode ser o endereço ILB de toohello associada para um ASE.
* 990: canal de controle para FTPS.  Essa porta poderá ser bloqueada com segurança se o FTPS não estiver sendo usado.  Em uma ASE ILB habilitado, essa porta pode ser o endereço ILB de toohello associada para um ASE.
* 10001-10020: canais de dados para FTP.  Como com o canal de controle hello, essas portas podem ser bloqueadas com segurança se FTP não está sendo usado.  Em uma ASE habilitado ILB, essa porta pode ser associado toohello do ASE endereço ILB.
* 4016: usado para depuração remota com o Visual Studio 2012.  Essa porta pode ser bloqueada com segurança se o recurso de saudação não está sendo usado.  Em uma ASE ILB habilitado, essa porta é associada toohello ILB endereço Olá ASE.
* 4018: usado para depuração remota com o Visual Studio 2013.  Essa porta pode ser bloqueada com segurança se o recurso de saudação não está sendo usado.  Em uma ASE ILB habilitado, essa porta é associada toohello ILB endereço Olá ASE.
* 4020: usado para depuração remota com o Visual Studio 2015.  Essa porta pode ser bloqueada com segurança se o recurso de saudação não está sendo usado.  Em uma ASE ILB habilitado, essa porta é associada toohello ILB endereço Olá ASE.

## <a name="outbound-connectivity-and-dns-requirements"></a>Requisitos de DNS e conectividade de saída
Para um ambiente de serviço de aplicativo toofunction corretamente, ele também requer acesso de saída toovarious pontos de extremidade. É uma lista completa dos pontos de extremidade externos Olá usado por uma ASE em Olá seção "Conectividade de rede necessária" hello [configuração de rede para a rota expressa](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) artigo.

Ambientes de serviço de aplicativo exigem uma infraestrutura DNS válida configurada para a rede virtual hello.  Se para qualquer Olá motivo a configuração do DNS é alterada após ter sido criado um ambiente de serviço de aplicativo, os desenvolvedores podem forçar o toopick um ambiente de serviço de aplicativo nova configuração de DNS Olá.  Disparar uma reinicialização sem interrupção de ambiente usando hello "Reiniciar" ícone localizado na parte superior de saudação da folha de gerenciamento do ambiente de serviço de aplicativo hello em Olá [portal do Azure] [ NewPortal] fará com que a saudação ambiente toopick a nova configuração de DNS hello.

Também é recomendável que todos os servidores DNS personalizados Olá vnet ser configurado antes do tempo anterior toocreating um ambiente de serviço de aplicativo.  Se a configuração do DNS da rede virtual for alterada enquanto um ambiente de serviço de aplicativo está sendo criado, que resultará em falha de processo de criação de ambiente de serviço de aplicativo hello.  Do mesmo modo, se um servidor DNS personalizado existir no hello outra extremidade de um gateway de VPN e o servidor DNS Olá é Olá inacessível ou não estiver disponível, ambiente de serviço de aplicativo, o processo de criação também falharão.

## <a name="creating-a-network-security-group"></a>Criando um grupo de segurança de rede
Para obter detalhes completos sobre como funcionam os grupos de segurança de rede, consulte a seguir Olá [informações][NetworkSecurityGroups].  exemplo de gerenciamento de serviços do Azure Hello abaixo ajustes na destaca dos grupos de segurança de rede, com um foco sobre como configurar e aplicar uma segurança grupo tooa sub-rede da rede que contém um ambiente de serviço de aplicativo.

**Observação:** grupos de segurança de rede podem ser configurados usando graficamente Olá [Portal do Azure](https://portal.azure.com) ou por meio do PowerShell do Azure.

Grupos de segurança de rede são criados pela primeira vez como uma entidade autônoma associada a uma assinatura. Como grupos de segurança de rede são criados em uma região do Azure, certifique-se que esse grupo de segurança de rede Olá é criado no hello mesmo região como Olá ambiente de serviço de aplicativo.

a seguir Olá demonstra a criação de um grupo de segurança de rede:

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

Depois de criar um grupo de segurança de rede, uma ou mais regras de segurança de rede são adicionadas tooit.  Como o conjunto de saudação de regras pode ser alterado ao longo do tempo, é recomendável toospace out Olá esquema de numeração usado para toomake de prioridades da regra regras adicionais tooinsert fácil ao longo do tempo.

exemplo Hello abaixo mostra uma regra que concede as portas de gerenciamento do acesso toohello necessárias por toomanage de infraestrutura do Azure Olá explicitamente e manter um ambiente de serviço de aplicativo.  Observe que todo o tráfego de gerenciamento atravessam SSL e protegido por certificados de cliente, portanto, embora Olá portas estão abertas ficam inacessíveis por qualquer entidade que não seja a infraestrutura de gerenciamento do Azure.

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP


Quando o bloqueio de acesso tooport 80 e 443 muito "Ocultar" um ambiente de serviço de aplicativo por trás de dispositivos upstream ou serviços, você precisará de endereço IP tooknow Olá upstream.  Por exemplo, se você estiver usando um firewall do aplicativo web (WAF), Olá WAF terá seu próprio endereço IP (ou endereços) que ele usa quando proxy tráfego tooa ambiente de serviço de aplicativo downstream.  Você precisará toouse esse endereço IP no hello *SourceAddressPrefix* parâmetro de uma regra de segurança de rede.

O exemplo hello abaixo, o tráfego de entrada de um determinado endereço IP upstream seja explicitamente permitido.  Olá endereço *1.2.3.4* é usado como um espaço reservado para o endereço IP de saudação de um WAF upstream.  Alterar Olá valor toomatch Olá endereço usado por seu dispositivo upstream ou o serviço.

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT HTTP" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT HTTPS" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

Se o suporte ao FTP for desejado, Olá seguindo as regras de pode ser usado como uma porta de controle do modelo toogrant acesso toohello FTP e portas de canal de dados.  Como o FTP é um protocolo com monitoração de estado, talvez não seja capaz de tooroute FTP tráfego por meio de um dispositivo de firewall ou proxy HTTP/HTTPS tradicional.  Nesse caso, você precisará Olá tooset *SourceAddressPrefix* valor diferente de tooa - por exemplo hello IP atender de desenvolvedor ou implantação de máquinas em qual FTP clientes estão sendo executado. 

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT FTPCtrl" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '21' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT FTPDataRange" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '10001-10020' -Protocol TCP

(**Observação:** intervalo de porta de canal de dados Olá pode ser alterados durante o período de visualização hello.)

Se a depuração remota com o Visual Studio for usado, Olá regras a seguir demonstram como acessar toogrant.  Há uma regra separada para cada versão do Visual Studio para a qual há suporte, já que cada versão usa uma porta diferente para a depuração remota.  Assim como acontece com acesso ao FTP, o tráfego de depuração remota pode não fluir corretamente por meio de um dispositivo de proxy ou WAF tradicional.  Olá *SourceAddressPrefix* em vez disso, pode definir toohello intervalo de endereços IP dos computadores de desenvolvedor executando o Visual Studio.

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT RemoteDebuggingVS2012" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '4016' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT RemoteDebuggingVS2013" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '4018' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT RemoteDebuggingVS2015" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '4020' -Protocol TCP

## <a name="assigning-a-network-security-group-tooa-subnet"></a>Atribuindo uma sub-rede de tooa do grupo de segurança de rede
Um grupo de segurança de rede tem uma regra de segurança padrão que nega acesso tooall o tráfego externo.  Olá o resultado da combinação de regras de segurança de rede Olá descritas acima e Olá bloqueando o tráfego de entrada de regra de segurança padrão, que apenas o tráfego de intervalos de endereço de origem associado a um *permitir* ação poderão tráfego de toosend tooapps em execução em um ambiente de serviço de aplicativo.

Depois que um grupo de segurança de rede é preenchido com as regras de segurança, ela deve toobe atribuído toohello sub-rede contendo Olá ambiente de serviço de aplicativo.  comando de atribuição Olá faz referência a ambos os nome de saudação da rede virtual hello, onde reside a saudação ambiente de serviço de aplicativo, bem como nome de saudação da sub-rede Olá onde Olá ambiente de serviço de aplicativo foi criado.  

exemplo Hello abaixo mostra um grupo de segurança de rede que está sendo atribuído tooa sub-rede e a rede virtual:

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-test'

Assim que tiver êxito de atribuição de grupo de segurança de rede hello (atribuição de saudação é as operações de longa execução e pode levar alguns toocomplete de minutos), apenas a correspondência de tráfego de entrada *permitir* regras com êxito alcançará aplicativos Olá aplicativo Ambiente de serviço.

Para Olá integridade o exemplo a seguir mostra como tooremove e, portanto, a segurança de rede Olá associar DIS agrupar da sub-rede hello:

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Remove-AzureNetworkSecurityGroupFromSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-test'

## <a name="special-considerations-for-explicit-ip-ssl"></a>Considerações especiais para IP-SSL explícito
Se um aplicativo está configurado com um endereço de IP SSL explícito (aplicável *somente* tooASEs que têm um VIP público), em vez de usar o endereço IP de padrão de saudação do hello ambiente de serviço de aplicativo, HTTP e HTTPS tráfego na sub-rede Olá em um conjunto diferente de portas diferentes portas 80 e 443.

par de saudação individual de portas usadas por cada endereço IP SSL pode ser encontrado na interface de usuário do portal Olá da folha UX detalhes do ambiente de serviço de aplicativo hello.  Selecione "Todas as configurações"--> "Endereços IP".  folha Hello "endereços IP" mostra uma tabela de todos os endereços IP SSL configurados explicitamente para Olá ambiente de serviço de aplicativo, junto com o par de porta especial de saudação tooroute usado tráfego HTTP e HTTPS associado com cada endereço IP SSL.  É esse par de porta que precisa toobe usado para parâmetros de DestinationPortRange Olá ao configurar as regras em um grupo de segurança de rede.

Quando um aplicativo em uma ASE é configurado toouse SSL de IP, clientes externos não verão e não é necessário tooworry sobre o mapeamento de par Olá porta especial.  Aplicativos de toohello tráfego fluirá normalmente endereço de IP SSL toohello configurado.  par de porta especial Olá tradução toohello automaticamente acontece internamente durante segmento final de saudação do roteamento de tráfego em Olá recipiente de sub-rede de Olá ASE. 

## <a name="getting-started"></a>Introdução
tooget iniciado com ambientes de serviço de aplicativo, consulte [Introdução tooApp ambiente de serviço][IntroToAppServiceEnvironment]

Todos os artigos e como-para para ambientes de serviço de aplicativo estão disponíveis no hello [Leiame para ambientes de serviço de aplicativo](../app-service/app-service-app-service-environments-readme.md).

Para obter detalhes sobre aplicativos toobackend recurso uma conexão segura de um ambiente de serviço de aplicativo, consulte [tooBackend recursos uma conexão segura de um ambiente de serviço de aplicativo][SecurelyConnecttoBackend]

Para obter mais informações sobre a plataforma do serviço de aplicativo do Azure hello, consulte [do serviço de aplicativo do Azure][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[SecurelyConnecttoBackend]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-securely-connecting-to-backend-resources/
[NewPortal]:  https://portal.azure.com  

<!-- IMAGES -->

