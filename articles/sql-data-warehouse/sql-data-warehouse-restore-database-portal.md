---
title: aaaRestore Azure SQL Data Warehouse (portal do Azure) | Microsoft Docs
description: "Tarefas do Portal do Azure para a restauração de um SQL Data Warehouse do Azure."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: barbkess
editor: 
ms.assetid: b0aef539-7657-4b0e-9899-74098f5c21bc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 09/21/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: cb225d2a21b61acab70a51b69c266f8d3ffacc9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-azure-sql-data-warehouse-portal"></a>Restaurar SQL Data Warehouse do Azure (Portal)
> [!div class="op_single_selector"]
> * [Visão geral][Overview]
> * [Portal][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
>
>
Neste artigo, você aprenderá como toorestore Azure SQL Data Warehouse usando Olá portal do Azure.

## <a name="before-you-begin"></a>Antes de começar
**Verifique sua capacidade de DTU.** Cada instância do SQL Data Warehouse é hospedada por um SQL Server (por exemplo, myserver.database.windows.net) que tem uma cota DTU (Unidade de Transmissão de Dados) padrão. Antes de poder restaurar SQL Data Warehouse, verifique se o SQL server tem suficiente restante cota de DTU para o banco de dados de saudação que você está restaurando. toolearn como cota de DTU toocalculate ou toorequest mais DTUs, consulte [solicitar uma alteração de cota DTU][Request a DTU quota change].

## <a name="restore-an-active-or-paused-database"></a>Restaurar um banco de dados ativo ou pausado
toorestore um banco de dados:

1. Entrar toohello [portal do Azure][Azure portal].
2. No painel esquerdo do hello, selecione **procurar**e, em seguida, selecione **servidores SQL**.

    ![Selecione Procurar > servidores SQL](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. Localize o servidor e, em seguida, selecione-o.

    ![Selecione seu servidor](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. Localize a instância de saudação do SQL Data Warehouse que você deseja toorestore do e, em seguida, selecione.

    ![Selecionar instância de saudação do SQL Data Warehouse toorestore](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. Na parte superior de saudação da folha de Data Warehouse hello, selecione **restauração**.

    ![Selecione Restaurar](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. Especifique um novo **Nome de banco de dados**.
7. Selecione hello mais recente **ponto de restauração**.

   Certifique-se de que escolher o ponto de restauração mais recente da saudação. Como pontos de restauração são mostrados no tempo Universal Coordenado (UTC), a opção de padrão de Olá não pode ser ponto de restauração mais recente da saudação.

      ![Selecione um ponto de restauração](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. Selecione **OK**.
9. processo de restauração de banco de dados de saudação será iniciado e você pode usar **notificações** toomonitor processo de saudação.

> [!NOTE]
> Após a restauração hello, você pode configurar o banco de dados recuperado seguindo [configurar seu banco de dados após a recuperação][Configure your database after recovery].
>
>

## <a name="restore-a-deleted-database"></a>Restaurar um banco de dados excluído
toorestore um banco de dados excluído:

1. Entrar toohello [portal do Azure][Azure portal].
2. No painel esquerdo do hello, selecione **procurar**e, em seguida, selecione **servidores SQL**.

    ![Selecione Procurar > servidores SQL](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. Localize o servidor e, em seguida, selecione-o.

    ![Selecione seu servidor](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. Role para baixo toohello **operações** seção na folha do seu servidor.
5. Selecione Olá **bancos de dados excluídos** lado a lado.

    ![Selecione Bloco de bancos de dados excluídos Olá](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. Selecione Olá excluído o banco de dados que você deseja toorestore.

    ![Selecione um banco de dados toorestore](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. Especifique um novo **Nome de banco de dados**.

    ![Adicionar um nome para o banco de dados de saudação](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. Selecione **OK**.
9. processo de restauração de banco de dados de saudação será iniciado e você pode usar **notificações** toomonitor processo de saudação.

> [!NOTE]
> tooconfigure seu banco de dados após a restauração hello, consulte [configurar seu banco de dados após a recuperação][Configure your database after recovery].
>
>

## <a name="next-steps"></a>Próximas etapas
toolearn sobre recursos de continuidade de negócios Olá de edições de banco de dados SQL, ler Olá [visão geral de continuidade de negócios do Azure SQL Database][Azure SQL Database business continuity overview].

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change

<!--MSDN references-->

<!--Blog references-->

<!--Other Web references-->
[Azure portal]: https://portal.azure.com/
