---
title: "Serviços de aaaMonitor Node. js com o Azure Application Insights | Microsoft Docs"
description: "Monitore o desempenho e diagnostique problemas em serviços do Node.js com o Application Insights."
services: application-insights
documentationcenter: nodejs
author: joshgav
manager: carmonm
ms.assetid: 2ec7f809-5e1a-41cf-9fcd-d0ed4bebd08c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/01/2017
ms.author: bwren
ms.openlocfilehash: 0a7e66990cd4d3a2fcaf3fa779adb336c861f8ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-nodejs-services-and-apps-with-application-insights"></a><span data-ttu-id="8d6f3-103">Como monitorar seus serviços do Node.js e aplicativos com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="8d6f3-103">Monitor your Node.js services and apps with Application Insights</span></span>

<span data-ttu-id="8d6f3-104">[Informações de aplicativo do Azure](app-insights-overview.md) monitora seus componentes e serviços de back-end depois de implantá-las toohelp você [detectar e diagnosticar rapidamente problemas de desempenho e outros](app-insights-detect-triage-diagnose.md).</span><span class="sxs-lookup"><span data-stu-id="8d6f3-104">[Azure Application Insights](app-insights-overview.md) monitors your backend services and components after you deploy them toohelp you [discover and rapidly diagnose performance and other issues](app-insights-detect-triage-diagnose.md).</span></span> <span data-ttu-id="8d6f3-105">Use-o nos serviços do Node.js hospedado em qualquer lugar: seu datacenter, VMs do Azure, aplicativos Web e até mesmo em outras nuvens públicas.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-105">Use it for Node.js services hosted anywhere: your datacenter, Azure VMs and Web Apps, and even other public clouds.</span></span>

<span data-ttu-id="8d6f3-106">tooreceive, armazenar e explorar os dados de monitoramentos, execute Olá seguindo as instruções tooinclude um agente em seu código e configurar um recurso do Application Insights correspondente no Azure.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-106">tooreceive, store, and explore your monitoring data, follow hello following instructions tooinclude an agent in your code and set up a corresponding Application Insights resource in Azure.</span></span> <span data-ttu-id="8d6f3-107">Agente de saudação envia recurso toothat de dados para análise posterior e exploração.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-107">hello agent sends data toothat resource for further analysis and exploration.</span></span>

<span data-ttu-id="8d6f3-108">Agente de Node. js Olá automaticamente pode monitorar entrada e saída HTTP solicitações, várias métricas de sistema e exceções.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-108">hello Node.js agent can automatically monitor incoming and outgoing HTTP requests, several system metrics, and exceptions.</span></span> <span data-ttu-id="8d6f3-109">A partir da v0.20, ele também pode monitorar alguns pacotes de terceiros comuns como `mongodb`, `mysql` e `redis`.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-109">Beginning in v0.20, it can also monitor some common third-party packages such as `mongodb`, `mysql`, and `redis`.</span></span> <span data-ttu-id="8d6f3-110">Todos os eventos relacionados a solicitação HTTP de entrada tooan são correlacionadas para solução de problemas mais rapidamente.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-110">All events related tooan incoming HTTP request are correlated for faster troubleshooting.</span></span>

<span data-ttu-id="8d6f3-111">Você pode monitorar outros aspectos do seu aplicativo e sistema por instrumentação-las manualmente usando a API de agente Olá descrita posteriormente.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-111">You can monitor more aspects of your app and system by manually instrumenting them using hello agent API described later.</span></span>

![Gráficos de exemplo de monitoramento de desempenho](./media/app-insights-nodejs/10-perf.png)

## <a name="getting-started"></a><span data-ttu-id="8d6f3-113">Introdução</span><span class="sxs-lookup"><span data-stu-id="8d6f3-113">Getting Started</span></span>

<span data-ttu-id="8d6f3-114">Vamos estudar a configuração de monitoramento para um serviço ou aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-114">Let's step through setting up monitoring for an app or service.</span></span>

### <span data-ttu-id="8d6f3-115"><a name="resource"></a>Configuração de um recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="8d6f3-115"><a name="resource"></a> Set up an App Insights resource</span></span>

<span data-ttu-id="8d6f3-116">**Antes de iniciar**, verifique se você tem uma assinatura do Azure ou [obtenha uma gratuitamente][azure-free-offer].</span><span class="sxs-lookup"><span data-stu-id="8d6f3-116">**Before you start**, make sure you have an Azure subscription or [get a new one for free][azure-free-offer].</span></span> <span data-ttu-id="8d6f3-117">Se sua organização já tiver uma assinatura do Azure, um administrador pode seguir [estas instruções] [ add-aad-user] tooadd tooit você.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-117">If your organization already has an Azure subscription, an administrator can follow [these instructions][add-aad-user] tooadd you tooit.</span></span>

[azure-free-offer]: https://azure.microsoft.com/en-us/free/
[add-aad-user]: https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-create-azure-portal

<span data-ttu-id="8d6f3-118">Agora, faça logon no toohello [portal do Azure] [ portal] e crie um recurso do Application Insights, conforme ilustrado no seguinte Olá - clique em "Novo" > "Developer tools" > "Application Insights".</span><span class="sxs-lookup"><span data-stu-id="8d6f3-118">Now log in toohello [Azure portal][portal] and create an Application Insights resource as illustrated in hello following - click "New" > "Developer tools" > "Application Insights".</span></span> <span data-ttu-id="8d6f3-119">recurso de saudação inclui um ponto de extremidade para receber dados de telemetria, armazenamento de dados, salvar relatórios e painéis, regras e configuração de alerta e muito mais.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-119">hello resource includes an endpoint for receiving telemetry data, storage for this data, saved reports and dashboards, rule and alert configuration, and more.</span></span>

![Criação de um recurso do Application Insights](./media/app-insights-nodejs/03-new_appinsights_resource.png)

<span data-ttu-id="8d6f3-121">Na página de criação do recurso hello, escolha "Aplicativo Node. js" da saudação aplicativo lista suspensa tipo.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-121">On hello resource creation page, choose "Node.js Application" from hello application type drop-down.</span></span> <span data-ttu-id="8d6f3-122">tipo de aplicativo Hello determina o conjunto padrão de saudação de painéis e relatórios criados para você.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-122">hello app type determines hello default set of dashboards and reports created for you.</span></span> <span data-ttu-id="8d6f3-123">Na verdade, não há com que se preocupar, qualquer recurso do Application Insights pode coletar dados de qualquer idioma e plataforma.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-123">Don't worry though, any App Insights resource can in fact collect data from any language and platform.</span></span>

![Formulário de recursos do Application Insights novo](./media/app-insights-nodejs/04-create_appinsights_resource.png)

### <span data-ttu-id="8d6f3-125"><a name="agent"></a>Configurar o agente do hello Node. js</span><span class="sxs-lookup"><span data-stu-id="8d6f3-125"><a name="agent"></a> Set up hello Node.js agent</span></span>

<span data-ttu-id="8d6f3-126">Agora ela é um agente de saudação do tempo tooinclude em seu aplicativo para que ele possa coletar dados.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-126">Now it's time tooinclude hello agent in your app so it can gather data.</span></span>
<span data-ttu-id="8d6f3-127">Inicie a cópia da chave de instrumentação do recurso (daqui por diante chamado tooas seu `ikey`) do portal Olá conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-127">Start by copying your resource's Instrumentation Key (hereinafter referred tooas your `ikey`) from hello portal as shown below.</span></span> <span data-ttu-id="8d6f3-128">Olá ideias de aplicativo sistema usa essa tooyour de dados toomap principais recursos do Azure para que seja necessário toospecify-lo no seu código para hello agente toouse ou de uma variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-128">hello App Insights system uses this key toomap data tooyour Azure resource so you need toospecify it in an environment variable or your code for hello agent toouse.</span></span>  

![Copie a chave de instrumentação](./media/app-insights-nodejs/05-appinsights_ikey_portal.png)

<span data-ttu-id="8d6f3-130">Em seguida, adicione as dependências do aplicativo do tooyour biblioteca agente Olá Node. js via Package. JSON.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-130">Next, add hello Node.js agent library tooyour app's dependencies via package.json.</span></span> <span data-ttu-id="8d6f3-131">Na pasta raiz de saudação do seu aplicativo, execute:</span><span class="sxs-lookup"><span data-stu-id="8d6f3-131">From hello root folder of your app, run:</span></span>

```bash
npm install applicationinsights --save
```

<span data-ttu-id="8d6f3-132">Agora você precisa tooexplicitly carregamento da biblioteca Olá no seu código.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-132">Now you need tooexplicitly load hello library in your code.</span></span> <span data-ttu-id="8d6f3-133">Porque o agente de saudação injeta instrumentação em muitas outras bibliotecas, você deve carregá-lo mais cedo possível, até mesmo antes de outro `require` instruções.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-133">Because hello agent injects instrumentation into many other libraries, you should load it as early as possible, even before other `require` statements.</span></span> <span data-ttu-id="8d6f3-134">tooget iniciado, na parte superior de saudação do primeiro arquivo. js adicionar:</span><span class="sxs-lookup"><span data-stu-id="8d6f3-134">tooget started, at hello top of your first .js file add:</span></span>

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>");
appInsights.start();
```

<span data-ttu-id="8d6f3-135">Olá `setup` método configura a chave de instrumentação da saudação (e, portanto, o recurso do Azure) toobe usado por padrão para itens todos rastreados.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-135">hello `setup` method configures hello instrumentation key (and thus Azure resource) toobe used by default for all tracked items.</span></span> <span data-ttu-id="8d6f3-136">Chamar `start` após a configuração toobegin terminar de coletar e enviar dados de telemetria.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-136">Call `start` after configuration is finished toobegin gathering and sending telemetry data.</span></span>

<span data-ttu-id="8d6f3-137">Você também pode fornecer um ikey por meio da variável de ambiente Olá APPINSIGHTS\_INSTRUMENTATIONKEY em vez de transmiti-lo manualmente muito `setup()` ou `getClient()`.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-137">You can also provide an ikey via hello environment variable APPINSIGHTS\_INSTRUMENTATIONKEY instead of passing it manually too `setup()` or `getClient()`.</span></span> <span data-ttu-id="8d6f3-138">Essa prática permite que você mantenha ikeys fora do código-fonte confirmada e toospecify ikeys de diferentes para diferentes ambientes.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-138">This practice lets you keep ikeys out of committed source code and toospecify different ikeys for different environments.</span></span>

<span data-ttu-id="8d6f3-139">As opções de configuração adicionais estão documentadas a seguir.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-139">Additional configuration options are documented below.</span></span>

<span data-ttu-id="8d6f3-140">Você pode tentar agente Olá sem enviar telemetria definindo a cadeia de caracteres de saudação instrumentação chave tooany não vazio.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-140">You can try hello agent without sending telemetry by setting hello instrumentation key tooany non-empty string.</span></span>

### <span data-ttu-id="8d6f3-141"><a name="monitor"></a>Monitore o seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="8d6f3-141"><a name="monitor"></a> Monitor your app</span></span>

<span data-ttu-id="8d6f3-142">agente Olá reúne automaticamente telemetria sobre o tempo de execução do hello Node. js e alguns módulos comuns de terceiros.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-142">hello agent automatically gathers telemetry about hello Node.js runtime and some common third-party modules.</span></span> <span data-ttu-id="8d6f3-143">Usar toogenerate de agora seu aplicativo alguns desses dados.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-143">Use your application now toogenerate some of this data.</span></span>

<span data-ttu-id="8d6f3-144">Em seguida, no hello [portal do Azure] [ portal] procurar recursos do Application Insights toohello criado anteriormente e procure seu primeiro alguns pontos de dados em Olá visão geral da linha do tempo, como Olá a imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-144">Then, in hello [Azure portal][portal] browse toohello Application Insights resource you created earlier and look for your first few data points in hello Overview timeline, as in hello following image.</span></span> <span data-ttu-id="8d6f3-145">Clique nos gráficos de saudação para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-145">Click through hello charts for more details.</span></span>

![Primeiros pontos de dados](./media/app-insights-nodejs/12-first-perf.png)

<span data-ttu-id="8d6f3-147">Clique em Olá Olá aplicativo mapa botão tooview topologia descoberta para seu aplicativo, como Olá a imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-147">Click hello Application map button tooview hello topology discovered for your app, as in hello following image.</span></span> <span data-ttu-id="8d6f3-148">Clique em componentes no mapa de saudação para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-148">Click through components in hello map for more details.</span></span>

![Mapa de aplicativo simples](./media/app-insights-nodejs/06-appinsights_appmap.png)

<span data-ttu-id="8d6f3-150">Saiba mais sobre o seu aplicativo e solucionar problemas usando Olá outros modos de exibição disponíveis em hello "Investigar" seção.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-150">Learn more about your app and troubleshoot problems using hello other views available under hello "Investigate" section.</span></span>

![Seção Investigar](./media/app-insights-nodejs/07-appinsights_investigate_blades.png)

#### <a name="no-data"></a><span data-ttu-id="8d6f3-152">Não há dados?</span><span class="sxs-lookup"><span data-stu-id="8d6f3-152">No data?</span></span>

<span data-ttu-id="8d6f3-153">Como agente Olá lotes de dados de envio pode ser um atraso antes de itens são exibidos no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-153">Because hello agent batches data for submission there may be a delay before items are displayed in hello portal.</span></span> <span data-ttu-id="8d6f3-154">Se você não vir dados em seu recurso tente algumas das Olá correções a seguir:</span><span class="sxs-lookup"><span data-stu-id="8d6f3-154">If you don't see data in your resource try some of hello following fixes:</span></span>

* <span data-ttu-id="8d6f3-155">Use o aplicativo hello mais; levar mais toogenerate de ações mais telemetria.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-155">Use hello application some more; take more actions toogenerate more telemetry.</span></span>
* <span data-ttu-id="8d6f3-156">Clique em **atualização** no modo de exibição de recursos de portal hello.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-156">Click **Refresh** in hello portal resource view.</span></span> <span data-ttu-id="8d6f3-157">Gráficos automaticamente atualizada se periodicamente mas atualizando força esse toohappen imediatamente.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-157">Charts automatically refresh themselves periodically but refreshing forces this toohappen immediately.</span></span>
* <span data-ttu-id="8d6f3-158">Verifique se [as portas de saídas necessárias](app-insights-ip-addresses.md) estão abertas.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-158">Verify that [needed outgoing ports](app-insights-ip-addresses.md) are open.</span></span>
* <span data-ttu-id="8d6f3-159">Olá abrir [pesquisa](app-insights-diagnostic-search.md) lado a lado e procure eventos individuais.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-159">Open hello [Search](app-insights-diagnostic-search.md) tile and look for individual events.</span></span>
* <span data-ttu-id="8d6f3-160">Verificar Olá [perguntas frequentes sobre][].</span><span class="sxs-lookup"><span data-stu-id="8d6f3-160">Check hello [FAQ][].</span></span>


## <a name="agent-configuration"></a><span data-ttu-id="8d6f3-161">Configuração do Agente</span><span class="sxs-lookup"><span data-stu-id="8d6f3-161">Agent Configuration</span></span>

<span data-ttu-id="8d6f3-162">Estes são os métodos de configuração do agente hello e seus valores padrão.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-162">Following are hello agent's configuration methods and their default values.</span></span>

<span data-ttu-id="8d6f3-163">eventos de correlacionar toofully em um serviço, ser tooset se `.setAutoDependencyCorrelation(true)`.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-163">toofully correlate events in a service, be sure tooset `.setAutoDependencyCorrelation(true)`.</span></span> <span data-ttu-id="8d6f3-164">Isso permite que o agente de saudação tootrack contexto em retornos de chamada assíncronos no Node. js.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-164">This allows hello agent tootrack context across asynchronous callbacks in Node.js.</span></span>

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>")
    .setAutoDependencyCorrelation(false)
    .setAutoCollectRequests(true)
    .setAutoCollectPerformance(true)
    .setAutoCollectExceptions(true)
    .setAutoCollectDependencies(true)
    .start();
```

## <a name="agent-api"></a><span data-ttu-id="8d6f3-165">API de agente</span><span class="sxs-lookup"><span data-stu-id="8d6f3-165">Agent API</span></span>

<!-- TODO: Fully document agent API. -->

<span data-ttu-id="8d6f3-166">Olá API de agente .NET é totalmente descrito [aqui](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="8d6f3-166">hello .NET agent API is fully described [here](app-insights-api-custom-events-metrics.md).</span></span>

<span data-ttu-id="8d6f3-167">Você pode controlar qualquer solicitação, evento, métrica ou exceção usando Olá Node. js Insights do aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-167">You can track any request, event, metric, or exception using hello Application Insights Node.js client.</span></span> <span data-ttu-id="8d6f3-168">Olá exemplo a seguir demonstra alguns Olá APIs disponíveis.</span><span class="sxs-lookup"><span data-stu-id="8d6f3-168">hello following example demonstrates some of hello available APIs.</span></span>

```javascript
let appInsights = require("applicationinsights");
appInsights.setup().start(); // assuming ikey in env var
let client = appInsights.getClient();

client.trackEvent("my custom event", {customProperty: "custom property value"});
client.trackException(new Error("handled exceptions can be logged with this method"));
client.trackMetric("custom metric", 3);
client.trackTrace("trace message");

let http = require("http");
http.createServer( (req, res) => {
  client.trackRequest(req, res); // Place at hello beginning of your request handler
});
```

### <a name="track-your-dependencies"></a><span data-ttu-id="8d6f3-169">Acompanhamento das suas dependências</span><span class="sxs-lookup"><span data-stu-id="8d6f3-169">Track your dependencies</span></span>

```javascript
let appInsights = require("applicationinsights");
let client = appInsights.getClient();

var success = false;
let startTime = Date.now();
// execute dependency call here....
let duration = Date.now() - startTime;
success = true;

client.trackDependency("dependency name", "command name", duration, success);
```

### <a name="add-a-custom-property-tooall-events"></a><span data-ttu-id="8d6f3-170">Adicione eventos de tooall uma propriedade personalizada</span><span class="sxs-lookup"><span data-stu-id="8d6f3-170">Add a custom property tooall events</span></span>

```javascript
appInsights.client.commonProperties = {
    environment: process.env.SOME_ENV_VARIABLE
};
```

### <a name="track-http-get-requests"></a><span data-ttu-id="8d6f3-171">Acompanhamento das solicitações GET HTTP</span><span class="sxs-lookup"><span data-stu-id="8d6f3-171">Track HTTP GET requests</span></span>

```javascript
var server = http.createServer((req, res) => {
    if ( req.method === "GET" ) {
            appInsights.client.trackRequest(req, res);
    }
    // other work here....
    res.end();
});
```

### <a name="track-server-startup-time"></a><span data-ttu-id="8d6f3-172">Tempo de inicialização do servidor de acompanhamento</span><span class="sxs-lookup"><span data-stu-id="8d6f3-172">Track server startup time</span></span>

```javascript
let start = Date.now();
server.on("listening", () => {
    let duration = Date.now() - start;
    appInsights.client.trackMetric("server startup time", duration);
});
```

## <a name="more-resources"></a><span data-ttu-id="8d6f3-173">Mais recursos</span><span class="sxs-lookup"><span data-stu-id="8d6f3-173">More resources</span></span>

* [<span data-ttu-id="8d6f3-174">Monitorar sua telemetria no portal de saudação</span><span class="sxs-lookup"><span data-stu-id="8d6f3-174">Monitor your telemetry in hello portal</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="8d6f3-175">Escrever consultas de análise sobre a telemetria</span><span class="sxs-lookup"><span data-stu-id="8d6f3-175">Write Analytics queries over your telemetry</span></span>](app-insights-analytics-tour.md)

<!--references-->

[portal]: https://portal.azure.com/
[perguntas frequentes sobre]: app-insights-troubleshoot-faq.md
