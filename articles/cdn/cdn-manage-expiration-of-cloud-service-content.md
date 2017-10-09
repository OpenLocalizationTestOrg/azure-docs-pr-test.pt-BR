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
# <a name="manage-expiration-of-azure-web-appscloud-services-aspnet-or-iis-content-in-azure-cdn"></a>Gerenciar a expiração de conteúdo de Serviços de Nuvem/Aplicativos Web do Azure, ASP.NET ou IIS na CDN do Azure
> [!div class="op_single_selector"]
> * [Serviços de Nuvem/Aplicativos Web do Azure, ASP.NET ou IIS](cdn-manage-expiration-of-cloud-service-content.md)
> * [Serviço Blob do Armazenamento do Azure](cdn-manage-expiration-of-blob-content.md)
> 
> 

Arquivos de qualquer servidor Web de origem publicamente acessível podem ser armazenados em cache no Azure CDN até que o TTL (tempo de vida) tenha decorrido.  Olá TTL é determinado pelo Olá [ *Cache-Control* cabeçalho](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) na resposta HTTP de saudação do servidor de origem de saudação.  Este artigo descreve como tooset `Cache-Control` cabeçalhos para aplicativos Web do Azure e sites de Internet Information Services, que são configurados da mesma forma, aplicativos ASP.NET e serviços de nuvem do Azure.

> [!TIP]
> Você não pode escolher tooset nenhum TTL em um arquivo.  Nesse caso, o Azure CDN aplica automaticamente um TTL padrão de sete dias.
> 
> Para obter mais informações sobre como funciona o Azure CDN toospeed toofiles de acesso e outros recursos, consulte Olá [visão geral do Azure CDN](cdn-overview.md).
> 
> 

## <a name="setting-cache-control-headers-in-configuration"></a>Definindo cabeçalhos Cache-Control na configuração
Conteúdo estático, como imagens e folhas de estilo, você pode controlar a frequência de atualização de saudação modificando Olá **applicationHost. config** ou **Web. config** arquivos para o aplicativo web.  Olá **system.webServer\staticContent\clientCache** elemento no arquivo de configuração de saudação definirá Olá `Cache-Control` cabeçalho para o seu conteúdo. Para **Web. config**, definições de configuração de saudação afetarão tudo na pasta hello e todas as subpastas, a menos que substituído no nível de subpasta hello.  Por exemplo, você pode definir um padrão time-to-live em Olá raiz toohave todo o conteúdo estático armazenado em cache por 3 dias, mas tem uma subpasta que tenha mais variável conteúdo com uma configuração de cache de 6 horas.  Para **applicationHost. config**, todos os aplicativos no site hello serão afetados, mas pode ser substituídos em **Web. config** arquivos em aplicativos de saudação.

Olá, XML a seguir mostra um exemplo de configuração **clientCache** toospecify a duração máxima de 3 dias:  

```xml
<configuration>
    <system.webServer>
        <staticContent>
            <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00" />
        </staticContent>
    </system.webServer>
</configuration>
```

Especificando **UseMaxAge** adiciona um `Cache-Control: max-age=<nnn>` resposta do cabeçalho toohello com base no valor de saudação especificado no hello **CacheControlMaxAge** atributo. formato de saudação de timespan Olá é para Olá **cacheControlMaxAge** atributo é <days>.<hours>:<min>:<sec>. Para obter mais informações sobre Olá **clientCache** nó, consulte [Cache do cliente <clientCache> ](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).  

## <a name="setting-cache-control-headers-in-code"></a>Definindo cabeçalhos Cache-Control no código
Para aplicativos ASP.NET, você pode definir o comportamento do cache de CDN Olá programaticamente, definindo Olá **HttpResponse** propriedade. Para obter mais informações sobre Olá **HttpResponse** propriedade, consulte [propriedade HttpResponse](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) e [classe HttpCachePolicy](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).  

Se desejar que o conteúdo do aplicativo de cache tooprogrammatically no ASP.NET, certifique-se de que o conteúdo de saudação está marcado como armazenável em cache, definindo HttpCacheability muito*público*. Além disso, verifique se um validador de cache está definido. Validador de cache Olá pode ser a última modificação timestamp definido ao chamar SetLastModified ou um valor de etag definido ao chamar SetETag. Opcionalmente, você também pode especificar um tempo de expiração de cache chamando SetExpires ou você pode confiar na heurística de cache padrão de saudação descrita anteriormente neste documento.  

Por exemplo, toocache o conteúdo de uma hora, adicione o seguinte hello:  

```csharp
// Set hello caching parameters.
Response.Cache.SetExpires(DateTime.Now.AddHours(1));
Response.Cache.SetCacheability(HttpCacheability.Public);
Response.Cache.SetLastModified(DateTime.Now);
```

## <a name="next-steps"></a>Próximas etapas
* [Ler os detalhes sobre Olá **clientCache** elemento](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)
* [Leia a documentação Olá Olá **HttpResponse** propriedade](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) 
* [Leia a documentação Olá Olá **classe HttpCachePolicy**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).  

