---
title: toomicroservices aaaIntroduction no Azure | Microsoft Docs
description: "Uma visão geral de por que a criação de aplicativos de nuvem com uma abordagem microservices é importante para desenvolvimento de aplicativos modernos e como Service Fabric do Azure fornece uma plataforma tooachieve isso."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: fae2be85-0ab4-4cd3-9d1f-e0d95fe1959b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: msfussell
ms.openlocfilehash: b11920b9105e7575390e8fcf0d1ef6ab3c632978
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="why-a-microservices-approach-toobuilding-applications"></a>Por que um microservices abordagem toobuilding aplicativos?
Para nós, desenvolvedores de software, não há qualquer novidade no modo como pensamos sobre a decomposição de um aplicativo em partes componentes. É paradigma de saudação central de orientação a objeto, abstrações de software e componentização. Atualmente, esse fatoração tende tootake formulário de saudação de classes e interfaces entre camadas de tecnologia e bibliotecas compartilhadas. Em geral, uma abordagem em camadas é adotada com um repositório de back-end, lógica de negócios de camada intermediária e uma IU (interface do usuário) de front-end. O que *tem* alterado ao longo do hello últimos anos é que estamos, como os desenvolvedores, criando aplicativos de nuvem Olá distribuídos e orientado pelos negócios hello.

necessidades de negócios alteração Olá são:

* Um serviço que é criado e opera em clientes de tooreach de escala em regiões geográficas novo (por exemplo).
* Transmissão mais rápida de recursos e funcionalidades toobe capaz de toorespond toocustomer demandas de forma ágil.
* Custos de tooreduce de utilização de recurso aprimorado.

Essas necessidades comerciais estão afetando o *modo* como criamos os aplicativos.

Para obter mais informações sobre a abordagem de saudação toomicroservices do Azure, leia [Microservices: uma revolução de aplicativo com a nuvem Olá](https://azure.microsoft.com/blog/microservices-an-application-revolution-powered-by-the-cloud/).

## <a name="monolithic-vs-microservice-design-approach"></a>Abordagem de design monolítico versus microsserviços
Todos os aplicativos evoluem ao longo do tempo. Aplicativos bem-sucedida evoluem sendo toopeople útil. Aplicativos sem sucesso não evoluem e eventualmente tornam-se obsoletos. pergunta Olá torna-se: A quantidade de saber sobre os requisitos de hoje, e quais elas serão no hello futuras? Por exemplo, digamos que você esteja criando um aplicativo de relatório para um departamento. Tiver certeza de que o aplicativo hello permanece no escopo de saudação da sua empresa e que os relatórios de saudação são de curta duração. A escolha do método é diferente de, digamos, criando um serviço que fornece vídeo tootens conteúdo de milhões de clientes. 

Às vezes, obtendo algo diferente de porta hello como prova de conceito é um fator importante hello, enquanto você sabe que o aplicativo hello pode ser reformulado mais tarde. Não há muito sentido em trabalhar muito em algo que nunca será usado. Sua saudação normal engenharia compensação. Em Olá outro lado, quando as empresas falam sobre criação hello nuvem, a expectativa de saudação é crescimento e uso. problema de saudação é de crescimento e escala são imprevisíveis. Gostaríamos tooprototype capaz de toobe rapidamente sabendo também que estamos em um toodeal de caminho com êxito futuras. Essa abordagem de inicialização lean Olá é: criar, medidas, aprender e iterar.

Durante a era de cliente-servidor hello, podemos tendeu toofocus na criação de aplicativos em camadas usando tecnologias específicas em cada camada. termo Olá *monolítico* aplicativo surgiu para essas abordagens. interfaces de saudação tendeu toobe entre camadas hello e um design mais rigidamente acoplado foi usado entre os componentes em cada camada. Os desenvolvedores projetaram e fatoraram classes compiladas em bibliotecas e as vincularam em alguns arquivos executáveis e DLLs. 

Há benefícios toosuch uma abordagem de design monolítico. Geralmente é mais simples toodesign e ele tem mais rápidas chamadas entre componentes, porque essas chamadas costumam ser sobre a comunicação entre processos (IPC). Além disso, todos testa um único produto, o que tende a toobe pessoas-recursos mais eficientes. desvantagem de saudação é que há uma grande união entre camadas em camadas e componentes individuais não podem ser dimensionados. Se você precisar tooperform correções ou atualizações, você tem toowait para outros toofinish seus testes. É mais difícil toobe agile.

Microservices tratar essas desvantagens e mais estreitamente alinham Olá precede os requisitos de negócios, mas eles também têm benefícios e passivos. Olá benefícios microservices é que cada um deles normalmente encapsula a funcionalidade de negócios mais simples, que você expandir ou reduzir, teste, implanta e gerencia de forma independente. Uma vantagem importante de uma abordagem de microsserviço é que as equipes são mais por cenários de negócios que orientada por tecnologia, que Olá abordagem em camadas incentiva. Na prática, equipes menores desenvolvem um microsserviço baseado em um cenário de cliente e usam qualquer tecnologia escolhida. 

Em outras palavras, organização de saudação não precisa de aplicativos de microsserviço toostandardize técnico toomaintain. Equipes individuais que os próprios serviços podem fazer o que faz sentido para eles com base no conhecimento da equipe ou o problema de Olá toosolve mais apropriado. Na prática, é preferível ter um conjunto de tecnologias recomendadas, como determinado repositório NoSQL ou uma estrutura de aplicativo Web.

desvantagem de saudação do microservices tem gerenciamento Olá maior número de entidades separadas e lidar com controle de versão e implantações mais complexas. Aumenta o tráfego de rede entre microservices hello, bem como as latências de rede correspondente hello. Ter muitos serviços informais e granulares é uma receita desastrosa para o desempenho. Sem ferramentas toohelp exibir essas dependências, é difícil muito "ver" todo o sistema hello. 

Padrões que abordagem de microsserviço Olá funcione por comum acordo em como toocommunicate e a tolerância a falhas de apenas os itens de saudação precisa de um serviço, em vez de contratos rígidos. É importante toodefine esses contratos com antecedência na saudação de design, porque os serviços de atualização independentemente um do outro. Outra descrição cunhada para desenvolver com uma abordagem de microsserviços é "SOA (arquitetura orientada a serviços) de granulação fina".

***Em sua forma mais simples, hello microservices design abordagem é sobre uma federação separada de serviços, com alterações independentes tooeach e padrões definidos para comunicação.***

Como mais aplicativos de nuvem são produzidos, pessoas descobrir que este Decomposição de saudação geral o aplicativo para os serviços independentes, voltada para o cenário é uma abordagem melhor a longo prazo.

## <a name="comparison-between-application-development-approaches"></a>Comparação entre abordagens de desenvolvimento de aplicativos
![Desenvolvimento de aplicativos da plataforma Service Fabric][Image1]

1) Um aplicativo monolítico contém uma funcionalidade específica ao domínio e é normalmente dividido por camadas funcionais, como Web, negócios e dados.

2) Você dimensiona um aplicativo monolítico clonando-o em vários servidores/máquinas virtuais/contêineres.

3) Um aplicativo de microsserviço separa a funcionalidade em serviços menores separados.

4) Olá microservices abordagem escalas out Implantando cada serviço independentemente, criar instâncias desses serviços em máquinas virtuais/servidores/contêineres.

Criando com um microsserviço abordagem não é uma solução completa de todos os projetos, mas alinhar melhor aos objetivos de negócios Olá descritos anteriormente. Começando com uma abordagem monolítica pode ser aceitável se você souber que você terá o código do hello oportunidade toorework hello mais tarde em um projeto de microservices. Mais comumente, você pode começa com um aplicativo monolítico e lenta dividi-la em etapas, começando com áreas funcionais do hello que precisam toobe mais escalonável ou agile.

toosummarize, Olá microsserviço abordagem é toocompose seu aplicativo de vários serviços pequenos. Serviços de saudação executados em contêineres são implantados em um cluster de computadores. Equipes menores desenvolvem um serviço que se concentra em um cenário e independentemente de teste, versão, implantar e dimensionar cada serviço para que todo o aplicativo hello pode evoluir.

## <a name="what-is-a-microservice"></a>O que é um microsserviço?
Há diferentes definições de microsserviços. Se você pesquisar Olá da Internet, você encontrará muitos recursos úteis que fornecem seus próprios pontos de Vista e definições. No entanto, a maioria das Olá características de microservices a seguir é amplamente acordada:

* Abrange um cenário de cliente ou comercial. Qual é o problema de saudação que está resolvendo?
* Desenvolvidos por uma pequena equipe de engenharia.
* Escritos em qualquer linguagem de programação e usam qualquer estrutura.
* Consistem em código e (opcionalmente) estado, com versão, implantação e dimensionamento independentes.
* Interagem com outros microsserviços em protocolos e interfaces bem definidos.
* Tem nomes exclusivos (URLs) usado tooresolve sua localização.
* Permanecem consistentes e disponíveis na presença de saudação de falhas.

Você pode resumir essas características em:

***Os aplicativos de microsserviços são compostos por serviços pequenos e focados no cliente, com controle de versão independente e escalonáveis que se comunicam entre si por meio de protocolos padrão com interfaces bem definidas.***

Abordamos primeiro dois pontos de saudação na saudação anterior seção e agora vamos expandir e esclarecer Olá outros.

### <a name="written-in-any-programming-language-and-use-any-framework"></a>Escritos em qualquer linguagem de programação e usam qualquer estrutura
Como os desenvolvedores, deveríamos estar livre toochoose um idioma ou uma estrutura que queremos, dependendo da nossa habilidades ou necessidades de saudação do serviço de saudação. Em alguns serviços, você poderá valor benefícios de desempenho de saudação do C++ acima de tudo. Em outros serviços, facilidade de saudação do desenvolvimento gerenciado em c# ou Java pode ser mais importante. Em alguns casos, talvez seja necessário toouse uma biblioteca específica de parceiro, a tecnologia de armazenamento de dados, ou meios de expor Olá tooclients de serviço.

Depois de ter escolhido uma tecnologia, você vir toohello operacional ou gerenciamento de ciclo de vida e dimensionamento do serviço de saudação.

### <a name="allows-code-and-state-toobe-independently-versioned-deployed-and-scaled"></a>Permite toobe de código e o estado independentemente com controle de versão, implantado e escala
No entanto você escolher toowrite seu microservices, Olá código e, opcionalmente, estado Olá deve independentemente implantar, atualizar e dimensionar. Isso é realmente uma saudação mais difícil problemas toosolve, porque resume tooyour variedade de tecnologias. Para dimensionar, compreender como toopartition (ou fragmento) ambos Olá código e o estado é um desafio. Quando Olá código e o estado de usar tecnologias separadas, que é comum atualmente, os scripts de implantação de saudação para seu microsserviço necessário toocope capaz de toobe com dimensionamento ambos. Trata-se também agilidade e flexibilidade, para poder atualizar algumas das Olá microservices sem ter que tooupgrade todos eles ao mesmo tempo.

Retornando toohello monolítico versus abordagem microsserviço por um momento, hello diagrama a seguir mostra Olá diferenças no estado de toostoring abordagem hello.

#### <a name="state-storage-between-application-styles"></a>Armazenamento de estado entre os estilos de aplicativo
![Armazenamento de estado da plataforma Service Fabric][Image2]

***a abordagem monolítico Olá Olá esquerda tem um único banco de dados e níveis de tecnologias específicas.***

***Olá microservices abordagem Olá direita tem escopo de um gráfico de interconectadas microservices onde o estado é normalmente toohello microsserviço e várias tecnologias são usadas.***

Uma abordagem monolítico, normalmente o aplicativo hello usa um único banco de dados. vantagem de saudação é que se trata de um único local, o que torna fácil toodeploy. Cada componente pode ter uma única tabela toostore seu estado. As equipes precisam estado separado toostrictly, que é um desafio. Inevitavelmente há temptations tooadd uma nova coluna tooan cliente tabela existente, faça uma junção entre tabelas e criar dependências na camada de armazenamento de saudação. Quando isso acontecer, não será possível dimensionar os componentes individuais. 

Olá microservices abordagem, cada serviço gerencia e armazena seu próprio estado. Cada serviço é responsável por dimensionar demandas de saudação toomeet juntos código e o estado do serviço de saudação. Uma desvantagem é que, quando há uma necessidade toocreate exibições ou consultas de dados do aplicativo, você precisa tooquery em estado de diferentes repositórios. Normalmente, isso é resolvido com um microsserviço separado que cria um modo de exibição em uma coleção de microsserviços. Se você precisar tooperform várias consultas ocasionais em dados Olá, considere cada microsserviço escrevendo seu serviço de armazenamento de dados de tooa de dados para análise offline.

Controle de versão é a versão toohello específico implantado de um microsserviço assim que várias versões diferentes implantar e executar lado a lado. Controle de versão abrange cenários de saudação em que uma versão mais recente de um microsserviço falha durante a atualização e precisa tooan back tooroll versão anterior. Olá outro cenário para controle de versão está executando A/B-estilo de teste, em que diferentes usuários experimentam diferentes versões do serviço de saudação. Por exemplo, é comum tooupgrade um microsserviço para um conjunto específico de novas funcionalidades do clientes tootest antes de implantá-la mais amplamente. Depois de gerenciamento do ciclo de vida de microservices, agora chegamos toocommunication entre eles.

### <a name="interacts-with-other-microservices-over-well-defined-interfaces-and-protocols"></a>Interage com outros microservices em protocolos e interfaces bem-definidos
Este tópico precisa pouca atenção aqui, porque a literatura abrangente sobre arquitetura orientada a serviços que tenha sido publicada pela Olá últimos 10 anos descreve os padrões de comunicação. Em geral, comunicação de serviço usa uma abordagem REST com os protocolos TCP e HTTP e XML ou JSON como formato de serialização de saudação. De uma perspectiva de interface, trata-se adotar a abordagem de design de web hello. Mas nada o impede de usar protocolos binários ou seus próprios formatos de dados. Esteja preparado para pessoas toohave vez mais difícil usando seu microservices se eles forem está disponíveis.

### <a name="has-a-unique-name-url-used-tooresolve-its-location"></a>Tem um nome exclusivo (URL) usado tooresolve seu local
Lembre-se de como podemos manter informando que abordagem de microsserviço hello como Olá web? Como Olá web seu microsserviço necessita toobe endereçável independentemente de onde ele está em execução. Se você ficar pensando em máquinas, e qual delas está executando um determinado microsserviço, as coisas vão dar errado rapidamente. 

Olá mesma maneira que DNS resolve um determinado computador específico do URL tooa, seu microsserviço precisa toohave um nome exclusivo para que seu local atual é detectável. Microservices necessário endereçável nomes que os tornam independente da infraestrutura de saudação que estão sendo executados em. Isso significa que há uma interação entre como seu serviço é implantado e como ele será descoberto, porque deve toobe um registro de serviço. Igualmente, quando uma máquina falhar, o serviço de registro Olá deve informar onde o serviço de hello está sendo executado. 

Isso traz toohello próximo tópico: resiliência e a consistência.

### <a name="remains-consistent-and-available-in-hello-presence-of-failures"></a>Permaneça consistente e disponíveis na presença de saudação de falhas
Lidar com falhas inesperadas é uma saudação mais difíceis problemas toosolve, especialmente em um sistema distribuído. Grande parte do código Olá escrevemos como os desenvolvedores de tratamento de exceções, e isso também é onde hello maior parte do tempo é gasto no teste. problema de saudação é mais envolvido que escrever código toohandle falhas. O que acontece quando ocorre falha na máquina Olá onde Olá microsserviço está em execução? Não só precisar toodetect essa falha de microsserviço (um problema de disco rígido em seu próprio), mas você também precisa de algo toorestart seu microsserviço. 

Um microsserviço precisa toofailures resiliente toobe e reinicie geralmente em outra máquina, por motivos de disponibilidade. Isso também se resume toohello estado que foi salvo em nome de microsserviço hello, onde microsserviço Olá pode recuperar esse estado de, e se microsserviço Olá é capaz de toorestart com êxito. Em outras palavras, preciso toobe resiliência em computação hello (Olá reinícios do processo), bem como a resiliência em estado de saudação ou dados (sem perda de dados, os dados Olá permanecem consistentes).

problemas de saudação de resiliência são abordados durante a outros cenários, como quando falhas ocorrem durante uma atualização do aplicativo. Olá microsserviço, trabalhando com o sistema de implantação hello, não precisará toorecover. Ele também precisa toothen decidir se ele pode continuar a versão mais recente do toomove toohello direta ou em vez disso, reverter tooa anterior versão toomaintain um estado consistente. Perguntas sobre como se máquinas suficientes são tookeep disponível no futuro e como toorecover de versões anteriores do microsserviço Olá necessário toobe considerado. Isso requer Olá microsserviço tooemit integridade informações toobe capaz de toomake essas decisões.

### <a name="reports-health-and-diagnostics"></a>Relatórios de integridade e diagnóstico
Pode parecer óbvio, e muitas vezes isso é negligenciado, mas um microsserviço deve relatar sua integridade e diagnóstico. Caso contrário, há pouca percepção de uma perspectiva de operações. Correlacionar eventos de diagnóstico em um conjunto de serviços independentes e lidar com desvios de relógio do computador toomake sentido de ordem de eventos de saudação é um desafio. Em Olá formatos da mesma maneira que você interaja com um microsserviço sobre dados e protocolos estabelecido, há surge a necessidade de padronização em como toolog integridade e eventos de diagnóstico que, por fim, terminam em um evento armazenam para consultar e exibir. Em uma abordagem de microsserviços, é importante que diferentes equipes concordem com um único formato de registro em log. Deve toobe uma abordagem consistente tooviewing diagnóstico eventos aplicativo hello como um todo.

Integridade é diferente de diagnóstico. Integridade é sobre Olá microsserviço reporting seus atual estado tootake as ações apropriadas. Um bom exemplo está trabalhando com a disponibilidade de toomaintain de mecanismos de implantação e atualização. Embora um serviço pode ser Íntegro no momento devido a falha no processo tooa ou reinicialização do computador, serviço Olá ainda pode estar operacional. Olá última coisa é toomake este pior executando uma atualização. Olá melhor abordagem é toodo uma investigação pela primeira vez ou aguarde até que Olá microsserviço toorecover. Os eventos de integridade de um microsserviço permitem tomar decisões bem informadas e ajudam realmente a criar serviços que recuperam a si próprios.

## <a name="service-fabric-as-a-microservices-platform"></a>Service Fabric como uma plataforma de microsserviço
Azure Service Fabric surgiu uma transição pela Microsoft do fornecimento de produtos de caixa, que foram normalmente monolíticos no estilo, toodelivering serviços. experiência de saudação de criar e operar serviços grandes, como o banco de dados do SQL Azure e banco de dados do Azure Cosmos, em forma de malha do serviço. plataforma de saudação desenvolvidos ao longo do tempo conforme mais e mais serviços adotaram. É importante, Service Fabric tinha toorun não apenas no Azure, mas também em implantações do Windows Server autônomo.

***objetivo de saudação do Service Fabric é toosolve problemas de disco rígido de saudação da criação e execução de um serviço e utilizar recursos de infraestrutura com eficiência, para que as equipes podem resolver problemas de negócios usando uma abordagem de microservices.***

Serviço de malha fornece três áreas amplas toohelp criar aplicativos que usam uma abordagem microservices:

* Uma plataforma que oferece toodeploy de serviços do sistema, atualizar, detectar, reinicie os serviços com falha, descobrir serviços, rotear mensagens, gerenciar o estado e monitorar a integridade. Esses serviços de sistema em vigor permitem que muitas das características de saudação do microservices descrito anteriormente.
* Aplicativos de toodeploy capacidade seja em execução em contêineres ou como processa. O Service Fabric é um orquestrador de contêiner e processo.
* APIs de programação produtivo, toohelp criar aplicativos como microservices: [ASP.NET Core, atores confiável e serviços confiáveis](service-fabric-choose-framework.md). Você pode escolher qualquer código toobuild seu microsserviço. Mas essas APIs que o trabalho de hello mais simples e integram-se com a plataforma de saudação em um nível mais profundo. Dessa forma, por exemplo, você pode obter informações de integridade e diagnóstico ou aproveitar a alta disponibilidade interna.

***O Service Fabric não se importa com o modo de criação de seu serviço, e você pode usar qualquer tecnologia. No entanto, ele oferece APIs de programação interno que o tornam mais fácil microservices de toobuild.***

### <a name="migrating-existing-applications-tooservice-fabric"></a>Migrando tooService aplicativos existentes do Fabric
TooService uma abordagem chave malha é o código existente tooreuse, que, em seguida, pode ser modernizado com microservices de novo. Há cinco estágios modernização tooapplication, e você pode iniciar e parar em qualquer um dos estágios de saudação. Estes são;

1) Colocar um aplicativo monolítico tradicional
2) Comparação de precisão e Shift - usar contêineres ou código existente do convidado executáveis toohost na malha do serviço.
3) Modernização - Novos microsserviços adicionados junto com o código em contêineres existente. 
4) Inovar - invadir Olá monolítico microservices puramente com base na necessidade.
5) Transformado em microservices - transformação Olá monolíticos aplicativos existentes ou criar novos aplicativos intacto.

![TooMicroservices de migração][Image3]

É importante tooemphasis novamente, que você pode **iniciar e parar em qualquer um desses estágios**, você não estiver interessado toomoved toohello próximo estágio. Agora vamos ver exemplos de cada um desses estágios.

**Comparar e deslocar** - grandes números de empresas são levantar e deslocamento monolíticos aplicativos em contêineres toofor dois motivos;

- Redução de custos devido a tooconsolidation e remoção de aplicativos existentes de hardware ou executando a densidade mais alta. 
- Contrato de implantação consistente entre o desenvolvimento e as operações.

Reduções de custos possam ser compreendidas e dentro da Microsoft estão sendo grandes números de aplicativos existentes em contêineres simplesmente toomillions de dólares. Implantação consistente é mais difícil tooevaluate, mas igualmente importantes. Ele diz que os desenvolvedores podem ainda ser toochoose livre Olá tecnologia que pacotes-los, no entanto, operações de saudação somente aceitará toodeploy um modo único e gerenciar esses aplicativos. Minimiza operações Olá tenham toodeal com complexidade Olá das muitas tecnologias diferentes ou fazer com que os desenvolvedores tooonly escolha algumas. Essencialmente, cada aplicativo está em contêineres em imagens de implantação independentes.

Muitas organizações param aqui. Já tenham benefícios de saudação de contêineres e Service Fabric fornece experiência de gerenciamento completo de saudação de implantação, atualizações, controle de versão, reversões, etc de monitoramento de integridade.

**Modernização** -é Olá adição de novos serviços junto com o código em contêineres existente. Se você for novo código de toowrite, é melhor toodecide tootake pequenas etapas para caminho de microservices hello. Isso pode adicionar um novo ponto de extremidade de API REST ou uma nova lógica de negócios. Dessa forma, inicie em jornada de saudação do microservices nova construção e práticas de desenvolvimento e implantá-los.

**Inovar** -Lembre-se essas original alteração necessidades de negócios no início de saudação deste artigo, que determinam a abordagem de microservices Olá? Em Olá este estágio decisão é, são aconteça toomy atual aplicativo e nesse caso, eu preciso toostart dividir monolito hello, ou inovando. Um exemplo aqui é quando um banco de dados se torna um afunilamento de processamento, pois ele está sendo usado como uma fila de fluxo de trabalho. Como o número de saudação do fluxo de trabalho solicitações aumentando Olá funcionam necessidades toobe distribuída de escala. Portanto para esta parte específica do aplicativo hello que não está sendo reduzido, ou você precisa tooupdate mais frequentemente, isso dividir um microsserviço e a inovem. 

**Transformado em microsserviços** - é quando o aplicativo é totalmente composto de (ou decomposto em) microsserviços. tooreach aqui, você fez jornada de microservices hello. Você pode iniciar aqui, mas toodo isso sem um toohelp de plataforma microservices é um investimento significativo. 

### <a name="are-microservices-right-for-my-application"></a>Os microsserviços são ideais para meu aplicativo?
Talvez. O que enfrentamos era conforme mais e mais equipes da Microsoft começaram toobuild para nuvem Olá por motivos comerciais, muitas delas percebida benefícios de saudação do adotando uma abordagem semelhante de microsserviço. O Bing, por exemplo, vem desenvolvendo os microsserviços em pesquisa por anos. Para outras equipes, abordagem de microservices Olá era nova. As equipes encontrado que não houve problemas de disco rígido toosolve fora de suas áreas de núcleo de força. É por isso Service Fabric obtido tração como Olá tecnologia de sua preferência para criar serviços.

Olá objetivo do Service Fabric é tooreduce complexidades de saudação da criação de aplicativos com uma abordagem de microsserviço, para que você não tenha toogo por meio de como muitos cara redesigns. Comece pequeno, dimensionar quando necessário, substituir os serviços, adicionar novos e evoluir com cliente uso é a abordagem de saudação. Também sabemos que há muitos outros problemas toobe resolvido toomake microservices mais acessível para a maioria dos desenvolvedores. Contêineres e modelo de programação de ator Olá são exemplos de etapas pequenas nessa direção, e temos certeza de que mais inovações vão surgir toomake isso mais fácil.
 
<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a>Próximas etapas
* [Visão geral da terminologia do Service Fabric](service-fabric-technical-overview.md)
* [Microservices: Uma revolução de aplicativo com a nuvem Olá](https://azure.microsoft.com/en-us/blog/microservices-an-application-revolution-powered-by-the-cloud/)

[Image1]: media/service-fabric-overview-microservices/monolithic-vs-micro.png
[Image2]: media/service-fabric-overview-microservices/statemonolithic-vs-micro.png
[Image3]: media/service-fabric-overview-microservices/microservices-migration.png
