---
title: aaaHow toouse Cache Redis do Azure com Java | Microsoft Docs
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
ms.openlocfilehash: 7768e879d71f61585b59cf4bd6634ba3f12e001d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache-with-java"></a><span data-ttu-id="6298b-103">Como toouse Cache Redis do Azure com Java</span><span class="sxs-lookup"><span data-stu-id="6298b-103">How toouse Azure Redis Cache with Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6298b-104">.NET</span><span class="sxs-lookup"><span data-stu-id="6298b-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="6298b-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="6298b-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="6298b-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="6298b-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="6298b-107">Java</span><span class="sxs-lookup"><span data-stu-id="6298b-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="6298b-108">Python</span><span class="sxs-lookup"><span data-stu-id="6298b-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="6298b-109">Oferece de Cache Redis do Azure acesso tooa dedicado Redis cache, gerenciado pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6298b-109">Azure Redis Cache gives you access tooa dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="6298b-110">O cache é acessível por meio de qualquer aplicativo no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6298b-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="6298b-111">Este tópico mostra como tooget iniciada com o Cache Redis do Azure usando o Java.</span><span class="sxs-lookup"><span data-stu-id="6298b-111">This topic shows you how tooget started with Azure Redis Cache using Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6298b-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6298b-112">Prerequisites</span></span>
<span data-ttu-id="6298b-113">[Jedis](https://github.com/xetorthio/jedis) - cliente Java para Redis</span><span class="sxs-lookup"><span data-stu-id="6298b-113">[Jedis](https://github.com/xetorthio/jedis) - Java client for Redis</span></span>

<span data-ttu-id="6298b-114">Este tutorial usa Jedis, mas você pode usar qualquer cliente Java listado em [http://redis.io/clients](http://redis.io/clients).</span><span class="sxs-lookup"><span data-stu-id="6298b-114">This tutorial uses Jedis, but you can use any Java client listed at [http://redis.io/clients](http://redis.io/clients).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="6298b-115">Criar um cache Redis no Azure</span><span class="sxs-lookup"><span data-stu-id="6298b-115">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a><span data-ttu-id="6298b-116">Recuperar as chaves de acesso e do nome de host Olá</span><span class="sxs-lookup"><span data-stu-id="6298b-116">Retrieve hello host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a><span data-ttu-id="6298b-117">Conecte-se o cache de toohello com segurança usando SSL</span><span class="sxs-lookup"><span data-stu-id="6298b-117">Connect toohello cache securely using SSL</span></span>
<span data-ttu-id="6298b-118">Olá versões mais recentes do [jedis](https://github.com/xetorthio/jedis) oferecem suporte para conexão tooAzure Redis Cache usando SSL.</span><span class="sxs-lookup"><span data-stu-id="6298b-118">hello latest builds of [jedis](https://github.com/xetorthio/jedis) provide support for connecting tooAzure Redis Cache using SSL.</span></span> <span data-ttu-id="6298b-119">saudação de exemplo a seguir mostra como tooconnect tooAzure Redis Cache usando Olá de 6380 no ponto de extremidade SSL.</span><span class="sxs-lookup"><span data-stu-id="6298b-119">hello following example shows how tooconnect tooAzure Redis Cache using hello SSL endpoint of 6380.</span></span> <span data-ttu-id="6298b-120">Substituir `<name>` com o nome de saudação do cache e `<key>` com a sua chave primária ou secundária conforme descrito em Olá anterior [recuperar as chaves de acesso e do nome de host Olá](#retrieve-the-host-name-and-access-keys) seção.</span><span class="sxs-lookup"><span data-stu-id="6298b-120">Replace `<name>` with hello name of your cache and `<key>` with either your primary or secondary key as described in hello previous [Retrieve hello host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

    boolean useSsl = true;
    /* In this line, replace <name> with your cache name: */
    JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */

> [!NOTE]
> <span data-ttu-id="6298b-121">porta do Hello não SSL está desabilitada para novas instâncias de Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="6298b-121">hello non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="6298b-122">Se você estiver usando outro cliente que não oferece suporte a SSL, consulte [como tooenable Olá porta não SSL](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="6298b-122">If you are using a different client that doesn't support SSL, see [How tooenable hello non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a><span data-ttu-id="6298b-123">Adicionar algo toohello armazenar em cache e recuperá-lo</span><span class="sxs-lookup"><span data-stu-id="6298b-123">Add something toohello cache and retrieve it</span></span>
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


## <a name="next-steps"></a><span data-ttu-id="6298b-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6298b-124">Next steps</span></span>
* <span data-ttu-id="6298b-125">[Habilitar o diagnóstico de cache](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) para que você possa [monitor](https://msdn.microsoft.com/library/azure/dn763945.aspx) Olá a integridade do cache.</span><span class="sxs-lookup"><span data-stu-id="6298b-125">[Enable cache diagnostics](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) so you can [monitor](https://msdn.microsoft.com/library/azure/dn763945.aspx) hello health of your cache.</span></span>
* <span data-ttu-id="6298b-126">Leitura Olá oficial [Redis documentação](http://redis.io/documentation).</span><span class="sxs-lookup"><span data-stu-id="6298b-126">Read hello official [Redis documentation](http://redis.io/documentation).</span></span>
