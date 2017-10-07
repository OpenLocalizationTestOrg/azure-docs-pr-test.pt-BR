---
title: aaaHow toouse Cache Redis do Azure com Python | Microsoft Docs
description: "Introdução ao Cache Redis do Azure usando Python"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: v-lincan
ms.assetid: f186202c-fdad-4398-af8c-aee91ec96ba3
ms.service: cache
ms.devlang: python
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/10/2017
ms.author: sdanie
ms.openlocfilehash: 74c03eb4ce17ff3574595fd2bb37e399d71c6eb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache-with-python"></a>Como toouse Cache Redis do Azure com Python
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Este tópico mostra como tooget iniciada com o Cache Redis do Azure usando Python.

## <a name="prerequisites"></a>Pré-requisitos
Instale o [redis-py](https://github.com/andymccurdy/redis-py).

## <a name="create-a-redis-cache-on-azure"></a>Criar um cache Redis no Azure
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a>Recuperar as chaves de acesso e do nome de host Olá
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="enable-hello-non-ssl-endpoint"></a>Habilitar o ponto de extremidade do hello não SSL
Alguns clientes Redis não oferecem suporte a SSL e por saudação padrão [porta não SSL está desabilitada para novas instâncias de Cache Redis do Azure](cache-configure.md#access-ports). Em tempo de saudação da redação deste artigo, Olá [redis py](https://github.com/andymccurdy/redis-py) cliente não oferece suporte a SSL. 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-non-ssl-port.md)]

## <a name="add-something-toohello-cache-and-retrieve-it"></a>Adicionar algo toohello armazenar em cache e recuperá-lo
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
