---
title: "Estado de sessão com cache Redis do Azure no Serviço de Aplicativo do Azure"
description: "Aprenda a usar o serviço de cache do Azure para dar suporte a cache de estado de sessão do ASP.NET."
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
ms.openlocfilehash: 64fa909daf92b2b1f0cf4c7b334edba807fe7228
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="session-state-with-azure-redis-cache-in-azure-app-service"></a><span data-ttu-id="41b69-103">Estado de sessão com cache Redis do Azure no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="41b69-103">Session state with Azure Redis cache in Azure App Service</span></span>
<span data-ttu-id="41b69-104">Este tópico explica como usar o Serviço de Cache Redis do Azure para o estado de sessão.</span><span class="sxs-lookup"><span data-stu-id="41b69-104">This topic explains how to use the Azure Redis Cache Service for session state.</span></span>

<span data-ttu-id="41b69-105">Se seu aplicativo web do ASP.NET usar o estado de sessão, você precisará configurar um provedor externo de estado de sessão (provedor de estado de sessão de Serviço de Cache Redis ou de SQL Server).</span><span class="sxs-lookup"><span data-stu-id="41b69-105">If your ASP.NET web app uses session state, you will need to configure an external session state provider (either the Redis Cache Service or a SQL Server session state provider).</span></span> <span data-ttu-id="41b69-106">Se você usar o estado de sessão, e não usar um provedor externo, você será limitado a uma instância do seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="41b69-106">If you use session state, and don't use an external provider, you will be limited to one instance of your web app.</span></span> <span data-ttu-id="41b69-107">O Serviço Cache Redis é o mais rápido e o mais simples de habilitar.</span><span class="sxs-lookup"><span data-stu-id="41b69-107">The Redis Cache Service is the fastest and simplest to enable.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="41b69-108"><a id="createcache"></a>Criar o cache</span><span class="sxs-lookup"><span data-stu-id="41b69-108"><a id="createcache"></a>Create the Cache</span></span>
<span data-ttu-id="41b69-109">Siga [estas instruções](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) para criar o cache.</span><span class="sxs-lookup"><span data-stu-id="41b69-109">Follow [these directions](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) to create the cache.</span></span>

## <span data-ttu-id="41b69-110"><a id="configureproject"></a>Adicionar o pacote NuGet RedisSessionStateProvider ao aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="41b69-110"><a id="configureproject"></a>Add the RedisSessionStateProvider NuGet package to your web app</span></span>
<span data-ttu-id="41b69-111">Instalar o pacote `RedisSessionStateProvider` NuGet.</span><span class="sxs-lookup"><span data-stu-id="41b69-111">Install the NuGet `RedisSessionStateProvider` package.</span></span>  <span data-ttu-id="41b69-112">Use o seguinte comando para instalar a partir da console de gerenciador de pacotes (**Ferramentas** > **Gerenciador de pacotes NuGet** > **Console do Gerenciador de Pacotes**):</span><span class="sxs-lookup"><span data-stu-id="41b69-112">Use the following command to install from the package manager console (**Tools** > **NuGet Package Manager** > **Package Manager Console**):</span></span>

  `PM> Install-Package Microsoft.Web.RedisSessionStateProvider`

<span data-ttu-id="41b69-113">Para instalar de **Ferramentas** > **Gerenciador de Pacotes NuGet** > **Gerenciar Pacotes NuGet para Solução**, procure `RedisSessionStateProvider`.</span><span class="sxs-lookup"><span data-stu-id="41b69-113">To install from **Tools** > **NuGet Package Manager** > **Manage NugGet Packages for Solution**, search for `RedisSessionStateProvider`.</span></span>

<span data-ttu-id="41b69-114">Para obter mais informações consulte a [página RedisSessionStateProvider de NuGet](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) e [Configurar o cliente do cache](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span><span class="sxs-lookup"><span data-stu-id="41b69-114">For more information see the [NuGet RedisSessionStateProvider page](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) and [Configure the cache client](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span></span>

## <span data-ttu-id="41b69-115"><a id="configurewebconfig"></a>Modificar o arquivo Web.Config</span><span class="sxs-lookup"><span data-stu-id="41b69-115"><a id="configurewebconfig"></a>Modify the Web.Config File</span></span>
<span data-ttu-id="41b69-116">Além de realizar referências do assembly para o Cache, o pacote NuGet adiciona entradas stub no arquivo *web.config* .</span><span class="sxs-lookup"><span data-stu-id="41b69-116">In addition to making assembly references for Cache, the NuGet package adds stub entries in the *web.config* file.</span></span> 

1. <span data-ttu-id="41b69-117">Abra o *web.config* e localize o elemento **sessionState** .</span><span class="sxs-lookup"><span data-stu-id="41b69-117">Open the *web.config* and find the the **sessionState** element.</span></span>
2. <span data-ttu-id="41b69-118">Insira os valores de `host`, `accessKey`, `port` (a porta SSL deve ser 6380) e defina `SSL` como `true`.</span><span class="sxs-lookup"><span data-stu-id="41b69-118">Enter the values for `host`, `accessKey`, `port` (the SSL port should be 6380), and set `SSL` to `true`.</span></span> <span data-ttu-id="41b69-119">Você pode obter esses valores na folha do [Portal do Azure](http://go.microsoft.com/fwlink/?LinkId=529715) da sua instância de cache.</span><span class="sxs-lookup"><span data-stu-id="41b69-119">These values can be obtained from the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) blade for your cache instance.</span></span> <span data-ttu-id="41b69-120">Para saber mais, confira [Conectar ao cache](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span><span class="sxs-lookup"><span data-stu-id="41b69-120">For more information, see [Connect to the cache](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span></span> <span data-ttu-id="41b69-121">Observe que a porta que não é do tipo SSL é desabilitada por padrão para novos caches.</span><span class="sxs-lookup"><span data-stu-id="41b69-121">Note that the non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="41b69-122">Para saber mais sobre como habilitar a porta que não é do tipo SSL, confira a seção [Portas de acesso](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) no tópico [Configurar um cache no Cache Redis do Azure](https://msdn.microsoft.com/library/azure/dn793612.aspx).</span><span class="sxs-lookup"><span data-stu-id="41b69-122">For more information about enabling the non-SSL port, see the [Access Ports](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) section in the [Configure a cache in Azure Redis Cache](https://msdn.microsoft.com/library/azure/dn793612.aspx) topic.</span></span> <span data-ttu-id="41b69-123">A marcação a seguir mostra as alterações para o *Web. config* arquivo, especificamente as alterações para *porta*, *host*, accessKey * e *ssl* .</span><span class="sxs-lookup"><span data-stu-id="41b69-123">The following markup shows the changes to the *web.config* file, specifically the changes to *port*, *host*, accessKey*, and *ssl*.</span></span>
   
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

## <span data-ttu-id="41b69-124"><a id="usesessionobject"></a> Usar o objeto da sessão em código</span><span class="sxs-lookup"><span data-stu-id="41b69-124"><a id="usesessionobject"></a> Use the Session Object in Code</span></span>
<span data-ttu-id="41b69-125">A etapa final é começar a usar o objeto da Sessão em seu código do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="41b69-125">The final step is to begin using the Session object in your ASP.NET code.</span></span> <span data-ttu-id="41b69-126">Você pode adicionar objetos ao estado de sessão usando o método **Session.Add** .</span><span class="sxs-lookup"><span data-stu-id="41b69-126">You add objects to session state by using the **Session.Add** method.</span></span> <span data-ttu-id="41b69-127">Este método utiliza pares de chave/valor para armazenar itens no cache do estado de sessão.</span><span class="sxs-lookup"><span data-stu-id="41b69-127">This method uses key-value pairs to store items in the session state cache.</span></span>

    string strValue = "yourvalue";
    Session.Add("yourkey", strValue);

<span data-ttu-id="41b69-128">O código seguinte recupera este valor do estado de sessão.</span><span class="sxs-lookup"><span data-stu-id="41b69-128">The following code retrieves this value from session state.</span></span>

    object objValue = Session["yourkey"];
    if (objValue != null)
       strValue = (string)objValue;    

<span data-ttu-id="41b69-129">Você também pode usar o Cache de Redis para armazenar em cache objetos no seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="41b69-129">You can also use the Redis Cache to cache objects in your web app.</span></span> <span data-ttu-id="41b69-130">Para saber mais, confira [Aplicativo de filme MVC com o Cache Redis do Azure em 15 minutos](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span><span class="sxs-lookup"><span data-stu-id="41b69-130">For more info, see [MVC movie app with Azure Redis Cache in 15 minutes](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span></span>
<span data-ttu-id="41b69-131">Para obter mais detalhes sobre como utilizar o estado de sessão do ASP.NET, confira [Visão geral do estado de sessão do ASP.NET][ASP.NET Session State Overview].</span><span class="sxs-lookup"><span data-stu-id="41b69-131">For more details about how to use ASP.NET session state, see [ASP.NET Session State Overview][ASP.NET Session State Overview].</span></span>

> [!NOTE]
> <span data-ttu-id="41b69-132">Se você deseja começar com o Serviço de Aplicativo do Azure antes de se inscrever em uma conta do Azure, acesse [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/), em que você pode criar imediatamente um aplicativo Web inicial de curta duração no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="41b69-132">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="41b69-133">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="41b69-133">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="41b69-134">O que mudou</span><span class="sxs-lookup"><span data-stu-id="41b69-134">What's changed</span></span>
* <span data-ttu-id="41b69-135">Para obter um guia sobre a alteração de Sites para o Serviço de Aplicativo, consulte: [Serviço de Aplicativo do Azure e seu impacto sobre os serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="41b69-135">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>
  
  <span data-ttu-id="41b69-136">*De [Rick Anderson](https://twitter.com/RickAndMSFT)*</span><span class="sxs-lookup"><span data-stu-id="41b69-136">*By [Rick Anderson](https://twitter.com/RickAndMSFT)*</span></span>

[installed the latest]: http://www.windowsazure.com/downloads/?sdk=net  
[ASP.NET Session State Overview]: http://msdn.microsoft.com/library/ms178581.aspx

[NewIcon]: ./media/web-sites-dotnet-session-state-caching/CacheScreenshot_NewButton.png
[NewCacheDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CreateOptions.png
[CacheIcon]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheIcon.png
[NuGetDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_NuGet.png
[OutputConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_OC_WebConfig.png
[CacheConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheConfig.png
[EndpointURL]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_EndpointURL.png
[ManageKeys]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_ManageAccessKeys.png

