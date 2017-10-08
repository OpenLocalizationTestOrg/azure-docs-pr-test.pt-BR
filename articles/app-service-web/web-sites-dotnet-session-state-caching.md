---
title: "estado de aaaSession com cache Redis do Azure no serviço de aplicativo do Azure"
description: "Saiba como toouse Olá cache de estado de sessão do serviço de Cache do Azure toosupport ASP.NET."
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
manager: erikre
editor: none
ms.assetid: 4f98d289-2698-464d-85cd-99ec40fad1f2
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 06/27/2016
ms.author: riande
ms.openlocfilehash: f689b6754ea072aa195f822ab6482f4bf2748375
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="session-state-with-azure-redis-cache-in-azure-app-service"></a>Estado de sessão com cache Redis do Azure no Serviço de Aplicativo do Azure
Este tópico explica como toouse Olá o serviço de Cache Redis do Azure para estado de sessão.

Se seu aplicativo da web ASP.NET usa estado de sessão, você precisará tooconfigure um provedor de estado de sessão externo (Olá Redis Cache de serviço ou um provedor de estado de sessão do SQL Server). Se você usar o estado da sessão e não use um provedor externo, você será limitado tooone instância de seu aplicativo web. Olá serviço de Cache Redis é tooenable rápida e simples de saudação.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a id="createcache"></a>Criar hello Cache
Execute [estas instruções](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) toocreate cache de saudação.

## <a id="configureproject"></a>Adicionar Olá RedisSessionStateProvider NuGet pacote tooyour web app
Instalar Olá NuGet `RedisSessionStateProvider` pacote.  Tooinstall do console do Gerenciador de pacote de saudação do comando de uso a seguir de saudação (**ferramentas** > **NuGet Package Manager** > **Package Manager Console**):

  `PM> Install-Package Microsoft.Web.RedisSessionStateProvider`

tooinstall de **ferramentas** > **NuGet Package Manager** > **gerenciar preciosidade pacotes para solução**, procure `RedisSessionStateProvider`.

Para obter mais informações, consulte Olá [página NuGet RedisSessionStateProvider](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) e [configuração de cliente de cache de saudação](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).

## <a id="configurewebconfig"></a>Modificar o arquivo Web. config de saudação
Além disso toomaking assembly faz referência para o Cache, pacote de NuGet Olá adiciona entradas de stub Olá *Web. config* arquivo. 

1. Olá abrir *Web. config* e localize Olá Olá **sessionState** elemento.
2. Digite os valores hello para `host`, `accessKey`, `port` (Olá porta SSL deve ser 6380) e defina `SSL` muito`true`. Esses valores podem ser obtidos da saudação [Portal do Azure](http://go.microsoft.com/fwlink/?LinkId=529715) folha para a instância de cache. Para obter mais informações, consulte [conectar cache toohello](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache). Observe que a porta não SSL de saudação é desabilitada por padrão para novos caches. Para obter mais informações sobre como habilitar a porta não SSL de hello, consulte Olá [portas de acesso](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) seção Olá [configurar um cache no Cache Redis do Azure](https://msdn.microsoft.com/library/azure/dn793612.aspx) tópico. Olá, marcação a seguir mostra Olá alterações toohello *Web. config* de arquivos, alterações de saudação especificamente muito*porta*, *host*, accessKey * e *ssl*.
   
          <system.web>;
            <customErrors mode="Off" />;
            <authentication mode="None" />;
            <compilation debug="true" targetFramework="4.5" />;
            <httpRuntime targetFramework="4.5" />;
            <sessionState mode="Custom" customProvider="RedisSessionProvider">;
              <providers>;  
                  <!--<add name="RedisSessionProvider" 
                    host = "127.0.0.1" [String]
                    port = "" [number]
                    accessKey = "" [String]
                    ssl = "false" [true|false]
                    throwOnError = "true" [true|false]
                    retryTimeoutInMilliseconds = "0" [number]
                    databaseId = "0" [number]
                    applicationName = "" [String]
                  />;-->;
                 <add name="RedisSessionProvider" 
                      type="Microsoft.Web.Redis.RedisSessionStateProvider" 
                      port="6380"
                      host="movie2.redis.cache.windows.net" 
                      accessKey="m7PNV60CrvKpLqMUxosC3dSe6kx9nQ6jP5del8TmADk=" 
                      ssl="true" />;
              <!--<add name="MySessionStateStore" type="Microsoft.Web.Redis.RedisSessionStateProvider" host="127.0.0.1" accessKey="" ssl="false" />;-->;
              </providers>;
            </sessionState>;
          </system.web>;

## <a id="usesessionobject"></a>Usar Olá objeto de sessão no código
Olá última etapa é toobegin usando o objeto de sessão de saudação em seu código ASP.NET. Adicionar o estado de toosession de objetos usando Olá **Session.Add** método. Esse método usa itens de toostore de pares chave-valor no cache de estado de sessão hello.

    string strValue = "yourvalue";
    Session.Add("yourkey", strValue);

saudação de código a seguir recupera esse valor de estado de sessão.

    object objValue = Session["yourkey"];
    if (objValue != null)
       strValue = (string)objValue;    

Você também pode usar objetos de toocache de Redis Cache Olá em seu aplicativo web. Para saber mais, confira [Aplicativo de filme MVC com o Cache Redis do Azure em 15 minutos](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).
Para obter mais detalhes sobre como toouse estado da sessão ASP.NET, consulte [visão geral sobre o estado de sessão ASP.NET][ASP.NET Session State Overview].

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
> 
> 

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)
  
  *De [Rick Anderson](https://twitter.com/RickAndMSFT)*

[installed hello latest]: http://www.windowsazure.com/downloads/?sdk=net  
[ASP.NET Session State Overview]: http://msdn.microsoft.com/library/ms178581.aspx

[NewIcon]: ./media/web-sites-dotnet-session-state-caching/CacheScreenshot_NewButton.png
[NewCacheDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CreateOptions.png
[CacheIcon]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheIcon.png
[NuGetDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_NuGet.png
[OutputConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_OC_WebConfig.png
[CacheConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheConfig.png
[EndpointURL]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_EndpointURL.png
[ManageKeys]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_ManageAccessKeys.png

