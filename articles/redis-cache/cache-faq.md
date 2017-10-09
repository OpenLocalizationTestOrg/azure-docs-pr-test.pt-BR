---
title: Perguntas frequentes sobre Cache Redis do aaaAzure | Microsoft Docs
description: "Aprenda a saudação responde perguntas toocommon, padrões e práticas recomendadas para o Cache Redis do Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: c2c52b7d-b2d1-433a-b635-c20180e5cab2
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: sdanie
ms.openlocfilehash: 2c6ed2f65f755bd08f04857b7af31f520cf4f158
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-redis-cache-faq"></a>Perguntas frequentes sobre Cache Redis do Azure
Aprenda a saudação responde perguntas toocommon, padrões e práticas recomendadas para o Cache Redis do Azure.

## <a name="what-if-my-question-isnt-answered-here"></a>E se dúvida não foi respondida aqui?
Se sua pergunta não estiver listada aqui, fale conosco e nós ajudaremos a encontrar uma resposta.

* Você pode postar uma pergunta nos comentários Olá final Olá essas perguntas Frequentes e entre em contato com a equipe de Cache do Azure hello e outros membros da comunidade sobre este artigo.
* tooreach um público maior, você poderá postar uma pergunta em hello [Fórum do MSDN do Azure Cache](https://social.msdn.microsoft.com/forums/azure/home?forum=azurecache) e entre em contato com a equipe de Cache do Azure hello e outros membros da comunidade de saudação.
* Se você quiser toomake uma solicitação de recurso, você pode enviar suas solicitações e ideias muito[Azure Redis Cache User Voice](https://feedback.azure.com/forums/169382-cache).
* Você também pode enviar um email toous em [Azure Cache externo comentários](mailto:azurecache@microsoft.com).

## <a name="azure-redis-cache-basics"></a>Noções básicas sobre o Cache Redis do Azure
Olá perguntas frequentes nesta seção abordam alguns dos conceitos básicos de saudação do Cache Redis do Azure.

* [O que é o Cache Redis do Azure?](#what-is-azure-redis-cache)
* [Como posso começar a usar o Cache Redis do Azure?](#how-can-i-get-started-with-azure-redis-cache)

Olá FAQs seguir abrangem os conceitos básicos e perguntas sobre o Cache Redis do Azure e são respondidas em um dos Olá outras seções de perguntas Frequentes.

* [Qual oferta e tamanho de Cache Redis devo usar?](#what-redis-cache-offering-and-size-should-i-use)
* [Quais clientes do cache Redis eu posso usar?](#what-redis-cache-clients-can-i-use)
* [Há um emulador local para o Cache Redis do Azure?](#is-there-a-local-emulator-for-azure-redis-cache)
* [Como monitorar integridade hello e o desempenho do meu cache?](#how-do-i-monitor-the-health-and-performance-of-my-cache)

## <a name="planning-faqs"></a>Perguntas frequentes sobre planejamento
* [Qual oferta e tamanho de Cache Redis devo usar?](#what-redis-cache-offering-and-size-should-i-use)
* [Desempenho do Cache Redis do Azure](#azure-redis-cache-performance)
* [Em que região posso localizar meu cache?](#in-what-region-should-i-locate-my-cache)
* [Como eu sou cobrado pelo Cache Redis do Azure?](#how-am-i-billed-for-azure-redis-cache)
* [Posso usar o Cache Redis do Azure com o Azure Governamental na Nuvem, o Azure China na Nuvem ou o Microsoft Azure Alemanha?](#can-i-use-azure-redis-cache-with-azure-government-cloud-azure-china-cloud-or-microsoft-azure-germany)

## <a name="development-faqs"></a>Perguntas frequentes sobre desenvolvimento
* [O que faço opções de configuração de Stackexchange Olá?](#what-do-the-stackexchangeredis-configuration-options-do)
* [Quais clientes do cache Redis eu posso usar?](#what-redis-cache-clients-can-i-use)
* [Há um emulador local para o Cache Redis do Azure?](#is-there-a-local-emulator-for-azure-redis-cache)
* [Como posso executar comandos do Redis?](#how-can-i-run-redis-commands)
* [Por que o Cache Redis do Azure não tem uma referência de biblioteca de classe do MSDN como alguns da Olá outros serviços do Azure?](#why-doesnt-azure-redis-cache-have-an-msdn-class-library-reference-like-some-of-the-other-azure-services)
* [Posso usar o Cache Redis do Azure como um cache de sessão do PHP?](#can-i-use-azure-redis-cache-as-a-php-session-cache)
* [Quais são os bancos de dados do Redis?](#what-are-redis-databases)

## <a name="security-faqs"></a>Perguntas frequentes sobre segurança
* [Quando eu habilito a porta não SSL de saudação para conectar-se tooRedis?](#when-should-i-enable-the-non-ssl-port-for-connecting-to-redis)

## <a name="production-faqs"></a>Perguntas frequentes sobre produção
* [Quais são algumas práticas recomendadas de produção?](#what-are-some-production-best-practices)
* [Quais são algumas das considerações de saudação ao usar os comandos comuns do Redis?](#what-are-some-of-the-considerations-when-using-common-redis-commands)
* [Como avaliar o desempenho e teste Olá desempenho de meu cache?](#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* [Detalhes importantes sobre o crescimento de ThreadPool](#important-details-about-threadpool-growth)
* [Habilitar servidor GC tooget mais taxa de transferência no cliente hello usando stackexchange. Redis](#enable-server-gc-to-get-more-throughput-on-the-client-when-using-stackexchangeredis)
* [Considerações sobre desempenho em torno de conexões](#performance-considerations-around-connections)

## <a name="monitoring-and-troubleshooting-faqs"></a>Perguntas frequentes sobre monitoramento e solução de problemas
Olá perguntas frequentes nesta seção abrange comuns monitoramento e perguntas sobre solução de problemas. Para obter mais informações sobre como monitorar e solucionar problemas de suas instâncias de Cache Redis do Azure, consulte [como toomonitor Cache Redis do Azure](cache-how-to-monitor.md) e [como tootroubleshoot Cache Redis do Azure](cache-how-to-troubleshoot.md).

* [Como monitorar integridade hello e o desempenho do meu cache?](#how-do-i-monitor-the-health-and-performance-of-my-cache)
* [Por que vejo tempos limite?](#why-am-i-seeing-timeouts)
* [Por que meu cliente foi desconectado do cache Olá?](#why-was-my-client-disconnected-from-the-cache)

## <a name="prior-cache-offering-faqs"></a>Perguntas frequentes sobre ofertas anteriores de cache
* [Qual oferta de Cache do Azure é a correta para mim?](#which-azure-cache-offering-is-right-for-me)

### <a name="what-is-azure-redis-cache"></a>O que é o Cache Redis do Azure?
Cache Redis do Azure baseia-se a saudação populares código-fonte aberto [Redis cache](http://redis.io). Isso lhe dá acesso tooa cache seguro e dedicado Redis, gerenciado pela Microsoft e acessível de qualquer aplicativo no Azure. Para obter uma visão mais detalhada, consulte Olá [Cache Redis do Azure](https://azure.microsoft.com/services/cache/) página de produto em Azure.com.

### <a name="how-can-i-get-started-with-azure-redis-cache"></a>Como posso começar a usar o Cache Redis do Azure?
Há várias maneiras de começar a usar o Cache Redis do Azure.

* Você pode conferir um dos nossos tutoriais disponíveis para [.NET](cache-dotnet-how-to-use-azure-redis-cache.md), [ASP.NET](cache-web-app-howto.md), [Java](cache-java-get-started.md), [Node.js](cache-nodejs-get-started.md) e [Python](cache-python-get-started.md).
* Você pode assistir [como tooBuild aplicativos usando o Microsoft Azure Redis Cache de alto desempenho](https://azure.microsoft.com/documentation/videos/how-to-build-high-performance-apps-using-microsoft-azure-cache/).
* Você pode verificar a documentação do cliente Olá para clientes de saudação que corresponder ao idioma de desenvolvimento de saudação do seu toosee projeto como toouse Redis. Há muitos clientes Redis que podem ser usados com o Cache Redis do Azure. Para obter uma lista de clientes Redis, acesse [http://redis.io/clients](http://redis.io/clients).

Se ainda não tiver uma conta do Azure, você poderá:

* [Abrir uma conta do Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero). Você obtém créditos que podem ser usado tootry out paga serviços do Azure. Mesmo depois de saudação créditos são esgotados, você pode manter Olá conta e usar os recursos e serviços do Azure gratuitos.
* [Ativar benefícios de assinante do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero). Todos os meses, sua assinatura do MSDN lhe oferece créditos que podem ser usados para serviços pagos do Azure.

<a name="cache-size"></a>

### <a name="what-redis-cache-offering-and-size-should-i-use"></a>Qual oferta e tamanho de Cache Redis devo usar?
Cada oferta de Cache Redis do Azure fornece diferentes níveis de opções **tamanho**, **largura de banda**, **alta disponibilidade** e **SLA**.

Olá seguem considerações sobre como escolher uma oferta de Cache.

* **Memória**: Olá básico e padrão as novas camadas oferecem 250 MB a 53 GB. camada de Premium Olá oferece até too530 GB. Para saber mais, confira [Preço do Cache Redis do Azure](https://azure.microsoft.com/pricing/details/cache/).
* **Desempenho de rede**: se você tiver uma carga de trabalho que requer alta taxa de transferência, a camada de Premium Olá oferece mais largura de banda em comparação comparada tooStandard ou Basic. Também em cada camada, caches de tamanho maior têm mais largura de banda devido a saudação subjacente VM que hospeda o cache de saudação. Consulte Olá [tabela a seguir](#cache-performance) para obter mais informações.
* **Taxa de transferência**: camada de Premium Olá oferece Olá disponível taxa de transferência máxima. Se o cliente ou servidor de cache de saudação atingir os limites de largura de banda hello, você pode receber tempos limite no lado do cliente de saudação. Para obter mais informações, consulte Olá a tabela a seguir.
* **Alta disponibilidade/SLA**: Cache Redis do Azure garante que um cache padrão/Premium está disponível pelo menos 99,9% de tempo de saudação. toolearn mais sobre nosso SLA, consulte [preços do Azure Redis Cache](https://azure.microsoft.com/support/legal/sla/cache/v1_0/). Olá SLA cobre apenas pontos de extremidade de Cache de toohello conectividade. Olá SLA não aborda a proteção contra perda de dados. É recomendável usar o recurso de persistência de dados do Redis Olá em Olá Premium camada tooincrease garantir a resiliência contra perda de dados.
* **Persistência de dados de redis**: camada de Premium Olá permite toopersist dados de cache de saudação em uma conta de armazenamento do Azure. Em um cache Basic/Standard, todos os dados de saudação é armazenado somente na memória. Se houver problemas de infraestrutura subjacente, pode haver uma possível perda de dados. É recomendável usar o recurso de persistência de dados do Redis Olá em Olá Premium camada tooincrease garantir a resiliência contra perda de dados. O Cache Redis do Azure oferece opções de RDB e AOF (em breve) na persistência do Redis. Para obter mais informações, consulte [como tooconfigure persistência para um Premium do Azure Redis Cache](cache-how-to-premium-persistence.md).
* **Cluster de redis**: toocreate armazena em cache maior 53 GB ou tooshard dados em vários nós de Redis, você pode usar clustering Redis, que está disponível na camada de Premium Olá. Cada nó consiste em um par de cache primário/de réplica para alta disponibilidade. Para obter mais informações, consulte [como tooconfigure clustering para um Premium do Azure Redis Cache](cache-how-to-premium-clustering.md).
* **Aprimorados de isolamento de rede e de segurança**: implantação de rede Virtual do Azure (VNET) fornece maior segurança e isolamento para Cache Redis do Azure, bem como as sub-redes, políticas de controle de acesso, e outros recursos toofurther restringir o acesso. Para obter mais informações, consulte [como suporte a tooconfigure rede Virtual para um Premium do Azure Redis Cache](cache-how-to-premium-vnet.md).
* **Configurar o Redis**: saudação padrão e as camadas Premium, você pode configurar Redis para as notificações Keyspace.
* **Número máximo de conexões de cliente**: camada de Premium Olá oferece o número máximo de saudação de clientes que se conectam a tooRedis, com um número mais alto de conexões para caches de tamanhos maior. Para obter mais informações, confira [Preço do Cache Redis do Azure](https://azure.microsoft.com/pricing/details/cache/).
* **Dedicado principal para o servidor Redis**: na camada de Premium Olá, todos os tamanhos de cache tem um núcleo dedicado para Redis. Em camadas básica/padrão de saudação, Olá tamanho C1 e acima tem um núcleo dedicado para o servidor Redis.
* **Como o Redis usa thread único** , ter mais de dois núcleos não oferece um benefício adicional em relação a ter apenas dois, mas tamanhos maiores de VM normalmente têm mais largura de banda que tamanhos menores. Se o cliente ou servidor de cache de saudação atingir os limites de largura de banda hello, você recebe tempos limite no lado do cliente de saudação.
* **Melhorias de desempenho**: Caches na camada de Premium Olá são implantados no hardware com processadores mais rápidos, proporcionando melhor desempenho em comparação com toohello camada básica ou Standard. Os Caches da camada Premium têm a taxa de transferência mais alta e as latências mais baixas.

<a name="cache-performance"></a>

### <a name="azure-redis-cache-performance"></a>Desempenho do Cache Redis do Azure
Olá, tabela a seguir mostra valores de largura de banda máxima de Olá observados ao testar vários tamanhos de Standard e Premium armazena em cache usando `redis-benchmark.exe` de uma VM de Iaas no ponto de extremidade do hello Cache Redis do Azure. 

>[!NOTE] 
>Esses valores não são garantidos e que não há nenhum SLA para esses números, mas eles devem ser típicos. Você deve carregar seu próprio tamanho de cache certo aplicativo toodetermine Olá para seu aplicativo de teste.
>
>

Desta tabela, podemos desenhar Olá conclusões a seguir:

* Taxa de transferência para os caches de saudação são Olá mesmo tamanho é maior em Olá camada Premium como camada padrão toohello comparados. Por exemplo, com um Cache de 6 GB, a taxa de transferência de P1 é 180.000 RPS como too49 comparados, 000 para C3.
* Com o Redis clustering, taxa de transferência aumenta linearmente conforme você aumenta o número de saudação de fragmentos (nós) no cluster hello. Por exemplo, se você criar um cluster P4 de 10 fragmentos, taxa de transferência disponível Olá é 400.000 * 10 = 4 milhões RPS.
* Taxa de transferência para tamanhos de chave maiores é mais alta na camada de Premium Olá como toohello em comparação com o nível padrão.

| Tipo de preço  | Tamanho | Núcleos de CPU | Largura de banda disponível | Tamanho do valor de 1 KB |
| --- | --- | --- | --- | --- |
| **Tamanhos de cache padrão** | | |**Megabits por segundo (Mb/s) / Megabytes por segundo (MB/s)** |**RPS (solicitações por segundo)** |
| C0 |250 MB |Compartilhado |5 / 0,625 |600 |
| C1 |1 GB |1 |100 / 12,5 |12.200 |
| C2 |2,5 GB |2 |200 / 25 |24.000 |
| C3 |6 GB |4 |400 / 50 |49.000 |
| C4 |13 GB |2 |500 / 62,5 |61.000 |
| C5 |26 GB |4 |1.000 / 125 |115.000 |
| C6 |53 GB |8 |2.000 / 250 |150.000 |
| **Tamanhos de cache Premium** | |**Núcleos de CPU por fragmento** | **Megabits por segundo (Mb/s) / Megabytes por segundo (MB/s)** |**RPS (solicitações por segundo) por fragmento** |
| P1 |6 GB |2 |1.500 / 187.5 |180,000 |
| P2 |13 GB |4 |3.000 / 375 |360,000 |
| P3 |26 GB |4 |3.000 / 375 |360,000 |
| P4 |53 GB |8 |6.000 / 750 |400.000 |

Para obter instruções sobre como baixar Olá Redis ferramentas como `redis-benchmark.exe`, consulte Olá [como executar comandos do Redis?](#cache-commands) seção.

<a name="cache-region"></a>

### <a name="in-what-region-should-i-locate-my-cache"></a>Em que região posso localizar meu cache?
Para obter um melhor desempenho e latência mais baixa, localize o Cache Redis do Azure no hello mesma região que o aplicativo cliente de cache.

<a name="cache-billing"></a>

### <a name="how-am-i-billed-for-azure-redis-cache"></a>Como eu sou cobrado pelo Cache Redis do Azure?
O preço do Cache Redis do Azure pode ser encontrado [aqui](https://azure.microsoft.com/pricing/details/cache/). página de preços de saudação lista preços como uma taxa por hora. Os caches são cobrados em uma base por minuto da hora Olá Olá cache é criado até que o tempo de saudação um cache é excluído. Não há nenhuma opção para parar ou pausar a cobrança de saudação do cache.

### <a name="can-i-use-azure-redis-cache-with-azure-government-cloud-azure-china-cloud-or-microsoft-azure-germany"></a>Posso usar o Cache Redis do Azure com o Azure Governamental na Nuvem, o Azure China na Nuvem ou o Microsoft Azure Alemanha?
Sim, o Cache Redis do Azure está disponível no Azure Governamental na Nuvem, Azure China na Nuvem e Microsoft Azure Alemanha. Olá URLs para acessar e gerenciar o Cache Redis do Azure são diferentes nessas nuvens em comparação com a nuvem pública do Azure. 

| Nuvem   | Sufixo DNS para Redis            |
|---------|---------------------------------|
| Público  | *.redis.cache.windows.net       |
| Gov dos EUA  | *.redis.cache.usgovcloudapi.net |
| Alemanha | *.redis.cache.cloudapi.de       |
| China   | *.redis.cache.chinacloudapi.cn  |

Para obter mais informações sobre considerações ao usar o Cache Redis do Azure com outras nuvens, consulte Olá links a seguir.

- [Bancos de dados do Azure Governamental – Cache Redis do Azure](../azure-government/documentation-government-services-database.md#azure-redis-cache)
- [Azure China na Nuvem – Cache Redis do Azure](https://www.azure.cn/documentation/services/redis-cache/)
- [Microsoft Azure Alemanha](https://azure.microsoft.com/overview/clouds/germany/)

Para obter informações sobre como usar o Cache Redis do Azure com o PowerShell na nuvem do Azure governamental, nuvem do Azure na China e Microsoft Azure Alemanha, consulte [como tooconnect tooother nuvens - Azure Redis Cache PowerShell](cache-howto-manage-redis-cache-powershell.md#how-to-connect-to-other-clouds).

<a name="cache-configuration"></a>

### <a name="what-do-hello-stackexchangeredis-configuration-options-do"></a>O que faço opções de configuração de Stackexchange Olá?
O StackExchange.Redis tem muitas opções. Esta seção fala sobre algumas das configurações comuns de saudação. Para obter mais informações sobre opções do StackExchange.Redis, consulte [configuração do StackExchange.Redis](https://stackexchange.github.io/StackExchange.Redis/Configuration).

| ConfigurationOptions | Descrição | Recomendações |
| --- | --- | --- |
| AbortOnConnectFail |Quando definido como tootrue, conexão Olá não reconectará após uma falha de rede. |Defina toofalse e permitem Stackexchange reconectar-se automaticamente. |
| ConnectRetry |Olá número de vezes de tentativas de conexão toorepeat durante inicial se conectar. |Consulte Olá notas para obter diretrizes a seguir. |
| ConnectTimeout |Tempo limite em ms para operações de conexão. |Consulte Olá notas para obter diretrizes a seguir. |

Geralmente os valores padrão de saudação do cliente Olá são suficientes. Você pode ajustar as opções de saudação com base em sua carga de trabalho.

* **Novas tentativas**
  * Para ConnectRetry e ConnectTimeout, diretrizes gerais de saudação é toofail rápida e tente novamente. Este guia se baseia em sua carga de trabalho e o tempo, em média ele leva para tooissue seu cliente um comando Redis e receber uma resposta.
  * Deixe o StackExchange.Redis reconectar-se automaticamente, em vez de você verificar o status de conexão e realizar a reconexão. **Evite usar Olá ConnectionMultiplexer.IsConnected propriedade**.
  * Snowballing - às vezes, você pode encontrar um problema em que você está tentando novamente e Olá repetições bola de neve e nunca recupera. Se snowballing ocorrer, considere usar um algoritmo de nova tentativa de retirada exponencial conforme descrito em [Repita diretrizes gerais](../best-practices-retry-general.md) publicado pelo grupo Microsoft Patterns & práticas de saudação.
* **Valores de tempo limite**
  * Considere a possibilidade de sua carga de trabalho e definir valores de saudação adequadamente. Se você estiver armazenando valores grandes, defina o valor mais alto do hello tempo limite tooa.
  * Definir `AbortOnConnectFail` toofalse e permitem Stackexchange reconexão para você.
  * Use uma única instância de ConnectionMultiplexer para o aplicativo hello. Você pode usar um toocreate LazyConnection uma única instância que é retornada por uma propriedade de Conexão, conforme mostrado no [conectar toohello cache usando a classe ConnectionMultiplexer de saudação](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache).
  * Saudação de conjunto `ConnectionMultiplexer.ClientName` propriedade tooan aplicativo instância nome exclusivo para fins de diagnóstico.
  * Usar várias instâncias de `ConnectionMultiplexer` para cargas de trabalho personalizadas.
      * Você pode seguir este modelo se tem variação de carga em seu aplicativo. Por exemplo:
      * Você pode ter um multiplexador para lidar com chaves grandes.
      * Você pode ter um multiplexador para lidar com chaves pequenas.
      * Você pode definir valores diferentes para o tempo limite da conexão e a lógica de repetição para cada ConnectionMultiplexer que você usa.
      * Saudação de conjunto `ClientName` propriedade em cada toohelp multiplexador com o diagnóstico.
      * Este guia pode levar a latência toomore simplificado por `ConnectionMultiplexer`.

### <a name="what-redis-cache-clients-can-i-use"></a>Quais clientes do cache Redis eu posso usar?
Um dos grandes benefícios de saudação do Redis é que há muitos clientes com suporte a várias linguagens de programação diferentes. Para obter uma lista atual de clientes, confira [Clientes Redis](http://redis.io/clients). Para tutoriais que abrangem vários idiomas diferentes e os clientes, consulte [como toouse Cache Redis do Azure](cache-dotnet-how-to-use-azure-redis-cache.md) e clique em idioma alternador de idioma Olá na parte superior de saudação do artigo Olá Olá desejado.

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

<a name="cache-emulator"></a>

### <a name="is-there-a-local-emulator-for-azure-redis-cache"></a>Há um emulador local para o Cache Redis do Azure?
Não há nenhum emulador local para o Cache Redis do Azure, mas você pode executar a versão de MSOpenTech de saudação do redis server.exe de saudação [Redis ferramentas de linha de comando](https://github.com/MSOpenTech/redis/releases/) no local do computador e conecte-se tooit tooget um cache local do semelhante experiência tooa emulador do Windows, conforme mostrado no exemplo a seguir de saudação:

    private static Lazy<ConnectionMultiplexer>
          lazyConnection = new Lazy<ConnectionMultiplexer>
        (() =>
        {
            // Connect tooa locally running instance of Redis toosimulate a local cache emulator experience.
            return ConnectionMultiplexer.Connect("127.0.0.1:6379");
        });

        public static ConnectionMultiplexer Connection
        {
            get
            {
                return lazyConnection.Value;
            }
        }


Opcionalmente, você pode configurar um [conf](http://redis.io/topics/config) toomore arquivo aproximada Olá [configurações de cache padrão](cache-configure.md#default-redis-server-configuration) para o on-line Cache Redis do Azure se desejado.

<a name="cache-commands"></a>

### <a name="how-can-i-run-redis-commands"></a>Como posso executar comandos do Redis?
Você pode usar qualquer um dos comandos de saudação listados em [comandos do Redis](http://redis.io/commands#) , exceto os comandos Olá listados em [Redis comandos não tem suportados no Cache Redis do Azure](cache-configure.md#redis-commands-not-supported-in-azure-redis-cache). Há vários comandos de Redis toorun de opções.

* Se você tiver um cache Standard ou Premium, você pode executar comandos do Redis usando Olá [Console Redis](cache-configure.md#redis-console). console de Redis Olá fornece toorun uma maneira segura comandos do Redis no portal do Azure de saudação.
* Você também pode usar ferramentas de linha de comando do hello Redis. toouse-los, executar Olá seguintes etapas:
* Baixar Olá [Redis ferramentas de linha de comando](https://github.com/MSOpenTech/redis/releases/).
* Conecte-se usando o cache toohello `redis-cli.exe`. Passe no ponto de extremidade de cache de saudação usando a opção -h hello e Olá chave usando - a conforme mostrado no exemplo a seguir de saudação:
* `redis-cli -h <your cache="" name="">
  .redis.cache.windows.net -a <key>
  `

> [!NOTE]
> Olá ferramentas de linha de comando Redis não funcionam com hello porta SSL, mas você pode usar um utilitário como `stunnel` toosecurely se conectar a porta SSL do hello ferramentas toohello seguindo instruções Olá Olá [anunciando provedor ASP.NET de estado de sessão para Versão de visualização de redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx) postagem de blog.
>
>

<a name="cache-reference"></a>

### <a name="why-doesnt-azure-redis-cache-have-an-msdn-class-library-reference-like-some-of-hello-other-azure-services"></a>Por que o Cache Redis do Azure não tem uma referência de biblioteca de classe do MSDN como alguns da Olá outros serviços do Azure?
Cache Redis do Microsoft Azure é baseado em Olá populares de software livre Cache Redis e podem ser acessado por uma ampla variedade de [clientes Redis](http://redis.io/clients) para muitas linguagens de programação. Cada cliente tem sua própria API que faz chamadas toohello Redis cache instância usando [Redis comandos](http://redis.io/commands).

Como cada cliente é diferente, não há não uma referência de classe centralizada no MSDN, e cada cliente mantém sua própria documentação de referência. Além disso toohello documentação de referência, há vários tutoriais mostrando como tooget iniciada com o Cache Redis do Azure usando diferentes idiomas e clientes de cache. tooaccess esses tutoriais, consulte [como toouse Cache Redis do Azure](cache-dotnet-how-to-use-azure-redis-cache.md) e clique em idioma alternador de idioma Olá na parte superior de saudação do artigo Olá Olá desejado.

### <a name="can-i-use-azure-redis-cache-as-a-php-session-cache"></a>Posso usar o Cache Redis do Azure como um cache de sessão do PHP?
Sim, toouse Cache Redis do Azure como um cache de sessão do PHP, especifique a instância de Cache Redis do Azure de tooyour de cadeia de caracteres da conexão do hello em `session.save_path`.

> [!IMPORTANT]
> Ao usar o Cache Redis do Azure como um cache de sessão do PHP, você deve URL codificar Olá segurança chave tooconnect usado toohello de cache, conforme mostrado no exemplo a seguir de saudação:
>
> `session.save_path = "tcp://mycache.redis.cache.windows.net:6379?auth=<url encoded primary or secondary key here>";`
>
> Se a chave de saudação não for codificados de URL, você receberá uma exceção com uma mensagem como:`Failed tooparse session.save_path`
>
>

Para obter mais informações sobre como usar o Cache Redis como um cache de sessão do PHP com o cliente de PhpRedis hello, consulte [manipulador de sessão do PHP](https://github.com/phpredis/phpredis#php-session-handler).

### <a name="what-are-redis-databases"></a>Quais são os bancos de dados do Redis?

Bancos de dados do redis são apenas uma separação lógica de dados dentro de saudação mesma instância do Redis. a memória de cache Olá é compartilhada entre todos os bancos de dados de saudação e consumo de memória real de um determinado banco de dados depende de saudação chaves/valores armazenados no banco de dados. Por exemplo, um cache C6 tem 53 GB de memória. Você pode escolher tooput todos os 53 GB em um banco de dados ou você pode dividi-lo entre vários bancos de dados. 

> [!NOTE]
> Ao usar um Cache Redis do Azure Premium com cluster habilitado, somente o banco de dados 0 estará disponível. Essa limitação é uma limitação de Redis intrínseca e não é específico tooAzure Cache Redis. Para obter mais informações, consulte [preciso toomake qualquer toouse de aplicativo alterações toomy cliente clustering?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
> 
> 


<a name="cache-ssl"></a>

### <a name="when-should-i-enable-hello-non-ssl-port-for-connecting-tooredis"></a>Quando eu habilito a porta não SSL de saudação para conectar-se tooRedis?
Redis servidor não oferece suporte a SSL, mas não de Cache Redis do Azure. Se você estiver se conectando tooAzure Redis Cache e o cliente oferece suporte a SSL, como Stackexchange, você deve usar SSL.

>[!NOTE]
>porta do Hello não SSL está desabilitada por padrão para novas instâncias de Cache Redis do Azure. Se o cliente não oferece suporte a SSL, você deve habilitar a porta não SSL de saudação seguindo instruções Olá Olá [acessar portas](cache-configure.md#access-ports) seção Olá [configurar um cache no Cache Redis do Azure](cache-configure.md) artigo.
>
>

Redis ferramentas como `redis-cli` não funcionam com hello porta SSL, mas você pode usar um utilitário como `stunnel` toosecurely se conectar a porta SSL do hello ferramentas toohello seguindo instruções Olá Olá [anunciando provedor de estado de sessão do ASP.NET versão de visualização Redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx) postagem de blog.

Para obter instruções sobre como baixar Olá Redis ferramentas, consulte Olá [como executar comandos do Redis?](#cache-commands) seção.

### <a name="what-are-some-production-best-practices"></a>Quais são algumas práticas recomendadas de produção?
* [Práticas recomendadas do StackExchange.Redis](#stackexchangeredis-best-practices)
* [Configuração e conceitos](#configuration-and-concepts)
* [Testes de desempenho](#performance-testing)

#### <a name="stackexchangeredis-best-practices"></a>Práticas recomendadas do StackExchange.Redis
* Definir `AbortConnect` toofalse, deixe Olá ConnectionMultiplexer reconectar-se automaticamente. [Consulte aqui para obter detalhes](https://gist.github.com/JonCole/36ba6f60c274e89014dd#file-se-redis-setabortconnecttofalse-md).
* Reutilizar Olá ConnectionMultiplexer - não criar um novo para cada solicitação. Olá `Lazy<ConnectionMultiplexer>` padrão [mostrado aqui](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache) é recomendado.
* O Redis funciona melhor com valores menores, portanto, considere talhar dados maiores em várias chaves. Nesta [discussão do Redis](https://groups.google.com/forum/#!searchin/redis-db/size/redis-db/n7aa2A4DZDs/3OeEPHSQBAAJ), 100 kb é considerado grande. Leia [este artigo](https://gist.github.com/JonCole/db0e90bedeb3fc4823c2#large-requestresponse-size) para obter um problema de exemplo que pode ser causado por valores grandes.
* Configurar seu [ThreadPool configurações](#important-details-about-threadpool-growth) tempos limite de tooavoid.
* Use pelo menos Olá connectTimeout padrão de 5 segundos. Esse intervalo daria Stackexchange toore de tempo suficiente-estabelecer conexão hello, no caso de um blip de rede.
* Lembre-Olá custos de desempenho associados a operações diferentes que você está executando. Por exemplo, Olá `KEYS` comando é uma operação (n) e deve ser evitado. Olá [redis.io site](http://redis.io/commands/) tem detalhes sobre a complexidade de tempo de saudação para cada operação que ele suporta. Clique em cada complexidade de saudação do comando toosee para cada operação.

#### <a name="configuration-and-concepts"></a>Configuração e conceitos
* Use as camadas Standard ou Premium para Sistemas de Produção. Olá camada básica é um sistema de nó único com nenhuma replicação de dados e não há SLA. Além disso, use pelo menos um cache C1. Caches C0 normalmente são usados para cenários de desenvolvimento/teste simples.
* Lembre-se de que o Redis é um armazenamento de dados **na memória** . Leia [este artigo](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md) para que você fique ciente de situações em que pode haver perda de dados.
* Desenvolver seu sistema, de modo que pode lidar com pontos de luz de conexão [devido a failover e toopatching](https://gist.github.com/JonCole/317fe03805d5802e31cfa37e646e419d#file-azureredis-patchingexplained-md).

#### <a name="performance-testing"></a>Testes de desempenho
* Iniciar usando `redis-benchmark.exe` tooget uma ideia de taxa de transferência possível antes de gravar seus próprios testes de desempenho. Porque `redis-benchmark` não oferece suporte a SSL, você deve [habilitar porta Olá não SSL por meio do portal do Azure de saudação](cache-configure.md#access-ports) antes de executar o teste de saudação. Para obter exemplos, consulte [como avaliar o desempenho e teste Olá desempenho de meu cache?](#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* Olá cliente usado para teste de VM deve ser no hello mesma região que sua instância de cache Redis.
* É recomendável usar Dv2 série de VM para o cliente como eles têm melhor hardware e devem fornecer os melhores resultados de saudação.
* Verifique se o cliente que você escolher a VM possui pelo menos a quantidade de capacidade de computação e de largura de banda como cache de saudação que você está testando.
* Habilite o VRSS na máquina do cliente Olá se você estiver usando o Windows. [Consulte aqui para obter detalhes](https://technet.microsoft.com/library/dn383582.aspx).
* As instâncias do Redis nível Premium terão melhor latência de rede e taxa de transferência porque estão em execução tanto para a CPU quanto para a Rede.

<a name="cache-redis-commands"></a>

### <a name="what-are-some-of-hello-considerations-when-using-common-redis-commands"></a>Quais são algumas das considerações de saudação ao usar os comandos comuns do Redis?
* Você não deve executar alguns comandos do Redis que levar toocomplete um longo tempo, sem entender o impacto de saudação desses comandos.
  * Por exemplo, não execute Olá [chaves](http://redis.io/commands/keys) comando em produção, pode levar um tooreturn muito tempo, dependendo do número de saudação de chaves. O Redis é um servidor de thread único e processa um comando por vez. Se você tiver outros comandos emitidos depois de chaves, eles não serão processados até Redis processa o comando de teclas hello. Olá [redis.io site](http://redis.io/commands/) tem detalhes sobre a complexidade de tempo de saudação para cada operação que ele suporta. Clique em cada complexidade de saudação do comando toosee para cada operação.
* Tamanhos de chave - devo usar valores pequenos ou grandes de chave? Em geral, depende do cenário de saudação. Se seu cenário exigir chaves maiores, é possível ajustar Olá ConnectionTimeout e repita valores e ajustar sua lógica de repetição. Da perspectiva do servidor Redis, valores menores são observados toohave melhor desempenho.
* Essas considerações não significam que você não pode armazenar valores maiores no Redis; Você deve estar atento a saudação considerações a seguir. As latências serão maiores. Se você tiver um conjunto de dados maior e um menor, você pode usar várias instâncias de ConnectionMultiplexer, cada uma configurada com um conjunto diferente de valores de tempo limite e tente novamente, conforme descrito em Olá anterior [o que Olá Opções de configuração de Stackexchange](#cache-configuration) seção.

<a name="cache-benchmarking"></a>

### <a name="how-can-i-benchmark-and-test-hello-performance-of-my-cache"></a>Como avaliar o desempenho e teste Olá desempenho de meu cache?
* [Habilitar o diagnóstico de cache](cache-how-to-monitor.md#enable-cache-diagnostics) para que você possa [monitor](cache-how-to-monitor.md) Olá a integridade do cache. Você pode exibir uma saudação métricas em hello portal do Azure e você também podem [Baixe e leia](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) -los usando as ferramentas de saudação de sua escolha.
* Você pode usar seu servidor Redis para teste de tooload benchmark.exe redis.
* Verifique se o cliente de teste de carga hello e cache de Redis Olá estão em Olá mesma região.
* Use redis cli.exe e monitorar o cache de saudação usando o comando de informações de saudação.
* Se sua carga está causando a fragmentação de memória alta, você deve aumentar o tamanho de cache maior tooa.
* Para obter instruções sobre como baixar Olá Redis ferramentas, consulte Olá [como executar comandos do Redis?](#cache-commands) seção.

Olá comandos a seguir fornecem um exemplo de uso benchmark.exe redis. Para obter resultados precisos, execute estes comandos de uma VM em Olá mesma região do seu cache.

* Teste solicitações SET de Pipeline usando um conteúdo de 1k

  `redis-benchmark.exe -h **yourcache**.redis.cache.windows.net -a **yourAccesskey** -t SET -n 1000000 -d 1024 -P 50`
* Solicitações GET de Pipelined usando uma conteúdo de 1k.
  Observação: Executar o teste de conjunto de saudação mostrado acima primeiro cache toopopulate

  `redis-benchmark.exe -h **yourcache**.redis.cache.windows.net -a **yourAccesskey** -t GET -n 1000000 -d 1024 -P 50`

<a name="threadpool"></a>

### <a name="important-details-about-threadpool-growth"></a>Detalhes importantes sobre o crescimento de ThreadPool
Olá CLR ThreadPool tem dois tipos de threads - "Trabalho" e "Porta de conclusão de e/s" (também conhecido como IOCP) de threads.

* Os threads de trabalho são usados em situações como o processamento dos métodos `Task.Run(…)` ou `ThreadPool.QueueUserWorkItem(…)`. Esses threads também são usados por vários componentes no hello CLR quando as necessidades de trabalho toohappen em um thread em segundo plano.
* Threads IOCP são usadas quando acontecer de e/s assíncrona (por exemplo, lendo da rede Olá).

o pool de threads Olá fornece novos threads de trabalho ou threads de conclusão de e/s sob demanda (sem qualquer limitação) até atingir a configuração de "Mínimo" Olá para cada tipo de segmento. Por padrão, o número mínimo de saudação de threads é definido toohello número de processadores em um sistema.

Uma vez Olá inúmeros existente (ocupado) threads acertos hello "" número mínimo de threads, Olá ThreadPool será taxa de aceleração Olá no qual ele insere um novo thread tooone de threads por 500 milissegundos. Geralmente, se seu sistema obtiver um pico de trabalho que precisa de um thread IOCP, ele processará esse trabalho muito rapidamente. No entanto, se o disparo de saudação do trabalho é maior do que Olá definido a configuração de "Mínimo", haverá algum atraso no processamento de parte do trabalho hello como hello ThreadPool aguarda uma das duas coisas toohappen.

1. Um thread existente torna-se livre tooprocess Olá trabalho.
2. Nenhum thread existente ficar livre para 500 ms, o que leva à criação de outro thread.

Basicamente, isso significa que quando o número Olá de threads ocupados for maior que o mínimo de threads, você estiver pagando provavelmente um atraso de 500 ms antes do tráfego de rede é processado pelo aplicativo hello. Além disso, é importante toonote que, quando um existente thread permanece inativo por mais de 15 segundos (com base no qual lembro), ele será limpo e repita esse ciclo de crescimento e a redução.

Se examinarmos um exemplo de mensagem de erro do StackExchange.Redis (versão 1.0.450 ou posterior), você verá que agora ela imprime estatísticas de ThreadPool (confira os detalhes de TRABALHO e IOCP abaixo).

    System.TimeoutException: Timeout performing GET MyKey, inst: 2, mgr: Inactive,
    queue: 6, qu: 0, qs: 6, qc: 0, wr: 0, wq: 0, in: 0, ar: 0,
    IOCP: (Busy=6,Free=994,Min=4,Max=1000),
    WORKER: (Busy=3,Free=997,Min=4,Max=1000)

No exemplo anterior de saudação, você pode ver que há 6 threads ocupados do thread IOCP e sistema de saudação está configurado tooallow 4 mínimo de threads. Nesse caso, o cliente de saudação provavelmente veria dois atrasos de 500 ms porque 6 > 4.

Observe que o StackExchange.Redis poderá atingir tempos limite se o crescimento de threads de TRABALHO ou IOCP for limitado.

### <a name="recommendation"></a>Recomendações
Dadas essas informações, é altamente recomendável que os clientes definirem valor de configuração mínima de saudação para toosomething de threads de trabalho e IOCP maior do que o valor padrão de saudação. Podemos dar orientação que sirva no qual esse valor deve ser porque o valor de saudação à direita de um aplicativo será muito alta/baixa para outro aplicativo. Essa configuração também pode afetar o desempenho de saudação de outras partes do aplicativos complicados, para que cada cliente precisa ajustar toofine que este tootheir configuração específica precisa. Um bom ponto de partida é 200 ou 300, para testar e ajustar conforme necessário.

Como tooconfigure essa configuração:

* No ASP.NET, use Olá ["minIoThreads" configuração] [ "minIoThreads" configuration setting] em Olá `<processModel>` elemento de configuração no Web. config. Se você estiver executando dentro de sites do Azure, essa configuração não é exposta por meio de opções de configuração de saudação. No entanto, você ainda deverá ser capaz de tooconfigure essa configuração por meio de programação (veja abaixo) de seu método Application_Start em global.asax.cs.

  > [!NOTE] 
  > Olá valor especificado neste elemento de configuração é um *por núcleo* configuração. Por exemplo, se você tiver uma máquina de 4 núcleos e quiser toobe sua configuração de minIOThreads 200 em tempo de execução, você usaria `<processModel minIoThreads="50"/>`.
  >

* Fora do ASP.NET, use Olá [ThreadPool.SetMinThreads(...) ](https://msdn.microsoft.com/library/system.threading.threadpool.setminthreads.aspx) API.

<a name="server-gc"></a>

### <a name="enable-server-gc-tooget-more-throughput-on-hello-client-when-using-stackexchangeredis"></a>Habilitar servidor GC tooget mais taxa de transferência no cliente hello usando stackexchange. Redis
Habilitar um servidor GC pode otimizar o cliente hello e fornecer melhor desempenho e taxa de transferência ao usar stackexchange. Redis. Para obter mais informações sobre servidor GC e como tooenable, consulte Olá artigos a seguir:

* [tooenable servidor GC](https://msdn.microsoft.com/library/ms229357.aspx)
* [Noções básicas sobre a coleta de lixo](https://msdn.microsoft.com/library/ee787088.aspx)
* [Coleta de lixo e desempenho](https://msdn.microsoft.com/library/ee851764.aspx)


### <a name="performance-considerations-around-connections"></a>Considerações sobre desempenho em torno de conexões

Cada tipo de preço tem limites diferentes para conexões de cliente, memória e largura de banda. Embora cada tamanho de cache permite que *até* um determinado número de conexões, tooRedis cada conexão tem sobrecarga associados a ele. Um exemplo de tal sobrecarga seria o uso da CPU e de memória como resultado de criptografia TLS/SSL. limite de conexão máximo Olá para um tamanho de cache determinado pressupõe um cache pouco carregado. Se carregar de sobrecarga de conexão *mais* carga a partir de operações do cliente excede a capacidade de sistema hello, cache Olá pode enfrentar problemas de capacidade, mesmo se você não tiver excedido o limite de conexão de saudação para o tamanho do cache atual hello.

Para obter mais informações sobre os limites de diferentes conexões Olá para cada camada, consulte [preço do Cache Redis do Azure](https://azure.microsoft.com/pricing/details/cache/). Para obter mais informações sobre as conexões e outras configurações padrão, consulte [configuração do servidor padrão Redis](cache-configure.md#default-redis-server-configuration).

<a name="cache-monitor"></a>

### <a name="how-do-i-monitor-hello-health-and-performance-of-my-cache"></a>Como monitorar integridade hello e o desempenho do meu cache?
Instâncias do Microsoft Azure Redis Cache podem ser monitoradas no hello [portal do Azure](https://portal.azure.com). Você pode exibir métricas, fixar gráficos de métricas toohello quadro inicial, personalizar o intervalo de data e hora de saudação de gráficos de monitoramento, adicionar e remover as métricas de gráficos de saudação e definir alertas quando determinadas condições forem atendidas. Para saber mais, veja [Como monitorar o Cache Redis do Azure](cache-how-to-monitor.md).

Olá Cache Redis **menu recursos** também contém várias ferramentas para monitorar e solucionar problemas de seus caches.

* **Diagnosticar e solucionar problemas** fornece informações sobre problemas comuns e estratégias para resolvê-los.
* **Resource Health** observa seu recurso e informa se ele está sendo executado conforme o esperado. Para obter mais informações sobre Olá serviço de integridade de recursos do Azure, consulte [visão geral da integridade do recurso Azure](../resource-health/resource-health-overview.md).
* **Nova solicitação de suporte** fornece opções tooopen uma solicitação de suporte para seu cache.

Essas ferramentas permitem a você toomonitor Olá integridade das instâncias de Cache Redis do Azure e ajudarão-lo a gerenciar seus aplicativos de cache. Para obter mais informações, consulte a seção de "Configurações de solução de problemas e suporte" de saudação do [como tooconfigure Cache Redis do Azure](cache-configure.md).

<a name="cache-timeouts"></a>

### <a name="why-am-i-seeing-timeouts"></a>Por que vejo tempos limite?
Tempos limite ocorrer no cliente de saudação que você use tootalk tooRedis. Quando um comando é enviado toohello Redis server, comando Olá na fila e servidor Redis eventualmente pega comando hello e executa-o. No entanto cliente Olá pode atingir o tempo limite durante este processo e se ele faz uma exceção é gerado em Olá chamando lado. Para saber mais sobre como solucionar problemas de tempo limite, consulte [Solução de problemas do lado do cliente](cache-how-to-troubleshoot.md#client-side-troubleshooting) e [Exceções de tempo limite do StackExchange.Redis](cache-how-to-troubleshoot.md#stackexchangeredis-timeout-exceptions).

<a name="cache-disconnect"></a>

### <a name="why-was-my-client-disconnected-from-hello-cache"></a>Por que meu cliente foi desconectado do cache Olá?
Olá seguem alguns motivo comum para uma desconexão do cache.

* Motivos no lado do cliente
  * aplicativo de cliente Hello foi reimplantado.
  * aplicativo de cliente Hello executou uma operação de escala.
    * No caso de saudação de serviços de nuvem ou aplicativos Web, isso pode ser devido tooauto dimensionamento.
  * camada de rede Olá Olá do lado do cliente alterada.
  * Erros transitórios ocorreram no cliente de saudação ou em nós de rede Olá entre cliente hello e servidor de saudação.
  * limites de largura de banda Olá foram atingidos.
  * CPU associada operações levou toocomplete muito longo.
* Motivos no lado do servidor
  * No hello oferta de cache standard, Olá serviço de Cache Redis do Azure iniciado um failover de nó secundário do toohello Olá nó primário.
  * Azure foi patches instância Olá onde o cache de saudação foi implantado
    * Isso pode ser para atualizações de servidor do Redis ou manutenção geral de VM.

### <a name="which-azure-cache-offering-is-right-for-me"></a>Qual oferta de Cache do Azure é a correta para mim?
> [!IMPORTANT]
> De acordo com o [comunicado](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/) do ano passado, o Serviço de Cache Gerenciado do Azure e o serviço Cache na Função do Azure **foram desativados** em 30 de novembro de 2016. Nossa recomendação é toouse [Cache Redis do Azure](https://azure.microsoft.com/services/cache/). Para obter informações sobre a migração, consulte [migração do serviço de Cache gerenciado tooAzure Cache Redis](cache-migrate-to-redis.md).
>
>

### <a name="azure-redis-cache"></a>Cache Redis do Azure
Cache Redis do Azure está disponível em tamanhos de too53 GB e tem um SLA de 99,9% de disponibilidade. Olá novo [camada premium](cache-premium-tier-intro.md) oferece tamanhos too530 GB e suporte para clustering, redes e persistência, com um SLA de 99,9%.

Azure Redis Cache fornece clientes Olá capacidade toouse um cache Redis seguro e dedicado, gerenciado pela Microsoft. Com essa oferta, você pode obter tooleverage Olá sofisticado conjunto de recursos e o ecossistema fornecidos pelo Redis e confiável de hospedagem e monitoramento da Microsoft.

Diferentemente dos caches tradicionais que lidam exclusivamente com pares chave-valor, o Redis é popular por seus tipos de dados altamente funcionais. O redis também permite executar operações atômicas nesses tipos, como anexar a cadeia de caracteres tooa; valor de incremento Olá em um hash; enviar a lista de tooa; Calculando a interseção, união e diferença; ou membro de obtenção Olá com classificação mais alta em um conjunto ordenado. Outros recursos incluem suporte para transações, pub/sub, scripts Lua, chaves com um tempo de vida de limitado e configuração configurações toomake Redis se comportar mais como um cache tradicional.

Êxito de tooRedis outro aspecto fundamental é Olá saudável e vibrante ecossistema construído ao redor dele. Isso é refletido no conjunto diversificado de saudação de clientes Redis disponíveis em vários idiomas. Esse ecossistema e uma ampla gama de clientes permitem toobe Cache Redis do Azure usado por praticamente qualquer carga de trabalho construída dentro do Azure.

Para obter mais informações sobre como começar com o Cache Redis do Azure, consulte [como tooUse Cache Redis do Azure](cache-dotnet-how-to-use-azure-redis-cache.md) e [documentação do Cache Redis do Azure](index.md).

### <a name="managed-cache-service"></a>Serviço de Cache gerenciado
[O serviço de Cache Gerenciado foi descontinuado em 30 de novembro de 2016.](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)

tooview arquivado documentação, consulte [arquivados gerenciados documentação de serviço de Cache](https://msdn.microsoft.com/library/azure/dn386094.aspx).

### <a name="in-role-cache"></a>Cache em Função
[Cache na função foi descontinuado em 30 de novembro de 2016.](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)

tooview arquivado documentação, consulte [arquivados documentação de Cache na função](https://msdn.microsoft.com/library/azure/dn386103.aspx).

["minIoThreads" configuration setting]: https://msdn.microsoft.com/library/vstudio/7w2sway1(v=vs.100).aspx
