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
# <a name="multi-master-globally-replicated-database-architectures-with-azure-cosmos-db"></a>Arquiteturas de banco de dados replicadas globalmente de vários mestres com o Azure Cosmos DB
Banco de dados do Azure Cosmos oferece suporte completo [replicação global](distribute-data-globally.md), que permite a você toodistribute as regiões de dados toomultiple com acesso de baixa latência em qualquer lugar na carga de trabalho de saudação. Esse modelo é usado para cargas de trabalho do publisher/consumidor onde há um gravador em uma única região geográfica e leitores distribuídos globalmente em outras regiões (leitura). 

Você também pode usar replicação global suporte toobuild aplicativos do Azure Cosmos DB em que os gravadores e leitores são globalmente distribuídos. Este documento descreve um padrão que permite obter gravação local e acesso de leitura local para gravadores distribuídos usando o Azure Cosmos DB.

## <a id="ExampleScenario"></a>Publicação de conteúdo - um cenário de exemplo
Vamos examinar um toodescribe de cenário do mundo real como você pode usar padrões globalmente distribuídos multi region/vários mestres leitura e gravação com o banco de dados do Azure Cosmos. Considere uma plataforma de publicação de conteúdo criada no Azure Cosmos DB. Aqui estão alguns requisitos que essa plataforma deve atender para uma excelente experiência de usuário para editores e consumidores.

* Autores e os assinantes são distribuídos por Olá, mundo 
* Os autores devem publicar (gravação) artigos tootheir (próximo) região local
* Os autores têm leitores/assinantes de seus artigos que são distribuídos globo hello. 
* Os assinantes devem receber uma notificação quando novos artigos são publicados.
* Assinantes devem ser capaz de tooread artigos da sua região local. Eles também devem ser capaz de tooadd revisões toothese artigos. 
* Qualquer pessoa, incluindo autor Olá artigos Olá deve ser capaz de exibir que todos os Olá tooarticles anexado de análises de uma região de local. 

Supondo que milhões de consumidores e editores com bilhões de artigos, assim, temos tooconfront problemas de saudação de escala junto com garantindo a localidade de acesso. Assim como acontece com a maioria dos problemas de escalabilidade, a solução hello está em uma boa estratégia de particionamento. Em seguida, vamos examinar como toomodel artigos, revise e notificações como documentos, configuram contas de banco de dados do Azure Cosmos e implementar uma camada de acesso a dados. 

Se você quiser toolearn mais informações sobre particionamento e chaves de partição, consulte [particionamento e escala no banco de dados do Azure Cosmos](partition-data.md).

## <a id="ModelingNotifications"></a>Notificações de modelagem
As notificações são um usuário de tooa específico de feeds de dados. Portanto, os padrões de acesso Olá para documentos de notificações são sempre no contexto de saudação do usuário único. Por exemplo, você seria "lançar um usuário de notificação tooa" ou "buscar todas as notificações para um determinado usuário". Olá, portanto, escolha ideal de chave de particionamento para esse tipo seria `UserId`.

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

## <a id="ModelingSubscriptions"></a>Assinaturas de modelagem
As assinaturas podem ser criadas para vários critérios, como uma categoria específica de artigos de interesse ou uma editora específica. Olá, portanto, `SubscriptionFilter` é uma boa opção para a chave de partição.

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

## <a id="ModelingArticles"></a>Artigos de modelagem
Quando um artigo é identificado por meio de notificações, as consultas subsequentes normalmente são baseadas no hello `Article.Id`. Escolhendo `Article.Id` como partição chave hello, portanto, fornece a distribuição melhor Olá para armazenar artigos dentro de uma coleção de banco de dados do Azure Cosmos. 

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

## <a id="ModelingReviews"></a>Análises de modelagem
Como artigos, análises principalmente são gravados e lidos no contexto de saudação do artigo. Escolhendo `ArticleId` como uma partição chave fornece acesso eficiente das revisões associada ao artigo e melhor distribuição. 

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

## <a id="DataAccessMethods"></a>Métodos de camada de acesso de dados
Agora vamos dar uma olhada em dados principal Olá precisamos tooimplement os métodos de acesso. Aqui está a lista Olá dos métodos Olá `ContentPublishDatabase` precisa:

    class ContentPublishDatabase 
    { 
        public async Task CreateSubscriptionAsync(string userId, string category);
    
        public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId);
    
        public async Task<Article> ReadArticleAsync(string articleId);
    
        public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating);
    
        public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId); 
    }

## <a id="Architecture"></a>Configuração de conta do Azure Cosmos DB
tooguarantee local leituras e gravações, é necessário particionar dados não apenas na chave de partição, mas também com base no padrão de acesso geográfica de saudação em regiões. modelo de saudação depende de ter uma conta de banco de dados de banco de dados do Azure Cosmos replicado geograficamente para cada região. Por exemplo, com duas regiões, aqui está uma configuração para gravações de várias regiões:

| Nome da conta | Região de gravação | Região de leitura |
| --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |

Olá diagrama a seguir mostra como leituras e gravações são executadas em um aplicativo típico com esta configuração:

![Arquitetura de vários mestres do Azure Cosmos DB](./media/multi-region-writers/multi-master.png)

Aqui está um trecho de código mostrando como tooinitialize Olá clientes em uma DAL em execução no hello `West US` região.
    
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

Com hello antes da instalação, camada de acesso a dados Olá pode encaminhar todas as gravações toohello conta local com base em onde ele é implantado. As leituras são executadas com a leitura de ambas as contas tooget Olá global modo de exibição de dados. Essa abordagem pode ser estendido tooas várias regiões, conforme necessário. Por exemplo, aqui está uma configuração com três regiões geográficas:

| Nome da conta | Região de gravação | Leitura região 1 | Região de leitura 2 |
| --- | --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |`Southeast Asia` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |`Southeast Asia` |
| `contentpubdatabase-asia.documents.azure.com` | `Southeast Asia` |`North Europe` |`West US` |

## <a id="DataAccessImplementation"></a>Implementação de camada de acesso de dados
Agora vamos dar uma olhada na implementação de Olá Olá acesso da camada de dados (DAL) para um aplicativo com duas regiões graváveis. Olá DAL deve implementar Olá etapas a seguir:

* Criar várias instâncias de `DocumentClient` para cada conta. Com duas regiões, cada instância DAL tem um `writeClient` e um `readClient`. 
* Com base na região de saudação implantada do aplicativo hello, configurar pontos de extremidade Olá para `writeclient` e `readClient`. Por exemplo, a saudação DAL implantado em `West US` usa `contentpubdatabase-usa.documents.azure.com` para realizar gravações. Olá DAL implantado em `NorthEurope` usa `contentpubdatabase-europ.documents.azure.com` para gravações.

Com hello antes da instalação, Olá métodos de acesso de dados podem ser implementados. Gravar operações encaminham Olá gravação toohello correspondente `writeClient`.

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

Para ler as notificações e análises, você deve ler de regiões e resultados de união Olá conforme Olá trecho de código a seguir:

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

Portanto, ao escolher uma boa chave de particionamento e particionamento estático baseado em conta, você pode obter leituras e gravações locais de várias regiões usando o Azure Cosmos DB.

## <a id="NextSteps"></a>Próximas etapas
Neste artigo, descrevemos como você pode usar padrões de leitura e gravação de várias regiões distribuídos globalmente com o Azure Cosmos DB usando a publicação de conteúdo como um cenário de exemplo.

* Saiba sobre como o Azure Cosmos DB dá suporte à [distribuição global](distribute-data-globally.md)
* Saiba mais sobre [failovers automáticos e manuais no Azure Cosmos DB](regional-failover.md)
* Saiba mais sobre [consistência global com o Azure Cosmos DB](consistency-levels.md)
* Desenvolver com várias regiões usando Olá [Azure Cosmos DB - API DocumentDB](tutorial-global-distribution-documentdb.md)
* Desenvolver com várias regiões usando Olá [Azure Cosmos DB - API do MongoDB](tutorial-global-distribution-MongoDB.md)
* Desenvolver com várias regiões usando Olá [Azure Cosmos DB - API de tabela](tutorial-global-distribution-table.md)
