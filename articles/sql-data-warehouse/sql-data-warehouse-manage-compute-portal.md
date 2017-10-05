---
title: "Gerenciar potência de computação no SQL Data Warehouse do Azure (portal do Azure) | Microsoft Docs"
description: "Tarefas do portal do Azure para gerenciar o poder de computação. Dimensionar recursos de computação ajustando as DWUs. Ou, para economizar custos, pause e retome os recursos de computação."
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
ms.openlocfilehash: 63888d5dd103b585cf18e4787d3e779810163e3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-azure-portal"></a><span data-ttu-id="54ab9-105">Gerenciar poder de computação no SQL Data Warehouse do Azure (portal do Azure)</span><span class="sxs-lookup"><span data-stu-id="54ab9-105">Manage compute power in Azure SQL Data Warehouse (Azure portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="54ab9-106">Visão geral</span><span class="sxs-lookup"><span data-stu-id="54ab9-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="54ab9-107">Portal</span><span class="sxs-lookup"><span data-stu-id="54ab9-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="54ab9-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="54ab9-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="54ab9-109">REST</span><span class="sxs-lookup"><span data-stu-id="54ab9-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="54ab9-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="54ab9-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>


## <a name="scale-compute-power"></a><span data-ttu-id="54ab9-111">Dimensionar poder de computação</span><span class="sxs-lookup"><span data-stu-id="54ab9-111">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="54ab9-112">Para alterar recursos de computação:</span><span class="sxs-lookup"><span data-stu-id="54ab9-112">To change compute resources:</span></span>

1. <span data-ttu-id="54ab9-113">Abra o [Portal do Azure][Azure portal], abra seu banco de dados e clique em **Escala**.</span><span class="sxs-lookup"><span data-stu-id="54ab9-113">Open the [Azure portal][Azure portal], open your database, and click **Scale**.</span></span>

    ![Clique em Escala.][1]
2. <span data-ttu-id="54ab9-115">Na folha Escala, mova o controle deslizante para a esquerda ou direita para alterar a configuração de DWU.</span><span class="sxs-lookup"><span data-stu-id="54ab9-115">In the Scale blade, move the slider left or right to change the DWU setting.</span></span>

    ![Mover o controle deslizante][2]
3. <span data-ttu-id="54ab9-117">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="54ab9-117">Click **Save**.</span></span> <span data-ttu-id="54ab9-118">Será exibida uma mensagem de confirmação.</span><span class="sxs-lookup"><span data-stu-id="54ab9-118">A confirmation message appears.</span></span> <span data-ttu-id="54ab9-119">Clique em **sim** para confirmar ou em **não** para cancelar.</span><span class="sxs-lookup"><span data-stu-id="54ab9-119">Click **yes** to confirm or **no** to cancel.</span></span>

    ![Clique em Salvar][3]

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="54ab9-121">Pausar computação</span><span class="sxs-lookup"><span data-stu-id="54ab9-121">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="54ab9-122">Para pausar um banco de dados:</span><span class="sxs-lookup"><span data-stu-id="54ab9-122">To pause a database:</span></span>

1. <span data-ttu-id="54ab9-123">Abra o [Portal do Azure][Azure portal] e abra seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="54ab9-123">Open the [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="54ab9-124">Observe que o Status é **Online**.</span><span class="sxs-lookup"><span data-stu-id="54ab9-124">Notice that the Status is **Online**.</span></span>

    ![Status online][6]
2. <span data-ttu-id="54ab9-126">Para suspender os recursos de computação e de memória, clique em **Pausar**e uma mensagem de confirmação será exibida.</span><span class="sxs-lookup"><span data-stu-id="54ab9-126">To suspend compute and memory resources, click **Pause**, and then a confirmation message appears.</span></span> <span data-ttu-id="54ab9-127">Clique em **sim** para confirmar ou em **não** para cancelar.</span><span class="sxs-lookup"><span data-stu-id="54ab9-127">Click **yes** to confirm or **no** to cancel.</span></span>

    ![Confirmar pausar][7]
3. <span data-ttu-id="54ab9-129">Enquanto o SQL Data Warehouse estiver iniciando o banco de dados, o status será **Pausando**.</span><span class="sxs-lookup"><span data-stu-id="54ab9-129">While SQL Data Warehouse is starting the database, the status is **Pausing**.</span></span>
4. <span data-ttu-id="54ab9-130">Quando o status for **Em pausa**, a operação de pausa terá sido concluída e você deixará de ser cobrado pelas DWUs.</span><span class="sxs-lookup"><span data-stu-id="54ab9-130">When the status is **Paused**, the pause operation is done and you are no longer being charged for DWUs.</span></span>

    ![Status em pausa][4]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="54ab9-132">Retomar a computação</span><span class="sxs-lookup"><span data-stu-id="54ab9-132">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="54ab9-133">Para retomar um banco de dados:</span><span class="sxs-lookup"><span data-stu-id="54ab9-133">To resume a database:</span></span>

1. <span data-ttu-id="54ab9-134">Abra o [Portal do Azure][Azure portal] e abra seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="54ab9-134">Open the [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="54ab9-135">Observe que o Status é **Em pausa**.</span><span class="sxs-lookup"><span data-stu-id="54ab9-135">Notice that the Status is **Paused**.</span></span>

    ![Pausar banco de dados][4]
2. <span data-ttu-id="54ab9-137">Para retomar o banco de dados, clique em **Iniciar**e uma mensagem de confirmação será exibida.</span><span class="sxs-lookup"><span data-stu-id="54ab9-137">To resume the database click **Start**, and then a confirmation message appears.</span></span> <span data-ttu-id="54ab9-138">Clique em **sim** para confirmar ou em **não** para cancelar.</span><span class="sxs-lookup"><span data-stu-id="54ab9-138">Click **yes** to confirm or **no** to cancel.</span></span>

    ![Confirmar retomar][5]
3. <span data-ttu-id="54ab9-140">Enquanto o SQL Data Warehouse estiver iniciando o banco de dados, o status será “Continuando”.</span><span class="sxs-lookup"><span data-stu-id="54ab9-140">While SQL Data Warehouse is starting the database, the status is "Resuming".</span></span>
4. <span data-ttu-id="54ab9-141">Quando o status for **online**, o banco de dados estará pronto.</span><span class="sxs-lookup"><span data-stu-id="54ab9-141">When the status is **online**, the database is ready.</span></span>

    ![Status online][6]

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="54ab9-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="54ab9-143">Next steps</span></span>
<span data-ttu-id="54ab9-144">Para obter mais informações, confira [Visão geral de gerenciamento][Management overview].</span><span class="sxs-lookup"><span data-stu-id="54ab9-144">For more information, see [Management overview][Management overview].</span></span>

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
