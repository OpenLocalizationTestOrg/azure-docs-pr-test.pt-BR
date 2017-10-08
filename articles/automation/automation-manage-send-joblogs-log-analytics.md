---
title: "aaaForward tooOMS de dados de trabalho de automação do Azure Log Analytics | Microsoft Docs"
description: "Este artigo demonstra como fluxos de trabalho de runbook e status do trabalho toosend gerenciamento e informações adicionais do toodeliver tooMicrosoft análise de Log do Operations Management Suite."
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: c12724c6-01a9-4b55-80ae-d8b7b99bd436
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/02/2017
ms.author: magoedte
ms.openlocfilehash: e78b6c6677d6502711ce828e2d32b7a91922ae26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="forward-job-status-and-job-streams-from-automation-toolog-analytics-oms"></a>Encaminhar o status do trabalho e fluxos de trabalho de automação tooLog Analytics (OMS)
Automação pode enviar runbook trabalho status e o trabalho fluxos tooyour análise de logs do Microsoft Operations Management Suite (OMS) espaço de trabalho.  Logs de trabalho e fluxos de trabalho são visíveis no hello portal do Azure, ou com o PowerShell, para trabalhos individuais e isso permite que você investigações de tooperform simples. Com o Log Analytics, você pode:

* Obter informações sobre os trabalhos de Automação
* Disparar um email ou um alerta com base no status do trabalho de runbook (por exemplo, com falha ou suspenso)
* Escrever consultas avançadas em seus fluxos de trabalho
* Correlacionar trabalhos em contas de Automação
* Visualizar o histórico de trabalho ao longo do tempo     

## <a name="prerequisites-and-deployment-considerations"></a>Pré-requisitos e considerações de implantação
toostart enviar sua automação logs tooLog análise, você precisa:

1. Olá novembro de 2016 ou versão posterior do [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) (v2.3.0).
2. Um espaço de trabalho do Log Analytics. Para saber mais, confira [Introdução ao Log Analytics](../log-analytics/log-analytics-get-started.md). 
3. Olá ResourceId para sua conta de automação do Azure

Olá toofind ResourceId para sua conta de automação do Azure e o espaço de trabalho de análise de Log, execute Olá PowerShell a seguir:

```powershell
# Find hello ResourceId for hello Automation Account
Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"

# Find hello ResourceId for hello Log Analytics workspace
Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
```

Se você tiver várias contas de automação, ou espaços de trabalho, na saída Olá Olá anterior comandos, localize Olá *nome* necessário tooconfigure e copie o valor Olá para *ResourceId*.

Se você precisar Olá toofind *nome* da sua conta de automação em Olá portal do Azure selecione sua conta de automação de saudação **conta de automação** folha e selecione **todas as configurações**.  De saudação **todas as configurações** folha, em **configurações de conta** selecione **propriedades**.  Em Olá **propriedades** folha, você pode observar esses valores.<br> ![Propriedades da Conta de Automação](media/automation-manage-send-joblogs-log-analytics/automation-account-properties.png).

## <a name="set-up-integration-with-log-analytics"></a>Configurar a integração com o Log Analytics
1. Em seu computador, inicie **do Windows PowerShell** de saudação **iniciar** tela.  
2. Copie e cole Olá PowerShell a seguir e Editar valor Olá Olá `$workspaceId` e `$automationAccountId`.  Para Olá `-Environment` parâmetro, os valores válidos são *AzureCloud* ou *AzureUSGovernment* dependendo do ambiente de nuvem Olá você está trabalhando.     

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check toosee which cloud environment toosign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }

# if you have one Log Analytics workspace you can use hello following command tooget hello resource id of hello workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $automationAccountId -WorkspaceId $workspaceId -Enabled $true

```

Depois de executar esse script, você verá os registros no Log Analytics em 10 minutos a seguir à gravação do novo JobLogs ou JobStreams.

logs de saudação toosee, executados Olá consulta na pesquisa de log de análise de Log a seguir:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`

### <a name="verify-configuration"></a>Verificar a configuração
tooconfirm sua conta de automação está enviando logs de espaço de trabalho de análise de Log tooyour, verifique se os diagnósticos estão definidos corretamente na conta de automação hello usando Olá PowerShell a seguir:

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check toosee which cloud environment toosign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }
# if you have one Log Analytics workspace you can use hello following command tooget hello resource id of hello workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Get-AzureRmDiagnosticSetting -ResourceId $automationAccountId
```

Na saída de hello Certifique-se de que:
+ Em *Logs*, Olá valor *habilitado* é *True*
+ Olá valor *WorkspaceId* está definida toohello ResourceId de seu espaço de trabalho de análise de Log


## <a name="log-analytics-records"></a>Registros do Log Analytics
O diagnóstico de Automação do Azure cira dois tipos de registros no Log Analytics e é marcado como **Type=AzureDiagnostics**.

### <a name="job-logs"></a>Logs de trabalho
| Propriedade | Descrição |
| --- | --- |
| TimeGenerated |Data e hora quando o trabalho de runbook Olá executado. |
| RunbookName_s |nome de saudação do runbook hello. |
| Caller_s |Quem iniciou a operação de saudação.  Os valores possíveis são um endereço de email ou o sistema para trabalhos agendados. |
| Tenant_g | GUID que identifica o locatário Olá para Olá chamador. |
| JobId_g |GUID que é hello Id do trabalho de runbook hello. |
| ResultType |status de Olá Olá do trabalho de runbook.  Os valores possíveis são:<br>- Iniciado<br>- Parado<br>- Suspenso<br>- Com falha<br>– Concluído |
| Categoria | Classificação de tipo de saudação de dados.  Para automação, o valor de saudação é JobLogs. |
| OperationName | Especifica o tipo de saudação da operação executada no Azure.  Para automação, o valor de saudação é trabalho. |
| Recurso | Nome da conta de automação de saudação |
| SourceSystem | Como a análise de Log coletados dados saudação. Sempre *Azure* para o Diagnóstico do Azure. |
| ResultDescription |Descreve o estado de resultado do trabalho de runbook hello.  Os valores possíveis são:<br>- O trabalho foi iniciado<br>- O trabalho falhou<br>- Trabalho Concluído |
| CorrelationId |GUID que é hello Id de correlação de trabalho de runbook hello. |
| ResourceId |Especifica a id de recurso de conta de automação do Azure de Olá do runbook hello. |
| SubscriptionId | Olá Id (GUID) de assinatura do Azure para Olá conta de automação. |
| ResourceGroup | Nome do grupo de recursos Olá Olá conta de automação. |
| ResourceProvider | MICROSOFT.AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |


### <a name="job-streams"></a>Transmissões de trabalho
| Propriedade | Descrição |
| --- | --- |
| TimeGenerated |Data e hora quando o trabalho de runbook Olá executado. |
| RunbookName_s |nome de saudação do runbook hello. |
| Caller_s |Quem iniciou a operação de saudação.  Os valores possíveis são um endereço de email ou o sistema para trabalhos agendados. |
| StreamType_s |tipo de saudação do fluxo de trabalho. Os valores possíveis são:<br>- Andamento<br>- Saída<br>- Aviso<br>- Erro<br>- Depurar<br>- Detalhado |
| Tenant_g | GUID que identifica o locatário Olá para Olá chamador. |
| JobId_g |GUID que é hello Id do trabalho de runbook hello. |
| ResultType |status de Olá Olá do trabalho de runbook.  Os valores possíveis são:<br>- em andamento |
| Categoria | Classificação de tipo de saudação de dados.  Para automação, o valor de saudação é JobStreams. |
| OperationName | Especifica o tipo de saudação da operação executada no Azure.  Para automação, o valor de saudação é trabalho. |
| Recurso | Nome da conta de automação de saudação |
| SourceSystem | Como a análise de Log coletados dados saudação. Sempre *Azure* para o Diagnóstico do Azure. |
| ResultDescription |Inclui Olá fluxo de saída de runbook hello. |
| CorrelationId |GUID que é hello Id de correlação de trabalho de runbook hello. |
| ResourceId |Especifica a id de recurso de conta de automação do Azure de Olá do runbook hello. |
| SubscriptionId | Olá Id (GUID) de assinatura do Azure para Olá conta de automação. |
| ResourceGroup | Nome do grupo de recursos Olá Olá conta de automação. |
| ResourceProvider | MICROSOFT.AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |

## <a name="viewing-automation-logs-in-log-analytics"></a>Exibir Logs de Automação no Log Analytics
Agora que você iniciou a enviar seu tooLog de logs de trabalho de automação Analytics, vamos ver o que você pode fazer com esses logs de análise de Log.

logs de saudação toosee, executados Olá consulta a seguir:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`

### <a name="send-an-email-when-a-runbook-job-fails-or-suspends"></a>Enviar um email quando um trabalho de runbook falhar ou for suspenso
Uma das nossas principais clientes pergunta é para Olá capacidade toosend um email ou um texto quando algo dá errado com um trabalho de runbook.   

a regra toocreate um alerta, comece criando uma pesquisa de log de runbook Olá registros de trabalho que devem chamar o alerta de saudação.  Clique em Olá **alerta** botão toocreate e configurar a regra de alerta de saudação.

1. Na página de visão geral de análise de Log de Olá, clique em **pesquisa de Log**.
2. Crie uma consulta de pesquisa de log para o alerta, digitando Olá a seguir pesquisa no campo de consulta Olá: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended)` você também pode agrupar por Olá RunbookName usando:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended) | measure Count() by RunbookName_s`   

   Se você configurar logs de mais de uma automação conta ou assinatura tooyour espaço de trabalho, você pode agrupar alertas por assinatura e conta de automação.  Nome da conta de automação pode ser derivada de campo de recurso Olá na pesquisa de saudação do JobLogs.  
3. Olá tooopen **Adicionar regra de alerta** tela, clique em **alerta** na parte superior de saudação da página de saudação. Para obter mais detalhes sobre o alerta de Olá Olá opções tooconfigure, consulte [alertas na análise de Log](../log-analytics/log-analytics-alerts.md#alert-rules).

### <a name="find-all-jobs-that-have-completed-with-errors"></a>Localizar todos os trabalhos que foram concluídos com erros
Além disso tooalerting em caso de falha, você pode encontrar quando um trabalho de runbook tem um erro não fatal. Nesses casos o PowerShell produz um fluxo de erro, mas os erros de não finalização Olá não causar toosuspend seu trabalho ou falhar.    

1. No seu espaço de trabalho do Log Analytics, clique em **Pesquisa de Logs**.
2. No campo de consulta hello, digite `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams StreamType_s=Error | measure count() by JobId_g` e, em seguida, clique em **pesquisa**.

### <a name="view-job-streams-for-a-job"></a>Exibir fluxos de trabalho para um trabalho
Quando você estiver depurando um trabalho, talvez você queira toolook em fluxos de trabalho de saudação.  Olá, consulta a seguir mostra todos os fluxos de saudação para um único trabalho com GUID 2ebd22ea-e05e-4eb9 - 9d 76-d73cbd4356e0:   

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams JobId_g="2ebd22ea-e05e-4eb9-9d76-d73cbd4356e0" | sort TimeGenerated | select ResultDescription`

### <a name="view-historical-job-status"></a>Exibir o status do histórico de trabalho
Por fim, talvez você queira toovisualize seu histórico de trabalho ao longo do tempo.  Você pode usar essa consulta toosearch para status Olá dos trabalhos ao longo do tempo.

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  
<br> ![Gráfico de status de trabalho histórico do OMS](media/automation-manage-send-joblogs-log-analytics/historical-job-status-chart.png)<br>

## <a name="summary"></a>Resumo
Enviando sua automação trabalho status e o fluxo de dados tooLog análise, você pode obter uma noção melhor sobre status de saudação de seus trabalhos de automação por:
+ Configurar alertas toonotify você quando há um problema
+ Usando modos de exibição personalizados e toovisualize de consultas de pesquisa seus resultados de runbook, o status do trabalho de runbook e outros relacionam principais indicadores ou métricas.  

Análise de log fornece maior visibilidade operacional tooyour trabalhos de automação e pode ajudar a incidentes de endereço mais rápidos.  

## <a name="next-steps"></a>Próximas etapas
* toolearn mais sobre como consultas de pesquisa diferentes tooconstruct e examine Olá automação trabalho logs de análise de Log, consulte [pesquisas de Log na análise de Log](../log-analytics/log-analytics-log-searches.md)
* toounderstand como mensagens de saída e o erro toocreate e recuperar de runbooks, consulte [mensagens e saída de Runbook](automation-runbook-output-and-messages.md)
* toolearn mais sobre a execução do runbook, como trabalhos de runbook toomonitor e outros detalhes técnicos, consulte [acompanhar um trabalho de runbook](automation-runbook-execution.md)
* toolearn mais sobre análise de logs do OMS e fontes de coleta de dados, consulte [dados de armazenamento do Azure coleta na visão geral da análise de Log](../log-analytics/log-analytics-azure-storage.md)
