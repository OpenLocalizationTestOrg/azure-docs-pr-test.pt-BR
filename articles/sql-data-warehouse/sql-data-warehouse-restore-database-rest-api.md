---
title: aaaRestore um Data Warehouse do SQL Azure (API REST) | Microsoft Docs
description: Tarefas da API REST para restaurar um Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: fca922c6-b675-49c7-907e-5dcf26d451dd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: cf6678d71aafff71b1ea715f447e41e25f20d1b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-data-warehouse-rest-api"></a>Recuperar um SQL Data Warehouse do Azure (API REST)
> [!div class="op_single_selector"]
> * [Visão geral][Overview]
> * [Portal][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
> 
> 

Neste artigo, você aprenderá como toorestore um usando o Azure SQL Data Warehouse Olá API REST.

## <a name="before-you-begin"></a>Antes de começar
**Verifique sua capacidade de DTU.** Cada SQL Data Warehouse é hospedado por um servidor SQL (por exemplo, myserver.database.windows.net) que tem uma cota de DTU padrão.  Antes de poder restaurar um SQL Data Warehouse, verifique se esse saudação que do SQL server tem suficiente restante cota de DTU para o banco de dados de hello está sendo restaurado. toolearn como toocalculate DTU necessário ou toorequest mais DTU, consulte [solicitar uma alteração de cota DTU][Request a DTU quota change].

## <a name="restore-an-active-or-paused-database"></a>Restaurar um banco de dados ativo ou pausado
toorestore um banco de dados:

1. Obter lista de saudação de pontos de restauração do banco de dados usando a operação de pontos de restauração do banco de dados de Get hello.
2. Iniciar a restauração usando Olá [criar solicitação de restauração de banco de dados] [ Create database restore request] operação.
3. Acompanhar o status de saudação de sua restauração usando Olá [status da operação de banco de dados] [ Database operation status] operação.

> [!NOTE]
> Após a restauração hello, você pode configurar o banco de dados recuperado seguindo [configurar seu banco de dados após a recuperação][Configure your database after recovery].
> 
> 

## <a name="restore-a-deleted-database"></a>Restaurar um banco de dados excluído
toorestore um banco de dados excluído:

1. Listar todos os seus bancos de dados excluídos restauráveis usando Olá [bancos de dados de lista restaurável descartados] [ List restorable dropped databases] operação.
2. Obter os detalhes de saudação para Olá excluído banco de dados toorestore usando Olá [Get restaurável descartado banco de dados] [ Get restorable dropped database] operação.
3. Iniciar a restauração usando Olá [criar solicitação de restauração de banco de dados] [ Create database restore request] operação.
4. Acompanhar o status de saudação de sua restauração usando Olá [status da operação de banco de dados] [ Database operation status] operação.

> [!NOTE]
> tooconfigure seu banco de dados após a restauração hello, consulte [configurar seu banco de dados após a recuperação][Configure your database after recovery].
> 
> 

## <a name="next-steps"></a>Próximas etapas
toolearn sobre recursos de continuidade de negócios Olá de edições de banco de dados de SQL do Azure, leia Olá [visão geral de continuidade de negócios do Azure SQL Database][Azure SQL Database business continuity overview].

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->
[Create database restore request]: https://msdn.microsoft.com/library/azure/dn509571.aspx
[Database operation status]: https://msdn.microsoft.com/library/azure/dn720371.aspx
[Get restorable dropped database]: https://msdn.microsoft.com/library/azure/dn509574.aspx
[List restorable dropped databases]: https://msdn.microsoft.com/library/azure/dn509562.aspx
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
