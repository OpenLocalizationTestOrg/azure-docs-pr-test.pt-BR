---
title: "aaaException de gerenciamento - ferramenta de modelagem de ameaça Microsoft - Azure | Microsoft Docs"
description: "reduções de ameaças expostas em Olá, ferramenta de modelagem de ameaça"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 247096c10deeca94ebb9b19df7ba60e442ca1e4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-exception-management--mitigations"></a><span data-ttu-id="bfd4f-103">Quadro de Segurança: Gerenciamento de Exceções | Atenuações</span><span class="sxs-lookup"><span data-stu-id="bfd4f-103">Security Frame: Exception Management | Mitigations</span></span> 
| <span data-ttu-id="bfd4f-104">Produto/Serviço</span><span class="sxs-lookup"><span data-stu-id="bfd4f-104">Product/Service</span></span> | <span data-ttu-id="bfd4f-105">Artigo</span><span class="sxs-lookup"><span data-stu-id="bfd4f-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="bfd4f-106">**WCF**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-106">**WCF**</span></span> | <ul><li>[<span data-ttu-id="bfd4f-107">WCF - não inclui o nó serviceDebug no arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="bfd4f-107">WCF- Do not include serviceDebug node in configuration file</span></span>](#servicedebug)</li><li>[<span data-ttu-id="bfd4f-108">WCF - não inclui o nó serviceMetadata no arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="bfd4f-108">WCF- Do not include serviceMetadata node in configuration file</span></span>](#servicemetadata)</li></ul> |
| <span data-ttu-id="bfd4f-109">**API da Web**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-109">**Web API**</span></span> | <ul><li>[<span data-ttu-id="bfd4f-110">Verificar se o tratamento de exceções adequado é feito na API Web ASP.NET </span><span class="sxs-lookup"><span data-stu-id="bfd4f-110">Ensure that proper exception handling is done in ASP.NET Web API </span></span>](#exception)</li></ul> |
| <span data-ttu-id="bfd4f-111">**Aplicativo Web**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-111">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="bfd4f-112">Não expor os detalhes da segurança nas mensagens de erro </span><span class="sxs-lookup"><span data-stu-id="bfd4f-112">Do not expose security details in error messages </span></span>](#messages)</li><li>[<span data-ttu-id="bfd4f-113">Implementar a página tratamento de erros Padrão </span><span class="sxs-lookup"><span data-stu-id="bfd4f-113">Implement Default error handling page </span></span>](#default)</li><li>[<span data-ttu-id="bfd4f-114">Definir o método de implantação tooRetail no IIS</span><span class="sxs-lookup"><span data-stu-id="bfd4f-114">Set Deployment Method tooRetail in IIS</span></span>](#deployment)</li><li>[<span data-ttu-id="bfd4f-115">As exceções devem falhar com segurança</span><span class="sxs-lookup"><span data-stu-id="bfd4f-115">Exceptions should fail safely</span></span>](#fail)</li></ul> |

## <span data-ttu-id="bfd4f-116"><a id="servicedebug"></a>WCF - não inclui o nó serviceDebug no arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="bfd4f-116"><a id="servicedebug"></a>WCF- Do not include serviceDebug node in configuration file</span></span>

| <span data-ttu-id="bfd4f-117">Title</span><span class="sxs-lookup"><span data-stu-id="bfd4f-117">Title</span></span>                   | <span data-ttu-id="bfd4f-118">Detalhes</span><span class="sxs-lookup"><span data-stu-id="bfd4f-118">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="bfd4f-119">**Componente**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-119">**Component**</span></span>               | <span data-ttu-id="bfd4f-120">WCF</span><span class="sxs-lookup"><span data-stu-id="bfd4f-120">WCF</span></span> | 
| <span data-ttu-id="bfd4f-121">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-121">**SDL Phase**</span></span>               | <span data-ttu-id="bfd4f-122">Compilação</span><span class="sxs-lookup"><span data-stu-id="bfd4f-122">Build</span></span> |  
| <span data-ttu-id="bfd4f-123">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-123">**Applicable Technologies**</span></span> | <span data-ttu-id="bfd4f-124">Genérico, NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="bfd4f-124">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="bfd4f-125">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-125">**Attributes**</span></span>              | <span data-ttu-id="bfd4f-126">N/D</span><span class="sxs-lookup"><span data-stu-id="bfd4f-126">N/A</span></span>  |
| <span data-ttu-id="bfd4f-127">**Referências**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-127">**References**</span></span>              | <span data-ttu-id="bfd4f-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="bfd4f-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="bfd4f-129">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-129">**Steps**</span></span> | <span data-ttu-id="bfd4f-130">Serviços Windows Communication Framework (WCF) podem ser configurado tooexpose as informações de depuração.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-130">Windows Communication Framework (WCF) services can be configured tooexpose debugging information.</span></span> <span data-ttu-id="bfd4f-131">As informações de depuração não devem ser usadas nos ambientes de produção.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-131">Debug information should not be used in production environments.</span></span> <span data-ttu-id="bfd4f-132">Olá `<serviceDebug>` marca define se o recurso de saudação de informações de depuração está habilitado para um serviço WCF.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-132">hello `<serviceDebug>` tag defines whether hello debug information feature is enabled for a WCF service.</span></span> <span data-ttu-id="bfd4f-133">Se Olá atributo includeExceptionDetailInFaults for definido tootrue, informações de exceção de aplicativo hello retornará tooclients.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-133">If hello attribute includeExceptionDetailInFaults is set tootrue, exception information from hello application will be returned tooclients.</span></span> <span data-ttu-id="bfd4f-134">Os invasores podem aproveitar informações adicionais de saudação obterem a depuração de saída toomount ataques direcionados framework hello, banco de dados ou outros recursos usados pelo aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-134">Attackers can leverage hello additional information they gain from debugging output toomount attacks targeted on hello framework, database, or other resources used by hello application.</span></span> |

### <a name="example"></a><span data-ttu-id="bfd4f-135">Exemplo</span><span class="sxs-lookup"><span data-stu-id="bfd4f-135">Example</span></span>
<span data-ttu-id="bfd4f-136">Olá, seguinte arquivo de configuração inclui Olá `<serviceDebug>` marca:</span><span class="sxs-lookup"><span data-stu-id="bfd4f-136">hello following configuration file includes hello `<serviceDebug>` tag:</span></span> 
```
<configuration> 
<system.serviceModel> 
<behaviors> 
<serviceBehaviors> 
<behavior name=""MyServiceBehavior""> 
<serviceDebug includeExceptionDetailInFaults=""True"" httpHelpPageEnabled=""True""/> 
... 
```
<span data-ttu-id="bfd4f-137">Desabilite as informações de depuração no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-137">Disable debugging information in hello service.</span></span> <span data-ttu-id="bfd4f-138">Isso pode ser feito removendo Olá `<serviceDebug>` marca de arquivo de configuração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-138">This can be accomplished by removing hello `<serviceDebug>` tag from your application's configuration file.</span></span> 

## <span data-ttu-id="bfd4f-139"><a id="servicemetadata"></a>WCF - não inclui o nó serviceMetadata no arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="bfd4f-139"><a id="servicemetadata"></a>WCF- Do not include serviceMetadata node in configuration file</span></span>

| <span data-ttu-id="bfd4f-140">Title</span><span class="sxs-lookup"><span data-stu-id="bfd4f-140">Title</span></span>                   | <span data-ttu-id="bfd4f-141">Detalhes</span><span class="sxs-lookup"><span data-stu-id="bfd4f-141">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="bfd4f-142">**Componente**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-142">**Component**</span></span>               | <span data-ttu-id="bfd4f-143">WCF</span><span class="sxs-lookup"><span data-stu-id="bfd4f-143">WCF</span></span> | 
| <span data-ttu-id="bfd4f-144">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-144">**SDL Phase**</span></span>               | <span data-ttu-id="bfd4f-145">Compilação</span><span class="sxs-lookup"><span data-stu-id="bfd4f-145">Build</span></span> |  
| <span data-ttu-id="bfd4f-146">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-146">**Applicable Technologies**</span></span> | <span data-ttu-id="bfd4f-147">Genérico</span><span class="sxs-lookup"><span data-stu-id="bfd4f-147">Generic</span></span> |
| <span data-ttu-id="bfd4f-148">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-148">**Attributes**</span></span>              | <span data-ttu-id="bfd4f-149">Genérico, NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="bfd4f-149">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="bfd4f-150">**Referências**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-150">**References**</span></span>              | <span data-ttu-id="bfd4f-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="bfd4f-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="bfd4f-152">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-152">**Steps**</span></span> | <span data-ttu-id="bfd4f-153">Expor publicamente informações sobre um serviço pode fornecer aos invasores informações valiosas em como eles podem explorar o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-153">Publicly exposing information about a service can provide attackers with valuable insight into how they might exploit hello service.</span></span> <span data-ttu-id="bfd4f-154">Olá `<serviceMetadata>` marca permite que o recurso de publicação de metadados de saudação.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-154">hello `<serviceMetadata>` tag enables hello metadata publishing feature.</span></span> <span data-ttu-id="bfd4f-155">Os metadados do serviço podem conter informações confidenciais e não devem ser acessíveis publicamente.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-155">Service metadata could contain sensitive information that should not be publicly accessible.</span></span> <span data-ttu-id="bfd4f-156">No mínimo, permitir somente usuários confiáveis tooaccess Olá metadados e certifique-se de que informações desnecessárias não são expostas.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-156">At a minimum, only allow trusted users tooaccess hello metadata and ensure that unnecessary information is not exposed.</span></span> <span data-ttu-id="bfd4f-157">Melhor ainda, desabilite totalmente Olá capacidade toopublish metadados.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-157">Better yet, entirely disable hello ability toopublish metadata.</span></span> <span data-ttu-id="bfd4f-158">Uma configuração segura do WCF não conterá Olá `<serviceMetadata>` marca.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-158">A safe WCF configuration will not contain hello `<serviceMetadata>` tag.</span></span> |

## <span data-ttu-id="bfd4f-159"><a id="exception"></a>Verificar se o tratamento de exceções adequado é feito na API Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="bfd4f-159"><a id="exception"></a>Ensure that proper exception handling is done in ASP.NET Web API</span></span>

| <span data-ttu-id="bfd4f-160">Title</span><span class="sxs-lookup"><span data-stu-id="bfd4f-160">Title</span></span>                   | <span data-ttu-id="bfd4f-161">Detalhes</span><span class="sxs-lookup"><span data-stu-id="bfd4f-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="bfd4f-162">**Componente**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-162">**Component**</span></span>               | <span data-ttu-id="bfd4f-163">API Web</span><span class="sxs-lookup"><span data-stu-id="bfd4f-163">Web API</span></span> | 
| <span data-ttu-id="bfd4f-164">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-164">**SDL Phase**</span></span>               | <span data-ttu-id="bfd4f-165">Compilação</span><span class="sxs-lookup"><span data-stu-id="bfd4f-165">Build</span></span> |  
| <span data-ttu-id="bfd4f-166">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-166">**Applicable Technologies**</span></span> | <span data-ttu-id="bfd4f-167">MVC 5, MVC 6</span><span class="sxs-lookup"><span data-stu-id="bfd4f-167">MVC 5, MVC 6</span></span> |
| <span data-ttu-id="bfd4f-168">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-168">**Attributes**</span></span>              | <span data-ttu-id="bfd4f-169">N/D</span><span class="sxs-lookup"><span data-stu-id="bfd4f-169">N/A</span></span>  |
| <span data-ttu-id="bfd4f-170">**Referências**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-170">**References**</span></span>              | <span data-ttu-id="bfd4f-171">[Tratamento de Exceções na API Web ASP.NET](http://www.asp.net/web-api/overview/error-handling/exception-handling), [Validação do Modelo na API Web ASP.NET](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span><span class="sxs-lookup"><span data-stu-id="bfd4f-171">[Exception Handling in ASP.NET Web API](http://www.asp.net/web-api/overview/error-handling/exception-handling), [Model Validation in ASP.NET Web API](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span></span> |
| <span data-ttu-id="bfd4f-172">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-172">**Steps**</span></span> | <span data-ttu-id="bfd4f-173">Por padrão, a maioria das exceções não identificadas na API Web ASP.NET é convertida em uma resposta HTTP com um código de status`500, Internal Server Error`</span><span class="sxs-lookup"><span data-stu-id="bfd4f-173">By default, most uncaught exceptions in ASP.NET Web API are translated into an HTTP response with status code `500, Internal Server Error`</span></span>|

### <a name="example"></a><span data-ttu-id="bfd4f-174">Exemplo</span><span class="sxs-lookup"><span data-stu-id="bfd4f-174">Example</span></span>
<span data-ttu-id="bfd4f-175">código de status de saudação toocontrol retornado por Olá API, `HttpResponseException` pode ser usado como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="bfd4f-175">toocontrol hello status code returned by hello API, `HttpResponseException` can be used as shown below:</span></span> 
```C#
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        throw new HttpResponseException(HttpStatusCode.NotFound);
    }
    return item;
}
```

### <a name="example"></a><span data-ttu-id="bfd4f-176">Exemplo</span><span class="sxs-lookup"><span data-stu-id="bfd4f-176">Example</span></span>
<span data-ttu-id="bfd4f-177">Para controlar ainda mais na resposta de exceção hello, Olá `HttpResponseMessage` classe pode ser usada, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="bfd4f-177">For further control on hello exception response, hello `HttpResponseMessage` class can be used as shown below:</span></span> 
```C#
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        var resp = new HttpResponseMessage(HttpStatusCode.NotFound)
        {
            Content = new StringContent(string.Format("No product with ID = {0}", id)),
            ReasonPhrase = "Product ID Not Found"
        }
        throw new HttpResponseException(resp);
    }
    return item;
}
```
<span data-ttu-id="bfd4f-178">toocatch sem tratamento de exceções que não são do tipo hello `HttpResponseException`, filtros de exceção pode ser usados.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-178">toocatch unhandled exceptions that are not of hello type `HttpResponseException`, Exception Filters can be used.</span></span> <span data-ttu-id="bfd4f-179">Filtros de exceção implementam Olá `System.Web.Http.Filters.IExceptionFilter` interface.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-179">Exception filters implement hello `System.Web.Http.Filters.IExceptionFilter` interface.</span></span> <span data-ttu-id="bfd4f-180">toowrite de maneira mais simples de saudação um filtro de exceção é tooderive de saudação `System.Web.Http.Filters.ExceptionFilterAttribute` classe e substituir o método OnException de saudação.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-180">hello simplest way toowrite an exception filter is tooderive from hello `System.Web.Http.Filters.ExceptionFilterAttribute` class and override hello OnException method.</span></span> 

### <a name="example"></a><span data-ttu-id="bfd4f-181">Exemplo</span><span class="sxs-lookup"><span data-stu-id="bfd4f-181">Example</span></span>
<span data-ttu-id="bfd4f-182">Aqui está um filtro que converte as exceções `NotImplementedException` no código de status HTTP `501, Not Implemented`:</span><span class="sxs-lookup"><span data-stu-id="bfd4f-182">Here is a filter that converts `NotImplementedException` exceptions into HTTP status code `501, Not Implemented`:</span></span> 
```C#
namespace ProductStore.Filters
{
    using System;
    using System.Net;
    using System.Net.Http;
    using System.Web.Http.Filters;

    public class NotImplExceptionFilterAttribute : ExceptionFilterAttribute 
    {
        public override void OnException(HttpActionExecutedContext context)
        {
            if (context.Exception is NotImplementedException)
            {
                context.Response = new HttpResponseMessage(HttpStatusCode.NotImplemented);
            }
        }
    }
}
```

<span data-ttu-id="bfd4f-183">Há várias maneiras tooregister um filtro de exceção de API da Web:</span><span class="sxs-lookup"><span data-stu-id="bfd4f-183">There are several ways tooregister a Web API exception filter:</span></span>
- <span data-ttu-id="bfd4f-184">por ação</span><span class="sxs-lookup"><span data-stu-id="bfd4f-184">By action</span></span>
- <span data-ttu-id="bfd4f-185">pelo controlador</span><span class="sxs-lookup"><span data-stu-id="bfd4f-185">By controller</span></span>
- <span data-ttu-id="bfd4f-186">globalmente</span><span class="sxs-lookup"><span data-stu-id="bfd4f-186">Globally</span></span>

### <a name="example"></a><span data-ttu-id="bfd4f-187">Exemplo</span><span class="sxs-lookup"><span data-stu-id="bfd4f-187">Example</span></span>
<span data-ttu-id="bfd4f-188">Olá tooapply filtrar ação específica tooa, adicionar filtro hello como uma ação de toohello do atributo:</span><span class="sxs-lookup"><span data-stu-id="bfd4f-188">tooapply hello filter tooa specific action, add hello filter as an attribute toohello action:</span></span> 
```C#
public class ProductsController : ApiController
{
    [NotImplExceptionFilter]
    public Contact GetContact(int id)
    {
        throw new NotImplementedException("This method is not implemented");
    }
}
```
### <a name="example"></a><span data-ttu-id="bfd4f-189">Exemplo</span><span class="sxs-lookup"><span data-stu-id="bfd4f-189">Example</span></span>
<span data-ttu-id="bfd4f-190">tooapply Olá filtro tooall de ações de saudação em uma `controller`, adicionar filtro hello como um atributo toohello `controller` classe:</span><span class="sxs-lookup"><span data-stu-id="bfd4f-190">tooapply hello filter tooall of hello actions on a `controller`, add hello filter as an attribute toohello `controller` class:</span></span> 

```C#
[NotImplExceptionFilter]
public class ProductsController : ApiController
{
    // ...
}
```

### <a name="example"></a><span data-ttu-id="bfd4f-191">Exemplo</span><span class="sxs-lookup"><span data-stu-id="bfd4f-191">Example</span></span>
<span data-ttu-id="bfd4f-192">Olá tooapply globalmente filtrar controladores de API da Web tooall, adicionar uma instância de saudação filtro toohello `GlobalConfiguration.Configuration.Filters` coleção.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-192">tooapply hello filter globally tooall Web API controllers, add an instance of hello filter toohello `GlobalConfiguration.Configuration.Filters` collection.</span></span> <span data-ttu-id="bfd4f-193">Filtros de exceção nesta coleção se aplicam a ação de controlador tooany API da Web.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-193">Exception filters in this collection apply tooany Web API controller action.</span></span> 
```C#
GlobalConfiguration.Configuration.Filters.Add(
    new ProductStore.NotImplExceptionFilterAttribute());
```

### <a name="example"></a><span data-ttu-id="bfd4f-194">Exemplo</span><span class="sxs-lookup"><span data-stu-id="bfd4f-194">Example</span></span>
<span data-ttu-id="bfd4f-195">Para validação de modelo, o estado de modelo Olá pode ser passado tooCreateErrorResponse método conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="bfd4f-195">For model validation, hello model state can be passed tooCreateErrorResponse method as shown below:</span></span> 
```C#
public HttpResponseMessage PostProduct(Product item)
{
    if (!ModelState.IsValid)
    {
        return Request.CreateErrorResponse(HttpStatusCode.BadRequest, ModelState);
    }
    // Implementation not shown...
}
```

<span data-ttu-id="bfd4f-196">Seleção Olá links na seção de referências de saudação para obter detalhes adicionais sobre manipulação excepcional e validação de modelo na API da Web do ASP.Net</span><span class="sxs-lookup"><span data-stu-id="bfd4f-196">Check hello links in hello references section for additional details about exceptional handling and model validation in ASP.Net Web API</span></span> 

## <span data-ttu-id="bfd4f-197"><a id="messages"></a>Não expor os detalhes da segurança nas mensagens de erro</span><span class="sxs-lookup"><span data-stu-id="bfd4f-197"><a id="messages"></a>Do not expose security details in error messages</span></span>

| <span data-ttu-id="bfd4f-198">Title</span><span class="sxs-lookup"><span data-stu-id="bfd4f-198">Title</span></span>                   | <span data-ttu-id="bfd4f-199">Detalhes</span><span class="sxs-lookup"><span data-stu-id="bfd4f-199">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="bfd4f-200">**Componente**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-200">**Component**</span></span>               | <span data-ttu-id="bfd4f-201">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="bfd4f-201">Web Application</span></span> | 
| <span data-ttu-id="bfd4f-202">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-202">**SDL Phase**</span></span>               | <span data-ttu-id="bfd4f-203">Compilação</span><span class="sxs-lookup"><span data-stu-id="bfd4f-203">Build</span></span> |  
| <span data-ttu-id="bfd4f-204">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-204">**Applicable Technologies**</span></span> | <span data-ttu-id="bfd4f-205">Genérico</span><span class="sxs-lookup"><span data-stu-id="bfd4f-205">Generic</span></span> |
| <span data-ttu-id="bfd4f-206">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-206">**Attributes**</span></span>              | <span data-ttu-id="bfd4f-207">N/D</span><span class="sxs-lookup"><span data-stu-id="bfd4f-207">N/A</span></span>  |
| <span data-ttu-id="bfd4f-208">**Referências**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-208">**References**</span></span>              | <span data-ttu-id="bfd4f-209">N/D</span><span class="sxs-lookup"><span data-stu-id="bfd4f-209">N/A</span></span>  |
| <span data-ttu-id="bfd4f-210">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-210">**Steps**</span></span> | <p><span data-ttu-id="bfd4f-211">Mensagens de erro genéricas são fornecidas diretamente toohello usuário sem incluir dados confidenciais de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-211">Generic error messages are provided directly toohello user without including sensitive application data.</span></span> <span data-ttu-id="bfd4f-212">Exemplos de dados confidenciais:</span><span class="sxs-lookup"><span data-stu-id="bfd4f-212">Examples of sensitive data include:</span></span></p><ul><li><span data-ttu-id="bfd4f-213">nomes do servidor</span><span class="sxs-lookup"><span data-stu-id="bfd4f-213">Server names</span></span></li><li><span data-ttu-id="bfd4f-214">Cadeias de conexão</span><span class="sxs-lookup"><span data-stu-id="bfd4f-214">Connection strings</span></span></li><li><span data-ttu-id="bfd4f-215">nomes de usuário</span><span class="sxs-lookup"><span data-stu-id="bfd4f-215">Usernames</span></span></li><li><span data-ttu-id="bfd4f-216">Senhas</span><span class="sxs-lookup"><span data-stu-id="bfd4f-216">Passwords</span></span></li><li><span data-ttu-id="bfd4f-217">procedimentos SQL</span><span class="sxs-lookup"><span data-stu-id="bfd4f-217">SQL procedures</span></span></li><li><span data-ttu-id="bfd4f-218">detalhes das falhas SQL dinâmicas</span><span class="sxs-lookup"><span data-stu-id="bfd4f-218">Details of dynamic SQL failures</span></span></li><li><span data-ttu-id="bfd4f-219">rastreamento de pilha e linhas de código</span><span class="sxs-lookup"><span data-stu-id="bfd4f-219">Stack trace and lines of code</span></span></li><li><span data-ttu-id="bfd4f-220">variáveis armazenadas na memória</span><span class="sxs-lookup"><span data-stu-id="bfd4f-220">Variables stored in memory</span></span></li><li><span data-ttu-id="bfd4f-221">locais da pasta e da unidade</span><span class="sxs-lookup"><span data-stu-id="bfd4f-221">Drive and folder locations</span></span></li><li><span data-ttu-id="bfd4f-222">pontos de instalação do aplicativo</span><span class="sxs-lookup"><span data-stu-id="bfd4f-222">Application install points</span></span></li><li><span data-ttu-id="bfd4f-223">definições de configuração do host</span><span class="sxs-lookup"><span data-stu-id="bfd4f-223">Host configuration settings</span></span></li><li><span data-ttu-id="bfd4f-224">outros detalhes internos do aplicativo</span><span class="sxs-lookup"><span data-stu-id="bfd4f-224">Other internal application details</span></span></li></ul><p><span data-ttu-id="bfd4f-225">Interceptar todos os erros em um aplicativo e fornecer mensagens de erro genéricas, bem como habilitar os erros personalizados no IIS, ajudará a evitar a divulgação das informações.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-225">Trapping all errors within an application and providing generic error messages, as well as enabling custom errors within IIS will help prevent information disclosure.</span></span> <span data-ttu-id="bfd4f-226">Banco de dados do SQL Server e .NET manipulação de exceções, entre outros arquiteturas de tratamento de erros são extremamente úteis e especialmente detalhado tooa usuário mal-intencionado que seu aplicativo de criação de perfil.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-226">SQL Server database and .NET Exception handling, among other error handling architectures, are especially verbose and extremely useful tooa malicious user profiling your application.</span></span> <span data-ttu-id="bfd4f-227">Faça não diretamente Olá exibir conteúdo de uma classe derivada da classe de exceção .NET hello e certifique-se de que você tenha a manipulação adequada de exceções para que uma exceção inesperada inadvertidamente não é gerado diretamente toohello usuário.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-227">Do not directly display hello contents of a class derived from hello .NET Exception class, and ensure that you have proper exception handling so that an unexpected exception isn't inadvertently raised directly toohello user.</span></span></p><ul><li><span data-ttu-id="bfd4f-228">Forneça o usuário toohello que abstraem longe detalhes específicos encontrados diretamente na mensagem de exceção/Erro de saudação de diretamente de mensagens de erro genérico</span><span class="sxs-lookup"><span data-stu-id="bfd4f-228">Provide generic error messages directly toohello user that abstract away specific details found directly in hello exception/error message</span></span></li><li><span data-ttu-id="bfd4f-229">Exibir conteúdo de saudação de uma exceção do .NET diretamente classe toohello usuário</span><span class="sxs-lookup"><span data-stu-id="bfd4f-229">Do not display hello contents of a .NET exception class directly toohello user</span></span></li><li><span data-ttu-id="bfd4f-230">Interceptação de todas as mensagens de erro e se apropriado informar o usuário Olá por meio de um cliente de aplicativo de toohello enviados de mensagem de erro genérico</span><span class="sxs-lookup"><span data-stu-id="bfd4f-230">Trap all error messages and if appropriate inform hello user via a generic error message sent toohello application client</span></span></li><li><span data-ttu-id="bfd4f-231">Não expõem conteúdo Olá da classe de exceção Olá diretamente usuário toohello, especialmente Olá retornar o valor de `.ToString()`, ou Olá valores de propriedades de mensagem ou o rastreamento de pilha hello.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-231">Do not expose hello contents of hello Exception class directly toohello user, especially hello return value from `.ToString()`, or hello values of hello Message or StackTrace properties.</span></span> <span data-ttu-id="bfd4f-232">Registrar essas informações com segurança e exibir um usuário mais simples de toohello de mensagem</span><span class="sxs-lookup"><span data-stu-id="bfd4f-232">Securely log this information and display a more innocuous message toohello user</span></span></li></ul>|

## <span data-ttu-id="bfd4f-233"><a id="default"></a>Implementar a página de tratamento de erros Padrão</span><span class="sxs-lookup"><span data-stu-id="bfd4f-233"><a id="default"></a>Implement Default error handling page</span></span>

| <span data-ttu-id="bfd4f-234">Title</span><span class="sxs-lookup"><span data-stu-id="bfd4f-234">Title</span></span>                   | <span data-ttu-id="bfd4f-235">Detalhes</span><span class="sxs-lookup"><span data-stu-id="bfd4f-235">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="bfd4f-236">**Componente**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-236">**Component**</span></span>               | <span data-ttu-id="bfd4f-237">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="bfd4f-237">Web Application</span></span> | 
| <span data-ttu-id="bfd4f-238">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-238">**SDL Phase**</span></span>               | <span data-ttu-id="bfd4f-239">Compilação</span><span class="sxs-lookup"><span data-stu-id="bfd4f-239">Build</span></span> |  
| <span data-ttu-id="bfd4f-240">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-240">**Applicable Technologies**</span></span> | <span data-ttu-id="bfd4f-241">Genérico</span><span class="sxs-lookup"><span data-stu-id="bfd4f-241">Generic</span></span> |
| <span data-ttu-id="bfd4f-242">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-242">**Attributes**</span></span>              | <span data-ttu-id="bfd4f-243">N/D</span><span class="sxs-lookup"><span data-stu-id="bfd4f-243">N/A</span></span>  |
| <span data-ttu-id="bfd4f-244">**Referências**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-244">**References**</span></span>              | <span data-ttu-id="bfd4f-245">[Caixa de Diálogo Editar Configurações das Páginas de Erro do ASP.NET](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="bfd4f-245">[Edit ASP.NET Error Pages Settings Dialog Box](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span></span> |
| <span data-ttu-id="bfd4f-246">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-246">**Steps**</span></span> | <p><span data-ttu-id="bfd4f-247">Quando um aplicativo ASP.NET falhar e fizer com que um Erro Interno do Servidor HTTP/1.x 500 ou uma configuração do recurso (por exemplo, Filtragem da Solicitação) impeça que uma página seja exibida, uma mensagem de erro será gerada.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-247">When an ASP.NET application fails and causes an HTTP/1.x 500 Internal Server Error, or a feature configuration (such as Request Filtering) prevents a page from being displayed, an error message will be generated.</span></span> <span data-ttu-id="bfd4f-248">Os administradores podem optar ou não o aplicativo hello deve exibir uma mensagem amigável toohello cliente, do cliente de toohello de mensagem de erro detalhada ou apenas toolocalhost de mensagem de erro detalhada.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-248">Administrators can choose whether or not hello application should display a friendly message toohello client, detailed error message toohello client, or detailed error message toolocalhost only.</span></span> <span data-ttu-id="bfd4f-249">Olá <customErrors> marca no Web. config de Olá tem três modos:</span><span class="sxs-lookup"><span data-stu-id="bfd4f-249">hello <customErrors> tag in hello web.config has three modes:</span></span></p><ul><li><span data-ttu-id="bfd4f-250">**Ativado:** especifica que os erros personalizados estão habilitados.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-250">**On:** Specifies that custom errors are enabled.</span></span> <span data-ttu-id="bfd4f-251">Se nenhum atributo defaultRedirect for especificado, os usuários verão um erro genérico.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-251">If no defaultRedirect attribute is specified, users see a generic error.</span></span> <span data-ttu-id="bfd4f-252">erros personalizados Olá são mostrados os clientes remotos toohello e host local toohello</span><span class="sxs-lookup"><span data-stu-id="bfd4f-252">hello custom errors are shown toohello remote clients and toohello local host</span></span></li><li><span data-ttu-id="bfd4f-253">**Desativado:** especifica que os erros personalizados estão desabilitados.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-253">**Off:** Specifies that custom errors are disabled.</span></span> <span data-ttu-id="bfd4f-254">Olá erros detalhados do ASP.NET são mostrados os clientes remotos toohello e host local toohello</span><span class="sxs-lookup"><span data-stu-id="bfd4f-254">hello detailed ASP.NET errors are shown toohello remote clients and toohello local host</span></span></li><li><span data-ttu-id="bfd4f-255">**RemoteOnly:** Especifica que os erros personalizados são mostrados apenas toohello clientes remotos e que os erros do ASP.NET são mostrados host local toohello.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-255">**RemoteOnly:** Specifies that custom errors are shown only toohello remote clients, and that ASP.NET errors are shown toohello local host.</span></span> <span data-ttu-id="bfd4f-256">Este é o valor padrão de saudação</span><span class="sxs-lookup"><span data-stu-id="bfd4f-256">This is hello default value</span></span></li></ul><p><span data-ttu-id="bfd4f-257">Olá abrir `web.config` de arquivos para o site da aplicativo hello e certifique-se de que marca Olá foi `<customErrors mode="RemoteOnly" />` ou `<customErrors mode="On" />` definido.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-257">Open hello `web.config` file for hello application/site and ensure that hello tag has either `<customErrors mode="RemoteOnly" />` or `<customErrors mode="On" />` defined.</span></span></p>|

## <span data-ttu-id="bfd4f-258"><a id="deployment"></a>Definir o método de implantação tooRetail no IIS</span><span class="sxs-lookup"><span data-stu-id="bfd4f-258"><a id="deployment"></a>Set Deployment Method tooRetail in IIS</span></span>

| <span data-ttu-id="bfd4f-259">Title</span><span class="sxs-lookup"><span data-stu-id="bfd4f-259">Title</span></span>                   | <span data-ttu-id="bfd4f-260">Detalhes</span><span class="sxs-lookup"><span data-stu-id="bfd4f-260">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="bfd4f-261">**Componente**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-261">**Component**</span></span>               | <span data-ttu-id="bfd4f-262">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="bfd4f-262">Web Application</span></span> | 
| <span data-ttu-id="bfd4f-263">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-263">**SDL Phase**</span></span>               | <span data-ttu-id="bfd4f-264">Implantação</span><span class="sxs-lookup"><span data-stu-id="bfd4f-264">Deployment</span></span> |  
| <span data-ttu-id="bfd4f-265">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-265">**Applicable Technologies**</span></span> | <span data-ttu-id="bfd4f-266">Genérico</span><span class="sxs-lookup"><span data-stu-id="bfd4f-266">Generic</span></span> |
| <span data-ttu-id="bfd4f-267">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-267">**Attributes**</span></span>              | <span data-ttu-id="bfd4f-268">N/D</span><span class="sxs-lookup"><span data-stu-id="bfd4f-268">N/A</span></span>  |
| <span data-ttu-id="bfd4f-269">**Referências**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-269">**References**</span></span>              | <span data-ttu-id="bfd4f-270">[implantação Element (Esquema de Configurações do ASP.NET)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span><span class="sxs-lookup"><span data-stu-id="bfd4f-270">[deployment Element (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span></span> |
| <span data-ttu-id="bfd4f-271">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-271">**Steps**</span></span> | <p><span data-ttu-id="bfd4f-272">Olá `<deployment retail>` switch é destinado ao uso por servidores IIS de produção.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-272">hello `<deployment retail>` switch is intended for use by production IIS servers.</span></span> <span data-ttu-id="bfd4f-273">Essa opção é usada toohelp aplicativos executados com o melhor desempenho possível de saudação e informações de segurança menos possíveis leakages desabilitando Olá a saída do rastreamento em uma página, desabilitando toodisplay de capacidade de saudação toogenerate capacidade do aplicativo para detalhes do erro mensagens tooend usuários e Olá desabilitar a opção de debug.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-273">This switch is used toohelp applications run with hello best possible performance and least possible security information leakages by disabling hello application's ability toogenerate trace output on a page, disabling hello ability toodisplay detailed error messages tooend users, and disabling hello debug switch.</span></span></p><p><span data-ttu-id="bfd4f-274">Muitas vezes, os argumentos e as opções que estão voltados para os desenvolvedores, como um rastreamento da solicitação e depuração com falha, são habilitados durante o desenvolvimento ativo.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-274">Often times, switches and options that are developer-focused, such as failed request tracing and debugging, are enabled during active development.</span></span> <span data-ttu-id="bfd4f-275">É recomendável que o método de implantação hello em qualquer servidor de produção seja definido tooretail.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-275">It is recommended that hello deployment method on any production server be set tooretail.</span></span> <span data-ttu-id="bfd4f-276">Abra o arquivo Machine. config de saudação e certifique-se de que `<deployment retail="true" />` permanece definido tootrue.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-276">open hello machine.config file and ensure that `<deployment retail="true" />` remains set tootrue.</span></span></p>|

## <span data-ttu-id="bfd4f-277"><a id="fail"></a>As exceções devem falhar com segurança</span><span class="sxs-lookup"><span data-stu-id="bfd4f-277"><a id="fail"></a>Exceptions should fail safely</span></span>

| <span data-ttu-id="bfd4f-278">Title</span><span class="sxs-lookup"><span data-stu-id="bfd4f-278">Title</span></span>                   | <span data-ttu-id="bfd4f-279">Detalhes</span><span class="sxs-lookup"><span data-stu-id="bfd4f-279">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="bfd4f-280">**Componente**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-280">**Component**</span></span>               | <span data-ttu-id="bfd4f-281">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="bfd4f-281">Web Application</span></span> | 
| <span data-ttu-id="bfd4f-282">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-282">**SDL Phase**</span></span>               | <span data-ttu-id="bfd4f-283">Compilação</span><span class="sxs-lookup"><span data-stu-id="bfd4f-283">Build</span></span> |  
| <span data-ttu-id="bfd4f-284">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-284">**Applicable Technologies**</span></span> | <span data-ttu-id="bfd4f-285">Genérico</span><span class="sxs-lookup"><span data-stu-id="bfd4f-285">Generic</span></span> |
| <span data-ttu-id="bfd4f-286">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-286">**Attributes**</span></span>              | <span data-ttu-id="bfd4f-287">N/D</span><span class="sxs-lookup"><span data-stu-id="bfd4f-287">N/A</span></span>  |
| <span data-ttu-id="bfd4f-288">**Referências**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-288">**References**</span></span>              | [<span data-ttu-id="bfd4f-289">Falhar com segurança</span><span class="sxs-lookup"><span data-stu-id="bfd4f-289">Fail securely</span></span>](https://www.owasp.org/index.php/Fail_securely) |
| <span data-ttu-id="bfd4f-290">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="bfd4f-290">**Steps**</span></span> | <span data-ttu-id="bfd4f-291">O aplicativo deve falhar com segurança.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-291">Application should fail safely.</span></span> <span data-ttu-id="bfd4f-292">Qualquer método que retorna um valor booliano, com base em qual determinada decisão é tomada, deve ter um bloco de exceção criado cuidadosamente.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-292">Any method that returns a Boolean value, based on which certain decision is made, should have exception block carefully created.</span></span> <span data-ttu-id="bfd4f-293">Há muitos erros lógicos devido toowhich deslizamento de problemas de segurança no, quando o bloco de exceção hello é escrito com negligência.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-293">There are lot of logical errors due toowhich security issues creep in, when hello exception block is written carelessly.</span></span>|

### <a name="example"></a><span data-ttu-id="bfd4f-294">Exemplo</span><span class="sxs-lookup"><span data-stu-id="bfd4f-294">Example</span></span>
```C#
        public static bool ValidateDomain(string pathToValidate, Uri currentUrl)
        {
            try
            {
                if (!string.IsNullOrWhiteSpace(pathToValidate))
                {
                    var domain = RetrieveDomain(currentUrl);
                    var replyPath = new Uri(pathToValidate);
                    var replyDomain = RetrieveDomain(replyPath);

                    if (string.Compare(domain, replyDomain, StringComparison.OrdinalIgnoreCase) != 0)
                    {
                        //// Adding additional check tooenable CMS urls if they are not hosted on same domain.
                        if (!string.IsNullOrWhiteSpace(Utilities.CmsBase))
                        {
                            var cmsDomain = RetrieveDomain(new Uri(Utilities.Base.Trim()));
                            if (string.Compare(cmDomain, replyDomain, StringComparison.OrdinalIgnoreCase) != 0)
                            {
                                return false;
                            }
                            else
                            {
                                return true;
                            }
                        }

                        return false;
                    }
                }

                return true;
            }
            catch (UriFormatException ex)
            {
                LogHelper.LogException("Utilities:ValidateDomain", ex);
                return true;
            }
        }
```
<span data-ttu-id="bfd4f-295">Olá acima método sempre retornará True, se ocorrer uma exceção.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-295">hello above method will always return True, if some exception happens.</span></span> <span data-ttu-id="bfd4f-296">Se o usuário final de saudação fornece uma URL malformada, que Olá aspectos do navegador, mas Olá `Uri()` construtor não, isso gerará uma exceção e vítima hello será tomada URL de toohello válido, mas malformado.</span><span class="sxs-lookup"><span data-stu-id="bfd4f-296">If hello end user provides a malformed URL, that hello browser respects, but hello `Uri()` constructor doesn't, this will throw an exception, and hello victim will be taken toohello valid but malformed URL.</span></span> 
