---
title: aaaGet iniciado com o Azure Application Insights com Java em Eclipse | Documentos da Microsoft
description: Use hello desempenho tooadd plug-in do Eclipse e uso de monitoramento tooyour Java com o Application Insights
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: e88c9f53-cd90-4abc-b097-1f170937908e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: bwren
ms.openlocfilehash: 3142a26a9e2d14c2c433882e3d337f2a8c8f2247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-with-java-in-eclipse"></a>Introdução ao Application Insights com Java no Eclipse
Olá SDK do Application Insights envia telemetria do seu aplicativo da web de Java para que você pode analisar o uso e desempenho. Olá Eclipse plug-in para o Application Insights instala automaticamente Olá SDK em seu projeto para que você obtenha de telemetria de caixa hello, além de uma API que você pode usar a telemetria personalizada de toowrite.   

## <a name="prerequisites"></a>Pré-requisitos
Olá plug-in trabalha atualmente para projetos Maven e dinâmico da Web no Eclipse.
([Tipos de tooother adicionar Application Insights do projeto Java][java].)

Você precisará de:

* Oracle JRE 1.6 ou posterior
* Uma assinatura muito[Microsoft Azure](https://azure.microsoft.com/).
* [Um IDE do Eclipse para desenvolvedores do Java EE](http://www.eclipse.org/downloads/), Indigo ou posterior.
* Windows 7 ou posterior, ou Windows Server 2008 ou posterior

## <a name="install-hello-sdk-on-eclipse-one-time"></a>Instalar Olá SDK no Eclipse (uma vez)
Você só tem toodo dessa vez por computador. Esta etapa instala um kit de ferramentas que possa adicionar Olá SDK tooeach projeto Web dinâmico.

1. No Eclipse, clique em Ajuda, depois em Instalar novo Software.

    ![Ajuda, Instalar Novo Software](./media/app-insights-java-eclipse/0-plugin.png)
2. Olá SDK está em http://dl.microsoft.com/eclipse no Kit de ferramentas do Azure.
3. Desmarque **Contatar todos os sites de atualização...**

    ![Para o SDK do Application Insights, limpe a opção Contatar todos os sites de atualização](./media/app-insights-java-eclipse/1-plugin.png)

Siga Olá restantes etapas para cada projeto Java.

## <a name="create-an-application-insights-resource-in-azure"></a>Criar um recurso do Application Insights no Azure
1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Criar um novo recurso do Application Insights Defina o aplicativo de web tooJava do tipo de aplicativo hello.  

    ![Clique em + e escolha Application Insights](./media/app-insights-java-eclipse/01-create.png)  

4. Localize a chave de instrumentação de saudação do novo recurso de saudação. Você precisará toopaste isso em seu projeto de código em breve.  

    ![No hello nova visão geral do recurso, clique em propriedades e copie Olá chave de instrumentação](./media/app-insights-java-eclipse/03-key.png)  

## <a name="add-application-insights-tooyour-project"></a>Adicionar Application Insights tooyour projeto
1. Adicione o Application Insights no menu de contexto de saudação do seu projeto da web de Java.

    ![No hello nova visão geral do recurso, clique em propriedades e copie Olá chave de instrumentação](./media/app-insights-java-eclipse/02-context-menu.png)
2. Cole a chave de instrumentação Olá que você obteve Olá portal do Azure.

    ![No hello nova visão geral do recurso, clique em propriedades e copie Olá chave de instrumentação](./media/app-insights-java-eclipse/03-ikey.png)

chave de saudação enviada juntamente com todos os itens de telemetria e informa ao Application Insights toodisplay-lo em seu recurso.

## <a name="run-hello-application-and-see-metrics"></a>Executar o aplicativo hello e ver as métricas
Execute seu aplicativo.

Retorne recurso do Application Insights tooyour no Microsoft Azure.

Dados de solicitações HTTP serão exibida na folha de visão geral de saudação. (Se não estiverem lá, aguarde alguns segundos e, em seguida, clique em Atualizar.)

![Falhas, contagens de solicitação e resposta do servidor ](./media/app-insights-java-eclipse/5-results.png)

Clique em por meio de qualquer gráfico toosee métricas mais detalhadas.

![Contagens de solicitação por nome](./media/app-insights-java-eclipse/6-barchart.png)

[Saiba mais sobre métricas.][metrics]

E, ao exibir as propriedades de saudação de uma solicitação, você pode ver eventos de telemetria Olá associados a ele, como solicitações e exceções.

![Todos os rastreamentos para esta solicitação](./media/app-insights-java-eclipse/7-instance.png)

## <a name="client-side-telemetry"></a>Telemetria do lado do cliente
Folha de início rápido de saudação, clique em obter código toomonitor minhas páginas da web:

![Na folha de visão geral sobre seu aplicativo, selecione início rápido, obter código toomonitor minhas páginas da web. Copie o script hello.](./media/app-insights-java-eclipse/02-monitor-web-page.png)

Inserir o trecho de código de saudação no cabeçalho Olá dos seus arquivos HTML.

#### <a name="view-client-side-data"></a>Exibir dados do lado do cliente
Abra suas páginas da Web atualizadas e use-as. Aguarde um minuto ou dois e depois retornar tooApplication Insights e folha de uso de saudação aberto. (Na folha de visão geral do hello, role para baixo e clique em uso.)

Métricas de sessão, de usuário e de exibição de página serão exibida na folha de uso de saudação:

![Sessões, usuários e modos de exibição de página](./media/app-insights-java-eclipse/appinsights-47usage-2.png)

[Saiba mais sobre como configurar a telemetria do lado do cliente.][usage]

## <a name="publish-your-application"></a>Publicar seu aplicativo
Publicar o seu servidor de toohello de aplicativo agora, permitem que pessoas usá-lo e assista a telemetria Olá aparecerão no portal de saudação.

* Verifique se o firewall permite que seu aplicativo toosend telemetria toothese portas:

  * dc.services.visualstudio.com:443
  * dc.services.visualstudio.com:80
  * f5.services.visualstudio.com:443
  * f5.services.visualstudio.com:80
* Nos servidores Windows, instale:

  * [Microsoft Visual C++ redistribuível](http://www.microsoft.com/download/details.aspx?id=40784)

    (Isso habilita os contadores de desempenho.)

## <a name="exceptions-and-request-failures"></a>Falhas de solicitação e exceções
Exceções sem tratamento são coletadas automaticamente:

![](./media/app-insights-java-eclipse/21-exceptions.png)

dados toocollect outras exceções, você tem duas opções:

* [Inserir chama tooTrackException no seu código](app-insights-api-custom-events-metrics.md#trackexception).
* [Instalar Olá agente Java em seu servidor](app-insights-java-agent.md). Você especificar métodos Olá toowatch desejado.

## <a name="monitor-method-calls-and-external-dependencies"></a>Monitorar chamadas de método e dependências externas
[Instalar Olá agente Java](app-insights-java-agent.md) toolog especificado métodos internos e as chamadas feitas por meio do JDBC, com dados de tempo.

## <a name="performance-counters"></a>Contadores de desempenho
Na sua folha de visão geral, role para baixo e clique em Olá **servidores** lado a lado. Você verá uma variedade de contadores de desempenho.

![Role para baixo do bloco de servidores tooclick Olá](./media/app-insights-java-eclipse/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a>Personalizar a coleta do contador de desempenho
coleção de toodisable de conjunto de contadores de desempenho padrão Olá adicionar Olá código sob o nó de raiz de saudação do arquivo de ApplicationInsights.xml Olá a seguir:

```XML

    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a>Coletar contadores de desempenho adicionais
Você pode especificar toobe de contadores de desempenho coletados.

#### <a name="jmx-counters-exposed-by-hello-java-virtual-machine"></a>Contadores do JMX (expostas pelo Olá Máquina Virtual Java)

```XML

    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* `displayName`– nome hello exibido no portal do Application Insights hello.
* `objectName`– nome do objeto Olá JMX.
* `attribute`– atributo Olá Olá toofetch de nome de objeto JMX
* `type`(opcional) - Olá tipo de atributo do objeto JMX:
  * Padrão: um tipo simples como “int” ou “long”.
  * `composite`: dados do contador de desempenho hello estão no formato de saudação do 'Attribute.Data'
  * `tabular`: dados do contador de desempenho hello estão no formato de saudação de uma linha da tabela

#### <a name="windows-performance-counters"></a>Contadores de desempenho do Windows
Cada [contador de desempenho do Windows](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) é um membro de uma categoria (em Olá mesma forma que um campo é um membro de uma classe). Categorias podem ser globais, ou podem ter instâncias numeradas ou nomeadas.

```XML

    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* displayName – nome hello exibido no portal do Application Insights hello.
* categoryName – Olá categoria contador de desempenho (objeto de desempenho) ao qual esse contador de desempenho está associado.
* counterName – nome Olá Olá do contador de desempenho.
* instanceName – Olá nome de instância de categoria do contador de desempenho de saudação ou uma cadeia de caracteres vazia (""), se a categoria de saudação contém uma única instância. Se Olá categoryName é o processo e contador de desempenho de saudação você gostaria que toocollect é do processo atual de JVM Olá em que seu aplicativo é executado, especifique `"__SELF__"`.

Seus contadores de desempenho são visíveis como métricas personalizadas em [Metrics Explorer][metrics].

![](./media/app-insights-java-eclipse/12-custom-perfs.png)

### <a name="unix-performance-counters"></a>Contadores de desempenho do Unix
* [Instalar collectd com plug-in Application Insights de saudação](app-insights-java-collectd.md) tooget uma ampla variedade de dados de sistema e de rede.

## <a name="availability-web-tests"></a>Testes de disponibilidade na Web
Application Insights pode testar seu site em toocheck em intervalos regulares que ele está ativo e também responder. [tooset backup][availability], role para baixo tooclick disponibilidade.

![Role para baixo, clique em Disponibilidade, em seguida, Adicionar teste na Web](./media/app-insights-java-eclipse/31-config-web-test.png)

Se seu site ficar inativo, você obterá gráficos de tempos de resposta e também notificações por email.

![Exemplo de teste da Web](./media/app-insights-java-eclipse/appinsights-10webtestresult.png)

[Saiba mais sobre testes de disponibilidade via web.][availability]

## <a name="diagnostic-logs"></a>Logs de diagnóstico
Se você estiver usando Log4J ou Logback (v 1.2 ou 2.0) para rastreamento, você pode ter seus logs de rastreamento enviados automaticamente tooApplication Insights onde você pode explorar e pesquisá-los.

[Saiba mais sobre logs de diagnóstico][javalogs]

## <a name="custom-telemetry"></a>Telemetria personalizada
Insira algumas linhas de código no seu toofind de aplicativo web Java out que os usuários estão fazendo com que ele ou toohelp diagnosticar problemas.

Você pode inserir o código na página da web JavaScript e em Java do lado do servidor de saudação.

[Saiba mais sobre a telemetria personalizada][track]

## <a name="next-steps"></a>Próximas etapas
#### <a name="detect-and-diagnose-issues"></a>Detectar e diagnosticar problemas
* [Adicionar telemetria do cliente web] [ usage] tooget telemetria de desempenho do cliente de web hello.
* [Configurar testes da web] [ availability] toomake-se de que seu aplicativo permanece em tempo real e responsivo.
* [Pesquisar eventos e logs de] [ diagnostic] toohelp diagnosticar problemas.
* [Capturar rastreamentos do Log4J ou Logback][javalogs]

#### <a name="track-usage"></a>Acompanhar uso
* [Adicionar telemetria do cliente web] [ usage] toomonitor página exibições e métricas de usuário básica.
* [Rastrear eventos personalizados e métricas](app-insights-web-track-usage.md) toolearn sobre como seu aplicativo é usado, tanto no cliente hello e no servidor de saudação.

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md
