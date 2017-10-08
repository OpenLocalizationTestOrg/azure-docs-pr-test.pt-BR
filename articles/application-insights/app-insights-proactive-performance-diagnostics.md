---
title: "aaaSmart detecção - anomalias de desempenho | Microsoft Docs"
description: "O Application Insights executa uma análise inteligente da telemetria do seu aplicativo e o avisa de possíveis problemas. Esse recurso não precisa de nenhuma configuração."
services: application-insights
documentationcenter: windows
author: antonfrMSFT
manager: carmonm
ms.assetid: 6acd41b9-fbf0-45b8-b83b-117e19062dd2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: bwren
ms.openlocfilehash: 60f10612188920330030129f7464e2f398ef1f2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection---performance-anomalies"></a>Detecção Inteligente - anomalias de desempenho

[Application Insights](app-insights-overview.md) automaticamente analisa o desempenho de saudação do seu aplicativo web e pode avisá-lo sobre problemas potenciais. Talvez você esteja lendo este artigo porque recebeu uma de nossas notificações de detecção inteligente.

Esse recurso não exige nenhuma configuração especial além de configurar seu aplicativo para o Application Insights (no [ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md) ou [Node.js](app-insights-nodejs.md) e no [código da página da Web](app-insights-javascript.md)). Ele fica ativo quando seu aplicativo gera telemetria suficiente.

## <a name="when-would-i-get-a-smart-detection-notification"></a>Quando eu receberia uma notificação de detecção inteligente?

Informações do aplicativo detectou que o desempenho de saudação do seu aplicativo foi degradado em uma das seguintes maneiras:

* **Reduzem o tempo de resposta** -seu aplicativo foi iniciado respondendo toorequests mais lentamente do que antes. alteração de saudação pode ter sido rápida, por exemplo devido a uma regressão em sua implantação mais recente. Ou pode ter sido gradual, talvez causada por uma perda de memória. 
* **Degradação de duração de dependência** -seu aplicativo faz chamadas tooa REST API, banco de dados ou outras dependências. dependência Olá é responder mais lentamente do que antes.
* **Padrão de desempenho lento** -seu aplicativo aparece toohave um desempenho de problema que está afetando apenas algumas solicitações. Por exemplo, as páginas estão sendo carregadas mais lentamente em um tipo de navegador do que em outros ou solicitações estão sendo atendidas de modo mais lento de um servidor específico. Atualmente, nossos algoritmos examinam os tempos de carregamento da página, os tempos de resposta de solicitação e os tempos de resposta de dependência.  

Detecção inteligente requer pelo menos 8 dias de telemetria em um volume viável em ordem tooestablish uma linha de base de desempenho normal. Portanto, após o aplicativo ser executado por esse período, qualquer problema significativo resultará em uma notificação.


## <a name="does-my-app-definitely-have-a-problem"></a>Meu aplicativo definitivamente tem um problema?

Não, uma notificação não significa que seu aplicativo definitivamente tem um problema. Ele é simplesmente uma sugestão sobre algo que talvez você queira toolook em mais de perto.

## <a name="how-do-i-fix-it"></a>Como corrigi-la?

notificações de saudação incluem informações de diagnóstico. Aqui está um exemplo:


![Veja um exemplo de detecção de Degradação do tempo de resposta do servidor](./media/app-insights-proactive-diagnostics/server_response_time_degradation.png)

1. **Triagem**. notificação de saudação mostra quantos usuários ou quantas operações são afetadas. Isso pode ajudá-lo a atribuir a um problema de toohello prioridade.
2. **Escopo**. Problema de saudação está afetando todo o tráfego ou apenas algumas páginas? É restringido de it tooparticular navegadores ou locais? Essas informações podem ser obtidas da notificação de saudação.
3. **Diagnosticar**. Geralmente, as informações de diagnóstico de saudação na notificação de saudação sugerirá natureza de saudação do problema de saudação. Por exemplo, se o tempo de resposta fica mais lento quando a taxa de solicitação está alta, o que sugere que seu servidor ou suas dependências estão sobrecarregadas. 

    Caso contrário, abra a folha de desempenho de saudação no Application Insights. Nela, você encontrará dados do [Criador de Perfil](app-insights-profiler.md). Se as exceções são geradas, você também pode tentar Olá [depurador instantâneo](app-insights-snapshot-debugger.md).



## <a name="configure-email-notifications"></a>Configurar notificações por email

As notificações de detecção inteligentes são habilitadas por padrão e enviadas toothose que têm [proprietários, Contribuidores e leitores que acessam o recurso do Application Insights toohello](app-insights-resources-roles-access-control.md). toochange isso, clique em **configurar** Olá notificação por email ou abrir as configurações de detecção inteligente no Application Insights. 
  
  ![Configurações de Detecção Inteligente](./media/app-insights-proactive-diagnostics/smart_detection_configuration.png)
  
  * Você pode usar o hello **cancelar a assinatura** link no hello detecção inteligente email toostop receber notificações por email de saudação.

Emails sobre anomalias de desempenho de detecções inteligente são limitadas tooone email por dia por recurso do Application Insights. Olá email será enviado somente se houver pelo menos um novo problema foi detectado em um dia. Você não receberá nenhuma mensagem repetida. 

## <a name="faq"></a>Perguntas frequentes

* *Então, vocês examinam os meus dados?*
  * Não. serviço de saudação é totalmente automático. Obter somente as notificações de saudação. Os dados são [privados](app-insights-data-retention-privacy.md).
* *Você analisar todos os dados de saudação coletados pelo Application Insights?*
  * Não no momento. Atualmente, analisamos o tempo de resposta de solicitação, o tempo de resposta da dependência e o tempo de carregamento da página. A análise de métricas adicionais está em nossa lista de pendências para o futuro.

* Com que tipos de aplicativo ele funciona?
  * Esses degradações são detectadas em qualquer aplicativo que gera a telemetria de saudação apropriado. Se você tiver instalado o Application Insights em seu aplicativo Web, as solicitações e as dependências serão monitoradas automaticamente. Mas em serviços de back-end ou outros aplicativos, se você inseriu chamadas muito[TrackRequest()](app-insights-api-custom-events-metrics.md#trackrequest) ou [TrackDependency](app-insights-api-custom-events-metrics.md#trackdependency), detecção inteligente funcionará no hello mesmo modo.

* *Posso criar minhas próprias regras de detecção de anomalias ou personalizar regras existentes?*

  * Ainda não, mas você pode:
    * [Configurar alertas](app-insights-alerts.md) que informam quando uma métrica excede um limite.
    * [Exportar telemetria](app-insights-export-telemetry.md) tooa [banco de dados](app-insights-code-sample-export-sql-stream-analytics.md) ou [tooPowerBI](app-insights-export-power-bi.md), em que você possa analisá-lo por conta própria.
* *A frequência com a análise de saudação é executada?*

  * Executamos Olá análise diariamente na telemetria Olá da saudação (dia inteiro no fuso horário UTC) do dia anterior.
* *Então isso substitui os [alertas de métrica](app-insights-alerts.md)?*
  * Não.  Nós não confirmar toodetecting cada comportamento que você pode considerar anormal.


* *Se eu não fazer nada em resposta tooa notificação, posso obter um lembrete?*
  * Não, você receberá uma mensagem sobre cada problema apenas uma vez. Se o problema de saudação persistir, ele será atualizado em Olá que detecção inteligente feed folha.
* *Perdi email hello. Onde posso encontrar notificações Olá no portal de Olá?*
  * Na visão geral do Application Insights de saudação do seu aplicativo, clique em Olá **detecção inteligente** lado a lado. Lá, você estará toofind capaz de que fazer todas as notificações de backup too90 dias.

## <a name="how-can-i-improve-performance"></a>Como posso melhorar o desempenho?
Respostas lentas e com falha são uma das maiores frustrações Olá para usuários do site da web, como você sabe, pela sua própria experiência. Portanto, é importante tooaddress Olá problemas.

### <a name="triage"></a>Triagem
Primeiro, isto é importante? Se uma página é sempre tooload lento, mas apenas 1% dos usuários do site tiver toolook-lo, talvez você tenha toothink de coisas mais importante sobre. Em Olá outro lado, se apenas 1% dos usuários abri-lo, mas ele lança exceções sempre, que talvez valha a pena investigar.

Use a instrução de impacto de saudação (usuários afetados ou % de tráfego) como guia geral, mas lembre-se de que não seja história toda hello. Colete outros tooconfirm evidência.

Considere a possibilidade de parâmetros de saudação do problema de saudação. Se for dependente da geografia, configure os [testes de disponibilidade](app-insights-monitor-web-app-availability.md) incluindo a região; talvez a área esteja simplesmente enfrentando problemas de rede.

### <a name="diagnose-slow-page-loads"></a>Diagnosticar carregamentos lentos de página
Onde está o problema Olá? É toorespond lenta de servidor de saudação, é muito longa de página hello, ou navegador Olá tenha toodo muito trabalho toodisplay-lo?

Abra a folha de métricas de navegadores hello. Olá segmentada exibição de navegador página carga tempo mostra onde o tempo de saudação será. 

* Se **enviar solicitação de tempo** é alto, o servidor de saudação estiver respondendo lentamente ou solicitação de saudação é post com uma grande quantidade de dados. Examinar Olá [métricas de desempenho](app-insights-web-monitor-performance.md#metrics) tooinvestigate tempos de resposta.
* Configurar [dependência controle](app-insights-asp-net-dependencies.md) toosee se a lentidão de saudação é devido tooexternal serviços ou o banco de dados.
* Se **Recebendo Resposta** for predominante, sua página e seus componentes dependentes, JavaScript, CSS, imagens e assim por diante (mas não os dados carregados de forma assíncrona) serão longos. Configurar um [teste de disponibilidade](app-insights-monitor-web-app-availability.md), e ser tooset se partes do hello opção tooload dependentes. Quando você receber alguns resultados, abra os detalhes de saudação do resultado de uma e expanda-a como toosee Olá tempos de arquivos diferentes de carregamento.
* Um **Tempo de Processamento do Cliente** alto sugere que os scripts estão sendo executados lentamente. Se o motivo Olá não é óbvio, considere adicionar um código de tempo e envie vezes Olá em chamadas trackMetric.

### <a name="improve-slow-pages"></a>Aprimorar páginas lentas
Não há uma web completa de aviso em melhorar sua respostas do servidor e os tempos de carregamento de página, então não tentaremos toorepeat todos os aqui. Aqui estão algumas dicas que você provavelmente já conhece, tooget apenas você pensa em:

* Lento Carregando devido a arquivos grandes: carregar scripts hello e outras partes de forma assíncrona. Use o agrupamento de script. Quebre a página principal de saudação em widgets que carregam seus dados separadamente. Não enviar o HTML antigo simples para tabelas longas: usar um script toorequest Olá de dados como JSON ou outro formato compacto e preencha a tabela Olá em vigor. Há toohelp excelente estruturas com tudo isso. (Que também envolvem scripts grandes, é claro).
* Diminuir as dependências do servidor: considere Olá localizações geográficas de seus componentes. Por exemplo, se você estiver usando o Azure, certifique-se de Olá web server e banco de dados de saudação estão em Olá mesma região. As consultas recuperam mais informações do que o necessário? O armazenamento em cache ou o envio em lote ajudaria?
* Problemas de capacidade: examinar as métricas do servidor de saudação de tempos de resposta e contagens de solicitações. Se os tempos de resposta apresentarem picos desproporcionais, com picos nas contagens de solicitação, é provável que seus servidores estejam alongados.


## <a name="server-response-time-degradation"></a>Degradação do tempo de resposta do servidor

notificação de degradação de tempo de resposta de saudação informa:

* tempo de resposta de saudação comparados toonormal tempo de resposta para esta operação.
* Quantos usuários são afetados.
* Tempo médio de resposta e o tempo de resposta 90º percentil para esta operação no dia Olá de detecção de saudação e sete dias antes. 
* Contagem de solicitações esta operação no dia de saudação da detecção de saudação e sete dias antes.
* A correlação entre a degradação nessa operação e degradações em dependências relacionadas. 
* Vincula toohelp diagnosticar o problema de saudação.
  * Profiler rastreia toohelp exibir onde o tempo de operação é gasto (link hello está disponível se os exemplos de rastreamento do Profiler foram coletados para esta operação durante o período de detecção de saudação). 
  * Relatórios de desempenho no Gerenciador de Métricas, nos quais você pode dividir e os filtros/intervalos de tempo para a operação.
  * Chamadas de pesquisa para este tooview propriedades chamadas específicas.
  * Relatórios de falha - se a contagem de > 1, isso significa que não houve falhas nesta operação que pode ter contribuído tooperformance degradação.

## <a name="dependency-duration-degradation"></a>Degradação da duração da dependência

Aplicativos modernos mais adotar a abordagem de design de serviços micro, que, em muitos casos, leva tooheavy confiabilidade em serviços externos. Por exemplo, se seu aplicativo depende de alguns plataforma de dados ou mesmo se você criar seus próprios bot serviço você provavelmente retransmitirá em algumas tooenable de provedor de serviços cognitivos seu toointeract bots maneiras mais humanos e alguns dados de serviço de saudação do bot toopull de armazenamento respostas do.  

Exemplo de notificação de degradação de dependência:

![Veja um exemplo de detecção de Degradação da duração da dependência](./media/app-insights-proactive-diagnostics/dependency_duration_degradation.png)

Observe o que ele diz:

* duração de saudação comparados toonormal tempo de resposta para esta operação
* Quantos usuários são afetados
* Duração média e duração de percentil 90º para essa dependência no dia de saudação da detecção de saudação e sete dias antes
* Número de dependência chama no dia de saudação da detecção de saudação e sete dias antes
* Links toohelp diagnosticar o problema de saudação
  * Relatórios de desempenho no Explorador de Métricas para essa dependência
  * Chamadas de pesquisa para essa dependência tooview propriedades de chamadas
  * Relatórios de falha - se a detecção de Olá contagem > 1, isso significa que houve falha de dependência chama durante o período que pode ter contribuído tooduration degradação. 
  * Abra o Analytics com consultas que calculam a contagem e a duração dessa dependência  

## <a name="smart-detection-of-slow-performing-patterns"></a>Detecção Inteligente de padrões de desempenho lentos 

O Application Insights encontra problemas de desempenho que afetam apenas alguns dos seus usuários ou só afetam os usuários em alguns casos. Por exemplo, pode haver uma notificação de que o carregamento de páginas é mais lento em um tipo de navegador do que em outros ou de que solicitações forem atendidas de modo mais lento de um servidor específico. Ele também pode descobrir problemas associados com combinações de propriedades, como carregamentos de página lentos em uma área geográfica para clientes que usam um sistema operacional específico.  

Anomalias como essas são muito difícil toodetect apenas ao inspecionar dados hello, mas são mais comuns que você imagina. Elas geralmente só surgem quando seus clientes reclamam. Nesse ponto, é muito tarde: usuários Olá afetado já estiver alternando tooyour concorrentes!

Atualmente, nossos algoritmos de examinar os tempos de carregamento de página, os tempos de resposta de solicitação no servidor de saudação e tempos de resposta de dependência.  

Você não tem tooset qualquer limite ou configurar regras. Aprendizado de máquina e algoritmos de mineração de dados são padrões anormais toodetect usado.

![De alerta por email hello, clique em Olá link tooopen Olá relatório de diagnóstico no Azure](./media/app-insights-proactive-performance-diagnostics/03.png)

* **Quando** mostra Olá tempo Olá problema foi detectado.
* **O que** descreve:

  * problema de saudação detectado;
  * características de saudação do hello conjunto de eventos que encontramos exibido o comportamento de problema de saudação.
* Olá tabela compara o conjunto de saudação insatisfatório com comportamento de saudação média de todos os outros eventos.

Clique em Olá links tooopen Explorer métrica e a pesquisa de relatórios relevantes, filtrados em tempo de saudação e propriedades de Olá lenta a execução de conjunto.

Modificar Olá tempo intervalo e filtros tooexplore Olá telemetria.

## <a name="next-steps"></a>Próximas etapas
Essas ferramentas de diagnóstico ajudam a inspecionar a telemetria de saudação do seu aplicativo:

* [Criador de perfil](app-insights-profiler.md) 
* [Depurador instantâneo](app-insights-snapshot-debugger.md)
* [Analytics](app-insights-analytics-tour.md)
* [Diagnóstico inteligente do Analytics](app-insights-analytics-diagnostics.md)

As detecções inteligentes são totalmente automáticas. Mas você queria tooset alguns alertas mais?

* [Alertas de métrica configurados manualmente](app-insights-alerts.md)
* [Testes de disponibilidade na Web](app-insights-monitor-web-app-availability.md)
