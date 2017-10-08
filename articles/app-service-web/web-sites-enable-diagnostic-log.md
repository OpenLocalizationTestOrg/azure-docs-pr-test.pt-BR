---
title: "aaaEnable o log de diagnóstico para aplicativos web no serviço de aplicativo do Azure"
description: "Saiba como o log de diagnóstico tooenable e adicione o aplicativo de tooyour de instrumentação, bem como tooaccess Olá informações registradas pelo Azure."
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: c9da27b2-47d4-4c33-a3cb-1819955ee43b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2016
ms.author: cephalin
ms.openlocfilehash: 4b2903ff31cc93180552cf51196c33505ffbaf07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-diagnostics-logging-for-web-apps-in-azure-app-service"></a>Habilitar o registro em log de diagnóstico para aplicativos Web no Serviço de Aplicativo do Azure
## <a name="overview"></a>Visão geral
Diagnóstico interno tooassist com a depuração do Azure fornece um [aplicativo do serviço de aplicativo web](http://go.microsoft.com/fwlink/?LinkId=529714). Neste artigo, você aprenderá como tooenable log de diagnóstico e adicione o aplicativo de tooyour de instrumentação, bem como tooaccess Olá informações registradas pelo Azure.

Este artigo usa Olá [Portal do Azure](https://portal.azure.com), PowerShell do Azure e hello Azure Interface de linha de comando (CLI do Azure) toowork com logs de diagnóstico. Para saber mais sobre como trabalhar com logs de diagnóstico usando o Visual Studio, confira [Solucionando problemas do Azure no Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="whatisdiag"></a>Diagnóstico de servidor Web e diagnóstico de aplicativos
Aplicativos do serviço de aplicativo web fornecem funcionalidade de diagnóstico para obter informações de registro em log do servidor de web hello e o aplicativo da web hello. Estes estão logicamente separados em **diagnóstico de servidor Web** e **diagnóstico de aplicativos**.

### <a name="web-server-diagnostics"></a>Diagnóstico de servidor Web
Você pode habilitar ou desabilitar Olá tipos de logs a seguir:

* **Registro em Log Detalhado de Erros** - informações detalhadas de erros para códigos de status HTTP que indiquem uma falha (código de status 400 ou superior). Pode conter informações que podem ajudar a determinar por que o servidor de saudação retornou o código de erro de saudação.
* **Falha no rastreamento de solicitação** -informações detalhadas sobre solicitações com falha, incluindo um rastreamento de Olá IIS componentes usados tooprocess Olá solicitação e tempo Olá em cada componente. Isso pode ser útil se você está tentando executar o desempenho do site tooincrease ou isolar o que está causando um toobe específico de erro HTTP retornado.
* **Log de servidor Web** -informações sobre transações HTTP usando Olá [formato de arquivo de log estendido W3C](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx). Isso é útil ao determinar a métrica geral do site como o número de saudação de solicitações administradas ou quantas solicitações são de um endereço IP específico.

### <a name="application-diagnostics"></a>diagnóstico de aplicativos
Diagnóstico de aplicativo permite que você toocapture informações produzidas por um aplicativo web. Aplicativos ASP.NET podem usar Olá [Trace](http://msdn.microsoft.com/library/36hhw2t6.aspx) classe toolog informações toohello aplicativo diagnóstico de log. Por exemplo:

    System.Diagnostics.Trace.TraceError("If you're seeing this, something bad happened");

Em tempo de execução, você pode recuperar essas toohelp de logs com a solução de problemas. Para obter mais informações, consulte [Solucionando problemas de aplicativos Web do Azure no Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md).

Aplicativos do serviço de aplicativo web também registra informações de implantação quando você publicar o aplicativo da web de conteúdo tooa. Isto acontece automaticamente e não há definições de configuração para log de implantação. Log de implantação permite toodetermine porque uma implantação falhou. Por exemplo, se você estiver usando um script de implantação personalizada, você pode usar toodetermine de registro em log de implantação por que o script hello está falhando.

## <a name="enablediag"></a>Como tooenable diagnóstico
Diagnóstico de tooenable em hello [Portal do Azure](https://portal.azure.com), vá toohello folha para seu aplicativo web e clique em **Configurações > logs de diagnóstico**.

<!-- todo:cleanup dogfood addresses in screenshot -->
![Parte de logs](./media/web-sites-enable-diagnostic-log/logspart.png)

Quando você habilita **diagnósticos de aplicativo** você também escolher Olá **nível**. Essa configuração permite que informações de saudação do toofilter capturadas muito**informativa**, **aviso** ou **erro** informações. Essa configuração muito**detalhado** registrará em log todas as informações geradas pelo aplicativo hello.

> [!NOTE]
> Ao contrário da alteração Olá Web. config arquivo, permitindo o diagnóstico do aplicativo ou alterar os níveis de log de diagnóstico não se recicla domínio de aplicativo hello que executa o aplicativo hello dentro.
>
>

Em Olá [portal clássico](https://manage.windowsazure.com) aplicativo Web **configurar** guia, você pode selecionar **armazenamento** ou **sistema de arquivos** para **servidor web registro em log**. Selecionando **armazenamento** permite que você tooselect uma conta de armazenamento e, em seguida, um contêiner de blob Olá logs serão gravados. Todos os outros logs para **diagnóstico de site** são gravados toohello sistema de arquivos somente.

Olá [portal clássico](https://manage.windowsazure.com) aplicativo Web **configurar** guia também tem configurações adicionais para o application diagnostics:

* **Sistema de arquivos** -Olá de repositórios de sistema de arquivos do aplicativo diagnóstico informações toohello web app. Esses arquivos podem ser acessados por FTP ou baixados como um arquivo Zip usando hello Azure PowerShell ou a Interface de linha de comando do Azure (CLI do Azure).
* **Armazenamento de tabela** -Olá de armazenamentos de informações de diagnóstico do aplicativo no nome especificado da tabela e a conta de armazenamento do Azure hello.
* **Armazenamento de blob** -repositórios Olá informações de diagnóstico de aplicativo no contêiner especificado de conta de armazenamento do Azure e o blob hello.
* **Período de retenção** — por padrão, os logs não são automaticamente excluídos do **armazenamento de blobs**. Selecione **definir retenção** e insira Olá número de dias tookeep logs se desejar tooautomatically excluir logs.

> [!NOTE]
> Se você [regenerar chaves de acesso da sua conta de armazenamento](../storage/common/storage-create-storage-account.md), você deverá redefinir as chaves de saudação respectivo log configuração toouse Olá atualizado. toodo isso:
>
> 1. Em Olá **configurar** guia, defina o recurso de log do respectivos Olá muito**Off**. Salve sua configuração.
> 2. Habilitar registro em log toohello blob da conta de armazenamento ou tabela novamente. Salve sua configuração.
>
>

Qualquer combinação de sistema de arquivos, armazenamento de tabelas ou armazenamento de blob pode ser habilitada em Olá ao mesmo tempo e ter configurações de nível de log individuais. Por exemplo, você poderá toolog erros e avisos tooblob armazenamento como uma solução a longo prazo do registro em log, ao habilitar o log do sistema de arquivos com um nível de detalhado.

Enquanto todos os três locais de armazenamento fornecem Olá informações básicas para eventos registrados, **armazenamento de tabela** e **armazenamento de blob** registrar informações adicionais, como a ID da instância hello, ID do thread e uma mais timestamp granular (formato de tique) de log muito**sistema de arquivos**.

> [!NOTE]
> As informações armazenadas em **armazenamento de tabelas** ou **armazenamento de blobs** podem ser acessadas apenas usando um cliente de armazenamento ou um aplicativo que possa trabalhar diretamente com esses sistemas de armazenamento. Por exemplo, o Visual Studio 2013 contém um Gerenciador de armazenamento que podem ser usados tooexplore tabela ou armazenamento de blob e HDInsight pode acessar os dados armazenados no armazenamento de blob. Você também pode escrever um aplicativo que acessa o armazenamento do Azure, usando uma saudação [SDKs do Azure](/downloads/#).
>
> [!NOTE]
> Também pode ser habilitado diagnóstico do Azure PowerShell usando Olá **AzureWebsite conjunto** cmdlet. Se você não tiver instalado o Azure PowerShell ou não o configurou toouse sua assinatura do Azure, consulte [como tooUse do Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).
>
>

## <a name="download"></a> Como baixar logs
O sistema de arquivos de aplicativo do informações de diagnóstico armazenados toohello web pode ser acessado diretamente usando o FTP. Ele também pode ser baixado como um arquivo Zip usando o PowerShell do Azure ou Olá Interface de linha de comando do Azure.

estrutura de diretórios de Olá Olá logs são armazenados em é o seguinte:

* **Logs do aplicativo** - /LogFiles/Application/. Essa pasta contém um ou mais arquivos de texto que contêm informações produzidas pelo log do aplicativo.
* **Rastreamento de Solicitação Falha** - /LogFiles/W3SVC#########/. Esta pasta contém um arquivo XSL e um ou mais arquivos XML. Certifique-se de que você baixe o arquivo XSL de saudação em Olá mesmo diretório Olá que nos arquivos XML porque o arquivo XSL de saudação fornece funcionalidade para formatar e filtragem de conteúdo de saudação do hello XML nos arquivos quando visualizada no Internet Explorer.
* **Logs de erro do aplicativo** - /LogFiles/DetailedErrors/. Esta pasta contém um ou mais arquivos .htm que fornecem informações exaustivas para quaisquer erros de HTTP.
* **Logs do Web Server** - /LogFiles/http/RawLogs. Esta pasta contém um ou mais arquivos de texto formatados usando Olá [formato de arquivo de log estendido W3C](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).
* **Logs de implantação** - /LogFiles/Git. Esta pasta contém os logs gerados por processos de implantação interna Olá usados por aplicativos web do Azure, bem como os logs para implantações do Git.

### <a name="ftp"></a>FTP
informações de diagnóstico tooaccess usando FTP, visite Olá **painel** de seu aplicativo web no hello [portal clássico](https://manage.windowsazure.com). Em Olá **visão rápida** seção, use Olá **Logs de diagnóstico de FTP** vincular os arquivos de log de saudação tooaccess usando FTP. Olá **usuário de implantação/FTP** entrada lista o nome de usuário de saudação que deve ser usado tooaccess Olá FTP.

> [!NOTE]
> Se hello **usuário de implantação/FTP** entrada não for definida, ou tiver esquecido a senha Olá para este usuário, você pode criar um novo usuário e uma senha usando Olá **Redefinir credenciais de implantação** link no hello **visão rápida** seção Olá **painel**.
>
>

### <a name="download-with-azure-powershell"></a>Baixar com o PowerShell do Azure
arquivos de log do toodownload hello, inicie uma nova instância do Azure PowerShell e use Olá comando a seguir:

    Save-AzureWebSiteLog -Name webappname

Isso salvará os logs de saudação do aplicativo web de saudação especificado pelo Olá **-nome** arquivo tooa de parâmetro nomeado **logs.zip** no diretório atual hello.

> [!NOTE]
> Se você não tiver instalado o Azure PowerShell ou não o configurou toouse sua assinatura do Azure, consulte [como tooUse do Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).
>
>

### <a name="download-with-azure-command-line-interface"></a>Baixar com a interface de linha de comando do Azure
arquivos de log de saudação toodownload usando Olá Interface de linha de comando do Azure, abra um novo prompt de comando, o PowerShell, Bash ou sessão do Terminal e insira Olá comando a seguir:

    azure site log download webappname

Isso salvará os logs de saudação do aplicativo web de saudação chamado 'webappname' tooa arquivo chamado **diagnostics.zip** no diretório atual hello.

> [!NOTE]
> Se você não tiver instalado hello Azure Interface de linha de comando (CLI do Azure) ou não o configurou toouse sua assinatura do Azure, consulte [como tooUse CLI do Azure](../cli-install-nodejs.md).
>
>

## <a name="how-to-view-logs-in-application-insights"></a>Como exibir os logs de rastreamento de Java no Application Insights
Visual Studio Application Insights fornece ferramentas para filtrar e pesquisar logs e para correlacionar os logs de saudação com solicitações e outros eventos.

1. Adicione projeto de tooyour do SDK do Application Insights Olá no Visual Studio.
   * Clique com o botão direito do mouse no projeto no Gerenciador de Soluções e selecione Adicionar Application Insights. Você será guiado pelas etapas que incluem a criação de um recurso do Application Insights. [Saiba mais](../application-insights/app-insights-asp-net.md)
2. Adicione projeto de tooyour de pacote hello ouvinte de rastreamento.
   * Clique com o botão direito do mouse em seu projeto e escolha Gerenciar Pacotes NuGet. Selecione `Microsoft.ApplicationInsights.TraceListener` [Saiba mais](../application-insights/app-insights-asp-net-trace-logs.md)
3. Carregue seu projeto e executá-lo toogenerate dados de log.
4. Em Olá [Portal do Azure](https://portal.azure.com/), procurar tooyour novo recurso do Application Insights e abra **pesquisa**. Você verá os dados de log, a solicitação, o uso e outras telemetrias. Alguns telemetria pode levar alguns tooarrive de minutos: clique em Atualizar. [Saiba mais](../application-insights/app-insights-diagnostic-search.md)

[Saiba mais sobre desempenho de rastreamento com o Application Insights](../application-insights/app-insights-azure-web-apps.md)

## <a name="streamlogs"></a> Como transmitir logs
Ao desenvolver um aplicativo, geralmente é útil toosee informações de log em tempo quase real. Isso pode ser feito pelo streaming de ambiente de desenvolvimento do registro em log informações tooyour usando o Azure PowerShell ou Olá Interface de linha de comando do Azure.

> [!NOTE]
> Alguns tipos de buffer de log gravar arquivo de log de toohello, que pode resultar em eventos fora de ordem no fluxo de saudação. Por exemplo, uma entrada de log de aplicativo que ocorre quando um usuário acessa uma página pode ser exibida no fluxo de saudação antes Olá HTTP entrada do log correspondente para a solicitação de página hello.
>
> [!NOTE]
> Fluxo de log também transmitir informações gravadas tooany arquivo de texto armazenado em Olá **unidade d:\\inicial\\LogFiles\\**  pasta.
>
>

### <a name="streaming-with-azure-powershell"></a>O streaming realizado com o PowerShell do Azure
informações de log toostream, inicie uma nova instância do Azure PowerShell e use Olá comando a seguir:

    Get-AzureWebSiteLog -Name webappname -Tail

Isso conectará toohello web aplicativo especificado por Olá **-nome** parâmetro e iniciar o streaming de janela do PowerShell toohello informações que ocorrem eventos de log no aplicativo web de saudação. Todas as informações gravadas toofiles termina em. txt,. log ou. htm que são armazenados no diretório de /LogFiles hello (início/d/logfiles) serão transmitidas console local toohello.

eventos específicos de toofilter, como erros, usam Olá **-mensagem** parâmetro. Por exemplo:

    Get-AzureWebSiteLog -Name webappname -Tail -Message Error

tipos de log específico toofilter, como HTTP, usam Olá **-caminho** parâmetro. Por exemplo:

    Get-AzureWebSiteLog -Name webappname -Tail -Path http

toosee uma lista de caminhos disponíveis, use Olá - ListPath parâmetro.

> [!NOTE]
> Se você não tiver instalado o Azure PowerShell ou não o configurou toouse sua assinatura do Azure, consulte [como tooUse do Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).
>
>

### <a name="streaming-with-azure-command-line-interface"></a>Transmitir com a Interface da linha de comando do Azure
toostream informações de log, abra um novo prompt de comando, o PowerShell, Bash ou sessão do Terminal e insira Olá comando a seguir:

    azure site log tail webappname

Isso se conectará toohello web aplicativo chamado 'webappname' e iniciar o streaming de janela toohello de informações que ocorrem eventos de log no aplicativo web de saudação. Todas as informações gravadas toofiles termina em. txt,. log ou. htm que são armazenados no diretório de /LogFiles hello (início/d/logfiles) serão transmitidas console local toohello.

eventos específicos de toofilter, como erros, usam Olá **– filtro** parâmetro. Por exemplo:

    azure site log tail webappname --filter Error

tipos de log específico toofilter, como HTTP, usam Olá **-caminho** parâmetro. Por exemplo:

    azure site log tail webappname --path http

> [!NOTE]
> Se você não tiver instalado Olá Interface de linha de comando do Azure ou não o configurou toouse sua assinatura do Azure, consulte [como tooUse Interface de linha de comando do Azure](../cli-install-nodejs.md).
>
>

## <a name="understandlogs"></a> Como compreender os logs de diagnóstico
### <a name="application-diagnostics-logs"></a>Logs de diagnóstico de aplicativo
Diagnóstico de aplicativo armazena informações em um formato específico para aplicativos .NET, dependendo se você armazena logs toohello sistema de arquivos, armazenamento de tabela, ou o armazenamento de blob. conjunto básico de saudação dos dados armazenados é Olá iguais em todos os três tipos de armazenamento - Olá data e hora Olá ocorreu Olá ID do processo que gerou o evento hello, tipo de evento hello (informações, aviso, erro) e mensagem de saudação do evento.

**Sistema de Arquivos**

Cada linha conectado toohello sistema de arquivos ou recebidas usando streaming será em Olá formato a seguir:

    {Date}  PID[{process id}] {event type/level} {message}

Por exemplo, um evento de erro apareceria a seguir toohello semelhante:

    2014-01-30T16:36:59  PID[3096] Error       Fatal error on hello page!

Log de sistema de arquivos toohello fornece informações de mais básicas de Olá dos três métodos disponíveis hello, fornecendo somente tempo de saudação, id de processo, nível de evento e mensagem.

**Armazenamento de tabelas**

Quando o log de armazenamento tootable propriedades adicionais são usada toofacilitate pesquisando Olá dados armazenados na tabela de hello, bem como informações mais granulares sobre o evento de saudação. Olá seguintes propriedades (colunas) são usadas para cada entidade (linha) armazenada na tabela de saudação.

| Nome da propriedade | Valor/formato |
| --- | --- |
| PartitionKey |Data/hora do evento Olá no formato Aaaammddhh |
| RowKey |Um valor de GUID que identifica exclusivamente esta entidade |
| Timestamp |Olá data e hora Olá evento ocorreu |
| EventTickCount |Olá data e hora Olá evento ocorreram, no formato de escala (precisão maior) |
| ApplicationName |nome do aplicativo web Olá |
| Nível |Nível de evento (por exemplo, erro, aviso ou informação) |
| EventId |ID do evento Olá deste evento<p><p>Padrões too0 se nenhum for especificado |
| InstanceId |Instância de aplicativo de web de Olá Olá mesmo ocorreu em |
| Pid |ID do Processo |
| Tid |ID de thread de saudação do thread Olá que produziu o evento de saudação |
| Mensagem |A mensagem com detalhes do evento |

**Armazenamento de Blobs**

Ao fazer logon tooblob armazenamento, os dados são armazenados no formato de valores separados por vírgulas (CSV). Armazenamento tootable semelhante, campos adicionais são registrada tooprovide informações mais detalhadas sobre o evento hello. Olá propriedades a seguir são usadas para cada linha hello CSV:

| Nome da propriedade | Valor/formato |
| --- | --- |
| Data |Olá data e hora Olá evento ocorreu |
| Nível |Nível de evento (por exemplo, erro, aviso ou informação) |
| ApplicationName |nome do aplicativo web Olá |
| InstanceId |Instância do aplicativo web Olá Olá evento ocorreu em |
| EventTickCount |Olá data e hora Olá evento ocorreram, no formato de escala (precisão maior) |
| EventId |ID do evento Olá deste evento<p><p>Padrões too0 se nenhum for especificado |
| Pid |ID do Processo |
| Tid |ID de thread de saudação do thread Olá que produziu o evento de saudação |
| Mensagem |A mensagem com detalhes do evento |

dados de saudação armazenados em um blob seria a seguir toohello semelhante:

    date,level,applicationName,instanceId,eventTickCount,eventId,pid,tid,message
    2014-01-30T16:36:52,Error,mywebapp,6ee38a,635266966128818593,0,3096,9,An error occurred

> [!NOTE]
> a primeira linha Hello do log de saudação contém cabeçalhos de coluna Olá conforme representado neste exemplo.
>
>

### <a name="failed-request-traces"></a>Rastreamento de Solicitação Falha
Os rastreamentos de solicitações com falha são armazenados em arquivos XML chamados **fr######.xml**. toomake-informações de saudação conectada de tooview mais fácil, uma folha de estilos XSL chamado **freb.xsl** é fornecido no hello mesmo diretório conforme Olá arquivos XML. Abertura de um dos arquivos XML de saudação no Internet Explorer usará tooprovide de folha de estilos XSL do hello a exibição formatada Olá informações de rastreamento. Isso será exibido a seguir toohello semelhante:

![exibido no navegador de saudação de solicitação com falha](./media/web-sites-enable-diagnostic-log/tws-failedrequestinbrowser.png)

### <a name="detailed-error-logs"></a>Logs de erro do aplicativo
Logs detalhados de erro são documentos HTML que fornecem informações mais detalhadas sobre erros HTTP que tenham ocorrido. Como são simplesmente documentos HTML, eles podem ser visualizados usando um navegador da Web.

### <a name="web-server-logs"></a>Logs do Web Server
Olá logs do servidor web são formatados usando Olá [formato de arquivo de log estendido W3C](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx). Esta informação pode ser lida usando um editor de texto ou analisada usando ferramentas como o [Analisador de Log](http://go.microsoft.com/fwlink/?LinkId=246619).

> [!NOTE]
> Olá logs produzidas por aplicativos web do Azure não oferecem suporte a saudação **s-computername**, **s-ip**, ou **cs-version** campos.
>
>

## <a name="nextsteps"></a> Próximas etapas
* [Como tooMonitor aplicativos Web](http://docs.microsoft.com/en-us/azure/app-service-web/web-sites-monitor)
* [Solucionando problemas de aplicativos Web do Azure no Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md)
* [Analisar logs de aplicativos Web no HDInsight](http://gallery.technet.microsoft.com/scriptcenter/Analyses-Windows-Azure-web-0b27d413)

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
>
>

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)
* Para um guia toohello alteração de saudação antigo portal toohello novo portal consulte: [referência para navegação Olá portal do Azure](http://go.microsoft.com/fwlink/?LinkId=529715)
