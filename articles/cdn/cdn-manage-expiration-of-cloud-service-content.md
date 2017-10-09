---
title: "aaaManage expiração de conteúdo da web no Azure CDN | Microsoft Docs"
description: "Saiba como toomanage expiração de conteúdo de serviços de nuvem/aplicativos de Web do Azure, ASP.NET ou IIS no Azure CDN."
services: cdn
documentationcenter: .NET
author: zhangmanling
manager: erikre
editor: 
ms.assetid: bef53fcc-bb13-4002-9324-9edee9da8288
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: a0154236c3893b627f4480e0688f555964862556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-expiration-of-azure-web-appscloud-services-aspnet-or-iis-content-in-azure-cdn"></a><span data-ttu-id="2294d-103">Gerenciar a expiração de conteúdo de Serviços de Nuvem/Aplicativos Web do Azure, ASP.NET ou IIS na CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="2294d-103">Manage expiration of Azure Web Apps/Cloud Services, ASP.NET, or IIS content in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2294d-104">Serviços de Nuvem/Aplicativos Web do Azure, ASP.NET ou IIS</span><span class="sxs-lookup"><span data-stu-id="2294d-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="2294d-105">Serviço Blob do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="2294d-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="2294d-106">Arquivos de qualquer servidor Web de origem publicamente acessível podem ser armazenados em cache no Azure CDN até que o TTL (tempo de vida) tenha decorrido.</span><span class="sxs-lookup"><span data-stu-id="2294d-106">Files from any publicly accessible origin web server can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="2294d-107">Olá TTL é determinado pelo Olá [ *Cache-Control* cabeçalho](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) na resposta HTTP de saudação do servidor de origem de saudação.</span><span class="sxs-lookup"><span data-stu-id="2294d-107">hello TTL is determined by hello [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in hello HTTP response from hello origin server.</span></span>  <span data-ttu-id="2294d-108">Este artigo descreve como tooset `Cache-Control` cabeçalhos para aplicativos Web do Azure e sites de Internet Information Services, que são configurados da mesma forma, aplicativos ASP.NET e serviços de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="2294d-108">This article describes how tooset `Cache-Control` headers for Azure Web Apps, Azure Cloud Services, ASP.NET applications, and Internet Information Services sites, all of which are configured similarly.</span></span>

> [!TIP]
> <span data-ttu-id="2294d-109">Você não pode escolher tooset nenhum TTL em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="2294d-109">You may choose tooset no TTL on a file.</span></span>  <span data-ttu-id="2294d-110">Nesse caso, o Azure CDN aplica automaticamente um TTL padrão de sete dias.</span><span class="sxs-lookup"><span data-stu-id="2294d-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="2294d-111">Para obter mais informações sobre como funciona o Azure CDN toospeed toofiles de acesso e outros recursos, consulte Olá [visão geral do Azure CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2294d-111">For more information about how Azure CDN works toospeed up access toofiles and other resources, see hello [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="setting-cache-control-headers-in-configuration"></a><span data-ttu-id="2294d-112">Definindo cabeçalhos Cache-Control na configuração</span><span class="sxs-lookup"><span data-stu-id="2294d-112">Setting Cache-Control Headers in configuration</span></span>
<span data-ttu-id="2294d-113">Conteúdo estático, como imagens e folhas de estilo, você pode controlar a frequência de atualização de saudação modificando Olá **applicationHost. config** ou **Web. config** arquivos para o aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="2294d-113">For static content, such as images and style sheets, you can control hello update frequency by modifying hello **applicationHost.config** or **web.config** files for your web application.</span></span>  <span data-ttu-id="2294d-114">Olá **system.webServer\staticContent\clientCache** elemento no arquivo de configuração de saudação definirá Olá `Cache-Control` cabeçalho para o seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="2294d-114">hello **system.webServer\staticContent\clientCache** element in hello configuration file will set hello `Cache-Control` header for your content.</span></span> <span data-ttu-id="2294d-115">Para **Web. config**, definições de configuração de saudação afetarão tudo na pasta hello e todas as subpastas, a menos que substituído no nível de subpasta hello.</span><span class="sxs-lookup"><span data-stu-id="2294d-115">For **web.config**, hello configuration settings will affect everything in hello folder and all subfolders, unless overridden at hello subfolder level.</span></span>  <span data-ttu-id="2294d-116">Por exemplo, você pode definir um padrão time-to-live em Olá raiz toohave todo o conteúdo estático armazenado em cache por 3 dias, mas tem uma subpasta que tenha mais variável conteúdo com uma configuração de cache de 6 horas.</span><span class="sxs-lookup"><span data-stu-id="2294d-116">For example, you can set a default time-to-live at hello root toohave all static content cached for 3 days, but have a subfolder that has more variable content with a cache setting of 6 hours.</span></span>  <span data-ttu-id="2294d-117">Para **applicationHost. config**, todos os aplicativos no site hello serão afetados, mas pode ser substituídos em **Web. config** arquivos em aplicativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="2294d-117">For **applicationHost.config**, all applications on hello site will be affected, but can be overridden in **web.config** files in hello applications.</span></span>

<span data-ttu-id="2294d-118">Olá, XML a seguir mostra um exemplo de configuração **clientCache** toospecify a duração máxima de 3 dias:</span><span class="sxs-lookup"><span data-stu-id="2294d-118">hello following XML shows an example of setting **clientCache** toospecify a maximum age of 3 days:</span></span>  

```xml
<configuration>
    <system.webServer>
        <staticContent>
            <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00" />
        </staticContent>
    </system.webServer>
</configuration>
```

<span data-ttu-id="2294d-119">Especificando **UseMaxAge** adiciona um `Cache-Control: max-age=<nnn>` resposta do cabeçalho toohello com base no valor de saudação especificado no hello **CacheControlMaxAge** atributo.</span><span class="sxs-lookup"><span data-stu-id="2294d-119">Specifying **UseMaxAge** adds a `Cache-Control: max-age=<nnn>` header toohello response based on hello value specified in hello **CacheControlMaxAge** attribute.</span></span> <span data-ttu-id="2294d-120">formato de saudação de timespan Olá é para Olá **cacheControlMaxAge** atributo é <days>.<hours>:<min>:<sec>.</span><span class="sxs-lookup"><span data-stu-id="2294d-120">hello format of hello timespan is for hello **cacheControlMaxAge** attribute is <days>.<hours>:<min>:<sec>.</span></span> <span data-ttu-id="2294d-121">Para obter mais informações sobre Olá **clientCache** nó, consulte [Cache do cliente <clientCache> ](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span><span class="sxs-lookup"><span data-stu-id="2294d-121">For more information on hello **clientCache** node, see [Client Cache <clientCache>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span></span>  

## <a name="setting-cache-control-headers-in-code"></a><span data-ttu-id="2294d-122">Definindo cabeçalhos Cache-Control no código</span><span class="sxs-lookup"><span data-stu-id="2294d-122">Setting Cache-Control Headers in Code</span></span>
<span data-ttu-id="2294d-123">Para aplicativos ASP.NET, você pode definir o comportamento do cache de CDN Olá programaticamente, definindo Olá **HttpResponse** propriedade.</span><span class="sxs-lookup"><span data-stu-id="2294d-123">For ASP.NET applications, you can set hello CDN caching behavior programmatically by setting hello **HttpResponse.Cache** property.</span></span> <span data-ttu-id="2294d-124">Para obter mais informações sobre Olá **HttpResponse** propriedade, consulte [propriedade HttpResponse](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) e [classe HttpCachePolicy](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span><span class="sxs-lookup"><span data-stu-id="2294d-124">For more information on hello **HttpResponse.Cache** property, see [HttpResponse.Cache Property](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) and [HttpCachePolicy Class](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

<span data-ttu-id="2294d-125">Se desejar que o conteúdo do aplicativo de cache tooprogrammatically no ASP.NET, certifique-se de que o conteúdo de saudação está marcado como armazenável em cache, definindo HttpCacheability muito*público*.</span><span class="sxs-lookup"><span data-stu-id="2294d-125">If you want tooprogrammatically cache application content in ASP.NET, make sure that hello content is marked as cacheable by setting HttpCacheability too*Public*.</span></span> <span data-ttu-id="2294d-126">Além disso, verifique se um validador de cache está definido.</span><span class="sxs-lookup"><span data-stu-id="2294d-126">Also, ensure that a cache validator is set.</span></span> <span data-ttu-id="2294d-127">Validador de cache Olá pode ser a última modificação timestamp definido ao chamar SetLastModified ou um valor de etag definido ao chamar SetETag.</span><span class="sxs-lookup"><span data-stu-id="2294d-127">hello cache validator can be a Last Modified timestamp set by calling SetLastModified, or an etag value set by calling SetETag.</span></span> <span data-ttu-id="2294d-128">Opcionalmente, você também pode especificar um tempo de expiração de cache chamando SetExpires ou você pode confiar na heurística de cache padrão de saudação descrita anteriormente neste documento.</span><span class="sxs-lookup"><span data-stu-id="2294d-128">Optionally, you can also specify a cache expiration time by calling SetExpires, or you can rely on hello default cache heuristics described earlier in this document.</span></span>  

<span data-ttu-id="2294d-129">Por exemplo, toocache o conteúdo de uma hora, adicione o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="2294d-129">For example, toocache content for one hour, add hello following:</span></span>  

```csharp
// Set hello caching parameters.
Response.Cache.SetExpires(DateTime.Now.AddHours(1));
Response.Cache.SetCacheability(HttpCacheability.Public);
Response.Cache.SetLastModified(DateTime.Now);
```

## <a name="next-steps"></a><span data-ttu-id="2294d-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2294d-130">Next Steps</span></span>
* [<span data-ttu-id="2294d-131">Ler os detalhes sobre Olá **clientCache** elemento</span><span class="sxs-lookup"><span data-stu-id="2294d-131">Read details about hello **clientCache** element</span></span>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)
* [<span data-ttu-id="2294d-132">Leia a documentação Olá Olá **HttpResponse** propriedade</span><span class="sxs-lookup"><span data-stu-id="2294d-132">Read hello documentation for hello **HttpResponse.Cache** Property</span></span>](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) 
* <span data-ttu-id="2294d-133">[Leia a documentação Olá Olá **classe HttpCachePolicy**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span><span class="sxs-lookup"><span data-stu-id="2294d-133">[Read hello documentation for hello **HttpCachePolicy Class**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

