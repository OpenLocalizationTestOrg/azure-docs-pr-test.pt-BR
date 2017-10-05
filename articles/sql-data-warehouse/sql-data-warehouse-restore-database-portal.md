---
title: Restaurar SQL Data Warehouse do Azure (Portal do Azure) | Microsoft Docs
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
ms.openlocfilehash: f6bc8671410dc7015a8d2a4bea1ba11f9ae526c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="restore-azure-sql-data-warehouse-portal"></a><span data-ttu-id="bd8c0-103">Restaurar SQL Data Warehouse do Azure (Portal)</span><span class="sxs-lookup"><span data-stu-id="bd8c0-103">Restore Azure SQL Data Warehouse (portal)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="bd8c0-104">[Visão geral][Overview]</span><span class="sxs-lookup"><span data-stu-id="bd8c0-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="bd8c0-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="bd8c0-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="bd8c0-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="bd8c0-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="bd8c0-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="bd8c0-107">[REST][REST]</span></span>
>
>
<span data-ttu-id="bd8c0-108">Neste artigo, você aprenderá como restaurar o SQL Data Warehouse do Azure usando o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bd8c0-108">In this article, you will learn how to restore Azure SQL Data Warehouse by using the Azure portal.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bd8c0-109">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="bd8c0-109">Before you begin</span></span>
<span data-ttu-id="bd8c0-110">**Verifique sua capacidade de DTU.**</span><span class="sxs-lookup"><span data-stu-id="bd8c0-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="bd8c0-111">Cada instância do SQL Data Warehouse é hospedada por um SQL Server (por exemplo, myserver.database.windows.net) que tem uma cota DTU (Unidade de Transmissão de Dados) padrão.</span><span class="sxs-lookup"><span data-stu-id="bd8c0-111">Each instance of SQL Data Warehouse is hosted by a SQL server (for example, myserver.database.windows.net) which has a default data throughput unit (DTU) quota.</span></span> <span data-ttu-id="bd8c0-112">Antes de restaurar o SQL Data Warehouse, verifique se o SQL Server tem cota de DTU suficiente restante para o banco de dados que você está restaurando.</span><span class="sxs-lookup"><span data-stu-id="bd8c0-112">Before you can restore SQL Data Warehouse, verify that your SQL server has enough remaining DTU quota for the database that you're restoring.</span></span> <span data-ttu-id="bd8c0-113">Para saber como calcular a cota de DTU ou para solicitar mais DTUs, veja [Solicitar uma alteração de cota de DTU][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="bd8c0-113">To learn how to calculate DTU quota or to request more DTUs, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="bd8c0-114">Restaurar um banco de dados ativo ou pausado</span><span class="sxs-lookup"><span data-stu-id="bd8c0-114">Restore an active or paused database</span></span>
<span data-ttu-id="bd8c0-115">Para restaurar um banco de dados:</span><span class="sxs-lookup"><span data-stu-id="bd8c0-115">To restore a database:</span></span>

1. <span data-ttu-id="bd8c0-116">Entre no [Portal do Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="bd8c0-116">Sign in to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="bd8c0-117">No painel esquerdo, selecione **Procurar** e, em seguida, selecione **Servidores SQL**.</span><span class="sxs-lookup"><span data-stu-id="bd8c0-117">In the left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Selecione Procurar > servidores SQL](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="bd8c0-119">Localize o servidor e, em seguida, selecione-o.</span><span class="sxs-lookup"><span data-stu-id="bd8c0-119">Find your server, and then select it.</span></span>

    ![Selecione seu servidor](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. <span data-ttu-id="bd8c0-121">Localize a instância do SQL Data Warehouse da qual você quer restaurar e selecione-a.</span><span class="sxs-lookup"><span data-stu-id="bd8c0-121">Find the instance of SQL Data Warehouse that you want to restore from, and then select it.</span></span>

    ![Selecione a instância do SQL Data Warehouse para restaurar](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. <span data-ttu-id="bd8c0-123">Na parte superior da folha Data Warehouse, selecione **Restaurar**.</span><span class="sxs-lookup"><span data-stu-id="bd8c0-123">At the top of the Data Warehouse blade, select **Restore**.</span></span>

    ![Selecione Restaurar](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. <span data-ttu-id="bd8c0-125">Especifique um novo **Nome de banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="bd8c0-125">Specify a new **Database name**.</span></span>
7. <span data-ttu-id="bd8c0-126">Selecione o **Ponto de restauração** mais recente.</span><span class="sxs-lookup"><span data-stu-id="bd8c0-126">Select the latest **Restore point**.</span></span>

   <span data-ttu-id="bd8c0-127">Certifique-se de escolher o ponto de restauração mais recente.</span><span class="sxs-lookup"><span data-stu-id="bd8c0-127">Make sure you choose the latest restore point.</span></span> <span data-ttu-id="bd8c0-128">Como os pontos de restauração são mostrados em Hora Universal Coordenada (UTC), a opção padrão poderá não ser o ponto de restauração mais recente.</span><span class="sxs-lookup"><span data-stu-id="bd8c0-128">Because restore points are shown in Coordinated Universal Time (UTC), the default option might not be the latest restore point.</span></span>

      ![Selecione um ponto de restauração](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. <span data-ttu-id="bd8c0-130">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="bd8c0-130">Select **OK**.</span></span>
9. <span data-ttu-id="bd8c0-131">O processo de restauração de banco de dados será iniciado e você poderá usar as **NOTIFICAÇÕES** para monitorar o processo.</span><span class="sxs-lookup"><span data-stu-id="bd8c0-131">The database restore process will begin, and you can use **NOTIFICATIONS** to monitor the process.</span></span>

> [!NOTE]
> <span data-ttu-id="bd8c0-132">Depois que a restauração estiver concluída, você poderá configurar o banco de dados recuperado seguindo [Configurar o banco de dados após a recuperação][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="bd8c0-132">After the restore has finished, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="restore-a-deleted-database"></a><span data-ttu-id="bd8c0-133">Restaurar um banco de dados excluído</span><span class="sxs-lookup"><span data-stu-id="bd8c0-133">Restore a deleted database</span></span>
<span data-ttu-id="bd8c0-134">Para restaurar um banco de dados excluído:</span><span class="sxs-lookup"><span data-stu-id="bd8c0-134">To restore a deleted database:</span></span>

1. <span data-ttu-id="bd8c0-135">Entre no [Portal do Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="bd8c0-135">Sign in to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="bd8c0-136">No painel esquerdo, selecione **Procurar** e, em seguida, selecione **Servidores SQL**.</span><span class="sxs-lookup"><span data-stu-id="bd8c0-136">In the left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Selecione Procurar > servidores SQL](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="bd8c0-138">Localize o servidor e, em seguida, selecione-o.</span><span class="sxs-lookup"><span data-stu-id="bd8c0-138">Find your server, and then select it.</span></span>

    ![Selecione seu servidor](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. <span data-ttu-id="bd8c0-140">Role para baixo até a seção **Operações** na folha do seu servidor.</span><span class="sxs-lookup"><span data-stu-id="bd8c0-140">Scroll down to the **Operations** section on your server's blade.</span></span>
5. <span data-ttu-id="bd8c0-141">Selecione o bloco **Bancos de Dados excluídos**.</span><span class="sxs-lookup"><span data-stu-id="bd8c0-141">Select the **Deleted databases** tile.</span></span>

    ![Selecione o bloco Bancos de Dados excluídos](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. <span data-ttu-id="bd8c0-143">Selecione o banco de dados excluído que você deseja restaurar.</span><span class="sxs-lookup"><span data-stu-id="bd8c0-143">Select the deleted database that you want to restore.</span></span>

    ![Selecionar um banco de dados para ser restaurado](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. <span data-ttu-id="bd8c0-145">Especifique um novo **Nome de banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="bd8c0-145">Specify a new **Database name**.</span></span>

    ![Adicione um nome para o banco de dados](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. <span data-ttu-id="bd8c0-147">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="bd8c0-147">Select **OK**.</span></span>
9. <span data-ttu-id="bd8c0-148">O processo de restauração de banco de dados será iniciado e você poderá usar as **NOTIFICAÇÕES** para monitorar o processo.</span><span class="sxs-lookup"><span data-stu-id="bd8c0-148">The database restore process will begin, and you can use **NOTIFICATIONS** to monitor the process.</span></span>

> [!NOTE]
> <span data-ttu-id="bd8c0-149">Para configurar o banco de dados após a conclusão da restauração, consulte [Configurar o banco de dados após a recuperação][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="bd8c0-149">To configure your database after the restore has finished, see [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="bd8c0-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bd8c0-150">Next steps</span></span>
<span data-ttu-id="bd8c0-151">Para saber mais sobre os recursos de continuidade dos negócios das edições do Banco de Dados SQL do Azure, leia a [Visão geral da continuidade dos negócios do Banco de Dados SQL do Azure][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="bd8c0-151">To learn about the business continuity features of Azure SQL Database editions, read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

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
