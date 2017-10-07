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
# <a name="how-toouse-azure-redis-cache-with-java"></a>Como toouse Cache Redis do Azure com Java
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Oferece de Cache Redis do Azure acesso tooa dedicado Redis cache, gerenciado pela Microsoft. O cache é acessível por meio de qualquer aplicativo no Microsoft Azure.

Este tópico mostra como tooget iniciada com o Cache Redis do Azure usando o Java.

## <a name="prerequisites"></a>Pré-requisitos
[Jedis](https://github.com/xetorthio/jedis) - cliente Java para Redis

Este tutorial usa Jedis, mas você pode usar qualquer cliente Java listado em [http://redis.io/clients](http://redis.io/clients).

## <a name="create-a-redis-cache-on-azure"></a>Criar um cache Redis no Azure
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a>Recuperar as chaves de acesso e do nome de host Olá
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a>Conecte-se o cache de toohello com segurança usando SSL
Olá versões mais recentes do [jedis](https://github.com/xetorthio/jedis) oferecem suporte para conexão tooAzure Redis Cache usando SSL. saudação de exemplo a seguir mostra como tooconnect tooAzure Redis Cache usando Olá de 6380 no ponto de extremidade SSL. Substituir `<name>` com o nome de saudação do cache e `<key>` com a sua chave primária ou secundária conforme descrito em Olá anterior [recuperar as chaves de acesso e do nome de host Olá](#retrieve-the-host-name-and-access-keys) seção.

    boolean useSsl = true;
    /* In this line, replace <name> with your cache name: */
    JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */

> [!NOTE]
> porta do Hello não SSL está desabilitada para novas instâncias de Cache Redis do Azure. Se você estiver usando outro cliente que não oferece suporte a SSL, consulte [como tooenable Olá porta não SSL](cache-configure.md#access-ports).
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a>Adicionar algo toohello armazenar em cache e recuperá-lo
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


## <a name="next-steps"></a>Próximas etapas
* [Habilitar o diagnóstico de cache](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) para que você possa [monitor](https://msdn.microsoft.com/library/azure/dn763945.aspx) Olá a integridade do cache.
* Leitura Olá oficial [Redis documentação](http://redis.io/documentation).
