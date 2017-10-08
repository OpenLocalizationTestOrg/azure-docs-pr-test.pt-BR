---
title: "aaaDiagnose falhas e exceções em aplicativos com o Azure Application Insights de web | Microsoft Docs"
description: "Capture exceções de aplicativos do ASP.NET junto com a telemetria de solicitação."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d1e98390-3ce4-4d04-9351-144314a42aa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 8930e6d2b29f83ea635c4ecb7afd11fc1d97d085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-exceptions-in-your-web-apps-with-application-insights"></a>Diagnosticar exceções em seus aplicativos Web com o Application Insights
Exceções em seu aplicativo Web ao vivo são relatadas pelo [Application Insights](app-insights-overview.md). Você pode correlacionar solicitações com falha com exceções e outros eventos no cliente hello e no servidor, para que você pode diagnosticar rapidamente Olá causas.

## <a name="set-up-exception-reporting"></a>Configurar os relatórios de exceção
* exceções de toohave relatadas por meio de seu aplicativo de servidor:
  * Instale o[ SDK do Application Insights](app-insights-asp-net.md) no aplicativo ou
  * Servidores Web IIS: executar o [Agente do Application Insights](app-insights-monitor-performance-live-website-now.md) ou
  * Aplicativos web do Azure: Adicionar Olá [extensão do Application Insights](app-insights-azure-web-apps.md)
  * Os aplicativos web Java: Install Olá [agente Java](app-insights-java-agent.md)
* Instalar Olá [trecho de JavaScript](app-insights-javascript.md) em exceções de navegador de toocatch suas páginas da web.
* Em algumas estruturas de aplicativo ou com algumas configurações, você precisará tootake toocatch algumas etapas adicionais mais exceções:
  * [Formulários da Web](#web-forms)
  * [MVC](#mvc)
  * [API Web 1.*](#web-api-1)
  * [API Web 2.*](#web-api-2)
  * [WCF](#wcf)

## <a name="diagnosing-exceptions-using-visual-studio"></a>Diagnosticar exceções usando o Visual Studio
Abra a solução do aplicativo hello no Visual Studio toohelp com a depuração.

Execute o aplicativo hello, no servidor ou no computador de desenvolvimento usando F5.

Abra a janela de pesquisa do Application Insights Olá no Visual Studio e defina-toodisplay eventos do aplicativo. Durante a depuração, você pode fazer isso apenas clicando o botão do Application Insights hello.

![Clique com botão direito hello e escolha o Application Insights, aberto.](./media/app-insights-asp-net-exceptions/34.png)

Observe que você pode filtrar apenas exceções do hello relatório tooshow.

*Nenhuma exceção mostrando? Consulte [Capturar exceções](#exceptions).*

Clique em um tooshow de relatório de exceção do rastreamento de pilha.
Clique em uma referência de linha no rastreamento de pilha hello, arquivo de código relevante Olá tooopen.  

No código de hello, observe que CodeLens mostra dados sobre exceções hello:

![Notificação de exceções do CodeLens.](./media/app-insights-asp-net-exceptions/35.png)

## <a name="diagnosing-failures-using-hello-azure-portal"></a>Diagnosticar falhas usando Olá portal do Azure
Da visão geral do Application Insights de saudação do seu aplicativo, o bloco de falhas de saudação mostra gráficos de exceções e falha nas solicitações HTTP, junto com uma lista de saudação solicitar URLs que causam falhas mais frequentes hello.

![Escolha Configurações, Falhas.](./media/app-insights-asp-net-exceptions/012-start.png)

Clique por meio de um Olá falha tipos de exceção em ocorrências de tooindividual Olá lista tooget de exceção hello, onde você pode ver os detalhes de saudação e rastreamento de pilha:

![Selecione uma instância de uma solicitação com falha e em detalhes da exceção, obter tooinstances da exceção de saudação.](./media/app-insights-asp-net-exceptions/030-req-drill.png)

**Como alternativa,** você pode iniciar na lista de saudação de solicitações e localizar tooit relacionados de exceções.

*Nenhuma exceção mostrando? Consulte [Capturar exceções](#exceptions).*


## <a name="custom-tracing-and-log-data"></a>Dados personalizados de rastreamento e log
tooget dados de diagnóstico específicos tooyour aplicativo, você pode inserir código toosend seus próprios dados de telemetria. Isso exibidos na pesquisa de diagnóstica junto com a solicitação de hello, exibição de página e outros dados coletados automaticamente.

Você tem várias opções:

* [Trackevent](app-insights-api-custom-events-metrics.md#trackevent) normalmente é usado para monitorar os padrões de uso, mas Olá dados envia também aparecem em eventos personalizados na pesquisa de diagnóstica. Os eventos são nomeados e podem conter propriedades de cadeia de caracteres e métricas numéricas nas quais é possível [filtrar pesquisas de diagnóstico](app-insights-diagnostic-search.md).
* [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) permite que você envie dados mais longos, como informações POST.
* [TrackException()](#exceptions) envia rastreamentos de pilha. [Mais sobre exceções](#exceptions).
* Se você já usa uma estrutura de registros, como Log4Net ou NLog poderá [capturar esses logs](app-insights-asp-net-trace-logs.md) e vê-los na pesquisa de diagnóstico junto com os dados de solicitação e exceção.

Esses eventos, abra o toosee [pesquisa](app-insights-diagnostic-search.md), abra o filtro e, em seguida, escolha Custom Event, rastreamento ou exceção.

![Drill-through](./media/app-insights-asp-net-exceptions/viewCustomEvents.png)

> [!NOTE]
> Se seu aplicativo gera um lote de telemetria, módulo de amostragem adaptável Olá automaticamente reduzirá o volume Olá enviada toohello portal enviando apenas uma fração representativa de eventos. Eventos que fazem parte da saudação mesma operação será marcada ou desmarcada como um grupo, para que você possa navegar entre eventos relacionados. [Saiba mais sobre amostragem.](app-insights-sampling.md)
>
>

### <a name="how-toosee-request-post-data"></a>Como toosee solicitar dados de POSTAGEM
Detalhes da solicitação não incluam dados de saudação enviados tooyour aplicativo em uma chamada POST. toohave esses dados relatados:

* [Instalar o SDK do hello](app-insights-asp-net.md) em seu projeto de aplicativo.
* Inserir o código no seu aplicativo toocall [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace). Envie dados de POSTAGEM Olá no parâmetro de mensagem de saudação. Há um limite de tamanho de toohello permitido, experimente os dados essenciais toosend Olá apenas.
* Ao investigar uma falha na solicitação, localize rastreamentos Olá associado.  

![Drill-through](./media/app-insights-asp-net-exceptions/060-req-related.png)

## <a name="exceptions"></a> Capturando exceções e dados de diagnóstico relacionados
Primeiro, você não verá no portal de saudação todas as exceções de saudação que causam falhas em seu aplicativo. Você verá as exceções de navegador (se você estiver usando Olá [SDK de JavaScript](app-insights-javascript.md) nas páginas da web). Mas a maioria das exceções de servidor são detectados pelo IIS e você tiver toowrite um pouco de código toosee-los.

Você pode:

* **Registrar exceções explicitamente** inserindo código em exceções de saudação de tooreport de manipuladores de exceção.
* **Capturar exceções automaticamente** configurando sua estrutura do ASP.NET. Olá necessárias forem diferentes para diferentes tipos de estrutura.

## <a name="reporting-exceptions-explicitly"></a>Relatar exceções explicitamente
Olá, a maneira mais simples é tooinsert tooTrackException() uma chamada em um manipulador de exceção.

JavaScript

    try
    { ...
    }
    catch (ex)
    {
      appInsights.trackException(ex, "handler loc",
        {Game: currentGame.Name,
         State: currentGame.State.ToString()});
    }

C#

    var telemetry = new TelemetryClient();
    ...
    try
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string>
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send hello exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }

VB

    Dim telemetry = New TelemetryClient
    ...
    Try
      ...
    Catch ex as Exception
      ' Set up some properties:
      Dim properties = New Dictionary (Of String, String)
      properties.Add("Game", currentGame.Name)

      Dim measurements = New Dictionary (Of String, Double)
      measurements.Add("Users", currentGame.Users.Count)

      ' Send hello exception telemetry:
      telemetry.TrackException(ex, properties, measurements)
    End Try

Olá as medidas e as propriedades de parâmetros são opcionais, mas são úteis para [filtragem e adição de](app-insights-diagnostic-search.md) informações extras. Por exemplo, se você tiver um aplicativo que pode executar vários jogos, pode encontrar todos os Olá exceção relatórios jogo específico tooa relacionados. Você pode adicionar quantos itens como você como tooeach dicionário.

## <a name="browser-exceptions"></a>Exceções de navegador
A maioria das exceções de navegador são relatados.

Se sua página da web inclui arquivos de script de redes de fornecimento de conteúdo ou de outros domínios, verifique a marca de script tem atributo Olá ```crossorigin="anonymous"```, e esse servidor de saudação envia [cabeçalhos CORS](http://enable-cors.org/). Isso permitirá que você tooget um rastreamento de pilha e detalhes de exceções sem tratamento JavaScript desses recursos.

## <a name="web-forms"></a>Formulários da Web
Para formulários da web, Olá módulo HTTP será capaz de toocollect exceções de saudação quando não houver nenhum redirecionamentos configurados com CustomErrors.

Mas se você tiver redirecionamentos ativos, adicionar Olá linhas toohello Application_Error funcionam em Global.asax.cs a seguir. (Adicionar um arquivo Global.asax se você ainda não tiver um).

*C#*

    void Application_Error(object sender, EventArgs e)
    {
      if (HttpContext.Current.IsCustomErrorEnabled && Server.GetLastError  () != null)
      {
         var ai = new TelemetryClient(); // or re-use an existing instance

         ai.TrackException(Server.GetLastError());
      }
    }


## <a name="mvc"></a>MVC
Se hello [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configuração é `Off`, exceções estará disponíveis para Olá [módulo HTTP](https://msdn.microsoft.com/library/ms178468.aspx) toocollect. No entanto, se ele for `RemoteOnly` (padrão), ou `On`, exceção Olá será limpo e coletar de tooautomatically não está disponível para o Application Insights. Você pode corrigir isso, substituindo Olá [System.Web.Mvc.HandleErrorAttribute classe](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx)e aplicar classe Olá substituído, conforme mostrado Olá MVC versões diferentes abaixo ([github origem](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):

    using System;
    using System.Web.Mvc;
    using Microsoft.ApplicationInsights;

    namespace MVC2App.Controllers
    {
      [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
      public class AiHandleErrorAttribute : HandleErrorAttribute
      {
        public override void OnException(ExceptionContext filterContext)
        {
            if (filterContext != null && filterContext.HttpContext != null && filterContext.Exception != null)
            {
                //If customError is Off, then AI HTTPModule will report hello exception
                if (filterContext.HttpContext.IsCustomErrorEnabled)
                {   //or reuse instance (recommended!). see note above  
                    var ai = new TelemetryClient();
                    ai.TrackException(filterContext.Exception);
                }
            }
            base.OnException(filterContext);
        }
      }
    }

#### <a name="mvc-2"></a>MVC 2
Substitua o atributo de HandleError de saudação com seu novo atributo em seus controladores.

    namespace MVC2App.Controllers
    {
       [AiHandleError]
       public class HomeController : Controller
       {
    ...

[Amostra](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions)

#### <a name="mvc-3"></a>MVC 3
Registrar `AiHandleErrorAttribute` como um filtro global em Global.asax.cs:

    public class MyMvcApplication : System.Web.HttpApplication
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
         filters.Add(new AiHandleErrorAttribute());
      }
     ...

[Amostra](https://github.com/AppInsightsSamples/Mvc3UnhandledExceptionTelemetry)

#### <a name="mvc-4-mvc5"></a>MVC 4, MVC5
Registre AiHandleErrorAttribute como um filtro global em FilterConfig.cs:

    public class FilterConfig
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
        // Default replaced with hello override tootrack unhandled exceptions
        filters.Add(new AiHandleErrorAttribute());
      }
    }

[Amostra](https://github.com/AppInsightsSamples/Mvc5UnhandledExceptionTelemetry)

## <a name="web-api-1x"></a>Web API 1.x
Substitua System.Web.Http.Filters.ExceptionFilterAttribute:

    using System.Web.Http.Filters;
    using Microsoft.ApplicationInsights;

    namespace WebAPI.App_Start
    {
      public class AiExceptionFilterAttribute : ExceptionFilterAttribute
      {
        public override void OnException(HttpActionExecutedContext actionExecutedContext)
        {
            if (actionExecutedContext != null && actionExecutedContext.Exception != null)
            {  //or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(actionExecutedContext.Exception);    
            }
            base.OnException(actionExecutedContext);
        }
      }
    }

Você pode adicionar controladores de toospecific este atributo substituído ou adicioná-lo a configuração de filtros globais toohello na classe WebApiConfig de saudação:

    using System.Web.Http;
    using WebApi1.x.App_Start;

    namespace WebApi1.x
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            config.Routes.MapHttpRoute(name: "DefaultApi", routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional });
            ...
            config.EnableSystemDiagnosticsTracing();

            // Capture exceptions for Application Insights:
            config.Filters.Add(new AiExceptionFilterAttribute());
        }
      }
    }

[Amostra](https://github.com/AppInsightsSamples/WebApi_1.x_UnhandledExceptions)

Há um número de casos que não é possível lidar com os filtros de exceção de saudação. Por exemplo:

* Exceções geradas por construtores de controlador.
* Exceções geradas por manipuladores de mensagens.
* Exceções geradas durante o roteamento.
* Exceções geradas durante a serialização de conteúdo da resposta.

## <a name="web-api-2x"></a>Web API 2.x
Adicione uma implementação de IExceptionLogger:

    using System.Web.Http.ExceptionHandling;
    using Microsoft.ApplicationInsights;

    namespace ProductsAppPureWebAPI.App_Start
    {
      public class AiExceptionLogger : ExceptionLogger
      {
        public override void Log(ExceptionLoggerContext context)
        {
            if (context !=null && context.Exception != null)
            {//or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(context.Exception);
            }
            base.Log(context);
        }
      }
    }

Adicione estes serviços toohello WebApiConfig:

    using System.Web.Http;
    using System.Web.Http.ExceptionHandling;
    using ProductsAppPureWebAPI.App_Start;

    namespace WebApi2WithMVC
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
            config.Services.Add(typeof(IExceptionLogger), new AiExceptionLogger());
        }
      }
  }

[Amostra](https://github.com/AppInsightsSamples/WebApi_2.x_UnhandledExceptions)

Como alternativas, você pode:

1. Substituir Olá apenas ExceptionHandler com uma implementação personalizada de IExceptionHandler. Isso é chamado apenas quando framework hello está ainda poderá toochoose qual resposta de mensagem toosend (e não quando a conexão de saudação é anulada para a instância)
2. Filtros de exceção (conforme descrito na seção de saudação em controladores de 1. x da API da Web acima) - não é chamados em todos os casos.

## <a name="wcf"></a>WCF
Adicione uma classe que estende o atributo e implementa IErrorHandler e IServiceBehavior.

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.ServiceModel.Description;
    using System.ServiceModel.Dispatcher;
    using System.Web;
    using Microsoft.ApplicationInsights;

    namespace WcfService4.ErrorHandling
    {
      public class AiLogExceptionAttribute : Attribute, IErrorHandler, IServiceBehavior
      {
        public void AddBindingParameters(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase,
            System.Collections.ObjectModel.Collection<ServiceEndpoint> endpoints,
            System.ServiceModel.Channels.BindingParameterCollection bindingParameters)
        {
        }

        public void ApplyDispatchBehavior(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
            foreach (ChannelDispatcher disp in serviceHostBase.ChannelDispatchers)
            {
                disp.ErrorHandlers.Add(this);
            }
        }

        public void Validate(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
        }

        bool IErrorHandler.HandleError(Exception error)
        {//or reuse instance (recommended!). see note above
            var ai = new TelemetryClient();

            ai.TrackException(error);
            return false;
        }

        void IErrorHandler.ProvideFault(Exception error,
            System.ServiceModel.Channels.MessageVersion version,
            ref System.ServiceModel.Channels.Message fault)
        {
        }
      }
    }

Adicione as implementações de serviço Olá atributo toohello:

    namespace WcfService4
    {
        [AiLogException]
        public class Service1 : IService1
        {
         ...

[Amostra](https://github.com/AppInsightsSamples/WCFUnhandledExceptions)

## <a name="exception-performance-counters"></a>Contadores de desempenho de exceção
Se você tiver [instalado Olá Application Insights Agent](app-insights-monitor-performance-live-website-now.md) no seu servidor, você pode obter um gráfico de taxa de exceções hello, medido pelo .NET. Isso inclui exceções .NET tradas e sem tratamento.

Abra uma folha do Metrics Explorer, adicione um novo gráfico e selecione **Taxa de exceção**, listada em Contadores de Desempenho.

.NET framework do Hello calcula a taxa de saudação contando o número de saudação de exceções em um intervalo e dividindo pelo comprimento de saudação do intervalo de saudação.

Observe que ele seja diferente da contagem de 'Exceções' hello calculada pelo portal do Application Insights Olá contando TrackException relatórios. intervalos de amostragem de saudação são diferentes e Olá SDK não envia relatórios de TrackException para todas as exceções manipuladas e não manipuladas.

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="next-steps"></a>Próximas etapas
* [Monitorar REST, SQL e outros toodependencies de chamadas](app-insights-asp-net-dependencies.md)
* [Monitorar tempos de carregamento de página, exceções de navegador e chamadas AJAX](app-insights-javascript.md)
* [Monitorar contadores de desempenho](app-insights-performance-counters.md)
