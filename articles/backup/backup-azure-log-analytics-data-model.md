---
title: "modelo de dados de análise de aaaLog para Backup do Azure"
description: Este artigo aborda detalhes de modelo de dados do Log Analytics para dados de Backup do Azure.
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: dfd5c73d-0d34-4d48-959e-1936986f9fc0
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 04ac16e38b896851f60b1c4ffbea4343347ae32c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-data-model-for-azure-backup-data"></a>Modelo de dados do Log Analytics para dados de Backup do Azure
Este artigo descreve o modelo de dados de saudação usado para enviar o relatório dados tooLog análise. Utilizando esse modelo de dados é possível criar consultas personalizadas, painéis e utilizá-lo no OMS. 

## <a name="using-azure-backup-data-model"></a>Usando o modelo de dados de Backup do Azure
Você pode usar o hello campos fornecidos como parte de visuais de toocreate de modelo de dados hello, consultas personalizadas e painel de acordo com seus requisitos a seguir.

### <a name="alert"></a>Alerta
Essa tabela fornece detalhes sobre campos relacionados ao alerta.

| Campo | Tipo de Dados | Descrição |
| --- | --- | --- |
| AlertUniqueId_s |Texto |Id exclusiva da saudação gerou o alerta |
| AlertType_s |Texto |Tipo de saudação gerou o alerta, por exemplo, Backup |
| AlertStatus_s |Texto |Status de saudação alerta, por exemplo, ativo |
| AlertOccurenceDateTime_s |Data/hora |Data e hora em que o alerta foi criado |
| AlertSeverity_s |Texto |Gravidade da saudação alerta, por exemplo, crítico |
| EventName_s |Texto |Este campo representa o nome desse evento, é sempre AzureBackupCentralReport |
| BackupItemUniqueId_s |Texto |Id exclusiva da saudação fazer backup do item toowhich que este alerta pertence muito|
| SchemaVersion_s |Texto |Este campo indica a versão atual do esquema de hello, é **V1** |
| State_s |Texto |Estado atual do objeto alerta hello, por exemplo, ativo, excluídos |
| BackupManagementType_s |Texto |Tipo de provedor para executar o backup, por exemplo, IaaSVM, toowhich FileFolder este alerta pertence muito|
| OperationName |Texto |Este campo representa o nome da operação atual de saudação - alerta |
| Categoria |Texto |Este campo representa a categoria de dados de diagnóstico enviados por push tooLog análise, é AzureBackupReport |
| Recurso |Texto |Este é o recurso Olá para o qual os dados estão sendo coletados, ele mostra o nome do Cofre de serviços de recuperação |
| ProtectedServerUniqueId_s |Texto |Id exclusiva da saudação protegido toowhich que este alerta pertence muito|
| VaultUniqueId_s |Texto |Id exclusiva da saudação protegido toowhich que este alerta pertence muito|
| SourceSystem |Texto |Sistema de fonte de dados atual da saudação - Azure |
| ResourceId |Texto |Este campo representa o ID do recurso para o qual os dados estão sendo coletados, ele mostra o ID do recurso do cofre dos Serviços de Recuperação |
| SubscriptionId |Texto |Este campo representa a id de assinatura do recurso de saudação (RS cofre) para o qual os dados estão sendo coletados |
| ResourceGroup |Texto |Este campo representa o grupo de recursos do recurso de saudação (RS cofre) para o qual os dados estão sendo coletados |
| ResourceProvider |Texto |Este campo representa o provedor de recursos de saudação para o qual os dados estão sendo coletados - Microsoft.RecoveryServices |
| ResourceType |Texto |Este campo representa o tipo de recurso de saudação para o qual os dados estão sendo coletados - cofres |

### <a name="backupitem"></a>BackupItem
Esta tabela fornece detalhes sobre os campos relacionados ao item de backup.

| Campo | Tipo de Dados | Descrição |
| --- | --- | --- |
| EventName_s |Texto |Este campo representa o nome desse evento, é sempre AzureBackupCentralReport |  
| BackupItemUniqueId_s |Texto |Id exclusiva do item de backup Olá |
| BackupItemId_s |Texto |ID do item de backup |
| BackupItemName_s |Texto |ID do item de backup |
| BackupItemFriendlyName_s |Texto |Nome amigável do item de backup |
| BackupItemType_s |Texto |Tipo de item de backup, por exemplo, VM, FileFolder |
| ProtectedServerName_s |Texto |Nome do item de backup do servidor protegido toowhich muito pertence|
| ProtectionState_s |Texto |Estado de proteção atual do item backup hello, por exemplo, Protected, ProtectionStopped |
| SchemaVersion_s |Texto |Este campo indica a versão atual do esquema de hello, é **V1** |
| State_s |Texto |Estado atual do objeto de item de backup hello, por exemplo, ativo, excluídos |
| BackupManagementType_s |Texto |Tipo de provedor para executar o backup, por exemplo, IaaSVM, toowhich FileFolder este item de backup muito pertence|
| OperationName |Texto |Este campo representa o nome da operação atual de saudação - BackupItem |
| Categoria |Texto |Este campo representa a categoria de dados de diagnóstico enviados por push tooLog análise, é AzureBackupReport |
| Recurso |Texto |Este é o recurso Olá para o qual os dados estão sendo coletados, ele mostra o nome do Cofre de serviços de recuperação |
| SourceSystem |Texto |Sistema de fonte de dados atual da saudação - Azure |
| ResourceId |Texto |Este campo representa o ID do recurso para o qual os dados estão sendo coletados, ele mostra o ID do recurso do cofre dos Serviços de Recuperação |
| SubscriptionId |Texto |Este campo representa a id de assinatura do recurso de saudação (RS cofre) para o qual os dados estão sendo coletados |
| ResourceGroup |Texto |Este campo representa o grupo de recursos do recurso de saudação (RS cofre) para o qual os dados estão sendo coletados |
| ResourceProvider |Texto |Este campo representa o provedor de recursos de saudação para o qual os dados estão sendo coletados - Microsoft.RecoveryServices |
| ResourceType |Texto |Este campo representa o tipo de recurso de saudação para o qual os dados estão sendo coletados - cofres |

### <a name="backupitemassociation"></a>BackupItemAssociation
Esta tabela fornece detalhes sobre associações de itens de backup com várias entidades.

| Campo | Tipo de Dados | Descrição |
| --- | --- | --- |
| EventName_s |Texto |Este campo representa o nome desse evento, é sempre AzureBackupCentralReport |  
| BackupItemUniqueId_s |Texto |Id exclusiva do item de backup Olá |
| SchemaVersion_s |Texto |Este campo indica a versão atual do esquema de hello, é **V1** |
| State_s |Texto |Estado atual do objeto Olá fazer backup do item associação, por exemplo, ativo, excluídos |
| BackupManagementType_s |Texto |Tipo de provedor para executar o backup, por exemplo, IaaSVM, toowhich FileFolder este item de backup muito pertence|
| OperationName |Texto |Este campo representa o nome da operação atual de saudação - BackupItemAssociation |
| Categoria |Texto |Este campo representa a categoria de dados de diagnóstico enviados por push tooLog análise, é AzureBackupReport |
| Recurso |Texto |Este é o recurso Olá para o qual os dados estão sendo coletados, ele mostra o nome do Cofre de serviços de recuperação |
| PolicyUniqueId_g |Texto |Id tooidentify Olá política exclusivo, qual item de backup é muito associado|
| ProtectedServerUniqueId_s |Texto |Id exclusiva da saudação protegido toowhich server que este item de backup muito pertence|
| VaultUniqueId_s |Texto |Id exclusiva da saudação cofre toowhich que este item de backup muito pertence|
| SourceSystem |Texto |Sistema de fonte de dados atual da saudação - Azure |
| ResourceId |Texto |Este campo representa o ID do recurso para o qual os dados estão sendo coletados, ele mostra o ID do recurso do cofre dos Serviços de Recuperação |
| SubscriptionId |Texto |Este campo representa a id de assinatura do recurso de saudação (RS cofre) para o qual os dados estão sendo coletados |
| ResourceGroup |Texto |Este campo representa o grupo de recursos do recurso de saudação (RS cofre) para o qual os dados estão sendo coletados |
| ResourceProvider |Texto |Este campo representa o provedor de recursos de saudação para o qual os dados estão sendo coletados - Microsoft.RecoveryServices |
| ResourceType |Texto |Este campo representa o tipo de recurso de saudação para o qual os dados estão sendo coletados - cofres |

### <a name="job"></a>Trabalho
Esta tabela fornece detalhes sobre campos relacionados ao trabalho.

| Campo | Tipo de Dados | Descrição |
| --- | --- | --- |
| EventName_s |Texto |Este campo representa o nome desse evento, é sempre AzureBackupCentralReport |
| BackupItemUniqueId_s |Texto |Id exclusiva da saudação fazer backup do item toowhich que este trabalho pertence muito|
| SchemaVersion_s |Texto |Este campo indica a versão atual do esquema de hello, é **V1** |
| State_s |Texto |Estado atual do objeto de trabalho hello, por exemplo, ativo, excluídos |
| BackupManagementType_s |Texto |Tipo de provedor para executar o backup, por exemplo, IaaSVM, toowhich FileFolder este trabalho pertence muito|
| OperationName |Texto |Este campo representa o nome da operação atual de saudação - trabalho |
| Categoria |Texto |Este campo representa a categoria de dados de diagnóstico enviados por push tooLog análise, é AzureBackupReport |
| Recurso |Texto |Este é o recurso Olá para o qual os dados estão sendo coletados, ele mostra o nome do Cofre de serviços de recuperação |
| ProtectedServerUniqueId_s |Texto |Id exclusiva da saudação protegido toowhich que este trabalho pertence muito|
| VaultUniqueId_s |Texto |Id exclusiva da saudação protegido toowhich que este trabalho pertence muito|
| JobOperation_s |Texto |Operação para a qual o trabalho é executado, por exemplo, backup, restauração, backup de configuração |
| JobStatus_s |Texto |Status da saudação terminar o trabalho, por exemplo, concluído, falha |
| JobFailureCode_s |Texto |Cadeia de caracteres de código de falha pela qual a falha no trabalho ocorreu |
| JobStartDateTime_s |Data/hora |Data e hora em que o trabalho iniciou a execução |
| BackupStorageDestination_s |Texto |Destino do armazenamento de backup, por exemplo, Nuvem, Disco  |
| JobDurationInSecs_s | Número |Duração total do trabalho em segundos |
| DataTransferredInMB_s | Número |Dados transferidos em MB para este trabalho|
| JobUniqueId_g |Texto |Trabalho de saudação do tooidentify Id exclusiva |
| SourceSystem |Texto |Sistema de fonte de dados atual da saudação - Azure |
| ResourceId |Texto |Este campo representa o ID do recurso para o qual os dados estão sendo coletados, ele mostra o ID do recurso do cofre dos Serviços de Recuperação |
| SubscriptionId |Texto |Este campo representa a id de assinatura do recurso de saudação (RS cofre) para o qual os dados estão sendo coletados |
| ResourceGroup |Texto |Este campo representa o grupo de recursos do recurso de saudação (RS cofre) para o qual os dados estão sendo coletados |
| ResourceProvider |Texto |Este campo representa o provedor de recursos de saudação para o qual os dados estão sendo coletados - Microsoft.RecoveryServices |
| ResourceType |Texto |Este campo representa o tipo de recurso de saudação para o qual os dados estão sendo coletados - cofres |

### <a name="policy"></a>Política
Esta tabela fornece detalhes sobre campos relacionados a políticas.

| Campo | Tipo de Dados | Descrição |
| --- | --- | --- |
| EventName_s |Texto |Este campo representa o nome desse evento, é sempre AzureBackupCentralReport |
| SchemaVersion_s |Texto |Este campo indica a versão atual do esquema de hello, é **V1** |
| State_s |Texto |Estado atual do objeto de diretiva de hello, por exemplo, ativo, excluídos |
| BackupManagementType_s |Texto |Tipo de provedor para executar o backup, por exemplo, IaaSVM, toowhich FileFolder esta política pertence muito|
| OperationName |Texto |Este campo representa o nome da operação atual de saudação - política |
| Categoria |Texto |Este campo representa a categoria de dados de diagnóstico enviados por push tooLog análise, é AzureBackupReport |
| Recurso |Texto |Este é o recurso Olá para o qual os dados estão sendo coletados, ele mostra o nome do Cofre de serviços de recuperação |
| PolicyUniqueId_g |Texto |Política de saudação do tooidentify Id exclusiva |
| PolicyName_s |Texto |Nome da política de saudação definida |
| BackupFrequency_s |Texto |Frequência com que os backups são executados, por exemplo, diária, semanal |
| BackupTimes_s |Texto |Data e hora quando os backups são agendados |
| BackupDaysOfTheWeek_s |Texto |Dias da semana hello quando os backups foram agendados |
| RetentionDuration_s |Número inteiro |Duração de retenção para backups configurados |
| DailyRetentionDuration_s |Número inteiro |Duração total da retenção em dias para backups configurados |
| DailyRetentionTimes_s |Texto |Data e hora quando a retenção diária foi configurada |
| WeeklyRetentionDuration_s |Número decimal |Duração total da retenção em semanas para backups configurados |
| WeeklyRetentionTimes_s |Texto |Data e hora quando a retenção semanal foi configurada |
| WeeklyRetentionDaysOfTheWeek_s |Texto |Dias da semana Olá marcada para retenção semanal |
| MonthlyRetentionDuration_s |Número decimal |Duração total da retenção em meses para backups configurados |
| MonthlyRetentionTimes_s |Texto |Data e hora quando a retenção mensal foi configurada |
| MonthlyRetentionFormat_s |Texto |Tipo de configuração de retenção mensal, por exemplo, diário, semanal |
| MonthlyRetentionDaysOfTheWeek_s |Texto |Dias da semana Olá marcada para retenção mensal |
| MonthlyRetentionWeeksOfTheMonth_s |Texto |Semanas do mês de saudação quando retenção mensal é configurada, por exemplo, a primeira, última etc. |
| YearlyRetentionDuration_s |Número decimal |Duração total da retenção em ano para backups configurados |
| YearlyRetentionTimes_s |Texto |Data e hora quando a retenção anual foi configurada |
| YearlyRetentionMonthsOfTheYear_s |Texto |Meses do ano Olá marcada para retenção anual |
| YearlyRetentionFormat_s |Texto |Tipo de configuração de retenção anual, por exemplo, diário, semanal |
| YearlyRetentionDaysOfTheMonth_s |Texto |Datas do mês Olá marcada para retenção anual |
| SourceSystem |Texto |Sistema de fonte de dados atual da saudação - Azure |
| ResourceId |Texto |Este campo representa o ID do recurso para o qual os dados estão sendo coletados, ele mostra o ID do recurso do cofre dos Serviços de Recuperação |
| SubscriptionId |Texto |Este campo representa a id de assinatura do recurso de saudação (RS cofre) para o qual os dados estão sendo coletados |
| ResourceGroup |Texto |Este campo representa o grupo de recursos do recurso de saudação (RS cofre) para o qual os dados estão sendo coletados |
| ResourceProvider |Texto |Este campo representa o provedor de recursos de saudação para o qual os dados estão sendo coletados - Microsoft.RecoveryServices |
| ResourceType |Texto |Este campo representa o tipo de recurso de saudação para o qual os dados estão sendo coletados - cofres |

### <a name="policyassociation"></a>PolicyAssociation
Esta tabela fornece detalhes sobre associações de políticas com várias entidades.

| Campo | Tipo de Dados | Descrição |
| --- | --- | --- |
| EventName_s |Texto |Este campo representa o nome desse evento, é sempre AzureBackupCentralReport |
| SchemaVersion_s |Texto |Este campo indica a versão atual do esquema de hello, é **V1** |
| State_s |Texto |Estado atual do objeto de diretiva de hello, por exemplo, ativo, excluídos |
| BackupManagementType_s |Texto |Tipo de provedor para executar o backup, por exemplo, IaaSVM, toowhich FileFolder esta política pertence muito|
| OperationName |Texto |Este campo representa o nome da operação atual de saudação - PolicyAssociation |
| Categoria |Texto |Este campo representa a categoria de dados de diagnóstico enviados por push tooLog análise, é AzureBackupReport |
| Recurso |Texto |Este é o recurso Olá para o qual os dados estão sendo coletados, ele mostra o nome do Cofre de serviços de recuperação |
| PolicyUniqueId_g |Texto |Política de saudação do tooidentify Id exclusiva |
| VaultUniqueId_s |Texto |Id exclusiva da saudação cofre toowhich que esta política pertence muito|
| SourceSystem |Texto |Sistema de fonte de dados atual da saudação - Azure |
| ResourceId |Texto |Este campo representa o ID do recurso para o qual os dados estão sendo coletados, ele mostra o ID do recurso do cofre dos Serviços de Recuperação |
| SubscriptionId |Texto |Este campo representa a id de assinatura do recurso de saudação (RS cofre) para o qual os dados estão sendo coletados |
| ResourceGroup |Texto |Este campo representa o grupo de recursos do recurso de saudação (RS cofre) para o qual os dados estão sendo coletados |
| ResourceProvider |Texto |Este campo representa o provedor de recursos de saudação para o qual os dados estão sendo coletados - Microsoft.RecoveryServices |
| ResourceType |Texto |Este campo representa o tipo de recurso de saudação para o qual os dados estão sendo coletados - cofres |

### <a name="protectedserver"></a>ProtectedServer
Esta tabela fornece detalhes sobre campos protegidos relacionados ao servidor protegido.

| Campo | Tipo de Dados | Descrição |
| --- | --- | --- |
| EventName_s |Texto |Este campo representa o nome desse evento, é sempre AzureBackupCentralReport |
| ProtectedServerName_s |Texto |Nome do servidor protegido |
| SchemaVersion_s |Texto |Este campo indica a versão atual do esquema de hello, é **V1** |
| State_s |Texto |Estado atual da saudação protegido por objeto de servidor, por exemplo, ativo, excluídos |
| BackupManagementType_s |Texto |Tipo de provedor para executar o backup, por exemplo, IaaSVM, toowhich FileFolder deste servidor protegido pertence muito|
| OperationName |Texto |Este campo representa o nome da operação atual de saudação - ProtectedServer |
| Categoria |Texto |Este campo representa a categoria de dados de diagnóstico enviados por push tooLog análise, é AzureBackupReport |
| Recurso |Texto |Este é o recurso Olá para o qual os dados estão sendo coletados, ele mostra o nome do Cofre de serviços de recuperação |
| ProtectedServerUniqueId_s |Texto |Id exclusiva da saudação protegido por servidor |
| RegisteredContainerId_s |Texto |ID do contêiner registrado para backup |
| ProtectedServerType_s |Texto |Tipo de servidor protegido do backup, por exemplo, Windows |
| ProtectedServerFriendlyName_s |Texto |Nome amigável do servidor protegido |
| AzureBackupAgentVersion_s |Texto |Número de versão da versão de Backup do Agente |
| SourceSystem |Texto |Sistema de fonte de dados atual da saudação - Azure |
| ResourceId |Texto |Este campo representa o ID do recurso para o qual os dados estão sendo coletados, ele mostra o ID do recurso do cofre dos Serviços de Recuperação |
| SubscriptionId |Texto |Este campo representa a id de assinatura do recurso de saudação (RS cofre) para o qual os dados estão sendo coletados |
| ResourceGroup |Texto |Este campo representa o grupo de recursos do recurso de saudação (RS cofre) para o qual os dados estão sendo coletados |
| ResourceProvider |Texto |Este campo representa o provedor de recursos de saudação para o qual os dados estão sendo coletados - Microsoft.RecoveryServices |
| ResourceType |Texto |Este campo representa o tipo de recurso de saudação para o qual os dados estão sendo coletados - cofres |

### <a name="protectedserverassociation"></a>ProtectedServerAssociation
Esta tabela fornece detalhes sobre associações de servidores protegidos com outras entidades.

| Campo | Tipo de Dados | Descrição |
| --- | --- | --- |
| EventName_s |Texto |Este campo representa o nome desse evento, é sempre AzureBackupCentralReport |
| SchemaVersion_s |Texto |Este campo indica a versão atual do esquema de hello, é **V1** |
| State_s |Texto |Estado atual da saudação protegido por objeto de associação do servidor, por exemplo, ativo, excluídos |
| BackupManagementType_s |Texto |Tipo de provedor para executar o backup, por exemplo, IaaSVM, toowhich FileFolder deste servidor protegido pertence muito|
| OperationName |Texto |Este campo representa o nome da operação atual de saudação - ProtectedServerAssociation |
| Categoria |Texto |Este campo representa a categoria de dados de diagnóstico enviados por push tooLog análise, é AzureBackupReport |
| Recurso |Texto |Este é o recurso Olá para o qual os dados estão sendo coletados, ele mostra o nome do Cofre de serviços de recuperação |
| ProtectedServerUniqueId_s |Texto |Id exclusiva da saudação protegido por servidor |
| VaultUniqueId_s |Texto |Id exclusiva da saudação cofre toowhich que deste servidor protegido pertence muito|
| SourceSystem |Texto |Sistema de fonte de dados atual da saudação - Azure |
| ResourceId |Texto |Este campo representa o ID do recurso para o qual os dados estão sendo coletados, ele mostra o ID do recurso do cofre dos Serviços de Recuperação |
| SubscriptionId |Texto |Este campo representa a id de assinatura do recurso de saudação (RS cofre) para o qual os dados estão sendo coletados |
| ResourceGroup |Texto |Este campo representa o grupo de recursos do recurso de saudação (RS cofre) para o qual os dados estão sendo coletados |
| ResourceProvider |Texto |Este campo representa o provedor de recursos de saudação para o qual os dados estão sendo coletados - Microsoft.RecoveryServices |
| ResourceType |Texto |Este campo representa o tipo de recurso de saudação para o qual os dados estão sendo coletados - cofres |

### <a name="storage"></a>Armazenamento
Esta tabela fornece detalhes sobre campos relacionados ao armazenamento.

| Campo | Tipo de Dados | Descrição |
| --- | --- | --- |
| CloudStorageInBytes_s |Número decimal |Armazenamento de backup na nuvem usado por backups, calculado baseado no valor mais recente |
| ProtectedInstances_s |Número decimal |Número de instâncias protegidas utilizadas para calcular o armazenamento de front-end na cobrança, calculada baseada no valor mais recente |
| EventName_s |Texto |Este campo representa o nome desse evento, é sempre AzureBackupCentralReport |
| SchemaVersion_s |Texto |Este campo indica a versão atual do esquema de hello, é **V1** |
| State_s |Texto |Estado atual do objeto de armazenamento hello, por exemplo, ativo, excluídos |
| BackupManagementType_s |Texto |Tipo de provedor para executar o backup, por exemplo, IaaSVM, toowhich FileFolder esse armazenamento muito pertence|
| OperationName |Texto |Este campo representa o nome da operação atual de saudação - armazenamento |
| Categoria |Texto |Este campo representa a categoria de dados de diagnóstico enviados por push tooLog análise, é AzureBackupReport |
| Recurso |Texto |Este é o recurso Olá para o qual os dados estão sendo coletados, ele mostra o nome do Cofre de serviços de recuperação |
| ProtectedServerUniqueId_s |Texto |Id exclusiva da saudação protegidos para que o armazenamento é calculado de servidor |
| VaultUniqueId_s |Texto |Id exclusiva do cofre Olá para o armazenamento é calculado |
| SourceSystem |Texto |Sistema de fonte de dados atual da saudação - Azure |
| ResourceId |Texto |Este campo representa o ID do recurso para o qual os dados estão sendo coletados, ele mostra o ID do recurso do cofre dos Serviços de Recuperação |
| SubscriptionId |Texto |Este campo representa a id de assinatura do recurso de saudação (RS cofre) para o qual os dados estão sendo coletados |
| ResourceGroup |Texto |Este campo representa o grupo de recursos do recurso de saudação (RS cofre) para o qual os dados estão sendo coletados |
| ResourceProvider |Texto |Este campo representa o provedor de recursos de saudação para o qual os dados estão sendo coletados - Microsoft.RecoveryServices |
| ResourceType |Texto |Representse esse campo tipo de recurso de saudação para o qual os dados estão sendo coletados - cofres |

### <a name="vault"></a>Cofre
Esta tabela fornece detalhes sobre campos relacionados ao cofre.

| Campo | Tipo de Dados | Descrição |
| --- | --- | --- |
| EventName_s |Texto |Este campo representa o nome desse evento, é sempre AzureBackupCentralReport |
| SchemaVersion_s |Texto |Este campo indica a versão atual do esquema de hello, é **V1** |
| State_s |Texto |Estado atual do objeto de cofre hello, por exemplo, ativo, excluídos |
| OperationName |Texto |Este campo representa o nome da operação atual de saudação - cofre |
| Categoria |Texto |Este campo representa a categoria de dados de diagnóstico enviados por push tooLog análise, é AzureBackupReport |
| Recurso |Texto |Este é o recurso Olá para o qual os dados estão sendo coletados, ele mostra o nome do Cofre de serviços de recuperação |
| VaultUniqueId_s |Texto |Id exclusiva do cofre Olá |
| VaultName_s |Texto |Nome do cofre Olá |
| AzureDataCenter_s |Texto |Data center onde o cofre está localizado |
| StorageReplicationType_s |Texto |Tipo de replicação de armazenamento para o cofre hello, por exemplo, GeoRedundant |
| SourceSystem |Texto |Sistema de fonte de dados atual da saudação - Azure |
| ResourceId |Texto |Este campo representa o ID do recurso para o qual os dados estão sendo coletados, ele mostra o ID do recurso do cofre dos Serviços de Recuperação |
| SubscriptionId |Texto |Este campo representa a id de assinatura do recurso de saudação (RS cofre) para o qual os dados estão sendo coletados |
| ResourceGroup |Texto |Este campo representa o grupo de recursos do recurso de saudação (RS cofre) para o qual os dados estão sendo coletados |
| ResourceProvider |Texto |Este campo representa o provedor de recursos de saudação para o qual os dados estão sendo coletados - Microsoft.RecoveryServices |
| ResourceType |Texto |Este campo representa o tipo de recurso de saudação para o qual os dados estão sendo coletados - cofres |

## <a name="next-steps"></a>Próximas etapas
Depois de examinar o modelo de dados de saudação para criação de relatórios de Backup do Azure, você pode iniciar [criando painel](../log-analytics/log-analytics-dashboards.md) na análise de Log e o OMS.
