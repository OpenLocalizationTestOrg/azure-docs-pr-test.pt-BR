---
title: "aaaNetwork detalhes de configuração para trabalhar com a rota expressa"
description: "Detalhes de configuração de rede para executar os ambientes de serviço de aplicativo em uma rede Virtual conectado tooan circuito de rota expressa."
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 34b49178-2595-4d32-9b41-110c96dde6bf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/14/2016
ms.author: stefsch
ms.openlocfilehash: 85bbc45cfed619485957ee2a898aa0a7604173cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="network-configuration-details-for-app-service-environments-with-expressroute"></a>Detalhes da configuração de rede para Ambientes de Serviço de Aplicativo com o ExpressRoute
## <a name="overview"></a>Visão geral
Os clientes podem conectar um [Azure ExpressRoute] [ ExpressRoute] infraestrutura de rede virtual tootheir circuito, estendendo assim seu tooAzure de rede local.  Um Ambiente de Serviço de Aplicativo pode ser criado em uma sub-rede dessa infraestrutura de [rede virtual][virtualnetwork].  Aplicativos executados em Olá ambiente de serviço de aplicativo, em seguida, podem estabelecer conexões seguras tooback ponta recursos acessíveis somente através de saudação conexão de rota expressa.  

Um Ambiente de Serviço de Aplicativo pode ser criado **tanto** em uma rede virtual do Azure Resource Manager **quanto** em uma rede virtual de modelo de implantação clássico.  Com uma alteração recente feita em junho de 2016, os ASEs agora também podem ser implantados nas redes virtuais que usam os intervalos de endereço público ou espaços de endereço RFC1918 (ou seja, endereços privados). 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="required-network-connectivity"></a>Conectividade de rede necessária
Há requisitos de conectividade de rede para os ambientes de serviço de aplicativo não pode ser atendido inicialmente em uma rede virtual conectado de tooan rota expressa.  Ambientes de serviço de aplicativo exigem Olá seguinte na ordem toofunction corretamente:

* Rede de saída conectividade tooAzure armazenamento pontos de extremidade em todo o mundo em ambas as portas 80 e 443.  Isso inclui os pontos de extremidade localizados em Olá mesma região Olá ambiente de serviço de aplicativo, bem como pontos de extremidade de armazenamento localizados na **outros** regiões do Azure.  Pontos de extremidade de armazenamento do Azure resolver em Olá domínios DNS a seguir: *n e t*, *>.blob.Core.Windows.NET*, *queue.core.windows.net* e *file.core.windows.net*.  
* Conectividade de rede de saída toohello serviço de arquivos do Azure na porta 445.
* Pontos de extremidade de tooSql banco de dados de conectividade rede de saída localizada no hello mesmo região como Olá ambiente de serviço de aplicativo.  Pontos de extremidade do banco de dados SQL resolver em Olá domínio a seguir: *t*.  Isso requer a abertura de acesso tooports 1433, 11.000 a 11.999 e 14.000 a 14.999.  Para obter mais detalhes, consulte [este artigo sobre o uso de portas do banco de dados SQL V12](../sql-database/sql-database-develop-direct-route-ports-adonet-v12.md).
* Rede de saída conectividade toohello gerenciamento do Azure plano pontos de extremidade (pontos de extremidade ASM e ARM).  Isso inclui conectividade de saída tooboth *management.core.windows.net* e *management.azure.com*. 
* Saída conectividade de rede muito*ocsp.msocsp.com*, *mscrl.microsoft.com* e *crl.microsoft.com*.  Essa é uma funcionalidade SSL toosupport necessários.
* configuração de DNS Olá para rede virtual Olá deve ser capaz de resolver todos os pontos de extremidade hello e domínios mencionado na Olá pontos anteriores.  Se esses pontos de extremidade não puderem ser resolvidos, tentativas de criação do Ambiente de Serviço de Aplicativo irão falhar, e Ambientes de Serviços de Aplicativo existentes serão marcados como não íntegros.
* O acesso de saída na porta 53 é necessário para a comunicação com servidores DNS.
* Se um servidor DNS personalizado existir no Olá outra extremidade de um gateway VPN, servidor DNS Olá deve ser acessível da sub-rede Olá contendo Olá ambiente de serviço de aplicativo. 
* caminho de rede de saída de saudação não pode percorrer proxies corporativos internos, nem pode ser local tooon de túnel de força.  Se o fizer, alterações Olá endereço NAT efetivo do tráfego de rede de saída do hello ambiente de serviço de aplicativo.  Alterar o endereço NAT de saudação do tráfego de rede de saída de um ambiente serviço de aplicativo fará com que conectividade toomany falhas de pontos de extremidade Olá listado acima.  Isso resulta em tentativas de criação de Ambiente de Serviço de Aplicativo, e faz com que Ambientes de Serviços de Aplicativo anteriormente íntegros sejam marcados como não íntegros.  
* Portas de toorequired de acesso de rede de entrada para os ambientes de serviço de aplicativo devem ser permitidos, conforme descrito neste [artigo][requiredports].

requisitos de DNS Olá podem ser atendidos, garantindo uma infraestrutura DNS válida está configurada e mantida para rede virtual hello.  Se para qualquer Olá motivo a configuração do DNS é alterada após ter sido criado um ambiente de serviço de aplicativo, os desenvolvedores podem forçar o toopick um ambiente de serviço de aplicativo nova configuração de DNS Olá.  Disparar uma reinicialização sem interrupção de ambiente usando hello "Reiniciar" ícone localizado na parte superior de saudação da folha de gerenciamento do ambiente de serviço de aplicativo hello em Olá [portal do Azure] [ NewPortal] fará com que a saudação ambiente toopick a nova configuração de DNS hello.

Hello requisitos de acesso de rede de entrada podem ser atendidos ao configurar um [grupo de segurança de rede] [ NetworkSecurityGroups] no acesso do ambiente de serviço de aplicativo hello sub-rede tooallow Olá necessárias conforme descrito neste [artigo][requiredports].

## <a name="enabling-outbound-network-connectivity-for-an-app-service-environment"></a>Habilitando a conectividade de rede de saída para um Ambiente do Serviço de Aplicativo
Por padrão, um circuito do ExpressRoute recentemente criado anuncia uma rota padrão que permite conectividade de saída da Internet.  Com essa configuração de um ambiente de serviço de aplicativo será capaz de tooconnect tooother pontos de extremidade do Azure.

No entanto, uma configuração de cliente comum é toodefine seus próprios rota padrão (0.0.0.0/0), que força o fluxo de tooinstead de tráfego de saída da Internet local.  Este fluxo de tráfego invariavelmente quebras de ambientes de serviço de aplicativo porque o tráfego de saída hello está bloqueado no local ou NAT por conjunto de irreconhecível tooan de endereços que não funcionam com vários pontos de extremidade do Azure.

solução de saudação é toodefine uma (ou mais) definidos pelo usuário rotas (UDRs) sub-rede Olá que contém Olá ambiente de serviço de aplicativo.  Um UDR define as rotas de sub-rede que serão cumpridas em vez de rota padrão de saudação.

Se possível, é recomendável Olá toouse seguinte configuração:

* configuração de rota expressa Olá anuncia 0.0.0.0/0 e todo o tráfego de saída no local de túneis de força por padrão.
* Olá UDR aplicada toohello sub-rede contendo Olá ambiente de serviço de aplicativo define 0.0.0.0/0 com um tipo de próximo salto da Internet (um exemplo disso esteja no final deste artigo).

Olá efeito combinado dessas etapas é que o nível de sub-rede Olá UDR terá precedência sobre Olá ExpressRoute forçada de túneis, garantindo, assim, o acesso de Internet de saída de saudação ambiente de serviço de aplicativo.

> [!IMPORTANT]
> Olá rotas definidas em um UDR **deve** ser específica o suficiente muito têm precedência sobre todas as rotas anunciadas pelo Olá configuração de rota expressa.  exemplo Hello abaixo usa o intervalo de endereços do hello amplo 0.0.0.0/0 e como tal, pode potencialmente ser acidentalmente substituído pelos anúncios de rota usando intervalos de endereços mais específicos.
> 
> Não há suporte para ambientes de serviço de aplicativo com as configurações de rota expressa que **entre-anunciar rotas de saudação emparelhamento caminho toohello privada caminho emparelhamento público**.  As configurações de ExpressRoute com emparelhamento público definido receberão anúncios de rota da Microsoft para um grande conjunto de intervalos de endereços IP do Microsoft Azure.  Se esses intervalos de endereços entre anunciados no caminho de emparelhamento privado hello, o resultado de final de saudação é que todos os pacotes de saída de rede da sub-rede do ambiente de serviço de aplicativo hello serão infraestrutura de rede local do cliente tooa túnel de força.  Esse fluxo de rede não tem suporte no momento com os Ambientes de Serviço de Aplicativo.  Um problema de toothis de solução é toostop as rotas entre publicidade Olá emparelhamento caminho toohello privada caminho emparelhamento público.
> 
> 

Informações básicas sobre as rotas definidas pelo usuário estão disponíveis nesta [visão geral][UDROverview].  

Detalhes sobre como criar e configurar rotas definidas pelo usuário está disponível neste [como tooGuide][UDRHowTo].

## <a name="example-udr-configuration-for-an-app-service-environment"></a>Exemplo de configuração da UDR para um Ambiente do Serviço de Aplicativo
**Pré-requisitos**

1. Instale o Azure Powershell Olá [página Downloads do Azure] [ AzureDownloads] (datado de junho de 2015 ou posterior).  Em "Ferramentas de linha de comando" há um link de "Instalar" em "Windows Powershell", que irá instalar os cmdlets do Powershell mais recente hello.
2. É recomendável que uma sub-rede exclusiva seja criada para uso exclusivo por um Ambiente do Serviço de Aplicativo.  Isso garante que a sub-rede Olá UDRs aplicados toohello abrirá somente o tráfego de saída para Olá ambiente de serviço de aplicativo.
3. **Importante**: não implante Olá ambiente de serviço de aplicativo até **depois** Olá seguindo as etapas de configuração é seguida.  Isso garante que a conectividade de rede de saída está disponível antes de tentar toodeploy um ambiente de serviço de aplicativo.

**Etapa 1: Criar uma tabela de rotas nomeada**

Olá trecho a seguir cria uma tabela de rota chamada "DirectInternetRouteTable" na região do Azure do Oeste nos hello:

    New-AzureRouteTable -Name 'DirectInternetRouteTable' -Location uswest

**Etapa 2: Criar uma ou mais rotas na tabela de rotas Olá**

Você precisará tooadd uma ou mais rotas toohello rota tabela de acesso de saída à Internet ordem tooenable.  

Olá recomendado abordagem para configurar o acesso de saída toohello que Internet é toodefine uma rota para 0.0.0.0/0 conforme mostrado abaixo.

    Get-AzureRouteTable -Name 'DirectInternetRouteTable' | Set-AzureRoute -RouteName 'Direct Internet Range 0' -AddressPrefix 0.0.0.0/0 -NextHopType Internet

Lembre-se de que 0.0.0.0/0 é um intervalo de endereço amplo e assim será substituído por intervalos de endereços mais específicos anunciados pelo Olá rota expressa.  toore-iterar Olá recomendação anterior, um UDR com uma rota 0.0.0.0/0 deve ser usada em conjunto com uma configuração de ExressRoute que só informa 0.0.0.0/0 também. 

Como alternativa, você pode baixar uma lista abrangente e atualizada de intervalos CIDR em uso pelo Azure.  Olá arquivo Xml que contém todos os intervalos de endereços IP do Azure hello está disponível no hello [Microsoft Download Center][DownloadCenterAddressRanges].  

Embora Observe que alterar esses intervalos ao longo do tempo, assim a necessidade de atualizações manuais periódica toohello definidas pelo usuário rotas tookeep em sincronia.  Além disso, já que há um padrão superior toofit dentro do limite de rota Olá 100 intervalos de limite de 100 rotas em um único UDR, você precisa muito "resumirá" endereço de IP do Azure hello, tendo em mente que UDR rotas definidas necessário toobe mais específico que Olá rotas anunciadas pelo seu Rota expressa.  

**Etapa 3: Associar Olá rota tabela toohello sub-rede contendo Olá ambiente de serviço de aplicativo**

a última etapa de configuração Olá é tooassociate Olá rota tabela toohello subrede onde Olá ambiente de serviço de aplicativo será implantado.  Olá comando a seguir associa toohello de "DirectInternetRouteTable" hello "ASESubnet" que eventualmente conterá um ambiente de serviço de aplicativo.

    Set-AzureSubnetRouteTable -VirtualNetworkName 'YourVirtualNetworkNameHere' -SubnetName 'ASESubnet' -RouteTableName 'DirectInternetRouteTable'


**Etapa 4: Etapas finais**

Após a tabela de rotas Olá sub-rede associada toohello, ele é recomendado toofirst teste e confirmar Olá pretendido efeito.  Por exemplo, implantar uma máquina virtual na sub-rede hello e confirme se:

* Tooboth de tráfego de saída do Azure e pontos de extremidade do Azure não mencionado anteriormente neste artigo é **não** que fluem para baixo Olá circuito de rota expressa.  É muito importante tooverify esse comportamento, como se o tráfego de saída da sub-rede Olá ainda está sendo forçado encapsulado no local, a criação do ambiente de serviço de aplicativo sempre irá falhar. 
* Pesquisas DNS para pontos de extremidade Olá mencionado anteriormente todos resolvendo corretamente. 

Depois de saudação acima etapas são confirmados, você precisará toodelete Olá virtual machine porque sub-rede Olá precisa toobe "empty" em Olá Olá de tempo que o ambiente de serviço de aplicativo é criado.

Prossiga então com a criação de um Ambiente do Serviço de Aplicativo.

## <a name="getting-started"></a>Introdução
Todos os artigos e como-para para ambientes de serviço de aplicativo estão disponíveis no hello [Leiame para ambientes de serviço de aplicativo](../app-service/app-service-app-service-environments-readme.md).

tooget iniciado com ambientes de serviço de aplicativo, consulte [Introdução tooApp ambiente de serviço][IntroToAppServiceEnvironment]

Para obter mais informações sobre a plataforma do serviço de aplicativo do Azure hello, consulte [do serviço de aplicativo do Azure][AzureAppService].

<!-- LINKS -->
[virtualnetwork]: http://azure.microsoft.com/services/virtual-network/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[requiredports]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[NetworkSecurityGroups]: http://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[UDROverview]: http://azure.microsoft.com/documentation/articles/virtual-networks-udr-overview/
[UDRHowTo]: http://azure.microsoft.com/documentation/articles/virtual-networks-udr-how-to/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[AzureDownloads]: http://azure.microsoft.com/en-us/downloads/ 
[DownloadCenterAddressRanges]: http://www.microsoft.com/download/details.aspx?id=41653  
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[NewPortal]:  https://portal.azure.com


<!-- IMAGES -->
