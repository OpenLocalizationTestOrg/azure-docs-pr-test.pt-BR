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
# <a name="monitor-your-nodejs-services-and-apps-with-application-insights"></a>Como monitorar seus serviços do Node.js e aplicativos com o Application Insights

[Informações de aplicativo do Azure](app-insights-overview.md) monitora seus componentes e serviços de back-end depois de implantá-las toohelp você [detectar e diagnosticar rapidamente problemas de desempenho e outros](app-insights-detect-triage-diagnose.md). Use-o nos serviços do Node.js hospedado em qualquer lugar: seu datacenter, VMs do Azure, aplicativos Web e até mesmo em outras nuvens públicas.

tooreceive, armazenar e explorar os dados de monitoramentos, execute Olá seguindo as instruções tooinclude um agente em seu código e configurar um recurso do Application Insights correspondente no Azure. Agente de saudação envia recurso toothat de dados para análise posterior e exploração.

Agente de Node. js Olá automaticamente pode monitorar entrada e saída HTTP solicitações, várias métricas de sistema e exceções. A partir da v0.20, ele também pode monitorar alguns pacotes de terceiros comuns como `mongodb`, `mysql` e `redis`. Todos os eventos relacionados a solicitação HTTP de entrada tooan são correlacionadas para solução de problemas mais rapidamente.

Você pode monitorar outros aspectos do seu aplicativo e sistema por instrumentação-las manualmente usando a API de agente Olá descrita posteriormente.

![Gráficos de exemplo de monitoramento de desempenho](./media/app-insights-nodejs/10-perf.png)

## <a name="getting-started"></a>Introdução

Vamos estudar a configuração de monitoramento para um serviço ou aplicativo.

### <a name="resource"></a>Configuração de um recurso do Application Insights

**Antes de iniciar**, verifique se você tem uma assinatura do Azure ou [obtenha uma gratuitamente][azure-free-offer]. Se sua organização já tiver uma assinatura do Azure, um administrador pode seguir [estas instruções] [ add-aad-user] tooadd tooit você.

[azure-free-offer]: https://azure.microsoft.com/en-us/free/
[add-aad-user]: https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-create-azure-portal

Agora, faça logon no toohello [portal do Azure] [ portal] e crie um recurso do Application Insights, conforme ilustrado no seguinte Olá - clique em "Novo" > "Developer tools" > "Application Insights". recurso de saudação inclui um ponto de extremidade para receber dados de telemetria, armazenamento de dados, salvar relatórios e painéis, regras e configuração de alerta e muito mais.

![Criação de um recurso do Application Insights](./media/app-insights-nodejs/03-new_appinsights_resource.png)

Na página de criação do recurso hello, escolha "Aplicativo Node. js" da saudação aplicativo lista suspensa tipo. tipo de aplicativo Hello determina o conjunto padrão de saudação de painéis e relatórios criados para você. Na verdade, não há com que se preocupar, qualquer recurso do Application Insights pode coletar dados de qualquer idioma e plataforma.

![Formulário de recursos do Application Insights novo](./media/app-insights-nodejs/04-create_appinsights_resource.png)

### <a name="agent"></a>Configurar o agente do hello Node. js

Agora ela é um agente de saudação do tempo tooinclude em seu aplicativo para que ele possa coletar dados.
Inicie a cópia da chave de instrumentação do recurso (daqui por diante chamado tooas seu `ikey`) do portal Olá conforme mostrado abaixo. Olá ideias de aplicativo sistema usa essa tooyour de dados toomap principais recursos do Azure para que seja necessário toospecify-lo no seu código para hello agente toouse ou de uma variável de ambiente.  

![Copie a chave de instrumentação](./media/app-insights-nodejs/05-appinsights_ikey_portal.png)

Em seguida, adicione as dependências do aplicativo do tooyour biblioteca agente Olá Node. js via Package. JSON. Na pasta raiz de saudação do seu aplicativo, execute:

```bash
npm install applicationinsights --save
```

Agora você precisa tooexplicitly carregamento da biblioteca Olá no seu código. Porque o agente de saudação injeta instrumentação em muitas outras bibliotecas, você deve carregá-lo mais cedo possível, até mesmo antes de outro `require` instruções. tooget iniciado, na parte superior de saudação do primeiro arquivo. js adicionar:

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>");
appInsights.start();
```

Olá `setup` método configura a chave de instrumentação da saudação (e, portanto, o recurso do Azure) toobe usado por padrão para itens todos rastreados. Chamar `start` após a configuração toobegin terminar de coletar e enviar dados de telemetria.

Você também pode fornecer um ikey por meio da variável de ambiente Olá APPINSIGHTS\_INSTRUMENTATIONKEY em vez de transmiti-lo manualmente muito `setup()` ou `getClient()`. Essa prática permite que você mantenha ikeys fora do código-fonte confirmada e toospecify ikeys de diferentes para diferentes ambientes.

As opções de configuração adicionais estão documentadas a seguir.

Você pode tentar agente Olá sem enviar telemetria definindo a cadeia de caracteres de saudação instrumentação chave tooany não vazio.

### <a name="monitor"></a>Monitore o seu aplicativo

agente Olá reúne automaticamente telemetria sobre o tempo de execução do hello Node. js e alguns módulos comuns de terceiros. Usar toogenerate de agora seu aplicativo alguns desses dados.

Em seguida, no hello [portal do Azure] [ portal] procurar recursos do Application Insights toohello criado anteriormente e procure seu primeiro alguns pontos de dados em Olá visão geral da linha do tempo, como Olá a imagem a seguir. Clique nos gráficos de saudação para obter mais detalhes.

![Primeiros pontos de dados](./media/app-insights-nodejs/12-first-perf.png)

Clique em Olá Olá aplicativo mapa botão tooview topologia descoberta para seu aplicativo, como Olá a imagem a seguir. Clique em componentes no mapa de saudação para obter mais detalhes.

![Mapa de aplicativo simples](./media/app-insights-nodejs/06-appinsights_appmap.png)

Saiba mais sobre o seu aplicativo e solucionar problemas usando Olá outros modos de exibição disponíveis em hello "Investigar" seção.

![Seção Investigar](./media/app-insights-nodejs/07-appinsights_investigate_blades.png)

#### <a name="no-data"></a>Não há dados?

Como agente Olá lotes de dados de envio pode ser um atraso antes de itens são exibidos no portal de saudação. Se você não vir dados em seu recurso tente algumas das Olá correções a seguir:

* Use o aplicativo hello mais; levar mais toogenerate de ações mais telemetria.
* Clique em **atualização** no modo de exibição de recursos de portal hello. Gráficos automaticamente atualizada se periodicamente mas atualizando força esse toohappen imediatamente.
* Verifique se [as portas de saídas necessárias](app-insights-ip-addresses.md) estão abertas.
* Olá abrir [pesquisa](app-insights-diagnostic-search.md) lado a lado e procure eventos individuais.
* Verificar Olá [perguntas frequentes sobre][].


## <a name="agent-configuration"></a>Configuração do Agente

Estes são os métodos de configuração do agente hello e seus valores padrão.

eventos de correlacionar toofully em um serviço, ser tooset se `.setAutoDependencyCorrelation(true)`. Isso permite que o agente de saudação tootrack contexto em retornos de chamada assíncronos no Node. js.

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

## <a name="agent-api"></a>API de agente

<!-- TODO: Fully document agent API. -->

Olá API de agente .NET é totalmente descrito [aqui](app-insights-api-custom-events-metrics.md).

Você pode controlar qualquer solicitação, evento, métrica ou exceção usando Olá Node. js Insights do aplicativo cliente. Olá exemplo a seguir demonstra alguns Olá APIs disponíveis.

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

### <a name="track-your-dependencies"></a>Acompanhamento das suas dependências

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

### <a name="add-a-custom-property-tooall-events"></a>Adicione eventos de tooall uma propriedade personalizada

```javascript
appInsights.client.commonProperties = {
    environment: process.env.SOME_ENV_VARIABLE
};
```

### <a name="track-http-get-requests"></a>Acompanhamento das solicitações GET HTTP

```javascript
var server = http.createServer((req, res) => {
    if ( req.method === "GET" ) {
            appInsights.client.trackRequest(req, res);
    }
    // other work here....
    res.end();
});
```

### <a name="track-server-startup-time"></a>Tempo de inicialização do servidor de acompanhamento

```javascript
let start = Date.now();
server.on("listening", () => {
    let duration = Date.now() - start;
    appInsights.client.trackMetric("server startup time", duration);
});
```

## <a name="more-resources"></a>Mais recursos

* [Monitorar sua telemetria no portal de saudação](app-insights-dashboards.md)
* [Escrever consultas de análise sobre a telemetria](app-insights-analytics-tour.md)

<!--references-->

[portal]: https://portal.azure.com/
[perguntas frequentes sobre]: app-insights-troubleshoot-faq.md
