---
title: "aaaManage computação power no Azure SQL Data Warehouse (visão geral) | Microsoft Docs"
description: "Funcionalidades de escala horizontal de desempenho no SQL Data Warehouse do Azure. Expansão ajustando DWUs ou pausar e retomar os custos de toosave de recursos de computação."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: e13a82b0-abfe-429f-ac3c-f2b6789a70c6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/22/2017
ms.author: elbutter
ms.openlocfilehash: 1ffbe8d694ac181eaeb6f585a2cee87a570ed7d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-overview"></a><span data-ttu-id="21a1b-104">Gerenciar poder de computação no SQL Data Warehouse do Azure (Visão Geral)</span><span class="sxs-lookup"><span data-stu-id="21a1b-104">Manage compute power in Azure SQL Data Warehouse (Overview)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="21a1b-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="21a1b-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="21a1b-106">Portal</span><span class="sxs-lookup"><span data-stu-id="21a1b-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="21a1b-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="21a1b-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="21a1b-108">REST</span><span class="sxs-lookup"><span data-stu-id="21a1b-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="21a1b-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="21a1b-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<span data-ttu-id="21a1b-110">arquitetura de saudação do SQL Data Warehouse separa o armazenamento e computação, permitindo que cada tooscale independentemente.</span><span class="sxs-lookup"><span data-stu-id="21a1b-110">hello architecture of SQL Data Warehouse separates storage and compute, allowing each tooscale independently.</span></span> <span data-ttu-id="21a1b-111">Como resultado, computação pode ser dimensionado toomeet as demandas de desempenho independente do valor de saudação de dados.</span><span class="sxs-lookup"><span data-stu-id="21a1b-111">As a result, compute can be scaled toomeet performance demands independent of hello amount of data.</span></span> <span data-ttu-id="21a1b-112">Uma consequência natural dessa arquitetura é que a [cobrança][billed] pela computação e pelo armazenamento é separada.</span><span class="sxs-lookup"><span data-stu-id="21a1b-112">A natural consequence of this architecture is that [billing][billed] for compute and storage is separate.</span></span> 

<span data-ttu-id="21a1b-113">Esta visão geral descreve como expandir funciona com o SQL Data Warehouse e como tooutilize Olá pausar, retomar e recursos de escala do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="21a1b-113">This overview describes how scale out works with SQL Data Warehouse and how tooutilize hello pause, resume, and scale capabilities of SQL Data Warehouse.</span></span> <span data-ttu-id="21a1b-114">Consulte Olá [unidades (DWUs) do data warehouse] [ data warehouse units (DWUs)] toolearn de página como DWUs e desempenho estão relacionados.</span><span class="sxs-lookup"><span data-stu-id="21a1b-114">Consult hello [data warehouse units (DWUs)][data warehouse units (DWUs)] page toolearn how DWUs and performance are related.</span></span> 

## <a name="how-compute-management-operations-work-in-sql-data-warehouse"></a><span data-ttu-id="21a1b-115">Como as operações de gerenciamento de computação funcionam no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="21a1b-115">How compute management operations work in SQL Data Warehouse</span></span>
<span data-ttu-id="21a1b-116">arquitetura de saudação do SQL Data Warehouse consiste em um nó de controle, nós de computação e Olá disseminadas por 60 distribuições de camada de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="21a1b-116">hello architecture for SQL Data Warehouse consists of a control node, compute nodes, and hello storage layer spread across 60 distributions.</span></span> 

<span data-ttu-id="21a1b-117">Durante uma sessão ativa normal no SQL Data Warehouse, nó principal do sistema gerencia os metadados de saudação e contém o otimizador de consulta Olá distribuída.</span><span class="sxs-lookup"><span data-stu-id="21a1b-117">During a normal active session in SQL Data Warehouse, your system's head node manages hello metadata and contains hello distributed query optimizer.</span></span> <span data-ttu-id="21a1b-118">Sob esse nó principal estão os nós de computação e a camada de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="21a1b-118">Beneath this head node are your compute nodes and your storage layer.</span></span> <span data-ttu-id="21a1b-119">Para um DWU 400, o sistema tem um nó principal, quatro nós de computação e camada de armazenamento hello, consistindo de 60 distribuições.</span><span class="sxs-lookup"><span data-stu-id="21a1b-119">For a DWU 400, your system has one head node, four compute nodes, and hello storage layer, consisting of 60 distributions.</span></span> 

<span data-ttu-id="21a1b-120">Quando você passar por uma escala ou pausa a operação, o sistema de saudação primeiro elimina todas as consultas de entrada e, em seguida, reverte as transações tooensure um estado consistente.</span><span class="sxs-lookup"><span data-stu-id="21a1b-120">When you undergo a scale or pause operation, hello system first kills all incoming queries and then rolls back transactions tooensure a consistent state.</span></span> <span data-ttu-id="21a1b-121">Para operações de escala, o dimensionamento só ocorrerá após a conclusão dessa reversão transacional.</span><span class="sxs-lookup"><span data-stu-id="21a1b-121">For scale operations, scaling will only occur once this transactional rollback has completed.</span></span> <span data-ttu-id="21a1b-122">Para uma operação de expansão, provisões de sistema Olá Olá número de nós de computação extra desejado e começa a reanexação de camada de armazenamento toohello de nós de computação hello.</span><span class="sxs-lookup"><span data-stu-id="21a1b-122">For a scale-up operation, hello system provisions hello extra desired number of compute nodes, and then begins reattaching hello compute nodes toohello storage layer.</span></span> <span data-ttu-id="21a1b-123">Para uma operação de redução de escala, hello nós desnecessários são liberados e nós de computação restantes Olá reconecte toohello o número apropriado de distribuições.</span><span class="sxs-lookup"><span data-stu-id="21a1b-123">For a scale-down operation, hello unneeded nodes are released and hello remaining compute nodes reattach themselves toohello appropriate number of distributions.</span></span> <span data-ttu-id="21a1b-124">Para uma operação de pausa de computação todos os nós são liberados e o sistema passará por uma variedade de metadados operações tooleave seu sistema final em um estado estável.</span><span class="sxs-lookup"><span data-stu-id="21a1b-124">For a pause operation, all compute nodes are released and your system will undergo a variety of metadata operations tooleave your final system in a stable state.</span></span>

| <span data-ttu-id="21a1b-125">DWU</span><span class="sxs-lookup"><span data-stu-id="21a1b-125">DWU</span></span>  | <span data-ttu-id="21a1b-126">\# de nós de computação</span><span class="sxs-lookup"><span data-stu-id="21a1b-126">\#of compute nodes</span></span> | <span data-ttu-id="21a1b-127">\# de distribuições por nó</span><span class="sxs-lookup"><span data-stu-id="21a1b-127">\# of distributions per node</span></span> |
| ---- | ------------------ | ---------------------------- |
| <span data-ttu-id="21a1b-128">100</span><span class="sxs-lookup"><span data-stu-id="21a1b-128">100</span></span>  | <span data-ttu-id="21a1b-129">1</span><span class="sxs-lookup"><span data-stu-id="21a1b-129">1</span></span>                  | <span data-ttu-id="21a1b-130">60</span><span class="sxs-lookup"><span data-stu-id="21a1b-130">60</span></span>                           |
| <span data-ttu-id="21a1b-131">200</span><span class="sxs-lookup"><span data-stu-id="21a1b-131">200</span></span>  | <span data-ttu-id="21a1b-132">2</span><span class="sxs-lookup"><span data-stu-id="21a1b-132">2</span></span>                  | <span data-ttu-id="21a1b-133">30</span><span class="sxs-lookup"><span data-stu-id="21a1b-133">30</span></span>                           |
| <span data-ttu-id="21a1b-134">300</span><span class="sxs-lookup"><span data-stu-id="21a1b-134">300</span></span>  | <span data-ttu-id="21a1b-135">3</span><span class="sxs-lookup"><span data-stu-id="21a1b-135">3</span></span>                  | <span data-ttu-id="21a1b-136">20</span><span class="sxs-lookup"><span data-stu-id="21a1b-136">20</span></span>                           |
| <span data-ttu-id="21a1b-137">400</span><span class="sxs-lookup"><span data-stu-id="21a1b-137">400</span></span>  | <span data-ttu-id="21a1b-138">4</span><span class="sxs-lookup"><span data-stu-id="21a1b-138">4</span></span>                  | <span data-ttu-id="21a1b-139">15</span><span class="sxs-lookup"><span data-stu-id="21a1b-139">15</span></span>                           |
| <span data-ttu-id="21a1b-140">500</span><span class="sxs-lookup"><span data-stu-id="21a1b-140">500</span></span>  | <span data-ttu-id="21a1b-141">5</span><span class="sxs-lookup"><span data-stu-id="21a1b-141">5</span></span>                  | <span data-ttu-id="21a1b-142">12</span><span class="sxs-lookup"><span data-stu-id="21a1b-142">12</span></span>                           |
| <span data-ttu-id="21a1b-143">600</span><span class="sxs-lookup"><span data-stu-id="21a1b-143">600</span></span>  | <span data-ttu-id="21a1b-144">6</span><span class="sxs-lookup"><span data-stu-id="21a1b-144">6</span></span>                  | <span data-ttu-id="21a1b-145">10</span><span class="sxs-lookup"><span data-stu-id="21a1b-145">10</span></span>                           |
| <span data-ttu-id="21a1b-146">1000</span><span class="sxs-lookup"><span data-stu-id="21a1b-146">1000</span></span> | <span data-ttu-id="21a1b-147">10</span><span class="sxs-lookup"><span data-stu-id="21a1b-147">10</span></span>                 | <span data-ttu-id="21a1b-148">6</span><span class="sxs-lookup"><span data-stu-id="21a1b-148">6</span></span>                            |
| <span data-ttu-id="21a1b-149">1.200</span><span class="sxs-lookup"><span data-stu-id="21a1b-149">1200</span></span> | <span data-ttu-id="21a1b-150">12</span><span class="sxs-lookup"><span data-stu-id="21a1b-150">12</span></span>                 | <span data-ttu-id="21a1b-151">5</span><span class="sxs-lookup"><span data-stu-id="21a1b-151">5</span></span>                            |
| <span data-ttu-id="21a1b-152">1500</span><span class="sxs-lookup"><span data-stu-id="21a1b-152">1500</span></span> | <span data-ttu-id="21a1b-153">15</span><span class="sxs-lookup"><span data-stu-id="21a1b-153">15</span></span>                 | <span data-ttu-id="21a1b-154">4</span><span class="sxs-lookup"><span data-stu-id="21a1b-154">4</span></span>                            |
| <span data-ttu-id="21a1b-155">2000</span><span class="sxs-lookup"><span data-stu-id="21a1b-155">2000</span></span> | <span data-ttu-id="21a1b-156">20</span><span class="sxs-lookup"><span data-stu-id="21a1b-156">20</span></span>                 | <span data-ttu-id="21a1b-157">3</span><span class="sxs-lookup"><span data-stu-id="21a1b-157">3</span></span>                            |
| <span data-ttu-id="21a1b-158">3000</span><span class="sxs-lookup"><span data-stu-id="21a1b-158">3000</span></span> | <span data-ttu-id="21a1b-159">30</span><span class="sxs-lookup"><span data-stu-id="21a1b-159">30</span></span>                 | <span data-ttu-id="21a1b-160">2</span><span class="sxs-lookup"><span data-stu-id="21a1b-160">2</span></span>                            |
| <span data-ttu-id="21a1b-161">6000</span><span class="sxs-lookup"><span data-stu-id="21a1b-161">6000</span></span> | <span data-ttu-id="21a1b-162">60</span><span class="sxs-lookup"><span data-stu-id="21a1b-162">60</span></span>                 | <span data-ttu-id="21a1b-163">1</span><span class="sxs-lookup"><span data-stu-id="21a1b-163">1</span></span>                            |

<span data-ttu-id="21a1b-164">Olá três principais funções de gerenciamento de computação são:</span><span class="sxs-lookup"><span data-stu-id="21a1b-164">hello three primary functions for managing compute are:</span></span>

1. <span data-ttu-id="21a1b-165">Pausar</span><span class="sxs-lookup"><span data-stu-id="21a1b-165">Pause</span></span>
2. <span data-ttu-id="21a1b-166">Continuar</span><span class="sxs-lookup"><span data-stu-id="21a1b-166">Resume</span></span>
3. <span data-ttu-id="21a1b-167">Escala</span><span class="sxs-lookup"><span data-stu-id="21a1b-167">Scale</span></span>

<span data-ttu-id="21a1b-168">Cada uma dessas operações pode levar vários toocomplete de minutos.</span><span class="sxs-lookup"><span data-stu-id="21a1b-168">Each of these operations may take several minutes toocomplete.</span></span> <span data-ttu-id="21a1b-169">Se você estiver dimensionando/interrompendo/retomando automaticamente, convém lógica tooimplement tooensure que determinadas operações tenham sido concluídas antes de continuar com a outra ação.</span><span class="sxs-lookup"><span data-stu-id="21a1b-169">If you are scaling/pausing/resuming automatically, you may want tooimplement logic tooensure that certain operations have been completed before proceeding with another action.</span></span> 

<span data-ttu-id="21a1b-170">Verificando o estado do banco de dados Olá por meio de vários pontos de extremidade permitirá toocorrectly implementar automação dessas operações.</span><span class="sxs-lookup"><span data-stu-id="21a1b-170">Checking hello database state through various endpoints will allow you toocorrectly implement automation of such operations.</span></span> <span data-ttu-id="21a1b-171">portal de saudação fornecerá notificação após a conclusão da operação e hello bancos de dados atual estado, mas não permite a verificação programático do estado.</span><span class="sxs-lookup"><span data-stu-id="21a1b-171">hello portal will provide notification upon completion of an operation and hello databases current state but does not allow for programmatic checking of state.</span></span> 

>  [!NOTE]
>
>  <span data-ttu-id="21a1b-172">A funcionalidade de gerenciamento de computação não existe em todos os pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="21a1b-172">Compute management functionality does not exist across all endpoints.</span></span>
>
>  

|              | <span data-ttu-id="21a1b-173">Pausar/Retomar</span><span class="sxs-lookup"><span data-stu-id="21a1b-173">Pause/Resume</span></span> | <span data-ttu-id="21a1b-174">Escala</span><span class="sxs-lookup"><span data-stu-id="21a1b-174">Scale</span></span> | <span data-ttu-id="21a1b-175">Verificar estado do banco de dados</span><span class="sxs-lookup"><span data-stu-id="21a1b-175">Check database state</span></span> |
| ------------ | ------------ | ----- | -------------------- |
| <span data-ttu-id="21a1b-176">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="21a1b-176">Azure portal</span></span> | <span data-ttu-id="21a1b-177">Sim</span><span class="sxs-lookup"><span data-stu-id="21a1b-177">Yes</span></span>          | <span data-ttu-id="21a1b-178">Sim</span><span class="sxs-lookup"><span data-stu-id="21a1b-178">Yes</span></span>   | <span data-ttu-id="21a1b-179">**Não**</span><span class="sxs-lookup"><span data-stu-id="21a1b-179">**No**</span></span>               |
| <span data-ttu-id="21a1b-180">PowerShell</span><span class="sxs-lookup"><span data-stu-id="21a1b-180">PowerShell</span></span>   | <span data-ttu-id="21a1b-181">Sim</span><span class="sxs-lookup"><span data-stu-id="21a1b-181">Yes</span></span>          | <span data-ttu-id="21a1b-182">Sim</span><span class="sxs-lookup"><span data-stu-id="21a1b-182">Yes</span></span>   | <span data-ttu-id="21a1b-183">Sim</span><span class="sxs-lookup"><span data-stu-id="21a1b-183">Yes</span></span>                  |
| <span data-ttu-id="21a1b-184">API REST</span><span class="sxs-lookup"><span data-stu-id="21a1b-184">REST API</span></span>     | <span data-ttu-id="21a1b-185">Sim</span><span class="sxs-lookup"><span data-stu-id="21a1b-185">Yes</span></span>          | <span data-ttu-id="21a1b-186">Sim</span><span class="sxs-lookup"><span data-stu-id="21a1b-186">Yes</span></span>   | <span data-ttu-id="21a1b-187">Sim</span><span class="sxs-lookup"><span data-stu-id="21a1b-187">Yes</span></span>                  |
| <span data-ttu-id="21a1b-188">T-SQL</span><span class="sxs-lookup"><span data-stu-id="21a1b-188">T-SQL</span></span>        | <span data-ttu-id="21a1b-189">**Não**</span><span class="sxs-lookup"><span data-stu-id="21a1b-189">**No**</span></span>       | <span data-ttu-id="21a1b-190">Sim</span><span class="sxs-lookup"><span data-stu-id="21a1b-190">Yes</span></span>   | <span data-ttu-id="21a1b-191">Sim</span><span class="sxs-lookup"><span data-stu-id="21a1b-191">Yes</span></span>                  |



<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a><span data-ttu-id="21a1b-192">Computação de escala</span><span class="sxs-lookup"><span data-stu-id="21a1b-192">Scale compute</span></span>

<span data-ttu-id="21a1b-193">O desempenho no SQL Data Warehouse é medido em [DWUs (unidades do data warehouse)][data warehouse units (DWUs)], que é uma medida abstrata de recursos de computação como CPU, memória e E/S de largura de banda.</span><span class="sxs-lookup"><span data-stu-id="21a1b-193">Performance in SQL Data Warehouse is measured in [data warehouse units (DWUs)][data warehouse units (DWUs)] which is an abstracted measure of compute resources such as CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="21a1b-194">Um usuário que deseja tooscale o desempenho do seu sistema pode fazer isso através de várias maneiras, como por meio do portal hello, T-SQL e APIs REST.</span><span class="sxs-lookup"><span data-stu-id="21a1b-194">A user who wishes tooscale their system's performance can do so through various means, such as through hello portal, T-SQL, and REST APIs.</span></span> 

### <a name="how-do-i-scale-compute"></a><span data-ttu-id="21a1b-195">Como eu dimensiono a computação?</span><span class="sxs-lookup"><span data-stu-id="21a1b-195">How do I scale compute?</span></span>
<span data-ttu-id="21a1b-196">Capacidade de computação é gerenciada por você SQL Data Warehouse, alterando a configuração de DWU de saudação.</span><span class="sxs-lookup"><span data-stu-id="21a1b-196">Compute power is managed for you SQL Data Warehouse by changing hello DWU setting.</span></span> <span data-ttu-id="21a1b-197">O desempenho aumenta [linearmente][linearly] conforme você adiciona mais DWUs para determinadas operações.</span><span class="sxs-lookup"><span data-stu-id="21a1b-197">Performance increases [linearly][linearly] as you add more DWU for certain operations.</span></span>  <span data-ttu-id="21a1b-198">Temos ofertas de DWU que asseguram que o desempenho será alterado visivelmente quando você escalar ou reduzir verticalmente seu sistema.</span><span class="sxs-lookup"><span data-stu-id="21a1b-198">We offer DWU offerings that ensure that your performance will change noticeably when you scale your system up or down.</span></span> 

<span data-ttu-id="21a1b-199">tooadjust DWUs, você pode usar qualquer um desses métodos individuais.</span><span class="sxs-lookup"><span data-stu-id="21a1b-199">tooadjust DWUs, you can use any of these individual methods.</span></span>

* <span data-ttu-id="21a1b-200">[Dimensionar a potência de computação com o Portal do Azure][Scale compute power with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="21a1b-200">[Scale compute power with Azure portal][Scale compute power with Azure portal]</span></span>
* <span data-ttu-id="21a1b-201">[Dimensionar a potência de computação com o PowerShell][Scale compute power with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="21a1b-201">[Scale compute power with PowerShell][Scale compute power with PowerShell]</span></span>
* <span data-ttu-id="21a1b-202">[Dimensionar a potência de computação com APIs REST][Scale compute power with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="21a1b-202">[Scale compute power with REST APIs][Scale compute power with REST APIs]</span></span>
* <span data-ttu-id="21a1b-203">[Dimensionar a potência de computação com o TSQL][Scale compute power with TSQL]</span><span class="sxs-lookup"><span data-stu-id="21a1b-203">[Scale compute power with TSQL][Scale compute power with TSQL]</span></span>

### <a name="how-many-dwus-should-i-use"></a><span data-ttu-id="21a1b-204">Quantas DWUs devo usar?</span><span class="sxs-lookup"><span data-stu-id="21a1b-204">How many DWUs should I use?</span></span>

<span data-ttu-id="21a1b-205">toounderstand é que o valor DWU ideal, tente dimensionamento para cima e para baixo e executando consultas alguns após o carregamento de dados.</span><span class="sxs-lookup"><span data-stu-id="21a1b-205">toounderstand what your ideal DWU value is, try scaling up and down, and running a few queries after loading your data.</span></span> <span data-ttu-id="21a1b-206">Como o dimensionamento é rápido, você pode experimentar vários níveis de desempenho diferentes durante uma hora ou menos.</span><span class="sxs-lookup"><span data-stu-id="21a1b-206">Since scaling is quick, you can try various performance levels in an hour or less.</span></span> 

> [!Note] 
> <span data-ttu-id="21a1b-207">SQL Data Warehouse é projetado tooprocess grandes quantidades de dados.</span><span class="sxs-lookup"><span data-stu-id="21a1b-207">SQL Data Warehouse is designed tooprocess large amounts of data.</span></span> <span data-ttu-id="21a1b-208">toosee seus recursos true para dimensionar, especialmente em DWUs maior, você deseja toouse um grande conjunto de dados que se aproxima ou exceder 1 TB.</span><span class="sxs-lookup"><span data-stu-id="21a1b-208">toosee its true capabilities for scaling, especially at larger DWUs, you want toouse a large data set which approaches or exceeds 1 TB.</span></span>

<span data-ttu-id="21a1b-209">Recomendações para encontrar hello DWU melhor para sua carga de trabalho:</span><span class="sxs-lookup"><span data-stu-id="21a1b-209">Recommendations for finding hello best DWU for your workload:</span></span>

1. <span data-ttu-id="21a1b-210">Para um data warehouse em desenvolvimento, comece selecionando um nível de desempenho de DWU menor.</span><span class="sxs-lookup"><span data-stu-id="21a1b-210">For a data warehouse in development, begin by selecting a smaller DWU performance level.</span></span>  <span data-ttu-id="21a1b-211">Um bom ponto de partida é DW400 ou DW200.</span><span class="sxs-lookup"><span data-stu-id="21a1b-211">A good starting point is DW400 or DW200.</span></span>
2. <span data-ttu-id="21a1b-212">Monitorar o desempenho do seu aplicativo, observar o número de saudação do DWUs selecionado em comparação com o desempenho toohello que você observar.</span><span class="sxs-lookup"><span data-stu-id="21a1b-212">Monitor your application performance, observing hello number of DWUs selected compared toohello performance you observe.</span></span>
3. <span data-ttu-id="21a1b-213">Determine quanto de desempenho mais rápido ou mais lento para você tooreach Olá nível de desempenho ideal para suas necessidades, supondo que a escala linear.</span><span class="sxs-lookup"><span data-stu-id="21a1b-213">Determine how much faster or slower performance should be for you tooreach hello optimum performance level for your requirements by assuming linear scale.</span></span>
4. <span data-ttu-id="21a1b-214">Aumentar ou diminuir o número de saudação de DWUs em proporção toohow muito mais rápida ou mais lenta do que você deseja tooperform sua carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="21a1b-214">Increase or decrease hello number of DWUs in proportion toohow much faster or slower you want your workload tooperform.</span></span> 
5. <span data-ttu-id="21a1b-215">Continue fazendo ajustes até alcançar um nível de desempenho ideal para seus requisitos de negócios.</span><span class="sxs-lookup"><span data-stu-id="21a1b-215">Continue making adjustments until you reach an optimum performance level for your business requirements.</span></span>

> [!NOTE]
>
> <span data-ttu-id="21a1b-216">Desempenho de consultas só aumenta com mais de paralelização se trabalho Olá pode ser dividido entre nós de computação.</span><span class="sxs-lookup"><span data-stu-id="21a1b-216">Query performance only increases with more parallelization if hello work can be split between compute nodes.</span></span> <span data-ttu-id="21a1b-217">Se você encontrar o dimensionamento não está alterando seu desempenho, faça check-out nossos artigos toocheck se seus dados são distribuídos ou se você está implantando uma grande quantidade de movimentação de dados de ajuste de desempenho.</span><span class="sxs-lookup"><span data-stu-id="21a1b-217">If you find that scaling is not changing your performance, please check out our performance tuning articles toocheck whether your data is unevenly distributed or if you are introducing a large amount of data movement.</span></span> 

### <a name="when-should-i-scale-dwus"></a><span data-ttu-id="21a1b-218">Quando devo dimensionar as DWUs?</span><span class="sxs-lookup"><span data-stu-id="21a1b-218">When should I scale DWUs?</span></span>
<span data-ttu-id="21a1b-219">Dimensionamento DWUs altera Olá cenários importantes a seguir:</span><span class="sxs-lookup"><span data-stu-id="21a1b-219">Scaling DWUs alters hello following important scenarios:</span></span>

1. <span data-ttu-id="21a1b-220">Alterando o desempenho do sistema de verificações, agregações e instruções CTAS Olá linearmente</span><span class="sxs-lookup"><span data-stu-id="21a1b-220">Linearly changing performance of hello system for scans, aggregations, and CTAS statements</span></span>
2. <span data-ttu-id="21a1b-221">Aumentar o número de saudação de leitores e gravadores ao carregar com PolyBase</span><span class="sxs-lookup"><span data-stu-id="21a1b-221">Increasing hello number of readers and writers when loading with PolyBase</span></span>
3. <span data-ttu-id="21a1b-222">Número máximo de consultas simultâneas e slots de simultaneidade</span><span class="sxs-lookup"><span data-stu-id="21a1b-222">Maximum number of concurrent queries and concurrency slots</span></span>

<span data-ttu-id="21a1b-223">Recomendações de quando tooscale DWUs:</span><span class="sxs-lookup"><span data-stu-id="21a1b-223">Recommendations for when tooscale DWUs:</span></span>

1. <span data-ttu-id="21a1b-224">Antes de executar uma operação de transformação ou carregamento de dados pesados, escale verticalmente as DWUs para que os dados fiquem disponíveis mais rapidamente.</span><span class="sxs-lookup"><span data-stu-id="21a1b-224">Before you perform a heavy data loading or transformation operation, scale up DWUs so that your data is available more quickly.</span></span>
2. <span data-ttu-id="21a1b-225">Durante o horário comercial de pico, dimensione tooaccommodate um número maior de consultas simultâneas.</span><span class="sxs-lookup"><span data-stu-id="21a1b-225">During peak business hours, scale tooaccommodate larger numbers of concurrent queries.</span></span> 

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="21a1b-226">Pausar computação</span><span class="sxs-lookup"><span data-stu-id="21a1b-226">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="21a1b-227">toopause um banco de dados, use qualquer um desses métodos individuais.</span><span class="sxs-lookup"><span data-stu-id="21a1b-227">toopause a database, use any of these individual methods.</span></span>

* <span data-ttu-id="21a1b-228">[Pausar a computação com o Portal do Azure][Pause compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="21a1b-228">[Pause compute with Azure portal][Pause compute with Azure portal]</span></span>
* <span data-ttu-id="21a1b-229">[Pausar a computação com o PowerShell][Pause compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="21a1b-229">[Pause compute with PowerShell][Pause compute with PowerShell]</span></span>
* <span data-ttu-id="21a1b-230">[Pausar a computação com APIs REST][Pause compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="21a1b-230">[Pause compute with REST APIs][Pause compute with REST APIs]</span></span>

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="21a1b-231">Retomar a computação</span><span class="sxs-lookup"><span data-stu-id="21a1b-231">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="21a1b-232">tooresume um banco de dados, use qualquer um desses métodos individuais.</span><span class="sxs-lookup"><span data-stu-id="21a1b-232">tooresume a database, use any of these individual methods.</span></span>

* <span data-ttu-id="21a1b-233">[Retomar a computação com o Portal do Azure][Resume compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="21a1b-233">[Resume compute with Azure portal][Resume compute with Azure portal]</span></span>
* <span data-ttu-id="21a1b-234">[Retomar a computação com o PowerShell][Resume compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="21a1b-234">[Resume compute with PowerShell][Resume compute with PowerShell]</span></span>
* <span data-ttu-id="21a1b-235">[Retomar a computação com APIs REST][Resume compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="21a1b-235">[Resume compute with REST APIs][Resume compute with REST APIs]</span></span>

<a name="check-compute-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="21a1b-236">Verificar estado do banco de dados</span><span class="sxs-lookup"><span data-stu-id="21a1b-236">Check database state</span></span> 

<span data-ttu-id="21a1b-237">tooresume um banco de dados, use qualquer um desses métodos individuais.</span><span class="sxs-lookup"><span data-stu-id="21a1b-237">tooresume a database, use any of these individual methods.</span></span>

- <span data-ttu-id="21a1b-238">[Verificar estado do banco de dados com o T-SQL][Check database state with T-SQL]</span><span class="sxs-lookup"><span data-stu-id="21a1b-238">[Check database state with T-SQL][Check database state with T-SQL]</span></span>
- <span data-ttu-id="21a1b-239">[Verificar estado do banco de dados com o PowerShell][Check database state with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="21a1b-239">[Check database state with PowerShell][Check database state with PowerShell]</span></span>
- <span data-ttu-id="21a1b-240">[Verificar estado do banco de dados com o APIs REST][Check database state with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="21a1b-240">[Check database state with REST APIs][Check database state with REST APIs]</span></span>

## <a name="permissions"></a><span data-ttu-id="21a1b-241">Permissões</span><span class="sxs-lookup"><span data-stu-id="21a1b-241">Permissions</span></span>

<span data-ttu-id="21a1b-242">Banco de dados de Olá escala requer permissões Olá descritas [ALTER DATABASE][ALTER DATABASE].</span><span class="sxs-lookup"><span data-stu-id="21a1b-242">Scaling hello database requires hello permissions described in [ALTER DATABASE][ALTER DATABASE].</span></span>  <span data-ttu-id="21a1b-243">Pausar e retomar exigem Olá [Colaborador de banco de dados SQL] [ SQL DB Contributor] permissão, especificamente Microsoft.Sql/servers/databases/action.</span><span class="sxs-lookup"><span data-stu-id="21a1b-243">Pause and Resume require hello [SQL DB Contributor][SQL DB Contributor] permission, specifically Microsoft.Sql/servers/databases/action.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="21a1b-244">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="21a1b-244">Next steps</span></span>
<span data-ttu-id="21a1b-245">Consulte toohello artigos toohelp entender alguns conceitos chave de desempenho adicionais a seguir:</span><span class="sxs-lookup"><span data-stu-id="21a1b-245">Refer toohello following articles toohelp you understand some additional key performance concepts:</span></span>

* <span data-ttu-id="21a1b-246">[Gerenciamento da carga de trabalho e simultaneidade][Workload and concurrency management]</span><span class="sxs-lookup"><span data-stu-id="21a1b-246">[Workload and concurrency management][Workload and concurrency management]</span></span>
* <span data-ttu-id="21a1b-247">[Visão geral do design da tabela][Table design overview]</span><span class="sxs-lookup"><span data-stu-id="21a1b-247">[Table design overview][Table design overview]</span></span>
* <span data-ttu-id="21a1b-248">[Distribuição de tabelas][Table distribution]</span><span class="sxs-lookup"><span data-stu-id="21a1b-248">[Table distribution][Table distribution]</span></span>
* <span data-ttu-id="21a1b-249">[Indexação de tabelas][Table indexing]</span><span class="sxs-lookup"><span data-stu-id="21a1b-249">[Table indexing][Table indexing]</span></span>
* <span data-ttu-id="21a1b-250">[Particionamento de tabelas][Table partitioning]</span><span class="sxs-lookup"><span data-stu-id="21a1b-250">[Table partitioning][Table partitioning]</span></span>
* <span data-ttu-id="21a1b-251">[Estatísticas de tabelas][Table statistics]</span><span class="sxs-lookup"><span data-stu-id="21a1b-251">[Table statistics][Table statistics]</span></span>
* <span data-ttu-id="21a1b-252">[Práticas recomendadas][Best practices]</span><span class="sxs-lookup"><span data-stu-id="21a1b-252">[Best practices][Best practices]</span></span>

<!--Image reference-->

<!--Article references-->
[data warehouse units (DWUs)]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[billed]: https://azure.microsoft.com/en-us/pricing/details/sql-data-warehouse/
[linearly]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[Scale compute power with Azure portal]: ./sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[Scale compute power with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#scale-compute-bk
[Scale compute power with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#scale-compute-bk
[Scale compute power with TSQL]: ./sql-data-warehouse-manage-compute-tsql.md#scale-compute-bk

[capacity limits]: ./sql-data-warehouse-service-capacity-limits.md

[Pause compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#pause-compute-bk
[Pause compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#pause-compute-bk
[Pause compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#pause-compute-bk

[Resume compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#resume-compute-bk
[Resume compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#resume-compute-bk
[Resume compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#resume-compute-bk

[Check database state with T-SQL]: ./sql-data-warehouse-manage-compute-tsql.md#check-database-state-and-operation-progress
[Check database state with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#check-database-state
[Check database state with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#check-database-state

[Workload and concurrency management]: ./sql-data-warehouse-develop-concurrency.md
[Table design overview]: ./sql-data-warehouse-tables-overview.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexing]: ./sql-data-warehouse-tables-index.md
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Table statistics]: ./sql-data-warehouse-tables-statistics.md
[Best practices]: ./sql-data-warehouse-best-practices.md
[development overview]: ./sql-data-warehouse-overview-develop.md

[SQL DB Contributor]: ../active-directory/role-based-access-built-in-roles.md#sql-db-contributor

<!--MSDN references-->
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx

<!--Other Web references-->
[Azure portal]: http://portal.azure.com/
