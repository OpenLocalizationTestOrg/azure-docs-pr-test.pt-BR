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
# <a name="filtering-and-preprocessing-telemetry-in-hello-application-insights-sdk"></a><span data-ttu-id="d971e-103">Filtragem e o pré-processamento telemetria no hello SDK do Application Insights</span><span class="sxs-lookup"><span data-stu-id="d971e-103">Filtering and preprocessing telemetry in hello Application Insights SDK</span></span>


<span data-ttu-id="d971e-104">Você pode gravar e configurar plug-ins para Olá SDK do Application Insights toocustomize como telemetria é capturada e processada antes de serem enviado toohello serviço Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d971e-104">You can write and configure plug-ins for hello Application Insights SDK toocustomize how telemetry is captured and processed before it is sent toohello Application Insights service.</span></span>

* <span data-ttu-id="d971e-105">[Amostragem](app-insights-sampling.md) reduz o volume de saudação de telemetria sem afetar as estatísticas.</span><span class="sxs-lookup"><span data-stu-id="d971e-105">[Sampling](app-insights-sampling.md) reduces hello volume of telemetry without affecting your statistics.</span></span> <span data-ttu-id="d971e-106">Ela mantém juntos os pontos de dados relacionadas para que você possa navegar entre eles para diagnosticar um problema.</span><span class="sxs-lookup"><span data-stu-id="d971e-106">It keeps together related data points so that you can navigate between them when diagnosing a problem.</span></span> <span data-ttu-id="d971e-107">No portal de hello, contagens do total de saudação são multiplicado toocompensate para amostragem de saudação.</span><span class="sxs-lookup"><span data-stu-id="d971e-107">In hello portal, hello total counts are multiplied toocompensate for hello sampling.</span></span>
* <span data-ttu-id="d971e-108">Filtrando com processadores de telemetria [para ASP.NET](#filtering) ou [Java](app-insights-java-filter-telemetry.md) permite selecionar ou modificar telemetria no hello SDK antes de serem enviado toohello server.</span><span class="sxs-lookup"><span data-stu-id="d971e-108">Filtering with Telemetry Processors [for ASP.NET](#filtering) or [Java](app-insights-java-filter-telemetry.md) lets you select or modify telemetry in hello SDK before it is sent toohello server.</span></span> <span data-ttu-id="d971e-109">Por exemplo, você pode reduzir o volume de saudação de telemetria excluindo solicitações de robôs.</span><span class="sxs-lookup"><span data-stu-id="d971e-109">For example, you could reduce hello volume of telemetry by excluding requests from robots.</span></span> <span data-ttu-id="d971e-110">Mas a filtragem é um tráfego de tooreducing abordagem mais simples de amostragem.</span><span class="sxs-lookup"><span data-stu-id="d971e-110">But filtering is a more basic approach tooreducing traffic than sampling.</span></span> <span data-ttu-id="d971e-111">Ele permite a você mais controle sobre o que é transmitido, mas ter toobe ciente de que ele afeta estatísticas - por exemplo, se você filtrar todas as solicitações bem sucedidas.</span><span class="sxs-lookup"><span data-stu-id="d971e-111">It allows you more control over what is transmitted, but you have toobe aware that it affects your statistics - for example, if you filter out all successful requests.</span></span>
* <span data-ttu-id="d971e-112">[Inicializadores de telemetria adicionar propriedades](#add-properties) tooany telemetria enviada do seu aplicativo, incluindo a telemetria dos módulos padrão hello.</span><span class="sxs-lookup"><span data-stu-id="d971e-112">[Telemetry Initializers add properties](#add-properties) tooany telemetry sent from your app, including telemetry from hello standard modules.</span></span> <span data-ttu-id="d971e-113">Por exemplo, você pode adicionar valores calculados; ou os números de versão de dados no portal de Olá Olá toofilter.</span><span class="sxs-lookup"><span data-stu-id="d971e-113">For example, you could add calculated values; or version numbers by which toofilter hello data in hello portal.</span></span>
* <span data-ttu-id="d971e-114">[Olá API do SDK](app-insights-api-custom-events-metrics.md) é métricas e eventos personalizados toosend usado.</span><span class="sxs-lookup"><span data-stu-id="d971e-114">[hello SDK API](app-insights-api-custom-events-metrics.md) is used toosend custom events and metrics.</span></span>

<span data-ttu-id="d971e-115">Antes de começar:</span><span class="sxs-lookup"><span data-stu-id="d971e-115">Before you start:</span></span>

* <span data-ttu-id="d971e-116">Instalar Olá Application Insights [SDK para ASP.NET](app-insights-asp-net.md) ou [SDK para Java](app-insights-java-get-started.md) em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d971e-116">Install hello Application Insights [SDK for ASP.NET](app-insights-asp-net.md) or [SDK for Java](app-insights-java-get-started.md) in your app.</span></span>

<a name="filtering"></a>

## <a name="filtering-itelemetryprocessor"></a><span data-ttu-id="d971e-117">Filtragem: ITelemetryProcessor</span><span class="sxs-lookup"><span data-stu-id="d971e-117">Filtering: ITelemetryProcessor</span></span>
<span data-ttu-id="d971e-118">Essa técnica fornece controle mais direto sobre o que é incluído ou excluído de fluxo de telemetria hello.</span><span class="sxs-lookup"><span data-stu-id="d971e-118">This technique gives you more direct control over what is included or excluded from hello telemetry stream.</span></span> <span data-ttu-id="d971e-119">Você pode usá-la em conjunto com a Amostragem, ou separadamente.</span><span class="sxs-lookup"><span data-stu-id="d971e-119">You can use it in conjunction with Sampling, or separately.</span></span>

<span data-ttu-id="d971e-120">Telemetria de toofilter você gravar um processador de telemetria e registrá-lo com hello SDK.</span><span class="sxs-lookup"><span data-stu-id="d971e-120">toofilter telemetry, you write a telemetry processor and register it with hello SDK.</span></span> <span data-ttu-id="d971e-121">Toda a telemetria atravessa o processador, e você pode escolher toodrop do hello fluxo ou adicionar propriedades.</span><span class="sxs-lookup"><span data-stu-id="d971e-121">All telemetry goes through your processor, and you can choose toodrop it from hello stream, or add properties.</span></span> <span data-ttu-id="d971e-122">Isso inclui a telemetria de módulos de saudação padrão como coletores de solicitação HTTP hello e coletor de dependência Olá, bem como telemetria que foram gravadas por conta própria.</span><span class="sxs-lookup"><span data-stu-id="d971e-122">This includes telemetry from hello standard modules such as hello HTTP request collector and hello dependency collector, as well as telemetry you have written yourself.</span></span> <span data-ttu-id="d971e-123">Por exemplo, você pode filtrar a telemetria sobre solicitações de robôs ou sobre chamadas de dependência bem-sucedidas.</span><span class="sxs-lookup"><span data-stu-id="d971e-123">You can, for example, filter out telemetry about requests from robots, or successful dependency calls.</span></span>

> [!WARNING]
> <span data-ttu-id="d971e-124">Filtragem de telemetria Olá enviada do hello SDK usando processadores pode afetar itens relacionados a estatísticas de saudação que você consulte no portal de saudação e torná-lo toofollow difícil.</span><span class="sxs-lookup"><span data-stu-id="d971e-124">Filtering hello telemetry sent from hello SDK using processors can skew hello statistics that you see in hello portal, and make it difficult toofollow related items.</span></span>
>
> <span data-ttu-id="d971e-125">Em vez disso, considere usar a [amostragem](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="d971e-125">Instead, consider using [sampling](app-insights-sampling.md).</span></span>
>
>

### <a name="create-a-telemetry-processor-c"></a><span data-ttu-id="d971e-126">Criar um processador de telemetria (C#)</span><span class="sxs-lookup"><span data-stu-id="d971e-126">Create a telemetry processor (C#)</span></span>
1. <span data-ttu-id="d971e-127">Verifique se esse SDK do Application Insights Olá em seu projeto está versão 2.0.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="d971e-127">Verify that hello Application Insights SDK in your project is  version 2.0.0 or later.</span></span> <span data-ttu-id="d971e-128">Clique com o botão direito do mouse no projeto no Gerenciador de Soluções do Visual Studio e escolha Gerenciar Pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="d971e-128">Right-click your project in Visual Studio Solution Explorer and choose Manage NuGet Packages.</span></span> <span data-ttu-id="d971e-129">No gerenciador de pacotes NuGet, marque Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="d971e-129">In NuGet package manager, check Microsoft.ApplicationInsights.Web.</span></span>
2. <span data-ttu-id="d971e-130">toocreate um filtro, implementar ITelemetryProcessor.</span><span class="sxs-lookup"><span data-stu-id="d971e-130">toocreate a filter, implement ITelemetryProcessor.</span></span> <span data-ttu-id="d971e-131">Este é outro ponto de extensibilidade como módulo de telemetria, inicializador de telemetria e canal de telemetria.</span><span class="sxs-lookup"><span data-stu-id="d971e-131">This is another extensibility point like telemetry module, telemetry initializer, and telemetry channel.</span></span>

    <span data-ttu-id="d971e-132">Observe que os Processadores de Telemetria criam uma cadeia de processamento.</span><span class="sxs-lookup"><span data-stu-id="d971e-132">Notice that Telemetry Processors construct a chain of processing.</span></span> <span data-ttu-id="d971e-133">Quando você cria uma instância de um processador de telemetria, você passar um processador de Avançar toohello link na cadeia de saudação.</span><span class="sxs-lookup"><span data-stu-id="d971e-133">When you instantiate a telemetry processor, you pass a link toohello next processor in hello chain.</span></span> <span data-ttu-id="d971e-134">Quando um ponto de dados de telemetria é passado método toohello, faz seu trabalho e, em seguida, chama Olá próximo processador telemetria na cadeia de saudação.</span><span class="sxs-lookup"><span data-stu-id="d971e-134">When a telemetry data point is passed toohello Process method, it does its work and then calls hello next Telemetry Processor in hello chain.</span></span>

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
1. <span data-ttu-id="d971e-135">Insira isto no ApplicationInsights.config:</span><span class="sxs-lookup"><span data-stu-id="d971e-135">Insert this in ApplicationInsights.config:</span></span>

```XML

    <TelemetryProcessors>
      <Add Type="WebApplication9.SuccessfulDependencyFilter, WebApplication9">
         <!-- Set public property -->
         <MyParamFromConfigFile>2-beta</MyParamFromConfigFile>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="d971e-136">(Isso é hello mesma seção em que você inicializar um filtro de amostragem.)</span><span class="sxs-lookup"><span data-stu-id="d971e-136">(This is hello same section where you initialize a sampling filter.)</span></span>

<span data-ttu-id="d971e-137">Você pode passar valores de cadeia de caracteres do arquivo. config de saudação fornecendo propriedades nomeadas públicas em sua classe.</span><span class="sxs-lookup"><span data-stu-id="d971e-137">You can pass string values from hello .config file by providing public named properties in your class.</span></span>

> [!WARNING]
> <span data-ttu-id="d971e-138">Lembre-se nome do tipo hello toomatch e nomes de propriedade da classe toohello do hello. config arquivo e nomes de propriedade no código de saudação.</span><span class="sxs-lookup"><span data-stu-id="d971e-138">Take care toomatch hello type name and any property names in hello .config file toohello class and property names in hello code.</span></span> <span data-ttu-id="d971e-139">Se o arquivo. config de saudação faz referência a um tipo de inexistente ou a propriedade, Olá SDK pode falhar em modo silencioso toosend qualquer telemetria.</span><span class="sxs-lookup"><span data-stu-id="d971e-139">If hello .config file references a non-existent type or property, hello SDK may silently fail toosend any telemetry.</span></span>
>
>

<span data-ttu-id="d971e-140">**Como alternativa,** , você pode inicializar filtro Olá no código.</span><span class="sxs-lookup"><span data-stu-id="d971e-140">**Alternatively,** you can initialize hello filter in code.</span></span> <span data-ttu-id="d971e-141">Em uma classe de inicialização adequado - por exemplo AppStart em Global.asax.cs - inserir o processador cadeia hello:</span><span class="sxs-lookup"><span data-stu-id="d971e-141">In a suitable initialization class - for example AppStart in Global.asax.cs - insert your processor into hello chain:</span></span>

```C#

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;
    builder.Use((next) => new SuccessfulDependencyFilter(next));

    // If you have more processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="d971e-142">Os TelemetryClients criados depois desse ponto usarão seus processadores.</span><span class="sxs-lookup"><span data-stu-id="d971e-142">TelemetryClients created after this point will use your processors.</span></span>

### <a name="example-filters"></a><span data-ttu-id="d971e-143">Filtros de exemplo</span><span class="sxs-lookup"><span data-stu-id="d971e-143">Example filters</span></span>
#### <a name="synthetic-requests"></a><span data-ttu-id="d971e-144">Solicitações sintéticas</span><span class="sxs-lookup"><span data-stu-id="d971e-144">Synthetic requests</span></span>
<span data-ttu-id="d971e-145">Filtre os bots e os testes Web.</span><span class="sxs-lookup"><span data-stu-id="d971e-145">Filter out bots and web tests.</span></span> <span data-ttu-id="d971e-146">Embora Metrics Explorer oferece Olá toofilter opção out sintéticos fontes, essa opção reduz o tráfego filtrá-los em Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="d971e-146">Although Metrics Explorer gives you hello option toofilter out synthetic sources, this option reduces traffic by filtering them at hello SDK.</span></span>

``` C#

    public void Process(ITelemetry item)
    {
      if (!string.IsNullOrEmpty(item.Context.Operation.SyntheticSource)) {return;}

      // Send everything else:
      this.Next.Process(item);
    }

```

#### <a name="failed-authentication"></a><span data-ttu-id="d971e-147">Autenticação com falha</span><span class="sxs-lookup"><span data-stu-id="d971e-147">Failed authentication</span></span>
<span data-ttu-id="d971e-148">Filtre as solicitações com uma resposta "401".</span><span class="sxs-lookup"><span data-stu-id="d971e-148">Filter out requests with a "401" response.</span></span>

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

#### <a name="filter-out-fast-remote-dependency-calls"></a><span data-ttu-id="d971e-149">Filtrar chamadas de dependência rápidas remotas</span><span class="sxs-lookup"><span data-stu-id="d971e-149">Filter out fast remote dependency calls</span></span>
<span data-ttu-id="d971e-150">Se você quiser apenas chamadas de toodiagnose estão lentas, filtre Olá fast os.</span><span class="sxs-lookup"><span data-stu-id="d971e-150">If you only want toodiagnose calls that are slow, filter out hello fast ones.</span></span>

> [!NOTE]
> <span data-ttu-id="d971e-151">Isso irá distorcer estatísticas Olá mostrados no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="d971e-151">This will skew hello statistics you see on hello portal.</span></span> <span data-ttu-id="d971e-152">gráfico de dependência de saudação aparecerá como se chamadas de dependência de saudação são todas as falhas.</span><span class="sxs-lookup"><span data-stu-id="d971e-152">hello dependency chart will look as if hello dependency calls are all failures.</span></span>
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

#### <a name="diagnose-dependency-issues"></a><span data-ttu-id="d971e-153">Diagnosticar problemas de dependência</span><span class="sxs-lookup"><span data-stu-id="d971e-153">Diagnose dependency issues</span></span>
<span data-ttu-id="d971e-154">[Este blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) descreve um problema de dependência do projeto toodiagnose enviando automaticamente toodependencies pings regular.</span><span class="sxs-lookup"><span data-stu-id="d971e-154">[This blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) describes a project toodiagnose dependency issues by automatically sending regular pings toodependencies.</span></span>


<a name="add-properties"></a>

## <a name="add-properties-itelemetryinitializer"></a><span data-ttu-id="d971e-155">Adicionar propriedades: ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="d971e-155">Add properties: ITelemetryInitializer</span></span>
<span data-ttu-id="d971e-156">Uso da telemetria inicializadores toodefine propriedades globais que são enviadas com toda a Telemetria; e o comportamento de toooverride selecionado dos módulos de telemetria padrão hello.</span><span class="sxs-lookup"><span data-stu-id="d971e-156">Use telemetry initializers toodefine global properties that are sent with all telemetry; and toooverride selected behavior of hello standard telemetry modules.</span></span>

<span data-ttu-id="d971e-157">Por exemplo, hello Application Insights para o pacote da Web coleta a telemetria sobre solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="d971e-157">For example, hello Application Insights for Web package collects telemetry about HTTP requests.</span></span> <span data-ttu-id="d971e-158">Por padrão, ele sinaliza como qualquer solicitação com um código de resposta de falha > = 400.</span><span class="sxs-lookup"><span data-stu-id="d971e-158">By default, it flags as failed any request with a response code >= 400.</span></span> <span data-ttu-id="d971e-159">Mas se você quiser tootreat 400 como um êxito, você pode fornecer um inicializador de telemetria que define a propriedade de êxito de saudação.</span><span class="sxs-lookup"><span data-stu-id="d971e-159">But if you want tootreat 400 as a success, you can provide a telemetry initializer that sets hello Success property.</span></span>

<span data-ttu-id="d971e-160">Se você fornecer um inicializador de telemetria, ele é chamado sempre que qualquer um dos Olá Track*() métodos é chamado.</span><span class="sxs-lookup"><span data-stu-id="d971e-160">If you provide a telemetry initializer, it is called whenever any of hello Track*() methods is called.</span></span> <span data-ttu-id="d971e-161">Isso inclui métodos chamados pelos módulos de telemetria padrão hello.</span><span class="sxs-lookup"><span data-stu-id="d971e-161">This includes methods called by hello standard telemetry modules.</span></span> <span data-ttu-id="d971e-162">Por convenção, esses módulos não definem qualquer propriedade que já foi definida por um inicializador.</span><span class="sxs-lookup"><span data-stu-id="d971e-162">By convention, these modules do not set any property that has already been set by an initializer.</span></span>

<span data-ttu-id="d971e-163">**Definir seu inicializador**</span><span class="sxs-lookup"><span data-stu-id="d971e-163">**Define your initializer**</span></span>

<span data-ttu-id="d971e-164">*C#*</span><span class="sxs-lookup"><span data-stu-id="d971e-164">*C#*</span></span>

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

<span data-ttu-id="d971e-165">**Carregue seu inicializador**</span><span class="sxs-lookup"><span data-stu-id="d971e-165">**Load your initializer**</span></span>

<span data-ttu-id="d971e-166">Em ApplicationInsights.config:</span><span class="sxs-lookup"><span data-stu-id="d971e-166">In ApplicationInsights.config:</span></span>

    <ApplicationInsights>
      <TelemetryInitializers>
        <!-- Fully qualified type name, assembly name: -->
        <Add Type="MvcWebRole.Telemetry.MyTelemetryInitializer, MvcWebRole"/>
        ...
      </TelemetryInitializers>
    </ApplicationInsights>

<span data-ttu-id="d971e-167">*Como alternativa,* você pode instanciar inicializador Olá no código, por exemplo, em Global.aspx.cs:</span><span class="sxs-lookup"><span data-stu-id="d971e-167">*Alternatively,* you can instantiate hello initializer in code, for example in Global.aspx.cs:</span></span>

```C#
    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```


[<span data-ttu-id="d971e-168">Ver mais deste exemplo.</span><span class="sxs-lookup"><span data-stu-id="d971e-168">See more of this sample.</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole)

<a name="js-initializer"></a>

### <a name="javascript-telemetry-initializers"></a><span data-ttu-id="d971e-169">Inicializadores de telemetria JavaScript</span><span class="sxs-lookup"><span data-stu-id="d971e-169">JavaScript telemetry initializers</span></span>
<span data-ttu-id="d971e-170">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="d971e-170">*JavaScript*</span></span>

<span data-ttu-id="d971e-171">Insira um inicializador de telemetria imediatamente após o código de inicialização de saudação que você obteve no portal de saudação:</span><span class="sxs-lookup"><span data-stu-id="d971e-171">Insert a telemetry initializer immediately after hello initialization code that you got from hello portal:</span></span>

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

<span data-ttu-id="d971e-172">Para obter um resumo das propriedades de não personalizado Olá disponíveis em telemetryItem hello, consulte [aplicativo Insights exportar dados de modelo](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="d971e-172">For a summary of hello non-custom properties available on hello telemetryItem, see [Application Insights Export Data Model](app-insights-export-data-model.md).</span></span>

<span data-ttu-id="d971e-173">Você pode adicionar quantos inicializadores desejar.</span><span class="sxs-lookup"><span data-stu-id="d971e-173">You can add as many initializers as you like.</span></span>

## <a name="itelemetryprocessor-and-itelemetryinitializer"></a><span data-ttu-id="d971e-174">ITelemetryProcessor e ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="d971e-174">ITelemetryProcessor and ITelemetryInitializer</span></span>
<span data-ttu-id="d971e-175">Qual é a diferença de saudação entre os processadores de telemetria e inicializadores de telemetria?</span><span class="sxs-lookup"><span data-stu-id="d971e-175">What's hello difference between telemetry processors and telemetry initializers?</span></span>

* <span data-ttu-id="d971e-176">Há algumas sobreposições em que você pode fazer com eles: ambos podem ser usados tooadd propriedades tootelemetry.</span><span class="sxs-lookup"><span data-stu-id="d971e-176">There are some overlaps in what you can do with them: both can be used tooadd properties tootelemetry.</span></span>
* <span data-ttu-id="d971e-177">Sempre execute TelemetryInitializers antes de TelemetryProcessors.</span><span class="sxs-lookup"><span data-stu-id="d971e-177">TelemetryInitializers always run before TelemetryProcessors.</span></span>
* <span data-ttu-id="d971e-178">TelemetryProcessors permitem que você substitua toocompletely ou descartar um item de telemetria.</span><span class="sxs-lookup"><span data-stu-id="d971e-178">TelemetryProcessors allow you toocompletely replace or discard a telemetry item.</span></span>
* <span data-ttu-id="d971e-179">TelemetryProcessors não processam telemetria do contador de desempenho.</span><span class="sxs-lookup"><span data-stu-id="d971e-179">TelemetryProcessors don't process performance counter telemetry.</span></span>


## <a name="reference-docs"></a><span data-ttu-id="d971e-180">Documentos de Referência</span><span class="sxs-lookup"><span data-stu-id="d971e-180">Reference docs</span></span>
* [<span data-ttu-id="d971e-181">Visão geral da API</span><span class="sxs-lookup"><span data-stu-id="d971e-181">API Overview</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="d971e-182">Referência do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d971e-182">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)

## <a name="sdk-code"></a><span data-ttu-id="d971e-183">Código do SDK</span><span class="sxs-lookup"><span data-stu-id="d971e-183">SDK Code</span></span>
* [<span data-ttu-id="d971e-184">SDK de Núcleo do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d971e-184">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="d971e-185">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="d971e-185">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="d971e-186">SDK do JavaScript</span><span class="sxs-lookup"><span data-stu-id="d971e-186">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)

## <span data-ttu-id="d971e-187"><a name="next"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d971e-187"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="d971e-188">Pesquisar eventos e logs</span><span class="sxs-lookup"><span data-stu-id="d971e-188">Search events and logs</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="d971e-189">Amostragem</span><span class="sxs-lookup"><span data-stu-id="d971e-189">Sampling</span></span>](app-insights-sampling.md)
* [<span data-ttu-id="d971e-190">Solução de problemas</span><span class="sxs-lookup"><span data-stu-id="d971e-190">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
