---
title: aaaPause, retomar, dimensionar com REST no Data Warehouse do Azure SQL | Microsoft Docs
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
ms.openlocfilehash: fc867febb118fb5c86c2637a41b232076021b95d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-rest"></a><span data-ttu-id="f2838-103">Gerenciar poder de computação no SQL Data Warehouse do Azure (REST)</span><span class="sxs-lookup"><span data-stu-id="f2838-103">Manage compute power in Azure SQL Data Warehouse (REST)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f2838-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="f2838-104">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="f2838-105">Portal</span><span class="sxs-lookup"><span data-stu-id="f2838-105">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="f2838-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2838-106">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="f2838-107">REST</span><span class="sxs-lookup"><span data-stu-id="f2838-107">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="f2838-108">TSQL</span><span class="sxs-lookup"><span data-stu-id="f2838-108">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a><span data-ttu-id="f2838-109">Dimensionar poder de computação</span><span class="sxs-lookup"><span data-stu-id="f2838-109">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="f2838-110">Olá toochange DWUs, use Olá [criar ou atualizar banco de dados] [ Create or Update Database] API REST.</span><span class="sxs-lookup"><span data-stu-id="f2838-110">toochange hello DWUs, use hello [Create or Update Database][Create or Update Database] REST API.</span></span> <span data-ttu-id="f2838-111">Olá exemplo a seguir define serviço Olá nível tooDW1000 objetivo para banco de dados Olá MySQLDW que está hospedado no servidor MyServer.</span><span class="sxs-lookup"><span data-stu-id="f2838-111">hello following example sets hello service level objective tooDW1000 for hello database MySQLDW which is hosted on server MyServer.</span></span> <span data-ttu-id="f2838-112">em um grupo de recursos do Azure, o servidor de saudação é denominado ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="f2838-112">hello server is in an Azure resource group named ResourceGroup1.</span></span>

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

## <a name="pause-compute"></a><span data-ttu-id="f2838-113">Pausar computação</span><span class="sxs-lookup"><span data-stu-id="f2838-113">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="f2838-114">toopause um banco de dados, use Olá [banco de dados de pausa] [ Pause Database] API REST.</span><span class="sxs-lookup"><span data-stu-id="f2838-114">toopause a database, use hello [Pause Database][Pause Database] REST API.</span></span> <span data-ttu-id="f2838-115">Olá exemplo a seguir faz uma pausa um banco de dados denominado Database02 hospedado em um servidor chamado Server01.</span><span class="sxs-lookup"><span data-stu-id="f2838-115">hello following example pauses a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="f2838-116">em um grupo de recursos do Azure, o servidor de saudação é denominado ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="f2838-116">hello server is in an Azure resource group named ResourceGroup1.</span></span>

```
POST https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}/pause?api-version=2014-04-01-preview HTTP/1.1
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="f2838-117">Retomar a computação</span><span class="sxs-lookup"><span data-stu-id="f2838-117">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="f2838-118">toostart um banco de dados, use Olá [banco de dados de retomar] [ Resume Database] API REST.</span><span class="sxs-lookup"><span data-stu-id="f2838-118">toostart a database, use hello [Resume Database][Resume Database] REST API.</span></span> <span data-ttu-id="f2838-119">Olá, exemplo a seguir inicia um banco de dados denominado Database02 hospedado em um servidor chamado Server01.</span><span class="sxs-lookup"><span data-stu-id="f2838-119">hello following example starts a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="f2838-120">em um grupo de recursos do Azure, o servidor de saudação é denominado ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="f2838-120">hello server is in an Azure resource group named ResourceGroup1.</span></span> 

```
POST https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}/resume?api-version=2014-04-01-preview HTTP/1.1
```

## <a name="check-database-state"></a><span data-ttu-id="f2838-121">Verificar estado do banco de dados</span><span class="sxs-lookup"><span data-stu-id="f2838-121">Check database state</span></span>

```
GET https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}?api-version=2014-04-01 HTTP/1.1
```

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="f2838-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f2838-122">Next steps</span></span>
<span data-ttu-id="f2838-123">Para outras tarefas de gerenciamento, consulte [Visão geral de gerenciamento][Management overview].</span><span class="sxs-lookup"><span data-stu-id="f2838-123">For other management tasks, see [Management overview][Management overview].</span></span>

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
