---
title: Como usar o Cache Redis do Azure com Java | Microsoft Docs
description: "Introdução ao Cache Redis do Azure usando o Java"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 29275a5e-2e39-4ef2-804f-7ecc5161eab9
ms.service: cache
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 04/13/2017
ms.author: sdanie
ms.openlocfilehash: 3cfad3a7279b5f9bbff1e6cd9794c492e3544752
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-redis-cache-with-java"></a><span data-ttu-id="e28fd-103">Como usar o Cache Redis do Azure com Java</span><span class="sxs-lookup"><span data-stu-id="e28fd-103">How to use Azure Redis Cache with Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e28fd-104">.NET</span><span class="sxs-lookup"><span data-stu-id="e28fd-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="e28fd-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e28fd-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="e28fd-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="e28fd-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="e28fd-107">Java</span><span class="sxs-lookup"><span data-stu-id="e28fd-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="e28fd-108">Python</span><span class="sxs-lookup"><span data-stu-id="e28fd-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="e28fd-109">O Cache Redis do Azure fornece acesso a um cache Redis dedicado, gerenciado pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e28fd-109">Azure Redis Cache gives you access to a dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="e28fd-110">O cache é acessível por meio de qualquer aplicativo no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e28fd-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="e28fd-111">Este tópico mostra uma introdução ao Cache Redis do Azure usando Java.</span><span class="sxs-lookup"><span data-stu-id="e28fd-111">This topic shows you how to get started with Azure Redis Cache using Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e28fd-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e28fd-112">Prerequisites</span></span>
<span data-ttu-id="e28fd-113">[Jedis](https://github.com/xetorthio/jedis) - cliente Java para Redis</span><span class="sxs-lookup"><span data-stu-id="e28fd-113">[Jedis](https://github.com/xetorthio/jedis) - Java client for Redis</span></span>

<span data-ttu-id="e28fd-114">Este tutorial usa Jedis, mas você pode usar qualquer cliente Java listado em [http://redis.io/clients](http://redis.io/clients).</span><span class="sxs-lookup"><span data-stu-id="e28fd-114">This tutorial uses Jedis, but you can use any Java client listed at [http://redis.io/clients](http://redis.io/clients).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="e28fd-115">Criar um cache Redis no Azure</span><span class="sxs-lookup"><span data-stu-id="e28fd-115">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-the-host-name-and-access-keys"></a><span data-ttu-id="e28fd-116">Recuperar as chaves de acesso e o nome do host</span><span class="sxs-lookup"><span data-stu-id="e28fd-116">Retrieve the host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-to-the-cache-securely-using-ssl"></a><span data-ttu-id="e28fd-117">Conectar-se ao cache com segurança usando SSL</span><span class="sxs-lookup"><span data-stu-id="e28fd-117">Connect to the cache securely using SSL</span></span>
<span data-ttu-id="e28fd-118">As últimas compilações do [jedis](https://github.com/xetorthio/jedis) oferecem suporte para se conectar ao Cache Redis do Azure usando SSL.</span><span class="sxs-lookup"><span data-stu-id="e28fd-118">The latest builds of [jedis](https://github.com/xetorthio/jedis) provide support for connecting to Azure Redis Cache using SSL.</span></span> <span data-ttu-id="e28fd-119">O exemplo a seguir mostra como se conectar ao Cache Redis do Azure usando o ponto de extremidade SSL 6380.</span><span class="sxs-lookup"><span data-stu-id="e28fd-119">The following example shows how to connect to Azure Redis Cache using the SSL endpoint of 6380.</span></span> <span data-ttu-id="e28fd-120">Substitua `<name>` pelo nome do seu cache e `<key>` pela chave primária ou secundária, como descrito anteriormente na seção [Recuperar as chaves de acesso e o nome do host](#retrieve-the-host-name-and-access-keys).</span><span class="sxs-lookup"><span data-stu-id="e28fd-120">Replace `<name>` with the name of your cache and `<key>` with either your primary or secondary key as described in the previous [Retrieve the host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

    boolean useSsl = true;
    /* In this line, replace <name> with your cache name: */
    JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */

> [!NOTE]
> <span data-ttu-id="e28fd-121">A porta não SSL está desabilitada para novas instâncias do Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="e28fd-121">The non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="e28fd-122">Se você estiver usando outro cliente que não ofereça suporte a SSL, veja [Como habilitar a porta não SSL](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="e28fd-122">If you are using a different client that doesn't support SSL, see [How to enable the non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-to-the-cache-and-retrieve-it"></a><span data-ttu-id="e28fd-123">Adicionar algo ao cache e recuperá-lo</span><span class="sxs-lookup"><span data-stu-id="e28fd-123">Add something to the cache and retrieve it</span></span>
    package com.mycompany.app;
    import redis.clients.jedis.Jedis;
    import redis.clients.jedis.JedisShardInfo;

    public class App
    {
      public static void main( String[] args )
      {
        boolean useSsl = true;
        /* In this line, replace <name> with your cache name: */
        JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
        shardInfo.setPassword("<key>"); /* Use your access key. */
        Jedis jedis = new Jedis(shardInfo);
        jedis.set("foo", "bar");
        String value = jedis.get("foo");
      }
    }


## <a name="next-steps"></a><span data-ttu-id="e28fd-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e28fd-124">Next steps</span></span>
* <span data-ttu-id="e28fd-125">[Habilite o diagnóstico de cache](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) para que você possa [monitorar](https://msdn.microsoft.com/library/azure/dn763945.aspx) a integridade do cache.</span><span class="sxs-lookup"><span data-stu-id="e28fd-125">[Enable cache diagnostics](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) so you can [monitor](https://msdn.microsoft.com/library/azure/dn763945.aspx) the health of your cache.</span></span>
* <span data-ttu-id="e28fd-126">Leia a [documentação oficial do Redis](http://redis.io/documentation).</span><span class="sxs-lookup"><span data-stu-id="e28fd-126">Read the official [Redis documentation](http://redis.io/documentation).</span></span>
