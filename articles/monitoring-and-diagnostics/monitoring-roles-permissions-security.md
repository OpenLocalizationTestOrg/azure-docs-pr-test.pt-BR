---
title: "aaaGet iniciado com funções, permissões e segurança com o Monitor do Azure | Microsoft Docs"
description: "Saiba como do Monitor do Azure toouse funções internas e permissões toorestrict acessam os recursos de toomonitoring."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 2686e53b-72f0-4312-bcd3-3dc1b4a9b912
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: johnkem
ms.openlocfilehash: 44fdf2a697050309480dfc164ebab51445b19bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-roles-permissions-and-security-with-azure-monitor"></a>Introdução às funções, permissões e segurança com o Azure Monitor
Muitas equipes necessário toostrictly regular o acesso toomonitoring dados e configurações. Por exemplo, se você tem os membros da equipe que trabalham exclusivamente no monitoramento (engenheiros de suporte, os engenheiros de devops) ou se você usar um provedor de serviço gerenciado, convém toogrant tooonly dados de monitoramento e restrinja sua capacidade toocreate a eles acesso, modificar, ou Exclua recursos. Este artigo mostra como tooquickly aplicar um monitoramento RBAC função tooa usuário internas no Azure ou criar sua própria função personalizada para um usuário que precisa de permissões limitadas de monitoramentos. Também discute considerações de segurança para os recursos relacionados ao Monitor do Azure e como você pode limitar o acesso toohello dados que eles contêm.

## <a name="built-in-monitoring-roles"></a>Funções internas de monitoramento
Funções internas do Monitor do Azure são tooresources de acesso de limite toohelp projetado em uma assinatura, permitindo que os responsáveis pelo monitoramento de infraestrutura tooobtain e configurar dados Olá necessários. O Azure Monitor fornece duas funções integradas: um Leitor de monitoramento e um Colaborador de monitoramento.

### <a name="monitoring-reader"></a>Leitor de monitoramento
Pessoas atribuídas a função de leitor de monitoramento de saudação podem exibir todos os dados de monitoramentos em uma assinatura, mas não pode modificar qualquer recurso ou editar as configurações relacionadas toomonitoring recursos. Essa função é apropriada para usuários em uma organização, como engenheiros de suporte ou de operações, que precisam de toobe capaz de:

* Exibir painéis de monitoramentos no portal de saudação e criar seus próprios painéis de monitoramentos privados.
* Consulta de métricas usando Olá [API REST do Azure Monitor](https://msdn.microsoft.com/library/azure/dn931930.aspx), [cmdlets do PowerShell](insights-powershell-samples.md), ou [CLI de plataforma cruzada](insights-cli-samples.md).
* Consulta hello atividade de Log usando o portal de hello, API de REST do Monitor do Azure, cmdlets do PowerShell ou CLI de plataforma cruzada.
* Saudação de exibição [configurações de diagnóstico](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) para um recurso.
* Saudação de exibição [log perfil](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) para uma assinatura.
* Exibir as configurações de autoescala.
* Exibir as configurações e a atividade do alerta.
* Acessar os dados do Application Insights e exiba os dados na Análise de AI.
* Pesquisar dados de espaço de trabalho de análise de Log (OMS), incluindo dados de uso do espaço de trabalho de saudação.
* Exibir grupos de gerenciamento do Log Analytics (OMS).
* Recupere o esquema de saudação de pesquisa de análise de Log (OMS).
* Listar os pacotes de inteligência do Log Analytics (OMS).
* Recuperar e executar as pesquisas salvas do Log Analytics (OMS).
* Recupere a configuração de armazenamento da análise de Log (OMS) hello.

> [!NOTE]
> Essa função não dá acesso de leitura toolog dados que foi hub de eventos tooan transmitidos ou armazenados em uma conta de armazenamento. [Veja abaixo](#security-considerations-for-monitoring-data) para obter informações sobre como configurar recursos de toothese de acesso.
> 
> 

### <a name="monitoring-contributor"></a>Colaborador de monitoramento
Pessoas atribuídas Olá Colaborador de monitoramento de função pode exibir todos os dados de monitoramentos em uma assinatura e criar ou modificar as configurações de monitoramento, mas não é possível modificar todos os outros recursos. Essa função é um superconjunto da função de leitor de monitoramento de saudação e é apropriada para membros da equipe de monitoramento ou provedores de serviço gerenciado que, além de permissões de toohello acima, também precisam toobe capaz de uma organização:

* Publicra os painéis de monitoramentos como um painel compartilhado.
* Definir as [configurações de diagnóstico](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) para um recurso.*
* Saudação de conjunto [log perfil](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) para um subscription.*
* Definir as configurações e a atividade do alerta.
* Criar testes Web e componentes do Application Insights.
* Listar chaves de espaço de trabalho compartilhadas do Log Analytics (OMS).
* Ativar ou desativar os pacotes de inteligência do Log Analytics (OMS).
* Criar e excluir as pesquisas salvas do Log Analytics (OMS).
* Criar e excluir configuração de armazenamento da análise de Log (OMS) hello.

* usuário separadamente também deve receber permissão de ListKeys Olá destino recursos (armazenamento conta ou evento de namespace de hub) tooset um perfil de registro ou configuração de diagnóstico.

> [!NOTE]
> Essa função não dá acesso de leitura toolog dados que foi hub de eventos tooan transmitidos ou armazenados em uma conta de armazenamento. [Veja abaixo](#security-considerations-for-monitoring-data) para obter informações sobre como configurar recursos de toothese de acesso.
> 
> 

## <a name="monitoring-permissions-and-custom-rbac-roles"></a>Monitoramento de permissões e funções RBAC personalizadas
Se Olá acima funções internas não atenderem às necessidades de saudação da sua equipe, você pode [criar uma função personalizada de RBAC](../active-directory/role-based-access-control-custom-roles.md) com permissões mais granulares. Abaixo está Olá operações comuns de RBAC do Monitor do Azure e suas descrições.

| Operação | Descrição |
| --- | --- |
| Microsoft.Insights/AlertRules/[Read, Write, Delete] |Leitura/gravação/exclusão de regras de alerta. |
| Microsoft.Insights/AlertRules/Incidents/Read |Lista de incidentes (histórico de regra de alerta hello está sendo disparado) de regras de alerta. Isso só se aplica a toohello portal. |
| Microsoft.Insights/AutoscaleSettings/[Read, Write, Delete] |Leitura/gravação/exclusão de configurações de dimensionamento automático. |
| Microsoft.Insights/DiagnosticSettings/[Read, Write, Delete] |Leitura/gravação/exclusão de configurações de diagnóstico. |
| Microsoft.Insights/eventtypes/digestevents/Read |Essa permissão é necessária para os usuários que precisam acessar os Logs de tooActivity por meio do portal de saudação. |
| Microsoft.Insights/eventtypes/values/Read |Listar eventos do Log de atividades (eventos de gerenciamento) em um assinatura. Essa permissão é aplicável tooboth acesso programático e portal toohello Log de atividades. |
| Microsoft.Insights/LogDefinitions/Read |Essa permissão é necessária para os usuários que precisam acessar os Logs de tooActivity por meio do portal de saudação. |
| Microsoft.Insights/MetricDefinitions/Read |Ler definições de métricas (lista de tipos de métrica disponíveis para um recurso). |
| Microsoft.Insights/Metrics/Read |Ler as métricas para um recurso. |

> [!NOTE]
> Acesso tooalerts, configurações de diagnóstico e métricas para um recurso requer que o usuário Olá tem o tipo de recurso de toohello de acesso de leitura e o escopo do recurso. Criando ("gravação") um perfil de configuração ou o log de diagnóstico arquivos tooa armazenamento conta ou fluxos tooevent hubs requer Olá usuário tooalso ter permissão do ListKeys no recurso de destino hello.
> 
> 

Por exemplo, usando Olá acima da tabela você pode criar uma função RBAC personalizada para um "leitor de Log de atividade" assim:

```powershell
$role = Get-AzureRmRoleDefinition "Reader"
$role.Id = $null
$role.Name = "Activity Log Reader"
$role.Description = "Can view activity logs."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Insights/eventtypes/*")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/mySubscription")
New-AzureRmRoleDefinition -Role $role 
```

## <a name="security-considerations-for-monitoring-data"></a>Considerações de segurança para dados de monitoramento
Dados de monitoramento — especialmente os arquivos de log — podem conter informações confidenciais, como endereços IP ou nomes de usuário. Os dados de monitoramento do Azure vêm em três formas básicas:

1. Hello atividade de Log, que descreve todas as ações do plano de controle em sua assinatura do Azure.
2. Logs de diagnóstico, que são logs emitidos por um recurso.
3. Métricas, que são emitidas pelos recursos.

Três desses tipos de dados podem ser armazenados em uma conta de armazenamento ou tooEvent Hub, que são recursos do Azure para fins gerais de streaming. Como esses são recursos de finalidade geral, criar, excluir e acessá-los são operações privilegiadas, normalmente reservadas para o administrador. Sugerimos que você use Olá seguir práticas recomendadas para o uso indevido de tooprevent relacionados ao monitoramento de recursos:

* Use uma conta de armazenamento única e dedicada para os dados de monitoramento. Se você precisar tooseparate dados de monitoramento em várias contas de armazenamento, nunca compartilham o uso de uma conta de armazenamento entre o monitoramento e aqueles que só precisam acessar os dados de toomonitoring (por exemplo, inadvertidamente podem resultar em dados não de monitoramento, como isso um terceiro SIEM) acessar dados de monitoramento de toonon.
* Use um namespace de barramento de serviço ou Hub de evento único e dedicado em todas as configurações de diagnósticas para Olá pelo mesmo motivo como acima.
* Limitar as contas de acesso de armazenamento relacionada toomonitoring ou hubs de eventos ao mantê-las em um grupo de recursos separado, e [usar escopo](../active-directory/role-based-access-control-what-is.md#basics-of-access-management-in-azure) em suas funções de monitoramentos toolimit acessar tooonly nesse grupo de recursos.
* Nunca conceda permissão do ListKeys Olá para contas de armazenamento ou hubs de eventos no escopo de assinatura quando um usuário só precisa acessar toomonitoring dados. Em vez disso, conceder essas permissões toohello do usuário em um recurso ou grupo de recursos (se você tiver um grupo de recursos de monitoramento dedicado) escopo.

### <a name="limiting-access-toomonitoring-related-storage-accounts"></a>Limitar as contas de acesso de armazenamento relacionada toomonitoring
Quando um usuário ou aplicativo precisa acessar dados de toomonitoring em uma conta de armazenamento, você deve [gerar uma SAS da conta](https://msdn.microsoft.com/library/azure/mt584140.aspx) na conta de armazenamento Olá que contém dados de monitoramento com o armazenamento de tooblob acesso somente leitura de nível de serviço. No PowerShell, isso pode ser semelhante a:

```powershell
$context = New-AzureStorageContext -ConnectionString "[connection string for your monitoring Storage Account]"
$token = New-AzureStorageAccountSASToken -ResourceType Service -Service Blob -Permission "rl" -Context $context
```

Em seguida, você pode dar a entidade do token toohello Olá que precisa tooread dessa conta de armazenamento, e pode listar e ler todos os blobs na conta de armazenamento.

Como alternativa, se você precisar toocontrol essa permissão com RBAC, você pode conceder esse Olá entidade Microsoft.Storage/storageAccounts/listkeys/action permissão na conta de armazenamento específico. Isso é necessário para usuários que precisam toobe capaz de tooset um diagnóstico log ou configuração de perfil tooarchive tooa conta de armazenamento. Por exemplo, você poderia criar hello função RBAC personalizada para um usuário ou aplicativo que precisa apenas tooread de uma conta de armazenamento a seguir:

```powershell
$role = Get-AzureRmRoleDefinition "Reader"
$role.Id = $null
$role.Name = "Monitoring Storage Account Reader"
$role.Description = "Can get hello storage account keys for a monitoring storage account."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Storage/storageAccounts/listkeys/action")
$role.Actions.Add("Microsoft.Storage/storageAccounts/Read")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/mySubscription/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/myMonitoringStorageAccount")
New-AzureRmRoleDefinition -Role $role 
```

> [!WARNING]
> Olá permissão do ListKeys permite que chaves de conta de armazenamento primário e secundário Olá usuário toolist hello. Essas chaves conceder usuário Olá tudo assinado permissões (leitura, gravação, criar blobs, excluir blobs, etc.) em todos os serviços (blob, fila, tabela, arquivo) na conta de armazenamento de assinatura. Recomendamos usar uma SAS da conta descrita acima, quando possível.
> 
> 

### <a name="limiting-access-toomonitoring-related-event-hubs"></a>Limitando a hubs de eventos relacionados a toomonitoring de acesso
Um padrão semelhante pode ser seguido com hubs de eventos, mas primeiro você precisa toocreate uma regra de autorização de escuta dedicada. Se você quiser toogrant acesso tooan aplicativo que só precisa de hubs de evento relacionado à toomonitoring toolisten, Olá a seguir:

1. Crie uma política de acesso compartilhado em hubs de evento Olá que foram criadas para o fluxo de dados de monitoramentos com apenas declarações de escuta. Isso pode ser feito no portal de saudação. Por exemplo, você pode chamá-la de "monitoringReadOnly." Se possível, você desejará toogive que toohello consumidor diretamente da chave e ignorar Olá próxima etapa.
2. Se o consumidor Olá precisar toobe tooget capaz de saudação chave ad hoc, conceda ação do ListKeys saudação do hello usuário hub de evento. Isso também é necessário para usuários que precisam toobe capaz de tooset uma configuração de diagnóstica ou de log hubs do perfil toostream tooevent. Por exemplo, você pode criar uma regra RBAC:
   
   ```powershell
   $role = Get-AzureRmRoleDefinition "Reader"
   $role.Id = $null
   $role.Name = "Monitoring Event Hub Listener"
   $role.Description = "Can get hello key toolisten tooan event hub streaming monitoring data."
   $role.Actions.Clear()
   $role.Actions.Add("Microsoft.ServiceBus/namespaces/authorizationrules/listkeys/action")
   $role.Actions.Add("Microsoft.ServiceBus/namespaces/Read")
   $role.AssignableScopes.Clear()
   $role.AssignableScopes.Add("/subscriptions/mySubscription/resourceGroups/myResourceGroup/providers/Microsoft.ServiceBus/namespaces/mySBNameSpace")
   New-AzureRmRoleDefinition -Role $role 
   ```

## <a name="next-steps"></a>Próximas etapas
* [Leia sobre RBAC e permissões no Gerenciador de Recursos](../active-directory/role-based-access-control-what-is.md)
* [Visão geral de saudação de leitura de monitoramento no Azure](monitoring-overview.md)

