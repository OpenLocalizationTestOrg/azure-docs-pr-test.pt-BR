---
title: "níveis de aaaConsistency no banco de dados do Azure Cosmos | Microsoft Docs"
description: "Banco de dados do Azure Cosmos tem cinco consistência níveis toohelp saldo eventual consistência, disponibilidade e latência de vantagens e desvantagens."
keywords: "consistência eventual, azure cosmos db, Microsoft azure"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: cgronlun
documentationcenter: 
ms.assetid: 3fe51cfa-a889-4a4a-b320-16bf871fe74c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac399c229d0856cd811bc81568536e519af3300f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tunable-data-consistency-levels-in-azure-cosmos-db"></a>Níveis ajustáveis de consistência de dados no Azure Cosmos DB
Banco de dados do Azure Cosmos destina-se da saudação Terra com distribuição global em mente para cada modelo de dados. É projetado toooffer garantias de baixa latência previsível, um SLA de disponibilidade de 99,99%, e vários bem-definidos relaxada modelos de consistência. Atualmente, o Azure Cosmos DB fornece cinco níveis de consistência: forte, desatualização limitada, sessão, prefixo consistente e eventual. 

Além dos modelos de consistência **forte** e **eventual** geralmente oferecidos por bancos de dados distribuídos, o Azure Cosmos DB oferece mais três modelos de consistência cuidadosamente codificados e operacionalizados, e validou sua utilidade em casos de uso do mundo real. Esses são Olá **limitada envelhecimento**, **sessão**, e **prefixo consistente** níveis de consistência. Esses níveis de cinco consistência habilitar coletivamente toomake bem fundamentada prós e contras latência, a disponibilidade e a consistência. 

## <a name="distributed-databases-and-consistency"></a>Consistência e bancos de dados distribuídos
Os bancos de dados distribuídos comercialmente se enquadram em duas categorias: bancos de dados que não oferecem opções de consistência bem definidas e comprovadas e bancos de dados que oferecem duas opções de programação extrema (consistência forte versus consistência eventual). 

Olá os desenvolvedores de aplicativos de carga anterior com detalhes de seus protocolos de replicação e esperada compensações de difícil toomake entre consistência, disponibilidade, latência e taxa de transferência. Olá último coloca um toochoose pressão um dos dois extremos de saudação. Apesar infinidade de saudação de pesquisa e propostas para mais de 50 modelos de consistência, hello comunidade do banco de dados distribuído não foi capaz de toocommercialize níveis de consistência além da consistência eventual e forte. Cosmos banco de dados permite que os desenvolvedores toochoose entre cinco modelos de consistência bem definido ao longo do espectro de consistência hello – forte, limitada envelhecimento, [sessão](http://dl.acm.org/citation.cfm?id=383631), prefixo consistente e eventual. 

![Banco de dados do Azure Cosmos oferece vários bem definidas (reduzida) consistência modelos toochoose do](./media/consistency-levels/five-consistency-levels.png)

Olá a tabela a seguir ilustra as garantias específico hello, que cada nível de consistência fornece.
 
**Níveis de consistência e garantias**

| Nível de Consistência | Garantias |
| --- | --- |
| Strong | Transação atômica |
| Bounded staleness | Prefixo consistente. Lê latência por trás de gravações por meio de prefixos k ou intervalos t |
| Session   | Prefixo consistente. Leituras monotônicas, gravações monotônicas, read-your-writes (operações de leitura refletem gravações anteriores), write-follows-reads (gravações são propagadas após as leituras) |
| Prefixo consistente | Atualizações retornadas são alguns prefixo de todas as atualizações de hello sem intervalos |
| Eventual  | Leituras fora de ordem |

Você pode configurar o nível de consistência saudação padrão em sua conta do banco de dados do Cosmos (e posteriormente substituir consistência Olá em uma solicitação de leitura específica). Internamente, o nível de consistência saudação padrão se aplica a toodata em conjuntos de partições de saudação que pode abranger regiões. Cerca de 73% dos nossos locatários usam a consistência de sessão e 20% preferem desatualização limitada. Observamos que aproximadamente 3% de nossos clientes experimentam vários níveis de consistência inicialmente antes de escolherem uma opção de consistência específica para seu aplicativo. Também observamos que apenas 2% de nossos locatários substituem os níveis de consistência por solicitação. 

No Cosmos DB, leituras que atuam em consistência de sessão, prefixo consistente e eventual são duas vezes mais econômicas que leituras com consistência forte ou de desatualização limitada. O Cosmos DB tem SLAs abrangente de 99,99% líderes do setor, incluindo garantias de consistência junto com disponibilidade, taxa de transferência e latência. Empregamos um [verificador linearizability](http://dl.acm.org/citation.cfm?id=1806634), que opera continuamente em nosso telemetria de serviço e relatórios aberta qualquer tooyou de violações de consistência. Para determinado envelhecimento, podemos monitorar e relatar qualquer violação levou e limites de t. Todos os cinco níveis de consistência reduzida, podemos também relata Olá [métrica probabilístico desatualização associada](http://dl.acm.org/citation.cfm?id=2212359) tooyou diretamente.  

## <a name="scope-of-consistency"></a>Escopo de consistência
granularidade de saudação de consistência é tooa escopo solicitação de usuário único. Uma solicitação de gravação pode corresponder tooan inserção, substituição, upsert ou excluir a transação. Assim como ocorre em gravações, uma transação de leitura/consulta também é tooa no escopo solicitação de usuário único. usuário Olá pode ser necessário toopaginate sobre um grande conjunto de resultados, abrangendo várias partições, mas cada leitura transação está no escopo tooa única página e atendidas a partir de uma única partição.

## <a name="consistency-levels"></a>Níveis de consistência
Você pode configurar um nível de consistência padrão em sua conta do banco de dados que se aplica a coleções de tooall (e bancos de dados) em sua conta do banco de dados do Cosmos. Por padrão, todas as leituras e consultas em Olá recursos definidos pelo usuário usam o nível de consistência de padrão de saudação especificado na conta de banco de dados de saudação. Você pode relaxar o nível de consistência de saudação de uma leitura/consulta específica solicitar suporte para usar em cada Olá APIs. Há cinco tipos de níveis de consistência com suporte do protocolo de replicação de banco de dados do Azure Cosmos Olá que fornecem uma compensação clara entre desempenho e garantias de consistência específico, conforme descrito nesta seção.

**Strong**: 

* Consistência forte oferece um [linearizability](https://aphyr.com/posts/313-strong-consistency-models) garantia com hello lê a versão mais recente do hello tooreturn garantida de um item. 
* Uma coerência forte garante que uma gravação seja visível somente após ela ser confirmada forma durável pela quorum de maioria de saudação de réplicas. Uma gravação é ou sincronicamente confirmada forma duradoura Olá primário e quorum de saudação de secundários, ou será anulada. Uma leitura sempre é confirmada por leitura quorum de maioria de hello, um cliente nunca pode ver uma gravação não confirmada ou parcial e sempre é garantido tooread hello mais recente confirmada gravação. 
* Contas Cosmos DB do Azure que são consistência forte toouse configurado não é possível associar mais de uma região do Azure com sua conta do banco de dados do Azure Cosmos. 
* Olá custo de uma operação de leitura (em termos de [unidades de solicitação](request-units.md) consumido) com consistência forte é maior do que a sessão e eventual, mas Olá mesmo como desatualização associada.

**Bounded staleness**: 

* Coerência de desatualização associada garante que as leituras de saudação podem atrasar gravações no máximo *K* versões ou prefixos de um item ou *t* intervalo de tempo. 
* Portanto, quando escolher limitada envelhecimento, Olá "envelhecimento" pode ser configurado de duas maneiras: número de versões *K* do item de saudação pelo qual Olá leituras atrasem Olá gravações e o intervalo de tempo de saudação *t* 
* Limitado envelhecimento oferece total global ordem exceto dentro hello "janela envelhecimento." Olá monotônico ler garantias existe dentro de uma região dentro e fora de hello "janela envelhecimento." 
* A bounded staleness oferece garantia de consistência mais forte do que session ou eventual. Para aplicativos distribuídos globalmente, é recomendável que você use desatualização associada para cenários onde você seria como consistência forte toohave mas também quer 99,99% de disponibilidade e de baixa latência. 
* As contas do Azure Cosmos DB configuradas com a consistência de desatualização limitada podem associar qualquer número de regiões do Azure à respectiva conta do Azure Cosmos DB. 
* Olá custo de uma operação de leitura (em termos de RUs consumido) com desatualização associada for maior do que a sessão e consistência eventual, mas Olá mesmo como consistência forte.

**Session**: 

* Ao contrários dos modelos de consistência global Olá oferecidos pelos níveis de consistência envelhecimento forte e limitada, a coerência de sessão é tooa escopo sessão de cliente. 
* A consistência session é ideal para todos os cenários em que há o envolvimento de um dispositivo ou uma sessão de usuário, uma vez que ela garante leituras monotônicas, gravações monotônicas e RYW (leitura de suas próprias gravações). 
* A coerência de sessão fornece consistência previsível para uma sessão e máxima de taxa de transferência de leitura, oferecendo leituras e gravações de latência mais baixas Olá. 
* As contas do Azure Cosmos DB configuradas com a consistência de sessão podem associar qualquer número de regiões do Azure à respectiva conta do Azure Cosmos DB. 
* Olá custo de uma operação de leitura (em termos de RUs consumido) com a sessão de nível de consistência é menor que envelhecimento forte e limitado, mas consistência eventual mais de

<a id="consistent-prefix"></a>
**Prefixo consistente**: 

* Prefixo consistente garante que na ausência de qualquer mais gravações, Olá réplicas no grupo Olá convertidas eventualmente. 
* O prefixo consistente garante que as leituras nunca vejam gravações fora de ordem. Se gravações foram executadas na ordem de saudação `A, B, C`, em seguida, um cliente vê o `A`, `A,B`, ou `A,B,C`, mas nunca fora de ordem como `A,C` ou `B,A,C`.
* As contas do Azure Cosmos DB configuradas com a consistência de prefixo consistente podem associar qualquer número de regiões do Azure à respectiva conta do Azure Cosmos DB. 

**Eventual**: 

* Consistência eventual garante que na ausência de qualquer mais gravações, Olá réplicas no grupo Olá convertidas eventualmente. 
* Consistência eventual é a forma mais fraca Olá de consistência onde um cliente pode obter valores hello mais antigos que Olá que ele tinha visto antes.
* Consistência eventual fornece consistência de leitura hello mais fraco, mas oferece hello latência mais baixa para leituras e gravações.
* As contas do Azure Cosmos DB configuradas com a consistência eventual podem associar qualquer número de regiões do Azure à respectiva conta do Azure Cosmos DB. 
* Olá custo de uma operação de leitura (em termos de RUs consumido) com consistência eventual Olá nível é hello mais baixo de todos os níveis de consistência do banco de dados do Azure Cosmos hello.

## <a name="configuring-hello-default-consistency-level"></a>Configurando o nível de consistência saudação padrão
1. Em Olá [portal do Azure](https://portal.azure.com/), Olá Jumpbar no, clique em **o banco de dados do Azure Cosmos**.
2. Em Olá **o banco de dados do Azure Cosmos** folha, selecione Olá toomodify de conta de banco de dados.
3. Na folha de conta hello, clique em **padrão consistência**.
4. Em Olá **consistência padrão** folha, o novo nível de consistência Olá selecione e clique em **salvar**.
   
    ![Captura de tela, realce o ícone de configurações de saudação e entrada de consistência padrão](./media/consistency-levels/database-consistency-level-1.png)

## <a name="consistency-levels-for-queries"></a>Níveis de consistência para consultas
Por padrão, para os recursos definidos pelo usuário, nível de consistência Olá para consultas é Olá mesmo como o nível de consistência Olá para leituras. Por padrão, o índice de saudação é atualizado de forma síncrona em cada inserção, substituição ou exclusão de um contêiner do item toohello Cosmos DB. Isso permite consultas Olá toohonor Olá mesmo nível de consistência de ponto de leituras. Enquanto o banco de dados do Azure Cosmos é otimizada de gravação e oferece suporte a volumes prolongados de gravações, a manutenção do índice síncrona e fazer consultas consistentes, você pode configurar determinada coleções tooupdate seu índice lentamente. Ainda mais a indexação lenta aumenta o desempenho de gravação da saudação e é ideal para cenários de ingestão em massa quando uma carga de trabalho é principalmente pesadas de leitura.  

| Modo de indexação | Leituras | Consultas |
| --- | --- | --- |
| Consistente (padrão) |Selecione entre forte, desatualização limitada, sessão, prefixo consistente ou eventual |Escolher entre strong, bounded staleness, session ou eventual |
| Lentidão |Selecione entre forte, desatualização limitada, sessão, prefixo consistente ou eventual |Eventual |
| Nenhum |Selecione entre forte, desatualização limitada, sessão, prefixo consistente ou eventual |Não aplicável |

Como com solicitações de leitura, você pode diminuir nível de consistência de saudação de uma solicitação de consulta específica em cada API.

## <a name="next-steps"></a>Próximas etapas
Se você quiser toodo ler mais sobre níveis de consistência e compensações, recomendamos Olá recursos a seguir:

* Doug Terry. Replicated Data Consistency explained through baseball (vídeo).   
  [https://www.youtube.com/watch?v=gluIh8zd26I](https://www.youtube.com/watch?v=gluIh8zd26I)
* Doug Terry. Replicated Data Consistency explained through baseball.   
  [http://research.microsoft.com/pubs/157411/ConsistencyAndBaseballReport.pdf](http://research.microsoft.com/pubs/157411/ConsistencyAndBaseballReport.pdf)
* Doug Terry. Session Guarantees for Weakly Consistent Replicated Data.   
  [http://dl.acm.org/citation.cfm?id=383631](http://dl.acm.org/citation.cfm?id=383631)
* Daniel Abadi. Vantagens e desvantagens de consistência no Design da modernos sistemas de banco de dados distribuído: CAP é apenas parte da história Olá ".   
  [http://computer.org/csdl/mags/co/2012/02/mco2012020037-abs.html](http://computer.org/csdl/mags/co/2012/02/mco2012020037-abs.html)
* Peter Bailis, Shivaram Venkataraman, Michael J. Franklin, Joseph M. Hellerstein, Ion Stoica. Probabilistic Bounded Staleness (PBS) para quóruns parciais práticos.   
  [http://vldb.org/pvldb/vol5/p776_peterbailis_vldb2012.pdf](http://vldb.org/pvldb/vol5/p776_peterbailis_vldb2012.pdf)
* Werner Vogels. Eventual Consistent - Revisited.    
  [http://allthingsdistributed.com/2008/12/eventually_consistent.html](http://allthingsdistributed.com/2008/12/eventually_consistent.html)
* Moni Naor, Avishai lã, Olá carga, capacidade e disponibilidade de Quorum sistemas, SIAM diário em computação, 27 n.2, p.423-447, abril de 1998.
  [http://epubs.siam.org/doi/abs/10.1137/S0097539795281232](http://epubs.siam.org/doi/abs/10.1137/S0097539795281232)
* Sebastian Burckhardt, Chris Dern, Macanal Musuvathi, Roy Tan, linha: um linearizability completa e automática verificador, procedimentos da conferência de ACM SIGPLAN 2010 Olá no idioma de design e implementação, 05-10 de junho de 2010, Toronto, Ontário, de programação Canadá [doi > 10.1145/1806596.1806634] [http://dl.acm.org/citation.cfm?id=1806634](http://dl.acm.org/citation.cfm?id=1806634)
* Peter Bailis, Shivaram Venkataraman, Michael J. Franklin, Joseph M. Hellerstein, Stoica de retenção limitado com probabilidade envelhecimento para quorums parciais práticos, procedimentos da saudação Endowment VLDB, v. 5 n.8, p.776-787, abril de 2012 [http:// DL.ACM.org/Citation.cfm?ID=2212359](http://dl.acm.org/citation.cfm?id=2212359)
