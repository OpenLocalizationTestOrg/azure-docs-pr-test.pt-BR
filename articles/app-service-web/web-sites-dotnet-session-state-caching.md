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
# <a name="session-state-with-azure-redis-cache-in-azure-app-service"></a><span data-ttu-id="b497e-103">Estado de sessão com cache Redis do Azure no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="b497e-103">Session state with Azure Redis cache in Azure App Service</span></span>
<span data-ttu-id="b497e-104">Este tópico explica como toouse Olá o serviço de Cache Redis do Azure para estado de sessão.</span><span class="sxs-lookup"><span data-stu-id="b497e-104">This topic explains how toouse hello Azure Redis Cache Service for session state.</span></span>

<span data-ttu-id="b497e-105">Se seu aplicativo da web ASP.NET usa estado de sessão, você precisará tooconfigure um provedor de estado de sessão externo (Olá Redis Cache de serviço ou um provedor de estado de sessão do SQL Server).</span><span class="sxs-lookup"><span data-stu-id="b497e-105">If your ASP.NET web app uses session state, you will need tooconfigure an external session state provider (either hello Redis Cache Service or a SQL Server session state provider).</span></span> <span data-ttu-id="b497e-106">Se você usar o estado da sessão e não use um provedor externo, você será limitado tooone instância de seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="b497e-106">If you use session state, and don't use an external provider, you will be limited tooone instance of your web app.</span></span> <span data-ttu-id="b497e-107">Olá serviço de Cache Redis é tooenable rápida e simples de saudação.</span><span class="sxs-lookup"><span data-stu-id="b497e-107">hello Redis Cache Service is hello fastest and simplest tooenable.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="b497e-108"><a id="createcache"></a>Criar hello Cache</span><span class="sxs-lookup"><span data-stu-id="b497e-108"><a id="createcache"></a>Create hello Cache</span></span>
<span data-ttu-id="b497e-109">Execute [estas instruções](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) toocreate cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="b497e-109">Follow [these directions](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) toocreate hello cache.</span></span>

## <span data-ttu-id="b497e-110"><a id="configureproject"></a>Adicionar Olá RedisSessionStateProvider NuGet pacote tooyour web app</span><span class="sxs-lookup"><span data-stu-id="b497e-110"><a id="configureproject"></a>Add hello RedisSessionStateProvider NuGet package tooyour web app</span></span>
<span data-ttu-id="b497e-111">Instalar Olá NuGet `RedisSessionStateProvider` pacote.</span><span class="sxs-lookup"><span data-stu-id="b497e-111">Install hello NuGet `RedisSessionStateProvider` package.</span></span>  <span data-ttu-id="b497e-112">Tooinstall do console do Gerenciador de pacote de saudação do comando de uso a seguir de saudação (**ferramentas** > **NuGet Package Manager** > **Package Manager Console**):</span><span class="sxs-lookup"><span data-stu-id="b497e-112">Use hello following command tooinstall from hello package manager console (**Tools** > **NuGet Package Manager** > **Package Manager Console**):</span></span>

  `PM> Install-Package Microsoft.Web.RedisSessionStateProvider`

<span data-ttu-id="b497e-113">tooinstall de **ferramentas** > **NuGet Package Manager** > **gerenciar preciosidade pacotes para solução**, procure `RedisSessionStateProvider`.</span><span class="sxs-lookup"><span data-stu-id="b497e-113">tooinstall from **Tools** > **NuGet Package Manager** > **Manage NugGet Packages for Solution**, search for `RedisSessionStateProvider`.</span></span>

<span data-ttu-id="b497e-114">Para obter mais informações, consulte Olá [página NuGet RedisSessionStateProvider](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) e [configuração de cliente de cache de saudação](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span><span class="sxs-lookup"><span data-stu-id="b497e-114">For more information see hello [NuGet RedisSessionStateProvider page](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) and [Configure hello cache client](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span></span>

## <span data-ttu-id="b497e-115"><a id="configurewebconfig"></a>Modificar o arquivo Web. config de saudação</span><span class="sxs-lookup"><span data-stu-id="b497e-115"><a id="configurewebconfig"></a>Modify hello Web.Config File</span></span>
<span data-ttu-id="b497e-116">Além disso toomaking assembly faz referência para o Cache, pacote de NuGet Olá adiciona entradas de stub Olá *Web. config* arquivo.</span><span class="sxs-lookup"><span data-stu-id="b497e-116">In addition toomaking assembly references for Cache, hello NuGet package adds stub entries in hello *web.config* file.</span></span> 

1. <span data-ttu-id="b497e-117">Olá abrir *Web. config* e localize Olá Olá **sessionState** elemento.</span><span class="sxs-lookup"><span data-stu-id="b497e-117">Open hello *web.config* and find hello hello **sessionState** element.</span></span>
2. <span data-ttu-id="b497e-118">Digite os valores hello para `host`, `accessKey`, `port` (Olá porta SSL deve ser 6380) e defina `SSL` muito`true`.</span><span class="sxs-lookup"><span data-stu-id="b497e-118">Enter hello values for `host`, `accessKey`, `port` (hello SSL port should be 6380), and set `SSL` too`true`.</span></span> <span data-ttu-id="b497e-119">Esses valores podem ser obtidos da saudação [Portal do Azure](http://go.microsoft.com/fwlink/?LinkId=529715) folha para a instância de cache.</span><span class="sxs-lookup"><span data-stu-id="b497e-119">These values can be obtained from hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) blade for your cache instance.</span></span> <span data-ttu-id="b497e-120">Para obter mais informações, consulte [conectar cache toohello](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span><span class="sxs-lookup"><span data-stu-id="b497e-120">For more information, see [Connect toohello cache](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span></span> <span data-ttu-id="b497e-121">Observe que a porta não SSL de saudação é desabilitada por padrão para novos caches.</span><span class="sxs-lookup"><span data-stu-id="b497e-121">Note that hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="b497e-122">Para obter mais informações sobre como habilitar a porta não SSL de hello, consulte Olá [portas de acesso](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) seção Olá [configurar um cache no Cache Redis do Azure](https://msdn.microsoft.com/library/azure/dn793612.aspx) tópico.</span><span class="sxs-lookup"><span data-stu-id="b497e-122">For more information about enabling hello non-SSL port, see hello [Access Ports](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) section in hello [Configure a cache in Azure Redis Cache](https://msdn.microsoft.com/library/azure/dn793612.aspx) topic.</span></span> <span data-ttu-id="b497e-123">Olá, marcação a seguir mostra Olá alterações toohello *Web. config* de arquivos, alterações de saudação especificamente muito*porta*, *host*, accessKey * e *ssl*.</span><span class="sxs-lookup"><span data-stu-id="b497e-123">hello following markup shows hello changes toohello *web.config* file, specifically hello changes too*port*, *host*, accessKey*, and *ssl*.</span></span>
   
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

## <span data-ttu-id="b497e-124"><a id="usesessionobject"></a>Usar Olá objeto de sessão no código</span><span class="sxs-lookup"><span data-stu-id="b497e-124"><a id="usesessionobject"></a> Use hello Session Object in Code</span></span>
<span data-ttu-id="b497e-125">Olá última etapa é toobegin usando o objeto de sessão de saudação em seu código ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b497e-125">hello final step is toobegin using hello Session object in your ASP.NET code.</span></span> <span data-ttu-id="b497e-126">Adicionar o estado de toosession de objetos usando Olá **Session.Add** método.</span><span class="sxs-lookup"><span data-stu-id="b497e-126">You add objects toosession state by using hello **Session.Add** method.</span></span> <span data-ttu-id="b497e-127">Esse método usa itens de toostore de pares chave-valor no cache de estado de sessão hello.</span><span class="sxs-lookup"><span data-stu-id="b497e-127">This method uses key-value pairs toostore items in hello session state cache.</span></span>

    string strValue = "yourvalue";
    Session.Add("yourkey", strValue);

<span data-ttu-id="b497e-128">saudação de código a seguir recupera esse valor de estado de sessão.</span><span class="sxs-lookup"><span data-stu-id="b497e-128">hello following code retrieves this value from session state.</span></span>

    object objValue = Session["yourkey"];
    if (objValue != null)
       strValue = (string)objValue;    

<span data-ttu-id="b497e-129">Você também pode usar objetos de toocache de Redis Cache Olá em seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="b497e-129">You can also use hello Redis Cache toocache objects in your web app.</span></span> <span data-ttu-id="b497e-130">Para saber mais, confira [Aplicativo de filme MVC com o Cache Redis do Azure em 15 minutos](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span><span class="sxs-lookup"><span data-stu-id="b497e-130">For more info, see [MVC movie app with Azure Redis Cache in 15 minutes](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span></span>
<span data-ttu-id="b497e-131">Para obter mais detalhes sobre como toouse estado da sessão ASP.NET, consulte [visão geral sobre o estado de sessão ASP.NET][ASP.NET Session State Overview].</span><span class="sxs-lookup"><span data-stu-id="b497e-131">For more details about how toouse ASP.NET session state, see [ASP.NET Session State Overview][ASP.NET Session State Overview].</span></span>

> [!NOTE]
> <span data-ttu-id="b497e-132">Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b497e-132">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="b497e-133">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="b497e-133">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="b497e-134">O que mudou</span><span class="sxs-lookup"><span data-stu-id="b497e-134">What's changed</span></span>
* <span data-ttu-id="b497e-135">Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="b497e-135">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>
  
  <span data-ttu-id="b497e-136">*De [Rick Anderson](https://twitter.com/RickAndMSFT)*</span><span class="sxs-lookup"><span data-stu-id="b497e-136">*By [Rick Anderson](https://twitter.com/RickAndMSFT)*</span></span>

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

