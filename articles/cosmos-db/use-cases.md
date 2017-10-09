---
title: "aaaCommon casos de uso e cenários para o banco de dados do Azure Cosmos | Microsoft Docs"
description: "Saiba mais sobre superior Olá cinco casos de uso para o banco de dados do Azure Cosmos: conteúdo, o log de eventos, dados de catálogo, os dados de preferências do usuário e Internet das coisas (IoT) gerado pelo usuário."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: eca68a58-1a8c-4851-8cf8-6e4d2b889905
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: mimig
ms.openlocfilehash: 115a418e7b18d5033c4d7e64591bf302aea0190b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="common-azure-cosmos-db-use-cases"></a>Casos de uso comuns do Azure Cosmos DB
Este artigo fornece uma visão geral dos vários casos de uso comuns do Azure Cosmos DB.  recomendações de saudação neste artigo servem como ponto de partida à medida que desenvolve seu aplicativo com o banco de dados do Cosmos.   

Depois de ler este artigo, você será capaz de tooanswer Olá perguntas a seguir: 

* Quais são os casos de uso comuns Olá para o banco de dados do Azure Cosmos?
* Quais são os benefícios de saudação do banco de dados do Azure Cosmos para aplicativos de varejo?
* Quais são os benefícios de saudação do uso de banco de dados do Azure Cosmos como um repositório de dados para sistemas de Internet das coisas (IoT)?
* Quais são os benefícios de saudação do banco de dados do Azure Cosmos para aplicativos web e móveis?

## <a name="introduction"></a>Introdução
O [Azure Cosmos DB](../cosmos-db/introduction.md) é um serviço de banco de dados distribuído globalmente da Microsoft. Olá, serviço é projetado tooallow clientes tooelastically (e independente) escalonar a taxa de transferência e armazenamento em qualquer número de regiões geográficas. Banco de dados do Azure Cosmos está Olá primeiro serviço de banco de dados distribuído globalmente em Olá mercado toooffer hoje abrangente [contratos de nível de serviço](https://azure.microsoft.com/support/legal/sla/cosmos-db/) que abrangem a taxa de transferência, a latência, a disponibilidade e a consistência. 

projeto de banco de dados do Azure Cosmos Olá iniciado em 2011 como "Projeto Florence" tooaddress desenvolvedor pontos problemáticos enfrentados pelos aplicativos de grande escala da Internet dentro da Microsoft. Observe que esses problemas não são aplicativos do tooMicrosoft exclusivo, decidimos toomake banco de dados do Azure Cosmos tooexternal disponível desenvolvedores em 2015 no formato de saudação do [DocumentDB do Azure](https://azure.microsoft.com/blog/documentdb-moving-to-general-availability/). serviço de saudação é usado ubiquitously internamente na Microsoft e é um dos serviços de crescimento mais rápido de saudação usados por desenvolvedores do Azure externamente. 

O Azure Cosmos DB é um multimodelo de banco de dados distribuído globalmente que é usado em uma ampla variedade de aplicativos e casos de uso. É uma boa escolha para qualquer [sem servidor](http://azure.com/serverless) aplicativo que precisa de tempos de resposta de ordem de milissegundo baixa e precisa tooscale rapidamente e global. Ele dá suporte a vários modelos de dados (chave-valor, documentos, gráficos e colunas) e várias APIs para acesso a dados, incluindo [MongoDB](mongodb-introduction.md), [SQL do DocumentDB](documentdb-introduction.md), [Gremlin](graph-introduction.md) e [Tabelas do Azure](table-introduction.md) nativamente, bem como de maneira extensível. 

Olá seguem alguns atributos de banco de dados do Azure Cosmos que a tornam bem adequado para aplicativos de alto desempenho com ambição global.

* O Azure Cosmos DB particiona os dados nativamente para alta disponibilidade e escalabilidade. O Azure Cosmos DB oferece garantias de 99,99% para disponibilidade, produtividade, baixa latência e consistência.
* O Azure Cosmos DB tem armazenamento com suporte de SSD com tempos de resposta de baixa latência na ordem de milissegundos.
* O suporte do Azure Cosmos DB para níveis de consistência (como deterioração restrita, de sessão, de prefixo consistente e eventual) proporciona flexibilidade total e taxas baixas em relação ao custo-desempenho. Nenhum serviço de banco de dados oferece tanta flexibilidade quanto o Azure Cosmos DB na consistência de níveis. 
* O Azure Cosmos DB tem um modelo de preços flexível e amigável aos dados que mede o armazenamento e a produtividade de modo independente.
* Modelo de taxa de transferência reservada do Azure Cosmos DB permite que você toothink em termos de número de leituras/gravações em vez de memória/CPU/IOPs de saudação hardware subjacente.
* Permite a estrutura do Azure Cosmos DB que você dimensionar toomassive volumes de solicitação no hello ordem de trilhões de solicitações por dia.

Esses atributos são benéficos na web, móvel, jogos e aplicativos IoT baixo tempo de resposta e precisarem toohandle grandes quantidades de leituras e gravações.

## <a name="iot-and-telematics"></a>IoT e telemático
Casos de uso de IoT normalmente compartilham alguns padrões sobre como consomem, processam e armazenam dados.  Primeiro, esses sistemas necessário tooingest intermitências de dados de sensores de dispositivo de vários locais. Em seguida, esses sistemas de processam e analisar informações em tempo real do streaming dados tooderive. Olá dados arquivados armazenamento toocold para análise de lote. O Microsoft Azure oferece serviços avançados que podem ser aplicados a casos de uso de IoT, incluindo Azure Cosmos DB, Hubs de Eventos do Azure, Stream Analytics do Azure, Hub de Notificação do Azure, Azure Machine Learning, Azure HDInsight e Power BI. 

![Arquitetura de referência de IoT do Azure Cosmos DB](./media/use-cases/iot.png)

Picos de dados podem ser processados por Hubs de eventos do Azure que oferecem inclusão de dados de alta taxa de transferência com baixa latência. Dados incluídos que precisa toobe processado para análise em tempo real podem ser encaminhada tooAzure Stream Analytics para análise em tempo real. Os dados podem ser carregados no Azure Cosmos DB para consultas ad hoc. Quando dados saudação são carregados no banco de dados do Azure Cosmos, dados saudação são toobe pronto consultada. Além disso, novos dados e alterações tooexisting dados podem ser lidos no feed de alteração. Feed de alteração é uma constante, acrescentar somente alterações de log que armazena tooCosmos DB coleções em ordem sequencial. Olá que todos os dados ou apenas as alterações toodata no banco de dados do Azure Cosmos pode ser usado como dados de referência como parte da análise em tempo real. Além disso, os dados mais podem ser refinados e processados por conexão tooHDInsight de dados do banco de dados do Azure Cosmos para trabalhos de Pig, Hive ou mapear/reduzir.  Dados refinados, em seguida, são carregados back tooAzure Cosmos banco de dados para relatórios.   

Para uma solução de IoT de exemplo usando o banco de dados do Azure Cosmos, EventHubs e tempestade, consulte Olá [hdinsight de profusão de exemplos repositório no GitHub](https://github.com/hdinsight/hdinsight-storm-examples/).

Para obter mais informações sobre as ofertas de IoT do Azure, consulte [criar hello Internet das coisas seu](http://www.microsoft.com/server-cloud/internet-of-things.aspx). 

## <a name="retail-and-marketing"></a>Varejo e marketing
Banco de dados do Azure Cosmos é usado extensivamente em plataformas de comércio eletrônico da Microsoft, que executam o armazenamento do Windows hello e XBox Live. Ele também é usado no setor de varejo Olá para armazenar dados de catálogo e para processamento de pipelines de fornecimento de evento.

Os cenários de uso de dados de catálogo envolvem armazenar e consultar um conjunto de atributos para entidades, como pessoas, lugares e produtos. Alguns exemplos de dados de catálogo são contas de usuário, catálogos de produtos, registros de dispositivos IoT e sistemas de listas de materiais. Atributos de dados podem variar e podem mudar com requisitos de aplicativo de toofit de tempo.

Considere um exemplo de um catálogo de produto para um fornecedor de peças automotivas. Todas as partes podem ter seus próprios atributos em adição toohello atributos comuns que compartilham todas as partes. Além disso, os atributos de uma parte específica podem alterar Olá após um ano em um novo modelo é lançado. O Azure Cosmos DB dá suporte a esquemas flexíveis e dados hierárquicos e, portanto, é adequado para armazenar dados de catálogo de produtos.

![Arquitetura de referência de catálogo para varejo do Azure Cosmos DB](./media/use-cases/product-catalog.png)

Banco de dados do Azure Cosmos geralmente é usado para o evento fornecimento toopower arquiteturas de orientados a eventos usando seu [alterar feed](change-feed.md) funcionalidade. Olá alteração feed fornece microservices downstream Olá tooreliably de capacidade e incrementalmente leitura inserções e atualizações (por exemplo, eventos de ordem) feitas tooan Azure Cosmos DB. Essa funcionalidade pode ser utilizado tooprovide um evento persistente armazenar como um agente de mensagens para eventos de alteração de estado e fluxo de trabalho de processamento de ordem de unidade entre muitos microservices (que podem ser implementado como [funções do Azure sem servidor](http://azure.com/serverless)).

![Arquitetura de referência de pipeline de ordenação do Azure Cosmos DB](./media/use-cases/event-sourcing.png)

Além disso, os dados armazenados no Azure Cosmos DB podem ser integrados com o HDInsight para análises de Big Data por meio de trabalhos do Apache Spark. Para obter detalhes sobre Olá conector Spark para o banco de dados do Azure Cosmos, consulte [executar um trabalho Spark com banco de dados do Cosmos e HDInsight](spark-connector.md).

## <a name="gaming"></a>Jogos
camada de banco de dados de saudação é um componente fundamental de aplicativos de jogos. Jogos modernos executam o processamento de gráfico em clientes móveis/console, mas dependem Olá nuvem toodeliver personalizado e conteúdo personalizado, como estatísticas de jogos, integração de mídia social e tabelas de pontuações. Jogos geralmente exigem latências de milissegundo único para leituras e gravações tooprovide uma experiência de jogo envolvente. Um banco de dados de jogo precisa toobe rápida e ser capaz de toohandle picos de grandes em taxas de solicitação durante novos lançamentos de jogos e atualizações do recurso.

Banco de dados do Azure Cosmos é usado por jogos como [Olá percorrer inativo: terra do homem não](https://azure.microsoft.com/blog/the-walking-dead-no-mans-land-game-soars-to-1-with-azure-documentdb/) por [jogos próximo](http://www.nextgames.com/), e [Halo 5: responsáveis](https://azure.microsoft.com/blog/how-halo-5-guardians-implemented-social-gameplay-using-azure-documentdb/). Banco de dados do Azure Cosmos fornece a seguinte Olá beneficia os desenvolvedores de toogame:

* Banco de dados do Azure Cosmos permite toobe desempenho dimensionada para cima ou para baixo de elasticidade. Isso permite que a atualização de perfil e estatísticas de dezenas de toohandle de jogos toomillions de gamers simultâneas, fazendo uma única chamada de API.
* Azure Cosmos DB oferece suporte a milissegundos leituras e gravações toohelp evitar qualquer atrasos durante o jogo.
* A indexação automática do Azure Cosmos DB permite a filtragem em várias propriedades diferentes em tempo real, por exemplo, localização de jogadores por suas IDs internas de jogador ou por suas IDs do GameCenter, do Facebook, do Google, ou ainda a realização de consulta baseada em associação do jogador a uma comunidade. Isso é possível sem a criação de indexação complexa ou infraestrutura de fragmentação.
* Recursos sociais, incluindo mensagens de chat de jogos, associações de guild player, desafios concluídos, pontuações tabelas e gráficos sociais são tooimplement mais fácil com um esquema flexível.
* Azure DB Cosmos como um plataforma-como-um-serviço gerenciado (PaaS) necessária uma configuração mínima e tooallow de trabalho de gerenciamento para iteração rápida e reduzir o tempo toomarket.

![Arquitetura de referência de jogos do Azure Cosmos DB](./media/use-cases/gaming.png)

## <a name="web-and-mobile-applications"></a>Aplicativos Web e móveis
O Azure Cosmos DB é normalmente usado em aplicativos Web e móveis e é bastante adequado para modelagem de interações sociais, integração com serviços de terceiros e desenvolvimento de experiências personalizadas avançadas. Olá Cosmos SDKs do banco de dados pode ser usado compilação avançados aplicativos iOS e Android usando Olá popular [Xamarin framework](mobile-apps-with-xamarin.md).  

### <a name="social-applications"></a>Aplicativos sociais
Um caso de uso comum para o banco de dados do Azure Cosmos é toostore e consulta de conteúdo gerado pelo usuário (UGC) para a web, aplicativos de mídia social e móveis. Alguns exemplos de UGC são sessões de bate-papo, tweets, postagens em blogs, classificações e comentários. Geralmente, Olá UGC em aplicativos de mídia social é uma mistura de texto de formato livre, propriedades, marcas e relações que não se limitam a estrutura rígida. Conteúdo como bate-papo, comentários e postagens podem ser armazenados no banco de dados do Cosmos sem a necessidade de camadas de mapeamento de toorelational objeto complexo ou de transformações.  Propriedades de dados podem ser adicionadas ou modificada facilmente toomatch requisitos, como os desenvolvedores iterar em código do aplicativo hello, assim, promover o rápido desenvolvimento.  

Aplicativos que se integram com redes sociais de terceiros devem responder esquemas toochanging essas redes. Como dados são automaticamente indexados por padrão no banco de dados do Cosmos, os dados são toobe pronto consultada a qualquer momento. Portanto, esses aplicativos têm projeções de tooretrieve Olá flexibilidade de acordo com suas respectivas necessidades.

Muitos dos aplicativos sociais Olá execute em escala global e podem apresentar os padrões de uso imprevisível. Flexibilidade na expansão de armazenamento de dados de saudação é essencial como camada de aplicativo hello dimensiona toomatch demanda de uso.  Escale horizontalmente adicionando outras partições de dados em uma conta do Cosmos DB.  Além disso, você também pode criar outras contas do Cosmos DB em várias regiões. Para obter a disponibilidade de regiões do serviço Cosmos DB, consulte [Regiões do Azure](https://azure.microsoft.com/regions/#services).

![Arquitetura de referência de aplicativo Web do Azure Cosmos DB](./media/use-cases/apps-with-global-reach.png)

### <a name="personalization"></a>Personalização
Hoje em dia, aplicativos modernos vêm com modos de exibição e experiências mais complexos. Esses são normalmente dinâmicos, buffet preferências toouser ou humor e necessidades de identidade visual. Portanto, os aplicativos precisam toobe capaz de tooretrieve personalizado configurações efetivamente os elementos de interface do usuário toorender e experiências rapidamente. 

JSON, um formato com suporte pelo DB Cosmos, é um formato efetivo toorepresent da interface do usuário layout de dados não é apenas superficial, mas também podem ser facilmente interpretado pelo JavaScript. O Cosmos DB oferece níveis de consistência ajustáveis que permitem leituras rápidas com gravações de baixa latência. Portanto, armazenar dados de layout de interface do usuário, incluindo configurações personalizadas, como documentos JSON no banco de dados do Cosmos é um meio eficaz tooget esses dados em transmissão de saudação.

![Arquitetura de referência de aplicativo Web do Azure Cosmos DB](./media/use-cases/personalization.png)

## <a name="next-steps"></a>Próximas etapas
tooget de Introdução ao banco de dados do Azure Cosmos, siga nosso [inícios rápidos](create-documentdb-dotnet.md), que orientam você durante a criação de uma conta e o guia de Introdução ao banco de dados do Cosmos. 

Ou, se você quiser mais informações sobre os clientes que usam o banco de dados do Cosmos de tooread, hello histórias seguintes estão disponíveis:

* [Jet.com](https://jet.com). Desafio de comércio eletrônico olhos Olá primeiro lugar, é executado em nuvem da Microsoft hello, aproveita o banco de dados do Cosmos em uma escala global.
* [Asos.com](http://www.asos.com/). Asos.com é uma loja online de produtos de beleza e moda do Reino Unido. Voltada principalmente para jovens adultos, a Asos vende mais de 850 marcas, bem como sua própria linha de roupas e acessórios.
* [Toyota](https://www.toyota.com/). A Toyota Motor Corporation é um fabricante automotivo japonês. A Toyota utilizou o Cosmos DB para um aplicativo de IoT global.
* [Citrix](https://customers.microsoft.com/story/citrix). A Citrix desenvolve uma solução de logon único usando o Azure Service Fabric e o Azure Cosmos DB
* [TEXA](https://customers.microsoft.com/story/texaspa) A solução de IoT revolucionária da TEXA para proprietários de veículos ajuda a economizar tempo, dinheiro e combustível – e possivelmente, vidas.
* [Domino's Pizza](https://www.dominos.com). A Domino's Pizza Inc. é uma cadeia de restaurantes especializados em pizza dos EUA.
* [Johnson Controls](http://www.johnsoncontrols.com). A Johnson Controls é líder global em vários setores e tecnologias diversificadas que atende a uma ampla variedade de clientes em mais de 150 países.
* [Microsoft Windows, Universal Store, Hub IoT do Azure, Xbox Live e outros serviços de escala da Internet](https://azure.microsoft.com/blog/how-azure-documentdb-planet-scale-nosql-helps-run-microsoft-s-own-businesses/). Como a Microsoft cria serviços altamente escalonáveis usando o Azure Cosmos DB.
* [Equipe de Dados e Análise da Microsoft](https://customers.microsoft.com/story/microsoftdataandanalytics). A equipe de Dados e Análise da Microsoft obtém uma coleção de Big Data de escala mundial com o Azure Cosmos DB
* [Sulekha.com](https://customers.microsoft.com/story/sulekha-uses-azure-documentdb-to-connect-customers-and-businesses-across-india). Sulekha usa o banco de dados do Azure Cosmos tooconnect clientes e empresas em Índia.
* [NewOrbit](https://customers.microsoft.com/story/neworbit-takes-flight-with-azure-documentdb). A NewOrbit decola com o Azure Cosmos DB.
* [Affinio](https://customers.microsoft.com/doclink/affinio-switches-from-aws-to-azure-documentdb-to-harness-social-data-at-scale). Affinio alterna do AWS tooAzure Cosmos DB tooharness sociais dados em grande escala.
* [Next Games](https://azure.microsoft.com//blog/the-walking-dead-no-mans-land-game-soars-to-1-with-azure-documentdb/). Olá Walking mortas: soars jogos manual de terra muito #1 tem suporte pelo banco de dados do Azure Cosmos.
* [Halo](https://azure.microsoft.com/blog/how-halo-5-guardians-implemented-social-gameplay-using-azure-documentdb/). Como a Halo 5 implementou partidas sociais usando o Azure Cosmos DB.
* [Cortana Analytics Gallery](https://azure.microsoft.com/blog/cortana-analytics-gallery-a-scalable-community-site-built-on-azure-documentdb/). Galeria do Cortana Analytics – um site da comunidade escalonável criado com base no Azure Cosmos DB.
* [Breeze](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18602). Integrador líder oferece a empresas multinacionais informações globais em minutos com as tecnologias de nuvem flexíveis.
* [News Republic](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18639). Adicionando inteligência toohello notícias tooprovide informações com a finalidade de cidadãos envolvidos. 
* [SGS International](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18653). Para cor consistente globo hello, principais marcas ativar tooSGS. E SGS ativa tooAzure.
* [Telenor](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18608). Líder global Telenor usa Olá nuvem toomove com velocidade de saudação de uma inicialização. 
* [XOMNI](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18667). repositório de saudação de execuções futuras Olá rápida pesquisa e hello fácil fluxo de dados.
* [Nucleo](https://customers.microsoft.com/story/azure-based-software-platform-breaks-down-barriers-bet). Plataforma de software com base no Azure quebra as barreiras entre as empresas e os clientes
* [Weka](https://customers.microsoft.com/story/weka-smart-fridge-improves-vaccine-management-so-more-people-can-be-protected-against-diseases). O Refrigerador Inteligente da Weka aprimora o gerenciamento de vacinas para que mais pessoas podem ser protegidas contra doenças
* [Orange Tribes](https://customers.microsoft.com/story/theres-more-to-that-food-app-than-meets-the-eye-or-the-mouth). Não há mais aplicativos de alimentos toothat que atende aos olhos hello ou boca hello.
* [Real Madrid](https://customers.microsoft.com/story/real-madrid-brings-the-stadium-closer-to-450-million-f). Madri real traz Olá Estádio próximo too450 milhão ventiladores mundo hello, com hello Microsoft Cloud.
* [Tuku](https://customers.microsoft.com/story/tuku-makes-car-buying-fun-with-help-from-azure-services). TUKU torna a compra de carros mais divertida com a Ajuda dos serviços do Azure
