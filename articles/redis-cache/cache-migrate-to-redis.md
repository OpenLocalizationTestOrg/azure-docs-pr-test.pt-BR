---
title: "aaaMigrate tooRedis de aplicativos do serviço de Cache gerenciado - Azure | Microsoft Docs"
description: "Saiba como toomigrate aplicativos de serviço de Cache gerenciado e o Cache na função tooAzure Cache Redis"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 041f077b-8c8e-4d7c-a3fc-89d334ed70d6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 05/30/2017
ms.author: sdanie
ms.openlocfilehash: bd81722820acf0d2637828fbb6100c723aafeba5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-managed-cache-service-tooazure-redis-cache"></a>Migrar do serviço de Cache gerenciado tooAzure Cache Redis
Migrar seus aplicativos que usam o serviço de Cache gerenciado do Azure tooAzure Redis Cache pode ser feito com o aplicativo de tooyour alterações mínimas, dependendo dos recursos do serviço de Cache gerenciado Olá usado pelo seu aplicativo em cache. Embora Olá APIs não são exatamente Olá mesmo que eles são semelhantes e grande parte do seu código existente que usa o serviço de Cache gerenciado tooaccess um cache pode ser reutilizado com poucas alterações. Este tópico mostra como configuração de aplicativo e toomake Olá necessárias alterações toomigrate seu aplicativos de serviço de Cache gerenciado toouse Cache Redis do Azure e mostra como alguns dos recursos de saudação do Cache Redis do Azure podem ser usado tooimplement Olá funcionalidade de um cache de serviço de Cache gerenciado.

>[!NOTE]
>Serviço de Cache Gerenciado e na Cache na Função foram [desativados](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/) em 30 de novembro de 2016. Se você tiver as implantações de Cache na função que você deseja toomigrate tooAzure Redis Cache, você pode seguir as etapas de saudação neste artigo.

## <a name="migration-steps"></a>Etapas da migração
Olá etapas a seguir é necessária toomigrate um aplicativo de serviço de Cache gerenciado toouse Cache Redis do Azure.

* Mapa de recursos de serviço de Cache gerenciado tooAzure Cache Redis
* Escolher uma oferta de Cache
* Criar um Cache
* Configurar clientes de Cache Olá
  * Remover configuração de serviço de Cache gerenciado do hello
  * Configurar um cliente de cache usando Olá pacote do NuGet stackexchange. Redis
* Migrar o código do Serviço de Cache Gerenciado
  * Conecte-se usando a classe ConnectionMultiplexer de saudação do cache de toohello
  * Tipos de dados primitivos de acesso no cache de saudação
  * Trabalhar com objetos .NET no cache de saudação
* Migrar o estado da sessão ASP.NET e cache tooAzure Redis Cache de saída 

## <a name="map-managed-cache-service-features-tooazure-redis-cache"></a>Mapa de recursos de serviço de Cache gerenciado tooAzure Cache Redis
Serviço de Cache Gerenciado do e Cache Redis do Azure são semelhantes, mas implementam alguns dos seus recursos de maneiras diferentes. Esta seção descreve algumas das diferenças de saudação e fornece orientação sobre como implementar recursos de saudação do serviço de Cache gerenciado no Cache Redis do Azure.

| Recurso do Serviço de Cache Gerenciado | Suporte do Serviço de Cache Gerenciado | Suporte do Cache Redis do Azure |
| --- | --- | --- |
| Caches nomeados |Um cache padrão está configurado e em Olá Standard e Premium ofertas de cache, o toonine adicional caches nomeadas podem ser configuradas se desejado. |Caches Redis do Azure tem um número configurável de bancos de dados (padrão de 16) que pode ser usado tooimplement armazena em cache uma toonamed funcionalidade semelhante. Para saber mais, veja [O que são os bancos de dados do Redis?](cache-faq.md#what-are-redis-databases) e [Configuração padrão do servidor Redis](cache-configure.md#default-redis-server-configuration). |
| Alta disponibilidade |Fornece alta disponibilidade para itens no cache de saudação nas ofertas de cache Standard e Premium Olá. Se os itens são perdidos devido a falha de tooa, cópias de backup de itens de saudação no cache de saudação ainda estão disponíveis. Grava o cache secundário toohello são feitas de forma síncrona. |Alta disponibilidade está disponível no hello Standard e Premium ofertas de cache, que têm uma configuração principal/réplica de dois nós (cada fragmento em um cache Premium tem um par primário/réplica). Gravações toohello réplica são feitas de forma assíncrona. Para obter mais informações, confira [Preço do Cache Redis do Azure](https://azure.microsoft.com/pricing/details/cache/). |
| Notificações |Permite que os clientes tooreceive notificações assíncronas quando várias operações de cache ocorrem em um cache nomeado. |Aplicativos cliente podem usar pub/sub Redis ou [notificações Keyspace](cache-configure.md#keyspace-notifications-advanced-settings) tooachieve um toonotifications funcionalidade semelhante. |
| Cache local |Armazena uma cópia dos objetos armazenados em cache localmente no cliente Olá para acesso extremamente rápido. |Aplicativos cliente precisaria tooimplement essa funcionalidade usando um dicionário ou uma estrutura de dados semelhantes. |
| Política de remoção |Nenhuma ou LRU. política do saudação padrão é LRU. |Cache Redis do Azure oferece suporte a saudação políticas de remoção a seguir: volatile-lru, allkeys-lru, ttl de volátil volátil aleatório, allkeys aleatório, noeviction. política do saudação padrão é volatile-lru. Para obter mais informações, confira [Configuração padrão do servidor Redis](cache-configure.md#default-redis-server-configuration). |
| Política de expiração |política de expiração saudação padrão é absoluta e o intervalo de expiração saudação padrão é de dez minutos. As políticas Sliding e Never também estão disponíveis. |Por padrão a itens no cache de saudação não expiram, mas uma expiração pode ser configurada em uma base por gravação usando sobrecargas de conjunto de cache. Para obter mais informações, consulte [adicionar e recuperar objetos do cache de saudação](cache-dotnet-how-to-use-azure-redis-cache.md#add-and-retrieve-objects-from-the-cache). |
| Regiões e marcação |As regiões são subgrupos para itens em cache. Regiões também oferecem suporte a anotação de saudação de itens em cache com adicionais cadeias de caracteres descritivas denominadas marcas. Regiões oferecem suporte a operações de pesquisa de tooperform Olá capacidade em qualquer item marcado nessa região. Todos os itens dentro de uma região são localizados em um único nó de cluster de cache de saudação. |Um cache Redis consiste em um único nó (a menos que o cluster Redis estiver habilitada) para que o conceito de saudação de regiões do serviço de Cache gerenciado não se aplica. O redis oferece suporte à pesquisa e operações curingas ao recuperar chaves para que as marcas descritivas podem ser inseridas em nomes de chave hello e usado itens de saudação tooretrieve posteriormente. Para obter um exemplo de implementação de uma solução de marcação usando Redis, consulte [Implementar marcação de cache com Redis](http://stackify.com/implementing-cache-tagging-redis/). |
| Serialização |Cache gerenciado suporta NetDataContractSerializer, BinaryFormatter e uso de saudação de serializadores personalizados. saudação padrão é NetDataContractSerializer. |É responsabilidade de Olá Olá cliente tooserialize .NET de objetos do aplicativo antes de colocá-los no cache de hello, com a opção de saudação do serializador Olá o desenvolvedor do aplicativo cliente toohello. Para obter mais informações e exemplo de código, consulte [trabalhar com objetos .NET no cache de saudação](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache). |
| Emulador de cache |O Cache Gerenciado fornece um emulador de cache local. |Cache Redis do Azure não tem um emulador, mas você pode [executados localmente o build de MSOpenTech de saudação do redis server.exe](cache-faq.md#cache-emulator) tooprovide uma experiência de emulador. |

## <a name="choose-a-cache-offering"></a>Escolher uma oferta de Cache
Cache Redis do Microsoft Azure está disponível em Olá níveis a seguir:

* **Básico** – um único nó. Vários tamanhos de backup too53 GB.
* **Standard** – principal/réplica com dois nós. Vários tamanhos de backup too53 GB. SLA de 99,9%.
* **Premium** – dois nós primário/réplica, com backup too10 fragmentos. Vários tamanhos de 6 GB too530 GB. Todos os recursos do tipo Standard e outros, incluindo suporte para [cluster Redis](cache-how-to-premium-clustering.md), [persistência Redis](cache-how-to-premium-persistence.md) e [Rede Virtual do Azure](cache-how-to-premium-vnet.md). SLA de 99,9%.

Cada camada é diferente em termos de recursos e preços. Olá recursos são abordados posteriormente neste guia e para obter mais informações sobre preços, consulte [detalhes de preços de Cache](https://azure.microsoft.com/pricing/details/cache/).

Um ponto de partida para a migração é toopick Olá tamanho que coincida com tamanho de saudação do seu cache anterior do serviço de Cache gerenciado e, em seguida, expandir ou reduzir, dependendo dos requisitos de saudação do seu aplicativo. Para obter instruções sobre como escolher a oferta certa de Cache Redis do Azure hello, consulte [qual oferta de Cache do Redis e tamanho devo usar?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).

## <a name="create-a-cache"></a>Criar um Cache
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="configure-hello-cache-clients"></a>Configurar clientes de Cache Olá
Depois que o cache de saudação é criada e configurada, Olá próxima etapa é a configuração de serviço de Cache gerenciado do tooremove Olá e adicionar Olá Adicionar configuração de Cache Redis do Azure hello e referências para que os clientes de cache possam acessar o cache de saudação.

* Remover configuração de serviço de Cache gerenciado do hello
* Configurar um cliente de cache usando Olá pacote do NuGet stackexchange. Redis

### <a name="remove-hello-managed-cache-service-configuration"></a>Remover configuração de serviço de Cache gerenciado do hello
Para Olá aplicativos cliente possam ser configurados para Cache Redis do Azure, configuração de serviço de Cache gerenciado existente hello e referências de assembly devem ser removidas Desinstalando o pacote do NuGet do serviço de Cache gerenciado hello.

Olá toouninstall pacote NuGet do serviço de Cache gerenciado, clique com botão direito Olá cliente em **Solution Explorer** e escolha **gerenciar pacotes NuGet**. Selecione Olá **pacotes instalados** nó e tipo W**indowsAzure.Caching** em Olá pesquisa instalado caixa pacotes. Selecione **Windows** **Cache do Azure** (ou **Windows** **cache do Azure** dependendo da versão de saudação do pacote do NuGet Olá), clique em  **Desinstalar**e, em seguida, clique em **fechar**.

![Desinstalar o pacote NuGet do Serviço de Cache Gerenciado do Azure](./media/cache-migrate-to-redis/IC757666.jpg)

Desinstalar pacote de NuGet de serviço de Cache gerenciado Olá remove assemblies do serviço de Cache gerenciado hello e entradas do serviço de Cache gerenciado Olá Olá App. config ou Web. config do aplicativo de cliente hello. Como algumas configurações personalizadas não podem ser removidas quando você desinstala o pacote do NuGet hello, abra Web. config ou App. config e certifique-se de que Olá elementos a seguir foram completamente removidos.

Certifique-se de que Olá `dataCacheClients` entrada será removida da saudação `configSections` elemento. Não remova todo Olá `configSections` elemento; basta remover Olá `dataCacheClients` entrada, se estiver presente.

```xml
<configSections>
  <!-- Existing sections omitted for clarity. -->
  <section name="dataCacheClients"type="Microsoft.ApplicationServer.Caching.DataCacheClientsSection, Microsoft.ApplicationServer.Caching.Core" allowLocation="true" allowDefinition="Everywhere"/>
</configSections>
```

Certifique-se de que Olá `dataCacheClients` seção é removida. Olá `dataCacheClients` seção será semelhante toohello exemplo a seguir.

```xml
<dataCacheClients>
  <dataCacheClientname="default">
    <!--toouse hello in-role flavor of Azure Cache, set identifier toobe hello cache cluster role name -->
    <!--toouse hello Azure Managed Cache Service, set identifier toobe hello endpoint of hello cache cluster -->
    <autoDiscoverisEnabled="true"identifier="[Cache role name or Service Endpoint]"/>

    <!--<localCache isEnabled="true" sync="TimeoutBased" objectCount="100000" ttlValue="300" />-->
    <!--Use this section toospecify security settings for connecting tooyour cache. This section is not required if your cache is hosted on a role that is a part of your cloud service. -->
    <!--<securityProperties mode="Message" sslEnabled="true">
      <messageSecurity authorizationInfo="[Authentication Key]" />
    </securityProperties>-->
  </dataCacheClient>
</dataCacheClients>
```

Depois que a configuração do serviço de Cache gerenciado Olá for removida, você pode configurar o cliente de cache Olá conforme descrito em Olá seção a seguir.

### <a name="configure-a-cache-client-using-hello-stackexchangeredis-nuget-package"></a>Configurar um cliente de cache usando Olá pacote do NuGet stackexchange. Redis
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

## <a name="migrate-managed-cache-service-code"></a>Migrar o código do Serviço de Cache Gerenciado
Olá API cliente de cache Stackexchange Olá é semelhante toohello serviço de Cache gerenciado. Esta seção fornece uma visão geral das diferenças de saudação.

### <a name="connect-toohello-cache-using-hello-connectionmultiplexer-class"></a>Conecte-se usando a classe ConnectionMultiplexer de saudação do cache de toohello
No serviço de Cache gerenciado, o cache de toohello conexões foram manipuladas pelo Olá `DataCacheFactory` e `DataCache` classes. No Cache Redis do Azure, essas conexões são gerenciadas pelo Olá `ConnectionMultiplexer` classe.

Adicione o seguinte Olá usando a instrução toohello superior de qualquer arquivo do qual você deseja tooaccess Olá cache.

```c#
using StackExchange.Redis
```

Se esse namespace não for resolvido, certifique-se de que você adicionou Olá pacote NuGet Stackexchange conforme descrito em [configurar clientes de cache Olá](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).

> [!NOTE]
> Observe que o cliente Stackexchange Olá requer o .NET Framework 4 ou superior.
> 
> 

instância de Cache Redis do Azure tooan tooconnect, chamada hello estático `ConnectionMultiplexer.Connect` método e passar no ponto de extremidade de saudação e a chave. Uma abordagem toosharing um `ConnectionMultiplexer` instância em seu aplicativo é toohave uma propriedade estática que retorna uma instância conectada, semelhante toohello exemplo a seguir. Isso fornece uma forma thread-safe tooinitialize apenas um único conectado `ConnectionMultiplexer` instância. Neste exemplo `abortConnect` é toofalse de conjunto, o que significa que a chamada de saudação será bem-sucedida mesmo se um cache de toohello de conexão não for estabelecido. Um recurso importante do `ConnectionMultiplexer` é que ele automaticamente restaura a cache de toohello conectividade depois que o problema de rede hello ou outras causas são resolvidas.

```c#
private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
{
    return ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
});

public static ConnectionMultiplexer Connection
{
    get
    {
        return lazyConnection.Value;
    }
}
```

Olá portas, chaves e ponto de extremidade do cache podem ser obtidas Olá **Redis Cache** folha para a instância de cache. Para obter mais informações, consulte as [Propriedades do Cache Redis](cache-configure.md#properties).

Após o estabelecimento de conexão hello, retornar um banco de dados referência toohello Redis cache por chamada hello `ConnectionMultiplexer.GetDatabase` método. objeto Olá retornado de saudação `GetDatabase` método é um objeto de passagem leve e não precisa toobe armazenado.

```c#
IDatabase cache = Connection.GetDatabase();

// Perform cache operations using hello cache object...
// Simple put of integral data types into hello cache
cache.StringSet("key1", "value");
cache.StringSet("key2", 25);

// Simple get of data types from hello cache
string key1 = cache.StringGet("key1");
int key2 = (int)cache.StringGet("key2");
```

cliente de Stackexchange Olá usa Olá `RedisKey` e `RedisValue` tipos para acessar e armazenar itens no cache de saudação. Esses tipos mapeiam para tipos de linguagem mais primitivos, incluindo a cadeia de caracteres e geralmente não são usados diretamente. Redis cadeias de caracteres são o tipo mais básico de saudação do valor do Redis e podem conter muitos tipos de dados, incluindo fluxos de binários serializados e enquanto você não pode usar o tipo de saudação diretamente, você usará métodos que contêm `String` em nome de saudação. Para tipos de dados primitivos mais você pode armazenar e recuperar itens do cache de saudação usando Olá `StringSet` e `StringGet` métodos, a menos que você está armazenando coleções ou outros tipos de dados Redis no cache de saudação. 

`StringSet`e `StringGet` são muito semelhante toohello serviço de Cache gerenciado `Put` e `Get` métodos, com uma grande diferença de que antes de definir e obter um objeto .NET no cache de saudação necessário serializá-lo primeiro. 

Ao chamar `StringGet`, se o objeto de saudação existir, ele é retornado e se não estiver, null será retornado. Nesse caso, você pode recuperar o valor de Olá Olá desejado da fonte de dados e armazená-la no cache de saudação para uso posterior. Isso é conhecido como padrão de cache-aside hello.

expiração de saudação toospecify de um item no cache de hello, use Olá `TimeSpan` parâmetro `StringSet`.

```c#
cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));
```

O Cache Redis do Azure pode trabalhar com objetos .NET, bem como tipos de dados primitivos, mas antes que um objeto .NET possa ser armazenado em cache, ele deve ser serializado. Isso é responsabilidade de saudação do desenvolvedor do aplicativo hello. Isso fornece flexibilidade de desenvolvedor de saudação na escolha de saudação do serializador hello. Para obter mais informações e exemplo de código, consulte [trabalhar com objetos .NET no cache de saudação](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).

## <a name="migrate-aspnet-session-state-and-output-caching-tooazure-redis-cache"></a>Migrar o estado da sessão ASP.NET e cache tooAzure Redis Cache de saída
O Cache Redis do Azure possui provedores de Estado da Sessão ASP.NET e o caching de Saída de Página. toomigrate seu aplicativo que usa versões do serviço de Cache gerenciado Olá desses provedores, primeiro remova Olá seções existentes do Web. config e, em seguida, configurar versões do Cache Redis do Azure de saudação dos provedores de saudação. Para obter instruções sobre como usar o hello provedores ASP.NET de Cache Redis do Azure, consulte [provedor de estado de sessão do ASP.NET para Cache Redis do Azure](cache-aspnet-session-state-provider.md) e [provedor de Cache de saída do ASP.NET para Cache Redis do Azure](cache-aspnet-output-cache-provider.md).

## <a name="next-steps"></a>Próximas etapas
Explorar Olá [documentação do Cache Redis do Azure](https://azure.microsoft.com/documentation/services/cache/) tutoriais, exemplos, vídeos e muito mais.

