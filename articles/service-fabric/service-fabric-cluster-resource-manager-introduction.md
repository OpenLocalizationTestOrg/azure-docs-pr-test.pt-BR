---
title: "Olá aaaIntroducing Gerenciador de recursos de Cluster do serviço de malha | Microsoft Docs"
description: "Uma introdução toohello Gerenciador de recursos de Cluster do serviço de malha."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: cfab735b-923d-4246-a2a8-220d4f4e0c64
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: e815925880e2f3a755294de1dcfb9b88fbdde08a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-hello-service-fabric-cluster-resource-manager"></a>Introdução ao Gerenciador de recursos de cluster Olá Service Fabric
Tradicionalmente gerenciar sistemas de TI ou serviços on-line deve dedicar específico máquinas físicas ou virtuais toothose serviços específicos ou sistemas. Os serviços foram projetados como camadas. Deveria haver uma camada da "Web" e uma camada de "dados" ou "armazenamento". Aplicativos teria uma camada de mensagem onde solicitações de fluíram de entrada e saída, bem como um conjunto de toocaching dedicado de máquinas. Cada camada ou o tipo de carga de trabalho tinha tooit dedicado máquinas específicas: banco de dados de saudação tem duas máquinas tooit dedicado, servidores de web hello alguns. Se um tipo específico de carga de trabalho causada máquinas Olá que estava toorun excessivamente solicitado, você adicionou mais máquinas com essa mesma camada toothat configuração. No entanto, nem todas as cargas de trabalho podem ser dimensionadas tão facilmente - principalmente com a camada de dados hello, você normalmente deve substituir máquinas com máquinas maiores. Fácil. Se uma máquina falhar, essa parte da saudação geral aplicativo executado em menor capacidade até que a máquina Olá pode ser restaurada. Ainda assim, relativamente fácil (mesmo que não necessariamente divertido).

Agora, no entanto Olá mundo de serviço e arquitetura de software foi alterada. É mais comum que os aplicativos adotem um design de expansão. É comum criar aplicativos com contêineres ou microsserviços (ou ambos). Agora, enquanto você ainda pode ter apenas alguns computadores, eles não executam apenas uma única instância de uma carga de trabalho. Eles podem ainda estar em execução várias cargas de trabalho diferentes Olá simultaneamente. Agora, você tem dezenas de tipos de serviços diferentes (nenhum deles consumindo todos os recursos de um computador), talvez centenas de instâncias diferentes desses serviços. Cada instância nomeada tem uma ou mais instâncias ou réplicas para HA (Alta Disponibilidade). Dependendo de tamanhos de saudação essas cargas de trabalho e a disponibilidade, você pode encontrar-se com centenas ou milhares de máquinas. 

Não é tão simple como o gerenciamento de alguns tipos de toosingle dedicado de máquinas de cargas de trabalho, de repente, gerenciamento de seu ambiente. Os servidores são virtuais e não mais nomes (troca pensamentos de [toocattle de animais de estimação](http://www.slideshare.net/randybias/architectures-for-open-and-scalable-clouds/20) depois que todos os). A configuração é menor sobre máquinas hello e muito mais sobre serviços de saudação. Hardware dedicado tooa única instância de uma carga de trabalho é basicamente uma saudação anterior. Os próprios serviços tornaram-se pequenos sistemas distribuídos que abrangem várias partes menores do hardware de mercadoria.

Como seu aplicativo não é uma série de monolitos se espalham por várias camadas, agora você tem muitos mais toodeal de combinações com. Quem decide quais tipos de carga de trabalho podem ser executados em qual hardware, ou quantos? Quais cargas de trabalho funcionam bem em Olá mesmo hardware e que entram em conflito? Quando um computador fica inoperante, como você sabe o que estava em execução nesse computador? Quem é o responsável por garantir que a carga de trabalho comece a execução novamente? Aguarde Olá máquinas (virtuais)? toocome de volta ou suas cargas de trabalho automaticamente o failover tooother máquinas e manter em execução? Há necessidade de intervenção humana? E quanto às atualizações nesse ambiente?

Como os desenvolvedores e operadores lidar nesse ambiente, vamos toowant ajuda Gerenciando essa complexidade. A contratação binge e tentar a complexidade de saudação toohide com pessoas provavelmente não são resposta correta hello, então o que fazemos?

## <a name="introducing-orchestrators"></a>Introdução aos orquestradores
"Orchestrator" é o termo geral Olá uma parte do software que ajuda os administradores a gerenciar esses tipos de ambientes. Orchestrators são componentes de saudação que fazem solicitações como "Gostaria cinco cópias desse serviço em execução no meu ambiente". Eles tentarão toomake Olá correspondência Olá desejado estado do ambiente, não importa o que acontece.

Os orquestradores (não humanos) são os que entram em ação quando um computador falha ou quando uma carga de trabalho é encerrada por algum motivo inesperado. A maioria dos orquestradores faz mais do que apenas lidar com falhas. Outros recursos que eles oferecem são o gerenciamento de novas implantações, a manipulação de atualizações e o tratamento do consumo e da governança de recursos. Todos os orchestrators são basicamente sobre como manter algum estado desejado da configuração no ambiente de saudação. Você deseja toobe capaz de tootell um orquestrador que você deseja e fazer com que ele Olá pesada. Aurora sobre Mesos, Docker Datacenter/Docker Swarm, Kubernetes e Service Fabric são exemplos de orquestradores. Essas orchestrators estão sendo ativamente desenvolvido toomeet Olá necessidades de cargas de trabalho reais em ambientes de produção. 

## <a name="orchestration-as-a-service"></a>Orquestração como um serviço
Olá Gerenciador de recursos de Cluster é o componente do sistema de saudação que manipula a orquestração na malha do serviço. trabalho do Gerenciador de recursos do Cluster Olá é dividido em três partes:

1. Imposição de regras
2. Otimização do seu ambiente
3. Ajudando com outros processos

toosee como Olá Gerenciador de recursos de Cluster funciona, assista Olá vídeo Microsoft Virtual Academy a seguir:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=d4tka66yC_5706218965">
<img src="./media/service-fabric-cluster-resource-manager-introduction/ConceptsAndDemoVid.png" WIDTH="360" HEIGHT="244">
</a></center>

### <a name="what-it-isnt"></a>O que não é
Em aplicativos tradicionais de N camadas, sempre há um [Balanceador de Carga](https://en.wikipedia.org/wiki/Load_balancing_(computing)). Geralmente, isso era um balanceador de carga de rede (NLB) ou o balanceador de carga um aplicativo (ALB) dependendo de onde ele permaneceu na pilha de rede hello. Alguns balanceadores de carga se baseiam em Hardware, como a oferta BigIP da F5 e outros em software, como o NLB da Microsoft. Em outros ambientes, você poderá ver algo como HAProxy, nginx, Istio ou Envoy nessa função. Essas arquiteturas, trabalho Olá de balanceamento de carga é tooensure cargas de trabalho sem monitoração de estado (aproximadamente) recebem Olá mesma quantidade de trabalho. As estratégias de balanceamento de carga variavam. Alguns balanceadores poderia enviar cada servidor diferente de tooa chamada diferente. Outros forneciam fixação/adesão à sessão. Balanceadores mais avançados usam estimativa de carga real ou relatório tooroute uma chamada com base em seu custo esperado e o carregamento de máquina atual.

Balanceadores de rede ou mensagem roteadores tentados tooensure Olá da camada da web/de trabalho permanece aproximadamente equilibrada. Estratégias para balanceamento de camada de dados Olá eram diferentes e dependência no mecanismo de armazenamento de dados de saudação. Balanceamento de camada de dados Olá dependia fragmentação de dados, cache, gerenciadas exibições, procedimentos armazenados e outros mecanismos de armazenamento específico.

Embora algumas dessas estratégias são interessantes, Olá Gerenciador de recursos de Cluster do serviço de malha não é nada como um balanceador de carga de rede ou um cache. Um balanceador de carga de rede equilibra front-ends, distribuindo o tráfego entre eles. Olá Gerenciador de recursos de Cluster do serviço de malha possui uma estratégia diferente. Essencialmente, o Service Fabric move *serviços* toowhere façam hello mais sentido, esperando o tráfego ou toofollow de carga. Por exemplo, ele pode mover toonodes de serviços que estão atualmente frios porque os serviços de saudação que existem não estão fazendo a quantidade de trabalho. nós Olá podem ser frios como serviços Olá que estavam presentes foram excluídos ou movidos em outro lugar. Como outro exemplo, Olá Gerenciador de recursos de Cluster também pode mover um serviço de uma máquina. Talvez Olá máquina é sobre toobe atualizado ou sobrecarregada devido tooa aumento no consumo por serviços Olá em execução. Alernatively, talvez tenha aumentado os requisitos de recursos do serviço de saudação. Como resultado, existem recursos suficientes neste toocontinue máquina executá-lo. 

Como Olá Gerenciador de recursos de Cluster é responsável por mover serviços ao redor, ele contém um toowhat de conjunto em comparação comparado diferentes recursos encontrados em um balanceador de carga de rede. Isso é porque os balanceadores de carga de rede fornecem toowhere de tráfego de rede, serviços já estão, mesmo se esse local não é ideal para executar o próprio serviço de saudação. Olá Gerenciador de recursos de Cluster do serviço de malha emprega fundamentalmente diferentes estratégias para garantir que os recursos de saudação em cluster Olá são utilizados com eficiência.

## <a name="next-steps"></a>Próximas etapas
- Para obter informações sobre o fluxo de informações e arquitetura de hello dentro Olá Gerenciador de recursos de Cluster, check-out [neste artigo](service-fabric-cluster-resource-manager-architecture.md)
- Olá Gerenciador de recursos de Cluster tem muitas opções para descrever o cluster hello. toofind mais informações sobre métricas, leia este artigo em [que descreve um cluster do Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)
- Para obter mais informações sobre a configuração de serviços, [Saiba mais sobre como configurar serviços](service-fabric-cluster-resource-manager-configure-services.md)(service-fabric-cluster-resource-manager-configure-services.md)
- Métricas são como Olá Gerenciador de recursos de Cluster do serviço de malha gerencia capacidade em cluster hello e consumo. mais sobre as métricas e como tooconfigure-os check-out de toolearn [neste artigo](service-fabric-cluster-resource-manager-metrics.md)
- Olá Gerenciador de recursos de Cluster funciona com os recursos de gerenciamento do Service Fabric. ler toofind mais informações sobre essa integração, [neste artigo](service-fabric-cluster-resource-manager-management-integration.md)
- toofind out sobre como Olá Gerenciador de recursos de Cluster gerencia e equilibra a carga no cluster hello, check-out artigo Olá em [balanceamento de carga](service-fabric-cluster-resource-manager-balancing.md)
