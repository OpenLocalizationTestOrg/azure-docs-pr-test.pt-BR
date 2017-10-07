---
title: exemplos de script do PowerShell aaaAzure para o banco de dados SQL | Microsoft Docs
description: "Azure PowerShell script exemplos toohelp criar e gerenciar servidores de banco de dados SQL, pools Elásticos, bancos de dados e firewalls."
services: sql-database
documentationcenter: sql-database
author: CarlRabeler
manager: jhubbard
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: overview-samples
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 1130ffb0e1c2b94c676d564ad5c4eb3b86374dbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-powershell-samples-for-azure-sql-database"></a>Amostras do Azure PowerShell para o Banco de Dados SQL do Azure

Olá tabela a seguir inclui links toosample Azure scripts do PowerShell para o banco de dados do SQL Azure.

| |  |
|---|---|
|**Criar um banco de dados individual e um pool elástico**||
| [Criar um Banco de Dados individual e configurar uma regra de firewall](scripts/sql-database-create-and-configure-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Este exemplo de script do PowerShell cria um Banco de Dados SQL do Azure e configura uma regra de firewall no nível do servidor. |
| [Criar pools Elásticos e mover bancos de dados em pools](scripts/sql-database-move-database-between-pools-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Este script do PowerShell cria pools elásticos do Banco de Dados SQL do Azure, move os bancos de dados em pool e altera os níveis de desempenho.|
|**Configurar a replicação geográfica e o failover**||
| [Configurar e fazer failover de um banco de dados individual usando replicação geográfica ativa](scripts/sql-database-setup-geodr-and-failover-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Este script do PowerShell configura a replicação geográfica ativa para um único banco de dados do SQL Azure e falha, ele pela réplica secundária toohello. |
| [Configurar e fazer failover de um banco de dados em pool usando replicação geográfica ativa](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Este script do PowerShell configura a replicação geográfica ativa para um banco de dados do SQL Azure em um pool Elástico do SQL e falha, ele pela réplica secundária toohello. |
| [Configurar e realizar o failover de um grupo de failover para um banco de dados individual (versão prévia)](scripts/sql-database-setup-geodr-failover-database-failover-group-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Este script do PowerShell configura um grupo de failover para uma instância de servidor de banco de dados SQL, adiciona um grupo de failover do banco de dados toohello e falhar, o servidor secundário toohello |
|**Dimensionar um banco de dados individual e um pool elástico**||
| [Dimensionar um banco de dados individual](scripts/sql-database-monitor-and-scale-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Este script do PowerShell monitora as métricas de desempenho de saudação de um banco de dados do SQL Azure, redimensiona tooa mais alto nível de desempenho e cria uma regra de alerta em uma saudação métricas de desempenho. |
| [Dimensionar um pool elástico](scripts/sql-database-monitor-and-scale-pool-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Este script do PowerShell monitora as métricas de desempenho de saudação de um pool Elástico de banco de dados SQL, redimensiona tooa mais alto nível de desempenho e cria uma regra de alerta em uma saudação métricas de desempenho.  |
| **Auditoria e detecção de ameaças** |
| [Configurar auditoria e detecção de ameaças](scripts/sql-database-auditing-and-threat-detection-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Esse script do PowerShell configura políticas de detecção de ameaças e auditoria para um Banco de Dados SQL do Azure. |
| **Restaurar, copiar e importar um banco de dados**||
| [Restaurar um banco de dados](scripts/sql-database-restore-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Este script do PowerShell restaura um banco de dados do SQL Azure de um backup com redundância geográfica e restaura um backup mais recente excluído do SQL Azure database toohello. |
| [Copiar de um servidor de banco de dados toonew](scripts/sql-database-copy-database-to-new-server-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Esse script do PowerShell cria uma cópia do Banco de Dados SQL do Azure existente em um novo Azure SQL Server. |
| [Importar um banco de dados de um arquivo bacpac](scripts/sql-database-import-from-bacpac-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Este script do PowerShell importa um banco de dados tooan do Azure do SQL server de um arquivo bacpac. |
| **Sincronizar dados entre bancos de dados**||
| [Sincronizar dados entre bancos de dados SQL](scripts/sql-database-sync-data-between-sql-databases.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Este script do PowerShell configura toosync de sincronização de dados entre vários bancos de dados do SQL Azure. |
| [Sincronizar dados entre o Banco de Dados SQL e o SQL Server local](scripts/sql-database-sync-data-between-azure-onprem.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Este script do PowerShell configura toosync de sincronização de dados entre um banco de dados do SQL Azure e um banco de dados do SQL Server local. |
|||
|||
