---
title: "aaaFiltering e o pré-processamento no hello Azure SDK do Application Insights | Microsoft Docs"
description: "Gravar inicializadores de telemetria e processadores de telemetria para Olá SDK toofilter ou adicione dados de toohello de propriedades antes de telemetria Olá é enviada toohello portal do Application Insights."
services: application-insights
documentationcenter: 
author: beckylino
manager: carmonm
ms.assetid: 38a9e454-43d5-4dba-a0f0-bd7cd75fb97b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 11/23/2016
ms.author: bwren
ms.openlocfilehash: 51b9db69b2375b8799718f1b0e1af77620dc2692
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="filtering-and-preprocessing-telemetry-in-hello-application-insights-sdk"></a>Filtragem e o pré-processamento telemetria no hello SDK do Application Insights


Você pode gravar e configurar plug-ins para Olá SDK do Application Insights toocustomize como telemetria é capturada e processada antes de serem enviado toohello serviço Application Insights.

* [Amostragem](app-insights-sampling.md) reduz o volume de saudação de telemetria sem afetar as estatísticas. Ela mantém juntos os pontos de dados relacionadas para que você possa navegar entre eles para diagnosticar um problema. No portal de hello, contagens do total de saudação são multiplicado toocompensate para amostragem de saudação.
* Filtrando com processadores de telemetria [para ASP.NET](#filtering) ou [Java](app-insights-java-filter-telemetry.md) permite selecionar ou modificar telemetria no hello SDK antes de serem enviado toohello server. Por exemplo, você pode reduzir o volume de saudação de telemetria excluindo solicitações de robôs. Mas a filtragem é um tráfego de tooreducing abordagem mais simples de amostragem. Ele permite a você mais controle sobre o que é transmitido, mas ter toobe ciente de que ele afeta estatísticas - por exemplo, se você filtrar todas as solicitações bem sucedidas.
* [Inicializadores de telemetria adicionar propriedades](#add-properties) tooany telemetria enviada do seu aplicativo, incluindo a telemetria dos módulos padrão hello. Por exemplo, você pode adicionar valores calculados; ou os números de versão de dados no portal de Olá Olá toofilter.
* [Olá API do SDK](app-insights-api-custom-events-metrics.md) é métricas e eventos personalizados toosend usado.

Antes de começar:

* Instalar Olá Application Insights [SDK para ASP.NET](app-insights-asp-net.md) ou [SDK para Java](app-insights-java-get-started.md) em seu aplicativo.

<a name="filtering"></a>

## <a name="filtering-itelemetryprocessor"></a>Filtragem: ITelemetryProcessor
Essa técnica fornece controle mais direto sobre o que é incluído ou excluído de fluxo de telemetria hello. Você pode usá-la em conjunto com a Amostragem, ou separadamente.

Telemetria de toofilter você gravar um processador de telemetria e registrá-lo com hello SDK. Toda a telemetria atravessa o processador, e você pode escolher toodrop do hello fluxo ou adicionar propriedades. Isso inclui a telemetria de módulos de saudação padrão como coletores de solicitação HTTP hello e coletor de dependência Olá, bem como telemetria que foram gravadas por conta própria. Por exemplo, você pode filtrar a telemetria sobre solicitações de robôs ou sobre chamadas de dependência bem-sucedidas.

> [!WARNING]
> Filtragem de telemetria Olá enviada do hello SDK usando processadores pode afetar itens relacionados a estatísticas de saudação que você consulte no portal de saudação e torná-lo toofollow difícil.
>
> Em vez disso, considere usar a [amostragem](app-insights-sampling.md).
>
>

### <a name="create-a-telemetry-processor-c"></a>Criar um processador de telemetria (C#)
1. Verifique se esse SDK do Application Insights Olá em seu projeto está versão 2.0.0 ou posterior. Clique com o botão direito do mouse no projeto no Gerenciador de Soluções do Visual Studio e escolha Gerenciar Pacotes NuGet. No gerenciador de pacotes NuGet, marque Microsoft.ApplicationInsights.Web.
2. toocreate um filtro, implementar ITelemetryProcessor. Este é outro ponto de extensibilidade como módulo de telemetria, inicializador de telemetria e canal de telemetria.

    Observe que os Processadores de Telemetria criam uma cadeia de processamento. Quando você cria uma instância de um processador de telemetria, você passar um processador de Avançar toohello link na cadeia de saudação. Quando um ponto de dados de telemetria é passado método toohello, faz seu trabalho e, em seguida, chama Olá próximo processador telemetria na cadeia de saudação.

    ``` C#

    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    public class SuccessfulDependencyFilter : ITelemetryProcessor
      {

        private ITelemetryProcessor Next { get; set; }

        // You can pass values from .config
        public string MyParamFromConfigFile { get; set; }

        // Link processors tooeach other in a chain.
        public SuccessfulDependencyFilter(ITelemetryProcessor next)
        {
            this.Next = next;
        }
        public void Process(ITelemetry item)
        {
            // toofilter out an item, just return
            if (!OKtoSend(item)) { return; }
            // Modify hello item if required
            ModifyItem(item);

            this.Next.Process(item);
        }

        // Example: replace with your own criteria.
        private bool OKtoSend (ITelemetry item)
        {
            var dependency = item as DependencyTelemetry;
            if (dependency == null) return true;

            return dependency.Success != true;
        }

        // Example: replace with your own modifiers.
        private void ModifyItem (ITelemetry item)
        {
            item.Context.Properties.Add("app-version", "1." + MyParamFromConfigFile);
        }
    }

    ```
1. Insira isto no ApplicationInsights.config:

```XML

    <TelemetryProcessors>
      <Add Type="WebApplication9.SuccessfulDependencyFilter, WebApplication9">
         <!-- Set public property -->
         <MyParamFromConfigFile>2-beta</MyParamFromConfigFile>
      </Add>
    </TelemetryProcessors>

```

(Isso é hello mesma seção em que você inicializar um filtro de amostragem.)

Você pode passar valores de cadeia de caracteres do arquivo. config de saudação fornecendo propriedades nomeadas públicas em sua classe.

> [!WARNING]
> Lembre-se nome do tipo hello toomatch e nomes de propriedade da classe toohello do hello. config arquivo e nomes de propriedade no código de saudação. Se o arquivo. config de saudação faz referência a um tipo de inexistente ou a propriedade, Olá SDK pode falhar em modo silencioso toosend qualquer telemetria.
>
>

**Como alternativa,** , você pode inicializar filtro Olá no código. Em uma classe de inicialização adequado - por exemplo AppStart em Global.asax.cs - inserir o processador cadeia hello:

```C#

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;
    builder.Use((next) => new SuccessfulDependencyFilter(next));

    // If you have more processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

Os TelemetryClients criados depois desse ponto usarão seus processadores.

### <a name="example-filters"></a>Filtros de exemplo
#### <a name="synthetic-requests"></a>Solicitações sintéticas
Filtre os bots e os testes Web. Embora Metrics Explorer oferece Olá toofilter opção out sintéticos fontes, essa opção reduz o tráfego filtrá-los em Olá SDK.

``` C#

    public void Process(ITelemetry item)
    {
      if (!string.IsNullOrEmpty(item.Context.Operation.SyntheticSource)) {return;}

      // Send everything else:
      this.Next.Process(item);
    }

```

#### <a name="failed-authentication"></a>Autenticação com falha
Filtre as solicitações com uma resposta "401".

```C#

public void Process(ITelemetry item)
{
    var request = item as RequestTelemetry;

    if (request != null &&
    request.ResponseCode.Equals("401", StringComparison.OrdinalIgnoreCase))
    {
        // toofilter out an item, just terminate hello chain:
        return;
    }
    // Send everything else:
    this.Next.Process(item);
}

```

#### <a name="filter-out-fast-remote-dependency-calls"></a>Filtrar chamadas de dependência rápidas remotas
Se você quiser apenas chamadas de toodiagnose estão lentas, filtre Olá fast os.

> [!NOTE]
> Isso irá distorcer estatísticas Olá mostrados no portal de saudação. gráfico de dependência de saudação aparecerá como se chamadas de dependência de saudação são todas as falhas.
>
>

``` C#

public void Process(ITelemetry item)
{
    var request = item as DependencyTelemetry;

    if (request != null && request.Duration.TotalMilliseconds < 100)
    {
        return;
    }
    this.Next.Process(item);
}

```

#### <a name="diagnose-dependency-issues"></a>Diagnosticar problemas de dependência
[Este blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) descreve um problema de dependência do projeto toodiagnose enviando automaticamente toodependencies pings regular.


<a name="add-properties"></a>

## <a name="add-properties-itelemetryinitializer"></a>Adicionar propriedades: ITelemetryInitializer
Uso da telemetria inicializadores toodefine propriedades globais que são enviadas com toda a Telemetria; e o comportamento de toooverride selecionado dos módulos de telemetria padrão hello.

Por exemplo, hello Application Insights para o pacote da Web coleta a telemetria sobre solicitações HTTP. Por padrão, ele sinaliza como qualquer solicitação com um código de resposta de falha > = 400. Mas se você quiser tootreat 400 como um êxito, você pode fornecer um inicializador de telemetria que define a propriedade de êxito de saudação.

Se você fornecer um inicializador de telemetria, ele é chamado sempre que qualquer um dos Olá Track*() métodos é chamado. Isso inclui métodos chamados pelos módulos de telemetria padrão hello. Por convenção, esses módulos não definem qualquer propriedade que já foi definida por um inicializador.

**Definir seu inicializador**

*C#*

```C#

    using System;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.DataContracts;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that overrides hello default SDK
       * behavior of treating response codes >= 400 as failed requests
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            var requestTelemetry = telemetry as RequestTelemetry;
            // Is this a TrackRequest() ?
            if (requestTelemetry == null) return;
            int code;
            bool parsed = Int32.TryParse(requestTelemetry.ResponseCode, out code);
            if (!parsed) return;
            if (code >= 400 && code < 500)
            {
                // If we set hello Success property, hello SDK won't change it:
                requestTelemetry.Success = true;
                // Allow us toofilter these requests in hello portal:
                requestTelemetry.Context.Properties["Overridden400s"] = "true";
            }
            // else leave hello SDK tooset hello Success property      
        }
      }
    }
```

**Carregue seu inicializador**

Em ApplicationInsights.config:

    <ApplicationInsights>
      <TelemetryInitializers>
        <!-- Fully qualified type name, assembly name: -->
        <Add Type="MvcWebRole.Telemetry.MyTelemetryInitializer, MvcWebRole"/>
        ...
      </TelemetryInitializers>
    </ApplicationInsights>

*Como alternativa,* você pode instanciar inicializador Olá no código, por exemplo, em Global.aspx.cs:

```C#
    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```


[Ver mais deste exemplo.](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole)

<a name="js-initializer"></a>

### <a name="javascript-telemetry-initializers"></a>Inicializadores de telemetria JavaScript
*JavaScript*

Insira um inicializador de telemetria imediatamente após o código de inicialização de saudação que você obteve no portal de saudação:

```JS

    <script type="text/javascript">
        // ... initialization code
        ...({
            instrumentationKey: "your instrumentation key"
        });
        window.appInsights = appInsights;


        // Adding telemetry initializer.
        // This is called whenever a new telemetry item
        // is created.

        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;

                // toocheck hello telemetry item’s type - for example PageView:
                if (envelope.name == Microsoft.ApplicationInsights.Telemetry.PageView.envelopeType) {
                    // this statement removes url from all page view documents
                    telemetryItem.url = "URL CENSORED";
                }

                // tooset custom properties:
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["globalProperty"] = "boo";

                // tooset custom metrics:
                telemetryItem.measurements = telemetryItem.measurements || {};
                telemetryItem.measurements["globalMetric"] = 100;
            });
        });

        // End of inserted code.

        appInsights.trackPageView();
    </script>
```

Para obter um resumo das propriedades de não personalizado Olá disponíveis em telemetryItem hello, consulte [aplicativo Insights exportar dados de modelo](app-insights-export-data-model.md).

Você pode adicionar quantos inicializadores desejar.

## <a name="itelemetryprocessor-and-itelemetryinitializer"></a>ITelemetryProcessor e ITelemetryInitializer
Qual é a diferença de saudação entre os processadores de telemetria e inicializadores de telemetria?

* Há algumas sobreposições em que você pode fazer com eles: ambos podem ser usados tooadd propriedades tootelemetry.
* Sempre execute TelemetryInitializers antes de TelemetryProcessors.
* TelemetryProcessors permitem que você substitua toocompletely ou descartar um item de telemetria.
* TelemetryProcessors não processam telemetria do contador de desempenho.


## <a name="reference-docs"></a>Documentos de Referência
* [Visão geral da API](app-insights-api-custom-events-metrics.md)
* [Referência do ASP.NET](https://msdn.microsoft.com/library/dn817570.aspx)

## <a name="sdk-code"></a>Código do SDK
* [SDK de Núcleo do ASP.NET](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [ASP.NET 5](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [SDK do JavaScript](https://github.com/Microsoft/ApplicationInsights-JS)

## <a name="next"></a>Próximas etapas
* [Pesquisar eventos e logs](app-insights-diagnostic-search.md)
* [Amostragem](app-insights-sampling.md)
* [Solução de problemas](app-insights-troubleshoot-faq.md)
