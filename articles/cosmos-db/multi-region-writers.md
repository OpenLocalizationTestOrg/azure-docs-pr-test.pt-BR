---
title: arquiteturas de banco de dados mestre aaaMulti com o banco de dados do Azure Cosmos | Microsoft Docs
description: "Saiba mais sobre como arquiteturas de aplicativo toodesign com local lê e grava em várias regiões geográficas com o banco de dados do Azure Cosmos."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 706ced74-ea67-45dd-a7de-666c3c893687
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3269c8405afe16f75db69b42e576fe76e00a8e16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="multi-master-globally-replicated-database-architectures-with-azure-cosmos-db"></a><span data-ttu-id="a503f-103">Arquiteturas de banco de dados replicadas globalmente de vários mestres com o Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a503f-103">Multi-master globally replicated database architectures with Azure Cosmos DB</span></span>
<span data-ttu-id="a503f-104">Banco de dados do Azure Cosmos oferece suporte completo [replicação global](distribute-data-globally.md), que permite a você toodistribute as regiões de dados toomultiple com acesso de baixa latência em qualquer lugar na carga de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="a503f-104">Azure Cosmos DB supports turnkey [global replication](distribute-data-globally.md), which allows you toodistribute data toomultiple regions with low latency access anywhere in hello workload.</span></span> <span data-ttu-id="a503f-105">Esse modelo é usado para cargas de trabalho do publisher/consumidor onde há um gravador em uma única região geográfica e leitores distribuídos globalmente em outras regiões (leitura).</span><span class="sxs-lookup"><span data-stu-id="a503f-105">This model is commonly used for publisher/consumer workloads where there is a writer in a single geographic region and globally distributed readers in other (read) regions.</span></span> 

<span data-ttu-id="a503f-106">Você também pode usar replicação global suporte toobuild aplicativos do Azure Cosmos DB em que os gravadores e leitores são globalmente distribuídos.</span><span class="sxs-lookup"><span data-stu-id="a503f-106">You can also use Azure Cosmos DB's global replication support toobuild applications in which writers and readers are globally distributed.</span></span> <span data-ttu-id="a503f-107">Este documento descreve um padrão que permite obter gravação local e acesso de leitura local para gravadores distribuídos usando o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a503f-107">This document outlines a pattern that enables achieving local write and local read access for distributed writers using Azure Cosmos DB.</span></span>

## <span data-ttu-id="a503f-108"><a id="ExampleScenario"></a>Publicação de conteúdo - um cenário de exemplo</span><span class="sxs-lookup"><span data-stu-id="a503f-108"><a id="ExampleScenario"></a>Content Publishing - an example scenario</span></span>
<span data-ttu-id="a503f-109">Vamos examinar um toodescribe de cenário do mundo real como você pode usar padrões globalmente distribuídos multi region/vários mestres leitura e gravação com o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="a503f-109">Let's look at a real world scenario toodescribe how you can use globally distributed multi-region/multi-master read write patterns with Azure Cosmos DB.</span></span> <span data-ttu-id="a503f-110">Considere uma plataforma de publicação de conteúdo criada no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a503f-110">Consider a content publishing platform built on Azure Cosmos DB.</span></span> <span data-ttu-id="a503f-111">Aqui estão alguns requisitos que essa plataforma deve atender para uma excelente experiência de usuário para editores e consumidores.</span><span class="sxs-lookup"><span data-stu-id="a503f-111">Here are some requirements that this platform must meet for a great user experience for both publishers and consumers.</span></span>

* <span data-ttu-id="a503f-112">Autores e os assinantes são distribuídos por Olá, mundo</span><span class="sxs-lookup"><span data-stu-id="a503f-112">Both authors and subscribers are spread over hello world</span></span> 
* <span data-ttu-id="a503f-113">Os autores devem publicar (gravação) artigos tootheir (próximo) região local</span><span class="sxs-lookup"><span data-stu-id="a503f-113">Authors must publish (write) articles tootheir local (closest) region</span></span>
* <span data-ttu-id="a503f-114">Os autores têm leitores/assinantes de seus artigos que são distribuídos globo hello.</span><span class="sxs-lookup"><span data-stu-id="a503f-114">Authors have readers/subscribers of their articles who are distributed across hello globe.</span></span> 
* <span data-ttu-id="a503f-115">Os assinantes devem receber uma notificação quando novos artigos são publicados.</span><span class="sxs-lookup"><span data-stu-id="a503f-115">Subscribers should get a notification when new articles are published.</span></span>
* <span data-ttu-id="a503f-116">Assinantes devem ser capaz de tooread artigos da sua região local.</span><span class="sxs-lookup"><span data-stu-id="a503f-116">Subscribers must be able tooread articles from their local region.</span></span> <span data-ttu-id="a503f-117">Eles também devem ser capaz de tooadd revisões toothese artigos.</span><span class="sxs-lookup"><span data-stu-id="a503f-117">They should also be able tooadd reviews toothese articles.</span></span> 
* <span data-ttu-id="a503f-118">Qualquer pessoa, incluindo autor Olá artigos Olá deve ser capaz de exibir que todos os Olá tooarticles anexado de análises de uma região de local.</span><span class="sxs-lookup"><span data-stu-id="a503f-118">Anyone including hello author of hello articles should be able view all hello reviews attached tooarticles from a local region.</span></span> 

<span data-ttu-id="a503f-119">Supondo que milhões de consumidores e editores com bilhões de artigos, assim, temos tooconfront problemas de saudação de escala junto com garantindo a localidade de acesso.</span><span class="sxs-lookup"><span data-stu-id="a503f-119">Assuming millions of consumers and publishers with billions of articles, soon we have tooconfront hello problems of scale along with guaranteeing locality of access.</span></span> <span data-ttu-id="a503f-120">Assim como acontece com a maioria dos problemas de escalabilidade, a solução hello está em uma boa estratégia de particionamento.</span><span class="sxs-lookup"><span data-stu-id="a503f-120">As with most scalability problems, hello solution lies in a good partitioning strategy.</span></span> <span data-ttu-id="a503f-121">Em seguida, vamos examinar como toomodel artigos, revise e notificações como documentos, configuram contas de banco de dados do Azure Cosmos e implementar uma camada de acesso a dados.</span><span class="sxs-lookup"><span data-stu-id="a503f-121">Next, let's look at how toomodel articles, review, and notifications as documents, configure Azure Cosmos DB accounts, and implement a data access layer.</span></span> 

<span data-ttu-id="a503f-122">Se você quiser toolearn mais informações sobre particionamento e chaves de partição, consulte [particionamento e escala no banco de dados do Azure Cosmos](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="a503f-122">If you would like toolearn more about partitioning and partition keys, see [Partitioning and Scaling in Azure Cosmos DB](partition-data.md).</span></span>

## <span data-ttu-id="a503f-123"><a id="ModelingNotifications"></a>Notificações de modelagem</span><span class="sxs-lookup"><span data-stu-id="a503f-123"><a id="ModelingNotifications"></a>Modeling notifications</span></span>
<span data-ttu-id="a503f-124">As notificações são um usuário de tooa específico de feeds de dados.</span><span class="sxs-lookup"><span data-stu-id="a503f-124">Notifications are data feeds specific tooa user.</span></span> <span data-ttu-id="a503f-125">Portanto, os padrões de acesso Olá para documentos de notificações são sempre no contexto de saudação do usuário único.</span><span class="sxs-lookup"><span data-stu-id="a503f-125">Therefore, hello access patterns for notifications documents are always in hello context of single user.</span></span> <span data-ttu-id="a503f-126">Por exemplo, você seria "lançar um usuário de notificação tooa" ou "buscar todas as notificações para um determinado usuário".</span><span class="sxs-lookup"><span data-stu-id="a503f-126">For example, you would "post a notification tooa user" or "fetch all notifications for a given user".</span></span> <span data-ttu-id="a503f-127">Olá, portanto, escolha ideal de chave de particionamento para esse tipo seria `UserId`.</span><span class="sxs-lookup"><span data-stu-id="a503f-127">So, hello optimal choice of partitioning key for this type would be `UserId`.</span></span>

    class Notification 
    { 
        // Unique ID for Notification. 
        public string Id { get; set; }

        // hello user Id for which notification is addressed to. 
        public string UserId { get; set; }

        // hello partition Key for hello resource. 
        public string PartitionKey 
        { 
            get 
            { 
                return this.UserId; 
            }
        }

        // Subscription for which this notification is raised. 
        public string SubscriptionFilter { get; set; }

        // Subject of hello notification. 
        public string ArticleId { get; set; } 
    }

## <span data-ttu-id="a503f-128"><a id="ModelingSubscriptions"></a>Assinaturas de modelagem</span><span class="sxs-lookup"><span data-stu-id="a503f-128"><a id="ModelingSubscriptions"></a>Modeling subscriptions</span></span>
<span data-ttu-id="a503f-129">As assinaturas podem ser criadas para vários critérios, como uma categoria específica de artigos de interesse ou uma editora específica.</span><span class="sxs-lookup"><span data-stu-id="a503f-129">Subscriptions can be created for various criteria like a specific category of articles of interest, or a specific publisher.</span></span> <span data-ttu-id="a503f-130">Olá, portanto, `SubscriptionFilter` é uma boa opção para a chave de partição.</span><span class="sxs-lookup"><span data-stu-id="a503f-130">Hence hello `SubscriptionFilter` is a good choice for partition key.</span></span>

    class Subscriptions 
    { 
        // Unique ID for Subscription 
        public string Id { get; set; }

        // Subscription source. Could be Author | Category etc. 
        public string SubscriptionFilter { get; set; }

        // subscribing User. 
        public string UserId { get; set; }

        public string PartitionKey 
        { 
            get 
            { 
                return this.SubscriptionFilter; 
            } 
        } 
    }

## <span data-ttu-id="a503f-131"><a id="ModelingArticles"></a>Artigos de modelagem</span><span class="sxs-lookup"><span data-stu-id="a503f-131"><a id="ModelingArticles"></a>Modeling articles</span></span>
<span data-ttu-id="a503f-132">Quando um artigo é identificado por meio de notificações, as consultas subsequentes normalmente são baseadas no hello `Article.Id`.</span><span class="sxs-lookup"><span data-stu-id="a503f-132">Once an article is identified through notifications, subsequent queries are typically based on hello `Article.Id`.</span></span> <span data-ttu-id="a503f-133">Escolhendo `Article.Id` como partição chave hello, portanto, fornece a distribuição melhor Olá para armazenar artigos dentro de uma coleção de banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="a503f-133">Choosing `Article.Id` as partition hello key thus provides hello best distribution for storing articles inside an Azure Cosmos DB collection.</span></span> 

    class Article 
    { 
        // Unique ID for Article 
        public string Id { get; set; }
        
        public string PartitionKey 
        { 
            get 
            { 
                return this.Id; 
            } 
        }
        
        // Author of hello article
        public string Author { get; set; }

        // Category/genre of hello article
        public string Category { get; set; }

        // Tags associated with hello article
        public string[] Tags { get; set; }

        // Title of hello article
        public string Title { get; set; }
        
        //... 
    }

## <span data-ttu-id="a503f-134"><a id="ModelingReviews"></a>Análises de modelagem</span><span class="sxs-lookup"><span data-stu-id="a503f-134"><a id="ModelingReviews"></a>Modeling reviews</span></span>
<span data-ttu-id="a503f-135">Como artigos, análises principalmente são gravados e lidos no contexto de saudação do artigo.</span><span class="sxs-lookup"><span data-stu-id="a503f-135">Like articles, reviews are mostly written and read in hello context of article.</span></span> <span data-ttu-id="a503f-136">Escolhendo `ArticleId` como uma partição chave fornece acesso eficiente das revisões associada ao artigo e melhor distribuição.</span><span class="sxs-lookup"><span data-stu-id="a503f-136">Choosing `ArticleId` as a partition key provides best distribution and efficient access of reviews associated with article.</span></span> 

    class Review 
    { 
        // Unique ID for Review 
        public string Id { get; set; }

        // Article Id of hello review 
        public string ArticleId { get; set; }

        public string PartitionKey 
        { 
            get 
            { 
                return this.ArticleId; 
            } 
        }
        
        //Reviewer Id 
        public string UserId { get; set; }
        public string ReviewText { get; set; }
        
        public int Rating { get; set; } }
    }

## <span data-ttu-id="a503f-137"><a id="DataAccessMethods"></a>Métodos de camada de acesso de dados</span><span class="sxs-lookup"><span data-stu-id="a503f-137"><a id="DataAccessMethods"></a>Data access layer methods</span></span>
<span data-ttu-id="a503f-138">Agora vamos dar uma olhada em dados principal Olá precisamos tooimplement os métodos de acesso.</span><span class="sxs-lookup"><span data-stu-id="a503f-138">Now let's look at hello main data access methods we need tooimplement.</span></span> <span data-ttu-id="a503f-139">Aqui está a lista Olá dos métodos Olá `ContentPublishDatabase` precisa:</span><span class="sxs-lookup"><span data-stu-id="a503f-139">Here's hello list of methods that hello `ContentPublishDatabase` needs:</span></span>

    class ContentPublishDatabase 
    { 
        public async Task CreateSubscriptionAsync(string userId, string category);
    
        public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId);
    
        public async Task<Article> ReadArticleAsync(string articleId);
    
        public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating);
    
        public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId); 
    }

## <span data-ttu-id="a503f-140"><a id="Architecture"></a>Configuração de conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a503f-140"><a id="Architecture"></a>Azure Cosmos DB account configuration</span></span>
<span data-ttu-id="a503f-141">tooguarantee local leituras e gravações, é necessário particionar dados não apenas na chave de partição, mas também com base no padrão de acesso geográfica de saudação em regiões.</span><span class="sxs-lookup"><span data-stu-id="a503f-141">tooguarantee local reads and writes, we must partition data not just on partition key, but also based on hello geographical access pattern into regions.</span></span> <span data-ttu-id="a503f-142">modelo de saudação depende de ter uma conta de banco de dados de banco de dados do Azure Cosmos replicado geograficamente para cada região.</span><span class="sxs-lookup"><span data-stu-id="a503f-142">hello model relies on having a geo-replicated Azure Cosmos DB database account for each region.</span></span> <span data-ttu-id="a503f-143">Por exemplo, com duas regiões, aqui está uma configuração para gravações de várias regiões:</span><span class="sxs-lookup"><span data-stu-id="a503f-143">For example, with two regions, here's a setup for multi-region writes:</span></span>

| <span data-ttu-id="a503f-144">Nome da conta</span><span class="sxs-lookup"><span data-stu-id="a503f-144">Account Name</span></span> | <span data-ttu-id="a503f-145">Região de gravação</span><span class="sxs-lookup"><span data-stu-id="a503f-145">Write Region</span></span> | <span data-ttu-id="a503f-146">Região de leitura</span><span class="sxs-lookup"><span data-stu-id="a503f-146">Read Region</span></span> |
| --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |

<span data-ttu-id="a503f-147">Olá diagrama a seguir mostra como leituras e gravações são executadas em um aplicativo típico com esta configuração:</span><span class="sxs-lookup"><span data-stu-id="a503f-147">hello following diagram shows how reads and writes are performed in a typical application with this setup:</span></span>

![Arquitetura de vários mestres do Azure Cosmos DB](./media/multi-region-writers/multi-master.png)

<span data-ttu-id="a503f-149">Aqui está um trecho de código mostrando como tooinitialize Olá clientes em uma DAL em execução no hello `West US` região.</span><span class="sxs-lookup"><span data-stu-id="a503f-149">Here is a code snippet showing how tooinitialize hello clients in a DAL running in hello `West US` region.</span></span>
    
    ConnectionPolicy writeClientPolicy = new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp };
    writeClientPolicy.PreferredLocations.Add(LocationNames.WestUS);
    writeClientPolicy.PreferredLocations.Add(LocationNames.NorthEurope);

    DocumentClient writeClient = new DocumentClient(
        new Uri("https://contentpubdatabase-usa.documents.azure.com"), 
        writeRegionAuthKey,
        writeClientPolicy);

    ConnectionPolicy readClientPolicy = new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp };
    readClientPolicy.PreferredLocations.Add(LocationNames.NorthEurope);
    readClientPolicy.PreferredLocations.Add(LocationNames.WestUS);

    DocumentClient readClient = new DocumentClient(
        new Uri("https://contentpubdatabase-europe.documents.azure.com"),
        readRegionAuthKey,
        readClientPolicy);

<span data-ttu-id="a503f-150">Com hello antes da instalação, camada de acesso a dados Olá pode encaminhar todas as gravações toohello conta local com base em onde ele é implantado.</span><span class="sxs-lookup"><span data-stu-id="a503f-150">With hello preceding setup, hello data access layer can forward all writes toohello local account based on where it is deployed.</span></span> <span data-ttu-id="a503f-151">As leituras são executadas com a leitura de ambas as contas tooget Olá global modo de exibição de dados.</span><span class="sxs-lookup"><span data-stu-id="a503f-151">Reads are performed by reading from both accounts tooget hello global view of data.</span></span> <span data-ttu-id="a503f-152">Essa abordagem pode ser estendido tooas várias regiões, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="a503f-152">This approach can be extended tooas many regions as required.</span></span> <span data-ttu-id="a503f-153">Por exemplo, aqui está uma configuração com três regiões geográficas:</span><span class="sxs-lookup"><span data-stu-id="a503f-153">For example, here's a setup with three geographic regions:</span></span>

| <span data-ttu-id="a503f-154">Nome da conta</span><span class="sxs-lookup"><span data-stu-id="a503f-154">Account Name</span></span> | <span data-ttu-id="a503f-155">Região de gravação</span><span class="sxs-lookup"><span data-stu-id="a503f-155">Write Region</span></span> | <span data-ttu-id="a503f-156">Leitura região 1</span><span class="sxs-lookup"><span data-stu-id="a503f-156">Read Region 1</span></span> | <span data-ttu-id="a503f-157">Região de leitura 2</span><span class="sxs-lookup"><span data-stu-id="a503f-157">Read Region 2</span></span> |
| --- | --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |`Southeast Asia` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |`Southeast Asia` |
| `contentpubdatabase-asia.documents.azure.com` | `Southeast Asia` |`North Europe` |`West US` |

## <span data-ttu-id="a503f-158"><a id="DataAccessImplementation"></a>Implementação de camada de acesso de dados</span><span class="sxs-lookup"><span data-stu-id="a503f-158"><a id="DataAccessImplementation"></a>Data access layer implementation</span></span>
<span data-ttu-id="a503f-159">Agora vamos dar uma olhada na implementação de Olá Olá acesso da camada de dados (DAL) para um aplicativo com duas regiões graváveis.</span><span class="sxs-lookup"><span data-stu-id="a503f-159">Now let's look at hello implementation of hello data access layer (DAL) for an application with two writable regions.</span></span> <span data-ttu-id="a503f-160">Olá DAL deve implementar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a503f-160">hello DAL must implement hello following steps:</span></span>

* <span data-ttu-id="a503f-161">Criar várias instâncias de `DocumentClient` para cada conta.</span><span class="sxs-lookup"><span data-stu-id="a503f-161">Create multiple instances of `DocumentClient` for each account.</span></span> <span data-ttu-id="a503f-162">Com duas regiões, cada instância DAL tem um `writeClient` e um `readClient`.</span><span class="sxs-lookup"><span data-stu-id="a503f-162">With two regions, each DAL instance has one `writeClient` and one `readClient`.</span></span> 
* <span data-ttu-id="a503f-163">Com base na região de saudação implantada do aplicativo hello, configurar pontos de extremidade Olá para `writeclient` e `readClient`.</span><span class="sxs-lookup"><span data-stu-id="a503f-163">Based on hello deployed region of hello application, configure hello endpoints for `writeclient` and `readClient`.</span></span> <span data-ttu-id="a503f-164">Por exemplo, a saudação DAL implantado em `West US` usa `contentpubdatabase-usa.documents.azure.com` para realizar gravações.</span><span class="sxs-lookup"><span data-stu-id="a503f-164">For example, hello DAL deployed in `West US` uses `contentpubdatabase-usa.documents.azure.com` for performing writes.</span></span> <span data-ttu-id="a503f-165">Olá DAL implantado em `NorthEurope` usa `contentpubdatabase-europ.documents.azure.com` para gravações.</span><span class="sxs-lookup"><span data-stu-id="a503f-165">hello DAL deployed in `NorthEurope` uses `contentpubdatabase-europ.documents.azure.com` for writes.</span></span>

<span data-ttu-id="a503f-166">Com hello antes da instalação, Olá métodos de acesso de dados podem ser implementados.</span><span class="sxs-lookup"><span data-stu-id="a503f-166">With hello preceding setup, hello data access methods can be implemented.</span></span> <span data-ttu-id="a503f-167">Gravar operações encaminham Olá gravação toohello correspondente `writeClient`.</span><span class="sxs-lookup"><span data-stu-id="a503f-167">Write operations forward hello write toohello corresponding `writeClient`.</span></span>

    public async Task CreateSubscriptionAsync(string userId, string category)
    {
        await this.writeClient.CreateDocumentAsync(this.contentCollection, new Subscriptions
        {
            UserId = userId,
            SubscriptionFilter = category
        });
    }

    public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating)
    {
        await this.writeClient.CreateDocumentAsync(this.contentCollection, new Review
        {
            UserId = userId,
            ArticleId = articleId,
            ReviewText = reviewText,
            Rating = rating
        });
    }

<span data-ttu-id="a503f-168">Para ler as notificações e análises, você deve ler de regiões e resultados de união Olá conforme Olá trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="a503f-168">For reading notifications and reviews, you must read from both regions and union hello results as shown in hello following snippet:</span></span>

    public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId)
    {
        IDocumentQuery<Notification> writeAccountNotification = (
            from notification in this.writeClient.CreateDocumentQuery<Notification>(this.contentCollection) 
            where notification.UserId == userId 
            select notification).AsDocumentQuery();
        
        IDocumentQuery<Notification> readAccountNotification = (
            from notification in this.readClient.CreateDocumentQuery<Notification>(this.contentCollection) 
            where notification.UserId == userId 
            select notification).AsDocumentQuery();

        List<Notification> notifications = new List<Notification>();

        while (writeAccountNotification.HasMoreResults || readAccountNotification.HasMoreResults)
        {
            IList<Task<FeedResponse<Notification>>> results = new List<Task<FeedResponse<Notification>>>();

            if (writeAccountNotification.HasMoreResults)
            {
                results.Add(writeAccountNotification.ExecuteNextAsync<Notification>());
            }

            if (readAccountNotification.HasMoreResults)
            {
                results.Add(readAccountNotification.ExecuteNextAsync<Notification>());
            }

            IList<FeedResponse<Notification>> notificationFeedResult = await Task.WhenAll(results);

            foreach (FeedResponse<Notification> feed in notificationFeedResult)
            {
                notifications.AddRange(feed);
            }
        }
        return notifications;
    }

    public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId)
    {
        IDocumentQuery<Review> writeAccountReviews = (
            from review in this.writeClient.CreateDocumentQuery<Review>(this.contentCollection) 
            where review.ArticleId == articleId 
            select review).AsDocumentQuery();
        
        IDocumentQuery<Review> readAccountReviews = (
            from review in this.readClient.CreateDocumentQuery<Review>(this.contentCollection) 
            where review.ArticleId == articleId 
            select review).AsDocumentQuery();

        List<Review> reviews = new List<Review>();
        
        while (writeAccountReviews.HasMoreResults || readAccountReviews.HasMoreResults)
        {
            IList<Task<FeedResponse<Review>>> results = new List<Task<FeedResponse<Review>>>();

            if (writeAccountReviews.HasMoreResults)
            {
                results.Add(writeAccountReviews.ExecuteNextAsync<Review>());
            }

            if (readAccountReviews.HasMoreResults)
            {
                results.Add(readAccountReviews.ExecuteNextAsync<Review>());
            }

            IList<FeedResponse<Review>> notificationFeedResult = await Task.WhenAll(results);

            foreach (FeedResponse<Review> feed in notificationFeedResult)
            {
                reviews.AddRange(feed);
            }
        }

        return reviews;
    }

<span data-ttu-id="a503f-169">Portanto, ao escolher uma boa chave de particionamento e particionamento estático baseado em conta, você pode obter leituras e gravações locais de várias regiões usando o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a503f-169">Thus, by choosing a good partitioning key and static account-based partitioning, you can achieve multi-region local writes and reads using Azure Cosmos DB.</span></span>

## <span data-ttu-id="a503f-170"><a id="NextSteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a503f-170"><a id="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="a503f-171">Neste artigo, descrevemos como você pode usar padrões de leitura e gravação de várias regiões distribuídos globalmente com o Azure Cosmos DB usando a publicação de conteúdo como um cenário de exemplo.</span><span class="sxs-lookup"><span data-stu-id="a503f-171">In this article, we described how you can use globally distributed multi-region read write patterns with Azure Cosmos DB using content publishing as a sample scenario.</span></span>

* <span data-ttu-id="a503f-172">Saiba sobre como o Azure Cosmos DB dá suporte à [distribuição global](distribute-data-globally.md)</span><span class="sxs-lookup"><span data-stu-id="a503f-172">Learn about how Azure Cosmos DB supports [global distribution](distribute-data-globally.md)</span></span>
* <span data-ttu-id="a503f-173">Saiba mais sobre [failovers automáticos e manuais no Azure Cosmos DB](regional-failover.md)</span><span class="sxs-lookup"><span data-stu-id="a503f-173">Learn about [automatic and manual failovers in Azure Cosmos DB](regional-failover.md)</span></span>
* <span data-ttu-id="a503f-174">Saiba mais sobre [consistência global com o Azure Cosmos DB](consistency-levels.md)</span><span class="sxs-lookup"><span data-stu-id="a503f-174">Learn about [global consistency with Azure Cosmos DB](consistency-levels.md)</span></span>
* <span data-ttu-id="a503f-175">Desenvolver com várias regiões usando Olá [Azure Cosmos DB - API DocumentDB](tutorial-global-distribution-documentdb.md)</span><span class="sxs-lookup"><span data-stu-id="a503f-175">Develop with multiple regions using hello [Azure Cosmos DB - DocumentDB API](tutorial-global-distribution-documentdb.md)</span></span>
* <span data-ttu-id="a503f-176">Desenvolver com várias regiões usando Olá [Azure Cosmos DB - API do MongoDB](tutorial-global-distribution-MongoDB.md)</span><span class="sxs-lookup"><span data-stu-id="a503f-176">Develop with multiple regions using hello [Azure Cosmos DB - MongoDB API](tutorial-global-distribution-MongoDB.md)</span></span>
* <span data-ttu-id="a503f-177">Desenvolver com várias regiões usando Olá [Azure Cosmos DB - API de tabela](tutorial-global-distribution-table.md)</span><span class="sxs-lookup"><span data-stu-id="a503f-177">Develop with multiple regions using hello [Azure Cosmos DB - Table API](tutorial-global-distribution-table.md)</span></span>
