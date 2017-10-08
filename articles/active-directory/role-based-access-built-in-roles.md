---
title: "aaaActions e NotActions - Azure baseado em função (RBAC) de controle de acesso | Microsoft Docs"
description: "Este tópico descreve Olá criado nas funções de controle de acesso baseado em função (RBAC). funções Hello são adicionadas continuamente, portanto seleção Olá documentação atualização."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: 
ms.assetid: b547c5a5-2da2-4372-9938-481cb962d2d6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/28/2017
ms.author: andredm
ms.reviewer: 
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0a4ef9923fe05ec38e968534951911eaa4440b88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="built-in-roles-for-azure-role-based-access-control"></a>Funções internas para o controle de acesso baseado em função do Azure
Controle de acesso do Azure baseado em função (RBAC) vem com hello funções internas que podem ser atribuídas toousers, grupos e serviços a seguir. Você não pode modificar as definições de saudação de funções internas. No entanto, você pode criar [funções personalizadas no Azure RBAC](role-based-access-control-custom-roles.md) toofit Olá necessidades da sua organização.

## <a name="roles-in-azure"></a>Funções no Azure
Olá tabela a seguir fornece descrições breves de saudação funções internas. Clique em Olá função nome toosee Olá lista detalhada de **ações** e **notactions** para função hello. Olá **ações** propriedade especifica Olá ações permitida em recursos do Azure. As cadeias de caracteres da ação podem usar caracteres curingas. Olá **notactions** propriedade especifica as ações de saudação que são excluídas da saudação ações permitida.

ação de saudação define o tipo das operações que você pode executar em um tipo de recurso específico. Por exemplo:
- **Gravar** permite que você tooperform PUT, POST, PATCH e operações de exclusão.
- **Leitura** permite operações GET de tooperform.

Este artigo aborda apenas funções diferentes de saudação que existem hoje. Quando você atribuir uma função tooa usuário, no entanto, você pode limitar Olá permitido ações adicionais ao definir um escopo. Isso é útil se você quiser toomake alguém um colaborador de site, mas apenas para um grupo de recursos.

> [!NOTE]
> definições de função do Azure Olá estão em constante evolução. Este artigo é mantido como backup toodate possível, mas você sempre pode encontrar as definições de funções mais recentes de saudação no Azure PowerShell. Saudação de uso [Get-AzureRmRoleDefinition](/powershell/module/azurerm.resources/get-azurermroledefinition) toolist cmdlet todas as funções atuais. Aprofunde-se no uso da função específica de tooa `(get-azurermroledefinition "<role name>").actions` ou `(get-azurermroledefinition "<role name>").notactions` conforme aplicável. Use [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) operações toolist de provedores de recursos do Azure específico.


| Nome da função | Descrição |
| --- | --- |
| [Colaborador de serviço de gerenciamento de API](#api-management-service-contributor) |Pode gerenciar o serviço de gerenciamento de API e hello APIs |
| [Função do operador de serviço de gerenciamento da API](#api-management-service-operator-role) | Pode gerenciar o serviço de gerenciamento de API, mas não Olá APIs próprios |
| [Função do leitor do serviço de gerenciamento da API](#api-management-service-reader-role) | Serviço de gerenciamento do acesso somente leitura tooAPI e APIs |
| [Colaborador de componente do Application Insights](#application-insights-component-contributor) |Pode gerenciar os componentes do Application Insights |
| [Operador de automação](#automation-operator) |Capaz de toostart, parar, suspender e reiniciar trabalhos |
| [Colaborador de Backup](#backup-contributor) | Pode gerenciar o backup no cofre dos Serviços de Recuperação |
| [Operador de Backup](#backup-operator) | Pode gerenciar o backup, exceto a remoção de backup, no cofre dos Serviços de Recuperação |
| [Leitor de Backup](#backup-reader) | Pode exibir todos os serviços de gerenciamento de backup  |
| [Leitor de cobrança](#billing-reader) | Pode exibir todas as informações de cobranças  |
| [Colaborador do BizTalk](#biztalk-contributor) |Pode gerenciar os serviços BizTalk |
| [Colaborador do DB MySQL ClearDB](#cleardb-mysql-db-contributor) |Pode gerenciar bancos de dados MySQL ClearDB |
| [Colaborador](#contributor) |Pode gerenciar tudo, exceto o acesso. |
| [Colaborador da fábrica de dados](#data-factory-contributor) |Pode criar e gerenciar data factories e recursos filho dentro deles. |
| [Usuário do DevTest Labs](#devtest-labs-user) |Pode exibir tudo e se conectar a máquinas virtuais, iniciá-las, reiniciá-las e desligá-las. |
| [Colaborador de zona DNS](#dns-zone-contributor) |Pode gerenciar zonas e registros DNS |
| [Colaborador de conta do Azure Cosmos DB](#documentdb-account-contributor) |Pode gerenciar contas do Azure Cosmos DB |
| [Colaborador de conta do sistemas inteligentes](#intelligent-systems-account-contributor) |Pode gerenciar contas do Intelligent Systems |
| Colaborador de aplicativo lógico | Pode gerenciar todos os aspectos de um aplicativo lógico, mas não pode criar um novo. |
| Operador de aplicativo lógico |Pode iniciar e parar fluxos de trabalho definidos dentro de um aplicativo lógico. |
| [Leitor de monitoramento](#monitoring-reader) |Pode ler todos os dados de monitoramento |
| [Colaborador de monitoramento](#monitoring-contributor) |Pode ler dados de monitoramento e editar configurações de monitoramento |
| [Colaborador de rede](#network-contributor) |Pode gerenciar todos os recursos de rede |
| [Colaborador de Conta APM do New Relic](#new-relic-apm-account-contributor) |Pode gerenciar contas e aplicativos de Gerenciamento de Desempenho do Aplicativo New Relic |
| [Proprietário](#owner) |Pode gerenciar tudo, incluindo o acesso |
| [Leitor](#reader) |Pode ver tudo, mas não pode fazer alterações |
| [Colaborador do Cache Redis](#redis-cache-contributor) |Pode gerenciar caches Redis |
| [Colaborador de Coleções de Trabalho do Agendador](#scheduler-job-collections-contributor) |Pode gerenciar coleções de trabalhos do agendador |
| [Colaborador do Serviço de Pesquisa](#search-service-contributor) |Pode gerenciar serviços de pesquisa |
| [Gerenciador de Segurança](#security-manager) |Pode gerenciar componentes de segurança, políticas de segurança e máquinas virtuais |
| [Colaborador do Site Recovery](#site-recovery-contributor) | Pode gerenciar o Site Recovery no cofre dos Serviços de Recuperação |
| [Operador do Site Recovery](#site-recovery-operator) | Pode gerenciar operações de failover e failback do Site Recovery no cofre dos Serviços de Recuperação |
| [Leitor do Site Recovery](#site-recovery-reader) | Pode exibir todas as operações de gerenciamento do Site Recovery  |
| [Colaborador do banco de dados SQL](#sql-db-contributor) |Pode gerenciar bancos de dados SQL, mas não suas políticas relacionadas à segurança |
| [Gerenciador de Segurança do SQL](#sql-security-manager) |Pode gerenciar políticas de saudação relacionadas à segurança de servidores SQL e bancos de dados |
| [Colaborador do SQL Server](#sql-server-contributor) |Pode gerenciar bancos de dados e servidores SQL, mas não suas políticas relacionadas à segurança |
| [Colaborador da conta de armazenamento clássica](#classic-storage-account-contributor) |Pode gerenciar contas de armazenamento clássicas |
| [Colaborador da Conta de Armazenamento](#storage-account-contributor) |Pode gerenciar contas de armazenamento |
| [Colaborador de solicitação de suporte](#support-request-contributor) | Pode criar e gerenciar solicitações de suporte |
| [Administrador de Acesso do Usuário](#user-access-administrator) |Pode gerenciar os recursos de tooAzure de acesso do usuário |
| [Colaborador de Máquina Virtual Clássica](#classic-virtual-machine-contributor) |Pode gerenciar máquinas virtuais clássicas, mas a rede virtual não hello ou toowhich de conta de armazenamento que estão conectados |
| [Colaborador de Máquina Virtual](#virtual-machine-contributor) |Pode gerenciar máquinas virtuais, mas não Olá virtual rede ou armazenamento conta toowhich que estão conectados |
| [Colaborador de rede clássica](#classic-network-contributor) |Pode gerenciar redes virtuais clássicas e IPs reservados |
| [Colaborador do Plano de Web](#web-plan-contributor) |Pode gerenciar planos da Web |
| [Colaborador do Site](#website-contributor) |Pode gerenciar sites, mas não Olá web planos toowhich estão conectados |

## <a name="role-permissions"></a>Permissões de função
Olá, tabelas a seguir descrevem as permissões específicas de saudação tooeach função. Isso pode incluir **Ações** que concedem permissões e **Não Ações** que as restringem.

### <a name="api-management-service-contributor"></a>Colaborador de serviço de gerenciamento de API
Pode gerenciar os serviços de gerenciamento de API

| **Ações** |  |
| --- | --- |
| Microsoft.ApiManagement/Service/* |Criar e gerenciar o serviço de gerenciamento da API |
| Microsoft.Authorization/*/read |Ler autorização |
| Microsoft.Insights/alertRules/* |Criar e gerenciar regras de alerta |
| Microsoft.ResourceHealth/availabilityStatuses/read |Integridade de recursos de saudação de leitura |
| Microsoft.Resources/deployments/* |Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read |Ler funções e atribuições de função |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |

### <a name="api-management-service-operator-role"></a>Função do operador de serviço de gerenciamento da API
Pode gerenciar os serviços de gerenciamento de API

| **Ações** |  |
| --- | --- |
| Microsoft.ApiManagement/Service/*/read | Ler instâncias do serviço de gerenciamento da API |
| Microsoft.ApiManagement/Service/backup/action | Fazer backup de contêiner especificado do serviço de gerenciamento de API toohello em um conta de armazenamento de fornecida pelo usuário |
| Microsoft.ApiManagement/Service/delete | Excluir uma instância do Serviço de Gerenciamento de API |
| Microsoft.ApiManagement/Service/managedeployments/action | Alterar SKU/unidades; adicionar ou remover implantações regionais do Serviço de Gerenciamento de API |
| Microsoft.ApiManagement/Service/read | Ler metadados de uma instância do Serviço de Gerenciamento de API |
| Microsoft.ApiManagement/Service/restore/action | Restaurar o serviço de gerenciamento de API do contêiner de saudação especificado em um conta de armazenamento de fornecida pelo usuário |
| Microsoft.ApiManagement/Service/updatehostname/action | Configurar, atualizar ou remover nomes de domínio personalizado para um Serviço de Gerenciamento de API |
| Microsoft.ApiManagement/Service/write | Criar uma nova instância do Serviço de Gerenciamento de API |
| Microsoft.Authorization/*/read |Ler autorização |
| Microsoft.Insights/alertRules/* |Criar e gerenciar regras de alerta |
| Microsoft.ResourceHealth/availabilityStatuses/read |Integridade de recursos de saudação de leitura |
| Microsoft.Resources/deployments/* |Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read |Ler funções e atribuições de função |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |

### <a name="api-management-service-reader-role"></a>Função de leitor do Serviço de Gerenciamento de API
Pode gerenciar os serviços de gerenciamento de API

| **Ações** |  |
| --- | --- |
| Microsoft.ApiManagement/Service/*/read | Ler instâncias do serviço de gerenciamento da API |
| Microsoft.ApiManagement/Service/read | Ler metadados de uma instância do Serviço de Gerenciamento de API |
| Microsoft.Authorization/*/read |Ler autorização |
| Microsoft.Insights/alertRules/* |Criar e gerenciar regras de alerta |
| Microsoft.ResourceHealth/availabilityStatuses/read |Integridade de recursos de saudação de leitura |
| Microsoft.Resources/deployments/* |Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read |Ler funções e atribuições de função |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |

### <a name="application-insights-component-contributor"></a>Colaborador de componente do Application Insights
Pode gerenciar os componentes do Application Insights

| **Ações** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Ler funções e atribuições de função |
| Microsoft.Insights/alertRules/* |Criar e gerenciar regras de alerta |
| Microsoft.Insights/components/* |Criar e gerenciar componentes do Insights |
| Microsoft.Insights/webtests/* |Criar e gerenciar testes da Web |
| Microsoft.ResourceHealth/availabilityStatuses/read |Integridade de recursos de saudação de leitura |
| Microsoft.Resources/deployments/* |Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read |Ler grupos de recursos |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |

### <a name="automation-operator"></a>Operador de automação
Capaz de toostart, parar, suspender e reiniciar trabalhos

| **Ações** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Ler funções e atribuições de função |
| Microsoft.Automation/automationAccounts/jobs/read |Ler trabalhos de conta de automação |
| Microsoft.Automation/automationAccounts/jobs/resume/action |Reiniciar um trabalho de conta de automação |
| Microsoft.Automation/automationAccounts/jobs/stop/action |Interromper um trabalho de conta de automação |
| Microsoft.Automation/automationAccounts/jobs/streams/read |Ler fluxos de trabalho de conta de automação |
| Microsoft.Automation/automationAccounts/jobs/suspend/action |Suspender um trabalho de conta de automação |
| Microsoft.Automation/automationAccounts/jobs/write |Gravar trabalhos de conta de automação |
| Microsoft.Automation/automationAccounts/jobSchedules/read |Ler um plano de trabalho de conta de automação |
| Microsoft.Automation/automationAccounts/jobSchedules/write |Ler um plano de trabalho de conta de automação |
| Microsoft.Automation/automationAccounts/read |Ler contas de automação |
| Microsoft.Automation/automationAccounts/runbooks/read |Ler runbooks de automação |
| Microsoft.Automation/automationAccounts/schedules/read |Ler agendamentos de conta de automação |
| Microsoft.Automation/automationAccounts/schedules/write |Gravar agendamentos de conta de automação |
| Microsoft.Insights/components/* |Criar e gerenciar componentes do Insights |
| Microsoft.ResourceHealth/availabilityStatuses/read |Integridade de recursos de saudação de leitura |
| Microsoft.Resources/deployments/* |Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read |Ler grupos de recursos |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |

### <a name="backup-contributor"></a>Colaborador de Backup
Pode gerenciar todas as ações de gerenciamento de backup, exceto criar Cofre de serviços de recuperação e fornecendo acesso tooothers

| **Ações** | |
| --- | --- |
| Microsoft.Network/virtualNetworks/read | Ler redes virtuais |
| Microsoft.RecoveryServices/Vaults/backupFabrics/operationResults/* | Gerenciar os resultados da operação no gerenciamento de backup |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/* | Criar e gerenciar contêineres de backup em malhas de backup do cofre de Serviços de Recuperação |
| Microsoft.RecoveryServices/Vaults/backupJobs/* | Criar e gerenciar trabalhos de backup |
| Microsoft.RecoveryServices/Vaults/backupJobsExport/action | Exportar trabalhos de backup para uma planilha do Excel |
| Microsoft.RecoveryServices/Vaults/backupManagementMetaData/* | Criar e gerenciar os meta dados relacionados a gerenciamento de toobackup |
| Microsoft.RecoveryServices/Vaults/backupOperationResults/* | Criar e gerenciar os Resultados das operações de gerenciamento de backup |
| Microsoft.RecoveryServices/Vaults/backupPolicies/* | Criar e gerenciar políticas de backup |
| Microsoft.RecoveryServices/Vaults/backupProtectableItems/* | Criar e gerenciar itens para backup |
| Microsoft.RecoveryServices/Vaults/backupProtectedItems/* | Criar e gerenciar itens submetidos a backup |
| Microsoft.RecoveryServices/Vaults/backupProtectionContainers/* | Criar e gerenciar contêineres que armazenam itens de backup |
| Microsoft.RecoveryServices/Vaults/certificates/* | Criar e gerenciar certificados toobackup relacionados no cofre de serviços de recuperação |
| Microsoft.RecoveryServices/Vaults/extendedInformation/* | Criar e gerenciar informações estendidas relacionadas toovault |
| Microsoft.RecoveryServices/Vaults/read | Ler cofres dos Serviços de Recuperação |
| Microsoft.RecoveryServices/Vaults/refreshContainers/* | Gerenciar operações de descoberta para buscar contêineres recém-criados |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/* | Criar e gerenciar identidades registradas |
| Microsoft.RecoveryServices/Vaults/usages/* | Criar e gerenciar o uso do cofre dos Serviços de Recuperação |
| Microsoft.Resources/deployments/* | Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read | Ler grupos de recursos |
| Microsoft.Storage/storageAccounts/read | Ler contas de armazenamento |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |

### <a name="backup-operator"></a>Operador de Backup
Pode gerenciar todas as ações de gerenciamento de backup, exceto criar cofres, removendo o backup e fornecendo acesso tooothers

| **Ações** | |
| --- | --- |
| Microsoft.Network/virtualNetworks/read | Ler redes virtuais |
| Microsoft.RecoveryServices/Vaults/backupFabrics/operationResults/read | Ler resultados de operações de gerenciamento de backup |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/operationResults/read | Ler resultados de operações de proteção de contêineres |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/backup/action | Executar operações de backup sob demanda em um item submetido a backup |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/operationResults/read | Ler o resultado de operações executadas em itens submetidos a backup |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/operationStatus/read | Ler o status de operações executadas em itens submetidos a backup |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/read | Ler itens submetidos a backup |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/recoveryPoints/read | Ler o ponto de recuperação de um item submetido a backup |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/recoveryPoints/restore/action | Executar uma operação de restauração usando um ponto de recuperação de um item submetido a backup |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/write | Criar um item de backup |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/read | Ler contêineres que armazenam o item de backup |
| Microsoft.RecoveryServices/Vaults/backupJobs/* | Criar e gerenciar trabalhos de backup |
| Microsoft.RecoveryServices/Vaults/backupJobsExport/action | Exportar trabalhos de backup para uma planilha do Excel |
| Microsoft.RecoveryServices/Vaults/backupManagementMetaData/read | Leitura de metadados relacionados ao gerenciamento de toobackup |
| Microsoft.RecoveryServices/Vaults/backupOperationResults/* | Criar e gerenciar os Resultados das operações de gerenciamento de backup |
| Microsoft.RecoveryServices/Vaults/backupPolicies/operationResults/read | Ler resultados de operações executadas em políticas de backup |
| Microsoft.RecoveryServices/Vaults/backupPolicies/read | Ler políticas de backup |
| Microsoft.RecoveryServices/Vaults/backupProtectableItems/* | Criar e gerenciar itens para backup |
| Microsoft.RecoveryServices/Vaults/backupProtectedItems/read | Ler itens submetidos a backup |
| Microsoft.RecoveryServices/Vaults/backupProtectionContainers/read | Ler contêineres submetidos a backup que armazenam itens de backup |
| Microsoft.RecoveryServices/Vaults/extendedInformation/read | Informações de leitura estendida relacionados toovault |
| Microsoft.RecoveryServices/Vaults/extendedInformation/write | Informações de gravação estendida relacionados toovault |
| Microsoft.RecoveryServices/Vaults/read | Ler cofres dos Serviços de Recuperação |
| Microsoft.RecoveryServices/Vaults/refreshContainers/* | Gerenciar operações de descoberta para buscar contêineres recém-criados |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/operationResults/read | Resultados de leitura da operação executada nos itens registrados do cofre Olá |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/read | Ler itens registrados do cofre Olá |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/write | Gravar toovault itens registrados |
| Microsoft.RecoveryServices/Vaults/usages/read | Uso de saudação que Cofre de serviços de recuperação de leitura |
| Microsoft.Resources/deployments/* | Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read | Ler grupos de recursos |
| Microsoft.Storage/storageAccounts/read | Ler contas de armazenamento |
| Microsoft.Support/* | Criar e gerenciar tíquetes de suporte |

### <a name="backup-reader"></a>Leitor de Backup
Pode monitorar o gerenciamento de backup em um cofre de Serviços de Recuperação

| **Ações** | |
| --- | --- |
| Microsoft.RecoveryServices/Vaults/backupFabrics/operationResults/read  | Ler resultados de operações de gerenciamento de backup |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/operationResults/read  | Ler resultados de operações de proteção de contêineres |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/operationResults/read  | Ler o resultado de operações executadas em itens submetidos a backup |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/operationStatus/read  | Ler o status de operações executadas em itens submetidos a backup |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/read  | Ler itens submetidos a backup |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/read  | Ler contêineres que armazenam o item de backup |
| Microsoft.RecoveryServices/Vaults/backupJobs/operationResults/read  | Ler resultados de trabalhos de backup |
| Microsoft.RecoveryServices/Vaults/backupJobs/read  | Ler os trabalhos de backup |
| Microsoft.RecoveryServices/Vaults/backupJobsExport/action | Exportar trabalhos de backup para uma planilha do Excel |
| Microsoft.RecoveryServices/Vaults/backupManagementMetaData/read  | Leitura de metadados relacionados ao gerenciamento de toobackup |
| Microsoft.RecoveryServices/Vaults/backupOperationResults/read  | Ler resultados de operações de gerenciamento de backup |
| Microsoft.RecoveryServices/Vaults/backupPolicies/operationResults/read  | Ler resultados de operações executadas em políticas de backup |
| Microsoft.RecoveryServices/Vaults/backupPolicies/read  | Ler políticas de backup |
| Microsoft.RecoveryServices/Vaults/backupProtectedItems/read  |  Ler itens submetidos a backup |
| Microsoft.RecoveryServices/Vaults/backupProtectionContainers/read  | Ler contêineres submetidos a backup que armazenam itens de backup |
| Microsoft.RecoveryServices/Vaults/extendedInformation/read  | Informações de leitura estendida relacionados toovault |
| Microsoft.RecoveryServices/Vaults/read  | Ler cofres dos Serviços de Recuperação |
| Microsoft.RecoveryServices/Vaults/refreshContainers/read  | Ler o resultado de uma operação de descoberta para buscar contêineres recém-criados |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/operationResults/read  | Resultados de leitura da operação executada nos itens registrados do cofre Olá |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/read  | Ler itens registrados do cofre Olá |
| Microsoft.RecoveryServices/Vaults/usages/read  |  Uso de saudação que Cofre de serviços de recuperação de leitura |

### <a name="billing-reader"></a>Leitor de cobrança
Pode exibir todas as informações de Cobranças

| **Ações** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Ler funções e atribuições de função |
| Microsoft.Billing/*/read |Ler Informações de cobrança |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |

### <a name="biztalk-contributor"></a>Colaborador do BizTalk
Pode gerenciar os serviços BizTalk

| **Ações** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Ler funções e atribuições de função |
| Microsoft.BizTalkServices/BizTalk/* |Criar e gerenciar serviços BizTalk |
| Microsoft.Insights/alertRules/* |Criar e gerenciar regras de alerta |
| Microsoft.ResourceHealth/availabilityStatuses/read |Integridade de recursos de saudação de leitura |
| Microsoft.Resources/deployments/* |Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read |Ler grupos de recursos |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |

### <a name="cleardb-mysql-db-contributor"></a>Colaborador do DB MySQL ClearDB
Pode gerenciar bancos de dados MySQL ClearDB

| **Ações** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Ler funções e atribuições de função |
| Microsoft.Insights/alertRules/* |Criar e gerenciar regras de alerta |
| Microsoft.ResourceHealth/availabilityStatuses/read |Integridade de recursos de saudação de leitura |
| Microsoft.Resources/deployments/* |Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read |Ler grupos de recursos |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |
| successbricks.cleardb/Databases/* |Criar e gerenciar bancos de dados MySQL ClearDB |

### <a name="contributor"></a>Colaborador
Pode gerenciar tudo, exceto o acesso.

| **Ações** |  |
| --- | --- |
| * |Criar e gerenciar recursos de todos os tipos |

| **NotActions** |  |
| --- | --- |
| Microsoft.Authorization/*/Delete |Não é possível excluir funções e atribuições de função |
| Microsoft.Authorization/*/Write |Não é possível criar funções e atribuições de função |

### <a name="data-factory-contributor"></a>Colaborador da fábrica de dados
Criar e gerenciar data factories e recursos filho dentro deles.

| **Ações** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Ler funções e atribuições de função |
| Microsoft.DataFactory/dataFactories/* |Criar e gerenciar data factories e recursos filho dentro deles. |
| Microsoft.Insights/alertRules/* |Criar e gerenciar regras de alerta |
| Microsoft.ResourceHealth/availabilityStatuses/read |Integridade de recursos de saudação de leitura |
| Microsoft.Resources/deployments/* |Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read |Ler grupos de recursos |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |

### <a name="devtest-labs-user"></a>Usuário do DevTest Labs
Pode exibir tudo e se conectar a máquinas virtuais, iniciá-las, reiniciá-las e desligá-las.

| **Ações** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Ler funções e atribuições de função |
| Microsoft.Compute/availabilitySets/read |Ler propriedades de saudação de conjuntos de disponibilidade |
| Microsoft.Compute/virtualMachines/*/read |Ler propriedades de saudação de uma máquina virtual (tamanhos de VM, em tempo de execução, as extensões de VM, etc.) |
| Microsoft.Compute/virtualMachines/deallocate/action |Desalocar máquinas virtuais |
| Microsoft.Compute/virtualMachines/read |Saudação de ler propriedades de uma máquina virtual |
| Microsoft.Compute/virtualMachines/restart/action |Reiniciar máquinas virtuais |
| Microsoft.Compute/virtualMachines/start/action |Iniciar máquinas virtuais |
| Microsoft.DevTestLab/*/read |Ler propriedades de saudação de um laboratório |
| Microsoft.DevTestLab/labs/createEnvironment/action |Criar um ambiente de laboratório |
| Microsoft.DevTestLab/labs/formulas/delete |Excluir fórmulas |
| Microsoft.DevTestLab/labs/formulas/read |Ler fórmulas |
| Microsoft.DevTestLab/labs/formulas/write |Adicionar ou modificar fórmulas |
| Microsoft.DevTestLab/labs/policySets/evaluatePolicies/action |Avaliar políticas de laboratório |
| Microsoft.Network/loadBalancers/backendAddressPools/join/action |Unir um pool de endereços de back-end de balanceador de carga |
| Microsoft.Network/loadBalancers/inboundNatRules/join/action |Unir uma regra de NAT de entrada de balanceadores de carga |
| Microsoft.Network/networkInterfaces/*/read |Ler propriedades de saudação de uma interface de rede (por exemplo, todos os balanceadores de carga de saudação essa interface de rede Olá é parte de) |
| Microsoft.Network/networkInterfaces/join/action |Ingressar em uma interface de rede de tooa da máquina Virtual |
| Microsoft.Network/networkInterfaces/read |Ler interfaces de rede |
| Microsoft.Network/networkInterfaces/write |Gravar interfaces de rede |
| Microsoft.Network/publicIPAddresses/*/read |Ler propriedades de saudação de um endereço IP público |
| Microsoft.Network/publicIPAddresses/join/action |Unir um endereço IP público |
| Microsoft.Network/publicIPAddresses/read |Ler endereços IP públicos de rede |
| Microsoft.Network/virtualNetworks/subnets/join/action |Unir uma rede virtual |
| Microsoft.Resources/deployments/operations/read |Ler operações de implantação |
| Microsoft.Resources/deployments/read |Ler implantações |
| Microsoft.Resources/subscriptions/resourceGroups/read |Ler grupos de recursos |
| Microsoft.Storage/storageAccounts/listKeys/action |Listar chaves da conta de armazenamento |

### <a name="dns-zone-contributor"></a>Colaborador de zona DNS
Pode gerenciar zonas e registros DNS.

| **Ações** |  |
| --- | --- |
| Microsoft.Authorization/\*/read |Ler funções e atribuições de função |
| Microsoft.Insights/alertRules/\* |Criar e gerenciar regras de alerta |
| Microsoft.Network/dnsZones/\* |Criar e gerenciar zonas e registros DNS |
| Microsoft.ResourceHealth/availabilityStatuses/read |Leitura Olá integridade de recursos de saudação |
| Microsoft.Resources/deployments/\* |Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read |Ler grupos de recursos |
| Microsoft.Support/\* |Criar e gerenciar tíquetes de suporte |

### <a name="azure-cosmos-db-account-contributor"></a>Colaborador de conta do Azure Cosmos DB
Pode gerenciar contas do Azure Cosmos DB

| **Ações** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Ler funções e atribuições de função |
| Microsoft.DocumentDb/databaseAccounts/* |Criar e gerenciar contas do DocumentDB |
| Microsoft.Insights/alertRules/* |Criar e gerenciar regras de alerta |
| Microsoft.ResourceHealth/availabilityStatuses/read |Integridade de recursos de saudação de leitura |
| Microsoft.Resources/deployments/* |Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read |Ler grupos de recursos |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |

### <a name="intelligent-systems-account-contributor"></a>Colaborador de conta do sistemas inteligentes
Pode gerenciar contas do Intelligent Systems

| **Ações** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Ler funções e atribuições de função |
| Microsoft.Insights/alertRules/* |Criar e gerenciar regras de alerta |
| Microsoft.IntelligentSystems/accounts/* |Criar e gerenciar contas do Sistemas Inteligentes |
| Microsoft.ResourceHealth/availabilityStatuses/read |Integridade de recursos de saudação de leitura |
| Microsoft.Resources/deployments/* |Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read |Ler grupos de recursos |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |

### <a name="monitoring-reader"></a>Leitor de monitoramento
Pode ler todos os dados de monitoramento (métricas, logs, etc). Consulte também [Introdução às funções, permissões e segurança com o Azure Monitor](/monitoring-and-diagnostics/monitoring-roles-permissions-security.md#built-in-monitoring-roles).

| **Ações** |  |
| --- | --- |
| */leitura |Ler recursos de todos os tipos, exceto segredos. |
| Microsoft.OperationalInsights/workspaces/search/action |Pesquisar dados do Log Analytics |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |

### <a name="monitoring-contributor"></a>Colaborador de monitoramento
Pode ler todos os dados de monitoramento e editar configurações de monitoramento. Consulte também [Introdução às funções, permissões e segurança com o Azure Monitor](/monitoring-and-diagnostics/monitoring-roles-permissions-security.md#built-in-monitoring-roles).

| **Ações** |  |
| --- | --- |
| */leitura |Ler recursos de todos os tipos, exceto segredos. |
| Microsoft.Insights/AlertRules/* |Leitura/gravação/exclusão de regras de alerta. |
| Microsoft.Insights/components/* |Leia/grave/exclua componentes do Application Insights. |
| Microsoft.Insights/DiagnosticSettings/* |Leitura/gravação/exclusão de configurações de diagnóstico. |
| Microsoft.Insights/eventtypes/* |Listar eventos do Log de atividades (eventos de gerenciamento) em um assinatura. Essa permissão é aplicável tooboth acesso programático e portal toohello Log de atividades. |
| Microsoft.Insights/LogDefinitions/* |Essa permissão é necessária para os usuários que precisam acessar os Logs de tooActivity por meio do portal de saudação. Liste as categorias de log no Log de Atividades. |
| Microsoft.Insights/MetricDefinitions/* |Ler definições de métricas (lista de tipos de métrica disponíveis para um recurso). |
| Microsoft.Insights/Metrics/* |Ler as métricas para um recurso. |
| Microsoft.Insights/Register/Action |Registre o provedor de Insights hello. |
| Microsoft.Insights/webtests/* |Leia/grave/exclua testes da Web do Application Insights. |
| Microsoft.OperationalInsights/workspaces/intelligencepacks/* |Leia/grave/exclua pacotes de solução do Log Analytics. |
| Microsoft.OperationalInsights/workspaces/savedSearches/* |Leia/grave/exclua pesquisas salvas do Log Analytics. |
| Microsoft.OperationalInsights/workspaces/search/action |Pesquise espaços de trabalho do Log Analytics. |
| Microsoft.OperationalInsights/workspaces/sharedKeys/action |Listar chaves para um espaço de trabalho do Log Analytics. |
| Microsoft.OperationalInsights/workspaces/storageinsightconfigs/* |Leia/grave/exclua configurações de insights de armazenamento do Log Analytics. |

### <a name="network-contributor"></a>Colaborador de rede
Pode gerenciar todos os recursos de rede

| **Ações** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Ler funções e atribuições de função |
| Microsoft.Insights/alertRules/* |Criar e gerenciar regras de alerta |
| Microsoft.Network/* |Criar e gerenciar redes |
| Microsoft.ResourceHealth/availabilityStatuses/read |Integridade de recursos de saudação de leitura |
| Microsoft.Resources/deployments/* |Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read |Ler grupos de recursos |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |

### <a name="new-relic-apm-account-contributor"></a>Colaborador de Conta APM do New Relic
Pode gerenciar contas e aplicativos de Gerenciamento de Desempenho do Aplicativo New Relic

| **Ações** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Ler funções e atribuições de função |
| Microsoft.Insights/alertRules/* |Criar e gerenciar regras de alerta |
| Microsoft.ResourceHealth/availabilityStatuses/read |Integridade de recursos de saudação de leitura |
| Microsoft.Resources/deployments/* |Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read |Ler grupos de recursos |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |
| NewRelic.APM/accounts/* |Criar e gerenciar contas de gerenciamento de desempenho do aplicativo New Relic |

### <a name="owner"></a>Proprietário
Pode gerenciar tudo, incluindo o acesso

| **Ações** |  |
| --- | --- |
| * |Criar e gerenciar recursos de todos os tipos |

### <a name="reader"></a>Leitor
Pode ver tudo, mas não pode fazer alterações

| **Ações** |  |
| --- | --- |
| */leitura |Ler recursos de todos os tipos, exceto segredos. |

### <a name="redis-cache-contributor"></a>Colaborador do Cache Redis
Pode gerenciar caches Redis

| **Ações** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Ler funções e atribuições de função |
| Microsoft.Cache/redis/* |Criar e gerenciar caches Redis |
| Microsoft.Insights/alertRules/* |Criar e gerenciar regras de alerta |
| Microsoft.ResourceHealth/availabilityStatuses/read |Integridade de recursos de saudação de leitura |
| Microsoft.Resources/deployments/* |Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read |Ler grupos de recursos |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |

### <a name="scheduler-job-collections-contributor"></a>Colaborador de Coleções de Trabalho do Agendador
Pode gerenciar coleções de trabalhos do agendador

| **Ações** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Ler funções e atribuições de função |
| Microsoft.Insights/alertRules/* |Criar e gerenciar regras de alerta |
| Microsoft.ResourceHealth/availabilityStatuses/read |Integridade de recursos de saudação de leitura |
| Microsoft.Resources/deployments/* |Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read |Ler grupos de recursos |
| Microsoft.Scheduler/jobcollections/* |Criar e gerenciar coleções de trabalhos |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |

### <a name="search-service-contributor"></a>Colaborador do Serviço de Pesquisa
Pode gerenciar serviços de pesquisa

| **Ações** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Ler funções e atribuições de função |
| Microsoft.Insights/alertRules/* |Criar e gerenciar regras de alerta |
| Microsoft.ResourceHealth/availabilityStatuses/read |Integridade de recursos de saudação de leitura |
| Microsoft.Resources/deployments/* |Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read |Ler grupos de recursos |
| Microsoft.Search/searchServices/* |Criar e gerenciar serviços de pesquisa |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |

### <a name="security-manager"></a>Gerenciador de Segurança
Pode gerenciar componentes de segurança, políticas de segurança e máquinas virtuais

| **Ações** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Ler funções e atribuições de função |
| Microsoft.ClassicCompute/*/read |Ler informações de configuração de máquinas virtuais de computação clássica |
| Microsoft.ClassicCompute/virtualMachines/*/write |Gravar configuração para máquinas virtuais |
| Microsoft.ClassicNetwork/*/read |Ler informações de configuração sobre a rede clássica |
| Microsoft.Insights/alertRules/* |Criar e gerenciar regras de alerta |
| Microsoft.ResourceHealth/availabilityStatuses/read |Integridade de recursos de saudação de leitura |
| Microsoft.Resources/deployments/* |Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read |Ler grupos de recursos |
| Microsoft.Security/* |Criar e gerenciar políticas e componentes de segurança |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |

### <a name="site-recovery-contributor"></a>Colaborador do Site Recovery
Pode gerenciar todas as ações de gerenciamento de recuperação de Site, exceto criar Cofre de serviços de recuperação e atribuição tooother os usuários com direitos de acesso

| **Ações** | |
| --- | --- |
| Microsoft.Authorization/*/read | Ler funções e atribuições de função |
| Microsoft.Insights/alertRules/* | Criar e gerenciar regras de alerta |
| Microsoft.Network/virtualNetworks/read | Ler redes virtuais |
| Microsoft.RecoveryServices/Vaults/certificates/write | Certificado de credencial de Cofre de saudação de atualizações |
| Microsoft.RecoveryServices/Vaults/extendedInformation/* | Criar e gerenciar informações estendidas relacionadas toovault |
| Microsoft.RecoveryServices/Vaults/monitoringAlerts/*  | Ler alertas para o Cofre de serviços de recuperação de saudação |
| Microsoft.RecoveryServices/Vaults/monitoringConfigurations/ notificationConfiguration/read  | Ler a configuração de notificação do cofre dos Serviços de Recuperação |
| Microsoft.RecoveryServices/Vaults/read | Ler cofres dos Serviços de Recuperação |
| Microsoft.RecoveryServices/Vaults/refreshContainers/read | Gerenciar operações de descoberta para buscar contêineres recém-criados |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/* | Criar e gerenciar identidades registradas |
| Microsoft.RecoveryServices/vaults/replicationAlertSettings/* | Criar ou atualizar as configurações de alerta de replicação |
| Microsoft.RecoveryServices/vaults/replicationEvents/read | Ler eventos de replicação |
| Microsoft.RecoveryServices/vaults/replicationFabrics/* | Criar e gerenciar malhas de replicação |
| Microsoft.RecoveryServices/vaults/replicationJobs/* | Criar e gerenciar trabalhos de replicação |
| Microsoft.RecoveryServices/vaults/replicationPolicies/* | Criar e gerenciar políticas de replicação |
| Microsoft.RecoveryServices/vaults/replicationRecoveryPlans/* | Criar e gerenciar planos de recuperação |
| Microsoft.RecoveryServices/Vaults/storageConfig/* | Criar e gerenciar a configuração de armazenamento do cofre de Serviços de Recuperação |
| Microsoft.RecoveryServices/Vaults/tokenInfo/read | Ler informações de token do cofre de Serviços de Recuperação |
| Microsoft.RecoveryServices/Vaults/usages/read | Ler os detalhes de uso de um cofre de Serviços de Recuperação |
| Microsoft.ResourceHealth/availabilityStatuses/read | Integridade de recursos de saudação de leitura |
| Microsoft.Resources/deployments/* | Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read | Ler grupos de recursos |
| Microsoft.Storage/storageAccounts/read | Ler contas de armazenamento |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |

### <a name="site-recovery-operator"></a>Operador do Site Recovery
Failover e Failback, mas pode não executar outras ações de gerenciamento de recuperação de Site nem atribuir acesso de usuários tooother

| **Ações** | |
| --- | --- |
| Microsoft.Authorization/*/read | Ler funções e atribuições de função |
| Microsoft.Insights/alertRules/* | Criar e gerenciar regras de alerta |
| Microsoft.Network/virtualNetworks/read | Ler redes virtuais |
| Microsoft.RecoveryServices/Vaults/extendedInformation/read | Informações de leitura estendida relacionados toovault |
| Microsoft.RecoveryServices/Vaults/monitoringAlerts/*  | Ler alertas para o Cofre de serviços de recuperação de saudação |
| Microsoft.RecoveryServices/Vaults/monitoringConfigurations/ notificationConfiguration/read  | Ler a configuração de notificação do cofre dos Serviços de Recuperação |
| Microsoft.RecoveryServices/Vaults/read | Ler cofres dos Serviços de Recuperação |
| Microsoft.RecoveryServices/Vaults/refreshContainers/read | Gerenciar operações de descoberta para buscar contêineres recém-criados |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/operationResults/read | Ler o status da operação e o resultado de uma operação enviada |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/read | Ler contêineres registrados para um recurso |
| Microsoft.RecoveryServices/vaults/replicationAlertSettings/read | Ler definições de alerta de replicação |
| Microsoft.RecoveryServices/vaults/replicationEvents/read | Ler eventos de replicação |
| Microsoft.RecoveryServices/vaults/replicationFabrics/checkConsistency/action | Verificação de consistência de malhas de saudação do |
| Microsoft.RecoveryServices/vaults/replicationFabrics/read | Ler malhas de replicação |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ reassociateGateway/action | Reassociar o gateway de replicação |
| Microsoft.RecoveryServices/vaults/replicationFabrics/renewcertificate/action | Renovar o certificado de malha de replicação |
| Microsoft.RecoveryServices/vaults/replicationFabrics/replicationNetworks/read | Ler redes de malha de replicação |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationNetworks/replicationNetworkMappings/read | Ler o mapeamento de rede de malha de replicação |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/read | Ler contêineres de proteção |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectableItems/read | Retornar a lista de todos os itens que podem ser protegidos |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/ applyRecoveryPoint/action | Aplicar um ponto de recuperação específico |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/ failoverCommit/action | Confirmar failover para um item que sofreu failover |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/ plannedFailover/action | Iniciar o failover planejado para um item protegido |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/read | Obter a lista de todos os itens protegidos |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/recoveryPoints/read | Obter a lista de pontos de recuperação disponíveis |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/ repairReplication/action | Reparar a replicação para um item protegido |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/reProtect/action | Começar a proteger novamente um item protegido|
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/testFailover/action | Iniciar o failover de teste de um item protegido |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/ testFailoverCleanup/action | Iniciar a limpeza de um failover de teste |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/ unplannedFailover/action | Iniciar o failover não planejado de um item protegido |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/ updateMobilityService/action | Atualizar serviço de mobilidade Olá |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectionContainerMappings/read | Ler mapeamentos de contêiner de proteção |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationRecoveryServicesProviders/read | Ler provedores de Serviços de Recuperação |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationRecoveryServicesProviders/refreshProvider/action | Atualizar o provedor de Serviços de Recuperação |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationStorageClassifications/read | Ler classificações de armazenamento para as malhas replicação |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationStorageClassifications/replicationStorageClassificationMappings/read | Ler mapeamentos de classificação de armazenamento |
| Microsoft.RecoveryServices/vaults/replicationFabrics/replicationvCenters/read | Ler informações do vCenter registradas |
| Microsoft.RecoveryServices/vaults/replicationJobs/* | Criar e gerenciar trabalhos de replicação |
| Microsoft.RecoveryServices/vaults/replicationPolicies/read | Ler políticas de replicação |
| Microsoft.RecoveryServices/vaults/replicationRecoveryPlans/ failoverCommit/action | Confirmar failover para failover do plano de recuperação |
| Microsoft.RecoveryServices/vaults/replicationRecoveryPlans/ plannedFailover/action | Iniciar o failover de um plano de recuperação |
| Microsoft.RecoveryServices/vaults/replicationRecoveryPlans/read | Ler planos de recuperação |
| Microsoft.RecoveryServices/vaults/replicationRecoveryPlans/reProtect/action | Começar a proteger novamente um plano de recuperação |
| Microsoft.RecoveryServices/vaults/replicationRecoveryPlans/testFailover/action | Iniciar o failover de teste de um plano de recuperação |
| Microsoft.RecoveryServices/vaults/replicationRecoveryPlans/ testFailoverCleanup/action | Iniciar a limpeza do failover de teste de um plano de recuperação |
| Microsoft.RecoveryServices/vaults/replicationRecoveryPlans/ unplannedFailover/action | Iniciar o failover não planejado de um plano de recuperação |
| Microsoft.RecoveryServices/Vaults/storageConfig/read | Ler a configuração de armazenamento de um cofre de Serviços de Recuperação |
| Microsoft.RecoveryServices/Vaults/tokenInfo/read | Ler informações de token do cofre de Serviços de Recuperação |
| Microsoft.RecoveryServices/Vaults/usages/read | Ler os detalhes de uso de um cofre de Serviços de Recuperação |
| Microsoft.ResourceHealth/availabilityStatuses/read | Integridade de recursos de saudação de leitura |
| Microsoft.Resources/deployments/* | Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read | Ler grupos de recursos |
| Microsoft.Storage/storageAccounts/read | Ler contas de armazenamento |
| Microsoft.Support/* | Criar e gerenciar tíquetes de suporte |

### <a name="site-recovery-reader"></a>Leitor do Site Recovery
Pode monitorar o status do Site Recovery no cofre de Serviços de Recuperação e gerar tíquetes de suporte

| **Ações** | |
| --- | --- |
| Microsoft.Authorization/*/read | Ler funções e atribuições de função |
| Microsoft.RecoveryServices/Vaults/extendedInformation/read  | Informações de leitura estendida relacionados toovault |
| Microsoft.RecoveryServices/Vaults/monitoringAlerts/read  | Ler alertas para o Cofre de serviços de recuperação de saudação |
| Microsoft.RecoveryServices/Vaults/monitoringConfigurations/ notificationConfiguration/read  | Ler a configuração de notificação do cofre dos Serviços de Recuperação |
| Microsoft.RecoveryServices/Vaults/read  | Ler cofres dos Serviços de Recuperação |
| Microsoft.RecoveryServices/Vaults/refreshContainers/read  | Gerenciar operações de descoberta para buscar contêineres recém-criados |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/operationResults/read  | Ler o status da operação e o resultado de uma operação enviada |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/read  | Ler contêineres registrados para um recurso |
| Microsoft.RecoveryServices/vaults/replicationAlertSettings/read | Ler definições de alerta de replicação |
| Microsoft.RecoveryServices/vaults/replicationEvents/read  | Ler eventos de replicação |
| Microsoft.RecoveryServices/vaults/replicationFabrics/read  | Ler malhas de replicação |
| Microsoft.RecoveryServices/vaults/replicationFabrics/replicationNetworks/read  | Ler redes de malha de replicação |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationNetworks/replicationNetworkMappings/read  | Ler o mapeamento de rede de malha de replicação |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/read  |  Ler contêineres de proteção |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectableItems/read  | Retornar a lista de todos os itens que podem ser protegidos |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/read  | Obter a lista de todos os itens protegidos |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/recoveryPoints/read  | Obter a lista de pontos de recuperação disponíveis |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectionContainerMappings/read  | Ler mapeamentos de contêiner de proteção |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationRecoveryServicesProviders/read  | Ler provedores de Serviços de Recuperação |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationStorageClassifications/read  | Ler classificações de armazenamento para as malhas replicação |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationStorageClassifications/replicationStorageClassificationMappings/read  |  Ler mapeamentos de classificação de armazenamento |
| Microsoft.RecoveryServices/vaults/replicationFabrics/replicationvCenters/read  |  Ler informações do vCenter registradas |
| Microsoft.RecoveryServices/vaults/replicationJobs/read  |  Ler o status dos trabalhos de replicação |
| Microsoft.RecoveryServices/vaults/replicationPolicies/read  |  Ler políticas de replicação |
| Microsoft.RecoveryServices/vaults/replicationRecoveryPlans/read  |  Ler planos de recuperação |
| Microsoft.RecoveryServices/Vaults/storageConfig/read  |  Ler a configuração de armazenamento de um cofre de Serviços de Recuperação |
| Microsoft.RecoveryServices/Vaults/tokenInfo/read  |  Ler informações de token do cofre de Serviços de Recuperação |
| Microsoft.RecoveryServices/Vaults/usages/read  |  Ler os detalhes de uso de um cofre de Serviços de Recuperação |
| Microsoft.Support/*  |  Criar e gerenciar tíquetes de suporte |

### <a name="sql-db-contributor"></a>Colaborador do banco de dados SQL
Pode gerenciar bancos de dados SQL, mas não suas políticas relacionadas à segurança

| **Ações** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Ler funções e atribuições de função |
| Microsoft.Insights/alertRules/* |Criar e gerenciar regras de alerta |
| Microsoft.ResourceHealth/availabilityStatuses/read |Integridade de recursos de saudação de leitura |
| Microsoft.Resources/deployments/* |Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read |Ler grupos de recursos |
| Microsoft.Sql/servers/databases/* |Criar e gerenciar bancos de dados SQL |
| Microsoft.Sql/servers/read |Leia os SQL Servers |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |

| **NotActions** |  |
| --- | --- |
| Microsoft.Sql/servers/databases/auditingPolicies/* |Não é possível editar políticas de auditoria |
| Microsoft.Sql/servers/databases/auditingSettings/* |Não é possível editar configurações de auditoria |
| Microsoft.Sql/servers/databases/auditRecords/read |Não é possível ler registros de auditoria |
| Microsoft.Sql/servers/databases/connectionPolicies/* |Não é possível editar políticas de conexão |
| Microsoft.Sql/servers/databases/dataMaskingPolicies/* |Não é possível editar políticas de mascaramento dos dados |
| Microsoft.Sql/servers/databases/securityAlertPolicies/* |Não é possível editar políticas de alerta de segurança |
| Microsoft.Sql/servers/databases/securityMetrics/* |Não é possível editar métricas de segurança |

### <a name="sql-security-manager"></a>Gerenciador de Segurança do SQL
Pode gerenciar políticas de saudação relacionadas à segurança de servidores SQL e bancos de dados

| **Ações** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Ler autorização da Microsoft |
| Microsoft.Insights/alertRules/* |Criar e gerenciar regras de alerta do Insights |
| Microsoft.ResourceHealth/availabilityStatuses/read |Integridade de recursos de saudação de leitura |
| Microsoft.Resources/deployments/* |Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read |Ler grupos de recursos |
| Microsoft.Sql/servers/auditingPolicies/* |Criar e gerenciar políticas de auditoria do servidor SQL |
| Microsoft.Sql/servers/auditingSettings/* |Criar e gerenciar a configuração de auditoria do servidor SQL |
| Microsoft.Sql/servers/databases/auditingPolicies/* |Criar e gerenciar políticas de auditoria de banco de dados do servidor SQL |
| Microsoft.Sql/servers/databases/auditingSettings/* |Criar e gerenciar configurações de auditoria de banco de dados do servidor SQL |
| Microsoft.Sql/servers/databases/auditRecords/read |Ler registros de auditoria |
| Microsoft.Sql/servers/databases/connectionPolicies/* |Criar e gerenciar políticas de conexão de banco de dados do servidor SQL |
| Microsoft.Sql/servers/databases/dataMaskingPolicies/* |Criar e gerenciar políticas de mascaramento de dados do banco de dados do servidor SQL |
| Microsoft.Sql/servers/databases/read |Ler bancos de dados SQL |
| Microsoft.Sql/servers/databases/schemas/read |Ler esquemas de banco de dados do SQL Server |
| Microsoft.Sql/servers/databases/schemas/tables/columns/read |Ler colunas de tabela de banco de dados do servidor SQL |
| Microsoft.Sql/servers/databases/schemas/tables/read |Ler tabelas de banco de dados do servidor SQL |
| Microsoft.Sql/servers/databases/securityAlertPolicies/* |Criar e gerenciar políticas de alerta de segurança do banco de dados do servidor SQL |
| Microsoft.Sql/servers/databases/securityMetrics/* |Criar e gerenciar métricas de segurança do banco de dados do servidor SQL |
| Microsoft.Sql/servers/read |Leia os SQL Servers |
| Microsoft.Sql/servers/securityAlertPolicies/* |Criar e gerenciar políticas de alerta de segurança de servidor SQL |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |

### <a name="sql-server-contributor"></a>Colaborador do SQL Server
Pode gerenciar servidores e bancos de dados SQL, mas não as políticas relacionadas à segurança

| **Ações** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Ler autorização |
| Microsoft.Insights/alertRules/* |Criar e gerenciar regras de alerta do Insights |
| Microsoft.ResourceHealth/availabilityStatuses/read |Integridade de recursos de saudação de leitura |
| Microsoft.Resources/deployments/* |Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read |Ler grupos de recursos |
| Microsoft.Sql/servers/* |Criar e gerenciar servidores SQL |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |

| **NotActions** |  |
| --- | --- |
| Microsoft.Sql/servers/auditingPolicies/* |Não é possível editar políticas de auditoria do servidor SQL |
| Microsoft.Sql/servers/auditingSettings/* |Não é possível editar configurações de auditoria do servidor SQL |
| Microsoft.Sql/servers/databases/auditingPolicies/* |Não é possível editar políticas de auditoria de banco de dados do servidor SQL |
| Microsoft.Sql/servers/databases/auditingSettings/* |Não é possível editar configurações de auditoria de banco de dados do servidor SQL |
| Microsoft.Sql/servers/databases/auditRecords/read |Não é possível ler registros de auditoria |
| Microsoft.Sql/servers/databases/connectionPolicies/* |Não é possível editar políticas de conexão de banco de dados do servidor SQL |
| Microsoft.Sql/servers/databases/dataMaskingPolicies/* |Não é possível editar políticas de mascaramento de banco de dados do servidor SQL |
| Microsoft.Sql/servers/databases/securityAlertPolicies/* |Não é possível editar políticas de alerta de segurança de banco de dados do servidor SQL |
| Microsoft.Sql/servers/databases/securityMetrics/* |Não é possível editar métricas de segurança de banco de dados do servidor SQL |
| Microsoft.Sql/servers/securityAlertPolicies/* |Não é possível editar políticas de alerta de segurança de servidor SQL |

### <a name="classic-storage-account-contributor"></a>Colaborador da conta de armazenamento clássica
Pode gerenciar contas de armazenamento clássicas

| **Ações** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Ler autorização |
| Microsoft.ClassicStorage/storageAccounts/* |Criar e gerenciar contas de armazenamento |
| Microsoft.Insights/alertRules/* |Criar e gerenciar regras de alerta do Insights |
| Microsoft.ResourceHealth/availabilityStatuses/read |Integridade de recursos de saudação de leitura |
| Microsoft.Resources/deployments/* |Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read |Ler grupos de recursos |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |

### <a name="storage-account-contributor"></a>Colaborador da Conta de Armazenamento
Pode gerenciar contas de armazenamento, mas não acessar toothem.

| **Ações** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Ler todas as autorizações |
| Microsoft.Insights/alertRules/* |Criar e gerenciar regras de alerta do Insights |
| Microsoft.Insights/diagnosticSettings/* |Gerenciar configurações de diagnóstico |
| Microsoft.ResourceHealth/availabilityStatuses/read |Integridade de recursos de saudação de leitura |
| Microsoft.Resources/deployments/* |Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read |Ler grupos de recursos |
| Microsoft.Storage/storageAccounts/* |Criar e gerenciar contas de armazenamento |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |

### <a name="support-request-contributor"></a>Colaborador de solicitação de suporte
Crie e gerencie os tíquetes de suporte no escopo de assinatura Olá

| **Ações** |  |
| --- | --- |
| Microsoft.Authorization/*/read | Ler autorização |
| Microsoft.Support/* | Criar e gerenciar tíquetes de suporte |
| Microsoft.Resources/subscriptions/resourceGroups/read | Ler funções e atribuições de função |

### <a name="user-access-administrator"></a>Administrador de Acesso do Usuário
Pode gerenciar os recursos de tooAzure de acesso do usuário

| **Ações** |  |
| --- | --- |
| */leitura |Ler recursos de todos os tipos, exceto segredos. |
| Microsoft.Authorization/* |Gerenciar autorização |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |

### <a name="classic-virtual-machine-contributor"></a>Colaborador de Máquina Virtual Clássica
Pode gerenciar máquinas virtuais clássicas, mas não rede virtual hello ou toowhich de conta de armazenamento que estão conectados

| **Ações** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Ler autorização |
| Microsoft.ClassicCompute/domainNames/* |Criar e gerenciar nomes de domínio de computação clássica |
| Microsoft.ClassicCompute/virtualMachines/* |Criar e gerenciar máquinas virtuais |
| Microsoft.ClassicNetwork/networkSecurityGroups/join/action |Unir grupos de segurança de rede |
| Microsoft.ClassicNetwork/reservedIps/link/action |Vincular IPs reservados |
| Microsoft.ClassicNetwork/reservedIps/read |Ler endereços IP reservados |
| Microsoft.ClassicNetwork/virtualNetworks/join/action |Unir redes virtuais |
| Microsoft.ClassicNetwork/virtualNetworks/read |Ler redes virtuais |
| Microsoft.ClassicStorage/storageAccounts/disks/read |Ler discos de contas de armazenamento |
| Microsoft.ClassicStorage/storageAccounts/images/read |Ler imagens de contas de armazenamento |
| Microsoft.ClassicStorage/storageAccounts/listKeys/action |Listar chaves da conta de armazenamento |
| Microsoft.ClassicStorage/storageAccounts/read |Ler contas de armazenamento clássico |
| Microsoft.Insights/alertRules/* |Criar e gerenciar regras de alerta do Insights |
| Microsoft.ResourceHealth/availabilityStatuses/read |Integridade de recursos de saudação de leitura |
| Microsoft.Resources/deployments/* |Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read |Ler grupos de recursos |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |

### <a name="virtual-machine-contributor"></a>Colaborador de Máquina Virtual
Pode gerenciar máquinas virtuais, mas não Olá virtual rede ou armazenamento conta toowhich que estão conectados

| **Ações** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Ler autorização |
| Microsoft.Compute/availabilitySets/* |Criar e gerenciar conjuntos de disponibilidade de computação |
| Microsoft.Compute/locations/* |Criar e gerenciar locais de computação |
| Microsoft.Compute/virtualMachines/* |Criar e gerenciar máquinas virtuais |
| Microsoft.Compute/virtualMachineScaleSets/* |Criar e gerenciar conjuntos de escala de máquina virtual |
| Microsoft.Insights/alertRules/* |Criar e gerenciar regras de alerta do Insights |
| Microsoft.Network/applicationGateways/backendAddressPools/join/action |Unir pools de endereços back-end do gateway de aplicativo de rede |
| Microsoft.Network/loadBalancers/backendAddressPools/join/action |Unir pools de endereços de back-end de balanceador de carga |
| Microsoft.Network/loadBalancers/inboundNatPools/join/action |Unir pools NAT de entrada dos balanceadores de carga |
| Microsoft.Network/loadBalancers/inboundNatRules/join/action |Unir regras NAT de entrada dos balanceadores de carga |
| Microsoft.Network/loadBalancers/read |Ler balanceadores de carga |
| Microsoft.Network/locations/* |Criar e gerenciar locais de rede |
| Microsoft.Network/networkInterfaces/* |Criar e gerenciar as interfaces de rede |
| Microsoft.Network/networkSecurityGroups/join/action |Unir grupos de segurança de rede |
| Microsoft.Network/networkSecurityGroups/read |Ler grupos de segurança de rede |
| Microsoft.Network/publicIPAddresses/join/action |Unir endereços IP públicos de rede |
| Microsoft.Network/publicIPAddresses/read |Ler endereços IP públicos de rede |
| Microsoft.Network/virtualNetworks/read |Ler redes virtuais |
| Microsoft.Network/virtualNetworks/subnets/join/action |Unir sub-redes de rede virtual |
| Microsoft.ResourceHealth/availabilityStatuses/read |Integridade de recursos de saudação de leitura |
| Microsoft.Resources/deployments/* |Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read |Ler grupos de recursos |
| Microsoft.Storage/storageAccounts/listKeys/action |Listar chaves da conta de armazenamento |
| Microsoft.Storage/storageAccounts/read |Ler contas de armazenamento |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |

### <a name="classic-network-contributor"></a>Colaborador de rede clássica
Pode gerenciar redes virtuais clássicas e IPs reservados

| **Ações** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Ler autorização |
| Microsoft.ClassicNetwork/* |Criar e gerenciar redes clássicas |
| Microsoft.Insights/alertRules/* |Criar e gerenciar regras de alerta do Insights |
| Microsoft.ResourceHealth/availabilityStatuses/read |Integridade de recursos de saudação de leitura |
| Microsoft.Resources/deployments/* |Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read |Ler grupos de recursos |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |

### <a name="web-plan-contributor"></a>Colaborador do Plano de Web
Pode gerenciar planos da Web

| **Ações** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Ler autorização |
| Microsoft.Insights/alertRules/* |Criar e gerenciar regras de alerta do Insights |
| Microsoft.ResourceHealth/availabilityStatuses/read |Integridade de recursos de saudação de leitura |
| Microsoft.Resources/deployments/* |Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read |Ler grupos de recursos |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |
| Microsoft.Web/serverFarms/* |Criar e gerenciar farms de servidores |

### <a name="website-contributor"></a>Colaborador do Site
Pode gerenciar sites, mas não Olá web planos toowhich estão conectados

| **Ações** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Ler autorização |
| Microsoft.Insights/alertRules/* |Criar e gerenciar regras de alerta do Insights |
| Microsoft.Insights/components/* |Criar e gerenciar componentes do Insights |
| Microsoft.ResourceHealth/availabilityStatuses/read |Integridade de recursos de saudação de leitura |
| Microsoft.Resources/deployments/* |Criar e gerenciar implantações do grupo de recursos |
| Microsoft.Resources/subscriptions/resourceGroups/read |Ler grupos de recursos |
| Microsoft.Support/* |Criar e gerenciar tíquetes de suporte |
| Microsoft.Web/certificates/* |Criar e gerenciar certificados de site da Web |
| Microsoft.Web/listSitesAssignedToHostName/read |Sites de leitura atribuídos um nome de host tooa |
| Microsoft.Web/serverFarms/join/action |Unir farms de servidores |
| Microsoft.Web/serverFarms/read |Ler farms de servidores |
| Microsoft.Web/sites/* |Criar e gerenciar sites (criação do site também requer toohello de permissões de gravação associados plano do serviço de aplicativo) |

## <a name="see-also"></a>Consulte também
* [Controle de acesso baseado em função](role-based-access-control-configure.md): Introdução ao RBAC em Olá portal do Azure.
* [Funções personalizadas no Azure RBAC](role-based-access-control-custom-roles.md): Saiba como toocreate funções personalizadas toofit sua necessidades de acesso.
* [Criar um relatório de histórico de alterações de acesso](role-based-access-control-access-change-history-report.md): mantenha o controle das alterações de atribuições de função no RBAC.
* [Solução de problemas de Controle de Acesso Baseado em Função](role-based-access-control-troubleshooting.md): obtenha sugestões para corrigir problemas comuns.
