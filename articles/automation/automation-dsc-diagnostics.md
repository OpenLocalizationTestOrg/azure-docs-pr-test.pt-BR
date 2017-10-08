---
title: "aaaForward tooOMS de dados relatório DSC de automação do Azure Log Analytics | Microsoft Docs"
description: "Este artigo demonstra como toosend desejado DSC (configuração) relatar dados tooMicrosoft análise de Log do Operations Management Suite toodeliver obter mais informações e gerenciamento de estado."
services: automation
documentationcenter: 
author: eslesar
manager: carmonm
editor: tysonn
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: eslesar
ms.openlocfilehash: 21f78d5549d53ba3d7e237f55d9086f380cf3351
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="forward-azure-automation-dsc-reporting-data-toooms-log-analytics"></a>Encaminhar relatórios dados tooOMS análise de Log de DSC de automação do Azure

Automação pode enviar o espaço de análise de logs do Microsoft Operations Management Suite (OMS) tooyour do dados de status de nó DSC.  
Status de conformidade é visível no portal do Azure de saudação ou com o PowerShell, para nós e recursos DSC individuais nos configurações do nó. Com o Log Analytics, você pode:

* Obter informações de conformidade para nós gerenciados e recursos individuais
* Disparar um email ou alerta com base no status de conformidade
* Escrever consultas avançadas em seus nós gerenciados
* Correlacionar o status de conformidade em contas de Automação
* Visualizar o histórico de conformidade do nó ao longo do tempo

## <a name="prerequisites"></a>Pré-requisitos

toostart enviando o DSC de automação relatórios tooLog análise, você precisa:

* Olá novembro de 2016 ou versão posterior do [Azure PowerShell](/powershell/azure/overview) (v2.3.0).
* Uma conta de Automação do Azure. Para saber mais, veja [Introdução à Automação do Azure](automation-offering-get-started.md)
* Um espaço de trabalho de Log Analytics com uma oferta de serviço **Automação e Controle**. Para saber mais, confira [Introdução ao Log Analytics](../log-analytics/log-analytics-get-started.md).
* Pelo menos um nó DSC de Automação do Azure. Para saber mais, veja [Máquinas de integração para o gerenciamento pelo DSC de Automação do Azure](automation-dsc-onboarding.md) 

## <a name="set-up-integration-with-log-analytics"></a>Configurar a integração com o Log Analytics

toobegin importar dados do DSC de automação do Azure para análise de logs, Olá concluir as etapas a seguir:

1. Faça logon no tooyour conta do Azure no PowerShell. Veja [Fazer logon com o Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/authenticate-azureps?view=azurermps-4.0.0)
1. Obter Olá _ResourceId_ de sua conta de automação executando Olá comando PowerShell a seguir: (se você tiver mais de uma conta de automação, escolha Olá _ResourceID_ conta Olá desejado tooconfigure).

  ```powershell
  # Find hello ResourceId for hello Automation Account
  Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"
  ```
1. Obter Olá _ResourceId_ de seu espaço de trabalho de análise de Log executando Olá comando PowerShell a seguir: (se você tiver mais de um espaço de trabalho, escolha Olá _ResourceID_ de espaço de trabalho de saudação desejado tooconfigure).

  ```powershell
  # Find hello ResourceId for hello Log Analytics workspace
  Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
  ```
1. Olá executar comandos do PowerShell a seguir, substituindo `<AutomationResourceId>` e `<WorkspaceResourceId>` com hello _ResourceId_ valores de cada uma das etapas anteriores hello:

  ```powershell
  Set-AzureRmDiagnosticSetting -ResourceId <AutomationResourceId> -WorkspaceId <WorkspaceResourceId> -Enabled $true -Categories "DscNodeStatus"
  ```

Se você quiser toostop importar dados do DSC de automação do Azure para análise de logs, execute Olá comando PowerShell a seguir.

```powershell
Set-AzureRmDiagnosticSetting -ResourceId <AutomationResourceId> -WorkspaceId <WorkspaceResourceId> -Enabled $false -Categories "DscNodeStatus"
```

## <a name="view-hello-dsc-logs"></a>Exibir logs de saudação DSC

Depois de configurar a integração com a análise de Log para os seus dados de DSC de automação, um **pesquisa de Log** botão aparecerá em Olá **nós DSC** folha da sua conta de automação. Clique em Olá **pesquisa de Log** botão logs de saudação tooview para dados do nó DSC.

![Botão Pesquisar Log](media/automation-dsc-diagnostics/log-search-button.png)

Olá **pesquisa de Log** folha é aberto e você verá um **DscNodeStatusData** operação para cada nó do DSC e um **DscResourceStatusData** operação para cada [DSC recurso](https://msdn.microsoft.com/powershell/dsc/resources) chamada em Olá configuração aplicada toothat nós.

Olá **DscResourceStatusData** operação contém informações de erro para qualquer recurso de DSC que falhou.

Clique em cada operação em dados de saudação do hello lista toosee para essa operação.

Você também pode exibir os logs de saudação [pesquisa na análise de Log. Veja [Localizar dados usando pesquisas de logs](../log-analytics/log-analytics-log-searches.md).
Digite o seguinte Olá consulta toofind seu DSC logs:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category = "DscNodeStatus"`

Você também pode limitar a consulta Olá pelo nome da operação hello. Por exemplo: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category = "DscNodeStatus" OperationName = "DscNodeStatusData"

### <a name="send-an-email-when-a-dsc-compliance-check-fails"></a>Enviar um email quando uma verificação de conformidade do DSC falhar

Uma de nossas principais solicitações dos clientes é Olá capacidade toosend um email ou um texto quando algo dá errado com uma configuração DSC.   

a regra toocreate um alerta, comece criando uma pesquisa de log para registros de relatório de DSC Olá que deve chamar o alerta de saudação.  Clique em Olá **alerta** botão toocreate e configurar a regra de alerta de saudação.

1. Na página de visão geral de análise de Log de Olá, clique em **pesquisa de Log**.
1. Crie uma consulta de pesquisa de log para o alerta, digitando Olá a seguir pesquisa no campo de consulta hello:`Type=AzureDiagnostics Category=DscNodeStatus NodeName_s=DSCTEST1 OperationName=DscNodeStatusData ResultType=Failed`

  Se você configurar logs de mais de uma automação conta ou assinatura tooyour espaço de trabalho, você pode agrupar alertas por assinatura e conta de automação.  
  Nome da conta de automação pode ser derivada de campo de recurso Olá na pesquisa de saudação do DscNodeStatusData.  
1. Olá tooopen **Adicionar regra de alerta** tela, clique em **alerta** na parte superior de saudação da página de saudação. Para obter mais informações sobre o alerta de Olá Olá opções tooconfigure, consulte [alertas na análise de Log](../log-analytics/log-analytics-alerts.md#alert-rules).

### <a name="find-failed-dsc-resources-across-all-nodes"></a>Encontrar recursos DSC com falha em todos os nós

Uma vantagem de usar o Log Analytics é que você pode pesquisar falhas de verificações em nós.
toofind todas as instâncias dos recursos de DSC que falhou.

1. Na página de visão geral de análise de Log de Olá, clique em **pesquisa de Log**.
1. Crie uma consulta de pesquisa de log para o alerta, digitando Olá a seguir pesquisa no campo de consulta hello:`Type=AzureDiagnostics Category=DscNodeStatus OperationName=DscResourceStatusData ResultType=Failed`

### <a name="view-historical-dsc-node-status"></a>Exibir status do nó DSC histórico

Por fim, talvez você queira toovisualize seu histórico de status do nó DSC ao longo do tempo.  
Você pode usar essa consulta toosearch para status de saudação do status do nó DSC ao longo do tempo.

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=DscNodeStatus NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  

Isso exibirá um gráfico de status do nó Olá ao longo do tempo.

## <a name="log-analytics-records"></a>Registros do Log Analytics

O diagnóstico da Automação do Azure cria duas categorias de registros no Log Analytics.

### <a name="dscnodestatusdata"></a>DscNodeStatusData

| Propriedade | Descrição |
| --- | --- |
| TimeGenerated |Data e hora quando a verificação de conformidade de saudação foi executada. |
| OperationName |DscNodeStatusData |
| ResultType |Se o nó hello está em conformidade. |
| NodeName_s |nome de saudação do nó gerenciado hello. |
| NodeComplianceStatus_s |Se o nó hello está em conformidade. |
| DscReportStatus |Verificação de conformidade de saudação foi executada com êxito. |
| ConfigurationMode | Como a configuração de saudação é nó toohello aplicado. Os valores possíveis são __"ApplyOnly"__,__"ApplyandMonitior"__ e __"ApplyandAutoCorrect"__. <ul><li>__ApplyOnly__: DSC aplica-se a configuração de saudação e não faz nada além disso, a menos que uma nova configuração seja enviada por push toohello nó de destino ou quando uma nova configuração é extraída de um servidor. Depois da aplicação inicial de uma nova configuração, o DSC não procura descompasso de um estado previamente configurado. DSC tentativas de configuração de saudação tooapply até que seja bem-sucedida antes __ApplyOnly__ entra em vigor. </li><li> __ApplyAndMonitor__: Este é o valor padrão de saudação. Olá LCM aplica as novas configurações. Após a aplicação inicial de uma nova configuração, se o nó de destino Olá estiver dessincronizada do estado de saudação desejado, a DSC relatará discrepância Olá nos logs. DSC tentativas de configuração de saudação tooapply até que seja bem-sucedida antes __ApplyAndMonitor__ entra em vigor.</li><li>__ApplyAndAutoCorrect__: o DSC aplica as novas configurações. Após a aplicação inicial de uma nova configuração, se o nó de destino Olá estiver dessincronizada do estado de saudação desejado, DSC relatará a discrepância Olá nos logs e reaplica a configuração atual de saudação.</li></ul> |
| HostName_s | nome de saudação do nó gerenciado hello. |
| IPAddress | endereço IPv4 Olá Olá gerenciados nó. |
| Categoria | DscNodeStatus |
| Recurso | nome de saudação do hello conta de automação do Azure. |
| Tenant_g | GUID que identifica o locatário Olá para Olá chamador. |
| NodeId_g |GUID que identifica o nó gerenciado hello. |
| DscReportId_g |GUID que identifica o relatório de saudação. |
| LastSeenTime_t |Data e hora quando o relatório de saudação última foi exibido. |
| ReportStartTime_t |Data e hora em que o relatório de saudação foi iniciado. |
| ReportEndTime_t |Data e hora em que o relatório de saudação concluído. |
| NumberOfResources_d |número de saudação de recursos DSC chamado hello configuração aplicada toohello nó. |
| SourceSystem | Como a análise de Log coletados dados saudação. Sempre *Azure* para o Diagnóstico do Azure. |
| ResourceId |Especifica a conta de automação do Azure hello. |
| ResultDescription | Descrição de saudação para esta operação. |
| SubscriptionId | Olá Id (GUID) de assinatura do Azure para Olá conta de automação. |
| ResourceGroup | Nome do grupo de recursos Olá Olá conta de automação. |
| ResourceProvider | MICROSOFT.AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |
| CorrelationId |GUID que é a Id de correlação de relatório de conformidade de saudação do hello. |

### <a name="dscresourcestatusdata"></a>DscResourceStatusData

| Propriedade | Descrição |
| --- | --- |
| TimeGenerated |Data e hora quando a verificação de conformidade de saudação foi executada. |
| OperationName |DscResourceStatusData|
| ResultType |Se o recurso de saudação está em conformidade. |
| NodeName_s |nome de saudação do nó gerenciado hello. |
| Categoria | DscNodeStatus |
| Recurso | nome de saudação do hello conta de automação do Azure. |
| Tenant_g | GUID que identifica o locatário Olá para Olá chamador. |
| NodeId_g |GUID que identifica o nó gerenciado hello. |
| DscReportId_g |GUID que identifica o relatório de saudação. |
| DscResourceId_s |nome de saudação da instância do recurso de saudação DSC. |
| DscResourceName_s |nome de saudação do recurso de saudação DSC. |
| DscResourceStatus_s |Se Olá recurso DSC está em conformidade. |
| DscModuleName_s |nome de saudação do módulo do PowerShell Olá que contém o recurso de DSC hello. |
| DscModuleVersion_s |versão de saudação do módulo do PowerShell Olá que contém o recurso de DSC hello. |
| DscConfigurationName_s |nome de saudação da configuração de saudação aplicado toohello nó. |
| ErrorCode_s | código de erro de saudação se Olá recurso falhou. |
| ErrorMessage_s |mensagem de erro de saudação se Olá recurso falhou. |
| DscResourceDuration_d |tempo de saudação, em segundos, que Olá recurso DSC executado. |
| SourceSystem | Como a análise de Log coletados dados saudação. Sempre *Azure* para o Diagnóstico do Azure. |
| ResourceId |Especifica a conta de automação do Azure hello. |
| ResultDescription | Descrição de saudação para esta operação. |
| SubscriptionId | Olá Id (GUID) de assinatura do Azure para Olá conta de automação. |
| ResourceGroup | Nome do grupo de recursos Olá Olá conta de automação. |
| ResourceProvider | MICROSOFT.AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |
| CorrelationId |GUID que é a Id de correlação de relatório de conformidade de saudação do hello. |

## <a name="summary"></a>Resumo

Enviando seu dados de DSC de automação tooLog análise, você pode obter uma noção melhor sobre status de saudação de seus nós de DSC de automação por:

* Configurar alertas toonotify você quando há um problema
* Usando modos de exibição personalizados e toovisualize de consultas de pesquisa seus resultados de runbook, o status do trabalho de runbook e outros relacionam principais indicadores ou métricas.  

Análise de log fornece maior visibilidade operacionais tooyour DSC de automação dados e pode ajudar a incidentes de endereço mais rapidamente.  

## <a name="next-steps"></a>Próximas etapas

* toolearn mais sobre como revisão e consultas de pesquisa diferentes tooconstruct Olá DSC de automação registra em log com a análise de Log, consulte [pesquisas de Log na análise de Log](../log-analytics/log-analytics-log-searches.md)
* toolearn mais sobre como usar o DSC de automação do Azure, consulte [guia de Introdução ao DSC de automação do Azure](automation-dsc-getting-started.md)
* toolearn mais sobre análise de logs do OMS e fontes de coleta de dados, consulte [dados de armazenamento do Azure coleta na visão geral da análise de Log](../log-analytics/log-analytics-azure-storage.md)

