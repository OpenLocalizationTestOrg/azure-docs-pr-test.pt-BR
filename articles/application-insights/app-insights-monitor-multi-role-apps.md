---
title: "aaaAzure Application Insights oferecem suporte para vários componentes, microservices e contêineres | Microsoft Docs"
description: "Monitoramento de aplicativos que consistem em vários componentes ou funções para desempenho e uso."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: 6185eedf32ec450d7541603b94de6c3dcdf64a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-multi-component-applications-with-application-insights-preview"></a>Monitore aplicativos de vários componentes com o Application Insights (visualização)

Você pode monitorar aplicativos que consistem em vários componentes, funções ou serviços de servidor com [Application Insights do Azure](app-insights-overview.md). integridade de saudação de componentes de saudação e relações de saudação entre eles são exibidos em um mapa de aplicativo único. Você pode rastrear a operações individuais por meio de vários componentes com correlação automática de HTTP. Os diagnósticos do contêiner podem ser integrados e correlacionados à telemetria de aplicativos. Use um único recurso do Application Insights para todos os componentes de saudação do seu aplicativo. 

![Mapa de aplicativos de vários componentes](./media/app-insights-monitor-multi-role-apps/app-map.png)

Podemos usar 'componente' toomean aqui qualquer parte do funcionamento de um aplicativo grande. Por exemplo, um aplicativo comercial comum pode consistir em código de cliente em execução em navegadores da web, falando tooone ou mais serviços de aplicativo web, que por sua vez usam novamente terminar serviços. Componentes de servidor podem ser hospedado no local na nuvem hello, ou podem ser funções da web e de trabalho do Azure ou podem ser executado em contêineres como Docker ou do Service Fabric. 

### <a name="sharing-a-single-application-insights-resource"></a>Compartilhamento um único recurso do Application Insights 

Olá, técnica chave aqui é toosend telemetria de cada componente em seu aplicativo toohello mesmo recurso Application Insights, mas use Olá `cloud_RoleName` componentes toodistinguish de propriedade quando necessário. Olá SDK do Application Insights adiciona Olá `cloud_RoleName` componentes de telemetria toohello propriedade emitir. Por exemplo, a saudação SDK adicionará um nome de site da web ou serviço toohello de nome de função `cloud_RoleName` propriedade. Você pode substituir esse valor com um telemetryinitializer. Olá mapa de aplicativo usa Olá `cloud_RoleName` componentes de saudação propriedade tooidentify no mapa de saudação.

Para obter mais informações sobre como substituir Olá `cloud_RoleName` consulte propriedade [adicionar propriedades: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).  

Em alguns casos, isso pode não ser apropriado e, talvez você prefira toouse de recursos separados para diferentes grupos de componentes. Por exemplo, talvez seja necessário toouse diferentes recursos de gerenciamento ou fins de cobrança. Usar recursos separados significa que você não vir todos os componentes de saudação exibidos em um mapa de aplicativo único; e se você não pode consultar em componentes [análise](app-insights-analytics.md). Você também tem tooset recursos separados de saudação.

Com essa limitação, vamos supor que no restante deste documento hello que você deseja toosend dados de recurso do Application Insights tooone de vários componentes.

## <a name="configure-multi-component-applications"></a>Configurar aplicativos de vários componentes

mapa de um aplicativo de vários componente tooget, é necessário tooachieve essas metas:

* **Instalar a pré-versão mais recente de Olá** pacote do Application Insights em cada componente do aplicativo hello. 
* **Compartilhar um único recurso do Application Insights** para todos os componentes do aplicativo de hello.
* **Habilitar mapa de aplicativos de várias funções** na folha de visualizações de saudação.

Configure cada componente do seu aplicativo usando o método apropriado de saudação para seu tipo. ([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)

### <a name="1-install-hello-latest-pre-release-package"></a>1. Instalar o pacote de pré-lançamento mais recente Olá

Atualizar ou instalar pacotes do Application Insights Olá no projeto Olá para cada componente do servidor. Se você estiver usando o Visual Studio:

1. Clique o botão direito do mouse no projeto e selecione **Gerenciar Pacotes NuGet**. 
2. Selecione **Incluir pré-lançamento**.
3. Se pacotes do Application Insights aparecerem nas atualizações, selecione-os. 

    Caso contrário, procurar e instalar o pacote de saudação apropriado:
    
    * Microsoft.ApplicationInsights.WindowsServer
    * Microsoft.ApplicationInsights.ServiceFabric – para componentes em execução como executáveis de convidado e executando um aplicativo do Service Fabric em contêineres do Docker
    * Microsoft.ApplicationInsights.ServiceFabric.Native - para serviços confiáveis em aplicativos no Service Fabric
    * Microsoft.ApplicationInsights.Kubernetes para componentes em execução no Docker e nos Kubernetes

### <a name="2-share-a-single-application-insights-resource"></a>2. Compartilhamento de um único recurso do Application Insights

* No Visual Studio, clique o botão direito do mouse em um projeto e selecione **Configurar o Application Insights** ou **Application Insights > Configuração**. Para o primeiro projeto de Olá, use Olá Assistente toocreate um recurso do Application Insights. Para projetos subsequentes, selecione Olá mesmo recurso.
* Se não houver nenhum menu do Application Insights, configure manualmente:

   1. Em [portal do Azure](https://portal,azure.com), abrir o recurso do Application Insights Olá você já criou para outro componente.
   2. Na folha de visão geral de saudação, guia Olá abrir menu suspenso do Essentials e Olá cópia **chave de instrumentação.**
   3. No seu projeto, abra ApplicationInsights.config e insira: `<InstrumentationKey>your copied key</InstrumentationKey>`

![Copiar Olá instrumentação chave toohello. config arquivo](./media/app-insights-monitor-multi-role-apps/copy-instrumentation-key.png)


### <a name="3-enable-multi-role-application-map"></a>3. Habilitação do mapa de aplicativo de várias funções

No portal do Azure de Olá, abra o recurso de saudação para seu aplicativo. Na folha de visualizações hello, habilitar *mapa de aplicativos de várias funções*.

### <a name="4-enable-docker-metrics-optional"></a>4. Habilitação das métricas de Docker (opcional) 

Se um componente é executado em um Docker hospedado em uma VM do Windows Azure, você pode coletar métricas adicionais de contêiner de saudação. Insira isso no seu arquivo de configuração de [diagnóstico do Azure](../monitoring-and-diagnostics/azure-diagnostics.md):

```
"DiagnosticMonitorConfiguration": {
        ...
        "sinks": "applicationInsights",
        "DockerSources": {
                "Stats": {
                    "enabled": true,
                    "sampleRate": "PT1M"
                }
            },
        ...
    }
    ...   
    "SinksConfig": {
        "Sink": [{
            "name": "applicationInsights",
            "ApplicationInsights": "<your instrumentation key here>"
        }]
    }
    ...
}

```

## <a name="use-cloudrolename-tooseparate-components"></a>Usar cloud_RoleName tooseparate componentes

Olá `cloud_RoleName` propriedade é telemetria tooall anexado. Ele identifica o componente de saudação - Olá função ou um serviço - que se origina a telemetria de saudação. (É não Olá mesmo como cloud_RoleInstance, que separa idênticas funções que são executados em paralelo em vários processos do servidor ou computadores.)

No portal de saudação, você pode filtrar ou segmentar sua telemetria usando essa propriedade. Neste exemplo, folha de falhas de saudação é filtrado tooshow apenas informações do serviço de front-end web Olá, filtragem de falhas de back-end de API do CRM Olá:

![Gráfico de métricas segmentado por nome de função de nuvem](./media/app-insights-monitor-multi-role-apps/cloud-role-name.png)

## <a name="trace-operations-between-components"></a>Rastrear operações entre componentes

Você pode rastrear a partir de um componente tooanother, chamadas de saudação feitas durante o processamento de uma operação individual.


![Mostrar telemetria para operação](./media/app-insights-monitor-multi-role-apps/show-telemetry-for-operation.png)

Clique em lista correlacionados de tooa de telemetria para esta operação no servidor de front-end web hello e na API de back-end de saudação:

![Pesquisar entre os componentes](./media/app-insights-monitor-multi-role-apps/search-across-components.png)


## <a name="next-steps"></a>Próximas etapas

* [Separação da telemetria de desenvolvimento, teste e produção](app-insights-separate-resources.md)
