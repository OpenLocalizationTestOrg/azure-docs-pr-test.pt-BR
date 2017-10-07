---
title: aaaHow tooconfigure Redis clustering para um Premium do Azure Redis Cache | Microsoft Docs
description: "Saiba como toocreate e gerenciar Redis clustering para da camada Premium instâncias de Cache Redis do Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 62208eec-52ae-4713-b077-62659fd844ab
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: 44d520facb9d1af145b69f1b58f082aabb655d4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-redis-clustering-for-a-premium-azure-redis-cache"></a>Como tooconfigure Redis clustering para um Premium do Azure Redis Cache
Cache Redis do Azure tem diferentes ofertas de cache, que fornecem flexibilidade na escolha de saudação do tamanho do cache e recursos, incluindo recursos de camada Premium, como clustering, persistência e suporte de rede virtual. Este artigo descreve como tooconfigure clustering em um premium do Azure Redis Cache de instância.

Para obter informações sobre outros recursos de cache premium, consulte [camada de Azure Redis Cache Premium Introdução toohello](cache-premium-tier-intro.md).

## <a name="what-is-redis-cluster"></a>O que é o Cluster Redis?
O Cache Redis do Azure oferece o cluster Redis como [implementado no Redis](http://redis.io/topics/cluster-tutorial). Com o Cluster Redis, você obtém Olá benefícios a seguir: 

* Olá capacidade tooautomatically dividir seu conjunto de dados entre vários nós. 
* Olá capacidade toocontinue operações quando um subconjunto de nós hello está apresentando falhas ou estão toocommunicate não é possível com o restante de saudação do cluster hello. 
* Taxa de transferência mais: taxa de transferência linearmente aumenta à medida que aumentar o número de saudação de fragmentos. 
* Tamanho de memória mais: aumenta linearmente à medida que aumentar o número de saudação de fragmentos.  

Para obter mais informações sobre tamanho, taxa de transferência e largura de banda com caches premium, veja [Qual oferta e tamanho de Cache Redis devo usar?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)

No Azure, o cluster Redis é oferecido como um modelo principal/réplica em que cada fragmento tem um par de principal/réplica com replicação em que a replicação Olá é gerenciada pelo serviço de Cache Redis do Azure. 

## <a name="clustering"></a>Clustering
Clustering é ativado Olá **novo Cache Redis** folha durante a criação do cache. 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

Clustering é configurado no hello **Cluster Redis** folha.

![Clustering][redis-cache-clustering]

Você pode ter até too10 fragmentos no cluster hello. Clique em **habilitado** e deslize o controle deslizante de saudação ou digite um número entre 1 e 10 para **contagem de fragmento** e clique em **Okey**.

Cada fragmento é um par de cache primário/réplica gerenciado pelo Azure e tamanho total de saudação do cache de saudação é calculado multiplicando o número Olá de fragmentos pelo tamanho do cache de saudação selecionado no hello preço. 

![Clustering][redis-cache-clustering-selected]

Após a criação do cache de saudação conectar tooit e use apenas como um cache não clusterizado e Redis distribui dados de saudação ao longo de fragmentos de Cache de saudação. Se os diagnósticos são [habilitado](cache-how-to-monitor.md#enable-cache-diagnostics), métricas são capturadas separadamente para cada fragmento e pode ser [exibidas](cache-how-to-monitor.md) na folha de Cache Redis hello. 

> [!NOTE]
> 
> Há algumas pequenas diferenças necessárias em seu aplicativo cliente quando o cluster é configurado. Para obter mais informações, consulte [preciso toomake qualquer toouse de aplicativo alterações toomy cliente clustering?](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
> 
> 

Para o código de exemplo sobre como trabalhar com o cluster com o cliente de Stackexchange Olá, consulte Olá [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs) parte da saudação [Hello World](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) exemplo.

<a name="cluster-size"></a>

## <a name="change-hello-cluster-size-on-a-running-premium-cache"></a>Alterar tamanho do cluster de saudação em um execução cache premium
tamanho do cluster de saudação toochange em um execução premium do cache com clustering clique habilitado, **tamanho do Cluster Redis** de saudação **menu recursos**.

> [!NOTE]
> Enquanto hello Azure Redis Cache Premium camada foi liberado tooGeneral disponibilidade, recurso de tamanho de Cluster Redis hello está atualmente em visualização.
> 
> 

![Tamanho do cluster Redis][redis-cache-redis-cluster-size]

tamanho do cluster Olá toochange, use o controle deslizante de saudação ou digite um número entre 1 e 10 Olá **contagem de fragmento** caixa de texto e clique em **Okey** toosave.

> [!NOTE]
> Dimensionamento de um cluster executa Olá [migrar](https://redis.io/commands/migrate) comando, que é um comando caro, portanto para minimizar o impacto, considere executar esta operação durante o horário de pico. Durante o processo de migração hello, você verá um aumento na carga do servidor. Dimensionamento de um cluster está executando de um longo processo e Olá período de tempo depende do número de saudação de chaves e tamanho Olá valores associados a essas chaves.
> 
> 

## <a name="clustering-faq"></a>Perguntas frequentes sobre clustering
Olá lista a seguir contém as respostas toocommonly perguntas frequentes sobre o cluster de Cache Redis do Azure.

* [É necessário toomake qualquer toouse de aplicativo alterações toomy cliente clustering?](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
* [Como as chaves são distribuídas em um cluster?](#how-are-keys-distributed-in-a-cluster)
* [Qual é o tamanho de cache maior Olá que posso criar?](#what-is-the-largest-cache-size-i-can-create)
* [Todos os clientes do Redis dão suporte ao clustering?](#do-all-redis-clients-support-clustering)
* [Como conectar toomy cache quando o cluster está habilitado?](#how-do-i-connect-to-my-cache-when-clustering-is-enabled)
* [Posso conectar diretamente toohello de fragmentos individuais do meu cache?](#can-i-directly-connect-to-the-individual-shards-of-my-cache)
* [Posso configurar o clustering para um cache criado anteriormente?](#can-i-configure-clustering-for-a-previously-created-cache)
* [Posso configurar o clustering para um cache básico ou standard?](#can-i-configure-clustering-for-a-basic-or-standard-cache)
* [Pode usar clustering com provedores de estado da sessão ASP.NET Redis e cache de saída Olá?](#can-i-use-clustering-with-the-redis-aspnet-session-state-and-output-caching-providers)
* [Estou recebendo exceções MOVE ao usar StackExchange.Redis e clustering. O que devo fazer?](#i-am-getting-move-exceptions-when-using-stackexchangeredis-and-clustering-what-should-i-do)

### <a name="do-i-need-toomake-any-changes-toomy-client-application-toouse-clustering"></a>É necessário toomake qualquer toouse de aplicativo alterações toomy cliente clustering?
* Quando o clustering estiver habilitado, somente o banco de dados 0 estará disponível. Se seu aplicativo cliente usa vários bancos de dados e ele tenta tooread gravação tooa banco de dados ou diferente de 0, hello seguinte exceção será lançada. `Unhandled Exception: StackExchange.Redis.RedisConnectionException: ProtocolFailure on GET --->` `StackExchange.Redis.RedisCommandException: Multiple databases are not supported on this server; cannot switch toodatabase: 6`
  
  Para saber mais, confira [Redis Cluster Specification - Implemented subset (Especificação do cluster Redis — subconjunto implementado)](http://redis.io/topics/cluster-spec#implemented-subset).
* Se você estiver usando [StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/), use a versão 1.0.481 ou posterior. Conecte-se toohello cache usando Olá mesmo [pontos de extremidade, portas e chaves](cache-configure.md#properties) que você usa ao conectar-se o cache de tooa que não tenha habilitado de clustering. Olá única diferença é que todas as leituras e gravações devem ser feitas toodatabase 0.
  
  * Outros clientes podem ter requisitos diferentes. Veja [Todos os clientes do Redis dão suporte ao clustering?](#do-all-redis-clients-support-clustering)
* Se seu aplicativo usa várias operações de chave em lote em um único comando, todas as chaves devem estar localizadas no hello mesmo fragmento. chaves de toolocate no hello mesmo fragmento, consulte [como as chaves são distribuídas em um cluster?](#how-are-keys-distributed-in-a-cluster)
* Se estiver usando o provedor de Estado de Sessão ASP.NET Redis, você deverá usar a versão 2.0.1 ou superior. Consulte [usar clustering com provedores de estado da sessão ASP.NET Redis e cache de saída Olá?](#can-i-use-clustering-with-the-redis-aspnet-session-state-and-output-caching-providers)

### <a name="how-are-keys-distributed-in-a-cluster"></a>Como as chaves são distribuídas em um cluster?
Por Olá Redis [modelo de distribuição de chaves](http://redis.io/topics/cluster-spec#keys-distribution-model) documentação: espaço da chave Olá é dividido em 16384 slots. Cada chave é colocado em hash e atribuído tooone desses slots, que são distribuídos entre nós de saudação do cluster de saudação. Você pode configurar qual parte da chave de saudação é hash tooensure localizados em várias chaves Olá mesmo fragmento usando marcas de hash.

* Chaves com uma marca de hash - se qualquer parte da chave de saudação estiver incluído em `{` e `}`, somente essa parte da chave de saudação é transformado em hash para fins de saudação da determinação do slot de hash de saudação de uma chave. Por exemplo, Olá 3 chaves a seguir deve estar localizado no hello mesmo fragmento: `{key}1`, `{key}2`, e `{key}3` desde apenas Olá `key` parte do nome de saudação é transformado em hash. Para obter uma lista completa das especificações da marca hash de chaves, confira [Keys hash tags](http://redis.io/topics/cluster-spec#keys-hash-tags).
* Chaves sem uma marca de hash - nome da chave inteira Olá é usada para hash. Isso resulta em uma distribuição estatisticamente uniforme entre fragmentos de saudação do cache de saudação.

Para melhor desempenho e a taxa de transferência, recomendamos a distribuição de chaves Olá uniformemente. Se você estiver usando chaves com uma marca de hash é que as chaves de saudação de tooensure de responsabilidade do aplicativo hello são distribuídas uniformemente.

Para saber mais, confira [Keys distribution model](http://redis.io/topics/cluster-spec#keys-distribution-model), [Redis Cluster data sharding](http://redis.io/topics/cluster-tutorial#redis-cluster-data-sharding) e [Keys hash tags](http://redis.io/topics/cluster-spec#keys-hash-tags).

Para o código de exemplo sobre como trabalhar com clustering e a localização de chaves em Olá fragmento mesmo com o cliente Stackexchange Olá, consulte Olá [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs) parte da saudação [Hello World](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) exemplo.

### <a name="what-is-hello-largest-cache-size-i-can-create"></a>Qual é o tamanho de cache maior Olá que posso criar?
maior tamanho de cache premium Olá é 53 GB. Você pode criar até too10 fragmentos fornecendo um tamanho máximo de 530 GB. Se precisar de um tamanho maior, você pode [solicitar mais](mailto:wapteams@microsoft.com?subject=Redis%20Cache%20quota%20increase). Para saber mais, confira [Preço do Cache Redis do Azure](https://azure.microsoft.com/pricing/details/cache/).

### <a name="do-all-redis-clients-support-clustering"></a>Todos os clientes do Redis dão suporte ao clustering?
Em Olá nem todos os clientes oferecem suporte a hora atual Redis clustering. StackExchange.Redis é o que dá suporte a ele. Para obter mais informações sobre outros clientes, consulte Olá [brincando com cluster Olá](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster) seção Olá [tutorial de cluster Redis](http://redis.io/topics/cluster-tutorial).

> [!NOTE]
> Se você estiver usando stackexchange. Redis como cliente, verifique se você estiver usando a versão mais recente de saudação do [Stackexchange](https://www.nuget.org/packages/StackExchange.Redis/) 1.0.481 ou posterior para clustering toowork corretamente. Se você tiver problemas com as exceções de movimentação, confira [exceções move](#move-exceptions) para obter mais informações.
> 
> 

### <a name="how-do-i-connect-toomy-cache-when-clustering-is-enabled"></a>Como conectar toomy cache quando o cluster está habilitado?
Você pode se conectar tooyour cache usando Olá mesmo [pontos de extremidade](cache-configure.md#properties), [portas](cache-configure.md#properties), e [chaves](cache-configure.md#access-keys) que você usa ao conectar-se o cache de tooa que não tenha habilitado de clustering. Redis gerencia Olá clustering em Olá back-end para não ter toomanage-lo do seu cliente.

### <a name="can-i-directly-connect-toohello-individual-shards-of-my-cache"></a>Posso conectar diretamente toohello de fragmentos individuais do meu cache?
Oficialmente, não há suporte para isso. Dito isso, cada fragmento consiste em um par de cache primário/de réplica que é conhecido coletivamente como uma instância de cache. Você pode se conectar a instâncias de cache toothese usando o utilitário de redis-cli Olá no hello [instável](http://redis.io/download) ramificação do repositório de Redis Olá no GitHub. Esta versão implementa suporte básico quando iniciado com hello `-c` alternar. Para obter mais informações, consulte [brincando com cluster Olá](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster) na [http://redis.io](http://redis.io) em Olá [tutorial de cluster Redis](http://redis.io/topics/cluster-tutorial).

Para não ssl, use Olá comandos a seguir.

    Redis-cli.exe –h <<cachename>> -p 13000 (tooconnect tooinstance 0)
    Redis-cli.exe –h <<cachename>> -p 13001 (tooconnect tooinstance 1)
    Redis-cli.exe –h <<cachename>> -p 13002 (tooconnect tooinstance 2)
    ...
    Redis-cli.exe –h <<cachename>> -p 1300N (tooconnect tooinstance N)

Para SSL, substitua `1300N` por `1500N`.

### <a name="can-i-configure-clustering-for-a-previously-created-cache"></a>Posso configurar o clustering para um cache criado anteriormente?
Neste momento, você pode habilitar e configurar o clustering apenas durante a criação de um cache. Você pode alterar o tamanho do cluster Olá depois Olá cache é criado, mas você não pode adicionar o cache de premium tooa clustering ou remover o agrupamento de um cache premium depois Olá cache é criado. Um cache premium com clustering habilitado e somente um fragmento é diferente de um cache com premium Olá mesmo tamanho com nenhum agrupamento.

### <a name="can-i-configure-clustering-for-a-basic-or-standard-cache"></a>Posso configurar o clustering para um cache básico ou standard?
O clustering está disponível apenas para os caches premium.

### <a name="can-i-use-clustering-with-hello-redis-aspnet-session-state-and-output-caching-providers"></a>Pode usar clustering com provedores de estado da sessão ASP.NET Redis e cache de saída Olá?
* **Provedor de Cache de Saída Redis** : sem necessidade de alterações.
* **Provedor de estado de sessão do redis** -toouse clustering, você deve usar [RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 ou superior ou uma exceção será lançada. Essa é uma alteração significativa; para saber mais, confira [v2.0.0 Breaking Change Details](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details).

<a name="move-exceptions"></a>

### <a name="i-am-getting-move-exceptions-when-using-stackexchangeredis-and-clustering-what-should-i-do"></a>Estou recebendo exceções MOVE ao usar StackExchange.Redis e clustering. O que devo fazer?
Se você estiver usando StackExchange.Redis e receber exceções `MOVE` ao usar clustering, verifique se está usando [StackExchange.Redis 1.1.603](https://www.nuget.org/packages/StackExchange.Redis/) ou posterior. Para obter instruções sobre como configurar seu toouse de aplicativos .NET stackexchange. Redis, consulte [configurar clientes de cache Olá](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).

## <a name="next-steps"></a>Próximas etapas
Saiba como toouse premium mais recursos de cache.

* [Camada de Azure Redis Cache Premium toohello Introdução](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-clustering]: ./media/cache-how-to-premium-clustering/redis-cache-clustering.png

[redis-cache-clustering-selected]: ./media/cache-how-to-premium-clustering/redis-cache-clustering-selected.png

[redis-cache-redis-cluster-size]: ./media/cache-how-to-premium-clustering/redis-cache-redis-cluster-size.png







