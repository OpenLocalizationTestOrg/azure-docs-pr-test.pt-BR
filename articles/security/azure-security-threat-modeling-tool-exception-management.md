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
# <a name="security-frame-exception-management--mitigations"></a>Quadro de Segurança: Gerenciamento de Exceções | Atenuações 
| Produto/Serviço | Artigo |
| --------------- | ------- |
| **WCF** | <ul><li>[WCF - não inclui o nó serviceDebug no arquivo de configuração](#servicedebug)</li><li>[WCF - não inclui o nó serviceMetadata no arquivo de configuração](#servicemetadata)</li></ul> |
| **API da Web** | <ul><li>[Verificar se o tratamento de exceções adequado é feito na API Web ASP.NET ](#exception)</li></ul> |
| **Aplicativo Web** | <ul><li>[Não expor os detalhes da segurança nas mensagens de erro ](#messages)</li><li>[Implementar a página tratamento de erros Padrão ](#default)</li><li>[Definir o método de implantação tooRetail no IIS](#deployment)</li><li>[As exceções devem falhar com segurança](#fail)</li></ul> |

## <a id="servicedebug"></a>WCF - não inclui o nó serviceDebug no arquivo de configuração

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico, NET Framework 3 |
| **Atributos**              | N/D  |
| **Referências**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Etapas** | Serviços Windows Communication Framework (WCF) podem ser configurado tooexpose as informações de depuração. As informações de depuração não devem ser usadas nos ambientes de produção. Olá `<serviceDebug>` marca define se o recurso de saudação de informações de depuração está habilitado para um serviço WCF. Se Olá atributo includeExceptionDetailInFaults for definido tootrue, informações de exceção de aplicativo hello retornará tooclients. Os invasores podem aproveitar informações adicionais de saudação obterem a depuração de saída toomount ataques direcionados framework hello, banco de dados ou outros recursos usados pelo aplicativo hello. |

### <a name="example"></a>Exemplo
Olá, seguinte arquivo de configuração inclui Olá `<serviceDebug>` marca: 
```
<configuration> 
<system.serviceModel> 
<behaviors> 
<serviceBehaviors> 
<behavior name=""MyServiceBehavior""> 
<serviceDebug includeExceptionDetailInFaults=""True"" httpHelpPageEnabled=""True""/> 
... 
```
Desabilite as informações de depuração no serviço de saudação. Isso pode ser feito removendo Olá `<serviceDebug>` marca de arquivo de configuração do aplicativo. 

## <a id="servicemetadata"></a>WCF - não inclui o nó serviceMetadata no arquivo de configuração

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | Genérico, NET Framework 3 |
| **Referências**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Etapas** | Expor publicamente informações sobre um serviço pode fornecer aos invasores informações valiosas em como eles podem explorar o serviço de saudação. Olá `<serviceMetadata>` marca permite que o recurso de publicação de metadados de saudação. Os metadados do serviço podem conter informações confidenciais e não devem ser acessíveis publicamente. No mínimo, permitir somente usuários confiáveis tooaccess Olá metadados e certifique-se de que informações desnecessárias não são expostas. Melhor ainda, desabilite totalmente Olá capacidade toopublish metadados. Uma configuração segura do WCF não conterá Olá `<serviceMetadata>` marca. |

## <a id="exception"></a>Verificar se o tratamento de exceções adequado é feito na API Web ASP.NET

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | MVC 5, MVC 6 |
| **Atributos**              | N/D  |
| **Referências**              | [Tratamento de Exceções na API Web ASP.NET](http://www.asp.net/web-api/overview/error-handling/exception-handling), [Validação do Modelo na API Web ASP.NET](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api) |
| **Etapas** | Por padrão, a maioria das exceções não identificadas na API Web ASP.NET é convertida em uma resposta HTTP com um código de status`500, Internal Server Error`|

### <a name="example"></a>Exemplo
código de status de saudação toocontrol retornado por Olá API, `HttpResponseException` pode ser usado como mostrado abaixo: 
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

### <a name="example"></a>Exemplo
Para controlar ainda mais na resposta de exceção hello, Olá `HttpResponseMessage` classe pode ser usada, conforme mostrado abaixo: 
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
toocatch sem tratamento de exceções que não são do tipo hello `HttpResponseException`, filtros de exceção pode ser usados. Filtros de exceção implementam Olá `System.Web.Http.Filters.IExceptionFilter` interface. toowrite de maneira mais simples de saudação um filtro de exceção é tooderive de saudação `System.Web.Http.Filters.ExceptionFilterAttribute` classe e substituir o método OnException de saudação. 

### <a name="example"></a>Exemplo
Aqui está um filtro que converte as exceções `NotImplementedException` no código de status HTTP `501, Not Implemented`: 
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

Há várias maneiras tooregister um filtro de exceção de API da Web:
- por ação
- pelo controlador
- globalmente

### <a name="example"></a>Exemplo
Olá tooapply filtrar ação específica tooa, adicionar filtro hello como uma ação de toohello do atributo: 
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
### <a name="example"></a>Exemplo
tooapply Olá filtro tooall de ações de saudação em uma `controller`, adicionar filtro hello como um atributo toohello `controller` classe: 

```C#
[NotImplExceptionFilter]
public class ProductsController : ApiController
{
    // ...
}
```

### <a name="example"></a>Exemplo
Olá tooapply globalmente filtrar controladores de API da Web tooall, adicionar uma instância de saudação filtro toohello `GlobalConfiguration.Configuration.Filters` coleção. Filtros de exceção nesta coleção se aplicam a ação de controlador tooany API da Web. 
```C#
GlobalConfiguration.Configuration.Filters.Add(
    new ProductStore.NotImplExceptionFilterAttribute());
```

### <a name="example"></a>Exemplo
Para validação de modelo, o estado de modelo Olá pode ser passado tooCreateErrorResponse método conforme mostrado abaixo: 
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

Seleção Olá links na seção de referências de saudação para obter detalhes adicionais sobre manipulação excepcional e validação de modelo na API da Web do ASP.Net 

## <a id="messages"></a>Não expor os detalhes da segurança nas mensagens de erro

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | <p>Mensagens de erro genéricas são fornecidas diretamente toohello usuário sem incluir dados confidenciais de aplicativos. Exemplos de dados confidenciais:</p><ul><li>nomes do servidor</li><li>Cadeias de conexão</li><li>nomes de usuário</li><li>Senhas</li><li>procedimentos SQL</li><li>detalhes das falhas SQL dinâmicas</li><li>rastreamento de pilha e linhas de código</li><li>variáveis armazenadas na memória</li><li>locais da pasta e da unidade</li><li>pontos de instalação do aplicativo</li><li>definições de configuração do host</li><li>outros detalhes internos do aplicativo</li></ul><p>Interceptar todos os erros em um aplicativo e fornecer mensagens de erro genéricas, bem como habilitar os erros personalizados no IIS, ajudará a evitar a divulgação das informações. Banco de dados do SQL Server e .NET manipulação de exceções, entre outros arquiteturas de tratamento de erros são extremamente úteis e especialmente detalhado tooa usuário mal-intencionado que seu aplicativo de criação de perfil. Faça não diretamente Olá exibir conteúdo de uma classe derivada da classe de exceção .NET hello e certifique-se de que você tenha a manipulação adequada de exceções para que uma exceção inesperada inadvertidamente não é gerado diretamente toohello usuário.</p><ul><li>Forneça o usuário toohello que abstraem longe detalhes específicos encontrados diretamente na mensagem de exceção/Erro de saudação de diretamente de mensagens de erro genérico</li><li>Exibir conteúdo de saudação de uma exceção do .NET diretamente classe toohello usuário</li><li>Interceptação de todas as mensagens de erro e se apropriado informar o usuário Olá por meio de um cliente de aplicativo de toohello enviados de mensagem de erro genérico</li><li>Não expõem conteúdo Olá da classe de exceção Olá diretamente usuário toohello, especialmente Olá retornar o valor de `.ToString()`, ou Olá valores de propriedades de mensagem ou o rastreamento de pilha hello. Registrar essas informações com segurança e exibir um usuário mais simples de toohello de mensagem</li></ul>|

## <a id="default"></a>Implementar a página de tratamento de erros Padrão

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Caixa de Diálogo Editar Configurações das Páginas de Erro do ASP.NET](https://technet.microsoft.com/library/dd569096(WS.10).aspx) |
| **Etapas** | <p>Quando um aplicativo ASP.NET falhar e fizer com que um Erro Interno do Servidor HTTP/1.x 500 ou uma configuração do recurso (por exemplo, Filtragem da Solicitação) impeça que uma página seja exibida, uma mensagem de erro será gerada. Os administradores podem optar ou não o aplicativo hello deve exibir uma mensagem amigável toohello cliente, do cliente de toohello de mensagem de erro detalhada ou apenas toolocalhost de mensagem de erro detalhada. Olá <customErrors> marca no Web. config de Olá tem três modos:</p><ul><li>**Ativado:** especifica que os erros personalizados estão habilitados. Se nenhum atributo defaultRedirect for especificado, os usuários verão um erro genérico. erros personalizados Olá são mostrados os clientes remotos toohello e host local toohello</li><li>**Desativado:** especifica que os erros personalizados estão desabilitados. Olá erros detalhados do ASP.NET são mostrados os clientes remotos toohello e host local toohello</li><li>**RemoteOnly:** Especifica que os erros personalizados são mostrados apenas toohello clientes remotos e que os erros do ASP.NET são mostrados host local toohello. Este é o valor padrão de saudação</li></ul><p>Olá abrir `web.config` de arquivos para o site da aplicativo hello e certifique-se de que marca Olá foi `<customErrors mode="RemoteOnly" />` ou `<customErrors mode="On" />` definido.</p>|

## <a id="deployment"></a>Definir o método de implantação tooRetail no IIS

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [implantação Element (Esquema de Configurações do ASP.NET)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx) |
| **Etapas** | <p>Olá `<deployment retail>` switch é destinado ao uso por servidores IIS de produção. Essa opção é usada toohelp aplicativos executados com o melhor desempenho possível de saudação e informações de segurança menos possíveis leakages desabilitando Olá a saída do rastreamento em uma página, desabilitando toodisplay de capacidade de saudação toogenerate capacidade do aplicativo para detalhes do erro mensagens tooend usuários e Olá desabilitar a opção de debug.</p><p>Muitas vezes, os argumentos e as opções que estão voltados para os desenvolvedores, como um rastreamento da solicitação e depuração com falha, são habilitados durante o desenvolvimento ativo. É recomendável que o método de implantação hello em qualquer servidor de produção seja definido tooretail. Abra o arquivo Machine. config de saudação e certifique-se de que `<deployment retail="true" />` permanece definido tootrue.</p>|

## <a id="fail"></a>As exceções devem falhar com segurança

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Falhar com segurança](https://www.owasp.org/index.php/Fail_securely) |
| **Etapas** | O aplicativo deve falhar com segurança. Qualquer método que retorna um valor booliano, com base em qual determinada decisão é tomada, deve ter um bloco de exceção criado cuidadosamente. Há muitos erros lógicos devido toowhich deslizamento de problemas de segurança no, quando o bloco de exceção hello é escrito com negligência.|

### <a name="example"></a>Exemplo
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
Olá acima método sempre retornará True, se ocorrer uma exceção. Se o usuário final de saudação fornece uma URL malformada, que Olá aspectos do navegador, mas Olá `Uri()` construtor não, isso gerará uma exceção e vítima hello será tomada URL de toohello válido, mas malformado. 
