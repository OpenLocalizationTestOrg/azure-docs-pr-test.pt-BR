---
title: Restaurar um Azure SQL Data Warehouse (API REST) | Microsoft Docs
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
ms.openlocfilehash: 8656607611e7518e42b51b91774f55abec15c228
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="restore-an-azure-sql-data-warehouse-rest-api"></a><span data-ttu-id="7b96a-103">Recuperar um SQL Data Warehouse do Azure (API REST)</span><span class="sxs-lookup"><span data-stu-id="7b96a-103">Restore an Azure SQL Data Warehouse (REST API)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="7b96a-104">[Visão geral][Overview]</span><span class="sxs-lookup"><span data-stu-id="7b96a-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="7b96a-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="7b96a-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="7b96a-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="7b96a-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="7b96a-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="7b96a-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="7b96a-108">Neste artigo, você aprenderá como restaurar um Azure SQL Data Warehouse usando a API REST.</span><span class="sxs-lookup"><span data-stu-id="7b96a-108">In this article you will learn how to restore an Azure SQL Data Warehouse using the REST API.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7b96a-109">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="7b96a-109">Before you begin</span></span>
<span data-ttu-id="7b96a-110">**Verifique sua capacidade de DTU.**</span><span class="sxs-lookup"><span data-stu-id="7b96a-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="7b96a-111">Cada SQL Data Warehouse é hospedado por um servidor SQL (por exemplo, myserver.database.windows.net) que tem uma cota de DTU padrão.</span><span class="sxs-lookup"><span data-stu-id="7b96a-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="7b96a-112">Antes de restaurar um SQL Data Warehouse, verifique se o SQL Server tem cota de DTU suficiente restante para o banco de dados que está sendo restaurado.</span><span class="sxs-lookup"><span data-stu-id="7b96a-112">Before you can restore a SQL Data Warehouse, verify that the your SQL server has enough remaining DTU quota for the database being restored.</span></span> <span data-ttu-id="7b96a-113">Para saber como calcular a DTU necessária ou para solicitar mais DTU, veja [Solicitar uma alteração de cota de DTU][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="7b96a-113">To learn how to calculate DTU needed or to request more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="7b96a-114">Restaurar um banco de dados ativo ou pausado</span><span class="sxs-lookup"><span data-stu-id="7b96a-114">Restore an active or paused database</span></span>
<span data-ttu-id="7b96a-115">Para restaurar um banco de dados:</span><span class="sxs-lookup"><span data-stu-id="7b96a-115">To restore a database:</span></span>

1. <span data-ttu-id="7b96a-116">Obtenha a lista de pontos de restauração do banco de dados usando a operação de obtenção de pontos de restauração de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="7b96a-116">Get the list of database restore points using the Get Database Restore Points operation.</span></span>
2. <span data-ttu-id="7b96a-117">Comece sua restauração usando a operação [Criar solicitação de restauração de banco de dados][Create database restore request].</span><span class="sxs-lookup"><span data-stu-id="7b96a-117">Begin your restore by using the [Create database restore request][Create database restore request] operation.</span></span>
3. <span data-ttu-id="7b96a-118">Acompanhe o status de sua restauração usando a operação [Status da operação de banco de dados][Database operation status].</span><span class="sxs-lookup"><span data-stu-id="7b96a-118">Track the status of your restore by using the [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="7b96a-119">Depois que a restauração estiver concluída, você poderá configurar o banco de dados recuperado seguindo [Configurar o banco de dados após a recuperação][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="7b96a-119">After the restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="7b96a-120">Restaurar um banco de dados excluído</span><span class="sxs-lookup"><span data-stu-id="7b96a-120">Restore a deleted database</span></span>
<span data-ttu-id="7b96a-121">Para restaurar um banco de dados excluído:</span><span class="sxs-lookup"><span data-stu-id="7b96a-121">To restore a deleted database:</span></span>

1. <span data-ttu-id="7b96a-122">Liste todos os bancos de dados excluídos restauráveis usando a operação [Listar bancos de dados descartados restauráveis][List restorable dropped databases].</span><span class="sxs-lookup"><span data-stu-id="7b96a-122">List all of your restorable deleted databases by using the [List restorable dropped databases][List restorable dropped databases] operation.</span></span>
2. <span data-ttu-id="7b96a-123">Obtenha os detalhes do banco de dados excluído que deseja restaurar usando a operação [Obter banco de dados descartados restauráveis][Get restorable dropped database].</span><span class="sxs-lookup"><span data-stu-id="7b96a-123">Get the details for the deleted database you want to restore by using the [Get restorable dropped database][Get restorable dropped database] operation.</span></span>
3. <span data-ttu-id="7b96a-124">Comece sua restauração usando a operação [Criar solicitação de restauração de banco de dados][Create database restore request].</span><span class="sxs-lookup"><span data-stu-id="7b96a-124">Begin your restore by using the [Create database restore request][Create database restore request] operation.</span></span>
4. <span data-ttu-id="7b96a-125">Acompanhe o status de sua restauração usando a operação [Status da operação de banco de dados][Database operation status].</span><span class="sxs-lookup"><span data-stu-id="7b96a-125">Track the status of your restore by using the [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="7b96a-126">Para configurar o banco de dados após a conclusão da restauração, veja [Configurar o banco de dados após a recuperação][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="7b96a-126">To configure your database after the restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="7b96a-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7b96a-127">Next steps</span></span>
<span data-ttu-id="7b96a-128">Para saber mais sobre os recursos de continuidade dos negócios das edições do Banco de Dados SQL do Azure, leia a [Visão geral da continuidade dos negócios do Banco de Dados SQL do Azure][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="7b96a-128">To learn about the business continuity features of Azure SQL Database editions, please read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
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
