---
title: aaaAzure log e auditoria | Microsoft Docs
description: "Saiba mais sobre como você pode usar o registro em log dados toogain informações sobre o seu aplicativo."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: d0e817b071962ad9bef6250267092b5f9282bc7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-logging-and-auditing"></a>Log e auditoria do Azure
## <a name="introduction"></a>Introdução
### <a name="overview"></a>Visão geral
tooassist clientes atuais e potenciais do Azure compreensão e uso Olá diversos recursos relacionados à segurança disponíveis no e ao redor Olá plataforma Azure, a Microsoft desenvolveu uma série de white papers, visões gerais de segurança, práticas recomendadas e listas de verificação. Olá tópicos variam em termos de amplitude e profundidade e são atualizadas periodicamente. Este documento é parte da série, como resumido Olá abstrata seção a seguir.
### <a name="azure-platform"></a>Plataforma Azure
O Azure é uma plataforma de serviço de nuvem aberta e flexível que suporta Olá a seleção mais ampla de sistemas operacionais, linguagens de programação, estruturas, ferramentas, bancos de dados e dispositivos.

Por exemplo, você pode:
-   Executar contêineres do Linux com a integração com o Docker.

-   Criar aplicativos com JavaScript, Python, .NET, PHP, Java e Node.js

-   Criar back-ends para dispositivos iOS, Android e Windows.

Serviços de nuvem pública do Azure oferecem suporte a saudação tecnologias mesmo milhões de desenvolvedores e profissionais de TI já contam e confiarem.

Quando você construir ou migra ativos de TI para um provedor de nuvem, você depender de tooprotect de recursos da organização seus aplicativos e dados com hello controles hello e serviços que eles fornecem segurança de saudação do toomanage de seus ativos com base em nuvem.

Infraestrutura do Azure foi projetada de saudação recurso tooapplications para hospedagem milhões de clientes simultaneamente, e fornece uma base confiável em que as empresas podem atender às suas necessidades de segurança. Além disso, Azure fornece uma ampla gama de segurança configuráveis toocontrol de capacidade de opções e hello-los para que você possa personalizar requisitos exclusivos de saudação do toomeet de segurança de suas implantações. Este documento ajuda você a atender a esses requisitos.

### <a name="abstract"></a>Resumo
A auditoria e o log de eventos relacionados à segurança, bem como alertas relacionados, são componentes importantes em uma estratégia de proteção de dados eficaz. Logs de segurança e os relatórios fornecem um registro eletrônico de atividades suspeitas e ajuda a detectar padrões que podem indicar a penetração externa com êxito ou tentativa de rede hello, bem como os ataques internos. Você pode usar a atividade de usuário toomonitor auditoria, conformidade normativa do documento, executar análise forense e muito mais. Os alertas fornecem uma notificação imediata quando ocorrem eventos de segurança.

Produtos e serviços do Microsoft Azure fornecem a auditoria de segurança configurável e log opções toohelp você identificar lacunas em suas políticas de segurança e mecanismos e toohelp esses intervalos de endereços impedir violações. Serviços da Microsoft oferecem algumas (e, em alguns casos, todas as) de saudação as opções a seguir: monitoramento centralizado, registro em log e visibilidade contínua de análise sistemas tooprovide; alertas em tempo hábil; e relatórios toohelp que gerenciar grande quantidade de saudação de informações geradas por dispositivos e serviços.

Dados de log do Microsoft Azure podem ser exportado tooSecurity sistemas de incidentes e gerenciamento de eventos (SIEM) para análise e integra-se com soluções de auditoria de terceiros.

Este white paper fornece uma introdução para a geração, coleta e análise dos logs de segurança de serviços hospedados no Azure e pode ajudá-lo a obter informações de segurança sobre as implantações do Azure. escopo de saudação deste white paper é tooapplications limitada e serviços construído e implantado no Azure.

> [!Note]
> Algumas recomendações contidas neste documento podem resultar no aumento do uso de dados, de rede ou dos recursos de computação e aumentar os custos da licença ou da assinatura.

## <a name="types-of-logs-in-azure"></a>Tipos de logs no Azure
Os aplicativos em nuvem são complexos com muitas partes móveis. Os logs fornecem dados tooensure que seu aplicativo permaneça ativo e em execução em um estado íntegro. Ele também ajuda você toostave off problemas potenciais ou solucionar problemas após os. Além disso, você pode usar o registro em log dados toogain informações sobre o seu aplicativo. Esse conhecimento pode ajudá-lo a facilidade de manutenção ou de desempenho do aplicativo tooimprove, ou automatizar ações que normalmente exigiriam a intervenção manual.

O Azure produz um log abrangente para cada um de seus serviço. Esses logs são categorizados por esses tipos principais:
-   **Logs de gerenciamento do controle** dar visibilidade Olá operações do Azure Resource Manager CREATE, UPDATE e DELETE. Os [Logs de Atividades do Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) são um exemplo desse tipo de log.

-   **Logs de plano de dados** ofereçam visibilidade em eventos de saudação gerados como parte do uso de saudação de um recurso do Azure. Exemplos desse tipo de log são Olá eventos do Windows no sistema, segurança, e logs do aplicativo em uma máquina virtual e Olá [Logs de diagnóstico](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) configurado por meio do Monitor do Azure


-   Os **eventos processados** fornecem informações sobre os eventos/alertas analisados que foram processados em seu nome. Exemplos desse tipo são os [Alertas da Central de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts), nos quais a [Central de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) processou e analisou sua assinatura e fornece alertas de segurança concisos

tabela a seguir de saudação tipo mais importante de lista de logs disponíveis no Azure.

| Categoria do Log | Tipo de Log | Usos | Integração |
| ------------ | -------- | ------ | ----------- |
|[Logs de Atividades](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)|Eventos de plano de controle nos recursos do Azure Resource Manager| Fornece informações sobre operações de saudação que foram executadas em recursos em sua assinatura.|   API REST e [Azure Monitor](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)|
|[Logs de Diagnóstico do Azure](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)|dados frequentes sobre a operação de saudação do Azure Resource Manager recursos na assinatura| Fornecem informações sobre as operações que o recurso executou por conta própria| Azure Monitor, [Stream](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)|
|[Relatórios do AAD](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-azure-portal)|Logs e relatórios|Atividades de conexão do usuário e informações de atividades do Sistema sobre gerenciamento de usuários e grupos|[API gráfica](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-graph-api-quickstart)|
|[Máquina Virtual e Serviços de Nuvem](https://docs.microsoft.com/en-us/azure/cloud-services/cloud-services-dotnet-diagnostics-storage)|Log de eventos do Windows e syslog do Linux|  Captura de dados do sistema e dados de log em máquinas virtuais de saudação e transfere dados em uma conta de armazenamento de sua escolha.| Windows com [WAD](https://docs.microsoft.com/en-us/azure/azure-diagnostics) (armazenamento do Diagnóstico do Microsoft Azure) e Linux no Azure Monitor|
|[Análise de Armazenamento](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/storage-analytics)|Log de armazenamento; fornece dados de métrica de uma conta de armazenamento|Fornece informações das solicitações de rastreamento, analisa tendências de uso e diagnostica problemas com a conta de armazenamento.|  API REST ou hello [biblioteca de cliente](https://msdn.microsoft.com/en-us/library/azure/mt347887.aspx)|
|[Logs de fluxo do NSG (Grupo de Segurança de Rede)](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-nsg-flow-logging-overview)|Formato JSON; mostra os fluxos de entrada e saída por regra|Exibe informações sobre o tráfego IP de entrada e saída por meio de um Grupo de Segurança de Rede|[Observador de Rede](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview)|
|[Application Insights](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-overview)|Logs, exceções e diagnóstico personalizado|  Serviço APM (Gerenciamento de Desempenho de Aplicativos) para desenvolvedores da Web em várias plataformas.| API REST, [Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-azure-and-power-bi/)|
|Dados do processo/alerta de segurança| Alerta da Central de Segurança do Azure, alerta do OMS| Informações de segurança e alertas.|   APIs REST, JSON|

### <a name="activity-log"></a>Log de Atividade
Olá [o Log de atividades do Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs), fornece informações sobre operações de saudação que foram executadas em recursos em sua assinatura. Hello atividade Log era conhecido anteriormente como "Logs de auditoria" ou "Logs operacionais", desde que ele relata [eventos de plano de controle](https://driftboatdave.com/2016/10/13/azure-auditing-options-for-your-custom-reporting-needs/) para suas assinaturas. Usando hello atividade de Log, você pode determinar hello ", que e quando" para qualquer gravação as operações executadas em recursos de saudação em sua assinatura (PUT, POST, DELETE). Você também pode saber o status de saudação da operação de saudação e outras propriedades relevantes. Olá Log de atividades não inclui operações de leitura (GET).

Aqui PUT, POST, DELETE se refere a operações de gravação de saudação tooall log de atividades contém recursos de saudação. Por exemplo, você pode usar o hello atividade logs toofind um erro ao solucionar o problema ou toomonitor como um usuário em sua organização modificado a um recurso.

![Log de Atividade](./media/azure-log-audit/azure-log-audit-fig1.png)


Você pode recuperar eventos de seu Log de atividade usando Olá portal do Azure, [CLI](https://docs.microsoft.com/azure/storage/storage-azure-cli), cmdlets do PowerShell, e [API REST do Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-rest-api-walkthrough). Os logs de atividades têm um período de retenção de dados de 19 dias.

Cenários de integração
-   [Criar um alerta de email ou webhook que dispara um evento do Log de Atividades.](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-auditlog-to-webhook-email)

-   [Fluxo de tooan Hub de eventos](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-stream-activity-logs-event-hubs) para ingestão por um serviço de terceiros ou a solução de análise personalizado, como o Power BI.

-   Analisá-los no Power BI usando Olá [pacote de conteúdo do Power BI.](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs/)

-   [Salvá-lo tooa conta de armazenamento para inspeção manual ou de arquivamento.](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-archive-activity-log) Você pode especificar o tempo de retenção de saudação (em dias) usando perfis de Log.

-   Consultar e exibi-lo no portal do Azure de saudação.

-   Consultar por meio de Cmdlet do PowerShell, da CLI ou da API REST.

-   Exportar Olá Log de atividades com perfis de Log muito[de análise de log](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview).

Você pode usar uma conta de armazenamento ou [namespace de hub de eventos](https://docs.microsoft.com/azure/event-hubs/event-hubs-resource-manager-namespace-event-hub-enable-archive) que não está em Olá a mesma assinatura conforme Olá um log de emissão. usuário de saudação que define a configuração de saudação deve ter Olá apropriado [RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) tooboth assinaturas de acesso
### <a name="azure-diagnostic-logs"></a>Logs de Diagnóstico do Azure
Logs de diagnóstico do Azure são emitidos por um recurso que fornecem dados ricos, frequentes sobre a operação de saudação do recurso. conteúdo de saudação desses logs varia por tipo de recurso (por exemplo, [os logs de eventos do sistema Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events)são uma categoria de Log de diagnóstico para VMs e [blob, tabela e fila logs](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account) são categorias de Logs de diagnóstico para contas de armazenamento) e diferem das hello atividade de Log, que fornece informações sobre operações de saudação que foram executadas em recursos em sua assinatura.

![Logs de Diagnóstico do Azure](./media/azure-log-audit/azure-log-audit-fig2.png)

Os Logs de Diagnóstico do Azure oferecem várias opções de configuração, ou seja, o portal do Azure, usando o PowerShell, a CLI (Interface de Linha de Comando) e a API REST.

**Cenários de integração**
-   Salvá-las tooa [conta de armazenamento](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-archive-diagnostic-logs) para inspeção de auditoria ou manual. Você pode especificar o tempo de retenção saudação (em dias) usando as configurações de diagnóstico de saudação.

-   [Transmiti-los Hubs tooEvent](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs) para ingestão por um serviço de terceiros ou a solução de análise personalizado como [Power BI.](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

-   Analisá-los com o [Log Analytics do OMS.](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)

**Serviços com suporte, esquema dos Logs de Diagnóstico e categorias de logs com suporte por tipo de recurso**


| O Barramento de | Esquema e Documentos | Tipo de recurso | Categoria |
| ------- | ------------- | ------------- | -------- |
|Balanceador de carga| [Análise de log para o Balanceador de Carga do Azure (Preview)](https://docs.microsoft.com/en-us/azure/load-balancer/load-balancer-monitor-log)|Microsoft.Network/loadBalancers|  LoadBalancerAlertEvent|
|||Microsoft.Network/loadBalancers| LoadBalancerProbeHealthStatus
|Grupos de segurança de rede|[Análise de logs para NSGs (grupos de segurança de rede)](https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-nsg-manage-log)|Microsoft.Network/networksecuritygroups|NetworkSecurityGroupEvent|
|||Microsoft.Network/networksecuritygroups|NetworkSecurityGroupRuleCounter|
|Gateways do Aplicativo|[Log de diagnóstico do Application Gateway](https://docs.microsoft.com/en-us/azure/application-gateway/application-gateway-diagnostics)|Microsoft.Network/applicationGateways|ApplicationGatewayAccessLog|
|||Microsoft.Network/applicationGateways|ApplicationGatewayPerformanceLog|
|||Microsoft.Network/applicationGateways|ApplicationGatewayFirewallLog|
|Cofre da Chave|[Logs do Cofre da Chave do Azure](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-logging)|Microsoft.KeyVault/vaults|AuditEvent|
|Pesquisa do Azure|[Habilitação e uso da análise de tráfego de pesquisa](https://docs.microsoft.com/en-us/azure/search/search-traffic-analytics)|Microsoft.Search/searchServices|OperationLogs|
|Repositório Data Lake|[Acessando os logs de diagnóstico do Azure Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-diagnostic-logs)|Microsoft.DataLakeStore/accounts|Audit|
|Análises Data Lake|[Acessando os logs de diagnóstico do Azure Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-diagnostic-logs)|Microsoft.DataLakeAnalytics/accounts|Audit|
|||Microsoft.DataLakeAnalytics/accounts|Solicitações|
|||Microsoft.DataLakeStore/accounts|Solicitações|
|Aplicativos Lógicos|[Esquema de controle personalizado dos Aplicativos Lógicos B2B](https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-track-integration-account-custom-tracking-schema)|Microsoft.Logic/workflows|WorkflowRuntime|
|||Microsoft.Logic/integrationAccounts|IntegrationAccountTrackingEvents|
|Lote do Azure|[Logs de diagnóstico do Lote do Azure](https://docs.microsoft.com/en-us/azure/batch/batch-diagnostics)|Microsoft.Batch/batchAccounts|ServiceLog|
|Automação do Azure|[Análise de log para automação do Azure](https://docs.microsoft.com/en-us/azure/automation/automation-manage-send-joblogs-log-analytics)|Microsoft.Automation/automationAccounts|JobLogs|
|||Microsoft.Automation/automationAccounts|JobStreams|
|Hubs de Eventos|[Logs de diagnóstico dos Hubs de Eventos do Azure](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-diagnostic-logs)|Microsoft.EventHub/namespaces|ArchiveLogs|
|||Microsoft.EventHub/namespaces|OperationalLogs|
|Stream Analytics|[Logs de diagnóstico do trabalho](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-job-diagnostic-logs)|Microsoft.StreamAnalytics/streamingjobs|Execução|
|||Microsoft.StreamAnalytics/streamingjobs|Criação|
|Barramento de Serviço|[Logs de diagnóstico do Barramento de Serviço do Azure](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-diagnostic-logs)|Microsoft.ServiceBus/namespaces|OperationalLogs|

### <a name="azure-active-directory-reporting"></a>Relatórios do Azure Active Directory
O Active Directory do Azure (Azure AD) inclui relatórios de auditoria, atividade e segurança para seu diretório. Olá [relatório de auditoria do Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-guide) ajuda os clientes tooidentify privilegiado ações que ocorreram no seu Active Directory do Azure. Ações privilegiadas incluem alterações de elevação (por exemplo, criação de função ou redefinições de senha), alterar configurações de política (por exemplo políticas de senha), ou a configuração de toodirectory de alterações (por exemplo, alterações toodomain configurações de federação).

relatórios de Olá fornecem o registro de auditoria Olá para o nome do evento hello, ator Olá que executou a ação hello, o recurso de destino Olá afetada pela alteração Olá e data de saudação (em UTC). Os clientes são tooretrieve capaz de lista de saudação de eventos de auditoria para seu Azure Active Directory por meio de saudação [portal do Azure](https://portal.azure.com/), conforme descrito em [Exibir Logs de auditoria](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal). Aqui está uma lista de relatórios de saudação incluídos:

| Relatórios de segurança | Relatórios de atividades | Relatórios de auditoria |
| :--------------- | :--------------- | :------------ |
|Entradas de fontes desconhecidas| Uso do aplicativo: resumo| Relatório de auditoria de diretório|
|Entradas após várias falhas|  Uso do aplicativo: detalhado||
|Entradas de várias geografias|    Painel do aplicativo||
|Entradas de endereços IP com atividade suspeita|   Erros de provisionamento de conta||
|Atividades de entrada irregulares|    Dispositivos de usuário individual||
|Entradas de dispositivos possivelmente infectados|   Atividade de usuário individual||
|Usuários com atividade de entrada anômala| Relatório de atividade de grupos||
||Relatório de atividade de registro de redefinição de senha||
||Atividade de redefinição de senha|||

dados Olá desses relatórios podem ser útil tooyour aplicativos, como sistemas SIEM, auditoria e ferramentas de business intelligence. Olá AD do Azure reporting que APIs fornecem dados de toohello acesso programático por meio de um conjunto de APIs com base em REST. Você pode chamar essas [APIs](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started) em várias ferramentas e linguagens de programação.

Eventos em Olá relatório de auditoria do AD do Azure são mantidos por 180 dias.

> [!Note]
> Para obter mais informações sobre a retenção de relatórios, consulte [Políticas de retenção de relatórios do Azure Active Directory.](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-retention)

Para clientes interessados no armazenamento de seus eventos de auditoria por longos períodos de retenção, hello API de relatório pode ser usado pull tooregularly [eventos de auditoria](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-audit-events) em um repositório de dados separado.

### <a name="virtual-machine-logs-using-azure-diagnostics"></a>Logs da Máquina Virtual que usam o Diagnóstico do Azure
[Diagnóstico do Azure](https://docs.microsoft.com/azure/azure-diagnostics) é a capacidade de saudação dentro do Azure que habilita a coleta de saudação de dados de diagnóstico em um aplicativo implantado. Você pode usar a extensão de diagnóstico de saudação de várias fontes diferentes. As que têm suporte no momento são as [Funções de Trabalho ou Web do Serviço de Nuvem do Azure](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me),

![Logs da Máquina Virtual que usam o Diagnóstico do Azure](./media/azure-log-audit/azure-log-audit-fig3.png)

[Máquinas Virtuais do Azure](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/) que executam o Microsoft Windows e o [Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview).

É possível habilitar o Diagnóstico do Azure em uma máquina virtual usando os seguintes:

-   Usando o Visual Studio, consulte [tootrace Use o Visual Studio máquinas virtuais do Azure](https://docs.microsoft.com/azure/vs-azure-tools-debug-cloud-services-virtual-machines)

-   [Configurar o Diagnóstico do Azure em uma Máquina Virtual do Azure remotamente](https://docs.microsoft.com/azure/virtual-machines-dotnet-diagnostics)

-   [Use o PowerShell tooset o diagnóstico em máquinas virtuais do Azure](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-ps-extensions-diagnostics?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

-   [Criar uma máquina virtual do Windows com monitoramento e diagnóstico usando o modelo do Azure Resource Manager](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-extensions-diagnostics-template?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="storage-analytics"></a>Análise de Armazenamento
O [Azure Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) executa o registro em log e fornece dados de métrica para uma conta de armazenamento. Você pode usar este tootrace as solicitações de dados, analisar tendências de uso e diagnosticar problemas com sua conta de armazenamento. Log de análise de armazenamento está disponível para Olá [serviços Blob, fila e tabela.](https://docs.microsoft.com/azure/storage/storage-introduction) Análise de armazenamento registra informações detalhadas sobre o serviço de armazenamento de tooa de solicitações bem-sucedidas e com falha.

Essas informações podem ser usadas toomonitor as solicitações individuais e toodiagnose problemas com um serviço de armazenamento. As solicitações são registradas em uma base de melhor esforço. Entradas de log são criadas somente se houver solicitações feitas no ponto de extremidade de serviço hello. Por exemplo, se uma conta de armazenamento tiver atividade em seu ponto de extremidade de Blob, mas não em seus pontos de extremidade de fila ou tabela, somente registra pertencentes toohello serviço Blob é criado.

toouse análise de armazenamento, você deve habilitá-lo individualmente para cada serviço, você deseja toomonitor. Você pode habilitá-lo no hello [portal do Azure](https://portal.azure.com/); para obter detalhes, consulte [monitorar uma conta de armazenamento Olá portal do Azure.](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account) Você também pode habilitar a análise de armazenamento programaticamente por meio de saudação API REST ou biblioteca de saudação do cliente. Use Olá definir propriedades de serviço operação tooenable análise de armazenamento individualmente para cada serviço.

dados agregados Hello são armazenados em um blob conhecido (para registro em log) e em tabelas conhecidas (para Métrica), que podem ser acessadas usando o serviço de Blob hello e APIs do serviço de tabela.

Análise de armazenamento tem um limite de 20 TB em quantidade Olá dos dados armazenados que são independentes do limite total de saudação para sua conta de armazenamento. Todos os logs são armazenados em [blobs de blocos](https://docs.microsoft.com/azure/storage/storage-analytics) em um contêiner chamado $logs, que é criado automaticamente quando o Storage Analytics é habilitado em uma conta de armazenamento.

> [!Note]
> Para obter mais informações sobre cobrança e políticas de retenção de dados, consulte [Storage Analytics e cobrança.](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-and-billing)
>
> [!Note]
> Para obter mais informações sobre os limites da conta de armazenamento, consulte [Escalabilidade e metas de desempenho do Armazenamento do Azure.](https://docs.microsoft.com/azure/storage/storage-scalability-targets)

Olá seguintes tipos de solicitações autenticadas e anônimas está conectado.



| Autenticada  | Anônima|
| :------------- | :-------------|
| Solicitações bem-sucedidas | Solicitações bem-sucedidas |
|Solicitações com falha, incluindo tempo limite, limitação, rede, autorização e outros erros | Solicitações que usam uma SAS (Assinatura de Acesso Compartilhado), incluindo solicitações bem-sucedidas e com falha |
| Solicitações que usam uma SAS (Assinatura de Acesso Compartilhado), incluindo solicitações bem-sucedidas e com falha |Erros de tempo limite para o cliente e o servidor |
|   Dados de tooanalytics de solicitações |    Solicitações GET com falha com o código de erro 304 (Não Modificado) |
| As solicitações feitas pela própria análise de armazenamento, como criação de log ou exclusão, não estão conectadas. Uma lista completa dos dados saudação conectado está documentada em Olá [operações registradas em log de análise de armazenamento e mensagens de Status](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-logged-operations-and-status-messages) e [formato de Log de análise de armazenamento](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-log-format) tópicos. | Todas as outras solicitações anônimas com falha não estão conectadas. Uma lista completa dos dados saudação conectado está documentada em Olá [operações registradas em log de análise de armazenamento e mensagens de Status](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-logged-operations-and-status-messages) e [formato de Log de análise de armazenamento](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-log-format). |

### <a name="azure-networking-logs"></a>Logs de rede do Azure
O log e monitoramento de rede no Azure é completo e abrange duas categorias amplas:

-   [Inspetor de rede](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-watcher) -monitoramento de rede baseada em cenário é fornecido com recursos de saudação do observador de rede. Esse serviço inclui a captura de pacotes, próximo salto, verificação do fluxo de IP, exibição do grupo de segurança e logs de fluxo de NSG. Monitoramento do nível do cenário fornece uma exibição de tooend final dos recursos de rede no monitoramento de recursos de rede do contraste tooindividual.

-   [Monitoramento de recursos](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-resource-level-monitoring) – o monitoramento no nível do recurso é composto por quatro recursos: logs de diagnóstico, métricas, solução de problemas e integridade de recursos. Todos esses recursos são criados no nível de recursos de rede hello.

![Logs de rede do Azure](./media/azure-log-audit/azure-log-audit-fig4.png)

Observador de rede é um serviço regional que permite que você toomonitor e diagnosticar as condições em uma rede cenário nível, para e do Azure. Diagnóstico de rede e as ferramentas de visualização disponíveis com o observador de rede ajudarão-lo a entender, diagnosticar e obter a rede de tooyour insights no Azure.

**Log de fluxo de NSG** -fluxo de logs para grupos de segurança de rede permitem que você toocapture logs tootraffic relacionados que são permitidas ou negadas pelas regras de segurança de saudação no grupo de saudação. Esses logs de fluxo são gravados no formato JSON e mostram saídas fluxos de entrada em uma base por regra, Olá fluxo de saudação do NIC se aplica, 5-tupla informações sobre o fluxo de saudação (protocolo IP de origem/destino, porta de origem/destino) e se hello tráfego foi permitido ou negado.

### <a name="network-security-group-flow-logging"></a>Log de fluxo do Grupo de Segurança de Rede

[Logs de fluxo de grupo de segurança de rede](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) são um recurso do observador de rede que permite que você tooview informações sobre o tráfego IP de entrada e saída por meio de um grupo de segurança de rede. Esses logs de fluxo são gravados no formato JSON e mostram saídas fluxos de entrada em uma base por regra, Olá fluxo de saudação do NIC se aplica, 5-tupla informações sobre o fluxo de saudação (protocolo IP de origem/destino, porta de origem/destino) e se hello tráfego foi permitido ou negado.

Enquanto o fluxo de logs de grupos de segurança de rede de destino, elas não são exibidas Olá mesmo como Olá outros logs. Os logs de fluxo são armazenados apenas em uma conta de armazenamento.

Olá mesmas políticas de retenção como visto em outros logs aplicam logs de tooflow. Logs de tem uma política de retenção pode ser definida de dias de too365 de 1 dia. Se uma política de retenção não for definida, Olá logs são mantidos indefinidamente.

**Logs de diagnóstico**

Eventos periódicos e espontâneas são criados pelos recursos de rede e registrados em contas de armazenamento, enviadas tooan Hub de eventos ou análise de Log. Esses logs fornecem informações sobre a integridade de saudação de um recurso. Esses logs podem ser visualizados em ferramentas como o Power BI e o Log Analytics. toolearn como logs de diagnóstico tooview, visite [análise de Log.](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-networking-analytics)

![Logs de diagnóstico](./media/azure-log-audit/azure-log-audit-fig5.png)

Os logs de diagnóstico estão disponíveis para o [Balanceador de Carga](https://docs.microsoft.com/azure/load-balancer/load-balancer-monitor-log), [Grupos de Segurança da Rede](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log), Rotas e o [Gateway de Aplicativo.](https://docs.microsoft.com/azure/application-gateway/application-gateway-diagnostics)

O Observador de Rede fornece uma exibição dos logs de diagnóstico. Essa exibição contém todos os recursos de rede que oferecem suporte ao log de diagnóstico. Nessa exibição, você pode habilitar e desabilitar os recursos de rede de modo rápido e prático.


No registro em log toopreceding de adição de recursos, o observador de rede atualmente tem Olá recursos a seguir:
- [Topologia](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-overview) -fornece uma saudação de mostrando de exibição de nível de rede vários interconexões e associações entre recursos de rede em um grupo de recursos.

- [Captura de Pacote Variável](https://docs.microsoft.com/azure/network-watcher/network-watcher-packet-capture-overview) – captura dados do pacote dentro e fora de uma máquina virtual. Filtragem opções avançadas e ajustados controles como sendo tooset capaz de limitações de tamanho e tempo fornecem dados de pacote versatility.hello podem ser armazenados em um repositório de blob ou no disco local do hello no formato. cap.

-   [Verificações do fluxo de IP](https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview) – verifica se um pacote é permitido ou negado com base nos parâmetros do pacote com cinco tuplas das informações do fluxo (IP de Destino, IP de Origem, Porta de Destino, Porta de Origem e Protocolo). Se o pacote de saudação é negado por um grupo de segurança, hello regra e o grupo negado de pacote de saudação é retornado.

-   [Próximo salto](https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview) -determina o próximo salto Olá para pacotes que está sendo direcionado no hello malha de rede do Azure, permitindo que você rotas toodiagnose qualquer configuradas incorretamente definido pelo usuário.

-   [Exibição de grupo de segurança](https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview) -obtém Olá segurança efetiva e aplicadas regras que são aplicadas em uma máquina virtual.

-   [Gateway de rede virtual e solução de problemas de Conexão](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest) -fornece Olá capacidade tootroubleshoot Gateways de rede Virtual e conexões.

-   [Limites de assinatura de rede](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-subscription-limits) -permite o uso de recursos de rede tooview em limites de.

### <a name="application-insight"></a>Application Insights

O [Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-overview) é um serviço APM (Gerenciamento de Desempenho de Aplicativos) extensível para desenvolvedores da Web em várias plataformas. Use-toomonitor seu aplicativo web em tempo real. Ele detecta anomalias de desempenho automaticamente. Ele inclui uma análise rigorosa ferramentas toohelp que diagnosticar problemas e toounderstand que os usuários, na verdade, fazem com seu aplicativo.

 Ele é projetado toohelp você continuamente melhorar o desempenho e usabilidade.

 Ele funciona para aplicativos em uma ampla variedade de plataformas, incluindo .NET, Node.js e J2EE, hospedado no local ou na nuvem hello. Ele se integra ao seu processo de devOps e tem as ferramentas de desenvolvimento de toovarious de pontos de conexão.

![Application Insights](./media/azure-log-audit/azure-log-audit-fig6.png)

Informações do aplicativo é destinado a equipe de desenvolvimento hello, toohelp você entender o desempenho do seu aplicativo e como ele está sendo usado. Ele monitora:

-   **Taxas de solicitação, tempos de resposta e taxas de falha** - descubra quais páginas estão mais populares, em que momentos do dia, e onde os usuários estão. Confira as páginas que têm melhor desempenho. Se as taxas de falha e os tempos de resposta ficam altos quando há mais solicitações, possivelmente você tem um problema de alocação de recursos.

-   **Taxas de dependência, tempos de resposta e taxas de falha** - descubra se os serviços externos estão atrasando você.

-   **Exceções** - analisar estatísticas agregada de saudação, ou selecionar instâncias específicas e analisar o rastreamento de pilha hello e solicitações relacionadas. A maioria das exceções de navegador e servidor são relatadas.

-   **Exibições de página e o desempenho de carregamento** - relatados por navegadores dos usuários.

-   **Chamadas AJAX** de páginas da web - taxas, tempos de resposta e taxas de falha.

-   **Contagens de seção e usuários**.

-   **Contadores de desempenho** de suas máquinas de servidor Linux ou Windows server, como CPU, memória e uso da rede.

-   **Diagnósticos de host** do Docker ou do Azure.

-   **Logs de rastreamento de diagnóstico** do seu aplicativo - para que você possa correlacionar eventos de rastreamento com solicitações.

-   **Eventos personalizados e métricas** que você escreva por conta própria no código de cliente ou servidor hello, tootrack eventos de negócios, como itens vendidos ou jogos ganha.

**Lista de cenários de integração e descrição:**

| Cenários de integração | Descrição |
| --------------------- | :---------- |
|[Mapa do aplicativo](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-app-map)|componentes de saudação do seu aplicativo, com as principais métricas e alertas.||
|[Pesquisa de diagnóstico para dados da instância](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-diagnostic-search)| pesquise e filtre eventos como solicitações, exceções, chamadas de dependência, rastreamentos de log e exibições de página.||
|[Metrics Explorer para dados agregados](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-metrics-explorer)|explore, filtre e segmente dados agregados, como taxas de solicitações, falhas e exceções; tempos de resposta e tempos de carregamento de página.||
|[Painéis](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-dashboards#dashboards)|faça um mashup de dados de vários recursos e compartilhe com outras pessoas. Excelente para aplicativos de vários componentes e para a exibição contínua em sala de equipe hello.||
|[Live Metrics Stream](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-live-stream)|Quando você implanta uma nova compilação, assista a esses toomake de indicadores de desempenho em tempo quase real se tudo está funcionando conforme o esperado.||
|[Analytics](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics)|responda perguntas difíceis sobre o desempenho e o uso do seu aplicativo usando essa poderosa linguagem de consulta.||
|[Alertas automáticos e manuais](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-alerts)|Alertas automáticos adaptar padrões normais de tooyour do aplicativo de telemetria e o gatilho quando há algo fora saudação padrão. Você também pode definir alertas em níveis específicos de métricas padrão ou personalizadas.||
|[Visual Studio](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-visual-studio)|Ver os dados de desempenho no código de saudação. Vá toocode de rastreamentos de pilha.||
|[Power BI](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-export-power-bi)|Integre as métricas de uso com outro business intelligence.||
|[API REST](https://dev.applicationinsights.io/)|Escreva código toorun consultas sobre o métricas e os dados brutos.||
|[Exportação contínua](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-export-telemetry)|Exportação em massa de dados brutos toostorage quando elas chegam.||

### <a name="azure-security-center-alerts"></a>Alertas da Central de Segurança do Azure
[Central de segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) automaticamente coleta, analisa e integra dados de log de seus recursos do Azure, rede hello e soluções de parceiros conectados, como soluções de proteção de firewall e de ponto de extremidade, ameaças reais toodetect e reduzir falsos positivos. É mostrada uma lista de alertas de segurança priorizados na Central de segurança junto com hello informações que você precisa tooquickly investigar o problema hello e recomendações sobre como tooremediate um ataque.

Detecção de ameaças de segurança central funciona automaticamente Coletando informações de segurança de seus recursos do Azure, rede hello e soluções de parceiros conectado. Ele analisa essas informações, geralmente correlacionando informações de várias fontes, tooidentify ameaças. Alertas de segurança são priorizados na Central de segurança, juntamente com recomendações sobre como tooremediate Olá ameaça.

![Central de Segurança do Azure](./media/azure-log-audit/azure-log-audit-fig7.png)

A Central de Segurança emprega análise de segurança avançada, que vai além das abordagens baseadas em assinatura. Soluções de dados grandes e [aprendizado de máquina](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/) tecnologias são aplicadas tooevaluate eventos em malha de nuvem inteira hello – detecção de ameaças que seriam impossível tooidentify usando abordagens manuais e prevendo Olá evolução de ataques. Essas análises de segurança incluem:

-   **Integrado a inteligência de ameaça:** parece para conhecidos atores ruins, aplicando a inteligência de ameaça global de produtos e serviços, Microsoft hello Microsoft Digital Crimes unidade (DCU), Olá Microsoft Security Response Center (MSRC) e externas feeds.

-   **Análise de comportamento:** aplica os comportamentos mal-intencionados de toodiscover padrões conhecidos.

-   **Detecção de anomalias:** usa estatísticas de criação de perfil toobuild uma linha de base histórica. Ele o alertará sobre desvios das linhas de base estabelecidas em conformidade com o vetor de ataque potencial tooa.


Muitas operações de segurança e as equipes de resposta a incidentes se baseiam em uma solução de gerenciamento de eventos (SIEM) e informações de segurança Olá ponto de partida para separação e investigando os alertas de segurança. Com a integração de log do Azure, os clientes podem sincronizar alertas da Central de Segurança e eventos de segurança da máquina virtual, coletados pelo Diagnóstico do Azure e pelos Logs de Auditoria do Azure, com suas soluções de análise de log e SIEM quase em tempo real.


## <a name="log-analytics"></a>Log Analytics

O Log Analytics é um serviço do [OMS (Operations Management Suite)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) que ajuda a coletar e analisar dados gerados pelos recursos em seus ambientes local e de nuvem. Ele fornece informações em tempo real usando a pesquisa integrada e painéis personalizados tooreadily analisar milhões de registros em todas as suas cargas de trabalho e servidores, independentemente de sua localização física.

![Log Analytics](./media/azure-log-audit/azure-log-audit-fig8.png)

Em Olá center de análise de Log é repositório do OMS hello, que está hospedado na nuvem do Azure de saudação. Dados são coletados no repositório de saudação de fontes conectadas por configurar fontes de dados e Adicionar assinatura tooyour de soluções. Soluções e fontes de dados irá criar diferentes tipos de registro que têm seu próprio conjunto de propriedades, mas ainda podem ser analisados no repositório de toohello de consultas. Isso permite que você toouse Olá mesmo toowork de ferramentas e os métodos com diferentes tipos de dados coletado por fontes diferentes.

Fontes conectadas são computadores hello e outros recursos que geram dados coletados pela análise de Log. Isso pode incluir os agentes instalados em computadores [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-windows-agents) e [Linux](https://docs.microsoft.com/azure/log-analytics/log-analytics-linux-agents) que se conectam diretamente ou agentes em um [grupo de gerenciamento conectado do System Center Operations Manager.](https://docs.microsoft.com/azure/log-analytics/log-analytics-om-agents) O Log Analytics também pode coletar dados do [armazenamento do Azure.](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-storage)

[Fontes de dados](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources) são Olá diferentes tipos de dados coletados de cada origem conectada. Isso inclui eventos e [dados de desempenho](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-performance-counters) de [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events) e agentes do Linux na adição toosources como [logs do IIS](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-iis-logs), e [logs de texto personalizado.](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-custom-logs) Configurar cada fonte de dados que você deseja toocollect, e a configuração de saudação é origem conectada tooeach entregue automaticamente.

Há quatro maneiras diferentes de [coletar logs e métricas para os serviços do Azure:](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-storage)
1.  Diagnóstico do Azure direcionar tooLog Analytics (diagnóstico em Olá a tabela a seguir)

2.  Diagnóstico do Azure tooAzure armazenamento tooLog Analytics (armazenamento em Olá a tabela a seguir)

3.  Conectores para os serviços do Azure (conectores no Olá a tabela a seguir)

4.  Scripts de toocollect e, em seguida, os dados de postagem em análise de Log (espaços em branco em Olá a tabela a seguir e serviços que não estão listados)

| O Barramento de | Tipo de recurso | Logs | Métricas | Solução |
| :------ | :------------ | :--- | :------ | :------- |
|Application gateways|  Microsoft.Network/<br>applicationGateways|  Diagnostics|Diagnostics|    [Análise de Gateway de](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-networking-analytics#azure-application-gateway-analytics-solution-in-log-analytics) [Aplicativo do Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-networking-analytics#azure-application-gateway-analytics-solution-in-log-analytics)|
|Application insights||     Conector|  Conector|  [Conector do Application](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/) [Insights (Visualização)](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/)|
|Contas de automação|   Microsoft.Automation/<br>AutomationAccounts|    Diagnostics||       [Mais informações](https://docs.microsoft.com/en-us/azure/automation/automation-manage-send-joblogs-log-analytics)|
|Contas do Lote|    Microsoft.Batch/<br>batchAccounts|  Diagnostics|    Diagnostics||
|Serviços de Nuvem clássicos||       Armazenamento||       [Mais informações](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-storage-iis-table)|
|Serviços cognitivos|    Microsoft.CognitiveServices/<br>accounts|       Diagnostics|||
|Data Lake Analytics|   Microsoft.DataLakeAnalytics/<br>accounts|   Diagnostics|||
|Data Lake Store|   Microsoft.DataLakeStore/<br>accounts|   Diagnostics|||
|Namespace do Hub de Eventos|   Microsoft.EventHub/<br>namespaces|  Diagnostics|    Diagnostics||
|Hubs IoT|  Microsoft.Devices/<br>IotHubs||     Diagnostics||
|Cofre da Chave| Microsoft.KeyVault/<br>vaults|  Diagnostics  || [KeyVault Analytics](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-key-vault)|
|Balanceadores de Carga|    Microsoft.Network/<br>loadBalancers|    Diagnostics|||
|Aplicativos Lógicos|    Microsoft.Logic/<br>workflows|  Diagnostics|    Diagnostics||
||Microsoft.Logic/<br>integrationAccounts||||
|Grupos de segurança de rede|   Microsoft.Network/<br>networksecuritygroups|Diagnostics||   [Análise de Grupo de Segurança de Rede do Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-networking-analytics#azure-network-security-group-analytics-solution-in-log-analytics)|
|Cofres de recuperação|   Microsoft.RecoveryServices/<br>vaults|||[Análise dos Serviços de Recuperação do Azure (Visualização)](https://github.com/krnese/AzureDeploy/blob/master/OMS/MSOMS/Solutions/recoveryservices/)|
|Serviços de pesquisa|   Microsoft.Search/<br>searchServices|    Diagnostics|    Diagnostics||
|Namespace do Barramento de Serviço| Microsoft.ServiceBus/<br>namespaces|    Diagnostics|Diagnostics|    [Análise do Barramento de Serviço (Visualização)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-servicebus-solution)|
|Service Fabric||       Armazenamento||    [Análise do Service Fabric (visualização)](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-service-fabric)|
|SQL (v12)| Microsoft.Sql/<br>servers/<br>databases||       Diagnostics||
||Microsoft.Sql/<br>servers/<br>elasticPools||||
|Armazenamento|||         Script| [Análise do Azure Storage (Visualização)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-azure-storage-analytics-solution)|
|Máquinas Virtuais|  Microsoft.Compute/<br>virtualMachines|  Extensão|  Extensão||
||||Diagnostics||
|Conjuntos de dimensionamento de Máquinas Virtuais|   Microsoft.Compute/<br>virtualMachines    ||Diagnostics||
||Microsoft.Compute/<br>virtualMachineScaleSets/<br>virtualMachines||||
|Farms do servidor Web|Microsoft.Web/<br>serverfarms||   Diagnostics
|Sites| Microsoft.Web/<br>sites ||      Diagnostics|    [Mais informações](https://github.com/Azure/azure-quickstart-templates/tree/master/101-webappazure-oms-monitoring)|
||Microsoft.Web/<br>sites/<br>slots|||||


## <a name="log-integration-with-on-premises-siem-systems"></a>Integração de log com sistemas SIEM locais
[Integração do Azure log](https://www.microsoft.com/download/details.aspx?id=53324) permite que você os logs de bruto toointegrate de seus recursos do Azure no local do tooyour **sistemas de gerenciamento de eventos (SIEM) e informações de segurança**.

![Integração de log](./media/azure-log-audit/azure-log-audit-fig9.png)

A integração de log do Azure coleta o Diagnóstico do Azure das máquinas virtuais do Windows (WAD), dos Logs de Atividades do Azure, dos alertas da Central de Segurança do Azure e dos logs do Provedor de Recursos do Azure. Essa integração oferece um painel unificado para todos os seus ativos, local ou na nuvem hello, para que você pode agregar, correlacionar, analisar e alertas para eventos de segurança.



Atualmente, a integração de log do Azure dá suporte à integração de Logs de Atividades do Azure, do log de Eventos do Windows de máquinas virtuais Windows em sua assinatura do Azure, de alertas da Central de Segurança do Azure, de logs de Diagnóstico do Azure e logs de auditoria do Azure Active Directory.

| Tipo de log | Log Analytics que dá suporte a JSON (Splunk, ArcSight, Qradar) |
| :------- | :-------------------------------------------------------- |
|Logs de auditoria do AAD|    sim|
|Logs de atividade| Sim|
|Alertas do ASC |Sim|
|Logs de diagnóstico (logs de recurso)|  Sim|
|Logs da VM|   Sim, por meio de eventos encaminhados e não por meio do JSON|


Olá tabela a seguir explica categoria do Log hello e detalhes de integração do SIEM.

[Introdução à integração de log do Azure](https://docs.microsoft.com/azure/security/security-azure-log-integration-get-started) – esse tutorial explica as etapas de instalação da integração de log do Azure, bem como a integração de logs do armazenamento WAD do Azure, Logs de Atividades do Azure, alertas da Central de Segurança do Azure e logs de auditoria do Azure Active Directory.

Cenários de integração

-   [Etapas de configuração de parceiro](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) – esta postagem de blog mostra como tooconfigure Azure log toowork integração com soluções de parceiros Splunk, HP ArcSight e IBM QRadar.

-   [Perguntas frequentes sobre o log de integração do Azure](https://docs.microsoft.com/azure/security/security-azure-log-integration-faq) – encontre as respostas para as perguntas frequentes sobre a integração de log do Azure.

-   [Integração Central de segurança do log de alertas com o Azure Integration](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration) – este documento mostra como alertas da Central de segurança toosync, juntamente com coletados pelo diagnóstico do Azure e os Logs de auditoria do Azure, com a análise de log de eventos de segurança de máquina virtual ou Solução SIEM.

## <a name="next-steps"></a>Próximas etapas

- [Auditoria e log](https://www.microsoft.com/trustcenter/security/auditingandlogging)

Proteger dados, mantendo a visibilidade e responder rapidamente tootimely alertas de segurança

- [Log de segurança e coleta de logs de auditoria no Azure](https://azure.microsoft.com/resources/videos/security-logging-and-audit-log-collection/)

Quais configurações você precisa tooenforce toomake-se de que suas instâncias do Azure estão coletando Olá segurança correto e os logs de auditoria.

- [Definir as configurações de auditoria de um conjunto de sites](https://support.office.com/article/Configure-audit-settings-for-a-site-collection-A9920C97-38C0-44F2-8BCB-4CF1E2AE22D2?ui=&rs=&ad=US)

Como um administrador de conjunto de sites, um pode recuperar o histórico de saudação das ações executadas por um usuário específico e também pode recuperar o histórico de saudação das ações executadas durante um determinado intervalo de datas. 

- [Log de auditoria de saudação de pesquisa no Centro de conformidade e Olá segurança do Office 365](https://support.office.com/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c?ui=&rs=&ad=US)

Você pode usar o hello Centro de conformidade e segurança do Office 365 toosearch Olá auditoria unificada log tooview usuário e atividade do administrador em sua organização do Office 365.


