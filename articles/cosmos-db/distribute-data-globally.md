---
title: dados de aaaDistribute global com o banco de dados do Azure Cosmos | Microsoft Docs
description: "Saiba mais sobre replicação geográfica em escala mundial, failover e recuperação de dados usando bancos de dados globais no Azure Cosmos DB, um serviço de multimodelo de banco de dados distribuído globalmente."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: ba5ad0cc-aa1f-4f40-aee9-3364af070725
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/14/2017
ms.author: arramac
ms.openlocfilehash: b50e8433dc7e70c54d68c4c2f99954a13f4951f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodistribute-data-globally-with-azure-cosmos-db"></a>Como os dados de toodistribute global com o banco de dados do Azure Cosmos
O Azure é onipresente: ele tem uma superfície global que abrange mais de 30 regiões geográficas e aumenta continuamente. Com sua presença em todo o mundo, um dos recursos de saudação diferenciado que Azure oferece aos desenvolvedores de tooits é Olá toobuild de capacidade, implantar e gerenciar aplicativos distribuídos globalmente facilmente. 

O [Azure Cosmos DB](../cosmos-db/introduction.md) é o serviço multimodelo de banco de dados da Microsoft, distribuído globalmente, para aplicativos críticos. Banco de dados do Azure Cosmos fornece distribuição global e completa, [dimensionamento Elástico de taxa de transferência e armazenamento](../cosmos-db/partition-data.md) latências de milissegundo em todo o mundo, dígito no percentual de 99th hello, [cinco níveis de consistência bem definidos ](consistency-levels.md)e a garantia de alta disponibilidade, apoiada por [SLAs do setor](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Banco de dados do Azure Cosmos [indexa automaticamente os dados](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) sem exigir que você toodeal com o gerenciamento de esquema e de índice. Ele tem vários modelos e suporta modelos de dados de colunas, gráficos, valores-chave e documentos. Como um serviço de nuvem, o banco de dados do Azure Cosmos cuidadosamente foi projetado com distribuição multilocação e global de saudação o plano de.

**Uma única coleção do Azure Cosmos DB particionada e distribuída em várias regiões do Azure**

![Coleção do Azure Cosmos DB particionada e distribuída em três regiões](./media/distribute-data-globally/global-apps.png)

Como aprendemos durante a criação do Azure Cosmos DB, a adição da distribuição global não pode ser uma consideração posterior: ela não pode ser “forçada” em um sistema de banco de dados de “site único”. recursos de Olá oferecidos por um banco de dados globalmente distribuído se estender além de que, de desastres geográficos tradicional recuperação (Geo-DR) oferecidos pelos bancos de dados do "site único". Bancos de dados de site único que oferecem a capacidade de Geo-DR são um subconjunto restrito de bancos de dados distribuídos globalmente. 

Com a distribuição de global completa do Azure Cosmos DB, os desenvolvedores não têm toobuild seu próprios scaffolding de replicação empregando um padrão de Lambda hello (por exemplo, [DynamoDB AWS replicação](https://github.com/awslabs/dynamodb-cross-region-library/blob/master/README.md)) sobre o log de banco de dados de saudação ou por fazendo "gravações duplas" em várias regiões. Não recomendamos essas abordagens porque é impossível tooensure exatidão essas abordagens e fornecer os SLAs de som. 

Neste artigo, apresentamos uma visão geral das funcionalidades de distribuição global do Azure Cosmos DB. Também descrevemos tooproviding de abordagem exclusiva do Azure Cosmos DB SLAs abrangentes. 

## <a id="EnableGlobalDistribution"></a>Habilitando a distribuição global turnkey
Banco de dados do Azure Cosmos fornece o seguinte Olá recursos tooenable tooeasily você escrever aplicativos de escala do planeta. Esses recursos estão disponíveis por meio do recurso do hello Azure Cosmos DB baseados em provedor [APIs REST](https://docs.microsoft.com/rest/api/documentdbresourceprovider/) , bem como Olá portal do Azure.

### <a id="RegionalPresence"></a>Presença regional em todos os lugares 
O Azure está constantemente expandindo sua presença geográfica colocando [novas regiões](https://azure.microsoft.com/regions/) online. O Azure Cosmos DB está disponível em todas as novas regiões do Azure por padrão. Isso permite que você tooassociate uma região geográfica com sua conta de banco de dados do banco de dados do Azure Cosmos como Azure abre a nova região hello para empresas.

**O Azure Cosmos DB está disponível em todas as regiões do Azure por padrão**

![Azure Cosmos DB disponível em todas as regiões do Azure](./media/distribute-data-globally/azure-regions.png)

### <a id="UnlimitedRegionsPerAccount"></a>Associando um número ilimitado de regiões à sua conta de banco de dados do Azure Cosmos DB
Banco de dados do Azure Cosmos permite que você tooassociate qualquer número de regiões do Azure com seu banco de dados do Azure Cosmos conta de banco de dados. Fora de restrições de isolamento geográfico (por exemplo, China, Alemanha), não há nenhuma limitação no número de saudação de regiões que pode ser associado à sua conta de banco de dados do banco de dados do Azure Cosmos. Olá figura a seguir mostra um toospan de conta configurada do banco de dados em 25 regiões do Azure.  

**Conta de banco de dados do Azure Cosmos DB de um locatário abrangendo 25 regiões do Azure**

![Conta de banco de dados do Azure Cosmos DB abrangendo 25 regiões do Azure](./media/distribute-data-globally/spanning-regions.png)

### <a id="PolicyBasedGeoFencing"></a>Isolamento geográfico baseado em políticas
Banco de dados do Azure Cosmos é toohave projetado com base na política geográfico recursos. Geoinstalação é um componente importante tooensure restrições de governança e conformidade de dados e pode impedir a associação de uma região específica com sua conta. Exemplos de isolamento geográfico incluem (mas não está restritos a), escopo regiões toohello de distribuição global em uma nuvem soberana (por exemplo, China e na Alemanha) ou dentro de um limite de tributação governo (por exemplo, Austrália). políticas de saudação são controladas usando metadados de saudação da sua assinatura do Azure.

### <a id="DynamicallyAddRegions"></a>Adicionar e remover regiões dinamicamente
Banco de dados do Azure Cosmos permite que você tooadd (associação) ou remova (dissociar) conta de banco de dados de tooyour regiões em qualquer ponto no tempo (consulte [Figura precedente](#UnlimitedRegionsPerAccount)). Em virtude de replicar dados entre partições em paralelo, o banco de dados do Azure Cosmos garante que quando uma nova região de fica online, banco de dados do Azure Cosmos está disponível dentro de 30 minutos em qualquer lugar no Olá, mundo para backup too100 TB. 

### <a id="FailoverPriorities"></a>Prioridades de failover
a sequência exata toocontrol de failovers regional quando houver uma interrupção de várias regiões, o banco de dados do Azure Cosmos permite que você as regiões de toovarious prioridade Olá tooassociate associadas à conta do banco de dados de saudação (consulte Olá figura a seguir). Banco de dados do Azure Cosmos garante que sequência do hello failover automático ocorre em ordem de prioridade de saudação especificado. Para obter mais informações sobre failovers regionais, consulte [Failovers regionais automáticos para continuidade dos negócios no Azure Cosmos DB](regional-failover.md).

**Um locatário do banco de dados do Azure Cosmos pode configurar a ordem de prioridade de failover de saudação (painel direito) para regiões associados com uma conta de banco de dados**

![Configurando prioridades de failover com o Azure Cosmos DB](./media/distribute-data-globally/failover-priorities.png)

### <a id="OfflineRegions"></a>Colocando uma região "offline" dinamicamente
Banco de dados do Azure Cosmos permite que você tootake seu banco de dados da conta offline em uma região específica e colocá-lo online novamente mais tarde. Regiões marcado como offline não ativamente participar da replicação e não fazem parte da sequência de failover de saudação. Isso permite que você toofreeze Olá conhecido última imagem do banco de dados válida em uma saudação ler regiões antes de implantar potencialmente perigoso atualiza o aplicativo de tooyour.

### <a id="ConsistencyLevels"></a>Vários modelos de consistência bem definidos para bancos de dados replicados globalmente
O Azure Cosmos DB expõe [vários níveis de consistência bem definidos](consistency-levels.md) com suporte de SLAs. Você pode escolher um modelo de consistência específicas (da lista Olá de opções) dependendo da carga de trabalho/cenários hello. 

### <a id="TunableConsistency"></a>Consistência ajustável para bancos de dados replicados globalmente
Banco de dados do Azure Cosmos permite substituir tooprogrammatically e relaxe a opção de consistência saudação padrão em uma base por solicitação, em tempo de execução. 

### <a id="DynamicallyConfigurableReadWriteRegions"></a>Regiões de leitura e gravação configuráveis dinamicamente
Banco de dados do Azure Cosmos permite que você tooconfigure regiões de saudação (associados com o banco de dados de saudação) para "leitura", "gravação" ou "leitura/gravação" regiões. 

### <a id="ElasticallyScaleThroughput"></a>Dimensionando a taxa de transferência com elasticidade entre regiões do Azure
Você pode dimensionar de modo elástico uma coleção do Azure Cosmos DB provisionando a produtividade de forma programática. taxa de transferência de saudação é aplicado tooall regiões de Olá coleção Olá é distribuída no.

### <a id="GeoLocalReadsAndWrites"></a>Leituras e gravações geograficamente locais
Olá principal benefício de um banco de dados globalmente distribuído é toooffer baixa latência acessar toohello dados em qualquer lugar em Olá, mundo. O Azure Cosmos DB oferece garantias de baixa latência em P99 para várias operações de banco de dados. Isso garante que todas as leituras são roteadas toohello região de leitura de local mais próximo. tooserve uma solicitação de leitura, região de toohello local quorum Olá no qual Olá ler é emitido é usado; Olá mesmo se aplica toohello gravações. Uma gravação ser confirmada somente depois que a maioria das réplicas de forma duradoura comprometeu gravação da saudação localmente, mas sem sendo concedido em réplicas remotas tooacknowledge Olá gravações. Protocolo de replicação de saudação do banco de dados do Azure Cosmos colocar de maneira diferente, opera em suposição Olá Olá leitura e gravação quorums sempre são toohello local ler e gravar regiões, respectivamente, no qual solicitação Olá é emitida.

### <a id="ManualFailover"></a>Iniciar manualmente o failover regional
Banco de dados do Azure Cosmos permite que você tootrigger Olá failover de Olá Olá de toovalidate de conta de banco de dados *terminar tooend* propriedades de disponibilidade de todo o aplicativo hello (além do banco de dados de saudação). Como ambos Olá segurança e têm a garantia de propriedades de execução de eleição de preenchimento e detecção de falha hello, o banco de dados do Azure Cosmos garante *zero perda de dados* para uma operação de failover manual iniciada pelo locatário.

### <a id="AutomaticFailover"></a>Failover automático
O Azure Cosmos DB dá suporte ao failover automático no caso de uma ou mais interrupções regionais. Durante um failover regional, o Azure Cosmos DB mantém seus SLAs de latência de leitura, disponibilidade de tempo de atividade, consistência e produtividade. Banco de dados do Azure Cosmos fornece um limite superior na duração de saudação de um toocomplete da operação de failover automático. Esta é a janela de saudação potencial de perda de dados durante a interrupção regional hello.

### <a id="GranularFailover"></a>Projetado para diferentes granularidades de failover
Olá atualmente automáticas e recursos de failover manual são expostos na granularidade de saudação de conta de banco de dados de saudação. Observe que, internamente o Azure Cosmos DB é projetado toooffer *automáticas* failover em uma granularidade maior de um banco de dados, conjunto ou até mesmo uma partição (de uma coleção que possui um intervalo de chaves). 

### <a id="MultiHomingAPIs"></a>APIs de hospedagem múltipla no Azure Cosmos DB
Banco de dados do Azure Cosmos permite toointeract com banco de dados de saudação usando lógica (independente de região) ou pontos de extremidade físicos (região específico). Usando pontos de extremidade lógicos garante que aplicativo hello pode transparentemente multihomed no caso de failover. Olá pontos de extremidade físicos, este último, fornecer controle refinado toohello aplicativo tooredirect leituras e gravações toospecific regiões.

Você pode encontrar informações sobre como tooconfigure ler preferências para Olá [API DocumentDB](../cosmos-db/tutorial-global-distribution-documentdb.md), [API do Graph](../cosmos-db/tutorial-global-distribution-graph.md), [API tabela](../cosmos-db/tutorial-global-distribution-table.md), e [MongoDB API](../cosmos-db/tutorial-global-distribution-mongodb.md)em suas respectivas vinculados artigos.

### <a id="TransparentSchemaMigration"></a>Migração de esquema e de índice de banco de dados transparente e consistente 
O Azure Cosmos DB é totalmente [independente de esquema](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf). design exclusivo de saudação de seu mecanismo de banco de dados permite que ele tooautomatically e sincronicamente índice todos os dados de saudação ele consome sem a necessidade de qualquer esquema ou os índices secundários por você. Isso permite que você tooiterate seu aplicativo distribuído globalmente rapidamente sem se preocupar sobre migração de esquema e de índice de banco de dados ou coordenar a implantação de aplicativos de várias fases de alterações de esquema. Banco de dados do Azure Cosmos garante que as políticas de tooindexing alterações explicitamente feitas por você não resultar em degradação de desempenho ou disponibilidade.  

### <a id="ComprehensiveSLAs"></a>SLAs abrangentes (além de apenas alta disponibilidade)
Como um serviço de banco de dados globalmente distribuído, o banco de dados do Azure Cosmos oferece SLA bem definido para **perda de dados**, **disponibilidade**, **latência em P99**, **taxa de transferência**  e **consistência** para banco de dados hello como um todo, independentemente do número Olá das regiões associados Olá banco de dados.  

## <a id="LatencyGuarantees"></a>Garantias de latência
Olá principal benefício de um serviço de banco de dados globalmente distribuído como o banco de dados do Azure Cosmos é toooffer baixa latência acessar tooyour dados em qualquer lugar em Olá, mundo. O Azure Cosmos DB oferece baixa latência garantida a P99 para várias operações de banco de dados. protocolo de replicação de saudação que utiliza o banco de dados do Azure Cosmos garante que Olá operações de banco de dados (de preferência, as leituras e gravações) sempre são executadas na toothat local de região de saudação do cliente de saudação. latência de saudação para que SLA do Azure Cosmos DB inclui P99 leituras e gravações (de forma síncrona) indexadas e consultas para vários tamanhos de solicitação e resposta. Olá garantias de latência para gravações incluem confirmações de quorum de maioria durável dentro do datacenter local hello.

### <a id="LatencyAndConsistency"></a>Relação da latência com a consistência 
Para obter uma serviço distribuído globalmente toooffer forte consistência em uma instalação distribuída globalmente, ele precisa toosynchronously Olá replicar gravações síncronas ou executar entre regiões leituras – velocidade de saudação do claro e Olá ditam de confiabilidade rede de longa distância uma coerência forte resulta em latências de alta e baixa disponibilidade de operações de banco de dados. Portanto, em ordem toooffer de garantia de latências de baixas P99 e disponibilidade 99.99, serviço Olá deve empregar replicação assíncrona. Na curva requer que o serviço Olá também deve oferecer [choice(s) consistência bem definidos, reduzida](consistency-levels.md) – mais fraca do que forte (toooffer baixa latência e disponibilidade garantias) e o ideal é mais seguro do que "eventual" consistência ( toooffer um modelo de programação intuitivo).

Banco de dados do Azure Cosmos garante que uma operação de leitura não seja necessário toocontact réplicas em várias regiões toodeliver Olá específico nível garantia de consistência. Da mesma forma, ele garante que uma operação de gravação não obter bloqueada enquanto dados hello está sendo replicados em todas as regiões hello (ou seja, as gravações são replicadas de maneira assíncrona em regiões). Para contas de banco de dados de várias regiões, estão disponíveis vários níveis de consistência reduzida. 

### <a id="LatencyAndAvailability"></a>Relação da latência com a disponibilidade 
A latência e disponibilidade são dois lados Olá Olá mesmo tipo de moeda. Falamos sobre a latência da operação de saudação no estado estável e disponibilidade em face de saudação de falhas. Do ponto de vista de aplicativo hello, uma operação de banco de dados em execução lenta é indistinguível de um banco de dados que não está disponível. 

toodistinguish alta latência de indisponibilidade do banco de dados do Azure Cosmos fornece um limite absoluto na latência de várias operações de banco de dados. Se a operação de banco de dados de saudação demora mais do que toocomplete de limite superior Olá, o banco de dados do Azure Cosmos retornará um erro de tempo limite. Olá SLA de disponibilidade do banco de dados do Azure Cosmos garante que tempos limite de saudação são contados no SLA de disponibilidade de saudação. 

### <a id="LatencyAndThroughput"></a>Relação da latência com a taxa de transferência
O Azure Cosmos DB não o obriga a escolher entre latência e produtividade. Ele respeita Olá SLA para ambos os latência em P99 e entregar a taxa de transferência Olá provisionada por você. 

## <a id="ConsistencyGuarantees"></a>Garantias de consistência
Durante a saudação [modelo de consistência forte](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf) é Olá ouro padrão de programação, que se trata a preço acentuada de saudação de alta latência (no estado estável) e a perda de disponibilidade (em face de saudação de falhas). 

Banco de dados do Azure Cosmos oferece um tooreason bem definido de programação do tooyou modelo sobre a consistência dos dados replicados. Em ordem tooenable você toobuild multihomed aplicativos, modelos de consistência Olá expostos pelo banco de dados do Azure Cosmos são independentes de região toobe projetado e não dependem de região Olá de onde Olá leituras e gravações são atendidas. 

SLA de consistência do Azure Cosmos DB garante que 100% de solicitações de leitura atenderá a garantia de consistência Olá para o nível de consistência Olá solicitado por vocês o (saudação padrão nível de consistência na conta de banco de dados de saudação ou valor Olá substituído na solicitação de saudação ). Uma solicitação de leitura é considerada toohave atendido Olá consistência SLA se todas as garantias de consistência Olá associadas ao nível de consistência Olá forem atendidas. Olá tabela a seguir captura as garantias de consistência de saudação que correspondem a níveis de consistência toospecific oferecidos pelo Azure Cosmos DB.

**Garantias de consistência associadas a um nível de consistência específico do Azure Cosmos DB**

<table>
    <tr>
        <td><strong>Nível de Consistência</strong></td>
        <td><strong>Características de Consistência</strong></td>
        <td><strong>SLA</strong></td>
    </tr>
    <tr>
        <td rowspan="3">Session</td>
        <td>Ler sua própria gravação</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Leitura monotônica</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Prefixo consistente</td>
        <td>100%</td>
    </tr>
    <tr>
        <td rowspan="3">Bounded staleness</td>
        <td>Leitura monotônica (em uma região)</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Prefixo consistente</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Desatualização limitada &lt; K,T</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Prefixo consistente</td>
        <td>Prefixo consistente</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Strong</td>
        <td>Linearizável</td>
        <td>100%</td>
    </tr>
</table>

### <a id="ConsistencyAndAvailability"></a>Relação de consistência com a disponibilidade
Olá [resultados impossibility](http://www.glassbeam.com/sites/all/themes/glassbeam/images/blog/10.1.1.67.6951.pdf) de saudação [Teorema de CAP](https://people.eecs.berkeley.edu/~brewer/cs262b-2004/PODC-keynote.pdf) prova que é realmente impossível Olá sistema tooremain disponível e a consistência de linearizable oferta em face de saudação de falhas. serviço de banco de dados de saudação deve escolher toobe CP ou PA - sistemas CP abrir mão de disponibilidade em favor de consistência linearizable enquanto sistemas Olá Pacífico abrir mão [linearizable consistência](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf) em favor de disponibilidade. Banco de dados do Azure Cosmos nunca viola Olá solicitou o nível de consistência, o que torna formalmente um sistema CP. No entanto, na prática consistência não é uma proposta de tudo ou nada – há vários modelos de consistência bem definido ao longo do espectro de consistência de saudação entre consistência eventual e linearizable. No banco de dados do Azure Cosmos, tentamos tooidentify vários Olá relaxada modelos de consistência com aplicabilidade do mundo real e um modelo de programação intuitivo. Banco de dados do Azure Cosmos navega compensações de disponibilidade de consistência Olá oferecendo 99.99 SLA de disponibilidade junto com [relaxada de vários níveis de consistência ainda bem definido](consistency-levels.md). 

### <a id="ConsistencyAndAvailability"></a>Relação da consistência com a latência
Uma variação mais abrangente do CAP foi proposta pelo Prof. Daniel Abadi e é chamado de [PACELC](http://cs-www.cs.yale.edu/homes/dna/papers/abadi-pacelc.pdf), abrangendo compensações de latência e consistência no estado estacionário. Ele declara que no estado estável, o sistema de banco de dados de saudação deve escolher entre consistência e a latência. Com vários modelos de consistência reduzida (apoiados por replicação assíncrona e local leitura, gravação quorums), o banco de dados do Azure Cosmos garante que todas as leituras e gravações são toohello local ler e gravar regiões respectivamente.  Isso permite que o banco de dados do Azure Cosmos toooffer baixa latência garante na região Olá para níveis de consistência de saudação.  

### <a id="ConsistencyAndThroughput"></a>Relação da consistência com a taxa de transferência
Como a implementação de saudação de um modelo de consistência específicas depende da escolha de saudação de um [tipo de quorum](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf), taxa de transferência Olá também varia com base na escolha de saudação de consistência. Por exemplo, no banco de dados do Azure Cosmos, hello taxa de transferência com leituras altamente consistentes é cerca de metade toothat de leituras finalmente consistentes. 
 
**Relação de capacidade de leitura para um nível de consistência específico no Azure Cosmos DB**

![Relação entre a consistência e a taxa de transferência](./media/distribute-data-globally/consistency-and-throughput.png)

## <a id="ThroughputGuarantees"></a>Garantias de taxa de transferência 
Banco de dados do Azure Cosmos permite que você tooscale taxa de transferência (bem como armazenamento), elasticidade em regiões diferentes, dependendo da demanda de saudação. 

**Uma única coleção do Azure Cosmos DB particionada (em três fragmentos) e, depois, distribuída em três regiões do Azure**

![Coleções distribuídas e particionadas do Azure Cosmos DB](../cosmos-db/media/introduction/azure-cosmos-db-global-distribution.png)

Uma coleção do Azure Cosmos DB é distribuída usando duas dimensões – em uma região e, depois, entre regiões. Faça assim: 

* Em uma única região, uma coleção do Azure Cosmos DB é escalada horizontalmente em termos de partições de recursos. Cada partição de recursos gerencia um conjunto de chaves e é altamente consistente e disponível em virtude da replicação da máquina de estado entre um conjunto de réplicas. Banco de dados do Azure Cosmos é um sistema de recursos administrados totalmente onde uma partição de recurso é responsável por fornecer sua parcela da taxa de transferência para o orçamento de saudação do sistema recursos alocados tooit. Olá dimensionamento de uma coleção de banco de dados do Azure Cosmos é completamente transparente – Azure Cosmos DB gerencia as partições de recurso hello e divisões e mescla conforme necessário. 
* Cada partição de recurso hello, em seguida, é distribuída entre várias regiões. Partições de recurso possui Olá mesmo conjunto de chaves em várias regiões formulário partição conjunto (consulte [Figura precedente](#ThroughputGuarantees)).  As partições de recursos dentro de um conjunto de partições são coordenadas com o uso de replicação da máquina de estado entre Olá várias regiões. Dependendo do nível de consistência de saudação configurado, partições de recursos hello dentro de um conjunto de partições são configuradas dinamicamente usando topologias diferentes (por exemplo, estrela, cascata, árvore etc.). 

Em virtude de um gerenciamento de partição altamente responsivo, balanceamento de carga e governança de recursos estrito, banco de dados do Azure Cosmos permite que você tooelastically throughput de escala em várias regiões do Azure em uma coleção de banco de dados do Azure Cosmos. Alteração de taxa de transferência em uma coleção é uma operação de tempo de execução no banco de dados do Azure Cosmos – como com outras operações de banco de dados do Azure Cosmos DB garante Olá absoluto limite latência para a taxa de transferência solicitação toochange hello. Por exemplo, Olá figura a seguir mostra o coleção do cliente com elasticidade provisionada taxa de transferência (em duas regiões, variando de 1 milhão - 10M solicitações/s) com base na demanda de saudação.
 
**Coleção de um cliente com taxa de transferência provisionada com elasticidade (1 M - 10 M solicitações/s)**

![Produtividade provisionada de modo elástico do Azure Cosmos DB](./media/distribute-data-globally/elastic-throughput.png)

### <a id="ThroughputAndConsistency"></a>Relação da taxa de transferência com a consistência 
O mesmo que [Relação entre a consistência e a taxa de transferência](#ConsistencyAndThroughput).

### <a id="ThroughputAndAvailability"></a>Relação entre a taxa de transferência e a disponibilidade
Banco de dados do Azure Cosmos continua toomaintain sua disponibilidade ao fazer alterações de saudação toohello taxa de transferência. Banco de dados do Azure Cosmos partições (por exemplo, dividir, mesclagem, operações de clonagem) gerencia de forma transparente e garante que as operações de saudação não degradar o desempenho ou disponibilidade, enquanto o aplicativo hello elasticidade aumenta ou diminui a taxa de transferência. 

## <a id="AvailabilityGuarantees"></a>Garantia de disponibilidade
Banco de dados do Azure Cosmos oferece um SLA de disponibilidade de tempo de atividade 99,99% para cada Olá operações de plano de controle e de dados. Conforme descrito anteriormente, as garantias de disponibilidade do Azure Cosmos DB incluem um limite superior absoluto na latência para todas as operações de plano de controle e de dados. Olá garantias de disponibilidade são sólidas e não se alteram com o número de saudação de distância geográfica entre regiões ou regiões. As garantias de disponibilidade se aplicam ao failover manual e automático. Banco de dados do Azure Cosmos oferece APIs de hospedagem múltipla transparente que garantem que seu aplicativo pode operar em pontos de extremidade lógicos e transparente pode rotear Olá solicitações toohello nova região no caso de failover. Colocar de maneira diferente, seu aplicativo não precisa toobe reimplantado após o failover regional e disponibilidade Olá SLAs são mantidas.

### <a id="AvailabilityAndConsistency"></a>Relação entre a disponibilidade e a consistência, a latência e a taxa de transferência
A relação entre a disponibilidade e a consistência, a latência e a taxa de transferência é descrita em [Relação entre a consistência e a disponibilidade](#ConsistencyAndAvailability), [Relação entre a latência e a disponibilidade](#LatencyAndAvailability) e [Relação entre a taxa de transferência e a disponibilidade](#ThroughputAndAvailability). 

## <a id="GuaranteesAgainstDataLoss"></a>Garantias e comportamento do sistema para "perda de dados"
No Azure Cosmos DB, cada partição (de uma coleção) se torna altamente disponível por várias réplicas, que são distribuídas entre, pelo menos, 10 a 20 domínios de falha. Todas as gravações são sincronicamente e forma duradoura confirmadas por um quorum de maioria das réplicas antes de serem reconhecidos toohello cliente. A replicação assíncrona é aplicada com coordenação entre partições espalhadas por várias regiões. O Azure Cosmos DB garante que não há perda de dados para um failover manual iniciado pelo locatário. Durante o failover automático, o banco de dados do Azure Cosmos garante um limite superior de saudação configurado associado intervalo envelhecimento na janela de perda de dados hello como parte do seu SLA.

## <a id="CustomerFacingSLAMetrics"></a>Métricas de SLA voltadas para o cliente
Banco de dados do Azure Cosmos transparentemente expõe as métricas de taxa de transferência, a latência, a consistência e a disponibilidade de saudação. Essas métricas são acessíveis por meio de programação e via Olá portal do Azure (consulte a figura a seguir). Você também pode configurar alertas em vários limites usando o Azure Application Insights.
 
**Métricas de consistência, latência, taxa de transferência e disponibilidade são locatário tooeach transparentemente disponíveis**

![Métricas do SLA visíveis para o cliente do Azure Cosmos DB](./media/distribute-data-globally/customer-slas.png)

## <a id="Next Steps"></a>Próximas etapas
* replicação de tooimplement global na sua conta de banco de dados do Azure Cosmos usando hello Azure portal, consulte [como tooperform replicação de banco de dados global de banco de dados do Azure Cosmos usando Olá portal do Azure](tutorial-global-distribution-documentdb.md).
* toolearn sobre como tooimplement arquiteturas de vários mestres com Azure Cosmos DB, consulte [arquiteturas de banco de dados de vários mestres com o banco de dados do Azure Cosmos](multi-region-writers.md).
* toolearn mais sobre como trabalhar de failovers automáticos e manuais no banco de dados de Cosmos do Azure, consulte [Failovers regionais no banco de dados do Azure Cosmos](regional-failover.md).

## <a id="References"></a>Referências
1. Eric Brewer. [Para garantir sistemas distribuídos robustos](https://people.eecs.berkeley.edu/~brewer/cs262b-2004/PODC-keynote.pdf)
2. Eric Brewer. [LIMITE de 12 anos mais tarde – como regras Olá foram alterados](http://informatik.unibas.ch/fileadmin/Lectures/HS2012/CS341/workshops/reportsAndSlides/PresentationKevinUrban.pdf)
3. Gilbert, Lynch. - [Brewer&#39;s Conjecture and Feasibility of Consistent, Available, Partition Tolerant Web Services](http://www.glassbeam.com/sites/all/themes/glassbeam/images/blog/10.1.1.67.6951.pdf) (Conjectura e viabilidade de serviços Web tolerantes a partição consistentes e disponíveis)
4. Daniel Abadi. [Consistency Tradeoffs in Modern Distributed Database Systems Design](http://cs-www.cs.yale.edu/homes/dna/papers/abadi-pacelc.pdf) (Compensações de consistência no projeto de sistemas de bancos de dados modernos distribuídos)
5. Martin Kleppmann. [Please stop calling databases CP or AP](https://martin.kleppmann.com/2015/05/11/please-stop-calling-databases-cp-or-ap.html) (Pare de chamar bancos de dados de CP ou AP)
6. Peter Bailis et al. [Probabilistic Bounded Staleness (PBS) for Practical Partial Quorums](http://vldb.org/pvldb/vol5/p776_peterbailis_vldb2012.pdf) (PBS (Probabilistic Bounded Staleness) para quóruns parciais práticos)
7. Naor e Wool. [Load, Capacity and Availability in Quorum Systems](http://www.cs.utexas.edu/~lorenzo/corsi/cs395t/04S/notes/naor98load.pdf) (Carga, capacidade e disponibilidade em sistemas de quorum)
8. Herlihy e Wing. [Lineralizability: A correctness condition for concurrent objects](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf) (Linearidade: uma condição de correção para objetos simultâneos)
9. [SLA do Azure Cosmos DB](https://azure.microsoft.com/support/legal/sla/cosmos-db/)
