---
title: aaaMonitor e gerenciar pipelines usando hello portal do Azure e do PowerShell | Microsoft Docs
description: "Saiba como toouse Olá portal do Azure e o Azure PowerShell toomonitor e gerenciar as fábricas de dados do Azure hello e pipelines que você criou."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 9b0fdc59-5bbe-44d1-9ebc-8be14d44def9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: a8d3c7943e79450895ff754f06a37fdad1cbef92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-azure-portal-and-powershell"></a>Monitorar e gerenciar os pipelines de fábrica de dados do Azure usando hello portal do Azure e do PowerShell
> [!div class="op_single_selector"]
> * [Usando o Portal do Azure/Azure PowerShell](data-factory-monitor-manage-pipelines.md)
> * [Usando o aplicativo de Monitoramento e Gerenciamento](data-factory-monitor-manage-app.md)


> [!IMPORTANT]
> aplicativo de gerenciamento e monitoramento Hello fornece um melhor suporte para monitorar e gerenciar seus pipelines de dados e os problemas de solução de problemas. Para obter detalhes sobre como usar o aplicativo hello, consulte [monitorar e gerenciar os pipelines de fábrica de dados usando o aplicativo de monitoramento e gerenciamento Olá](data-factory-monitor-manage-app.md). 


Este artigo descreve como toomonitor, gerenciar e depurar seus pipelines usando o portal do Azure e o PowerShell. Olá artigo também fornece informações sobre como toocreate alertas e obter notificado sobre falhas.

## <a name="understand-pipelines-and-activity-states"></a>Entenda os pipelines e os estados de atividade
Usando Olá portal do Azure, você pode:

* Exibir sua data factory como um diagrama.
* Exibir atividades dentro de um pipeline.
* Exibir conjuntos de dados de entrada e saída.

Esta seção também descreve como uma fatia do conjunto de dados faz a transição de um estado de tooanother.   

### <a name="navigate-tooyour-data-factory"></a>Navegue tooyour fábrica de dados
1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Clique em **fábricas de dados** no menu Olá Olá esquerda. Se você não estiver visível, clique em **mais serviços >**e, em seguida, clique em **fábricas de dados** em Olá **INTELLIGENCE + análise** categoria.

   ![Procurar tudo > Data factories](./media/data-factory-monitor-manage-pipelines/browseall-data-factories.png)
3. Em Olá **fábricas de dados** folha, a fábrica de dados Olá select que você está interessado.

    ![Selecionar o data factory](./media/data-factory-monitor-manage-pipelines/select-data-factory.png)

   Você verá a página inicial de Olá Olá fábrica de dados.

   ![Folha Data factory](./media/data-factory-monitor-manage-pipelines/data-factory-blade.png)

#### <a name="diagram-view-of-your-data-factory"></a>Modo de exibição de diagrama de uma data factory
Olá **diagrama** de uma fábrica de dados fornece um único painel de vidro toomonitor e gerencia Olá data factory e seus ativos. Olá toosee **diagrama** exibir sua fábrica de dados, clique em **diagrama** na página inicial do Olá Olá fábrica de dados.

![Exibição de diagrama](./media/data-factory-monitor-manage-pipelines/diagram-view.png)

Você pode ampliar, zoom, toofit de zoom, zoom too100%, layout de saudação do bloqueio do diagrama de saudação e posicione automaticamente pipelines e conjuntos de dados. Você também pode ver informações de linhagem de dados hello (ou seja, Mostrar itens upstream e downstream dos itens selecionados).

### <a name="activities-inside-a-pipeline"></a>Atividades dentro de um pipeline
1. Clique com botão direito pipeline hello e, em seguida, clique em **pipeline abrir** toosee todas as atividades em Olá pipeline, juntamente com conjuntos de dados de entrada e saídos para atividades de saudação. Esse recurso é útil quando seu pipeline inclui mais de uma atividade e desejar linhagem operacionais do hello toounderstand de um único pipeline.

    ![Menu do pipeline aberto](./media/data-factory-monitor-manage-pipelines/open-pipeline-menu.png)     
2. Saudação de exemplo a seguir, você verá uma atividade de cópia no pipeline de saudação com uma entrada e uma saída. 

    ![Atividades dentro de um pipeline](./media/data-factory-monitor-manage-pipelines/activities-inside-pipeline.png)
3. Você pode navegar toohello back home page da fábrica de dados Olá clicando Olá **fábrica de dados** link na navegação de trilha Olá no canto superior esquerdo de saudação.

    ![Navegue fábrica toodata back](./media/data-factory-monitor-manage-pipelines/navigate-back-to-data-factory.png)

### <a name="view-hello-state-of-each-activity-inside-a-pipeline"></a>Estado de saudação de exibição de cada atividade dentro de um pipeline
Você pode exibir o estado atual de saudação de uma atividade exibindo status de saudação de qualquer um dos conjuntos de dados de saudação que são produzidos pela atividade de saudação.

Clicando duas vezes em Olá **OutputBlobTable** em Olá **diagrama**, você pode ver todas as fatias de saudação que são produzidas pela atividade diferente executa dentro de um pipeline. Você pode ver que a atividade de cópia Olá foi executado com êxito para Olá últimas oito horas e produzido fatias Olá Olá **pronto** estado.  

![Estado do pipeline de saudação](./media/data-factory-monitor-manage-pipelines/state-of-pipeline.png)

fatias de conjunto de dados de saudação na fábrica de dados Olá podem ter um dos Olá status a seguir:

<table>
<tr>
    <th align="left">Estado</th><th align="left">Subestado</th><th align="left">Descrição</th>
</tr>
<tr>
    <td rowspan="8">Aguardando</td><td>ScheduleTime</td><td>tempo de saudação não são fornecidos para Olá fatia toorun.</td>
</tr>
<tr>
<td>DatasetDependencies</td><td>dependências de upstream Olá não estão prontas.</td>
</tr>
<tr>
<td>ComputeResources</td><td>recursos de computação de saudação não estão disponíveis.</td>
</tr>
<tr>
<td>ConcurrencyLimit</td> <td>Todas as instâncias do hello atividade estão ocupadas executando outras fatias.</td>
</tr>
<tr>
<td>ActivityResume</td><td>atividade de saudação está em pausa e fatias Olá não pode ser executado até que a atividade de saudação é retomada.</td>
</tr>
<tr>
<td>Retry</td><td>A execução da atividade está sendo repetida.</td>
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
<td>fatia Hello está sendo processada.</td>
</tr>
<tr>
<td rowspan="4">Com falha</td><td>TimedOut</td><td>a execução da atividade Olá demorou mais do que o permitido pela atividade de saudação.</td>
</tr>
<tr>
<td>Cancelado</td><td>fatia Olá foi cancelada por ação do usuário.</td>
</tr>
<tr>
<td>Validação</td><td>A validação falhou.</td>
</tr>
<tr>
<td>-</td><td>fatia Olá falha toobe gerado e/ou validado.</td>
</tr>
<td>Ready</td><td>-</td><td>fatia Hello está pronta para consumo.</td>
</tr>
<tr>
<td>Ignorado</td><td>Nenhum</td><td>fatia Olá não está sendo processada.</td>
</tr>
<tr>
<td>Nenhum</td><td>-</td><td>Uma fatia usada tooexist com um status diferente, mas foi redefinida.</td>
</tr>
</table>



Você pode exibir detalhes de saudação sobre uma fatia, clicando em uma entrada de fatia Olá **recentemente atualizado fatias** folha.

![Detalhes da fatia](./media/data-factory-monitor-manage-pipelines/slice-details.png)

Se fatia Olá tiver sido executada várias vezes, você verá várias linhas de saudação **atividade é executada** lista. Você pode exibir detalhes sobre uma atividade executar clicando em entrada hello executar Olá **atividade é executada** lista. lista de saudação mostra todos os arquivos de log hello, juntamente com uma mensagem de erro se houver um. Esse recurso é útil logs tooview e depuração sem ter que tooleave sua fábrica de dados.

![Detalhes da execução da atividade](./media/data-factory-monitor-manage-pipelines/activity-run-details.png)

Se não fatia Olá Olá **pronto** estado, você pode ver fatias de upstream Olá que não estão prontos e estão bloqueando a fatia atual Olá executadas em Olá **fatias de Upstream que não estão prontas** lista. Esse recurso é útil quando a fatia é em **esperando** estado e você desejar que toounderstand Olá dependências de upstream que Olá fatia está aguardando.

![Fatias de upstream que não estão prontas](./media/data-factory-monitor-manage-pipelines/upstream-slices-not-ready.png)

### <a name="dataset-state-diagram"></a>Diagrama de estado do conjunto de dados
Depois de implantar uma fábrica de dados e pipelines Olá têm um período de ativo válido, Olá dataset fatias de transição de um estado tooanother. Atualmente, status da fatia Olá segue Olá diagrama de estado a seguir:

![Diagrama de estado](./media/data-factory-monitor-manage-pipelines/state-diagram.png)

Olá, fluxo de transição de estado do conjunto de dados na fábrica de dados é a seguir Olá: espera -> em andamento/em execução (Validando) -> pronto/falha.

fatia Olá inicia em uma **esperando** estado, aguardando pré-condições toobe atendido antes de ele ser executado. Em seguida, inicia a execução da atividade hello e fatia Olá entra em um **em andamento** estado. a execução da atividade Olá pode ter êxito ou falhar. fatia Hello está marcada como **pronto** ou **falha**, com base no resultado de saudação da execução de saudação.

Você pode redefinir Olá fatia toogo da saudação **pronto** ou **falha** estado toohello **esperando** estado. Você também pode marcar o estado de fatia Olá muito**ignorar**, que impede que a atividade de saudação de execução e não processando fatia hello.

## <a name="pause-and-resume-pipelines"></a>Pausar e retomar pipelines
Você pode gerenciar seus pipelines usando o Azure PowerShell. Por exemplo, você pode pausar e retomar pipelines executando cmdlets do Azure PowerShell. 

> [!NOTE] 
> modo de exibição de diagrama de saudação não dá suporte a pausa e retomada de pipelines. Se você quiser toouse uma interface do usuário, use Olá monitoramento e gerenciamento de aplicativo. Para obter detalhes sobre como usar o aplicativo hello, consulte [monitorar e gerenciar os pipelines de fábrica de dados usando o aplicativo de monitoramento e gerenciamento Olá](data-factory-monitor-manage-app.md) artigo. 

Você pode pausar/suspender pipelines usando Olá **AzureRmDataFactoryPipeline Suspend** cmdlet do PowerShell. Esse cmdlet é útil quando você não deseja toorun seus pipelines até que um problema seja corrigido. 

```powershell
Suspend-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
Por exemplo:

```powershell
Suspend-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

Após Olá problema foi corrigido com pipeline hello, você pode retomar pipeline Olá suspenso executando Olá comando PowerShell a seguir:

```powershell
Resume-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
Por exemplo:

```powershell
Resume-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

## <a name="debug-pipelines"></a>Depurar pipelines
A fábrica de dados do Azure fornece recursos avançados para você toodebug e solucionar problemas de pipelines usando hello portal do Azure e o Azure PowerShell.

> [! Observe} é muito mais fácil tootroubleshot erros usando Olá monitoramento e gerenciamento de aplicativo. Para obter detalhes sobre como usar o aplicativo hello, consulte [monitorar e gerenciar os pipelines de fábrica de dados usando o aplicativo de monitoramento e gerenciamento Olá](data-factory-monitor-manage-app.md) artigo. 

### <a name="find-errors-in-a-pipeline"></a>Localizar erros em um pipeline
Se a execução da atividade Olá falhar em um pipeline, Olá conjunto de dados que é produzido pelo pipeline de saudação está em um estado de erro devido a falha de saudação. Você pode depurar e solucionar problemas de erros na fábrica de dados do Azure usando Olá métodos a seguir.

#### <a name="use-hello-azure-portal-toodebug-an-error"></a>Use Olá toodebug portal do Azure um erro
1. Em Olá **tabela** folha, clique Olá problema fatia que tenha Olá **Status** definido muito**falha**.

   ![Folha de tabela com fatia com problema](./media/data-factory-monitor-manage-pipelines/table-blade-with-error.png)
2. Em Olá **fatia de dados** folha, clique em que a falha de execução da atividade hello.

   ![Fatia de dados com erro](./media/data-factory-monitor-manage-pipelines/dataslice-with-error.png)
3. Em Olá **detalhes da execução de atividade** folha, você pode baixar arquivos de saudação que estão associados com o processamento do HDInsight hello. Clique em **baixar** Status/stderr toodownload Olá erro arquivo de log que contém detalhes sobre o erro de saudação.

   ![Folha de detalhes da execução da atividade com erro](./media/data-factory-monitor-manage-pipelines/activity-run-details-with-error.png)     

#### <a name="use-powershell-toodebug-an-error"></a>Use o PowerShell toodebug um erro
1. Inicie o **PowerShell**.
2. Executar Olá **AzureRmDataFactorySlice Get** comando fatias de saudação toosee e seus status. Você deve ver uma fatia com o status de saudação do **falha**.        

    ```powershell   
    Get-AzureRmDataFactorySlice [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime] <DateTime> [[-EndDateTime] <DateTime> ] [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```   
   Por exemplo:

    ```powershell   
    Get-AzureRmDataFactorySlice -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime 2014-05-04 20:00:00
    ```

   Substitua **StartDateTime** pela hora de início do pipeline. 
3. Agora, execute Olá **AzureRmDataFactoryRun Get** cmdlet tooget detalhes sobre a atividade de saudação executar fatia hello.

    ```powershell   
    Get-AzureRmDataFactoryRun [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime]
    <DateTime> [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```

    Por exemplo:

    ```powershell   
    Get-AzureRmDataFactoryRun -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime "5/5/2014 12:00:00 AM"
    ```

    valor de saudação do StartDateTime é hora de início de saudação de fatia de erro/problema Olá que você anotou na etapa anterior hello. Olá data e hora deve ser colocada entre aspas duplas.
4. Você deve ver a saída com detalhes sobre o erro Olá a seguir toohello semelhante:

    ```   
    Id                      : 841b77c9-d56c-48d1-99a3-8c16c3e77d39
    ResourceGroupName       : ADF
    DataFactoryName         : LogProcessingFactory3
    DatasetName               : EnrichedGameEventsTable
    ProcessingStartTime     : 10/10/2014 3:04:52 AM
    ProcessingEndTime       : 10/10/2014 3:06:49 AM
    PercentComplete         : 0
    DataSliceStart          : 5/5/2014 12:00:00 AM
    DataSliceEnd            : 5/6/2014 12:00:00 AM
    Status                  : FailedExecution
    Timestamp               : 10/10/2014 3:04:52 AM
    RetryAttempt            : 0
    Properties              : {}
    ErrorMessage            : Pig script failed with exit code '5'. See wasb://        adfjobs@spestore.blob.core.windows.net/PigQuery
                                    Jobs/841b77c9-d56c-48d1-99a3-
                8c16c3e77d39/10_10_2014_03_04_53_277/Status/stderr' for
                more details.
    ActivityName            : PigEnrichLogs
    PipelineName            : EnrichGameLogsPipeline
    Type                    :
    ```
5. Você pode executar Olá **salvar AzureRmDataFactoryLog** cmdlet com hello valor da Id que você consulte da saída de hello e baixar arquivos de log hello usando Olá **- DownloadLogsoption** Olá cmdlet.

    ```powershell
    Save-AzureRmDataFactoryLog -ResourceGroupName "ADF" -DataFactoryName "LogProcessingFactory" -Id "841b77c9-d56c-48d1-99a3-8c16c3e77d39" -DownloadLogs -Output "C:\Test"
    ```

## <a name="rerun-failures-in-a-pipeline"></a>Executar novamente as falhas em um pipeline

> [!IMPORTANT]
> É mais fácil erros de tootroubleshoot e execute fatias com falha usando Olá monitoramento e gerenciamento de aplicativo. Para obter detalhes sobre como usar o aplicativo hello, consulte [monitorar e gerenciar os pipelines de fábrica de dados usando o aplicativo de monitoramento e gerenciamento Olá](data-factory-monitor-manage-app.md). 

### <a name="use-hello-azure-portal"></a>Use Olá portal do Azure
Depois de solucionar problemas e falhas em um pipeline de depuração, você pode executar novamente falhas navegando toohello fatia de erro e clicando em Olá **executar** botão na barra de comandos de saudação.

![Executar novamente uma fatia com falha](./media/data-factory-monitor-manage-pipelines/rerun-slice.png)

Caso fatia Olá Falha na validação devido a uma falha de política (por exemplo, se dados não estiver disponíveis), você pode corrigir falha hello e valide novamente clicando em Olá **validar** botão na barra de comandos de saudação.

![Corrigir os erros e validar](./media/data-factory-monitor-manage-pipelines/fix-error-and-validate.png)

### <a name="use-azure-powershell"></a>Usar PowerShell do Azure
Você pode executar novamente a falhas usando Olá **AzureRmDataFactorySliceStatus conjunto** cmdlet. Consulte Olá [AzureRmDataFactorySliceStatus conjunto](https://msdn.microsoft.com/library/mt603522.aspx) tópico para sintaxe e outros detalhes sobre o cmdlet hello.

**Exemplo:**

Olá, exemplo a seguir define Olá status de todas as fatias de saudação tabela 'DAWikiAggregatedData' too'Waiting' hello Azure data Factory 'WikiADF'.

Olá 'Tipo de atualização' é definido too'UpstreamInPipeline ', que significa que o status de cada fatia para tabela hello e todas as tabelas (upstream) de dependente de saudação são definidas too'Waiting'. Olá, outro valor possível para esse parâmetro é "Individual".

```powershell
Set-AzureRmDataFactorySliceStatus -ResourceGroupName ADF -DataFactoryName WikiADF -DatasetName DAWikiAggregatedData -Status Waiting -UpdateType UpstreamInPipeline -StartDateTime 2014-05-21T16:00:00 -EndDateTime 2014-05-21T20:00:00
```

## <a name="create-alerts"></a>Criar alertas
O Azure registra eventos do usuário quando um recurso do Azure (por exemplo, Data Factory) é criado, atualizado ou excluído. Você pode criar alertas para esses eventos. Você pode usar várias métricas de toocapture da fábrica de dados e criar alertas em métricas. Recomendamos que você use os eventos para monitoramento em tempo real e métricas para fins de histórico.

### <a name="alerts-on-events"></a>Alertas de eventos
Eventos do Azure fornecem percepções úteis sobre o que está acontecendo em seus recursos do Azure. Ao usar o Azure Data Factory, os eventos são gerados quando:

* Um data factory é criado, atualizado ou excluído.
* O processamento de dados (como "execuções") foi iniciado ou concluído.
* Um cluster de HDInsight sob demanda é criado ou removido.

Você pode criar alertas nesses eventos de usuário e configurá-los toosend administrador de toohello de notificações de email e coadministrators de assinatura de saudação. Além disso, você pode especificar endereços de email adicionais de usuários que precisam de notificações de email tooreceive quando Olá condições forem atendidas. Esse recurso é útil quando você deseja tooget notificado sobre as falhas e não quiser que o monitor de toocontinuously sua fábrica de dados.

> [!NOTE]
> Atualmente, portal de saudação não mostra alertas em eventos. Saudação de uso [monitoramento e gerenciamento de aplicativo](data-factory-monitor-manage-app.md) toosee todos os alertas.


#### <a name="specify-an-alert-definition"></a>Especificar uma definição de alerta
toospecify uma definição de alerta, você criar um arquivo JSON que descreve as operações de saudação que você deseja toobe alertado no. Saudação de exemplo a seguir, alerta Olá envia uma notificação por email para Olá RunFinished operação. toobe específico, uma notificação por email é enviada quando uma execução de fábrica de dados Olá foi concluída e Olá executar falhou (Status = FailedExecution).

```JSON
{
    "contentVersion": "1.0.0.0",
     "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters": {},
    "resources":
    [
        {
            "name": "ADFAlertsSlice",
            "type": "microsoft.insights/alertrules",
            "apiVersion": "2014-04-01",
            "location": "East US",
            "properties":
            {
                "name": "ADFAlertsSlice",
                "description": "One or more of hello data slices for hello Azure Data Factory has failed processing.",
                "isEnabled": true,
                "condition":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.ManagementEventRuleCondition",
                    "dataSource":
                    {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleManagementEventDataSource",
                        "operationName": "RunFinished",
                        "status": "Failed",
                        "subStatus": "FailedExecution"   
                    }
                },
                "action":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails": [ "<your alias>@contoso.com" ]
                }
            }
        }
    ]
}
```

Você pode remover **subStatus** de saudação definição JSON se você não quiser toobe alertado sobre uma falha específica.

Este exemplo define o alerta de saudação para todas as fábricas de dados em sua assinatura. Se você quiser Olá toobe alerta configurado para uma fábrica de dados específico, você pode especificar a fábrica de dados **resourceUri** em Olá **dataSource**:

```JSON
"resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>"
```

Olá, tabela a seguir fornece Olá lista de operações disponíveis e status (e substatus).

| Nome da operação | Status | Substatus |
| --- | --- | --- |
| RunStarted |Iniciado |Iniciando |
| RunFinished |Falhou / Bem-sucedido |FailedResourceAllocation<br/><br/>Bem-sucedido<br/><br/>FailedExecution<br/><br/>TimedOut<br/><br/><Cancelado<br/><br/>FailedValidation<br/><br/>Abandoned |
| OnDemandClusterCreateStarted |Iniciado | |
| OnDemandClusterCreateSuccessful |Bem-sucedido | |
| OnDemandClusterDeleted |Bem-sucedido | |

Consulte [criar regra de alerta](https://msdn.microsoft.com/library/azure/dn510366.aspx) para obter detalhes sobre os elementos JSON Olá que são usados no exemplo hello.

#### <a name="deploy-hello-alert"></a>Implantar o alerta Olá
alerta de Olá toodeploy, use o cmdlet do hello Azure PowerShell **AzureRmResourceGroupDeployment novo**, conforme mostrado no exemplo a seguir de saudação:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\ADFAlertFailedSlice.json  
```

Após a implantação do grupo de recursos de saudação foi concluído com êxito, você verá Olá mensagens a seguir:

```
VERBOSE: 7:00:48 PM - Template is valid.
WARNING: 7:00:48 PM - hello StorageAccountName parameter is no longer used and will be removed in a future release.
Please update scripts tooremove this parameter.
VERBOSE: 7:00:49 PM - Create template deployment 'ADFAlertFailedSlice'.
VERBOSE: 7:00:57 PM - Resource microsoft.insights/alertrules 'ADFAlertsSlice' provisioning status is succeeded

DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

> [!NOTE]
> Você pode usar o hello [criar regra de alerta](https://msdn.microsoft.com/library/azure/dn510366.aspx) API REST toocreate uma regra de alerta. carga JSON Olá é exemplo JSON toohello semelhante.  


#### <a name="retrieve-hello-list-of-azure-resource-group-deployments"></a>Recuperar a lista de saudação de implantações de grupos de recursos do Azure
lista de saudação tooretrieve de implantado implantações de grupos de recursos do Azure, use o cmdlet Olá **Get-AzureRmResourceGroupDeployment**, conforme mostrado no exemplo a seguir de saudação:

```powershell
Get-AzureRmResourceGroupDeployment -ResourceGroupName adf
```

```
DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

#### <a name="troubleshoot-user-events"></a>Solucionar problemas de eventos de usuário
1. Você pode ver todos os eventos de saudação que são gerados depois de clicar em Olá **métricas e operações** lado a lado.

    ![Bloco Métricas e operações](./media/data-factory-monitor-manage-pipelines/metrics-and-operations-tile.png)
2. Clique em Olá **eventos** eventos de saudação toosee lado a lado.

    ![Bloco de eventos](./media/data-factory-monitor-manage-pipelines/events-tile.png)
3. Em Olá **eventos** folha, você pode ver detalhes sobre eventos, eventos filtrados e assim por diante.

    ![Folha Eventos](./media/data-factory-monitor-manage-pipelines/events-blade.png)
4. Clique em uma **operação** na lista de operações de saudação que causa um erro.

    ![Selecionar uma operação](./media/data-factory-monitor-manage-pipelines/select-operation.png)
5. Clique em uma **erro** detalhes do evento toosee sobre o erro de saudação.

    ![Erro de evento](./media/data-factory-monitor-manage-pipelines/operation-error-event.png)

Consulte [cmdlets do Azure Insight](https://msdn.microsoft.com/library/mt282452.aspx) cmdlets do PowerShell que você pode usar tooadd, obter ou remover alertas. Aqui estão alguns exemplos de como usar o hello **AlertRule Get** cmdlet:

```powershell
get-alertrule -res $resourceGroup -n ADFAlertsSlice -det
```

```
Properties :
Action      : Microsoft.Azure.Management.Insights.Models.RuleEmailAction
Condition   :
DataSource :
EventName             :
Category              :
Level                 :
OperationName         : RunFinished
ResourceGroupName     :
ResourceProviderName  :
ResourceId            :
Status                : Failed
SubStatus             : FailedExecution
Claims                : Microsoft.Azure.Management.Insights.Models.RuleManagementEventClaimsDataSource
Condition      :
Description : One or more of hello data slices for hello Azure Data Factory has failed processing.
Status      : Enabled
Name:       : ADFAlertsSlice
Tags       :
$type          : Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage
Id: /subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/ADFAlertsSlice
Location   : West US
Name       : ADFAlertsSlice
```

```powershell
Get-AlertRule -res $resourceGroup
```
```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0

Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest3
Location   : West US
Name       : FailedExecutionRunsWest3
```

```powershell
Get-AlertRule -res $resourceGroup -Name FailedExecutionRunsWest0
```

```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0
```

Execute Olá detalhes de toosee comandos get-help e exemplos para Olá Get-AlertRule cmdlet a seguir.

```powershell
get-help Get-AlertRule -detailed
```

```powershell
get-help Get-AlertRule -examples
```


Se ocorrerem eventos de geração de alerta Olá Olá portal folha, mas você não recebe notificações por email, verifique se o endereço de email de saudação especificado está definido tooreceive emails de remetentes externos. emails de alerta Olá podem ter bloqueados por suas configurações de email.

### <a name="alerts-on-metrics"></a>Alertas sobre métricas
No Data Factory, você pode capturar várias métricas e criar alertas sobre as métricas. Você pode monitorar e criar alertas em Olá métricas para fatias Olá sua fábrica de dados a seguir:

* **Execuções com falha**
* **Execuções com êxito**

Essas métricas são úteis e ajudarão-lo a tooget que uma visão geral de geral com falha e bem-sucedida é executado na fábrica de dados hello. Métricas são emitidas sempre que há uma fatia de execução. No início de saudação de hora hello, essas métricas são agregadas e enviados por push tooyour conta de armazenamento. métricas de tooenable, configure uma conta de armazenamento.

#### <a name="enable-metrics"></a>Habilitar a métrica
tooenable métricas, clique em seguinte de saudação do hello **Data Factory** folha:

**Monitoramento** > **Métrica** > **Configurações de diagnóstico** > **Diagnóstico**

![Link de diagnóstico](./media/data-factory-monitor-manage-pipelines/diagnostics-link.png)

Em Olá **diagnóstico** folha, clique em **na**, selecione a conta de armazenamento hello e clique em **salvar**.

![Folha de diagnósticos](./media/data-factory-monitor-manage-pipelines/diagnostics-blade.png)

Pode levar até tooone horas para Olá métricas toobe visível em hello **monitoramento** folha porque a agregação de métricas acontece por hora.

### <a name="set-up-an-alert-on-metrics"></a>Configurar alertas sobre métricas
Clique em Olá **métricas de fábrica de dados** lado a lado:

![Bloco Métricas de data factory](./media/data-factory-monitor-manage-pipelines/data-factory-metrics-tile.png)

Em Olá **métrica** folha, clique em **+ adicionar alerta** na barra de ferramentas de saudação.
![Folha Métricas do data factory > Adicionar alerta](./media/data-factory-monitor-manage-pipelines/add-alert.png)

Em Olá **adicionar uma regra de alerta** página Olá etapas a seguir e clique em **Okey**.

* Insira um nome para o alerta de saudação (exemplo: "Falha no alerta").
* Insira uma descrição do alerta de saudação (exemplo: "enviar um email quando ocorre uma falha").
* Selecione uma métrica ("Execuções com falha" versus "Execuções com êxito").
* Especifique uma condição e um valor de limite.   
* Especifica Olá período de tempo.
* Especifique se deve ser enviado um email tooowners, colaboradores e leitores.

![Folha Métricas de data factory > Adicionar regra de alerta](./media/data-factory-monitor-manage-pipelines/add-an-alert-rule.png)

Depois de regra de alerta de saudação é adicionada com êxito, folha Olá fecha e ver o novo alerta de saudação em Olá **métrica** folha.

![Folha Métrica do data factory > Novo alerta adicionado](./media/data-factory-monitor-manage-pipelines/failed-alert-in-metric-blade.png)

Você também deve ver o número de saudação de alertas no hello **regras de alerta** lado a lado. Clique em Olá **regras de alerta** lado a lado.

![Folha Métrica de data factory - Regras de alerta](./media/data-factory-monitor-manage-pipelines/alert-rules-tile-rules.png)

Em Olá **alertas regras** folha, consulte todos os alertas existentes. tooadd um alerta, clique em **adicionar alerta** na barra de ferramentas de saudação.

![Folha Regras de alerta](./media/data-factory-monitor-manage-pipelines/alert-rules-blade.png)

### <a name="alert-notifications"></a>Notificações de alerta
Depois de regra de alerta Olá corresponde a condição de saudação, você deve obter um email informando Olá alerta for ativado. Depois de Olá resolvido e a condição de alerta de saudação não corresponde mais, você obterá um email informando Olá alerta é resolvido.

Esse comportamento é diferente dos eventos, para os quais uma notificação é enviada em cada falha para a qual a regra de alerta se qualifica.

### <a name="deploy-alerts-by-using-powershell"></a>Implantar alertas usando o PowerShell
Você pode implantar os alertas para métricas Olá mesma maneira que faria para eventos.

**Definição do alerta**

```JSON
{
    "contentVersion" : "1.0.0.0",
    "$schema" : "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters" : {},
    "resources" : [
    {
            "name" : "FailedRunsGreaterThan5",
            "type" : "microsoft.insights/alertrules",
            "apiVersion" : "2014-04-01",
            "location" : "East US",
            "properties" : {
                "name" : "FailedRunsGreaterThan5",
                "description" : "Failed Runs greater than 5",
                "isEnabled" : true,
                "condition" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
                    "dataSource" : {
                        "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
                        "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
                        "resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName
>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>",
                        "metricName" : "FailedRuns"
                    },
                    "threshold" : 5.0,
                    "windowSize" : "PT3H",
                    "timeAggregation" : "Total"
                },
                "action" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails" : ["abhinav.gpt@live.com"]
                }
            }
        }
    ]
}
```

Substituir *subscriptionId*, *resourceGroupName*, e *dataFactoryName* no exemplo hello com valores apropriados.

No momento, *metricName* dá suporte a dois valores:

* FailedRuns
* SuccessfulRuns

**Implantar o alerta Olá**

alerta de Olá toodeploy, use o cmdlet do hello Azure PowerShell **AzureRmResourceGroupDeployment novo**, conforme mostrado no exemplo a seguir de saudação:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\FailedRunsGreaterThan5.json
```

Você verá a seguinte mensagem após uma implantação bem-sucedida:

```
VERBOSE: 12:52:47 PM - Template is valid.
VERBOSE: 12:52:48 PM - Create template deployment 'FailedRunsGreaterThan5'.
VERBOSE: 12:52:55 PM - Resource microsoft.insights/alertrules 'FailedRunsGreaterThan5' provisioning status is succeeded


DeploymentName    : FailedRunsGreaterThan5
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 7/27/2015 7:52:56 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           
```

Você também pode usar o hello **AlertRule adicionar** cmdlet toodeploy uma regra de alerta. Consulte Olá [AlertRule adicionar](https://msdn.microsoft.com/library/mt282468.aspx) tópico para obter detalhes e exemplos.  

## <a name="move-a-data-factory-tooa-different-resource-group-or-subscription"></a>Mover um grupo de recursos diferente de tooa de fábrica de dados ou a assinatura
Você pode mover um grupo de recursos diferentes de tooa de fábrica de dados ou uma assinatura diferente usando Olá **mover** botão Olá home page de sua fábrica de dados de barra de comandos.

![Mover o Data Factory](./media/data-factory-monitor-manage-pipelines/MoveDataFactory.png)

Você também pode mover os recursos relacionados (como alertas que estão associados a fábrica de dados Olá), juntamente com a fábrica de dados hello.

![Caixa de diálogo Mover recursos](./media/data-factory-monitor-manage-pipelines/MoveResources.png)
