# Visão geral
## [Ferramentas de monitoramento no Azure](monitoring-overview.md)
## [Azure Monitor](monitoring-overview-azure-monitor.md)
## [Métricas](monitoring-overview-metrics.md)
## [Alertas](monitoring-overview-alerts.md)
## [Autoescala](monitoring-overview-autoscale.md)
## [Log de atividade](monitoring-overview-activity-logs.md)
## [Grupos de Ação](monitoring-action-groups.md)
## [Logs de Diagnóstico](monitoring-overview-of-diagnostic-logs.md)
## [Integrações de parceiro](monitoring-partners.md)
## [Extensão de Diagnóstico do Azure](azure-diagnostics.md)


# Introdução
## [Introdução ao Azure Monitor](monitoring-get-started.md)
## [Introdução ao Dimensionamento Automático](monitoring-autoscale-get-started.md)
## [Permissões e segurança de funções](monitoring-roles-permissions-security.md)


# Como
## Usar alertas
### [Configurar alertas no Portal do Azure](insights-alerts-portal.md)
### [Configurar alertas com a CLI](insights-alerts-command-line-interface.md)
### [Configurar alertas com o PowerShell](insights-alerts-powershell.md)
### [Fazer com que a alerta de métrica chame um webhook](insights-webhooks-alerts.md)
### [Criar um alerta de métrica com um modelo do Resource Manager](monitoring-enable-alerts-using-template.md)
## Usar autoescala
### [Práticas recomendadas](insights-autoscale-best-practices.md)
### [Métricas comuns](insights-autoscale-common-metrics.md)
### [Padrões comuns](monitoring-autoscale-common-scale-patterns.md)
### [Dimensionamento automático usando uma métrica personalizada](monitoring-autoscale-scale-by-custom-metric.md)
### [Dimensionar automaticamente conjuntos de Dimensionamento de VMs usando modelos do Resource Manager](insights-advanced-autoscale-virtual-machine-scale-sets.md)
### [Dimensionar automaticamente computadores em um conjunto de Dimensionamento de VM](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md?toc=%2fazure%2fmonitoring-and-diagnostics%2ftoc.json)
### [Configurar webhooks e notificações por email em dimensionamento automático](insights-autoscale-to-webhook-email.md)
## Use o log de atividades de saudação
### [Exibir eventos no log de atividades](../azure-resource-manager/resource-group-audit.md?toc=%2fazure%2fmonitoring-and-diagnostics%2ftoc.json)
### [Configurar alertas em um evento de log de atividade](monitoring-activity-log-alerts.md)
### [Arquivar log de atividades](monitoring-archive-activity-log.md)
### [Fluxo de log de atividade tooEvent Hubs](monitoring-stream-activity-logs-event-hubs.md)
### [Operações de auditoria com o Gerenciador de Recursos](../azure-resource-manager/resource-group-audit.md?toc=%2fazure%2fmonitoring-and-diagnostics%2ftoc.json)
### [Criar alertas de log de atividade com o Gerenciador de Recursos](monitoring-create-activity-log-alerts-with-resource-manager-template.md)
### [Migrar tooActivity alertas de Log](monitoring-migrate-management-alerts.md)
## Usar Notificações de serviço
### [Exibir notificações de serviço](monitoring-service-notifications.md)
### [Configurar alertas em notificações de serviço](monitoring-activity-log-alerts-on-service-notifications.md)
## Usar Grupos de Ação
### [Saiba mais sobre o esquema de webhook](monitoring-activity-log-alerts-webhook.md)
### [Comportamento de Alerta do SMS](monitoring-sms-alert-behavior.md)
### [Limitação de Taxa de Alerta](monitoring-alerts-rate-limiting.md)
### [Criar grupos de ação com o Gerenciador de Recursos](monitoring-create-action-group-with-resource-manager-template.md)
## Gerenciar logs de diagnóstico
### [Arquivar](monitoring-archive-diagnostic-logs.md)
### [Fluxo tooEvent Hubs](monitoring-stream-diagnostic-logs-to-event-hubs.md)
### [Habilitar configurações de Diagnóstico usando modelos do Gerenciador de Recursos](monitoring-enable-diagnostic-logs-using-template.md)
## Use Olá API REST
### [Passo a passo usando a API REST](monitoring-rest-api-walkthrough.md)
## Use a extensão de Diagnóstico do Azure
### [Enviar informações de tooApplication](azure-diagnostics-configure-application-insights.md)
### [Enviar Hubs tooEvent](azure-diagnostics-streaming-event-hubs.md)
### [Solução de problemas](azure-diagnostics-troubleshooting.md)

# Referência
## [Exemplos de código](https://azure.microsoft.com/en-us/resources/samples/?service=monitor)
## [Fontes de dados de monitoramento](monitoring-data-sources.md)
## [Lista de métricas com suporte](monitoring-supported-metrics.md)
## [Esquema sobre eventos do log de atividades](monitoring-activity-log-schema.md)
## [Serviços com suporte, categorias e esquemas para logs de diagnóstico](monitoring-diagnostic-logs-schema.md)
## [PowerShell](/powershell/module/azurerm.insights)
## [.NET](https://msdn.microsoft.com/library/azure/dn802153)
## [REST](/rest/api/monitor/)
## [Esquema de extensão do Diagnóstico do Azure](azure-diagnostics-schema.md)
### [1.0](azure-diagnostics-schema-1dot0.md)
### [1.2](azure-diagnostics-schema-1dot2.md)
### [1.3 e posterior](azure-diagnostics-schema-1dot3-and-later.md)

# Recursos
## [Exemplos de CLI 1.0 do Azure](insights-cli-samples.md)
## [Roteiro do Azure](https://azure.microsoft.com/roadmap/?category=monitoring-management)
## [Exemplos do PowerShell](insights-powershell-samples.md)
## [Calculadora de preço](https://azure.microsoft.com/pricing/calculator/)
## [Vídeos](https://azure.microsoft.com/resources/videos/index/?services=monitor)
## [Modelos de início rápido](https://azure.microsoft.com/en-us/resources/templates/?resourceType=Microsoft.Insights)
