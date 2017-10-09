---
title: "aaaCollect Azure serviço logs e métricas para análise de Log | Microsoft Docs"
description: "Configure o diagnóstico em recursos do Azure toowrite logs e métricas tooLog análise."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 84105740-3697-4109-bc59-2452c1131bfe
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1cede9a94ec83c4e3a95853dc2ec355d8df06d6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-azure-service-logs-and-metrics-for-use-in-log-analytics"></a>Coletar logs e as métricas do serviço do Azure para uso no Log Analytics

Há quatro maneiras diferentes de coletar logs e métricas para os serviços do Azure:

1. Diagnóstico do Azure direcionar tooLog Analytics (*diagnóstico* em Olá a tabela a seguir)
2. Diagnóstico do Azure tooAzure armazenamento tooLog Analytics (*armazenamento* em Olá a tabela a seguir)
3. Conectores para os serviços do Azure (*conectores* em Olá a tabela a seguir)
4. Scripts de toocollect e, em seguida, os dados de postagem em análise de Log (espaços em branco em Olá a tabela a seguir e serviços que não estão listados)


| O Barramento de                 | Tipo de recurso                           | Logs        | Métricas     | Solução |
| --- | --- | --- | --- | --- |
| Application gateways    | Microsoft.Network/applicationGateways   | Diagnostics | Diagnostics | [Análise de Gateway de Aplicativo do Azure](log-analytics-azure-networking-analytics.md#azure-application-gateway-analytics-solution-in-log-analytics) |
| Application insights    |                                         | Conector   | Conector   | [Conector do Application Insights](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/) (visualização) |
| Contas de automação     | Microsoft.Automation/AutomationAccounts | Diagnostics |             | [Mais informações](../automation/automation-manage-send-joblogs-log-analytics.md)|
| Contas do Lote          | Microsoft.Batch/batchAccounts           | Diagnostics | Diagnostics | |
| Serviços de Nuvem clássicos  |                                         | Armazenamento     |             | [Mais informações](log-analytics-azure-storage-iis-table.md) |
| Serviços cognitivos      | Microsoft.CognitiveServices/accounts    |             | Diagnostics | |
| Data Lake Analytics     | Microsoft.DataLakeAnalytics/accounts    | Diagnostics |             | |
| Data Lake Store         | Microsoft.DataLakeStore/accounts        | Diagnostics |             | |
| Namespace do Hub de Eventos     | Microsoft.EventHub/namespaces           | Diagnostics | Diagnostics | |
| Hubs IoT                | Microsoft.Devices/IotHubs               |             | Diagnostics | |
| Cofre da Chave               | Microsoft.KeyVault/vaults               | Diagnostics |             | [KeyVault Analytics](log-analytics-azure-key-vault.md) |
| Balanceadores de Carga          | Microsoft.Network/loadBalancers         | Diagnostics |             |  |
| Aplicativos Lógicos              | Microsoft.Logic/workflows <br> Microsoft.Logic/integrationAccounts | Diagnostics | Diagnostics | |
| Grupos de segurança de rede | Microsoft.Network/networksecuritygroups | Diagnostics |             | [Análise de Grupo de Segurança de Rede do Azure](log-analytics-azure-networking-analytics.md#azure-network-security-group-analytics-solution-in-log-analytics) |
| Cofres de recuperação         | Microsoft.RecoveryServices/vaults       |             |             | [Análise dos Serviços de Recuperação do Azure (Visualização)](https://github.com/krnese/AzureDeploy/blob/master/OMS/MSOMS/Solutions/recoveryservices/)|
| Serviços de pesquisa         | Microsoft.Search/searchServices         | Diagnostics | Diagnostics | |
| Namespace do Barramento de Serviço   | Microsoft.ServiceBus/namespaces         | Diagnostics | Diagnostics | [Análise do Barramento de Serviço (Visualização)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-servicebus-solution)|
| Service Fabric          |                                         | Armazenamento     |             | [Análise do Service Fabric (visualização)](log-analytics-service-fabric.md) |
| SQL (v12)               | Microsoft.Sql/servers/databases <br> Microsoft.Sql/servers/elasticPools |             | Diagnostics | [Azure SQL Analytics (Visualização)](log-analytics-azure-sql.md) |
| Armazenamento                 |                                         |             | Script      | [Análise do Azure Storage (Visualização)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-azure-storage-analytics-solution) |
| Máquinas Virtuais        | Microsoft.Compute/virtualMachines       | Extensão   | Extensão <br> Diagnostics  | |
| Conjuntos de dimensionamento de Máquinas Virtuais | Microsoft.Compute/virtualMachines <br> Microsoft.Compute/virtualMachineScaleSets/virtualMachines |             | Diagnostics | |
| Farms do servidor Web        | Microsoft.Web/serverfarms               |             | Diagnostics | |
| Sites               | Microsoft.Web/sites <br> Microsoft.Web/sites/slots |             | Diagnostics | [Análise dos Aplicativos Web do Azure (Visualização)](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureWebAppsAnalyticsOMS?tab=Overview) |


> [!NOTE]
> Monitoramento de máquinas virtuais do Azure (Linux e Windows), é recomendável instalar Olá [extensão VM de análise de Log](log-analytics-azure-vm-extension.md). Agente de saudação fornece informações coletadas de dentro de suas máquinas virtuais. Você também pode usar a extensão de saudação para conjuntos de escala de máquina Virtual.
>
>

## <a name="azure-diagnostics-direct-toolog-analytics"></a>Diagnóstico do Azure direcionar tooLog análise
Muitos recursos do Azure são métricas e logs de diagnóstico toowrite capaz diretamente tooLog análise e isso é a maneira de saudação preferencial de coleta de dados de saudação para análise. Ao usar o diagnóstico do Azure, dados são gravados imediatamente tooLog análise e não há nenhuma necessidade toofirst gravação Olá dados toostorage.

Recursos do Azure que oferecem suporte a [monitor Azure](../monitoring-and-diagnostics/monitoring-overview.md) pode enviar seus logs e métricas diretamente tooLog análise.

* Para obter detalhes de saudação de métricas disponíveis Olá, consulte muito[suporte para métricas com o Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).
* Para obter detalhes de saudação dos logs disponíveis hello, consulte muito[serviços e esquema com suporte para logs de diagnóstico](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).

### <a name="enable-diagnostics-with-powershell"></a>Habilitar diagnóstico com PowerShell
Você precisa Olá novembro de 2016 (v2.3.0) ou versão posterior do [Azure PowerShell](/powershell/azure/overview).

Olá PowerShell mostrado no exemplo a seguir como toouse [AzureRmDiagnosticSetting conjunto](/powershell/module/azurerm.insights/set-azurermdiagnosticsetting) tooenable diagnóstico em um grupo de segurança de rede. Olá mesma abordagem funciona para todos os recursos com suporte - definir `$resourceId` toohello id de recurso do recurso Olá você deseja que o diagnóstico tooenable para.

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO"

Set-AzureRmDiagnosticSetting -ResourceId $ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="enable-diagnostics-with-resource-manager-templates"></a>Habilitar diagnósticos com modelos do Resource Manager

tooenable o diagnóstico em um recurso quando ele é criado e diagnóstico Olá enviaram espaço de trabalho de análise de Log de tooyour que você pode usar um toohello semelhante de modelo um abaixo. Este exemplo destina-se a uma conta de automação, mas funciona em todos os tipos de recursos com suporte.

```json
        {
            "type": "Microsoft.Automation/automationAccounts/providers/diagnosticSettings",
            "name": "[concat(parameters('omsAutomationAccountName'), '/', 'Microsoft.Insights/service')]",
            "apiVersion": "2015-07-01",
            "dependsOn": [
                "[concat('Microsoft.Automation/automationAccounts/', parameters('omsAutomationAccountName'))]",
                "[concat('Microsoft.OperationalInsights/workspaces/', parameters('omsWorkspaceName'))]"
            ],
            "properties": {
                "workspaceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('omsWorkspaceName'))]",
                "logs": [
                    {
                        "category": "JobLogs",
                        "enabled": true
                    },
                    {
                        "category": "JobStreams",
                        "enabled": true
                    }
                ]
            }
        }
```

[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="azure-diagnostics-toostorage-then-toolog-analytics"></a>Diagnóstico do Azure toostorage e tooLog análise

Para coletar logs de dentro de alguns recursos, é possível toosend Olá logs tooAzure armazenamento e, em seguida, configurar logs de saudação de tooread de análise de Log do armazenamento.

Análise de log pode usar o diagnóstico de toocollect essa abordagem do armazenamento do Azure para Olá logs e os recursos a seguir:

| Recurso | Logs |
| --- | --- |
| Service Fabric |ETWEvent <br> Evento operacional <br> Evento de ator confiável <br> Evento de serviço confiável |
| Máquinas Virtuais |Linux Syslog <br> Evento do Windows <br> Log do IIS <br> Windows ETWEvent |
| Funções web <br> Funções de trabalho |Linux Syslog <br> Evento do Windows <br> Log do IIS <br> Windows ETWEvent |

> [!NOTE]
> Você é cobrado taxas de dados do Azure normais para armazenamento e transações quando enviar diagnósticos tooa conta de armazenamento e quando a análise de Log ler dados saudação da conta de armazenamento.
>
>

Consulte [armazenamento de blob de uso para o IIS e a tabela de armazenamento para eventos](log-analytics-azure-storage-iis-table.md) toolearn mais informações sobre como a análise de Log pode coletar esses logs.

## <a name="connectors-for-azure-services"></a>Conectores para serviços do Azure

Há um conector para o Application Insights, que permite que os dados coletados pelo Application Insights toobe enviado tooLog análise.

Saiba mais sobre Olá [conector Application Insights](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/).

## <a name="scripts-toocollect-and-post-data-toolog-analytics"></a>Scripts dados de postagem e toocollect tooLog análise

Serviços do Azure que não fornecem um tooLog de forma direta toosend logs e métricas de análise, você pode usar um toocollect de script de automação do Azure Olá log e métricas. Olá Olá script pode, em seguida, enviar Olá dados tooLog análise usando [API do coletor de dados](log-analytics-data-collector-api.md)

Galeria de modelos do Azure de saudação tem [exemplos de como usar a automação do Azure](https://azure.microsoft.com/en-us/resources/templates/?term=OMS) toocollect dados dos serviços e enviá-la tooLog análise.

## <a name="next-steps"></a>Próximas etapas

* [Usar o armazenamento de blob para IIS e a tabela de armazenamento para eventos](log-analytics-azure-storage-iis-table.md) tooread logs de saudação para serviços do Azure que gravar diagnóstico tootable tooblob escrito armazenamento de logs de armazenamento ou o IIS.
* [Habilitar soluções](log-analytics-add-solutions.md) tooprovide ideias sobre dados de saudação.
* [Usar consultas de pesquisa](log-analytics-log-searches.md) tooanalyze dados de saudação.
