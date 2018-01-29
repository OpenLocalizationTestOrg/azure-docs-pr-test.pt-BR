---
title: "Encaminhar dados do trabalho da Automação do Azure para o OMS Log Analytics | Microsoft Docs"
description: "Este artigo demonstra como enviar status de trabalho e fluxos de trabalho de runbook para Gerenciamento e Log Analytics do Microsoft Operations Management Suite para fornecer informações adicionais."
services: automation
documentationcenter: 
author: georgewallace
manager: carmonm
editor: tysonn
ms.assetid: c12724c6-01a9-4b55-80ae-d8b7b99bd436
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/31/2017
ms.author: magoedte
ms.openlocfilehash: 0319a7b9248dec9d7cdabba9c18a25463d94284b
ms.sourcegitcommit: 0e4491b7fdd9ca4408d5f2d41be42a09164db775
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="forward-job-status-and-job-streams-from-automation-to-log-analytics-oms"></a>Encaminhar status do trabalho e fluxos de trabalho de Automação para Log Analytics (OMS)
A Automação pode enviar o status do trabalho de runbook e fluxos de trabalho para seu espaço de trabalho de Log Analytics do Microsoft Operations Management Suite (OMS). Os logs e fluxos de trabalho podem ser vistos no portal do Azure ou com o PowerShell, no caso de trabalhos individuais, e isso permite a você fazer investigações simples. Com o Log Analytics, você pode:

* Obter informações sobre os Trabalhos de automação.
* Disparar um email ou um alerta com base no status de trabalho de runbook (por exemplo, com falha ou suspenso).
* Escrever consultas avançadas em seus fluxos de trabalho.
* Correlacionar trabalhos em Contas de automação.
* Visualizar o histórico de trabalhos ao longo do tempo.

## <a name="prerequisites-and-deployment-considerations"></a>Pré-requisitos e considerações de implantação
Para começar a enviar seus logs de Automação para Log Analytics, você precisará do seguinte:

* Versão de novembro 2016 ou posterior do [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) ( versão 2.3.0).
* Um espaço de trabalho do Log Analytics. Para saber mais, confira [Introdução ao Log Analytics](../log-analytics/log-analytics-get-started.md). 
* O ResourceId para sua Conta de automação do Azure.


Para encontrar o ResourceId da sua Conta de automação do Azure:

```powershell-interactive
# Find the ResourceId for the Automation Account
Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"
```

Para localizar o ResourceId do seu espaço de trabalho do Log Analytics, execute o seguinte PowerShell:

```powershell-interactive
# Find the ResourceId for the Log Analytics workspace
Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
```

Caso tenha mais de uma Conta de automação ou espaços de trabalho na saída dos comandos anteriores, localize o *Nome* que você precisa configurar e copie o valor de *ResourceId*.

Se precisar encontrar o *Nome* da sua Conta de automação, no portal do Azure, selecione sua conta de Automação na folha **Conta de automação** e selecione **Todas as configurações**. Na folha **Todas as configurações**, em **Configurações de Conta**, selecione **Propriedades**.  Na folha **Propriedades**, você pode observar esses valores.<br> ![Propriedades da Conta de Automação](media/automation-manage-send-joblogs-log-analytics/automation-account-properties.png).

## <a name="set-up-integration-with-log-analytics"></a>Configurar a integração com o Log Analytics

1. Em seu computador, inicie o **Windows PowerShell** na tela **Inicial**.
2. Execute o PowerShell a seguir e edite o valor para `[your resource id]` e `[resource id of the log analytics workspace]` com os valores da etapa anterior.

   ```powershell-interactive
   $workspaceId = "[resource id of the log analytics workspace]"
   $automationAccountId = "[resource id of your automation account]"

   Set-AzureRmDiagnosticSetting -ResourceId $automationAccountId -WorkspaceId $workspaceId -Enabled $true
   ```

Depois de executar esse script, você verá os registros no Log Analytics dentro de 10 minutos da gravação do novo JobLogs ou JobStreams.

Para ver os logs, execute a seguinte consulta na pesquisa de logs do Log Analytics: `AzureDiagnostics | where ResourceProvider == "MICROSOFT.AUTOMATION""`

### <a name="verify-configuration"></a>Verificar a configuração
Para confirmar que sua Conta de automação está enviando logs para o seu espaço de trabalho do Log Analytics, verifique se os diagnósticos estão configurados corretamente na Conta de automação usando o seguinte PowerShell:

```powershell-interactive
Get-AzureRmDiagnosticSetting -ResourceId $automationAccountId
```

Na saída, verifique se:
+ Em *Logs*, o valor de *Habilitado* é *True*.
+ O valor de *WorkspaceId* é definido como o ResourceId do seu espaço de trabalho do Log Analytics.

## <a name="log-analytics-records"></a>Registros do Log Analytics

O diagnóstico de Automação do Azure cria dois tipos de registros no Log Analytics e é marcado como **AzureDiagnostics**. As consultas a seguir usam a linguagem de consulta atualizada para o Log Analytics. Para obter informações sobre consultas comuns entre a linguagem de consulta herdada e a nova linguagem de consulta do Log Analytics do Azure, visite [Herança para novo roteiro de Linguagem de Consulta do Log Analytics do Azure](https://docs.loganalytics.io/docs/Learn/References/Legacy-to-new-to-Azure-Log-Analytics-Language)

### <a name="job-logs"></a>Logs de trabalho
| Propriedade | DESCRIÇÃO |
| --- | --- |
| TimeGenerated |Data e hora da execução do trabalho de runbook. |
| RunbookName_s |O nome do runbook. |
| Caller_s |Quem iniciou a operação. Os valores possíveis são um endereço de email ou o sistema para trabalhos agendados. |
| Tenant_g | GUID que identifica o locatário para o Chamador. |
| JobId_g |GUID que é a Id do trabalho de runbook. |
| ResultType |O status do trabalho de runbook. Os valores possíveis são:<br>- Novo<br>- Iniciado<br>- Parado<br>- Suspenso<br>- Com falha<br>– Concluído |
| Categoria | Classificação do tipo de dados. Para a Automação, o valor é JobLogs. |
| OperationName | Especifica o tipo de operação realizada no Azure. Para a Automação, o valor é Job. |
| Recurso | Nome da Conta de automação |
| SourceSystem | Como o Log Analytics coletou os dados. Sempre *Azure* para o Diagnóstico do Azure. |
| ResultDescription |Descreve o estado de resultado do trabalho de runbook. Os valores possíveis são:<br>- O trabalho foi iniciado<br>- O trabalho falhou<br>- Trabalho Concluído |
| CorrelationId |O GUID que é a Id de correlação do trabalho de runbook. |
| ResourceId |Especifica a ID de recurso da conta da Automação do Azure para o runbook. |
| SubscriptionId | O GUID (ID de assinatura do Azure) para a Conta de automação. |
| ResourceGroup | Nome do grupo de recursos para a Conta de automação. |
| ResourceProvider | MICROSOFT.AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |


### <a name="job-streams"></a>Transmissões de trabalho
| Propriedade | DESCRIÇÃO |
| --- | --- |
| TimeGenerated |Data e hora da execução do trabalho de runbook. |
| RunbookName_s |O nome do runbook. |
| Caller_s |Quem iniciou a operação. Os valores possíveis são um endereço de email ou o sistema para trabalhos agendados. |
| StreamType_s |O tipo de fluxo de trabalho. Os valores possíveis são:<br>- Andamento<br>- Saída<br>- Aviso<br>- Erro<br>- Depurar<br>- Detalhado |
| Tenant_g | GUID que identifica o locatário para o Chamador. |
| JobId_g |GUID que é a Id do trabalho de runbook. |
| ResultType |O status do trabalho de runbook. Os valores possíveis são:<br>- em andamento |
| Categoria | Classificação do tipo de dados. Para a Automação, o valor é JobStreams. |
| OperationName | Especifica o tipo de operação realizada no Azure. Para a Automação, o valor é Job. |
| Recurso | Nome da Conta de automação |
| SourceSystem | Como o Log Analytics coletou os dados. Sempre *Azure* para o Diagnóstico do Azure. |
| ResultDescription |Inclui o fluxo de saída do runbook. |
| CorrelationId |O GUID que é a Id de correlação do trabalho de runbook. |
| ResourceId |Especifica a ID de recurso da conta da Automação do Azure para o runbook. |
| SubscriptionId | O GUID (ID de assinatura do Azure) para a Conta de automação. |
| ResourceGroup | Nome do grupo de recursos para a Conta de automação. |
| ResourceProvider | MICROSOFT.AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |

## <a name="viewing-automation-logs-in-log-analytics"></a>Exibir Logs de Automação no Log Analytics
Agora que você começou a enviar seus logs de trabalho de Automação para o Log Analytics, vamos ver o que você pode fazer com esses logs no Log Analytics.

Para ver os logs, execute a seguinte consulta: `AzureDiagnostics | where ResourceProvider == "MICROSOFT.AUTOMATION"`

### <a name="send-an-email-when-a-runbook-job-fails-or-suspends"></a>Enviar um email quando um trabalho de runbook falhar ou for suspenso
Uma das principais solicitações de nossos clientes é a capacidade de enviar um email ou uma mensagem de texto quando algo dá errado em um trabalho de runbook.   

Para criar uma regra de alerta, você começa criando uma pesquisa de log para os registros de trabalhos de runbook que devem invocar o alerta. Clique no botão **Alerta** para criar e configurar a regra de alerta.

1. Na página Visão geral do Log Analytics, clique em **Pesquisa de Logs**.
2. Crie uma consulta de pesquisa de logs para o alerta digitando a seguinte pesquisa no campo de consulta: `AzureDiagnostics | where ResourceProvider == "MICROSOFT.AUTOMATION" and Category == "JobLogs" and (ResultType == "Failed" or ResultType == "Suspended")` Você também pode agrupar pelo RunbookName usando: `AzureDiagnostics | where ResourceProvider == "MICROSOFT.AUTOMATION" and Category == "JobLogs" and (ResultType == "Failed" or ResultType == "Suspended") | summarize AggregatedValue = count() by RunbookName_s`

   Se você configurou logs de mais de uma Conta de automação ou assinatura para o espaço de trabalho, também poderá agrupar os alertas por assinatura e por Conta de automação. O nome da Conta de automação pode ser encontrado no campo Recurso na pesquisa de JobLogs.
1. Para abrir a tela **Adicionar Regra de Alerta**, clique em **Alerta** na parte superior da página. Para saber mais sobre as opções de configuração de alerta, confira [Alertas no Log Analytics](../log-analytics/log-analytics-alerts.md#alert-rules).

### <a name="find-all-jobs-that-have-completed-with-errors"></a>Localizar todos os trabalhos que foram concluídos com erros
Além de alertas de falhas, você pode descobrir quando um trabalho de runbook tem um erro não fatal. Nesses casos, o PowerShell produz um fluxo de erro, mas os erros não fatais não fazem com que seu trabalho seja suspenso ou falhe.    

1. No seu espaço de trabalho do Log Analytics, clique em **Pesquisa de Logs**.
2. No campo de consulta, digite `AzureDiagnostics | where ResourceProvider == "MICROSOFT.AUTOMATION" and Category == "JobStreams" and StreamType_s == "Error" | summarize AggregatedValue = count() by JobId_g` e clique no botão **Pesquisar**.

### <a name="view-job-streams-for-a-job"></a>Exibir fluxos de trabalho para um trabalho
Ao depurar um trabalho, talvez você também queira examinar os fluxos de trabalho. A consulta abaixo mostra todos os fluxos para um único trabalho com GUID 2ebd22ea-e05e-4eb9-9d76-d73cbd4356e0:   

`AzureDiagnostics | where ResourceProvider == "MICROSOFT.AUTOMATION" and Category == "JobStreams" and JobId_g == "2ebd22ea-e05e-4eb9-9d76-d73cbd4356e0" | sort by TimeGenerated asc | project ResultDescription`

### <a name="view-historical-job-status"></a>Exibir o status do histórico de trabalho
Finalmente, talvez você queira visualizar o histórico de trabalho ao longo do tempo. Você pode usar essa consulta para pesquisar o status dos trabalhos ao longo do tempo.

`AzureDiagnostics | where ResourceProvider == "MICROSOFT.AUTOMATION" and Category == "JobLogs" and ResultType != "started" | summarize AggregatedValue = count() by ResultType, bin(TimeGenerated, 1h)`  
<br> ![Gráfico de status de trabalho histórico do OMS](media/automation-manage-send-joblogs-log-analytics/historical-job-status-chart.png)<br>

## <a name="summary"></a>Resumo
Ao enviar seus dados de fluxo e status do Trabalho de automação para Log Analytics, você poderá ter mais informações sobre o status de seus Trabalhos de automação:
+ Configurando alertas para notificá-lo quando houver um problema.
+ Usando exibições personalizadas e consultas de pesquisa para visualizar os resultados de runbook, o status do trabalho de runbook e outros principais indicadores ou métricas relacionadas.  

O Log Analytics oferece maior visibilidade operacional para os Trabalhos de automação e pode ajudar a tratar de incidentes mais rapidamente.  

## <a name="next-steps"></a>Próximas etapas
* Para saber mais sobre como construir consultas de pesquisa diferentes e examinar os logs de trabalho de Automação com o Log Analytics, confira [Efetuar pesquisas no Log Analytics](../log-analytics/log-analytics-log-searches.md).
* Para entender como criar e recuperar mensagens de erro e de saída de runbooks, confira [Saída e mensagens de Runbook](automation-runbook-output-and-messages.md).
* Para saber mais sobre a execução de runbooks, como monitorar trabalhos de runbook e outros detalhes técnicos, confira [Acompanhar um trabalho de runbook](automation-runbook-execution.md).
* Para saber mais sobre o Log Analytics do OMS e fontes de coleta de dados, confira [Coletar dados do Armazenamento do Azure na visão geral do Log Analytics](../log-analytics/log-analytics-azure-storage.md).
