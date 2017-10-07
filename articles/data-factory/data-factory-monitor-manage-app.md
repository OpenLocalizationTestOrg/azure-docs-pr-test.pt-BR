---
title: aaaMonitor e gerenciar os pipelines de dados - Azure | Microsoft Docs
description: "Saiba como toouse Olá toomonitor de aplicativo de gerenciamento e monitoramento e gerenciar canais e fábricas de dados do Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f3f07bc4-6dc3-4d4d-ac22-0be62189d578
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: 5e4ef6ec5fb8ebc9bda0be7899a39a51d58403d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-monitoring-and-management-app"></a>Monitorar e gerenciar os pipelines de fábrica de dados do Azure usando o aplicativo de monitoramento e gerenciamento de saudação
> [!div class="op_single_selector"]
> * [Usando o Portal do Azure/Azure PowerShell](data-factory-monitor-manage-pipelines.md)
> * [Usando o aplicativo de Monitoramento e Gerenciamento](data-factory-monitor-manage-app.md)
>
>

Este artigo descreve como toouse Olá toomonitor de aplicativo de gerenciamento e monitoramento, gerenciar e depurar seus pipelines de fábrica de dados. Ela também fornece informações sobre como toocreate alertas tooget notificado em caso de falha. Você pode começar a usar aplicativo hello por Olá assistindo a seguir vídeo:

> [!NOTE]
> interface do usuário Olá mostrado no hello vídeo pode não corresponder exatamente o que você vê no portal de saudação. É um pouco mais antigo, mas conceitos permanecem Olá mesmo. 

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>

## <a name="launch-hello-monitoring-and-management-app"></a>Inicie o aplicativo de monitoramento e gerenciamento de saudação
Olá toolaunch Monitor e o aplicativo de gerenciamento, clique em Olá **monitorar e gerenciar** bloco Olá **Data Factory** folha sua fábrica de dados.

![Monitoramento do lado a lado na home page do hello fábrica de dados](./media/data-factory-monitor-manage-app/MonitoringAppTile.png)

Você deve ver o aplicativo de monitoramento e gerenciamento de saudação abrir em uma janela separada.  

![Aplicativo de Monitoramento e Gerenciamento](./media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> Se você vir esse navegador da web hello está preso em "Autorizar...", desmarque Olá **bloquear cookies de terceiros e dados do site** caixa de seleção — ou manter essa opção selecionada, criar uma exceção para **login.microsoftonline.com** e, em seguida, tente tooopen Olá aplicativo novamente.


Na lista de atividade Windows hello no painel do meio hello, você vê uma janela de atividade para cada execução de uma atividade. Por exemplo, se você tiver hello atividade agendada toorun por hora por cinco horas, você vê cinco janelas de atividade associadas com fatias de cinco dados. Se você não vir o windows de atividade na lista de saudação na parte inferior do hello, Olá a seguir:
 
- Saudação de atualização **hora de início** e **hora de término** filtros em Olá toomatch superior Olá início e término do pipeline e clique em Olá **aplicar** botão.  
- lista de atividade Windows Hello não será atualizada automaticamente. Clique em Olá **atualizar** botão na barra de ferramentas de saudação em Olá **atividade Windows** lista.  

Se você não tiver um tootest de aplicativo da fábrica de dados essas etapas com, Olá tutorial: [copiar dados de armazenamento de Blob tooSQL banco de dados usando a fábrica de dados](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

## <a name="understand-hello-monitoring-and-management-app"></a>Entender o aplicativo de monitoramento e gerenciamento de saudação
Há três guias Olá esquerda: **Resource Explorer**, **modos de exibição de monitoramento**, e **alertas**. guia primeiro Hello (**Resource Explorer**) é selecionada por padrão.

### <a name="resource-explorer"></a>Gerenciador de Recursos
Consulte o seguinte hello:

* Olá Resource Explorer **exibição de árvore** no painel esquerdo da saudação.
* Olá **exibição de diagrama** na parte superior de saudação no painel do meio hello.
* Olá **atividade Windows** lista na parte inferior da saudação no painel do meio hello.
* Olá **propriedades**, **Pesquisador de objetos de janela de atividade**, e **Script** guias no painel direito da saudação.

No Gerenciador de recursos, você vê todos os recursos (pipelines, conjuntos de dados, serviços vinculados) na fábrica de dados de saudação em uma exibição de árvore. Ao selecionar um objeto no Gerenciador de Recursos, você nota o seguinte:

* Olá associados a entidade está realçada na saudação de exibição de diagrama de fábrica de dados.
* [Associados windows atividade](data-factory-scheduling-and-execution.md) são realçados na lista de atividade Windows hello na parte inferior da saudação.  
* Propriedades de saudação do objeto selecionado Olá são mostradas na janela de propriedades de saudação no painel direito da saudação.
* Olá definição JSON do objeto selecionado Olá é mostrado, se aplicável. Por exemplo: um serviço vinculado, um conjunto de dados ou um pipeline.

![Gerenciador de Recursos](./media/data-factory-monitor-manage-app/ResourceExplorer.png)

Consulte Olá [de agendamento e execução](data-factory-scheduling-and-execution.md) artigo para obter informações conceituais detalhadas sobre janelas de atividade.

### <a name="diagram-view"></a>Exibição de diagrama
saudação de exibição de diagrama de uma fábrica de dados fornece um único painel de vidro toomonitor e gerenciar uma fábrica de dados e seus ativos. Quando você seleciona uma entidade de fábrica de dados (conjunto de dados/pipeline) na saudação de exibição de diagrama:

* entidade Olá da fábrica de dados é selecionada na exibição de árvore de saudação.
* Olá associados atividade windows é realçado na lista de atividade Windows hello.
* Propriedades de saudação do objeto selecionado Olá são mostradas na janela de propriedades de saudação.

Quando o pipeline de saudação está habilitado (não em um estado de pausa), ela é mostrada com uma linha verde:

![Execução do pipeline](./media/data-factory-monitor-manage-app/PipelineRunning.png)

Você pode pausar, retomar ou encerrar um pipeline, selecionando-o no modo de exibição de diagrama hello e usando os botões de saudação na barra de comandos de saudação.

![Pausar/retomar na barra de comandos Olá](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)
 
Existem três botões de barra de comandos para o pipeline Olá Olá exibição de diagrama. Você pode usar o pipeline do hello segundo botão toopause hello. Pausando não encerrar Olá em atividades em execução no momento e permite que eles continuar toocompletion. botão terceiro Olá pausa pipeline hello e finaliza a execução de atividades existente. botão de primeira Olá retoma pipeline hello. Quando o pipeline é pausado, a cor de saudação do pipeline Olá muda. Por exemplo, um pipeline pausa aparece no Olá a imagem a seguir: 

![Pipeline em pausa](./media/data-factory-monitor-manage-app/PipelinePaused.png)

Você pode selecionar vários pipelines de dois ou mais usando a tecla Ctrl de saudação. Você pode usar botões de barra de comando toopause/retomar Olá pipelines várias por vez.

Você pode também clique um pipeline e selecione as opções toosuspend, retome ou finalize um pipeline. 

![Menu de contexto do pipeline](./media/data-factory-monitor-manage-app/right-click-menu-for-pipeline.png)

Clique em Olá **abrir pipeline** opção toosee todas as atividades de saudação no pipeline de saudação. 

![Menu do pipeline aberto](./media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

No modo de pipeline de saudação aberto, você verá todas as atividades no pipeline de saudação. Neste exemplo, há apenas uma atividade: Copiar Atividade. 

![Pipeline aberto](./media/data-factory-monitor-manage-app/OpenedPipeline.png)

toogo fazer toohello modo de exibição anterior, clique em nome de fábrica de dados Olá no menu de navegação estrutural Olá na parte superior da saudação.

No modo de pipeline hello, quando você seleciona um conjunto de dados de saída ou quando você move o mouse sobre o conjunto de dados de saída Olá, consulte janela pop-up do Windows de atividade Olá para esse conjunto de dados.

![Janela pop-up de Atividades do Windows](./media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

Você pode clicar em um toosee detalhes da janela de atividade para ele no hello **propriedades** janela no painel direito da saudação.

![Propriedades da Janela de Atividades](./media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

No painel direito da saudação, alterne toohello **Pesquisador de objetos de janela de atividade** guia toosee obter mais detalhes.

![Gerenciador de Janelas de Atividades](./media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

Consulte também **resolvido variáveis** para cada tentativa de execução de uma atividade em Olá **tentativas** seção.

![Variáveis resolvidas](./media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

Alternar toohello **Script** guia definição de script toosee Olá JSON para o objeto selecionado hello.   

![Guia Script](./media/data-factory-monitor-manage-app/ScriptTab.png)

Você pode ver janelas de atividades em três locais:

* Hello atividade Windows pop-up no hello modo de exibição de diagrama (painel central).
* Hello atividade janela Explorer no painel direito da saudação.
* lista de atividade Windows Hello no painel inferior de saudação.

No pop-up de atividade Windows hello e Gerenciador de janela de atividade, você pode rolar toohello semana anterior e Olá próxima semana usando Olá setas à esquerda e à direita.

![Setas para a direita/esquerda do Gerenciador de Janelas de Atividades](./media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

Final Olá Olá exibição de diagrama, você pode ver esses botões: ampliar, zoom, tooFit de Zoom, Zoom 100%, o layout de bloqueio. Olá **layout de bloqueio** botão impede que você mova acidentalmente tabelas e pipelines no hello exibição de diagrama. Ele está ligado por padrão. Você pode desativá-lo e mover os entidades no diagrama de saudação. Quando você pode desativá-lo, você pode usar pipelines e tabelas do hello último botão tooautomatically posição. Você também pode ampliar ou reduzir usando a roda do mouse hello.

![Comandos de zoom da Exibição de Diagrama](./media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a>Lista Janelas de Atividades
lista de atividade Windows Hello na parte inferior de saudação do painel do meio Olá exibe todas as janelas de atividade para Olá conjunto de dados que você selecionou na Olá Gerenciador de recursos ou hello exibição de diagrama. Por padrão, a lista de hello está em ordem decrescente, que significa que você verá a janela de atividade mais recente Olá na parte superior da saudação.

![Lista Janelas de Atividades](./media/data-factory-monitor-manage-app/ActivityWindowsList.png)

Esta lista não atualiza automaticamente, portanto use Olá botão Olá barra de ferramentas toomanually atualizá-lo.  

Windows de atividade podem ser em uma saudação status a seguir:

<table>
<tr>
    <th align="left">Status</th><th align="left">Substatus</th><th align="left">Descrição</th>
</tr>
<tr>
    <td rowspan="8">Aguardando</td><td>ScheduleTime</td><td>tempo de saudação não são fornecidos para hello atividade janela toorun.</td>
</tr>
<tr>
<td>DatasetDependencies</td><td>dependências de upstream Olá não estão prontas.</td>
</tr>
<tr>
<td>ComputeResources</td><td>recursos de computação de saudação não estão disponíveis.</td>
</tr>
<tr>
<td>ConcurrencyLimit</td> <td>Todas as instâncias do hello atividade estão ocupadas executando outras janelas de atividade.</td>
</tr>
<tr>
<td>ActivityResume</td><td>atividade de saudação é pausada e não é possível executar o windows de atividade Olá até que ela seja retomada.</td>
</tr>
<tr>
<td>Retry</td><td>a execução da atividade Hello está sendo repetida.</td>
</tr>
<tr>
<td>Validação</td><td>A validação ainda não foi iniciada.</td>
</tr>
<tr>
<td>ValidationRetry</td><td>A validação é toobe espera repetida.</td>
</tr>
<tr>
<tr>
<td rowspan="2">InProgress</td><td>Validando</td><td>Validação em andamento.</td>
</tr>
<td>-</td>
<td>janela de atividade Hello está sendo processada.</td>
</tr>
<tr>
<td rowspan="4">Com falha</td><td>TimedOut</td><td>a execução da atividade Olá demorou mais do que o permitido pela atividade de saudação.</td>
</tr>
<tr>
<td>Cancelado</td><td>janela de atividade Olá foi cancelada por ação do usuário.</td>
</tr>
<tr>
<td>Validação</td><td>A validação falhou.</td>
</tr>
<tr>
<td>-</td><td>janela de atividade Olá falha toobe gerado ou validado.</td>
</tr>
<td>Ready</td><td>-</td><td>janela de atividade Hello está pronta para consumo.</td>
</tr>
<tr>
<td>Ignorado</td><td>-</td><td>janela de atividade de saudação não foi processada.</td>
</tr>
<tr>
<td>Nenhum</td><td>-</td><td>Uma janela de atividade usado tooexist com um status diferente, mas foi redefinida.</td>
</tr>
</table>


Quando você clica em uma janela de atividade na lista hello, você verá detalhes sobre ele no hello **atividade Windows Explorer** ou hello **propriedades** janela saudação à direita.

![Gerenciador de Janelas de Atividades](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a>Atualizar janelas de atividades
detalhes de saudação não são atualizados automaticamente, portanto, use Olá atualização botão (Olá segundo) na lista de windows toomanually atualização hello atividade da barra de comandos de saudação.  

### <a name="properties-window"></a>Janela Propriedades
janela de propriedades de saudação estiver no painel de mais à direita de saudação do aplicativo de monitoramento e gerenciamento de saudação.

![Janela Propriedades](./media/data-factory-monitor-manage-app/PropertiesWindow.png)

Exibe as propriedades do item de saudação que você selecionou na saudação (exibição de árvore), Gerenciador de recursos de exibição de diagrama ou lista do Windows de atividade.

### <a name="activity-window-explorer"></a>Gerenciador de Janelas de Atividades
Olá **atividade janela Explorer** janela está no painel de mais à direita de saudação do aplicativo de monitoramento e gerenciamento de saudação. Exibe detalhes sobre a janela de atividade de saudação que você selecionou na janela pop-up de atividade Windows hello ou lista de atividade Windows hello.

![Gerenciador de Janelas de Atividades](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

Você pode alternar a janela de atividade tooanother clicando na exibição do calendário Olá na parte superior da saudação. Também pode usar botões de seta de seta para a esquerda/direita Olá em janelas de atividade de toosee superior de saudação do hello semana anterior ou Olá próxima semana.

Você pode usar os botões da barra de ferramentas de saudação na janela de atividade de Olá Olá inferior painel toorerun ou atualizar os detalhes de saudação no painel de saudação.

### <a name="script"></a>Script
Você pode usar o hello **Script** Olá tooview de guia definição JSON da saudação selecionado entidade da fábrica de dados (serviço vinculado, o conjunto de dados ou pipeline).

![Guia Script](./media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a>Exibições do sistema
Monitoramento e gerenciamento de aplicativo Hello contém exibições do sistema predefinidos (**windows de atividade recente**, **falha windows atividade**, **windows atividade em andamento**) que permitir janelas de atividade recente/falha/em andamento de tooview para sua fábrica de dados.

Alternar toohello **modos de exibição de monitoramento** guia esquerda Olá clicando nele.

![Guia Exibições de Monitoramento](./media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

Atualmente, há três exibições do sistema com suporte. Selecione uma opção toosee windows de atividade recente, a atividade com falha windows ou windows atividades em andamento na lista de atividade Windows hello (na parte inferior de saudação do painel do meio Olá).

Quando você seleciona Olá **windows de atividade recente** opção, você verá todas as janelas de atividade recente em ordem decrescente de saudação **hora da última tentativa**.

Você pode usar o hello **falha windows atividade** exibir janelas de atividade de todos os toosee falhado na lista de saudação. Selecione uma janela de atividade com falha nos detalhes do hello lista toosee sobre ele no hello **propriedades** janela ou hello **Pesquisador de objetos de janela de atividade**. Você também pode baixar todos os logs de uma janela de atividades com falha.

## <a name="sort-and-filter-activity-windows"></a>Classificar e filtrar janelas de atividades
Saudação de alteração **hora de início** e **hora de término** configurações no windows de atividade toofilter da barra de comandos de saudação. Depois de alterar a hora de início hello e a hora de término, clique em Olá botão Avançar toohello final tempo toorefresh hello atividade lista Windows.

![Horas de início e término](./media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> No momento, todos os tempos estão em formato UTC no aplicativo de monitoramento e gerenciamento de saudação.
>
>

Em Olá **lista atividade Windows**, clique em nome de saudação de uma coluna (por exemplo: Status).

![Menu da coluna da lista de Janelas de Atividades](./media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

Você pode fazer a seguir hello:

* Classificar em ordem crescente.
* Classificar em ordem decrescente.
* Filtrar por um ou mais valores (Pronto, Aguardando etc.).

Quando você especificar um filtro em uma coluna, você vê o botão de filtro de saudação habilitado para aquela coluna, que indica que Olá valores na coluna de saudação são filtrados.

![Filtrar uma coluna da lista de atividade Windows hello](./media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

Você pode usar Olá mesmo filtros de tooclear janela pop-up. tooclear todos os filtros para a lista de atividade Windows hello, botão Olá Limpar filtro na barra de comandos de saudação.

![Limpar todos os filtros para a lista de atividade Windows hello](./media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a>Execute ações em lote
### <a name="rerun-selected-activity-windows"></a>Executar novamente as janelas de atividades selecionadas
Selecione uma janela de atividade, clique Olá para baixo para o primeiro botão da barra de comando hello e selecione **execute** / **novamente com upstream no pipeline**. Quando você seleciona Olá **novamente com upstream no pipeline** opção, ele repete todas as janelas de atividade de upstream.
    ![Executar novamente uma janela de atividades](./media/data-factory-monitor-manage-app/ReRunSlice.png)

Você também pode selecionar várias janelas de atividade na lista de saudação e executá-los novamente no hello simultaneamente. Talvez você queira toofilter windows de atividade com base no status da saudação (por exemplo: **falha**) – e, em seguida, execute novamente Olá Falha na atividade windows depois de corrigir o problema de saudação que faz com que o hello atividade windows toofail. Consulte Olá seção para obter detalhes sobre a filtragem do windows de atividade na lista de saudação a seguir.  

### <a name="pauseresume-multiple-pipelines"></a>Pausar/retomar vários pipelines
Você pode multiselect pipelines de dois ou mais usando a tecla Ctrl de saudação. Você pode usar os botões da barra de comando hello (que serão destacados no retângulo Olá vermelho Olá a imagem a seguir) toopause/retomá-los.

![Pausar/retomar na barra de comandos Olá](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## <a name="create-alerts"></a>Criar alertas
Olá **alertas** página permite que você criar um alerta e exibir/editar/excluir os alertas existentes. Também é possível desabilitar/habilitar um alerta. toosee Olá página alertas, clique em Olá **alertas** guia.

![Guia Alertas](./media/data-factory-monitor-manage-app/AlertsTab.png)

### <a name="toocreate-an-alert"></a>toocreate um alerta
1. Clique em **adicionar alerta** tooadd um alerta. Consulte Olá **detalhes** página.

    ![Criar Alertas - página Detalhes](./media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
2. Especifique a saudação **nome** e **descrição** alerta hello e clique em **próximo**. Você deve ver Olá **filtros** página.

    ![Criar Alertas - página Filtros](./media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)
3. Selecione Olá **evento**, **status**, e **substatus** (opcional) que você deseja toocreate um serviço de fábrica de dados de alerta para e clique em **próximo**. Você deve ver Olá **destinatários** página.

    ![Criar Alertas - página Destinatários](./media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png)
4. Selecione Olá **administradores de assinatura de Email** opção e/ou insira um **email adicional do administrador**e clique em **concluir**. Você deve ver o alerta de saudação na lista de saudação.

    ![Lista Alertas](./media/data-factory-monitor-manage-app/AlertsList.png)

Na lista de alertas hello, use os botões de saudação que estão associados a saudação alerta tooedit/excluir/desabilitar/habilitar um alerta.

### <a name="eventstatussubstatus"></a>Evento/status/substatus
Olá, tabela a seguir fornece Olá lista de eventos disponíveis e status (e substatus).

| Nome do evento | Status | Substatus |
| --- | --- | --- |
| Execução de Atividade Iniciada |Iniciado |Iniciando |
| Execução de Atividade Concluída |Bem-sucedido |Bem-sucedido |
| Execução de Atividade Concluída |Com falha |Alocação de Recursos com Falha<br/><br/>Execução com falha<br/><br/>Timed Out<br/><br/>Failed Validation<br/><br/>Abandoned |
| Criação de Cluster HDI sob Demanda Iniciada |Iniciado |-|
| Cluster HDI sob Demanda Criado com Êxito |Bem-sucedido |-|
| Cluster HDI sob Demanda Excluído |Bem-sucedido |-|

### <a name="tooedit-delete-or-disable-an-alert"></a>tooedit, excluir ou desabilitar um alerta

Use Olá tooedit botões (realçado em vermelho), excluir ou desabilitar um alerta a seguir.

![Botões Alertas](./media/data-factory-monitor-manage-app/AlertButtons.png)
