---
title: "aaaHow toomanage simultâneo grava tooresources na pesquisa do Azure"
description: "Use colisões de ar intermediário de tooavoid de simultaneidade otimista em índices de pesquisa tooAzure atualizações ou exclusões, indexadores e fontes de dados."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 
ms.service: search
ms.devlang: 
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/21/2017
ms.author: heidist
ms.openlocfilehash: c061d2b5c4d2dbd0fd5633405b01ab2912fbc754
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-concurrency-in-azure-search"></a>Como a simultaneidade toomanage na pesquisa do Azure

Ao gerenciar recursos de pesquisa do Azure, como índices e fontes de dados, é importante tooupdate recursos com segurança, especialmente se os recursos são acessados simultaneamente por diferentes componentes do seu aplicativo. Quando dois clientes atualizam simultaneamente um recurso sem coordenação, condições de corrida são possíveis. tooprevent isso, oferece uma pesquisa do Azure uma *modelo de simultaneidade otimista*. Não há nenhum bloqueio em um recurso. Em vez disso, há uma ETag para todos os recursos que identifica a versão do recurso Olá para que você pode criar solicitações evitar acidental substitui.

> [!Tip]
> Código conceitual em uma [solução C# de exemplo](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) explica como funciona o controle de simultaneidade no Azure Search. código de saudação cria condições que invocar o controle de simultaneidade. Saudação de leitura [fragmento de código a seguir](#samplecode) provavelmente será suficiente para a maioria dos desenvolvedores, mas se você quiser toorun, editar o nome do serviço de saudação appSettings. JSON tooadd e uma chave de api de administração. Dado um URL de serviço de `http://myservice.search.windows.net`, nome do serviço Olá é `myservice`.

## <a name="how-it-works"></a>Como ele funciona

Otimista de simultaneidade é implementada por meio do acesso condição verifica nas chamadas à API escrever tooindexes, indexadores, fontes de dados e recursos de synonymMap. 

Todos os recursos tiverem uma [ *marca da entidade (ETag)* ](https://en.wikipedia.org/wiki/HTTP_ETag) que fornece informações de versão do objeto. Verificando Olá ETag pela primeira vez, você pode evitar atualizações simultâneas em um fluxo de trabalho típico (get, modificar localmente e atualizar), garantindo correspondências de ETag do recurso Olá sua cópia local. 

+ Olá REST API usa uma [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) no cabeçalho da solicitação hello.
+ Olá SDK .NET define Olá ETag por meio de um objeto accessCondition, definindo Olá [If-Match | Cabeçalho If-Match-nenhum](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) no recurso de saudação. Qualquer objeto que herda de [IResourceWithETag (SDK do .NET)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) possui um objeto accessCondition.

Sempre que você atualizar um recurso, a ETag é alterada automaticamente. Quando você implementa o gerenciamento de simultaneidade, tudo o que você está fazendo é colocar uma pré-condição na solicitação de atualização de saudação que requer o recurso remoto Olá toohave Olá ETag mesmo como cópia de saudação do recurso Olá modificado no cliente de saudação. Se um processo simultâneo foi alterado recurso remoto Olá já, Olá ETag não corresponderá a pré-condição hello e Olá solicitação falha com HTTP 412. Se você estiver usando o SDK .NET de hello, isso se manifesta como uma `CloudException` onde Olá `IsAccessConditionFailed()` método de extensão retorna true.

> [!Note]
> Há apenas um mecanismo para simultaneidade. Ele sempre é usado, independentemente de qual API é usada para atualizações de recursos. 

<a name="samplecode"></a>
## <a name="use-cases-and-sample-code"></a>Casos de uso e código de exemplo

saudação de código a seguir demonstra accessCondition verifica para operações de atualização da chave:

+ Falha de uma atualização se Olá recurso não existe mais
+ Falha de uma atualização se altera de versão do recurso de saudação

### <a name="sample-code-from-dotnetetagsexplainer-programhttpsgithubcomazure-samplessearch-dotnet-getting-startedtreemasterdotnetetagsexplainer"></a>Código de exemplo do [programa DotNetETagsExplainer](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)

```
    class Program
    {
        // This sample shows how ETags work by performing conditional updates and deletes
        // on an Azure Search index.
        static void Main(string[] args)
        {
            IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
            IConfigurationRoot configuration = builder.Build();

            SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

            Console.WriteLine("Deleting index...\n");
            DeleteTestIndexIfExists(serviceClient);

            // Every top-level resource in Azure Search has an associated ETag that keeps track of which version
            // of hello resource you're working on. When you first create a resource such as an index, its ETag is
            // empty.
            Index index = DefineTestIndex();
            Console.WriteLine(
                $"Test index hasn't been created yet, so its ETag should be blank. ETag: '{index.ETag}'");

            // Once hello resource exists in Azure Search, its ETag will be populated. Make sure toouse hello object
            // returned by hello SearchServiceClient! Otherwise, you will still have hello old object with the
            // blank ETag.
            Console.WriteLine("Creating index...\n");
            index = serviceClient.Indexes.Create(index);
            
            Console.WriteLine($"Test index created; Its ETag should be populated. ETag: '{index.ETag}'");

            // ETags let you do some useful things you couldn't do otherwise. For example, by using an If-Match
            // condition, we can update an index using CreateOrUpdate and be guaranteed that hello update will only
            // succeed if hello index already exists.
            index.Fields.Add(new Field("name", AnalyzerName.EnMicrosoft));
            index =
                serviceClient.Indexes.CreateOrUpdate(
                    index,
                    accessCondition: AccessCondition.GenerateIfExistsCondition());

            Console.WriteLine(
                $"Test index updated; Its ETag should have changed since it was created. ETag: '{index.ETag}'");

            // More importantly, ETags protect you from concurrent updates toohello same resource. If another
            // client tries tooupdate hello resource, it will fail as long as all clients are using hello right
            // access conditions.
            Index indexForClient1 = index;
            Index indexForClient2 = serviceClient.Indexes.Get("test");

            Console.WriteLine("Simulating concurrent update. toostart, both clients see hello same ETag.");
            Console.WriteLine($"Client 1 ETag: '{indexForClient1.ETag}' Client 2 ETag: '{indexForClient2.ETag}'");

            // Client 1 successfully updates hello index.
            indexForClient1.Fields.Add(new Field("a", DataType.Int32));
            indexForClient1 =
                serviceClient.Indexes.CreateOrUpdate(
                    indexForClient1,
                    accessCondition: AccessCondition.IfNotChanged(indexForClient1));

            Console.WriteLine($"Test index updated by client 1; ETag: '{indexForClient1.ETag}'");

            // Client 2 tries tooupdate hello index, but fails, thanks toohello ETag check.
            try
            {
                indexForClient2.Fields.Add(new Field("b", DataType.Boolean));
                serviceClient.Indexes.CreateOrUpdate(
                    indexForClient2, 
                    accessCondition: AccessCondition.IfNotChanged(indexForClient2));

                Console.WriteLine("Whoops; This shouldn't happen");
                Environment.Exit(1);
            }
            catch (CloudException e) when (e.IsAccessConditionFailed())
            {
                Console.WriteLine("Client 2 failed tooupdate hello index, as expected.");
            }

            // You can also use access conditions with Delete operations. For example, you can implement an
            // atomic version of hello DeleteTestIndexIfExists method from this sample like this:
            Console.WriteLine("Deleting index...\n");
            serviceClient.Indexes.Delete("test", accessCondition: AccessCondition.GenerateIfExistsCondition());

            // This is slightly better than using hello Exists method since it makes only one round trip to
            // Azure Search instead of potentially two. It also avoids an extra Delete request in cases where
            // hello resource is deleted concurrently, but this doesn't matter much since resource deletion in
            // Azure Search is idempotent.

            // And we're done! Bye!
            Console.WriteLine("Complete.  Press any key tooend application...\n");
            Console.ReadKey();
        }

        private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
        {
            string searchServiceName = configuration["SearchServiceName"];
            string adminApiKey = configuration["SearchServiceAdminApiKey"];

            SearchServiceClient serviceClient =
                new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
            return serviceClient;
        }

        private static void DeleteTestIndexIfExists(SearchServiceClient serviceClient)
        {
            if (serviceClient.Indexes.Exists("test"))
            {
                serviceClient.Indexes.Delete("test");
            }
        }

        private static Index DefineTestIndex() =>
            new Index()
            {
                Name = "test",
                Fields = new[] { new Field("id", DataType.String) { IsKey = true } }
            };
    }
}
```

## <a name="design-pattern"></a>Padrão de design

Um padrão de design para implementar a simultaneidade otimista deve incluir um loop que repete a verificação de condição de acesso hello, um teste para a condição de acesso Olá e, opcionalmente, recupera um recurso atualizado antes de tentar toore-aplicar alterações de saudação. 

Este trecho de código ilustra a adição de saudação de um índice de tooan synonymMap que já existe. Esse código é do hello [tutorial c# sinônimo (visualização) para pesquisa do Azure](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk). 

trecho de saudação obtém hotéis"hello" índice, verifica a versão do objeto Olá em uma operação de atualização, lança uma exceção se a condição Olá falhar e, em seguida, repetições Olá operação (backup toothree vezes), iniciando com a recuperação de índice de saudação do hello servidor tooget mais recente Versão.

        private static void EnableSynonymsInHotelsIndexSafely(SearchServiceClient serviceClient)
        {
            int MaxNumTries = 3;

            for (int i = 0; i < MaxNumTries; ++i)
            {
                try
                {
                    Index index = serviceClient.Indexes.Get("hotels");
                    index = AddSynonymMapsToFields(index);

                    // hello IfNotChanged condition ensures that hello index is updated only if hello ETags match.
                    serviceClient.Indexes.CreateOrUpdate(index, accessCondition: AccessCondition.IfNotChanged(index));

                    Console.WriteLine("Updated hello index successfully.\n");
                    break;
                }
                catch (CloudException e) when (e.IsAccessConditionFailed())
                {
                    Console.WriteLine($"Index update failed : {e.Message}. Attempt({i}/{MaxNumTries}).\n");
                }
            }
        }
        
        private static Index AddSynonymMapsToFields(Index index)
        {
            index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
            index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };
            return index;
        }


## <a name="next-steps"></a>Próximas etapas

Saudação de revisão [exemplo sinônimos c#](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) para obter mais contexto sobre como atualizar um índice existente, toosafely.

Tente modificar qualquer uma das seguintes Olá exemplos tooinclude ETags ou AccessCondition objetos.

+ [exemplo de REST API no GitHub](https://github.com/Azure-Samples/search-rest-api-getting-started) 
+ [exemplo do SDK do .NET no GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started). Essa solução inclui o projeto de "DotNetEtagsExplainer" hello contendo código Olá apresentado neste artigo.

## <a name="see-also"></a>Consulte também

  [Cabeçalhos de resposta e solicitação HTTP comuns](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)    
  [Códigos de status HTTP](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [operações de índice (REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)