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
# <a name="restore-azure-sql-data-warehouse-portal"></a><span data-ttu-id="3653b-103">Restaurar SQL Data Warehouse do Azure (Portal)</span><span class="sxs-lookup"><span data-stu-id="3653b-103">Restore Azure SQL Data Warehouse (portal)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="3653b-104">[Visão geral][Overview]</span><span class="sxs-lookup"><span data-stu-id="3653b-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="3653b-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="3653b-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="3653b-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="3653b-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="3653b-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="3653b-107">[REST][REST]</span></span>
>
>
<span data-ttu-id="3653b-108">Neste artigo, você aprenderá como toorestore Azure SQL Data Warehouse usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3653b-108">In this article, you will learn how toorestore Azure SQL Data Warehouse by using hello Azure portal.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3653b-109">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="3653b-109">Before you begin</span></span>
<span data-ttu-id="3653b-110">**Verifique sua capacidade de DTU.**</span><span class="sxs-lookup"><span data-stu-id="3653b-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="3653b-111">Cada instância do SQL Data Warehouse é hospedada por um SQL Server (por exemplo, myserver.database.windows.net) que tem uma cota DTU (Unidade de Transmissão de Dados) padrão.</span><span class="sxs-lookup"><span data-stu-id="3653b-111">Each instance of SQL Data Warehouse is hosted by a SQL server (for example, myserver.database.windows.net) which has a default data throughput unit (DTU) quota.</span></span> <span data-ttu-id="3653b-112">Antes de poder restaurar SQL Data Warehouse, verifique se o SQL server tem suficiente restante cota de DTU para o banco de dados de saudação que você está restaurando.</span><span class="sxs-lookup"><span data-stu-id="3653b-112">Before you can restore SQL Data Warehouse, verify that your SQL server has enough remaining DTU quota for hello database that you're restoring.</span></span> <span data-ttu-id="3653b-113">toolearn como cota de DTU toocalculate ou toorequest mais DTUs, consulte [solicitar uma alteração de cota DTU][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="3653b-113">toolearn how toocalculate DTU quota or toorequest more DTUs, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="3653b-114">Restaurar um banco de dados ativo ou pausado</span><span class="sxs-lookup"><span data-stu-id="3653b-114">Restore an active or paused database</span></span>
<span data-ttu-id="3653b-115">toorestore um banco de dados:</span><span class="sxs-lookup"><span data-stu-id="3653b-115">toorestore a database:</span></span>

1. <span data-ttu-id="3653b-116">Entrar toohello [portal do Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="3653b-116">Sign in toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="3653b-117">No painel esquerdo do hello, selecione **procurar**e, em seguida, selecione **servidores SQL**.</span><span class="sxs-lookup"><span data-stu-id="3653b-117">In hello left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Selecione Procurar > servidores SQL](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="3653b-119">Localize o servidor e, em seguida, selecione-o.</span><span class="sxs-lookup"><span data-stu-id="3653b-119">Find your server, and then select it.</span></span>

    ![Selecione seu servidor](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. <span data-ttu-id="3653b-121">Localize a instância de saudação do SQL Data Warehouse que você deseja toorestore do e, em seguida, selecione.</span><span class="sxs-lookup"><span data-stu-id="3653b-121">Find hello instance of SQL Data Warehouse that you want toorestore from, and then select it.</span></span>

    ![Selecionar instância de saudação do SQL Data Warehouse toorestore](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. <span data-ttu-id="3653b-123">Na parte superior de saudação da folha de Data Warehouse hello, selecione **restauração**.</span><span class="sxs-lookup"><span data-stu-id="3653b-123">At hello top of hello Data Warehouse blade, select **Restore**.</span></span>

    ![Selecione Restaurar](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. <span data-ttu-id="3653b-125">Especifique um novo **Nome de banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="3653b-125">Specify a new **Database name**.</span></span>
7. <span data-ttu-id="3653b-126">Selecione hello mais recente **ponto de restauração**.</span><span class="sxs-lookup"><span data-stu-id="3653b-126">Select hello latest **Restore point**.</span></span>

   <span data-ttu-id="3653b-127">Certifique-se de que escolher o ponto de restauração mais recente da saudação.</span><span class="sxs-lookup"><span data-stu-id="3653b-127">Make sure you choose hello latest restore point.</span></span> <span data-ttu-id="3653b-128">Como pontos de restauração são mostrados no tempo Universal Coordenado (UTC), a opção de padrão de Olá não pode ser ponto de restauração mais recente da saudação.</span><span class="sxs-lookup"><span data-stu-id="3653b-128">Because restore points are shown in Coordinated Universal Time (UTC), hello default option might not be hello latest restore point.</span></span>

      ![Selecione um ponto de restauração](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. <span data-ttu-id="3653b-130">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="3653b-130">Select **OK**.</span></span>
9. <span data-ttu-id="3653b-131">processo de restauração de banco de dados de saudação será iniciado e você pode usar **notificações** toomonitor processo de saudação.</span><span class="sxs-lookup"><span data-stu-id="3653b-131">hello database restore process will begin, and you can use **NOTIFICATIONS** toomonitor hello process.</span></span>

> [!NOTE]
> <span data-ttu-id="3653b-132">Após a restauração hello, você pode configurar o banco de dados recuperado seguindo [configurar seu banco de dados após a recuperação][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="3653b-132">After hello restore has finished, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="restore-a-deleted-database"></a><span data-ttu-id="3653b-133">Restaurar um banco de dados excluído</span><span class="sxs-lookup"><span data-stu-id="3653b-133">Restore a deleted database</span></span>
<span data-ttu-id="3653b-134">toorestore um banco de dados excluído:</span><span class="sxs-lookup"><span data-stu-id="3653b-134">toorestore a deleted database:</span></span>

1. <span data-ttu-id="3653b-135">Entrar toohello [portal do Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="3653b-135">Sign in toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="3653b-136">No painel esquerdo do hello, selecione **procurar**e, em seguida, selecione **servidores SQL**.</span><span class="sxs-lookup"><span data-stu-id="3653b-136">In hello left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Selecione Procurar > servidores SQL](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="3653b-138">Localize o servidor e, em seguida, selecione-o.</span><span class="sxs-lookup"><span data-stu-id="3653b-138">Find your server, and then select it.</span></span>

    ![Selecione seu servidor](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. <span data-ttu-id="3653b-140">Role para baixo toohello **operações** seção na folha do seu servidor.</span><span class="sxs-lookup"><span data-stu-id="3653b-140">Scroll down toohello **Operations** section on your server's blade.</span></span>
5. <span data-ttu-id="3653b-141">Selecione Olá **bancos de dados excluídos** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="3653b-141">Select hello **Deleted databases** tile.</span></span>

    ![Selecione Bloco de bancos de dados excluídos Olá](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. <span data-ttu-id="3653b-143">Selecione Olá excluído o banco de dados que você deseja toorestore.</span><span class="sxs-lookup"><span data-stu-id="3653b-143">Select hello deleted database that you want toorestore.</span></span>

    ![Selecione um banco de dados toorestore](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. <span data-ttu-id="3653b-145">Especifique um novo **Nome de banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="3653b-145">Specify a new **Database name**.</span></span>

    ![Adicionar um nome para o banco de dados de saudação](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. <span data-ttu-id="3653b-147">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="3653b-147">Select **OK**.</span></span>
9. <span data-ttu-id="3653b-148">processo de restauração de banco de dados de saudação será iniciado e você pode usar **notificações** toomonitor processo de saudação.</span><span class="sxs-lookup"><span data-stu-id="3653b-148">hello database restore process will begin, and you can use **NOTIFICATIONS** toomonitor hello process.</span></span>

> [!NOTE]
> <span data-ttu-id="3653b-149">tooconfigure seu banco de dados após a restauração hello, consulte [configurar seu banco de dados após a recuperação][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="3653b-149">tooconfigure your database after hello restore has finished, see [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="3653b-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3653b-150">Next steps</span></span>
<span data-ttu-id="3653b-151">toolearn sobre recursos de continuidade de negócios Olá de edições de banco de dados SQL, ler Olá [visão geral de continuidade de negócios do Azure SQL Database][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="3653b-151">toolearn about hello business continuity features of Azure SQL Database editions, read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

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
