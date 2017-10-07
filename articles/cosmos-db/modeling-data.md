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
# <a name="modeling-document-data-for-nosql-databases"></a><span data-ttu-id="07426-104">Modelando dados de documentos para bancos de dados NoSQL</span><span class="sxs-lookup"><span data-stu-id="07426-104">Modeling document data for NoSQL databases</span></span>
<span data-ttu-id="07426-105">Enquanto os bancos de dados independentes de esquema, como banco de dados do Azure Cosmos, facilitam super tooembrace modelo de dados de alterações tooyour você ainda deve levar algum tempo pensar sobre seus dados.</span><span class="sxs-lookup"><span data-stu-id="07426-105">While schema-free databases, like Azure Cosmos DB, make it super easy tooembrace changes tooyour data model you should still spend some time thinking about your data.</span></span> 

<span data-ttu-id="07426-106">Como a data será toobe armazenado?</span><span class="sxs-lookup"><span data-stu-id="07426-106">How is data going toobe stored?</span></span> <span data-ttu-id="07426-107">É como os dados do aplicativo vai tooretrieve e consulta?</span><span class="sxs-lookup"><span data-stu-id="07426-107">How is your application going tooretrieve and query data?</span></span> <span data-ttu-id="07426-108">O aplicativo realizará grandes volumes de leitura e gravação?</span><span class="sxs-lookup"><span data-stu-id="07426-108">Is your application read heavy, or write heavy?</span></span> 

<span data-ttu-id="07426-109">Depois de ler este artigo, você será capaz de tooanswer Olá perguntas a seguir:</span><span class="sxs-lookup"><span data-stu-id="07426-109">After reading this article, you will be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="07426-110">Como devo pensar em um documento num banco de dados de documentos?</span><span class="sxs-lookup"><span data-stu-id="07426-110">How should I think about a document in a document database?</span></span>
* <span data-ttu-id="07426-111">O que é modelagem de dados e como ele me afeta?</span><span class="sxs-lookup"><span data-stu-id="07426-111">What is data modeling and why should I care?</span></span> 
* <span data-ttu-id="07426-112">Como é a modelagem de dados em um documento banco de dados diferentes tooa banco de dados relacional?</span><span class="sxs-lookup"><span data-stu-id="07426-112">How is modeling data in a document database different tooa relational database?</span></span>
* <span data-ttu-id="07426-113">Como posso expressar relações de dados em um banco de dados não relacional?</span><span class="sxs-lookup"><span data-stu-id="07426-113">How do I express data relationships in a non-relational database?</span></span>
* <span data-ttu-id="07426-114">Ao incorporar a dados e ao vincular a toodata?</span><span class="sxs-lookup"><span data-stu-id="07426-114">When do I embed data and when do I link toodata?</span></span>

## <a name="embedding-data"></a><span data-ttu-id="07426-115">Inserindo dados</span><span class="sxs-lookup"><span data-stu-id="07426-115">Embedding data</span></span>
<span data-ttu-id="07426-116">Quando você iniciar a modelagem de dados em um armazenamento de documentos, como o banco de dados do Azure Cosmos, tente tootreat suas entidades como **documentos autossuficientes** representado em JSON.</span><span class="sxs-lookup"><span data-stu-id="07426-116">When you start modeling data in a document store, such as Azure Cosmos DB, try tootreat your entities as **self-contained documents** represented in JSON.</span></span>

<span data-ttu-id="07426-117">Antes de nos aprofundarmos demais, vamos voltar um pouco e ver como modelaríamos algo num banco de dados relacional, que é um processo que muitos de nós já conhecemos.</span><span class="sxs-lookup"><span data-stu-id="07426-117">Before we dive in too much further, let us take a few steps back and have a look at how we might model something in a relational database, a subject many of us are already familiar with.</span></span> <span data-ttu-id="07426-118">Olá exemplo a seguir mostra como uma pessoa pode ser armazenada em um banco de dados relacional.</span><span class="sxs-lookup"><span data-stu-id="07426-118">hello following example shows how a person might be stored in a relational database.</span></span> 

![Modelo de banco de dados relacional](./media/documentdb-modeling-data/relational-data-model.png)

<span data-ttu-id="07426-120">Ao trabalhar com bancos de dados relacionais, já foi apresentados para toonormalize anos, normalizar, normalizar.</span><span class="sxs-lookup"><span data-stu-id="07426-120">When working with relational databases, we've been taught for years toonormalize, normalize, normalize.</span></span>

<span data-ttu-id="07426-121">Normalizar os dados geralmente envolve a criação de uma entidade, como uma pessoa e dividi-la em toodiscrete partes de dados.</span><span class="sxs-lookup"><span data-stu-id="07426-121">Normalizing your data typically involves taking an entity, such as a person, and breaking it down in toodiscrete pieces of data.</span></span> <span data-ttu-id="07426-122">O exemplo hello acima, uma pessoa pode ter vários registros de detalhe de contato, bem como vários registros de endereço.</span><span class="sxs-lookup"><span data-stu-id="07426-122">In hello example above, a person can have multiple contact detail records as well as multiple address records.</span></span> <span data-ttu-id="07426-123">Nós ainda vamos além e dividimos os detalhes de contato extraindo campos comuns, como tipo.</span><span class="sxs-lookup"><span data-stu-id="07426-123">We even go one step further and break down contact details by further extracting common fields like a type.</span></span> <span data-ttu-id="07426-124">O mesmo vale para o endereço, cada registro tem um tipo, como *Residencial* ou *Comercial*</span><span class="sxs-lookup"><span data-stu-id="07426-124">Same for address, each record here has a type like *Home* or *Business*</span></span> 

<span data-ttu-id="07426-125">Olá guiando local quando a normalização dos dados é muito**evitar armazenar dados redundantes** em cada registro e em vez disso, consulte toodata.</span><span class="sxs-lookup"><span data-stu-id="07426-125">hello guiding premise when normalizing data is too**avoid storing redundant data** on each record and rather refer toodata.</span></span> <span data-ttu-id="07426-126">Neste exemplo, tooread uma pessoa, com todos os seus detalhes de contato e endereços, é necessário toouse junções tooeffectively-agregado seus dados em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="07426-126">In this example, tooread a person, with all their contact details and addresses, you need toouse JOINS tooeffectively aggregate your data at run time.</span></span>

    SELECT p.FirstName, p.LastName, a.City, cd.Detail
    FROM Person p
    JOIN ContactDetail cd ON cd.PersonId = p.Id
    JOIN ContactDetailType on cdt ON cdt.Id = cd.TypeId
    JOIN Address a ON a.PersonId = p.Id

<span data-ttu-id="07426-127">Atualizar uma pessoa, com seus detalhes de contato e endereço, demanda várias operações de gravação em várias tabelas individuais.</span><span class="sxs-lookup"><span data-stu-id="07426-127">Updating a single person with their contact details and addresses requires write operations across many individual tables.</span></span> 

<span data-ttu-id="07426-128">Agora vamos dar uma olhada em como podemos seria modelo Olá mesmo dados como uma entidade independente em um banco de dados do documento.</span><span class="sxs-lookup"><span data-stu-id="07426-128">Now let's take a look at how we would model hello same data as a self-contained entity in a document database.</span></span>

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

<span data-ttu-id="07426-129">Usando a abordagem de saudação acima, temos agora **desnormalizados** Olá registro pessoa onde podemos **inserido** todos Olá informações relacionadas toothis pessoa, como seus detalhes de contato e endereços em tooa único Documento JSON.</span><span class="sxs-lookup"><span data-stu-id="07426-129">Using hello approach above we have now **denormalized** hello person record where we **embedded** all hello information relating toothis person, such as their contact details and addresses, in tooa single JSON document.</span></span>
<span data-ttu-id="07426-130">Além disso, porque não podemos está restrita tooa esquema fixo que temos Olá flexibilidade toodo itens, como com detalhes de contato de diferentes formas completamente.</span><span class="sxs-lookup"><span data-stu-id="07426-130">In addition, because we're not confined tooa fixed schema we have hello flexibility toodo things like having contact details of different shapes entirely.</span></span> 

<span data-ttu-id="07426-131">Recuperar um registro de pessoa completa do banco de dados de saudação agora é uma única operação em uma única coleção e de um único documento de leitura.</span><span class="sxs-lookup"><span data-stu-id="07426-131">Retrieving a complete person record from hello database is now a single read operation against a single collection and for a single document.</span></span> <span data-ttu-id="07426-132">A atualização do registro de uma pessoa, com seus detalhes de contato e endereços, também é feita em uma única operação de gravação, de um único documento.</span><span class="sxs-lookup"><span data-stu-id="07426-132">Updating a person record, with their contact details and addresses, is also a single write operation against a single document.</span></span>

<span data-ttu-id="07426-133">Por desnormalização de dados, seu aplicativo pode ser necessário tooissue menos consultas e atualizações toocomplete operações comuns.</span><span class="sxs-lookup"><span data-stu-id="07426-133">By denormalizing data, your application may need tooissue fewer queries and updates toocomplete common operations.</span></span> 

### <a name="when-tooembed"></a><span data-ttu-id="07426-134">Quando tooembed</span><span class="sxs-lookup"><span data-stu-id="07426-134">When tooembed</span></span>
<span data-ttu-id="07426-135">De modo geral, use modelos de dados inseridos quando:</span><span class="sxs-lookup"><span data-stu-id="07426-135">In general, use embedded data models when:</span></span>

* <span data-ttu-id="07426-136">Houver relações de **contém** entre entidades.</span><span class="sxs-lookup"><span data-stu-id="07426-136">There are **contains** relationships between entities.</span></span>
* <span data-ttu-id="07426-137">Houver relações **de um para poucos** entre entidades.</span><span class="sxs-lookup"><span data-stu-id="07426-137">There are **one-to-few** relationships between entities.</span></span>
* <span data-ttu-id="07426-138">Houver dados inseridos que são **alterados com pouca frequência**.</span><span class="sxs-lookup"><span data-stu-id="07426-138">There is embedded data that **changes infrequently**.</span></span>
* <span data-ttu-id="07426-139">Houver dados inseridos que não crescerão **sem limite**.</span><span class="sxs-lookup"><span data-stu-id="07426-139">There is embedded data won't grow **without bound**.</span></span>
* <span data-ttu-id="07426-140">Dados inseridos é **integral** toodata em um documento.</span><span class="sxs-lookup"><span data-stu-id="07426-140">There is embedded data that is **integral** toodata in a document.</span></span>

> [!NOTE]
> <span data-ttu-id="07426-141">De modo geral, modelos de dados desnormalizados oferecem melhor desempenho de **leitura** .</span><span class="sxs-lookup"><span data-stu-id="07426-141">Typically denormalized data models provide better **read** performance.</span></span>
> 
> 

### <a name="when-not-tooembed"></a><span data-ttu-id="07426-142">Quando não tooembed</span><span class="sxs-lookup"><span data-stu-id="07426-142">When not tooembed</span></span>
<span data-ttu-id="07426-143">Enquanto Olá regra geral em um banco de dados de documento é toodenormalize tudo e inserir todos os dados no documento único tooa, isso pode levar a situações toosome que devem ser evitadas.</span><span class="sxs-lookup"><span data-stu-id="07426-143">While hello rule of thumb in a document database is toodenormalize everything and embed all data in tooa single document, this can lead toosome situations that should be avoided.</span></span>

<span data-ttu-id="07426-144">Veja este trecho de JSON.</span><span class="sxs-lookup"><span data-stu-id="07426-144">Take this JSON snippet.</span></span>

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

<span data-ttu-id="07426-145">Uma entidade de postagem com comentários inseridos seria assim se estivéssemos modelando um sistema de blog comum, ou CMS.</span><span class="sxs-lookup"><span data-stu-id="07426-145">This might be what a post entity with embedded comments would look like if we were modeling a typical blog, or CMS, system.</span></span> <span data-ttu-id="07426-146">problema com este exemplo Hello é que hello a matriz de comentários é **unbounded**, que significa que há um número de toohello de limite (prático) de qualquer publicação único pode ter de comentários.</span><span class="sxs-lookup"><span data-stu-id="07426-146">hello problem with this example is that hello comments array is **unbounded**, meaning that there is no (practical) limit toohello number of comments any single post can have.</span></span> <span data-ttu-id="07426-147">Isso se tornará um problema como tamanho de saudação do documento hello pode crescer significativamente.</span><span class="sxs-lookup"><span data-stu-id="07426-147">This will become a problem as hello size of hello document could grow significantly.</span></span>

<span data-ttu-id="07426-148">Como tamanho de saudação do hello documento expande os dados de saudação do hello capacidade tootransmit pela transmissão hello, bem como a leitura e atualização documento hello, em grande escala, será afetado.</span><span class="sxs-lookup"><span data-stu-id="07426-148">As hello size of hello document grows hello ability tootransmit hello data over hello wire as well as reading and updating hello document, at scale, will be impacted.</span></span>

<span data-ttu-id="07426-149">Nesse caso seria melhor Olá tooconsider modelo a seguir.</span><span class="sxs-lookup"><span data-stu-id="07426-149">In this case it would be better tooconsider hello following model.</span></span>

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

<span data-ttu-id="07426-150">Este modelo tem comentários mais recentes de Olá três incorporados em Olá postagem em si, que é uma matriz com um limite fixo isso tempo.</span><span class="sxs-lookup"><span data-stu-id="07426-150">This model has hello three most recent comments embedded on hello post itself, which is an array with a fixed bound this time.</span></span> <span data-ttu-id="07426-151">Olá outros comentários são agrupados em toobatches de 100 comentários e armazenados em documentos separados.</span><span class="sxs-lookup"><span data-stu-id="07426-151">hello other comments are grouped in toobatches of 100 comments and stored in separate documents.</span></span> <span data-ttu-id="07426-152">tamanho de saudação do lote Olá foi escolhido como 100 como nosso aplicativo fictício permite Olá 100 comentários do usuário tooload por vez.</span><span class="sxs-lookup"><span data-stu-id="07426-152">hello size of hello batch was chosen as 100 because our fictitious application allows hello user tooload 100 comments at a time.</span></span>  

<span data-ttu-id="07426-153">Outro caso em que a inserção de dados não são uma boa ideia é quando Olá inseridos dados são usados frequentemente em documentos e serão alterados com frequência.</span><span class="sxs-lookup"><span data-stu-id="07426-153">Another case where embedding data is not a good idea is when hello embedded data is used often across documents and will change frequently.</span></span> 

<span data-ttu-id="07426-154">Veja este trecho de JSON.</span><span class="sxs-lookup"><span data-stu-id="07426-154">Take this JSON snippet.</span></span>

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

<span data-ttu-id="07426-155">Isto pode representar o portfólio de ações de alguém.</span><span class="sxs-lookup"><span data-stu-id="07426-155">This could represent a person's stock portfolio.</span></span> <span data-ttu-id="07426-156">Escolhemos informações sobre ações de saudação tooembed no documento de portfólio de tooeach.</span><span class="sxs-lookup"><span data-stu-id="07426-156">We have chosen tooembed hello stock information in tooeach portfolio document.</span></span> <span data-ttu-id="07426-157">Em um ambiente em que os dados relacionados mudar com frequência, como uma aplicativo, de comercialização de ações a inserção de dados que mudam frequentemente será toomean que você está atualizando constantemente cada documento portfólio toda vez que uma ação foi negociada.</span><span class="sxs-lookup"><span data-stu-id="07426-157">In an environment where related data is changing frequently, like a stock trading application, embedding data that changes frequently is going toomean that you are constantly updating each portfolio document every time a stock is traded.</span></span>

<span data-ttu-id="07426-158">A ação *zaza* pode ser negociada centenas de vezes em apenas um dia, e milhares de usuários podem ter a ação *zaza* em seus portfólios.</span><span class="sxs-lookup"><span data-stu-id="07426-158">Stock *zaza* may be traded many hundreds of times in a single day and thousands of users could have *zaza* on their portfolio.</span></span> <span data-ttu-id="07426-159">Com um modelo de dados como Olá acima seria temos tooupdate milhares de documentos de portfólio muitas vezes diariamente principal sistema tooa dimensionamento muito bem.</span><span class="sxs-lookup"><span data-stu-id="07426-159">With a data model like hello above we would have tooupdate many thousands of portfolio documents many times every day leading tooa system that won't scale very well.</span></span> 

## <span data-ttu-id="07426-160"><a id="Refer"></a>Fazendo referência a dados</span><span class="sxs-lookup"><span data-stu-id="07426-160"><a id="Refer"></a>Referencing data</span></span>
<span data-ttu-id="07426-161">Inserir dados funciona bem em muitos casos, mas claramente há situações em que desnormalizar seus dados trará mais problemas do que soluções.</span><span class="sxs-lookup"><span data-stu-id="07426-161">So, embedding data works nicely for many cases but it is clear that there are scenarios when denormalizing your data will cause more problems than it is worth.</span></span> <span data-ttu-id="07426-162">E o que podemos fazer?</span><span class="sxs-lookup"><span data-stu-id="07426-162">So what do we do now?</span></span> 

<span data-ttu-id="07426-163">Bancos de dados relacionais não estão local somente hello, onde você pode criar relações entre entidades.</span><span class="sxs-lookup"><span data-stu-id="07426-163">Relational databases are not hello only place where you can create relationships between entities.</span></span> <span data-ttu-id="07426-164">Em um banco de dados de documento, você pode ter informações em um documento que relaciona realmente toodata em outros documentos.</span><span class="sxs-lookup"><span data-stu-id="07426-164">In a document database you can have information in one document that actually relates toodata in other documents.</span></span> <span data-ttu-id="07426-165">Agora, eu não estou defendendo por até um minuto que criamos sistemas que seriam melhor adequado tooa banco de dados relacional no banco de dados do Azure Cosmos ou qualquer outro banco de dados de documento, mas relações simples são permitidas e podem ser muito útil.</span><span class="sxs-lookup"><span data-stu-id="07426-165">Now, I am not advocating for even one minute that we build systems that would be better suited tooa relational database in Azure Cosmos DB, or any other document database, but simple relationships are fine and can be very useful.</span></span> 

<span data-ttu-id="07426-166">Olá JSON abaixo escolhemos toouse exemplo hello um portfólio de ações de anteriormente mas, desta vez, que fazemos referência de item de estoque toohello no portfólio de saudação em vez de incorporá-las.</span><span class="sxs-lookup"><span data-stu-id="07426-166">In hello JSON below we chose toouse hello example of a stock portfolio from earlier but this time we refer toohello stock item on hello portfolio instead of embedding it.</span></span> <span data-ttu-id="07426-167">Dessa forma, quando o item de estoque Olá alterados com frequência Olá dia Olá somente documento que precisa toobe atualizado é único documento de estoque de saudação.</span><span class="sxs-lookup"><span data-stu-id="07426-167">This way, when hello stock item changes frequently throughout hello day hello only document that needs toobe updated is hello single stock document.</span></span> 

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


<span data-ttu-id="07426-168">Porém, uma abordagem de toothis desvantagem imediata é se o aplicativo é necessário tooshow informações sobre cada ação que é mantida ao exibir o portfólio de uma pessoa; Nesse caso seria necessário toomake várias viagens toohello banco de dados tooload Olá informações para cada documento de estoque.</span><span class="sxs-lookup"><span data-stu-id="07426-168">An immediate downside toothis approach though is if your application is required tooshow information about each stock that is held when displaying a person's portfolio; in this case you would need toomake multiple trips toohello database tooload hello information for each stock document.</span></span> <span data-ttu-id="07426-169">Aqui, fizemos uma decisão tooimprove Olá a eficiência das operações de gravação, o que acontecer com frequência ao longo do dia hello, mas por sua vez comprometido em Olá operações de leitura que potencialmente tem menos impacto no desempenho de saudação do sistema específico.</span><span class="sxs-lookup"><span data-stu-id="07426-169">Here we've made a decision tooimprove hello efficiency of write operations, which happen frequently throughout hello day, but in turn compromised on hello read operations that potentially have less impact on hello performance of this particular system.</span></span>

> [!NOTE]
> <span data-ttu-id="07426-170">Normalizado modelos de dados **pode exigir mais viagens de ida e** toohello server.</span><span class="sxs-lookup"><span data-stu-id="07426-170">Normalized data models **can require more round trips** toohello server.</span></span>
> 
> 

### <a name="what-about-foreign-keys"></a><span data-ttu-id="07426-171">E as chaves estrangeiras?</span><span class="sxs-lookup"><span data-stu-id="07426-171">What about foreign keys?</span></span>
<span data-ttu-id="07426-172">Porque não há nenhum conceito de uma restrição, chave estrangeira ou caso contrário, todas as relações entre documentos que você tem em documentos são efetivamente "fracos" e não serão verificadas pela Olá próprio banco de dados.</span><span class="sxs-lookup"><span data-stu-id="07426-172">Because there is currently no concept of a constraint, foreign-key or otherwise, any inter-document relationships that you have in documents are effectively "weak links" and will not be verified by hello database itself.</span></span> <span data-ttu-id="07426-173">Se você quiser tooensure que Olá dados que se refere a um documento tooactually existir, você precisará toodo isso em seu aplicativo, ou por meio do uso de saudação do lado do servidor gatilhos ou procedimentos armazenados no banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="07426-173">If you want tooensure that hello data a document is referring tooactually exists, then you need toodo this in your application, or through hello use of server-side triggers or stored procedures on Azure Cosmos DB.</span></span>

### <a name="when-tooreference"></a><span data-ttu-id="07426-174">Quando tooreference</span><span class="sxs-lookup"><span data-stu-id="07426-174">When tooreference</span></span>
<span data-ttu-id="07426-175">De modo geral, use modelos de dados normalizados quando:</span><span class="sxs-lookup"><span data-stu-id="07426-175">In general, use normalized data models when:</span></span>

* <span data-ttu-id="07426-176">Representar relações de **um para muitos** .</span><span class="sxs-lookup"><span data-stu-id="07426-176">Representing **one-to-many** relationships.</span></span>
* <span data-ttu-id="07426-177">Representar relações de **muitos para muitos** .</span><span class="sxs-lookup"><span data-stu-id="07426-177">Representing **many-to-many** relationships.</span></span>
* <span data-ttu-id="07426-178">Dados relacionados **mudarem com frequência**.</span><span class="sxs-lookup"><span data-stu-id="07426-178">Related data **changes frequently**.</span></span>
* <span data-ttu-id="07426-179">Dados referenciados podem ser **ilimitados**.</span><span class="sxs-lookup"><span data-stu-id="07426-179">Referenced data could be **unbounded**.</span></span>

> [!NOTE]
> <span data-ttu-id="07426-180">De moro geral, normalizar traz melhor desempenho de **gravação** .</span><span class="sxs-lookup"><span data-stu-id="07426-180">Typically normalizing provides better **write** performance.</span></span>
> 
> 

### <a name="where-do-i-put-hello-relationship"></a><span data-ttu-id="07426-181">Onde posso colocar relação Olá?</span><span class="sxs-lookup"><span data-stu-id="07426-181">Where do I put hello relationship?</span></span>
<span data-ttu-id="07426-182">crescimento de saudação do relacionamento Olá ajudam a determinar na qual referência toostore hello.</span><span class="sxs-lookup"><span data-stu-id="07426-182">hello growth of hello relationship will help determine in which document toostore hello reference.</span></span>

<span data-ttu-id="07426-183">Se observarmos Olá JSON abaixo que modela editores e manuais.</span><span class="sxs-lookup"><span data-stu-id="07426-183">If we look at hello JSON below that models publishers and books.</span></span>

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

<span data-ttu-id="07426-184">Se o número de saudação de manuais Olá por publicador é pequeno com crescimento limitado, armazenando referência de catálogo Olá Olá publicador documento pode ser útil.</span><span class="sxs-lookup"><span data-stu-id="07426-184">If hello number of hello books per publisher is small with limited growth, then storing hello book reference inside hello publisher document may be useful.</span></span> <span data-ttu-id="07426-185">No entanto, se o número de saudação de livros por publicador é não vinculado, esse modelo de dados levaria toomutable, aumentando a matrizes, como no documento do publisher exemplo hello acima.</span><span class="sxs-lookup"><span data-stu-id="07426-185">However, if hello number of books per publisher is unbounded, then this data model would lead toomutable, growing arrays, as in hello example publisher document above.</span></span> 

<span data-ttu-id="07426-186">Alternar as coisas em torno de um bit seria resultará em um modelo que representa ainda Olá os mesmos dados mas agora evita essas coleções mutáveis grandes.</span><span class="sxs-lookup"><span data-stu-id="07426-186">Switching things around a bit would result in a model that still represents hello same data but now avoids these large mutable collections.</span></span>

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

<span data-ttu-id="07426-187">Em Olá exemplo acima, podemos ter removido Olá coleção não vinculada no documento do publisher hello.</span><span class="sxs-lookup"><span data-stu-id="07426-187">In hello above example, we have dropped hello unbounded collection on hello publisher document.</span></span> <span data-ttu-id="07426-188">Em vez disso, basta que um publicador de toohello uma referência em cada documento de catálogo.</span><span class="sxs-lookup"><span data-stu-id="07426-188">Instead we just have a a reference toohello publisher on each book document.</span></span>

### <a name="how-do-i-model-manymany-relationships"></a><span data-ttu-id="07426-189">Como eu modelo relações de muitos para muitos?</span><span class="sxs-lookup"><span data-stu-id="07426-189">How do I model many:many relationships?</span></span>
<span data-ttu-id="07426-190">Em um banco de dados relacional, relações *muitos:muitos* frequentemente são modeladas com tabelas de junção, que simplesmente reúnem os registros de outras tabelas.</span><span class="sxs-lookup"><span data-stu-id="07426-190">In a relational database *many:many* relationships are often modeled with join tables, which just join records from other tables together.</span></span> 

![Associar tabelas](./media/documentdb-modeling-data/join-table.png)

<span data-ttu-id="07426-192">Você pode ser tentado tooreplicate Olá mesma coisa usando documentos e produzir um modelo de dados que pesquisa a seguir toohello semelhante.</span><span class="sxs-lookup"><span data-stu-id="07426-192">You might be tempted tooreplicate hello same thing using documents and produce a data model that looks similar toohello following.</span></span>

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

<span data-ttu-id="07426-193">Isso funcionaria.</span><span class="sxs-lookup"><span data-stu-id="07426-193">This would work.</span></span> <span data-ttu-id="07426-194">No entanto, carregar ou um autor com seus livros ou carregar um livro com seu autor, sempre exigem pelo menos duas consultas adicionais no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="07426-194">However, loading either an author with their books, or loading a book with its author, would always require at least two additional queries against hello database.</span></span> <span data-ttu-id="07426-195">Toohello de uma consulta unir o documento e, em seguida, outra consulta toofetch Olá real documento sendo unidas.</span><span class="sxs-lookup"><span data-stu-id="07426-195">One query toohello joining document and then another query toofetch hello actual document being joined.</span></span> 

<span data-ttu-id="07426-196">Se tudo o que a tabela de junção está fazendo é unir dois dados, por que não simplesmente removê-la?</span><span class="sxs-lookup"><span data-stu-id="07426-196">If all this join table is doing is gluing together two pieces of data, then why not drop it completely?</span></span>
<span data-ttu-id="07426-197">Considere o seguinte hello.</span><span class="sxs-lookup"><span data-stu-id="07426-197">Consider hello following.</span></span>

    Author documents:
    {"id": "a1", "name": "Thomas Andersen", "books": ["b1, "b2", "b3"]}
    {"id": "a2", "name": "William Wakefield", "books": ["b1", "b4"]}

    Book documents: 
    {"id": "b1", "name": "Azure Cosmos DB 101", "authors": ["a1", "a2"]}
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users", "authors": ["a1"]}
    {"id": "b3", "name": "Learn about Azure Cosmos DB", "authors": ["a1"]}
    {"id": "b4", "name": "Deep Dive in tooAzure Cosmos DB", "authors": ["a2"]}

<span data-ttu-id="07426-198">Agora, se eu tivesse um autor, saber imediatamente quais livros que foram gravadas, e por outro lado se eu tivesse um documento de livro carregado seria sei ids de saudação dos autores de saudação.</span><span class="sxs-lookup"><span data-stu-id="07426-198">Now, if I had an author, I immediately know which books they have written, and conversely if I had a book document loaded I would know hello ids of hello author(s).</span></span> <span data-ttu-id="07426-199">Isso economiza intermediária consulta em relação à tabela de junção Olá reduzindo o número de saudação do servidor de viagens de ida e seu aplicativo tiver toomake.</span><span class="sxs-lookup"><span data-stu-id="07426-199">This saves that intermediary query against hello join table reducing hello number of server round trips your application has toomake.</span></span> 

## <span data-ttu-id="07426-200"><a id="WrapUp"></a>Modelos de dados híbridos</span><span class="sxs-lookup"><span data-stu-id="07426-200"><a id="WrapUp"></a>Hybrid data models</span></span>
<span data-ttu-id="07426-201">Nós vimos que inserir (ou desnormalizar) e referenciar (ou normalizar) dados têm suas vantagens e desvantagens.</span><span class="sxs-lookup"><span data-stu-id="07426-201">We've now looked embedding (or denormalizing) and referencing (or normalizing) data, each have their upsides and each have compromises as we have seen.</span></span> 

<span data-ttu-id="07426-202">Ele não sempre têm toobe ou, não tenham toomix assustados coisas um pouco.</span><span class="sxs-lookup"><span data-stu-id="07426-202">It doesn't always have toobe either or, don't be scared toomix things up a little.</span></span> 

<span data-ttu-id="07426-203">Com base em padrões de uso específicos e pode haver casos onde incorporado a combinação de cargas de trabalho do seu aplicativo e dados referenciados faz sentido e pôde lead toosimpler a lógica do aplicativo com o servidor menos processamentos e ainda manter um bom nível de desempenho .</span><span class="sxs-lookup"><span data-stu-id="07426-203">Based on your application's specific usage patterns and workloads there may be cases where mixing embedded and referenced data makes sense and could lead toosimpler application logic with fewer server round trips while still maintaining a good level of performance.</span></span>

<span data-ttu-id="07426-204">Considere Olá JSON a seguir.</span><span class="sxs-lookup"><span data-stu-id="07426-204">Consider hello following JSON.</span></span> 

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

<span data-ttu-id="07426-205">Aqui nós (principalmente) seguiu modelo incorporado hello, onde os dados de outras entidades são inseridos no documento de nível superior Olá, mas outros dados são referenciados.</span><span class="sxs-lookup"><span data-stu-id="07426-205">Here we've (mostly) followed hello embedded model, where data from other entities are embedded in hello top-level document, but other data is referenced.</span></span> 

<span data-ttu-id="07426-206">Se você examinar o documento de livro Olá, podemos ver algumas interessantes campos quando vamos examinar a matriz de saudação de autores.</span><span class="sxs-lookup"><span data-stu-id="07426-206">If you look at hello book document, we can see a few interesting fields when we look at hello array of authors.</span></span> <span data-ttu-id="07426-207">Há um *id* campo que é o campo de saudação usar documentos de autor back tooan toorefer, prática padrão em um modelo normalizado, mas, em seguida, podemos também ter *nome* e *thumbnailUrl*.</span><span class="sxs-lookup"><span data-stu-id="07426-207">There is an *id* field which is hello field we use toorefer back tooan author document, standard practice in a normalized model, but then we also have *name* and *thumbnailUrl*.</span></span> <span data-ttu-id="07426-208">Pode apenas adotamos *id* e deixado Olá aplicativo tooget qualquer informação adicional, ela necessária do documento do respectivos autor hello usando hello "link", mas como nosso aplicativo exibe o nome do autor hello e um imagem em miniatura com cada livro exibido poderemos salvar um servidor de toohello de ida e volta por catálogo em uma lista por desnormalização **alguns** dados de autor hello.</span><span class="sxs-lookup"><span data-stu-id="07426-208">We could've just stuck with *id* and left hello application tooget any additional information it needed from hello respective author document using hello "link", but because our application displays hello author's name and a thumbnail picture with every book displayed we can save a round trip toohello server per book in a list by denormalizing **some** data from hello author.</span></span>

<span data-ttu-id="07426-209">Obviamente, se o nome do autor Olá alterado ou quisessem tooupdate suas fotos haveria toogo uma atualização de todos os livros que nunca de publicados, mas para nosso aplicativo, com base na suposição de saudação que os autores não alterem seus nomes com frequência, esse é um design aceitável decisão.</span><span class="sxs-lookup"><span data-stu-id="07426-209">Sure, if hello author's name changed or they wanted tooupdate their photo we'd have toogo an update every book they ever published but for our application, based on hello assumption that authors don't change their names very often, this is an acceptable design decision.</span></span>  

<span data-ttu-id="07426-210">No exemplo hello há **pré-calculada agregações** toosave caro de processamento em uma operação de leitura de valores.</span><span class="sxs-lookup"><span data-stu-id="07426-210">In hello example there are **pre-calculated aggregates** values toosave expensive processing on a read operation.</span></span> <span data-ttu-id="07426-211">Exemplo hello, alguns dos dados Olá inseridos no documento de autor Olá são dados que são calculados em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="07426-211">In hello example, some of hello data embedded in hello author document is data that is calculated at run-time.</span></span> <span data-ttu-id="07426-212">Sempre que um novo catálogo é publicado, um documento de catálogo é criado **e** campo de countOfBooks Olá estiver definido como valor tooa calculado com base no número de saudação de documentos de catálogo que existem para um determinado autor.</span><span class="sxs-lookup"><span data-stu-id="07426-212">Every time a new book is published, a book document is created **and** hello countOfBooks field is set tooa calculated value based on hello number of book documents that exist for a particular author.</span></span> <span data-ttu-id="07426-213">Essa otimização seria bom em sistemas de intenso leitura em que podemos pode toodo computações em gravações em ordem toooptimize leituras.</span><span class="sxs-lookup"><span data-stu-id="07426-213">This optimization would be good in read heavy systems where we can afford toodo computations on writes in order toooptimize reads.</span></span>

<span data-ttu-id="07426-214">Olá capacidade toohave um modelo com campos calculados previamente é possibilitado porque oferece suporte a banco de dados do Azure Cosmos **transações de vários documentos**.</span><span class="sxs-lookup"><span data-stu-id="07426-214">hello ability toohave a model with pre-calculated fields is made possible because Azure Cosmos DB supports **multi-document transactions**.</span></span> <span data-ttu-id="07426-215">Muitos repositórios NoSQL não podem fazer transações entre documentos e portanto defendem decisões de design, como "sempre incorporar tudo", devido a limitação de toothis.</span><span class="sxs-lookup"><span data-stu-id="07426-215">Many NoSQL stores cannot do transactions across documents and therefore advocate design decisions, such as "always embed everything", due toothis limitation.</span></span> <span data-ttu-id="07426-216">Com o Azure Cosmos DB, você pode usar gatilhos do lado do servidor ou procedimentos armazenados, que inserem manuais e atualizam autores, tudo isso em uma transação ACID.</span><span class="sxs-lookup"><span data-stu-id="07426-216">With Azure Cosmos DB, you can use server-side triggers, or stored procedures, that insert books and update authors all within an ACID transaction.</span></span> <span data-ttu-id="07426-217">Agora você não **ter** tooembed tudo no tooone documento apenas toobe-se de que seus dados permaneçam consistentes.</span><span class="sxs-lookup"><span data-stu-id="07426-217">Now you don't **have** tooembed everything in tooone document just toobe sure that your data remains consistent.</span></span>

## <span data-ttu-id="07426-218"><a name="NextSteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="07426-218"><a name="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="07426-219">argumentos de maiores Olá deste artigo é toounderstand que em um mundo independentes de esquema de modelagem de dados são tão importantes como nunca.</span><span class="sxs-lookup"><span data-stu-id="07426-219">hello biggest takeaways from this article is toounderstand that data modeling in a schema-free world is just as important as ever.</span></span> 

<span data-ttu-id="07426-220">Como não há nenhum toorepresent de maneira única uma parte dos dados em uma tela, não há nenhum toomodel de uma maneira de seus dados.</span><span class="sxs-lookup"><span data-stu-id="07426-220">Just as there is no single way toorepresent a piece of data on a screen, there is no single way toomodel your data.</span></span> <span data-ttu-id="07426-221">Você precisa toounderstand seu aplicativo e como ele produzirá consumir e processar dados saudação.</span><span class="sxs-lookup"><span data-stu-id="07426-221">You need toounderstand your application and how it will produce, consume, and process hello data.</span></span> <span data-ttu-id="07426-222">Em seguida, aplicando alguns Olá diretrizes apresentadas aqui, você podem definir sobre como criar um modelo que atenda às necessidades imediatas de saudação do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="07426-222">Then, by applying some of hello guidelines presented here you can set about creating a model that addresses hello immediate needs of your application.</span></span> <span data-ttu-id="07426-223">Quando seus aplicativos precisam toochange, você pode aproveitar flexibilidade de saudação de um banco de dados independentes de esquema tooembrace que alterar e desenvolver seu modelo de dados facilmente.</span><span class="sxs-lookup"><span data-stu-id="07426-223">When your applications need toochange, you can leverage hello flexibility of a schema-free database tooembrace that change and evolve your data model easily.</span></span> 

<span data-ttu-id="07426-224">toolearn mais sobre Azure Cosmos DB, consulte do serviço toohello [documentação](https://azure.microsoft.com/documentation/services/cosmos-db/) página.</span><span class="sxs-lookup"><span data-stu-id="07426-224">toolearn more about Azure Cosmos DB, refer toohello service's [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span> 

<span data-ttu-id="07426-225">toounderstand como tooshard seus dados por várias partições, consulte muito[particionamento de dados no banco de dados do Azure Cosmos](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="07426-225">toounderstand how tooshard your data across multiple partitions, refer too[Partitioning Data in Azure Cosmos DB](documentdb-partition-data.md).</span></span> 
