---
title: "Como monitorar os serviços Node.js com o Application Insights do Azure | Microsoft Docs"
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
ms.openlocfilehash: ee65207e546c7050cc7bf35c36624fc49ad9eec4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-your-nodejs-services-and-apps-with-application-insights"></a><span data-ttu-id="2defa-103">Como monitorar seus serviços do Node.js e aplicativos com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="2defa-103">Monitor your Node.js services and apps with Application Insights</span></span>

<span data-ttu-id="2defa-104">O [Application Insights do Azure](app-insights-overview.md) monitora seus componentes e serviços de back-end depois de implantá-los para ajudá-lo a [detectar e diagnosticar rapidamente problemas de desempenho, entre outros](app-insights-detect-triage-diagnose.md).</span><span class="sxs-lookup"><span data-stu-id="2defa-104">[Azure Application Insights](app-insights-overview.md) monitors your backend services and components after you deploy them to help you [discover and rapidly diagnose performance and other issues](app-insights-detect-triage-diagnose.md).</span></span> <span data-ttu-id="2defa-105">Use-o nos serviços do Node.js hospedado em qualquer lugar: seu datacenter, VMs do Azure, aplicativos Web e até mesmo em outras nuvens públicas.</span><span class="sxs-lookup"><span data-stu-id="2defa-105">Use it for Node.js services hosted anywhere: your datacenter, Azure VMs and Web Apps, and even other public clouds.</span></span>

<span data-ttu-id="2defa-106">Para receber, armazenar e explorar os dados de monitoramento, siga as instruções a seguir para incluir um agente em seu código e configurar um recurso do Application Insights correspondente no Azure.</span><span class="sxs-lookup"><span data-stu-id="2defa-106">To receive, store, and explore your monitoring data, follow the following instructions to include an agent in your code and set up a corresponding Application Insights resource in Azure.</span></span> <span data-ttu-id="2defa-107">O agente envia dados a esse recurso para análise posterior e exploração.</span><span class="sxs-lookup"><span data-stu-id="2defa-107">The agent sends data to that resource for further analysis and exploration.</span></span>

<span data-ttu-id="2defa-108">O agente do Node.js pode monitorar automaticamente as solicitações HTTP de entrada e saída, várias métricas de sistema e exceções.</span><span class="sxs-lookup"><span data-stu-id="2defa-108">The Node.js agent can automatically monitor incoming and outgoing HTTP requests, several system metrics, and exceptions.</span></span> <span data-ttu-id="2defa-109">A partir da v0.20, ele também pode monitorar alguns pacotes de terceiros comuns como `mongodb`, `mysql` e `redis`.</span><span class="sxs-lookup"><span data-stu-id="2defa-109">Beginning in v0.20, it can also monitor some common third-party packages such as `mongodb`, `mysql`, and `redis`.</span></span> <span data-ttu-id="2defa-110">Todos os eventos relacionados a uma solicitação HTTP de entrada são correlacionados para solução de problemas mais rápida.</span><span class="sxs-lookup"><span data-stu-id="2defa-110">All events related to an incoming HTTP request are correlated for faster troubleshooting.</span></span>

<span data-ttu-id="2defa-111">Você pode monitorar outros aspectos do seu aplicativo e do sistema pela instrumentação manual usando a API do agente descrito posteriormente.</span><span class="sxs-lookup"><span data-stu-id="2defa-111">You can monitor more aspects of your app and system by manually instrumenting them using the agent API described later.</span></span>

![Gráficos de exemplo de monitoramento de desempenho](./media/app-insights-nodejs/10-perf.png)

## <a name="getting-started"></a><span data-ttu-id="2defa-113">Introdução</span><span class="sxs-lookup"><span data-stu-id="2defa-113">Getting Started</span></span>

<span data-ttu-id="2defa-114">Vamos estudar a configuração de monitoramento para um serviço ou aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2defa-114">Let's step through setting up monitoring for an app or service.</span></span>

### <span data-ttu-id="2defa-115"><a name="resource"></a>Configuração de um recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="2defa-115"><a name="resource"></a> Set up an App Insights resource</span></span>

<span data-ttu-id="2defa-116">**Antes de iniciar**, verifique se você tem uma assinatura do Azure ou [obtenha uma gratuitamente][azure-free-offer].</span><span class="sxs-lookup"><span data-stu-id="2defa-116">**Before you start**, make sure you have an Azure subscription or [get a new one for free][azure-free-offer].</span></span> <span data-ttu-id="2defa-117">Se sua organização já tiver uma assinatura do Azure, um administrador pode seguir [estas instruções][add-aad-user] para adicioná-lo a ela.</span><span class="sxs-lookup"><span data-stu-id="2defa-117">If your organization already has an Azure subscription, an administrator can follow [these instructions][add-aad-user] to add you to it.</span></span>

[azure-free-offer]: https://azure.microsoft.com/en-us/free/
[add-aad-user]: https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-create-azure-portal

<span data-ttu-id="2defa-118">Faça logon no [portal do Azure][portal] e crie um recurso no Application Insights, conforme ilustrado a seguir - clique em "Novo" > "Ferramentas do desenvolvedor" > "Application Insights".</span><span class="sxs-lookup"><span data-stu-id="2defa-118">Now log in to the [Azure portal][portal] and create an Application Insights resource as illustrated in the following - click "New" > "Developer tools" > "Application Insights".</span></span> <span data-ttu-id="2defa-119">O recurso inclui um ponto de extremidade para receber dados de telemetria, armazenamento para esses dados, painéis e relatórios salvos, configurações de alerta e regra e muito mais.</span><span class="sxs-lookup"><span data-stu-id="2defa-119">The resource includes an endpoint for receiving telemetry data, storage for this data, saved reports and dashboards, rule and alert configuration, and more.</span></span>

![Criação de um recurso do Application Insights](./media/app-insights-nodejs/03-new_appinsights_resource.png)

<span data-ttu-id="2defa-121">Na página de criação de recursos, selecione "Aplicativo do Node.js" a partir do menu suspenso Tipo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2defa-121">On the resource creation page, choose "Node.js Application" from the application type drop-down.</span></span> <span data-ttu-id="2defa-122">O tipo de aplicativo determina o conjunto-padrão de painéis e relatórios criados para você.</span><span class="sxs-lookup"><span data-stu-id="2defa-122">The app type determines the default set of dashboards and reports created for you.</span></span> <span data-ttu-id="2defa-123">Na verdade, não há com que se preocupar, qualquer recurso do Application Insights pode coletar dados de qualquer idioma e plataforma.</span><span class="sxs-lookup"><span data-stu-id="2defa-123">Don't worry though, any App Insights resource can in fact collect data from any language and platform.</span></span>

![Formulário de recursos do Application Insights novo](./media/app-insights-nodejs/04-create_appinsights_resource.png)

### <span data-ttu-id="2defa-125"><a name="agent"></a>Configuração do agente do Node.js</span><span class="sxs-lookup"><span data-stu-id="2defa-125"><a name="agent"></a> Set up the Node.js agent</span></span>

<span data-ttu-id="2defa-126">Agora é hora de incluir o agente em seu aplicativo para que ele possa coletar dados.</span><span class="sxs-lookup"><span data-stu-id="2defa-126">Now it's time to include the agent in your app so it can gather data.</span></span>
<span data-ttu-id="2defa-127">Para começar, copie a chave de instrumentação do recurso (doravante referidos como seu `ikey`) do portal, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="2defa-127">Start by copying your resource's Instrumentation Key (hereinafter referred to as your `ikey`) from the portal as shown below.</span></span> <span data-ttu-id="2defa-128">O sistema do Application Insights usa essa chave para mapear dados para os seus recursos do Azure, por isso você precisa especificá-lo em uma variável de ambiente ou seu código para que o agente o use.</span><span class="sxs-lookup"><span data-stu-id="2defa-128">The App Insights system uses this key to map data to your Azure resource so you need to specify it in an environment variable or your code for the agent to use.</span></span>  

![Copie a chave de instrumentação](./media/app-insights-nodejs/05-appinsights_ikey_portal.png)

<span data-ttu-id="2defa-130">Em seguida, adicione a biblioteca de agente do Node.js para as dependências do seu aplicativo por meio do package.json.</span><span class="sxs-lookup"><span data-stu-id="2defa-130">Next, add the Node.js agent library to your app's dependencies via package.json.</span></span> <span data-ttu-id="2defa-131">Na pasta raiz do seu aplicativo, execute:</span><span class="sxs-lookup"><span data-stu-id="2defa-131">From the root folder of your app, run:</span></span>

```bash
npm install applicationinsights --save
```

<span data-ttu-id="2defa-132">Agora você precisa carregar explicitamente a biblioteca em seu código.</span><span class="sxs-lookup"><span data-stu-id="2defa-132">Now you need to explicitly load the library in your code.</span></span> <span data-ttu-id="2defa-133">Como o agente injeta instrumentação em muitas outras bibliotecas, você deve carregá-lo o mais cedo possível, mesmo antes de outras instruções `require`.</span><span class="sxs-lookup"><span data-stu-id="2defa-133">Because the agent injects instrumentation into many other libraries, you should load it as early as possible, even before other `require` statements.</span></span> <span data-ttu-id="2defa-134">Para começar, na parte superior do seu primeiro arquivo .js, adicione:</span><span class="sxs-lookup"><span data-stu-id="2defa-134">To get started, at the top of your first .js file add:</span></span>

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>");
appInsights.start();
```

<span data-ttu-id="2defa-135">O método `setup` configura a chave de instrumentação (e, portanto, os recursos do Azure) a ser usada por padrão para todos os itens rastreados.</span><span class="sxs-lookup"><span data-stu-id="2defa-135">The `setup` method configures the instrumentation key (and thus Azure resource) to be used by default for all tracked items.</span></span> <span data-ttu-id="2defa-136">Chame `start` após a conclusão da configuração para começar a coletar e enviar os dados de telemetria.</span><span class="sxs-lookup"><span data-stu-id="2defa-136">Call `start` after configuration is finished to begin gathering and sending telemetry data.</span></span>

<span data-ttu-id="2defa-137">Você também pode fornecer um ikey por meio da variável de ambiente APPINSIGHTS\_INSTRUMENTATIONKEY em vez de transmiti-lo manualmente ao `setup()` ou `getClient()`.</span><span class="sxs-lookup"><span data-stu-id="2defa-137">You can also provide an ikey via the environment variable APPINSIGHTS\_INSTRUMENTATIONKEY instead of passing it manually to  `setup()` or `getClient()`.</span></span> <span data-ttu-id="2defa-138">Essa prática permite manter ikeys fora do código-fonte comprometido e especificar ikeys diferentes para ambientes diferentes.</span><span class="sxs-lookup"><span data-stu-id="2defa-138">This practice lets you keep ikeys out of committed source code and to specify different ikeys for different environments.</span></span>

<span data-ttu-id="2defa-139">As opções de configuração adicionais estão documentadas a seguir.</span><span class="sxs-lookup"><span data-stu-id="2defa-139">Additional configuration options are documented below.</span></span>

<span data-ttu-id="2defa-140">Você pode tentar o agente sem enviar telemetria definindo a chave de instrumentação para qualquer cadeia de caracteres não vazia.</span><span class="sxs-lookup"><span data-stu-id="2defa-140">You can try the agent without sending telemetry by setting the instrumentation key to any non-empty string.</span></span>

### <span data-ttu-id="2defa-141"><a name="monitor"></a>Monitore o seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="2defa-141"><a name="monitor"></a> Monitor your app</span></span>

<span data-ttu-id="2defa-142">O agente reúne automaticamente a telemetria sobre o tempo de execução do Node.js e alguns módulos de terceiros comuns.</span><span class="sxs-lookup"><span data-stu-id="2defa-142">The agent automatically gathers telemetry about the Node.js runtime and some common third-party modules.</span></span> <span data-ttu-id="2defa-143">Use o aplicativo agora para gerar alguns desses dados.</span><span class="sxs-lookup"><span data-stu-id="2defa-143">Use your application now to generate some of this data.</span></span>

<span data-ttu-id="2defa-144">Em seguida, no [portal do Azure][portal], navegue até o recurso Application Insights que você criou anteriormente e procure alguns dos seus primeiros pontos de dados na linha do tempo da visão geral, como mostra a imagem seguinte.</span><span class="sxs-lookup"><span data-stu-id="2defa-144">Then, in the [Azure portal][portal] browse to the Application Insights resource you created earlier and look for your first few data points in the Overview timeline, as in the following image.</span></span> <span data-ttu-id="2defa-145">Clique nos gráficos para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="2defa-145">Click through the charts for more details.</span></span>

![Primeiros pontos de dados](./media/app-insights-nodejs/12-first-perf.png)

<span data-ttu-id="2defa-147">Clique no botão de mapa de aplicativo para exibir a topologia de descoberta para seu aplicativo, como mostra a imagem seguinte.</span><span class="sxs-lookup"><span data-stu-id="2defa-147">Click the Application map button to view the topology discovered for your app, as in the following image.</span></span> <span data-ttu-id="2defa-148">Clique em componentes no mapa para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="2defa-148">Click through components in the map for more details.</span></span>

![Mapa de aplicativo simples](./media/app-insights-nodejs/06-appinsights_appmap.png)

<span data-ttu-id="2defa-150">Saiba mais sobre seu aplicativo e como solucionar problemas usando as exibições disponíveis na seção "Investigar".</span><span class="sxs-lookup"><span data-stu-id="2defa-150">Learn more about your app and troubleshoot problems using the other views available under the "Investigate" section.</span></span>

![Seção Investigar](./media/app-insights-nodejs/07-appinsights_investigate_blades.png)

#### <a name="no-data"></a><span data-ttu-id="2defa-152">Não há dados?</span><span class="sxs-lookup"><span data-stu-id="2defa-152">No data?</span></span>

<span data-ttu-id="2defa-153">Como o agente envia lotes de dados, pode haver um atraso antes de os itens serem exibidos no portal.</span><span class="sxs-lookup"><span data-stu-id="2defa-153">Because the agent batches data for submission there may be a delay before items are displayed in the portal.</span></span> <span data-ttu-id="2defa-154">Se você não visualizar os dados em seu recurso tente algumas das seguintes correções:</span><span class="sxs-lookup"><span data-stu-id="2defa-154">If you don't see data in your resource try some of the following fixes:</span></span>

* <span data-ttu-id="2defa-155">Use mais o aplicativo; execute mais ações para gerar mais telemetria.</span><span class="sxs-lookup"><span data-stu-id="2defa-155">Use the application some more; take more actions to generate more telemetry.</span></span>
* <span data-ttu-id="2defa-156">Clique em **Atualizar** no modo de exibição de recursos do portal.</span><span class="sxs-lookup"><span data-stu-id="2defa-156">Click **Refresh** in the portal resource view.</span></span> <span data-ttu-id="2defa-157">Periodicamente, os gráficos se atualizam automaticamente, mas se quiser atualizá-los imediatamente, clique em atualizar.</span><span class="sxs-lookup"><span data-stu-id="2defa-157">Charts automatically refresh themselves periodically but refreshing forces this to happen immediately.</span></span>
* <span data-ttu-id="2defa-158">Verifique se [as portas de saídas necessárias](app-insights-ip-addresses.md) estão abertas.</span><span class="sxs-lookup"><span data-stu-id="2defa-158">Verify that [needed outgoing ports](app-insights-ip-addresses.md) are open.</span></span>
* <span data-ttu-id="2defa-159">Abra o bloco [Pesquisar](app-insights-diagnostic-search.md) e procure eventos individuais.</span><span class="sxs-lookup"><span data-stu-id="2defa-159">Open the [Search](app-insights-diagnostic-search.md) tile and look for individual events.</span></span>
* <span data-ttu-id="2defa-160">Leia as [Perguntas Frequentes][].</span><span class="sxs-lookup"><span data-stu-id="2defa-160">Check the [FAQ][].</span></span>


## <a name="agent-configuration"></a><span data-ttu-id="2defa-161">Configuração do Agente</span><span class="sxs-lookup"><span data-stu-id="2defa-161">Agent Configuration</span></span>

<span data-ttu-id="2defa-162">A seguir estão os métodos de configuração do agente e seus valores-padrão.</span><span class="sxs-lookup"><span data-stu-id="2defa-162">Following are the agent's configuration methods and their default values.</span></span>

<span data-ttu-id="2defa-163">Para correlacionar totalmente eventos em um serviço, você deve definir `.setAutoDependencyCorrelation(true)`.</span><span class="sxs-lookup"><span data-stu-id="2defa-163">To fully correlate events in a service, be sure to set `.setAutoDependencyCorrelation(true)`.</span></span> <span data-ttu-id="2defa-164">Isso permite que o agente controle o contexto em retornos de chamada assíncronas no Node.js.</span><span class="sxs-lookup"><span data-stu-id="2defa-164">This allows the agent to track context across asynchronous callbacks in Node.js.</span></span>

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

## <a name="agent-api"></a><span data-ttu-id="2defa-165">API de agente</span><span class="sxs-lookup"><span data-stu-id="2defa-165">Agent API</span></span>

<!-- TODO: Fully document agent API. -->

<span data-ttu-id="2defa-166">Confira a descrição completa sobre a API do agente .NET [aqui](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="2defa-166">The .NET agent API is fully described [here](app-insights-api-custom-events-metrics.md).</span></span>

<span data-ttu-id="2defa-167">Você pode acompanhar qualquer solicitação, evento, métrica ou exceção usando o cliente do Node.js do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2defa-167">You can track any request, event, metric, or exception using the Application Insights Node.js client.</span></span> <span data-ttu-id="2defa-168">O exemplo a seguir demonstra algumas das APIs disponíveis.</span><span class="sxs-lookup"><span data-stu-id="2defa-168">The following example demonstrates some of the available APIs.</span></span>

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
  client.trackRequest(req, res); // Place at the beginning of your request handler
});
```

### <a name="track-your-dependencies"></a><span data-ttu-id="2defa-169">Acompanhamento das suas dependências</span><span class="sxs-lookup"><span data-stu-id="2defa-169">Track your dependencies</span></span>

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

### <a name="add-a-custom-property-to-all-events"></a><span data-ttu-id="2defa-170">Adição de uma propriedade personalizada para todos os eventos</span><span class="sxs-lookup"><span data-stu-id="2defa-170">Add a custom property to all events</span></span>

```javascript
appInsights.client.commonProperties = {
    environment: process.env.SOME_ENV_VARIABLE
};
```

### <a name="track-http-get-requests"></a><span data-ttu-id="2defa-171">Acompanhamento das solicitações GET HTTP</span><span class="sxs-lookup"><span data-stu-id="2defa-171">Track HTTP GET requests</span></span>

```javascript
var server = http.createServer((req, res) => {
    if ( req.method === "GET" ) {
            appInsights.client.trackRequest(req, res);
    }
    // other work here....
    res.end();
});
```

### <a name="track-server-startup-time"></a><span data-ttu-id="2defa-172">Tempo de inicialização do servidor de acompanhamento</span><span class="sxs-lookup"><span data-stu-id="2defa-172">Track server startup time</span></span>

```javascript
let start = Date.now();
server.on("listening", () => {
    let duration = Date.now() - start;
    appInsights.client.trackMetric("server startup time", duration);
});
```

## <a name="more-resources"></a><span data-ttu-id="2defa-173">Mais recursos</span><span class="sxs-lookup"><span data-stu-id="2defa-173">More resources</span></span>

* [<span data-ttu-id="2defa-174">Monitorar sua telemetria no portal</span><span class="sxs-lookup"><span data-stu-id="2defa-174">Monitor your telemetry in the portal</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="2defa-175">Escrever consultas de análise sobre a telemetria</span><span class="sxs-lookup"><span data-stu-id="2defa-175">Write Analytics queries over your telemetry</span></span>](app-insights-analytics-tour.md)

<!--references-->

[portal]: https://portal.azure.com/
<span data-ttu-id="2defa-176">[Perguntas Frequentes]: app-insights-troubleshoot-faq.md</span><span class="sxs-lookup"><span data-stu-id="2defa-176">[FAQ]: app-insights-troubleshoot-faq.md</span></span>
