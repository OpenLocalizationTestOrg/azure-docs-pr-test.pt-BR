---
title: "Gerenciar potência de computação no SQL Data Warehouse do Azure (Visão geral) | Microsoft Docs"
description: "Funcionalidades de escala horizontal de desempenho no SQL Data Warehouse do Azure. Escale horizontalmente por meio de ajuste de DWUs ou, para economizar custos, pause e retome os recursos de computação."
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
ms.openlocfilehash: abe22f542a79714f6e894870872ee6b76ffe7633
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-overview"></a><span data-ttu-id="fbc42-104">Gerenciar poder de computação no SQL Data Warehouse do Azure (Visão Geral)</span><span class="sxs-lookup"><span data-stu-id="fbc42-104">Manage compute power in Azure SQL Data Warehouse (Overview)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fbc42-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="fbc42-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="fbc42-106">Portal</span><span class="sxs-lookup"><span data-stu-id="fbc42-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="fbc42-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fbc42-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="fbc42-108">REST</span><span class="sxs-lookup"><span data-stu-id="fbc42-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="fbc42-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="fbc42-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<span data-ttu-id="fbc42-110">A arquitetura do SQL Data Warehouse separa armazenamento e computação, permitindo que cada um seja dimensionado independentemente.</span><span class="sxs-lookup"><span data-stu-id="fbc42-110">The architecture of SQL Data Warehouse separates storage and compute, allowing each to scale independently.</span></span> <span data-ttu-id="fbc42-111">Como resultado, a computação pode ser dimensionada para atender às demandas de desempenho independentemente da quantidade de dados.</span><span class="sxs-lookup"><span data-stu-id="fbc42-111">As a result, compute can be scaled to meet performance demands independent of the amount of data.</span></span> <span data-ttu-id="fbc42-112">Uma consequência natural dessa arquitetura é que a [cobrança][billed] pela computação e pelo armazenamento é separada.</span><span class="sxs-lookup"><span data-stu-id="fbc42-112">A natural consequence of this architecture is that [billing][billed] for compute and storage is separate.</span></span> 

<span data-ttu-id="fbc42-113">Esta visão geral descreve como o escalonamento horizontal funciona com o SQL Data Warehouse e como utilizar os recursos de pausar, retomar e dimensionar do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="fbc42-113">This overview describes how scale out works with SQL Data Warehouse and how to utilize the pause, resume, and scale capabilities of SQL Data Warehouse.</span></span> <span data-ttu-id="fbc42-114">Consulte a página [DWUs (unidades do Data Warehouse)][data warehouse units (DWUs)] para saber como as DWUs e o desempenho estão relacionados.</span><span class="sxs-lookup"><span data-stu-id="fbc42-114">Consult the [data warehouse units (DWUs)][data warehouse units (DWUs)] page to learn how DWUs and performance are related.</span></span> 

## <a name="how-compute-management-operations-work-in-sql-data-warehouse"></a><span data-ttu-id="fbc42-115">Como as operações de gerenciamento de computação funcionam no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="fbc42-115">How compute management operations work in SQL Data Warehouse</span></span>
<span data-ttu-id="fbc42-116">A arquitetura para o SQL Data Warehouse consiste em um nó de controle, nós de computação e a camada de armazenamento espalhados por 60 distribuições.</span><span class="sxs-lookup"><span data-stu-id="fbc42-116">The architecture for SQL Data Warehouse consists of a control node, compute nodes, and the storage layer spread across 60 distributions.</span></span> 

<span data-ttu-id="fbc42-117">Durante uma sessão ativa normal no SQL Data Warehouse, o nó principal do sistema que gerencia os metadados e contém o otimizador de consulta distribuída.</span><span class="sxs-lookup"><span data-stu-id="fbc42-117">During a normal active session in SQL Data Warehouse, your system's head node manages the metadata and contains the distributed query optimizer.</span></span> <span data-ttu-id="fbc42-118">Sob esse nó principal estão os nós de computação e a camada de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fbc42-118">Beneath this head node are your compute nodes and your storage layer.</span></span> <span data-ttu-id="fbc42-119">Para um DWU 400, seu sistema tem um nó principal, quatro nós de computação e a camada de armazenamento, consistindo de 60 distribuições.</span><span class="sxs-lookup"><span data-stu-id="fbc42-119">For a DWU 400, your system has one head node, four compute nodes, and the storage layer, consisting of 60 distributions.</span></span> 

<span data-ttu-id="fbc42-120">Quando você passar por uma escala ou operação de pausa, o sistema primeiro interrompe todas as consultas de entrada e, em seguida, reverte as transações para assegurar um estado consistente.</span><span class="sxs-lookup"><span data-stu-id="fbc42-120">When you undergo a scale or pause operation, the system first kills all incoming queries and then rolls back transactions to ensure a consistent state.</span></span> <span data-ttu-id="fbc42-121">Para operações de escala, o dimensionamento só ocorrerá após a conclusão dessa reversão transacional.</span><span class="sxs-lookup"><span data-stu-id="fbc42-121">For scale operations, scaling will only occur once this transactional rollback has completed.</span></span> <span data-ttu-id="fbc42-122">Para uma operação de escalonamento vertical, o sistema provisiona o número desejado de nós de computação adicionais desejado e começa a reconectar os nós de computação à camada de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fbc42-122">For a scale-up operation, the system provisions the extra desired number of compute nodes, and then begins reattaching the compute nodes to the storage layer.</span></span> <span data-ttu-id="fbc42-123">Para uma operação de redução de escala, os nós desnecessários são liberados e os demais nós de computação reconectam-se ao número adequado de distribuições.</span><span class="sxs-lookup"><span data-stu-id="fbc42-123">For a scale-down operation, the unneeded nodes are released and the remaining compute nodes reattach themselves to the appropriate number of distributions.</span></span> <span data-ttu-id="fbc42-124">Para uma operação de pausa, todos os nós de computação são liberados e o sistema passará por uma variedade de operações de metadados para deixar o sistema final em um estado estável.</span><span class="sxs-lookup"><span data-stu-id="fbc42-124">For a pause operation, all compute nodes are released and your system will undergo a variety of metadata operations to leave your final system in a stable state.</span></span>

| <span data-ttu-id="fbc42-125">DWU</span><span class="sxs-lookup"><span data-stu-id="fbc42-125">DWU</span></span>  | <span data-ttu-id="fbc42-126">\# de nós de computação</span><span class="sxs-lookup"><span data-stu-id="fbc42-126">\#of compute nodes</span></span> | <span data-ttu-id="fbc42-127">\# de distribuições por nó</span><span class="sxs-lookup"><span data-stu-id="fbc42-127">\# of distributions per node</span></span> |
| ---- | ------------------ | ---------------------------- |
| <span data-ttu-id="fbc42-128">100</span><span class="sxs-lookup"><span data-stu-id="fbc42-128">100</span></span>  | <span data-ttu-id="fbc42-129">1</span><span class="sxs-lookup"><span data-stu-id="fbc42-129">1</span></span>                  | <span data-ttu-id="fbc42-130">60</span><span class="sxs-lookup"><span data-stu-id="fbc42-130">60</span></span>                           |
| <span data-ttu-id="fbc42-131">200</span><span class="sxs-lookup"><span data-stu-id="fbc42-131">200</span></span>  | <span data-ttu-id="fbc42-132">2</span><span class="sxs-lookup"><span data-stu-id="fbc42-132">2</span></span>                  | <span data-ttu-id="fbc42-133">30</span><span class="sxs-lookup"><span data-stu-id="fbc42-133">30</span></span>                           |
| <span data-ttu-id="fbc42-134">300</span><span class="sxs-lookup"><span data-stu-id="fbc42-134">300</span></span>  | <span data-ttu-id="fbc42-135">3</span><span class="sxs-lookup"><span data-stu-id="fbc42-135">3</span></span>                  | <span data-ttu-id="fbc42-136">20</span><span class="sxs-lookup"><span data-stu-id="fbc42-136">20</span></span>                           |
| <span data-ttu-id="fbc42-137">400</span><span class="sxs-lookup"><span data-stu-id="fbc42-137">400</span></span>  | <span data-ttu-id="fbc42-138">4</span><span class="sxs-lookup"><span data-stu-id="fbc42-138">4</span></span>                  | <span data-ttu-id="fbc42-139">15</span><span class="sxs-lookup"><span data-stu-id="fbc42-139">15</span></span>                           |
| <span data-ttu-id="fbc42-140">500</span><span class="sxs-lookup"><span data-stu-id="fbc42-140">500</span></span>  | <span data-ttu-id="fbc42-141">5</span><span class="sxs-lookup"><span data-stu-id="fbc42-141">5</span></span>                  | <span data-ttu-id="fbc42-142">12</span><span class="sxs-lookup"><span data-stu-id="fbc42-142">12</span></span>                           |
| <span data-ttu-id="fbc42-143">600</span><span class="sxs-lookup"><span data-stu-id="fbc42-143">600</span></span>  | <span data-ttu-id="fbc42-144">6</span><span class="sxs-lookup"><span data-stu-id="fbc42-144">6</span></span>                  | <span data-ttu-id="fbc42-145">10</span><span class="sxs-lookup"><span data-stu-id="fbc42-145">10</span></span>                           |
| <span data-ttu-id="fbc42-146">1000</span><span class="sxs-lookup"><span data-stu-id="fbc42-146">1000</span></span> | <span data-ttu-id="fbc42-147">10</span><span class="sxs-lookup"><span data-stu-id="fbc42-147">10</span></span>                 | <span data-ttu-id="fbc42-148">6</span><span class="sxs-lookup"><span data-stu-id="fbc42-148">6</span></span>                            |
| <span data-ttu-id="fbc42-149">1.200</span><span class="sxs-lookup"><span data-stu-id="fbc42-149">1200</span></span> | <span data-ttu-id="fbc42-150">12</span><span class="sxs-lookup"><span data-stu-id="fbc42-150">12</span></span>                 | <span data-ttu-id="fbc42-151">5</span><span class="sxs-lookup"><span data-stu-id="fbc42-151">5</span></span>                            |
| <span data-ttu-id="fbc42-152">1500</span><span class="sxs-lookup"><span data-stu-id="fbc42-152">1500</span></span> | <span data-ttu-id="fbc42-153">15</span><span class="sxs-lookup"><span data-stu-id="fbc42-153">15</span></span>                 | <span data-ttu-id="fbc42-154">4</span><span class="sxs-lookup"><span data-stu-id="fbc42-154">4</span></span>                            |
| <span data-ttu-id="fbc42-155">2000</span><span class="sxs-lookup"><span data-stu-id="fbc42-155">2000</span></span> | <span data-ttu-id="fbc42-156">20</span><span class="sxs-lookup"><span data-stu-id="fbc42-156">20</span></span>                 | <span data-ttu-id="fbc42-157">3</span><span class="sxs-lookup"><span data-stu-id="fbc42-157">3</span></span>                            |
| <span data-ttu-id="fbc42-158">3000</span><span class="sxs-lookup"><span data-stu-id="fbc42-158">3000</span></span> | <span data-ttu-id="fbc42-159">30</span><span class="sxs-lookup"><span data-stu-id="fbc42-159">30</span></span>                 | <span data-ttu-id="fbc42-160">2</span><span class="sxs-lookup"><span data-stu-id="fbc42-160">2</span></span>                            |
| <span data-ttu-id="fbc42-161">6000</span><span class="sxs-lookup"><span data-stu-id="fbc42-161">6000</span></span> | <span data-ttu-id="fbc42-162">60</span><span class="sxs-lookup"><span data-stu-id="fbc42-162">60</span></span>                 | <span data-ttu-id="fbc42-163">1</span><span class="sxs-lookup"><span data-stu-id="fbc42-163">1</span></span>                            |

<span data-ttu-id="fbc42-164">As três funções principais para o gerenciamento de computação são:</span><span class="sxs-lookup"><span data-stu-id="fbc42-164">The three primary functions for managing compute are:</span></span>

1. <span data-ttu-id="fbc42-165">Pausar</span><span class="sxs-lookup"><span data-stu-id="fbc42-165">Pause</span></span>
2. <span data-ttu-id="fbc42-166">Continuar</span><span class="sxs-lookup"><span data-stu-id="fbc42-166">Resume</span></span>
3. <span data-ttu-id="fbc42-167">Escala</span><span class="sxs-lookup"><span data-stu-id="fbc42-167">Scale</span></span>

<span data-ttu-id="fbc42-168">Cada uma dessas operações pode levar vários minutos para ser concluída.</span><span class="sxs-lookup"><span data-stu-id="fbc42-168">Each of these operations may take several minutes to complete.</span></span> <span data-ttu-id="fbc42-169">Se você estiver dimensionando/pausando/retomando automaticamente, talvez você queira implementar a lógica para assegurar que determinadas operações tenham sido concluídas antes de prosseguir com outra ação.</span><span class="sxs-lookup"><span data-stu-id="fbc42-169">If you are scaling/pausing/resuming automatically, you may want to implement logic to ensure that certain operations have been completed before proceeding with another action.</span></span> 

<span data-ttu-id="fbc42-170">Verificar o estado do banco de dados por meio de vários pontos de extremidade permitirá que você implemente corretamente a automação dessas operações.</span><span class="sxs-lookup"><span data-stu-id="fbc42-170">Checking the database state through various endpoints will allow you to correctly implement automation of such operations.</span></span> <span data-ttu-id="fbc42-171">O portal fornecerá uma notificação após a conclusão de uma operação e o estado atual do bancos de dados, mas não permite a verificação de estado programática.</span><span class="sxs-lookup"><span data-stu-id="fbc42-171">The portal will provide notification upon completion of an operation and the databases current state but does not allow for programmatic checking of state.</span></span> 

>  [!NOTE]
>
>  <span data-ttu-id="fbc42-172">A funcionalidade de gerenciamento de computação não existe em todos os pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="fbc42-172">Compute management functionality does not exist across all endpoints.</span></span>
>
>  

|              | <span data-ttu-id="fbc42-173">Pausar/Retomar</span><span class="sxs-lookup"><span data-stu-id="fbc42-173">Pause/Resume</span></span> | <span data-ttu-id="fbc42-174">Escala</span><span class="sxs-lookup"><span data-stu-id="fbc42-174">Scale</span></span> | <span data-ttu-id="fbc42-175">Verificar estado do banco de dados</span><span class="sxs-lookup"><span data-stu-id="fbc42-175">Check database state</span></span> |
| ------------ | ------------ | ----- | -------------------- |
| <span data-ttu-id="fbc42-176">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="fbc42-176">Azure portal</span></span> | <span data-ttu-id="fbc42-177">Sim</span><span class="sxs-lookup"><span data-stu-id="fbc42-177">Yes</span></span>          | <span data-ttu-id="fbc42-178">Sim</span><span class="sxs-lookup"><span data-stu-id="fbc42-178">Yes</span></span>   | <span data-ttu-id="fbc42-179">**Não**</span><span class="sxs-lookup"><span data-stu-id="fbc42-179">**No**</span></span>               |
| <span data-ttu-id="fbc42-180">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fbc42-180">PowerShell</span></span>   | <span data-ttu-id="fbc42-181">Sim</span><span class="sxs-lookup"><span data-stu-id="fbc42-181">Yes</span></span>          | <span data-ttu-id="fbc42-182">Sim</span><span class="sxs-lookup"><span data-stu-id="fbc42-182">Yes</span></span>   | <span data-ttu-id="fbc42-183">Sim</span><span class="sxs-lookup"><span data-stu-id="fbc42-183">Yes</span></span>                  |
| <span data-ttu-id="fbc42-184">API REST</span><span class="sxs-lookup"><span data-stu-id="fbc42-184">REST API</span></span>     | <span data-ttu-id="fbc42-185">Sim</span><span class="sxs-lookup"><span data-stu-id="fbc42-185">Yes</span></span>          | <span data-ttu-id="fbc42-186">Sim</span><span class="sxs-lookup"><span data-stu-id="fbc42-186">Yes</span></span>   | <span data-ttu-id="fbc42-187">Sim</span><span class="sxs-lookup"><span data-stu-id="fbc42-187">Yes</span></span>                  |
| <span data-ttu-id="fbc42-188">T-SQL</span><span class="sxs-lookup"><span data-stu-id="fbc42-188">T-SQL</span></span>        | <span data-ttu-id="fbc42-189">**Não**</span><span class="sxs-lookup"><span data-stu-id="fbc42-189">**No**</span></span>       | <span data-ttu-id="fbc42-190">Sim</span><span class="sxs-lookup"><span data-stu-id="fbc42-190">Yes</span></span>   | <span data-ttu-id="fbc42-191">Sim</span><span class="sxs-lookup"><span data-stu-id="fbc42-191">Yes</span></span>                  |



<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a><span data-ttu-id="fbc42-192">Computação de escala</span><span class="sxs-lookup"><span data-stu-id="fbc42-192">Scale compute</span></span>

<span data-ttu-id="fbc42-193">O desempenho no SQL Data Warehouse é medido em [DWUs (unidades do data warehouse)][data warehouse units (DWUs)], que é uma medida abstrata de recursos de computação como CPU, memória e E/S de largura de banda.</span><span class="sxs-lookup"><span data-stu-id="fbc42-193">Performance in SQL Data Warehouse is measured in [data warehouse units (DWUs)][data warehouse units (DWUs)] which is an abstracted measure of compute resources such as CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="fbc42-194">Um usuário que deseja dimensionar o desempenho do seu sistema pode fazer isso de várias maneiras, por exemplo, por meio do portal, T-SQL e APIs REST.</span><span class="sxs-lookup"><span data-stu-id="fbc42-194">A user who wishes to scale their system's performance can do so through various means, such as through the portal, T-SQL, and REST APIs.</span></span> 

### <a name="how-do-i-scale-compute"></a><span data-ttu-id="fbc42-195">Como eu dimensiono a computação?</span><span class="sxs-lookup"><span data-stu-id="fbc42-195">How do I scale compute?</span></span>
<span data-ttu-id="fbc42-196">O poder de computação é gerenciado pelo seu SQL Data Warehouse alterando a configuração de DWU.</span><span class="sxs-lookup"><span data-stu-id="fbc42-196">Compute power is managed for you SQL Data Warehouse by changing the DWU setting.</span></span> <span data-ttu-id="fbc42-197">O desempenho aumenta [linearmente][linearly] conforme você adiciona mais DWUs para determinadas operações.</span><span class="sxs-lookup"><span data-stu-id="fbc42-197">Performance increases [linearly][linearly] as you add more DWU for certain operations.</span></span>  <span data-ttu-id="fbc42-198">Temos ofertas de DWU que asseguram que o desempenho será alterado visivelmente quando você escalar ou reduzir verticalmente seu sistema.</span><span class="sxs-lookup"><span data-stu-id="fbc42-198">We offer DWU offerings that ensure that your performance will change noticeably when you scale your system up or down.</span></span> 

<span data-ttu-id="fbc42-199">Para ajustar DWUs, você pode usar qualquer um destes métodos individuais.</span><span class="sxs-lookup"><span data-stu-id="fbc42-199">To adjust DWUs, you can use any of these individual methods.</span></span>

* <span data-ttu-id="fbc42-200">[Dimensionar a potência de computação com o Portal do Azure][Scale compute power with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="fbc42-200">[Scale compute power with Azure portal][Scale compute power with Azure portal]</span></span>
* <span data-ttu-id="fbc42-201">[Dimensionar a potência de computação com o PowerShell][Scale compute power with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="fbc42-201">[Scale compute power with PowerShell][Scale compute power with PowerShell]</span></span>
* <span data-ttu-id="fbc42-202">[Dimensionar a potência de computação com APIs REST][Scale compute power with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="fbc42-202">[Scale compute power with REST APIs][Scale compute power with REST APIs]</span></span>
* <span data-ttu-id="fbc42-203">[Dimensionar a potência de computação com o TSQL][Scale compute power with TSQL]</span><span class="sxs-lookup"><span data-stu-id="fbc42-203">[Scale compute power with TSQL][Scale compute power with TSQL]</span></span>

### <a name="how-many-dwus-should-i-use"></a><span data-ttu-id="fbc42-204">Quantas DWUs devo usar?</span><span class="sxs-lookup"><span data-stu-id="fbc42-204">How many DWUs should I use?</span></span>

<span data-ttu-id="fbc42-205">Para entender qual é o valor ideal de DWU é, tente escalar verticalmente, para cima e para baixo, e executar algumas consultas após carregar os dados.</span><span class="sxs-lookup"><span data-stu-id="fbc42-205">To understand what your ideal DWU value is, try scaling up and down, and running a few queries after loading your data.</span></span> <span data-ttu-id="fbc42-206">Como o dimensionamento é rápido, você pode experimentar vários níveis de desempenho diferentes durante uma hora ou menos.</span><span class="sxs-lookup"><span data-stu-id="fbc42-206">Since scaling is quick, you can try various performance levels in an hour or less.</span></span> 

> [!Note] 
> <span data-ttu-id="fbc42-207">O SQL Data Warehouse é projetado para processar grandes quantidades de dados.</span><span class="sxs-lookup"><span data-stu-id="fbc42-207">SQL Data Warehouse is designed to process large amounts of data.</span></span> <span data-ttu-id="fbc42-208">Para ver suas verdadeiras capacidades de dimensionamento, especialmente com DWUs maiores, é melhor você usar um grande conjunto de dados que se aproxime de 1 TB ou ultrapasse esse tamanho.</span><span class="sxs-lookup"><span data-stu-id="fbc42-208">To see its true capabilities for scaling, especially at larger DWUs, you want to use a large data set which approaches or exceeds 1 TB.</span></span>

<span data-ttu-id="fbc42-209">Recomendações para encontrar a melhor DWU para sua carga de trabalho:</span><span class="sxs-lookup"><span data-stu-id="fbc42-209">Recommendations for finding the best DWU for your workload:</span></span>

1. <span data-ttu-id="fbc42-210">Para um data warehouse em desenvolvimento, comece selecionando um nível de desempenho de DWU menor.</span><span class="sxs-lookup"><span data-stu-id="fbc42-210">For a data warehouse in development, begin by selecting a smaller DWU performance level.</span></span>  <span data-ttu-id="fbc42-211">Um bom ponto de partida é DW400 ou DW200.</span><span class="sxs-lookup"><span data-stu-id="fbc42-211">A good starting point is DW400 or DW200.</span></span>
2. <span data-ttu-id="fbc42-212">Monitore o desempenho do seu aplicativo, observando o número de DWUs selecionadas comparado ao desempenho que você observar.</span><span class="sxs-lookup"><span data-stu-id="fbc42-212">Monitor your application performance, observing the number of DWUs selected compared to the performance you observe.</span></span>
3. <span data-ttu-id="fbc42-213">Determine quão rápido ou lento o desempenho deve ser para você obter o nível de desempenho ideal para seus requisitos, presumindo uma escala linear.</span><span class="sxs-lookup"><span data-stu-id="fbc42-213">Determine how much faster or slower performance should be for you to reach the optimum performance level for your requirements by assuming linear scale.</span></span>
4. <span data-ttu-id="fbc42-214">Aumente ou diminua o número de DWUs proporcionalmente à velocidade desejada do desempenho de sua carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="fbc42-214">Increase or decrease the number of DWUs in proportion to how much faster or slower you want your workload to perform.</span></span> 
5. <span data-ttu-id="fbc42-215">Continue fazendo ajustes até alcançar um nível de desempenho ideal para seus requisitos de negócios.</span><span class="sxs-lookup"><span data-stu-id="fbc42-215">Continue making adjustments until you reach an optimum performance level for your business requirements.</span></span>

> [!NOTE]
>
> <span data-ttu-id="fbc42-216">O desempenho de consulta só aumentará com mais paralelização se o trabalho puder ser dividido entre nós de computação.</span><span class="sxs-lookup"><span data-stu-id="fbc42-216">Query performance only increases with more parallelization if the work can be split between compute nodes.</span></span> <span data-ttu-id="fbc42-217">Se você achar que o dimensionamento não está alterando seu desempenho, verifique nossos artigos sobre ajuste de desempenho para verificar se os dados são distribuídos sem uniformidade ou se você está implantando uma grande quantidade de movimentação de dados.</span><span class="sxs-lookup"><span data-stu-id="fbc42-217">If you find that scaling is not changing your performance, please check out our performance tuning articles to check whether your data is unevenly distributed or if you are introducing a large amount of data movement.</span></span> 

### <a name="when-should-i-scale-dwus"></a><span data-ttu-id="fbc42-218">Quando devo dimensionar as DWUs?</span><span class="sxs-lookup"><span data-stu-id="fbc42-218">When should I scale DWUs?</span></span>
<span data-ttu-id="fbc42-219">O dimensionamento de DWUs altera os seguintes cenários importantes:</span><span class="sxs-lookup"><span data-stu-id="fbc42-219">Scaling DWUs alters the following important scenarios:</span></span>

1. <span data-ttu-id="fbc42-220">Alteração linear do desempenho do sistema para verificações, agregações e instruções de CTAS</span><span class="sxs-lookup"><span data-stu-id="fbc42-220">Linearly changing performance of the system for scans, aggregations, and CTAS statements</span></span>
2. <span data-ttu-id="fbc42-221">Aumento do número de leitores e gravadores ao carregar com o PolyBase</span><span class="sxs-lookup"><span data-stu-id="fbc42-221">Increasing the number of readers and writers when loading with PolyBase</span></span>
3. <span data-ttu-id="fbc42-222">Número máximo de consultas simultâneas e slots de simultaneidade</span><span class="sxs-lookup"><span data-stu-id="fbc42-222">Maximum number of concurrent queries and concurrency slots</span></span>

<span data-ttu-id="fbc42-223">Recomendações para quando dimensionar DWUs:</span><span class="sxs-lookup"><span data-stu-id="fbc42-223">Recommendations for when to scale DWUs:</span></span>

1. <span data-ttu-id="fbc42-224">Antes de executar uma operação de transformação ou carregamento de dados pesados, escale verticalmente as DWUs para que os dados fiquem disponíveis mais rapidamente.</span><span class="sxs-lookup"><span data-stu-id="fbc42-224">Before you perform a heavy data loading or transformation operation, scale up DWUs so that your data is available more quickly.</span></span>
2. <span data-ttu-id="fbc42-225">Durante o horário comercial de pico, dimensione para acomodar um número maior de consultas simultâneas.</span><span class="sxs-lookup"><span data-stu-id="fbc42-225">During peak business hours, scale to accommodate larger numbers of concurrent queries.</span></span> 

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="fbc42-226">Pausar computação</span><span class="sxs-lookup"><span data-stu-id="fbc42-226">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="fbc42-227">Para pausar um banco de dados, use qualquer um destes métodos individuais.</span><span class="sxs-lookup"><span data-stu-id="fbc42-227">To pause a database, use any of these individual methods.</span></span>

* <span data-ttu-id="fbc42-228">[Pausar a computação com o Portal do Azure][Pause compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="fbc42-228">[Pause compute with Azure portal][Pause compute with Azure portal]</span></span>
* <span data-ttu-id="fbc42-229">[Pausar a computação com o PowerShell][Pause compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="fbc42-229">[Pause compute with PowerShell][Pause compute with PowerShell]</span></span>
* <span data-ttu-id="fbc42-230">[Pausar a computação com APIs REST][Pause compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="fbc42-230">[Pause compute with REST APIs][Pause compute with REST APIs]</span></span>

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="fbc42-231">Retomar a computação</span><span class="sxs-lookup"><span data-stu-id="fbc42-231">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="fbc42-232">Para retomar um banco de dados, use qualquer um destes métodos individuais.</span><span class="sxs-lookup"><span data-stu-id="fbc42-232">To resume a database, use any of these individual methods.</span></span>

* <span data-ttu-id="fbc42-233">[Retomar a computação com o Portal do Azure][Resume compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="fbc42-233">[Resume compute with Azure portal][Resume compute with Azure portal]</span></span>
* <span data-ttu-id="fbc42-234">[Retomar a computação com o PowerShell][Resume compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="fbc42-234">[Resume compute with PowerShell][Resume compute with PowerShell]</span></span>
* <span data-ttu-id="fbc42-235">[Retomar a computação com APIs REST][Resume compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="fbc42-235">[Resume compute with REST APIs][Resume compute with REST APIs]</span></span>

<a name="check-compute-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="fbc42-236">Verificar estado do banco de dados</span><span class="sxs-lookup"><span data-stu-id="fbc42-236">Check database state</span></span> 

<span data-ttu-id="fbc42-237">Para retomar um banco de dados, use qualquer um destes métodos individuais.</span><span class="sxs-lookup"><span data-stu-id="fbc42-237">To resume a database, use any of these individual methods.</span></span>

- <span data-ttu-id="fbc42-238">[Verificar estado do banco de dados com o T-SQL][Check database state with T-SQL]</span><span class="sxs-lookup"><span data-stu-id="fbc42-238">[Check database state with T-SQL][Check database state with T-SQL]</span></span>
- <span data-ttu-id="fbc42-239">[Verificar estado do banco de dados com o PowerShell][Check database state with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="fbc42-239">[Check database state with PowerShell][Check database state with PowerShell]</span></span>
- <span data-ttu-id="fbc42-240">[Verificar estado do banco de dados com o APIs REST][Check database state with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="fbc42-240">[Check database state with REST APIs][Check database state with REST APIs]</span></span>

## <a name="permissions"></a><span data-ttu-id="fbc42-241">Permissões</span><span class="sxs-lookup"><span data-stu-id="fbc42-241">Permissions</span></span>

<span data-ttu-id="fbc42-242">Dimensionar o banco de dados exige as permissões descritas em [ALTERAR BANCO DE DADOS][ALTER DATABASE].</span><span class="sxs-lookup"><span data-stu-id="fbc42-242">Scaling the database requires the permissions described in [ALTER DATABASE][ALTER DATABASE].</span></span>  <span data-ttu-id="fbc42-243">Pausar e Retomar exigirá a permissão [Colaborador do BD SQL][SQL DB Contributor], especificamente Microsoft.Sql/servers/databases/action.</span><span class="sxs-lookup"><span data-stu-id="fbc42-243">Pause and Resume require the [SQL DB Contributor][SQL DB Contributor] permission, specifically Microsoft.Sql/servers/databases/action.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="fbc42-244">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fbc42-244">Next steps</span></span>
<span data-ttu-id="fbc42-245">Consulte os artigos a seguir para ajudar a entender alguns dos principais conceitos de desempenho adicionais:</span><span class="sxs-lookup"><span data-stu-id="fbc42-245">Refer to the following articles to help you understand some additional key performance concepts:</span></span>

* <span data-ttu-id="fbc42-246">[Gerenciamento da carga de trabalho e simultaneidade][Workload and concurrency management]</span><span class="sxs-lookup"><span data-stu-id="fbc42-246">[Workload and concurrency management][Workload and concurrency management]</span></span>
* <span data-ttu-id="fbc42-247">[Visão geral do design da tabela][Table design overview]</span><span class="sxs-lookup"><span data-stu-id="fbc42-247">[Table design overview][Table design overview]</span></span>
* <span data-ttu-id="fbc42-248">[Distribuição de tabelas][Table distribution]</span><span class="sxs-lookup"><span data-stu-id="fbc42-248">[Table distribution][Table distribution]</span></span>
* <span data-ttu-id="fbc42-249">[Indexação de tabelas][Table indexing]</span><span class="sxs-lookup"><span data-stu-id="fbc42-249">[Table indexing][Table indexing]</span></span>
* <span data-ttu-id="fbc42-250">[Particionamento de tabelas][Table partitioning]</span><span class="sxs-lookup"><span data-stu-id="fbc42-250">[Table partitioning][Table partitioning]</span></span>
* <span data-ttu-id="fbc42-251">[Estatísticas de tabelas][Table statistics]</span><span class="sxs-lookup"><span data-stu-id="fbc42-251">[Table statistics][Table statistics]</span></span>
* <span data-ttu-id="fbc42-252">[Práticas recomendadas][Best practices]</span><span class="sxs-lookup"><span data-stu-id="fbc42-252">[Best practices][Best practices]</span></span>

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
