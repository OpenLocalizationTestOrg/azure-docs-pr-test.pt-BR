---
title: amostragem aaaTelemetry no Azure Application Insights | Microsoft Docs
description: "Como tookeep Olá volume de telemetria sob controle."
services: application-insights
documentationcenter: windows
author: vgorbenko
manager: carmonm
ms.assetid: 015ab744-d514-42c0-8553-8410eef00368
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bwren
ms.openlocfilehash: e19c350d0a5f16736c100322a9922fcfbf5d7b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sampling-in-application-insights"></a>Amostragem no Application Insights


A amostragem é um recurso do [Azure Application Insights](app-insights-overview.md). É recomendado de saudação tráfego de telemetria do modo tooreduce e armazenamento, enquanto preserva uma análise estatística correta de dados de aplicativo. filtro de saudação seleciona itens relacionados, para que você possa navegar entre os itens quando você estiver realizando investigações de diagnósticas.
Quando as contagens de métrica são apresentadas tooyou no portal de hello, eles são renormalized tootake conta de saudação de amostragem toominimize qualquer efeito em estatísticas de saudação.

A amostragem reduz os custos de tráfego e de dados e ajuda a evitar a limitação.

## <a name="in-brief"></a>Em resumo:
* Amostragem retém 1 em  *n*  registra e descarta o resto de saudação. Por exemplo, ela pode reter 1 em 5 eventos, com uma taxa de amostragem de 20%. 
* A amostragem acontece automaticamente se o seu aplicativo enviar muita telemetria em aplicativos de servidor Web do ASP.NET.
* Você também pode definir a amostragem manualmente, a saudação na portal em Olá preços página; ou, no hello SDK de ASP.NET no arquivo. config de hello, tooalso reduzir o tráfego de rede de saudação.
* Se você registra eventos personalizados e você desejar toomake-se de que um conjunto de eventos é retido ou descartado juntos, certifique-se de que eles têm Olá mesmo valor de ID da operação.
* divisor de amostragem Olá  *n*  é informada em cada registro na propriedade Olá `itemCount`, que pesquisa aparece sob Olá nome amigável "contagem de solicitação" ou "contagem de eventos". Quando a amostragem não estiver em operação, `itemCount==1`.
* Se você escrever consultas de Análise, deverá [levar em conta a amostragem](app-insights-analytics-tour.md#counting-sampled-data). Em particular, em vez de simplesmente contar registros, você deve usar `summarize sum(itemCount)`.

## <a name="types-of-sampling"></a>Tipos de amostragem
Há três módulos de amostragem alternativos:

* **Amostragem adaptável** ajusta automaticamente o volume de saudação de telemetria enviada do hello SDK em seu aplicativo ASP.NET. Ela é padrão desde o SDK v 2.0.0-beta3. Disponível atualmente somente para telemetria ASP.NET do lado do servidor. 
* **-Taxa amostragem** reduz o volume de saudação de telemetria enviada do seu servidor ASP.NET e navegadores dos usuários. Você definir a taxa de saudação. saudação de cliente e servidor sincronizará seu amostragem de forma que, na pesquisa, você pode navegar entre os modos de exibição de página relacionada e solicitações.
* **Amostragem de inclusão** funciona em Olá portal do Azure. Descarta algumas telemetria Olá que chega de seu aplicativo, a uma taxa que você definir. Ela não reduz o tráfego de telemetria, mas ajuda você a se manter em sua cota mensal. Olá grande vantagem de amostragem de inclusão é que você pode configurá-lo sem reimplantar o aplicativo e funciona uniformemente para todos os servidores e clientes. 

Se a amostragem de taxa Adaptável ou Fixa estiver em operação, a amostragem de Ingestão estará desabilitada.

## <a name="ingestion-sampling"></a>amostragem de ingestão
Essa forma de amostragem opera no ponto de saudação onde telemetria de saudação do seu servidor web, navegadores e dispositivos atinge o ponto de extremidade do serviço Olá Application Insights. Embora ele não reduzir o tráfego de telemetria de saudação enviado do seu aplicativo, ele reduzir a quantidade de saudação processados e retidos (e cobrada por) pelo Application Insights.

Use este tipo de amostragem, se seu aplicativo geralmente vai exceder sua cota mensal e você não tem a opção hello usando um dos tipos de saudação com base no SDK de amostragem. 

Definir a taxa de amostragem de saudação em Olá cotas e folha de preços:

![Na folha de visão geral do aplicativo hello, clique em configurações de cota, exemplos, e em seguida, selecione uma taxa de amostragem e clique em Atualizar.](./media/app-insights-sampling/04.png)

Como outros tipos de amostragem, o algoritmo Olá retém itens de telemetria relacionados. Por exemplo, quando você está verificando telemetria Olá na pesquisa, você poderá toofind solicitação de saudação relacionadas tooa exceção em particular. As contagens de métrica como a taxa de solicitação e a taxa de exceções são mantidas corretamente.

Os pontos de dados que são descartados pela amostragem não estão disponíveis em nenhum recurso do Application Insights como [Exportação Contínua](app-insights-export-telemetry.md).

A amostragem de ingestão não funciona enquanto a amostragem adaptável ou de taxa fixa com base no SDK estiver em operação. Se a taxa de amostragem de saudação em Olá SDK for inferior a 100%, em seguida, hello taxa de amostragem de inclusão definido é ignorada.

> [!WARNING]
> valor Olá mostrado no bloco Olá indica o valor de saudação que você definiu para amostragem de inclusão. Ele não representa a taxa de amostragem real Olá se amostragem SDK está em operação.
> 
> 

## <a name="adaptive-sampling-at-your-web-server"></a>Amostragem adaptável em seu servidor Web
Amostragem adaptável está disponível para Olá SDK do Application Insights para ASP.NET v 2.0.0-beta3 e posterior e é habilitada por padrão. 

Amostragem adaptável afeta o volume de saudação de telemetria enviada do seu toohello de aplicativo do servidor web serviço do Application Insights. Olá volume é ajustado automaticamente tookeep dentro de uma taxa máxima especificada de tráfego.

Ela não funciona em volumes baixos de telemetria e, portanto, um aplicativo em depuração ou um site com baixo uso não serão afetados.

o volume de destino do tooachieve hello, alguns dos telemetria Olá gerada é descartado. Mas, como outros tipos de amostragem, o algoritmo Olá retém itens de telemetria relacionados. Por exemplo, quando você está verificando telemetria Olá na pesquisa, você poderá toofind solicitação de saudação relacionadas tooa exceção em particular. 

Métrica de conta, como taxa de solicitação e taxa de exceções são toocompensate ajustada para Olá taxa de amostragem para que elas mostram valores aproximadamente corretos no Explorer de métrica.

**Atualização NuGet do projeto** pacotes toohello mais recente *pré-lançamento* versão do Application Insights: clique com botão direito Olá no Gerenciador de soluções, escolha gerenciar pacotes NuGet, verifique **Include pré-lançamento** e procure Microsoft.ApplicationInsights.Web. 

Em [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md), você pode ajustar vários parâmetros no hello `AdaptiveSamplingTelemetryProcessor` nó. números Olá mostrados são valores padrão de saudação:

* `<MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>`
  
    Olá taxa de destino que Olá algoritmo adaptável objetiva **em cada host de servidor**. Se seu aplicativo web é executado em vários hosts, reduza esse valor como tooremain dentro de sua taxa de destino do tráfego no portal do Application Insights hello.
* `<EvaluationInterval>00:00:15</EvaluationInterval>` 
  
    intervalo de saudação em qual Olá taxa atual de telemetria é avaliada novamente. Avaliação é executada como uma média móvel. Talvez você queira tooshorten esse intervalo se a telemetria é intermitências toosudden responsável.
* `<SamplingPercentageDecreaseTimeout>00:02:00</SamplingPercentageDecreaseTimeout>`
  
    Quando alterações de valor de porcentagem de amostragem, quanto tempo depois é permitido toolower amostragem percentual novamente toocapture menos dados.
* `<SamplingPercentageIncreaseTimeout>00:15:00</SamplingPercentageIncreaseTimeout>`
  
    Quando alterações de valor de porcentagem de amostragem, quanto tempo depois podemos tooincrease amostragem percentual novamente toocapture mais dados.
* `<MinSamplingPercentage>0.1</MinSamplingPercentage>`
  
    Como percentual de amostragem varia, o que é o valor mínimo de saudação tooset são permitidos.
* `<MaxSamplingPercentage>100.0</MaxSamplingPercentage>`
  
    Como percentual de amostragem varia, o que é o valor máximo de saudação tooset são permitidos.
* `<MovingAverageRatio>0.25</MovingAverageRatio>` 
  
    No cálculo de saudação do hello média móvel, peso Olá atribuído valor mais recente toohello. Use um tooor igual do valor menor que 1. Valores menores alterar algoritmo Olá menos reativo toosudden.
* `<InitialSamplingPercentage>100</InitialSamplingPercentage>`
  
    valor de Olá atribuído quando o aplicativo hello começou. Não o reduza enquanto estiver depurando. 

* `<ExcludedTypes>Trace;Exception</ExcludedTypes>`
  
    Lista de tipos que não deseja toobe amostra delimitada por ponto e vírgula. Os tipos reconhecidos são: Dependência, Evento, Exceção, PageView, Solicitação, Rastreamento. Todas as instâncias de saudação especificado tipos são transmitidos; tipos de saudação que não são especificados são amostrados.

* `<IncludedTypes>Request;Dependency</IncludedTypes>`
  
    Uma lista delimitada por ponto e vírgula de tipos que você deseja toobe de amostra. Os tipos reconhecidos são: Dependência, Evento, Exceção, PageView, Solicitação, Rastreamento. Olá especificados tipos são amostrados; todas as instâncias de saudação os outros tipos sempre serão transmitidos.


**tooswitch desativar** amostragem adaptável, remover Olá AdaptiveSamplingTelemetryProcessor nó de configuração applicationinsights.

### <a name="alternative-configure-adaptive-sampling-in-code"></a>Alternativa: configurar amostragem adaptável no código
Em vez de ajuste de amostragem no arquivo. config de saudação, você pode usar o código. Isso permite que você toospecify uma função de retorno de chamada invocado sempre que a taxa de amostragem hello serão reavaliada. Você pode usar isso, por exemplo, toofind limite de taxa de amostragem que está sendo usado.

Remover Olá `AdaptiveSamplingTelemetryProcessor` nó do arquivo. config de saudação.

*C#*

```C#

    using Microsoft.ApplicationInsights;
    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.Channel.Implementation;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var adaptiveSamplingSettings = new SamplingPercentageEstimatorSettings();

    // Optional: here you can adjust hello settings from their defaults.

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;

    builder.UseAdaptiveSampling(
         adaptiveSamplingSettings,

        // Callback on rate re-evaluation:
        (double afterSamplingTelemetryItemRatePerSecond,
         double currentSamplingPercentage,
         double newSamplingPercentage,
         bool isSamplingPercentageChanged,
         SamplingPercentageEstimatorSettings s
        ) =>
        {
          if (isSamplingPercentageChanged)
          {
             // Report hello sampling rate.
             telemetryClient.TrackMetric("samplingPercentage", newSamplingPercentage);
          }
      });

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

([Saiba mais sobre os processadores de telemetria](app-insights-api-filtering-sampling.md#filtering).)

<a name="other-web-pages"></a>

## <a name="sampling-for-web-pages-with-javascript"></a>Amostragem para áginas da Web com JavaScript
Você pode configurar as páginas da Web para amostragem de taxa fixa de qualquer servidor. 

Quando você [configurar páginas de web Olá para o Application Insights](app-insights-javascript.md), modificar o trecho de saudação que você obteve no portal do Application Insights hello. (Em aplicativos ASP.NET, trecho Olá geralmente vai layout. cshtml.)  Inserir uma linha como `samplingPercentage: 10,` antes da chave de instrumentação hello:

    <script>
    var appInsights= ... 
    }({ 


    // Value must be 100/N where N is an integer.
    // Valid examples: 50, 25, 20, 10, 5, 1, 0.1, ...
    samplingPercentage: 10, 

    instrumentationKey:...
    }); 

    window.appInsights=appInsights; 
    appInsights.trackPageView(); 
    </script> 

Para o percentual de amostragem hello, escolha uma porcentagem que é fechar too100/N onde N é um inteiro.  Atualmente, a amostragem não dá suporte a outros valores.

Se você habilitar também-taxa amostragem no servidor de saudação, servidor e clientes hello serão sincronizados para que, na pesquisa, você pode navegar entre os modos de exibição de página relacionada e solicitações.

## <a name="fixed-rate-sampling-for-aspnet-web-sites"></a>Amostragem de taxa fixa para sites ASP.NET
Taxa fixa amostragem reduz o tráfego de saudação enviado do seu servidor web e navegadores da web. Ao contrário da amostragem adaptável, ela reduz a telemetria a uma taxa fixa decidida por você. Ele também sincronizará cliente hello e amostragem de servidor para que itens relacionados são mantidos - por exemplo, para que se você observar um modo de exibição de página na pesquisa, você pode encontrar sua solicitação relacionadas.

algoritmo de amostragem Olá retém itens relacionados. Para cada evento de solicitação HTTP, ele e os eventos relacionados são descartados ou transmitidos. 

No Metrics Explorer taxas como contagens de solicitação e a exceção são multiplicadas por toocompensate um fator de taxa de amostragem de hello, para que eles sejam aproximadamente corretos.

1. **Atualizar pacotes do NuGet do projeto** toohello mais recente *pré-lançamento* versão do Application Insights. Clique com botão direito Olá no Gerenciador de soluções, escolha gerenciar pacotes NuGet, verifique **incluir pré-lançamento** e procure Microsoft.ApplicationInsights.Web. 
2. **Desabilitar amostragem adaptável**: em [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md), remova ou comente Olá `AdaptiveSamplingTelemetryProcessor` nó.
   
    ```xml
   
    <TelemetryProcessors>
   
    <!-- Disabled adaptive sampling:
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    -->

    ```

1. **Habilita Olá-taxa de amostragem módulo.** Adicionar este trecho de código muito[Applicationinsights](app-insights-configuration-with-applicationinsights-config.md):
   
    ```XML
   
    <TelemetryProcessors>
     <Add  Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
   
      <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
      <SamplingPercentage>10</SamplingPercentage>
      </Add>
    </TelemetryProcessors>
   
    ```

> [!NOTE]
> Para o percentual de amostragem hello, escolha uma porcentagem que é fechar too100/N onde N é um inteiro.  Atualmente, a amostragem não dá suporte a outros valores.
> 
> 

### <a name="alternative-enable-fixed-rate-sampling-in-your-server-code"></a>Alternativa: habilite a amostragem de taxa fixa no código do servidor
Em vez de definir o parâmetro de amostragem de saudação no arquivo. config de saudação, você pode usar o código. 

*C#*

```C#

    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var builder = TelemetryConfiguration.Active.GetTelemetryProcessorChainBuilder();
    builder.UseSampling(10.0); // percentage

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

([Saiba mais sobre os processadores de telemetria](app-insights-api-filtering-sampling.md#filtering).)

## <a name="when-toouse-sampling"></a>Quando toouse amostragem?
Amostragem adaptável é habilitada automaticamente se você usar o hello ASP.NET SDK versão 2.0.0-beta3 ou posterior. Você pode usar a amostragem de ingestão (em nosso servidor) independente da versão do SDK utilizada.

A amostragem não é necessária para a maioria dos aplicativos de pequeno e médio porte. informações de diagnóstico mais úteis Hello e estatísticas mais precisas são obtidas pela coleta de dados em todas as atividades do usuário. 

Olá principais vantagens de amostragem são:

* O serviço Application Insights remove (“limita”) os pontos de dados quando o aplicativo envia uma taxa muito alta de telemetria em um curto intervalo de tempo. 
* tookeep em Olá [cota](app-insights-pricing.md) de pontos de dados para o tipo de preços. 
* tráfego de rede tooreduce da coleção de saudação de telemetria. 

### <a name="which-type-of-sampling-should-i-use"></a>Que tipo de amostragem eu devo usar?
**Use a amostragem de ingestão se:**

* Você geralmente ultrapassa sua cota mensal de telemetria.
* Você está usando uma versão do hello SDK que não dá suporte a amostragem - por exemplo, Olá Java SDK ou ASP.NET versões anteriores a 2.
* Você estiver recebendo muita telemetria dos navegadores dos usuários.

**Use a amostragem de taxa fixa se:**

* Você está usando Olá SDK do Application Insights para a versão de serviços web do ASP.NET 2.0.0 ou posterior, e
* Você deseja amostragem sincronizados entre cliente e servidor, para que, quando você estiver investigando eventos em [pesquisa](app-insights-diagnostic-search.md), você pode navegar entre os eventos relacionados no cliente hello e servidor, como exibições de página e solicitações http.
* Que esteja confiante de percentual de amostragem apropriado de saudação para seu aplicativo. Ele deve ser uma métrica precisa tooget alta o suficiente, mas abaixo Olá taxa excede sua cota de preços e Olá limites de limitação. 

**Use a amostragem adaptável:**

Caso contrário, recomendamos a amostragem adaptável. Isso é habilitado por padrão no servidor do ASP.NET Olá SDK, versão 2.0.0-beta3 ou posterior. Ela não reduz o tráfego até uma determinada taxa mínima e, portanto, não afetará um site de baixa utilização.

## <a name="how-do-i-know-whether-sampling-is-in-operation"></a>Como saber se a amostragem está em operação?
toodiscover Olá real amostragem taxa, independentemente de onde ela foi aplicada, use um [consulta analítica](app-insights-analytics.md) como este:

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

Em cada retidos registro, `itemCount` indica número Olá de originais registros que ele representa, igual too1 + número de saudação de registros descartados anteriores. 

## <a name="how-does-sampling-work"></a>Como funciona a amostragem?
Taxa fixa e amostragem adaptável são um recurso da saudação SDK em versões do ASP.NET de 2.0.0 em diante. Amostragem de inclusão é um recurso do hello serviço Application Insights e pode estar em operação se Olá SDK não está executando a amostragem. 

algoritmo de amostragem Olá decide qual toodrop de itens de telemetria e quais os tookeep (se está Olá SDK ou no serviço do Application Insights Olá). Olá amostragem decisão se baseia em várias regras que visam toopreserve todos os pontos de dados inter-relacionados intacto, manter uma experiência no Application Insights acionáveis e confiável até mesmo com um conjunto reduzido de dados de diagnóstica. Por exemplo, se para uma solicitação com falha seu aplicativo enviar itens de telemetria adicionais (como exceção e rastreamentos registrados desta solicitação), a amostragem não dividirá essa solicitação e outra telemetria. Ela mantém ou remove todos juntos. Como resultado, quando examinar os detalhes de solicitação de saudação no Application Insights, você verá sempre solicitação Olá junto com seus itens de telemetria associada. 

Para aplicativos que definem o "usuário" (ou seja, aplicativos de web mais comuns), Olá amostragem decisão se baseia no hash de saudação do id de usuário hello, o que significa que toda a telemetria para qualquer usuário específico é preservada ou descartada. Para tipos de saudação de aplicativos que não definem os usuários (como serviços web) Olá amostragem decisão se baseia na id de operação de saudação da solicitação de saudação. Por fim, para itens de telemetria Olá que não têm a id de usuário nem operação definida (por exemplo, itens telemetria relatados de threads assíncronas com nenhum contexto http) amostragem simplesmente captura uma porcentagem de itens de telemetria de cada tipo. 

Ao apresentar tooyou back telemetria, Olá Application Insights serviço ajusta as métricas de saudação por Olá mesmo percentual de amostragem que foi usado no tempo de saudação da coleção, toocompensate para Olá pontos de dados. Portanto, ao analisar a telemetria Olá no Application Insights, usuários hello estão vendo aproximações estatisticamente corretas que são muito próxima toohello em números reais.

precisão de saudação do aproximação Olá depende principalmente da porcentagem de amostragem de saudação configurada. Além disso, aumenta a precisão de saudação para aplicativos que lidam com um grande volume de solicitações geralmente semelhantes de vários usuários. Em Olá outro lado, para aplicativos que não funcionam com uma carga significativa, a amostragem não é necessário como esses aplicativos normalmente podem enviar todos os seu telemetria mantendo dentro da cota de saudação sem causar perda de dados da limitação. 

Observe que o Application Insights não exemplos de tipos de telemetria de métricas e sessões, desde para esses tipos, redução na precisão Olá pode ser altamente indesejável. 

### <a name="adaptive-sampling"></a>amostragem adaptável
Amostragem adaptável adiciona um componente que monitores Olá atual taxa de transmissão de Olá SDK e ajusta Olá amostragem percentual tootry toostay na taxa máxima de destino de saudação. ajuste Olá é recalculado em intervalos regulares e baseia-se em uma média móvel de saudação taxa de transmissão de saída.

## <a name="sampling-and-hello-javascript-sdk"></a>Amostragem e hello SDK de JavaScript
saudação do cliente (JavaScript) SDK participa-taxa amostragem em conjunto com saudação do servidor SDK. páginas Olá instrumentado somente enviará telemetria do lado do cliente da saudação mesmos usuários para qual saudação do servidor feita sua decisão muito "sample em." Essa lógica é projetado toomaintain integridade de sessão de usuário em lado cliente e servidor lados. Como resultado, em qualquer item de telemetria específico no Application Insights é possível encontrar todos os outros itens de telemetria para esse usuário ou sessão. 

*Minha telemetria do lado do cliente e do servidor não mostra exemplos coordenados como descrito acima.*

* Verifique se você habilitou a amostragem de taxa fixa tanto no servidor quanto no cliente.
* Certifique-se de que a versão SDK Olá é 2.0 ou posterior.
* Verifique se você definir Olá mesmo amostragem percentual no hello cliente e servidor.

## <a name="frequently-asked-questions"></a>Perguntas frequentes
*Por que a amostragem não se trata apenas de “coletar X% de cada tipo de telemetria”?*

* Enquanto essa abordagem de amostragem ofereceria com uma precisão muito alta em aproximações métricas, ele interrompe os dados de diagnóstico capacidade toocorrelate por usuário, sessão e solicitação, que é essencial para diagnóstico. Portanto, a amostragem funciona melhor com a lógica “coletar todos os itens de telemetria para X% de usuários do aplicativo” ou “coletar toda a telemetria para X% das solicitações do aplicativo”. Para itens de telemetria Olá não associados a solicitações de saudação (como o processamento assíncrono em segundo plano), estão Olá será muito "coletar X por cento de todos os itens para cada tipo de telemetria." 

*Percentual de amostragem Olá pode mudar ao longo do tempo?*

* Sim, a amostragem adaptável gradualmente altera percentual de amostragem hello, com base em Olá observada no momento o volume de telemetria de saudação.

*Se usar-taxa amostragem, como saber quais amostragem percentual funcionará Olá melhor para meu aplicativo?*

* Uma maneira é toostart com a amostragem adaptável, descobrir o que classificar paga em (consulte Olá acima pergunta), e, em seguida, switch toofixed-taxa de amostragem usando essa taxa. 
  
    Caso contrário, você tem tooguess. Analisar o uso atual de telemetria em AI, observe qualquer limitação ou seja ocorrendo e estimativa Olá volume de telemetria Olá coletado. Esses três entradas, junto com sua camada de preços selecionada, sugerem quanto desejar tooreduce volume de saudação de telemetria Olá coletado. No entanto, um aumento no número de saudação dos usuários ou alguns outros shift no volume de saudação de telemetria pode invalidar sua estimativa.

*O que acontece se eu configurar o percentual de amostragem com um valor muito baixo?*

* Percentual de amostragem excessivamente baixo (over-aggressive amostragem) reduz a precisão de saudação do aproximações Olá, ao Application Insights tentativas de visualização de saudação toocompensate dos dados Olá para redução de volume de dados de saudação. Além disso, experiência de diagnóstica pode piorar, pois algumas Olá raramente falhando ou solicitações lenta podem servir como amostra.

*O que acontece se eu configurar o percentual de amostragem com um valor muito alto?*

* Configurando resultados de porcentagem (não agressiva suficiente) de amostragem muito alto em uma redução insuficiente no volume de saudação do hello coletados telemetria. Pode ocorrer perda de dados relacionados a toothrottling e o custo de saudação do usando o Application Insights podem ser maior do que você planejado devido toooverage encargos de telemetria.

*Em quais plataformas posso usar a amostragem?*

* Amostragem de ingestão poderá ocorrer automaticamente para qualquer telemetria acima de um determinado volume se Olá SDK não está executando a amostragem. Isso funcionaria, por exemplo, se seu aplicativo usa um servidor Java, ou se você estiver usando uma versão mais antiga do hello SDK do ASP.NET.
* Se você estiver usando versões do SDK de ASP.NET 2.0.0 e superior (hospedado no Azure ou em seu próprio servidor), você obtém adaptável amostragem por padrão, mas você pode alternar a taxa de toofixed conforme descrito acima. Com-taxa amostragem, o navegador Olá SDK sincroniza automaticamente toosample eventos relacionados. 

*Há certos eventos raros desejo sempre toosee. Como posso obtê-los após o módulo de amostragem Olá?*

* Inicialize uma instância separada do TelemetryClient com um novo TelemetryConfiguration (não saudação padrão ativo). Use esse toosend seus eventos raros.

## <a name="next-steps"></a>Próximas etapas
* [filtragem](app-insights-api-filtering-sampling.md) pode fornecer um controle mais restrito do que o SDK envia.

