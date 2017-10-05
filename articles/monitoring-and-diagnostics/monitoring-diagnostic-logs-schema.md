---
title: "Serviços e esquemas com suporte para os logs de diagnóstico do Azure | Microsoft Docs"
description: "Compreenda o esquema de serviços e eventos com suporte para Logs de Diagnóstico do Azure."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: fe8887df-b0e6-46f8-b2c0-11994d28e44f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: aa4fa6e0310b2725005dfa34e3225c89fb4282d6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="supported-services-schemas-and-categories-for-azure-diagnostic-logs"></a>Serviços, esquemas e categorias com suporte para os logs de diagnóstico do Azure

Os [logs de diagnóstico de recursos do Azure](monitoring-overview-of-diagnostic-logs.md) são emitidos por seus recursos do Azure que descrevem a operação do recurso. Esses logs são específicos do tipo de recurso. Neste artigo, vamos descrever o conjunto de serviços com suporte e o esquema de evento para os eventos emitidos por cada serviço. Este artigo também inclui uma lista completa das categorias de log disponíveis por tipo de recurso.

## <a name="supported-services-and-schemas-for-resource-diagnostic-logs"></a>Serviços e esquemas com suporte para os logs de diagnóstico de recurso
O esquema para os logs de diagnóstico de recurso varia dependendo do recurso e da categoria do log.   

| O Barramento de | Esquema e Documentos |
| --- | --- |
| Gerenciamento da API | Esquema não disponível. |
| Gateways do Aplicativo |[Log de diagnóstico do Gateway de Aplicativo](../application-gateway/application-gateway-diagnostics.md) |
| Automação do Azure |[Análise de log para automação do Azure](../automation/automation-manage-send-joblogs-log-analytics.md) |
| Lote do Azure |[Logs de diagnóstico do Lote do Azure](../batch/batch-diagnostics.md) |
| Customer Insights | Esquema não disponível. |
| Rede de Distribuição de Conteúdo | Esquema não disponível. |
| CosmosDB | Esquema não disponível. |
| Análises Data Lake |[Acessando os logs de diagnóstico do Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-diagnostic-logs.md) |
| Repositório Data Lake |[Acessando os logs de diagnóstico do Azure Data Lake Store](../data-lake-store/data-lake-store-diagnostic-logs.md) |
| Hubs de Eventos |[Logs de diagnóstico dos Hubs de Eventos do Azure](../event-hubs/event-hubs-diagnostic-logs.md) |
| Cofre da Chave |[Logs do Cofre da Chave do Azure](../key-vault/key-vault-logging.md) |
| Balanceador de carga |[Log Analytics para o Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md) |
| Aplicativos Lógicos |[Esquema de controle personalizado dos Aplicativos Lógicos B2B](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md) |
| Grupos de segurança de rede |[Análise de logs para NSGs (grupos de segurança de rede)](../virtual-network/virtual-network-nsg-manage-log.md) |
| Serviços de Recuperação | Esquema não disponível.|
| Pesquisar |[Habilitação e uso da análise de tráfego de pesquisa](../search/search-traffic-analytics.md) |
| Gerenciamento do Servidor | Esquema não disponível. |
| Barramento de Serviço |[Logs de diagnóstico do Barramento de Serviço do Azure](../service-bus-messaging/service-bus-diagnostic-logs.md) |
| Análise de fluxo |[Logs de diagnóstico do trabalho](../stream-analytics/stream-analytics-job-diagnostic-logs.md) |

## <a name="supported-log-categories-per-resource-type"></a>Categorias de log com suporte por tipo de recurso
|Tipo de recurso|Categoria|Nome de exibição da categoria|
|---|---|---|
|Microsoft.ApiManagement/service|GatewayLogs|Logs relacionados ao Gateway ApiManagement|
|Microsoft.Automation/automationAccounts|JobLogs|Logs de trabalho|
|Microsoft.Automation/automationAccounts|JobStreams|Transmissões de trabalho|
|Microsoft.Automation/automationAccounts|DscNodeStatus|Status do nó DSC|
|Microsoft.Batch/batchAccounts|ServiceLog|Logs de serviço|
|Microsoft.Cdn/profiles/endpoints|CoreAnalytics|Obtém as métricas do ponto de extremidade, como largura de banda, saída etc.|
|Microsoft.CustomerInsights/hubs|AuditEvents|AuditEvents|
|Microsoft.DataLakeAnalytics/accounts|Audit|Logs de Auditoria|
|Microsoft.DataLakeAnalytics/accounts|Solicitações|Logs de solicitação|
|Microsoft.DataLakeStore/accounts|Audit|Logs de Auditoria|
|Microsoft.DataLakeStore/accounts|Solicitações|Logs de solicitação|
|Microsoft.DocumentDB/databaseAccounts|DataPlaneRequests|DataPlaneRequests|
|Microsoft.EventHub/namespaces|ArchiveLogs|Logs de arquivo|
|Microsoft.EventHub/namespaces|OperationalLogs|Logs operacionais|
|Microsoft.EventHub/namespaces|AutoScaleLogs|Logs de Escala Automática|
|Microsoft.KeyVault/vaults|AuditEvent|Logs de Auditoria|
|Microsoft.Logic/workflows|WorkflowRuntime|Eventos de diagnóstico de tempo de execução do fluxo de trabalho|
|Microsoft.Logic/integrationAccounts|IntegrationAccountTrackingEvents|Acompanhar os eventos da Conta de Integração|
|Microsoft.Network/networksecuritygroups|NetworkSecurityGroupEvent|Network Security Group Event|
|Microsoft.Network/networksecuritygroups|NetworkSecurityGroupRuleCounter|Contador de regras de grupo de segurança de rede|
|Microsoft.Network/loadBalancers|LoadBalancerAlertEvent|Eventos de alerta do Load Balancer|
|Microsoft.Network/loadBalancers|LoadBalancerProbeHealthStatus|Status de integridade da investigação do Load Balancer|
|Microsoft.Network/applicationGateways|ApplicationGatewayAccessLog|Log de acesso do Gateway de Aplicativo|
|Microsoft.Network/applicationGateways|ApplicationGatewayPerformanceLog|Log de desempenho do Gateway de Aplicativo|
|Microsoft.Network/applicationGateways|ApplicationGatewayFirewallLog|Log de firewall do Gateway de Aplicativo|
|Microsoft.RecoveryServices/Vaults|AzureBackupReport|Dados de relatórios de backup do Azure|
|Microsoft.RecoveryServices/Vaults|AzureSiteRecoveryJobs|Trabalhos do Azure Site Recovery|
|Microsoft.RecoveryServices/Vaults|AzureSiteRecoveryEvents|Eventos do Azure Site Recovery|
|Microsoft.RecoveryServices/Vaults|AzureSiteRecoveryReplicatedItems|Itens replicados do Azure Site Recovery|
|Microsoft.Search/searchServices|OperationLogs|Logs de operação|
|Microsoft.ServiceBus/namespaces|OperationalLogs|Logs operacionais|
|Microsoft.StreamAnalytics/streamingjobs|Execução|Execução|
|Microsoft.StreamAnalytics/streamingjobs|Criação|Criação|

## <a name="next-steps"></a>Próximas etapas

* [Saiba mais sobre logs de diagnóstico](monitoring-overview-of-diagnostic-logs.md)
* [Transmitir logs de diagnóstico de recurso os **Hubs de Eventos**](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [Alterar as configurações de diagnóstico do recurso usando a API REST do Azure Monitor](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [Analisar logs do Armazenamento do Azure com o Log Analytics](../log-analytics/log-analytics-azure-storage.md)
