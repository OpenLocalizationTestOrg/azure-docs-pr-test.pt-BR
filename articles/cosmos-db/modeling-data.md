---
title: dados de documento aaaModeling para um banco de dados NoSQL | Microsoft Docs
description: Saiba mais sobre a modelagem de dados para bancos de dados NoSQL
keywords: modelando dados
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig1
documentationcenter: 
ms.assetid: 69521eb9-590b-403c-9b36-98253a4c88b5
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2016
ms.author: arramac
ms.openlocfilehash: 2e388c833f204287896dfa8e6f79c88073731b6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="modeling-document-data-for-nosql-databases"></a>Modelando dados de documentos para bancos de dados NoSQL
Enquanto os bancos de dados independentes de esquema, como banco de dados do Azure Cosmos, facilitam super tooembrace modelo de dados de alterações tooyour você ainda deve levar algum tempo pensar sobre seus dados. 

Como a data será toobe armazenado? É como os dados do aplicativo vai tooretrieve e consulta? O aplicativo realizará grandes volumes de leitura e gravação? 

Depois de ler este artigo, você será capaz de tooanswer Olá perguntas a seguir:

* Como devo pensar em um documento num banco de dados de documentos?
* O que é modelagem de dados e como ele me afeta? 
* Como é a modelagem de dados em um documento banco de dados diferentes tooa banco de dados relacional?
* Como posso expressar relações de dados em um banco de dados não relacional?
* Ao incorporar a dados e ao vincular a toodata?

## <a name="embedding-data"></a>Inserindo dados
Quando você iniciar a modelagem de dados em um armazenamento de documentos, como o banco de dados do Azure Cosmos, tente tootreat suas entidades como **documentos autossuficientes** representado em JSON.

Antes de nos aprofundarmos demais, vamos voltar um pouco e ver como modelaríamos algo num banco de dados relacional, que é um processo que muitos de nós já conhecemos. Olá exemplo a seguir mostra como uma pessoa pode ser armazenada em um banco de dados relacional. 

![Modelo de banco de dados relacional](./media/documentdb-modeling-data/relational-data-model.png)

Ao trabalhar com bancos de dados relacionais, já foi apresentados para toonormalize anos, normalizar, normalizar.

Normalizar os dados geralmente envolve a criação de uma entidade, como uma pessoa e dividi-la em toodiscrete partes de dados. O exemplo hello acima, uma pessoa pode ter vários registros de detalhe de contato, bem como vários registros de endereço. Nós ainda vamos além e dividimos os detalhes de contato extraindo campos comuns, como tipo. O mesmo vale para o endereço, cada registro tem um tipo, como *Residencial* ou *Comercial* 

Olá guiando local quando a normalização dos dados é muito**evitar armazenar dados redundantes** em cada registro e em vez disso, consulte toodata. Neste exemplo, tooread uma pessoa, com todos os seus detalhes de contato e endereços, é necessário toouse junções tooeffectively-agregado seus dados em tempo de execução.

    SELECT p.FirstName, p.LastName, a.City, cd.Detail
    FROM Person p
    JOIN ContactDetail cd ON cd.PersonId = p.Id
    JOIN ContactDetailType on cdt ON cdt.Id = cd.TypeId
    JOIN Address a ON a.PersonId = p.Id

Atualizar uma pessoa, com seus detalhes de contato e endereço, demanda várias operações de gravação em várias tabelas individuais. 

Agora vamos dar uma olhada em como podemos seria modelo Olá mesmo dados como uma entidade independente em um banco de dados do documento.

    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "addresses": [
            {            
                "line1": "100 Some Street",
                "line2": "Unit 1",
                "city": "Seattle",
                "state": "WA",
                "zip": 98012
            }
        ],
        "contactDetails": [
            {"email: "thomas@andersen.com"},
            {"phone": "+1 555 555-5555", "extension": 5555}
        ] 
    }

Usando a abordagem de saudação acima, temos agora **desnormalizados** Olá registro pessoa onde podemos **inserido** todos Olá informações relacionadas toothis pessoa, como seus detalhes de contato e endereços em tooa único Documento JSON.
Além disso, porque não podemos está restrita tooa esquema fixo que temos Olá flexibilidade toodo itens, como com detalhes de contato de diferentes formas completamente. 

Recuperar um registro de pessoa completa do banco de dados de saudação agora é uma única operação em uma única coleção e de um único documento de leitura. A atualização do registro de uma pessoa, com seus detalhes de contato e endereços, também é feita em uma única operação de gravação, de um único documento.

Por desnormalização de dados, seu aplicativo pode ser necessário tooissue menos consultas e atualizações toocomplete operações comuns. 

### <a name="when-tooembed"></a>Quando tooembed
De modo geral, use modelos de dados inseridos quando:

* Houver relações de **contém** entre entidades.
* Houver relações **de um para poucos** entre entidades.
* Houver dados inseridos que são **alterados com pouca frequência**.
* Houver dados inseridos que não crescerão **sem limite**.
* Dados inseridos é **integral** toodata em um documento.

> [!NOTE]
> De modo geral, modelos de dados desnormalizados oferecem melhor desempenho de **leitura** .
> 
> 

### <a name="when-not-tooembed"></a>Quando não tooembed
Enquanto Olá regra geral em um banco de dados de documento é toodenormalize tudo e inserir todos os dados no documento único tooa, isso pode levar a situações toosome que devem ser evitadas.

Veja este trecho de JSON.

    {
        "id": "1",
        "name": "What's new in hello coolest Cloud",
        "summary": "A blog post by someone real famous",
        "comments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from hello interwebs"},
            …
            {"id": 100001, "author": "jane", "comment": "and on we go ..."},
            …
            {"id": 1000000001, "author": "angry", "comment": "blah angry blah angry"},
            …
            {"id": ∞ + 1, "author": "bored", "comment": "oh man, will this ever end?"},
        ]
    }

Uma entidade de postagem com comentários inseridos seria assim se estivéssemos modelando um sistema de blog comum, ou CMS. problema com este exemplo Hello é que hello a matriz de comentários é **unbounded**, que significa que há um número de toohello de limite (prático) de qualquer publicação único pode ter de comentários. Isso se tornará um problema como tamanho de saudação do documento hello pode crescer significativamente.

Como tamanho de saudação do hello documento expande os dados de saudação do hello capacidade tootransmit pela transmissão hello, bem como a leitura e atualização documento hello, em grande escala, será afetado.

Nesse caso seria melhor Olá tooconsider modelo a seguir.

    Post document:
    {
        "id": "1",
        "name": "What's new in hello coolest Cloud",
        "summary": "A blog post by someone real famous",
        "recentComments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from hello interwebs"},
            {"id": 3, "author": "jane", "comment": "....."}
        ]
    }

    Comment documents:
    {
        "postId": "1"
        "comments": [
            {"id": 4, "author": "anon", "comment": "more goodness"},
            {"id": 5, "author": "bob", "comment": "tails from hello field"},
            ...
            {"id": 99, "author": "angry", "comment": "blah angry blah angry"}
        ]
    },
    {
        "postId": "1"
        "comments": [
            {"id": 100, "author": "anon", "comment": "yet more"},
            ...
            {"id": 199, "author": "bored", "comment": "will this ever end?"}
        ]
    }

Este modelo tem comentários mais recentes de Olá três incorporados em Olá postagem em si, que é uma matriz com um limite fixo isso tempo. Olá outros comentários são agrupados em toobatches de 100 comentários e armazenados em documentos separados. tamanho de saudação do lote Olá foi escolhido como 100 como nosso aplicativo fictício permite Olá 100 comentários do usuário tooload por vez.  

Outro caso em que a inserção de dados não são uma boa ideia é quando Olá inseridos dados são usados frequentemente em documentos e serão alterados com frequência. 

Veja este trecho de JSON.

    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "holdings": [
            {
                "numberHeld": 100,
                "stock": { "symbol": "zaza", "open": 1, "high": 2, "low": 0.5 }
            },
            {
                "numberHeld": 50,
                "stock": { "symbol": "xcxc", "open": 89, "high": 93.24, "low": 88.87 }
            }
        ]
    }

Isto pode representar o portfólio de ações de alguém. Escolhemos informações sobre ações de saudação tooembed no documento de portfólio de tooeach. Em um ambiente em que os dados relacionados mudar com frequência, como uma aplicativo, de comercialização de ações a inserção de dados que mudam frequentemente será toomean que você está atualizando constantemente cada documento portfólio toda vez que uma ação foi negociada.

A ação *zaza* pode ser negociada centenas de vezes em apenas um dia, e milhares de usuários podem ter a ação *zaza* em seus portfólios. Com um modelo de dados como Olá acima seria temos tooupdate milhares de documentos de portfólio muitas vezes diariamente principal sistema tooa dimensionamento muito bem. 

## <a id="Refer"></a>Fazendo referência a dados
Inserir dados funciona bem em muitos casos, mas claramente há situações em que desnormalizar seus dados trará mais problemas do que soluções. E o que podemos fazer? 

Bancos de dados relacionais não estão local somente hello, onde você pode criar relações entre entidades. Em um banco de dados de documento, você pode ter informações em um documento que relaciona realmente toodata em outros documentos. Agora, eu não estou defendendo por até um minuto que criamos sistemas que seriam melhor adequado tooa banco de dados relacional no banco de dados do Azure Cosmos ou qualquer outro banco de dados de documento, mas relações simples são permitidas e podem ser muito útil. 

Olá JSON abaixo escolhemos toouse exemplo hello um portfólio de ações de anteriormente mas, desta vez, que fazemos referência de item de estoque toohello no portfólio de saudação em vez de incorporá-las. Dessa forma, quando o item de estoque Olá alterados com frequência Olá dia Olá somente documento que precisa toobe atualizado é único documento de estoque de saudação. 

    Person document:
    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "holdings": [
            { "numberHeld":  100, "stockId": 1},
            { "numberHeld":  50, "stockId": 2}
        ]
    }

    Stock documents:
    {
        "id": "1",
        "symbol": "zaza",
        "open": 1,
        "high": 2,
        "low": 0.5,
        "vol": 11970000,
        "mkt-cap": 42000000,
        "pe": 5.89
    },
    {
        "id": "2",
        "symbol": "xcxc",
        "open": 89,
        "high": 93.24,
        "low": 88.87,
        "vol": 2970200,
        "mkt-cap": 1005000,
        "pe": 75.82
    }


Porém, uma abordagem de toothis desvantagem imediata é se o aplicativo é necessário tooshow informações sobre cada ação que é mantida ao exibir o portfólio de uma pessoa; Nesse caso seria necessário toomake várias viagens toohello banco de dados tooload Olá informações para cada documento de estoque. Aqui, fizemos uma decisão tooimprove Olá a eficiência das operações de gravação, o que acontecer com frequência ao longo do dia hello, mas por sua vez comprometido em Olá operações de leitura que potencialmente tem menos impacto no desempenho de saudação do sistema específico.

> [!NOTE]
> Normalizado modelos de dados **pode exigir mais viagens de ida e** toohello server.
> 
> 

### <a name="what-about-foreign-keys"></a>E as chaves estrangeiras?
Porque não há nenhum conceito de uma restrição, chave estrangeira ou caso contrário, todas as relações entre documentos que você tem em documentos são efetivamente "fracos" e não serão verificadas pela Olá próprio banco de dados. Se você quiser tooensure que Olá dados que se refere a um documento tooactually existir, você precisará toodo isso em seu aplicativo, ou por meio do uso de saudação do lado do servidor gatilhos ou procedimentos armazenados no banco de dados do Azure Cosmos.

### <a name="when-tooreference"></a>Quando tooreference
De modo geral, use modelos de dados normalizados quando:

* Representar relações de **um para muitos** .
* Representar relações de **muitos para muitos** .
* Dados relacionados **mudarem com frequência**.
* Dados referenciados podem ser **ilimitados**.

> [!NOTE]
> De moro geral, normalizar traz melhor desempenho de **gravação** .
> 
> 

### <a name="where-do-i-put-hello-relationship"></a>Onde posso colocar relação Olá?
crescimento de saudação do relacionamento Olá ajudam a determinar na qual referência toostore hello.

Se observarmos Olá JSON abaixo que modela editores e manuais.

    Publisher document:
    {
        "id": "mspress",
        "name": "Microsoft Press",
        "books": [ 1, 2, 3, ..., 100, ..., 1000]
    }

    Book documents:
    {"id": "1", "name": "Azure Cosmos DB 101" }
    {"id": "2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "3", "name": "Taking over hello world one JSON doc at a time" }
    ...
    {"id": "100", "name": "Learn about Azure Cosmos DB" }
    ...
    {"id": "1000", "name": "Deep Dive in tooAzure Cosmos DB" }

Se o número de saudação de manuais Olá por publicador é pequeno com crescimento limitado, armazenando referência de catálogo Olá Olá publicador documento pode ser útil. No entanto, se o número de saudação de livros por publicador é não vinculado, esse modelo de dados levaria toomutable, aumentando a matrizes, como no documento do publisher exemplo hello acima. 

Alternar as coisas em torno de um bit seria resultará em um modelo que representa ainda Olá os mesmos dados mas agora evita essas coleções mutáveis grandes.

    Publisher document: 
    {
        "id": "mspress",
        "name": "Microsoft Press"
    }

    Book documents: 
    {"id": "1","name": "Azure Cosmos DB 101", "pub-id": "mspress"}
    {"id": "2","name": "Azure Cosmos DB for RDBMS Users", "pub-id": "mspress"}
    {"id": "3","name": "Taking over hello world one JSON doc at a time"}
    ...
    {"id": "100","name": "Learn about Azure Cosmos DB", "pub-id": "mspress"}
    ...
    {"id": "1000","name": "Deep Dive in tooAzure Cosmos DB", "pub-id": "mspress"}

Em Olá exemplo acima, podemos ter removido Olá coleção não vinculada no documento do publisher hello. Em vez disso, basta que um publicador de toohello uma referência em cada documento de catálogo.

### <a name="how-do-i-model-manymany-relationships"></a>Como eu modelo relações de muitos para muitos?
Em um banco de dados relacional, relações *muitos:muitos* frequentemente são modeladas com tabelas de junção, que simplesmente reúnem os registros de outras tabelas. 

![Associar tabelas](./media/documentdb-modeling-data/join-table.png)

Você pode ser tentado tooreplicate Olá mesma coisa usando documentos e produzir um modelo de dados que pesquisa a seguir toohello semelhante.

    Author documents: 
    {"id": "a1", "name": "Thomas Andersen" }
    {"id": "a2", "name": "William Wakefield" }

    Book documents:
    {"id": "b1", "name": "Azure Cosmos DB 101" }
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "b3", "name": "Taking over hello world one JSON doc at a time" }
    {"id": "b4", "name": "Learn about Azure Cosmos DB" }
    {"id": "b5", "name": "Deep Dive in tooAzure Cosmos DB" }

    Joining documents: 
    {"authorId": "a1", "bookId": "b1" }
    {"authorId": "a2", "bookId": "b1" }
    {"authorId": "a1", "bookId": "b2" }
    {"authorId": "a1", "bookId": "b3" }

Isso funcionaria. No entanto, carregar ou um autor com seus livros ou carregar um livro com seu autor, sempre exigem pelo menos duas consultas adicionais no banco de dados de saudação. Toohello de uma consulta unir o documento e, em seguida, outra consulta toofetch Olá real documento sendo unidas. 

Se tudo o que a tabela de junção está fazendo é unir dois dados, por que não simplesmente removê-la?
Considere o seguinte hello.

    Author documents:
    {"id": "a1", "name": "Thomas Andersen", "books": ["b1, "b2", "b3"]}
    {"id": "a2", "name": "William Wakefield", "books": ["b1", "b4"]}

    Book documents: 
    {"id": "b1", "name": "Azure Cosmos DB 101", "authors": ["a1", "a2"]}
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users", "authors": ["a1"]}
    {"id": "b3", "name": "Learn about Azure Cosmos DB", "authors": ["a1"]}
    {"id": "b4", "name": "Deep Dive in tooAzure Cosmos DB", "authors": ["a2"]}

Agora, se eu tivesse um autor, saber imediatamente quais livros que foram gravadas, e por outro lado se eu tivesse um documento de livro carregado seria sei ids de saudação dos autores de saudação. Isso economiza intermediária consulta em relação à tabela de junção Olá reduzindo o número de saudação do servidor de viagens de ida e seu aplicativo tiver toomake. 

## <a id="WrapUp"></a>Modelos de dados híbridos
Nós vimos que inserir (ou desnormalizar) e referenciar (ou normalizar) dados têm suas vantagens e desvantagens. 

Ele não sempre têm toobe ou, não tenham toomix assustados coisas um pouco. 

Com base em padrões de uso específicos e pode haver casos onde incorporado a combinação de cargas de trabalho do seu aplicativo e dados referenciados faz sentido e pôde lead toosimpler a lógica do aplicativo com o servidor menos processamentos e ainda manter um bom nível de desempenho .

Considere Olá JSON a seguir. 

    Author documents: 
    {
        "id": "a1",
        "firstName": "Thomas",
        "lastName": "Andersen",        
        "countOfBooks": 3,
         "books": ["b1", "b2", "b3"],
        "images": [
            {"thumbnail": "http://....png"}
            {"profile": "http://....png"}
            {"large": "http://....png"}
        ]
    },
    {
        "id": "a2",
        "firstName": "William",
        "lastName": "Wakefield",
        "countOfBooks": 1,
        "books": ["b1"],
        "images": [
            {"thumbnail": "http://....png"}
        ]
    }

    Book documents:
    {
        "id": "b1",
        "name": "Azure Cosmos DB 101",
        "authors": [
            {"id": "a1", "name": "Thomas Andersen", "thumbnailUrl": "http://....png"},
            {"id": "a2", "name": "William Wakefield", "thumbnailUrl": "http://....png"}
        ]
    },
    {
        "id": "b2",
        "name": "Azure Cosmos DB for RDBMS Users",
        "authors": [
            {"id": "a1", "name": "Thomas Andersen", "thumbnailUrl": "http://....png"},
        ]
    }

Aqui nós (principalmente) seguiu modelo incorporado hello, onde os dados de outras entidades são inseridos no documento de nível superior Olá, mas outros dados são referenciados. 

Se você examinar o documento de livro Olá, podemos ver algumas interessantes campos quando vamos examinar a matriz de saudação de autores. Há um *id* campo que é o campo de saudação usar documentos de autor back tooan toorefer, prática padrão em um modelo normalizado, mas, em seguida, podemos também ter *nome* e *thumbnailUrl*. Pode apenas adotamos *id* e deixado Olá aplicativo tooget qualquer informação adicional, ela necessária do documento do respectivos autor hello usando hello "link", mas como nosso aplicativo exibe o nome do autor hello e um imagem em miniatura com cada livro exibido poderemos salvar um servidor de toohello de ida e volta por catálogo em uma lista por desnormalização **alguns** dados de autor hello.

Obviamente, se o nome do autor Olá alterado ou quisessem tooupdate suas fotos haveria toogo uma atualização de todos os livros que nunca de publicados, mas para nosso aplicativo, com base na suposição de saudação que os autores não alterem seus nomes com frequência, esse é um design aceitável decisão.  

No exemplo hello há **pré-calculada agregações** toosave caro de processamento em uma operação de leitura de valores. Exemplo hello, alguns dos dados Olá inseridos no documento de autor Olá são dados que são calculados em tempo de execução. Sempre que um novo catálogo é publicado, um documento de catálogo é criado **e** campo de countOfBooks Olá estiver definido como valor tooa calculado com base no número de saudação de documentos de catálogo que existem para um determinado autor. Essa otimização seria bom em sistemas de intenso leitura em que podemos pode toodo computações em gravações em ordem toooptimize leituras.

Olá capacidade toohave um modelo com campos calculados previamente é possibilitado porque oferece suporte a banco de dados do Azure Cosmos **transações de vários documentos**. Muitos repositórios NoSQL não podem fazer transações entre documentos e portanto defendem decisões de design, como "sempre incorporar tudo", devido a limitação de toothis. Com o Azure Cosmos DB, você pode usar gatilhos do lado do servidor ou procedimentos armazenados, que inserem manuais e atualizam autores, tudo isso em uma transação ACID. Agora você não **ter** tooembed tudo no tooone documento apenas toobe-se de que seus dados permaneçam consistentes.

## <a name="NextSteps"></a>Próximas etapas
argumentos de maiores Olá deste artigo é toounderstand que em um mundo independentes de esquema de modelagem de dados são tão importantes como nunca. 

Como não há nenhum toorepresent de maneira única uma parte dos dados em uma tela, não há nenhum toomodel de uma maneira de seus dados. Você precisa toounderstand seu aplicativo e como ele produzirá consumir e processar dados saudação. Em seguida, aplicando alguns Olá diretrizes apresentadas aqui, você podem definir sobre como criar um modelo que atenda às necessidades imediatas de saudação do seu aplicativo. Quando seus aplicativos precisam toochange, você pode aproveitar flexibilidade de saudação de um banco de dados independentes de esquema tooembrace que alterar e desenvolver seu modelo de dados facilmente. 

toolearn mais sobre Azure Cosmos DB, consulte do serviço toohello [documentação](https://azure.microsoft.com/documentation/services/cosmos-db/) página. 

toounderstand como tooshard seus dados por várias partições, consulte muito[particionamento de dados no banco de dados do Azure Cosmos](documentdb-partition-data.md). 
