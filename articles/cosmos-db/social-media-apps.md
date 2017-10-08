---
title: "Padrão de design do Azure Cosmos DB: Aplicativos de mídia social | Microsoft Docs"
description: "Saiba mais sobre um padrão de design de redes sociais, aproveitando a flexibilidade de armazenamento de saudação do banco de dados do Azure Cosmos e outros serviços do Azure."
keywords: "aplicativos de mídia social"
services: cosmos-db
author: ealsur
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 2dbf83a7-512a-4993-bf1b-ea7d72e095d9
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2017
ms.author: mimig
ms.openlocfilehash: 47a22f2c5762d62b176921c8052e7bd75d8cf6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="going-social-with-azure-cosmos-db"></a>Expandindo o Azure Cosmos DB para as redes sociais
Viver em uma sociedade amplamente interconectada significa que, em determinado momento da vida, você acaba se tornando parte de uma **rede social**. Podemos usar nossa entusiasta redes sociais tookeep entre em contato com amigos, colegas de trabalho, família ou às vezes tooshare com pessoas com interesses comuns.

Como engenheiros ou desenvolvedores, pode ter pensado como essas redes de armazenamento e interconexão de nossos dados, ou pode ter até mesmo foi encarregado toocreate ou arquiteto de uma nova rede social para um pequeno porte específico mercado si. Ou seja, quando a pergunta Olá surge: como todos os dados são armazenados?

Vamos supor que estamos criando uma nova rede social, na qual nossos usuários podem postar artigos com mídia relacionada como imagens, vídeos ou, até mesmo, música. Os usuários podem fazer comentários sobre as postagens e fornecer pontos para classificações. Haverá um feed de postagens que usuários e ser capaz de toointeract na página de aterrissagem do site principal hello. Isso não parece muito complexo (no primeiro), mas para bem Olá de simplicidade, vamos parar (pôde examinarmos afetados por relações de feeds de usuário personalizada, mas ele exceder o objetivo deste artigo Olá).

Então, como e onde armazenamos tudo isso?

Muitos de vocês talvez tenham experiência em bancos de dados SQL ou pelo menos ter a noção de [relacional de modelagem de dados](https://en.wikipedia.org/wiki/Relational_model) e pode ser tentado toostart desenho algo assim:

![Diagrama ilustrando um modelo relacional relativo](./media/social-media-apps/social-media-apps-sql.png) 

Uma bela estrutura de dados perfeitamente normalizada... que não pode ser dimensionada. 

Não me entendam mal: sempre trabalhei com bancos de dados SQL; eles são ótimos, mas como acontece com cada padrão, prática e plataforma de software, eles não são perfeitos para todos os cenários.

Por que não SQL Olá melhor opção neste cenário? Vamos examinar a estrutura de saudação de uma postagem único, se queria tooshow post em um site ou aplicativo, teria toodo uma consulta com... Tabela 8 junções (!) tooshow apenas um único post, agora, um fluxo de postagens que carregar dinamicamente e são exibidas na tela hello e você poderá ver onde vou de imagem.

Poderíamos, obviamente, usar uma instância do SQL humongous com suficiente toosolve power milhares de consultas com esses tooserve junções muitos nosso conteúdo, mas realmente, por que, quando uma solução mais simples seria existe?

## <a name="hello-nosql-road"></a>Estrada de NoSQL Olá
Este artigo vai guiá-lo para modelar dados do sua plataforma sociais banco de dados do Azure NoSQL [o banco de dados do Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) de maneira econômica e aproveitar a outros recursos de banco de dados do Azure Cosmos como Olá [Gremlin Graph API ](../cosmos-db/graph-introduction.md). Usando uma abordagem [NoSQL](https://en.wikipedia.org/wiki/NoSQL), armazenando os dados no formato JSON e aplicando a [desnormalização](https://en.wikipedia.org/wiki/Denormalization), nossa postagem anteriormente complicada pode ser transformada em um único [Documento](https://en.wikipedia.org/wiki/Document-oriented_database):


    {
        "id":"ew12-res2-234e-544f",
        "title":"post title",
        "date":"2016-01-01",
        "body":"this is an awesome post stored on NoSQL",
        "createdBy":User,
        "images":["http://myfirstimage.png","http://mysecondimage.png"],
        "videos":[
            {"url":"http://myfirstvideo.mp4", "title":"hello first video"},
            {"url":"http://mysecondvideo.mp4", "title":"hello second video"}
        ],
        "audios":[
            {"url":"http://myfirstaudio.mp3", "title":"hello first audio"},
            {"url":"http://mysecondaudio.mp3", "title":"hello second audio"}
        ]
    }

E isso pode ser obtido com uma única consulta, sem junções. Isso é muito mais simples e direto e budget-wise, ele requer menos recursos tooachieve um resultado melhor.

Banco de dados do Azure Cosmos garante que todas as propriedades de saudação são indexadas com seu indexação automática, que pode ser até mesmo [personalizado](indexing-policies.md). Olá livre de esquemas abordagem permite armazenar documentos com diferentes e dinâmicas estruturas, talvez amanhã que queremos toohave postagens trate uma lista de categorias ou hashtags associados a eles, Cosmos DB Olá novos documentos com hello adicionar atributos com e sem extras trabalho necessário por nós.

Os comentários em uma postagem podem ser tratados da mesma forma como outras postagens com uma propriedade pai (isso simplifica nosso mapeamento de objeto). 

    {
        "id":"1234-asd3-54ts-199a",
        "title":"Awesome post!",
        "date":"2016-01-02",
        "createdBy":User2,
        "parent":"ew12-res2-234e-544f"
    }

    {
        "id":"asd2-fee4-23gc-jh67",
        "title":"Ditto!",
        "date":"2016-01-03",
        "createdBy":User3,
        "parent":"ew12-res2-234e-544f"
    }

Além disso, todas as interações sociais podem ser armazenadas em um objeto separado como contadores:

    {
        "id":"dfe3-thf5-232s-dse4",
        "post":"ew12-res2-234e-544f",
        "comments":2,
        "likes":10,
        "points":200
    }

A criação de feeds resume-se à criação de documentos que podem reter uma lista de IDs da postagem com determinada ordem de relevância:

    [
        {"relevance":9, "post":"ew12-res2-234e-544f"},
        {"relevance":8, "post":"fer7-mnb6-fgh9-2344"},
        {"relevance":7, "post":"w34r-qeg6-ref6-8565"}
    ]

Poderíamos ter um fluxo "mais recente" com postagens ordenadas por data de criação, um fluxo "mais" com as postagens com mais gosta em Olá últimas 24 horas, poderíamos mesmo implementar um fluxo personalizado para cada usuário com base em lógica como seguidores e interesses e ainda seria uma lista de  postagens. É uma questão de como toobuild essas listas, mas o desempenho de leitura Olá permanece maneira ilimitado. Quando é adquirir uma dessas listas, podemos emitir tooCosmos uma única consulta DB usando Olá [no operador](documentdb-sql-query.md#WhereClause) tooobtain páginas de postagens por vez.

Olá feed fluxos poderia ser criada usando [serviços de aplicativos do Azure](https://azure.microsoft.com/services/app-service/) processos de plano de fundo: [Webjobs](../app-service-web/web-sites-create-web-jobs.md). Quando uma mensagem é criada, o processamento em segundo plano pode ser acionado por usando [armazenamento do Azure](https://azure.microsoft.com/services/storage/) [filas](../storage/queues/storage-dotnet-how-to-use-queues.md) e Webjobs disparados usando Olá [SDK do Azure Webjobs](../app-service-web/websites-dotnet-webjobs-sdk.md), implementação Olá lançar propagação dentro de fluxos com base em nossa própria lógica personalizada. 

Pontos e semelhante em uma postagem pode ser processados de maneira adiada usando esse mesmo toocreate de técnica um ambiente finalmente consistente.

Os seguidores são mais complicados. Cosmos banco de dados tem um limite de tamanho máximo de documento e leitura/gravação documentos grandes podem afetar a escalabilidade de saudação do seu aplicativo. Portanto, pense em armazenar seguidores como um documento com esta estrutura:

    {
        "id":"234d-sd23-rrf2-552d",
        "followersOf": "dse4-qwe2-ert4-aad2",
        "followers":[
            "ewr5-232d-tyrg-iuo2",
            "qejh-2345-sdf1-ytg5",
            //...
            "uie0-4tyg-3456-rwjh"
        ]
    }

Isso pode funcionar para um usuário com alguns milhares seguidores, mas se alguns celebridade une nosso classificações, essa abordagem levará o tamanho do documento grande tooa e pode limitar a tamanho do documento hello eventualmente ocorrências.

toosolve isso, podemos usar uma abordagem mista. Como parte do documento de estatísticas do usuário hello, pode armazenar o número de saudação de seguidores:

    {
        "id":"234d-sd23-rrf2-552d",
        "user": "dse4-qwe2-ert4-aad2",
        "followers":55230,
        "totalPosts":452,
        "totalPoints":11342
    }

E o gráfico real de saudação do seguidores pode ser armazenado usando o banco de dados do Azure Cosmos [API do Graph Gremlin](../cosmos-db/graph-introduction.md), toocreate [vértices](http://mathworld.wolfram.com/GraphVertex.html) para cada usuário e [bordas](http://mathworld.wolfram.com/GraphEdge.html) que mantêm hello " Relações de maneira-A-B". Olá Graph API permite não apenas obter seguidores Olá de um determinado usuário mas criar consultas mais complexas tooeven sugerir pessoas em comum. Se adicionarmos Olá de gráfico toohello categorias de conteúdo que as pessoas como ou Desfrute, podemos começar dando experiências que incluem a descoberta de conteúdo inteligente, sugerindo conteúdo aqueles seguimos como ou localizar pessoas com quem pode temos muito em comum.

documento de estatísticas do usuário Olá ainda pode ser toocreate usados cartões Olá da interface do usuário ou visualizações de perfil rápido.

## <a name="hello-ladder-pattern-and-data-duplication"></a>Olá duplicação de dados e o padrão "Pirâmide"
Como você deve ter notado no documento JSON Olá que faz referência a uma postagem, há várias ocorrências de um usuário. E você deve ter percebido direita, que isso significa que informações Olá que representa um usuário, considerando esta desnormalização, podem estar presentes em mais de um local.

Ordem tooallow para consultas mais rápidas, tivermos eliminação de duplicação de dados. problema Olá esse efeito colateral é que, se por alguma ação, as alterações de dados do usuário, é preciso toofind todas as atividades de saudação ele nunca foi e atualizá-los todos os. Não parece muito prático, certo?

Estamos toosolve contínuo-identificando Olá atributos de chave de um usuário que mostramos em nosso aplicativo para cada atividade. Se Mostrar uma postagem em nosso aplicativo visualmente e mostrar apenas do criador de saudação do nome e imagem, por que armazena todos os dados do usuário Olá no atributo createdBy"hello"? Se cada comentário apenas mostramos imagem saudação do usuário, nós não precisa realmente restante Olá das suas informações. Isso é que algo que posso chamar hello "Escada padrão" entra em cena.

Vamos usar as informações do usuário como exemplo:

    {
        "id":"dse4-qwe2-ert4-aad2",
        "name":"John",
        "surname":"Doe",
        "address":"742 Evergreen Terrace",
        "birthday":"1983-05-07",
        "email":"john@doe.com",
        "twitterHandle":"@john",
        "username":"johndoe",
        "password":"some_encrypted_phrase",
        "totalPoints":100,
        "totalPosts":24
    }

Examinando essas informações, podemos detectar rapidamente quais informações são críticas e quais não são, criando, assim, uma “Escada”:

![Diagrama de um padrão de escada](./media/social-media-apps/social-media-apps-ladder.png)

etapa menor Olá é chamada um UserChunk, Olá mínimo informação que identifica um usuário e é usado para eliminação de duplicação de dados. Reduzindo o tamanho de Olá Olá duplicado tooonly Olá de informações de dados "mostramos", podemos reduzir possibilidade Olá atualizações grandes.

etapa intermediária Olá é chamada de usuário Olá, é dados completa de saudação que serão usados na maioria das consultas dependentes de desempenho no banco de dados do Cosmos, Olá mais críticos e acessados. Ela inclui informações de saudação representadas por um UserChunk.

Olá maior é hello usuário estendido. Ele inclui todas as informações de usuário crítica hello e outros dados que realmente não exigem leitura toobe rapidamente ou seu uso é eventual (como o processo de logon de saudação). Esses dados podem ser armazenados fora do Cosmos DB, no Banco de Dados SQL do Azure ou nas Tabelas de Armazenamento do Azure.

Por que seria é dividir usuário hello e até mesmo armazenar essas informações em diferentes locais? Como de um ponto de vista de desempenho, hello documentos Olá maiores, Olá costlier consultas de saudação. Manter documentos fino, Olá direito toodo informações sobre consultas de todos os seus dependentes de desempenho para sua rede social e repositório Olá outras informações extras para eventual cenários como, o perfil completo edições, logons, até mesmo a mineração de dados para análise de uso e grande Iniciativas de dados. Realmente não importa se Olá coleta de dados para mineração de dados são mais lentos porque ele está em execução no banco de dados do SQL Azure, podemos ter preocupar embora que nossos usuários tenham uma experiência rápida e fina. Um usuário, armazenado no Cosmos DB, teria esta aparência:

    {
        "id":"dse4-qwe2-ert4-aad2",
        "name":"John",
        "surname":"Doe",
        "username":"johndoe"
        "email":"john@doe.com",
        "twitterHandle":"@john"
    }

E um Post teria a seguinte aparência:

    {
        "id":"1234-asd3-54ts-199a",
        "title":"Awesome post!",
        "date":"2016-01-02",
        "createdBy":{
            "id":"dse4-qwe2-ert4-aad2",
            "username":"johndoe"
        }
    }

E quando uma edição surge em que um dos atributos de saudação do bloco Olá é afetado, é fácil toofind documentos de saudação afetado por meio de consultas que aponte toohello indexado atributos (selecione * FROM postagens p WHERE p.createdBy.id = = "edited_user_id") e, em seguida, atualizando partes de saudação.

## <a name="hello-search-box"></a>caixa de pesquisa Olá
Felizmente, os usuários vão gerar muito conteúdo. E nós deve ser capaz de tooprovide Olá capacidade toosearch e localizar conteúdo que pode não ser diretamente em seus fluxos de conteúdo, talvez porque não seguimos criadores de hello, ou talvez nós são simplesmente tentar toofind essa postagem antiga que fizemos 6 meses atrás.

Felizmente, e porque estamos usando o banco de dados do Azure Cosmos, podemos facilmente implementar um mecanismo de pesquisa usando [pesquisa do Azure](https://azure.microsoft.com/services/search/) em alguns minutos e sem digitar uma única linha de código (diferente de saudação obviamente, procure o processo e a interface do usuário).

Por que isso é tão fácil?

A pesquisa do Azure implementa o que eles chamam [indexadores](https://msdn.microsoft.com/library/azure/dn946891.aspx), plano de fundo processa esse gancho em seus repositórios de dados e forma mágica adicionar, atualizar ou remover os objetos em índices de saudação. Eles dão suporte a [indexadores do Banco de Dados SQL do Azure](https://blogs.msdn.microsoft.com/kaevans/2015/03/06/indexing-azure-sql-database-with-azure-search/), [indexadores dos Blobs do Azure](../search/search-howto-indexing-azure-blob-storage.md) e, ainda bem, [indexadores do Azure Cosmos DB](../search/search-howto-index-documentdb.md). Olá transição de informações do banco de dados do Cosmos tooAzure pesquisa é simples, como ambas as informações do repositório no formato JSON, precisamos apenas muito[criar nosso índice](../search/search-create-index-portal.md) e mapear os atributos de nossos documentos queremos indexadas e isto é, em questão de minutos (depende de tamanho de saudação de nossos dados), todos os nossos conteúdo estará disponível toobe pesquisado com, pelo melhor solução de pesquisa como um serviço Olá na infraestrutura de nuvem. 

Para obter mais informações sobre a pesquisa do Azure, você pode visitar Olá [tooSearch de guia do Hitchhiker](https://blogs.msdn.microsoft.com/mvpawardprogram/2016/02/02/a-hitchhikers-guide-to-search/).

## <a name="hello-underlying-knowledge"></a>Conhecimento subjacente Olá
Depois de armazenar todo esse conteúdo que aumenta a cada dia, talvez comecemos a pensar: O que posso fazer com todo esse fluxo de informações de meus usuários?

resposta de saudação é simples: colocá-la toowork e aprender com ele.

Mas o que podemos aprender? Alguns exemplos simples: [análise de sentimento](https://en.wikipedia.org/wiki/Sentiment_analysis), conteúdo recomendações com base nas preferências do usuário ou até mesmo um moderador conteúdo automatizada que garante que todos os Olá conteúdo publicado por nossa rede social é seguro para Olá família.

Agora que obtive você conectado, será provavelmente imagina precisar alguns PhD em Matemática Ciência tooextract esses padrões e as informações de arquivos e bancos de dados simples, mas está errado.

[O aprendizado de máquina do Azure](https://azure.microsoft.com/services/machine-learning/), parte da saudação [Cortana Intelligence Suite](https://www.microsoft.com/en/server-cloud/cortana-analytics-suite/overview.aspx), é um serviço de nuvem totalmente gerenciado que lhe permite criar fluxos de trabalho usando algoritmos em uma interface simple de arrastar e soltar, código de seus próprios algoritmos de hello em [R](https://en.wikipedia.org/wiki/R_\(programming_language\)) ou usar alguns dos Olá já criado e pronto toouse APIs, como: [análises de texto](https://gallery.cortanaanalytics.com/MachineLearningAPI/Text-Analytics-2), [moderador conteúdo](https://www.microsoft.com/moderator) ou [recomendações](https://gallery.cortanaanalytics.com/MachineLearningAPI/Recommendations-2).

tooachieve qualquer desses cenários de aprendizado de máquina, podemos usar [Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/) tooingest Olá informações de diferentes fontes e usar [U-SQL](https://azure.microsoft.com/documentation/videos/data-lake-u-sql-query-execution/) tooprocess Olá informações e gerar uma saída que podem ser processadas pelo aprendizado de máquina do Azure.

Outra opção disponível é toouse [serviços Cognitivos Microsoft](https://www.microsoft.com/cognitive-services) tooanalyze nossos usuários conteúdos; não só podemos compreendê-los melhor (por meio de análise de escrever com [API de análise de texto](https://www.microsoft.com/cognitive-services/en-us/text-analytics-api)), mas também pode detectar conteúdo indesejado ou consolidado e agir de acordo com [API de visão do computador](https://www.microsoft.com/cognitive-services/en-us/computer-vision-api). Serviços cognitivos incluem muitas soluções prontas para uso que não exigem qualquer tipo de aprendizado de máquina toouse de dados de Conhecimento.

## <a name="a-planet-scale-social-experience"></a>Uma experiência social em grande escala
Por último, mas não menos importante, há um tópico importante que devo abordar: **escalabilidade**. Durante a criação de uma arquitetura é crucial que cada componente pode ser dimensionado por conta própria, ou porque precisamos tooprocess mais dados ou queremos toohave uma cobertura geográfica maior (ou ambos!). Felizmente, realizar uma tarefa complexa como essa é uma **experiência turnkey** com o Cosmos DB.

Cosmos banco de dados oferece suporte a [o particionamento dinâmico](https://azure.microsoft.com/blog/10-things-to-know-about-documentdb-partitioned-collections/) -de-prontos, automaticamente Criando partições com base em um determinado **chave de partição** (definido como um dos atributos de saudação em seus documentos). Definindo Olá correto de chave de partição deve ser feita em tempo de design e manter no hello mente [práticas recomendadas](../cosmos-db/partition-data.md#designing-for-partitioning) disponível; no caso de saudação de uma experiência social, sua estratégia de particionamento deve estar alinhada com forma Olá consultar (leituras dentro de saudação a mesma partição são desejáveis) e gravar (evite "pontos de acesso" Distribuindo gravações em várias partições). Algumas opções são: partições com base em uma chave de tempo (dia/mês/semana), por categoria de conteúdo, por região geográfica, por usuário. tudo realmente depende de como você consultar dados hello e mostrá-la em sua experiência social. 

Um ponto interessante vale a pena mencionar é que o banco de dados do Cosmos executará suas consultas (incluindo [agregações](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/)) em todas as partições de forma transparente, não é necessário tooadd qualquer lógica à medida que aumenta de seus dados.

Com o tempo, em última análise, você terá um aumento no tráfego e no consumo de recursos (medido em [RUs](request-units.md), ou Unidades de Solicitação). Você lerá e gravará com mais frequência do que seu userbase cresce e eles começarão a criar e ler mais conteúdo; Olá a capacidade de **dimensionamento a taxa de transferência** é vital. Aumentar nossas RUs é muito fácil, poderemos fazer isso com alguns cliques no hello Portal do Azure ou por [emitir comandos por meio de saudação API](https://docs.microsoft.com/rest/api/documentdb/replace-an-offer).

![Aumentando e definindo uma chave de partição](./media/social-media-apps/social-media-apps-scaling.png)

Se as coisas ficarem cada vez melhores e usuários de outra região, país ou continente descobrirem sua plataforma e começarem a usá-la, será uma ótima surpresa!

Mas, aguarde... em breve você percebe sua experiência com a plataforma não é ideal; até agora, eles são longe de sua região operacional, que latência Olá é terrível e obviamente não deseja que elas tooquit. Se houvesse uma maneira fácil de **estender seu alcance global**... mas há!

Cosmos banco de dados permite que você [replicar seus dados globalmente](../cosmos-db/tutorial-global-distribution-documentdb.md) e transparente com alguns cliques e automaticamente, selecione entre as regiões disponíveis de saudação do seu [código de cliente](../cosmos-db/tutorial-global-distribution-documentdb.md). Isso também significa que é possível ter [várias regiões de failover](regional-failover.md). 

Quando você replica os dados globais, será necessário toomake-se de que os clientes podem tirar proveito dele. Se você estiver usando um front-end da web ou acessar APIs de cliente móveis, você pode implantar [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) e clonar seu serviço de aplicativo do Azure em todas as regiões de saudação desejada, usando um [configuração desempenho](../app-service-web/web-sites-traffic-manager.md)toosupport sua cobertura global estendida. Quando os clientes acessam o front-end ou APIs, eles serão roteada toohello mais próximo serviço de aplicativo, que por sua vez, se conectará toohello réplica de banco de dados do Cosmos local.

![Adicionando plataforma social tooyour de cobertura global](./media/social-media-apps/social-media-apps-global-replicate.png)

## <a name="conclusion"></a>Conclusão
Este artigo tenta tooshed alguns claro em alternativas de saudação de criação de redes sociais completamente no Azure com serviços de baixo custo e fornecer excelentes resultados usando incentivando Olá uma distribuição de solução e os dados de várias camadas de armazenamento chamada "Pirâmide".

![Diagrama de interação entre os serviços do Azure para rede social](./media/social-media-apps/social-media-apps-azure-solution.png)

verdade Olá é que não há nenhum definitiva para esse tipo de cenários, ela tem Olá sinergia criada pela combinação de saudação de ótimos serviços que nos permitem toobuild grandes experiências: Olá velocidade e a liberdade de banco de dados do Azure Cosmos tooprovide um ótimo aplicativo social inteligência de saudação atrás de uma solução de pesquisa de primeira classe, como pesquisa do Azure, flexibilidade de saudação do toohost de serviços de aplicativo do Azure não mesmo idioma agnóstico aplicativos mas processos em segundo plano eficiente e Olá expansível armazenamento do Azure e banco de dados SQL Azure para armazenar grandes quantidades de dados e hello potência analítica de aprendizado de máquina do Azure toocreate conhecimento e inteligência que pode fornecer comentários tooour processos e ajude-na entregar Olá usuários toohello conteúdo à direita.

## <a name="next-steps"></a>Próximas etapas
toolearn mais informações sobre os casos de uso para Cosmos DB, consulte [casos de uso do banco de dados comum Cosmos](use-cases.md).
