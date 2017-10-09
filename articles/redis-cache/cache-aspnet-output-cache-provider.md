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
# <a name="aspnet-output-cache-provider-for-azure-redis-cache"></a><span data-ttu-id="1155d-103">Provedor de Cache de Saída ASP.NET do Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="1155d-103">ASP.NET Output Cache Provider for Azure Redis Cache</span></span>
<span data-ttu-id="1155d-104">Olá provedor de Cache de saída Redis é um mecanismo de armazenamento fora do processo para dados de cache de saída.</span><span class="sxs-lookup"><span data-stu-id="1155d-104">hello Redis Output Cache Provider is an out-of-process storage mechanism for output cache data.</span></span> <span data-ttu-id="1155d-105">Esses dados são especificamente para respostas HTTP completas (cache de saída de página).</span><span class="sxs-lookup"><span data-stu-id="1155d-105">This data is specifically for full HTTP responses (page output caching).</span></span> <span data-ttu-id="1155d-106">provedor de saudação conecta-se à saudação nova saída cache provedor ponto de extensibilidade que foi introduzido no ASP.NET 4.</span><span class="sxs-lookup"><span data-stu-id="1155d-106">hello provider plugs into hello new output cache provider extensibility point that was introduced in ASP.NET 4.</span></span>

<span data-ttu-id="1155d-107">Olá toouse provedor de Cache de saída Redis, primeiro configure seu cache e, em seguida, configurar seu aplicativo ASP.NET usando o pacote de NuGet de provedor de Cache de saída Redis hello.</span><span class="sxs-lookup"><span data-stu-id="1155d-107">toouse hello Redis Output Cache Provider, first configure your cache, and then configure your ASP.NET application using hello Redis Output Cache Provider NuGet package.</span></span> <span data-ttu-id="1155d-108">Este tópico fornece orientação sobre como configurar seu Olá toouse do aplicativo provedor de Cache de saída Redis.</span><span class="sxs-lookup"><span data-stu-id="1155d-108">This topic provides guidance on configuring your application toouse hello Redis Output Cache Provider.</span></span> <span data-ttu-id="1155d-109">Para saber mais sobre como criar e configurar uma instância do Cache Redis do Azure, consulte [Criar um cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span><span class="sxs-lookup"><span data-stu-id="1155d-109">For more information about creating and configuring an Azure Redis Cache instance, see [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

## <a name="store-aspnet-page-output-in-hello-cache"></a><span data-ttu-id="1155d-110">Armazenar a saída de página ASP.NET no cache de saudação</span><span class="sxs-lookup"><span data-stu-id="1155d-110">Store ASP.NET page output in hello cache</span></span>
<span data-ttu-id="1155d-111">tooconfigure um aplicativo cliente no Visual Studio usando o pacote de NuGet de estado de sessão de Cache Redis hello, clique em **NuGet Package Manager**, **Package Manager Console** de saudação **ferramentas** menu.</span><span class="sxs-lookup"><span data-stu-id="1155d-111">tooconfigure a client application in Visual Studio using hello Redis Cache Session State NuGet package, click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>

<span data-ttu-id="1155d-112">Execução hello seguinte comando do hello `Package Manager Console` janela.</span><span class="sxs-lookup"><span data-stu-id="1155d-112">Run hello following command from hello `Package Manager Console` window.</span></span>
    
```
Install-Package Microsoft.Web.RedisOutputCacheProvider
```

<span data-ttu-id="1155d-113">pacote de NuGet de provedor de Cache de saída Redis Olá tem uma dependência Olá pacote Stackexchange.</span><span class="sxs-lookup"><span data-stu-id="1155d-113">hello Redis Output Cache Provider NuGet package has a dependency on hello StackExchange.Redis.StrongName package.</span></span> <span data-ttu-id="1155d-114">Se o pacote de Stackexchange Olá não está presente no seu projeto, ele é instalado.</span><span class="sxs-lookup"><span data-stu-id="1155d-114">If hello StackExchange.Redis.StrongName package is not present in your project, it is installed.</span></span> <span data-ttu-id="1155d-115">Para obter mais informações sobre o pacote de NuGet de provedor de Cache de saída Redis hello, consulte Olá [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) página NuGet.</span><span class="sxs-lookup"><span data-stu-id="1155d-115">For more information about hello Redis Output Cache Provider NuGet package, see hello [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet page.</span></span>

>[!NOTE]
><span data-ttu-id="1155d-116">Em adição toohello fortes Stackexchange pacote, também há Olá Stackexchange não-versão de nome forte.</span><span class="sxs-lookup"><span data-stu-id="1155d-116">In addition toohello strong-named StackExchange.Redis.StrongName package, there is also hello StackExchange.Redis non-strong-named version.</span></span> <span data-ttu-id="1155d-117">Se seu projeto está usando Olá não-versão de nome forte Stackexchange que você deve desinstalá-lo, caso contrário você conflitos de nomenclatura no projeto.</span><span class="sxs-lookup"><span data-stu-id="1155d-117">If your project is using hello non-strong-named StackExchange.Redis version you must uninstall it, otherwise you get naming conflicts in your project.</span></span> <span data-ttu-id="1155d-118">Para saber mais sobre esses pacotes, consulte [Configurar clientes de cache .NET](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span><span class="sxs-lookup"><span data-stu-id="1155d-118">For more information about these packages, see [Configure .NET cache clients](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span></span>
>
>

<span data-ttu-id="1155d-119">Olá NuGet pacote baixa e adiciona Olá necessário assembly faz referência e adiciona Olá seção a seguir no arquivo Web. config.</span><span class="sxs-lookup"><span data-stu-id="1155d-119">hello NuGet package downloads and adds hello required assembly references and adds hello following section into your web.config file.</span></span> <span data-ttu-id="1155d-120">Esta seção contém a configuração necessária Olá para sua saudação de toouse de aplicativo do ASP.NET provedor de Cache de saída Redis.</span><span class="sxs-lookup"><span data-stu-id="1155d-120">This section contains hello required configuration for your ASP.NET application toouse hello Redis Output Cache Provider.</span></span>

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

<span data-ttu-id="1155d-121">Olá comentado seção fornece um exemplo dos atributos de saudação e configurações de exemplo para cada atributo.</span><span class="sxs-lookup"><span data-stu-id="1155d-121">hello commented section provides an example of hello attributes and sample settings for each attribute.</span></span>

<span data-ttu-id="1155d-122">Configurar atributos de saudação com valores de saudação da sua folha de cache no portal do Microsoft Azure hello e configurar Olá outros valores conforme desejado.</span><span class="sxs-lookup"><span data-stu-id="1155d-122">Configure hello attributes with hello values from your cache blade in hello Microsoft Azure portal, and configure hello other values as desired.</span></span> <span data-ttu-id="1155d-123">Para obter instruções sobre como acessar as propriedades do cache, consulte [Definir as configurações de cache Redis](cache-configure.md#configure-redis-cache-settings).</span><span class="sxs-lookup"><span data-stu-id="1155d-123">For instructions on accessing your cache properties, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

* <span data-ttu-id="1155d-124">**host** – especifique o ponto de extremidade do cache.</span><span class="sxs-lookup"><span data-stu-id="1155d-124">**host** – specify your cache endpoint.</span></span>
* <span data-ttu-id="1155d-125">**porta** – usar a porta não SSL ou a porta SSL, dependendo das configurações de ssl hello.</span><span class="sxs-lookup"><span data-stu-id="1155d-125">**port** – use either your non-SSL port or your SSL port, depending on hello ssl settings.</span></span>
* <span data-ttu-id="1155d-126">**accessKey** – usar a chave primária ou secundária de saudação para seu cache.</span><span class="sxs-lookup"><span data-stu-id="1155d-126">**accessKey** – use either hello primary or secondary key for your cache.</span></span>
* <span data-ttu-id="1155d-127">**SSL** – verdadeiro se desejar toosecure comunicações de cache e cliente com ssl; caso contrário, false.</span><span class="sxs-lookup"><span data-stu-id="1155d-127">**ssl** – true if you want toosecure cache/client communications with ssl; otherwise false.</span></span> <span data-ttu-id="1155d-128">Ser se toospecify Olá correto da porta.</span><span class="sxs-lookup"><span data-stu-id="1155d-128">Be sure toospecify hello correct port.</span></span>
  * <span data-ttu-id="1155d-129">porta do Hello não SSL está desabilitada por padrão para novos caches.</span><span class="sxs-lookup"><span data-stu-id="1155d-129">hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="1155d-130">Especifique true para essa saudação de toouse configuração porta SSL.</span><span class="sxs-lookup"><span data-stu-id="1155d-130">Specify true for this setting toouse hello SSL port.</span></span> <span data-ttu-id="1155d-131">Para obter mais informações sobre como habilitar a porta não SSL de hello, consulte Olá [portas de acesso](cache-configure.md#access-ports) seção Olá [configurar um cache](cache-configure.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="1155d-131">For more information about enabling hello non-SSL port, see hello [Access Ports](cache-configure.md#access-ports) section in hello [Configure a cache](cache-configure.md) topic.</span></span>
* <span data-ttu-id="1155d-132">**databaseId** – especificado toouse qual banco de dados para o cache de saída de dados.</span><span class="sxs-lookup"><span data-stu-id="1155d-132">**databaseId** – Specified which database toouse for cache output data.</span></span> <span data-ttu-id="1155d-133">Se não for especificado, o valor padrão Olá 0 é usado.</span><span class="sxs-lookup"><span data-stu-id="1155d-133">If not specified, hello default value of 0 is used.</span></span>
* <span data-ttu-id="1155d-134">**applicationName** – As chaves são armazenadas em redis como `<AppName>_<SessionId>_Data`.</span><span class="sxs-lookup"><span data-stu-id="1155d-134">**applicationName** – Keys are stored in redis as `<AppName>_<SessionId>_Data`.</span></span> <span data-ttu-id="1155d-135">Esse esquema de nomenclatura permite que vários Olá de tooshare aplicativos mesma chave.</span><span class="sxs-lookup"><span data-stu-id="1155d-135">This naming scheme enables multiple applications tooshare hello same key.</span></span> <span data-ttu-id="1155d-136">Esse parâmetro é opcional e, se você não fornecê-lo, um valor padrão será usado.</span><span class="sxs-lookup"><span data-stu-id="1155d-136">This parameter is optional and if you do not provide it a default value is used.</span></span>
* <span data-ttu-id="1155d-137">**connectionTimeoutInMilliseconds** – essa configuração permite que você toooverride Olá connectTimeout definindo no cliente stackexchange. Redis de saudação.</span><span class="sxs-lookup"><span data-stu-id="1155d-137">**connectionTimeoutInMilliseconds** – This setting allows you toooverride hello connectTimeout setting in hello StackExchange.Redis client.</span></span> <span data-ttu-id="1155d-138">Se não for especificado, a configuração de connectTimeout saudação padrão de 5000 é usada.</span><span class="sxs-lookup"><span data-stu-id="1155d-138">If not specified, hello default connectTimeout setting of 5000 is used.</span></span> <span data-ttu-id="1155d-139">Para saber mais, consulte [Modelo de configuração StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).</span><span class="sxs-lookup"><span data-stu-id="1155d-139">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>
* <span data-ttu-id="1155d-140">**operationTimeoutInMilliseconds** – essa configuração permite que você toooverride Olá syncTimeout definindo no cliente stackexchange. Redis de saudação.</span><span class="sxs-lookup"><span data-stu-id="1155d-140">**operationTimeoutInMilliseconds** – This setting allows you toooverride hello syncTimeout setting in hello StackExchange.Redis client.</span></span> <span data-ttu-id="1155d-141">Se não for especificado, a configuração de syncTimeout saudação padrão de 1000 é usada.</span><span class="sxs-lookup"><span data-stu-id="1155d-141">If not specified, hello default syncTimeout setting of 1000 is used.</span></span> <span data-ttu-id="1155d-142">Para saber mais, consulte [Modelo de configuração StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).</span><span class="sxs-lookup"><span data-stu-id="1155d-142">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>

<span data-ttu-id="1155d-143">Adicione uma página de tooeach diretiva OutputCache para o qual você deseja toocache saída de hello.</span><span class="sxs-lookup"><span data-stu-id="1155d-143">Add an OutputCache directive tooeach page for which you wish toocache hello output.</span></span>

```
<%@ OutputCache Duration="60" VaryByParam="*" %>
```

<span data-ttu-id="1155d-144">No exemplo anterior de saudação, Olá armazenadas em cache dados de página permanece no cache de saudação por 60 segundos e uma versão diferente da página de saudação é armazenado em cache para cada combinação de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="1155d-144">In hello previous example, hello cached page data remains in hello cache for 60 seconds, and a different version of hello page is cached for each parameter combination.</span></span> <span data-ttu-id="1155d-145">Para obter mais informações sobre a diretiva OutputCache de hello, consulte [ @OutputCache ](http://go.microsoft.com/fwlink/?linkid=320837).</span><span class="sxs-lookup"><span data-stu-id="1155d-145">For more information about hello OutputCache directive, see [@OutputCache](http://go.microsoft.com/fwlink/?linkid=320837).</span></span>

<span data-ttu-id="1155d-146">Quando essas etapas são executadas, seu aplicativo é configurado toouse Olá provedor de Cache de saída Redis.</span><span class="sxs-lookup"><span data-stu-id="1155d-146">Once these steps are performed, your application is configured toouse hello Redis Output Cache Provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1155d-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1155d-147">Next steps</span></span>
<span data-ttu-id="1155d-148">Check-out Olá [provedor de estado de sessão do ASP.NET para Cache Redis do Azure](cache-aspnet-session-state-provider.md).</span><span class="sxs-lookup"><span data-stu-id="1155d-148">Check out hello [ASP.NET Session State Provider for Azure Redis Cache](cache-aspnet-session-state-provider.md).</span></span>

