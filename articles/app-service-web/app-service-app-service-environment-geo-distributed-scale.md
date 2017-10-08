---
title: "aaaGeo escala Distributed com ambientes de serviço de aplicativo"
description: "Saiba como toohorizontally dimensionar aplicativos usando a distribuição geográfica com o Gerenciador de tráfego e ambientes de serviço de aplicativo."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: c1b05ca8-3703-4d87-a9ae-819d741787fb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: stefsch
ms.openlocfilehash: 9b441f637d8b7f679b3d83240baf99b8ee57e8f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="geo-distributed-scale-with-app-service-environments"></a>Escala distribuída geograficamente com ambientes de Serviço de Aplicativo
## <a name="overview"></a>Visão geral
Cenários de aplicativos que exigem muito alta escala podem exceder Olá computação capacidade disponível tooa única implantação de recursos de um aplicativo.  Aplicativos de votação, eventos esportivos e de entretenimento televisionados são exemplos de cenários que exigem escala extremamente alta. Requisitos de alta escala podem ser atendidos pela expansão horizontal aplicativos, com várias implantações de aplicativo que está sendo feitas dentro de uma única região, bem como entre regiões, toohandle requisitos de carga extrema.

Ambientes de Serviço de Aplicativo são uma plataforma ideal para escalar horizontalmente.  Depois que uma configuração de ambiente de serviço de aplicativo foi selecionada que pode dar suporte a uma taxa de solicitação conhecido, os desenvolvedores podem implantar os ambientes de serviço de aplicativo adicionais na forma de "cortador" tooattain uma capacidade de carga de pico desejado.

Por exemplo, suponha que um aplicativo em execução em uma configuração de ambiente de serviço de aplicativo foi testado toohandle 20 mil solicitações por segundo (RPS).  Se a carga de pico desejado Olá capacidade é de 100 mil RPS, ambientes de serviço de aplicativo cinco (5) podem ser criados e tooensure configurado Olá aplicativo pode lidar com a carga de projetada máximo hello.

Desde que os clientes normalmente usando um domínio personalizado (ou banido), os desenvolvedores de aplicativos de acessar um aplicativo de toodistribute de maneira solicitações em todas as instâncias do ambiente de serviço de aplicativo hello.  Tooaccomplish uma ótima maneira que isso é tooresolve Olá domínio personalizado usando um [perfil do Azure Traffic Manager][AzureTrafficManagerProfile].  Olá Traffic Manager perfil pode ser configurado toopoint todos Olá ambientes de serviço de aplicativo individuais.  Gerenciador de tráfego manipula automaticamente a distribuição de clientes em todos os Olá que ambientes de serviço de aplicativo com base em configurações no perfil do Traffic Manager Olá de balanceamento de carga de saudação.  Essa abordagem funciona independentemente de todos os ambientes de serviço de aplicativo hello são implantados em uma única região do Azure, ou em todo o mundo implantados em várias regiões do Azure.

Além disso, desde que os clientes acessar aplicativos por meio do domínio banido de saudação, os clientes são não sabe nada sobre o número de saudação de ambientes de serviço de aplicativo, um aplicativo em execução.  Sendo assim, os desenvolvedores podem adicionar e remover Ambientes de Serviço de Aplicativo rápida e facilmente baseados na carga de tráfego observada.

diagrama conceitual de saudação abaixo mostra um aplicativo expandido horizontalmente em três ambientes de serviço de aplicativo dentro de uma única região.

![Arquitetura conceitual][ConceptualArchitecture] 

restante deste tópico Olá passo Olá envolvidos com a configuração de uma topologia distribuída para o aplicativo de exemplo hello usando vários ambientes de serviço de aplicativo.

## <a name="planning-hello-topology"></a>Olá planejamento topologia
Antes da criação de um volume de aplicativo distribuído, ele ajuda toohave algumas informações de partes antecipadamente.

* **Domínio personalizado para o aplicativo hello:** o que é o nome de domínio personalizado de saudação que os clientes usarão tooaccess Olá aplicativo?  Para o domínio personalizado do hello exemplo aplicativo hello nome é *www.scalableasedemo.com*
* **Domínio do Traffic Manager:** um nome de domínio precisa toobe escolhida ao criar um [perfil do Azure Traffic Manager][AzureTrafficManagerProfile].  Esse nome será combinado com hello *trafficmanager.net* sufixo tooregister uma entrada de domínio que é gerenciada pelo Gerenciador de tráfego.  Para o aplicativo de exemplo hello, é escolhido de nome hello *demonstração escalonável ase*.  Como resultado é o nome de domínio completo Olá que é gerenciado pelo Gerenciador de tráfego *demo.trafficmanager.net escalonável ase*.
* **Estratégia para expandir o volume de aplicativo hello:** superfície do aplicativo hello será distribuído em vários ambientes de serviço de aplicativo em uma única região?  Várias regiões?  Uma combinação de ambas as abordagens?  decisão de saudação deve ser baseada em expectativas de onde o tráfego de cliente serão originadas, bem como rest Olá bem da infraestrutura de back-end de suporte de um aplicativo pode ser dimensionado.  Por exemplo, com um aplicativo 100% sem monitoração de estado, ele pode ser altamente dimensionado usando uma combinação de vários Ambientes de Serviço de Aplicativo por região do Azure, multiplicado por Ambientes de Serviço de Aplicativo implantado em várias regiões do Azure.  Com 15 + pública regiões do Azure toochoose disponíveis do, os clientes podem realmente criar uma superfície de aplicativo do hyper-escala em todo o mundo.  Para o aplicativo de exemplo hello usado para este artigo, três ambientes de serviço de aplicativo foram criados em uma única região do Azure (Centro Sul dos EUA).
* **Convenção de nomenclatura para Olá ambientes de serviço de aplicativo:** cada ambiente de serviço de aplicativo requer um nome exclusivo.  Além de um ou dois ambientes de serviço de aplicativo é útil toohave uma convenção de nomenclatura toohelp identificar cada ambiente de serviço de aplicativo.  Para o aplicativo de exemplo hello uma convenção de nomenclatura simple foi usada.  Olá nomes de saudação três ambientes de serviço de aplicativo são *fe1ase*, *fe2ase*, e *fe3ase*.
* **Convenção de nomenclatura para aplicativos Olá:** como várias instâncias do aplicativo hello serão implantadas, é necessário um nome para cada instância do aplicativo hello implantado.  Um recurso muito conveniente, mas pouco conhecidos de ambientes de serviço de aplicativo é que hello mesmo nome de aplicativo pode ser usado em vários ambientes de serviço de aplicativo.  Como cada ambiente de serviço de aplicativo tem um sufixo de domínio exclusivo, os desenvolvedores podem optar usar toore Olá exatamente o mesmo aplicativo nome em cada ambiente.  Por exemplo um desenvolvedor poderia ter aplicativos nomeados da seguinte forma: *myapp.foo1.p.azurewebsites.net*, *myapp.foo2.p.azurewebsites.net*, *myapp.foo3.p.azurewebsites.net* etc.  Para o aplicativo de exemplo hello Embora cada instância do aplicativo também tem um nome exclusivo.  Olá nomes de instância de aplicativo usados são *webfrontend1*, *webfrontend2*, e *webfrontend3*.

## <a name="setting-up-hello-traffic-manager-profile"></a>Configurando Olá perfil do Traffic Manager
Quando várias instâncias de um aplicativo são implantadas em vários ambientes de serviço de aplicativo, instâncias de aplicativos individuais Olá podem ser registradas com o Gerenciador de tráfego.  Para o aplicativo de exemplo hello um Gerenciador de tráfego de perfil é necessária para *demo.trafficmanager.net escalonável ase* que pode rotear as instâncias de aplicativo tooany de saudação seguir implantado os clientes:

* **webfrontend1.fe1ase.p.azurewebsites.NET:** uma instância do aplicativo de exemplo hello implantado em Olá primeiro ambiente de serviço de aplicativo.
* **webfrontend2.fe2ase.p.azurewebsites.NET:** uma instância do aplicativo de exemplo hello implantado em Olá segundo ambiente de serviço de aplicativo.
* **webfrontend3.fe3ase.p.azurewebsites.NET:** uma instância do aplicativo de exemplo hello implantado em Olá terceiro ambiente de serviço de aplicativo.

Olá tooregister de maneira mais fácil vários do serviço de aplicativo do Azure pontos de extremidade, todos executados no hello **mesmo** região do Azure, está com hello Powershell [suporte do Gerenciador de tráfego do Azure Resource Manager] [ ARMTrafficManager].  

Olá primeira etapa é toocreate um perfil do Gerenciador de tráfego do Azure.  Olá código a seguir mostra como o perfil de saudação foi criado para o aplicativo de exemplo hello:

    $profile = New-AzureTrafficManagerProfile –Name scalableasedemo -ResourceGroupName yourRGNameHere -TrafficRoutingMethod Weighted -RelativeDnsName scalable-ase-demo -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"

Observe como Olá *RelativeDnsName* parâmetro foi definido muito*demonstração escalonável ase*.  Isso é hello como o nome de domínio *demo.trafficmanager.net escalonável ase* é criado e associado a um perfil do Gerenciador de tráfego.

Olá *TrafficRoutingMethod* parâmetro define a política do Traffic Manager usará toodetermine como cliente toospread de carga em todos os pontos de extremidade disponíveis Olá de balanceamento de carga de saudação.  Em Olá Este exemplo *ponderado* método foi escolhido.  Isso resultará em solicitações de cliente que estão sendo distribuídas em todos os pontos de extremidade do aplicativo hello registrado com base nos níveis de importância relativa Olá associados a cada ponto de extremidade. 

Com o perfil de saudação criado, cada instância do aplicativo é adicionada toohello perfil como um ponto de extremidade do Azure nativo.  Olá código abaixo busca um aplicativo web de front-end de tooeach de referência e, em seguida, adiciona cada aplicativo como um ponto de extremidade do Gerenciador de tráfego por meio da saudação *TargetResourceId* parâmetro.

    $webapp1 = Get-AzureRMWebApp -Name webfrontend1
    Add-AzureTrafficManagerEndpointConfig –EndpointName webfrontend1 –TrafficManagerProfile $profile –Type AzureEndpoints -TargetResourceId $webapp1.Id –EndpointStatus Enabled –Weight 10

    $webapp2 = Get-AzureRMWebApp -Name webfrontend2
    Add-AzureTrafficManagerEndpointConfig –EndpointName webfrontend2 –TrafficManagerProfile $profile –Type AzureEndpoints -TargetResourceId $webapp2.Id –EndpointStatus Enabled –Weight 10

    $webapp3 = Get-AzureRMWebApp -Name webfrontend3
    Add-AzureTrafficManagerEndpointConfig –EndpointName webfrontend3 –TrafficManagerProfile $profile –Type AzureEndpoints -TargetResourceId $webapp3.Id –EndpointStatus Enabled –Weight 10

    Set-AzureTrafficManagerProfile –TrafficManagerProfile $profile

Observe como não há uma chamada muito*AzureTrafficManagerEndpointConfig adicionar* para cada instância de aplicativo individuais.  Olá *TargetResourceId* em cada comando Powershell faz referência a uma das três instâncias de aplicativo implantado hello.  Olá perfil do Traffic Manager distribuirão a carga entre todos os três pontos de extremidade registrados no perfil de saudação.

Todos Olá três pontos de extremidade usam Olá mesmo valor (10) para Olá *peso* parâmetro.  Isso faz com que o Gerenciador de Tráfego distribua as solicitações de cliente entre todas as três instâncias do aplicativo de forma quase igual. 

## <a name="pointing-hello-apps-custom-domain-at-hello-traffic-manager-domain"></a>Apontar um domínio personalizado de saudação do aplicativo no hello domínio do Traffic Manager
etapa final da saudação necessário é toopoint Olá domínio personalizado aplicativo hello no domínio do Traffic Manager hello.  Para o aplicativo de exemplo hello significa apontar *www.scalableasedemo.com* em *demo.trafficmanager.net escalonável ase*.  Esta etapa deve toobe concluída com o registrador de saudação que gerencia o domínio personalizado hello.  

Usando ferramentas de gerenciamento de domínio do seu registrador de domínio, um toobe de necessidades de registros CNAME quais pontos Olá domínio personalizado criado no domínio do Traffic Manager hello.  imagem de saudação abaixo mostra um exemplo de como essa configuração de CNAME aparece:

![CNAME para um domínio personalizado][CNAMEforCustomDomain] 

Embora não abordados neste tópico, lembre-se de que cada instância de aplicativo individuais precisa de domínio personalizado de saudação toohave registrado com ele também.  Caso contrário, se uma solicitação torna tooan instância de aplicativo, e o aplicativo hello não tem um domínio personalizado de Olá registrado com um aplicativo hello, solicitação Olá falhará.  

Olá Este exemplo domínio personalizado é *www.scalableasedemo.com*, e cada instância de aplicativo tem o domínio personalizado de saudação associado a ele.

![Domínio personalizado][CustomDomain] 

Para uma recapitulação de registro de um domínio personalizado com aplicativos de serviço de aplicativo do Azure, consulte Olá artigo a seguir [registrar domínios personalizados][RegisterCustomDomain].

## <a name="trying-out-hello-distributed-topology"></a>Experimentar Olá topologia distribuída
Olá resultado final da configuração de saudação do Traffic Manager e o DNS é que as solicitações de *www.scalableasedemo.com* fluirá pelo Olá sequência a seguir:

1. Um navegador ou dispositivo fará uma pesquisa de DNS para *www.scalableasedemo.com*
2. Olá entrada CNAME no registrador de domínio Olá faz com que Olá DNS pesquisa toobe redirecionado tooAzure Gerenciador de tráfego.
3. Uma pesquisa de DNS é feita *demo.trafficmanager.net escalonável ase* em relação a um dos servidores de DNS do Azure Traffic Manager hello.
4. Com base na política de balanceamento de carga de saudação (Olá *TrafficRoutingMethod* parâmetro usado anteriormente durante a criação de perfil do Gerenciador de tráfego de saudação), Gerenciador de tráfego será selecione um dos Olá configurado pontos de extremidade e retorna Olá FQDN do que dispositivo ou navegador de toohello do ponto de extremidade.
5. Como Olá FQDN do ponto de extremidade Olá Olá Url de uma instância de aplicativo em execução em um ambiente de serviço de aplicativo, hello dispositivo ou navegador solicitará um servidor DNS do Microsoft Azure tooresolve Olá endereço IP do FQDN tooan. 
6. dispositivo ou navegador Olá enviará o endereço IP do hello HTTP/S solicitação toohello.  
7. solicitação de saudação chegará em uma das instâncias de aplicativo hello em execução em uma saudação ambientes de serviço de aplicativo.

Olá, console figura abaixo mostra uma pesquisa de DNS domínio personalizado com êxito a resolução tooan aplicativo instância do aplicativo de exemplo hello em execução em um exemplo de hello três ambientes de serviço de aplicativo (neste caso Olá segundo de saudação três ambientes de serviço de aplicativo):

![Pesquisa de DNS][DNSLookup] 

## <a name="additional-links-and-information"></a>Informações e links adicionais
Todos os artigos e como-para para ambientes de serviço de aplicativo estão disponíveis no hello [Leiame para ambientes de serviço de aplicativo](../app-service/app-service-app-service-environments-readme.md).

Documentação sobre Olá Powershell [suporte do Gerenciador de tráfego do Azure Resource Manager][ARMTrafficManager].  

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[AzureTrafficManagerProfile]: ../traffic-manager/traffic-manager-manage-profiles.md
[ARMTrafficManager]: ../traffic-manager/traffic-manager-powershell-arm.md
[RegisterCustomDomain]: app-service-web-tutorial-custom-domain.md


<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-geo-distributed-scale/ConceptualArchitecture-1.png
[CNAMEforCustomDomain]:  ./media/app-service-app-service-environment-geo-distributed-scale/CNAMECustomDomain-1.png
[DNSLookup]:  ./media/app-service-app-service-environment-geo-distributed-scale/DNSLookup-1.png
[CustomDomain]:  ./media/app-service-app-service-environment-geo-distributed-scale/CustomDomain-1.png 
