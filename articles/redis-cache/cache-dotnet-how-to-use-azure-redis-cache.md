---
title: Como usar o Cache Redis do Azure | Microsoft Docs
description: Saiba como melhorar o desempenho de seus aplicativos do Azure com o Cache Redis do Azure
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
ms.openlocfilehash: 3dfc026490093523446650c510dbebdd660e8b6b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-azure-redis-cache"></a><span data-ttu-id="9cc68-103">Como utilizar o cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="9cc68-103">How to Use Azure Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9cc68-104">.NET</span><span class="sxs-lookup"><span data-stu-id="9cc68-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="9cc68-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9cc68-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="9cc68-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="9cc68-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="9cc68-107">Java</span><span class="sxs-lookup"><span data-stu-id="9cc68-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="9cc68-108">Python</span><span class="sxs-lookup"><span data-stu-id="9cc68-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="9cc68-109">Este guia mostra como começar a usar o **Cache Redis do Azure**.</span><span class="sxs-lookup"><span data-stu-id="9cc68-109">This guide shows you how to get started using **Azure Redis Cache**.</span></span> <span data-ttu-id="9cc68-110">O cache Redis do Microsoft Azure é baseado no popular software livre Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="9cc68-110">Microsoft Azure Redis Cache is based on the popular open source Redis Cache.</span></span> <span data-ttu-id="9cc68-111">Ele fornece acesso a um cache Redis dedicado e seguro, gerenciado pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9cc68-111">It gives you access to a secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="9cc68-112">Um cache criado usando o cache Redis do Azure é acessível de qualquer aplicativo do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9cc68-112">A cache created using Azure Redis Cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="9cc68-113">O Cache Redis do Microsoft Azure está disponível nas seguintes camadas:</span><span class="sxs-lookup"><span data-stu-id="9cc68-113">Microsoft Azure Redis Cache is available in the following tiers:</span></span>

* <span data-ttu-id="9cc68-114">**Básico** – um único nó.</span><span class="sxs-lookup"><span data-stu-id="9cc68-114">**Basic** – Single node.</span></span> <span data-ttu-id="9cc68-115">Vários tamanhos acima de 53 GB.</span><span class="sxs-lookup"><span data-stu-id="9cc68-115">Multiple sizes up to 53 GB.</span></span>
* <span data-ttu-id="9cc68-116">**Standard** – principal/réplica com dois nós.</span><span class="sxs-lookup"><span data-stu-id="9cc68-116">**Standard** – Two-node Primary/Replica.</span></span> <span data-ttu-id="9cc68-117">Vários tamanhos acima de 53 GB.</span><span class="sxs-lookup"><span data-stu-id="9cc68-117">Multiple sizes up to 53 GB.</span></span> <span data-ttu-id="9cc68-118">SLA de 99,9%.</span><span class="sxs-lookup"><span data-stu-id="9cc68-118">99.9% SLA.</span></span>
* <span data-ttu-id="9cc68-119">**Premium** – dois nós Primário/Réplica com até 10 fragmentos.</span><span class="sxs-lookup"><span data-stu-id="9cc68-119">**Premium** – Two-node Primary/Replica with up to 10 shards.</span></span> <span data-ttu-id="9cc68-120">Vários tamanhos de 6 GB a 530 GB.</span><span class="sxs-lookup"><span data-stu-id="9cc68-120">Multiple sizes from 6 GB to 530 GB.</span></span> <span data-ttu-id="9cc68-121">Todos os recursos do tipo Standard e outros, incluindo suporte para [cluster Redis](cache-how-to-premium-clustering.md), [persistência Redis](cache-how-to-premium-persistence.md) e [Rede Virtual do Azure](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="9cc68-121">All Standard tier features and more including support for [Redis cluster](cache-how-to-premium-clustering.md), [Redis persistence](cache-how-to-premium-persistence.md), and [Azure Virtual Network](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="9cc68-122">SLA de 99,9%.</span><span class="sxs-lookup"><span data-stu-id="9cc68-122">99.9% SLA.</span></span>

<span data-ttu-id="9cc68-123">Cada camada é diferente em termos de recursos e preços.</span><span class="sxs-lookup"><span data-stu-id="9cc68-123">Each tier differs in terms of features and pricing.</span></span> <span data-ttu-id="9cc68-124">Para saber mais sobre preços, consulte [Detalhes de preços do cache][Cache Pricing Details].</span><span class="sxs-lookup"><span data-stu-id="9cc68-124">For information on pricing, see [Cache Pricing Details][Cache Pricing Details].</span></span>

<span data-ttu-id="9cc68-125">Este guia mostra a você como usar o cliente [StackExchange.Redis][StackExchange.Redis] usando o código em C\#.</span><span class="sxs-lookup"><span data-stu-id="9cc68-125">This guide shows you how to use the [StackExchange.Redis][StackExchange.Redis] client using C\# code.</span></span> <span data-ttu-id="9cc68-126">Os cenários abordados incluem a **criação e configuração de um cache**, a **configuração de clientes de cache** e a **adição e remoção de objetos do cache**.</span><span class="sxs-lookup"><span data-stu-id="9cc68-126">The scenarios covered include **creating and configuring a cache**, **configuring cache clients**, and **adding and removing objects from the cache**.</span></span> <span data-ttu-id="9cc68-127">Para obter mais informações sobre como usar o Cache Redis do Azure, consulte [Próximas etapas][Next Steps].</span><span class="sxs-lookup"><span data-stu-id="9cc68-127">For more information on using Azure Redis Cache, see [Next Steps][Next Steps].</span></span> <span data-ttu-id="9cc68-128">Para obter um tutorial passo a passo da complicação de um aplicativo Web ASP.NET MVC com o Cache Redis, confira [Como criar um Aplicativo Web com o Cache Redis](cache-web-app-howto.md).</span><span class="sxs-lookup"><span data-stu-id="9cc68-128">For a step-by-step tutorial of building an ASP.NET MVC web app with Redis Cache, see [How to create a Web App with Redis Cache](cache-web-app-howto.md).</span></span>

<a name="getting-started-cache-service"></a>

## <a name="get-started-with-azure-redis-cache"></a><span data-ttu-id="9cc68-129">Introdução ao Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="9cc68-129">Get Started with Azure Redis Cache</span></span>
<span data-ttu-id="9cc68-130">Começar a usar o cache Redis do Azure é fácil.</span><span class="sxs-lookup"><span data-stu-id="9cc68-130">Getting started with Azure Redis Cache is easy.</span></span> <span data-ttu-id="9cc68-131">Para começar, você provisiona e configura um cache.</span><span class="sxs-lookup"><span data-stu-id="9cc68-131">To get started, you provision and configure a cache.</span></span> <span data-ttu-id="9cc68-132">Em seguida, você configura os clientes de cache para que possam acessar o cache.</span><span class="sxs-lookup"><span data-stu-id="9cc68-132">Next, you configure the cache clients so they can access the cache.</span></span> <span data-ttu-id="9cc68-133">Quando os clientes de cache estiverem configurados, você pode começar a trabalhar com eles.</span><span class="sxs-lookup"><span data-stu-id="9cc68-133">Once the cache clients are configured, you can begin working with them.</span></span>

* <span data-ttu-id="9cc68-134">[Criar o cache][Create the cache]</span><span class="sxs-lookup"><span data-stu-id="9cc68-134">[Create the cache][Create the cache]</span></span>
* <span data-ttu-id="9cc68-135">[Configurar os clientes de cache][Configure the cache clients]</span><span class="sxs-lookup"><span data-stu-id="9cc68-135">[Configure the cache clients][Configure the cache clients]</span></span>

<a name="create-cache"></a>

## <a name="create-a-cache"></a><span data-ttu-id="9cc68-136">Criar um cache</span><span class="sxs-lookup"><span data-stu-id="9cc68-136">Create a cache</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

### <a name="to-access-your-cache-after-its-created"></a><span data-ttu-id="9cc68-137">Para acessar o cache depois que ele for criado</span><span class="sxs-lookup"><span data-stu-id="9cc68-137">To access your cache after it's created</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="9cc68-138">Para saber mais sobre como configurar o cache, confira [Como configurar o Cache Redis do Azure](cache-configure.md).</span><span class="sxs-lookup"><span data-stu-id="9cc68-138">For more information about configuring your cache, see [How to configure Azure Redis Cache](cache-configure.md).</span></span>

<a name="NuGet"></a>

## <a name="configure-the-cache-clients"></a><span data-ttu-id="9cc68-139">Configurar os clientes de cache</span><span class="sxs-lookup"><span data-stu-id="9cc68-139">Configure the cache clients</span></span>
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

<span data-ttu-id="9cc68-140">Depois que o projeto de cliente estiver configurado para caching, você poderá usar as técnicas descritas nas seções a seguir para trabalhar com o cache.</span><span class="sxs-lookup"><span data-stu-id="9cc68-140">Once your client project is configured for caching, you can use the techniques described in the following sections for working with your cache.</span></span>

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a><span data-ttu-id="9cc68-141">Trabalhando com caches</span><span class="sxs-lookup"><span data-stu-id="9cc68-141">Working with Caches</span></span>
<span data-ttu-id="9cc68-142">As etapas desta seção descrevem como realizar tarefas comuns com o Cache.</span><span class="sxs-lookup"><span data-stu-id="9cc68-142">The steps in this section describe how to perform common tasks with Cache.</span></span>

* <span data-ttu-id="9cc68-143">[Conectar-se ao cache][Connect to the cache]</span><span class="sxs-lookup"><span data-stu-id="9cc68-143">[Connect to the cache][Connect to the cache]</span></span>
* <span data-ttu-id="9cc68-144">[Adicionar e recuperar objetos do cache][Add and retrieve objects from the cache]</span><span class="sxs-lookup"><span data-stu-id="9cc68-144">[Add and retrieve objects from the cache][Add and retrieve objects from the cache]</span></span>
* [<span data-ttu-id="9cc68-145">Trabalhar com objetos .NET no cache</span><span class="sxs-lookup"><span data-stu-id="9cc68-145">Work with .NET objects in the cache</span></span>](#work-with-net-objects-in-the-cache)

<a name="connect-to-cache"></a>

## <a name="connect-to-the-cache"></a><span data-ttu-id="9cc68-146">Conectar-se ao cache</span><span class="sxs-lookup"><span data-stu-id="9cc68-146">Connect to the cache</span></span>
<span data-ttu-id="9cc68-147">Para trabalhar de forma programática com um cache, você precisa de uma referência ao cache.</span><span class="sxs-lookup"><span data-stu-id="9cc68-147">To programmatically work with a cache, you need a reference to the cache.</span></span> <span data-ttu-id="9cc68-148">Adicione o seguinte à parte superior de qualquer arquivo do qual você deseja usar o cliente StackExchange.Redis para acessar um cache Redis do Azure:</span><span class="sxs-lookup"><span data-stu-id="9cc68-148">Add the following to the top of any file from which you want to use the StackExchange.Redis client to access an Azure Redis Cache.</span></span>

    using StackExchange.Redis;

> [!NOTE]
> <span data-ttu-id="9cc68-149">O cliente StackExchange.Redis requer o .NET Framework 4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="9cc68-149">The StackExchange.Redis client requires .NET Framework 4 or higher.</span></span>
> 
> 

<span data-ttu-id="9cc68-150">A conexão com o Cache Redis do Azure é gerenciada pela classe `ConnectionMultiplexer` .</span><span class="sxs-lookup"><span data-stu-id="9cc68-150">The connection to the Azure Redis Cache is managed by the `ConnectionMultiplexer` class.</span></span> <span data-ttu-id="9cc68-151">Essa classe deve ser compartilhada e reutilizada em todo aplicativo cliente e não precisa ser criada para cada operação.</span><span class="sxs-lookup"><span data-stu-id="9cc68-151">This class should be shared and reused throughout your client application, and does not need to be created on a per operation basis.</span></span> 

<span data-ttu-id="9cc68-152">Para conectar-se a um Cache Redis do Azure e obter uma instância de um `ConnectionMultiplexer` conectado, chame o método estático `Connect` e passe a chave e o ponto de extremidade do cache.</span><span class="sxs-lookup"><span data-stu-id="9cc68-152">To connect to an Azure Redis Cache and be returned an instance of a connected `ConnectionMultiplexer`, call the static `Connect` method and pass in the cache endpoint and key.</span></span> <span data-ttu-id="9cc68-153">Use a chave gerada do Portal do Azure como o parâmetro de senha.</span><span class="sxs-lookup"><span data-stu-id="9cc68-153">Use the key generated from the Azure portal as the password parameter.</span></span>

    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");

> [!IMPORTANT]
> <span data-ttu-id="9cc68-154">Aviso: nunca armazene credenciais no código-fonte.</span><span class="sxs-lookup"><span data-stu-id="9cc68-154">Warning: Never store credentials in source code.</span></span> <span data-ttu-id="9cc68-155">Para manter esse exemplo simples, eu estou mostrando-lhes no código-fonte.</span><span class="sxs-lookup"><span data-stu-id="9cc68-155">To keep this sample simple, I’m showing them in the source code.</span></span> <span data-ttu-id="9cc68-156">Consulte [Como cadeias de caracteres de aplicativo e cadeias de caracteres de conexão funcionam][How Application Strings and Connection Strings Work] para obter informações sobre como armazenar credenciais.</span><span class="sxs-lookup"><span data-stu-id="9cc68-156">See [How Application Strings and Connection Strings Work][How Application Strings and Connection Strings Work] for information on how to store credentials.</span></span>
> 
> 

<span data-ttu-id="9cc68-157">Se não desejar usar o SSL, defina `ssl=false` ou omita o parâmetro `ssl`.</span><span class="sxs-lookup"><span data-stu-id="9cc68-157">If you don't want to use SSL, either set `ssl=false` or omit the `ssl` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="9cc68-158">A porta não SSL é desabilitada por padrão para novos caches.</span><span class="sxs-lookup"><span data-stu-id="9cc68-158">The non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="9cc68-159">Para obter instruções sobre como habilitar a porta não SSL, consulte [Portas de acesso](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="9cc68-159">For instructions on enabling the non-SSL port, see [Access Ports](cache-configure.md#access-ports).</span></span>
> 
> 

<span data-ttu-id="9cc68-160">Uma abordagem para compartilhar uma instância do `ConnectionMultiplexer` em seu aplicativo deve ter uma propriedade estática que retorna uma instância conectada, semelhante ao exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="9cc68-160">One approach to sharing a `ConnectionMultiplexer` instance in your application is to have a static property that returns a connected instance, similar to the following example.</span></span> <span data-ttu-id="9cc68-161">Essa abordagem oferece uma maneira thread-safe de inicializar somente uma instância única conectada do `ConnectionMultiplexer`.</span><span class="sxs-lookup"><span data-stu-id="9cc68-161">This approach provides a thread-safe way to initialize only a single connected `ConnectionMultiplexer` instance.</span></span> <span data-ttu-id="9cc68-162">Nestes exemplos, `abortConnect` é definido como false, o que significa que a chamada terá êxito mesmo que não seja possível estabelecer uma conexão com o Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="9cc68-162">In these examples `abortConnect` is set to false, which means that the call succeeds even if a connection to the Azure Redis Cache is not established.</span></span> <span data-ttu-id="9cc68-163">Um recurso chave do `ConnectionMultiplexer` é que ele restaura automaticamente a conectividade com o cache assim que o problema de rede ou outras causas sejam resolvidos.</span><span class="sxs-lookup"><span data-stu-id="9cc68-163">One key feature of `ConnectionMultiplexer` is that it automatically restores connectivity to the cache once the network issue or other causes are resolved.</span></span>

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

<span data-ttu-id="9cc68-164">Para obter mais informações nas opções de configuração de conexão avançada, consulte [Modelo de configuração de StackExchange.Redis][StackExchange.Redis configuration model].</span><span class="sxs-lookup"><span data-stu-id="9cc68-164">For more information on advanced connection configuration options, see [StackExchange.Redis configuration model][StackExchange.Redis configuration model].</span></span>

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

<span data-ttu-id="9cc68-165">Quando a conexão for estabelecida, retorne uma referência para o banco de dados do redis cache chamando o método `ConnectionMultiplexer.GetDatabase` .</span><span class="sxs-lookup"><span data-stu-id="9cc68-165">Once the connection is established, return a reference to the redis cache database by calling the `ConnectionMultiplexer.GetDatabase` method.</span></span> <span data-ttu-id="9cc68-166">O objeto retornado pelo método `GetDatabase` é um objeto leve de passagem e não precisa ser armazenado.</span><span class="sxs-lookup"><span data-stu-id="9cc68-166">The object returned from the `GetDatabase` method is a lightweight pass-through object and does not need to be stored.</span></span>

    // Connection refers to a property that returns a ConnectionMultiplexer
    // as shown in the previous example.
    IDatabase cache = Connection.GetDatabase();

    // Perform cache operations using the cache object...
    // Simple put of integral data types into the cache
    cache.StringSet("key1", "value");
    cache.StringSet("key2", 25);

    // Simple get of data types from the cache
    string key1 = cache.StringGet("key1");
    int key2 = (int)cache.StringGet("key2");

<span data-ttu-id="9cc68-167">Os caches Redis do Azure têm um número configurável de bancos de dados (padrão de 16) que podem ser usados para separar logicamente os dados em um cache Redis.</span><span class="sxs-lookup"><span data-stu-id="9cc68-167">Azure Redis caches have a configurable number of databases (default of 16) that can be used to logically separate the data within a Redis cache.</span></span> <span data-ttu-id="9cc68-168">Para saber mais, veja [O que são os bancos de dados do Redis?](cache-faq.md#what-are-redis-databases) e [Configuração padrão do servidor Redis](cache-configure.md#default-redis-server-configuration).</span><span class="sxs-lookup"><span data-stu-id="9cc68-168">For more information, see [What are Redis databases?](cache-faq.md#what-are-redis-databases) and [Default Redis server configuration](cache-configure.md#default-redis-server-configuration).</span></span>

<span data-ttu-id="9cc68-169">Agora que você já sabe como conectar-se a uma instância do Cache Redis do Azure e retornar uma referência para o banco de dados do cache, vamos ver como trabalhar com o cache.</span><span class="sxs-lookup"><span data-stu-id="9cc68-169">Now that you know how to connect to an Azure Redis Cache instance and return a reference to the cache database, let's look at working with the cache.</span></span>

<a name="add-object"></a>

## <a name="add-and-retrieve-objects-from-the-cache"></a><span data-ttu-id="9cc68-170">Adicionar e recuperar objetos do cache</span><span class="sxs-lookup"><span data-stu-id="9cc68-170">Add and retrieve objects from the cache</span></span>
<span data-ttu-id="9cc68-171">Itens podem ser armazenados e recuperados de um cache usando os métodos `StringSet` e `StringGet`.</span><span class="sxs-lookup"><span data-stu-id="9cc68-171">Items can be stored in and retrieved from a cache by using the `StringSet` and `StringGet` methods.</span></span>

    // If key1 exists, it is overwritten.
    cache.StringSet("key1", "value1");

    string value = cache.StringGet("key1");

<span data-ttu-id="9cc68-172">O Redis armazena mais dados como cadeias de caracteres Redis, mas essas cadeias de caracteres podem conter muitos tipos de dados, incluindo dados binários serializados, que podem ser usados ao armazenar objetos .NET no cache.</span><span class="sxs-lookup"><span data-stu-id="9cc68-172">Redis stores most data as Redis strings, but these strings can contain many types of data, including serialized binary data, which can be used when storing .NET objects in the cache.</span></span>

<span data-ttu-id="9cc68-173">Ao se chamar `StringGet`, se o objeto existir, ele será retornado e, se não existir, será retornado `null`.</span><span class="sxs-lookup"><span data-stu-id="9cc68-173">When calling `StringGet`, if the object exists, it is returned, and if it does not, `null` is returned.</span></span> <span data-ttu-id="9cc68-174">Se `null` for retornado, você poderá recuperar o valor da fonte de dados desejada e armazená-lo no cache para uso subsequente.</span><span class="sxs-lookup"><span data-stu-id="9cc68-174">If `null` is returned, you can retrieve the value from the desired data source and store it in the cache for subsequent use.</span></span> <span data-ttu-id="9cc68-175">Esse padrão de uso é conhecido como padrão cache-aside.</span><span class="sxs-lookup"><span data-stu-id="9cc68-175">This usage pattern is known as the cache-aside pattern.</span></span>

    string value = cache.StringGet("key1");
    if (value == null)
    {
        // The item keyed by "key1" is not in the cache. Obtain
        // it from the desired data source and add it to the cache.
        value = GetValueFromDataSource();

        cache.StringSet("key1", value);
    }

<span data-ttu-id="9cc68-176">Você também pode usar `RedisValue`, conforme mostra o exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="9cc68-176">You can also use `RedisValue`, as shown in the following example.</span></span> <span data-ttu-id="9cc68-177">O `RedisValue` tem operadores implícitos para trabalhar com tipos de dados integrais e pode ser útil se `null` for um valor esperado para um item em cache.</span><span class="sxs-lookup"><span data-stu-id="9cc68-177">`RedisValue` has implicit operators for working with integral data types, and can be useful if `null` is an expected value for a cached item.</span></span>


    RedisValue value = cache.StringGet("key1");
    if (!value.HasValue)
    {
        value = GetValueFromDataSource();
        cache.StringSet("key1", value);
    }


<span data-ttu-id="9cc68-178">Para especificar a expiração de um item no cache, use o parâmetro `TimeSpan` de `StringSet`.</span><span class="sxs-lookup"><span data-stu-id="9cc68-178">To specify the expiration of an item in the cache, use the `TimeSpan` parameter of `StringSet`.</span></span>

    cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));

## <a name="work-with-net-objects-in-the-cache"></a><span data-ttu-id="9cc68-179">Trabalhar com objetos .NET no cache</span><span class="sxs-lookup"><span data-stu-id="9cc68-179">Work with .NET objects in the cache</span></span>
<span data-ttu-id="9cc68-180">O Cache Redis do Azure pode armazenar objetos .NET e tipos de dados primitivos em cache, mas antes que um objeto .NET seja armazenado em cache, ele deve ser serializado.</span><span class="sxs-lookup"><span data-stu-id="9cc68-180">Azure Redis Cache can cache both .NET objects and primitive data types, but before a .NET object can be cached it must be serialized.</span></span> <span data-ttu-id="9cc68-181">Essa serialização de objetos .NET é de responsabilidade do desenvolvedor do aplicativo e proporciona ao desenvolvedor a flexibilidade na escolha do serializador.</span><span class="sxs-lookup"><span data-stu-id="9cc68-181">This .NET object serialization is the responsibility of the application developer, and gives the developer flexibility in the choice of the serializer.</span></span>

<span data-ttu-id="9cc68-182">Uma maneira simples de serializar objetos é usar os métodos de serialização do `JsonConvert` em [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) e serializar para e do JSON.</span><span class="sxs-lookup"><span data-stu-id="9cc68-182">One simple way to serialize objects is to use the `JsonConvert` serialization methods in [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) and serialize to and from JSON.</span></span> <span data-ttu-id="9cc68-183">O exemplo a seguir mostra um get e set usando uma instância do objeto `Employee` .</span><span class="sxs-lookup"><span data-stu-id="9cc68-183">The following example shows a get and set using an `Employee` object instance.</span></span>

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

    // Store to cache
    cache.StringSet("e25", JsonConvert.SerializeObject(new Employee(25, "Clayton Gragg")));

    // Retrieve from cache
    Employee e25 = JsonConvert.DeserializeObject<Employee>(cache.StringGet("e25"));

<a name="next-steps"></a>

## <a name="next-steps"></a><span data-ttu-id="9cc68-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9cc68-184">Next Steps</span></span>
<span data-ttu-id="9cc68-185">Agora que você aprendeu os conceitos básicos, siga estes links para saber mais sobre o Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="9cc68-185">Now that you've learned the basics, follow these links to learn more about Azure Redis Cache.</span></span>

* <span data-ttu-id="9cc68-186">Confira os provedores ASP.NET para o Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="9cc68-186">Check out the ASP.NET providers for Azure Redis Cache.</span></span>
  * [<span data-ttu-id="9cc68-187">Provedor de estado de sessão do Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="9cc68-187">Azure Redis Session State Provider</span></span>](cache-aspnet-session-state-provider.md)
  * [<span data-ttu-id="9cc68-188">Provedor de Cache de Saída ASP.NET do Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="9cc68-188">Azure Redis Cache ASP.NET Output Cache Provider</span></span>](cache-aspnet-output-cache-provider.md)
* <span data-ttu-id="9cc68-189">[Habilite o diagnóstico de cache](cache-how-to-monitor.md#enable-cache-diagnostics) para que você possa [monitorar](cache-how-to-monitor.md) a integridade do cache.</span><span class="sxs-lookup"><span data-stu-id="9cc68-189">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) the health of your cache.</span></span> <span data-ttu-id="9cc68-190">Você pode exibir as métricas no portal do Azure e também pode [baixá-las e analisá-las](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) usando as ferramentas de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="9cc68-190">You can view the metrics in the Azure portal and you can also [download and review](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) them using the tools of your choice.</span></span>
* <span data-ttu-id="9cc68-191">Confira a [documentação do cliente de cache StackExchange.Redis][StackExchange.Redis cache client documentation].</span><span class="sxs-lookup"><span data-stu-id="9cc68-191">Check out the [StackExchange.Redis cache client documentation][StackExchange.Redis cache client documentation].</span></span>
  * <span data-ttu-id="9cc68-192">O Cache Redis do Azure pode ser acessado por meio de muitos clientes Redis e linguagens de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="9cc68-192">Azure Redis Cache can be accessed from many Redis clients and development languages.</span></span> <span data-ttu-id="9cc68-193">Para obter mais informações, veja [http://redis.io/clients][http://redis.io/clients].</span><span class="sxs-lookup"><span data-stu-id="9cc68-193">For more information, see [http://redis.io/clients][http://redis.io/clients].</span></span>
* <span data-ttu-id="9cc68-194">O Cache Redis do Azure também pode ser usado com ferramentas como Redsmin e Redis Desktop Manager.</span><span class="sxs-lookup"><span data-stu-id="9cc68-194">Azure Redis Cache can also be used with third-party services and tools such as Redsmin and Redis Desktop Manager.</span></span>
  * <span data-ttu-id="9cc68-195">Para obter mais informações sobre o Redsmin, confira [Como recuperar uma cadeia de conexão do Redis do Azure e usá-la com o Redsmin][How to retrieve an Azure Redis connection string and use it with Redsmin].</span><span class="sxs-lookup"><span data-stu-id="9cc68-195">For more information about Redsmin, see [How to retrieve an Azure Redis connection string and use it with Redsmin][How to retrieve an Azure Redis connection string and use it with Redsmin].</span></span>
  * <span data-ttu-id="9cc68-196">Acesse e inspecione seus dados no Cache Redis do Azure com uma interface gráfica do usuário usando [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span><span class="sxs-lookup"><span data-stu-id="9cc68-196">Access and inspect your data in Azure Redis Cache with a GUI using [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span></span>
* <span data-ttu-id="9cc68-197">Veja a documentação do [Redis][redis] e leia sobre [tipos de dados de Redis][redis data types] e [uma introdução de quinze minutos aos tipos de dados de Redis][a fifteen minute introduction to Redis data types].</span><span class="sxs-lookup"><span data-stu-id="9cc68-197">See the [redis][redis] documentation and read about [redis data types][redis data types] and [a fifteen minute introduction to Redis data types][a fifteen minute introduction to Redis data types].</span></span>

<!-- INTRA-TOPIC LINKS -->
[Next Steps]: #next-steps
[Introduction to Azure Redis Cache (Video)]: #video
[What is Azure Redis Cache?]: #what-is
[Create an Azure Cache]: #create-cache
[Which type of caching is right for me?]: #choosing-cache
[Prepare Your Visual Studio Project to Use Azure Caching]: #prepare-vs
[Configure Your Application to Use Caching]: #configure-app
[Get Started with Azure Redis Cache]: #getting-started-cache-service
[Create the cache]: #create-cache
[Configure the cache]: #enable-caching
[Configure the cache clients]: #NuGet
[Working with Caches]: #working-with-caches
[Connect to the cache]: #connect-to-cache
[Add and retrieve objects from the cache]: #add-object
[Specify the expiration of an object in the cache]: #specify-expiration
[Store ASP.NET session state in the cache]: #store-session


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
[How to retrieve an Azure Redis connection string and use it with Redsmin]: https://redsmin.uservoice.com/knowledgebase/articles/485711-how-to-connect-redsmin-to-azure-redis-cache
[Azure Redis Session State Provider]: http://go.microsoft.com/fwlink/?LinkId=398249
[How to: Configure a Cache Client Programmatically]: http://msdn.microsoft.com/library/windowsazure/gg618003.aspx
[Session State Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320835
[Azure AppFabric Cache: Caching Session State]: http://www.microsoft.com/showcase/details.aspx?uuid=87c833e9-97a9-42b2-8bb1-7601f9b5ca20
[Output Cache Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320837
[Azure Shared Caching]: http://msdn.microsoft.com/library/windowsazure/gg278356.aspx
[Team Blog]: http://blogs.msdn.com/b/windowsazure/
[Azure Caching]: http://www.microsoft.com/showcase/Search.aspx?phrase=azure+caching
[How to Configure Virtual Machine Sizes]: http://go.microsoft.com/fwlink/?LinkId=164387
[Azure Caching Capacity Planning Considerations]: http://go.microsoft.com/fwlink/?LinkId=320167
[Azure Caching]: http://go.microsoft.com/fwlink/?LinkId=252658
[How to: Set the Cacheability of an ASP.NET Page Declaratively]: http://msdn.microsoft.com/library/zd1ysf1y.aspx
[How to: Set a Page's Cacheability Programmatically]: http://msdn.microsoft.com/library/z852zf6b.aspx
[Configure a cache in Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn793612.aspx

[StackExchange.Redis configuration model]: https://stackexchange.github.io/StackExchange.Redis/Configuration

[Work with .NET objects in the cache]: http://msdn.microsoft.com/library/dn690521.aspx#Objects


[NuGet Package Manager Installation]: http://go.microsoft.com/fwlink/?LinkId=240311
[Cache Pricing Details]: http://www.windowsazure.com/pricing/details/cache/
[Azure portal]: https://portal.azure.com/

[Overview of Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=320830
[Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=398247

[Migrate to Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=317347
[Azure Redis Cache Samples]: http://go.microsoft.com/fwlink/?LinkId=320840
[Using Resource groups to manage your Azure resources]: ../azure-resource-manager/resource-group-overview.md

[StackExchange.Redis]: http://github.com/StackExchange/StackExchange.Redis
[StackExchange.Redis cache client documentation]: http://github.com/StackExchange/StackExchange.Redis#documentation

[Redis]: http://redis.io/documentation
[Redis data types]: http://redis.io/topics/data-types
[a fifteen minute introduction to Redis data types]: http://redis.io/topics/data-types-intro

[How Application Strings and Connection Strings Work]: http://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/


