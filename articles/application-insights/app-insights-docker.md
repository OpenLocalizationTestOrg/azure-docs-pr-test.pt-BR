---
title: aplicativos de Docker aaaMonitor no Azure Application Insights | Microsoft Docs
description: "Exceções, eventos e contadores de desempenho de docker podem ser exibidas no Application Insights, juntamente com telemetria de saudação de saudação em contêineres de aplicativos."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 27a3083d-d67f-4a07-8f3c-4edb65a0a685
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 9aaf1076bae25485a396db1bb3dcd13bccd87c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-docker-applications-in-application-insights"></a>Monitorar aplicativos do Docker no Application Insights
Os eventos de ciclo de vida e os contadores de desempenho dos contêineres [Docker](https://www.docker.com/) podem ser representados em gráfico no Application Insights. Instalar Olá [Application Insights](app-insights-overview.md) imagem em um contêiner em seu host e ele exibirá contadores de desempenho para o host de saudação, bem como para Olá outras imagens.

Com o Docker, você distribui os aplicativos em contêineres leves com todas as dependências. Eles serão executados em qualquer máquina host que executa um Mecanismo de Docker.

Quando você executa Olá [imagem Application Insights](https://hub.docker.com/r/microsoft/applicationinsights/) no host do Docker, você obtém esses benefícios:

* Ciclo de vida telemetria sobre todos os contêineres de saudação em execução no host de saudação - Iniciar, parar e assim por diante.
* Contadores de desempenho para todos os contêineres de saudação. CPU, memória, uso da rede e muito mais.
* Se você [instalado o SDK do Application Insights para Java](app-insights-java-live.md) em aplicativos de saudação em execução em contêineres hello, toda a telemetria Olá desses aplicativos terão propriedades adicionais que identifica o contêiner hello e o computador host. Portanto, por exemplo, se você tiver instâncias de um aplicativo em execução em mais de um host, poderá filtrar a telemetria do aplicativo pelo host com facilidade.

![exemplo](./media/app-insights-docker/00.png)

## <a name="set-up-your-application-insights-resource"></a>Configurar seu recurso do Application Insights
1. Entrar no [portal do Microsoft Azure](https://azure.com) e abrir o recurso do Application Insights Olá para seu aplicativo; ou [criar um novo](app-insights-create-new-resource.md). 
   
    *Qual recurso devo usar?* Se Olá aplicativos em execução no host do foram desenvolvidos por outra pessoa, você precisará de muito[criar um novo recurso do Application Insights](app-insights-create-new-resource.md). Isso é onde você pode exibir e analisar a telemetria de saudação. (Selecione 'Geral' para o tipo de aplicativo hello.)
   
    Mas se você for desenvolvedor Olá Olá aplicativos, em seguida, esperamos que você [adicionado SDK do Application Insights](app-insights-java-live.md) tooeach deles. Se eles são todos os componentes realmente de um aplicativo de negócios único, em seguida, você pode configurar recursos de tooone telemetria toosend para todos eles, e você usará esses mesmo recurso toodisplay Olá Docker do ciclo de vida e dados de desempenho. 
   
    Um terceiro cenário é que você desenvolveu a maioria dos aplicativos hello, mas você estiver usando recursos separados toodisplay sua telemetria. Nesse caso, você provavelmente também deseja toocreate um recurso separado para Olá dados Docker. 
2. Adicionar bloco de Docker Olá: escolha **Adicionar bloco**, arraste o bloco de Docker de saudação da Galeria hello e, em seguida, clique em **feito**. 
   
    ![exemplo](./media/app-insights-docker/03.png)
3. Clique em Olá **Essentials** suspenso e copie Olá chave de instrumentação. Use este Olá tootell SDK onde toosend sua telemetria.

    ![exemplo](./media/app-insights-docker/02-props.png)

Mantenha essa janela do navegador útil, pois você voltaremos tooit assim toolook em sua telemetria.

## <a name="run-hello-application-insights-monitor-on-your-host"></a>Executar o monitor do Application Insights Olá em seu host
Agora que temos em algum lugar da telemetria do toodisplay Olá, você pode configurar o aplicativo em contêineres de saudação que coletará e enviá-lo.

1. Conecte-se o host do Docker tooyour. 
2. Edite a chave de instrumentação nesse comando e, em seguida, execute-a:
   
   ```
   
   docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=000000-1111-2222-3333-444444444
   ```

Apenas uma imagem do Application Insights é necessária por host do Docker. Se seu aplicativo for implantado em vários hosts de Docker, em seguida, repita o comando de saudação em cada host.

## <a name="update-your-app"></a>Atualizar seu aplicativo
Se seu aplicativo está instrumentado com hello [SDK do Application Insights para Java](app-insights-java-get-started.md), adicionar Olá a seguinte linha no arquivo de ApplicationInsights.xml Olá no seu projeto, em Olá `<TelemetryInitializers>` elemento:

```xml

    <Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/> 
```

Isso adiciona informações de Docker como contêiner host id tooevery telemetria item e enviado de seu aplicativo.

## <a name="view-your-telemetry"></a>Exibir sua telemetria
Volte tooyour recurso Application Insights Olá portal do Azure.

Clique em bloco de Docker hello.

Em breve você verá dados chegando do aplicativo de Docker hello, especialmente se você tiver outros contêineres em execução no seu mecanismo do Docker.

Aqui estão algumas das exibições de saudação, que você pode obter.

### <a name="perf-counters-by-host-activity-by-image"></a>Contadores de desempenho por host, atividade por imagem
![exemplo](./media/app-insights-docker/10.png)

![exemplo](./media/app-insights-docker/11.png)

Clique em qualquer nome de imagem ou host para obter mais detalhes.

modo de exibição toocustomize hello, clique em qualquer gráfico, a grade de saudação do título ou use Adicionar gráfico. 

[Saiba mais sobre o Metrics Explorer](app-insights-metrics-explorer.md).

### <a name="docker-container-events"></a>Eventos de contêiner do Docker
![exemplo](./media/app-insights-docker/13.png)

eventos individuais de tooinvestigate, clique em [pesquisa](app-insights-diagnostic-search.md). Pesquisar e filtrar toofind Olá eventos que você deseja. Clique em qualquer evento tooget mais detalhes.

### <a name="exceptions-by-container-name"></a>Exceções por nome do contêiner
![exemplo](./media/app-insights-docker/14.png)

### <a name="docker-context-added-tooapp-telemetry"></a>O contexto de docker adicionado tooapp Telemetria
Telemetria de solicitação enviada do aplicativo hello instrumentado com o SDK do AI, aprimorada com o contexto do Docker:

![exemplo](./media/app-insights-docker/16.png)

Tempo do processador e contadores de desempenho de memória disponíveis, aprimorados e agrupados por nome de contêiner do Docker:

![exemplo](./media/app-insights-docker/15.png)

## <a name="q--a"></a>Perguntas e respostas
*O que o Application Insights me proporciona que eu não consigo obter com o Docker?*

* Análise detalhada dos contadores de desempenho por contêiner e imagem.
* Integração dos dados de contêiner e do aplicativo em um painel.
* [Exportar telemetria](app-insights-export-telemetry.md) para o banco de dados de tooa análise adicional, o Power BI ou outro painel.

*Como obter telemetria de aplicativo hello em si?*

* Instale Olá SDK do Application Insights no aplicativo hello. Saiba mais para: [aplicativos Web Java](app-insights-java-get-started.md), [aplicativos Web Windows](app-insights-asp-net.md).

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Próximas etapas

* [Application Insights para Java](app-insights-java-get-started.md)
* [Application Insights para Node.js](app-insights-nodejs.md)
* [Application Insights para ASP.NET](app-insights-asp-net.md)
