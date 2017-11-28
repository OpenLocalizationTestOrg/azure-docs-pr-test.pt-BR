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
# <a name="how-toouse-azure-redis-cache"></a><span data-ttu-id="33e6b-103">Como tooUse Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="33e6b-103">How tooUse Azure Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="33e6b-104">.NET</span><span class="sxs-lookup"><span data-stu-id="33e6b-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="33e6b-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="33e6b-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="33e6b-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="33e6b-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="33e6b-107">Java</span><span class="sxs-lookup"><span data-stu-id="33e6b-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="33e6b-108">Python</span><span class="sxs-lookup"><span data-stu-id="33e6b-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="33e6b-109">Este guia mostra como tooget iniciado usando **Cache Redis do Azure**.</span><span class="sxs-lookup"><span data-stu-id="33e6b-109">This guide shows you how tooget started using **Azure Redis Cache**.</span></span> <span data-ttu-id="33e6b-110">Cache Redis do Microsoft Azure baseia-se em Olá populares de software livre Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="33e6b-110">Microsoft Azure Redis Cache is based on hello popular open source Redis Cache.</span></span> <span data-ttu-id="33e6b-111">Isso lhe dá acesso tooa seguro e dedicado cache Redis, gerenciado pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="33e6b-111">It gives you access tooa secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="33e6b-112">Um cache criado usando o cache Redis do Azure é acessível de qualquer aplicativo do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="33e6b-112">A cache created using Azure Redis Cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="33e6b-113">Cache Redis do Microsoft Azure está disponível em Olá níveis a seguir:</span><span class="sxs-lookup"><span data-stu-id="33e6b-113">Microsoft Azure Redis Cache is available in hello following tiers:</span></span>

* <span data-ttu-id="33e6b-114">**Básico** – um único nó.</span><span class="sxs-lookup"><span data-stu-id="33e6b-114">**Basic** – Single node.</span></span> <span data-ttu-id="33e6b-115">Vários tamanhos de backup too53 GB.</span><span class="sxs-lookup"><span data-stu-id="33e6b-115">Multiple sizes up too53 GB.</span></span>
* <span data-ttu-id="33e6b-116">**Standard** – principal/réplica com dois nós.</span><span class="sxs-lookup"><span data-stu-id="33e6b-116">**Standard** – Two-node Primary/Replica.</span></span> <span data-ttu-id="33e6b-117">Vários tamanhos de backup too53 GB.</span><span class="sxs-lookup"><span data-stu-id="33e6b-117">Multiple sizes up too53 GB.</span></span> <span data-ttu-id="33e6b-118">SLA de 99,9%.</span><span class="sxs-lookup"><span data-stu-id="33e6b-118">99.9% SLA.</span></span>
* <span data-ttu-id="33e6b-119">**Premium** – dois nós primário/réplica, com backup too10 fragmentos.</span><span class="sxs-lookup"><span data-stu-id="33e6b-119">**Premium** – Two-node Primary/Replica with up too10 shards.</span></span> <span data-ttu-id="33e6b-120">Vários tamanhos de 6 GB too530 GB.</span><span class="sxs-lookup"><span data-stu-id="33e6b-120">Multiple sizes from 6 GB too530 GB.</span></span> <span data-ttu-id="33e6b-121">Todos os recursos do tipo Standard e outros, incluindo suporte para [cluster Redis](cache-how-to-premium-clustering.md), [persistência Redis](cache-how-to-premium-persistence.md) e [Rede Virtual do Azure](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="33e6b-121">All Standard tier features and more including support for [Redis cluster](cache-how-to-premium-clustering.md), [Redis persistence](cache-how-to-premium-persistence.md), and [Azure Virtual Network](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="33e6b-122">SLA de 99,9%.</span><span class="sxs-lookup"><span data-stu-id="33e6b-122">99.9% SLA.</span></span>

<span data-ttu-id="33e6b-123">Cada camada é diferente em termos de recursos e preços.</span><span class="sxs-lookup"><span data-stu-id="33e6b-123">Each tier differs in terms of features and pricing.</span></span> <span data-ttu-id="33e6b-124">Para saber mais sobre preços, consulte [Detalhes de preços do cache][Cache Pricing Details].</span><span class="sxs-lookup"><span data-stu-id="33e6b-124">For information on pricing, see [Cache Pricing Details][Cache Pricing Details].</span></span>

<span data-ttu-id="33e6b-125">Este guia mostra como Olá toouse [Stackexchange] [ StackExchange.Redis] cliente usando C\# código.</span><span class="sxs-lookup"><span data-stu-id="33e6b-125">This guide shows you how toouse hello [StackExchange.Redis][StackExchange.Redis] client using C\# code.</span></span> <span data-ttu-id="33e6b-126">Olá cenários abordados incluem **criar e configurar um cache**, **como configurar clientes de cache**, e **adicionando e removendo objetos do cache de saudação**.</span><span class="sxs-lookup"><span data-stu-id="33e6b-126">hello scenarios covered include **creating and configuring a cache**, **configuring cache clients**, and **adding and removing objects from hello cache**.</span></span> <span data-ttu-id="33e6b-127">Para obter mais informações sobre como usar o Cache Redis do Azure, consulte [Próximas etapas][Next Steps].</span><span class="sxs-lookup"><span data-stu-id="33e6b-127">For more information on using Azure Redis Cache, see [Next Steps][Next Steps].</span></span> <span data-ttu-id="33e6b-128">Para obter um tutorial passo a passo de compilação um ASP.NET MVC de aplicativo web com o Cache Redis, consulte [como toocreate um aplicativo Web com o Cache Redis](cache-web-app-howto.md).</span><span class="sxs-lookup"><span data-stu-id="33e6b-128">For a step-by-step tutorial of building an ASP.NET MVC web app with Redis Cache, see [How toocreate a Web App with Redis Cache](cache-web-app-howto.md).</span></span>

<a name="getting-started-cache-service"></a>

## <a name="get-started-with-azure-redis-cache"></a><span data-ttu-id="33e6b-129">Introdução ao Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="33e6b-129">Get Started with Azure Redis Cache</span></span>
<span data-ttu-id="33e6b-130">Começar a usar o cache Redis do Azure é fácil.</span><span class="sxs-lookup"><span data-stu-id="33e6b-130">Getting started with Azure Redis Cache is easy.</span></span> <span data-ttu-id="33e6b-131">tooget iniciado, você provisionar e configurar um cache.</span><span class="sxs-lookup"><span data-stu-id="33e6b-131">tooget started, you provision and configure a cache.</span></span> <span data-ttu-id="33e6b-132">Em seguida, configure clientes de cache Olá para que possam acessar o cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="33e6b-132">Next, you configure hello cache clients so they can access hello cache.</span></span> <span data-ttu-id="33e6b-133">Quando os clientes de cache de saudação são configurados, você pode começar a trabalhar com eles.</span><span class="sxs-lookup"><span data-stu-id="33e6b-133">Once hello cache clients are configured, you can begin working with them.</span></span>

* <span data-ttu-id="33e6b-134">[Criar cache Olá][Create hello cache]</span><span class="sxs-lookup"><span data-stu-id="33e6b-134">[Create hello cache][Create hello cache]</span></span>
* <span data-ttu-id="33e6b-135">[Configurar clientes de cache Olá][Configure hello cache clients]</span><span class="sxs-lookup"><span data-stu-id="33e6b-135">[Configure hello cache clients][Configure hello cache clients]</span></span>

<a name="create-cache"></a>

## <a name="create-a-cache"></a><span data-ttu-id="33e6b-136">Criar um cache</span><span class="sxs-lookup"><span data-stu-id="33e6b-136">Create a cache</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

### <a name="tooaccess-your-cache-after-its-created"></a><span data-ttu-id="33e6b-137">tooaccess seu cache depois que ele é criado</span><span class="sxs-lookup"><span data-stu-id="33e6b-137">tooaccess your cache after it's created</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="33e6b-138">Para obter mais informações sobre como configurar seu cache, consulte [como tooconfigure Cache Redis do Azure](cache-configure.md).</span><span class="sxs-lookup"><span data-stu-id="33e6b-138">For more information about configuring your cache, see [How tooconfigure Azure Redis Cache](cache-configure.md).</span></span>

<a name="NuGet"></a>

## <a name="configure-hello-cache-clients"></a><span data-ttu-id="33e6b-139">Configurar clientes de cache Olá</span><span class="sxs-lookup"><span data-stu-id="33e6b-139">Configure hello cache clients</span></span>
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

<span data-ttu-id="33e6b-140">Quando o projeto de cliente está configurado para armazenar em cache, você pode usar técnicas de saudação descritas nas seguintes seções para trabalhar com o cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="33e6b-140">Once your client project is configured for caching, you can use hello techniques described in hello following sections for working with your cache.</span></span>

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a><span data-ttu-id="33e6b-141">Trabalhando com caches</span><span class="sxs-lookup"><span data-stu-id="33e6b-141">Working with Caches</span></span>
<span data-ttu-id="33e6b-142">Olá etapas desta seção descrevem como as tarefas comuns de tooperform com o Cache.</span><span class="sxs-lookup"><span data-stu-id="33e6b-142">hello steps in this section describe how tooperform common tasks with Cache.</span></span>

* <span data-ttu-id="33e6b-143">[Conecte-se o cache de toohello][Connect toohello cache]</span><span class="sxs-lookup"><span data-stu-id="33e6b-143">[Connect toohello cache][Connect toohello cache]</span></span>
* <span data-ttu-id="33e6b-144">[Adicionar e recuperar objetos do cache de saudação][Add and retrieve objects from hello cache]</span><span class="sxs-lookup"><span data-stu-id="33e6b-144">[Add and retrieve objects from hello cache][Add and retrieve objects from hello cache]</span></span>
* [<span data-ttu-id="33e6b-145">Trabalhar com objetos .NET no cache de saudação</span><span class="sxs-lookup"><span data-stu-id="33e6b-145">Work with .NET objects in hello cache</span></span>](#work-with-net-objects-in-the-cache)

<a name="connect-to-cache"></a>

## <a name="connect-toohello-cache"></a><span data-ttu-id="33e6b-146">Conecte-se o cache de toohello</span><span class="sxs-lookup"><span data-stu-id="33e6b-146">Connect toohello cache</span></span>
<span data-ttu-id="33e6b-147">trabalho de tooprogrammatically com um cache, você precisa de um cache de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="33e6b-147">tooprogrammatically work with a cache, you need a reference toohello cache.</span></span> <span data-ttu-id="33e6b-148">Adicione Olá toohello superior de qualquer arquivo do qual você deseja toouse Olá Stackexchange cliente tooaccess um Cache Redis do Azure a seguir.</span><span class="sxs-lookup"><span data-stu-id="33e6b-148">Add hello following toohello top of any file from which you want toouse hello StackExchange.Redis client tooaccess an Azure Redis Cache.</span></span>

    using StackExchange.Redis;

> [!NOTE]
> <span data-ttu-id="33e6b-149">cliente de Stackexchange Olá requer o .NET Framework 4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="33e6b-149">hello StackExchange.Redis client requires .NET Framework 4 or higher.</span></span>
> 
> 

<span data-ttu-id="33e6b-150">Olá toohello conexão Cache Redis do Azure é gerenciado pelo Olá `ConnectionMultiplexer` classe.</span><span class="sxs-lookup"><span data-stu-id="33e6b-150">hello connection toohello Azure Redis Cache is managed by hello `ConnectionMultiplexer` class.</span></span> <span data-ttu-id="33e6b-151">Essa classe deve ser compartilhada e reutilizados em todo o seu aplicativo cliente e não precisa toobe criado em uma base por operação.</span><span class="sxs-lookup"><span data-stu-id="33e6b-151">This class should be shared and reused throughout your client application, and does not need toobe created on a per operation basis.</span></span> 

<span data-ttu-id="33e6b-152">tooconnect tooan Cache Redis do Azure e retornar uma instância de um conectado `ConnectionMultiplexer`, chamada hello estático `Connect` método e passar Olá cache ponto de extremidade e a chave.</span><span class="sxs-lookup"><span data-stu-id="33e6b-152">tooconnect tooan Azure Redis Cache and be returned an instance of a connected `ConnectionMultiplexer`, call hello static `Connect` method and pass in hello cache endpoint and key.</span></span> <span data-ttu-id="33e6b-153">Use chave Olá gerado a partir de saudação portal do Azure como parâmetro de senha hello.</span><span class="sxs-lookup"><span data-stu-id="33e6b-153">Use hello key generated from hello Azure portal as hello password parameter.</span></span>

    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");

> [!IMPORTANT]
> <span data-ttu-id="33e6b-154">Aviso: nunca armazene credenciais no código-fonte.</span><span class="sxs-lookup"><span data-stu-id="33e6b-154">Warning: Never store credentials in source code.</span></span> <span data-ttu-id="33e6b-155">tookeep esse exemplo simples, estou mostrando-los no código-fonte hello.</span><span class="sxs-lookup"><span data-stu-id="33e6b-155">tookeep this sample simple, I’m showing them in hello source code.</span></span> <span data-ttu-id="33e6b-156">Consulte [como cadeias de caracteres de aplicativo e o trabalho de cadeias de caracteres de Conexão] [ How Application Strings and Connection Strings Work] para obter informações sobre como toostore credenciais.</span><span class="sxs-lookup"><span data-stu-id="33e6b-156">See [How Application Strings and Connection Strings Work][How Application Strings and Connection Strings Work] for information on how toostore credentials.</span></span>
> 
> 

<span data-ttu-id="33e6b-157">Se você não quiser toouse SSL, definir `ssl=false` ou omita Olá `ssl` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="33e6b-157">If you don't want toouse SSL, either set `ssl=false` or omit hello `ssl` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="33e6b-158">porta do Hello não SSL está desabilitada por padrão para novos caches.</span><span class="sxs-lookup"><span data-stu-id="33e6b-158">hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="33e6b-159">Para obter instruções sobre como habilitar a porta não SSL de hello, consulte [portas de acesso](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="33e6b-159">For instructions on enabling hello non-SSL port, see [Access Ports](cache-configure.md#access-ports).</span></span>
> 
> 

<span data-ttu-id="33e6b-160">Uma abordagem toosharing um `ConnectionMultiplexer` instância em seu aplicativo é toohave uma propriedade estática que retorna uma instância conectada, semelhante toohello exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="33e6b-160">One approach toosharing a `ConnectionMultiplexer` instance in your application is toohave a static property that returns a connected instance, similar toohello following example.</span></span> <span data-ttu-id="33e6b-161">Essa abordagem fornece uma forma thread-safe tooinitialize apenas um único conectado `ConnectionMultiplexer` instância.</span><span class="sxs-lookup"><span data-stu-id="33e6b-161">This approach provides a thread-safe way tooinitialize only a single connected `ConnectionMultiplexer` instance.</span></span> <span data-ttu-id="33e6b-162">Nestes exemplos `abortConnect` é toofalse de conjunto, o que significa que a chamada de saudação é bem-sucedida mesmo se não for estabelecida uma conexão toohello Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="33e6b-162">In these examples `abortConnect` is set toofalse, which means that hello call succeeds even if a connection toohello Azure Redis Cache is not established.</span></span> <span data-ttu-id="33e6b-163">Um recurso importante do `ConnectionMultiplexer` é que ele automaticamente restaura cache de toohello conectividade depois que o problema de rede hello ou outras causas são resolvidas.</span><span class="sxs-lookup"><span data-stu-id="33e6b-163">One key feature of `ConnectionMultiplexer` is that it automatically restores connectivity toohello cache once hello network issue or other causes are resolved.</span></span>

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

<span data-ttu-id="33e6b-164">Para obter mais informações nas opções de configuração de conexão avançada, consulte [Modelo de configuração de StackExchange.Redis][StackExchange.Redis configuration model].</span><span class="sxs-lookup"><span data-stu-id="33e6b-164">For more information on advanced connection configuration options, see [StackExchange.Redis configuration model][StackExchange.Redis configuration model].</span></span>

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

<span data-ttu-id="33e6b-165">Após o estabelecimento de conexão hello, retornar um banco de dados referência toohello redis cache por chamada hello `ConnectionMultiplexer.GetDatabase` método.</span><span class="sxs-lookup"><span data-stu-id="33e6b-165">Once hello connection is established, return a reference toohello redis cache database by calling hello `ConnectionMultiplexer.GetDatabase` method.</span></span> <span data-ttu-id="33e6b-166">objeto Olá retornado de saudação `GetDatabase` método é um objeto de passagem leve e não precisa toobe armazenado.</span><span class="sxs-lookup"><span data-stu-id="33e6b-166">hello object returned from hello `GetDatabase` method is a lightweight pass-through object and does not need toobe stored.</span></span>

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

<span data-ttu-id="33e6b-167">Caches Redis do Azure tem um número configurável de bancos de dados (padrão de 16) que podem ser usados toologically Olá separada dados dentro de um cache Redis.</span><span class="sxs-lookup"><span data-stu-id="33e6b-167">Azure Redis caches have a configurable number of databases (default of 16) that can be used toologically separate hello data within a Redis cache.</span></span> <span data-ttu-id="33e6b-168">Para saber mais, veja [O que são os bancos de dados do Redis?](cache-faq.md#what-are-redis-databases) e [Configuração padrão do servidor Redis](cache-configure.md#default-redis-server-configuration).</span><span class="sxs-lookup"><span data-stu-id="33e6b-168">For more information, see [What are Redis databases?](cache-faq.md#what-are-redis-databases) and [Default Redis server configuration](cache-configure.md#default-redis-server-configuration).</span></span>

<span data-ttu-id="33e6b-169">Agora que você sabe como instância de Cache Redis do Azure tooan tooconnect e retornar uma referência toohello cache de banco de dados, vamos dar uma olhada em trabalhar com o cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="33e6b-169">Now that you know how tooconnect tooan Azure Redis Cache instance and return a reference toohello cache database, let's look at working with hello cache.</span></span>

<a name="add-object"></a>

## <a name="add-and-retrieve-objects-from-hello-cache"></a><span data-ttu-id="33e6b-170">Adicionar e recuperar objetos do cache de saudação</span><span class="sxs-lookup"><span data-stu-id="33e6b-170">Add and retrieve objects from hello cache</span></span>
<span data-ttu-id="33e6b-171">Itens podem ser armazenados em e recuperados de um cache usando Olá `StringSet` e `StringGet` métodos.</span><span class="sxs-lookup"><span data-stu-id="33e6b-171">Items can be stored in and retrieved from a cache by using hello `StringSet` and `StringGet` methods.</span></span>

    // If key1 exists, it is overwritten.
    cache.StringSet("key1", "value1");

    string value = cache.StringGet("key1");

<span data-ttu-id="33e6b-172">Armazena a maioria dos dados como cadeias de caracteres do Redis, mas essas cadeias de caracteres pode conter muitos tipos de dados, incluindo dados binários serializados, que podem ser usados ao armazenar .NET de objetos no cache de saudação o redis.</span><span class="sxs-lookup"><span data-stu-id="33e6b-172">Redis stores most data as Redis strings, but these strings can contain many types of data, including serialized binary data, which can be used when storing .NET objects in hello cache.</span></span>

<span data-ttu-id="33e6b-173">Ao chamar `StringGet`, se o objeto de saudação existir, ele é retornado, e se não estiver, `null` será retornado.</span><span class="sxs-lookup"><span data-stu-id="33e6b-173">When calling `StringGet`, if hello object exists, it is returned, and if it does not, `null` is returned.</span></span> <span data-ttu-id="33e6b-174">Se `null` for retornado, você pode recuperar o valor de Olá Olá desejado da fonte de dados e armazená-la no cache de saudação para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="33e6b-174">If `null` is returned, you can retrieve hello value from hello desired data source and store it in hello cache for subsequent use.</span></span> <span data-ttu-id="33e6b-175">Esse padrão de uso é conhecido como padrão de cache-aside hello.</span><span class="sxs-lookup"><span data-stu-id="33e6b-175">This usage pattern is known as hello cache-aside pattern.</span></span>

    string value = cache.StringGet("key1");
    if (value == null)
    {
        // hello item keyed by "key1" is not in hello cache. Obtain
        // it from hello desired data source and add it toohello cache.
        value = GetValueFromDataSource();

        cache.StringSet("key1", value);
    }

<span data-ttu-id="33e6b-176">Você também pode usar `RedisValue`, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="33e6b-176">You can also use `RedisValue`, as shown in hello following example.</span></span> <span data-ttu-id="33e6b-177">O `RedisValue` tem operadores implícitos para trabalhar com tipos de dados integrais e pode ser útil se `null` for um valor esperado para um item em cache.</span><span class="sxs-lookup"><span data-stu-id="33e6b-177">`RedisValue` has implicit operators for working with integral data types, and can be useful if `null` is an expected value for a cached item.</span></span>


    RedisValue value = cache.StringGet("key1");
    if (!value.HasValue)
    {
        value = GetValueFromDataSource();
        cache.StringSet("key1", value);
    }


<span data-ttu-id="33e6b-178">expiração de saudação toospecify de um item no cache de hello, use Olá `TimeSpan` parâmetro `StringSet`.</span><span class="sxs-lookup"><span data-stu-id="33e6b-178">toospecify hello expiration of an item in hello cache, use hello `TimeSpan` parameter of `StringSet`.</span></span>

    cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));

## <a name="work-with-net-objects-in-hello-cache"></a><span data-ttu-id="33e6b-179">Trabalhar com objetos .NET no cache de saudação</span><span class="sxs-lookup"><span data-stu-id="33e6b-179">Work with .NET objects in hello cache</span></span>
<span data-ttu-id="33e6b-180">O Cache Redis do Azure pode armazenar objetos .NET e tipos de dados primitivos em cache, mas antes que um objeto .NET seja armazenado em cache, ele deve ser serializado.</span><span class="sxs-lookup"><span data-stu-id="33e6b-180">Azure Redis Cache can cache both .NET objects and primitive data types, but before a .NET object can be cached it must be serialized.</span></span> <span data-ttu-id="33e6b-181">Essa serialização de objeto do .NET é responsabilidade de saudação do desenvolvedor do aplicativo hello e flexibilidade de desenvolvedor Olá na escolha de saudação do serializador de saudação.</span><span class="sxs-lookup"><span data-stu-id="33e6b-181">This .NET object serialization is hello responsibility of hello application developer, and gives hello developer flexibility in hello choice of hello serializer.</span></span>

<span data-ttu-id="33e6b-182">Objetos de um tooserialize de maneira simples é hello toouse `JsonConvert` métodos de serialização em [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) e serializar tooand do JSON.</span><span class="sxs-lookup"><span data-stu-id="33e6b-182">One simple way tooserialize objects is toouse hello `JsonConvert` serialization methods in [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) and serialize tooand from JSON.</span></span> <span data-ttu-id="33e6b-183">Olá exemplo a seguir mostra um get e set usando um `Employee` a instância do objeto.</span><span class="sxs-lookup"><span data-stu-id="33e6b-183">hello following example shows a get and set using an `Employee` object instance.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="33e6b-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="33e6b-184">Next Steps</span></span>
<span data-ttu-id="33e6b-185">Agora que você aprendeu as Noções básicas de hello, siga essas toolearn links mais informações sobre o Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="33e6b-185">Now that you've learned hello basics, follow these links toolearn more about Azure Redis Cache.</span></span>

* <span data-ttu-id="33e6b-186">Check-out Olá provedores ASP.NET para Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="33e6b-186">Check out hello ASP.NET providers for Azure Redis Cache.</span></span>
  * [<span data-ttu-id="33e6b-187">Provedor de estado de sessão do Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="33e6b-187">Azure Redis Session State Provider</span></span>](cache-aspnet-session-state-provider.md)
  * [<span data-ttu-id="33e6b-188">Provedor de Cache de Saída ASP.NET do Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="33e6b-188">Azure Redis Cache ASP.NET Output Cache Provider</span></span>](cache-aspnet-output-cache-provider.md)
* <span data-ttu-id="33e6b-189">[Habilitar o diagnóstico de cache](cache-how-to-monitor.md#enable-cache-diagnostics) para que você possa [monitor](cache-how-to-monitor.md) Olá a integridade do cache.</span><span class="sxs-lookup"><span data-stu-id="33e6b-189">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) hello health of your cache.</span></span> <span data-ttu-id="33e6b-190">Você pode exibir uma saudação métricas em hello portal do Azure e você também podem [Baixe e leia](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) -los usando as ferramentas de saudação de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="33e6b-190">You can view hello metrics in hello Azure portal and you can also [download and review](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) them using hello tools of your choice.</span></span>
* <span data-ttu-id="33e6b-191">Check-out Olá [documentação do cliente de cache Stackexchange][StackExchange.Redis cache client documentation].</span><span class="sxs-lookup"><span data-stu-id="33e6b-191">Check out hello [StackExchange.Redis cache client documentation][StackExchange.Redis cache client documentation].</span></span>
  * <span data-ttu-id="33e6b-192">O Cache Redis do Azure pode ser acessado por meio de muitos clientes Redis e linguagens de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="33e6b-192">Azure Redis Cache can be accessed from many Redis clients and development languages.</span></span> <span data-ttu-id="33e6b-193">Para obter mais informações, veja [http://redis.io/clients][http://redis.io/clients].</span><span class="sxs-lookup"><span data-stu-id="33e6b-193">For more information, see [http://redis.io/clients][http://redis.io/clients].</span></span>
* <span data-ttu-id="33e6b-194">O Cache Redis do Azure também pode ser usado com ferramentas como Redsmin e Redis Desktop Manager.</span><span class="sxs-lookup"><span data-stu-id="33e6b-194">Azure Redis Cache can also be used with third-party services and tools such as Redsmin and Redis Desktop Manager.</span></span>
  * <span data-ttu-id="33e6b-195">Para obter mais informações sobre Redsmin, consulte [como tooretrieve uma conexão Redis do Azure de cadeia de caracteres e usá-lo com Redsmin][How tooretrieve an Azure Redis connection string and use it with Redsmin].</span><span class="sxs-lookup"><span data-stu-id="33e6b-195">For more information about Redsmin, see [How tooretrieve an Azure Redis connection string and use it with Redsmin][How tooretrieve an Azure Redis connection string and use it with Redsmin].</span></span>
  * <span data-ttu-id="33e6b-196">Acesse e inspecione seus dados no Cache Redis do Azure com uma interface gráfica do usuário usando [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span><span class="sxs-lookup"><span data-stu-id="33e6b-196">Access and inspect your data in Azure Redis Cache with a GUI using [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span></span>
* <span data-ttu-id="33e6b-197">Consulte Olá [redis] [ redis] documentação e leia sobre [redis tipos de dados] [ redis data types] e [uma introdução de quinze minutos tipos de dados tooRedis][a fifteen minute introduction tooRedis data types].</span><span class="sxs-lookup"><span data-stu-id="33e6b-197">See hello [redis][redis] documentation and read about [redis data types][redis data types] and [a fifteen minute introduction tooRedis data types][a fifteen minute introduction tooRedis data types].</span></span>

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


