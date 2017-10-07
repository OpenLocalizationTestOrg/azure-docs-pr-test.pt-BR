---
title: aaaHow tooUse Cache Redis do Azure | Microsoft Docs
description: "Saiba como tooimprove Olá desempenho dos aplicativos do Azure com o Cache Redis do Azure"
services: redis-cache,app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: c502f74c-44de-4087-8303-1b1f43da12d5
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/27/2017
ms.author: sdanie
ms.openlocfilehash: 763d70c10972eec9a1885969e8da5bf1c4084727
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache"></a>Como tooUse Cache Redis do Azure
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Este guia mostra como tooget iniciado usando **Cache Redis do Azure**. Cache Redis do Microsoft Azure baseia-se em Olá populares de software livre Cache Redis. Isso lhe dá acesso tooa seguro e dedicado cache Redis, gerenciado pela Microsoft. Um cache criado usando o cache Redis do Azure é acessível de qualquer aplicativo do Microsoft Azure.

Cache Redis do Microsoft Azure está disponível em Olá níveis a seguir:

* **Básico** – um único nó. Vários tamanhos de backup too53 GB.
* **Standard** – principal/réplica com dois nós. Vários tamanhos de backup too53 GB. SLA de 99,9%.
* **Premium** – dois nós primário/réplica, com backup too10 fragmentos. Vários tamanhos de 6 GB too530 GB. Todos os recursos do tipo Standard e outros, incluindo suporte para [cluster Redis](cache-how-to-premium-clustering.md), [persistência Redis](cache-how-to-premium-persistence.md) e [Rede Virtual do Azure](cache-how-to-premium-vnet.md). SLA de 99,9%.

Cada camada é diferente em termos de recursos e preços. Para saber mais sobre preços, consulte [Detalhes de preços do cache][Cache Pricing Details].

Este guia mostra como Olá toouse [Stackexchange] [ StackExchange.Redis] cliente usando C\# código. Olá cenários abordados incluem **criar e configurar um cache**, **como configurar clientes de cache**, e **adicionando e removendo objetos do cache de saudação**. Para obter mais informações sobre como usar o Cache Redis do Azure, consulte [Próximas etapas][Next Steps]. Para obter um tutorial passo a passo de compilação um ASP.NET MVC de aplicativo web com o Cache Redis, consulte [como toocreate um aplicativo Web com o Cache Redis](cache-web-app-howto.md).

<a name="getting-started-cache-service"></a>

## <a name="get-started-with-azure-redis-cache"></a>Introdução ao Cache Redis do Azure
Começar a usar o cache Redis do Azure é fácil. tooget iniciado, você provisionar e configurar um cache. Em seguida, configure clientes de cache Olá para que possam acessar o cache de saudação. Quando os clientes de cache de saudação são configurados, você pode começar a trabalhar com eles.

* [Criar cache Olá][Create hello cache]
* [Configurar clientes de cache Olá][Configure hello cache clients]

<a name="create-cache"></a>

## <a name="create-a-cache"></a>Criar um cache
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

### <a name="tooaccess-your-cache-after-its-created"></a>tooaccess seu cache depois que ele é criado
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

Para obter mais informações sobre como configurar seu cache, consulte [como tooconfigure Cache Redis do Azure](cache-configure.md).

<a name="NuGet"></a>

## <a name="configure-hello-cache-clients"></a>Configurar clientes de cache Olá
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

Quando o projeto de cliente está configurado para armazenar em cache, você pode usar técnicas de saudação descritas nas seguintes seções para trabalhar com o cache de saudação.

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a>Trabalhando com caches
Olá etapas desta seção descrevem como as tarefas comuns de tooperform com o Cache.

* [Conecte-se o cache de toohello][Connect toohello cache]
* [Adicionar e recuperar objetos do cache de saudação][Add and retrieve objects from hello cache]
* [Trabalhar com objetos .NET no cache de saudação](#work-with-net-objects-in-the-cache)

<a name="connect-to-cache"></a>

## <a name="connect-toohello-cache"></a>Conecte-se o cache de toohello
trabalho de tooprogrammatically com um cache, você precisa de um cache de toohello de referência. Adicione Olá toohello superior de qualquer arquivo do qual você deseja toouse Olá Stackexchange cliente tooaccess um Cache Redis do Azure a seguir.

    using StackExchange.Redis;

> [!NOTE]
> cliente de Stackexchange Olá requer o .NET Framework 4 ou superior.
> 
> 

Olá toohello conexão Cache Redis do Azure é gerenciado pelo Olá `ConnectionMultiplexer` classe. Essa classe deve ser compartilhada e reutilizados em todo o seu aplicativo cliente e não precisa toobe criado em uma base por operação. 

tooconnect tooan Cache Redis do Azure e retornar uma instância de um conectado `ConnectionMultiplexer`, chamada hello estático `Connect` método e passar Olá cache ponto de extremidade e a chave. Use chave Olá gerado a partir de saudação portal do Azure como parâmetro de senha hello.

    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");

> [!IMPORTANT]
> Aviso: nunca armazene credenciais no código-fonte. tookeep esse exemplo simples, estou mostrando-los no código-fonte hello. Consulte [como cadeias de caracteres de aplicativo e o trabalho de cadeias de caracteres de Conexão] [ How Application Strings and Connection Strings Work] para obter informações sobre como toostore credenciais.
> 
> 

Se você não quiser toouse SSL, definir `ssl=false` ou omita Olá `ssl` parâmetro.

> [!NOTE]
> porta do Hello não SSL está desabilitada por padrão para novos caches. Para obter instruções sobre como habilitar a porta não SSL de hello, consulte [portas de acesso](cache-configure.md#access-ports).
> 
> 

Uma abordagem toosharing um `ConnectionMultiplexer` instância em seu aplicativo é toohave uma propriedade estática que retorna uma instância conectada, semelhante toohello exemplo a seguir. Essa abordagem fornece uma forma thread-safe tooinitialize apenas um único conectado `ConnectionMultiplexer` instância. Nestes exemplos `abortConnect` é toofalse de conjunto, o que significa que a chamada de saudação é bem-sucedida mesmo se não for estabelecida uma conexão toohello Cache Redis do Azure. Um recurso importante do `ConnectionMultiplexer` é que ele automaticamente restaura cache de toohello conectividade depois que o problema de rede hello ou outras causas são resolvidas.

    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
    });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

Para obter mais informações nas opções de configuração de conexão avançada, consulte [Modelo de configuração de StackExchange.Redis][StackExchange.Redis configuration model].

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

Após o estabelecimento de conexão hello, retornar um banco de dados referência toohello redis cache por chamada hello `ConnectionMultiplexer.GetDatabase` método. objeto Olá retornado de saudação `GetDatabase` método é um objeto de passagem leve e não precisa toobe armazenado.

    // Connection refers tooa property that returns a ConnectionMultiplexer
    // as shown in hello previous example.
    IDatabase cache = Connection.GetDatabase();

    // Perform cache operations using hello cache object...
    // Simple put of integral data types into hello cache
    cache.StringSet("key1", "value");
    cache.StringSet("key2", 25);

    // Simple get of data types from hello cache
    string key1 = cache.StringGet("key1");
    int key2 = (int)cache.StringGet("key2");

Caches Redis do Azure tem um número configurável de bancos de dados (padrão de 16) que podem ser usados toologically Olá separada dados dentro de um cache Redis. Para saber mais, veja [O que são os bancos de dados do Redis?](cache-faq.md#what-are-redis-databases) e [Configuração padrão do servidor Redis](cache-configure.md#default-redis-server-configuration).

Agora que você sabe como instância de Cache Redis do Azure tooan tooconnect e retornar uma referência toohello cache de banco de dados, vamos dar uma olhada em trabalhar com o cache de saudação.

<a name="add-object"></a>

## <a name="add-and-retrieve-objects-from-hello-cache"></a>Adicionar e recuperar objetos do cache de saudação
Itens podem ser armazenados em e recuperados de um cache usando Olá `StringSet` e `StringGet` métodos.

    // If key1 exists, it is overwritten.
    cache.StringSet("key1", "value1");

    string value = cache.StringGet("key1");

Armazena a maioria dos dados como cadeias de caracteres do Redis, mas essas cadeias de caracteres pode conter muitos tipos de dados, incluindo dados binários serializados, que podem ser usados ao armazenar .NET de objetos no cache de saudação o redis.

Ao chamar `StringGet`, se o objeto de saudação existir, ele é retornado, e se não estiver, `null` será retornado. Se `null` for retornado, você pode recuperar o valor de Olá Olá desejado da fonte de dados e armazená-la no cache de saudação para uso posterior. Esse padrão de uso é conhecido como padrão de cache-aside hello.

    string value = cache.StringGet("key1");
    if (value == null)
    {
        // hello item keyed by "key1" is not in hello cache. Obtain
        // it from hello desired data source and add it toohello cache.
        value = GetValueFromDataSource();

        cache.StringSet("key1", value);
    }

Você também pode usar `RedisValue`, conforme mostrado no exemplo a seguir de saudação. O `RedisValue` tem operadores implícitos para trabalhar com tipos de dados integrais e pode ser útil se `null` for um valor esperado para um item em cache.


    RedisValue value = cache.StringGet("key1");
    if (!value.HasValue)
    {
        value = GetValueFromDataSource();
        cache.StringSet("key1", value);
    }


expiração de saudação toospecify de um item no cache de hello, use Olá `TimeSpan` parâmetro `StringSet`.

    cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));

## <a name="work-with-net-objects-in-hello-cache"></a>Trabalhar com objetos .NET no cache de saudação
O Cache Redis do Azure pode armazenar objetos .NET e tipos de dados primitivos em cache, mas antes que um objeto .NET seja armazenado em cache, ele deve ser serializado. Essa serialização de objeto do .NET é responsabilidade de saudação do desenvolvedor do aplicativo hello e flexibilidade de desenvolvedor Olá na escolha de saudação do serializador de saudação.

Objetos de um tooserialize de maneira simples é hello toouse `JsonConvert` métodos de serialização em [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) e serializar tooand do JSON. Olá exemplo a seguir mostra um get e set usando um `Employee` a instância do objeto.

    class Employee
    {
        public int Id { get; set; }
        public string Name { get; set; }

        public Employee(int EmployeeId, string Name)
        {
            this.Id = EmployeeId;
            this.Name = Name;
        }
    }

    // Store toocache
    cache.StringSet("e25", JsonConvert.SerializeObject(new Employee(25, "Clayton Gragg")));

    // Retrieve from cache
    Employee e25 = JsonConvert.DeserializeObject<Employee>(cache.StringGet("e25"));

<a name="next-steps"></a>

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas de hello, siga essas toolearn links mais informações sobre o Cache Redis do Azure.

* Check-out Olá provedores ASP.NET para Cache Redis do Azure.
  * [Provedor de estado de sessão do Redis do Azure](cache-aspnet-session-state-provider.md)
  * [Provedor de Cache de Saída ASP.NET do Cache Redis do Azure](cache-aspnet-output-cache-provider.md)
* [Habilitar o diagnóstico de cache](cache-how-to-monitor.md#enable-cache-diagnostics) para que você possa [monitor](cache-how-to-monitor.md) Olá a integridade do cache. Você pode exibir uma saudação métricas em hello portal do Azure e você também podem [Baixe e leia](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) -los usando as ferramentas de saudação de sua escolha.
* Check-out Olá [documentação do cliente de cache Stackexchange][StackExchange.Redis cache client documentation].
  * O Cache Redis do Azure pode ser acessado por meio de muitos clientes Redis e linguagens de desenvolvimento. Para obter mais informações, veja [http://redis.io/clients][http://redis.io/clients].
* O Cache Redis do Azure também pode ser usado com ferramentas como Redsmin e Redis Desktop Manager.
  * Para obter mais informações sobre Redsmin, consulte [como tooretrieve uma conexão Redis do Azure de cadeia de caracteres e usá-lo com Redsmin][How tooretrieve an Azure Redis connection string and use it with Redsmin].
  * Acesse e inspecione seus dados no Cache Redis do Azure com uma interface gráfica do usuário usando [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).
* Consulte Olá [redis] [ redis] documentação e leia sobre [redis tipos de dados] [ redis data types] e [uma introdução de quinze minutos tipos de dados tooRedis][a fifteen minute introduction tooRedis data types].

<!-- INTRA-TOPIC LINKS -->
[Next Steps]: #next-steps
[Introduction tooAzure Redis Cache (Video)]: #video
[What is Azure Redis Cache?]: #what-is
[Create an Azure Cache]: #create-cache
[Which type of caching is right for me?]: #choosing-cache
[Prepare Your Visual Studio Project tooUse Azure Caching]: #prepare-vs
[Configure Your Application tooUse Caching]: #configure-app
[Get Started with Azure Redis Cache]: #getting-started-cache-service
[Create hello cache]: #create-cache
[Configure hello cache]: #enable-caching
[Configure hello cache clients]: #NuGet
[Working with Caches]: #working-with-caches
[Connect toohello cache]: #connect-to-cache
[Add and retrieve objects from hello cache]: #add-object
[Specify hello expiration of an object in hello cache]: #specify-expiration
[Store ASP.NET session state in hello cache]: #store-session


<!-- IMAGES -->


[StackExchangeNuget]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-stackexchange-redis.png

[NuGetMenu]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-manage-nuget-menu.png

[CacheProperties]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-properties.png

[ManageKeys]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-manage-keys.png

[SessionStateNuGet]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-session-state-provider.png

[BrowseCaches]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-browse-caches.png

[Caches]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-caches.png







<!-- LINKS -->
[http://redis.io/clients]: http://redis.io/clients
[Develop in other languages for Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn690470.aspx
[How tooretrieve an Azure Redis connection string and use it with Redsmin]: https://redsmin.uservoice.com/knowledgebase/articles/485711-how-to-connect-redsmin-to-azure-redis-cache
[Azure Redis Session State Provider]: http://go.microsoft.com/fwlink/?LinkId=398249
[How to: Configure a Cache Client Programmatically]: http://msdn.microsoft.com/library/windowsazure/gg618003.aspx
[Session State Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320835
[Azure AppFabric Cache: Caching Session State]: http://www.microsoft.com/showcase/details.aspx?uuid=87c833e9-97a9-42b2-8bb1-7601f9b5ca20
[Output Cache Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320837
[Azure Shared Caching]: http://msdn.microsoft.com/library/windowsazure/gg278356.aspx
[Team Blog]: http://blogs.msdn.com/b/windowsazure/
[Azure Caching]: http://www.microsoft.com/showcase/Search.aspx?phrase=azure+caching
[How tooConfigure Virtual Machine Sizes]: http://go.microsoft.com/fwlink/?LinkId=164387
[Azure Caching Capacity Planning Considerations]: http://go.microsoft.com/fwlink/?LinkId=320167
[Azure Caching]: http://go.microsoft.com/fwlink/?LinkId=252658
[How to: Set hello Cacheability of an ASP.NET Page Declaratively]: http://msdn.microsoft.com/library/zd1ysf1y.aspx
[How to: Set a Page's Cacheability Programmatically]: http://msdn.microsoft.com/library/z852zf6b.aspx
[Configure a cache in Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn793612.aspx

[StackExchange.Redis configuration model]: https://stackexchange.github.io/StackExchange.Redis/Configuration

[Work with .NET objects in hello cache]: http://msdn.microsoft.com/library/dn690521.aspx#Objects


[NuGet Package Manager Installation]: http://go.microsoft.com/fwlink/?LinkId=240311
[Cache Pricing Details]: http://www.windowsazure.com/pricing/details/cache/
[Azure portal]: https://portal.azure.com/

[Overview of Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=320830
[Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=398247

[Migrate tooAzure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=317347
[Azure Redis Cache Samples]: http://go.microsoft.com/fwlink/?LinkId=320840
[Using Resource groups toomanage your Azure resources]: ../azure-resource-manager/resource-group-overview.md

[StackExchange.Redis]: http://github.com/StackExchange/StackExchange.Redis
[StackExchange.Redis cache client documentation]: http://github.com/StackExchange/StackExchange.Redis#documentation

[Redis]: http://redis.io/documentation
[Redis data types]: http://redis.io/topics/data-types
[a fifteen minute introduction tooRedis data types]: http://redis.io/topics/data-types-intro

[How Application Strings and Connection Strings Work]: http://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/


