---
title: "aaaCache provedor de Cache de saída do ASP.NET"
description: "Saiba como a saída de página ASP.NET toocache usando o Cache Redis do Azure"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 78469a66-0829-484f-8660-b2598ec60fbf
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/14/2017
ms.author: sdanie
ms.openlocfilehash: fc38cc657604b351f55ad8febac383783ac29700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-output-cache-provider-for-azure-redis-cache"></a>Provedor de Cache de Saída ASP.NET do Cache Redis do Azure
Olá provedor de Cache de saída Redis é um mecanismo de armazenamento fora do processo para dados de cache de saída. Esses dados são especificamente para respostas HTTP completas (cache de saída de página). provedor de saudação conecta-se à saudação nova saída cache provedor ponto de extensibilidade que foi introduzido no ASP.NET 4.

Olá toouse provedor de Cache de saída Redis, primeiro configure seu cache e, em seguida, configurar seu aplicativo ASP.NET usando o pacote de NuGet de provedor de Cache de saída Redis hello. Este tópico fornece orientação sobre como configurar seu Olá toouse do aplicativo provedor de Cache de saída Redis. Para saber mais sobre como criar e configurar uma instância do Cache Redis do Azure, consulte [Criar um cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).

## <a name="store-aspnet-page-output-in-hello-cache"></a>Armazenar a saída de página ASP.NET no cache de saudação
tooconfigure um aplicativo cliente no Visual Studio usando o pacote de NuGet de estado de sessão de Cache Redis hello, clique em **NuGet Package Manager**, **Package Manager Console** de saudação **ferramentas** menu.

Execução hello seguinte comando do hello `Package Manager Console` janela.
    
```
Install-Package Microsoft.Web.RedisOutputCacheProvider
```

pacote de NuGet de provedor de Cache de saída Redis Olá tem uma dependência Olá pacote Stackexchange. Se o pacote de Stackexchange Olá não está presente no seu projeto, ele é instalado. Para obter mais informações sobre o pacote de NuGet de provedor de Cache de saída Redis hello, consulte Olá [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) página NuGet.

>[!NOTE]
>Em adição toohello fortes Stackexchange pacote, também há Olá Stackexchange não-versão de nome forte. Se seu projeto está usando Olá não-versão de nome forte Stackexchange que você deve desinstalá-lo, caso contrário você conflitos de nomenclatura no projeto. Para saber mais sobre esses pacotes, consulte [Configurar clientes de cache .NET](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).
>
>

Olá NuGet pacote baixa e adiciona Olá necessário assembly faz referência e adiciona Olá seção a seguir no arquivo Web. config. Esta seção contém a configuração necessária Olá para sua saudação de toouse de aplicativo do ASP.NET provedor de Cache de saída Redis.

```xml
<caching>
  <outputCachedefault Provider="MyRedisOutputCache">
    <providers>
      <!--
      <add name="MyRedisOutputCache"
        host = "127.0.0.1" [String]
        port = "" [number]
        accessKey = "" [String]
        ssl = "false" [true|false]
        databaseId = "0" [number]
        applicationName = "" [String]
        connectionTimeoutInMilliseconds = "5000" [number]
        operationTimeoutInMilliseconds = "5000" [number]
      />
      -->
      <add name="MyRedisOutputCache" type="Microsoft.Web.Redis.RedisOutputCacheProvider" host="127.0.0.1" accessKey="" ssl="false"/>
    </providers>
  </outputCache>
</caching>
```

Olá comentado seção fornece um exemplo dos atributos de saudação e configurações de exemplo para cada atributo.

Configurar atributos de saudação com valores de saudação da sua folha de cache no portal do Microsoft Azure hello e configurar Olá outros valores conforme desejado. Para obter instruções sobre como acessar as propriedades do cache, consulte [Definir as configurações de cache Redis](cache-configure.md#configure-redis-cache-settings).

* **host** – especifique o ponto de extremidade do cache.
* **porta** – usar a porta não SSL ou a porta SSL, dependendo das configurações de ssl hello.
* **accessKey** – usar a chave primária ou secundária de saudação para seu cache.
* **SSL** – verdadeiro se desejar toosecure comunicações de cache e cliente com ssl; caso contrário, false. Ser se toospecify Olá correto da porta.
  * porta do Hello não SSL está desabilitada por padrão para novos caches. Especifique true para essa saudação de toouse configuração porta SSL. Para obter mais informações sobre como habilitar a porta não SSL de hello, consulte Olá [portas de acesso](cache-configure.md#access-ports) seção Olá [configurar um cache](cache-configure.md) tópico.
* **databaseId** – especificado toouse qual banco de dados para o cache de saída de dados. Se não for especificado, o valor padrão Olá 0 é usado.
* **applicationName** – As chaves são armazenadas em redis como `<AppName>_<SessionId>_Data`. Esse esquema de nomenclatura permite que vários Olá de tooshare aplicativos mesma chave. Esse parâmetro é opcional e, se você não fornecê-lo, um valor padrão será usado.
* **connectionTimeoutInMilliseconds** – essa configuração permite que você toooverride Olá connectTimeout definindo no cliente stackexchange. Redis de saudação. Se não for especificado, a configuração de connectTimeout saudação padrão de 5000 é usada. Para saber mais, consulte [Modelo de configuração StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).
* **operationTimeoutInMilliseconds** – essa configuração permite que você toooverride Olá syncTimeout definindo no cliente stackexchange. Redis de saudação. Se não for especificado, a configuração de syncTimeout saudação padrão de 1000 é usada. Para saber mais, consulte [Modelo de configuração StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).

Adicione uma página de tooeach diretiva OutputCache para o qual você deseja toocache saída de hello.

```
<%@ OutputCache Duration="60" VaryByParam="*" %>
```

No exemplo anterior de saudação, Olá armazenadas em cache dados de página permanece no cache de saudação por 60 segundos e uma versão diferente da página de saudação é armazenado em cache para cada combinação de parâmetros. Para obter mais informações sobre a diretiva OutputCache de hello, consulte [ @OutputCache ](http://go.microsoft.com/fwlink/?linkid=320837).

Quando essas etapas são executadas, seu aplicativo é configurado toouse Olá provedor de Cache de saída Redis.

## <a name="next-steps"></a>Próximas etapas
Check-out Olá [provedor de estado de sessão do ASP.NET para Cache Redis do Azure](cache-aspnet-session-state-provider.md).

