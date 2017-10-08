---
title: um aplicativo Web de aaaMonitor | Microsoft Docs
description: Saiba como tooset o monitoramento em seu aplicativo Web
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: c2f5e9842c732a804f1caee5d67e53dad24e190a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-app-service"></a>Monitorar o Serviço de Aplicativo
Este tutorial orienta você por seu aplicativo de monitoramento e usando os problemas de toosolve de ferramentas de plataforma interna hello quando eles ocorrerem.

Cada seção deste documento será um recurso específico. Usar recursos de saudação juntos permitem que você:
- Identificar um problema em seu aplicativo.
- Determinando quando o problema de saudação é causado pela sua plataforma de código ou hello.
- Restrinja a origem de saudação de problema de saudação em seu código.
- Depure e corrija o problema de saudação.

## <a name="before-you-begin"></a>Antes de começar
- Você precisa de um aplicativo Web toomonitor e siga Olá descritas etapas.
    - Você pode criar um aplicativo hello etapas descritas Olá [criar um aplicativo ASP.NET no Azure com o banco de dados SQL](app-service-web-tutorial-dotnet-sqldatabase.md) tutorial.

- Se você quiser tootry out **depuração remota** do seu aplicativo, você precisará do Visual Studio.
    - Se você ainda não tiver o Visual Studio de 2017 instalado, você pode baixar e usar Olá livre [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).
    - Certifique-se de que você habilite **desenvolvimento do Azure** durante a instalação do Visual Studio hello.

## <a name="metrics"></a>Etapa 1 - Métricas de exibição
**Métricas** são toounderstand úteis:
- Integridade do aplicativo
- Desempenho do apliativo
- Consumo de recursos

Ao investigar um problema de aplicativo, revisar as métricas é um bom lugar toostart. Portal do Azure tem uma maneira rápida toovisually inspecionar as métricas de saudação do seu aplicativo usando **Azure Monitor**.

Métricas fornecem uma exibição histórica entre várias agregações chave para seu aplicativo. Para qualquer aplicativo hospedado no serviço de aplicativo, você deve monitorar Olá Web App e Olá plano de serviço de aplicativo.

> [!NOTE]
> Um plano de serviço de aplicativo representa a coleção de saudação de recursos físicos usados toohost seus aplicativos. Todos os aplicativos tooan do serviço de aplicativo plano compartilhamento Olá recursos atribuídos definida por ela, permitindo que você toosave custo ao hospedar vários aplicativos.
>
> Os Planos do Serviço de Aplicativo definem:
> * Região: Norte da Europa, Leste dos EUA, Sudeste da Ásia, etc.
> * Tamanho da instância: Pequeno, médio, grande, etc.
> * Contagem da Escala: uma, duas ou três instâncias, etc.
> * SKU: Gratuito, Compartilhado, Básico, Standard, Premium, etc.

métricas de tooreview para seu aplicativo Web, vá toohello **visão geral** folha do aplicativo hello deseja toomonitor. A partir daqui, você pode exibir um gráfico de métricas do seu aplicativo como um **bloco de monitoramento**. Clique em Olá bloco tooedit e configurar quais tooview de métricas e Olá toodisplay de intervalo de tempo.

Por folha de recursos de saudação padrão fornece uma exibição para Olá solicitações de aplicativos e erros de saudação última hora.
![Monitorar o aplicativo](media/app-service-web-tutorial-monitoring/app-service-monitor.png)

Como você pode ver no exemplo hello, temos um aplicativo que está gerando muitos **erros de servidor HTTP**. alto volume de saudação de erros é indicação de primeira Olá precisamos tooinvestigate este aplicativo.

> [!TIP]
> Saiba mais sobre o Monitor do Azure com hello links a seguir:
> - [Introdução ao Azure Monitor](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [Métricas do Azure](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [Métricas compatíveis com o Azure Monitor](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [Painéis do Azure](..\azure-portal\azure-portal-dashboards.md)

## <a name="alerts"></a>Etapa 2 - Configurar Alertas
**Alertas** pode ser configurado tootrigger em condições específicas para seu aplicativo.

Em [etapa 1 - métricas de exibição](#metrics), vimos que o aplicativo hello tinha um grande número de erros.

Permite configurar um alerta tooautomatically ser notificado quando ocorrerem erros. Nesse caso, estamos deseja toosend alerta hello e enviar por email sempre que o número de saudação de erros HTTP 50 X passa por um certo limite.

toocreate um alerta, navegue muito**monitoramento** > **alertas** e clique em **[+] adicionar alerta**.

![Alertas](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

Forneça valores para a configuração de alerta de saudação:
- **Recurso:** Olá toomonitor de site com o alerta de saudação.
- **Nome:** um nome para o alerta, nesse caso: *HTTP alta 50 X*.
- **Descrição:** explicação de texto sem formatação do que esse alerta está observando.
- **Alerta sobre:** alertas podem examinar eventos ou métricas, para este exemplo Estamos analisando as métricas.
- **Métrica:** que toomonitor métrica, nesse caso: *erros de servidor HTTP*.
- **Condição:** quando tooalert, neste caso, selecione Olá *maior* opção.
- **Limite:** o que é o valor toolook, nesse caso: *400*.
- **Período:** alertas operam em valor médio de saudação de uma métrica. Períodos menores geram alertas mais importantes. Neste caso temos *5 minutos*.
- **Os proprietários e colaboradores de e-mail:** nesse caso: *Habilitado*.

Agora que hello alerta é criado um email é enviado sempre hello aplicativo fica acima do limite de saudação configurada. Alertas ativos também podem ser examinados em Olá portal do Azure.

![Acionado alertas](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> Saiba mais sobre alertas do Azure com hello links a seguir:
> - [O que são alertas no Microsoft Azure?](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [Executar uma Ação com Base nas Métricas](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [Criar alertas de métricas](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <a name="companion"></a> Etapa 3 - Complemento do Serviço de Aplicativo
**Complemento de serviço de aplicativo** oferece uma maneira conveniente toomonitor seu aplicativo com uma experiência nativo em seu dispositivo móvel (iOS ou Android).

Use o Complemento do Serviço de Aplicativo para:
- Analisar as métricas de aplicativo
- Analisar e agir sobre alertas de aplicativos e recomendações
- Executar a solução de problemas básicos (Procurar, iniciar, parar, reiniciar Olá aplicativo)
- Recebe notificações por push para eventos críticos.

![Complemento do Serviço de Aplicativo](media/app-service-web-tutorial-monitoring/app-service-companion.png)

[![Loja de Aplicativos do Complemento do Serviço de Aplicativo](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![Google Play do Complemento do Serviço de Aplicativo ](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)

Você pode instalar o complemento de serviço de aplicativo do hello [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) ou [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)

## <a name="diagnose"></a> Etapa 4 - Diagnosticar e resolver problemas
**Diagnosticar e resolver problemas** ajuda a separar questões de aplicativo forma a problemas de plataforma. Ele também pode sugerir possíveis atenuações tooget toohealthy de fundo seu aplicativo Web.

![Diagnosticar e Resolver Problemas](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

Continuar com as etapas anteriores de formulário de exemplo de hello, podemos ver que aplicativo hello tem sido com disponibilidade problemas. Por outro lado, a disponibilidade da plataforma de saudação não foi movida de 100%.

Quando o aplicativo hello está tendo o problema e hello plataforma permaneça em funcionamento, ele é uma indicação clara que estamos lidando com um problema de aplicativo.

## <a name="logging"></a> Etapa 5 - Registrar em Log
Agora que já têm restringimos problema de aplicativo hello falhas tooan, podemos ver tooget de logs de aplicativo e servidor de saudação obter mais informações.

O registro permite que ambos os toocollect **Application Diagnostics** e **diagnósticos do servidor Web** logs para seu aplicativo Web.

### <a name="application-diagnostics"></a>Diagnóstico de Aplicativos
O diagnóstico de aplicativo permite que você toocapture rastreamentos produzidos pelo aplicativo hello em tempo de execução.

Adicionando rastreamento tooyour aplicativo melhora significativamente sua capacidade toodebug e problemas de ponto de pin.

No ASP.NET, você pode registrar rastreamentos de aplicativo usando [classe Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) toogenerate eventos que são capturados pela infraestrutura de log hello. Você também pode especificar a severidade de saudação do rastreamento Olá para filtragem mais fácil.

```csharp
public ActionResult Delete(Guid? id)
{
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id);
    if (id == null)
    {
        System.Diagnostics.Trace.TraceError("/Todos/Delete/ failed, ID is null");
        return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
    }
    Todo todo = db.Todoes.Find(id);
    if (todo == null)
    {
        System.Diagnostics.Trace.TraceWarning("/Todos/Delete/ failed, ID: " + id + " could not be found");
        return HttpNotFound();
    }
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id + "completed successfully");
    return View(todo);
}
```
log de aplicativo tooenable ir muito**monitoramento** > **Logs de diagnóstico** e habilitar o log de aplicativo usando as alternâncias de saudação.

![Monitorar o aplicativo](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

Logs de aplicativo podem ser um sistema de arquivos do aplicativo da Web armazenado tooyour ou enviados por push tooblob armazenamento. Para cenários de produção, é recomendado toouse armazenamento de blob.

> [!IMPORTANT]
> Habilitar o registro no log tem um impacto sobre o desempenho do aplicativo e a utilização de recursos. Para cenários de produção, logs de erros são recomendados. Somente habilite o registro no log mais detalhado quando investigar problemas.

 ### <a name="web-server-diagnostics"></a>Diagnóstico de Servidor Web
Logs do servidor Web são gerados, mesmo que seu aplicativo não é instrumentado. O Serviço de Aplicativo pode coletar três tipos diferentes de logs do servidor:

- **Log do Servidor Web**
    - Informações sobre transações HTTP usando Olá [formato de arquivo de log estendido W3C](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).
    - Útil ao determinar a métrica geral do site, como número de saudação de solicitações manipuladas ou quantas solicitações são de um endereço IP específico.
- **Logs de Erros Detalhados**
    - Informações detalhadas de erros para códigos de status HTTP que indiquem uma falha (código de status 400 ou superior).
    - [Saiba mais sobre o log de erro detalhado](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- **Rastreamento de Solicitações com Falha**
    - Informações detalhadas sobre solicitações com falha, incluindo um rastreamento de componentes do IIS Olá usado tooprocess Olá Olá e solicitação de tempo em cada componente.
    - Logs de solicitação com falha são úteis quando você tentar tooisolate o que está causando um erro HTTP específico.
    - [Saiba mais sobre falha de solicitação de rastreamento](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

log do servidor tooenable:
- Vá muito**monitoramento** > **Logs de diagnóstico**.
- Habilite tipos diferentes de saudação do diagnóstico de servidor da Web usando alternâncias de saudação.

![Monitorar o aplicativo](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> Habilitar o registro no log tem um impacto sobre o desempenho do aplicativo e a utilização de recursos. Para Cenários de Produção, os Logs de Erros são recomendados, Somente habilite o registro no log mais detalhado quando investigar problemas.

### <a name="accessing-logs"></a>Acessar Logs
Os logs armazenados no armazenamento de blobs são acessados usando o Gerenciador de Armazenamento do Azure. Logs armazenados no sistema de arquivos do aplicativo da Web hello são acessados por meio de FTP em Olá caminhos a seguir:

- **Logs de aplicativos** - `%HOME%/LogFiles/Application/`.
    - Essa pasta contém um ou mais arquivos de texto que contêm informações produzidas pelo log do aplicativo.
- **Falha de solicitação de rastreamento** - `%HOME%/LogFiles/W3SVC#########/`.
    - Esta pasta contém um arquivo XSL e um ou mais arquivos XML.
- **Logs de erro detalhadas** - `%HOME%/LogFiles/DetailedErrors/`.
    - Esta pasta contém um ou mais arquivos .htm com informações abrangentes sobre erros HTTP gerados pelo aplicativo.
- **Logs do Web Server** - `%HOME%/LogFiles/http/RawLogs`.
    - Esta pasta contém um ou mais arquivos de texto formatados usando o formato de arquivo de log estendido W3C de saudação.

## <a name="streaming"></a> Etapa 6 - Streaming de Log
Os logs de streaming são convenientes ao depurar um aplicativo desde que ele economiza tempo em comparação comparado muito[acessar logs de saudação](#Accessing-Logs) por meio de FTP.

O Serviço de Aplicativo pode fazer streaming de **Logs do Aplicativo** e **Logs do Servidor Web** conforme eles são gerados.

> [!TIP]
> Antes de tentar toostream logs, verifique se você habilitou coletar logs conforme descrito em Olá [log](#logging) seção.

logs de toostream ir muito**monitoramento**> **fluxo de Log**. Selecione **Logs do Aplicativo** ou **Logs do Servidor Web**, dependendo de quais informações você está procurando. A partir daqui, também pausar, reiniciar e limpar o buffer de saudação.

![Logs de streaming](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> Logs são gerados somente quando há tráfego no aplicativo hello, você também pode aumentar o nível de detalhes de saudação do tooget de logs mais informações ou eventos.

## <a name="remote"></a> Etapa 7 - Depuração Remota
Quando você tiver origem Olá apontada pin de problemas de aplicativos hello, usar **depuração remota** toowalk através do código de saudação.

Remota de depuração permite que você anexar um depurador tooyour aplicativo Web em execução na nuvem hello. Você pode definir pontos de interrupção, manipular memória diretamente, percorrer o código e até mesmo alterar o caminho de código Olá exatamente como faria para um aplicativo em execução localmente.

tooattach Olá depurador tooyour o aplicativo em execução na nuvem hello:

- Usando o Visual Studio de 2017, solução de saudação aberta para o aplicativo hello deseja toodebug
- Defina alguns pontos de interrupção, exatamente como faria para desenvolvimento local.
- Abra o **cloud explorer** (ctr + /, ctrl + x).
- Faça logon com suas credenciais do Azure, conforme necessário.
- Localizar Olá aplicativo deseja toodebug
- Selecione **Anexar depurador** Olá formulário **ações** painel.

![Depuração Remota](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

Visual Studio configura seu aplicativo para depuração remota e abre uma janela de navegador que navega tooyour aplicativo. Navegue pelos seus pontos de interrupção do aplicativo tootrigger e percorrer o código de saudação.

> [!WARNING]
> A execução em modo de depuração em produção não é recomendada. Se seu aplicativo de produção não é expandido toomultiple instâncias de servidor, depuração impedir o servidor web de saudação de solicitações de tooother está respondendo. Para solucionar problemas de produção, o melhor recurso é muito[configurar o log](#logging) e [Application Insights](#insights).



## <a name="explorer"></a> Etapa 8 - Gerenciador de Processos
Quando seu aplicativo é expandido toomore de uma instância, **Explorador de processos** pode ajudar a identificar problemas específicos da instância.

Use **Gerenciador de Processos** para:

- Enumere todos os processos de saudação instâncias diferentes do seu plano de serviço de aplicativo.
- Fazer drill down e exiba Olá identificadores e módulos associados a cada processo.
- Contagem de CPU do modo de exibição, o conjunto de trabalho e o Thread em Olá processar nível toohelp identificar processos sem controle
- Localize identificadores de arquivos abertos e, até mesmo, encerre uma instância de processo específico.

O Gerenciador de Processos pode estar em **Monitoramento** > **Explorador de Processos**.

![Gerenciador de Processos](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <a name="insights"></a> Etapa 9 - Application Insights
O **Application Insights** fornece perfil de aplicativo e recursos avançados de monitoramento para seu aplicativo.

Use o Application Insights toodetect e diagnosticar exceções e problemas de desempenho em seu aplicativo Web.

É possível habilitar o Application Insights para seu aplicativo Web em **Monitoramento** > **Application Insights**

> [!NOTE]
> Application Insights pode solicitar tooinstall Olá Application Insights site extensão toostart coleta de dados. Instalação da extensão do site Olá faz com que uma reinicialização do aplicativo.

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

Application Insights tem um recurso avançado definido, toolearn mais, siga os links de saudação incluídos no hello [próximas etapas](#next) seção.

## <a name="next"></a> Próximas etapas

 - [O que é o Application Insights](..\application-insights\app-insights-overview.md)
 - [Monitorar o desempenho do aplicativo Web do Azure com o Application Insights](..\application-insights\app-insights-azure-web-apps.md)
 - [Monitorar a disponibilidade e capacidade de resposta de qualquer site da Web com o Application Insights](..\application-insights\app-insights-monitor-web-app-availability.md)
