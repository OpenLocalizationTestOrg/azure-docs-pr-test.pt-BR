---
title: "Referência de ApplicationInsights.config - Azure | Microsoft Docs"
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
ms.openlocfilehash: 7737f47d4181b5e920434f3a5372991efb58f63e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="configuring-the-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a><span data-ttu-id="8f9f6-103">Configurar o SDK do Application Insights com ApplicationInsights.config ou.xml</span><span class="sxs-lookup"><span data-stu-id="8f9f6-103">Configuring the Application Insights SDK with ApplicationInsights.config or .xml</span></span>
<span data-ttu-id="8f9f6-104">O SDK .NET do Application Insights consiste em vários pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-104">The Application Insights .NET SDK consists of a number of NuGet packages.</span></span> <span data-ttu-id="8f9f6-105">O [pacote principal](http://www.nuget.org/packages/Microsoft.ApplicationInsights) fornece a API para enviar telemetria ao Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-105">The [core package](http://www.nuget.org/packages/Microsoft.ApplicationInsights) provides the API for sending telemetry to the Application Insights.</span></span> <span data-ttu-id="8f9f6-106">Os [pacotes adicionais](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) fornecem *módulos* e *inicializadores* de telemetria para rastreamento automático de telemetria do seu aplicativo e respectivo contexto.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-106">[Additional packages](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) provide telemetry *modules* and *initializers* for automatically tracking telemetry from your application and its context.</span></span> <span data-ttu-id="8f9f6-107">Ajustando o arquivo de configuração, você pode habilitar ou desabilitar módulos e inicializadores de telemetria, bem como definir parâmetros para alguns deles.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-107">By adjusting the configuration file, you can enable or disable telemetry modules and initializers, and set parameters for some of them.</span></span>

<span data-ttu-id="8f9f6-108">O arquivo de configuração é chamado `ApplicationInsights.config` ou `ApplicationInsights.xml`, dependendo do tipo do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-108">The configuration file is named `ApplicationInsights.config` or `ApplicationInsights.xml`, depending on the type of your application.</span></span> <span data-ttu-id="8f9f6-109">Ele é adicionado automaticamente ao seu projeto quando você [instala a maioria das versões do SDK][start].</span><span class="sxs-lookup"><span data-stu-id="8f9f6-109">It is automatically added to your project when you [install most versions of the SDK][start].</span></span> <span data-ttu-id="8f9f6-110">Ele também é adicionado a um aplicativo Web pelo [Status Monitor em um servidor IIS][redfield] ou quando você seleciona a [extensão do Application Insights para um site ou VM do Azure](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="8f9f6-110">It is also added to a web app by [Status Monitor on an IIS server][redfield], or when you select the Appplication Insights [extension for an Azure website or VM](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="8f9f6-111">Não há um arquivo equivalente para controlar o [SDK em uma página da Web][client].</span><span class="sxs-lookup"><span data-stu-id="8f9f6-111">There isn't an equivalent file to control the [SDK in a web page][client].</span></span>

<span data-ttu-id="8f9f6-112">Este documento descreve as seções que você vê no arquivo de configuração, como controlar os componentes do SDK, e quais pacotes NuGet carregar esses componentes.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-112">This document describes the sections you see in the configuration file, how they control the components of the SDK, and which NuGet packages load those components.</span></span>

## <a name="telemetry-modules-aspnet"></a><span data-ttu-id="8f9f6-113">Módulos de telemetria (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="8f9f6-113">Telemetry Modules (ASP.NET)</span></span>
<span data-ttu-id="8f9f6-114">Cada módulo de telemetria coleta um tipo específico de dados e usa o API principal para enviar os dados.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-114">Each telemetry module collects a specific type of data and uses the core API to send the data.</span></span> <span data-ttu-id="8f9f6-115">Os módulos são instalados por diferentes pacotes NuGet, que também adicionam as linhas necessárias para o arquivo. config.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-115">The modules are installed by different NuGet packages, which also add the required lines to the .config file.</span></span>

<span data-ttu-id="8f9f6-116">Há um nó no arquivo de configuração para cada módulo.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-116">There's a node in the configuration file for each module.</span></span> <span data-ttu-id="8f9f6-117">Para desabilitar um módulo, exclua o nó ou remova o comentário dele.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-117">To disable a module, delete the node or comment it out.</span></span>

### <a name="dependency-tracking"></a><span data-ttu-id="8f9f6-118">Acompanhamento de dependência</span><span class="sxs-lookup"><span data-stu-id="8f9f6-118">Dependency Tracking</span></span>
<span data-ttu-id="8f9f6-119">[Dependency tracking](app-insights-asp-net-dependencies.md) coleta a telemetria sobre chamadas para bancos de dados e serviços externos e torna o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-119">[Dependency tracking](app-insights-asp-net-dependencies.md) collects telemetry about calls your app makes to databases and external services and databases.</span></span> <span data-ttu-id="8f9f6-120">Para permitir que esse módulo funcione em um servidor IIS, é necessário [instalar o Status Monitor][redfield].</span><span class="sxs-lookup"><span data-stu-id="8f9f6-120">To allow this module to work in an IIS server, you need to [install Status Monitor][redfield].</span></span> <span data-ttu-id="8f9f6-121">Para usá-lo em aplicativos Web do Azure ou VMs, [selecione a extensão do Application Insights](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="8f9f6-121">To use it in Azure web apps or VMs, [select the Application Insights extension](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="8f9f6-122">Você também pode escrever seu próprio código de rastreamento de dependência usando a [API TrackDependency](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="8f9f6-122">You can also write your own dependency tracking code using the [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* <span data-ttu-id="8f9f6-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) .</span><span class="sxs-lookup"><span data-stu-id="8f9f6-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet package.</span></span>

### <a name="performance-collector"></a><span data-ttu-id="8f9f6-124">Coletor de desempenho</span><span class="sxs-lookup"><span data-stu-id="8f9f6-124">Performance collector</span></span>
<span data-ttu-id="8f9f6-125">[Coleta contadores de desempenho do sistema](app-insights-performance-counters.md), como CPU, memória e carga de rede de instalações do IIS.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-125">[Collects system performance counters](app-insights-performance-counters.md) such as CPU, memory and network load from IIS installations.</span></span> <span data-ttu-id="8f9f6-126">Você pode especificar quais contadores coletar, incluindo contadores de desempenho que você configurou por si mesmo.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-126">You can specify which counters to collect, including performance counters you have set up yourself.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* <span data-ttu-id="8f9f6-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) .</span><span class="sxs-lookup"><span data-stu-id="8f9f6-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet package.</span></span>

### <a name="application-insights-diagnostics-telemetry"></a><span data-ttu-id="8f9f6-128">Telemetria de diagnóstico do Application Insights</span><span class="sxs-lookup"><span data-stu-id="8f9f6-128">Application Insights Diagnostics Telemetry</span></span>
<span data-ttu-id="8f9f6-129">Os erros de `DiagnosticsTelemetryModule` relatórios na instrumentação do Application Insights se codificam sozinhos.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-129">The `DiagnosticsTelemetryModule` reports errors in the Application Insights instrumentation code itself.</span></span> <span data-ttu-id="8f9f6-130">Por exemplo, se o código não puder acessar contadores de desempenho ou se um `ITelemetryInitializer` lançar uma exceção.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-130">For example, if the code cannot access performance counters or if an `ITelemetryInitializer` throws an exception.</span></span> <span data-ttu-id="8f9f6-131">A telemetria de rastreamento rastreada por esse módulo aparece na [Pesquisa de Diagnóstico][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="8f9f6-131">Trace telemetry tracked by this module appears in the [Diagnostic Search][diagnostic].</span></span> <span data-ttu-id="8f9f6-132">Envia dados de diagnóstico para dc.services.vsallin.net.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-132">Sends diagnostic data to dc.services.vsallin.net.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* <span data-ttu-id="8f9f6-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) .</span><span class="sxs-lookup"><span data-stu-id="8f9f6-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="8f9f6-134">Se você instalar apenas esse pacote, o arquivo applicationinsights. config não é criado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-134">If you only install this package, the ApplicationInsights.config file is not automatically created.</span></span>

### <a name="developer-mode"></a><span data-ttu-id="8f9f6-135">Modo de desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="8f9f6-135">Developer Mode</span></span>
<span data-ttu-id="8f9f6-136">`DeveloperModeWithDebuggerAttachedTelemetryModule` força `TelemetryChannel` do Application Insights a enviar dados imediatamente, um item de telemetria por vez, quando um depurador é conectado ao processo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-136">`DeveloperModeWithDebuggerAttachedTelemetryModule` forces the Application Insights `TelemetryChannel` to send data immediately, one telemetry item at a time, when a debugger is attached to the application process.</span></span> <span data-ttu-id="8f9f6-137">Isso reduz a quantidade de tempo entre o momento em que seu aplicativo rastreia a telemetria e quando ele aparece no portal do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-137">This reduces the amount of time between the moment when your application tracks telemetry and when it appears on the Application Insights portal.</span></span> <span data-ttu-id="8f9f6-138">Faz com uma sobrecarga significativa na largura de banda de CPU e rede.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-138">It causes significant overhead in CPU and network bandwidth.</span></span>

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* <span data-ttu-id="8f9f6-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) .</span><span class="sxs-lookup"><span data-stu-id="8f9f6-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package</span></span>

### <a name="web-request-tracking"></a><span data-ttu-id="8f9f6-140">Acompanhamento de solicitação da Web</span><span class="sxs-lookup"><span data-stu-id="8f9f6-140">Web Request Tracking</span></span>
<span data-ttu-id="8f9f6-141">Relatórios do [código de tempo e o resultado da resposta](app-insights-asp-net.md) de solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-141">Reports the [response time and result code](app-insights-asp-net.md) of HTTP requests.</span></span>

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* <span data-ttu-id="8f9f6-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) .</span><span class="sxs-lookup"><span data-stu-id="8f9f6-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>

### <a name="exception-tracking"></a><span data-ttu-id="8f9f6-143">Acompanhamento de exceções</span><span class="sxs-lookup"><span data-stu-id="8f9f6-143">Exception tracking</span></span>
<span data-ttu-id="8f9f6-144">`ExceptionTrackingTelemetryModule` rastreia exceção sem tratamento no seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-144">`ExceptionTrackingTelemetryModule` tracks unhandled exceptions in your web app.</span></span> <span data-ttu-id="8f9f6-145">Consulte [Falhas e exceções][exceptions].</span><span class="sxs-lookup"><span data-stu-id="8f9f6-145">See [Failures and exceptions][exceptions].</span></span>

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* <span data-ttu-id="8f9f6-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) .</span><span class="sxs-lookup"><span data-stu-id="8f9f6-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>
* <span data-ttu-id="8f9f6-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` -rastreia [exceções de tarefa não observada](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span><span class="sxs-lookup"><span data-stu-id="8f9f6-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - tracks [unobserved task exceptions](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span></span>
* <span data-ttu-id="8f9f6-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` -rastreia as exceções sem tratamento para funções de trabalho, serviços do Windows e aplicativos de console.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - tracks unhandled exceptions for worker roles, windows services, and console applications.</span></span>
* <span data-ttu-id="8f9f6-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) .</span><span class="sxs-lookup"><span data-stu-id="8f9f6-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package.</span></span>

### <a name="eventsource-tracking"></a><span data-ttu-id="8f9f6-150">Monitoramento de EventSource</span><span class="sxs-lookup"><span data-stu-id="8f9f6-150">EventSource Tracking</span></span>
<span data-ttu-id="8f9f6-151">O `EventSourceTelemetryModule` permite configurar eventos EventSource a serem enviados ao Application Insights como rastreamentos.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-151">`EventSourceTelemetryModule` allows you to configure EventSource events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="8f9f6-152">Para obter informações sobre o monitoramento de eventos EventSource, consulte [Usando eventos EventSource](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span><span class="sxs-lookup"><span data-stu-id="8f9f6-152">For information on tracking EventSource events, see [Using EventSource Events](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span></span>

* `Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule`
* [<span data-ttu-id="8f9f6-153">Microsoft.ApplicationInsights.EventSourceListener</span><span class="sxs-lookup"><span data-stu-id="8f9f6-153">Microsoft.ApplicationInsights.EventSourceListener</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EventSourceListener) 

### <a name="etw-event-tracking"></a><span data-ttu-id="8f9f6-154">Monitoramento de eventos ETW</span><span class="sxs-lookup"><span data-stu-id="8f9f6-154">ETW Event Tracking</span></span>
<span data-ttu-id="8f9f6-155">O `EtwCollectorTelemetryModule` permite configurar eventos de provedores ETW a serem enviados ao Application Insights como rastreamentos.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-155">`EtwCollectorTelemetryModule` allows you to configure events from ETW providers to be sent to Application Insights as traces.</span></span> <span data-ttu-id="8f9f6-156">Para obter informações sobre o monitoramento de eventos ETW, consulte [Usando eventos ETW](app-insights-asp-net-trace-logs.md#using-etw-events).</span><span class="sxs-lookup"><span data-stu-id="8f9f6-156">For information on tracking ETW events, see [Using ETW Events](app-insights-asp-net-trace-logs.md#using-etw-events).</span></span>

* `Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule`
* [<span data-ttu-id="8f9f6-157">Microsoft.ApplicationInsights.EtwCollector</span><span class="sxs-lookup"><span data-stu-id="8f9f6-157">Microsoft.ApplicationInsights.EtwCollector</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EtwCollector) 

### <a name="microsoftapplicationinsights"></a><span data-ttu-id="8f9f6-158">Microsoft.ApplicationInsights</span><span class="sxs-lookup"><span data-stu-id="8f9f6-158">Microsoft.ApplicationInsights</span></span>
<span data-ttu-id="8f9f6-159">O pacote Microsoft.ApplicationInsights fornece a [API principal](https://msdn.microsoft.com/library/mt420197.aspx) do SDK.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-159">The Microsoft.ApplicationInsights package provides the [core API](https://msdn.microsoft.com/library/mt420197.aspx) of the SDK.</span></span> <span data-ttu-id="8f9f6-160">Usam os outros módulos de telemetria e você também pode [usá-lo para definir sua própria telemetria](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="8f9f6-160">The other telemetry modules use this, and you can also [use it to define your own telemetry](app-insights-api-custom-events-metrics.md).</span></span>

* <span data-ttu-id="8f9f6-161">Nenhuma entrada em ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-161">No entry in ApplicationInsights.config.</span></span>
* <span data-ttu-id="8f9f6-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) .</span><span class="sxs-lookup"><span data-stu-id="8f9f6-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="8f9f6-163">Se você acabou de instalar este NuGet, nenhum arquivo. config será gerado.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-163">If you just install this NuGet, no .config file is generated.</span></span>

## <a name="telemetry-channel"></a><span data-ttu-id="8f9f6-164">Canal de telemetria</span><span class="sxs-lookup"><span data-stu-id="8f9f6-164">Telemetry Channel</span></span>
<span data-ttu-id="8f9f6-165">O canal de telemetria gerencia o armazenamento em buffer e transmissão de telemetria ao serviço Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-165">The telemetry channel manages buffering and transmission of telemetry to the Application Insights service.</span></span>

* <span data-ttu-id="8f9f6-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel` é o canal padrão para serviços.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel` is the default channel for services.</span></span> <span data-ttu-id="8f9f6-167">Ele armazena em buffer dados na memória.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-167">It buffers data in memory.</span></span>
* <span data-ttu-id="8f9f6-168">`Microsoft.ApplicationInsights.PersistenceChannel` é uma alternativa para aplicativos de console.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-168">`Microsoft.ApplicationInsights.PersistenceChannel` is an alternative for console applications.</span></span> <span data-ttu-id="8f9f6-169">Pode salvar os dados não certificados para armazenamento persistente quando seu aplicativo estiver fechado e vai enviá-los quando o aplicativo for iniciado novamente.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-169">It can save any unflushed data to persistent storage when your app closes down, and will send it when the app starts again.</span></span>

## <a name="telemetry-initializers-aspnet"></a><span data-ttu-id="8f9f6-170">Inicializadores de telemetria (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="8f9f6-170">Telemetry Initializers (ASP.NET)</span></span>
<span data-ttu-id="8f9f6-171">Os inicializadores de telemetria definem propriedades de contexto que são enviadas com cada item de telemetria.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-171">Telemetry initializers set context properties that are sent along with every item of telemetry.</span></span>

<span data-ttu-id="8f9f6-172">Você pode [escrever seus próprios inicializadores](app-insights-api-filtering-sampling.md#add-properties) para definir as propriedades de contexto.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-172">You can [write your own initializers](app-insights-api-filtering-sampling.md#add-properties) to set context properties.</span></span>

<span data-ttu-id="8f9f6-173">Os inicializadores padrão foram todos configurados pelos pacotes do WindowsServer NuGet ou Web:</span><span class="sxs-lookup"><span data-stu-id="8f9f6-173">The standard initializers are all set either by the Web or WindowsServer NuGet packages:</span></span>

* <span data-ttu-id="8f9f6-174">`AccountIdTelemetryInitializer` define a propriedade AccountId.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-174">`AccountIdTelemetryInitializer` sets the AccountId property.</span></span>
* <span data-ttu-id="8f9f6-175">`AuthenticatedUserIdTelemetryInitializer` define a propriedade AuthenticatedUserId como definido pelo SDK do JavaScript.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-175">`AuthenticatedUserIdTelemetryInitializer` sets the AuthenticatedUserId property as set by the JavaScript SDK.</span></span>
* <span data-ttu-id="8f9f6-176">`AzureRoleEnvironmentTelemetryInitializer` atualiza as propriedades `RoleName` e `RoleInstance` do contexto `Device` para todos os itens de telemetria com informações extraídas do ambiente de tempo de execução do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-176">`AzureRoleEnvironmentTelemetryInitializer` updates the `RoleName` and `RoleInstance` properties of the `Device` context for all telemetry items with information extracted from the Azure runtime environment.</span></span>
* <span data-ttu-id="8f9f6-177">`BuildInfoConfigComponentVersionTelemetryInitializer` atualiza a `Version` propriedade do `Component` contexto para todos os itens de telemetria com o valor extraído do arquivo `BuildInfo.config` produzido pelo MS Build.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-177">`BuildInfoConfigComponentVersionTelemetryInitializer` updates the `Version` property of the `Component` context for all telemetry items with the value extracted from the `BuildInfo.config` file produced by MS Build.</span></span>
* <span data-ttu-id="8f9f6-178">`ClientIpHeaderTelemetryInitializer` atualiza a propriedade `Ip` do contexto `Location` de todos os itens de telemetria baseados no cabeçalho HTTP `X-Forwarded-For` da solicitação.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-178">`ClientIpHeaderTelemetryInitializer` updates `Ip` property of the `Location` context of all telemetry items based on the `X-Forwarded-For` HTTP header of the request.</span></span>
* <span data-ttu-id="8f9f6-179">`DeviceTelemetryInitializer` atualiza as propriedades a seguir do contexto `Device` para todos os itens de telemetria.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-179">`DeviceTelemetryInitializer` updates the following properties of the `Device` context for all telemetry items.</span></span>
  * <span data-ttu-id="8f9f6-180">`Type` é definido como "PC"</span><span class="sxs-lookup"><span data-stu-id="8f9f6-180">`Type` is set to "PC"</span></span>
  * <span data-ttu-id="8f9f6-181">`Id` é definido para o nome de domínio do computador onde o aplicativo Web está em execução.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-181">`Id` is set to the domain name of the computer where the web application is running.</span></span>
  * <span data-ttu-id="8f9f6-182">`OemName` é definido para o valor extraído do campo `Win32_ComputerSystem.Manufacturer` usando WMI.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-182">`OemName` is set to the value extracted from the `Win32_ComputerSystem.Manufacturer` field using WMI.</span></span>
  * <span data-ttu-id="8f9f6-183">`Model` é definido para o valor extraído do campo `Win32_ComputerSystem.Model` usando WMI.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-183">`Model` is set to the value extracted from the `Win32_ComputerSystem.Model` field using WMI.</span></span>
  * <span data-ttu-id="8f9f6-184">`NetworkType` é definido para o valor extraído de `NetworkInterface`.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-184">`NetworkType` is set to the value extracted from the `NetworkInterface`.</span></span>
  * <span data-ttu-id="8f9f6-185">`Language` é definido para o nome da `CurrentCulture`.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-185">`Language` is set to the name of the `CurrentCulture`.</span></span>
* <span data-ttu-id="8f9f6-186">`DomainNameRoleInstanceTelemetryInitializer` atualiza a propriedade `RoleInstance` do contexto `Device` para todos os itens de telemetria com o nome de domínio do computador onde o aplicativo Web está em execução.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-186">`DomainNameRoleInstanceTelemetryInitializer` updates the `RoleInstance` property of the `Device` context for all telemetry items with the domain name of the computer where the web application is running.</span></span>
* <span data-ttu-id="8f9f6-187">`OperationNameTelemetryInitializer` atualiza a propriedade `Name` das propriedades `RequestTelemetry` e `Name` do contexto `Operation` de todos os itens de telemetria baseados no método HTTP, bem como nomes do controlador MVC do ASP.NET e ação invocada para processar a solicitação.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-187">`OperationNameTelemetryInitializer` updates the `Name` property of the `RequestTelemetry` and the `Name` property of the `Operation` context of all telemetry items based on the HTTP method, as well as names of ASP.NET MVC controller and action invoked to process the request.</span></span>
* <span data-ttu-id="8f9f6-188">`OperationIdTelemetryInitializer` ou `OperationCorrelationTelemetryInitializer` atualiza a propriedade de contexto `Operation.Id` de todos os itens de telemetria rastreados ao manipular uma solicitação com o `RequestTelemetry.Id` gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-188">`OperationIdTelemetryInitializer` or `OperationCorrelationTelemetryInitializer` updates the `Operation.Id` context property of all telemetry items tracked while handling a request with the automatically generated `RequestTelemetry.Id`.</span></span>
* <span data-ttu-id="8f9f6-189">`SessionTelemetryInitializer` atualiza a propriedade `Id` do contexto `Session` para todos os itens de telemetria com valor extraído do cookie `ai_session` gerado pelo código de instrumentação do JavaScript do ApplicationInsights em execução no navegador do usuário.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-189">`SessionTelemetryInitializer` updates the `Id` property of the `Session` context for all telemetry items with value extracted from the `ai_session` cookie generated by the ApplicationInsights JavaScript instrumentation code running in the user's browser.</span></span>
* <span data-ttu-id="8f9f6-190">`SyntheticTelemetryInitializer` ou `SyntheticUserAgentTelemetryInitializer` atualiza as propriedades de contexto `User`, `Session` e `Operation` de todos os itens de telemetria rastreados ao lidar com uma solicitação de uma fonte sintética, como um teste de disponibilidade ou um bot do mecanismo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-190">`SyntheticTelemetryInitializer` or `SyntheticUserAgentTelemetryInitializer` updates the `User`, `Session` and `Operation` contexts properties of all telemetry items tracked when handling a request from a synthetic source, such as an availability test or search engine bot.</span></span> <span data-ttu-id="8f9f6-191">Por padrão, o [Metrics Explorer](app-insights-metrics-explorer.md) não exibe telemetria sintética.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-191">By default, [Metrics Explorer](app-insights-metrics-explorer.md) does not display synthetic telemetry.</span></span>

    <span data-ttu-id="8f9f6-192">Os `<Filters>` definem as propriedades de identificação das solicitações.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-192">The `<Filters>` set identifying properties of the requests.</span></span>
* <span data-ttu-id="8f9f6-193">`UserAgentTelemetryInitializer` atualiza a propriedade `UserAgent` do contexto `User` de todos os itens de telemetria baseados no cabeçalho HTTP `User-Agent` da solicitação.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-193">`UserAgentTelemetryInitializer` updates the `UserAgent` property of the `User` context of all telemetry items based on the `User-Agent` HTTP header of the request.</span></span>
* <span data-ttu-id="8f9f6-194">`UserTelemetryInitializer` atualiza as propriedades `Id` e `AcquisitionDate` do contexto `User` para todos os itens de telemetria com valores extraídos do cookie `ai_user` gerado pelo código de instrumentação do JavaScript do Application Insights em execução no navegador do usuário.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-194">`UserTelemetryInitializer` updates the `Id` and `AcquisitionDate` properties of `User` context for all telemetry items with values extracted from the `ai_user` cookie generated by the Application Insights JavaScript instrumentation code running in the user's browser.</span></span>
* <span data-ttu-id="8f9f6-195">`WebTestTelemetryInitializer` define a ID do usuário, a ID da sessão e as propriedades da fonte sintética para solicitações HTTP advindas dos [testes de disponibilidade](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="8f9f6-195">`WebTestTelemetryInitializer` sets the user id, session id and synthetic source properties for HTTP requests that come from [availability tests](app-insights-monitor-web-app-availability.md).</span></span>
  <span data-ttu-id="8f9f6-196">Os `<Filters>` definem as propriedades de identificação das solicitações.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-196">The `<Filters>` set identifying properties of the requests.</span></span>

<span data-ttu-id="8f9f6-197">Para aplicativos .NET em execução no Service Fabric, você pode incluir o pacote do NuGet `Microsoft.ApplicationInsights.ServiceFabric`.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-197">For .NET applications running in Service Fabric, you can include the `Microsoft.ApplicationInsights.ServiceFabric` NuGet package.</span></span> <span data-ttu-id="8f9f6-198">Este pacote inclui um `FabricTelemetryInitializer`, que adiciona propriedades do Service Fabric a itens de telemetria.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-198">This package includes a `FabricTelemetryInitializer`, which adds Service Fabric properties to telemetry items.</span></span> <span data-ttu-id="8f9f6-199">Para obter mais informações, consulte a [página do GitHub](https://go.microsoft.com/fwlink/?linkid=848457) sobre as propriedades adicionadas por este pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-199">For more information, see the [GitHub page](https://go.microsoft.com/fwlink/?linkid=848457) about the properties added by this NuGet package.</span></span>

## <a name="telemetry-processors-aspnet"></a><span data-ttu-id="8f9f6-200">Processadores de Telemetria (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="8f9f6-200">Telemetry Processors (ASP.NET)</span></span>
<span data-ttu-id="8f9f6-201">Processadores de telemetria podem filtrar e modificar cada item de telemetria antes de serem enviado do SDK para o portal.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-201">Telemetry processors can filter and modify each telemetry item just before it is sent from the SDK to the portal.</span></span>

<span data-ttu-id="8f9f6-202">Você pode [escrever seus próprios processadores de telemetria](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="8f9f6-202">You can [write your own telemetry processors](app-insights-api-filtering-sampling.md#filtering).</span></span>

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a><span data-ttu-id="8f9f6-203">Processador de telemetria de amostragem adaptável (da 2.0.0-beta3)</span><span class="sxs-lookup"><span data-stu-id="8f9f6-203">Adaptive sampling telemetry processor (from 2.0.0-beta3)</span></span>
<span data-ttu-id="8f9f6-204">Isso é habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-204">This is enabled by default.</span></span> <span data-ttu-id="8f9f6-205">Se o seu aplicativo envia muita telemetria, esse processador remove parte dela.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-205">If your app sends a lot of telemetry, this processor removes some of it.</span></span>

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="8f9f6-206">O parâmetro fornece o destino que o algoritmo tenta obter.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-206">The parameter provides the target that the algorithm tries to achieve.</span></span> <span data-ttu-id="8f9f6-207">Cada instância do SDK funciona independentemente, portanto, se o servidor for um cluster de vários computadores, o volume real de telemetria será multiplicado adequadamente.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-207">Each instance of the SDK works independently, so if your server is a cluster of several machines, the actual volume of telemetry will be multiplied accordingly.</span></span>

<span data-ttu-id="8f9f6-208">[Saiba mais sobre a amostragem](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="8f9f6-208">[Learn more about sampling](app-insights-sampling.md).</span></span>

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a><span data-ttu-id="8f9f6-209">Processador de telemetria de amostragem de taxa fixa (da 2.0.0-beta1)</span><span class="sxs-lookup"><span data-stu-id="8f9f6-209">Fixed-rate sampling telemetry processor (from 2.0.0-beta1)</span></span>
<span data-ttu-id="8f9f6-210">Também há um [processador de telemetria de amostra](app-insights-api-filtering-sampling.md) padrão (de 2.0.1):</span><span class="sxs-lookup"><span data-stu-id="8f9f6-210">There is also a standard [sampling telemetry processor](app-insights-api-filtering-sampling.md) (from 2.0.1):</span></span>

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close to 100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a><span data-ttu-id="8f9f6-211">Parâmetros de canal (Java)</span><span class="sxs-lookup"><span data-stu-id="8f9f6-211">Channel parameters (Java)</span></span>
<span data-ttu-id="8f9f6-212">Esses parâmetros afetam como o SDK do Java deve armazenar e liberar os dados de telemetria coletados.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-212">These parameters affect how the Java SDK should store and flush the telemetry data that it collects.</span></span>

#### <a name="maxtelemetrybuffercapacity"></a><span data-ttu-id="8f9f6-213">MaxTelemetryBufferCapacity</span><span class="sxs-lookup"><span data-stu-id="8f9f6-213">MaxTelemetryBufferCapacity</span></span>
<span data-ttu-id="8f9f6-214">O número de itens de telemetria que podem ser armazenados na memória do SDK.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-214">The number of telemetry items that can be stored in the SDK's in-memory storage.</span></span> <span data-ttu-id="8f9f6-215">Quando esse número for atingido, o buffer de telemetria é liberado, ou seja, os itens de telemetria são enviados para o servidor do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-215">When this number is reached, the telemetry buffer is flushed - that is, the telemetry items are sent to the Application Insights server.</span></span>

* <span data-ttu-id="8f9f6-216">Mín.: 1</span><span class="sxs-lookup"><span data-stu-id="8f9f6-216">Min: 1</span></span>
* <span data-ttu-id="8f9f6-217">Máx.: 1.000</span><span class="sxs-lookup"><span data-stu-id="8f9f6-217">Max: 1000</span></span>
* <span data-ttu-id="8f9f6-218">Padrão: 500</span><span class="sxs-lookup"><span data-stu-id="8f9f6-218">Default: 500</span></span>

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a><span data-ttu-id="8f9f6-219">FlushIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="8f9f6-219">FlushIntervalInSeconds</span></span>
<span data-ttu-id="8f9f6-220">Determina com que frequência os dados armazenados no armazenamento de memória devem ser liberados (enviada para o Application Insights).</span><span class="sxs-lookup"><span data-stu-id="8f9f6-220">Determines how often the data that is stored in the in-memory storage should be flushed (sent to Application Insights).</span></span>

* <span data-ttu-id="8f9f6-221">Mín.: 1</span><span class="sxs-lookup"><span data-stu-id="8f9f6-221">Min: 1</span></span>
* <span data-ttu-id="8f9f6-222">Máx.: 300</span><span class="sxs-lookup"><span data-stu-id="8f9f6-222">Max: 300</span></span>
* <span data-ttu-id="8f9f6-223">Padrão: 5</span><span class="sxs-lookup"><span data-stu-id="8f9f6-223">Default: 5</span></span>

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a><span data-ttu-id="8f9f6-224">MaxTransmissionStorageCapacityInMB</span><span class="sxs-lookup"><span data-stu-id="8f9f6-224">MaxTransmissionStorageCapacityInMB</span></span>
<span data-ttu-id="8f9f6-225">Determina o tamanho máximo em MB alocado para o armazenamento persistente no disco local.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-225">Determines the maximum size in MB that is allotted to the persistent storage on the local disk.</span></span> <span data-ttu-id="8f9f6-226">Esse armazenamento é usado para itens de telemetria persistentes que falharam ao serem transmitidos para o ponto de extremidade do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-226">This storage is used for persisting telemetry items that failed to be transmitted to the Application Insights endpoint.</span></span> <span data-ttu-id="8f9f6-227">Quando o tamanho do armazenamento for atingido, novos itens de telemetria serão descartados.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-227">When the storage size has been met, new telemetry items will be discarded.</span></span>

* <span data-ttu-id="8f9f6-228">Mín.: 1</span><span class="sxs-lookup"><span data-stu-id="8f9f6-228">Min: 1</span></span>
* <span data-ttu-id="8f9f6-229">Máx.: 100</span><span class="sxs-lookup"><span data-stu-id="8f9f6-229">Max: 100</span></span>
* <span data-ttu-id="8f9f6-230">Padrão: 10</span><span class="sxs-lookup"><span data-stu-id="8f9f6-230">Default: 10</span></span>

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a><span data-ttu-id="8f9f6-231">InstrumentationKey</span><span class="sxs-lookup"><span data-stu-id="8f9f6-231">InstrumentationKey</span></span>
<span data-ttu-id="8f9f6-232">Isso determina o recurso do Application Insights em que seus dados aparecem.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-232">This determines the Application Insights resource in which your data appears.</span></span> <span data-ttu-id="8f9f6-233">Normalmente um recurso separado, com uma chave separada, é criado para cada um dos seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-233">Typically you create a separate resource, with a separate key, for each of your applications.</span></span>

<span data-ttu-id="8f9f6-234">Se você deseja definir a chave dinamicamente, por exemplo, se quiser enviar os resultados do seu aplicativo para outros recursos, é possível omitir a chave do arquivo de configuração e defini-lo no código.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-234">If you want to set the key dynamically - for example if you want to send results from your application to different resources - you can omit the key from the configuration file, and set it in code instead.</span></span>

<span data-ttu-id="8f9f6-235">Para definir a chave para todas as instâncias de TelemetryClient, incluindo módulos de telemetria padrão, defina a chave em TelemetryConfiguration.Active.</span><span class="sxs-lookup"><span data-stu-id="8f9f6-235">To set the key for all instances of TelemetryClient, including standard telemetry modules, set the key in TelemetryConfiguration.Active.</span></span> <span data-ttu-id="8f9f6-236">Faça isso em um método de inicialização como global.aspx.cs em um serviço ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="8f9f6-236">Do this in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

```C#

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

<span data-ttu-id="8f9f6-237">Se quiser enviar um conjunto específico de eventos para um recurso diferente, você pode definir a chave para um TelemetryClient específico:</span><span class="sxs-lookup"><span data-stu-id="8f9f6-237">If you just want to send a specific set of events to a different resource, you can set the key for a specific TelemetryClient:</span></span>

```C#

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

<span data-ttu-id="8f9f6-238">Para obter uma nova chave, [crie um novo recurso no portal do Application Insights][new].</span><span class="sxs-lookup"><span data-stu-id="8f9f6-238">To get a new key, [create a new resource in the Application Insights portal][new].</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f9f6-239">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8f9f6-239">Next steps</span></span>
<span data-ttu-id="8f9f6-240">[Saiba mais sobre a API][api].</span><span class="sxs-lookup"><span data-stu-id="8f9f6-240">[Learn more about the API][api].</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
