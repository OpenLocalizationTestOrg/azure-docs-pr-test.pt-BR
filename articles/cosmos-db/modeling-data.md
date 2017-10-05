---
title: Modelando dados de documentos para um banco de dados NoSQL | Microsoft Docs
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
ms.openlocfilehash: 16c387fe574243544cf54cf283c7713ddcaa1942
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="modeling-document-data-for-nosql-databases"></a><span data-ttu-id="b68ab-104">Modelando dados de documentos para bancos de dados NoSQL</span><span class="sxs-lookup"><span data-stu-id="b68ab-104">Modeling document data for NoSQL databases</span></span>
<span data-ttu-id="b68ab-105">Embora bancos de dados sem esquemas, como o Azure Cosmos DB, facilitem muito a adoção de mudanças em seu modelo de dados, ainda é recomendável dedicar algum tempo para considerar os dados.</span><span class="sxs-lookup"><span data-stu-id="b68ab-105">While schema-free databases, like Azure Cosmos DB, make it super easy to embrace changes to your data model you should still spend some time thinking about your data.</span></span> 

<span data-ttu-id="b68ab-106">Como eles serão armazenados?</span><span class="sxs-lookup"><span data-stu-id="b68ab-106">How is data going to be stored?</span></span> <span data-ttu-id="b68ab-107">Como seu aplicativo vai recuperá-los e consultá-los?</span><span class="sxs-lookup"><span data-stu-id="b68ab-107">How is your application going to retrieve and query data?</span></span> <span data-ttu-id="b68ab-108">O aplicativo realizará grandes volumes de leitura e gravação?</span><span class="sxs-lookup"><span data-stu-id="b68ab-108">Is your application read heavy, or write heavy?</span></span> 

<span data-ttu-id="b68ab-109">Depois de ler este artigo, você poderá responder as seguintes perguntas:</span><span class="sxs-lookup"><span data-stu-id="b68ab-109">After reading this article, you will be able to answer the following questions:</span></span>

* <span data-ttu-id="b68ab-110">Como devo pensar em um documento num banco de dados de documentos?</span><span class="sxs-lookup"><span data-stu-id="b68ab-110">How should I think about a document in a document database?</span></span>
* <span data-ttu-id="b68ab-111">O que é modelagem de dados e como ele me afeta?</span><span class="sxs-lookup"><span data-stu-id="b68ab-111">What is data modeling and why should I care?</span></span> 
* <span data-ttu-id="b68ab-112">Como a modelagem de dados em um banco de dados de documentos difere da modelagem de dados em um banco de dados relacional?</span><span class="sxs-lookup"><span data-stu-id="b68ab-112">How is modeling data in a document database different to a relational database?</span></span>
* <span data-ttu-id="b68ab-113">Como posso expressar relações de dados em um banco de dados não relacional?</span><span class="sxs-lookup"><span data-stu-id="b68ab-113">How do I express data relationships in a non-relational database?</span></span>
* <span data-ttu-id="b68ab-114">Quando eu insiro dados e quando vinculo a eles?</span><span class="sxs-lookup"><span data-stu-id="b68ab-114">When do I embed data and when do I link to data?</span></span>

## <a name="embedding-data"></a><span data-ttu-id="b68ab-115">Inserindo dados</span><span class="sxs-lookup"><span data-stu-id="b68ab-115">Embedding data</span></span>
<span data-ttu-id="b68ab-116">Ao começar a modelar dados em um repositório de documentos, como o Azure Cosmos DB, tente tratar as entidades como **documentos independentes** representados em JSON.</span><span class="sxs-lookup"><span data-stu-id="b68ab-116">When you start modeling data in a document store, such as Azure Cosmos DB, try to treat your entities as **self-contained documents** represented in JSON.</span></span>

<span data-ttu-id="b68ab-117">Antes de nos aprofundarmos demais, vamos voltar um pouco e ver como modelaríamos algo num banco de dados relacional, que é um processo que muitos de nós já conhecemos.</span><span class="sxs-lookup"><span data-stu-id="b68ab-117">Before we dive in too much further, let us take a few steps back and have a look at how we might model something in a relational database, a subject many of us are already familiar with.</span></span> <span data-ttu-id="b68ab-118">O exemplo a seguir mostra como uma pessoa poderia ser armazenada em um banco de dados relacional.</span><span class="sxs-lookup"><span data-stu-id="b68ab-118">The following example shows how a person might be stored in a relational database.</span></span> 

![Modelo de banco de dados relacional](./media/documentdb-modeling-data/relational-data-model.png)

<span data-ttu-id="b68ab-120">Durante anos trabalhando com bancos de dados relacionais, aprendemos a normalizar, normalizar e normalizar.</span><span class="sxs-lookup"><span data-stu-id="b68ab-120">When working with relational databases, we've been taught for years to normalize, normalize, normalize.</span></span>

<span data-ttu-id="b68ab-121">Normalizar os dados geralmente envolve pegar uma entidade, como uma pessoa, e dividi-la em dados separados.</span><span class="sxs-lookup"><span data-stu-id="b68ab-121">Normalizing your data typically involves taking an entity, such as a person, and breaking it down in to discrete pieces of data.</span></span> <span data-ttu-id="b68ab-122">No exemplo acima, uma pessoa pode ter vários registros de detalhes de contato, bem como vários registros de endereço.</span><span class="sxs-lookup"><span data-stu-id="b68ab-122">In the example above, a person can have multiple contact detail records as well as multiple address records.</span></span> <span data-ttu-id="b68ab-123">Nós ainda vamos além e dividimos os detalhes de contato extraindo campos comuns, como tipo.</span><span class="sxs-lookup"><span data-stu-id="b68ab-123">We even go one step further and break down contact details by further extracting common fields like a type.</span></span> <span data-ttu-id="b68ab-124">O mesmo vale para o endereço, cada registro tem um tipo, como *Residencial* ou *Comercial*</span><span class="sxs-lookup"><span data-stu-id="b68ab-124">Same for address, each record here has a type like *Home* or *Business*</span></span> 

<span data-ttu-id="b68ab-125">A premissa que orienta a normalização de dados é **evitar armazenar dados redundantes** em cada registro e, em vez disso, referir-se a eles.</span><span class="sxs-lookup"><span data-stu-id="b68ab-125">The guiding premise when normalizing data is to **avoid storing redundant data** on each record and rather refer to data.</span></span> <span data-ttu-id="b68ab-126">Neste exemplo, para ler uma pessoa, com todos os endereços e detalhes de contato, você precisa usar junções para agregar os dados de modo eficaz em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="b68ab-126">In this example, to read a person, with all their contact details and addresses, you need to use JOINS to effectively aggregate your data at run time.</span></span>

    SELECT p.FirstName, p.LastName, a.City, cd.Detail
    FROM Person p
    JOIN ContactDetail cd ON cd.PersonId = p.Id
    JOIN ContactDetailType on cdt ON cdt.Id = cd.TypeId
    JOIN Address a ON a.PersonId = p.Id

<span data-ttu-id="b68ab-127">Atualizar uma pessoa, com seus detalhes de contato e endereço, demanda várias operações de gravação em várias tabelas individuais.</span><span class="sxs-lookup"><span data-stu-id="b68ab-127">Updating a single person with their contact details and addresses requires write operations across many individual tables.</span></span> 

<span data-ttu-id="b68ab-128">Agora, vejamos como nós modelaríamos os mesmos dados como uma entidade autossuficiente em um banco de dados de documentos.</span><span class="sxs-lookup"><span data-stu-id="b68ab-128">Now let's take a look at how we would model the same data as a self-contained entity in a document database.</span></span>

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

<span data-ttu-id="b68ab-129">Usando a abordagem acima, nós **desnormalizamos** o registro da pessoa, no qual **inserimos** todas as informações relacionadas à pessoa, como seus detalhes de contato e endereços, criando um único documento JSON.</span><span class="sxs-lookup"><span data-stu-id="b68ab-129">Using the approach above we have now **denormalized** the person record where we **embedded** all the information relating to this person, such as their contact details and addresses, in to a single JSON document.</span></span>
<span data-ttu-id="b68ab-130">Além disso, como não estamos restritos a um esquema fixo, nós temos a flexibilidade de, por exemplo, ter detalhes de contato com formas totalmente diferentes.</span><span class="sxs-lookup"><span data-stu-id="b68ab-130">In addition, because we're not confined to a fixed schema we have the flexibility to do things like having contact details of different shapes entirely.</span></span> 

<span data-ttu-id="b68ab-131">Agora, a recuperação do registro completo de uma pessoa do banco de dados é feita em somente uma operação de leitura, de uma única coleção e para um único documento.</span><span class="sxs-lookup"><span data-stu-id="b68ab-131">Retrieving a complete person record from the database is now a single read operation against a single collection and for a single document.</span></span> <span data-ttu-id="b68ab-132">A atualização do registro de uma pessoa, com seus detalhes de contato e endereços, também é feita em uma única operação de gravação, de um único documento.</span><span class="sxs-lookup"><span data-stu-id="b68ab-132">Updating a person record, with their contact details and addresses, is also a single write operation against a single document.</span></span>

<span data-ttu-id="b68ab-133">Com a desnormalização dos dados, seu aplicativo possivelmente precisará emitir menos consultas e atualizações para concluir operações comuns.</span><span class="sxs-lookup"><span data-stu-id="b68ab-133">By denormalizing data, your application may need to issue fewer queries and updates to complete common operations.</span></span> 

### <a name="when-to-embed"></a><span data-ttu-id="b68ab-134">Quando inserir</span><span class="sxs-lookup"><span data-stu-id="b68ab-134">When to embed</span></span>
<span data-ttu-id="b68ab-135">De modo geral, use modelos de dados inseridos quando:</span><span class="sxs-lookup"><span data-stu-id="b68ab-135">In general, use embedded data models when:</span></span>

* <span data-ttu-id="b68ab-136">Houver relações de **contém** entre entidades.</span><span class="sxs-lookup"><span data-stu-id="b68ab-136">There are **contains** relationships between entities.</span></span>
* <span data-ttu-id="b68ab-137">Houver relações **de um para poucos** entre entidades.</span><span class="sxs-lookup"><span data-stu-id="b68ab-137">There are **one-to-few** relationships between entities.</span></span>
* <span data-ttu-id="b68ab-138">Houver dados inseridos que são **alterados com pouca frequência**.</span><span class="sxs-lookup"><span data-stu-id="b68ab-138">There is embedded data that **changes infrequently**.</span></span>
* <span data-ttu-id="b68ab-139">Houver dados inseridos que não crescerão **sem limite**.</span><span class="sxs-lookup"><span data-stu-id="b68ab-139">There is embedded data won't grow **without bound**.</span></span>
* <span data-ttu-id="b68ab-140">Houver dados inseridos que são **integrais** aos dados de um documento.</span><span class="sxs-lookup"><span data-stu-id="b68ab-140">There is embedded data that is **integral** to data in a document.</span></span>

> [!NOTE]
> <span data-ttu-id="b68ab-141">De modo geral, modelos de dados desnormalizados oferecem melhor desempenho de **leitura** .</span><span class="sxs-lookup"><span data-stu-id="b68ab-141">Typically denormalized data models provide better **read** performance.</span></span>
> 
> 

### <a name="when-not-to-embed"></a><span data-ttu-id="b68ab-142">Quando não inserir</span><span class="sxs-lookup"><span data-stu-id="b68ab-142">When not to embed</span></span>
<span data-ttu-id="b68ab-143">Embora o princípio básico do banco de dados de documentos seja desnormalizar tudo e inserir todos os dados em um único documento, isso pode levar a alguma situações que devem ser evitadas.</span><span class="sxs-lookup"><span data-stu-id="b68ab-143">While the rule of thumb in a document database is to denormalize everything and embed all data in to a single document, this can lead to some situations that should be avoided.</span></span>

<span data-ttu-id="b68ab-144">Veja este trecho de JSON.</span><span class="sxs-lookup"><span data-stu-id="b68ab-144">Take this JSON snippet.</span></span>

    {
        "id": "1",
        "name": "What's new in the coolest Cloud",
        "summary": "A blog post by someone real famous",
        "comments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from the interwebs"},
            …
            {"id": 100001, "author": "jane", "comment": "and on we go ..."},
            …
            {"id": 1000000001, "author": "angry", "comment": "blah angry blah angry"},
            …
            {"id": ∞ + 1, "author": "bored", "comment": "oh man, will this ever end?"},
        ]
    }

<span data-ttu-id="b68ab-145">Uma entidade de postagem com comentários inseridos seria assim se estivéssemos modelando um sistema de blog comum, ou CMS.</span><span class="sxs-lookup"><span data-stu-id="b68ab-145">This might be what a post entity with embedded comments would look like if we were modeling a typical blog, or CMS, system.</span></span> <span data-ttu-id="b68ab-146">O problema com este exemplo é que a matriz de comentários é **ilimitada**, o que significa que não há limite (prático) para o número de comentários que qualquer postagem pode ter.</span><span class="sxs-lookup"><span data-stu-id="b68ab-146">The problem with this example is that the comments array is **unbounded**, meaning that there is no (practical) limit to the number of comments any single post can have.</span></span> <span data-ttu-id="b68ab-147">Isso se tornará um problema, pois o tamanho do documento poderá aumentar significativamente.</span><span class="sxs-lookup"><span data-stu-id="b68ab-147">This will become a problem as the size of the document could grow significantly.</span></span>

<span data-ttu-id="b68ab-148">Conforme o tamanho do documento aumenta, a capacidade de transmitir dados eletronicamente, bem como de ler e atualizar o documento, em escala, será afetada.</span><span class="sxs-lookup"><span data-stu-id="b68ab-148">As the size of the document grows the ability to transmit the data over the wire as well as reading and updating the document, at scale, will be impacted.</span></span>

<span data-ttu-id="b68ab-149">Nesse caso, seria melhor considerar o modelo a seguir.</span><span class="sxs-lookup"><span data-stu-id="b68ab-149">In this case it would be better to consider the following model.</span></span>

    Post document:
    {
        "id": "1",
        "name": "What's new in the coolest Cloud",
        "summary": "A blog post by someone real famous",
        "recentComments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from the interwebs"},
            {"id": 3, "author": "jane", "comment": "....."}
        ]
    }

    Comment documents:
    {
        "postId": "1"
        "comments": [
            {"id": 4, "author": "anon", "comment": "more goodness"},
            {"id": 5, "author": "bob", "comment": "tails from the field"},
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

<span data-ttu-id="b68ab-150">Este modelo tem os três comentários mais recentes inseridos na postagem em si, que é uma matriz com limite fixo.</span><span class="sxs-lookup"><span data-stu-id="b68ab-150">This model has the three most recent comments embedded on the post itself, which is an array with a fixed bound this time.</span></span> <span data-ttu-id="b68ab-151">Os outros comentários são agrupados em lotes de 100 e armazenados em documentos separados.</span><span class="sxs-lookup"><span data-stu-id="b68ab-151">The other comments are grouped in to batches of 100 comments and stored in separate documents.</span></span> <span data-ttu-id="b68ab-152">O tamanho de 100 foi escolhido para o lote porque nosso aplicativo fictício permite ao usuário carregar 100 comentários por vez.</span><span class="sxs-lookup"><span data-stu-id="b68ab-152">The size of the batch was chosen as 100 because our fictitious application allows the user to load 100 comments at a time.</span></span>  

<span data-ttu-id="b68ab-153">Inserir dados também não é recomendado em casos em que os dados inseridos são usados em diferentes documentos e são alterados com frequência.</span><span class="sxs-lookup"><span data-stu-id="b68ab-153">Another case where embedding data is not a good idea is when the embedded data is used often across documents and will change frequently.</span></span> 

<span data-ttu-id="b68ab-154">Veja este trecho de JSON.</span><span class="sxs-lookup"><span data-stu-id="b68ab-154">Take this JSON snippet.</span></span>

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

<span data-ttu-id="b68ab-155">Isto pode representar o portfólio de ações de alguém.</span><span class="sxs-lookup"><span data-stu-id="b68ab-155">This could represent a person's stock portfolio.</span></span> <span data-ttu-id="b68ab-156">Nós optamos por inserir as informações das ações em cada documento do portfólio.</span><span class="sxs-lookup"><span data-stu-id="b68ab-156">We have chosen to embed the stock information in to each portfolio document.</span></span> <span data-ttu-id="b68ab-157">Em um ambiente onde dados relacionados mudam com frequência, como um aplicativo de corretagem de ações, inserir dados que mudam frequentemente significa que você atualiza constantemente cada documento do portfólio, sempre que uma ação for negociada.</span><span class="sxs-lookup"><span data-stu-id="b68ab-157">In an environment where related data is changing frequently, like a stock trading application, embedding data that changes frequently is going to mean that you are constantly updating each portfolio document every time a stock is traded.</span></span>

<span data-ttu-id="b68ab-158">A ação *zaza* pode ser negociada centenas de vezes em apenas um dia, e milhares de usuários podem ter a ação *zaza* em seus portfólios.</span><span class="sxs-lookup"><span data-stu-id="b68ab-158">Stock *zaza* may be traded many hundreds of times in a single day and thousands of users could have *zaza* on their portfolio.</span></span> <span data-ttu-id="b68ab-159">Com um modelo de dados como o acima, teríamos que atualizar vários milhares de documentos de portfólio muitas vezes por dia, o que levaria a um sistema mal dimensionado.</span><span class="sxs-lookup"><span data-stu-id="b68ab-159">With a data model like the above we would have to update many thousands of portfolio documents many times every day leading to a system that won't scale very well.</span></span> 

## <span data-ttu-id="b68ab-160"><a id="Refer"></a>Fazendo referência a dados</span><span class="sxs-lookup"><span data-stu-id="b68ab-160"><a id="Refer"></a>Referencing data</span></span>
<span data-ttu-id="b68ab-161">Inserir dados funciona bem em muitos casos, mas claramente há situações em que desnormalizar seus dados trará mais problemas do que soluções.</span><span class="sxs-lookup"><span data-stu-id="b68ab-161">So, embedding data works nicely for many cases but it is clear that there are scenarios when denormalizing your data will cause more problems than it is worth.</span></span> <span data-ttu-id="b68ab-162">E o que podemos fazer?</span><span class="sxs-lookup"><span data-stu-id="b68ab-162">So what do we do now?</span></span> 

<span data-ttu-id="b68ab-163">Bancos de dados relacionais não são o único lugar onde você pode criar relações entre entidades.</span><span class="sxs-lookup"><span data-stu-id="b68ab-163">Relational databases are not the only place where you can create relationships between entities.</span></span> <span data-ttu-id="b68ab-164">Em um banco de dados de documentos, você pode ter informações em um documento que se relacionam a dados de outros documentos.</span><span class="sxs-lookup"><span data-stu-id="b68ab-164">In a document database you can have information in one document that actually relates to data in other documents.</span></span> <span data-ttu-id="b68ab-165">Eu não estou, de modo algum, defendendo a criação de sistemas que seriam mais adequados a um banco de dados relacional no Azure Cosmos DB ou a qualquer outro banco de dados de documentos. O que estou dizendo é que relações simples são ótimas e podem ser muito úteis.</span><span class="sxs-lookup"><span data-stu-id="b68ab-165">Now, I am not advocating for even one minute that we build systems that would be better suited to a relational database in Azure Cosmos DB, or any other document database, but simple relationships are fine and can be very useful.</span></span> 

<span data-ttu-id="b68ab-166">No JSON abaixo, optamos por usar o exemplo do portfólio de ações, mas, dessa vez, fazemos referência ao item de estoque no portfólio em vez de inseri-lo.</span><span class="sxs-lookup"><span data-stu-id="b68ab-166">In the JSON below we chose to use the example of a stock portfolio from earlier but this time we refer to the stock item on the portfolio instead of embedding it.</span></span> <span data-ttu-id="b68ab-167">Dessa forma, quando o item de estoque mudar frequentemente ao longo do dia, o único documento que precisará ser atualizado será o documento de estoque.</span><span class="sxs-lookup"><span data-stu-id="b68ab-167">This way, when the stock item changes frequently throughout the day the only document that needs to be updated is the single stock document.</span></span> 

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


<span data-ttu-id="b68ab-168">Uma desvantagem imediata dessa abordagem é se o aplicativo precisar mostrar informações sobre cada ação contida no portfólio de uma pessoa ao mostrar o portfólio. Nesse caso, você precisaria ir várias vezes ao banco de dados para carregar as informações de cada documento de ação.</span><span class="sxs-lookup"><span data-stu-id="b68ab-168">An immediate downside to this approach though is if your application is required to show information about each stock that is held when displaying a person's portfolio; in this case you would need to make multiple trips to the database to load the information for each stock document.</span></span> <span data-ttu-id="b68ab-169">Aqui, nós decidimos aumentar a eficiência das operações de gravação, que acontecem com frequência ao longo do dia. Por outro lado, comprometemos as operações de leitura, que têm menor potencial de afetar o desempenho deste sistema em particular.</span><span class="sxs-lookup"><span data-stu-id="b68ab-169">Here we've made a decision to improve the efficiency of write operations, which happen frequently throughout the day, but in turn compromised on the read operations that potentially have less impact on the performance of this particular system.</span></span>

> [!NOTE]
> <span data-ttu-id="b68ab-170">Modelos de dados normalizados **podem demandar mais viagens de ida e volta ao servidor** .</span><span class="sxs-lookup"><span data-stu-id="b68ab-170">Normalized data models **can require more round trips** to the server.</span></span>
> 
> 

### <a name="what-about-foreign-keys"></a><span data-ttu-id="b68ab-171">E as chaves estrangeiras?</span><span class="sxs-lookup"><span data-stu-id="b68ab-171">What about foreign keys?</span></span>
<span data-ttu-id="b68ab-172">Como no momento não há o conceito de restrição e chave estrangeira, entre outros, qualquer relação interna que houver nos documentos será um "elo fraco" e não será verificada pelo banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b68ab-172">Because there is currently no concept of a constraint, foreign-key or otherwise, any inter-document relationships that you have in documents are effectively "weak links" and will not be verified by the database itself.</span></span> <span data-ttu-id="b68ab-173">Se você desejar garantir que os dados aos quais um documento está se referindo realmente existem, você precisa fazer isso no aplicativo, por meio do uso de gatilhos do lado do servidor ou de procedimentos armazenados no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b68ab-173">If you want to ensure that the data a document is referring to actually exists, then you need to do this in your application, or through the use of server-side triggers or stored procedures on Azure Cosmos DB.</span></span>

### <a name="when-to-reference"></a><span data-ttu-id="b68ab-174">Quando fazer referência</span><span class="sxs-lookup"><span data-stu-id="b68ab-174">When to reference</span></span>
<span data-ttu-id="b68ab-175">De modo geral, use modelos de dados normalizados quando:</span><span class="sxs-lookup"><span data-stu-id="b68ab-175">In general, use normalized data models when:</span></span>

* <span data-ttu-id="b68ab-176">Representar relações de **um para muitos** .</span><span class="sxs-lookup"><span data-stu-id="b68ab-176">Representing **one-to-many** relationships.</span></span>
* <span data-ttu-id="b68ab-177">Representar relações de **muitos para muitos** .</span><span class="sxs-lookup"><span data-stu-id="b68ab-177">Representing **many-to-many** relationships.</span></span>
* <span data-ttu-id="b68ab-178">Dados relacionados **mudarem com frequência**.</span><span class="sxs-lookup"><span data-stu-id="b68ab-178">Related data **changes frequently**.</span></span>
* <span data-ttu-id="b68ab-179">Dados referenciados podem ser **ilimitados**.</span><span class="sxs-lookup"><span data-stu-id="b68ab-179">Referenced data could be **unbounded**.</span></span>

> [!NOTE]
> <span data-ttu-id="b68ab-180">De moro geral, normalizar traz melhor desempenho de **gravação** .</span><span class="sxs-lookup"><span data-stu-id="b68ab-180">Typically normalizing provides better **write** performance.</span></span>
> 
> 

### <a name="where-do-i-put-the-relationship"></a><span data-ttu-id="b68ab-181">Onde eu coloco a relação?</span><span class="sxs-lookup"><span data-stu-id="b68ab-181">Where do I put the relationship?</span></span>
<span data-ttu-id="b68ab-182">O crescimento da relação ajuda a determinar em qual documento armazenar a referência.</span><span class="sxs-lookup"><span data-stu-id="b68ab-182">The growth of the relationship will help determine in which document to store the reference.</span></span>

<span data-ttu-id="b68ab-183">Observemos o JSON abaixo que modela editoras e livros.</span><span class="sxs-lookup"><span data-stu-id="b68ab-183">If we look at the JSON below that models publishers and books.</span></span>

    Publisher document:
    {
        "id": "mspress",
        "name": "Microsoft Press",
        "books": [ 1, 2, 3, ..., 100, ..., 1000]
    }

    Book documents:
    {"id": "1", "name": "Azure Cosmos DB 101" }
    {"id": "2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "3", "name": "Taking over the world one JSON doc at a time" }
    ...
    {"id": "100", "name": "Learn about Azure Cosmos DB" }
    ...
    {"id": "1000", "name": "Deep Dive in to Azure Cosmos DB" }

<span data-ttu-id="b68ab-184">Se o número de livros por editora for pequeno, com crescimento limitado, armazenar a referência do livro no documento da editora pode ser útil.</span><span class="sxs-lookup"><span data-stu-id="b68ab-184">If the number of the books per publisher is small with limited growth, then storing the book reference inside the publisher document may be useful.</span></span> <span data-ttu-id="b68ab-185">No entanto, se o número de livros por editora for ilimitado, esse modelo de dados levaria a matrizes crescentes e mutáveis, como no exemplo de documento de editora abaixo.</span><span class="sxs-lookup"><span data-stu-id="b68ab-185">However, if the number of books per publisher is unbounded, then this data model would lead to mutable, growing arrays, as in the example publisher document above.</span></span> 

<span data-ttu-id="b68ab-186">Mudar um pouco as coisas resultaria em um modelo que ainda representa os mesmos dados, mas que agora evita essas grandes coleções mutáveis.</span><span class="sxs-lookup"><span data-stu-id="b68ab-186">Switching things around a bit would result in a model that still represents the same data but now avoids these large mutable collections.</span></span>

    Publisher document: 
    {
        "id": "mspress",
        "name": "Microsoft Press"
    }

    Book documents: 
    {"id": "1","name": "Azure Cosmos DB 101", "pub-id": "mspress"}
    {"id": "2","name": "Azure Cosmos DB for RDBMS Users", "pub-id": "mspress"}
    {"id": "3","name": "Taking over the world one JSON doc at a time"}
    ...
    {"id": "100","name": "Learn about Azure Cosmos DB", "pub-id": "mspress"}
    ...
    {"id": "1000","name": "Deep Dive in to Azure Cosmos DB", "pub-id": "mspress"}

<span data-ttu-id="b68ab-187">No exemplo acima, tiramos a coleção ilimitada do documento da editora.</span><span class="sxs-lookup"><span data-stu-id="b68ab-187">In the above example, we have dropped the unbounded collection on the publisher document.</span></span> <span data-ttu-id="b68ab-188">Em vez disso, temos apenas uma referência à editora no documento de cada livro.</span><span class="sxs-lookup"><span data-stu-id="b68ab-188">Instead we just have a a reference to the publisher on each book document.</span></span>

### <a name="how-do-i-model-manymany-relationships"></a><span data-ttu-id="b68ab-189">Como eu modelo relações de muitos para muitos?</span><span class="sxs-lookup"><span data-stu-id="b68ab-189">How do I model many:many relationships?</span></span>
<span data-ttu-id="b68ab-190">Em um banco de dados relacional, relações *muitos:muitos* frequentemente são modeladas com tabelas de junção, que simplesmente reúnem os registros de outras tabelas.</span><span class="sxs-lookup"><span data-stu-id="b68ab-190">In a relational database *many:many* relationships are often modeled with join tables, which just join records from other tables together.</span></span> 

![Associar tabelas](./media/documentdb-modeling-data/join-table.png)

<span data-ttu-id="b68ab-192">Você pode ficar tentado a fazer a mesma coisa usando documentos e produzir um modelo de dados semelhante ao seguinte.</span><span class="sxs-lookup"><span data-stu-id="b68ab-192">You might be tempted to replicate the same thing using documents and produce a data model that looks similar to the following.</span></span>

    Author documents: 
    {"id": "a1", "name": "Thomas Andersen" }
    {"id": "a2", "name": "William Wakefield" }

    Book documents:
    {"id": "b1", "name": "Azure Cosmos DB 101" }
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "b3", "name": "Taking over the world one JSON doc at a time" }
    {"id": "b4", "name": "Learn about Azure Cosmos DB" }
    {"id": "b5", "name": "Deep Dive in to Azure Cosmos DB" }

    Joining documents: 
    {"authorId": "a1", "bookId": "b1" }
    {"authorId": "a2", "bookId": "b1" }
    {"authorId": "a1", "bookId": "b2" }
    {"authorId": "a1", "bookId": "b3" }

<span data-ttu-id="b68ab-193">Isso funcionaria.</span><span class="sxs-lookup"><span data-stu-id="b68ab-193">This would work.</span></span> <span data-ttu-id="b68ab-194">No entanto, carregar um autor com seus livros ou carregar um livro com o autor iria sempre demandar pelo menos duas consultas adicionais no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b68ab-194">However, loading either an author with their books, or loading a book with its author, would always require at least two additional queries against the database.</span></span> <span data-ttu-id="b68ab-195">Uma consulta do documento de junção e outra consulta para obter o documento real que sofreu a junção.</span><span class="sxs-lookup"><span data-stu-id="b68ab-195">One query to the joining document and then another query to fetch the actual document being joined.</span></span> 

<span data-ttu-id="b68ab-196">Se tudo o que a tabela de junção está fazendo é unir dois dados, por que não simplesmente removê-la?</span><span class="sxs-lookup"><span data-stu-id="b68ab-196">If all this join table is doing is gluing together two pieces of data, then why not drop it completely?</span></span>
<span data-ttu-id="b68ab-197">Considere o seguinte.</span><span class="sxs-lookup"><span data-stu-id="b68ab-197">Consider the following.</span></span>

    Author documents:
    {"id": "a1", "name": "Thomas Andersen", "books": ["b1, "b2", "b3"]}
    {"id": "a2", "name": "William Wakefield", "books": ["b1", "b4"]}

    Book documents: 
    {"id": "b1", "name": "Azure Cosmos DB 101", "authors": ["a1", "a2"]}
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users", "authors": ["a1"]}
    {"id": "b3", "name": "Learn about Azure Cosmos DB", "authors": ["a1"]}
    {"id": "b4", "name": "Deep Dive in to Azure Cosmos DB", "authors": ["a2"]}

<span data-ttu-id="b68ab-198">Agora, se eu tivesse um autor, eu saberia imediatamente quais livros ele escreveu e, da mesma forma, se carregasse o documento de um livro, saberia quem é o autor.</span><span class="sxs-lookup"><span data-stu-id="b68ab-198">Now, if I had an author, I immediately know which books they have written, and conversely if I had a book document loaded I would know the ids of the author(s).</span></span> <span data-ttu-id="b68ab-199">Isso anula a consulta intermediária, da tabela de junção, reduzindo o número de viagens de ida e volta ao servidor que o aplicativo precisa fazer.</span><span class="sxs-lookup"><span data-stu-id="b68ab-199">This saves that intermediary query against the join table reducing the number of server round trips your application has to make.</span></span> 

## <span data-ttu-id="b68ab-200"><a id="WrapUp"></a>Modelos de dados híbridos</span><span class="sxs-lookup"><span data-stu-id="b68ab-200"><a id="WrapUp"></a>Hybrid data models</span></span>
<span data-ttu-id="b68ab-201">Nós vimos que inserir (ou desnormalizar) e referenciar (ou normalizar) dados têm suas vantagens e desvantagens.</span><span class="sxs-lookup"><span data-stu-id="b68ab-201">We've now looked embedding (or denormalizing) and referencing (or normalizing) data, each have their upsides and each have compromises as we have seen.</span></span> 

<span data-ttu-id="b68ab-202">Nem sempre é necessário escolher um dos dois. Não tenha medo de misturar um pouco as coisas.</span><span class="sxs-lookup"><span data-stu-id="b68ab-202">It doesn't always have to be either or, don't be scared to mix things up a little.</span></span> 

<span data-ttu-id="b68ab-203">Com base nas cargas de trabalho e nos padrões de uso específicos do aplicativo, pode haver casos em que misturar dados inseridos e referenciados faz sentido, levando a uma lógica mais simples do aplicativo, com menos viagens de ia e volta ao servidor e mantendo um bom nível de desempenho.</span><span class="sxs-lookup"><span data-stu-id="b68ab-203">Based on your application's specific usage patterns and workloads there may be cases where mixing embedded and referenced data makes sense and could lead to simpler application logic with fewer server round trips while still maintaining a good level of performance.</span></span>

<span data-ttu-id="b68ab-204">Considere o JSON a seguir.</span><span class="sxs-lookup"><span data-stu-id="b68ab-204">Consider the following JSON.</span></span> 

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

<span data-ttu-id="b68ab-205">Aqui, seguimos (principalmente) o modelo inserido, em que dados de outras entidades são inseridos no documento de nível superior, mas outros dados são referenciados.</span><span class="sxs-lookup"><span data-stu-id="b68ab-205">Here we've (mostly) followed the embedded model, where data from other entities are embedded in the top-level document, but other data is referenced.</span></span> 

<span data-ttu-id="b68ab-206">Olhando o documento do livro, vemos alguns campos interessantes na matriz de autores.</span><span class="sxs-lookup"><span data-stu-id="b68ab-206">If you look at the book document, we can see a few interesting fields when we look at the array of authors.</span></span> <span data-ttu-id="b68ab-207">Há um campo *id* que é o campo que usamos para fazer referência a um documento de autor, prática padrão em um modelo normalizado, mas também temos *nome* e *thumbnailUrl*.</span><span class="sxs-lookup"><span data-stu-id="b68ab-207">There is an *id* field which is the field we use to refer back to an author document, standard practice in a normalized model, but then we also have *name* and *thumbnailUrl*.</span></span> <span data-ttu-id="b68ab-208">Nós poderíamos ter ficado somente com a *id* e deixado o aplicativo obter informações adicionais do documento do autor usando o "vínculo", mas como nosso aplicativo mostra o nome do autor e uma foto em miniatura com cada livro mostrado, podemos eliminar uma viagem de ida e volta ao servidor por livro da lista desnormalizando **alguns** dados do autor.</span><span class="sxs-lookup"><span data-stu-id="b68ab-208">We could've just stuck with *id* and left the application to get any additional information it needed from the respective author document using the "link", but because our application displays the author's name and a thumbnail picture with every book displayed we can save a round trip to the server per book in a list by denormalizing **some** data from the author.</span></span>

<span data-ttu-id="b68ab-209">Claro, se o nome do autor mudasse ou se ele quisesse altera sua foto, teríamos que atualizar cada livro publicado. Mas para nosso aplicativo, com base no fato de que autores não mudam de nome com frequência, essa é uma decisão de design aceitável.</span><span class="sxs-lookup"><span data-stu-id="b68ab-209">Sure, if the author's name changed or they wanted to update their photo we'd have to go an update every book they ever published but for our application, based on the assumption that authors don't change their names very often, this is an acceptable design decision.</span></span>  

<span data-ttu-id="b68ab-210">No exemplo, há valores **agregados pré-calculados** para reduzir o processamento extensivo das operações de leitura.</span><span class="sxs-lookup"><span data-stu-id="b68ab-210">In the example there are **pre-calculated aggregates** values to save expensive processing on a read operation.</span></span> <span data-ttu-id="b68ab-211">No exemplo, alguns dos dados inseridos no documento do autor são calculados em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="b68ab-211">In the example, some of the data embedded in the author document is data that is calculated at run-time.</span></span> <span data-ttu-id="b68ab-212">Sempre que um novo livro é publicado, um documento de livro é criado **e** o campo countOfBooks, relativo à contagem de livros, é definido como um valor calculado com base no número de documentos de livros que existem para um dado autor.</span><span class="sxs-lookup"><span data-stu-id="b68ab-212">Every time a new book is published, a book document is created **and** the countOfBooks field is set to a calculated value based on the number of book documents that exist for a particular author.</span></span> <span data-ttu-id="b68ab-213">Essa otimização seria útil em sistemas com grandes volumes de leitura nos quais podemos computar as gravações para otimizar as leituras.</span><span class="sxs-lookup"><span data-stu-id="b68ab-213">This optimization would be good in read heavy systems where we can afford to do computations on writes in order to optimize reads.</span></span>

<span data-ttu-id="b68ab-214">A capacidade de ter um modelo com campos pré-calculados é possibilitada porque o Azure Cosmos DB dá suporte a **transações de vários documentos**.</span><span class="sxs-lookup"><span data-stu-id="b68ab-214">The ability to have a model with pre-calculated fields is made possible because Azure Cosmos DB supports **multi-document transactions**.</span></span> <span data-ttu-id="b68ab-215">Muitos repositórios NoSQL não podem fazer transações entre documentos e por isso defendem decisões de design, como "sempre inserir tudo", devido a essa limitação.</span><span class="sxs-lookup"><span data-stu-id="b68ab-215">Many NoSQL stores cannot do transactions across documents and therefore advocate design decisions, such as "always embed everything", due to this limitation.</span></span> <span data-ttu-id="b68ab-216">Com o Azure Cosmos DB, você pode usar gatilhos do lado do servidor ou procedimentos armazenados, que inserem manuais e atualizam autores, tudo isso em uma transação ACID.</span><span class="sxs-lookup"><span data-stu-id="b68ab-216">With Azure Cosmos DB, you can use server-side triggers, or stored procedures, that insert books and update authors all within an ACID transaction.</span></span> <span data-ttu-id="b68ab-217">Você não **precisa** inserir tudo em um documento para garantir que seus dados permaneçam consistentes.</span><span class="sxs-lookup"><span data-stu-id="b68ab-217">Now you don't **have** to embed everything in to one document just to be sure that your data remains consistent.</span></span>

## <span data-ttu-id="b68ab-218"><a name="NextSteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b68ab-218"><a name="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="b68ab-219">O principal aspecto deste artigo é entender que modelar dados em um ambiente sem esquemas é tão importante quanto sempre foi.</span><span class="sxs-lookup"><span data-stu-id="b68ab-219">The biggest takeaways from this article is to understand that data modeling in a schema-free world is just as important as ever.</span></span> 

<span data-ttu-id="b68ab-220">Assim como não há apenas uma forma de representar um dado em uma tela, não há apenas uma forma de modelar seus dados.</span><span class="sxs-lookup"><span data-stu-id="b68ab-220">Just as there is no single way to represent a piece of data on a screen, there is no single way to model your data.</span></span> <span data-ttu-id="b68ab-221">Você precisa entender eu aplicativo e como ele vai produzir, consumir e processar dados.</span><span class="sxs-lookup"><span data-stu-id="b68ab-221">You need to understand your application and how it will produce, consume, and process the data.</span></span> <span data-ttu-id="b68ab-222">E então, aplicando algumas das diretrizes apresentadas aqui, você pode começar a criar um modelo que trata das necessidades imediatas do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b68ab-222">Then, by applying some of the guidelines presented here you can set about creating a model that addresses the immediate needs of your application.</span></span> <span data-ttu-id="b68ab-223">Quando seus aplicativos precisarem mudar, você pode tirar proveito da flexibilidade de um banco de dados sem esquemas para adotar as mudanças e desenvolver seu modelo de dados facilmente.</span><span class="sxs-lookup"><span data-stu-id="b68ab-223">When your applications need to change, you can leverage the flexibility of a schema-free database to embrace that change and evolve your data model easily.</span></span> 

<span data-ttu-id="b68ab-224">Para saber mais sobre o Azure Cosmos DB, consulte a página de [documentação](https://azure.microsoft.com/documentation/services/cosmos-db/) do serviço.</span><span class="sxs-lookup"><span data-stu-id="b68ab-224">To learn more about Azure Cosmos DB, refer to the service's [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span> 

<span data-ttu-id="b68ab-225">Para entender como fragmentar seus dados em várias partições, consulte [Particionando dados no Azure Cosmos DB](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="b68ab-225">To understand how to shard your data across multiple partitions, refer to [Partitioning Data in Azure Cosmos DB](documentdb-partition-data.md).</span></span> 
