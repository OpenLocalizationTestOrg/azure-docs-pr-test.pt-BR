---
title: exemplos de Cache Redis aaaAzure | Microsoft Docs
description: Saiba como toouse Cache Redis do Azure
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 1f8d210c-ee09-4fe2-b63f-1e69246a27d8
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: multiple
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: 5cf9287b577758b5d880d1ca3928c1bee643a8ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-redis-cache-samples"></a>Exemplos do Cache Redis do Azure
Este tópico fornece uma lista de exemplos de Cache Redis do Azure, que abrangem cenários como conexão tooa cache, ler e gravar dados tooand a partir de um cache e usando provedores de Cache Redis do ASP.NET hello. Alguns dos exemplos de saudação são projetos para download, e alguns fornecem orientação passo a passo e incluem trechos de código, mas não vinculam o projeto pode ser baixado de tooa.

## <a name="hello-world-samples"></a>Exemplos Hello world
exemplos de saudação nesta seção mostram Noções básicas de saudação de conectar-se a instância de Cache Redis do Azure tooan leitura e gravação e cache de toohello dados usando uma variedade de linguagens e clientes Redis.

Olá [Olá, mundo](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) de exemplo mostra como tooperform várias operações usando saudação do cache [Stackexchange](https://github.com/StackExchange/StackExchange.Redis) cliente .NET.

Este exemplo mostra como:

* Usar várias opções de conexão
* Ler e gravar objetos tooand do cache de saudação usando operações síncronas e assíncronas
* Usar MGET/MSET Redis comandos tooreturn valores de chaves especificados
* Executar operações transacionais do Redis
* Trabalhar com listas do Redis e conjuntos classificados
* Armazenar objetos .NET usando serializadores JsonConvert
* Use Redis define tooimplement marcação
* Trabalhar com o Cluster Redis

Para obter mais informações, consulte Olá [Stackexchange](https://github.com/StackExchange/StackExchange.Redis) documentação no github e para cenários de uso mais consulte Olá [StackExchange.Redis.Tests](https://github.com/StackExchange/StackExchange.Redis/tree/master/StackExchange.Redis.Tests) testes de unidade.

[Como toouse Cache Redis do Azure com Python](cache-python-get-started.md) mostra como tooget iniciada com o Cache Redis do Azure usando Python e hello [redis py](https://github.com/andymccurdy/redis-py) cliente.

[Trabalhar com objetos .NET no cache de saudação](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache) mostra a você uma maneira tooserialize .NET objetos, portanto você pode escrever tooand lê-los de uma instância de Cache Redis do Azure. 

## <a name="use-redis-cache-as-a-scale-out-backplane-for-aspnet-signalr"></a>Usar o Cache Redis como um backplane de expansão para ASP.NET SignalR
Olá [usar Cache Redis como uma expansão de Backplane do ASP.NET SignalR](https://github.com/rustd/RedisSamples/tree/master/RedisAsSignalRBackplane) demonstra como você pode usar o Cache Redis do Azure como um backplane SignalR. Para obter mais informações sobre o backplane, consulte [SignalR Scaleout com Redis](http://www.asp.net/signalr/overview/performance/scaleout-with-redis).

## <a name="redis-cache-customer-query-sample"></a>Exemplo de consulta de cliente do Cache Redis
Esse exemplo demonstra a comparação de desempenho entre o acesso a dados de um cache e o acesso a dados do armazenamento de persistência. Esse exemplo tem dois projetos.

* [Demonstração de como o Cache Redis pode melhorar o desempenho armazenando dados em cache](https://github.com/rustd/RedisSamples/tree/master/RedisCacheCustomerQuerySample)
* [Semente hello banco de dados e o Cache para demonstração Olá](https://github.com/rustd/RedisSamples/tree/master/SeedCacheForCustomerQuerySample)

## <a name="aspnet-session-state-and-output-caching"></a>Estado de sessão do ASP.NET e cache de saída
Olá [toostore de usar o Azure Redis Cache ASP.NET SessionState e OutputCache](https://github.com/rustd/RedisSamples/tree/master/SessionState_OutputCaching) demonstra como você toouse Cache Redis do Azure toostore sessão ASP.NET e o Cache de saída usando Olá SessionState e OutputCache provedores para O redis.

## <a name="manage-azure-redis-cache-with-maml"></a>Gerenciar o Cache Redis do Azure com MAML
Olá [Gerenciar Cache Redis do Azure usando bibliotecas de gerenciamento do Azure](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) demonstra como você pode usar bibliotecas de gerenciamento do Azure toomanage - (criar / atualizar / excluir) seu Cache. 

## <a name="custom-monitoring-sample"></a>Exemplo de monitoramento personalizado
Olá [dados de monitoramento de acesso Redis Cache](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) demonstra como você pode acessar dados de monitoramento para seu Cache Redis do Azure fora Olá Portal do Azure.

## <a name="a-twitter-style-clone-written-using-php-and-redis"></a>Um clone no estilo do Twitter escrito usando PHP e Redis
Olá [Retwis](https://github.com/SyntaxC4-MSFT/retwis) exemplo é hello Redis Hello World. É um clone de rede social estilo Twitter mínimo escrito usando Redis e PHP usando Olá [Predis](https://github.com/nrk/predis) cliente. código-fonte Olá é projetado toobe muito simples e a saudação mesmo momento tooshow estruturas de dados diferentes do Redis.

## <a name="bandwidth-monitor"></a>Monitor de largura de banda
Olá [monitor de largura de banda](https://github.com/JonCole/SampleCode/tree/master/BandWidthMonitor) amostra permite que você toomonitor Olá da largura de banda usada em Olá cliente. toomeasure Olá largura de banda, executar o exemplo hello na máquina de cliente de cache Olá, fazer chamadas toohello cache e observar a largura de banda Olá relatada pelo exemplo de monitor de largura de banda de saudação.

