---
title: aaaHow tootroubleshoot Cache Redis do Azure | Microsoft Docs
description: Saiba como tooresolve comum problemas com Cache Redis do Azure.
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 928b9b9c-d64f-4252-884f-af7ba8309af6
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: sdanie
ms.openlocfilehash: 4e736fce2b6d5200a2a8d802f3f1384b63458cab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-azure-redis-cache"></a>Como tootroubleshoot Cache Redis do Azure
Este artigo fornece orientação para solução Olá seguintes categorias de problemas de Cache Redis do Azure.

* [Solução de problemas do cliente lado](#client-side-troubleshooting) - esta seção fornece diretrizes sobre como identificar e resolver problemas causados por aplicativo hello conectando tooAzure Cache Redis.
* [Solução de problemas de lado do servidor](#server-side-troubleshooting) - esta seção fornece diretrizes sobre como identificar e resolver problemas causados saudação do lado do servidor de Cache Redis do Azure.
* [Exceções de tempo limite de Stackexchange](#stackexchangeredis-timeout-exceptions) -esta seção fornece informações sobre solução de problemas ao usar o cliente do hello stackexchange. Redis.

> [!NOTE]
> Várias das etapas neste guia de solução de problemas de saudação incluem instruções toorun comandos do Redis e monitorar várias métricas de desempenho. Para obter mais informações e instruções, consulte os artigos de Olá Olá [informações adicionais](#additional-information) seção.
> 
> 

## <a name="client-side-troubleshooting"></a>Solução de problemas do cliente
Esta seção discute problemas que ocorrem devido a uma condição em um aplicativo de cliente hello.

* [Pressão de memória no cliente Olá](#memory-pressure-on-the-client)
* [Intermitência de tráfego](#burst-of-traffic)
* [Alto nível de uso da CPU do cliente](#high-client-cpu-usage)
* [Largura de banda do cliente ultrapassada](#client-side-bandwidth-exceeded)
* [Solicitação/resposta grande](#large-requestresponse-size)
* [Os dados com toomy no Redis?](#what-happened-to-my-data-in-redis)

### <a name="memory-pressure-on-hello-client"></a>Pressão de memória no cliente Olá
#### <a name="problem"></a>Problema
Pressão de memória na máquina do cliente Olá leva tooall tipos de problemas de desempenho que podem atrasar o processamento de dados que foi enviados por instância do Redis Olá sem atraso. Quando atinge a pressão de memória, o sistema Olá geralmente tem dados de toopage da memória de toovirtual de memória física que está no disco. Isso *a falha de página* causas Olá significativamente sistema tooslow para baixo.

#### <a name="measurement"></a>Medida
1. Monitorar o uso de memória na máquina toomake-se de que não exceda a memória disponível. 
2. Saudação de monitor `Page Faults/Sec` contador de desempenho. A maioria dos sistemas terá algumas falhas de página até mesmo durante a operação normal, portanto, fique atento a picos no contador de desempenho de falhas página que correspondem aos tempos limite.

#### <a name="resolution"></a>Resolução
Atualizar o cliente do maior cliente tooa tamanho da VM com mais memória ou examinar sua memória uso padrões tooreduce memória consuption.

### <a name="burst-of-traffic"></a>Intermitência de tráfego
#### <a name="problem"></a>Problema
Picos de tráfego combinado com baixa `ThreadPool` configurações podem resultar em atrasos no processamento de dados já enviadas por Olá servidor Redis, mas ainda não consumidos no lado do cliente de saudação.

#### <a name="measurement"></a>Medida
Monitor como suas estatísticas de `ThreadPool` mudam ao longo do tempo usando um código [como este](https://github.com/JonCole/SampleCode/blob/master/ThreadPoolMonitor/ThreadPoolLogger.cs). Você também pode examinar Olá `TimeoutException` mensagem do stackexchange. Redis. Veja um exemplo:

    System.TimeoutException: Timeout performing EVAL, inst: 8, mgr: Inactive, queue: 0, qu: 0, qs: 0, qc: 0, wr: 0, wq: 0, in: 64221, ar: 0, 
    IOCP: (Busy=6,Free=999,Min=2,Max=1000), WORKER: (Busy=7,Free=8184,Min=2,Max=8191)

Olá acima mensagem, há vários problemas que são interessantes:

1. Observe que em Olá `IOCP` seção e hello `WORKER` seção que você tem um `Busy` valor maior que Olá `Min` valor. Isso significa que suas configurações de `ThreadPool` precisam de ajuste.
2. Você também pode ver `in: 64221`. Isso indica que 64211 bytes foram recebidos na camada de soquete de kernel hello, mas ainda não foram lidas pelo aplicativo hello (por exemplo, Stackexchange). Normalmente, isso significa que seu aplicativo não está lendo dados de rede Olá rapidamente o servidor de saudação está enviando tooyou.

#### <a name="resolution"></a>Resolução
Configurar seu [ThreadPool configurações](https://gist.github.com/JonCole/e65411214030f0d823cb) toomake-se de que o pool de threads será dimensionado rapidamente em cenários de disparo.

### <a name="high-client-cpu-usage"></a>Alto nível de uso da CPU do cliente
#### <a name="problem"></a>Problema
Alto uso da CPU no cliente de saudação é uma indicação de que o sistema Olá não é possível acompanhar o trabalho Olá que foi solicitado que ele tooperform. Isso significa que o cliente Olá pode falhar tooprocess uma resposta do Redis de maneira oportuna, embora Redis enviou resposta de saudação muito rapidamente.

#### <a name="measurement"></a>Medida
Olá monitor sistema ampla da CPU por meio de saudação Portal do Azure ou Olá associados contador de desempenho. Tenha cuidado não toomonitor *processo* CPU como um único processo pode ter baixa utilização da CPU Olá mesmo tempo que o sistema geral da CPU pode ser alta. Fique atento a picos de uso de CPU que correspondem aos tempos limite. Como resultado de alta utilização da CPU, você também poderá ver alto `in: XXX` valores em `TimeoutException` mensagens de erro, conforme descrito em Olá [intermitência de tráfego](#burst-of-traffic) seção.

> [!NOTE]
> Stackexchange 1.1.603 e posteriores, inclui Olá `local-cpu` métrica em `TimeoutException` mensagens de erro. Certifique-se estiver usando a versão mais recente de saudação do hello [pacote NuGet Stackexchange](https://www.nuget.org/packages/StackExchange.Redis/). Há constantemente de bugs corrigidos no Olá código toomake-tootimeouts mais robusto para ter a versão mais recente da saudação é importante.
> 
> 

#### <a name="resolution"></a>Resolução
Atualizar tooa maior tamanho da VM com maior capacidade de CPU ou investigar o que está causando picos de CPU. 

### <a name="client-side-bandwidth-exceeded"></a>Largura de banda do cliente ultrapassada
#### <a name="problem"></a>Problema
Computadores cliente com tamanhos diferentes têm limitações quanto à largura de banda de rede que têm disponível. Se o cliente Olá excede Olá largura de banda disponível, dados não serão processados no lado do cliente Olá rapidamente o servidor de saudação é enviá-la. Isso pode levar tootimeouts.

#### <a name="measurement"></a>Medida
Monitorar como seu uso de largura de banda muda ao longo do tempo usando um código [como este](https://github.com/JonCole/SampleCode/blob/master/BandWidthMonitor/BandwidthLogger.cs). Observe que esse código pode não ser executado com êxito em alguns ambientes com permissões restritas (como sites do Azure).

#### <a name="resolution"></a>Resolução
Aumentar o tamanho da VM do cliente ou reduzir o consumo de largura de banda da rede.

### <a name="large-requestresponse-size"></a>Solicitação/resposta grande
#### <a name="problem"></a>Problema
Uma solicitação/resposta grande pode causar tempos limite. Por exemplo, suponha que o valor do tempo limite configurado no seu cliente seja de um segundo. Seu aplicativo solicita duas chaves (por exemplo, 'A' e 'B') no hello simultaneamente (usando Olá a mesma conexão de rede física). A maioria dos clientes oferecem suporte a "Pipelining" de solicitações, de modo que as solicitações de 'A' e 'B' são enviadas em Olá durante a transmissão toohello um servidor após Olá outros sem esperar por respostas de saudação. Olá servidor enviará respostas Olá novamente Olá mesmo pedido. Se a resposta 'A' é grande o suficiente, ele pode consomem a maior parte do tempo limite de saudação para solicitações subsequentes. 

saudação de exemplo a seguir demonstra esse cenário. Nesse cenário, solicitação 'A' e 'B' são enviados rapidamente, servidor Olá começa a enviar respostas 'A' e 'B' rapidamente, mas devido a tempo de transferência de dados, 'B' presa atrás Olá outra solicitação e o tempo limite, mesmo que o servidor de saudação respondeu rapidamente.

    |-------- 1 Second Timeout (A)----------|
    |-Request A-|
         |-------- 1 Second Timeout (B) ----------|
         |-Request B-|
                |- Read Response A --------|
                                           |- Read Response B-| (**TIMEOUT**)



#### <a name="measurement"></a>Medida
Este é um um toomeasure difícil. Basicamente, você tem tooinstrument seu cliente código tootrack grandes solicitações e respostas de. 

#### <a name="resolution"></a>Resolução
1. O Redis é otimizado para um grande número de valores pequenos, em vez de alguns valores grandes. Olá preferencial solução é toobreak backup de seus dados em valores menores relacionados. Consulte Olá [o que é o intervalo de tamanho Olá valor ideal para redis? Is 100KB too large? (Qual é o intervalo de tamanho ideal para o Redis? 100 KB é muito?)](https://groups.google.com/forum/#!searchin/redis-db/size/redis-db/n7aa2A4DZDs/3OeEPHSQBAAJ) para obter detalhes sobre por que valores menores são recomendados.
2. Aumentar o tamanho de saudação da VM (para o cliente e servidor de Cache Redis), tooget de recursos de largura de banda maior, redução de dados transferidos vezes para respostas maior. Observe que obter mais largura de banda no servidor de saudação apenas ou apenas no cliente Olá pode não ser suficiente. Medir o uso de largura de banda e compará-la toohello recursos do tamanho de saudação do VM no momento.
3. Aumentar o número de saudação do `ConnectionMultiplexer` objetos uso e solicitações de round-robin em conexões diferentes.

### <a name="what-happened-toomy-data-in-redis"></a>Os dados com toomy no Redis?
#### <a name="problem"></a>Problema
Para determinados esperados dados toobe na minha instância de Cache Redis do Azure, mas ele não parece ser toobe existe.

#### <a name="resolution"></a>Resolução
Consulte [quais dados toomy com Redis?](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md) para possíveis causas e resoluções.

## <a name="server-side-troubleshooting"></a>Solução de problemas do servidor
Esta seção discute problemas que ocorrem devido a uma condição no servidor de cache de saudação.

* [Pressão de memória no servidor de saudação](#memory-pressure-on-the-server)
* [Alto nível de uso da CPU/carga de servidor](#high-cpu-usage-server-load)
* [Largura de banda do servidor ultrapassada](#server-side-bandwidth-exceeded)

### <a name="memory-pressure-on-hello-server"></a>Pressão de memória no servidor de saudação
#### <a name="problem"></a>Problema
Pressão de memória no lado do servidor de saudação leva tooall tipos de problemas de desempenho que podem atrasar o processamento de solicitações. Quando atinge a pressão de memória, o sistema Olá geralmente tem dados de toopage da memória de toovirtual de memória física que está no disco. Isso *a falha de página* causas Olá significativamente sistema tooslow para baixo. Há diversas causas possíveis para essa demanda de memória: 

1. Preencher toofull capacidade de cache da saudação com dados. 
2. Redis está vendo a fragmentação de memória alta - frequentemente causada por armazenar objetos grandes (Redis é otimizado para um pequeno objetos - Consulte Olá [o que é o intervalo de tamanho Olá valor ideal para redis? Is 100KB too large?(Qual é o intervalo de tamanho ideal para o Redis? 100 KB é muito?)](https://groups.google.com/forum/#!searchin/redis-db/size/redis-db/n7aa2A4DZDs/3OeEPHSQBAAJ) para obter mais detalhes). 

#### <a name="measurement"></a>Medida
O Redis expõe duas métricas que podem ajudá-lo a identificar esse problema. Olá primeiro é `used_memory` e Olá outros `used_memory_rss`. [Essas métricas](cache-how-to-monitor.md#available-metrics-and-reporting-intervals) estão disponíveis em Olá Portal do Azure ou por meio de saudação [Redis informações](http://redis.io/commands/info) comando.

#### <a name="resolution"></a>Resolução
Há várias alterações possíveis que você pode fazer uso de memória de manter toohelp Íntegro:

1. [Configurar uma política de memória](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) e definir tempos de expiração em suas chaves. Observe que isso poderá não ser suficiente se você tiver fragmentação.
2. [Configurar um valor reservado maxmemory](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) que é grande o suficiente toocompensate de fragmentação de memória.
3. Dividir os objetos grandes armazenados em cache em objetos menores relacionados.
4. [Escala](cache-how-to-scale.md) tooa maior tamanho do cache.
5. Se você estiver usando um [cache premium com cluster Redis habilitado](cache-how-to-premium-clustering.md) você pode [aumentar Olá número de fragmentos](cache-how-to-premium-clustering.md#change-the-cluster-size-on-a-running-premium-cache).

### <a name="high-cpu-usage--server-load"></a>Alto nível de uso da CPU/carga de servidor
#### <a name="problem"></a>Problema
Alto uso da CPU pode significar que o do lado do cliente de saudação pode falhar tooprocess uma resposta do Redis de maneira oportuna, embora Redis enviou resposta de saudação muito rapidamente.

#### <a name="measurement"></a>Medida
Olá monitor sistema ampla da CPU por meio de saudação Portal do Azure ou Olá associados contador de desempenho. Tenha cuidado não toomonitor *processo* CPU como um único processo pode ter baixa utilização da CPU Olá mesmo tempo que o sistema geral da CPU pode ser alta. Fique atento a picos de uso de CPU que correspondem aos tempos limite.

#### <a name="resolution"></a>Resolução
[Escala](cache-how-to-scale.md) tooa maior cache de camada com capacidade da CPU ou investigar o que está causando picos de CPU. 

### <a name="server-side-bandwidth-exceeded"></a>Largura de banda do servidor ultrapassada
#### <a name="problem"></a>Problema
Instâncias de cache com tamanhos diferentes têm limitações quanto à largura de banda de rede que têm disponível. Se o servidor de saudação excede a largura de banda disponível Olá, em seguida, dados não funcionará toohello cliente mais rapidamente. Isso pode levar tootimeouts.

#### <a name="measurement"></a>Medida
Você pode monitorar Olá `Cache Read` métrica, que é a quantidade de saudação de dados lidos do cache de saudação em Megabytes por segundo (MB/s) durante o intervalo de relatório especificado hello. Esse valor corresponde a largura de banda de rede de toohello usada por esse cache. Se você quiser tooset alertas para limites de largura de banda de rede de lado do servidor, você pode criá-los usando esse `Cache Read` contador. Compare seu leituras com valores hello [essa tabela](cache-faq.md#cache-performance) para Olá observado limites de largura de banda para o cache de vários tamanhos e as camadas de preços.

#### <a name="resolution"></a>Resolução
Se estiver consistentemente próximo Olá observada máxima largura de banda para o tamanho do cache e de camada preços, considere [dimensionamento](cache-how-to-scale.md) tooa preços camada ou tamanho que tem a maior largura de banda de rede, usando os valores hello na [essa tabela](cache-faq.md#cache-performance) como um guia.

## <a name="stackexchangeredis-timeout-exceptions"></a>Exceções de tempo limite do StackExchange.Redis
O StackExchange.Redis usa uma configuração chamada `synctimeout` para operações síncronas, que tem um valor padrão de 1000 ms. Se não for concluída em uma chamada síncrona Olá estipulado tempo, Olá Stackexchange cliente gera um toohello semelhante de erro de tempo limite exemplo a seguir.

    System.TimeoutException: Timeout performing MGET 2728cc84-58ae-406b-8ec8-3f962419f641, inst: 1,mgr: Inactive, queue: 73, qu=6, qs=67, qc=0, wr=1/1, in=0/0 IOCP: (Busy=6, Free=999, Min=2,Max=1000), WORKER (Busy=7,Free=8184,Min=2,Max=8191)


Essa mensagem de erro contém as métricas que podem ajudar a indicar toohello causa e possível a resolução do problema de saudação. Olá tabela a seguir contém detalhes sobre as métricas de mensagem de erro hello.

| Métrica da mensagem de erro | Detalhes |
| --- | --- |
| inst |No último intervalo de tempo Olá: 0 comandos foram emitidos |
| mgr |o Gerenciador de soquete Hello está executando `socket.select` que significa que ele está solicitando Olá SO tooindicate um soquete que tem algo toodo; basicamente: leitor Olá não está lendo ativamente de rede Olá porque ele não que há algo toodo |
| fila |Existem 73 operações em andamento no total |
| qu |6 de operações em andamento de saudação estão na fila não enviado hello e não tiver sido escrito toohello saída de rede |
| qs |67 das operações de em andamento foram enviadas toohello server, mas uma resposta ainda não está disponível. Olá resposta pode ser `Not yet sent by hello server` ou`sent by hello server but not yet processed by hello client.` |
| qc |0 de operações em andamento de saudação viu respostas, mas não ainda foram marcados como concluídos devido toowaiting em loop de conclusão de saudação |
| wr |Há um gravador active (que significa Olá 6 solicitações não enviadas não estão sendo ignoradas) bytes/activewriters |
| mergulhar |Não há nenhum leitor ativo e zero bytes estão disponível toobe Olá NIC bytes/activereaders de leitura |

### <a name="steps-tooinvestigate"></a>Etapas tooinvestigate
1. Como uma prática recomendada Verifique se você estiver usando Olá tooconnect padrão a seguir ao usar o cliente stackexchange. Redis de saudação.

    ```c#
    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("cachename.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
    
    });
    
    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }
    ````

    Para obter mais informações, consulte [conectar cache toohello usando Stackexchange](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache).

1. Certifique-se de que seu Cache Redis do Azure e o aplicativo de cliente hello são Olá mesma região no Azure. Por exemplo, você pode conseguir tempos limite quando o cache está em Leste dos EUA, mas cliente Olá é no Oeste dos EUA e solicitação Olá não for concluída dentro de saudação `synctimeout` intervalo ou você pode conseguir tempos limite quando você estiver depurando em sua máquina de desenvolvimento local. 
   
    Ele é altamente recomendado toohave cache de saudação e no cliente Olá Olá mesma região do Azure. Se você tiver um cenário que inclui chamadas entre regiões, você deve definir Olá `synctimeout` valor tooa de intervalo maior do que o intervalo de 1000 ms saudação padrão, incluindo um `synctimeout` propriedade na cadeia de conexão de saudação. Olá, exemplo a seguir mostra um trecho de cadeia de caracteres de conexão de cache Stackexchange com um `synctimeout` de 2000 ms.
   
        synctimeout=2000,cachename.redis.cache.windows.net,abortConnect=false,ssl=true,password=...
2. Certifique-se estiver usando a versão mais recente de saudação do hello [pacote NuGet Stackexchange](https://www.nuget.org/packages/StackExchange.Redis/). Há constantemente de bugs corrigidos no Olá código toomake-tootimeouts mais robusto para ter a versão mais recente da saudação é importante.
3. Se houver solicitações obtendo associados por limitações de largura de banda no servidor de saudação ou cliente, levará mais tempo para que eles toocomplete e, assim, causar tempos limite. toosee se o tempo limite devido toonetwork largura de banda no servidor de saudação, consulte [largura de banda do lado servidor excedida](#server-side-bandwidth-exceeded). toosee se o tempo limite devido tooclient a largura de banda de rede, consulte [largura de banda do lado cliente excedida](#client-side-bandwidth-exceeded).
4. Você se a CPU associada no servidor de saudação ou no cliente de saudação?
   
   * Verifique se você estiver obtendo associar por CPU no cliente que pode causar Olá solicitação toonot processados na Olá `synctimeout` intervalo, provocando um tempo limite. Movendo tooa maior tamanho de cliente ou distribuir a carga de saudação pode ajudar a toocontrol isso. 
   * Verifique se você estiver obtendo CPU associada no servidor de saudação monitorando Olá `CPU` [métrica de desempenho de cache](cache-how-to-monitor.md#available-metrics-and-reporting-intervals). Solicitações recebidas enquanto o Redis é o limite de CPU pode fazer com que as solicitações tootimeout. tooaddress isso você pode distribuir Olá carregar por vários fragmentos em um cache premium ou atualizar o tamanho maior tooa ou camada de preços. Para obter mais informações, consulte [Largura de banda do servidor ultrapassada](#server-side-bandwidth-exceeded).
5. Há comandos levando muito tempo tooprocess no servidor de saudação? Tempo executando comandos que estão demorando muito tempo tooprocess no servidor redis Olá pode causar tempos limite. Alguns exemplos de comandos de execução longa são `mget` com um grande número de chaves, `keys *` ou scripts lua mal escritos. Você pode conectar tooyour instância de Cache Redis do Azure usando o cliente do redis-cli hello ou usar Olá [Console Redis](cache-configure.md#redis-console) e execução hello [SlowLog](http://redis.io/commands/slowlog) toosee comando se houver solicitações demorando mais do que o esperado. O Servidor do Redis e o StackExchange.Redis são otimizados para várias solicitações pequenas, em vez de menos solicitações grandes. Dividir os dados em partes menores pode melhorar as coisa. 
   
    Para obter informações sobre como conectar o ponto de extremidade do Azure Redis Cache SSL toohello usando a cli do redis e stunnel, consulte Olá [anunciando provedor de estado de sessão ASP.NET a versão de visualização Redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx) postagem de blog. Para obter mais informações, consulte [SlowLog](http://redis.io/commands/slowlog).
6. Uma carga alta no servidor Redis pode resultar em tempos limite. Você pode monitorar a carga do servidor de saudação monitorando Olá `Redis Server Load` [métrica de desempenho de cache](cache-how-to-monitor.md#available-metrics-and-reporting-intervals). Uma carga de servidor de 100 (valor máximo) significa que o servidor redis Olá foi ocupado, sem tempo ocioso, processamento de solicitações. toosee se determinadas solicitações faz backup de todos os recursos de servidor de saudação, execute Olá SlowLog comando, conforme descrito no parágrafo anterior hello. Para obter mais informações, consulte [Alto nível de uso da CPU/carga de servidor](#high-cpu-usage-server-load).
7. Houve qualquer outro evento no lado do cliente de saudação que pode ter causado um blip rede? Verifique no cliente de saudação (web, função de trabalho ou um VM de Iaas) se ocorreu um evento como escalonar o número de saudação de instâncias de cliente para cima ou para baixo ou implantar uma nova versão do cliente de saudação ou dimensionamento automático está habilitado? Em nossos testes que descobrimos que o dimensionamento automático ou o dimensionamento para cima/baixo pode causar a conectividade de rede de saída pode ser perdida durante vários segundos. Código de Stackexchange é toosuch resiliente eventos e se conectará novamente. Durante esse tempo de reconexão quaisquer solicitações na fila de saudação podem atingir o tempo limite.
8. Houve uma solicitação grande anterior várias solicitações pequeno toohello Redis Cache atingiu o tempo limite? Olá parâmetro `qs` erro Olá mensagem informa quantas solicitações foram enviadas do servidor de toohello cliente hello, mas ainda não processou uma resposta. Esse valor pode continuar crescendo porque o StackExchange.Redis usa uma única conexão TCP e só pode ler uma resposta por vez. Mesmo que a primeira operação de saudação atingiu o tempo limite, não impede que dados Olá sendo enviados para/do servidor de saudação e outras solicitações serão bloqueadas até que esse processo for concluído, fazendo com que o tempo limite. Uma solução é toominimize chance de saudação de tempos limite, garantindo que o cache é grande o suficiente para sua carga de trabalho e dividir valores grandes em partes menores. Outra solução possível é toouse um pool de `ConnectionMultiplexer` objetos no seu cliente e escolha Olá menos carregado `ConnectionMultiplexer` ao enviar uma nova solicitação. Isso deve impedir que um tempo limite único fazendo com que o tempo limite da tooalso outras solicitações.
9. Se você estiver usando `RedisSessionStateprovider`, certifique-se de ter definido a tempo limite de novas tentativas de saudação corretamente. `retrytimeoutInMilliseconds` deve ser maior do que `operationTimeoutinMilliseonds`; caso contrário, não haverá novas tentativas. No exemplo a seguir de saudação `retrytimeoutInMilliseconds` é definido too3000. Para obter mais informações, consulte [provedor de estado de sessão do ASP.NET para Cache Redis do Azure](cache-aspnet-session-state-provider.md) e [como toouse Olá parâmetros de configuração do provedor de estado de sessão e o provedor de Cache de saída](https://github.com/Azure/aspnet-redis-providers/wiki/Configuration).

    <add
      name="AFRedisCacheSessionStateProvider"
      type="Microsoft.Web.Redis.RedisSessionStateProvider"
      host="enbwcache.redis.cache.windows.net"
      port="6380"
      accessKey="…"
      ssl="true"
      databaseId="0"
      applicationName="AFRedisCacheSessionState"
      connectionTimeoutInMilliseconds = "5000"
      operationTimeoutInMilliseconds = "1000"
      retryTimeoutInMilliseconds="3000" />


1. Verificar o uso de memória no servidor de Cache Redis do Azure Olá por [monitoramento](cache-how-to-monitor.md#available-metrics-and-reporting-intervals) `Used Memory RSS` e `Used Memory`. Se uma política de remoção está em vigor, o Redis começa removendo chaves quando `Used_Memory` atingir Olá tamanho do cache. Idealmente, `Used Memory RSS` deve ser apenas um pouco maior do que `Used memory`. Uma grande diferença significa que há fragmentação de memória (interna ou externa). Quando `Used Memory RSS` é menor que `Used Memory`, isso significa que parte da memória de cache Olá foram trocada por sistema operacional de saudação. Se isso ocorrer, você poderá esperar que haja algumas latências significativas. Porque Redis não tem controle sobre como suas alocações são mapeados toomemory páginas, alta `Used Memory RSS` geralmente é resultado de saudação de um aumento no uso de memória. Quando o Redis libera memória, memória Olá recebe volta toohello alocador e alocador Olá pode ou não pode oferecer Olá memória toohello back sistema. Pode haver uma discrepância entre hello `Used Memory` consumo de memória e o valor conforme relatado pelo sistema operacional de saudação. Ele pode ser devido fatos toohello memória foi usada e lançada por Redis, mas não fornecido toohello back sistema. toohelp reduzir problemas de memória, você pode executar Olá etapas a seguir.
   
   * Atualize o tamanho maior da saudação cache tooa para que você não estiver executando no limitações de memória no sistema de saudação.
   * Definir tempos de expiração em chaves Olá para que os valores antigos são removidos de maneira proativa.
   * Saudação de saudação do monitor `used_memory_rss` métrica de cache. Quando esse valor se aproximar o tamanho de saudação do seu cache, você está provavelmente toostart tiver problemas de desempenho. Distribua dados saudação por vários fragmentos se você estiver usando um cache premium, ou atualizar tooa maior tamanho do cache.
   
   Para obter mais informações, consulte [pressão de memória no servidor de saudação](#memory-pressure-on-the-server).

## <a name="additional-information"></a>Informações adicionais
* [Qual oferta e tamanho de Cache Redis devo usar?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)
* [Como avaliar o desempenho e teste Olá desempenho de meu cache?](cache-faq.md#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* [Como posso executar comandos do Redis?](cache-faq.md#how-can-i-run-redis-commands)
* [Como toomonitor Cache Redis do Azure](cache-how-to-monitor.md)

