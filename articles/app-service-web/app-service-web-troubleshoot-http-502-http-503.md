---
title: "gateway incorreto de aaaFix 502, 503 serviço indisponíveis erros | Microsoft Docs"
description: "Solucionar problemas dos erros \"502 Gateway Incorreto\" e \"503 Serviço Indisponível\" no seu aplicativo Web hospedado no Serviço de Aplicativo do Azure."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: top-support-issue
keywords: "502 Gateway Incorreto, 503 Serviço Indisponível, erro 503, erro 502"
ms.assetid: 51cd331a-a3fa-438f-90ef-385e755e50d5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: d9d8dcddaac930967a2e8d2bfd8cad09e6824c17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-http-errors-of-502-bad-gateway-and-503-service-unavailable-in-your-azure-web-apps"></a>Solucionar problemas de erros HTTP de "502 Gateway Incorreto" e "503 Serviço Indisponível" em seus Aplicativos Web do Azure
"502 Gateway Incorreto" e "503 Serviço Indisponível" são os erros comuns em seu aplicativo Web hospedado no [Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714). Este artigo ajuda você a solucionar esses erros.

Se você precisar de mais ajuda a qualquer momento neste artigo, você pode contatar hello Azure especialistas em [hello Azure MSDN e Olá fóruns de estouro de pilha](https://azure.microsoft.com/support/forums/). Como alternativa, você também pode registrar um incidente de suporte do Azure. Vá toohello [site de suporte do Azure](https://azure.microsoft.com/support/options/) e clique em **suporte**.

## <a name="symptom"></a>Sintoma
Quando você procurar o aplicativo web de toohello, ele retorna um HTTP um HTTP ou erro de "502 Gateway incorreto" erro "503 serviço não disponível".

## <a name="cause"></a>Causa
Esse problema geralmente é causado por questões no nível de aplicativo, como:

* solicitações demorando muito
* aplicativo usando muita memória/CPU
* aplicativo falha devido a exceção tooan.

## <a name="troubleshooting-steps-toosolve-502-bad-gateway-and-503-service-unavailable-errors"></a>Solução de problemas de erros de "503 Serviço indisponível" e etapas toosolve "502 gateway incorreto"
A solução de problemas pode ser dividida em três tarefas distintas, em ordem sequencial:

1. [Observar e monitorar o comportamento do aplicativo](#observe)
2. [Coletar dados](#collect)
3. [Reduzir o problema de saudação](#mitigate)

[Os Aplicativos Web do Serviço de Aplicativo](/services/app-service/web/) oferecem várias opções em cada etapa.

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a>1. Observar e monitorar o comportamento do aplicativo
#### <a name="track-service-health"></a>Controlar a integridade do serviço
O Microsoft Azure publica sempre que há uma degradação no desempenho ou interrupção do serviço. Você pode acompanhar a integridade de saudação do serviço de saudação em Olá [Portal do Azure](https://portal.azure.com/). Para obter mais informações, confira [Controlar a integridade do serviço](../monitoring-and-diagnostics/insights-service-health.md).

#### <a name="monitor-your-web-app"></a>Monitorar seu aplicativo Web
Essa opção permite que você toofind out se seu aplicativo estiver com problemas. Na folha do seu aplicativo web, clique em Olá **solicitações e erros** lado a lado. Olá **métrica** folha mostrará todas as métricas de saudação, você pode adicionar.

Algumas das métricas de saudação que você pode querer toomonitor de seu aplicativo web são

* Conjunto de trabalho de memória média
* Tempo médio de resposta
* Tempo de CPU
* Conjunto de trabalho de memória
* Solicitações

![monitorar aplicativo Web para solucionar problemas de erros HTTP de 502 Gateway Incorreto e 503 Serviço Indisponível](./media/app-service-web-troubleshoot-HTTP-502-503/1-monitor-metrics.png)

Para obter mais informações, confira:

* [Monitorar aplicativos Web no Serviço de Aplicativo do Azure](web-sites-monitor.md)
* [Receber notificações de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

<a name="collect" />

### <a name="2-collect-data"></a>2. Coletar dados
#### <a name="use-hello-azure-app-service-support-portal"></a>Use Olá Portal de suporte do serviço de aplicativo do Azure
Os aplicativos Web fornece Olá capacidade tootroubleshoot problemas relacionados tooyour web aplicativo examinando HTTP logs, logs de eventos, os despejos de processo e muito mais. Você pode acessar todas essas informações usando nosso portal de Suporte em **http://&lt;nome do aplicativo>.scm.azurewebsites.net/Support**

portal de suporte de serviço de aplicativo do Azure Olá fornece três guias separadas toosupport Olá três etapas de um cenário de solução de problemas comuns:

1. Observar o comportamento atual
2. Analisar a coleta de informações de diagnóstico e executando Olá analisadores internos
3. Atenuar

Se o problema de saudação estiver ocorrendo no momento, clique em **analisar** > **diagnóstico** > **diagnosticar agora** toocreate uma sessão de diagnóstico para você, que coletará HTTP logs, logs do Visualizador de eventos, PHP, logs de erros do PHP e despejos de processam o relatório de memória.

Depois de saudação os dados são coletados, também será executar uma análise em dados de saudação e fornecer um relatório HTML.

Caso você deseje dados de saudação toodownload, por padrão, ele seria armazenado na pasta de D:\home\data\DaaS hello.

Para obter mais informações sobre o portal de suporte de serviço de aplicativo do Azure hello, consulte [tooSupport de novas atualizações a extensão de Site para sites do Azure](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).

#### <a name="use-hello-kudu-debug-console"></a>Use Olá Kudu Console de depuração
Aplicativos Web vêm com um console de depuração que você pode usar para depuração, exploração, carregamento de arquivos, bem como para pontos de extremidade JSON para obter informações sobre seu ambiente. Isso é chamado hello *Kudu Console* ou hello *SCM painel* para seu aplicativo web.

Você pode acessar este painel, vai toohello link **https://&lt;nome do aplicativo >.scm.azurewebsites.net/**.

Algumas das coisas Olá Kudu oferece são:

* configurações de ambiente para seu aplicativo
* fluxo de logs
* despejos de diagnóstico
* console de depuração no qual você pode executar os cmdlets do Powershell e os comandos básicos de DOS.

Outro recurso útil de Kudu é que, no caso de seu aplicativo está gerando exceções de primeira chance, você pode usar o Kudu e despejos de memória do hello SysInternals ferramenta Procdump toocreate. Esses despejos de memória são instantâneos do processo de saudação e podem geralmente ajudá-lo a solucionar problemas mais complexos com seu aplicativo web.

Para saber mais sobre recursos disponíveis no Kudu, consulte [Ferramentas online de Sites do Azure que você deve conhecer](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).

<a name="mitigate" />

### <a name="3-mitigate-hello-issue"></a>3. Reduzir o problema de saudação
#### <a name="scale-hello-web-app"></a>Escala Olá web app
No serviço de aplicativo do Azure, para aumentar o desempenho e a taxa de transferência, você pode ajustar a escala de saudação em que você estiver executando o aplicativo. Dimensionamento de um aplicativo web envolve duas ações relacionadas: alterando sua tooa de plano de serviço de aplicativo maior preço e determinadas configurações após a troca de toohello maior preço.

Para saber mais sobre como escalar, consulte [Escalar um aplicativo Web no Serviço de Aplicativo do Azure](web-sites-scale.md).

Além disso, você pode escolher toorun seu aplicativo em mais de uma instância. Isso não apenas fornece mais capacidade de processamento, como também oferece alguma quantidade de tolerância a falhas. Se hello processo falhar em uma instância, hello outra instância ainda continuará atender solicitações.

Você pode definir Olá dimensionamento toobe Manual ou automático.

#### <a name="use-autoheal"></a>Usar AutoHeal
O AutoHeal recicla o processo do operador de saudação para seu aplicativo com base nas configurações que você escolha (como as alterações de configuração, solicitações, limites de memória ou tempo de saudação necessário tooexecute uma solicitação). A maioria do tempo de saudação Reciclar processos do hello são Olá toorecover de maneira mais rápida de um problema. Embora você sempre pode reiniciar aplicativo web de saudação do diretamente dentro de saudação Portal do Azure, AutoHeal fará automaticamente para você. Você só precisa toodo é adicionar alguns gatilhos no Web. config de raiz de saudação para seu aplicativo web. Observe que essas configurações funcionaria em Olá mesma forma, mesmo que seu aplicativo não é um .net.

Para saber mais, consulte [AutoHeal em sites do Azure](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).

#### <a name="restart-hello-web-app"></a>Reiniciar o aplicativo web de saudação
Isso geralmente é Olá toorecover de maneira mais simples de problemas ocasionais. Em Olá [Portal do Azure](https://portal.azure.com/), na folha do seu aplicativo web, você tem Olá opções toostop ou reiniciar o seu aplicativo.

 ![Reinicie os erros do aplicativo toosolve HTTP 502 gateway incorreto e 503 serviço não disponível](./media/app-service-web-troubleshoot-HTTP-502-503/2-restart.png)

Você também pode gerenciar seu aplicativo Web usando o Azure Powershell. Para obter mais informações, consulte [Usando o PowerShell do Azure com o Azure Resource Manager](../powershell-azure-resource-manager.md).

