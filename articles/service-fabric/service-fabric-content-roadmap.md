---
title: aaaLearn mais sobre o Azure Service Fabric | Microsoft Docs
description: "Saiba mais sobre conceitos básicos de saudação e as áreas principais do Azure Service Fabric. Fornece uma visão geral do Service Fabric estendida e como toocreate microservices."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/14/2017
ms.author: ryanwi
ms.openlocfilehash: 7fe8de777755be11635912613bb5b970e3fe3ea3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="so-you-want-toolearn-about-service-fabric"></a>Portanto, você deseja toolearn sobre a malha do serviço?
Malha do serviço do Azure é uma plataforma de sistemas distribuídos que torna mais fácil toopackage, implantar e gerenciar microservices escalonável e confiável.  No entanto, o Service Fabric tem uma área de superfície grande, e há muito toolearn.  Este artigo fornece um resumo da malha do serviço e descreve os conceitos fundamentais hello, modelos de ciclo de vida do aplicativo, teste, clusters e monitoramento de integridade de programação. Saudação de leitura [visão geral](service-fabric-overview.md) e [quais são microservices?](service-fabric-overview-microservices.md) para obter uma introdução e como o Service Fabric podem ser usados toocreate microservices. Este artigo não contém uma lista abrangente de conteúdo, mas vincular toooverview e obter artigos iniciados para cada área do Service Fabric. 

## <a name="core-concepts"></a>Conceitos principais
[Terminologia do Service Fabric](service-fabric-technical-overview.md), [modelo de aplicativo](service-fabric-application-model.md), e [suporte para modelos de programação](service-fabric-choose-framework.md) fornecem mais conceitos e descrições, mas aqui são os fundamentos de saudação.

<table><tr><th>Conceitos principais</th><th>Tempo de design</th><th>Tempo de execução</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">
<img src="./media/service-fabric-content-roadmap/CoreConceptsVid.png" WIDTH="240" HEIGHT="162"></a></td>
<td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tlkI046yC_2906218965"><img src="./media/service-fabric-content-roadmap/RunTimeVid.png" WIDTH="240" HEIGHT="162"></a></td>
<td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=x7CVH56yC_1406218965">
<img src="./media/service-fabric-content-roadmap/RunTimeVid.png" WIDTH="240" HEIGHT="162"></a></td></tr>
</table>

### <a name="design-time-application-type-service-type-application-package-and-manifest-service-package-and-manifest"></a>Tempo de design: o tipo de aplicativo, tipo de serviço, o pacote de aplicativos e manifesto, pacote de serviço e manifesto
Um tipo de aplicativo é Olá atribuído tooa coleção dos tipos de serviços de nome/versão. Isso é definido em um arquivo *ApplicationManifest.xml*, que é inserido em um diretório do pacote de aplicativos. Olá pacote de aplicativos é, em seguida, copiado o repositório de imagens do cluster do Service Fabric toohello. Você pode criar um aplicativo nomeada deste tipo de aplicativo, que executa em cluster hello. 

Um tipo de serviço é Olá nome/versão atribuído pacotes de códigos, pacotes de dados e pacotes de configuração do serviço tooa. Isso é definido em um arquivo ServiceManifest.xml, que é inserido em um diretório do pacote de serviço. Olá diretório do pacote de serviço é, em seguida, referenciado por um pacote de aplicativo *ApplicationManifest.xml* arquivo. Em cluster hello, depois de criar um aplicativo nomeado, você pode criar um serviço nomeado de uma saudação tipos de serviço do tipo de aplicativo. Um tipo de serviço é descrito pelo seu arquivo *ServiceManifest.xml*. tipo de serviço de saudação é composto de definições de configuração do serviço código executável, que são carregadas em tempo de execução, e os dados estáticos que são consumidos pelo serviço de saudação.

![Tipos de aplicativos do Service Fabric e tipos de serviço][cluster-imagestore-apptypes]

Olá, pacote de aplicativo é um diretório de disco que contém o tipo de aplicativo a saudação *ApplicationManifest.xml* arquivo, o que faz referência a pacotes de serviço Olá para cada tipo de serviço que compõe o tipo de aplicativo hello. Por exemplo, um pacote de aplicativo para um tipo de aplicativo de email pode conter um pacote de serviço do banco de dados, um pacote de serviço front-end e pacote de serviço de fila de tooa de referências. arquivos Olá no diretório do pacote de aplicativo hello são repositório de imagens do cluster do Service Fabric toohello copiado. 

Um pacote de serviço é um diretório de disco que contém o tipo de serviço a saudação *ServiceManifest.xml* arquivo, o que faz referência a código hello, dados estáticos e pacotes de configuração para o tipo de serviço hello. arquivos Olá no diretório do pacote de serviço Olá são referenciados por tipo de aplicativo a saudação *ApplicationManifest.xml* arquivo. Por exemplo, um pacote de serviço pode se referir a código toohello, dados estáticos e pacotes de configuração que compõem um serviço de banco de dados.

### <a name="run-time-clusters-and-nodes-named-applications-named-services-partitions-and-replicas"></a>Tempo de execução: clusters e nós, chamados de aplicativos, chamado de serviços, partições e réplicas
Um [cluster do Service Fabric](service-fabric-deploy-anywhere.md) é um conjunto de máquinas físicas ou virtuais conectadas em rede, no qual os microsserviços são implantados e gerenciados. Clusters podem ser dimensionado toothousands de máquinas.

Uma máquina ou VM que faz parte de um cluster é chamado de nó. Cada nó recebe um nome de nó (uma cadeia de caracteres). Os nós têm características como propriedades de posicionamento. Cada máquina ou VM tem um serviço do Windows de início automático, `FabricHost.exe` que começa a ser executado na inicialização e então inicia dois executáveis: `Fabric.exe` e `FabricGateway.exe`. Esses dois executáveis compõem o nó de saudação. Para cenários de desenvolvimento ou teste, você pode hospedar vários nós em um único computador ou VM executando várias instâncias de `Fabric.exe` e `FabricGateway.exe`.

Um aplicativo nomeado é uma coleção de serviços membros que executam uma determinada função ou funções. Um serviço executa uma função autônoma completa (que pode iniciar e ser executada independentemente de outros serviços) e é composto de código, configuração e dados. Depois que um pacote de aplicativo é copiado toohello repositório de imagens, você cria uma instância de aplicativo hello em cluster Olá especificando um tipo de aplicativo do pacote de aplicativo hello (usando seu nome/versão). Cada instância do tipo de aplicativo tem um nome URI atribuído que se parece com *fabric:/MyNamedApp*. Em um cluster, você pode criar vários aplicativos nomeados a partir de um tipo de aplicativo único. Você também pode criar aplicativos nomeados a partir de diferentes tipos de aplicativos. Cada aplicativo nomeado é gerenciado e possui controle de versão independente.

Depois de criar um aplicativo nomeada, você pode criar uma instância de um de seus tipos de serviço (um serviço nomeado) no cluster Olá especificando o tipo de serviço da saudação (usando seu nome/versão). Cada instância de tipo de serviço recebe um nome de URI com escopo dentro do URI de seu aplicativo nomeado. Por exemplo, se você criar uma chamada de serviço dentro de um aplicativo de chamada "MyNamedApp" "MyDatabase", Olá URI é parecido com: *fabric: / MyNamedApp/MyDatabase*. Dentro de um aplicativo nomeado, você pode criar um ou mais serviços nomeados. Cada serviço nomeado pode ter seu próprio esquema de partição e contagens de instância/réplica. 

Há dois tipos de serviços: com e sem monitoração. Os serviços sem monitoração de estado podem armazenar o estado persistente em um serviço de armazenamento externo, como o Armazenamento do Azure, o Banco de Dados SQL do Azure ou o Azure Cosmos DB. Use um serviço sem monitoração de estado quando o serviço de saudação não tem nenhum armazenamento persistente em todos os. Um serviço com monitoração de estado usa toomanage de malha do serviço de estado do serviço por meio de suas coleções confiável ou Reliable Actors modelos de programação. 

Ao criar um serviço nomeado, você especifica um esquema de partição. Serviços com grandes quantidades de estado dividir os dados de saudação entre partições. Cada partição é responsável por uma parte de estado completo de saudação do serviço de saudação, que é distribuído entre nós do cluster hello. Dentro de uma partição, serviços nomeados sem estado têm instâncias, enquanto serviços nomeados com estado têm réplicas. Normalmente, os serviços nomeadas sem estado têm apenas uma partição, já que não têm estado interno. Os serviços nomeados com estado mantêm seu estado dentro de réplicas e cada partição tem seu próprio conjunto de réplicas. Operações de leitura e gravação são executadas em uma réplica (chamada hello primário). Alterações toostate de gravação operações são replicados toomultiple outras réplicas (chamadas secundárias ativas). 

Olá diagrama a seguir mostra a relação Olá entre aplicativos e instâncias de serviço, partições e réplicas.

![Partições e réplicas dentro de um serviço][cluster-application-instances]

### <a name="partitioning-scaling-and-availability"></a>Particionamento, dimensionamento e disponibilidade
[Particionamento](service-fabric-concepts-partitioning.md) não é exclusivo tooService malha. Uma forma bem conhecida de particionamento é o particionamento de dados ou fragmentação. Serviços com monitoração de estado com grandes quantidades de estado dividir os dados de saudação entre partições. Cada partição é responsável por uma parte do estado de conclusão Olá do serviço de saudação. 

réplicas de saudação de cada partição são distribuídas em nós do cluster Olá, permitindo que o estado do serviço nomeado muito[escala](service-fabric-concepts-scalability.md). À medida que dados saudação crescer, aumento de partições e do Service Fabric redistribui partições em uso eficiente de toomake de nós de recursos de hardware. Se você adicionar um novo cluster de toohello de nós, Service Fabric será reequilibrar réplicas da partição Olá em Olá aumentado o número de nós. Geral melhora o desempenho do aplicativo e reduz a contenção de toomemory de acesso. Se nós Olá cluster Olá não estão sendo usados com eficiência, você pode diminuir o número de saudação de nós no cluster de saudação. Service Fabric novamente redistribui réplicas da partição Olá em número de saudação reduzido de nós toomake melhor uso do hardware de saudação em cada nó.

Dentro de uma partição, serviços nomeados sem estado têm instâncias, enquanto serviços nomeados com estado têm réplicas. Normalmente, os serviços nomeadas sem estado têm apenas uma partição, já que não têm estado interno. instâncias de partição Olá fornecem para [disponibilidade](service-fabric-availability-services.md). Se uma instância falhar, outras instâncias continuam toooperate normalmente e, em seguida, o Service Fabric cria uma nova instância. Os serviços nomeados com estado mantêm seu estado dentro de réplicas e cada partição tem seu próprio conjunto de réplicas. Operações de leitura e gravação são executadas em uma réplica (chamada hello primário). Alterações toostate de gravação operações são replicados toomultiple outras réplicas (chamadas secundárias ativas). Uma réplica falhar, o Service Fabric cria uma nova réplica de réplicas existentes Olá.

## <a name="stateless-and-stateful-microservices-for-service-fabric"></a>Microsserviços com e sem estado para o Service Fabric
Malha do serviço permite que aplicativos toobuild que consistem em microservices ou contêineres. Microservices sem monitoração de estado (como gateways de protocolo e proxies da web) não mantém um estado mutável fora de uma solicitação e sua resposta do serviço de saudação. As funções de trabalho dos Serviços de Nuvem do Azure são um exemplo de serviço sem estado. Microservices com monitoração de estado (como contas de usuário, bancos de dados, dispositivos, carrinhos de compra e filas) manter um estado mutável autoritativo além Olá solicitação e sua resposta. Os aplicativos em escala da Internet de hoje consistem em uma combinação de microsserviços com e sem estado. 

Uma chave differentation com o Service Fabric é seu foco forte na criação de serviços com monitoração de estado, com hello [criados em modelos de programação ](service-fabric-choose-framework.md) ou com os serviços em contêineres com monitoração de estado. Olá [cenários de aplicativo](service-fabric-application-scenarios.md) descrevem Olá cenários onde os serviços com monitoração de estado são usados.

Por que tem com monitoração de estado microservices juntamente com aqueles sem monitoração de estado? Olá duas razões principais são:

* Você pode criar alta taxa de transferência, baixa latência, serviços de processamento tolerantes a falhas de transações online (OLTP) por manter o código e dados fechar Olá mesma máquina. Alguns exemplos são vitrines interativas, pesquisa, sistemas de Internet das coisas (IoT), sistemas de comércio, sistemas de detecção de fraudes e processamento de cartão de crédito e gerenciamento de registros pessoais.
* Você pode simplificar o design do aplicativo. Com monitoração de estado microservices eliminar a necessidade de saudação de filas adicionais e caches, que são normalmente necessárias tooaddress Olá disponibilidade e requisitos de latência de um aplicativo totalmente sem monitoração de estado. Serviços com monitoração de estado são naturalmente alta disponibilidade e baixa latência, que reduz o número de saudação do toomanage de partes de movimentação em seu aplicativo como um todo.

## <a name="supported-programming-models"></a>Modelos de programação com suporte
Service Fabric oferece toowrite de várias maneiras e gerenciar seus serviços. Serviços podem usar Olá APIs de malha do serviço tootake aproveitar os recursos e estruturas de aplicativo da plataforma hello. Os serviços também podem ser um programa executável compilado, escrito em qualquer linguagem e hospedado em um cluster do Service Fabric. Para saber mais, veja [Modelos de programação com suporte](service-fabric-choose-framework.md).

### <a name="containers"></a>Contêineres
Por padrão, o Service Fabric implanta e ativa esses serviços como processos. O Service Fabric também pode implantar serviços em [contêineres](service-fabric-containers-overview.md). É importante, você pode combinar serviços em processos e serviços em contêineres Olá mesmo aplicativo. O Service Fabric dá suporte à implantação de contêineres do Linux e do Windows no Windows Server 2016. Você pode implantar aplicativos existentes, serviços sem monitoração de estado ou serviços com estado em contêineres. 

### <a name="reliable-services"></a>Reliable Services
[Serviços confiáveis](service-fabric-reliable-services-introduction.md) é uma estrutura simples para escrever serviços que integram Olá Service Fabric plataforma e aproveitar o conjunto completo de recursos de plataforma de hello. Serviços confiáveis podem ser sem monitoração de estado (semelhante toomost plataformas de serviços, como servidores web ou funções de trabalho nos serviços de nuvem do Azure), onde o estado é mantido em uma solução externa, como o armazenamento de tabela do Azure ou banco de dados do Azure. Serviços confiáveis também podem ser com monitoração de estado, onde o estado é mantido diretamente no serviço de saudação usando coleções confiável. O estado se torna [altamente disponível](service-fabric-availability-services.md) por meio de replicação e é distribuído por meio de [particionamento](service-fabric-concepts-partitioning.md), tudo gerenciado automaticamente pelo Service Fabric.

### <a name="reliable-actors"></a>Reliable Actors
Criado com base em serviços confiáveis, Olá [Reliable Actor](service-fabric-reliable-actors-introduction.md) framework é uma estrutura de aplicativo que implementa o padrão de ator Virtual hello, com base no padrão de design de ator hello. estrutura de Reliable Actor de saudação usa unidades independentes de computação e de estado com a execução de thread único chamada atores. Olá Reliable Actor framework fornece criados em comunicação para atores e persistência de estado previamente configurado e configurações em expansão.

### <a name="aspnet-core"></a>ASP.NET Core
O Service Fabric é integrado ao [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) como um modelo de programação de primeira classe para a criação de aplicativos Web e de API

### <a name="guest-executables"></a>Executáveis de convidado
Um [executável convidado](service-fabric-deploy-existing-app.md) é um executável existente e arbitrário (escrito em qualquer linguagem), hospedado em um cluster do Service Fabric junto com outros serviços. Os executáveis convidados não são integrados diretamente às APIs do Service Fabric. Porém eles ainda aproveitar os recursos de Olá ofertas da plataforma, como integridade personalizado e carregar relatórios e descoberta de serviço chamando APIs REST. Eles também têm suporte completo do ciclo de vida do aplicativo. 

## <a name="application-lifecycle"></a>Ciclo de vida do aplicativo
Como com outras plataformas, um aplicativo no serviço de malha normalmente passa pelas Olá seguintes fases: design, desenvolvimento, teste, implantação, atualização, manutenção e remoção. Serviço de malha fornece suporte de primeira classe para Olá o ciclo de vida do aplicativo completo de aplicativos de nuvem, de desenvolvimento por meio de implantação, gerenciamento diário e manutenção tooeventual encerramento. modelo de serviço Olá permite que vários tooparticipate diferentes funções independentemente no ciclo de vida de aplicativo hello. [Ciclo de vida do aplicativo de malha do serviço](service-fabric-application-lifecycle.md) fornece uma visão geral da saudação APIs e como eles são usados por diferentes funções hello durante as fases de saudação do ciclo de vida do aplicativo hello Service Fabric. 

Olá ciclo de vida do aplicativo inteiro pode ser gerenciado usando [cmdlets do PowerShell](/powershell/module/ServiceFabric/), [c# APIs](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient), [APIs Java](/java/api/system.fabric._application_management_client), e [APIs REST](/rest/api/servicefabric/). Você também pode configurar pipelines de integração contínua/implantação contínua, usando ferramentas como o [Visual Studio Team Services](service-fabric-set-up-continuous-integration.md) ou [Jenkins](service-fabric-cicd-your-linux-java-application-with-jenkins.md).

Olá vídeo Microsoft Virtual Academy a seguir descreve como toomanage ciclo de vida do aplicativo:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=My3Ka56yC_6106218965">
<img src="./media/service-fabric-content-roadmap/AppLifecycleVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="test-applications-and-services"></a>Testar aplicativos e serviços
toocreate realmente serviços de nuvem escala é tooverify crítico que seus aplicativos e serviços podem suportar falhas do mundo real. Olá serviço de análise de falha foi projetado para testar os serviços que são criados no Service Fabric. Com hello [serviço de análise de falha](service-fabric-testability-overview.md), você pode induzir falhas significativas e execute os cenários de teste completo em relação a seus aplicativos. Esses cenários e falhas de exercício em validar Olá vários estados e transições que um serviço enfrentam ao longo de seu ciclo de vida, tudo em uma maneira consistente, segura e controlada.

As [Ações](service-fabric-testability-actions.md) destinam-se ao teste de um serviço, usando falhas individuais. Um desenvolvedor de serviço pode usá-los como blocos de construção toowrite complicado cenários. Exemplos de falhas simuladas são:

* Reinicie um nó toosimulate inúmeras situações em que um computador ou VM for reinicializado.
* Mova uma réplica de seu serviço com monitoração de estado toosimulate balanceamento de carga, failover ou atualização do aplicativo.
* Invocação de perda de quorum em um serviço com monitoração de estado de toocreate uma situação em que as operações de gravação não podem continuar porque não existem dados novos de tooaccept suficientes réplicas "backup" ou "secondary".
* Invocação de perda de dados em um serviço com monitoração de estado de toocreate uma situação em que todos os estados de memória é completamente apagados.

Os [cenários](service-fabric-testability-scenarios.md) são operações complexas compostas de uma ou mais ações. Olá falhas Analysis Services fornece dois cenários completos internos:

* [Cenário de caos](service-fabric-controlled-chaos.md)-simula falhas contínuas, intercaladas (normais e anormais) em todo o cluster Olá por longos períodos de tempo.
* [Cenário de failover](service-fabric-testability-scenarios.md#failover-test)-uma versão do cenário de teste de caos Olá que tem como alvo uma partição de serviço específico, deixando outros serviços afetados.

## <a name="clusters"></a>Clusters
Um [cluster do Service Fabric](service-fabric-deploy-anywhere.md) é um conjunto de máquinas físicas ou virtuais conectadas em rede, no qual os microsserviços são implantados e gerenciados. Clusters podem ser dimensionado toothousands de máquinas. Um computador ou VM que faz parte de um cluster é chamado de nó de cluster. Cada nó recebe um nome de nó (uma cadeia de caracteres). Os nós têm características como propriedades de posicionamento. Cada computador ou VM tem um serviço de início automático, `FabricHost.exe`, que começa a ser executado na inicialização e, em seguida, inicia dois executáveis: Fabric.exe e FabricGateway.exe. Esses dois executáveis compõem o nó de saudação. Para cenários de teste, você pode hospedar vários nós em um único computador ou VM, executando várias instâncias do `Fabric.exe` e do `FabricGateway.exe`.

Os clusters do Service Fabric podem ser criados em máquinas virtuais ou computadores físicos que executam o Windows Server ou Linux. Você é capaz de toodeploy e executar aplicativos de malha do serviço em qualquer ambiente em que você tem um conjunto de computadores Windows Server ou Linux que estão interconectados: no local, no Microsoft Azure ou em qualquer provedor de nuvem.

Hello vídeo Microsoft Virtual Academy a seguir descreve os clusters de malha do serviço:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">
<img src="./media/service-fabric-content-roadmap/ClusterOverview.png" WIDTH="360" HEIGHT="244">
</a></center>

### <a name="clusters-on-azure"></a>Clusters no Azure
A execução de clusters de malha do serviço no Azure fornece integração com outros recursos do Azure e serviços, que torna as operações e o gerenciamento de cluster hello mais fácil e confiável. Um cluster é um recurso do Azure Resource Manager, portanto você pode modelar clusters da mesma maneira que qualquer outro recurso no Azure. Gerenciador de recursos também fornece gerenciamento fácil de todos os recursos usados pelo cluster hello como uma única unidade. Os clusters no Azure são integrados com o diagnóstico do Azure e o Log Analytics. Os tipos de nó de cluster são [conjuntos de dimensionamento de máquinas virtuais](/azure/virtual-machine-scale-sets/index) e, portanto, a funcionalidade de dimensionamento automático é interna.

Você pode criar um cluster no Azure por meio de saudação [portal do Azure](service-fabric-cluster-creation-via-portal.md), de um [modelo](service-fabric-cluster-creation-via-arm.md), ou de [Visual Studio](service-fabric-cluster-creation-via-visual-studio.md).

visualização de saudação do Service Fabric no Linux permite toobuild, implantar e gerenciar aplicativos altamente escalonáveis, altamente disponíveis no Linux, exatamente como você faria no Windows. estruturas de malha do serviço de saudação (serviços confiáveis e atores confiável) estão disponíveis em Java no Linux, em adição tooC # (.NET Core). Você também pode compilar os [serviços executáveis convidados](service-fabric-deploy-existing-app.md) com qualquer linguagem ou estrutura. Além disso, visualização de saudação também oferece suporte a orquestração contêineres do Docker. Contêineres do docker podem executar arquivos executáveis de convidado ou nativo serviços do Service Fabric, que usa estruturas de malha do serviço de saudação. Para obter mais informações, leia [Service Fabric no Linux](service-fabric-linux-overview.md).

Como o Service Fabric no Linux é uma visualização, há alguns recursos que têm suporte no Windows, mas não no Linux. mais, leia toolearn [diferenças entre o Service Fabric no Linux e Windows](service-fabric-linux-windows-differences.md).

### <a name="standalone-clusters"></a>Clusters independentes
Serviço de malha fornece um pacote de instalação para você toocreate autônomo do Service Fabric clusters no local ou em qualquer provedor de nuvem. Autônomo clusters dê Olá liberdade toohost um cluster onde desejar. Se seus dados são toocompliance assunto ou restrições regulamentares, ou se desejar tookeep seu local de dados, você pode hospedar seu próprio cluster e aplicativos. Aplicativos do Service Fabric podem ser executados em vários ambientes de hospedagem sem alterações, portanto traz seu conhecimento da criação de aplicativos de um tooanother de ambiente de hospedagem. 

[Criar seu primeiro cluster autônomo do Service Fabric](service-fabric-get-started-standalone-cluster.md)

Ainda não há suporte para clusters autônomos do Linux.

### <a name="cluster-security"></a>Segurança de cluster
Clusters devem ser protegido tooprevent não autorizado usuários conectem cluster tooyour, especialmente quando ele tiver cargas de trabalho de produção em execução. Embora seja possível toocreate um cluster não seguro, isso permite que os usuários anônimos tooconnect tooit se pontos de extremidade de gerenciamento são expostos toohello internet pública. Não é possível toolater Ativar segurança em um cluster não segura: segurança de cluster está habilitada no momento da criação de cluster.

Olá cenários de segurança de cluster são:
* Segurança de nó para nó
* Segurança de cliente para nó
* RBAC (Controle de Acesso Baseado em Função)

Para obter mais informações, leia [Proteger um cluster](service-fabric-cluster-security.md).

### <a name="scaling"></a>Dimensionamento
Se você adicionar um novo cluster de toohello de nós, o Service Fabric redistribui réplicas da partição hello e instâncias em Olá aumentado o número de nós. Geral melhora o desempenho do aplicativo e reduz a contenção de toomemory de acesso. Se nós Olá cluster Olá não estão sendo usados com eficiência, você pode diminuir o número de saudação de nós no cluster de saudação. Serviço de malha novamente redistribui réplicas da partição hello e instâncias em número de saudação reduzido de nós toomake melhor o uso de hardware de saudação em cada nó. Você pode dimensionar clusters no Azure [manualmente](service-fabric-cluster-scale-up-down.md) ou [programaticamente](service-fabric-cluster-programmatic-scaling.md). Clusters autônomos podem ser dimensionados [manualmente](service-fabric-cluster-windows-server-add-remove-nodes.md).

### <a name="cluster-upgrades"></a>Atualizações do cluster
Periodicamente, são lançadas novas versões do tempo de execução do Service Fabric hello. Realize as atualizações de tempo de execução ou de malha no cluster para que você sempre tenha uma [versão com suporte](service-fabric-support.md) em execução. Além disso toofabric atualizações, você também pode atualizar a configuração de cluster, como certificados ou portas de aplicativo.

Um cluster do Service Fabric é um recurso cujo proprietário é você, mas que é parcialmente gerenciado pela Microsoft. Microsoft é responsável pela aplicação de patch Olá subjacente do sistema operacional e executar atualizações de malha no cluster. Você pode definir sua malha automática do cluster tooreceive atualizações, quando a Microsoft lança uma nova versão, ou escolha tooselect uma versão com suporte de malha que você deseja. Atualizações de malha e de configuração podem ser definidas por meio de saudação portal do Azure ou por meio do Gerenciador de recursos. Para obter mais informações, leia [Atualizar um cluster do Service Fabric](service-fabric-cluster-upgrade.md). 

Um cluster autônomo é um recurso que é totalmente seu. Você é responsável pela aplicação de patch Olá subjacente do sistema operacional e iniciar atualizações de malha. Se o cluster pode conectar-se muito[https://www.microsoft.com/download](https://www.microsoft.com/download), você pode definir o download de tooautomatically do cluster e provisionar Olá Service Fabric do novo pacote de tempo de execução. Você, em seguida, deve iniciar a atualização de saudação. Se o cluster não puder acessar [https://www.microsoft.com/download](https://www.microsoft.com/download), você pode baixar manualmente o novo pacote de tempo de execução de saudação de um computador conectado à internet e, em seguida, iniciar a atualização de saudação. Para obter mais informações, leia [Atualizar um cluster autônomo do Service Fabric](service-fabric-cluster-upgrade-windows-server.md).

## <a name="health-monitoring"></a>Monitoramento da integridade
Malha do serviço apresenta uma [modelo de integridade](service-fabric-health-introduction.md) projetado cluster não íntegro tooflag e condições de aplicativo em entidades específicas (como nós de cluster e réplicas do serviço). modelo de integridade Olá usa relatórios de integridade (componentes do sistema e watchdogs). meta de saudação é fácil e rápido de diagnóstico e reparo. Gravadores de serviço precisam toothink antecipadamente sobre integridade e como muito[criar relatórios de integridade](service-fabric-report-health.md#design-health-reporting). Qualquer condição que pode afetar a integridade deve ser relatada, especialmente se ele pode ajudar a problemas de sinalizador fechar toohello raiz. informações de integridade Olá podem economizar tempo e esforço na depuração e investigação depois que o serviço hello está ativo e em execução em grande escala em produção.

monitor de recursos do Service Fabric Olá identificado condições de interesse. Eles informam essas condições com base na respectiva exibição local. Olá [repositório de integridade](service-fabric-health-introduction.md#health-store) agrega dados de integridade enviados por toodetermine de Relatores todas as entidades estão íntegros globalmente. modelo de saudação é toouse avançados, flexíveis e fáceis de toobe pretendido. qualidade Olá Olá de relatórios de integridade determina a precisão de saudação do modo de exibição de integridade de saudação do cluster de saudação. Falsos positivos que mostram incorretamente problemas de integridade podem afetar negativamente atualizações ou outros serviços que usam dados de integridade. Exemplos de tais serviços são os serviços de reparo e os mecanismos de alerta. Portanto, alguns pensamento é relatórios tooprovide necessários que capturam as condições de interesse em Olá melhor maneira possível.

A emissão de relatórios pode ser feita:
* Olá monitorado réplicas do serviço de malha do serviço ou instância.
* De watchdogs internos implantados como um serviço do Service Fabric (por exemplo, um serviço sem estado do Service Fabric que monitora as condições e emite relatórios). watchdogs Olá podem ser implantados em todos os nós ou podem ser serviço de afinidade toohello monitorado.
* Watchdogs internos que é executado em nós do Service Fabric hello, mas não são implementados como serviços do Service Fabric.
* Externa watchdogs investigação Olá recurso de cluster de malha do serviço Olá externa (por exemplo, serviço de monitoramento como Gomez).

Fora da caixa Olá, componentes do Service Fabric relatam integridade todas as entidades no cluster hello. Os [relatórios de integridade do sistema](service-fabric-understand-and-troubleshoot-with-system-health-reports.md) fornecem visibilidade da funcionalidade do cluster e de aplicativos e sinalizam problemas por meio da integridade. Para aplicativos e serviços, relatórios de integridade do sistema, verifique se que entidades foram implementadas e estão funcionando corretamente da perspectiva de saudação do tempo de execução do Service Fabric hello. Olá relatórios não fornece nenhum monitoramento de integridade da lógica de negócios de saudação do serviço de saudação ou detectar processos travados. lógica de tooadd informações tooyour específica desse serviço, [implementar relatórios de integridade personalizada](service-fabric-report-health.md) em seus serviços.

Serviço de malha fornece várias maneiras muito[exibir relatórios de integridade](service-fabric-view-entities-aggregated-health.md) agregados no repositório de integridade hello:
* [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) ou outras ferramentas de visualização.
* Consultas de integridade (por meio de [PowerShell](/powershell/module/ServiceFabric/), Olá [c# FabricClient APIs](/api/system.fabric.fabricclient.healthclient) e [FabricClient APIs Java](/java/api/system.fabric._health_client), ou [APIs REST](/rest/api/servicefabric)).
* Gerais consultas que retornam uma lista de entidades que têm integridade como uma das propriedades de saudação (por meio do PowerShell, API de saudação ou REST).

Olá que seguintes Microsoft Virtual Academy vídeo descreve o modelo de integridade de malha do serviço hello e como ele é usado:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tevZw56yC_1906218965">
<img src="./media/service-fabric-content-roadmap/HealthIntroVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="next-steps"></a>Próximas etapas
* Saiba como toocreate uma [cluster no Azure](service-fabric-cluster-creation-via-portal.md) ou um [cluster autônomo no Windows](service-fabric-cluster-creation-for-windows-server.md).
* Tente criar um serviço usando Olá [serviços confiáveis](service-fabric-reliable-services-quick-start.md) ou [Reliable Actors](service-fabric-reliable-actors-get-started.md) modelos de programação.
* Saiba como muito[migrar dos serviços de nuvem](service-fabric-cloud-services-migration-differences.md).
* Aprender muito[monitorar e diagnosticar serviços](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md). 
* Aprender muito[testar seus aplicativos e serviços](service-fabric-testability-overview.md).
* Aprender muito[gerenciar e organizar recursos de cluster](service-fabric-cluster-resource-manager-introduction.md).
* Examine a saudação [exemplos do Service Fabric](http://aka.ms/servicefabricsamples).
* Saiba mais sobre as [opções de suporte do Service Fabric](service-fabric-support.md).
* Saudação de leitura [blog da equipe](https://blogs.msdn.microsoft.com/azureservicefabric/) para artigos e anúncios.


[cluster-application-instances]: media/service-fabric-content-roadmap/cluster-application-instances.png
[cluster-imagestore-apptypes]: ./media/service-fabric-content-roadmap/cluster-imagestore-apptypes.png
