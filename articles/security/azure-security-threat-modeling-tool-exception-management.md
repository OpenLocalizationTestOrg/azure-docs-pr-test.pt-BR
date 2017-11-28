---
title: "Gerenciamento de Exceções - Ferramenta de Modelagem de Ameaças da Microsoft - Azure | Microsoft Docs"
description: "atenuações de ameaças expostas na Ferramenta de Modelagem de Ameaças"
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
ms.openlocfilehash: bbf357b902474a1812eb7a5a2c914d0c8b91934b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="security-frame-exception-management--mitigations"></a><span data-ttu-id="b3e7f-103">Quadro de Segurança: Gerenciamento de Exceções | Atenuações</span><span class="sxs-lookup"><span data-stu-id="b3e7f-103">Security Frame: Exception Management | Mitigations</span></span> 
| <span data-ttu-id="b3e7f-104">Produto/Serviço</span><span class="sxs-lookup"><span data-stu-id="b3e7f-104">Product/Service</span></span> | <span data-ttu-id="b3e7f-105">Artigo</span><span class="sxs-lookup"><span data-stu-id="b3e7f-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="b3e7f-106">**WCF**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-106">**WCF**</span></span> | <ul><li>[<span data-ttu-id="b3e7f-107">WCF - não inclui o nó serviceDebug no arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="b3e7f-107">WCF- Do not include serviceDebug node in configuration file</span></span>](#servicedebug)</li><li>[<span data-ttu-id="b3e7f-108">WCF - não inclui o nó serviceMetadata no arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="b3e7f-108">WCF- Do not include serviceMetadata node in configuration file</span></span>](#servicemetadata)</li></ul> |
| <span data-ttu-id="b3e7f-109">**API da Web**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-109">**Web API**</span></span> | <ul><li>[<span data-ttu-id="b3e7f-110">Verificar se o tratamento de exceções adequado é feito na API Web ASP.NET </span><span class="sxs-lookup"><span data-stu-id="b3e7f-110">Ensure that proper exception handling is done in ASP.NET Web API </span></span>](#exception)</li></ul> |
| <span data-ttu-id="b3e7f-111">**Aplicativo Web**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-111">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="b3e7f-112">Não expor os detalhes da segurança nas mensagens de erro </span><span class="sxs-lookup"><span data-stu-id="b3e7f-112">Do not expose security details in error messages </span></span>](#messages)</li><li>[<span data-ttu-id="b3e7f-113">Implementar a página tratamento de erros Padrão </span><span class="sxs-lookup"><span data-stu-id="b3e7f-113">Implement Default error handling page </span></span>](#default)</li><li>[<span data-ttu-id="b3e7f-114">Definir o Método de Implantação para o Varejo no IIS</span><span class="sxs-lookup"><span data-stu-id="b3e7f-114">Set Deployment Method to Retail in IIS</span></span>](#deployment)</li><li>[<span data-ttu-id="b3e7f-115">As exceções devem falhar com segurança</span><span class="sxs-lookup"><span data-stu-id="b3e7f-115">Exceptions should fail safely</span></span>](#fail)</li></ul> |

## <span data-ttu-id="b3e7f-116"><a id="servicedebug"></a>WCF - não inclui o nó serviceDebug no arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="b3e7f-116"><a id="servicedebug"></a>WCF- Do not include serviceDebug node in configuration file</span></span>

| <span data-ttu-id="b3e7f-117">Title</span><span class="sxs-lookup"><span data-stu-id="b3e7f-117">Title</span></span>                   | <span data-ttu-id="b3e7f-118">Detalhes</span><span class="sxs-lookup"><span data-stu-id="b3e7f-118">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b3e7f-119">**Componente**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-119">**Component**</span></span>               | <span data-ttu-id="b3e7f-120">WCF</span><span class="sxs-lookup"><span data-stu-id="b3e7f-120">WCF</span></span> | 
| <span data-ttu-id="b3e7f-121">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-121">**SDL Phase**</span></span>               | <span data-ttu-id="b3e7f-122">Compilação</span><span class="sxs-lookup"><span data-stu-id="b3e7f-122">Build</span></span> |  
| <span data-ttu-id="b3e7f-123">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-123">**Applicable Technologies**</span></span> | <span data-ttu-id="b3e7f-124">Genérico, NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="b3e7f-124">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="b3e7f-125">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-125">**Attributes**</span></span>              | <span data-ttu-id="b3e7f-126">N/D</span><span class="sxs-lookup"><span data-stu-id="b3e7f-126">N/A</span></span>  |
| <span data-ttu-id="b3e7f-127">**Referências**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-127">**References**</span></span>              | <span data-ttu-id="b3e7f-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="b3e7f-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="b3e7f-129">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-129">**Steps**</span></span> | <span data-ttu-id="b3e7f-130">Os serviços do Windows Communication Framework (WCF) podem ser configurados para expor as informações de depuração.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-130">Windows Communication Framework (WCF) services can be configured to expose debugging information.</span></span> <span data-ttu-id="b3e7f-131">As informações de depuração não devem ser usadas nos ambientes de produção.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-131">Debug information should not be used in production environments.</span></span> <span data-ttu-id="b3e7f-132">A marcação `<serviceDebug>` define se o recurso das informações de depuração está habilitado para um serviço WCF.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-132">The `<serviceDebug>` tag defines whether the debug information feature is enabled for a WCF service.</span></span> <span data-ttu-id="b3e7f-133">Se o atributo includeExceptionDetailInFaults for definido para true, as informações de exceção do aplicativo serão retornadas aos clientes.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-133">If the attribute includeExceptionDetailInFaults is set to true, exception information from the application will be returned to clients.</span></span> <span data-ttu-id="b3e7f-134">Os invasores podem aproveitar as informações adicionais que eles obtêm na saída da depuração para montar ataques direcionados na estrutura, banco de dados ou outros recursos usados pelo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-134">Attackers can leverage the additional information they gain from debugging output to mount attacks targeted on the framework, database, or other resources used by the application.</span></span> |

### <a name="example"></a><span data-ttu-id="b3e7f-135">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b3e7f-135">Example</span></span>
<span data-ttu-id="b3e7f-136">O arquivo de configuração a seguir inclui a marcação `<serviceDebug>`:</span><span class="sxs-lookup"><span data-stu-id="b3e7f-136">The following configuration file includes the `<serviceDebug>` tag:</span></span> 
```
<configuration> 
<system.serviceModel> 
<behaviors> 
<serviceBehaviors> 
<behavior name=""MyServiceBehavior""> 
<serviceDebug includeExceptionDetailInFaults=""True"" httpHelpPageEnabled=""True""/> 
... 
```
<span data-ttu-id="b3e7f-137">Desabilite as informações de depuração no serviço.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-137">Disable debugging information in the service.</span></span> <span data-ttu-id="b3e7f-138">Isso pode ser feito removendo a marcação `<serviceDebug>` do arquivo de configuração de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-138">This can be accomplished by removing the `<serviceDebug>` tag from your application's configuration file.</span></span> 

## <span data-ttu-id="b3e7f-139"><a id="servicemetadata"></a>WCF - não inclui o nó serviceMetadata no arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="b3e7f-139"><a id="servicemetadata"></a>WCF- Do not include serviceMetadata node in configuration file</span></span>

| <span data-ttu-id="b3e7f-140">Title</span><span class="sxs-lookup"><span data-stu-id="b3e7f-140">Title</span></span>                   | <span data-ttu-id="b3e7f-141">Detalhes</span><span class="sxs-lookup"><span data-stu-id="b3e7f-141">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b3e7f-142">**Componente**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-142">**Component**</span></span>               | <span data-ttu-id="b3e7f-143">WCF</span><span class="sxs-lookup"><span data-stu-id="b3e7f-143">WCF</span></span> | 
| <span data-ttu-id="b3e7f-144">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-144">**SDL Phase**</span></span>               | <span data-ttu-id="b3e7f-145">Compilação</span><span class="sxs-lookup"><span data-stu-id="b3e7f-145">Build</span></span> |  
| <span data-ttu-id="b3e7f-146">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-146">**Applicable Technologies**</span></span> | <span data-ttu-id="b3e7f-147">Genérico</span><span class="sxs-lookup"><span data-stu-id="b3e7f-147">Generic</span></span> |
| <span data-ttu-id="b3e7f-148">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-148">**Attributes**</span></span>              | <span data-ttu-id="b3e7f-149">Genérico, NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="b3e7f-149">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="b3e7f-150">**Referências**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-150">**References**</span></span>              | <span data-ttu-id="b3e7f-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="b3e7f-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="b3e7f-152">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-152">**Steps**</span></span> | <span data-ttu-id="b3e7f-153">Expor publicamente as informações sobre um serviço pode dar aos invasores ideias valiosas sobre como eles podem explorar o serviço.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-153">Publicly exposing information about a service can provide attackers with valuable insight into how they might exploit the service.</span></span> <span data-ttu-id="b3e7f-154">A marcação `<serviceMetadata>` habilita o recurso de publicação de metadados.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-154">The `<serviceMetadata>` tag enables the metadata publishing feature.</span></span> <span data-ttu-id="b3e7f-155">Os metadados do serviço podem conter informações confidenciais e não devem ser acessíveis publicamente.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-155">Service metadata could contain sensitive information that should not be publicly accessible.</span></span> <span data-ttu-id="b3e7f-156">No mínimo, apenas permita que usuários confiáveis acessem os metadados e verifique se informações desnecessárias não são expostas.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-156">At a minimum, only allow trusted users to access the metadata and ensure that unnecessary information is not exposed.</span></span> <span data-ttu-id="b3e7f-157">Melhor ainda, desabilite totalmente a capacidade de publicar metadados.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-157">Better yet, entirely disable the ability to publish metadata.</span></span> <span data-ttu-id="b3e7f-158">Uma configuração segura do WCF não conterá a marcação `<serviceMetadata>`.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-158">A safe WCF configuration will not contain the `<serviceMetadata>` tag.</span></span> |

## <span data-ttu-id="b3e7f-159"><a id="exception"></a>Verificar se o tratamento de exceções adequado é feito na API Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b3e7f-159"><a id="exception"></a>Ensure that proper exception handling is done in ASP.NET Web API</span></span>

| <span data-ttu-id="b3e7f-160">Title</span><span class="sxs-lookup"><span data-stu-id="b3e7f-160">Title</span></span>                   | <span data-ttu-id="b3e7f-161">Detalhes</span><span class="sxs-lookup"><span data-stu-id="b3e7f-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b3e7f-162">**Componente**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-162">**Component**</span></span>               | <span data-ttu-id="b3e7f-163">API Web</span><span class="sxs-lookup"><span data-stu-id="b3e7f-163">Web API</span></span> | 
| <span data-ttu-id="b3e7f-164">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-164">**SDL Phase**</span></span>               | <span data-ttu-id="b3e7f-165">Compilação</span><span class="sxs-lookup"><span data-stu-id="b3e7f-165">Build</span></span> |  
| <span data-ttu-id="b3e7f-166">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-166">**Applicable Technologies**</span></span> | <span data-ttu-id="b3e7f-167">MVC 5, MVC 6</span><span class="sxs-lookup"><span data-stu-id="b3e7f-167">MVC 5, MVC 6</span></span> |
| <span data-ttu-id="b3e7f-168">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-168">**Attributes**</span></span>              | <span data-ttu-id="b3e7f-169">N/D</span><span class="sxs-lookup"><span data-stu-id="b3e7f-169">N/A</span></span>  |
| <span data-ttu-id="b3e7f-170">**Referências**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-170">**References**</span></span>              | <span data-ttu-id="b3e7f-171">[Tratamento de Exceções na API Web ASP.NET](http://www.asp.net/web-api/overview/error-handling/exception-handling), [Validação do Modelo na API Web ASP.NET](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span><span class="sxs-lookup"><span data-stu-id="b3e7f-171">[Exception Handling in ASP.NET Web API](http://www.asp.net/web-api/overview/error-handling/exception-handling), [Model Validation in ASP.NET Web API](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span></span> |
| <span data-ttu-id="b3e7f-172">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-172">**Steps**</span></span> | <span data-ttu-id="b3e7f-173">Por padrão, a maioria das exceções não identificadas na API Web ASP.NET é convertida em uma resposta HTTP com um código de status`500, Internal Server Error`</span><span class="sxs-lookup"><span data-stu-id="b3e7f-173">By default, most uncaught exceptions in ASP.NET Web API are translated into an HTTP response with status code `500, Internal Server Error`</span></span>|

### <a name="example"></a><span data-ttu-id="b3e7f-174">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b3e7f-174">Example</span></span>
<span data-ttu-id="b3e7f-175">Para controlar o código de status retornado pela API, `HttpResponseException` pode ser usado como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="b3e7f-175">To control the status code returned by the API, `HttpResponseException` can be used as shown below:</span></span> 
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

### <a name="example"></a><span data-ttu-id="b3e7f-176">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b3e7f-176">Example</span></span>
<span data-ttu-id="b3e7f-177">Para ter mais controle sobre a resposta da exceção, a classe `HttpResponseMessage` pode ser usada como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="b3e7f-177">For further control on the exception response, the `HttpResponseMessage` class can be used as shown below:</span></span> 
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
<span data-ttu-id="b3e7f-178">Para capturar as exceções sem tratamento que não são do tipo `HttpResponseException`, podem ser usados Filtros de Exceção.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-178">To catch unhandled exceptions that are not of the type `HttpResponseException`, Exception Filters can be used.</span></span> <span data-ttu-id="b3e7f-179">Os Filtros de Exceção implementam a interface `System.Web.Http.Filters.IExceptionFilter`.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-179">Exception filters implement the `System.Web.Http.Filters.IExceptionFilter` interface.</span></span> <span data-ttu-id="b3e7f-180">A maneira mais simples de escrever um filtro de exceção é derivar da classe `System.Web.Http.Filters.ExceptionFilterAttribute` e substituir o método OnException.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-180">The simplest way to write an exception filter is to derive from the `System.Web.Http.Filters.ExceptionFilterAttribute` class and override the OnException method.</span></span> 

### <a name="example"></a><span data-ttu-id="b3e7f-181">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b3e7f-181">Example</span></span>
<span data-ttu-id="b3e7f-182">Aqui está um filtro que converte as exceções `NotImplementedException` no código de status HTTP `501, Not Implemented`:</span><span class="sxs-lookup"><span data-stu-id="b3e7f-182">Here is a filter that converts `NotImplementedException` exceptions into HTTP status code `501, Not Implemented`:</span></span> 
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

<span data-ttu-id="b3e7f-183">Há várias maneiras de registrar um filtro de exceção da API Web:</span><span class="sxs-lookup"><span data-stu-id="b3e7f-183">There are several ways to register a Web API exception filter:</span></span>
- <span data-ttu-id="b3e7f-184">por ação</span><span class="sxs-lookup"><span data-stu-id="b3e7f-184">By action</span></span>
- <span data-ttu-id="b3e7f-185">pelo controlador</span><span class="sxs-lookup"><span data-stu-id="b3e7f-185">By controller</span></span>
- <span data-ttu-id="b3e7f-186">globalmente</span><span class="sxs-lookup"><span data-stu-id="b3e7f-186">Globally</span></span>

### <a name="example"></a><span data-ttu-id="b3e7f-187">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b3e7f-187">Example</span></span>
<span data-ttu-id="b3e7f-188">Para aplicar o filtro em uma ação específica, adicione o filtro como um atributo à ação:</span><span class="sxs-lookup"><span data-stu-id="b3e7f-188">To apply the filter to a specific action, add the filter as an attribute to the action:</span></span> 
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
### <a name="example"></a><span data-ttu-id="b3e7f-189">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b3e7f-189">Example</span></span>
<span data-ttu-id="b3e7f-190">Para aplicar o filtro em todas as ações em um `controller`, adicione o filtro como um atributo à classe `controller`:</span><span class="sxs-lookup"><span data-stu-id="b3e7f-190">To apply the filter to all of the actions on a `controller`, add the filter as an attribute to the `controller` class:</span></span> 

```C#
[NotImplExceptionFilter]
public class ProductsController : ApiController
{
    // ...
}
```

### <a name="example"></a><span data-ttu-id="b3e7f-191">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b3e7f-191">Example</span></span>
<span data-ttu-id="b3e7f-192">Para aplicar o filtro globalmente em todos os controladores da API Web, adicione uma instância do filtro à coleção `GlobalConfiguration.Configuration.Filters`.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-192">To apply the filter globally to all Web API controllers, add an instance of the filter to the `GlobalConfiguration.Configuration.Filters` collection.</span></span> <span data-ttu-id="b3e7f-193">Os filtros de exceção nesta coleção aplicam-se a qualquer ação do controlador da API Web.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-193">Exception filters in this collection apply to any Web API controller action.</span></span> 
```C#
GlobalConfiguration.Configuration.Filters.Add(
    new ProductStore.NotImplExceptionFilterAttribute());
```

### <a name="example"></a><span data-ttu-id="b3e7f-194">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b3e7f-194">Example</span></span>
<span data-ttu-id="b3e7f-195">Para a validação do modelo, o estado do modelo pode ser passado para o método CreateErrorResponse como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="b3e7f-195">For model validation, the model state can be passed to CreateErrorResponse method as shown below:</span></span> 
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

<span data-ttu-id="b3e7f-196">Verificar os links na seção de referências para obter detalhes adicionais sobre o tratamento de exceção e a validação do modelo na API Web ASP.Net</span><span class="sxs-lookup"><span data-stu-id="b3e7f-196">Check the links in the references section for additional details about exceptional handling and model validation in ASP.Net Web API</span></span> 

## <span data-ttu-id="b3e7f-197"><a id="messages"></a>Não expor os detalhes da segurança nas mensagens de erro</span><span class="sxs-lookup"><span data-stu-id="b3e7f-197"><a id="messages"></a>Do not expose security details in error messages</span></span>

| <span data-ttu-id="b3e7f-198">Title</span><span class="sxs-lookup"><span data-stu-id="b3e7f-198">Title</span></span>                   | <span data-ttu-id="b3e7f-199">Detalhes</span><span class="sxs-lookup"><span data-stu-id="b3e7f-199">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b3e7f-200">**Componente**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-200">**Component**</span></span>               | <span data-ttu-id="b3e7f-201">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="b3e7f-201">Web Application</span></span> | 
| <span data-ttu-id="b3e7f-202">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-202">**SDL Phase**</span></span>               | <span data-ttu-id="b3e7f-203">Compilação</span><span class="sxs-lookup"><span data-stu-id="b3e7f-203">Build</span></span> |  
| <span data-ttu-id="b3e7f-204">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-204">**Applicable Technologies**</span></span> | <span data-ttu-id="b3e7f-205">Genérico</span><span class="sxs-lookup"><span data-stu-id="b3e7f-205">Generic</span></span> |
| <span data-ttu-id="b3e7f-206">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-206">**Attributes**</span></span>              | <span data-ttu-id="b3e7f-207">N/D</span><span class="sxs-lookup"><span data-stu-id="b3e7f-207">N/A</span></span>  |
| <span data-ttu-id="b3e7f-208">**Referências**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-208">**References**</span></span>              | <span data-ttu-id="b3e7f-209">N/D</span><span class="sxs-lookup"><span data-stu-id="b3e7f-209">N/A</span></span>  |
| <span data-ttu-id="b3e7f-210">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-210">**Steps**</span></span> | <p><span data-ttu-id="b3e7f-211">As mensagens de erro genéricas são fornecidas diretamente para o usuário sem incluir os dados confidenciais do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-211">Generic error messages are provided directly to the user without including sensitive application data.</span></span> <span data-ttu-id="b3e7f-212">Os exemplos de dados confidenciais incluem:</span><span class="sxs-lookup"><span data-stu-id="b3e7f-212">Examples of sensitive data include:</span></span></p><ul><li><span data-ttu-id="b3e7f-213">nomes do servidor</span><span class="sxs-lookup"><span data-stu-id="b3e7f-213">Server names</span></span></li><li><span data-ttu-id="b3e7f-214">Cadeias de conexão</span><span class="sxs-lookup"><span data-stu-id="b3e7f-214">Connection strings</span></span></li><li><span data-ttu-id="b3e7f-215">nomes de usuário</span><span class="sxs-lookup"><span data-stu-id="b3e7f-215">Usernames</span></span></li><li><span data-ttu-id="b3e7f-216">Senhas</span><span class="sxs-lookup"><span data-stu-id="b3e7f-216">Passwords</span></span></li><li><span data-ttu-id="b3e7f-217">procedimentos SQL</span><span class="sxs-lookup"><span data-stu-id="b3e7f-217">SQL procedures</span></span></li><li><span data-ttu-id="b3e7f-218">detalhes das falhas SQL dinâmicas</span><span class="sxs-lookup"><span data-stu-id="b3e7f-218">Details of dynamic SQL failures</span></span></li><li><span data-ttu-id="b3e7f-219">rastreamento de pilha e linhas de código</span><span class="sxs-lookup"><span data-stu-id="b3e7f-219">Stack trace and lines of code</span></span></li><li><span data-ttu-id="b3e7f-220">variáveis armazenadas na memória</span><span class="sxs-lookup"><span data-stu-id="b3e7f-220">Variables stored in memory</span></span></li><li><span data-ttu-id="b3e7f-221">locais da pasta e da unidade</span><span class="sxs-lookup"><span data-stu-id="b3e7f-221">Drive and folder locations</span></span></li><li><span data-ttu-id="b3e7f-222">pontos de instalação do aplicativo</span><span class="sxs-lookup"><span data-stu-id="b3e7f-222">Application install points</span></span></li><li><span data-ttu-id="b3e7f-223">definições de configuração do host</span><span class="sxs-lookup"><span data-stu-id="b3e7f-223">Host configuration settings</span></span></li><li><span data-ttu-id="b3e7f-224">outros detalhes internos do aplicativo</span><span class="sxs-lookup"><span data-stu-id="b3e7f-224">Other internal application details</span></span></li></ul><p><span data-ttu-id="b3e7f-225">Interceptar todos os erros em um aplicativo e fornecer mensagens de erro genéricas, bem como habilitar os erros personalizados no IIS, ajudará a evitar a divulgação das informações.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-225">Trapping all errors within an application and providing generic error messages, as well as enabling custom errors within IIS will help prevent information disclosure.</span></span> <span data-ttu-id="b3e7f-226">O banco de dados do SQL Server e o tratamento Exception do .NET, entre outras arquiteturas de tratamento de erros, são especialmente detalhados e extremamente úteis para um usuário mal-intencionado que cria o perfil de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-226">SQL Server database and .NET Exception handling, among other error handling architectures, are especially verbose and extremely useful to a malicious user profiling your application.</span></span> <span data-ttu-id="b3e7f-227">Não exiba diretamente o conteúdo de uma classe derivada da classe Exception do .NET e verifique se você tem o tratamento adequado das exceções para que uma exceção inesperada não seja gerada sem querer diretamente para o usuário.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-227">Do not directly display the contents of a class derived from the .NET Exception class, and ensure that you have proper exception handling so that an unexpected exception isn't inadvertently raised directly to the user.</span></span></p><ul><li><span data-ttu-id="b3e7f-228">Fornecer mensagens de erro genéricas diretamente para o usuário que abstrai os detalhes específicos encontrados diretamente na mensagem de erro/exceção</span><span class="sxs-lookup"><span data-stu-id="b3e7f-228">Provide generic error messages directly to the user that abstract away specific details found directly in the exception/error message</span></span></li><li><span data-ttu-id="b3e7f-229">Não exibir o conteúdo de uma classe exception do .NET diretamente para o usuário</span><span class="sxs-lookup"><span data-stu-id="b3e7f-229">Do not display the contents of a .NET exception class directly to the user</span></span></li><li><span data-ttu-id="b3e7f-230">Interceptar todas as mensagens de erro e se apropriado, informar ao usuário por meio de uma mensagem de erro genérica enviada ao cliente do aplicativo</span><span class="sxs-lookup"><span data-stu-id="b3e7f-230">Trap all error messages and if appropriate inform the user via a generic error message sent to the application client</span></span></li><li><span data-ttu-id="b3e7f-231">Não exponha o conteúdo da classe Exception diretamente para o usuário, especialmente o valor de retorno de `.ToString()` ou os valores das propriedades Message ou StackTrace.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-231">Do not expose the contents of the Exception class directly to the user, especially the return value from `.ToString()`, or the values of the Message or StackTrace properties.</span></span> <span data-ttu-id="b3e7f-232">Registrar essas informações com segurança e exibir uma mensagem mais inofensiva para o usuário</span><span class="sxs-lookup"><span data-stu-id="b3e7f-232">Securely log this information and display a more innocuous message to the user</span></span></li></ul>|

## <span data-ttu-id="b3e7f-233"><a id="default"></a>Implementar a página de tratamento de erros Padrão</span><span class="sxs-lookup"><span data-stu-id="b3e7f-233"><a id="default"></a>Implement Default error handling page</span></span>

| <span data-ttu-id="b3e7f-234">Title</span><span class="sxs-lookup"><span data-stu-id="b3e7f-234">Title</span></span>                   | <span data-ttu-id="b3e7f-235">Detalhes</span><span class="sxs-lookup"><span data-stu-id="b3e7f-235">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b3e7f-236">**Componente**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-236">**Component**</span></span>               | <span data-ttu-id="b3e7f-237">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="b3e7f-237">Web Application</span></span> | 
| <span data-ttu-id="b3e7f-238">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-238">**SDL Phase**</span></span>               | <span data-ttu-id="b3e7f-239">Compilação</span><span class="sxs-lookup"><span data-stu-id="b3e7f-239">Build</span></span> |  
| <span data-ttu-id="b3e7f-240">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-240">**Applicable Technologies**</span></span> | <span data-ttu-id="b3e7f-241">Genérico</span><span class="sxs-lookup"><span data-stu-id="b3e7f-241">Generic</span></span> |
| <span data-ttu-id="b3e7f-242">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-242">**Attributes**</span></span>              | <span data-ttu-id="b3e7f-243">N/D</span><span class="sxs-lookup"><span data-stu-id="b3e7f-243">N/A</span></span>  |
| <span data-ttu-id="b3e7f-244">**Referências**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-244">**References**</span></span>              | <span data-ttu-id="b3e7f-245">[Caixa de Diálogo Editar Configurações das Páginas de Erro do ASP.NET](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="b3e7f-245">[Edit ASP.NET Error Pages Settings Dialog Box](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span></span> |
| <span data-ttu-id="b3e7f-246">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-246">**Steps**</span></span> | <p><span data-ttu-id="b3e7f-247">Quando um aplicativo ASP.NET falhar e fizer com que um Erro Interno do Servidor HTTP/1.x 500 ou uma configuração do recurso (por exemplo, Filtragem da Solicitação) impeça que uma página seja exibida, uma mensagem de erro será gerada.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-247">When an ASP.NET application fails and causes an HTTP/1.x 500 Internal Server Error, or a feature configuration (such as Request Filtering) prevents a page from being displayed, an error message will be generated.</span></span> <span data-ttu-id="b3e7f-248">Os administradores podem escolher se o aplicativo deve exibir ou não uma mensagem amigável para o cliente, mensagem de erro detalhada para o cliente ou mensagem de erro detalhada para o localhost apenas.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-248">Administrators can choose whether or not the application should display a friendly message to the client, detailed error message to the client, or detailed error message to localhost only.</span></span> <span data-ttu-id="b3e7f-249">A marcação <customErrors> no web.config tem três modos:</span><span class="sxs-lookup"><span data-stu-id="b3e7f-249">The <customErrors> tag in the web.config has three modes:</span></span></p><ul><li><span data-ttu-id="b3e7f-250">**Ativado:** especifica que os erros personalizados estão habilitados.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-250">**On:** Specifies that custom errors are enabled.</span></span> <span data-ttu-id="b3e7f-251">Se nenhum atributo defaultRedirect for especificado, os usuários verão um erro genérico.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-251">If no defaultRedirect attribute is specified, users see a generic error.</span></span> <span data-ttu-id="b3e7f-252">Os erros personalizados são mostrados para os clientes remotos e para o host local</span><span class="sxs-lookup"><span data-stu-id="b3e7f-252">The custom errors are shown to the remote clients and to the local host</span></span></li><li><span data-ttu-id="b3e7f-253">**Desativado:** especifica que os erros personalizados estão desabilitados.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-253">**Off:** Specifies that custom errors are disabled.</span></span> <span data-ttu-id="b3e7f-254">Os erros detalhados do ASP.NET são mostrados para os clientes remotos e o host local</span><span class="sxs-lookup"><span data-stu-id="b3e7f-254">The detailed ASP.NET errors are shown to the remote clients and to the local host</span></span></li><li><span data-ttu-id="b3e7f-255">**RemoteOnly:** especifica que os erros personalizados são mostrados apenas para os clientes remotos e que os erros do ASP.NET são mostrados para o host local.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-255">**RemoteOnly:** Specifies that custom errors are shown only to the remote clients, and that ASP.NET errors are shown to the local host.</span></span> <span data-ttu-id="b3e7f-256">Este é o valor padrão</span><span class="sxs-lookup"><span data-stu-id="b3e7f-256">This is the default value</span></span></li></ul><p><span data-ttu-id="b3e7f-257">Abra o arquivo `web.config` do aplicativo/site e verifique se a marcação foi `<customErrors mode="RemoteOnly" />` ou `<customErrors mode="On" />` definido.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-257">Open the `web.config` file for the application/site and ensure that the tag has either `<customErrors mode="RemoteOnly" />` or `<customErrors mode="On" />` defined.</span></span></p>|

## <span data-ttu-id="b3e7f-258"><a id="deployment"></a>Definir o Método de Implantação para o Varejo no IIS</span><span class="sxs-lookup"><span data-stu-id="b3e7f-258"><a id="deployment"></a>Set Deployment Method to Retail in IIS</span></span>

| <span data-ttu-id="b3e7f-259">Title</span><span class="sxs-lookup"><span data-stu-id="b3e7f-259">Title</span></span>                   | <span data-ttu-id="b3e7f-260">Detalhes</span><span class="sxs-lookup"><span data-stu-id="b3e7f-260">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b3e7f-261">**Componente**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-261">**Component**</span></span>               | <span data-ttu-id="b3e7f-262">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="b3e7f-262">Web Application</span></span> | 
| <span data-ttu-id="b3e7f-263">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-263">**SDL Phase**</span></span>               | <span data-ttu-id="b3e7f-264">Implantação</span><span class="sxs-lookup"><span data-stu-id="b3e7f-264">Deployment</span></span> |  
| <span data-ttu-id="b3e7f-265">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-265">**Applicable Technologies**</span></span> | <span data-ttu-id="b3e7f-266">Genérico</span><span class="sxs-lookup"><span data-stu-id="b3e7f-266">Generic</span></span> |
| <span data-ttu-id="b3e7f-267">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-267">**Attributes**</span></span>              | <span data-ttu-id="b3e7f-268">N/D</span><span class="sxs-lookup"><span data-stu-id="b3e7f-268">N/A</span></span>  |
| <span data-ttu-id="b3e7f-269">**Referências**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-269">**References**</span></span>              | <span data-ttu-id="b3e7f-270">[implantação Element (Esquema de Configurações do ASP.NET)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span><span class="sxs-lookup"><span data-stu-id="b3e7f-270">[deployment Element (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span></span> |
| <span data-ttu-id="b3e7f-271">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-271">**Steps**</span></span> | <p><span data-ttu-id="b3e7f-272">O argumento `<deployment retail>` é para ser usado pelos servidores IIS de produção.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-272">The `<deployment retail>` switch is intended for use by production IIS servers.</span></span> <span data-ttu-id="b3e7f-273">Esse argumento é usado para ajudar os aplicativos a serem executados com o melhor desempenho possível e o mínimo de vazamento de informações de segurança desabilitando a capacidade dele de gerar a saída de rastreamento em uma página, desabilitando a capacidade de exibir mensagens de erro detalhadas para os usuários finais e desativando o argumento debug.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-273">This switch is used to help applications run with the best possible performance and least possible security information leakages by disabling the application's ability to generate trace output on a page, disabling the ability to display detailed error messages to end users, and disabling the debug switch.</span></span></p><p><span data-ttu-id="b3e7f-274">Muitas vezes, os argumentos e as opções que estão voltados para os desenvolvedores, como um rastreamento da solicitação e depuração com falha, são habilitados durante o desenvolvimento ativo.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-274">Often times, switches and options that are developer-focused, such as failed request tracing and debugging, are enabled during active development.</span></span> <span data-ttu-id="b3e7f-275">É recomendável que o método de implantação, em qualquer servidor de produção, seja definido para varejo.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-275">It is recommended that the deployment method on any production server be set to retail.</span></span> <span data-ttu-id="b3e7f-276">abra o arquivo machine.config e verifique se `<deployment retail="true" />` permanece definido para true.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-276">open the machine.config file and ensure that `<deployment retail="true" />` remains set to true.</span></span></p>|

## <span data-ttu-id="b3e7f-277"><a id="fail"></a>As exceções devem falhar com segurança</span><span class="sxs-lookup"><span data-stu-id="b3e7f-277"><a id="fail"></a>Exceptions should fail safely</span></span>

| <span data-ttu-id="b3e7f-278">Title</span><span class="sxs-lookup"><span data-stu-id="b3e7f-278">Title</span></span>                   | <span data-ttu-id="b3e7f-279">Detalhes</span><span class="sxs-lookup"><span data-stu-id="b3e7f-279">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b3e7f-280">**Componente**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-280">**Component**</span></span>               | <span data-ttu-id="b3e7f-281">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="b3e7f-281">Web Application</span></span> | 
| <span data-ttu-id="b3e7f-282">**Fase do SDL**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-282">**SDL Phase**</span></span>               | <span data-ttu-id="b3e7f-283">Compilação</span><span class="sxs-lookup"><span data-stu-id="b3e7f-283">Build</span></span> |  
| <span data-ttu-id="b3e7f-284">**Tecnologias aplicáveis**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-284">**Applicable Technologies**</span></span> | <span data-ttu-id="b3e7f-285">Genérico</span><span class="sxs-lookup"><span data-stu-id="b3e7f-285">Generic</span></span> |
| <span data-ttu-id="b3e7f-286">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-286">**Attributes**</span></span>              | <span data-ttu-id="b3e7f-287">N/D</span><span class="sxs-lookup"><span data-stu-id="b3e7f-287">N/A</span></span>  |
| <span data-ttu-id="b3e7f-288">**Referências**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-288">**References**</span></span>              | [<span data-ttu-id="b3e7f-289">Falhar com segurança</span><span class="sxs-lookup"><span data-stu-id="b3e7f-289">Fail securely</span></span>](https://www.owasp.org/index.php/Fail_securely) |
| <span data-ttu-id="b3e7f-290">**Etapas**</span><span class="sxs-lookup"><span data-stu-id="b3e7f-290">**Steps**</span></span> | <span data-ttu-id="b3e7f-291">O aplicativo deve falhar com segurança.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-291">Application should fail safely.</span></span> <span data-ttu-id="b3e7f-292">Qualquer método que retorna um valor booliano, com base em qual determinada decisão é tomada, deve ter um bloco de exceção criado cuidadosamente.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-292">Any method that returns a Boolean value, based on which certain decision is made, should have exception block carefully created.</span></span> <span data-ttu-id="b3e7f-293">Há muitos erros lógicos devido a problemas de segurança que passam quando o bloco de exceção é escrito com negligência.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-293">There are lot of logical errors due to which security issues creep in, when the exception block is written carelessly.</span></span>|

### <a name="example"></a><span data-ttu-id="b3e7f-294">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b3e7f-294">Example</span></span>
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
                        //// Adding additional check to enable CMS urls if they are not hosted on same domain.
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
<span data-ttu-id="b3e7f-295">O método acima sempre retornará True se ocorrer uma exceção.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-295">The above method will always return True, if some exception happens.</span></span> <span data-ttu-id="b3e7f-296">Se o usuário final fornecer uma URL malformada, que o navegador respeita, mas o construtor `Uri()` não, isso irá gerar uma exceção e a vítima será levada para uma URL válida, mas malformada.</span><span class="sxs-lookup"><span data-stu-id="b3e7f-296">If the end user provides a malformed URL, that the browser respects, but the `Uri()` constructor doesn't, this will throw an exception, and the victim will be taken to the valid but malformed URL.</span></span> 