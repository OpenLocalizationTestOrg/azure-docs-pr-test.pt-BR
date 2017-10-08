---
title: "Introdução tooAzure Cosmos DB Graph APIs | Microsoft Docs"
description: "Saiba como você pode usar o banco de dados do Azure Cosmos toostore, consulta e gráficos grandes completa com baixa latência usando linguagem de consulta de gráfico Olá Olá Gremlin do Apache TinkerPop."
services: cosmos-db
author: dennyglee
documentationcenter: 
ms.assetid: b916644c-4f28-4964-95fe-681faa6d6e08
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/21/2017
ms.author: denlee
ms.openlocfilehash: a4e79a4aa27976966baf0554928026177991ff69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-graph-api"></a>Introdução tooAzure Cosmos DB: API do Graph

[Banco de dados do Azure Cosmos](introduction.md) é Olá serviço globalmente distribuídos vários modelos de banco de dados da Microsoft para aplicativos de missão crítica. Banco de dados do Azure Cosmos fornece [distribuição global turnkey](distribute-data-globally.md), [dimensionamento Elástico de taxa de transferência e armazenamento](partition-data.md) latências de milissegundo em todo o mundo, dígito no percentual de 99th hello, [cinco níveis de consistência bem definidos](consistency-levels.md)e a garantia de alta disponibilidade, que são apoiadas por [SLAs do setor](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Banco de dados do Azure Cosmos [indexa automaticamente os dados](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) sem exigir que você toodeal com o gerenciamento de esquema e de índice. Ele tem vários modelos e suporta modelos de dados de colunas, gráficos, valores-chave e documentos.

![Gremlin, gráfico e o BD Cosmos do Azure](./media/graph-introduction/graph-gremlin.png)

Olá API do Graph do Azure Cosmos DB fornece:

- Modelagem de gráfico
- APIs transversais
- Distribuição global com tudo incluído
- A escala elástica de armazenamento e a taxa de transferência com menos de 10 ms, latências de leitura e menor que 15 ms percentil 99th Olá
- Indexação automática com disponibilidade imediata de consulta
- Níveis de consistência ajustáveis
- SLAs abrangentes, incluindo 99,99% de disponibilidade

tooquery Azure Cosmos DB, você pode usar o hello [Apache TinkerPop](http://tinkerpop.apache.org) graph idioma de passagem, [Gremlin](http://tinkerpop.apache.org/docs/current/reference/#graph-traversal-steps), ou outros sistemas de gráfico compatível com TinkerPop como [Apache Spark GraphX](spark-connector-graph.md).

Este artigo fornece uma visão geral de hello Azure Cosmos DB Graph API e explica como você pode usá-la gráficos grandes toostore bilhões de vértices e bordas. Você pode consultar os gráficos de saudação com latência de milissegundo e evoluir facilmente o esquema e a estrutura do gráfico de saudação.

## <a name="graph-database"></a>Banco de dados do gráfico
Dados como ele aparece no Olá, mundo real é naturalmente conectados. A modelagem de dados tradicional se concentra em entidades. Para muitos aplicativos, também há uma necessidade toomodel ou toomodel entidades e relações naturalmente.

Um [gráfico](http://mathworld.wolfram.com/Graph.html) é uma estrutura composta por [vértices](http://mathworld.wolfram.com/GraphVertex.html) e [bordas](http://mathworld.wolfram.com/GraphEdge.html). Os vértices e as bordas podem ter um número arbitrário de propriedades. Os vértices denotam objetos individuais, como uma pessoa, um lugar ou um evento. As bordas indicam relações entre os vértices. Por exemplo, uma pessoa pode conhecer a outra pessoa, estar envolvida em um evento e foi recentemente a um local. Propriedades expressam informações sobre vértices hello e bordas. Propriedades de exemplo incluem um vértice que tem um nome, uma idade e uma borda que tem um carimbo de data e/ou um peso. Mais formalmente, esse modelo é conhecido como um [gráfico de propriedade](http://tinkerpop.apache.org/docs/current/reference/#intro). Banco de dados do Azure Cosmos dá suporte ao modelo de gráfico de propriedade hello.

Por exemplo, Olá de exemplo a seguir gráfico mostra relações entre as pessoas, dispositivos móveis, interesses e sistemas operacionais.

![Banco de dados de exemplo mostrando interesses, dispositivos e pessoas](./media/graph-introduction/sample-graph.png)

Gráficos são úteis toounderstand uma ampla variedade de conjuntos de dados ciência, tecnologia e negócios. Bancos de dados de gráfico permitem modelar e armazenar gráficos de forma natural e eficiente, o que os torna atraentes para muitos cenários. Bancos de dados de gráfico normalmente são bancos de dados NoSQL, porque frequentemente esses casos de uso também precisam de iteração rápida e flexibilidade de esquema.

Os gráficos oferecem uma nova e avançada técnica de modelagem de dados. Mas esse fato por si só não é um toouse de motivo suficiente um banco de dados do gráfico. Para muitos casos de uso e padrões que envolvem passagens de gráfico, os gráficos superam o desempenho de bancos de dados SQL e NoSQL tradicionais em ordens de magnitude. Essa diferença no desempenho aumenta ainda mais ao percorrer mais de uma relação, como a de amigo de amigo.

Você pode combinar traversais rápida de saudação que fornecem bancos de dados do gráfico com algoritmos de gráfico, como a pesquisa, pesquisa de amplitude e algoritmo de Dijkstra, toosolve problemas em vários domínios, como redes sociais, gerenciamento de conteúdo, geoespaciais, e recomendações.

## <a name="planet-scale-graphs-with-azure-cosmos-db"></a>Gráficos de escala planetária com o BD Cosmos do Azure
Banco de dados do Azure Cosmos é um banco de dados do gráfico totalmente gerenciado que oferece distribuição global elástica de dimensionamento de armazenamento e taxa de transferência, a indexação automática e consulta, níveis de consistência ajustáveis e suporte para Olá TinkerPop padrão.  

![Arquitetura de gráfico do BD Cosmos do Azure](./media/graph-introduction/cosmosdb-graph-architecture.png)

Banco de dados do Azure Cosmos oferece o seguinte Olá diferenciados recursos em comparação com bancos de dados do gráfico tooother no mercado de saudação:

* Dimensionamento elástico do armazenamento e da taxa de transferência

 Gráficos em Olá, mundo real necessário tooscale além da capacidade de saudação de um único servidor. Com o BD Cosmos do Azure, é possível expandir facilmente seus gráficos em vários servidores. Você também pode expandir a taxa de transferência de saudação do seu gráfico independentemente com base nos seus padrões de acesso. Banco de dados do Azure Cosmos oferece suporte a bancos de dados do gráfico que podem ser dimensionado toovirtually tamanhos de armazenamento ilimitado e taxa de transferência fornecida.

* Replicação de várias regiões

 Banco de dados do Azure Cosmos transparentemente replica as regiões de tooall de dados do gráfico que você associou com sua conta. A replicação permite que você toodevelop aplicativos que exigem acesso global toodata. Há vantagens e desvantagens em áreas de saudação de consistência, disponibilidade e desempenho e garantias correspondentes. O BD Cosmos do Azure fornece failover transparente regional com APIs de hospedagem múltipla. Elasticidade, você pode dimensionar o armazenamento e a taxa de transferência globo hello.

* Passagens e consultas rápidas com sintaxe familiar de Gremlin

 Armazenar bordas e vértices heterogêneos e consultar esses documentos por meio de uma sintaxe Gremlin familiar. Banco de dados do Azure Cosmos utiliza um altamente simultânea sem bloqueio estruturado log indexação tecnologia tooautomatically índice, todo o conteúdo. Esse recurso permite que as consultas em tempo real avançadas e traversais sem Olá precisam toospecify dicas de esquema, índices secundários ou modos de exibição. Saiba mais em [Consultar gráficos usando Gremlin](gremlin-support.md).

* Totalmente gerenciado

 Banco de dados do Azure Cosmos elimina Olá necessidade toomanage banco de dados e máquina recursos. Como um serviço totalmente gerenciado do Microsoft Azure, você faça não necessidade toomanage VMs, implanta e configurar o software, gerenciar dimensionamento ou lida com as atualizações da camada de dados complexos. Cada gráfico é salvo em backup automaticamente e protegido contra falhas regionais. Você pode adicionar facilmente uma conta do BD Cosmos do Azure e provisionar a capacidade conforme for necessário, permitindo que você se concentre em seu aplicativo sem se preocupar com a operação e com o gerenciamento do banco de dados.

* Indexação automática

 Por padrão, o banco de dados do Azure Cosmos automaticamente índices todas as propriedades de saudação em nós e bordas no gráfico de saudação e não espera ou exigir qualquer esquema ou a criação de índices secundários.

* Compatibilidade com o Apache TinkerPop

 Banco de dados do Azure Cosmos nativamente dá suporte à saudação código-fonte aberto Apache TinkerPop padrão e pode ser integrado a outros sistemas de gráfico TinkerPop habilitado. Dessa forma, é possível migrar facilmente de outro banco de dados de gráfico, como Titan ou Neo4j, ou usar o BD Cosmos do Azure com estruturas de análise de gráfico como o [Apache Spark GraphX](spark-connector-graph.md).

* Níveis de consistência ajustáveis

 Selecione cinco consistência bem definidos níveis tooachieve compensação ideal entre desempenho e consistência. Para operações de consulta e leitura, o Azure Cosmos DB oferece cinco níveis de consistência diferentes: forte, desatualização limitada, sessão, prefixo constante e eventual. Esses níveis de consistência bem definidos, granular permitem compensações de som toomake entre consistência, disponibilidade e latência. Saiba mais em [usar consistência níveis de desempenho em documentos e a disponibilidade de toomaximize](consistency-levels.md).

Banco de dados do Azure Cosmos também pode usar vários modelos, como o documento e o gráfico, em Olá contêineres mesmo/bancos de dados. Você pode usar um documento coleção toostore gráfico de dados lado a lado com documentos. Você pode usar ambas as consultas SQL em JSON e Gremlin consultas tooquery Olá os mesmos dados como um gráfico.

## <a name="getting-started"></a>Introdução
Você pode usar o hello Azure interface de linha de comando (CLI) do Powershell do Azure, ou Olá portal do Azure com suporte para contas de banco de dados do Azure Cosmos graph API toocreate. Depois de criar contas, hello portal do Azure fornece um ponto de extremidade de serviço, como `https://<youraccount>.graphs.azure.com`, que fornece um front-end do WebSocket para Gremlin. Você pode configurar suas ferramentas TinkerPop compatível, como Olá [Gremin Console](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console), aplicativos de ponto de extremidade e compilação de toothis de tooconnect em Java, Node.js ou qualquer driver de cliente Gremlin.

Olá tabela a seguir mostra populares Gremlin drivers que você pode usar com o banco de dados do Azure Cosmos:

| Baixar | Documentação |
| --- | --- |
| [Java](https://mvnrepository.com/artifact/com.tinkerpop.gremlin/gremlin-java) |[Gremlin JavaDoc](http://tinkerpop.apache.org/javadocs/current/full/) |
| [Node.js](https://www.npmjs.com/package/gremlin) |[Gremlin-JavaScript no GitHub](https://github.com/jbmusso/gremlin-javascript) |
| [Console do Gremlin](https://tinkerpop.apache.org/downloads.html) |[Documentos do TinkerPop](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console) |

Banco de dados do Azure Cosmos também fornece uma biblioteca .NET que tem os métodos de extensão Gremlin sobre Olá [SDKs do banco de dados do Azure Cosmos](documentdb-sdk-dotnet.md) por meio do NuGet. Essa biblioteca fornece um "" Gremlin do servidor em processo que você pode usar tooconnect tooDocumentDB diretamente as partições de dados.

| Baixar | Documentação |
| --- | --- |
| [.NET](https://www.nuget.org/packages/Microsoft.Azure.Graphs/) |[Microsoft.Azure.Graphs](https://msdn.microsoft.com/library/azure/dn948556.aspx) |

Usando Olá [emulador de banco de dados do Azure Cosmos](local-emulator.md), você pode usar toodevelop de API do Graph hello e testar localmente, sem criar uma assinatura do Azure ou incorrer em custos de qualquer. Quando estiver satisfeito com o funcionamento seu aplicativo no emulador de saudação, você pode alternar toousing uma conta de banco de dados do Azure Cosmos na nuvem hello.

## <a name="scenarios-for-graph-support-of-azure-cosmos-db"></a>Cenários de suporte a gráfico do BD Cosmos do Azure
Veja alguns cenários em que o suporte para gráfico do BD Cosmos do Azure pode ser usado:

* Redes Sociais

 Combinando dados sobre seus clientes e as interações deles com outras pessoas, você pode desenvolver experiências personalizadas, prever o comportamento do cliente ou conectar pessoas com interesses semelhantes. Banco de dados do Azure Cosmos pode ser usado toomanage redes sociais e controlar os dados e as preferências do cliente.

* Mecanismos de recomendação

 Esse cenário normalmente é usado no setor de varejo hello. Combinando informações sobre produtos, usuários e interações do usuário, como compras, navegação ou a classificação de um item, você pode criar recomendações personalizadas. Olá nativo de baixa latência e escala elástica suporte gráfico de banco de dados do Azure Cosmos é ideal para essas interações de modelagem.

* Geoespacial

 Muitos aplicativos de telecomunicações, logística e planejamento de viagem necessário toofind um local de interesse dentro de uma área ou localizar rota mais curta ideal Olá entre dois locais. O BD Cosmos do Azure é uma solução natural para esses problemas.

* Internet das coisas

 Com a rede hello e conexões entre dispositivos IoT modelados como um gráfico, você pode criar uma melhor compreensão do estado de saudação de seus dispositivos e ativos e saber como as alterações em uma parte da rede Olá podem afetar potencialmente outra parte.

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre o suporte de gráfico no banco de dados do Azure Cosmos, consulte:

* Introdução ao Olá [tutorial do gráfico de banco de dados do Azure Cosmos](create-graph-dotnet.md).
* Saiba mais sobre como muito[consulta gráficos no banco de dados do Cosmos do Azure usando Gremlin](gremlin-support.md).
