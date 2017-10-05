---
title: "Várias arquiteturas de banco de dados mestre com o Azure Cosmos DB | Microsoft Docs"
description: "Saiba mais sobre como projetar arquiteturas de aplicativos com leituras e gravações locais em várias regiões geográficas com o Azure Cosmos DB."
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
ms.openlocfilehash: cf1482ae7b1070023703f5dbe861d151f5d64fd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="multi-master-globally-replicated-database-architectures-with-azure-cosmos-db"></a><span data-ttu-id="5f1ad-103">Arquiteturas de banco de dados replicadas globalmente de vários mestres com o Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5f1ad-103">Multi-master globally replicated database architectures with Azure Cosmos DB</span></span>
<span data-ttu-id="5f1ad-104">O Azure Cosmos DB dá suporte turnkey à [replicação global](distribute-data-globally.md), que permite que você distribua dados para várias regiões com acesso de baixa latência em qualquer lugar na carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-104">Azure Cosmos DB supports turnkey [global replication](distribute-data-globally.md), which allows you to distribute data to multiple regions with low latency access anywhere in the workload.</span></span> <span data-ttu-id="5f1ad-105">Esse modelo é usado para cargas de trabalho do publisher/consumidor onde há um gravador em uma única região geográfica e leitores distribuídos globalmente em outras regiões (leitura).</span><span class="sxs-lookup"><span data-stu-id="5f1ad-105">This model is commonly used for publisher/consumer workloads where there is a writer in a single geographic region and globally distributed readers in other (read) regions.</span></span> 

<span data-ttu-id="5f1ad-106">Você também pode usar o suporte de replicação global do Azure Cosmos DB para criar aplicativos em que os gravadores e leitores são distribuídos globalmente.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-106">You can also use Azure Cosmos DB's global replication support to build applications in which writers and readers are globally distributed.</span></span> <span data-ttu-id="5f1ad-107">Este documento descreve um padrão que permite obter gravação local e acesso de leitura local para gravadores distribuídos usando o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-107">This document outlines a pattern that enables achieving local write and local read access for distributed writers using Azure Cosmos DB.</span></span>

## <span data-ttu-id="5f1ad-108"><a id="ExampleScenario"></a>Publicação de conteúdo - um cenário de exemplo</span><span class="sxs-lookup"><span data-stu-id="5f1ad-108"><a id="ExampleScenario"></a>Content Publishing - an example scenario</span></span>
<span data-ttu-id="5f1ad-109">Vamos examinar um cenário do mundo real para descrever como você pode usar padrões de leitura e gravação de várias regiões/vários mestres distribuídos globalmente com o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-109">Let's look at a real world scenario to describe how you can use globally distributed multi-region/multi-master read write patterns with Azure Cosmos DB.</span></span> <span data-ttu-id="5f1ad-110">Considere uma plataforma de publicação de conteúdo criada no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-110">Consider a content publishing platform built on Azure Cosmos DB.</span></span> <span data-ttu-id="5f1ad-111">Aqui estão alguns requisitos que essa plataforma deve atender para uma excelente experiência de usuário para editores e consumidores.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-111">Here are some requirements that this platform must meet for a great user experience for both publishers and consumers.</span></span>

* <span data-ttu-id="5f1ad-112">Os autores e os assinantes estão espalhados pelo mundo</span><span class="sxs-lookup"><span data-stu-id="5f1ad-112">Both authors and subscribers are spread over the world</span></span> 
* <span data-ttu-id="5f1ad-113">Os autores devem publicar artigos (gravação) em sua região local (mais próxima)</span><span class="sxs-lookup"><span data-stu-id="5f1ad-113">Authors must publish (write) articles to their local (closest) region</span></span>
* <span data-ttu-id="5f1ad-114">Os autores têm leitores/assinantes de seus artigos distribuídos pelo mundo.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-114">Authors have readers/subscribers of their articles who are distributed across the globe.</span></span> 
* <span data-ttu-id="5f1ad-115">Os assinantes devem receber uma notificação quando novos artigos são publicados.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-115">Subscribers should get a notification when new articles are published.</span></span>
* <span data-ttu-id="5f1ad-116">Os assinantes devem ser capazes de ler artigos da sua região local.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-116">Subscribers must be able to read articles from their local region.</span></span> <span data-ttu-id="5f1ad-117">Também devem ser capazes de adicionar críticas a esses artigos.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-117">They should also be able to add reviews to these articles.</span></span> 
* <span data-ttu-id="5f1ad-118">Qualquer pessoa, incluindo o autor dos artigos, deve ser capaz de exibir todas as críticas anexados aos artigos de uma região local.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-118">Anyone including the author of the articles should be able view all the reviews attached to articles from a local region.</span></span> 

<span data-ttu-id="5f1ad-119">Supondo que haja milhões de clientes e fornecedores com bilhões de artigos, assim temos de enfrentar os problemas de escala junto com a garantia de localidade de acesso.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-119">Assuming millions of consumers and publishers with billions of articles, soon we have to confront the problems of scale along with guaranteeing locality of access.</span></span> <span data-ttu-id="5f1ad-120">Assim como acontece com a maioria dos problemas de escalabilidade, a solução está em uma boa estratégia de particionamento.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-120">As with most scalability problems, the solution lies in a good partitioning strategy.</span></span> <span data-ttu-id="5f1ad-121">Em seguida, vamos examinar como modelar artigos, revisão e notificações como documentos, configurar contas do Azure Cosmos DB e implementar uma camada de acesso a dados.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-121">Next, let's look at how to model articles, review, and notifications as documents, configure Azure Cosmos DB accounts, and implement a data access layer.</span></span> 

<span data-ttu-id="5f1ad-122">Se você quiser saber mais sobre particionamento e chaves de partição, consulte [Particionamento e dimensionamento no Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="5f1ad-122">If you would like to learn more about partitioning and partition keys, see [Partitioning and Scaling in Azure Cosmos DB](partition-data.md).</span></span>

## <span data-ttu-id="5f1ad-123"><a id="ModelingNotifications"></a>Notificações de modelagem</span><span class="sxs-lookup"><span data-stu-id="5f1ad-123"><a id="ModelingNotifications"></a>Modeling notifications</span></span>
<span data-ttu-id="5f1ad-124">As notificações são feeds específicos de dados para um usuário.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-124">Notifications are data feeds specific to a user.</span></span> <span data-ttu-id="5f1ad-125">Portanto, os padrões de acesso para documentos de notificações são sempre no contexto de usuário único.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-125">Therefore, the access patterns for notifications documents are always in the context of single user.</span></span> <span data-ttu-id="5f1ad-126">Por exemplo, você poderia "lançar uma notificação a um usuário" ou "buscar todas as notificações para um determinado usuário".</span><span class="sxs-lookup"><span data-stu-id="5f1ad-126">For example, you would "post a notification to a user" or "fetch all notifications for a given user".</span></span> <span data-ttu-id="5f1ad-127">Portanto, a opção de chave para esse tipo de particionamento ideal seria `UserId`.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-127">So, the optimal choice of partitioning key for this type would be `UserId`.</span></span>

    class Notification 
    { 
        // Unique ID for Notification. 
        public string Id { get; set; }

        // The user Id for which notification is addressed to. 
        public string UserId { get; set; }

        // The partition Key for the resource. 
        public string PartitionKey 
        { 
            get 
            { 
                return this.UserId; 
            }
        }

        // Subscription for which this notification is raised. 
        public string SubscriptionFilter { get; set; }

        // Subject of the notification. 
        public string ArticleId { get; set; } 
    }

## <span data-ttu-id="5f1ad-128"><a id="ModelingSubscriptions"></a>Assinaturas de modelagem</span><span class="sxs-lookup"><span data-stu-id="5f1ad-128"><a id="ModelingSubscriptions"></a>Modeling subscriptions</span></span>
<span data-ttu-id="5f1ad-129">As assinaturas podem ser criadas para vários critérios, como uma categoria específica de artigos de interesse ou uma editora específica.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-129">Subscriptions can be created for various criteria like a specific category of articles of interest, or a specific publisher.</span></span> <span data-ttu-id="5f1ad-130">Portanto, o `SubscriptionFilter` é uma boa opção para a chave de partição.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-130">Hence the `SubscriptionFilter` is a good choice for partition key.</span></span>

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

## <span data-ttu-id="5f1ad-131"><a id="ModelingArticles"></a>Artigos de modelagem</span><span class="sxs-lookup"><span data-stu-id="5f1ad-131"><a id="ModelingArticles"></a>Modeling articles</span></span>
<span data-ttu-id="5f1ad-132">Quando um artigo é identificado por meio de notificações, as consultas subsequentes são normalmente baseadas no `Article.Id`.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-132">Once an article is identified through notifications, subsequent queries are typically based on the `Article.Id`.</span></span> <span data-ttu-id="5f1ad-133">Portanto, escolher `Article.Id` como chave de partição oferece a melhor distribuição para armazenar artigos dentro de uma coleção do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-133">Choosing `Article.Id` as partition the key thus provides the best distribution for storing articles inside an Azure Cosmos DB collection.</span></span> 

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
        
        // Author of the article
        public string Author { get; set; }

        // Category/genre of the article
        public string Category { get; set; }

        // Tags associated with the article
        public string[] Tags { get; set; }

        // Title of the article
        public string Title { get; set; }
        
        //... 
    }

## <span data-ttu-id="5f1ad-134"><a id="ModelingReviews"></a>Análises de modelagem</span><span class="sxs-lookup"><span data-stu-id="5f1ad-134"><a id="ModelingReviews"></a>Modeling reviews</span></span>
<span data-ttu-id="5f1ad-135">Como artigos, resenhas principalmente são escritas e ler no contexto do artigo.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-135">Like articles, reviews are mostly written and read in the context of article.</span></span> <span data-ttu-id="5f1ad-136">Escolhendo `ArticleId` como uma partição chave fornece acesso eficiente das revisões associada ao artigo e melhor distribuição.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-136">Choosing `ArticleId` as a partition key provides best distribution and efficient access of reviews associated with article.</span></span> 

    class Review 
    { 
        // Unique ID for Review 
        public string Id { get; set; }

        // Article Id of the review 
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

## <span data-ttu-id="5f1ad-137"><a id="DataAccessMethods"></a>Métodos de camada de acesso de dados</span><span class="sxs-lookup"><span data-stu-id="5f1ad-137"><a id="DataAccessMethods"></a>Data access layer methods</span></span>
<span data-ttu-id="5f1ad-138">Agora vamos examinar os dados principais, precisamos implementar os métodos de acesso.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-138">Now let's look at the main data access methods we need to implement.</span></span> <span data-ttu-id="5f1ad-139">Aqui está a lista dos métodos que o `ContentPublishDatabase` precisa:</span><span class="sxs-lookup"><span data-stu-id="5f1ad-139">Here's the list of methods that the `ContentPublishDatabase` needs:</span></span>

    class ContentPublishDatabase 
    { 
        public async Task CreateSubscriptionAsync(string userId, string category);
    
        public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId);
    
        public async Task<Article> ReadArticleAsync(string articleId);
    
        public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating);
    
        public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId); 
    }

## <span data-ttu-id="5f1ad-140"><a id="Architecture"></a>Configuração de conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5f1ad-140"><a id="Architecture"></a>Azure Cosmos DB account configuration</span></span>
<span data-ttu-id="5f1ad-141">Para garantir a local lê e grava, podemos deve particionar dados será não apenas na partição chave, mas também com base no padrão de acesso geográfica em regiões.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-141">To guarantee local reads and writes, we must partition data not just on partition key, but also based on the geographical access pattern into regions.</span></span> <span data-ttu-id="5f1ad-142">O modelo se baseia em ter uma conta de banco de dados do Azure Cosmos DB replicada geograficamente para cada região.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-142">The model relies on having a geo-replicated Azure Cosmos DB database account for each region.</span></span> <span data-ttu-id="5f1ad-143">Por exemplo, com duas regiões, aqui está uma configuração para gravações de várias regiões:</span><span class="sxs-lookup"><span data-stu-id="5f1ad-143">For example, with two regions, here's a setup for multi-region writes:</span></span>

| <span data-ttu-id="5f1ad-144">Nome da conta</span><span class="sxs-lookup"><span data-stu-id="5f1ad-144">Account Name</span></span> | <span data-ttu-id="5f1ad-145">Região de gravação</span><span class="sxs-lookup"><span data-stu-id="5f1ad-145">Write Region</span></span> | <span data-ttu-id="5f1ad-146">Região de leitura</span><span class="sxs-lookup"><span data-stu-id="5f1ad-146">Read Region</span></span> |
| --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |

<span data-ttu-id="5f1ad-147">O diagrama a seguir mostra como as leituras e gravações são executadas em um aplicativo típico com esta configuração:</span><span class="sxs-lookup"><span data-stu-id="5f1ad-147">The following diagram shows how reads and writes are performed in a typical application with this setup:</span></span>

![Arquitetura de vários mestres do Azure Cosmos DB](./media/multi-region-writers/multi-master.png)

<span data-ttu-id="5f1ad-149">Aqui está um trecho de código mostrando como inicializar os clientes em uma DAL em execução no `West US` região.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-149">Here is a code snippet showing how to initialize the clients in a DAL running in the `West US` region.</span></span>
    
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

<span data-ttu-id="5f1ad-150">Com a configuração anterior, a camada de acesso a dados pode encaminhar todas as gravações para a conta local com base em onde ele é implantado.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-150">With the preceding setup, the data access layer can forward all writes to the local account based on where it is deployed.</span></span> <span data-ttu-id="5f1ad-151">As leituras são executadas pela leitura de ambas as contas para obter a exibição global dos dados.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-151">Reads are performed by reading from both accounts to get the global view of data.</span></span> <span data-ttu-id="5f1ad-152">Essa abordagem pode ser estendida para regiões tantos conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-152">This approach can be extended to as many regions as required.</span></span> <span data-ttu-id="5f1ad-153">Por exemplo, aqui está uma configuração com três regiões geográficas:</span><span class="sxs-lookup"><span data-stu-id="5f1ad-153">For example, here's a setup with three geographic regions:</span></span>

| <span data-ttu-id="5f1ad-154">Nome da conta</span><span class="sxs-lookup"><span data-stu-id="5f1ad-154">Account Name</span></span> | <span data-ttu-id="5f1ad-155">Região de gravação</span><span class="sxs-lookup"><span data-stu-id="5f1ad-155">Write Region</span></span> | <span data-ttu-id="5f1ad-156">Leitura região 1</span><span class="sxs-lookup"><span data-stu-id="5f1ad-156">Read Region 1</span></span> | <span data-ttu-id="5f1ad-157">Região de leitura 2</span><span class="sxs-lookup"><span data-stu-id="5f1ad-157">Read Region 2</span></span> |
| --- | --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |`Southeast Asia` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |`Southeast Asia` |
| `contentpubdatabase-asia.documents.azure.com` | `Southeast Asia` |`North Europe` |`West US` |

## <span data-ttu-id="5f1ad-158"><a id="DataAccessImplementation"></a>Implementação de camada de acesso de dados</span><span class="sxs-lookup"><span data-stu-id="5f1ad-158"><a id="DataAccessImplementation"></a>Data access layer implementation</span></span>
<span data-ttu-id="5f1ad-159">Agora vamos examinar a implementação da camada de acesso a dados (DAL) para um aplicativo com duas regiões graváveis.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-159">Now let's look at the implementation of the data access layer (DAL) for an application with two writable regions.</span></span> <span data-ttu-id="5f1ad-160">A DAL deve implementar as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="5f1ad-160">The DAL must implement the following steps:</span></span>

* <span data-ttu-id="5f1ad-161">Criar várias instâncias de `DocumentClient` para cada conta.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-161">Create multiple instances of `DocumentClient` for each account.</span></span> <span data-ttu-id="5f1ad-162">Com duas regiões, cada instância DAL tem um `writeClient` e um `readClient`.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-162">With two regions, each DAL instance has one `writeClient` and one `readClient`.</span></span> 
* <span data-ttu-id="5f1ad-163">Com base na região de implantação do aplicativo, configure os pontos de extremidade `writeclient` e `readClient`.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-163">Based on the deployed region of the application, configure the endpoints for `writeclient` and `readClient`.</span></span> <span data-ttu-id="5f1ad-164">Por exemplo, a DAL implantado em `West US` usa `contentpubdatabase-usa.documents.azure.com` para executar gravações.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-164">For example, the DAL deployed in `West US` uses `contentpubdatabase-usa.documents.azure.com` for performing writes.</span></span> <span data-ttu-id="5f1ad-165">A DAL implantado em `NorthEurope` usa `contentpubdatabase-europ.documents.azure.com` para gravações.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-165">The DAL deployed in `NorthEurope` uses `contentpubdatabase-europ.documents.azure.com` for writes.</span></span>

<span data-ttu-id="5f1ad-166">Com a configuração anterior, os métodos de acesso a dados podem ser implementados.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-166">With the preceding setup, the data access methods can be implemented.</span></span> <span data-ttu-id="5f1ad-167">Gravar operações encaminham a gravação correspondente `writeClient`.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-167">Write operations forward the write to the corresponding `writeClient`.</span></span>

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

<span data-ttu-id="5f1ad-168">Para ler notificações e revisões, você deve ler de regiões e união os resultados conforme mostrado no trecho a seguir:</span><span class="sxs-lookup"><span data-stu-id="5f1ad-168">For reading notifications and reviews, you must read from both regions and union the results as shown in the following snippet:</span></span>

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

<span data-ttu-id="5f1ad-169">Portanto, ao escolher uma boa chave de particionamento e particionamento estático baseado em conta, você pode obter leituras e gravações locais de várias regiões usando o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-169">Thus, by choosing a good partitioning key and static account-based partitioning, you can achieve multi-region local writes and reads using Azure Cosmos DB.</span></span>

## <span data-ttu-id="5f1ad-170"><a id="NextSteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5f1ad-170"><a id="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="5f1ad-171">Neste artigo, descrevemos como você pode usar padrões de leitura e gravação de várias regiões distribuídos globalmente com o Azure Cosmos DB usando a publicação de conteúdo como um cenário de exemplo.</span><span class="sxs-lookup"><span data-stu-id="5f1ad-171">In this article, we described how you can use globally distributed multi-region read write patterns with Azure Cosmos DB using content publishing as a sample scenario.</span></span>

* <span data-ttu-id="5f1ad-172">Saiba sobre como o Azure Cosmos DB dá suporte à [distribuição global](distribute-data-globally.md)</span><span class="sxs-lookup"><span data-stu-id="5f1ad-172">Learn about how Azure Cosmos DB supports [global distribution](distribute-data-globally.md)</span></span>
* <span data-ttu-id="5f1ad-173">Saiba mais sobre [failovers automáticos e manuais no Azure Cosmos DB](regional-failover.md)</span><span class="sxs-lookup"><span data-stu-id="5f1ad-173">Learn about [automatic and manual failovers in Azure Cosmos DB](regional-failover.md)</span></span>
* <span data-ttu-id="5f1ad-174">Saiba mais sobre [consistência global com o Azure Cosmos DB](consistency-levels.md)</span><span class="sxs-lookup"><span data-stu-id="5f1ad-174">Learn about [global consistency with Azure Cosmos DB](consistency-levels.md)</span></span>
* <span data-ttu-id="5f1ad-175">Desenvolver com várias regiões usando o [Azure Cosmos DB – API do DocumentDB](tutorial-global-distribution-documentdb.md)</span><span class="sxs-lookup"><span data-stu-id="5f1ad-175">Develop with multiple regions using the [Azure Cosmos DB - DocumentDB API](tutorial-global-distribution-documentdb.md)</span></span>
* <span data-ttu-id="5f1ad-176">Desenvolver com várias regiões usando o [Azure Cosmos DB – API do MongoDB](tutorial-global-distribution-MongoDB.md)</span><span class="sxs-lookup"><span data-stu-id="5f1ad-176">Develop with multiple regions using the [Azure Cosmos DB - MongoDB API](tutorial-global-distribution-MongoDB.md)</span></span>
* <span data-ttu-id="5f1ad-177">Desenvolver com várias regiões usando o [Azure Cosmos DB – API da Tabela](tutorial-global-distribution-table.md)</span><span class="sxs-lookup"><span data-stu-id="5f1ad-177">Develop with multiple regions using the [Azure Cosmos DB - Table API](tutorial-global-distribution-table.md)</span></span>
