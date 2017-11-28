---
title: "referência de aaaApplicationInsights.config - Azure | Microsoft Docs"
description: "Habilitar ou desabilitar módulos de coleta de dados e adicionar contadores de desempenho e outros parâmetros."
services: application-insights
documentationcenter: 
author: OlegAnaniev-MSFT
editor: alancameronwills
manager: carmonm
ms.assetid: 6e397752-c086-46e9-8648-a1196e8078c2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 76cb11349d87dfc508ec8b1c454259a0b079c48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-hello-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a><span data-ttu-id="cc686-103">Configurar Olá SDK do Application Insights com applicationinsights. config ou. XML</span><span class="sxs-lookup"><span data-stu-id="cc686-103">Configuring hello Application Insights SDK with ApplicationInsights.config or .xml</span></span>
<span data-ttu-id="cc686-104">Olá SDK .NET do Application Insights consiste em um número de pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="cc686-104">hello Application Insights .NET SDK consists of a number of NuGet packages.</span></span> <span data-ttu-id="cc686-105">O [pacote core](http://www.nuget.org/packages/Microsoft.ApplicationInsights) fornece a API de hello para enviar telemetria à saudação do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="cc686-105">The [core package](http://www.nuget.org/packages/Microsoft.ApplicationInsights) provides hello API for sending telemetry to hello Application Insights.</span></span> <span data-ttu-id="cc686-106">Os [pacotes adicionais](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) fornecem *módulos* e *inicializadores* de telemetria para rastreamento automático de telemetria do seu aplicativo e respectivo contexto.</span><span class="sxs-lookup"><span data-stu-id="cc686-106">[Additional packages](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) provide telemetry *modules* and *initializers* for automatically tracking telemetry from your application and its context.</span></span> <span data-ttu-id="cc686-107">Ajustando o arquivo de configuração hello, habilitar ou desabilitar inicializadores e módulos de telemetria e definir parâmetros para algumas delas.</span><span class="sxs-lookup"><span data-stu-id="cc686-107">By adjusting hello configuration file, you can enable or disable telemetry modules and initializers, and set parameters for some of them.</span></span>

<span data-ttu-id="cc686-108">arquivo de configuração de saudação é nomeado `ApplicationInsights.config` ou `ApplicationInsights.xml`, dependendo do tipo de saudação do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cc686-108">hello configuration file is named `ApplicationInsights.config` or `ApplicationInsights.xml`, depending on hello type of your application.</span></span> <span data-ttu-id="cc686-109">Ele é adicionado automaticamente tooyour projeto quando você [instalar a maioria das versões do SDK do hello][start].</span><span class="sxs-lookup"><span data-stu-id="cc686-109">It is automatically added tooyour project when you [install most versions of hello SDK][start].</span></span> <span data-ttu-id="cc686-110">Ele também é adicionado tooa web aplicativo por [Monitor de Status em um servidor IIS][redfield], ou quando você seleciona Olá aplicativo Insights [extensão para um site do Azure ou VM](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="cc686-110">It is also added tooa web app by [Status Monitor on an IIS server][redfield], or when you select hello Appplication Insights [extension for an Azure website or VM](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="cc686-111">Não há uma saudação de toocontrol arquivo equivalente [SDK em uma página da web][client].</span><span class="sxs-lookup"><span data-stu-id="cc686-111">There isn't an equivalent file toocontrol hello [SDK in a web page][client].</span></span>

<span data-ttu-id="cc686-112">Este documento descreve as seções de saudação que você vê na configuração de saudação do arquivo, como controlar os componentes de saudação do hello SDK, e os pacotes do NuGet carregar esses componentes.</span><span class="sxs-lookup"><span data-stu-id="cc686-112">This document describes hello sections you see in hello configuration file, how they control hello components of hello SDK, and which NuGet packages load those components.</span></span>

## <a name="telemetry-modules-aspnet"></a><span data-ttu-id="cc686-113">Módulos de telemetria (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="cc686-113">Telemetry Modules (ASP.NET)</span></span>
<span data-ttu-id="cc686-114">Cada módulo de telemetria coleta um tipo específico de dados e usa o núcleo de saudação dados de saudação toosend API.</span><span class="sxs-lookup"><span data-stu-id="cc686-114">Each telemetry module collects a specific type of data and uses hello core API toosend hello data.</span></span> <span data-ttu-id="cc686-115">módulos de saudação são instalados por diferentes pacotes do NuGet, que também adicionar o arquivo. config do hello linhas necessárias toohello.</span><span class="sxs-lookup"><span data-stu-id="cc686-115">hello modules are installed by different NuGet packages, which also add hello required lines toohello .config file.</span></span>

<span data-ttu-id="cc686-116">Há um nó no arquivo de configuração de saudação para cada módulo.</span><span class="sxs-lookup"><span data-stu-id="cc686-116">There's a node in hello configuration file for each module.</span></span> <span data-ttu-id="cc686-117">toodisable um módulo, exclua o nó hello ou comente-o.</span><span class="sxs-lookup"><span data-stu-id="cc686-117">toodisable a module, delete hello node or comment it out.</span></span>

### <a name="dependency-tracking"></a><span data-ttu-id="cc686-118">Acompanhamento de dependência</span><span class="sxs-lookup"><span data-stu-id="cc686-118">Dependency Tracking</span></span>
<span data-ttu-id="cc686-119">[Controle de dependência](app-insights-asp-net-dependencies.md) coleta a telemetria sobre chamadas de seu aplicativo torna toodatabases e bancos de dados e serviços externos.</span><span class="sxs-lookup"><span data-stu-id="cc686-119">[Dependency tracking](app-insights-asp-net-dependencies.md) collects telemetry about calls your app makes toodatabases and external services and databases.</span></span> <span data-ttu-id="cc686-120">tooallow toowork esse módulo em um servidor IIS, é necessário muito[instalar o Monitor de Status][redfield].</span><span class="sxs-lookup"><span data-stu-id="cc686-120">tooallow this module toowork in an IIS server, you need too[install Status Monitor][redfield].</span></span> <span data-ttu-id="cc686-121">toouse-la em aplicativos web do Azure ou máquinas virtuais, [Selecionar extensão do Application Insights Olá](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="cc686-121">toouse it in Azure web apps or VMs, [select hello Application Insights extension](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="cc686-122">Você também pode escrever seu próprio controle de código usando a saudação de dependência [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="cc686-122">You can also write your own dependency tracking code using hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* <span data-ttu-id="cc686-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) .</span><span class="sxs-lookup"><span data-stu-id="cc686-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet package.</span></span>

### <a name="performance-collector"></a><span data-ttu-id="cc686-124">Coletor de desempenho</span><span class="sxs-lookup"><span data-stu-id="cc686-124">Performance collector</span></span>
<span data-ttu-id="cc686-125">[Coleta contadores de desempenho do sistema](app-insights-performance-counters.md), como CPU, memória e carga de rede de instalações do IIS.</span><span class="sxs-lookup"><span data-stu-id="cc686-125">[Collects system performance counters](app-insights-performance-counters.md) such as CPU, memory and network load from IIS installations.</span></span> <span data-ttu-id="cc686-126">Você pode especificar quais toocollect contadores, incluindo contadores de desempenho que você configurou por conta própria.</span><span class="sxs-lookup"><span data-stu-id="cc686-126">You can specify which counters toocollect, including performance counters you have set up yourself.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* <span data-ttu-id="cc686-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) .</span><span class="sxs-lookup"><span data-stu-id="cc686-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet package.</span></span>

### <a name="application-insights-diagnostics-telemetry"></a><span data-ttu-id="cc686-128">Telemetria de diagnóstico do Application Insights</span><span class="sxs-lookup"><span data-stu-id="cc686-128">Application Insights Diagnostics Telemetry</span></span>
<span data-ttu-id="cc686-129">Olá `DiagnosticsTelemetryModule` relata erros em Olá próprio código de instrumentação do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="cc686-129">hello `DiagnosticsTelemetryModule` reports errors in hello Application Insights instrumentation code itself.</span></span> <span data-ttu-id="cc686-130">Por exemplo, se o código de saudação não pode acessar os contadores de desempenho ou se um `ITelemetryInitializer` lança uma exceção.</span><span class="sxs-lookup"><span data-stu-id="cc686-130">For example, if hello code cannot access performance counters or if an `ITelemetryInitializer` throws an exception.</span></span> <span data-ttu-id="cc686-131">Telemetria de rastreamento controlada por esse módulo aparece no hello [pesquisa diagnóstico][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="cc686-131">Trace telemetry tracked by this module appears in hello [Diagnostic Search][diagnostic].</span></span> <span data-ttu-id="cc686-132">Envia dados de diagnóstico toodc.services.vsallin.net.</span><span class="sxs-lookup"><span data-stu-id="cc686-132">Sends diagnostic data toodc.services.vsallin.net.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* <span data-ttu-id="cc686-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) .</span><span class="sxs-lookup"><span data-stu-id="cc686-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="cc686-134">Se você só pode instalar esse pacote, arquivo applicationinsights. config de saudação não será criado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="cc686-134">If you only install this package, hello ApplicationInsights.config file is not automatically created.</span></span>

### <a name="developer-mode"></a><span data-ttu-id="cc686-135">Modo de desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="cc686-135">Developer Mode</span></span>
<span data-ttu-id="cc686-136">`DeveloperModeWithDebuggerAttachedTelemetryModule`força Olá Application Insights `TelemetryChannel` toosend dados imediatamente, item de um telemetria por vez, quando um depurador é anexado toohello o processo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cc686-136">`DeveloperModeWithDebuggerAttachedTelemetryModule` forces hello Application Insights `TelemetryChannel` toosend data immediately, one telemetry item at a time, when a debugger is attached toohello application process.</span></span> <span data-ttu-id="cc686-137">Isso reduz a quantidade de saudação de tempo entre o momento de saudação quando seu aplicativo controla a telemetria e quando ele aparece no portal do Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="cc686-137">This reduces hello amount of time between hello moment when your application tracks telemetry and when it appears on hello Application Insights portal.</span></span> <span data-ttu-id="cc686-138">Faz com uma sobrecarga significativa na largura de banda de CPU e rede.</span><span class="sxs-lookup"><span data-stu-id="cc686-138">It causes significant overhead in CPU and network bandwidth.</span></span>

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* <span data-ttu-id="cc686-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) .</span><span class="sxs-lookup"><span data-stu-id="cc686-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package</span></span>

### <a name="web-request-tracking"></a><span data-ttu-id="cc686-140">Acompanhamento de solicitação da Web</span><span class="sxs-lookup"><span data-stu-id="cc686-140">Web Request Tracking</span></span>
<span data-ttu-id="cc686-141">Olá relatórios [código de tempo e o resultado da resposta](app-insights-asp-net.md) de solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="cc686-141">Reports hello [response time and result code](app-insights-asp-net.md) of HTTP requests.</span></span>

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* <span data-ttu-id="cc686-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) .</span><span class="sxs-lookup"><span data-stu-id="cc686-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>

### <a name="exception-tracking"></a><span data-ttu-id="cc686-143">Acompanhamento de exceções</span><span class="sxs-lookup"><span data-stu-id="cc686-143">Exception tracking</span></span>
<span data-ttu-id="cc686-144">`ExceptionTrackingTelemetryModule` rastreia exceção sem tratamento no seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="cc686-144">`ExceptionTrackingTelemetryModule` tracks unhandled exceptions in your web app.</span></span> <span data-ttu-id="cc686-145">Consulte [Falhas e exceções][exceptions].</span><span class="sxs-lookup"><span data-stu-id="cc686-145">See [Failures and exceptions][exceptions].</span></span>

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* <span data-ttu-id="cc686-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) .</span><span class="sxs-lookup"><span data-stu-id="cc686-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>
* <span data-ttu-id="cc686-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` -rastreia [exceções de tarefa não observada](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span><span class="sxs-lookup"><span data-stu-id="cc686-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - tracks [unobserved task exceptions](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span></span>
* <span data-ttu-id="cc686-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` -rastreia as exceções sem tratamento para funções de trabalho, serviços do Windows e aplicativos de console.</span><span class="sxs-lookup"><span data-stu-id="cc686-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - tracks unhandled exceptions for worker roles, windows services, and console applications.</span></span>
* <span data-ttu-id="cc686-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) .</span><span class="sxs-lookup"><span data-stu-id="cc686-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package.</span></span>

### <a name="eventsource-tracking"></a><span data-ttu-id="cc686-150">Monitoramento de EventSource</span><span class="sxs-lookup"><span data-stu-id="cc686-150">EventSource Tracking</span></span>
<span data-ttu-id="cc686-151">`EventSourceTelemetryModule`permite que você tooconfigure EventSource eventos toobe enviado tooApplication Insights como rastreamentos.</span><span class="sxs-lookup"><span data-stu-id="cc686-151">`EventSourceTelemetryModule` allows you tooconfigure EventSource events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="cc686-152">Para obter informações sobre o monitoramento de eventos EventSource, consulte [Usando eventos EventSource](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span><span class="sxs-lookup"><span data-stu-id="cc686-152">For information on tracking EventSource events, see [Using EventSource Events](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span></span>

* `Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule`
* [<span data-ttu-id="cc686-153">Microsoft.ApplicationInsights.EventSourceListener</span><span class="sxs-lookup"><span data-stu-id="cc686-153">Microsoft.ApplicationInsights.EventSourceListener</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EventSourceListener) 

### <a name="etw-event-tracking"></a><span data-ttu-id="cc686-154">Monitoramento de eventos ETW</span><span class="sxs-lookup"><span data-stu-id="cc686-154">ETW Event Tracking</span></span>
<span data-ttu-id="cc686-155">`EtwCollectorTelemetryModule`permite que você tooconfigure eventos do ETW provedores toobe enviados tooApplication Insights como rastreamentos.</span><span class="sxs-lookup"><span data-stu-id="cc686-155">`EtwCollectorTelemetryModule` allows you tooconfigure events from ETW providers toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="cc686-156">Para obter informações sobre o monitoramento de eventos ETW, consulte [Usando eventos ETW](app-insights-asp-net-trace-logs.md#using-etw-events).</span><span class="sxs-lookup"><span data-stu-id="cc686-156">For information on tracking ETW events, see [Using ETW Events](app-insights-asp-net-trace-logs.md#using-etw-events).</span></span>

* `Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule`
* [<span data-ttu-id="cc686-157">Microsoft.ApplicationInsights.EtwCollector</span><span class="sxs-lookup"><span data-stu-id="cc686-157">Microsoft.ApplicationInsights.EtwCollector</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EtwCollector) 

### <a name="microsoftapplicationinsights"></a><span data-ttu-id="cc686-158">Microsoft.ApplicationInsights</span><span class="sxs-lookup"><span data-stu-id="cc686-158">Microsoft.ApplicationInsights</span></span>
<span data-ttu-id="cc686-159">pacote de Microsoft.ApplicationInsights Olá fornece Olá [core API](https://msdn.microsoft.com/library/mt420197.aspx) de saudação SDK.</span><span class="sxs-lookup"><span data-stu-id="cc686-159">hello Microsoft.ApplicationInsights package provides hello [core API](https://msdn.microsoft.com/library/mt420197.aspx) of hello SDK.</span></span> <span data-ttu-id="cc686-160">Olá outros módulos de telemetria usam isso, e você também pode [usá-lo toodefine sua telemetria](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="cc686-160">hello other telemetry modules use this, and you can also [use it toodefine your own telemetry](app-insights-api-custom-events-metrics.md).</span></span>

* <span data-ttu-id="cc686-161">Nenhuma entrada em ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="cc686-161">No entry in ApplicationInsights.config.</span></span>
* <span data-ttu-id="cc686-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) .</span><span class="sxs-lookup"><span data-stu-id="cc686-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="cc686-163">Se você acabou de instalar este NuGet, nenhum arquivo. config será gerado.</span><span class="sxs-lookup"><span data-stu-id="cc686-163">If you just install this NuGet, no .config file is generated.</span></span>

## <a name="telemetry-channel"></a><span data-ttu-id="cc686-164">Canal de telemetria</span><span class="sxs-lookup"><span data-stu-id="cc686-164">Telemetry Channel</span></span>
<span data-ttu-id="cc686-165">canal de telemetria Olá gerencia o buffer e transmissão de telemetria toohello serviço Application Insights.</span><span class="sxs-lookup"><span data-stu-id="cc686-165">hello telemetry channel manages buffering and transmission of telemetry toohello Application Insights service.</span></span>

* <span data-ttu-id="cc686-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel`é o canal de padrão de saudação para serviços.</span><span class="sxs-lookup"><span data-stu-id="cc686-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel` is hello default channel for services.</span></span> <span data-ttu-id="cc686-167">Ele armazena em buffer dados na memória.</span><span class="sxs-lookup"><span data-stu-id="cc686-167">It buffers data in memory.</span></span>
* <span data-ttu-id="cc686-168">`Microsoft.ApplicationInsights.PersistenceChannel` é uma alternativa para aplicativos de console.</span><span class="sxs-lookup"><span data-stu-id="cc686-168">`Microsoft.ApplicationInsights.PersistenceChannel` is an alternative for console applications.</span></span> <span data-ttu-id="cc686-169">Ele pode salvar qualquer armazenamento de dados unflushed toopersistent quando seu aplicativo encerra e será enviado quando o aplicativo hello começa novamente.</span><span class="sxs-lookup"><span data-stu-id="cc686-169">It can save any unflushed data toopersistent storage when your app closes down, and will send it when hello app starts again.</span></span>

## <a name="telemetry-initializers-aspnet"></a><span data-ttu-id="cc686-170">Inicializadores de telemetria (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="cc686-170">Telemetry Initializers (ASP.NET)</span></span>
<span data-ttu-id="cc686-171">Os inicializadores de telemetria definem propriedades de contexto que são enviadas com cada item de telemetria.</span><span class="sxs-lookup"><span data-stu-id="cc686-171">Telemetry initializers set context properties that are sent along with every item of telemetry.</span></span>

<span data-ttu-id="cc686-172">Você pode [gravar seus próprio inicializadores](app-insights-api-filtering-sampling.md#add-properties) tooset propriedades de contexto.</span><span class="sxs-lookup"><span data-stu-id="cc686-172">You can [write your own initializers](app-insights-api-filtering-sampling.md#add-properties) tooset context properties.</span></span>

<span data-ttu-id="cc686-173">inicializadores padrão Olá estão definidos por pacotes de Web ou WindowsServer NuGet hello:</span><span class="sxs-lookup"><span data-stu-id="cc686-173">hello standard initializers are all set either by hello Web or WindowsServer NuGet packages:</span></span>

* <span data-ttu-id="cc686-174">`AccountIdTelemetryInitializer`Define a propriedade AccountId hello.</span><span class="sxs-lookup"><span data-stu-id="cc686-174">`AccountIdTelemetryInitializer` sets hello AccountId property.</span></span>
* <span data-ttu-id="cc686-175">`AuthenticatedUserIdTelemetryInitializer`Define propriedades de AuthenticatedUserId hello como conjunto de por Olá SDK de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="cc686-175">`AuthenticatedUserIdTelemetryInitializer` sets hello AuthenticatedUserId property as set by hello JavaScript SDK.</span></span>
* <span data-ttu-id="cc686-176">`AzureRoleEnvironmentTelemetryInitializer`saudação de atualizações `RoleName` e `RoleInstance` propriedades de saudação `Device` contexto para todos os itens de telemetria com informações extraídas do ambiente de tempo de execução do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="cc686-176">`AzureRoleEnvironmentTelemetryInitializer` updates hello `RoleName` and `RoleInstance` properties of hello `Device` context for all telemetry items with information extracted from hello Azure runtime environment.</span></span>
* <span data-ttu-id="cc686-177">`BuildInfoConfigComponentVersionTelemetryInitializer`saudação de atualizações `Version` propriedade Olá `Component` contexto para todos os itens de telemetria com valor de saudação extraídos da saudação `BuildInfo.config` arquivo produzido pelo MS Build.</span><span class="sxs-lookup"><span data-stu-id="cc686-177">`BuildInfoConfigComponentVersionTelemetryInitializer` updates hello `Version` property of hello `Component` context for all telemetry items with hello value extracted from hello `BuildInfo.config` file produced by MS Build.</span></span>
* <span data-ttu-id="cc686-178">`ClientIpHeaderTelemetryInitializer`atualizações `Ip` propriedade Olá `Location` contexto de todos os itens de telemetria com base em Olá `X-Forwarded-For` cabeçalho HTTP de solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="cc686-178">`ClientIpHeaderTelemetryInitializer` updates `Ip` property of hello `Location` context of all telemetry items based on hello `X-Forwarded-For` HTTP header of hello request.</span></span>
* <span data-ttu-id="cc686-179">`DeviceTelemetryInitializer`Olá atualizações seguintes propriedades de saudação `Device` contexto para todos os itens de telemetria.</span><span class="sxs-lookup"><span data-stu-id="cc686-179">`DeviceTelemetryInitializer` updates hello following properties of hello `Device` context for all telemetry items.</span></span>
  * <span data-ttu-id="cc686-180">`Type`está definido muito "Computador"</span><span class="sxs-lookup"><span data-stu-id="cc686-180">`Type` is set too"PC"</span></span>
  * <span data-ttu-id="cc686-181">`Id`é definido toohello nome de domínio Olá computador onde o aplicativo da web hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="cc686-181">`Id` is set toohello domain name of hello computer where hello web application is running.</span></span>
  * <span data-ttu-id="cc686-182">`OemName`é definir o valor de toohello extraído da saudação `Win32_ComputerSystem.Manufacturer` campo usando o WMI.</span><span class="sxs-lookup"><span data-stu-id="cc686-182">`OemName` is set toohello value extracted from hello `Win32_ComputerSystem.Manufacturer` field using WMI.</span></span>
  * <span data-ttu-id="cc686-183">`Model`é definir o valor de toohello extraído da saudação `Win32_ComputerSystem.Model` campo usando o WMI.</span><span class="sxs-lookup"><span data-stu-id="cc686-183">`Model` is set toohello value extracted from hello `Win32_ComputerSystem.Model` field using WMI.</span></span>
  * <span data-ttu-id="cc686-184">`NetworkType`é definir o valor de toohello extraído da saudação `NetworkInterface`.</span><span class="sxs-lookup"><span data-stu-id="cc686-184">`NetworkType` is set toohello value extracted from hello `NetworkInterface`.</span></span>
  * <span data-ttu-id="cc686-185">`Language`é definir o nome toohello Olá `CurrentCulture`.</span><span class="sxs-lookup"><span data-stu-id="cc686-185">`Language` is set toohello name of hello `CurrentCulture`.</span></span>
* <span data-ttu-id="cc686-186">`DomainNameRoleInstanceTelemetryInitializer`saudação de atualizações `RoleInstance` propriedade Olá `Device` contexto para todos os itens de telemetria com nome de domínio de saudação do computador Olá onde o aplicativo da web hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="cc686-186">`DomainNameRoleInstanceTelemetryInitializer` updates hello `RoleInstance` property of hello `Device` context for all telemetry items with hello domain name of hello computer where hello web application is running.</span></span>
* <span data-ttu-id="cc686-187">`OperationNameTelemetryInitializer`saudação de atualizações `Name` propriedade Olá `RequestTelemetry` e hello `Name` propriedade Olá `Operation` contexto de todos os itens de telemetria com base no método hello HTTP, bem como nomes de saudação do ASP.NET MVC controlador e ação tooprocess invocado solicitação.</span><span class="sxs-lookup"><span data-stu-id="cc686-187">`OperationNameTelemetryInitializer` updates hello `Name` property of hello `RequestTelemetry` and hello `Name` property of hello `Operation` context of all telemetry items based on hello HTTP method, as well as names of ASP.NET MVC controller and action invoked tooprocess hello request.</span></span>
* <span data-ttu-id="cc686-188">`OperationIdTelemetryInitializer`ou `OperationCorrelationTelemetryInitializer` Olá atualizações `Operation.Id` propriedade de contexto de todos os itens de telemetria controlada ao tratar uma solicitação com hello gerado automaticamente `RequestTelemetry.Id`.</span><span class="sxs-lookup"><span data-stu-id="cc686-188">`OperationIdTelemetryInitializer` or `OperationCorrelationTelemetryInitializer` updates hello `Operation.Id` context property of all telemetry items tracked while handling a request with hello automatically generated `RequestTelemetry.Id`.</span></span>
* <span data-ttu-id="cc686-189">`SessionTelemetryInitializer`saudação de atualizações `Id` propriedade Olá `Session` contexto para todos os itens de telemetria com valor extraído da saudação `ai_session` cookie gerado o código de instrumentação ApplicationInsights JavaScript em execução no navegador do usuário Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="cc686-189">`SessionTelemetryInitializer` updates hello `Id` property of hello `Session` context for all telemetry items with value extracted from hello `ai_session` cookie generated by hello ApplicationInsights JavaScript instrumentation code running in hello user's browser.</span></span>
* <span data-ttu-id="cc686-190">`SyntheticTelemetryInitializer`ou `SyntheticUserAgentTelemetryInitializer` Olá atualizações `User`, `Session` e `Operation` propriedades de contextos de todos os itens de telemetria rastreadas ao lidar com uma solicitação de uma fonte sintética, como uma disponibilidade de teste ou o bot do mecanismo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="cc686-190">`SyntheticTelemetryInitializer` or `SyntheticUserAgentTelemetryInitializer` updates hello `User`, `Session` and `Operation` contexts properties of all telemetry items tracked when handling a request from a synthetic source, such as an availability test or search engine bot.</span></span> <span data-ttu-id="cc686-191">Por padrão, o [Metrics Explorer](app-insights-metrics-explorer.md) não exibe telemetria sintética.</span><span class="sxs-lookup"><span data-stu-id="cc686-191">By default, [Metrics Explorer](app-insights-metrics-explorer.md) does not display synthetic telemetry.</span></span>

    <span data-ttu-id="cc686-192">Olá `<Filters>` definir identificando as propriedades das solicitações de saudação.</span><span class="sxs-lookup"><span data-stu-id="cc686-192">hello `<Filters>` set identifying properties of hello requests.</span></span>
* <span data-ttu-id="cc686-193">`UserAgentTelemetryInitializer`saudação de atualizações `UserAgent` propriedade Olá `User` contexto de todos os itens de telemetria com base em Olá `User-Agent` cabeçalho HTTP de solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="cc686-193">`UserAgentTelemetryInitializer` updates hello `UserAgent` property of hello `User` context of all telemetry items based on hello `User-Agent` HTTP header of hello request.</span></span>
* <span data-ttu-id="cc686-194">`UserTelemetryInitializer`saudação de atualizações `Id` e `AcquisitionDate` propriedades de `User` contexto para todos os itens de telemetria com valores extraídos de saudação `ai_user` cookie gerada pelo código de instrumentação do hello Application Insights JavaScript em execução no Olá navegador do usuário.</span><span class="sxs-lookup"><span data-stu-id="cc686-194">`UserTelemetryInitializer` updates hello `Id` and `AcquisitionDate` properties of `User` context for all telemetry items with values extracted from hello `ai_user` cookie generated by hello Application Insights JavaScript instrumentation code running in hello user's browser.</span></span>
* <span data-ttu-id="cc686-195">`WebTestTelemetryInitializer`conjuntos de Olá id de usuário, id de sessão e as propriedades de fonte sintético para solicitações de HTTP que venham de [testes de disponibilidade](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="cc686-195">`WebTestTelemetryInitializer` sets hello user id, session id and synthetic source properties for HTTP requests that come from [availability tests](app-insights-monitor-web-app-availability.md).</span></span>
  <span data-ttu-id="cc686-196">Olá `<Filters>` definir identificando as propriedades das solicitações de saudação.</span><span class="sxs-lookup"><span data-stu-id="cc686-196">hello `<Filters>` set identifying properties of hello requests.</span></span>

<span data-ttu-id="cc686-197">Para aplicativos .NET em execução no serviço de malha, você pode incluir Olá `Microsoft.ApplicationInsights.ServiceFabric` pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="cc686-197">For .NET applications running in Service Fabric, you can include hello `Microsoft.ApplicationInsights.ServiceFabric` NuGet package.</span></span> <span data-ttu-id="cc686-198">Este pacote inclui um `FabricTelemetryInitializer`, que adiciona propriedades tootelemetry itens de malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="cc686-198">This package includes a `FabricTelemetryInitializer`, which adds Service Fabric properties tootelemetry items.</span></span> <span data-ttu-id="cc686-199">Para obter mais informações, consulte Olá [página GitHub](https://go.microsoft.com/fwlink/?linkid=848457) sobre as propriedades de saudação adicionadas por este pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="cc686-199">For more information, see hello [GitHub page](https://go.microsoft.com/fwlink/?linkid=848457) about hello properties added by this NuGet package.</span></span>

## <a name="telemetry-processors-aspnet"></a><span data-ttu-id="cc686-200">Processadores de Telemetria (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="cc686-200">Telemetry Processors (ASP.NET)</span></span>
<span data-ttu-id="cc686-201">Processadores de telemetria podem filtrar e modificar cada item de telemetria apenas antes de serem enviado no portal de toohello Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="cc686-201">Telemetry processors can filter and modify each telemetry item just before it is sent from hello SDK toohello portal.</span></span>

<span data-ttu-id="cc686-202">Você pode [escrever seus próprios processadores de telemetria](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="cc686-202">You can [write your own telemetry processors](app-insights-api-filtering-sampling.md#filtering).</span></span>

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a><span data-ttu-id="cc686-203">Processador de telemetria de amostragem adaptável (da 2.0.0-beta3)</span><span class="sxs-lookup"><span data-stu-id="cc686-203">Adaptive sampling telemetry processor (from 2.0.0-beta3)</span></span>
<span data-ttu-id="cc686-204">Isso é habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="cc686-204">This is enabled by default.</span></span> <span data-ttu-id="cc686-205">Se o seu aplicativo envia muita telemetria, esse processador remove parte dela.</span><span class="sxs-lookup"><span data-stu-id="cc686-205">If your app sends a lot of telemetry, this processor removes some of it.</span></span>

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="cc686-206">parâmetro Hello fornece destino Olá Olá algoritmo tenta tooachieve.</span><span class="sxs-lookup"><span data-stu-id="cc686-206">hello parameter provides hello target that hello algorithm tries tooachieve.</span></span> <span data-ttu-id="cc686-207">Cada instância de saudação que SDK funciona independentemente, portanto, se o servidor for um cluster de vários computadores, volume real de saudação de telemetria será multiplicado adequadamente.</span><span class="sxs-lookup"><span data-stu-id="cc686-207">Each instance of hello SDK works independently, so if your server is a cluster of several machines, hello actual volume of telemetry will be multiplied accordingly.</span></span>

<span data-ttu-id="cc686-208">[Saiba mais sobre a amostragem](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="cc686-208">[Learn more about sampling](app-insights-sampling.md).</span></span>

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a><span data-ttu-id="cc686-209">Processador de telemetria de amostragem de taxa fixa (da 2.0.0-beta1)</span><span class="sxs-lookup"><span data-stu-id="cc686-209">Fixed-rate sampling telemetry processor (from 2.0.0-beta1)</span></span>
<span data-ttu-id="cc686-210">Também há um [processador de telemetria de amostra](app-insights-api-filtering-sampling.md) padrão (de 2.0.1):</span><span class="sxs-lookup"><span data-stu-id="cc686-210">There is also a standard [sampling telemetry processor](app-insights-api-filtering-sampling.md) (from 2.0.1):</span></span>

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a><span data-ttu-id="cc686-211">Parâmetros de canal (Java)</span><span class="sxs-lookup"><span data-stu-id="cc686-211">Channel parameters (Java)</span></span>
<span data-ttu-id="cc686-212">Esses parâmetros afetam como hello Java SDK deve armazenar e liberar dados de telemetria Olá que coleta.</span><span class="sxs-lookup"><span data-stu-id="cc686-212">These parameters affect how hello Java SDK should store and flush hello telemetry data that it collects.</span></span>

#### <a name="maxtelemetrybuffercapacity"></a><span data-ttu-id="cc686-213">MaxTelemetryBufferCapacity</span><span class="sxs-lookup"><span data-stu-id="cc686-213">MaxTelemetryBufferCapacity</span></span>
<span data-ttu-id="cc686-214">número de saudação de itens de telemetria que podem ser armazenados no armazenamento em memória de saudação do SDK.</span><span class="sxs-lookup"><span data-stu-id="cc686-214">hello number of telemetry items that can be stored in hello SDK's in-memory storage.</span></span> <span data-ttu-id="cc686-215">Quando esse número for atingido, Olá telemetria seja liberado - isto é, itens de telemetria de saudação são enviados server do Application Insights toohello.</span><span class="sxs-lookup"><span data-stu-id="cc686-215">When this number is reached, hello telemetry buffer is flushed - that is, hello telemetry items are sent toohello Application Insights server.</span></span>

* <span data-ttu-id="cc686-216">Mín.: 1</span><span class="sxs-lookup"><span data-stu-id="cc686-216">Min: 1</span></span>
* <span data-ttu-id="cc686-217">Máx.: 1.000</span><span class="sxs-lookup"><span data-stu-id="cc686-217">Max: 1000</span></span>
* <span data-ttu-id="cc686-218">Padrão: 500</span><span class="sxs-lookup"><span data-stu-id="cc686-218">Default: 500</span></span>

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a><span data-ttu-id="cc686-219">FlushIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="cc686-219">FlushIntervalInSeconds</span></span>
<span data-ttu-id="cc686-220">Determina com que frequência hello dados armazenados no armazenamento em memória de saudação devem ser liberado (enviada tooApplication Insights).</span><span class="sxs-lookup"><span data-stu-id="cc686-220">Determines how often hello data that is stored in hello in-memory storage should be flushed (sent tooApplication Insights).</span></span>

* <span data-ttu-id="cc686-221">Mín.: 1</span><span class="sxs-lookup"><span data-stu-id="cc686-221">Min: 1</span></span>
* <span data-ttu-id="cc686-222">Máx.: 300</span><span class="sxs-lookup"><span data-stu-id="cc686-222">Max: 300</span></span>
* <span data-ttu-id="cc686-223">Padrão: 5</span><span class="sxs-lookup"><span data-stu-id="cc686-223">Default: 5</span></span>

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a><span data-ttu-id="cc686-224">MaxTransmissionStorageCapacityInMB</span><span class="sxs-lookup"><span data-stu-id="cc686-224">MaxTransmissionStorageCapacityInMB</span></span>
<span data-ttu-id="cc686-225">Determina o tamanho máximo de saudação em MB alocado toohello o armazenamento persistente no disco local hello.</span><span class="sxs-lookup"><span data-stu-id="cc686-225">Determines hello maximum size in MB that is allotted toohello persistent storage on hello local disk.</span></span> <span data-ttu-id="cc686-226">Esse armazenamento é usado para persistir itens de telemetria que falharam toobe transmitido toohello Application Insights ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="cc686-226">This storage is used for persisting telemetry items that failed toobe transmitted toohello Application Insights endpoint.</span></span> <span data-ttu-id="cc686-227">Quando o tamanho do armazenamento Olá tem sido atendido, novos itens de telemetria serão descartados.</span><span class="sxs-lookup"><span data-stu-id="cc686-227">When hello storage size has been met, new telemetry items will be discarded.</span></span>

* <span data-ttu-id="cc686-228">Mín.: 1</span><span class="sxs-lookup"><span data-stu-id="cc686-228">Min: 1</span></span>
* <span data-ttu-id="cc686-229">Máx.: 100</span><span class="sxs-lookup"><span data-stu-id="cc686-229">Max: 100</span></span>
* <span data-ttu-id="cc686-230">Padrão: 10</span><span class="sxs-lookup"><span data-stu-id="cc686-230">Default: 10</span></span>

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a><span data-ttu-id="cc686-231">InstrumentationKey</span><span class="sxs-lookup"><span data-stu-id="cc686-231">InstrumentationKey</span></span>
<span data-ttu-id="cc686-232">Isso determina o recurso do Application Insights Olá na qual seus dados é exibida.</span><span class="sxs-lookup"><span data-stu-id="cc686-232">This determines hello Application Insights resource in which your data appears.</span></span> <span data-ttu-id="cc686-233">Normalmente um recurso separado, com uma chave separada, é criado para cada um dos seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="cc686-233">Typically you create a separate resource, with a separate key, for each of your applications.</span></span>

<span data-ttu-id="cc686-234">Se você deseja tooset Olá chave dinamicamente - por exemplo, se você deseja que os resultados de toosend de seus recursos do aplicativo toodifferent - omitir chave Olá Olá do arquivo de configuração e defini-la no código.</span><span class="sxs-lookup"><span data-stu-id="cc686-234">If you want tooset hello key dynamically - for example if you want toosend results from your application toodifferent resources - you can omit hello key from hello configuration file, and set it in code instead.</span></span>

<span data-ttu-id="cc686-235">chave de saudação tooset para todas as instâncias de TelemetryClient, incluindo módulos de telemetria padrão, defina a chave de saudação no TelemetryConfiguration.Active.</span><span class="sxs-lookup"><span data-stu-id="cc686-235">tooset hello key for all instances of TelemetryClient, including standard telemetry modules, set hello key in TelemetryConfiguration.Active.</span></span> <span data-ttu-id="cc686-236">Faça isso em um método de inicialização como global.aspx.cs em um serviço ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="cc686-236">Do this in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

```C#

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

<span data-ttu-id="cc686-237">Se você quiser apenas toosend um conjunto específico de recursos diferente de tooa de eventos, você pode definir a chave de saudação para um TelemetryClient específico:</span><span class="sxs-lookup"><span data-stu-id="cc686-237">If you just want toosend a specific set of events tooa different resource, you can set hello key for a specific TelemetryClient:</span></span>

```C#

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

<span data-ttu-id="cc686-238">uma nova chave de tooget [criar um novo recurso no portal do Application Insights Olá][new].</span><span class="sxs-lookup"><span data-stu-id="cc686-238">tooget a new key, [create a new resource in hello Application Insights portal][new].</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc686-239">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cc686-239">Next steps</span></span>
<span data-ttu-id="cc686-240">[Saiba mais sobre Olá API][api].</span><span class="sxs-lookup"><span data-stu-id="cc686-240">[Learn more about hello API][api].</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
