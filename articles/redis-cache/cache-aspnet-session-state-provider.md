---
title: "Provedor de estado de sessão do ASP.NET de aaaCache | Microsoft Docs"
description: "Saiba como o estado de sessão ASP.NET toostore usando o Cache Redis do Azure"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 192f384c-836a-479a-bb65-8c3e6d6522bb
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 05/01/2017
ms.author: sdanie
ms.openlocfilehash: 9ea84cf67b9314b15dce696f596d399921194510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-session-state-provider-for-azure-redis-cache"></a>Provedor de estado de sessão ASP.NET para Cache Redis do Azure
Cache Redis do Azure fornece um provedor de estado de sessão que você pode usar toostore o estado da sessão em cache em vez de na memória ou em um SQL Server do banco de dados. toouse Olá cache provedor de estado de sessão, primeiro configure seu cache e, em seguida, configurar seu aplicativo ASP.NET para o cache usando o pacote de NuGet de estado de sessão de Cache Redis hello.

Geralmente não é prático em um tooavoid do aplicativo de nuvem do mundo real armazenamento de alguma forma de estado para uma sessão de usuário, mas algumas abordagens afetam o desempenho e escalabilidade mais do que outras pessoas. Se você tiver toostore estado, o hello melhor solução é tookeep Olá quantidade do estado pequeno e armazená-lo em cookies. Se isso não for viável, Olá próxima melhor solução é toouse estado da sessão ASP.NET com um provedor de cache distribuído na memória. a pior solução Olá de um ponto de vista de desempenho e escalabilidade é toouse um provedor de estado de sessão de backup do banco de dados. Este tópico fornece orientação sobre como usar o hello provedor de estado de sessão do ASP.NET para Cache Redis do Azure. Para saber mais sobre outras opções de estado de sessão, consulte [Opções de estado da sessão ASP.NET](#aspnet-session-state-options).

## <a name="store-aspnet-session-state-in-hello-cache"></a>Armazenar o estado da sessão ASP.NET no cache de saudação
tooconfigure um aplicativo cliente no Visual Studio usando o pacote de NuGet de estado de sessão de Cache Redis hello, clique em **NuGet Package Manager**, **Package Manager Console** de saudação **ferramentas** menu.

Execução hello seguinte comando do hello `Package Manager Console` janela.
    
```
Install-Package Microsoft.Web.RedisSessionStateProvider
```

> [!IMPORTANT]
> Se você estiver usando Olá recurso de clustering de camada de premium Olá, você deve usar [RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 ou superior ou uma exceção será lançada. Movendo too2.0.1 ou superior é uma alteração significativa; Para obter mais informações, consulte [v 2.0.0 detalhes de alteração de quebra](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details). Em tempo de saudação dessa atualização de artigo, a versão atual Olá deste pacote é 2.2.3.
> 
> 

pacote de NuGet de provedor de estado de sessão Redis Olá tem uma dependência Olá pacote Stackexchange. Se o pacote de Stackexchange Olá não está presente no seu projeto, ele é instalado.

>[!NOTE]
>Em adição toohello fortes Stackexchange pacote, também há Olá Stackexchange não-versão de nome forte. Se seu projeto está usando Olá não-versão de nome forte Stackexchange que você deve desinstalá-lo, caso contrário você conflitos de nomenclatura no projeto. Para saber mais sobre esses pacotes, consulte [Configurar clientes de cache .NET](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).
>
>

Olá NuGet pacote baixa e adiciona Olá necessário assembly faz referência e adiciona Olá seção a seguir no arquivo Web. config. Esta seção contém a configuração necessária Olá para sua saudação de toouse de aplicativo do ASP.NET provedor de estado de sessão de Cache Redis.

```xml
<sessionState mode="Custom" customProvider="MySessionStateStore">
    <providers>
    <!--
    <add name="MySessionStateStore"
           host = "127.0.0.1" [String]
        port = "" [number]
        accessKey = "" [String]
        ssl = "false" [true|false]
        throwOnError = "true" [true|false]
        retryTimeoutInMilliseconds = "0" [number]
        databaseId = "0" [number]
        applicationName = "" [String]
        connectionTimeoutInMilliseconds = "5000" [number]
        operationTimeoutInMilliseconds = "5000" [number]
    />
    -->
    <add name="MySessionStateStore" type="Microsoft.Web.Redis.RedisSessionStateProvider" host="127.0.0.1" accessKey="" ssl="false"/>
    </providers>
</sessionState>
```

Olá comentado seção fornece um exemplo dos atributos de saudação e configurações de exemplo para cada atributo.

Configurar atributos de saudação com valores de saudação da sua folha de cache no portal do Microsoft Azure hello e configurar Olá outros valores conforme desejado. Para obter instruções sobre como acessar as propriedades do cache, consulte [Definir as configurações de cache Redis](cache-configure.md#configure-redis-cache-settings).

* **host** – especifique o ponto de extremidade do cache.
* **porta** – usar a porta não SSL ou a porta SSL, dependendo das configurações de ssl hello.
* **accessKey** – usar a chave primária ou secundária de saudação para seu cache.
* **SSL** – verdadeiro se desejar toosecure comunicações de cache e cliente com ssl; caso contrário, false. Ser se toospecify Olá correto da porta.
  * porta do Hello não SSL está desabilitada por padrão para novos caches. Especifique true para essa saudação de toouse configuração porta SSL. Para obter mais informações sobre como habilitar a porta não SSL de hello, consulte Olá [portas de acesso](cache-configure.md#access-ports) seção Olá [configurar um cache](cache-configure.md) tópico.
* **throwOnError** – verdadeiro se você quiser um toobe exceção lançada se houver uma falha, ou false se desejar Olá toofail de operação silenciosamente. Você pode verificar uma falha, verificando a propriedade estática de Microsoft.Web.Redis.RedisSessionStateProvider.LastException hello. saudação padrão é true.
* **retryTimeoutInMilliseconds** – as operações que apresentam falhas recebem uma nova tentativa durante esse intervalo, especificado em milissegundos. primeira nova tentativa de saudação ocorre após 20 milissegundos e, em seguida, novas tentativas ocorrem a cada segundo até que o intervalo de retryTimeoutInMilliseconds saudação expira. Imediatamente após esse intervalo, a operação de saudação é repetida uma vez final. Se a operação de saudação ainda falhar, Olá exceção será devolvida toohello chamador, dependendo da configuração throwOnError hello. valor padrão de saudação é 0, o que significa nenhuma nova tentativa.
* **databaseId** – Especifica qual toouse de banco de dados para o cache de saída de dados. Se não for especificado, o valor padrão Olá 0 é usado.
* **applicationName** – As chaves são armazenadas em redis como `{<Application Name>_<Session ID>}_Data`. Esse esquema de nomenclatura permite que vários aplicativos tooshare Olá a mesma instância do Redis. Esse parâmetro é opcional e, se você não fornecê-lo, um valor padrão será usado.
* **connectionTimeoutInMilliseconds** – essa configuração permite que você toooverride Olá connectTimeout definindo no cliente stackexchange. Redis de saudação. Se não for especificado, a configuração de connectTimeout saudação padrão de 5000 é usada. Para saber mais, consulte [Modelo de configuração StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).
* **operationTimeoutInMilliseconds** – essa configuração permite que você toooverride Olá syncTimeout definindo no cliente stackexchange. Redis de saudação. Se não for especificado, a configuração de syncTimeout saudação padrão de 1000 é usada. Para saber mais, consulte [Modelo de configuração StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).

Para obter mais informações sobre essas propriedades, consulte o anúncio postagem de blog de Olá original no [anunciando provedor ASP.NET do estado de sessão para Redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx).

Não se esqueça de toocomment saudação padrão InProc sessão estado provedor seção no Web. config.

```xml
<!-- <sessionState mode="InProc"
     customProvider="DefaultSessionProvider">
     <providers>
        <add name="DefaultSessionProvider"
              type="System.Web.Providers.DefaultSessionStateProvider,
                    System.Web.Providers, Version=1.0.0.0, Culture=neutral,
                    PublicKeyToken=31bf3856ad364e35"
              connectionStringName="DefaultConnection" />
      </providers>
</sessionState> -->
```

Quando essas etapas são executadas, seu aplicativo é configurado toouse Olá provedor de estado de sessão de Cache Redis. Quando você usa o estado de sessão em seu aplicativo, ele é armazenado em uma instância do Cache Redis do Azure.

> [!IMPORTANT]
> Dados armazenados em cache Olá deve ser serializável, diferentemente dos dados de saudação que podem ser armazenados em saudação padrão provedor de estado de sessão ASP.NET na memória. Quando Olá provedor de estado de sessão para Redis for usado, certifique-se de que os tipos de dados Olá que estão sendo armazenados no estado de sessão são serializáveis.
> 
> 

## <a name="aspnet-session-state-options"></a>Opções de estado da sessão ASP.NET
* No provedor de estado de sessão de memória - esse provedor armazena Olá estado da sessão na memória. benefício de saudação de usar esse provedor é é simples e rápido. No entanto, não é possível dimensionar seus Aplicativos Web se você estiver usando o provedor na memória, pois ele não é distribuído.
* Provedor de estado de sessão do SQL Server - esse provedor armazena o estado de sessão Olá no Sql Server. Use este provedor se desejar que o estado da sessão Olá toostore no armazenamento persistente. Você pode dimensionar seu Aplicativo Web, mas o uso do Sql Server para sessão afeta o desempenho de seu Aplicativo Web.
* Distribuído na memória provedor estado de sessão como Redis Cache Session State Provider - isso proporciona provedor Olá melhor de ambos. Seu Aplicativo Web pode ter um Provedor de estado de sessão simples, rápido e escalonável. Como essa saudação de repositórios de provedor estado da sessão em Cache, seu aplicativo tem tootake em consideração todos os Olá características associadas ao conversar tooa distribuídos no Cache de memória, como falhas de rede temporárias. Para conhecer as práticas recomendadas sobre o uso do Cache, consulte [Orientação sobre cache](../best-practices-caching.md) da Microsoft Patterns & Practices [Orientação sobre design e implementação de aplicativo na nuvem do Azure](https://github.com/mspnp/azure-guidance).

Para saber mais sobre o estado da sessão e outras práticas recomendadas, consulte [Práticas recomendadas para o desenvolvimento na Web (Criando aplicativos de nuvem reais com o Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices).

## <a name="next-steps"></a>Próximas etapas
Check-out Olá [provedor de Cache de saída do ASP.NET para Cache Redis do Azure](cache-aspnet-output-cache-provider.md).

