---
title: aaaHow toouse Cache Redis do Azure com Node. js | Microsoft Docs
description: "Introdução ao Cache Redis do Azure usando Node.js e node_redis."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: v-lincan
ms.assetid: 06fddc95-8029-4a8d-83f5-ebd5016891d9
ms.service: cache
ms.devlang: nodejs
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/10/2017
ms.author: sdanie
ms.openlocfilehash: dc8732041d2c4e5793e684e0c80b87a1c9d17f34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache-with-nodejs"></a>Como toouse Cache Redis do Azure com Node. js
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Oferece de Cache Redis do Azure acesso tooa seguro e dedicado cache Redis, gerenciado pela Microsoft. O cache é acessível por meio de qualquer aplicativo no Microsoft Azure.

Este tópico mostra como tooget iniciada com o Cache Redis do Azure usando o Node. js. Para obter outro exemplo do uso do Cache Redis do Azure com Node.js, consulte [Criar um aplicativo de chat do Node.js com Socket.IO em um site do Azure](../app-service-web/web-sites-nodejs-chat-app-socketio.md).

## <a name="prerequisites"></a>Pré-requisitos
Instale o [node_redis](https://github.com/mranney/node_redis):

    npm install redis

Este tutorial usa o [node_redis](https://github.com/mranney/node_redis). Para obter exemplos do uso de outros clientes de Node. js, consulte a documentação de individuais Olá para clientes do Node. js Olá listados em [clientes Redis Node. js](http://redis.io/clients#nodejs).

## <a name="create-a-redis-cache-on-azure"></a>Criar um cache Redis no Azure
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a>Recuperar as chaves de acesso e do nome de host Olá
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a>Conecte-se o cache de toohello com segurança usando SSL
Olá versões mais recentes do [node_redis](https://github.com/mranney/node_redis) oferecem suporte para conexão tooAzure Redis Cache usando SSL. saudação de exemplo a seguir mostra como tooconnect tooAzure Redis Cache usando Olá de 6380 no ponto de extremidade SSL. Substituir `<name>` com o nome de saudação do cache e `<key>` com a sua chave primária ou secundária conforme descrito em Olá anterior [recuperar as chaves de acesso e do nome de host Olá](#retrieve-the-host-name-and-access-keys) seção.

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

> [!NOTE]
> porta do Hello não SSL está desabilitada para novas instâncias de Cache Redis do Azure. Se você estiver usando outro cliente que não oferece suporte a SSL, consulte [como tooenable Olá porta não SSL](cache-configure.md#access-ports).
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a>Adicionar algo toohello armazenar em cache e recuperá-lo
Olá exemplo mostra a você como tooconnect tooan Azure Redis Cache instância, armazena e recuperar um item de cache Olá a seguir. Para obter mais exemplos de como usar o Redis com hello [node_redis](https://github.com/mranney/node_redis) cliente, consulte [http://redis.js.org/](http://redis.js.org/).

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

    client.set("key1", "value", function(err, reply) {
            console.log(reply);
        });

    client.get("key1",  function(err, reply) {
            console.log(reply);
        });

Saída:

    OK
    value


## <a name="next-steps"></a>Próximas etapas
* [Habilitar o diagnóstico de cache](cache-how-to-monitor.md#enable-cache-diagnostics) para que você possa [monitor](cache-how-to-monitor.md) Olá a integridade do cache.
* Leitura Olá oficial [Redis documentação](http://redis.io/documentation).

