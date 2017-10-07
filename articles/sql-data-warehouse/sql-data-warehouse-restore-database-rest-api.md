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
# <a name="restore-an-azure-sql-data-warehouse-rest-api"></a><span data-ttu-id="04b40-103">Recuperar um SQL Data Warehouse do Azure (API REST)</span><span class="sxs-lookup"><span data-stu-id="04b40-103">Restore an Azure SQL Data Warehouse (REST API)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="04b40-104">[Visão geral][Overview]</span><span class="sxs-lookup"><span data-stu-id="04b40-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="04b40-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="04b40-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="04b40-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="04b40-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="04b40-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="04b40-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="04b40-108">Neste artigo, você aprenderá como toorestore um usando o Azure SQL Data Warehouse Olá API REST.</span><span class="sxs-lookup"><span data-stu-id="04b40-108">In this article you will learn how toorestore an Azure SQL Data Warehouse using hello REST API.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="04b40-109">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="04b40-109">Before you begin</span></span>
<span data-ttu-id="04b40-110">**Verifique sua capacidade de DTU.**</span><span class="sxs-lookup"><span data-stu-id="04b40-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="04b40-111">Cada SQL Data Warehouse é hospedado por um servidor SQL (por exemplo, myserver.database.windows.net) que tem uma cota de DTU padrão.</span><span class="sxs-lookup"><span data-stu-id="04b40-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="04b40-112">Antes de poder restaurar um SQL Data Warehouse, verifique se esse saudação que do SQL server tem suficiente restante cota de DTU para o banco de dados de hello está sendo restaurado.</span><span class="sxs-lookup"><span data-stu-id="04b40-112">Before you can restore a SQL Data Warehouse, verify that hello your SQL server has enough remaining DTU quota for hello database being restored.</span></span> <span data-ttu-id="04b40-113">toolearn como toocalculate DTU necessário ou toorequest mais DTU, consulte [solicitar uma alteração de cota DTU][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="04b40-113">toolearn how toocalculate DTU needed or toorequest more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="04b40-114">Restaurar um banco de dados ativo ou pausado</span><span class="sxs-lookup"><span data-stu-id="04b40-114">Restore an active or paused database</span></span>
<span data-ttu-id="04b40-115">toorestore um banco de dados:</span><span class="sxs-lookup"><span data-stu-id="04b40-115">toorestore a database:</span></span>

1. <span data-ttu-id="04b40-116">Obter lista de saudação de pontos de restauração do banco de dados usando a operação de pontos de restauração do banco de dados de Get hello.</span><span class="sxs-lookup"><span data-stu-id="04b40-116">Get hello list of database restore points using hello Get Database Restore Points operation.</span></span>
2. <span data-ttu-id="04b40-117">Iniciar a restauração usando Olá [criar solicitação de restauração de banco de dados] [ Create database restore request] operação.</span><span class="sxs-lookup"><span data-stu-id="04b40-117">Begin your restore by using hello [Create database restore request][Create database restore request] operation.</span></span>
3. <span data-ttu-id="04b40-118">Acompanhar o status de saudação de sua restauração usando Olá [status da operação de banco de dados] [ Database operation status] operação.</span><span class="sxs-lookup"><span data-stu-id="04b40-118">Track hello status of your restore by using hello [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="04b40-119">Após a restauração hello, você pode configurar o banco de dados recuperado seguindo [configurar seu banco de dados após a recuperação][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="04b40-119">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="04b40-120">Restaurar um banco de dados excluído</span><span class="sxs-lookup"><span data-stu-id="04b40-120">Restore a deleted database</span></span>
<span data-ttu-id="04b40-121">toorestore um banco de dados excluído:</span><span class="sxs-lookup"><span data-stu-id="04b40-121">toorestore a deleted database:</span></span>

1. <span data-ttu-id="04b40-122">Listar todos os seus bancos de dados excluídos restauráveis usando Olá [bancos de dados de lista restaurável descartados] [ List restorable dropped databases] operação.</span><span class="sxs-lookup"><span data-stu-id="04b40-122">List all of your restorable deleted databases by using hello [List restorable dropped databases][List restorable dropped databases] operation.</span></span>
2. <span data-ttu-id="04b40-123">Obter os detalhes de saudação para Olá excluído banco de dados toorestore usando Olá [Get restaurável descartado banco de dados] [ Get restorable dropped database] operação.</span><span class="sxs-lookup"><span data-stu-id="04b40-123">Get hello details for hello deleted database you want toorestore by using hello [Get restorable dropped database][Get restorable dropped database] operation.</span></span>
3. <span data-ttu-id="04b40-124">Iniciar a restauração usando Olá [criar solicitação de restauração de banco de dados] [ Create database restore request] operação.</span><span class="sxs-lookup"><span data-stu-id="04b40-124">Begin your restore by using hello [Create database restore request][Create database restore request] operation.</span></span>
4. <span data-ttu-id="04b40-125">Acompanhar o status de saudação de sua restauração usando Olá [status da operação de banco de dados] [ Database operation status] operação.</span><span class="sxs-lookup"><span data-stu-id="04b40-125">Track hello status of your restore by using hello [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="04b40-126">tooconfigure seu banco de dados após a restauração hello, consulte [configurar seu banco de dados após a recuperação][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="04b40-126">tooconfigure your database after hello restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="04b40-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="04b40-127">Next steps</span></span>
<span data-ttu-id="04b40-128">toolearn sobre recursos de continuidade de negócios Olá de edições de banco de dados de SQL do Azure, leia Olá [visão geral de continuidade de negócios do Azure SQL Database][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="04b40-128">toolearn about hello business continuity features of Azure SQL Database editions, please read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

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
