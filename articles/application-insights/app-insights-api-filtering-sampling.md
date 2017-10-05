---
title: "Filtrando e pré-processando no SDK do Azure Application Insights | Microsoft Docs"
description: Escreva Processadores de Telemetria e Inicializadores de Telemetria para o SDK filtrar ou adicionar propriedades aos dados antes da telemetria ser enviada ao portal do Application Insights.
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
ms.openlocfilehash: 17e66775dd2cd1c858594102f1ddb32e2fbbccc8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="filtering-and-preprocessing-telemetry-in-the-application-insights-sdk"></a><span data-ttu-id="9e413-103">Filtrando e pré-processando a telemetria no SDK do Application Insights</span><span class="sxs-lookup"><span data-stu-id="9e413-103">Filtering and preprocessing telemetry in the Application Insights SDK</span></span>


<span data-ttu-id="9e413-104">Você pode escrever e configurar plug-ins para o SDK do Application Insights, a fim de personalizar o modo como a telemetria é capturada e processada antes de ser enviada ao serviço Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9e413-104">You can write and configure plug-ins for the Application Insights SDK to customize how telemetry is captured and processed before it is sent to the Application Insights service.</span></span>

* <span data-ttu-id="9e413-105">[Amostragem](app-insights-sampling.md) reduz o volume de telemetria sem afetar as estatísticas.</span><span class="sxs-lookup"><span data-stu-id="9e413-105">[Sampling](app-insights-sampling.md) reduces the volume of telemetry without affecting your statistics.</span></span> <span data-ttu-id="9e413-106">Ela mantém juntos os pontos de dados relacionadas para que você possa navegar entre eles para diagnosticar um problema.</span><span class="sxs-lookup"><span data-stu-id="9e413-106">It keeps together related data points so that you can navigate between them when diagnosing a problem.</span></span> <span data-ttu-id="9e413-107">No portal, as contagens totais são multiplicadas para compensar a amostragem.</span><span class="sxs-lookup"><span data-stu-id="9e413-107">In the portal, the total counts are multiplied to compensate for the sampling.</span></span>
* <span data-ttu-id="9e413-108">A Filtragem com Processadores de Telemetria [para ASP.NET](#filtering) ou [Java](app-insights-java-filter-telemetry.md) permite selecionar ou modificar a telemetria no SDK antes que ela seja enviada ao servidor.</span><span class="sxs-lookup"><span data-stu-id="9e413-108">Filtering with Telemetry Processors [for ASP.NET](#filtering) or [Java](app-insights-java-filter-telemetry.md) lets you select or modify telemetry in the SDK before it is sent to the server.</span></span> <span data-ttu-id="9e413-109">Por exemplo, você pode reduzir o volume de telemetria excluindo as solicitações de robôs.</span><span class="sxs-lookup"><span data-stu-id="9e413-109">For example, you could reduce the volume of telemetry by excluding requests from robots.</span></span> <span data-ttu-id="9e413-110">Mas a filtragem é uma abordagem mais básica para reduzir o tráfego comparado à amostragem.</span><span class="sxs-lookup"><span data-stu-id="9e413-110">But filtering is a more basic approach to reducing traffic than sampling.</span></span> <span data-ttu-id="9e413-111">Ela permite um maior controle sobre o que é transmitido, mas você precisa estar ciente de que ela afetará as estatísticas - por exemplo, se você filtrar todas as solicitações bem-sucedidas.</span><span class="sxs-lookup"><span data-stu-id="9e413-111">It allows you more control over what is transmitted, but you have to be aware that it affects your statistics - for example, if you filter out all successful requests.</span></span>
* <span data-ttu-id="9e413-112">[Inicializadores de Telemetria adicionam propriedades](#add-properties) a qualquer telemetria enviada do seu aplicativo, incluindo a telemetria dos módulos padrão.</span><span class="sxs-lookup"><span data-stu-id="9e413-112">[Telemetry Initializers add properties](#add-properties) to any telemetry sent from your app, including telemetry from the standard modules.</span></span> <span data-ttu-id="9e413-113">Por exemplo, você pode adicionar valores calculados ou números de versão pelos qual os dados serão filtrados no portal.</span><span class="sxs-lookup"><span data-stu-id="9e413-113">For example, you could add calculated values; or version numbers by which to filter the data in the portal.</span></span>
* <span data-ttu-id="9e413-114">[A API do SDK](app-insights-api-custom-events-metrics.md) é usada para enviar eventos personalizados e métricas.</span><span class="sxs-lookup"><span data-stu-id="9e413-114">[The SDK API](app-insights-api-custom-events-metrics.md) is used to send custom events and metrics.</span></span>

<span data-ttu-id="9e413-115">Antes de começar:</span><span class="sxs-lookup"><span data-stu-id="9e413-115">Before you start:</span></span>

* <span data-ttu-id="9e413-116">Instale o [SDK para ASP.NET](app-insights-asp-net.md) ou [SDK para Java](app-insights-java-get-started.md) do Application Insights em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9e413-116">Install the Application Insights [SDK for ASP.NET](app-insights-asp-net.md) or [SDK for Java](app-insights-java-get-started.md) in your app.</span></span>

<a name="filtering"></a>

## <a name="filtering-itelemetryprocessor"></a><span data-ttu-id="9e413-117">Filtragem: ITelemetryProcessor</span><span class="sxs-lookup"><span data-stu-id="9e413-117">Filtering: ITelemetryProcessor</span></span>
<span data-ttu-id="9e413-118">Essa técnica fornece um controle mais direto sobre o que é incluído ou excluído da transmissão de telemetria.</span><span class="sxs-lookup"><span data-stu-id="9e413-118">This technique gives you more direct control over what is included or excluded from the telemetry stream.</span></span> <span data-ttu-id="9e413-119">Você pode usá-la em conjunto com a Amostragem, ou separadamente.</span><span class="sxs-lookup"><span data-stu-id="9e413-119">You can use it in conjunction with Sampling, or separately.</span></span>

<span data-ttu-id="9e413-120">Para filtrar a telemetria, escreva um processador de telemetria e registre-o no SDK.</span><span class="sxs-lookup"><span data-stu-id="9e413-120">To filter telemetry, you write a telemetry processor and register it with the SDK.</span></span> <span data-ttu-id="9e413-121">Toda a telemetria passa pelo seu processador, e você pode optar por removê-la da transmissão ou por adicionar propriedades.</span><span class="sxs-lookup"><span data-stu-id="9e413-121">All telemetry goes through your processor, and you can choose to drop it from the stream, or add properties.</span></span> <span data-ttu-id="9e413-122">Isso inclui a telemetria dos módulos padrão como o coletor de solicitação HTTP e o coletor de dependência, além da telemetria escrita por você.</span><span class="sxs-lookup"><span data-stu-id="9e413-122">This includes telemetry from the standard modules such as the HTTP request collector and the dependency collector, as well as telemetry you have written yourself.</span></span> <span data-ttu-id="9e413-123">Por exemplo, você pode filtrar a telemetria sobre solicitações de robôs ou sobre chamadas de dependência bem-sucedidas.</span><span class="sxs-lookup"><span data-stu-id="9e413-123">You can, for example, filter out telemetry about requests from robots, or successful dependency calls.</span></span>

> [!WARNING]
> <span data-ttu-id="9e413-124">Filtrar a telemetria enviada do SDK usando processadores pode distorcer as estatísticas que você vê no portal e dificultar o acompanhamento de itens relacionados.</span><span class="sxs-lookup"><span data-stu-id="9e413-124">Filtering the telemetry sent from the SDK using processors can skew the statistics that you see in the portal, and make it difficult to follow related items.</span></span>
>
> <span data-ttu-id="9e413-125">Em vez disso, considere usar a [amostragem](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="9e413-125">Instead, consider using [sampling](app-insights-sampling.md).</span></span>
>
>

### <a name="create-a-telemetry-processor-c"></a><span data-ttu-id="9e413-126">Criar um processador de telemetria (C#)</span><span class="sxs-lookup"><span data-stu-id="9e413-126">Create a telemetry processor (C#)</span></span>
1. <span data-ttu-id="9e413-127">Verifique se a versão do SDK do Application Insights em seu projeto é a 2.0.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="9e413-127">Verify that the Application Insights SDK in your project is  version 2.0.0 or later.</span></span> <span data-ttu-id="9e413-128">Clique com o botão direito do mouse no projeto no Gerenciador de Soluções do Visual Studio e escolha Gerenciar Pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="9e413-128">Right-click your project in Visual Studio Solution Explorer and choose Manage NuGet Packages.</span></span> <span data-ttu-id="9e413-129">No gerenciador de pacotes NuGet, marque Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="9e413-129">In NuGet package manager, check Microsoft.ApplicationInsights.Web.</span></span>
2. <span data-ttu-id="9e413-130">Para criar um filtro, implemente ITelemetryProcessor.</span><span class="sxs-lookup"><span data-stu-id="9e413-130">To create a filter, implement ITelemetryProcessor.</span></span> <span data-ttu-id="9e413-131">Este é outro ponto de extensibilidade como módulo de telemetria, inicializador de telemetria e canal de telemetria.</span><span class="sxs-lookup"><span data-stu-id="9e413-131">This is another extensibility point like telemetry module, telemetry initializer, and telemetry channel.</span></span>

    <span data-ttu-id="9e413-132">Observe que os Processadores de Telemetria criam uma cadeia de processamento.</span><span class="sxs-lookup"><span data-stu-id="9e413-132">Notice that Telemetry Processors construct a chain of processing.</span></span> <span data-ttu-id="9e413-133">Ao criar uma instância de um processador de telemetria, você transmite um link para o próximo processador na cadeia.</span><span class="sxs-lookup"><span data-stu-id="9e413-133">When you instantiate a telemetry processor, you pass a link to the next processor in the chain.</span></span> <span data-ttu-id="9e413-134">Quando um ponto de dados de telemetria é transmitido para o método Process, ele faz seu trabalho e, em seguida, chama o próximo Processador de Telemetria da cadeia.</span><span class="sxs-lookup"><span data-stu-id="9e413-134">When a telemetry data point is passed to the Process method, it does its work and then calls the next Telemetry Processor in the chain.</span></span>

    ``` C#

    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    public class SuccessfulDependencyFilter : ITelemetryProcessor
      {

        private ITelemetryProcessor Next { get; set; }

        // You can pass values from .config
        public string MyParamFromConfigFile { get; set; }

        // Link processors to each other in a chain.
        public SuccessfulDependencyFilter(ITelemetryProcessor next)
        {
            this.Next = next;
        }
        public void Process(ITelemetry item)
        {
            // To filter out an item, just return
            if (!OKtoSend(item)) { return; }
            // Modify the item if required
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
1. <span data-ttu-id="9e413-135">Insira isto no ApplicationInsights.config:</span><span class="sxs-lookup"><span data-stu-id="9e413-135">Insert this in ApplicationInsights.config:</span></span>

```XML

    <TelemetryProcessors>
      <Add Type="WebApplication9.SuccessfulDependencyFilter, WebApplication9">
         <!-- Set public property -->
         <MyParamFromConfigFile>2-beta</MyParamFromConfigFile>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="9e413-136">(Essa é a mesma seção em que você inicializa um filtro de amostragem).</span><span class="sxs-lookup"><span data-stu-id="9e413-136">(This is the same section where you initialize a sampling filter.)</span></span>

<span data-ttu-id="9e413-137">Você pode transmitir valores de cadeia de caracteres do arquivo .config fornecendo propriedades nomeadas públicas em sua classe.</span><span class="sxs-lookup"><span data-stu-id="9e413-137">You can pass string values from the .config file by providing public named properties in your class.</span></span>

> [!WARNING]
> <span data-ttu-id="9e413-138">Fique atento para que o nome do tipo e todos os nomes de propriedade no arquivo .config correspondam aos nomes de classe e de propriedade no código.</span><span class="sxs-lookup"><span data-stu-id="9e413-138">Take care to match the type name and any property names in the .config file to the class and property names in the code.</span></span> <span data-ttu-id="9e413-139">Se o arquivo .config fizer referência a um tipo ou propriedade inexistente, o SDK poderá silenciosamente falhar ao enviar qualquer telemetria.</span><span class="sxs-lookup"><span data-stu-id="9e413-139">If the .config file references a non-existent type or property, the SDK may silently fail to send any telemetry.</span></span>
>
>

<span data-ttu-id="9e413-140">**Como alternativa,** é possível inicializar o filtro no código.</span><span class="sxs-lookup"><span data-stu-id="9e413-140">**Alternatively,** you can initialize the filter in code.</span></span> <span data-ttu-id="9e413-141">Em uma classe de inicialização adequada - por exemplo AppStart em Global.asax.cs - insira seu processador na cadeia:</span><span class="sxs-lookup"><span data-stu-id="9e413-141">In a suitable initialization class - for example AppStart in Global.asax.cs - insert your processor into the chain:</span></span>

```C#

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;
    builder.Use((next) => new SuccessfulDependencyFilter(next));

    // If you have more processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="9e413-142">Os TelemetryClients criados depois desse ponto usarão seus processadores.</span><span class="sxs-lookup"><span data-stu-id="9e413-142">TelemetryClients created after this point will use your processors.</span></span>

### <a name="example-filters"></a><span data-ttu-id="9e413-143">Filtros de exemplo</span><span class="sxs-lookup"><span data-stu-id="9e413-143">Example filters</span></span>
#### <a name="synthetic-requests"></a><span data-ttu-id="9e413-144">Solicitações sintéticas</span><span class="sxs-lookup"><span data-stu-id="9e413-144">Synthetic requests</span></span>
<span data-ttu-id="9e413-145">Filtre os bots e os testes Web.</span><span class="sxs-lookup"><span data-stu-id="9e413-145">Filter out bots and web tests.</span></span> <span data-ttu-id="9e413-146">Embora o Metrics Explorer ofereça a opção para filtrar fontes sintéticas, essa opção reduz o tráfego filtrando-as no SDK.</span><span class="sxs-lookup"><span data-stu-id="9e413-146">Although Metrics Explorer gives you the option to filter out synthetic sources, this option reduces traffic by filtering them at the SDK.</span></span>

``` C#

    public void Process(ITelemetry item)
    {
      if (!string.IsNullOrEmpty(item.Context.Operation.SyntheticSource)) {return;}

      // Send everything else:
      this.Next.Process(item);
    }

```

#### <a name="failed-authentication"></a><span data-ttu-id="9e413-147">Autenticação com falha</span><span class="sxs-lookup"><span data-stu-id="9e413-147">Failed authentication</span></span>
<span data-ttu-id="9e413-148">Filtre as solicitações com uma resposta "401".</span><span class="sxs-lookup"><span data-stu-id="9e413-148">Filter out requests with a "401" response.</span></span>

```C#

public void Process(ITelemetry item)
{
    var request = item as RequestTelemetry;

    if (request != null &&
    request.ResponseCode.Equals("401", StringComparison.OrdinalIgnoreCase))
    {
        // To filter out an item, just terminate the chain:
        return;
    }
    // Send everything else:
    this.Next.Process(item);
}

```

#### <a name="filter-out-fast-remote-dependency-calls"></a><span data-ttu-id="9e413-149">Filtrar chamadas de dependência rápidas remotas</span><span class="sxs-lookup"><span data-stu-id="9e413-149">Filter out fast remote dependency calls</span></span>
<span data-ttu-id="9e413-150">Se desejar diagnosticar chamadas lentas, filtre as rápidas.</span><span class="sxs-lookup"><span data-stu-id="9e413-150">If you only want to diagnose calls that are slow, filter out the fast ones.</span></span>

> [!NOTE]
> <span data-ttu-id="9e413-151">Isso distorcerá as estatísticas que você vê no portal.</span><span class="sxs-lookup"><span data-stu-id="9e413-151">This will skew the statistics you see on the portal.</span></span> <span data-ttu-id="9e413-152">O gráfico de dependência parecerá como se as chamadas de dependência fossem todas falhas.</span><span class="sxs-lookup"><span data-stu-id="9e413-152">The dependency chart will look as if the dependency calls are all failures.</span></span>
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

#### <a name="diagnose-dependency-issues"></a><span data-ttu-id="9e413-153">Diagnosticar problemas de dependência</span><span class="sxs-lookup"><span data-stu-id="9e413-153">Diagnose dependency issues</span></span>
<span data-ttu-id="9e413-154">[Este blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) descreve um projeto para diagnosticar problemas de dependência ao enviar automaticamente pings regulares para as dependências.</span><span class="sxs-lookup"><span data-stu-id="9e413-154">[This blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) describes a project to diagnose dependency issues by automatically sending regular pings to dependencies.</span></span>


<a name="add-properties"></a>

## <a name="add-properties-itelemetryinitializer"></a><span data-ttu-id="9e413-155">Adicionar propriedades: ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="9e413-155">Add properties: ITelemetryInitializer</span></span>
<span data-ttu-id="9e413-156">Use inicializadores de telemetria para definir propriedades globais que são enviadas com todas as telemetrias e para substituir o comportamento selecionado dos módulos de telemetria padrão.</span><span class="sxs-lookup"><span data-stu-id="9e413-156">Use telemetry initializers to define global properties that are sent with all telemetry; and to override selected behavior of the standard telemetry modules.</span></span>

<span data-ttu-id="9e413-157">Por exemplo, o Application Insights para o pacote da Web coleta a telemetria sobre solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="9e413-157">For example, the Application Insights for Web package collects telemetry about HTTP requests.</span></span> <span data-ttu-id="9e413-158">Por padrão, ele sinaliza como qualquer solicitação com um código de resposta de falha > = 400.</span><span class="sxs-lookup"><span data-stu-id="9e413-158">By default, it flags as failed any request with a response code >= 400.</span></span> <span data-ttu-id="9e413-159">Mas se desejar tratar 400 como êxito, você pode fornecer um inicializador de telemetria que define a propriedade Sucess.</span><span class="sxs-lookup"><span data-stu-id="9e413-159">But if you want to treat 400 as a success, you can provide a telemetry initializer that sets the Success property.</span></span>

<span data-ttu-id="9e413-160">Se você fornecer um inicializador de telemetria, ele é chamado sempre que qualquer um dos métodos Track*() for chamado.</span><span class="sxs-lookup"><span data-stu-id="9e413-160">If you provide a telemetry initializer, it is called whenever any of the Track*() methods is called.</span></span> <span data-ttu-id="9e413-161">Isso inclui métodos chamados pelos módulos de telemetria padrão.</span><span class="sxs-lookup"><span data-stu-id="9e413-161">This includes methods called by the standard telemetry modules.</span></span> <span data-ttu-id="9e413-162">Por convenção, esses módulos não definem qualquer propriedade que já foi definida por um inicializador.</span><span class="sxs-lookup"><span data-stu-id="9e413-162">By convention, these modules do not set any property that has already been set by an initializer.</span></span>

<span data-ttu-id="9e413-163">**Definir seu inicializador**</span><span class="sxs-lookup"><span data-stu-id="9e413-163">**Define your initializer**</span></span>

<span data-ttu-id="9e413-164">*C#*</span><span class="sxs-lookup"><span data-stu-id="9e413-164">*C#*</span></span>

```C#

    using System;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.DataContracts;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that overrides the default SDK
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
                // If we set the Success property, the SDK won't change it:
                requestTelemetry.Success = true;
                // Allow us to filter these requests in the portal:
                requestTelemetry.Context.Properties["Overridden400s"] = "true";
            }
            // else leave the SDK to set the Success property      
        }
      }
    }
```

<span data-ttu-id="9e413-165">**Carregue seu inicializador**</span><span class="sxs-lookup"><span data-stu-id="9e413-165">**Load your initializer**</span></span>

<span data-ttu-id="9e413-166">Em ApplicationInsights.config:</span><span class="sxs-lookup"><span data-stu-id="9e413-166">In ApplicationInsights.config:</span></span>

    <ApplicationInsights>
      <TelemetryInitializers>
        <!-- Fully qualified type name, assembly name: -->
        <Add Type="MvcWebRole.Telemetry.MyTelemetryInitializer, MvcWebRole"/>
        ...
      </TelemetryInitializers>
    </ApplicationInsights>

<span data-ttu-id="9e413-167">*Como alternativa,* você pode instanciar o inicializador no código, por exemplo em Global.aspx.cs:</span><span class="sxs-lookup"><span data-stu-id="9e413-167">*Alternatively,* you can instantiate the initializer in code, for example in Global.aspx.cs:</span></span>

```C#
    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```


[<span data-ttu-id="9e413-168">Ver mais deste exemplo.</span><span class="sxs-lookup"><span data-stu-id="9e413-168">See more of this sample.</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole)

<a name="js-initializer"></a>

### <a name="javascript-telemetry-initializers"></a><span data-ttu-id="9e413-169">Inicializadores de telemetria JavaScript</span><span class="sxs-lookup"><span data-stu-id="9e413-169">JavaScript telemetry initializers</span></span>
<span data-ttu-id="9e413-170">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="9e413-170">*JavaScript*</span></span>

<span data-ttu-id="9e413-171">Insira um inicializador de telemetria logo após o código de inicialização que você obteve do portal:</span><span class="sxs-lookup"><span data-stu-id="9e413-171">Insert a telemetry initializer immediately after the initialization code that you got from the portal:</span></span>

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

                // To check the telemetry item’s type - for example PageView:
                if (envelope.name == Microsoft.ApplicationInsights.Telemetry.PageView.envelopeType) {
                    // this statement removes url from all page view documents
                    telemetryItem.url = "URL CENSORED";
                }

                // To set custom properties:
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["globalProperty"] = "boo";

                // To set custom metrics:
                telemetryItem.measurements = telemetryItem.measurements || {};
                telemetryItem.measurements["globalMetric"] = 100;
            });
        });

        // End of inserted code.

        appInsights.trackPageView();
    </script>
```

<span data-ttu-id="9e413-172">Para obter um resumo das propriedades não personalizadas disponíveis em telemetryItem, veja o [Modelo de dados de exportação do Application Insights](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="9e413-172">For a summary of the non-custom properties available on the telemetryItem, see [Application Insights Export Data Model](app-insights-export-data-model.md).</span></span>

<span data-ttu-id="9e413-173">Você pode adicionar quantos inicializadores desejar.</span><span class="sxs-lookup"><span data-stu-id="9e413-173">You can add as many initializers as you like.</span></span>

## <a name="itelemetryprocessor-and-itelemetryinitializer"></a><span data-ttu-id="9e413-174">ITelemetryProcessor e ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="9e413-174">ITelemetryProcessor and ITelemetryInitializer</span></span>
<span data-ttu-id="9e413-175">Qual é a diferença entre os processadores de telemetria e inicializadores de telemetria?</span><span class="sxs-lookup"><span data-stu-id="9e413-175">What's the difference between telemetry processors and telemetry initializers?</span></span>

* <span data-ttu-id="9e413-176">Há algumas sobreposições no que você pode fazer com eles: ambos podem ser usados para adicionar propriedades à telemetria.</span><span class="sxs-lookup"><span data-stu-id="9e413-176">There are some overlaps in what you can do with them: both can be used to add properties to telemetry.</span></span>
* <span data-ttu-id="9e413-177">Sempre execute TelemetryInitializers antes de TelemetryProcessors.</span><span class="sxs-lookup"><span data-stu-id="9e413-177">TelemetryInitializers always run before TelemetryProcessors.</span></span>
* <span data-ttu-id="9e413-178">TelemetryProcessors permitem que você substitua ou descarte completamente um item de telemetria.</span><span class="sxs-lookup"><span data-stu-id="9e413-178">TelemetryProcessors allow you to completely replace or discard a telemetry item.</span></span>
* <span data-ttu-id="9e413-179">TelemetryProcessors não processam telemetria do contador de desempenho.</span><span class="sxs-lookup"><span data-stu-id="9e413-179">TelemetryProcessors don't process performance counter telemetry.</span></span>


## <a name="reference-docs"></a><span data-ttu-id="9e413-180">Documentos de Referência</span><span class="sxs-lookup"><span data-stu-id="9e413-180">Reference docs</span></span>
* [<span data-ttu-id="9e413-181">Visão geral da API</span><span class="sxs-lookup"><span data-stu-id="9e413-181">API Overview</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="9e413-182">Referência do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9e413-182">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)

## <a name="sdk-code"></a><span data-ttu-id="9e413-183">Código do SDK</span><span class="sxs-lookup"><span data-stu-id="9e413-183">SDK Code</span></span>
* [<span data-ttu-id="9e413-184">SDK de Núcleo do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9e413-184">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="9e413-185">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="9e413-185">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="9e413-186">SDK do JavaScript</span><span class="sxs-lookup"><span data-stu-id="9e413-186">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)

## <span data-ttu-id="9e413-187"><a name="next"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9e413-187"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="9e413-188">Pesquisar eventos e logs</span><span class="sxs-lookup"><span data-stu-id="9e413-188">Search events and logs</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="9e413-189">Amostragem</span><span class="sxs-lookup"><span data-stu-id="9e413-189">Sampling</span></span>](app-insights-sampling.md)
* [<span data-ttu-id="9e413-190">Solução de problemas</span><span class="sxs-lookup"><span data-stu-id="9e413-190">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
