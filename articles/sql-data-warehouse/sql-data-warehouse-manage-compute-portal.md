---
title: "aaaManage computação power no Azure SQL Data Warehouse (portal do Azure) | Microsoft Docs"
description: "Capacidade de computação toomanage tarefas do portal do Azure. Dimensionar recursos de computação ajustando as DWUs. Ou, pausar e retomar os custos de toosave de recursos de computação."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 233b0da5-4abd-4d1d-9586-4ccc5f50b071
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: b2e84b3763e97ce88c190eecfb64b2d06f727229
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-azure-portal"></a><span data-ttu-id="e4d85-105">Gerenciar poder de computação no SQL Data Warehouse do Azure (portal do Azure)</span><span class="sxs-lookup"><span data-stu-id="e4d85-105">Manage compute power in Azure SQL Data Warehouse (Azure portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e4d85-106">Visão geral</span><span class="sxs-lookup"><span data-stu-id="e4d85-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="e4d85-107">Portal</span><span class="sxs-lookup"><span data-stu-id="e4d85-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="e4d85-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e4d85-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="e4d85-109">REST</span><span class="sxs-lookup"><span data-stu-id="e4d85-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="e4d85-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="e4d85-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>


## <a name="scale-compute-power"></a><span data-ttu-id="e4d85-111">Dimensionar poder de computação</span><span class="sxs-lookup"><span data-stu-id="e4d85-111">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="e4d85-112">recursos de computação toochange:</span><span class="sxs-lookup"><span data-stu-id="e4d85-112">toochange compute resources:</span></span>

1. <span data-ttu-id="e4d85-113">Olá abrir [portal do Azure][Azure portal], abra o banco de dados e clique em **escala**.</span><span class="sxs-lookup"><span data-stu-id="e4d85-113">Open hello [Azure portal][Azure portal], open your database, and click **Scale**.</span></span>

    ![Clique em Escala.][1]
2. <span data-ttu-id="e4d85-115">Na folha de escala hello, mova o controle deslizante de saudação à esquerda ou direita toochange configuração de DWU de saudação.</span><span class="sxs-lookup"><span data-stu-id="e4d85-115">In hello Scale blade, move hello slider left or right toochange hello DWU setting.</span></span>

    ![Mover o controle deslizante][2]
3. <span data-ttu-id="e4d85-117">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="e4d85-117">Click **Save**.</span></span> <span data-ttu-id="e4d85-118">Será exibida uma mensagem de confirmação.</span><span class="sxs-lookup"><span data-stu-id="e4d85-118">A confirmation message appears.</span></span> <span data-ttu-id="e4d85-119">Clique em **Sim** tooconfirm ou **sem** toocancel.</span><span class="sxs-lookup"><span data-stu-id="e4d85-119">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![Clique em Salvar][3]

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="e4d85-121">Pausar computação</span><span class="sxs-lookup"><span data-stu-id="e4d85-121">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="e4d85-122">toopause um banco de dados:</span><span class="sxs-lookup"><span data-stu-id="e4d85-122">toopause a database:</span></span>

1. <span data-ttu-id="e4d85-123">Olá abrir [portal do Azure] [ Azure portal] e abra o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e4d85-123">Open hello [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="e4d85-124">Observe que Olá Status é **Online**.</span><span class="sxs-lookup"><span data-stu-id="e4d85-124">Notice that hello Status is **Online**.</span></span>

    ![Status online][6]
2. <span data-ttu-id="e4d85-126">Clique em recursos de computação e memória toosuspend, **pausar**, e, em seguida, será exibida uma mensagem de confirmação.</span><span class="sxs-lookup"><span data-stu-id="e4d85-126">toosuspend compute and memory resources, click **Pause**, and then a confirmation message appears.</span></span> <span data-ttu-id="e4d85-127">Clique em **Sim** tooconfirm ou **sem** toocancel.</span><span class="sxs-lookup"><span data-stu-id="e4d85-127">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![Confirmar pausar][7]
3. <span data-ttu-id="e4d85-129">Quando o SQL Data Warehouse é iniciar o banco de dados do hello, status de saudação é **pausar**.</span><span class="sxs-lookup"><span data-stu-id="e4d85-129">While SQL Data Warehouse is starting hello database, hello status is **Pausing**.</span></span>
4. <span data-ttu-id="e4d85-130">Quando o status de saudação é **pausado**, Olá pausar operação seja concluída e você não está sendo cobradas DWUs.</span><span class="sxs-lookup"><span data-stu-id="e4d85-130">When hello status is **Paused**, hello pause operation is done and you are no longer being charged for DWUs.</span></span>

    ![Status em pausa][4]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="e4d85-132">Retomar a computação</span><span class="sxs-lookup"><span data-stu-id="e4d85-132">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="e4d85-133">tooresume um banco de dados:</span><span class="sxs-lookup"><span data-stu-id="e4d85-133">tooresume a database:</span></span>

1. <span data-ttu-id="e4d85-134">Olá abrir [portal do Azure] [ Azure portal] e abra o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e4d85-134">Open hello [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="e4d85-135">Observe que Olá Status é **pausado**.</span><span class="sxs-lookup"><span data-stu-id="e4d85-135">Notice that hello Status is **Paused**.</span></span>

    ![Pausar banco de dados][4]
2. <span data-ttu-id="e4d85-137">Clique em banco de dados de saudação tooresume **iniciar**, e, em seguida, será exibida uma mensagem de confirmação.</span><span class="sxs-lookup"><span data-stu-id="e4d85-137">tooresume hello database click **Start**, and then a confirmation message appears.</span></span> <span data-ttu-id="e4d85-138">Clique em **Sim** tooconfirm ou **sem** toocancel.</span><span class="sxs-lookup"><span data-stu-id="e4d85-138">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![Confirmar retomar][5]
3. <span data-ttu-id="e4d85-140">Enquanto o SQL Data Warehouse é iniciar o banco de dados de saudação, o status de saudação é "Retomando".</span><span class="sxs-lookup"><span data-stu-id="e4d85-140">While SQL Data Warehouse is starting hello database, hello status is "Resuming".</span></span>
4. <span data-ttu-id="e4d85-141">Quando o status de saudação é **online**, Olá está pronto.</span><span class="sxs-lookup"><span data-stu-id="e4d85-141">When hello status is **online**, hello database is ready.</span></span>

    ![Status online][6]

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="e4d85-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e4d85-143">Next steps</span></span>
<span data-ttu-id="e4d85-144">Para obter mais informações, confira [Visão geral de gerenciamento][Management overview].</span><span class="sxs-lookup"><span data-stu-id="e4d85-144">For more information, see [Management overview][Management overview].</span></span>

<!--Image references-->
[1]: ./media/sql-data-warehouse-manage-compute-portal/click-scale.png
[2]: ./media/sql-data-warehouse-manage-compute-portal/move-slider.png
[3]: ./media/sql-data-warehouse-manage-compute-portal/click-save.png
[4]: ./media/sql-data-warehouse-manage-compute-portal/resume-database.png
[5]: ./media/sql-data-warehouse-manage-compute-portal/resume-confirm.png
[6]: ./media/sql-data-warehouse-manage-compute-portal/pause-database.png
[7]: ./media/sql-data-warehouse-manage-compute-portal/pause-confirm.png

<!--Article references-->
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
