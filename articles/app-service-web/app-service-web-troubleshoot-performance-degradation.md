---
title: "desempenho do aplicativo web aaaSlow no serviço de aplicativo | Microsoft Docs"
description: "Este artigo ajuda você a solucionar problemas de desempenho de aplicativo Web lento no Serviço de Aplicativo do Azure."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: top-support-issue
keywords: "desempenho do aplicativo Web, aplicativo lento, lentidão do aplicativo"
ms.assetid: b8783c10-3a4a-4dd6-af8c-856baafbdde5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2016
ms.author: cephalin
ms.openlocfilehash: 3e56b99b48db0e7baae1fac797a7fcb9eff74c9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-slow-web-app-performance-issues-in-azure-app-service"></a>Solucionar problemas de desempenho de aplicativo Web lento no Serviço de Aplicativo do Azure
Este artigo ajuda você a solucionar problemas de desempenho de aplicativo Web lento no [Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714).

Se você precisar de mais ajuda a qualquer momento neste artigo, você pode contatar hello Azure especialistas em [hello Azure MSDN e Olá fóruns de estouro de pilha](https://azure.microsoft.com/support/forums/). Como alternativa, você também pode registrar um incidente de suporte do Azure. Vá toohello [site de suporte do Azure](https://azure.microsoft.com/support/options/) e clique em **suporte**.

## <a name="symptom"></a>Sintoma
Quando você procurar o aplicativo web de saudação, Olá páginas carga lenta e, às vezes, tempo limite.

## <a name="cause"></a>Causa
Esse problema geralmente é causado por questões no nível de aplicativo, como:

* solicitações de rede demorando muito
* código de aplicativo ou consultas de banco de dados sendo ineficientes
* aplicativo usando muita memória/CPU
* aplicativo falha devido a exceção tooan

## <a name="troubleshooting-steps"></a>Etapas para solucionar problemas
A solução de problemas pode ser dividida em três tarefas distintas, em ordem sequencial:

1. [Observar e monitorar o comportamento do aplicativo](#observe)
2. [Coletar dados](#collect)
3. [Reduzir o problema de saudação](#mitigate)

[Os Aplicativos Web do Serviço de Aplicativo](/services/app-service/web/) oferecem várias opções em cada etapa.

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a>1. Observar e monitorar o comportamento do aplicativo
#### <a name="track-service-health"></a>Controlar a integridade do serviço
O Microsoft Azure publica sempre que há uma degradação no desempenho ou interrupção do serviço. Você pode acompanhar a integridade de saudação do serviço de saudação em Olá [portal do Azure](https://portal.azure.com/). Para obter mais informações, confira [Controlar a integridade do serviço](../monitoring-and-diagnostics/insights-service-health.md).

#### <a name="monitor-your-web-app"></a>Monitorar seu aplicativo Web
Essa opção permite que você toofind out se seu aplicativo estiver com problemas. Na folha do seu aplicativo web, clique em Olá **solicitações e erros** lado a lado. Olá **métrica** folha mostra todas as métricas de saudação, você pode adicionar.

Algumas das métricas de saudação que você pode querer toomonitor de seu aplicativo web são

* Conjunto de trabalho de memória média
* Tempo médio de resposta
* Tempo de CPU
* Conjunto de trabalho de memória
* Solicitações

![monitorar o desempenho do aplicativo Web](./media/app-service-web-troubleshoot-performance-degradation/1-monitor-metrics.png)

Para obter mais informações, consulte:

* [Monitorar aplicativos Web no Serviço de Aplicativo do Azure](web-sites-monitor.md)
* [Receber notificações de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

#### <a name="monitor-web-endpoint-status"></a>Monitorar o status de ponto de extremidade da Web
Se você estiver executando seu aplicativo web em Olá **padrão** preço, aplicativos Web, você pode monitorar dois pontos de extremidade de três locais geográficos.

O monitoramento de ponto de extremidade configura testes da web de locais distribuídos geograficamente que testa o tempo de resposta e tempo de atividade de URLs de web. teste de saudação executa uma operação HTTP GET em tempo de resposta de Olá Olá web URL toodetermine e tempo de atividade de cada local. Cada local configurado executa um teste a cada cinco minutos.

O tempo de atividade é monitorado usando códigos de resposta HTTP e o tempo de resposta é medido em milissegundos. Teste de monitoramento falhará se Olá código de resposta HTTP for maior que ou igual too400 ou se resposta Olá leva mais de 30 segundos. Um ponto de extremidade é considerado disponível caso seus testes de monitoramento bem-sucedida de todos os Olá especificou locais.

tooset-lo, consulte [monitorar aplicativos no serviço de aplicativo do Azure](web-sites-monitor.md).

Veja também um vídeo sobre monitoramento de pontos de extremidade em [Mantendo os sites do Azure ativos e monitorando pontos de extremidade - com Stefan Schackow](https://channel9.msdn.com/Shows/Azure-Friday/Keeping-Azure-Web-Sites-up-plus-Endpoint-Monitoring-with-Stefan-Schackow)

#### <a name="application-performance-monitoring-using-extensions"></a>Monitoramento de desempenho de aplicativos usando extensões
Você também pode monitorar o desempenho do aplicativo usando *extensões de site*.

Cada aplicativo do serviço de aplicativo web fornece um ponto de extremidade de gerenciamento extensível que permite que você toouse um conjunto poderoso de ferramentas implantado como extensões de site. As extensões incluem: 

- Editores de código-fonte, como o [Visual Studio Team Services](https://www.visualstudio.com/products/what-is-visual-studio-online-vs.aspx). 
- Ferramentas de gerenciamento de recursos conectados como um banco de dados MySQL conectado tooa web app.

[Informações de aplicativo do Azure](/services/application-insights/) e [New Relic](/marketplace/partners/newrelic/newrelic/) são as duas extensões de site que estão disponíveis de monitoramento de desempenho de saudação. toouse New Relic, instale um agente em tempo de execução. toouse Insights do aplicativo do Azure, recriar seu código com um SDK, e você também pode instalar uma extensão que fornece acesso tooadditional dados. Olá SDK permite que você escreva o uso do código toomonitor hello e o desempenho do seu aplicativo mais detalhadamente.

toouse Application Insights, consulte [monitorar o desempenho em aplicativos da web](../application-insights/app-insights-web-monitor-performance.md).

Consulte toouse New Relic, [novo gerenciamento de desempenho de aplicativos Relic no Azure](../store-new-relic-cloud-services-dotnet-application-performance-management.md).

<a name="collect" />

### <a name="2-collect-data"></a>2. Coletar dados
ambiente de aplicativos Web Hello fornece funcionalidade de diagnóstico para obter informações de registro em log do servidor de web hello e o aplicativo da web hello. informações de saudação são separadas em Diagnóstico de servidor da web e o application diagnostics.

#### <a name="enable-web-server-diagnostics"></a>Habilitar o diagnóstico de servidor Web
Você pode habilitar ou desabilitar Olá tipos de logs a seguir:

* **Registro em Log Detalhado de Erros** - informações detalhadas de erros para códigos de status HTTP que indiquem uma falha (código de status 400 ou superior). Pode conter informações que podem ajudar a determinar por que o servidor de saudação retornou o código de erro de saudação.
* **Falha no rastreamento de solicitação** -informações detalhadas sobre solicitações com falha, incluindo um rastreamento de Olá IIS componentes usados tooprocess Olá solicitação e tempo Olá em cada componente. Isso pode ser útil se você está tentando executar o desempenho do aplicativo web tooimprove ou isolar o que está causando um erro HTTP específico.
* **Log de servidor Web** -informações sobre transações HTTP usando o formato de arquivo de log estendido W3C de saudação. Isso é útil ao determinar a métrica geral de aplicativo web, como número de saudação de solicitações manipuladas ou quantas solicitações são de um endereço IP específico.

#### <a name="enable-application-diagnostics"></a>Habilitar o diagnóstico de aplicativos
Há várias opções toocollect aplicativo dados de desempenho de aplicativos Web, analisar seu aplicativo em tempo real do Visual Studio ou modificar sua toolog de código de aplicativo mais informações e rastreamentos. Você pode escolher opções de saudação com base no nível de acesso toohello aplicativo e observada de saudação ferramentas de monitoramento.

##### <a name="use-application-insights-profiler"></a>Use o Application Insights Profiler
Você pode habilitar Olá criador de perfil do aplicativo Insights toostart capturar rastreamentos de desempenho detalhada. Você pode acessar rastreamentos capturados backup toofive dias atrás quando precisar tooinvestigate problemas aconteceu em Olá anterior. Você pode escolher essa opção, contanto que tenha o recurso do Application Insights do aplicativo de web toohello acesso no portal do Azure.

O criador de perfil do aplicativo Insights fornece estatísticas em tempo de resposta para cada chamada de web e os rastreamentos que indica a linha de código causou Olá respostas lentas. Às vezes, hello aplicativo de serviço de aplicativo é lento como certos tipos de código não é gravado em um alto desempenho maneira. Exemplos incluem um código sequencial que pode ser executado em contenções de bloqueio do banco de dados paralelas e indesejadas. Removendo esses afunilamentos no código Olá aumenta o desempenho do aplicativo hello, mas são toodetect rígido sem configurar logs e rastreamentos elaborados. rastreamentos de saudação coletados pelo criador de perfil do Application Insights ajuda a identificar linhas de saudação do código diminui o aplicativo hello e superar esse desafio para os aplicativos de serviço de aplicativo.

 Para obter mais informações, consulte [Criação de perfil de aplicativos Web do Azure ativos com o Application Insights](../application-insights/app-insights-profiler.md).

##### <a name="use-remote-profiling"></a>Usar a criação de perfil remota
No Serviço de Aplicativo do Azure, Aplicativos Web, Aplicativos de API e WebJobs podem ter perfis criados remotamente. Escolha esta opção se você tem acesso toohello web app recursos e você sabe como tooreproduce Olá problema ou se você souber Olá exata ocorre problema de desempenho de saudação de intervalo de tempo.

Criação de perfil remota é útil se Olá uso da CPU do processo de saudação for alta e o processo está sendo executado mais lentamente do que o esperado ou latência de saudação de solicitações HTTP estão acima do normal, você pode remotamente o processo de perfil e obter Olá CPU amostragem chamada pilhas tooanalyze Hello atividade de processo e hot caminhos de código.

Para obter mais informações, consulte [Suporte à criação de perfil remota no Serviço de Aplicativo do Azure](https://azure.microsoft.com/blog/remote-profiling-support-in-azure-app-service).

##### <a name="set-up-diagnostic-traces-manually"></a>Configurar manualmente os rastreamentos de diagnóstico
Se você tiver código fonte do aplicativo web de toohello do access, o diagnóstico de aplicativo permite que informações toocapture produzidas por um aplicativo web. Aplicativos ASP.NET podem usar Olá `System.Diagnostics.Trace` classe toolog informações toohello aplicativo diagnóstico de log. No entanto, é necessário toochange Olá código e reimplantar o aplicativo. Esse método é recomendado se o aplicativo está sendo executado em um ambiente de teste.

Para obter instruções detalhadas sobre como tooconfigure seu aplicativo para o log, consulte [habilitar o log de diagnóstico para aplicativos web no serviço de aplicativo do Azure](web-sites-enable-diagnostic-log.md).

#### <a name="use-hello-azure-app-service-support-portal"></a>Use o portal de suporte do serviço de aplicativo do Azure Olá
Os aplicativos Web fornece Olá capacidade tootroubleshoot problemas relacionados tooyour web aplicativo examinando HTTP logs, logs de eventos, os despejos de processo e muito mais. Você pode acessar todas essas informações usando nosso portal de Suporte em **http://&lt;nome do aplicativo>.scm.azurewebsites.net/Support**

portal de suporte do serviço de aplicativo do Azure Olá fornece três guias separadas toosupport Olá três etapas de um cenário de solução de problemas comuns:

1. Observar o comportamento atual
2. Analisar a coleta de informações de diagnóstico e executando Olá analisadores internos
3. Atenuar

Se o problema de saudação estiver ocorrendo no momento, clique em **analisar** > **diagnóstico** > **diagnosticar agora** toocreate uma sessão de diagnóstico para você, que coleta logs de HTTP, logs do Visualizador de eventos, despejos de memória, logs de erros do PHP e relatório de processo do PHP.

Depois de saudação os dados são coletados, portal de suporte de saudação executa uma análise em dados hello e fornece um relatório HTML.

Caso você deseje dados de saudação toodownload, por padrão, ele seria armazenado na pasta de D:\home\data\DaaS hello.

Para obter mais informações sobre o portal de suporte do serviço de aplicativo do Azure hello, consulte [tooSupport de novas atualizações a extensão de Site para sites do Azure](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).

#### <a name="use-hello-kudu-debug-console"></a>Use Olá Kudu Console de depuração
Aplicativos Web vêm com um console de depuração que você pode usar para depuração, exploração, carregamento de arquivos, bem como para pontos de extremidade JSON para obter informações sobre seu ambiente. Esse console é chamado hello *Kudu Console* ou hello *SCM painel* para seu aplicativo web.

Você pode acessar este painel, vai toohello link **https://&lt;nome do aplicativo >.scm.azurewebsites.net/**.

Algumas das coisas Olá Kudu oferece são:

* configurações de ambiente para seu aplicativo
* fluxo de logs
* despejos de diagnóstico
* console de depuração no qual você pode executar os cmdlets do Powershell e os comandos básicos de DOS.

Outro recurso útil de Kudu é que, no caso de seu aplicativo está gerando exceções de primeira chance, você pode usar o Kudu e despejos de memória do hello SysInternals ferramenta Procdump toocreate. Esses despejos de memória são instantâneos do processo de saudação e podem geralmente ajudá-lo a solucionar problemas mais complexos com seu aplicativo web.

Para saber mais sobre os recursos disponíveis no Kudu, veja [Ferramentas online do Azure Websites Team Services que você precisa conhecer](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).

<a name="mitigate" />

### <a name="3-mitigate-hello-issue"></a>3. Reduzir o problema de saudação
#### <a name="scale-hello-web-app"></a>Escala Olá web app
No serviço de aplicativo do Azure, para aumentar o desempenho e a taxa de transferência, você pode ajustar a escala de saudação em que você estiver executando o aplicativo. Dimensionamento de um aplicativo web envolve duas ações relacionadas: alterando sua tooa de plano de serviço de aplicativo maior preço e determinadas configurações após a troca de toohello maior preço.

Para saber mais sobre como escalar, consulte [Escalar um aplicativo Web no Serviço de Aplicativo do Azure](web-sites-scale.md).

Além disso, você pode escolher toorun seu aplicativo em mais de uma instância. Escalar horizontalmente não apenas fornece mais capacidade de processamento, como também oferece alguma quantidade de tolerância a falhas. Se o processo de saudação falhar em uma instância, hello outras instâncias continuam tooserve solicitações.

Você pode definir Olá dimensionamento toobe Manual ou automático.

#### <a name="use-autoheal"></a>Usar AutoHeal
O AutoHeal recicla o processo do operador de saudação para seu aplicativo com base nas configurações que você escolha (como as alterações de configuração, solicitações, limites de memória ou tempo de saudação necessário tooexecute uma solicitação). A maioria do tempo de saudação Reciclar processos do hello são Olá toorecover de maneira mais rápida de um problema. Embora você sempre pode reiniciar o aplicativo web de saudação do diretamente no portal do Azure de saudação, AutoHeal faz isso automaticamente para você. Você só precisa toodo é adicionar alguns gatilhos no Web. config de raiz de saudação para seu aplicativo web. Essas configurações funcionaria em Olá mesma forma, mesmo que seu aplicativo não é um aplicativo .net.

Para saber mais, consulte [AutoHeal em sites do Azure](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).

#### <a name="restart-hello-web-app"></a>Reiniciar o aplicativo web de saudação
Reinicialização costuma Olá toorecover de maneira mais simples de problemas ocasionais. Em Olá [portal do Azure](https://portal.azure.com/), na folha do seu aplicativo web, você tem Olá opções toostop ou reiniciar o seu aplicativo.

 ![Reinicie os problemas de desempenho de toosolve de aplicativo web](./media/app-service-web-troubleshoot-performance-degradation/2-restart.png)

Você também pode gerenciar seu aplicativo Web usando o Azure Powershell. Para obter mais informações, consulte [Usando o PowerShell do Azure com o Azure Resource Manager](../powershell-azure-resource-manager.md).
