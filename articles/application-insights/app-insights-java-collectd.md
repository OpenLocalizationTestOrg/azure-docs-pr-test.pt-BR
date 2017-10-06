---
title: aaaMonitor o desempenho do aplicativo web Java no Linux - Azure | Microsoft Docs
description: Estendido aplicativo monitoramento de desempenho do seu site de Java com hello CollectD plug-in do Application Insights.
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 40c68f45-197a-4624-bf89-541eb7323002
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: bwren
ms.openlocfilehash: f783e8607a83b2b43f67d3a2fc20f100aa2f75ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="collectd-linux-performance-metrics-in-application-insights"></a>collectd: métricas de desempenho do Linux no Application Insights


métricas de desempenho do sistema tooexplore Linux em [Application Insights](app-insights-overview.md), instalar [collectd](http://collectd.org/), junto com o plug-in Application Insights. Essa solução de software livre reúne várias estatísticas de sistema e de rede.

Normalmente, você usará o collectd se já tiver [instrumentado seu serviço Web Java com o Application Insights][java]. Isso lhe dá mais toohelp de dados você tooenhance desempenho do seu aplicativo ou diagnosticar problemas. 

![Exemplo de gráficos](./media/app-insights-java-collectd/sample.png)

## <a name="get-your-instrumentation-key"></a>Obter a chave de instrumentação
Em Olá [portal do Microsoft Azure](https://portal.azure.com), abra Olá [Application Insights](app-insights-overview.md) recursos onde você deseja Olá tooappear de dados. (Ou [crie um novo recurso](app-insights-create-new-resource.md).)

Faça uma cópia da chave de instrumentação hello, que identifica o recurso de saudação.

![Procurar tudo, abra o recurso e, em seguida, em Olá Essentials lista suspensa, selecione e copie Olá chave de instrumentação](./media/app-insights-java-collectd/02-props.png)

## <a name="install-collectd-and-hello-plug-in"></a>Instalar collectd e hello plug-in
Em seus computadores com o servidor Linux:

1. Instale [collectd](http://collectd.org/) versão 5.4.0 ou posterior.
2. Baixar Olá [plug-in do Application Insights collectd gravador](https://aka.ms/aijavasdk). Observe o número de versão de saudação.
3. Copie o plug-in Olá JAR em `/usr/share/collectd/java`.
4. Edite `/etc/collectd/collectd.conf`:
   * Certifique-se de que [Olá Java plug-in](https://collectd.org/wiki/index.php/Plugin:Java) está habilitado.
   * Atualize hello JVMArg para Olá java.class.path tooinclude Olá JAR a seguir. Atualize Olá versão número toomatch Olá que você baixou:
   * `/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar`
   * Adicione este trecho de código, usando Olá chave de instrumentação do recurso:

```XML

     LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"
     <Plugin ApplicationInsightsWriter>
        InstrumentationKey "Your key"
     </Plugin>
```

Veja o exemplo de parte de um arquivo de configuração:

```XML

    ...
    # collectd plugins
    LoadPlugin cpu
    LoadPlugin disk
    LoadPlugin load
    ...

    # Enable Java Plugin
    LoadPlugin "java"

    # Configure Java Plugin
    <Plugin "java">
      JVMArg "-verbose:jni"
      JVMArg "-Djava.class.path=/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar:/usr/share/collectd/java/collectd-api.jar"

      # Enabling Application Insights plugin
      LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"

      # Configuring Application Insights plugin
      <Plugin ApplicationInsightsWriter>
        InstrumentationKey "12345678-1234-1234-1234-123456781234"
      </Plugin>

      # Other plugin configurations ...
      ...
    </Plugin>
    ...
```

Configure outros [plug-ins collectd](https://collectd.org/wiki/index.php/Table_of_Plugins), que possam coletar vários dados de diferentes fontes.

Reiniciar collectd de acordo com o tooits [manual](https://collectd.org/wiki/index.php/First_steps).

## <a name="view-hello-data-in-application-insights"></a>Exibir dados de saudação no Application Insights
Em seu recurso Application Insights, abra [Metrics Explorer e adicione gráficos][metrics], selecionar métricas Olá deseja toosee de categoria personalizada de saudação.

![](./media/app-insights-java-collectd/result.png)

Por padrão, as métricas de saudação são agregadas em todas as máquinas de host do qual métricas Olá foram coletadas. métricas de saudação tooview por host, na folha de detalhes do gráfico hello, ativar o agrupamento e escolha toogroup pelo Host CollectD.

## <a name="tooexclude-upload-of-specific-statistics"></a>carregamento de tooexclude de estatísticas específicos
Por padrão, o plug-in do Application Insights Olá envia todos os dados de saudação coletados por todos os collectd de saudação habilitada 'leitura' Plug-ins. 

tooexclude dados de fontes de dados ou plug-ins específicos:

* Edite o arquivo de configuração de saudação. 
* Em `<Plugin ApplicationInsightsWriter>`, adicione linhas diretivas como esta:

| Diretiva | Efeito |
| --- | --- |
| `Exclude disk` |Excluir todos os dados coletados pelo Olá `disk` plug-in |
| `Exclude disk:read,write` |Excluir fontes de saudação denominados `read` e `write` de saudação `disk` plug-in. |

Diretivas separadas por uma nova linha.

## <a name="problems"></a>Problemas?
*Não vejo dados no portal de saudação*

* Abra [pesquisa] [ diagnostic] toosee se eventos brutos Olá chegaram. Às vezes, eles têm mais tooappear no metrics explorer.
* Talvez seja necessário muito[definir exceções de firewall para dados de saída](app-insights-ip-addresses.md)
* Habilite o rastreamento no plug-in Application Insights de saudação. Adicione esta linha em `<Plugin ApplicationInsightsWriter>`:
  * `SDKLogger true`
* Abrir um terminal e iniciar collectd em modo detalhado, toosee quaisquer problemas que ele estiver se comunicando:
  * `sudo collectd -f`

## <a name="known-issue"></a>Problema conhecido

plug-in Olá de gravação de informações do aplicativo é incompatível com determinados plug-ins de leitura. Alguns plug-ins, às vezes, enviam "NaN", onde o plug-in do Application Insights Olá espera um número de ponto flutuante.

Sintoma: o log de collectd Olá mostra erros que incluem "AI:... SyntaxError: token N" inexperado.

Solução alternativa: Exclua dados coletados pelo plug-ins de gravação de problema hello. 

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md


