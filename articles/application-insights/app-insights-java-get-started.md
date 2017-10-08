---
title: "análise de aplicativo da web aaaJava com o Azure Application Insights | Microsoft Docs"
description: 'Monitoramento de desempenho de aplicativos usando o Application Insights para aplicativos Web Java. '
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 051d4285-f38a-45d8-ad8a-45c3be828d91
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 6555ee53a44f937350e4fa296080f7dce4f45226
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-in-a-java-web-project"></a>Introdução ao Application Insights em um projeto Web Java


[Application Insights](https://azure.microsoft.com/services/application-insights/) é um serviço de análise extensível para desenvolvedores da web que ajuda você a entender o uso do seu aplicativo ao vivo e desempenho de saudação. Usá-la também[detectar e diagnosticar problemas de desempenho e exceções](app-insights-detect-triage-diagnose.md), e [escrever código] [ api] tootrack que os usuários fazem com seu aplicativo.

![dados de exemplo](./media/app-insights-java-get-started/5-results.png)

O Application Insights oferece suporte a aplicativos Java em execução no Windows, no Unix ou no Linux.

Você precisa de:

* Oracle JRE 1.6 ou posterior, ou então JRE Zulu 1.6 ou posterior
* Uma assinatura muito[Microsoft Azure](https://azure.microsoft.com/).

*Se você tiver um aplicativo web que já está ativo, você pode seguir procedimento alternativo Olá muito[adicionar Olá SDK em tempo de execução no servidor de web hello](app-insights-java-live.md). Essa alternativa evita a recompilação código hello, mas você não obterá a atividade de usuário Olá opção toowrite código tootrack.*

## <a name="1-get-an-application-insights-instrumentation-key"></a>1. Obter uma chave de instrumentação do Application Insights
1. Entrar toohello [portal do Microsoft Azure](https://portal.azure.com).
2. Crie um recurso Application Insights. Defina o aplicativo de web tooJava do tipo de aplicativo hello.

    ![Preencha um nome, escolha o aplicativo Java da Web e clique em Criar](./media/app-insights-java-get-started/02-create.png)
3. Localize a chave de instrumentação de saudação do novo recurso de saudação. Você precisará toopaste essa chave em seu projeto de código em breve.

    ![No hello nova visão geral do recurso, clique em propriedades e copie Olá chave de instrumentação](./media/app-insights-java-get-started/03-key.png)

## <a name="2-add-hello-application-insights-sdk-for-java-tooyour-project"></a>2. Adicionar hello SDK do Application Insights para projeto de tooyour de Java
*Escolha o modo apropriado de saudação do seu projeto.*

#### <a name="if-youre-using-eclipse-toocreate-a-maven-or-dynamic-web-project-"></a>Se você estiver usando o Eclipse toocreate um projeto Web dinâmico ou Maven...
Saudação de uso [SDK do Application Insights para Java plug-in][eclipse].

#### <a name="if-youre-using-maven"></a>Se você estiver usando o Maven...
Se o projeto já está definido toouse Maven para compilação, mescle Olá arquivo de pom.xml de tooyour de código a seguir.

Em seguida, atualizar Olá projeto dependências tooget Olá binários baixados.

```XML

    <repositories>
       <repository>
          <id>central</id>
          <name>Central</name>
          <url>http://repo1.maven.org/maven2</url>
       </repository>
    </repositories>

    <dependencies>
      <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-web</artifactId>
        <!-- or applicationinsights-core for bare API -->
        <version>[1.0,)</version>
      </dependency>
    </dependencies>
```

* *Erros de build ou validação de soma de verificação?* Tente usar uma versão específica, como: `<version>1.0.n</version>`. Você encontrará versão mais recente Olá Olá [notas de versão do SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) ou no nosso [artefatos Maven](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).
* *Necessário tooupdate tooa SDK novo?* Atualize as dependências do seu projeto.

#### <a name="if-youre-using-gradle"></a>Se você estiver usando o Gradle...
Se o projeto já está definido toouse Gradle para compilação, mescle Olá arquivo de gradle de tooyour de código a seguir.

Atualização Olá projeto dependências tooget Olá binários baixados.

```JSON

    repositories {
      mavenCentral()
    }

    dependencies {
      compile group: 'com.microsoft.azure', name: 'applicationinsights-web', version: '1.+'
      // or applicationinsights-core for bare API
    }
```

* *Erros de validação de soma de verificação ou compilação? Tente usar uma versão específica, como: ** `version:'1.0.n'`. *Você encontrará versão mais recente Olá Olá [notas de versão do SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*
* *tooupdate tooa novo SDK*
  * Atualize as dependências do seu projeto.

#### <a name="otherwise-"></a>Caso contrário...
Adicione manualmente Olá SDK:

1. Baixar Olá [SDK do Application Insights para Java](https://aka.ms/aijavasdk).
2. Extrair os binários de saudação do arquivo zip de saudação e adicioná-los tooyour projeto.

### <a name="questions"></a>Perguntas...
* *Qual é a relação de saudação entre hello `-core` e `-web` componentes ZIP Olá?*

  * `applicationinsights-core`Fornece Olá API vazio. Você sempre precisa desse componente.
  * `applicationinsights-web` fornece métricas que rastreiam as contagens de solicitação de HTTP e tempos de resposta. Você poderá omitir esse componente se não quiser que a telemetria seja coletada automaticamente. Por exemplo, se você quiser toowrite seus próprios.
* *Olá tooupdate SDK quando publicamos as alterações*

  * Baixar hello mais recente [SDK do Application Insights para Java](https://aka.ms/qqkaq6) e substituir Olá antigas.
  * As alterações são descritas no hello [notas de versão do SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).

## <a name="3-add-an-application-insights-xml-file"></a>3. Adicione um arquivo xml do Application Insights
Adicionar pasta de recursos do ApplicationInsights.xml toohello em seu projeto, ou verifique se que ele é adicionado o caminho de classe de implantação do projeto tooyour. Copie Olá XML a seguir para ele.

Substitua a chave de instrumentação Olá que você obteve Olá portal do Azure.

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- hello key from hello portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data tooeach event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```


* chave de instrumentação de saudação enviada juntamente com todos os itens de telemetria e informa ao Application Insights toodisplay-lo em seu recurso.
* Olá componente de solicitação HTTP é opcional. Ele envia automaticamente telemetria sobre solicitações e o portal de toohello de tempos de resposta.
* Correlação de eventos é um componente de solicitação HTTP de toohello de adição. Ele atribui uma solicitação de tooeach identificador recebida pelo servidor de saudação e adiciona esse identificador como um item de tooevery de propriedade de telemetria como propriedade Olá 'Operation.Id'. Ele permite toocorrelate telemetria de saudação associada com cada solicitação, definindo um filtro no [pesquisa diagnóstica][diagnostic].
* Olá Application Insights chave pode ser passada dinamicamente de saudação portal do Azure como uma propriedade do sistema (-DAPPLICATION_INSIGHTS_IKEY = your_ikey). Se não houver uma propriedade definida, ele verificará a variável de ambiente (APPLICATION_INSIGHTS_IKEY) nas Configurações do Aplicativo do Azure. Se ambas as propriedades de saudação são indefinidas, padrão Olá InstrumentationKey é usado no ApplicationInsights.xml. Esta sequência ajuda toomanage InstrumentationKeys diferentes para diferentes ambientes dinamicamente.

### <a name="alternative-ways-tooset-hello-instrumentation-key"></a>Chave de instrumentação modos alternativos tooset Olá
SDK do Application Insights procura chave Olá nesta ordem:

1. Propriedade do sistema: -DAPPLICATION_INSIGHTS_IKEY=your_ikey
2. Variável de ambiente: APPLICATION_INSIGHTS_IKEY
3. Arquivo de configuração: ApplicationInsights.xml

Você também pode [defini-lo no código](app-insights-api-custom-events-metrics.md#ikey):

```Java

    telemetryClient.InstrumentationKey = "...";
```

## <a name="4-add-an-http-filter"></a>4. Adicionar um filtro HTTP
a última etapa de configuração Olá permite toolog de componente de solicitação HTTP Olá cada solicitação da web. (Não necessárias se você quiser apenas API bare hello.)

Localize e abra o arquivo Web. XML de saudação em seu projeto e saudação de mesclagem após o código sob o nó de aplicativo web hello, onde os filtros de aplicativo estão configurados.

resultados mais precisos tooget hello, filtro Olá devem ser mapeados antes de todos os outros filtros.

```XML

    <filter>
      <filter-name>ApplicationInsightsWebFilter</filter-name>
      <filter-class>
        com.microsoft.applicationinsights.web.internal.WebRequestTrackingFilter
      </filter-class>
    </filter>
    <filter-mapping>
       <filter-name>ApplicationInsightsWebFilter</filter-name>
       <url-pattern>/*</url-pattern>
    </filter-mapping>
```

#### <a name="if-youre-using-spring-web-mvc-31-or-later"></a>Se você estiver usando Spring Web MVC 3.1 ou posterior
Editar esses elementos em *-pacote de aplicativo Insights servlet tooinclude hello:

```XML

    <context:component-scan base-package=" com.springapp.mvc, com.microsoft.applicationinsights.web.spring"/>

    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <bean class="com.microsoft.applicationinsights.web.spring.RequestNameHandlerInterceptorAdapter" />
        </mvc:interceptor>
    </mvc:interceptors>
```

#### <a name="if-youre-using-struts-2"></a>Se você estiver usando o Struts 2
Adicione esse arquivo de configuração do item toohello Struts (geralmente nomeado struts.xml ou default.xml struts):

```XML

     <interceptors>
       <interceptor name="ApplicationInsightsRequestNameInterceptor" class="com.microsoft.applicationinsights.web.struts.RequestNameInterceptor" />
     </interceptors>
     <default-interceptor-ref name="ApplicationInsightsRequestNameInterceptor" />
```

(Se você tiver interceptores definidos em uma pilha padrão, interceptador Olá pode simplesmente ser adicionada pilha toothat).

## <a name="5-run-your-application"></a>5. Execute seu aplicativo.
Ou executá-lo no modo de depuração no computador de desenvolvimento ou publicar tooyour server.

## <a name="6-view-your-telemetry-in-application-insights"></a>6. Exibir sua telemetria no Application Insights
Retornar recurso Application Insights tooyour [portal do Microsoft Azure](https://portal.azure.com).

Dados de solicitações HTTP é exibida na folha de visão geral de saudação. (Se não estiverem lá, aguarde alguns segundos e, em seguida, clique em Atualizar.)

![dados de exemplo](./media/app-insights-java-get-started/5-results.png)

[Saiba mais sobre métricas.][metrics]

Clique em qualquer toosee de gráfico mais detalhada agregado métricas.

![](./media/app-insights-java-get-started/6-barchart.png)

> Application Insights assume o formato Olá de solicitações HTTP para aplicativos MVC é: `VERB controller/action`. Por exemplo, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` e `GET Home/Product/sdf96vws` são agrupados em `GET Home/Product`. Esse agrupamento habilita agregações significativas de solicitações, como o número de solicitações e o tempo médio de execução para solicitações.
>
>

### <a name="instance-data"></a>Dados de instância
Clique em instâncias individuais do tipo toosee uma solicitação específica.

Dois tipos de dados são exibidos no Application Insights: dados agregados, armazenados e exibidos como médias, contagens e somas, e dados de instância ‒ relatórios individuais de solicitações HTTP, exceções, exibições de página ou eventos personalizados.

Ao exibir as propriedades de saudação de uma solicitação, você pode ver eventos de telemetria Olá associados a ele, como solicitações e exceções.

![](./media/app-insights-java-get-started/7-instance.png)

### <a name="analytics-powerful-query-language"></a>Análise: linguagem de consulta poderosa
Como você acumular mais dados, você pode executar consultas em ambos os tooaggregate dados e toofind instâncias individuais.  [Análise](app-insights-analytics.md) é uma ferramenta poderosa para entender o desempenho e o uso e para fins de diagnóstico.

![Exemplo de Análise](./media/app-insights-java-get-started/025.png)

## <a name="7-install-your-app-on-hello-server"></a>7. Instalar o aplicativo no servidor de saudação
Publicar o seu servidor de toohello de aplicativo agora, permitem que pessoas usá-lo e assista a telemetria Olá aparecerão no portal de saudação.

* Verifique se o firewall permite que seu aplicativo toosend telemetria toothese portas:

  * dc.services.visualstudio.com:443
  * f5.services.visualstudio.com:443

* Se o tráfego de saída precisar passar por um firewall, defina as propriedades do sistema `http.proxyHost` e `http.proxyPort`.

* Nos servidores Windows, instale:

  * [Microsoft Visual C++ redistribuível](http://www.microsoft.com/download/details.aspx?id=40784)

    (Esse componente habilita contadores de desempenho.)


## <a name="exceptions-and-request-failures"></a>Falhas de solicitação e exceções
Exceções sem tratamento são coletadas automaticamente:

![Abra Configurações, Falhas](./media/app-insights-java-get-started/21-exceptions.png)

dados toocollect outras exceções, você tem duas opções:

* [Inserir chama tootrackException() no seu código][apiexceptions].
* [Instalar Olá agente Java em seu servidor](app-insights-java-agent.md). Você especificar métodos Olá toowatch desejado.

## <a name="monitor-method-calls-and-external-dependencies"></a>Monitorar chamadas de método e dependências externas
[Instalar Olá agente Java](app-insights-java-agent.md) toolog especificado métodos internos e as chamadas feitas por meio do JDBC, com dados de tempo.

## <a name="performance-counters"></a>Contadores de desempenho
Abra **configurações**, **servidores**, toosee uma variedade de contadores de desempenho.

![](./media/app-insights-java-get-started/11-perf-counters.png)

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

![](./media/app-insights-java-get-started/12-custom-perfs.png)

### <a name="unix-performance-counters"></a>Contadores de desempenho do Unix
* [Instalar collectd com plug-in Application Insights de saudação](app-insights-java-collectd.md) tooget uma ampla variedade de dados de sistema e de rede.

## <a name="get-user-and-session-data"></a>Obter dados de usuário e de sessão
OK, você está enviando a telemetria do seu servidor Web. Agora tooget Olá visão de 360 graus completo do seu aplicativo, você pode adicionar mais monitoramento:

* [Adicionar páginas da web a telemetria tooyour] [ usage] toomonitor página exibições e métricas de usuário.
* [Configurar testes da web] [ availability] toomake-se de que seu aplicativo permanece em tempo real e responsivo.

## <a name="capture-log-traces"></a>Capturar rastreamentos de log
Você pode usar o Application Insights tooslice e nos dados de logs de Log4J, Logback ou outras estruturas de registro em log. Você pode correlacionar os logs de saudação com solicitações HTTP e outra telemetria. [Saiba como][javalogs].

## <a name="send-your-own-telemetry"></a>Enviar sua própria telemetria
Agora que você instalou Olá SDK, você pode usar Olá API toosend sua telemetria.

* [Rastrear eventos personalizados e métricas] [ api] toolearn que os usuários estão fazendo com o seu aplicativo.
* [Pesquisar eventos e logs de] [ diagnostic] toohelp diagnosticar problemas.

## <a name="availability-web-tests"></a>Testes de disponibilidade na Web
Application Insights pode testar seu site em toocheck em intervalos regulares que ele está ativo e também responder. [tooset backup][availability], clique em testes da Web.

![Clique em Testes na Web e em Adicionar Teste na Web](./media/app-insights-java-get-started/31-config-web-test.png)

Se seu site ficar inativo, você obterá gráficos de tempos de resposta e também notificações por email.

![Exemplo de teste da Web](./media/app-insights-java-get-started/appinsights-10webtestresult.png)

[Saiba mais sobre testes de disponibilidade via web.][availability]

## <a name="questions-problems"></a>Perguntas? Problemas?
[Solucionar problemas de Java](app-insights-java-troubleshoot.md)

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Próximas etapas
* [Monitorar chamadas de dependência](app-insights-java-agent.md)
* [Monitorar os contadores de desempenho do Unix](app-insights-java-collectd.md)
* Adicionar [monitoramento páginas da web de tooyour](app-insights-javascript.md) tempo de carregamento de página toomonitor, chamadas AJAX, exceções de navegador.
* Gravar [telemetria personalizada](app-insights-api-custom-events-metrics.md) tootrack uso no navegador de saudação ou no servidor de saudação.
* Criar [painéis](app-insights-dashboards.md) toobring gráficos-chave Olá juntos para seu sistema de monitoramento.
* Usar [Análise](app-insights-analytics.md) para consultas avançadas por telemetria a o aplicativo
* Para saber mais, visite [Azure para desenvolvedores Java](/java/azure).

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#trackexception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[usage]: app-insights-javascript.md
