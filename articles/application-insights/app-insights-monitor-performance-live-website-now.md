---
title: aplicativo com o Azure Insights de aplicativo da web aaaMonitor um ASP.NET ao vivo | Microsoft Docs
description: "Monitore o desempenho do site sem implantá-lo novamente. Funciona com aplicativos web ASP.NET hospedado no local, em máquinas virtuais ou no Azure."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 769a5ea4-a8c6-4c18-b46c-657e864e24de
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: 0d53f0a59974f40767fae681bafc4f358d1283a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="instrument-web-apps-at-runtime-with-application-insights"></a>Instrumentar aplicativos Web no tempo de execução com o Application Insights


Você pode instrumentar um aplicativo web em tempo real com informações de aplicativo do Azure, sem ter que toomodify ou reimplantar seu código. Se os seus aplicativos forem hospedados por um servidor IIS local, instale o Monitor de Status. Caso de aplicativos web do Azure ou executados em uma VM do Azure, você pode alternar no monitoramento do Application Insights hello Azure no painel de controle. (Também há artigos separados sobre como instrumentar os [aplicativos Web J2EE dinâmicos](app-insights-java-live.md) e os [Serviços de Nuvem do Azure](app-insights-cloudservices.md).) É necessário ter uma assinatura do [Microsoft Azure](http://azure.com) .

![gráficos de exemplo](./media/app-insights-monitor-performance-live-website-now/10-intro.png)

Você tem a opção de três rotas tooapply Application Insights tooyour .NET web aplicativos:

* **Tempo de compilação:** [Olá adicionar SDK do Application Insights] [ greenbrown] tooyour código de aplicativo de web.
* **Tempo de execução:** instrumentar seu aplicativo web no servidor de saudação, conforme descrito abaixo, sem recompilar e reimplantar o código de saudação.
* **Ambos:** criar hello SDK em seu código de aplicativo web e também se aplicam a extensões de tempo de execução de saudação. Olá obter o melhor de ambas as opções.

Aqui está um resumo do que você tem com cada rota:

|  | Tempo de compilação | Tempo de execução |
| --- | --- | --- |
| Solicitações e exceções |Sim |Sim |
| [Exceções mais detalhadas](app-insights-asp-net-exceptions.md) | |Sim |
| [Diagnóstico de dependência](app-insights-asp-net-dependencies.md) |No .NET 4.6+, mas menos detalhes |Sim, detalhes completos: códigos de resultado, texto do comando SQL, verbo HTTP|
| [Contadores de desempenho do sistema](app-insights-performance-counters.md) |Sim |Sim |
| [API de telemetria personalizada][api] |Sim |Não |
| [Integração do log de rastreamento](app-insights-asp-net-trace-logs.md) |Sim |Não |
| [Exibição da página e dados do usuário](app-insights-javascript.md) |Sim |Não |
| Código de toorebuild necessário |Sim | Não |


## <a name="monitor-a-live-azure-web-app"></a>Monitorar um aplicativo da web ao vivo

Se seu aplicativo é executado como um serviço de web do Azure, aqui como tooswitch no monitoramento:

* Selecione o Application Insights no painel de controle de saudação do aplicativo no Azure.

    ![Configurar o Application Insights para um aplicativo Web do Azure](./media/app-insights-monitor-performance-live-website-now/azure-web-setup.png)
* Quando abre a página Resumo do Application Insights hello, clique o link de saudação na Olá inferior tooopen Olá completo recurso do Application Insights.

    ![Clique nas tooApplication Insights](./media/app-insights-monitor-performance-live-website-now/azure-web-view-more.png)

[Monitoramento de aplicativos de nuvem e a VM](app-insights-azure.md).

### <a name="enable-client-side-monitoring-in-azure"></a>Habilitar o monitoramento do lado do cliente no Azure

Se você tiver habilitado o Application Insights no Azure, você poderá adicionar telemetria de usuário e exibição de página.

1. Selecione Configurações > Configurações do Aplicativo
2.  Em configurações do aplicativo, adicione um novo par de chave/valor: 
   
    Chave: `APPINSIGHTS_JAVASCRIPT_ENABLED` 
    
    Valor: `true`
3. **Salvar** Olá configurações e **reiniciar** seu aplicativo.

Olá SDK de JavaScript do Application Insights agora é injetado em cada página da web.

## <a name="monitor-a-live-iis-web-app"></a>Monitorar um aplicativo de web IIS ao vivo

Se seu aplicativo estiver hospedado em um servidor do IIS, habilite o Application Insights usando o Monitor de Status.

1. No servidor Web IIS, entre com as credenciais de administrador.
2. Se o Application Insights Status Monitor não estiver instalado, baixe e execute Olá [instalador do Monitor de Status](http://go.microsoft.com/fwlink/?LinkId=506648) (ou execute [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) e procure nele Application Insights Status Monitor).
3. No Monitor de Status, selecione o aplicativo hello instalado ou o site que você deseja toomonitor. Entre com suas credenciais do Azure.

    Configure o recurso de saudação onde você deseja que os resultados de saudação toosee no portal do Application Insights hello. (Normalmente, é melhor toocreate um novo recurso. Selecione um recurso existente se você já tiver [testes da web][availability] ou [monitoramento de cliente][client] para esse aplicativo). 

    ![Escolha um aplicativo e um recurso.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-configAIC.png)

4. Reinicie o IIS.

    ![Escolha reiniciar na parte superior de saudação da caixa de diálogo de saudação.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-restart.png)

    O serviço Web é interrompido por um período curto.

## <a name="customize-monitoring-options"></a>Personalizar opções de monitoramento

A habilitação do Application Insights adiciona DLLs e Applicationinsights tooyour web app. Você pode [editar o arquivo. config de saudação](app-insights-configuration-with-applicationinsights-config.md) toochange algumas das opções de saudação.

## <a name="when-you-re-publish-your-app-re-enable-application-insights"></a>Quando você publicar novamente seu aplicativo, habilite novamente o Application Insights

Antes de publicar seu aplicativo novamente, considere [adicionando o código de toohello do Application Insights no Visual Studio][greenbrown]. Você obterá mais detalhada de telemetria e telemetria personalizada de toowrite de capacidade de saudação.

Se você quiser toore-publicar sem adicionar Application Insights toohello código, lembre-se de que o processo de implantação Olá pode excluir Olá DLLs e applicationinsights. config de saudação publicado o site da web. Portanto:

1. Se você tiver editado applicationinsights.config, faça uma cópia dele antes de publicar seu aplicativo novamente.
2. Republique seu aplicativo.
3. Habilite novamente o monitoramento do Application Insights. (Use o método apropriado de saudação: painel de controle de aplicativo web do Azure Olá ou Olá Monitor de Status em um host IIS.)
4. Reaplicar as edições realizadas no arquivo. config de saudação.


## <a name="troubleshooting-runtime-configuration-of-application-insights"></a>Solução de problemas de configuração de tempo de execução do Application Insights

### <a name="cant-connect-no-telemetry"></a>Não consegue se conectar? Sem telemetria?

* Abra [Olá portas de saída necessário](app-insights-ip-addresses.md#outgoing-ports) no toowork de Monitor de Status de tooallow de firewall do servidor.

* Abra o Monitor de Status e selecione seu aplicativo no painel esquerdo. Verifique se há mensagens de diagnóstico para este aplicativo no hello seção "Configuração de notificações":

  ![Abra a solicitação de toosee Olá desempenho folha, tempo de resposta, dependências e outros dados](./media/app-insights-monitor-performance-live-website-now/appinsights-status-monitor-diagnostics-message.png)
* No servidor de saudação, se você vir uma mensagem sobre "permissões insuficientes", tente seguir hello:
  * No Gerenciador do IIS, selecione o pool de aplicativos, abra **configurações avançadas**e, em **modelo de processo** Observe identidade hello.
  * No painel de controle de gerenciamento do computador, adicione esse grupo de usuários de Monitor de desempenho de toohello de identidade.
* Se você tiver o MMA/SCOM (Systems Center Operations Manager) instalado em seu servidor, algumas versões poderão entrar em conflito. Desinstalar o SCOM e o Monitor de Status e reinstale em versões mais recentes de saudação.
* Consulte [Solução de problemas][qna].

## <a name="system-requirements"></a>Requisitos do Sistema
Suporte de sistema operacional para Application Insights Status Monitor no servidor:

* Windows Server 2008
* Windows Server 2008 R2
* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

com o SP mais recente e o .NET Framework 4.5

No lado do cliente Olá: Windows 7, 8, 8.1 e 10, novamente com o .NET Framework 4.5

Suporte ao IIS: IIS 7, 7,5, 8 e 8.5 (o IIS é obrigatório)

## <a name="automation-with-powershell"></a>Automação com o PowerShell
Você pode iniciar e interromper o monitoramento usando o PowerShell no servidor IIS.

Primeiro importe o módulo do Application Insights hello:

`Import-Module 'C:\Program Files\Microsoft Application Insights\Status Monitor\PowerShell\Microsoft.Diagnostics.Agent.StatusMonitor.PowerShell.dll'`

Saiba quais aplicativos estão sendo monitorados:

`Get-ApplicationInsightsMonitoringStatus [-Name appName]`

* `-Name`Nome da saudação (opcional) de um aplicativo web.
* Exibe Olá status de monitoramento do Application Insights para cada aplicativo web (ou Olá denominado aplicativo) neste servidor IIS.
* Retorna `ApplicationInsightsApplication` para cada aplicativo:

  * `SdkState==EnabledAfterDeployment`: O aplicativo está sendo monitorado e foi instrumentado em tempo de execução, pela ferramenta de Monitor de Status de hello, ou por `Start-ApplicationInsightsMonitoring`.
  * `SdkState==Disabled`: aplicativo hello não está instrumentado para o Application Insights. Ele nunca foi instrumentado, tanto o monitoramento de tempo de execução foi desabilitado com a ferramenta de Monitor de Status de saudação ou com `Stop-ApplicationInsightsMonitoring`.
  * `SdkState==EnabledByCodeInstrumentation`: aplicativo hello foi instrumentado, adicionando o código-fonte toohello Olá SDK. Seu SDK não pode ser atualizado ou interrompido.
  * `SdkVersion`mostra a versão de saudação em uso para este aplicativo de monitoramento.
  * `LatestAvailableSdkVersion`mostra a versão de hello atualmente disponível na Galeria do NuGet hello. tooupgrade Olá aplicativo toothis a versão `Update-ApplicationInsightsMonitoring`.

`Start-ApplicationInsightsMonitoring -Name appName -InstrumentationKey 00000000-000-000-000-0000000`

* `-Name`nome de saudação do aplicativo hello no IIS
* `-InstrumentationKey`Olá ikey de saudação recurso do Application Insights onde você deseja Olá resultados toobe exibida.
* Este cmdlet afeta apenas os aplicativos que ainda não estão instrumentados - ou seja, SdkState==NotInstrumented.

    Olá cmdlet não afeta um aplicativo que já está instrumentado. Não importa se o aplicativo hello foi instrumentado no momento da compilação, adicionando Olá SDK toohello código, ou em tempo de execução por um uso anterior deste cmdlet.

    Olá SDK versão usada tooinstrument Olá aplicativo é versão hello mais recentemente baixado toothis server.

    versão mais recente do toodownload hello, use ApplicationInsightsVersion de atualização.
* Retorna `ApplicationInsightsApplication` se há êxito. Se ele falhar, ele registra um toostderr de rastreamento.

          Name                      : Default Web Site/WebApp1
          InstrumentationKey        : 00000000-0000-0000-0000-000000000000
          ProfilerState             : ApplicationInsights
          SdkState                  : EnabledAfterDeployment
          SdkVersion                : 1.2.1
          LatestAvailableSdkVersion : 1.2.3

`Stop-ApplicationInsightsMonitoring [-Name appName | -All]`

* `-Name`nome de saudação de um aplicativo no IIS
* `-All` Para o monitoramento de todos os aplicativos desse servidor IIS para o qual `SdkState==EnabledAfterDeployment`
* Interrompe o monitoramento Olá determinados aplicativos e remove a instrumentação. Ele só funciona para aplicativos que foram instrumentados em tempo de execução usando Olá, ferramenta de monitoramento de Status ou ApplicationInsightsApplication de início. (`SdkState==EnabledAfterDeployment`)
* Retorna ApplicationInsightsApplication.

`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]

* `-Name`: nome de saudação de um aplicativo web no IIS.
* `-InstrumentationKey` (Opcional.) Use que este toochange Olá recurso toowhich Olá telemetria do aplicativo é enviada.
* Este cmdlet:
  * Olá atualizações chamado toohello do aplicativo versão do SDK do hello mais recentemente baixado toothis máquina. (Só funciona se `SdkState==EnabledAfterDeployment`)
  * Se você fornecer uma chave de instrumentação, Olá denominado aplicativo é reconfigurado toosend telemetria toohello recursos com essa chave. (Funciona se `SdkState != Disabled`)

`Update-ApplicationInsightsVersion`

* Faz o download do servidor de toohello do SDK do Application Insights mais recente hello.

## <a name="questions"></a>Perguntas sobre o Status Monitor

### <a name="what-is-status-monitor"></a>O que é o Status Monitor?

Um aplicativo de desktop instalado no servidor web IIS. Ele ajuda você instrumentar e configurar aplicativos web. 

### <a name="when-do-i-use-status-monitor"></a>Quando eu devo usar o Status Monitor?

* tooinstrument qualquer aplicativo da web que está em execução no servidor IIS - mesmo se ele já está em execução.
* tooenable a telemetria adicional para aplicativos web que foram [criados com hello SDK do Application Insights](app-insights-asp-net.md) em tempo de compilação. 

### <a name="can-i-close-it-after-it-runs"></a>Eu posso fechá-lo depois de ser executado?

Sim. Depois que ele foi instrumentado sites Olá que você selecionar, você pode fechá-lo.

Ele não coleta telemetria por si só. Ele apenas configura os aplicativos web hello e define algumas permissões.

### <a name="what-does-status-monitor-do"></a>O que o Status Monitor faz?

Quando você seleciona um aplicativo web para o Monitor de Status tooinstrument:

* Baixa e coloca os assemblies do Application Insights hello e arquivo. config na pasta de binários do aplicativo da web de saudação.
* Modifica `web.config` módulo de controle de aplicativo Insights HTTP tooadd hello.
* Habilita o CLR toocollect chamadas de dependência de criação de perfil.

### <a name="do-i-need-toorun-status-monitor-whenever-i-update-hello-app"></a>É necessário o Monitor de Status de toorun sempre que atualiza o aplicativo hello?

Não ocorre se você reimplantar incrementalmente. 

Se você selecionar a opção de 'Excluir os arquivos existentes' de saudação em Olá processo de publicação, você deve executar toore Status Monitor tooconfigure Application Insights.

### <a name="what-telemetry-is-collected"></a>Qual telemetria é coletada?

Para aplicativos que você instrumenta apenas em tempo de execução usando o Status Monitor:

* Solicitações HTTP
* Chamadas toodependencies
* Exceções
* Contadores de desempenho

Para aplicativos já instrumentados em tempo de compilação:

 * Contadores de processo.
 * Chamadas de dependência (.NET 4.5); valores de retorno em chamadas de dependência (.NET 4.6).
 * Exceção dos valores do rastreamento de pilha.

[Saiba mais](http://apmtips.com/blog/2016/11/18/how-application-insights-status-monitor-not-monitors-dependencies/)

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next"></a>Próximas etapas

Exiba sua telemetria:

* [Explorar as métricas](app-insights-metrics-explorer.md) toomonitor desempenho e uso
* [Pesquisar eventos e logs de] [ diagnostic] toodiagnose problemas
* [Analise](app-insights-analytics.md) para obter mais consultas avançadas
* [Crie painéis](app-insights-dashboards.md)

Adicione mais telemetria:

* [Criar testes da web] [ availability] toomake-se de que o site permanece ativo.
* [Adicionar telemetria do cliente web] [ usage] toosee exceções do código de página da web e toolet inserir chamadas de rastreamento.
* [Adicione o código do SDK do Application Insights tooyour] [ greenbrown] para que você pode inserir o rastreamento e chamadas de log

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[roles]: app-insights-resources-roles-access-control.md
[usage]: app-insights-javascript.md
