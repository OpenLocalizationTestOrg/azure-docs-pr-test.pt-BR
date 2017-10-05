---
title: Pausar, retomar, dimensionar com o REST no Azure SQL Data Warehouse | Microsoft Docs
description: "Gerencie o poder de computação no SQL Data Warehouse por meio da REST, do T-SQL e do PowerShell."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: 21de7337-9356-49bb-a6eb-06c1beeba2c4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 07/25/2017
ms.author: elbutter
ms.openlocfilehash: 24e43205c0c562fca9b1c2c0e5eed4da54e17ed7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-rest"></a><span data-ttu-id="b8dc9-103">Gerenciar poder de computação no SQL Data Warehouse do Azure (REST)</span><span class="sxs-lookup"><span data-stu-id="b8dc9-103">Manage compute power in Azure SQL Data Warehouse (REST)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b8dc9-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="b8dc9-104">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="b8dc9-105">Portal</span><span class="sxs-lookup"><span data-stu-id="b8dc9-105">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="b8dc9-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8dc9-106">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="b8dc9-107">REST</span><span class="sxs-lookup"><span data-stu-id="b8dc9-107">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="b8dc9-108">TSQL</span><span class="sxs-lookup"><span data-stu-id="b8dc9-108">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a><span data-ttu-id="b8dc9-109">Dimensionar poder de computação</span><span class="sxs-lookup"><span data-stu-id="b8dc9-109">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="b8dc9-110">Para alterar as DWUs, use a API REST [Criar ou Atualizar Banco de Dados][Create or Update Database].</span><span class="sxs-lookup"><span data-stu-id="b8dc9-110">To change the DWUs, use the [Create or Update Database][Create or Update Database] REST API.</span></span> <span data-ttu-id="b8dc9-111">O exemplo a seguir define o objetivo de nível de serviço como DW1000 para o banco de dados MySQLDW, que está hospedado no servidor MyServer.</span><span class="sxs-lookup"><span data-stu-id="b8dc9-111">The following example sets the service level objective to DW1000 for the database MySQLDW which is hosted on server MyServer.</span></span> <span data-ttu-id="b8dc9-112">O servidor está em um grupo de recursos do Azure chamado ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="b8dc9-112">The server is in an Azure resource group named ResourceGroup1.</span></span>

```
PATCH https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}?api-version=2014-04-01-preview HTTP/1.1
Content-Type: application/json; charset=UTF-8

{
    "properties": {
        "requestedServiceObjectiveName": DW1000
    }
}
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="b8dc9-113">Pausar computação</span><span class="sxs-lookup"><span data-stu-id="b8dc9-113">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="b8dc9-114">Para pausar um banco de dados, use a API REST [Pausar o banco de dados][Pause Database].</span><span class="sxs-lookup"><span data-stu-id="b8dc9-114">To pause a database, use the [Pause Database][Pause Database] REST API.</span></span> <span data-ttu-id="b8dc9-115">O exemplo a seguir pausa um banco de dados chamado Database02 hospedado em um servidor chamado Server01.</span><span class="sxs-lookup"><span data-stu-id="b8dc9-115">The following example pauses a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="b8dc9-116">O servidor está em um grupo de recursos do Azure chamado ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="b8dc9-116">The server is in an Azure resource group named ResourceGroup1.</span></span>

```
POST https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}/pause?api-version=2014-04-01-preview HTTP/1.1
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="b8dc9-117">Retomar a computação</span><span class="sxs-lookup"><span data-stu-id="b8dc9-117">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="b8dc9-118">Para iniciar um banco de dados, use a API REST [Retomar o banco de dados][Resume Database].</span><span class="sxs-lookup"><span data-stu-id="b8dc9-118">To start a database, use the [Resume Database][Resume Database] REST API.</span></span> <span data-ttu-id="b8dc9-119">O exemplo a seguir inicia um banco de dados chamado Database02 hospedado em um servidor chamado Server01.</span><span class="sxs-lookup"><span data-stu-id="b8dc9-119">The following example starts a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="b8dc9-120">O servidor está em um grupo de recursos do Azure chamado ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="b8dc9-120">The server is in an Azure resource group named ResourceGroup1.</span></span> 

```
POST https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}/resume?api-version=2014-04-01-preview HTTP/1.1
```

## <a name="check-database-state"></a><span data-ttu-id="b8dc9-121">Verificar estado do banco de dados</span><span class="sxs-lookup"><span data-stu-id="b8dc9-121">Check database state</span></span>

```
GET https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}?api-version=2014-04-01 HTTP/1.1
```

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="b8dc9-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b8dc9-122">Next steps</span></span>
<span data-ttu-id="b8dc9-123">Para outras tarefas de gerenciamento, consulte [Visão geral de gerenciamento][Management overview].</span><span class="sxs-lookup"><span data-stu-id="b8dc9-123">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->
[Pause Database]: https://msdn.microsoft.com/library/azure/mt718817.aspx
[Resume Database]: https://msdn.microsoft.com/library/azure/mt718820.aspx
[Create or Update Database]: https://msdn.microsoft.com/library/azure/mt163685.aspx

<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
