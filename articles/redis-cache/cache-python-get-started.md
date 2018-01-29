---
title: Como usar o Cache Redis do Azure com Python | Microsoft Docs
description: "Introdução ao Cache Redis do Azure usando Python"
services: redis-cache
documentationcenter: 
author: wesmc7777
manager: cfowler
editor: v-lincan
ms.assetid: f186202c-fdad-4398-af8c-aee91ec96ba3
ms.service: cache
ms.devlang: python
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/10/2017
ms.author: wesmc
ms.openlocfilehash: 17a22dc7a18931e368c7f2e61c563e0d99c3a7ac
ms.sourcegitcommit: 2a70752d0987585d480f374c3e2dba0cd5097880
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="how-to-use-azure-redis-cache-with-python"></a>Como usar o Cache Redis do Azure com Python
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Este tópico mostra uma introdução ao Cache Redis do Azure usando Python.

## <a name="prerequisites"></a>pré-requisitos
Instale o [redis-py](https://github.com/andymccurdy/redis-py).

## <a name="create-a-redis-cache-on-azure"></a>Criar um cache Redis no Azure
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-the-host-name-and-access-keys"></a>Recuperar as chaves de acesso e o nome do host
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="enable-the-non-ssl-endpoint"></a>Habilitar o ponto de extremidade não SSL
Alguns clientes Redis não dão suporte a SSL e, por padrão, a [porta não SSL está desabilitada para novas instâncias do Cache Redis do Azure](cache-configure.md#access-ports). No momento da redação deste artigo, o cliente [redis_py](https://github.com/andymccurdy/redis-py) não oferecia suporte a SSL. 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-non-ssl-port.md)]

## <a name="add-something-to-the-cache-and-retrieve-it"></a>Adicionar algo ao cache e recuperá-lo
    >>> import redis
    >>> r = redis.StrictRedis(host='<name>.redis.cache.windows.net',
          port=6380, db=0, password='<key>', ssl=True)
    >>> r.set('foo', 'bar')
    True
    >>> r.get('foo')
    b'bar'


Substitua `<name>` pelo nome do seu cache e `key` por sua chave de acesso.

<!--Image references-->
[1]: ./media/cache-python-get-started/redis-cache-new-cache-menu.png
[2]: ./media/cache-python-get-started/redis-cache-cache-create.png
