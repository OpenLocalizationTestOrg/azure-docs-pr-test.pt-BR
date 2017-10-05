---
title: "Gerenciar a expiração do conteúdo da Web na CDN do Azure | Microsoft Docs"
description: "Saiba como gerenciar a expiração de conteúdo de Serviços de Nuvem/Aplicativos Web do Azure, ASP.NET ou IIS na CDN do Azure."
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
ms.openlocfilehash: c207d780857a61d4b1fc0f39e6185cae67abc955
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-expiration-of-azure-web-appscloud-services-aspnet-or-iis-content-in-azure-cdn"></a><span data-ttu-id="00e2e-103">Gerenciar a expiração de conteúdo de Serviços de Nuvem/Aplicativos Web do Azure, ASP.NET ou IIS na CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="00e2e-103">Manage expiration of Azure Web Apps/Cloud Services, ASP.NET, or IIS content in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="00e2e-104">Serviços de Nuvem/Aplicativos Web do Azure, ASP.NET ou IIS</span><span class="sxs-lookup"><span data-stu-id="00e2e-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="00e2e-105">Serviço Blob do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="00e2e-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="00e2e-106">Arquivos de qualquer servidor Web de origem publicamente acessível podem ser armazenados em cache no Azure CDN até que o TTL (tempo de vida) tenha decorrido.</span><span class="sxs-lookup"><span data-stu-id="00e2e-106">Files from any publicly accessible origin web server can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="00e2e-107">O TTL é determinado pelo [cabeçalho *Controle de Cache*](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) na resposta HTTP do servidor de origem.</span><span class="sxs-lookup"><span data-stu-id="00e2e-107">The TTL is determined by the [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in the HTTP response from the origin server.</span></span>  <span data-ttu-id="00e2e-108">Este artigo descreve como definir cabeçalhos `Cache-Control` para Aplicativos Web do Azure, Serviços de Nuvem do Azure, aplicativos ASP.NET e sites de Internet Information Services, todos configurados de maneira semelhante.</span><span class="sxs-lookup"><span data-stu-id="00e2e-108">This article describes how to set `Cache-Control` headers for Azure Web Apps, Azure Cloud Services, ASP.NET applications, and Internet Information Services sites, all of which are configured similarly.</span></span>

> [!TIP]
> <span data-ttu-id="00e2e-109">Você pode optar por não definir nenhum TTL em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="00e2e-109">You may choose to set no TTL on a file.</span></span>  <span data-ttu-id="00e2e-110">Nesse caso, o Azure CDN aplica automaticamente um TTL padrão de sete dias.</span><span class="sxs-lookup"><span data-stu-id="00e2e-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="00e2e-111">Para saber mais sobre como o Azure CDN trabalha para acelerar o acesso a blobs e outros recursos, confira a [Visão geral do Azure CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="00e2e-111">For more information about how Azure CDN works to speed up access to files and other resources, see the [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="setting-cache-control-headers-in-configuration"></a><span data-ttu-id="00e2e-112">Definindo cabeçalhos Cache-Control na configuração</span><span class="sxs-lookup"><span data-stu-id="00e2e-112">Setting Cache-Control Headers in configuration</span></span>
<span data-ttu-id="00e2e-113">Para conteúdo estático, como imagens e folhas de estilo, você pode controlar a frequência de atualização modificando os arquivos **applicationHost.config** ou **Web.config** para seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="00e2e-113">For static content, such as images and style sheets, you can control the update frequency by modifying the **applicationHost.config** or **web.config** files for your web application.</span></span>  <span data-ttu-id="00e2e-114">O elemento **system.webServer\staticContent\clientCache** no arquivo de configuração definirá o cabeçalho `Cache-Control` para seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="00e2e-114">The **system.webServer\staticContent\clientCache** element in the configuration file will set the `Cache-Control` header for your content.</span></span> <span data-ttu-id="00e2e-115">Em **eb.config**, as configurações afetarão tudo na pasta e em todas as subpastas, a menos que sejam substituídas no nível da subpasta.</span><span class="sxs-lookup"><span data-stu-id="00e2e-115">For **web.config**, the configuration settings will affect everything in the folder and all subfolders, unless overridden at the subfolder level.</span></span>  <span data-ttu-id="00e2e-116">Por exemplo, você pode definir um tempo de vida padrão na raiz para que todo o conteúdo estático seja armazenado em cache por três dias, mas ter uma subpasta que tenha conteúdo mais variável com uma configuração de cache de seis horas.</span><span class="sxs-lookup"><span data-stu-id="00e2e-116">For example, you can set a default time-to-live at the root to have all static content cached for 3 days, but have a subfolder that has more variable content with a cache setting of 6 hours.</span></span>  <span data-ttu-id="00e2e-117">Em **applicationHost.config**, todos os aplicativos no site serão afetados, mas pode ser substituídos nos arquivos **eb.config** dos aplicativos.</span><span class="sxs-lookup"><span data-stu-id="00e2e-117">For **applicationHost.config**, all applications on the site will be affected, but can be overridden in **web.config** files in the applications.</span></span>

<span data-ttu-id="00e2e-118">O seguinte XML mostra e exemplo de configuração de **clientCache** para especificar um tempo decorrido máximo de três dias:</span><span class="sxs-lookup"><span data-stu-id="00e2e-118">The following XML shows an example of setting **clientCache** to specify a maximum age of 3 days:</span></span>  

```xml
<configuration>
    <system.webServer>
        <staticContent>
            <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00" />
        </staticContent>
    </system.webServer>
</configuration>
```

<span data-ttu-id="00e2e-119">A especificação de **UseMaxAge** adiciona um `Cache-Control: max-age=<nnn>` à resposta com base no valor especificado no atributo **CacheControlMaxAge**.</span><span class="sxs-lookup"><span data-stu-id="00e2e-119">Specifying **UseMaxAge** adds a `Cache-Control: max-age=<nnn>` header to the response based on the value specified in the **CacheControlMaxAge** attribute.</span></span> <span data-ttu-id="00e2e-120">O formato do período de tempo para o atributo **cacheControlMaxAge** é <days>.<hours>:<min>:<sec>.</span><span class="sxs-lookup"><span data-stu-id="00e2e-120">The format of the timespan is for the **cacheControlMaxAge** attribute is <days>.<hours>:<min>:<sec>.</span></span> <span data-ttu-id="00e2e-121">Para obter mais informações sobre o nó **clientCache**, consulte [Cache de cliente <clientCache>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span><span class="sxs-lookup"><span data-stu-id="00e2e-121">For more information on the **clientCache** node, see [Client Cache <clientCache>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span></span>  

## <a name="setting-cache-control-headers-in-code"></a><span data-ttu-id="00e2e-122">Definindo cabeçalhos Cache-Control no código</span><span class="sxs-lookup"><span data-stu-id="00e2e-122">Setting Cache-Control Headers in Code</span></span>
<span data-ttu-id="00e2e-123">Para aplicativos ASP.NET, você pode definir o comportamento do caching de CDN programaticamente definindo a propriedade **HttpResponse** .</span><span class="sxs-lookup"><span data-stu-id="00e2e-123">For ASP.NET applications, you can set the CDN caching behavior programmatically by setting the **HttpResponse.Cache** property.</span></span> <span data-ttu-id="00e2e-124">Para obter mais informações sobre a propriedade **HttpResponse.Cache**, consulte [Propriedade HttpResponse.Cache](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) e [Classe HttpCachePolicy](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span><span class="sxs-lookup"><span data-stu-id="00e2e-124">For more information on the **HttpResponse.Cache** property, see [HttpResponse.Cache Property](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) and [HttpCachePolicy Class](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

<span data-ttu-id="00e2e-125">Se você quiser armazenar em cache programaticamente o conteúdo do aplicativo no ASP.NET, verifique se o conteúdo está marcado como armazenável em cache, definindo HttpCacheability como *Public*.</span><span class="sxs-lookup"><span data-stu-id="00e2e-125">If you want to programmatically cache application content in ASP.NET, make sure that the content is marked as cacheable by setting HttpCacheability to *Public*.</span></span> <span data-ttu-id="00e2e-126">Além disso, verifique se um validador de cache está definido.</span><span class="sxs-lookup"><span data-stu-id="00e2e-126">Also, ensure that a cache validator is set.</span></span> <span data-ttu-id="00e2e-127">O validador de cache pode ser um carimbo de data/hora de Última Modificação definido chamando SetLastModified ou um valor de etag definido chamando SetETag.</span><span class="sxs-lookup"><span data-stu-id="00e2e-127">The cache validator can be a Last Modified timestamp set by calling SetLastModified, or an etag value set by calling SetETag.</span></span> <span data-ttu-id="00e2e-128">Opcionalmente, você também pode especificar um tempo de expiração de cache chamando SetExpires ou pode contar com a heurística de cache padrão descrita anteriormente neste documento.</span><span class="sxs-lookup"><span data-stu-id="00e2e-128">Optionally, you can also specify a cache expiration time by calling SetExpires, or you can rely on the default cache heuristics described earlier in this document.</span></span>  

<span data-ttu-id="00e2e-129">Por exemplo, para armazenar o conteúdo em cache por uma hora, adicione o seguinte:</span><span class="sxs-lookup"><span data-stu-id="00e2e-129">For example, to cache content for one hour, add the following:</span></span>  

```csharp
// Set the caching parameters.
Response.Cache.SetExpires(DateTime.Now.AddHours(1));
Response.Cache.SetCacheability(HttpCacheability.Public);
Response.Cache.SetLastModified(DateTime.Now);
```

## <a name="next-steps"></a><span data-ttu-id="00e2e-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="00e2e-130">Next Steps</span></span>
* [<span data-ttu-id="00e2e-131">Leia os detalhes sobre o elemento **clientCache**</span><span class="sxs-lookup"><span data-stu-id="00e2e-131">Read details about the **clientCache** element</span></span>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)
* [<span data-ttu-id="00e2e-132">Leia a documentação sobre a propriedade **HttpResponse.Cache**</span><span class="sxs-lookup"><span data-stu-id="00e2e-132">Read the documentation for the **HttpResponse.Cache** Property</span></span>](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) 
* <span data-ttu-id="00e2e-133">[Leia a documentação sobre a **classe HttpCachePolicy**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span><span class="sxs-lookup"><span data-stu-id="00e2e-133">[Read the documentation for the **HttpCachePolicy Class**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

