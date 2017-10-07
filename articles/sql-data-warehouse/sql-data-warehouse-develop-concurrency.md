---
title: gerenciamento de aaaConcurrency e carga de trabalho no SQL Data Warehouse | Microsoft Docs
description: "Compreender o gerenciamento de simultaneidade e carga de trabalho no SQL Data Warehouse do Azure para desenvolvimento de soluções."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 08/23/2017
ms.author: joeyong;barbkess;kavithaj
ms.openlocfilehash: 7f7e77aa687760252aed16573b609817ed9111c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="concurrency-and-workload-management-in-sql-data-warehouse"></a><span data-ttu-id="a5115-103">Gerenciamento de simultaneidade e carga de trabalho no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a5115-103">Concurrency and workload management in SQL Data Warehouse</span></span>
<span data-ttu-id="a5115-104">um desempenho previsível em grande escala, Microsoft Azure SQL Data Warehouse toodeliver ajuda a controlar os níveis de simultaneidade e alocações de recursos como priorização de CPU e memória.</span><span class="sxs-lookup"><span data-stu-id="a5115-104">toodeliver predictable performance at scale, Microsoft Azure SQL Data Warehouse helps you control concurrency levels and resource allocations like memory and CPU prioritization.</span></span> <span data-ttu-id="a5115-105">Este artigo apresenta os conceitos de toohello de gerenciamento de simultaneidade e a carga de trabalho, explicando como ambos os recursos foram implementados e como você pode controlá-los no data warehouse.</span><span class="sxs-lookup"><span data-stu-id="a5115-105">This article introduces you toohello concepts of concurrency and workload management, explaining how both features have been implemented and how you can control them in your data warehouse.</span></span> <span data-ttu-id="a5115-106">Gerenciamento de carga de trabalho do SQL Data Warehouse é pretendido toohelp você oferece suporte a ambientes de vários usuários.</span><span class="sxs-lookup"><span data-stu-id="a5115-106">SQL Data Warehouse workload management is intended toohelp you support multi-user environments.</span></span> <span data-ttu-id="a5115-107">Ele não se destina a cargas de trabalho com vários locatários.</span><span class="sxs-lookup"><span data-stu-id="a5115-107">It is not intended for multi-tenant workloads.</span></span>

## <a name="concurrency-limits"></a><span data-ttu-id="a5115-108">Limites de simultaneidade</span><span class="sxs-lookup"><span data-stu-id="a5115-108">Concurrency limits</span></span>
<span data-ttu-id="a5115-109">SQL Data Warehouse permite que até too1, 024 conexões simultâneas.</span><span class="sxs-lookup"><span data-stu-id="a5115-109">SQL Data Warehouse allows up too1,024 concurrent connections.</span></span> <span data-ttu-id="a5115-110">Todas as 1.024 conexões podem enviar consultas ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="a5115-110">All 1,024 connections can submit queries concurrently.</span></span> <span data-ttu-id="a5115-111">No entanto, taxa de transferência toooptimize, SQL Data Warehouse pode enfileirar tooensure algumas consultas que cada consulta recebe uma concessão de memória mínima.</span><span class="sxs-lookup"><span data-stu-id="a5115-111">However, toooptimize throughput, SQL Data Warehouse may queue some queries tooensure that each query receives a minimal memory grant.</span></span> <span data-ttu-id="a5115-112">O enfileiramento ocorre no tempo de execução de consulta.</span><span class="sxs-lookup"><span data-stu-id="a5115-112">Queuing occurs at query execution time.</span></span> <span data-ttu-id="a5115-113">Por consultas de enfileiramento de mensagens quando simultaneidade limites são atingidos, o SQL Data Warehouse pode aumentar a taxa de transferência total, garantindo que consultas ativas obtenham acesso toocritically necessários recursos de memória.</span><span class="sxs-lookup"><span data-stu-id="a5115-113">By queuing queries when concurrency limits are reached, SQL Data Warehouse can increase total throughput by ensuring that active queries get access toocritically needed memory resources.</span></span>  

<span data-ttu-id="a5115-114">Os limites de simultaneidade são regidos por dois conceitos: *consultas simultâneas* e *slots de simultaneidade*.</span><span class="sxs-lookup"><span data-stu-id="a5115-114">Concurrency limits are governed by two concepts: *concurrent queries* and *concurrency slots*.</span></span> <span data-ttu-id="a5115-115">Para tooexecute uma consulta, ele deve executar dentro do limite de simultaneidade de consultas hello e alocação de slot de simultaneidade hello.</span><span class="sxs-lookup"><span data-stu-id="a5115-115">For a query tooexecute, it must execute within both hello query concurrency limit and hello concurrency slot allocation.</span></span>

* <span data-ttu-id="a5115-116">Consultas simultâneas são consultas de saudação em execução a saudação mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="a5115-116">Concurrent queries are hello queries executing at hello same time.</span></span> <span data-ttu-id="a5115-117">SQL Data Warehouse dá suporte para até too32 de consultas simultâneas em Olá DWU maiores.</span><span class="sxs-lookup"><span data-stu-id="a5115-117">SQL Data Warehouse supports up too32 concurrent queries on hello larger DWU sizes.</span></span>
* <span data-ttu-id="a5115-118">Os slots de simultaneidade são alocados com base em DWU.</span><span class="sxs-lookup"><span data-stu-id="a5115-118">Concurrency slots are allocated based on DWU.</span></span> <span data-ttu-id="a5115-119">Cada DWU 100 fornece quatro slots de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="a5115-119">Each 100 DWU provides 4 concurrency slots.</span></span> <span data-ttu-id="a5115-120">Por exemplo, um DW100 aloca quatro slots de simultaneidade e um DW1000 aloca 40.</span><span class="sxs-lookup"><span data-stu-id="a5115-120">For example, a DW100 allocates 4 concurrency slots and DW1000 allocates 40.</span></span> <span data-ttu-id="a5115-121">Cada consulta consome um ou mais simultaneidade slots, dependentes Olá [classe de recurso](#resource-classes) de consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="a5115-121">Each query consumes one or more concurrency slots, dependent on hello [resource class](#resource-classes) of hello query.</span></span> <span data-ttu-id="a5115-122">Consultas em execução na classe de recurso de smallrc Olá consumam um slot de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="a5115-122">Queries running in hello smallrc resource class consume one concurrency slot.</span></span> <span data-ttu-id="a5115-123">As consultas em execução em uma classe de recurso superior consomem mais slots de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="a5115-123">Queries running in a higher resource class consume more concurrency slots.</span></span>

<span data-ttu-id="a5115-124">Olá tabela a seguir descreve limites Olá para consultas simultâneas e slots de simultaneidade em Olá vários tamanhos DWU.</span><span class="sxs-lookup"><span data-stu-id="a5115-124">hello following table describes hello limits for both concurrent queries and concurrency slots at hello various DWU sizes.</span></span>

### <a name="concurrency-limits"></a><span data-ttu-id="a5115-125">Limites de simultaneidade</span><span class="sxs-lookup"><span data-stu-id="a5115-125">Concurrency limits</span></span>
| <span data-ttu-id="a5115-126">DWU</span><span class="sxs-lookup"><span data-stu-id="a5115-126">DWU</span></span> | <span data-ttu-id="a5115-127">Máximo de consultas simultâneas</span><span class="sxs-lookup"><span data-stu-id="a5115-127">Max concurrent queries</span></span> | <span data-ttu-id="a5115-128">Slots de simultaneidade alocados</span><span class="sxs-lookup"><span data-stu-id="a5115-128">Concurrency slots allocated</span></span> |
|:--- |:---:|:---:|
| <span data-ttu-id="a5115-129">DW100</span><span class="sxs-lookup"><span data-stu-id="a5115-129">DW100</span></span> |<span data-ttu-id="a5115-130">4</span><span class="sxs-lookup"><span data-stu-id="a5115-130">4</span></span> |<span data-ttu-id="a5115-131">4</span><span class="sxs-lookup"><span data-stu-id="a5115-131">4</span></span> |
| <span data-ttu-id="a5115-132">DW200</span><span class="sxs-lookup"><span data-stu-id="a5115-132">DW200</span></span> |<span data-ttu-id="a5115-133">8</span><span class="sxs-lookup"><span data-stu-id="a5115-133">8</span></span> |<span data-ttu-id="a5115-134">8</span><span class="sxs-lookup"><span data-stu-id="a5115-134">8</span></span> |
| <span data-ttu-id="a5115-135">DW300</span><span class="sxs-lookup"><span data-stu-id="a5115-135">DW300</span></span> |<span data-ttu-id="a5115-136">12</span><span class="sxs-lookup"><span data-stu-id="a5115-136">12</span></span> |<span data-ttu-id="a5115-137">12</span><span class="sxs-lookup"><span data-stu-id="a5115-137">12</span></span> |
| <span data-ttu-id="a5115-138">DW400</span><span class="sxs-lookup"><span data-stu-id="a5115-138">DW400</span></span> |<span data-ttu-id="a5115-139">16</span><span class="sxs-lookup"><span data-stu-id="a5115-139">16</span></span> |<span data-ttu-id="a5115-140">16</span><span class="sxs-lookup"><span data-stu-id="a5115-140">16</span></span> |
| <span data-ttu-id="a5115-141">DW500</span><span class="sxs-lookup"><span data-stu-id="a5115-141">DW500</span></span> |<span data-ttu-id="a5115-142">20</span><span class="sxs-lookup"><span data-stu-id="a5115-142">20</span></span> |<span data-ttu-id="a5115-143">20</span><span class="sxs-lookup"><span data-stu-id="a5115-143">20</span></span> |
| <span data-ttu-id="a5115-144">DW600</span><span class="sxs-lookup"><span data-stu-id="a5115-144">DW600</span></span> |<span data-ttu-id="a5115-145">24</span><span class="sxs-lookup"><span data-stu-id="a5115-145">24</span></span> |<span data-ttu-id="a5115-146">24</span><span class="sxs-lookup"><span data-stu-id="a5115-146">24</span></span> |
| <span data-ttu-id="a5115-147">DW1000</span><span class="sxs-lookup"><span data-stu-id="a5115-147">DW1000</span></span> |<span data-ttu-id="a5115-148">32</span><span class="sxs-lookup"><span data-stu-id="a5115-148">32</span></span> |<span data-ttu-id="a5115-149">40</span><span class="sxs-lookup"><span data-stu-id="a5115-149">40</span></span> |
| <span data-ttu-id="a5115-150">DW1200</span><span class="sxs-lookup"><span data-stu-id="a5115-150">DW1200</span></span> |<span data-ttu-id="a5115-151">32</span><span class="sxs-lookup"><span data-stu-id="a5115-151">32</span></span> |<span data-ttu-id="a5115-152">48</span><span class="sxs-lookup"><span data-stu-id="a5115-152">48</span></span> |
| <span data-ttu-id="a5115-153">DW1500</span><span class="sxs-lookup"><span data-stu-id="a5115-153">DW1500</span></span> |<span data-ttu-id="a5115-154">32</span><span class="sxs-lookup"><span data-stu-id="a5115-154">32</span></span> |<span data-ttu-id="a5115-155">60</span><span class="sxs-lookup"><span data-stu-id="a5115-155">60</span></span> |
| <span data-ttu-id="a5115-156">DW2000</span><span class="sxs-lookup"><span data-stu-id="a5115-156">DW2000</span></span> |<span data-ttu-id="a5115-157">32</span><span class="sxs-lookup"><span data-stu-id="a5115-157">32</span></span> |<span data-ttu-id="a5115-158">80</span><span class="sxs-lookup"><span data-stu-id="a5115-158">80</span></span> |
| <span data-ttu-id="a5115-159">DW3000</span><span class="sxs-lookup"><span data-stu-id="a5115-159">DW3000</span></span> |<span data-ttu-id="a5115-160">32</span><span class="sxs-lookup"><span data-stu-id="a5115-160">32</span></span> |<span data-ttu-id="a5115-161">120</span><span class="sxs-lookup"><span data-stu-id="a5115-161">120</span></span> |
| <span data-ttu-id="a5115-162">DW6000</span><span class="sxs-lookup"><span data-stu-id="a5115-162">DW6000</span></span> |<span data-ttu-id="a5115-163">32</span><span class="sxs-lookup"><span data-stu-id="a5115-163">32</span></span> |<span data-ttu-id="a5115-164">240</span><span class="sxs-lookup"><span data-stu-id="a5115-164">240</span></span> |

<span data-ttu-id="a5115-165">Quando um desses limites for atingido, novas consultas serão enfileiradas e executadas em uma base de primeira a entrar, primeira a sair.</span><span class="sxs-lookup"><span data-stu-id="a5115-165">When one of these thresholds is met, new queries are queued and executed on a first-in, first-out basis.</span></span>  <span data-ttu-id="a5115-166">Como um consultas for concluído e número de saudação de consultas e slots cai abaixo limites hello, consultas em fila são liberadas.</span><span class="sxs-lookup"><span data-stu-id="a5115-166">As a queries finishes and hello number of queries and slots falls below hello limits, queued queries are released.</span></span> 

> [!NOTE]  
> <span data-ttu-id="a5115-167">*Selecione* consultas executando exclusivamente em exibições de gerenciamento dinâmico (DMVs) ou exibições do catálogo não são regidas por qualquer um dos limites de simultaneidade hello.</span><span class="sxs-lookup"><span data-stu-id="a5115-167">*Select* queries executing exclusively on dynamic management views (DMVs) or catalog views are not governed by any of hello concurrency limits.</span></span> <span data-ttu-id="a5115-168">Você pode monitorar o sistema hello, independentemente do número de saudação de consultas em execução nele.</span><span class="sxs-lookup"><span data-stu-id="a5115-168">You can monitor hello system regardless of hello number of queries executing on it.</span></span>
> 
> 

## <a name="resource-classes"></a><span data-ttu-id="a5115-169">Classes de recursos</span><span class="sxs-lookup"><span data-stu-id="a5115-169">Resource classes</span></span>
<span data-ttu-id="a5115-170">Classes de recursos ajudam a controlar dado consulta de tooa de ciclos de CPU e alocação de memória.</span><span class="sxs-lookup"><span data-stu-id="a5115-170">Resource classes help you control memory allocation and CPU cycles given tooa query.</span></span> <span data-ttu-id="a5115-171">Você pode atribuir dois tipos de usuário de tooa de classes de recurso na forma de saudação de funções de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a5115-171">You can assign two types of resource classes tooa user in hello form of database roles.</span></span> <span data-ttu-id="a5115-172">Olá dois tipos de classes de recurso são da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="a5115-172">hello two types of resource classes are as follows:</span></span>
1. <span data-ttu-id="a5115-173">Classes de recursos dinâmicos (**smallrc, mediumrc, largerc, xlargerc**) alocar uma variável quantidade de memória dependendo Olá DWU atual.</span><span class="sxs-lookup"><span data-stu-id="a5115-173">Dynamic Resource Classes (**smallrc, mediumrc, largerc, xlargerc**) allocate a variable amount of memory depending on hello current DWU.</span></span> <span data-ttu-id="a5115-174">Isso significa que, quando você escala verticalmente tooa DWU maior, suas consultas obtém automaticamente mais memória.</span><span class="sxs-lookup"><span data-stu-id="a5115-174">This means that when you scale up tooa larger DWU, your queries automatically get more memory.</span></span> 
2. <span data-ttu-id="a5115-175">Classes de recursos estáticos (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) alocar Olá Olá a mesma quantidade de memória, independentemente do DWU atual (desde que Olá DWU em si tem memória suficiente).</span><span class="sxs-lookup"><span data-stu-id="a5115-175">Static Resource Classes (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) allocate hello same amount of memory regardless of hello current DWU (provided that hello DWU itself has enough memory).</span></span> <span data-ttu-id="a5115-176">Isso significa que em DWUs maiores, você pode executar mais consultas em cada classe de recursos simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="a5115-176">This means that on larger DWUs, you can run more queries in each resource class concurrently.</span></span>

<span data-ttu-id="a5115-177">Os usuários em **smallrc** e **staticrc10** recebem uma quantidade menor de memória e podem tirar proveito da simultaneidade superior.</span><span class="sxs-lookup"><span data-stu-id="a5115-177">Users in **smallrc** and **staticrc10** are given a smaller amount of memory and can take advantage of higher concurrency.</span></span> <span data-ttu-id="a5115-178">Em contraste, os usuários atribuídos muito**xlargerc** ou **staticrc80** recebem grandes quantidades de memória, e, portanto, menos suas consultas podem ser executados simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="a5115-178">In contrast, users assigned too**xlargerc** or **staticrc80** are given large amounts of memory, and therefore fewer of their queries can run concurrently.</span></span>

<span data-ttu-id="a5115-179">Por padrão, cada usuário é um membro da classe do recurso pequeno hello, **smallrc**.</span><span class="sxs-lookup"><span data-stu-id="a5115-179">By default, each user is a member of hello small resource class, **smallrc**.</span></span> <span data-ttu-id="a5115-180">Olá procedimento `sp_addrolemember` é usado a classe de recurso tooincrease hello e `sp_droprolemember` é usada a classe de recurso de saudação toodecrease.</span><span class="sxs-lookup"><span data-stu-id="a5115-180">hello procedure `sp_addrolemember` is used tooincrease hello resource class, and `sp_droprolemember` is used toodecrease hello resource class.</span></span> <span data-ttu-id="a5115-181">Por exemplo, este comando poderia aumentar a classe de recurso de saudação do loaduser muito**largerc**:</span><span class="sxs-lookup"><span data-stu-id="a5115-181">For example, this command would increase hello resource class of loaduser too**largerc**:</span></span>

```sql
EXEC sp_addrolemember 'largerc', 'loaduser'
```


### <a name="queries-that-do-not-honor-resource-classes"></a><span data-ttu-id="a5115-182">Consultas que não consideram classes de recursos</span><span class="sxs-lookup"><span data-stu-id="a5115-182">Queries that do not honor resource classes</span></span>

<span data-ttu-id="a5115-183">Existem alguns tipos de consultas que não se beneficiam de uma alocação de memória maior.</span><span class="sxs-lookup"><span data-stu-id="a5115-183">There are a few types of queries that do not benefit from a larger memory allocation.</span></span> <span data-ttu-id="a5115-184">sistema Olá ignora a alocação de classe de recurso e sempre executa essas consultas na classe de recursos pequeno Olá em vez disso.</span><span class="sxs-lookup"><span data-stu-id="a5115-184">hello system ignores their resource class allocation and always run these queries in hello small resource class instead.</span></span> <span data-ttu-id="a5115-185">Se essas consultas sempre em execução na classe de recursos pequeno hello, eles podem executar quando os slots de simultaneidade estão sob pressão e não consomem mais slots que o necessário.</span><span class="sxs-lookup"><span data-stu-id="a5115-185">If these queries always run in hello small resource class, they can run when concurrency slots are under pressure and they won't consume more slots than needed.</span></span> <span data-ttu-id="a5115-186">Consulte as [exceções de classe de recurso](#query-exceptions-to-concurrency-limits) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="a5115-186">See [Resource class exceptions](#query-exceptions-to-concurrency-limits) for more information.</span></span>

## <a name="details-on-resource-class-assignment"></a><span data-ttu-id="a5115-187">Detalhes sobre a atribuição de classe de recursos</span><span class="sxs-lookup"><span data-stu-id="a5115-187">Details on resource class assignment</span></span>


<span data-ttu-id="a5115-188">Mais alguns detalhes sobre classes de recurso:</span><span class="sxs-lookup"><span data-stu-id="a5115-188">A few more details on resource class:</span></span>

* <span data-ttu-id="a5115-189">*Alterar função* é necessária a permissão toochange classe de recurso de saudação de um usuário.</span><span class="sxs-lookup"><span data-stu-id="a5115-189">*Alter role* permission is required toochange hello resource class of a user.</span></span>
* <span data-ttu-id="a5115-190">Embora você pode adicionar um usuário tooone ou mais classes superiores de recurso Olá, classes de recursos dinâmicos têm precedência sobre classes de recursos estáticos.</span><span class="sxs-lookup"><span data-stu-id="a5115-190">Although you can add a user tooone or more of hello higher resource classes, dynamic resource classes take precedence over static resource classes.</span></span> <span data-ttu-id="a5115-191">Ou seja, se um usuário é atribuído tooboth **mediumrc**(dinâmico) e **staticrc80**(estático), **mediumrc** é a classe de recurso de saudação que é cumprido.</span><span class="sxs-lookup"><span data-stu-id="a5115-191">That is, if a user is assigned tooboth **mediumrc**(dynamic) and **staticrc80**(static), **mediumrc** is hello resource class that is honored.</span></span>
 * <span data-ttu-id="a5115-192">Quando um usuário é atribuído toomore que a classe de um recurso em um tipo de classe de recurso específico (mais de uma classe de recurso dinâmico ou mais de uma classe de recurso estático), a classe de recurso hello mais alto é cumprido.</span><span class="sxs-lookup"><span data-stu-id="a5115-192">When a user is assigned toomore than one resource class in a specific resource class type (more than one dynamic resource class or more than one static resource class), hello highest resource class is honored.</span></span> <span data-ttu-id="a5115-193">Ou seja, se um usuário é atribuído largerc e tooboth mediumrc, classe de recurso superior hello (largerc) é cumprido.</span><span class="sxs-lookup"><span data-stu-id="a5115-193">That is, if a user is assigned tooboth mediumrc and largerc, hello higher resource class (largerc) is honored.</span></span> <span data-ttu-id="a5115-194">E se um usuário é atribuído tooboth **staticrc20** e **statirc80**, **staticrc80** é respeitada.</span><span class="sxs-lookup"><span data-stu-id="a5115-194">And if a user is assigned tooboth **staticrc20** and **statirc80**, **staticrc80** is honored.</span></span>
* <span data-ttu-id="a5115-195">classe de recurso de saudação do usuário administrativo do sistema Olá não pode ser alterado.</span><span class="sxs-lookup"><span data-stu-id="a5115-195">hello resource class of hello system administrative user cannot be changed.</span></span>

<span data-ttu-id="a5115-196">Para obter um exemplo detalhado, consulte [Alterando o exemplo de classe de recurso de usuário](#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="a5115-196">For a detailed example, see [Changing user resource class example](#changing-user-resource-class-example).</span></span>

## <a name="memory-allocation"></a><span data-ttu-id="a5115-197">Alocação de memória</span><span class="sxs-lookup"><span data-stu-id="a5115-197">Memory allocation</span></span>
<span data-ttu-id="a5115-198">Há prós e contras tooincreasing classe de recurso do usuário.</span><span class="sxs-lookup"><span data-stu-id="a5115-198">There are pros and cons tooincreasing a user's resource class.</span></span> <span data-ttu-id="a5115-199">Aumentando a uma classe de recurso para um usuário, fornece suas consultas de memória toomore, que pode significar que executar consultas mais rapidamente.</span><span class="sxs-lookup"><span data-stu-id="a5115-199">Increasing a resource class for a user, gives their queries access toomore memory, which may mean queries execute faster.</span></span>  <span data-ttu-id="a5115-200">No entanto, o classes superiores de recurso também reduzem o número de saudação de consultas simultâneas que podem ser executados.</span><span class="sxs-lookup"><span data-stu-id="a5115-200">However, higher resource classes also reduce hello number of concurrent queries that can run.</span></span> <span data-ttu-id="a5115-201">Essa é a compensação de saudação entre a alocação de grandes quantidades de consulta única de tooa de memória ou permitindo que outras consultas, que também precisam de alocações de memória, toorun simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="a5115-201">This is hello trade-off between allocating large amounts of memory tooa single query or allowing other queries, which also need memory allocations, toorun concurrently.</span></span> <span data-ttu-id="a5115-202">Se um usuário receber alta alocações de memória para uma consulta, outros usuários não terão acesso toothat mesmo memória toorun uma consulta.</span><span class="sxs-lookup"><span data-stu-id="a5115-202">If one user is given high allocations of memory for a query, other users will not have access toothat same memory toorun a query.</span></span>

<span data-ttu-id="a5115-203">Olá, a tabela a seguir mapeia memória Olá alocada distribuição tooeach pela classe DWU e recursos.</span><span class="sxs-lookup"><span data-stu-id="a5115-203">hello following table maps hello memory allocated tooeach distribution by DWU and resource class.</span></span>

### <a name="memory-allocations-per-distribution-for-dynamic-resource-classes-mb"></a><span data-ttu-id="a5115-204">Alocações de memória por distribuição de classes de recursos dinâmicos (MB)</span><span class="sxs-lookup"><span data-stu-id="a5115-204">Memory allocations per distribution for dynamic resource classes (MB)</span></span>
| <span data-ttu-id="a5115-205">DWU</span><span class="sxs-lookup"><span data-stu-id="a5115-205">DWU</span></span> | <span data-ttu-id="a5115-206">smallrc</span><span class="sxs-lookup"><span data-stu-id="a5115-206">smallrc</span></span> | <span data-ttu-id="a5115-207">mediumrc</span><span class="sxs-lookup"><span data-stu-id="a5115-207">mediumrc</span></span> | <span data-ttu-id="a5115-208">largerc</span><span class="sxs-lookup"><span data-stu-id="a5115-208">largerc</span></span> | <span data-ttu-id="a5115-209">xlargerc</span><span class="sxs-lookup"><span data-stu-id="a5115-209">xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="a5115-210">DW100</span><span class="sxs-lookup"><span data-stu-id="a5115-210">DW100</span></span> |<span data-ttu-id="a5115-211">100</span><span class="sxs-lookup"><span data-stu-id="a5115-211">100</span></span> |<span data-ttu-id="a5115-212">100</span><span class="sxs-lookup"><span data-stu-id="a5115-212">100</span></span> |<span data-ttu-id="a5115-213">200</span><span class="sxs-lookup"><span data-stu-id="a5115-213">200</span></span> |<span data-ttu-id="a5115-214">400</span><span class="sxs-lookup"><span data-stu-id="a5115-214">400</span></span> |
| <span data-ttu-id="a5115-215">DW200</span><span class="sxs-lookup"><span data-stu-id="a5115-215">DW200</span></span> |<span data-ttu-id="a5115-216">100</span><span class="sxs-lookup"><span data-stu-id="a5115-216">100</span></span> |<span data-ttu-id="a5115-217">200</span><span class="sxs-lookup"><span data-stu-id="a5115-217">200</span></span> |<span data-ttu-id="a5115-218">400</span><span class="sxs-lookup"><span data-stu-id="a5115-218">400</span></span> |<span data-ttu-id="a5115-219">800</span><span class="sxs-lookup"><span data-stu-id="a5115-219">800</span></span> |
| <span data-ttu-id="a5115-220">DW300</span><span class="sxs-lookup"><span data-stu-id="a5115-220">DW300</span></span> |<span data-ttu-id="a5115-221">100</span><span class="sxs-lookup"><span data-stu-id="a5115-221">100</span></span> |<span data-ttu-id="a5115-222">200</span><span class="sxs-lookup"><span data-stu-id="a5115-222">200</span></span> |<span data-ttu-id="a5115-223">400</span><span class="sxs-lookup"><span data-stu-id="a5115-223">400</span></span> |<span data-ttu-id="a5115-224">800</span><span class="sxs-lookup"><span data-stu-id="a5115-224">800</span></span> |
| <span data-ttu-id="a5115-225">DW400</span><span class="sxs-lookup"><span data-stu-id="a5115-225">DW400</span></span> |<span data-ttu-id="a5115-226">100</span><span class="sxs-lookup"><span data-stu-id="a5115-226">100</span></span> |<span data-ttu-id="a5115-227">400</span><span class="sxs-lookup"><span data-stu-id="a5115-227">400</span></span> |<span data-ttu-id="a5115-228">800</span><span class="sxs-lookup"><span data-stu-id="a5115-228">800</span></span> |<span data-ttu-id="a5115-229">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-229">1,600</span></span> |
| <span data-ttu-id="a5115-230">DW500</span><span class="sxs-lookup"><span data-stu-id="a5115-230">DW500</span></span> |<span data-ttu-id="a5115-231">100</span><span class="sxs-lookup"><span data-stu-id="a5115-231">100</span></span> |<span data-ttu-id="a5115-232">400</span><span class="sxs-lookup"><span data-stu-id="a5115-232">400</span></span> |<span data-ttu-id="a5115-233">800</span><span class="sxs-lookup"><span data-stu-id="a5115-233">800</span></span> |<span data-ttu-id="a5115-234">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-234">1,600</span></span> |
| <span data-ttu-id="a5115-235">DW600</span><span class="sxs-lookup"><span data-stu-id="a5115-235">DW600</span></span> |<span data-ttu-id="a5115-236">100</span><span class="sxs-lookup"><span data-stu-id="a5115-236">100</span></span> |<span data-ttu-id="a5115-237">400</span><span class="sxs-lookup"><span data-stu-id="a5115-237">400</span></span> |<span data-ttu-id="a5115-238">800</span><span class="sxs-lookup"><span data-stu-id="a5115-238">800</span></span> |<span data-ttu-id="a5115-239">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-239">1,600</span></span> |
| <span data-ttu-id="a5115-240">DW1000</span><span class="sxs-lookup"><span data-stu-id="a5115-240">DW1000</span></span> |<span data-ttu-id="a5115-241">100</span><span class="sxs-lookup"><span data-stu-id="a5115-241">100</span></span> |<span data-ttu-id="a5115-242">800</span><span class="sxs-lookup"><span data-stu-id="a5115-242">800</span></span> |<span data-ttu-id="a5115-243">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-243">1,600</span></span> |<span data-ttu-id="a5115-244">3.200</span><span class="sxs-lookup"><span data-stu-id="a5115-244">3,200</span></span> |
| <span data-ttu-id="a5115-245">DW1200</span><span class="sxs-lookup"><span data-stu-id="a5115-245">DW1200</span></span> |<span data-ttu-id="a5115-246">100</span><span class="sxs-lookup"><span data-stu-id="a5115-246">100</span></span> |<span data-ttu-id="a5115-247">800</span><span class="sxs-lookup"><span data-stu-id="a5115-247">800</span></span> |<span data-ttu-id="a5115-248">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-248">1,600</span></span> |<span data-ttu-id="a5115-249">3.200</span><span class="sxs-lookup"><span data-stu-id="a5115-249">3,200</span></span> |
| <span data-ttu-id="a5115-250">DW1500</span><span class="sxs-lookup"><span data-stu-id="a5115-250">DW1500</span></span> |<span data-ttu-id="a5115-251">100</span><span class="sxs-lookup"><span data-stu-id="a5115-251">100</span></span> |<span data-ttu-id="a5115-252">800</span><span class="sxs-lookup"><span data-stu-id="a5115-252">800</span></span> |<span data-ttu-id="a5115-253">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-253">1,600</span></span> |<span data-ttu-id="a5115-254">3.200</span><span class="sxs-lookup"><span data-stu-id="a5115-254">3,200</span></span> |
| <span data-ttu-id="a5115-255">DW2000</span><span class="sxs-lookup"><span data-stu-id="a5115-255">DW2000</span></span> |<span data-ttu-id="a5115-256">100</span><span class="sxs-lookup"><span data-stu-id="a5115-256">100</span></span> |<span data-ttu-id="a5115-257">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-257">1,600</span></span> |<span data-ttu-id="a5115-258">3.200</span><span class="sxs-lookup"><span data-stu-id="a5115-258">3,200</span></span> |<span data-ttu-id="a5115-259">6.400</span><span class="sxs-lookup"><span data-stu-id="a5115-259">6,400</span></span> |
| <span data-ttu-id="a5115-260">DW3000</span><span class="sxs-lookup"><span data-stu-id="a5115-260">DW3000</span></span> |<span data-ttu-id="a5115-261">100</span><span class="sxs-lookup"><span data-stu-id="a5115-261">100</span></span> |<span data-ttu-id="a5115-262">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-262">1,600</span></span> |<span data-ttu-id="a5115-263">3.200</span><span class="sxs-lookup"><span data-stu-id="a5115-263">3,200</span></span> |<span data-ttu-id="a5115-264">6.400</span><span class="sxs-lookup"><span data-stu-id="a5115-264">6,400</span></span> |
| <span data-ttu-id="a5115-265">DW6000</span><span class="sxs-lookup"><span data-stu-id="a5115-265">DW6000</span></span> |<span data-ttu-id="a5115-266">100</span><span class="sxs-lookup"><span data-stu-id="a5115-266">100</span></span> |<span data-ttu-id="a5115-267">3.200</span><span class="sxs-lookup"><span data-stu-id="a5115-267">3,200</span></span> |<span data-ttu-id="a5115-268">6.400</span><span class="sxs-lookup"><span data-stu-id="a5115-268">6,400</span></span> |<span data-ttu-id="a5115-269">12.800</span><span class="sxs-lookup"><span data-stu-id="a5115-269">12,800</span></span> |

<span data-ttu-id="a5115-270">Olá, a tabela a seguir mapeia memória Olá alocada distribuição tooeach por DWU e classe de recurso estático.</span><span class="sxs-lookup"><span data-stu-id="a5115-270">hello following table maps hello memory allocated tooeach distribution by DWU and static resource class.</span></span> <span data-ttu-id="a5115-271">Observe que as classes superiores de recurso Olá tem sua memória reduzido limites DWU toohonor Olá global.</span><span class="sxs-lookup"><span data-stu-id="a5115-271">Note that hello higher resource classes have their memory reduced toohonor hello global DWU limits.</span></span>

### <a name="memory-allocations-per-distribution-for-static-resource-classes-mb"></a><span data-ttu-id="a5115-272">Alocações de memória por distribuição de classes de recursos estáticos (MB)</span><span class="sxs-lookup"><span data-stu-id="a5115-272">Memory allocations per distribution for static resource classes (MB)</span></span>
| <span data-ttu-id="a5115-273">DWU</span><span class="sxs-lookup"><span data-stu-id="a5115-273">DWU</span></span> | <span data-ttu-id="a5115-274">staticrc10</span><span class="sxs-lookup"><span data-stu-id="a5115-274">staticrc10</span></span> | <span data-ttu-id="a5115-275">staticrc20</span><span class="sxs-lookup"><span data-stu-id="a5115-275">staticrc20</span></span> | <span data-ttu-id="a5115-276">staticrc30</span><span class="sxs-lookup"><span data-stu-id="a5115-276">staticrc30</span></span> | <span data-ttu-id="a5115-277">staticrc40</span><span class="sxs-lookup"><span data-stu-id="a5115-277">staticrc40</span></span> | <span data-ttu-id="a5115-278">staticrc50</span><span class="sxs-lookup"><span data-stu-id="a5115-278">staticrc50</span></span> | <span data-ttu-id="a5115-279">staticrc60</span><span class="sxs-lookup"><span data-stu-id="a5115-279">staticrc60</span></span> | <span data-ttu-id="a5115-280">staticrc70</span><span class="sxs-lookup"><span data-stu-id="a5115-280">staticrc70</span></span> | <span data-ttu-id="a5115-281">staticrc80</span><span class="sxs-lookup"><span data-stu-id="a5115-281">staticrc80</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="a5115-282">DW100</span><span class="sxs-lookup"><span data-stu-id="a5115-282">DW100</span></span> |<span data-ttu-id="a5115-283">100</span><span class="sxs-lookup"><span data-stu-id="a5115-283">100</span></span> |<span data-ttu-id="a5115-284">200</span><span class="sxs-lookup"><span data-stu-id="a5115-284">200</span></span> |<span data-ttu-id="a5115-285">400</span><span class="sxs-lookup"><span data-stu-id="a5115-285">400</span></span> |<span data-ttu-id="a5115-286">400</span><span class="sxs-lookup"><span data-stu-id="a5115-286">400</span></span> |<span data-ttu-id="a5115-287">400</span><span class="sxs-lookup"><span data-stu-id="a5115-287">400</span></span> |<span data-ttu-id="a5115-288">400</span><span class="sxs-lookup"><span data-stu-id="a5115-288">400</span></span> |<span data-ttu-id="a5115-289">400</span><span class="sxs-lookup"><span data-stu-id="a5115-289">400</span></span> |<span data-ttu-id="a5115-290">400</span><span class="sxs-lookup"><span data-stu-id="a5115-290">400</span></span> |
| <span data-ttu-id="a5115-291">DW200</span><span class="sxs-lookup"><span data-stu-id="a5115-291">DW200</span></span> |<span data-ttu-id="a5115-292">100</span><span class="sxs-lookup"><span data-stu-id="a5115-292">100</span></span> |<span data-ttu-id="a5115-293">200</span><span class="sxs-lookup"><span data-stu-id="a5115-293">200</span></span> |<span data-ttu-id="a5115-294">400</span><span class="sxs-lookup"><span data-stu-id="a5115-294">400</span></span> |<span data-ttu-id="a5115-295">800</span><span class="sxs-lookup"><span data-stu-id="a5115-295">800</span></span> |<span data-ttu-id="a5115-296">800</span><span class="sxs-lookup"><span data-stu-id="a5115-296">800</span></span> |<span data-ttu-id="a5115-297">800</span><span class="sxs-lookup"><span data-stu-id="a5115-297">800</span></span> |<span data-ttu-id="a5115-298">800</span><span class="sxs-lookup"><span data-stu-id="a5115-298">800</span></span> |<span data-ttu-id="a5115-299">800</span><span class="sxs-lookup"><span data-stu-id="a5115-299">800</span></span> |
| <span data-ttu-id="a5115-300">DW300</span><span class="sxs-lookup"><span data-stu-id="a5115-300">DW300</span></span> |<span data-ttu-id="a5115-301">100</span><span class="sxs-lookup"><span data-stu-id="a5115-301">100</span></span> |<span data-ttu-id="a5115-302">200</span><span class="sxs-lookup"><span data-stu-id="a5115-302">200</span></span> |<span data-ttu-id="a5115-303">400</span><span class="sxs-lookup"><span data-stu-id="a5115-303">400</span></span> |<span data-ttu-id="a5115-304">800</span><span class="sxs-lookup"><span data-stu-id="a5115-304">800</span></span> |<span data-ttu-id="a5115-305">800</span><span class="sxs-lookup"><span data-stu-id="a5115-305">800</span></span> |<span data-ttu-id="a5115-306">800</span><span class="sxs-lookup"><span data-stu-id="a5115-306">800</span></span> |<span data-ttu-id="a5115-307">800</span><span class="sxs-lookup"><span data-stu-id="a5115-307">800</span></span> |<span data-ttu-id="a5115-308">800</span><span class="sxs-lookup"><span data-stu-id="a5115-308">800</span></span> |
| <span data-ttu-id="a5115-309">DW400</span><span class="sxs-lookup"><span data-stu-id="a5115-309">DW400</span></span> |<span data-ttu-id="a5115-310">100</span><span class="sxs-lookup"><span data-stu-id="a5115-310">100</span></span> |<span data-ttu-id="a5115-311">200</span><span class="sxs-lookup"><span data-stu-id="a5115-311">200</span></span> |<span data-ttu-id="a5115-312">400</span><span class="sxs-lookup"><span data-stu-id="a5115-312">400</span></span> |<span data-ttu-id="a5115-313">800</span><span class="sxs-lookup"><span data-stu-id="a5115-313">800</span></span> |<span data-ttu-id="a5115-314">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-314">1,600</span></span> |<span data-ttu-id="a5115-315">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-315">1,600</span></span> |<span data-ttu-id="a5115-316">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-316">1,600</span></span> |<span data-ttu-id="a5115-317">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-317">1,600</span></span> |
| <span data-ttu-id="a5115-318">DW500</span><span class="sxs-lookup"><span data-stu-id="a5115-318">DW500</span></span> |<span data-ttu-id="a5115-319">100</span><span class="sxs-lookup"><span data-stu-id="a5115-319">100</span></span> |<span data-ttu-id="a5115-320">200</span><span class="sxs-lookup"><span data-stu-id="a5115-320">200</span></span> |<span data-ttu-id="a5115-321">400</span><span class="sxs-lookup"><span data-stu-id="a5115-321">400</span></span> |<span data-ttu-id="a5115-322">800</span><span class="sxs-lookup"><span data-stu-id="a5115-322">800</span></span> |<span data-ttu-id="a5115-323">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-323">1,600</span></span> |<span data-ttu-id="a5115-324">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-324">1,600</span></span> |<span data-ttu-id="a5115-325">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-325">1,600</span></span> |<span data-ttu-id="a5115-326">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-326">1,600</span></span> |
| <span data-ttu-id="a5115-327">DW600</span><span class="sxs-lookup"><span data-stu-id="a5115-327">DW600</span></span> |<span data-ttu-id="a5115-328">100</span><span class="sxs-lookup"><span data-stu-id="a5115-328">100</span></span> |<span data-ttu-id="a5115-329">200</span><span class="sxs-lookup"><span data-stu-id="a5115-329">200</span></span> |<span data-ttu-id="a5115-330">400</span><span class="sxs-lookup"><span data-stu-id="a5115-330">400</span></span> |<span data-ttu-id="a5115-331">800</span><span class="sxs-lookup"><span data-stu-id="a5115-331">800</span></span> |<span data-ttu-id="a5115-332">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-332">1,600</span></span> |<span data-ttu-id="a5115-333">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-333">1,600</span></span> |<span data-ttu-id="a5115-334">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-334">1,600</span></span> |<span data-ttu-id="a5115-335">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-335">1,600</span></span> |
| <span data-ttu-id="a5115-336">DW1000</span><span class="sxs-lookup"><span data-stu-id="a5115-336">DW1000</span></span> |<span data-ttu-id="a5115-337">100</span><span class="sxs-lookup"><span data-stu-id="a5115-337">100</span></span> |<span data-ttu-id="a5115-338">200</span><span class="sxs-lookup"><span data-stu-id="a5115-338">200</span></span> |<span data-ttu-id="a5115-339">400</span><span class="sxs-lookup"><span data-stu-id="a5115-339">400</span></span> |<span data-ttu-id="a5115-340">800</span><span class="sxs-lookup"><span data-stu-id="a5115-340">800</span></span> |<span data-ttu-id="a5115-341">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-341">1,600</span></span> |<span data-ttu-id="a5115-342">3.200</span><span class="sxs-lookup"><span data-stu-id="a5115-342">3,200</span></span> |<span data-ttu-id="a5115-343">3.200</span><span class="sxs-lookup"><span data-stu-id="a5115-343">3,200</span></span> |<span data-ttu-id="a5115-344">3.200</span><span class="sxs-lookup"><span data-stu-id="a5115-344">3,200</span></span> |
| <span data-ttu-id="a5115-345">DW1200</span><span class="sxs-lookup"><span data-stu-id="a5115-345">DW1200</span></span> |<span data-ttu-id="a5115-346">100</span><span class="sxs-lookup"><span data-stu-id="a5115-346">100</span></span> |<span data-ttu-id="a5115-347">200</span><span class="sxs-lookup"><span data-stu-id="a5115-347">200</span></span> |<span data-ttu-id="a5115-348">400</span><span class="sxs-lookup"><span data-stu-id="a5115-348">400</span></span> |<span data-ttu-id="a5115-349">800</span><span class="sxs-lookup"><span data-stu-id="a5115-349">800</span></span> |<span data-ttu-id="a5115-350">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-350">1,600</span></span> |<span data-ttu-id="a5115-351">3.200</span><span class="sxs-lookup"><span data-stu-id="a5115-351">3,200</span></span> |<span data-ttu-id="a5115-352">3.200</span><span class="sxs-lookup"><span data-stu-id="a5115-352">3,200</span></span> |<span data-ttu-id="a5115-353">3.200</span><span class="sxs-lookup"><span data-stu-id="a5115-353">3,200</span></span> |
| <span data-ttu-id="a5115-354">DW1500</span><span class="sxs-lookup"><span data-stu-id="a5115-354">DW1500</span></span> |<span data-ttu-id="a5115-355">100</span><span class="sxs-lookup"><span data-stu-id="a5115-355">100</span></span> |<span data-ttu-id="a5115-356">200</span><span class="sxs-lookup"><span data-stu-id="a5115-356">200</span></span> |<span data-ttu-id="a5115-357">400</span><span class="sxs-lookup"><span data-stu-id="a5115-357">400</span></span> |<span data-ttu-id="a5115-358">800</span><span class="sxs-lookup"><span data-stu-id="a5115-358">800</span></span> |<span data-ttu-id="a5115-359">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-359">1,600</span></span> |<span data-ttu-id="a5115-360">3.200</span><span class="sxs-lookup"><span data-stu-id="a5115-360">3,200</span></span> |<span data-ttu-id="a5115-361">3.200</span><span class="sxs-lookup"><span data-stu-id="a5115-361">3,200</span></span> |<span data-ttu-id="a5115-362">3.200</span><span class="sxs-lookup"><span data-stu-id="a5115-362">3,200</span></span> |
| <span data-ttu-id="a5115-363">DW2000</span><span class="sxs-lookup"><span data-stu-id="a5115-363">DW2000</span></span> |<span data-ttu-id="a5115-364">100</span><span class="sxs-lookup"><span data-stu-id="a5115-364">100</span></span> |<span data-ttu-id="a5115-365">200</span><span class="sxs-lookup"><span data-stu-id="a5115-365">200</span></span> |<span data-ttu-id="a5115-366">400</span><span class="sxs-lookup"><span data-stu-id="a5115-366">400</span></span> |<span data-ttu-id="a5115-367">800</span><span class="sxs-lookup"><span data-stu-id="a5115-367">800</span></span> |<span data-ttu-id="a5115-368">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-368">1,600</span></span> |<span data-ttu-id="a5115-369">3.200</span><span class="sxs-lookup"><span data-stu-id="a5115-369">3,200</span></span> |<span data-ttu-id="a5115-370">6.400</span><span class="sxs-lookup"><span data-stu-id="a5115-370">6,400</span></span> |<span data-ttu-id="a5115-371">6.400</span><span class="sxs-lookup"><span data-stu-id="a5115-371">6,400</span></span> |
| <span data-ttu-id="a5115-372">DW3000</span><span class="sxs-lookup"><span data-stu-id="a5115-372">DW3000</span></span> |<span data-ttu-id="a5115-373">100</span><span class="sxs-lookup"><span data-stu-id="a5115-373">100</span></span> |<span data-ttu-id="a5115-374">200</span><span class="sxs-lookup"><span data-stu-id="a5115-374">200</span></span> |<span data-ttu-id="a5115-375">400</span><span class="sxs-lookup"><span data-stu-id="a5115-375">400</span></span> |<span data-ttu-id="a5115-376">800</span><span class="sxs-lookup"><span data-stu-id="a5115-376">800</span></span> |<span data-ttu-id="a5115-377">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-377">1,600</span></span> |<span data-ttu-id="a5115-378">3.200</span><span class="sxs-lookup"><span data-stu-id="a5115-378">3,200</span></span> |<span data-ttu-id="a5115-379">6.400</span><span class="sxs-lookup"><span data-stu-id="a5115-379">6,400</span></span> |<span data-ttu-id="a5115-380">6.400</span><span class="sxs-lookup"><span data-stu-id="a5115-380">6,400</span></span> |
| <span data-ttu-id="a5115-381">DW6000</span><span class="sxs-lookup"><span data-stu-id="a5115-381">DW6000</span></span> |<span data-ttu-id="a5115-382">100</span><span class="sxs-lookup"><span data-stu-id="a5115-382">100</span></span> |<span data-ttu-id="a5115-383">200</span><span class="sxs-lookup"><span data-stu-id="a5115-383">200</span></span> |<span data-ttu-id="a5115-384">400</span><span class="sxs-lookup"><span data-stu-id="a5115-384">400</span></span> |<span data-ttu-id="a5115-385">800</span><span class="sxs-lookup"><span data-stu-id="a5115-385">800</span></span> |<span data-ttu-id="a5115-386">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-386">1,600</span></span> |<span data-ttu-id="a5115-387">3.200</span><span class="sxs-lookup"><span data-stu-id="a5115-387">3,200</span></span> |<span data-ttu-id="a5115-388">6.400</span><span class="sxs-lookup"><span data-stu-id="a5115-388">6,400</span></span> |<span data-ttu-id="a5115-389">12.800</span><span class="sxs-lookup"><span data-stu-id="a5115-389">12,800</span></span> |

<span data-ttu-id="a5115-390">Olá anterior da tabela, você pode ver que uma consulta em execução em um DW2000 no hello **xlargerc** classe de recurso teria acesso too6, 400 MB de memória em cada banco de dados distribuído 60 de saudação.</span><span class="sxs-lookup"><span data-stu-id="a5115-390">From hello preceding table, you can see that a query running on a DW2000 in hello **xlargerc** resource class would have access too6,400 MB of memory within each of hello 60 distributed databases.</span></span>  <span data-ttu-id="a5115-391">Há 60 distribuições no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a5115-391">In SQL Data Warehouse, there are 60 distributions.</span></span> <span data-ttu-id="a5115-392">Portanto, alocação de memória total toocalculate Olá para uma consulta em uma classe de recurso fornecido, Olá acima valores deve ser multiplicada por 60.</span><span class="sxs-lookup"><span data-stu-id="a5115-392">Therefore, toocalculate hello total memory allocation for a query in a given resource class, hello above values should be multiplied by 60.</span></span>

### <a name="memory-allocations-system-wide-gb"></a><span data-ttu-id="a5115-393">Alocações de memória em todo o sistema (GB)</span><span class="sxs-lookup"><span data-stu-id="a5115-393">Memory allocations system-wide (GB)</span></span>
| <span data-ttu-id="a5115-394">DWU</span><span class="sxs-lookup"><span data-stu-id="a5115-394">DWU</span></span> | <span data-ttu-id="a5115-395">smallrc</span><span class="sxs-lookup"><span data-stu-id="a5115-395">smallrc</span></span> | <span data-ttu-id="a5115-396">mediumrc</span><span class="sxs-lookup"><span data-stu-id="a5115-396">mediumrc</span></span> | <span data-ttu-id="a5115-397">largerc</span><span class="sxs-lookup"><span data-stu-id="a5115-397">largerc</span></span> | <span data-ttu-id="a5115-398">xlargerc</span><span class="sxs-lookup"><span data-stu-id="a5115-398">xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="a5115-399">DW100</span><span class="sxs-lookup"><span data-stu-id="a5115-399">DW100</span></span> |<span data-ttu-id="a5115-400">6</span><span class="sxs-lookup"><span data-stu-id="a5115-400">6</span></span> |<span data-ttu-id="a5115-401">6</span><span class="sxs-lookup"><span data-stu-id="a5115-401">6</span></span> |<span data-ttu-id="a5115-402">12</span><span class="sxs-lookup"><span data-stu-id="a5115-402">12</span></span> |<span data-ttu-id="a5115-403">23</span><span class="sxs-lookup"><span data-stu-id="a5115-403">23</span></span> |
| <span data-ttu-id="a5115-404">DW200</span><span class="sxs-lookup"><span data-stu-id="a5115-404">DW200</span></span> |<span data-ttu-id="a5115-405">6</span><span class="sxs-lookup"><span data-stu-id="a5115-405">6</span></span> |<span data-ttu-id="a5115-406">12</span><span class="sxs-lookup"><span data-stu-id="a5115-406">12</span></span> |<span data-ttu-id="a5115-407">23</span><span class="sxs-lookup"><span data-stu-id="a5115-407">23</span></span> |<span data-ttu-id="a5115-408">47</span><span class="sxs-lookup"><span data-stu-id="a5115-408">47</span></span> |
| <span data-ttu-id="a5115-409">DW300</span><span class="sxs-lookup"><span data-stu-id="a5115-409">DW300</span></span> |<span data-ttu-id="a5115-410">6</span><span class="sxs-lookup"><span data-stu-id="a5115-410">6</span></span> |<span data-ttu-id="a5115-411">12</span><span class="sxs-lookup"><span data-stu-id="a5115-411">12</span></span> |<span data-ttu-id="a5115-412">23</span><span class="sxs-lookup"><span data-stu-id="a5115-412">23</span></span> |<span data-ttu-id="a5115-413">47</span><span class="sxs-lookup"><span data-stu-id="a5115-413">47</span></span> |
| <span data-ttu-id="a5115-414">DW400</span><span class="sxs-lookup"><span data-stu-id="a5115-414">DW400</span></span> |<span data-ttu-id="a5115-415">6</span><span class="sxs-lookup"><span data-stu-id="a5115-415">6</span></span> |<span data-ttu-id="a5115-416">23</span><span class="sxs-lookup"><span data-stu-id="a5115-416">23</span></span> |<span data-ttu-id="a5115-417">47</span><span class="sxs-lookup"><span data-stu-id="a5115-417">47</span></span> |<span data-ttu-id="a5115-418">94</span><span class="sxs-lookup"><span data-stu-id="a5115-418">94</span></span> |
| <span data-ttu-id="a5115-419">DW500</span><span class="sxs-lookup"><span data-stu-id="a5115-419">DW500</span></span> |<span data-ttu-id="a5115-420">6</span><span class="sxs-lookup"><span data-stu-id="a5115-420">6</span></span> |<span data-ttu-id="a5115-421">23</span><span class="sxs-lookup"><span data-stu-id="a5115-421">23</span></span> |<span data-ttu-id="a5115-422">47</span><span class="sxs-lookup"><span data-stu-id="a5115-422">47</span></span> |<span data-ttu-id="a5115-423">94</span><span class="sxs-lookup"><span data-stu-id="a5115-423">94</span></span> |
| <span data-ttu-id="a5115-424">DW600</span><span class="sxs-lookup"><span data-stu-id="a5115-424">DW600</span></span> |<span data-ttu-id="a5115-425">6</span><span class="sxs-lookup"><span data-stu-id="a5115-425">6</span></span> |<span data-ttu-id="a5115-426">23</span><span class="sxs-lookup"><span data-stu-id="a5115-426">23</span></span> |<span data-ttu-id="a5115-427">47</span><span class="sxs-lookup"><span data-stu-id="a5115-427">47</span></span> |<span data-ttu-id="a5115-428">94</span><span class="sxs-lookup"><span data-stu-id="a5115-428">94</span></span> |
| <span data-ttu-id="a5115-429">DW1000</span><span class="sxs-lookup"><span data-stu-id="a5115-429">DW1000</span></span> |<span data-ttu-id="a5115-430">6</span><span class="sxs-lookup"><span data-stu-id="a5115-430">6</span></span> |<span data-ttu-id="a5115-431">47</span><span class="sxs-lookup"><span data-stu-id="a5115-431">47</span></span> |<span data-ttu-id="a5115-432">94</span><span class="sxs-lookup"><span data-stu-id="a5115-432">94</span></span> |<span data-ttu-id="a5115-433">188</span><span class="sxs-lookup"><span data-stu-id="a5115-433">188</span></span> |
| <span data-ttu-id="a5115-434">DW1200</span><span class="sxs-lookup"><span data-stu-id="a5115-434">DW1200</span></span> |<span data-ttu-id="a5115-435">6</span><span class="sxs-lookup"><span data-stu-id="a5115-435">6</span></span> |<span data-ttu-id="a5115-436">47</span><span class="sxs-lookup"><span data-stu-id="a5115-436">47</span></span> |<span data-ttu-id="a5115-437">94</span><span class="sxs-lookup"><span data-stu-id="a5115-437">94</span></span> |<span data-ttu-id="a5115-438">188</span><span class="sxs-lookup"><span data-stu-id="a5115-438">188</span></span> |
| <span data-ttu-id="a5115-439">DW1500</span><span class="sxs-lookup"><span data-stu-id="a5115-439">DW1500</span></span> |<span data-ttu-id="a5115-440">6</span><span class="sxs-lookup"><span data-stu-id="a5115-440">6</span></span> |<span data-ttu-id="a5115-441">47</span><span class="sxs-lookup"><span data-stu-id="a5115-441">47</span></span> |<span data-ttu-id="a5115-442">94</span><span class="sxs-lookup"><span data-stu-id="a5115-442">94</span></span> |<span data-ttu-id="a5115-443">188</span><span class="sxs-lookup"><span data-stu-id="a5115-443">188</span></span> |
| <span data-ttu-id="a5115-444">DW2000</span><span class="sxs-lookup"><span data-stu-id="a5115-444">DW2000</span></span> |<span data-ttu-id="a5115-445">6</span><span class="sxs-lookup"><span data-stu-id="a5115-445">6</span></span> |<span data-ttu-id="a5115-446">94</span><span class="sxs-lookup"><span data-stu-id="a5115-446">94</span></span> |<span data-ttu-id="a5115-447">188</span><span class="sxs-lookup"><span data-stu-id="a5115-447">188</span></span> |<span data-ttu-id="a5115-448">375</span><span class="sxs-lookup"><span data-stu-id="a5115-448">375</span></span> |
| <span data-ttu-id="a5115-449">DW3000</span><span class="sxs-lookup"><span data-stu-id="a5115-449">DW3000</span></span> |<span data-ttu-id="a5115-450">6</span><span class="sxs-lookup"><span data-stu-id="a5115-450">6</span></span> |<span data-ttu-id="a5115-451">94</span><span class="sxs-lookup"><span data-stu-id="a5115-451">94</span></span> |<span data-ttu-id="a5115-452">188</span><span class="sxs-lookup"><span data-stu-id="a5115-452">188</span></span> |<span data-ttu-id="a5115-453">375</span><span class="sxs-lookup"><span data-stu-id="a5115-453">375</span></span> |
| <span data-ttu-id="a5115-454">DW6000</span><span class="sxs-lookup"><span data-stu-id="a5115-454">DW6000</span></span> |<span data-ttu-id="a5115-455">6</span><span class="sxs-lookup"><span data-stu-id="a5115-455">6</span></span> |<span data-ttu-id="a5115-456">188</span><span class="sxs-lookup"><span data-stu-id="a5115-456">188</span></span> |<span data-ttu-id="a5115-457">375</span><span class="sxs-lookup"><span data-stu-id="a5115-457">375</span></span> |<span data-ttu-id="a5115-458">750</span><span class="sxs-lookup"><span data-stu-id="a5115-458">750</span></span> |

<span data-ttu-id="a5115-459">Essa tabela de alocações de memória do sistema, você pode ver que uma consulta em execução em um DW2000 na classe de recurso de xlargerc Olá é alocada um total de 375 GB de memória (distribuições 6.400 MB * 60 / 1.024 tooconvert tooGB) sobre a totalidade saudação do Data Warehouse do SQL.</span><span class="sxs-lookup"><span data-stu-id="a5115-459">From this table of system-wide memory allocations, you can see that a query running on a DW2000 in hello xlargerc resource class is allocated a total of 375 GB of memory (6,400 MB * 60 distributions / 1,024 tooconvert tooGB) over hello entirety of your SQL Data Warehouse.</span></span>

<span data-ttu-id="a5115-460">Olá mesmo cálculo se aplica toostatic classes de recursos.</span><span class="sxs-lookup"><span data-stu-id="a5115-460">hello same calculation applies toostatic resource classes.</span></span>
 
## <a name="concurrency-slot-consumption"></a><span data-ttu-id="a5115-461">Consumo de slot de simultaneidade</span><span class="sxs-lookup"><span data-stu-id="a5115-461">Concurrency slot consumption</span></span>  
<span data-ttu-id="a5115-462">SQL Data Warehouse concede mais tooqueries de memória em execução em classes superiores de recurso.</span><span class="sxs-lookup"><span data-stu-id="a5115-462">SQL Data Warehouse grants more memory tooqueries running in higher resource classes.</span></span> <span data-ttu-id="a5115-463">A memória é um recurso fixo.</span><span class="sxs-lookup"><span data-stu-id="a5115-463">Memory is a fixed resource.</span></span>  <span data-ttu-id="a5115-464">Portanto, hello mais memória alocada por consulta, Olá menos consultas simultâneas podem executar.</span><span class="sxs-lookup"><span data-stu-id="a5115-464">Therefore, hello more memory allocated per query, hello fewer concurrent queries can execute.</span></span> <span data-ttu-id="a5115-465">Olá tabela a seguir reitera todos os conceitos de saudação anterior em uma única exibição que mostra o número de saudação de slots de simultaneidade disponíveis por DWU e slots de saudação consumidos por cada classe de recurso.</span><span class="sxs-lookup"><span data-stu-id="a5115-465">hello following table reiterates all of hello previous concepts in a single view that shows hello number of concurrency slots available by DWU and hello slots consumed by each resource class.</span></span>  

### <a name="allocation-and-consumption-of-concurrency-slots-for-dynamic-resource-classes"></a><span data-ttu-id="a5115-466">Alocação e consumo de slots de simultaneidade para classes de recursos dinâmicos</span><span class="sxs-lookup"><span data-stu-id="a5115-466">Allocation and consumption of concurrency slots for dynamic resource classes</span></span>  
| <span data-ttu-id="a5115-467">DWU</span><span class="sxs-lookup"><span data-stu-id="a5115-467">DWU</span></span> | <span data-ttu-id="a5115-468">Máximo de consultas simultâneas</span><span class="sxs-lookup"><span data-stu-id="a5115-468">Maximum concurrent queries</span></span> | <span data-ttu-id="a5115-469">Slots de simultaneidade alocados</span><span class="sxs-lookup"><span data-stu-id="a5115-469">Concurrency slots allocated</span></span> | <span data-ttu-id="a5115-470">Slots usados pelo smallrc</span><span class="sxs-lookup"><span data-stu-id="a5115-470">Slots used by smallrc</span></span> | <span data-ttu-id="a5115-471">Slots usados pelo mediumrc</span><span class="sxs-lookup"><span data-stu-id="a5115-471">Slots used by mediumrc</span></span> | <span data-ttu-id="a5115-472">Slots usados pelo largerc</span><span class="sxs-lookup"><span data-stu-id="a5115-472">Slots used by largerc</span></span> | <span data-ttu-id="a5115-473">Slots usados pelo xlargerc</span><span class="sxs-lookup"><span data-stu-id="a5115-473">Slots used by xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="a5115-474">DW100</span><span class="sxs-lookup"><span data-stu-id="a5115-474">DW100</span></span> |<span data-ttu-id="a5115-475">4</span><span class="sxs-lookup"><span data-stu-id="a5115-475">4</span></span> |<span data-ttu-id="a5115-476">4</span><span class="sxs-lookup"><span data-stu-id="a5115-476">4</span></span> |<span data-ttu-id="a5115-477">1</span><span class="sxs-lookup"><span data-stu-id="a5115-477">1</span></span> |<span data-ttu-id="a5115-478">1</span><span class="sxs-lookup"><span data-stu-id="a5115-478">1</span></span> |<span data-ttu-id="a5115-479">2</span><span class="sxs-lookup"><span data-stu-id="a5115-479">2</span></span> |<span data-ttu-id="a5115-480">4</span><span class="sxs-lookup"><span data-stu-id="a5115-480">4</span></span> |
| <span data-ttu-id="a5115-481">DW200</span><span class="sxs-lookup"><span data-stu-id="a5115-481">DW200</span></span> |<span data-ttu-id="a5115-482">8</span><span class="sxs-lookup"><span data-stu-id="a5115-482">8</span></span> |<span data-ttu-id="a5115-483">8</span><span class="sxs-lookup"><span data-stu-id="a5115-483">8</span></span> |<span data-ttu-id="a5115-484">1</span><span class="sxs-lookup"><span data-stu-id="a5115-484">1</span></span> |<span data-ttu-id="a5115-485">2</span><span class="sxs-lookup"><span data-stu-id="a5115-485">2</span></span> |<span data-ttu-id="a5115-486">4</span><span class="sxs-lookup"><span data-stu-id="a5115-486">4</span></span> |<span data-ttu-id="a5115-487">8</span><span class="sxs-lookup"><span data-stu-id="a5115-487">8</span></span> |
| <span data-ttu-id="a5115-488">DW300</span><span class="sxs-lookup"><span data-stu-id="a5115-488">DW300</span></span> |<span data-ttu-id="a5115-489">12</span><span class="sxs-lookup"><span data-stu-id="a5115-489">12</span></span> |<span data-ttu-id="a5115-490">12</span><span class="sxs-lookup"><span data-stu-id="a5115-490">12</span></span> |<span data-ttu-id="a5115-491">1</span><span class="sxs-lookup"><span data-stu-id="a5115-491">1</span></span> |<span data-ttu-id="a5115-492">2</span><span class="sxs-lookup"><span data-stu-id="a5115-492">2</span></span> |<span data-ttu-id="a5115-493">4</span><span class="sxs-lookup"><span data-stu-id="a5115-493">4</span></span> |<span data-ttu-id="a5115-494">8</span><span class="sxs-lookup"><span data-stu-id="a5115-494">8</span></span> |
| <span data-ttu-id="a5115-495">DW400</span><span class="sxs-lookup"><span data-stu-id="a5115-495">DW400</span></span> |<span data-ttu-id="a5115-496">16</span><span class="sxs-lookup"><span data-stu-id="a5115-496">16</span></span> |<span data-ttu-id="a5115-497">16</span><span class="sxs-lookup"><span data-stu-id="a5115-497">16</span></span> |<span data-ttu-id="a5115-498">1</span><span class="sxs-lookup"><span data-stu-id="a5115-498">1</span></span> |<span data-ttu-id="a5115-499">4</span><span class="sxs-lookup"><span data-stu-id="a5115-499">4</span></span> |<span data-ttu-id="a5115-500">8</span><span class="sxs-lookup"><span data-stu-id="a5115-500">8</span></span> |<span data-ttu-id="a5115-501">16</span><span class="sxs-lookup"><span data-stu-id="a5115-501">16</span></span> |
| <span data-ttu-id="a5115-502">DW500</span><span class="sxs-lookup"><span data-stu-id="a5115-502">DW500</span></span> |<span data-ttu-id="a5115-503">20</span><span class="sxs-lookup"><span data-stu-id="a5115-503">20</span></span> |<span data-ttu-id="a5115-504">20</span><span class="sxs-lookup"><span data-stu-id="a5115-504">20</span></span> |<span data-ttu-id="a5115-505">1</span><span class="sxs-lookup"><span data-stu-id="a5115-505">1</span></span> |<span data-ttu-id="a5115-506">4</span><span class="sxs-lookup"><span data-stu-id="a5115-506">4</span></span> |<span data-ttu-id="a5115-507">8</span><span class="sxs-lookup"><span data-stu-id="a5115-507">8</span></span> |<span data-ttu-id="a5115-508">16</span><span class="sxs-lookup"><span data-stu-id="a5115-508">16</span></span> |
| <span data-ttu-id="a5115-509">DW600</span><span class="sxs-lookup"><span data-stu-id="a5115-509">DW600</span></span> |<span data-ttu-id="a5115-510">24</span><span class="sxs-lookup"><span data-stu-id="a5115-510">24</span></span> |<span data-ttu-id="a5115-511">24</span><span class="sxs-lookup"><span data-stu-id="a5115-511">24</span></span> |<span data-ttu-id="a5115-512">1</span><span class="sxs-lookup"><span data-stu-id="a5115-512">1</span></span> |<span data-ttu-id="a5115-513">4</span><span class="sxs-lookup"><span data-stu-id="a5115-513">4</span></span> |<span data-ttu-id="a5115-514">8</span><span class="sxs-lookup"><span data-stu-id="a5115-514">8</span></span> |<span data-ttu-id="a5115-515">16</span><span class="sxs-lookup"><span data-stu-id="a5115-515">16</span></span> |
| <span data-ttu-id="a5115-516">DW1000</span><span class="sxs-lookup"><span data-stu-id="a5115-516">DW1000</span></span> |<span data-ttu-id="a5115-517">32</span><span class="sxs-lookup"><span data-stu-id="a5115-517">32</span></span> |<span data-ttu-id="a5115-518">40</span><span class="sxs-lookup"><span data-stu-id="a5115-518">40</span></span> |<span data-ttu-id="a5115-519">1</span><span class="sxs-lookup"><span data-stu-id="a5115-519">1</span></span> |<span data-ttu-id="a5115-520">8</span><span class="sxs-lookup"><span data-stu-id="a5115-520">8</span></span> |<span data-ttu-id="a5115-521">16</span><span class="sxs-lookup"><span data-stu-id="a5115-521">16</span></span> |<span data-ttu-id="a5115-522">32</span><span class="sxs-lookup"><span data-stu-id="a5115-522">32</span></span> |
| <span data-ttu-id="a5115-523">DW1200</span><span class="sxs-lookup"><span data-stu-id="a5115-523">DW1200</span></span> |<span data-ttu-id="a5115-524">32</span><span class="sxs-lookup"><span data-stu-id="a5115-524">32</span></span> |<span data-ttu-id="a5115-525">48</span><span class="sxs-lookup"><span data-stu-id="a5115-525">48</span></span> |<span data-ttu-id="a5115-526">1</span><span class="sxs-lookup"><span data-stu-id="a5115-526">1</span></span> |<span data-ttu-id="a5115-527">8</span><span class="sxs-lookup"><span data-stu-id="a5115-527">8</span></span> |<span data-ttu-id="a5115-528">16</span><span class="sxs-lookup"><span data-stu-id="a5115-528">16</span></span> |<span data-ttu-id="a5115-529">32</span><span class="sxs-lookup"><span data-stu-id="a5115-529">32</span></span> |
| <span data-ttu-id="a5115-530">DW1500</span><span class="sxs-lookup"><span data-stu-id="a5115-530">DW1500</span></span> |<span data-ttu-id="a5115-531">32</span><span class="sxs-lookup"><span data-stu-id="a5115-531">32</span></span> |<span data-ttu-id="a5115-532">60</span><span class="sxs-lookup"><span data-stu-id="a5115-532">60</span></span> |<span data-ttu-id="a5115-533">1</span><span class="sxs-lookup"><span data-stu-id="a5115-533">1</span></span> |<span data-ttu-id="a5115-534">8</span><span class="sxs-lookup"><span data-stu-id="a5115-534">8</span></span> |<span data-ttu-id="a5115-535">16</span><span class="sxs-lookup"><span data-stu-id="a5115-535">16</span></span> |<span data-ttu-id="a5115-536">32</span><span class="sxs-lookup"><span data-stu-id="a5115-536">32</span></span> |
| <span data-ttu-id="a5115-537">DW2000</span><span class="sxs-lookup"><span data-stu-id="a5115-537">DW2000</span></span> |<span data-ttu-id="a5115-538">32</span><span class="sxs-lookup"><span data-stu-id="a5115-538">32</span></span> |<span data-ttu-id="a5115-539">80</span><span class="sxs-lookup"><span data-stu-id="a5115-539">80</span></span> |<span data-ttu-id="a5115-540">1</span><span class="sxs-lookup"><span data-stu-id="a5115-540">1</span></span> |<span data-ttu-id="a5115-541">16</span><span class="sxs-lookup"><span data-stu-id="a5115-541">16</span></span> |<span data-ttu-id="a5115-542">32</span><span class="sxs-lookup"><span data-stu-id="a5115-542">32</span></span> |<span data-ttu-id="a5115-543">64</span><span class="sxs-lookup"><span data-stu-id="a5115-543">64</span></span> |
| <span data-ttu-id="a5115-544">DW3000</span><span class="sxs-lookup"><span data-stu-id="a5115-544">DW3000</span></span> |<span data-ttu-id="a5115-545">32</span><span class="sxs-lookup"><span data-stu-id="a5115-545">32</span></span> |<span data-ttu-id="a5115-546">120</span><span class="sxs-lookup"><span data-stu-id="a5115-546">120</span></span> |<span data-ttu-id="a5115-547">1</span><span class="sxs-lookup"><span data-stu-id="a5115-547">1</span></span> |<span data-ttu-id="a5115-548">16</span><span class="sxs-lookup"><span data-stu-id="a5115-548">16</span></span> |<span data-ttu-id="a5115-549">32</span><span class="sxs-lookup"><span data-stu-id="a5115-549">32</span></span> |<span data-ttu-id="a5115-550">64</span><span class="sxs-lookup"><span data-stu-id="a5115-550">64</span></span> |
| <span data-ttu-id="a5115-551">DW6000</span><span class="sxs-lookup"><span data-stu-id="a5115-551">DW6000</span></span> |<span data-ttu-id="a5115-552">32</span><span class="sxs-lookup"><span data-stu-id="a5115-552">32</span></span> |<span data-ttu-id="a5115-553">240</span><span class="sxs-lookup"><span data-stu-id="a5115-553">240</span></span> |<span data-ttu-id="a5115-554">1</span><span class="sxs-lookup"><span data-stu-id="a5115-554">1</span></span> |<span data-ttu-id="a5115-555">32</span><span class="sxs-lookup"><span data-stu-id="a5115-555">32</span></span> |<span data-ttu-id="a5115-556">64</span><span class="sxs-lookup"><span data-stu-id="a5115-556">64</span></span> |<span data-ttu-id="a5115-557">128</span><span class="sxs-lookup"><span data-stu-id="a5115-557">128</span></span> |

### <a name="allocation-and-consumption-of-concurrency-slots-for-static-resource-classes"></a><span data-ttu-id="a5115-558">Alocação e consumo de slots de simultaneidade para classes de recursos estáticos</span><span class="sxs-lookup"><span data-stu-id="a5115-558">Allocation and consumption of concurrency slots for static resource classes</span></span>  
| <span data-ttu-id="a5115-559">DWU</span><span class="sxs-lookup"><span data-stu-id="a5115-559">DWU</span></span> | <span data-ttu-id="a5115-560">Máximo de consultas simultâneas</span><span class="sxs-lookup"><span data-stu-id="a5115-560">Maximum concurrent queries</span></span> | <span data-ttu-id="a5115-561">Slots de simultaneidade alocados</span><span class="sxs-lookup"><span data-stu-id="a5115-561">Concurrency slots allocated</span></span> |<span data-ttu-id="a5115-562">staticrc10</span><span class="sxs-lookup"><span data-stu-id="a5115-562">staticrc10</span></span> | <span data-ttu-id="a5115-563">staticrc20</span><span class="sxs-lookup"><span data-stu-id="a5115-563">staticrc20</span></span> | <span data-ttu-id="a5115-564">staticrc30</span><span class="sxs-lookup"><span data-stu-id="a5115-564">staticrc30</span></span> | <span data-ttu-id="a5115-565">staticrc40</span><span class="sxs-lookup"><span data-stu-id="a5115-565">staticrc40</span></span> | <span data-ttu-id="a5115-566">staticrc50</span><span class="sxs-lookup"><span data-stu-id="a5115-566">staticrc50</span></span> | <span data-ttu-id="a5115-567">staticrc60</span><span class="sxs-lookup"><span data-stu-id="a5115-567">staticrc60</span></span> | <span data-ttu-id="a5115-568">staticrc70</span><span class="sxs-lookup"><span data-stu-id="a5115-568">staticrc70</span></span> | <span data-ttu-id="a5115-569">staticrc80</span><span class="sxs-lookup"><span data-stu-id="a5115-569">staticrc80</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="a5115-570">DW100</span><span class="sxs-lookup"><span data-stu-id="a5115-570">DW100</span></span> |<span data-ttu-id="a5115-571">4</span><span class="sxs-lookup"><span data-stu-id="a5115-571">4</span></span> |<span data-ttu-id="a5115-572">4</span><span class="sxs-lookup"><span data-stu-id="a5115-572">4</span></span> |<span data-ttu-id="a5115-573">1</span><span class="sxs-lookup"><span data-stu-id="a5115-573">1</span></span> |<span data-ttu-id="a5115-574">2</span><span class="sxs-lookup"><span data-stu-id="a5115-574">2</span></span> |<span data-ttu-id="a5115-575">4</span><span class="sxs-lookup"><span data-stu-id="a5115-575">4</span></span> |<span data-ttu-id="a5115-576">4</span><span class="sxs-lookup"><span data-stu-id="a5115-576">4</span></span> |<span data-ttu-id="a5115-577">4</span><span class="sxs-lookup"><span data-stu-id="a5115-577">4</span></span> |<span data-ttu-id="a5115-578">4</span><span class="sxs-lookup"><span data-stu-id="a5115-578">4</span></span> |<span data-ttu-id="a5115-579">4</span><span class="sxs-lookup"><span data-stu-id="a5115-579">4</span></span> |<span data-ttu-id="a5115-580">4</span><span class="sxs-lookup"><span data-stu-id="a5115-580">4</span></span> |
| <span data-ttu-id="a5115-581">DW200</span><span class="sxs-lookup"><span data-stu-id="a5115-581">DW200</span></span> |<span data-ttu-id="a5115-582">8</span><span class="sxs-lookup"><span data-stu-id="a5115-582">8</span></span> |<span data-ttu-id="a5115-583">8</span><span class="sxs-lookup"><span data-stu-id="a5115-583">8</span></span> |<span data-ttu-id="a5115-584">1</span><span class="sxs-lookup"><span data-stu-id="a5115-584">1</span></span> |<span data-ttu-id="a5115-585">2</span><span class="sxs-lookup"><span data-stu-id="a5115-585">2</span></span> |<span data-ttu-id="a5115-586">4</span><span class="sxs-lookup"><span data-stu-id="a5115-586">4</span></span> |<span data-ttu-id="a5115-587">8</span><span class="sxs-lookup"><span data-stu-id="a5115-587">8</span></span> |<span data-ttu-id="a5115-588">8</span><span class="sxs-lookup"><span data-stu-id="a5115-588">8</span></span> |<span data-ttu-id="a5115-589">8</span><span class="sxs-lookup"><span data-stu-id="a5115-589">8</span></span> |<span data-ttu-id="a5115-590">8</span><span class="sxs-lookup"><span data-stu-id="a5115-590">8</span></span> |<span data-ttu-id="a5115-591">8</span><span class="sxs-lookup"><span data-stu-id="a5115-591">8</span></span> |
| <span data-ttu-id="a5115-592">DW300</span><span class="sxs-lookup"><span data-stu-id="a5115-592">DW300</span></span> |<span data-ttu-id="a5115-593">12</span><span class="sxs-lookup"><span data-stu-id="a5115-593">12</span></span> |<span data-ttu-id="a5115-594">12</span><span class="sxs-lookup"><span data-stu-id="a5115-594">12</span></span> |<span data-ttu-id="a5115-595">1</span><span class="sxs-lookup"><span data-stu-id="a5115-595">1</span></span> |<span data-ttu-id="a5115-596">2</span><span class="sxs-lookup"><span data-stu-id="a5115-596">2</span></span> |<span data-ttu-id="a5115-597">4</span><span class="sxs-lookup"><span data-stu-id="a5115-597">4</span></span> |<span data-ttu-id="a5115-598">8</span><span class="sxs-lookup"><span data-stu-id="a5115-598">8</span></span> |<span data-ttu-id="a5115-599">8</span><span class="sxs-lookup"><span data-stu-id="a5115-599">8</span></span> |<span data-ttu-id="a5115-600">8</span><span class="sxs-lookup"><span data-stu-id="a5115-600">8</span></span> |<span data-ttu-id="a5115-601">8</span><span class="sxs-lookup"><span data-stu-id="a5115-601">8</span></span> |<span data-ttu-id="a5115-602">8</span><span class="sxs-lookup"><span data-stu-id="a5115-602">8</span></span> |
| <span data-ttu-id="a5115-603">DW400</span><span class="sxs-lookup"><span data-stu-id="a5115-603">DW400</span></span> |<span data-ttu-id="a5115-604">16</span><span class="sxs-lookup"><span data-stu-id="a5115-604">16</span></span> |<span data-ttu-id="a5115-605">16</span><span class="sxs-lookup"><span data-stu-id="a5115-605">16</span></span> |<span data-ttu-id="a5115-606">1</span><span class="sxs-lookup"><span data-stu-id="a5115-606">1</span></span> |<span data-ttu-id="a5115-607">2</span><span class="sxs-lookup"><span data-stu-id="a5115-607">2</span></span> |<span data-ttu-id="a5115-608">4</span><span class="sxs-lookup"><span data-stu-id="a5115-608">4</span></span> |<span data-ttu-id="a5115-609">8</span><span class="sxs-lookup"><span data-stu-id="a5115-609">8</span></span> |<span data-ttu-id="a5115-610">16</span><span class="sxs-lookup"><span data-stu-id="a5115-610">16</span></span> |<span data-ttu-id="a5115-611">16</span><span class="sxs-lookup"><span data-stu-id="a5115-611">16</span></span> |<span data-ttu-id="a5115-612">16</span><span class="sxs-lookup"><span data-stu-id="a5115-612">16</span></span> |<span data-ttu-id="a5115-613">16</span><span class="sxs-lookup"><span data-stu-id="a5115-613">16</span></span> |
| <span data-ttu-id="a5115-614">DW500</span><span class="sxs-lookup"><span data-stu-id="a5115-614">DW500</span></span> | <span data-ttu-id="a5115-615">20</span><span class="sxs-lookup"><span data-stu-id="a5115-615">20</span></span>| <span data-ttu-id="a5115-616">20</span><span class="sxs-lookup"><span data-stu-id="a5115-616">20</span></span>| <span data-ttu-id="a5115-617">1</span><span class="sxs-lookup"><span data-stu-id="a5115-617">1</span></span>| <span data-ttu-id="a5115-618">2</span><span class="sxs-lookup"><span data-stu-id="a5115-618">2</span></span>| <span data-ttu-id="a5115-619">4</span><span class="sxs-lookup"><span data-stu-id="a5115-619">4</span></span>| <span data-ttu-id="a5115-620">8</span><span class="sxs-lookup"><span data-stu-id="a5115-620">8</span></span>| <span data-ttu-id="a5115-621">16</span><span class="sxs-lookup"><span data-stu-id="a5115-621">16</span></span>| <span data-ttu-id="a5115-622">16</span><span class="sxs-lookup"><span data-stu-id="a5115-622">16</span></span>| <span data-ttu-id="a5115-623">16</span><span class="sxs-lookup"><span data-stu-id="a5115-623">16</span></span>| <span data-ttu-id="a5115-624">16</span><span class="sxs-lookup"><span data-stu-id="a5115-624">16</span></span>|
| <span data-ttu-id="a5115-625">DW600</span><span class="sxs-lookup"><span data-stu-id="a5115-625">DW600</span></span> | <span data-ttu-id="a5115-626">24</span><span class="sxs-lookup"><span data-stu-id="a5115-626">24</span></span>| <span data-ttu-id="a5115-627">24</span><span class="sxs-lookup"><span data-stu-id="a5115-627">24</span></span>| <span data-ttu-id="a5115-628">1</span><span class="sxs-lookup"><span data-stu-id="a5115-628">1</span></span>| <span data-ttu-id="a5115-629">2</span><span class="sxs-lookup"><span data-stu-id="a5115-629">2</span></span>| <span data-ttu-id="a5115-630">4</span><span class="sxs-lookup"><span data-stu-id="a5115-630">4</span></span>| <span data-ttu-id="a5115-631">8</span><span class="sxs-lookup"><span data-stu-id="a5115-631">8</span></span>| <span data-ttu-id="a5115-632">16</span><span class="sxs-lookup"><span data-stu-id="a5115-632">16</span></span>| <span data-ttu-id="a5115-633">16</span><span class="sxs-lookup"><span data-stu-id="a5115-633">16</span></span>| <span data-ttu-id="a5115-634">16</span><span class="sxs-lookup"><span data-stu-id="a5115-634">16</span></span>| <span data-ttu-id="a5115-635">16</span><span class="sxs-lookup"><span data-stu-id="a5115-635">16</span></span>|
| <span data-ttu-id="a5115-636">DW1000</span><span class="sxs-lookup"><span data-stu-id="a5115-636">DW1000</span></span> | <span data-ttu-id="a5115-637">32</span><span class="sxs-lookup"><span data-stu-id="a5115-637">32</span></span>| <span data-ttu-id="a5115-638">40</span><span class="sxs-lookup"><span data-stu-id="a5115-638">40</span></span>| <span data-ttu-id="a5115-639">1</span><span class="sxs-lookup"><span data-stu-id="a5115-639">1</span></span>| <span data-ttu-id="a5115-640">2</span><span class="sxs-lookup"><span data-stu-id="a5115-640">2</span></span>| <span data-ttu-id="a5115-641">4</span><span class="sxs-lookup"><span data-stu-id="a5115-641">4</span></span>| <span data-ttu-id="a5115-642">8</span><span class="sxs-lookup"><span data-stu-id="a5115-642">8</span></span>| <span data-ttu-id="a5115-643">16</span><span class="sxs-lookup"><span data-stu-id="a5115-643">16</span></span>| <span data-ttu-id="a5115-644">32</span><span class="sxs-lookup"><span data-stu-id="a5115-644">32</span></span>| <span data-ttu-id="a5115-645">32</span><span class="sxs-lookup"><span data-stu-id="a5115-645">32</span></span>| <span data-ttu-id="a5115-646">32</span><span class="sxs-lookup"><span data-stu-id="a5115-646">32</span></span>|
| <span data-ttu-id="a5115-647">DW1200</span><span class="sxs-lookup"><span data-stu-id="a5115-647">DW1200</span></span> | <span data-ttu-id="a5115-648">32</span><span class="sxs-lookup"><span data-stu-id="a5115-648">32</span></span>| <span data-ttu-id="a5115-649">48</span><span class="sxs-lookup"><span data-stu-id="a5115-649">48</span></span>| <span data-ttu-id="a5115-650">1</span><span class="sxs-lookup"><span data-stu-id="a5115-650">1</span></span>| <span data-ttu-id="a5115-651">2</span><span class="sxs-lookup"><span data-stu-id="a5115-651">2</span></span>| <span data-ttu-id="a5115-652">4</span><span class="sxs-lookup"><span data-stu-id="a5115-652">4</span></span>| <span data-ttu-id="a5115-653">8</span><span class="sxs-lookup"><span data-stu-id="a5115-653">8</span></span>| <span data-ttu-id="a5115-654">16</span><span class="sxs-lookup"><span data-stu-id="a5115-654">16</span></span>| <span data-ttu-id="a5115-655">32</span><span class="sxs-lookup"><span data-stu-id="a5115-655">32</span></span>| <span data-ttu-id="a5115-656">32</span><span class="sxs-lookup"><span data-stu-id="a5115-656">32</span></span>| <span data-ttu-id="a5115-657">32</span><span class="sxs-lookup"><span data-stu-id="a5115-657">32</span></span>|
| <span data-ttu-id="a5115-658">DW1500</span><span class="sxs-lookup"><span data-stu-id="a5115-658">DW1500</span></span> | <span data-ttu-id="a5115-659">32</span><span class="sxs-lookup"><span data-stu-id="a5115-659">32</span></span>| <span data-ttu-id="a5115-660">60</span><span class="sxs-lookup"><span data-stu-id="a5115-660">60</span></span>| <span data-ttu-id="a5115-661">1</span><span class="sxs-lookup"><span data-stu-id="a5115-661">1</span></span>| <span data-ttu-id="a5115-662">2</span><span class="sxs-lookup"><span data-stu-id="a5115-662">2</span></span>| <span data-ttu-id="a5115-663">4</span><span class="sxs-lookup"><span data-stu-id="a5115-663">4</span></span>| <span data-ttu-id="a5115-664">8</span><span class="sxs-lookup"><span data-stu-id="a5115-664">8</span></span>| <span data-ttu-id="a5115-665">16</span><span class="sxs-lookup"><span data-stu-id="a5115-665">16</span></span>| <span data-ttu-id="a5115-666">32</span><span class="sxs-lookup"><span data-stu-id="a5115-666">32</span></span>| <span data-ttu-id="a5115-667">32</span><span class="sxs-lookup"><span data-stu-id="a5115-667">32</span></span>| <span data-ttu-id="a5115-668">32</span><span class="sxs-lookup"><span data-stu-id="a5115-668">32</span></span>|
| <span data-ttu-id="a5115-669">DW2000</span><span class="sxs-lookup"><span data-stu-id="a5115-669">DW2000</span></span> | <span data-ttu-id="a5115-670">32</span><span class="sxs-lookup"><span data-stu-id="a5115-670">32</span></span>| <span data-ttu-id="a5115-671">80</span><span class="sxs-lookup"><span data-stu-id="a5115-671">80</span></span>| <span data-ttu-id="a5115-672">1</span><span class="sxs-lookup"><span data-stu-id="a5115-672">1</span></span>| <span data-ttu-id="a5115-673">2</span><span class="sxs-lookup"><span data-stu-id="a5115-673">2</span></span>| <span data-ttu-id="a5115-674">4</span><span class="sxs-lookup"><span data-stu-id="a5115-674">4</span></span>| <span data-ttu-id="a5115-675">8</span><span class="sxs-lookup"><span data-stu-id="a5115-675">8</span></span>| <span data-ttu-id="a5115-676">16</span><span class="sxs-lookup"><span data-stu-id="a5115-676">16</span></span>| <span data-ttu-id="a5115-677">32</span><span class="sxs-lookup"><span data-stu-id="a5115-677">32</span></span>| <span data-ttu-id="a5115-678">64</span><span class="sxs-lookup"><span data-stu-id="a5115-678">64</span></span>| <span data-ttu-id="a5115-679">64</span><span class="sxs-lookup"><span data-stu-id="a5115-679">64</span></span>|
| <span data-ttu-id="a5115-680">DW3000</span><span class="sxs-lookup"><span data-stu-id="a5115-680">DW3000</span></span> | <span data-ttu-id="a5115-681">32</span><span class="sxs-lookup"><span data-stu-id="a5115-681">32</span></span>| <span data-ttu-id="a5115-682">120</span><span class="sxs-lookup"><span data-stu-id="a5115-682">120</span></span>| <span data-ttu-id="a5115-683">1</span><span class="sxs-lookup"><span data-stu-id="a5115-683">1</span></span>| <span data-ttu-id="a5115-684">2</span><span class="sxs-lookup"><span data-stu-id="a5115-684">2</span></span>| <span data-ttu-id="a5115-685">4</span><span class="sxs-lookup"><span data-stu-id="a5115-685">4</span></span>| <span data-ttu-id="a5115-686">8</span><span class="sxs-lookup"><span data-stu-id="a5115-686">8</span></span>| <span data-ttu-id="a5115-687">16</span><span class="sxs-lookup"><span data-stu-id="a5115-687">16</span></span>| <span data-ttu-id="a5115-688">32</span><span class="sxs-lookup"><span data-stu-id="a5115-688">32</span></span>| <span data-ttu-id="a5115-689">64</span><span class="sxs-lookup"><span data-stu-id="a5115-689">64</span></span>| <span data-ttu-id="a5115-690">64</span><span class="sxs-lookup"><span data-stu-id="a5115-690">64</span></span>|
| <span data-ttu-id="a5115-691">DW6000</span><span class="sxs-lookup"><span data-stu-id="a5115-691">DW6000</span></span> | <span data-ttu-id="a5115-692">32</span><span class="sxs-lookup"><span data-stu-id="a5115-692">32</span></span>| <span data-ttu-id="a5115-693">240</span><span class="sxs-lookup"><span data-stu-id="a5115-693">240</span></span>| <span data-ttu-id="a5115-694">1</span><span class="sxs-lookup"><span data-stu-id="a5115-694">1</span></span>| <span data-ttu-id="a5115-695">2</span><span class="sxs-lookup"><span data-stu-id="a5115-695">2</span></span>| <span data-ttu-id="a5115-696">4</span><span class="sxs-lookup"><span data-stu-id="a5115-696">4</span></span>| <span data-ttu-id="a5115-697">8</span><span class="sxs-lookup"><span data-stu-id="a5115-697">8</span></span>| <span data-ttu-id="a5115-698">16</span><span class="sxs-lookup"><span data-stu-id="a5115-698">16</span></span>| <span data-ttu-id="a5115-699">32</span><span class="sxs-lookup"><span data-stu-id="a5115-699">32</span></span>| <span data-ttu-id="a5115-700">64</span><span class="sxs-lookup"><span data-stu-id="a5115-700">64</span></span>| <span data-ttu-id="a5115-701">128</span><span class="sxs-lookup"><span data-stu-id="a5115-701">128</span></span>|

<span data-ttu-id="a5115-702">Nestas tabelas, você pode ver que um SQL Data Warehouse em execução como DW1000 aloca uma quantidade máxima de 32 consultas simultâneas e um total de 40 slots de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="a5115-702">From these tables, you can see that SQL Data Warehouse running as DW1000 allocates a maximum of 32 concurrent queries and a total of 40 concurrency slots.</span></span> <span data-ttu-id="a5115-703">Se todos os usuários estivessem em execução no smallrc, seriam permitidas 32 consultas simultâneas, pois cada consulta consumiria um slot de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="a5115-703">If all users are running in smallrc, 32 concurrent queries would be allowed because each query would consume 1 concurrency slot.</span></span> <span data-ttu-id="a5115-704">Se todos os usuários em um DW1000 estavam em execução no mediumrc, cada consulta seria alocada 800 MB por distribuição de uma alocação de memória total de 47 GB por consulta, simultaneidade seria too5 limitado de usuários (40 slots de simultaneidade slots de 8 por usuário mediumrc /).</span><span class="sxs-lookup"><span data-stu-id="a5115-704">If all users on a DW1000 were running in mediumrc, each query would be allocated 800 MB per distribution for a total memory allocation of 47 GB per query, and concurrency would be limited too5 users (40 concurrency slots / 8 slots per mediumrc user).</span></span>

## <a name="selecting-proper-resource-class"></a><span data-ttu-id="a5115-705">Selecionando a classe de recursos apropriada</span><span class="sxs-lookup"><span data-stu-id="a5115-705">Selecting proper resource class</span></span>  
<span data-ttu-id="a5115-706">Uma prática recomendada é a classe de recurso do toopermanently atribuir usuários tooa em vez de alterar suas classes de recursos.</span><span class="sxs-lookup"><span data-stu-id="a5115-706">A good practice is toopermanently assign users tooa resource class rather than changing their resource classes.</span></span> <span data-ttu-id="a5115-707">Por exemplo, tabelas de columnstore cargas tooclustered criam índices de alta qualidade quando mais memória alocada.</span><span class="sxs-lookup"><span data-stu-id="a5115-707">For example, loads tooclustered columnstore tables create higher-quality indexes when allocated more memory.</span></span> <span data-ttu-id="a5115-708">tooensure que carrega tem acesso toohigher memória, cria um usuário especificamente para carregar dados e atribui permanentemente esta classe de recursos do usuário tooa superior.</span><span class="sxs-lookup"><span data-stu-id="a5115-708">tooensure that loads have access toohigher memory, create a user specifically for loading data and permanently assign this user tooa higher resource class.</span></span>
<span data-ttu-id="a5115-709">Há algumas toofollow práticas recomendada aqui.</span><span class="sxs-lookup"><span data-stu-id="a5115-709">There are a couple of best practices toofollow here.</span></span> <span data-ttu-id="a5115-710">Como mencionado acima, o SQL DW dá suporte a dois tipos de classes de recursos: classes de recursos estáticos e classes de recursos dinâmicos.</span><span class="sxs-lookup"><span data-stu-id="a5115-710">As mentioned above, SQL DW supports two kinds of resource class types: static resource classes and dynamic resource classes.</span></span>
### <a name="loading-best-practices"></a><span data-ttu-id="a5115-711">Melhores práticas de carregamento</span><span class="sxs-lookup"><span data-stu-id="a5115-711">Loading best practices</span></span>
1.  <span data-ttu-id="a5115-712">Se as expectativas de saudação carrega com quantidade regular de dados, uma classe de recurso estático é uma boa opção.</span><span class="sxs-lookup"><span data-stu-id="a5115-712">If hello expectations are loads with regular amount of data, a static resource class is a good choice.</span></span> <span data-ttu-id="a5115-713">Posteriormente, quando o dimensionamento das tooget mais potência computacional, data warehouse de saudação será capaz de toorun simultâneo mais consultas out-of-the-box, como usuário de carga Olá não consome mais memória.</span><span class="sxs-lookup"><span data-stu-id="a5115-713">Later, when scaling up tooget more computational power, hello data warehouse will be able toorun more concurrent queries out-of-the-box, as hello load user does not consume more memory.</span></span>
2.  <span data-ttu-id="a5115-714">Se as expectativas de saudação maiores cargas em algumas ocasiões, uma classe de recurso dinâmico é uma boa opção.</span><span class="sxs-lookup"><span data-stu-id="a5115-714">If hello expectations are bigger loads in some occasions, a dynamic resource class is a good choice.</span></span> <span data-ttu-id="a5115-715">Posteriormente, quando o dimensionamento das tooget mais potência computacional, Olá carga usuário receberá mais memória out-of-the-box, permitindo, portanto, Olá carga tooperform mais rapidamente.</span><span class="sxs-lookup"><span data-stu-id="a5115-715">Later, when scaling up tooget more computational power, hello load user will get more memory out-of-the-box, hence allowing hello load tooperform faster.</span></span>

<span data-ttu-id="a5115-716">Olá memória necessária tooprocess cargas com eficiência depende Olá natureza da tabela de saudação carregada e quantidade de saudação de dados processados.</span><span class="sxs-lookup"><span data-stu-id="a5115-716">hello memory needed tooprocess loads efficiently depends on hello nature of hello table loaded and hello amount of data processed.</span></span> <span data-ttu-id="a5115-717">Por exemplo, carregar dados em tabelas CCI requer que algumas rowgroups CCI toolet memória alcançar ideais.</span><span class="sxs-lookup"><span data-stu-id="a5115-717">For instance, loading data into CCI tables requires some memory toolet CCI rowgroups reach optimality.</span></span> <span data-ttu-id="a5115-718">Para obter mais detalhes, consulte índices de Columnstore Olá - diretrizes de carregamento de dados.</span><span class="sxs-lookup"><span data-stu-id="a5115-718">For more details, see hello Columnstore indexes - data loading guidance.</span></span>

<span data-ttu-id="a5115-719">Como prática recomendada, aconselhamos que você toouse pelo menos 200MB de memória para cargas.</span><span class="sxs-lookup"><span data-stu-id="a5115-719">As a best practice, we advise you toouse at least 200MB of memory for loads.</span></span>

### <a name="querying-best-practices"></a><span data-ttu-id="a5115-720">Melhores práticas de consulta</span><span class="sxs-lookup"><span data-stu-id="a5115-720">Querying best practices</span></span>
<span data-ttu-id="a5115-721">As consultas têm requisitos diferentes dependendo de sua complexidade.</span><span class="sxs-lookup"><span data-stu-id="a5115-721">Queries have different requirements depending on their complexity.</span></span> <span data-ttu-id="a5115-722">Aumentar a memória por consulta ou aumentar a simultaneidade de saudação são ambas as maneiras válidas tooaugment produtividade geral dependendo das necessidades de consulta hello.</span><span class="sxs-lookup"><span data-stu-id="a5115-722">Increasing memory per query or increasing hello concurrency are both valid ways tooaugment overall throughput depending on hello query needs.</span></span>
1.  <span data-ttu-id="a5115-723">Se expectativas Olá são consultas complexas, regulares (toogenerate, por exemplo, relatórios de diários e semanais) e não é necessário tootake vantagem de simultaneidade, uma classe de recurso dinâmico é uma boa opção.</span><span class="sxs-lookup"><span data-stu-id="a5115-723">If hello expectations are regular, complex queries (for instance, toogenerate daily and weekly reports) and do not need tootake advantage of concurrency, a dynamic resource class is a good choice.</span></span> <span data-ttu-id="a5115-724">Se o sistema Olá tem mais tooprocess de dados, expansão do data warehouse de saudação, portanto, fornecerá automaticamente usuário de toohello mais memória execução de consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="a5115-724">If hello system has more data tooprocess, scaling up hello data warehouse will therefore automatically provide more memory toohello user running hello query.</span></span>
2.  <span data-ttu-id="a5115-725">Se as expectativas de saudação são padrões de simultaneidade diurnal ou variável (por exemplo se o banco de dados de saudação é consultado por meio de uma interface amplamente acessível da web), uma classe de recurso estático é uma boa opção.</span><span class="sxs-lookup"><span data-stu-id="a5115-725">If hello expectations are variable or diurnal concurrency patterns (for instance if hello database is queried through a web UI broadly accessible), a static resource class is a good choice.</span></span> <span data-ttu-id="a5115-726">Posteriormente, ao aumento toodata warehouse, usuário Olá associado à classe de recurso estático hello serão automaticamente ser capaz de toorun consultas mais simultâneas.</span><span class="sxs-lookup"><span data-stu-id="a5115-726">Later, when scaling up toodata warehouse, hello user associated with hello static resource class will automatically be able toorun more concurrent queries.</span></span>

<span data-ttu-id="a5115-727">Selecionando concessão de memória apropriada dependendo da necessidade de saudação da consulta é incomum, pois ele depende de muitos fatores, como quantidade de saudação de dados consultados, natureza Olá esquemas de tabela hello e vários junção, seleção e predicados de grupo.</span><span class="sxs-lookup"><span data-stu-id="a5115-727">Selecting proper memory grant depending on hello need of your query is non-trivial, as it depends on many factors, such as hello amount of data queried, hello nature of hello table schemas, and various join, selection, and group predicates.</span></span> <span data-ttu-id="a5115-728">Alocar mais memória permitirá consultas toocomplete mais rápido do ponto de vista geral, mas reduziria Olá simultaneidade geral.</span><span class="sxs-lookup"><span data-stu-id="a5115-728">From a general standpoint, allocating more memory will allow queries toocomplete faster, but would reduce hello overall concurrency.</span></span> <span data-ttu-id="a5115-729">Se a simultaneidade não for um problema, a alocação excessiva de memória não será prejudicial.</span><span class="sxs-lookup"><span data-stu-id="a5115-729">If concurrency is not an issue, over-allocating memory does not harm.</span></span> <span data-ttu-id="a5115-730">taxa de transferência toofine ajustar, tentativa de vários tipos de classes de recursos pode ser necessária.</span><span class="sxs-lookup"><span data-stu-id="a5115-730">toofine-tune throughput, trying various flavors of resource classes may be required.</span></span>

<span data-ttu-id="a5115-731">Você pode usar o seguinte Olá armazenados procedimento toofigure limite de concessão de memória e simultaneidade por classe de recurso a uma determinada SLO e hello mais próximo melhor recurso classe para memória intensiva CCI operações de tabela CCI não particionada em uma classe de recurso específico:</span><span class="sxs-lookup"><span data-stu-id="a5115-731">You can use hello following stored procedure toofigure out concurrency and memory grant per resource class at a given SLO and hello closest best resource class for memory intensive CCI operations on non-partitioned CCI table at a given resource class:</span></span>

#### <a name="description"></a><span data-ttu-id="a5115-732">Descrição:</span><span class="sxs-lookup"><span data-stu-id="a5115-732">Description:</span></span>  
<span data-ttu-id="a5115-733">Aqui está a finalidade de saudação deste procedimento armazenado:</span><span class="sxs-lookup"><span data-stu-id="a5115-733">Here's hello purpose of this stored procedure:</span></span>  
1. <span data-ttu-id="a5115-734">toohelp usuário descobrir concessão de memória e simultaneidade por classe de recurso em um determinado SLO.</span><span class="sxs-lookup"><span data-stu-id="a5115-734">toohelp user figure out concurrency and memory grant per resource class at a given SLO.</span></span> <span data-ttu-id="a5115-735">Usuário precisa tooprovide NULL para o esquema e tablename isso conforme mostrado no exemplo hello abaixo.</span><span class="sxs-lookup"><span data-stu-id="a5115-735">User needs tooprovide NULL for both schema and tablename for this as shown in hello example below.</span></span>  
2. <span data-ttu-id="a5115-736">usuário toohelp descobrir hello mais próxima melhor classe de recurso para Olá memória intensed operações CCI (carga de tabela de cópia, recriar o índice, etc.) em uma tabela CCI não particionada em uma classe de recurso específico.</span><span class="sxs-lookup"><span data-stu-id="a5115-736">toohelp user figure out hello closest best resource class for hello memory intensed CCI operations (load, copy table, rebuild index, etc.) on non partitioned CCI table at a given resource class.</span></span> <span data-ttu-id="a5115-737">Olá armazenado proc usa toofind de esquema de tabela out Olá concessão de memória necessária para isso.</span><span class="sxs-lookup"><span data-stu-id="a5115-737">hello stored proc uses table schema toofind out hello required memory grant for this.</span></span>

#### <a name="dependencies--restrictions"></a><span data-ttu-id="a5115-738">Dependências e restrições:</span><span class="sxs-lookup"><span data-stu-id="a5115-738">Dependencies & Restrictions:</span></span>
- <span data-ttu-id="a5115-739">Esse procedimento armazenado não é um requisito de memória toocalculate projetado para a tabela particionada cci.</span><span class="sxs-lookup"><span data-stu-id="a5115-739">This stored proc is not designed toocalculate memory requirement for partitioned-cci table.</span></span>    
- <span data-ttu-id="a5115-740">Esse procedimento armazenado não tem um requisito de memória em consideração para a parte SELECT Olá de inserção/CTAS-SELECT e pressupõe que ele toobe SELECT simples.</span><span class="sxs-lookup"><span data-stu-id="a5115-740">This stored proc doesn't take memory requirement into account for hello SELECT part of CTAS/INSERT-SELECT and assumes it toobe a simple SELECT.</span></span>
- <span data-ttu-id="a5115-741">Esse procedimento armazenado usa uma tabela temporária para que isso pode ser usado na sessão Olá onde esse procedimento armazenado foi criado.</span><span class="sxs-lookup"><span data-stu-id="a5115-741">This stored proc uses a temp table so this can be used in hello session where this stored proc was created.</span></span>    
- <span data-ttu-id="a5115-742">Esse procedimento armazenado depende de ofertas de saudação atual (por exemplo, a configuração de hardware, a configuração DMS) e se qualquer um dos que for alterado, em seguida, esse procedimento armazenado não funcionará corretamente.</span><span class="sxs-lookup"><span data-stu-id="a5115-742">This stored proc depends on hello current offerings (e.g. hardware configuration, DMS config) and if any of that changes then this stored proc would not work correctly.</span></span>  
- <span data-ttu-id="a5115-743">Esse procedimento armazenado depende do limite de simultaneidade oferecidos existente e se isso mudar, o procedimento armazenado não funcionará corretamente.</span><span class="sxs-lookup"><span data-stu-id="a5115-743">This stored proc depends on existing offered concurrency limit and if that changes then this stored proc would not work correctly.</span></span>  
- <span data-ttu-id="a5115-744">Esse procedimento armazenado depende das ofertas de classe de recursos existentes e se isso mudar, o procedimento armazenado não funcionará corretamente.</span><span class="sxs-lookup"><span data-stu-id="a5115-744">This stored proc depends on existing resource class offerings and if that changes then this stored proc wuold not work correctly.</span></span>  

>  [!NOTE]  
>  <span data-ttu-id="a5115-745">Se nenhuma saída aparecer após a execução do procedimento armazenado com parâmetros fornecidos, isso poderá ser consequência de dois problemas.</span><span class="sxs-lookup"><span data-stu-id="a5115-745">If you are not getting output after executing stored procedure with parameters provided then there could be two cases.</span></span> <br /><span data-ttu-id="a5115-746">1. Um parâmetro de DW contém o valor inválido de SLO</span><span class="sxs-lookup"><span data-stu-id="a5115-746">1. Either DW Parameter contains invalid SLO value</span></span> <br /><span data-ttu-id="a5115-747">2. OU não há nenhuma classe de recurso correspondente para a operação CCI se o nome de tabela tiver sido fornecido.</span><span class="sxs-lookup"><span data-stu-id="a5115-747">2. OR there are no matching resource class for CCI operation if table name was provided.</span></span> <br /><span data-ttu-id="a5115-748">Por exemplo, em DW100, concessão de memória mais alto disponível é de 400MB e se o esquema de tabela for grande o suficiente toocross Olá requisito de 400MB.</span><span class="sxs-lookup"><span data-stu-id="a5115-748">For example, at DW100, highest memory grant available is 400MB and if table schema is wide enough toocross hello requirement of 400MB.</span></span>
      
#### <a name="usage-example"></a><span data-ttu-id="a5115-749">Exemplo de uso:</span><span class="sxs-lookup"><span data-stu-id="a5115-749">Usage example:</span></span>
<span data-ttu-id="a5115-750">Sintaxe:</span><span class="sxs-lookup"><span data-stu-id="a5115-750">Syntax:</span></span>  
`EXEC dbo.prc_workload_management_by_DWU @DWU VARCHAR(7), @SCHEMA_NAME VARCHAR(128), @TABLE_NAME VARCHAR(128)`  
1. <span data-ttu-id="a5115-751">@DWU:Forneça um tooextract de parâmetro NULL Olá DWU atual do BD de DW do hello ou fornecer qualquer suporte DWU na forma de saudação de 'DW100'</span><span class="sxs-lookup"><span data-stu-id="a5115-751">@DWU: Either provide a NULL parameter tooextract hello current DWU from hello DW DB or provide any supported DWU in hello form of 'DW100'</span></span>
2. <span data-ttu-id="a5115-752">@SCHEMA_NAME:Forneça um nome de esquema da tabela de saudação</span><span class="sxs-lookup"><span data-stu-id="a5115-752">@SCHEMA_NAME: Provide a schema name of hello table</span></span>
3. <span data-ttu-id="a5115-753">@TABLE_NAME:Forneça um nome de tabela de interesse Olá</span><span class="sxs-lookup"><span data-stu-id="a5115-753">@TABLE_NAME: Provide a table name of hello interest</span></span>

<span data-ttu-id="a5115-754">Exemplos executando esse procedimento armazenado:</span><span class="sxs-lookup"><span data-stu-id="a5115-754">Examples executing this stored proc:</span></span>  
```sql  
EXEC dbo.prc_workload_management_by_DWU 'DW2000', 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU NULL, 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU 'DW6000', NULL, NULL;  
EXEC dbo.prc_workload_management_by_DWU NULL, NULL, NULL;  
```

<span data-ttu-id="a5115-755">Table1 usado em Olá acima exemplos pôde ser criado como abaixo:</span><span class="sxs-lookup"><span data-stu-id="a5115-755">Table1 used in hello above examples could be created as below:</span></span>  
`CREATE TABLE Table1 (a int, b varchar(50), c decimal (18,10), d char(10), e varbinary(15), f float, g datetime, h date);`

#### <a name="heres-hello-stored-procedure-definition"></a><span data-ttu-id="a5115-756">Aqui está a definição do procedimento armazenada de saudação:</span><span class="sxs-lookup"><span data-stu-id="a5115-756">Here's hello stored procedure definition:</span></span>
```sql  
-------------------------------------------------------------------------------
-- Dropping prc_workload_management_by_DWU procedure if it exists.
-------------------------------------------------------------------------------
IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'prc_workload_management_by_DWU')
DROP PROCEDURE dbo.prc_workload_management_by_DWU
GO

-------------------------------------------------------------------------------
-- Creating prc_workload_management_by_DWU.
-------------------------------------------------------------------------------
CREATE PROCEDURE dbo.prc_workload_management_by_DWU
(   @DWU VARCHAR(7),
      @SCHEMA_NAME VARCHAR(128),
       @TABLE_NAME VARCHAR(128)
)
AS
IF @DWU IS NULL
BEGIN
-- Selecting proper DWU for hello current DB if not specified.
SET @DWU = (
  SELECT 'DW'+CAST(COUNT(*)*100 AS VARCHAR(10))
  FROM sys.dm_pdw_nodes
  WHERE type = 'COMPUTE')
END

DECLARE @DWU_NUM INT
SET @DWU_NUM = CAST (SUBSTRING(@DWU, 3, LEN(@DWU)-2) AS INT)

-- Raise error if either schema name or table name is supplied but not both them supplied
--IF ((@SCHEMA_NAME IS NOT NULL AND @TABLE_NAME IS NULL) OR (@TABLE_NAME IS NULL AND @SCHEMA_NAME IS NOT NULL))
--     RAISEERROR('User need toosupply either both Schema Name and Table Name or none of them')
       
-- Dropping temp table if exists.
IF OBJECT_ID('tempdb..#ref') IS NOT NULL
BEGIN
  DROP TABLE #ref;
END

-- Creating ref. temptable (CTAS) toohold mapping info.
-- CREATE TABLE #ref
CREATE TABLE #ref
WITH (DISTRIBUTION = ROUND_ROBIN)
AS 
WITH
-- Creating concurrency slots mapping for various DWUs.
alloc
AS
(
  SELECT 'DW100' AS DWU, 4 AS max_queries, 4 AS max_slots, 1 AS slots_used_smallrc, 1 AS slots_used_mediumrc,
        2 AS slots_used_largerc, 4 AS slots_used_xlargerc, 1 AS slots_used_staticrc10, 2 AS slots_used_staticrc20,
        4 AS slots_used_staticrc30, 4 AS slots_used_staticrc40, 4 AS slots_used_staticrc50,
        4 AS slots_used_staticrc60, 4 AS slots_used_staticrc70, 4 AS slots_used_staticrc80
  UNION ALL
    SELECT 'DW200', 8, 8, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW300', 12, 12, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW400', 16, 16, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
     SELECT 'DW500', 20, 20, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW600', 24, 24, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW1000', 32, 40, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1200', 32, 48, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1500', 32, 60, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW2000', 32, 80, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
   SELECT 'DW3000', 32, 120, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
    SELECT 'DW6000', 32, 240, 1, 32, 64, 128, 1, 2, 4, 8, 16, 32, 64, 128
)
-- Creating workload mapping tootheir corresponding slot consumption and default memory grant.
,map
AS
(
  SELECT 'SloDWGroupC00' AS wg_name,1 AS slots_used,100 AS tgt_mem_grant_MB
  UNION ALL
    SELECT 'SloDWGroupC01',2,200
  UNION ALL
    SELECT 'SloDWGroupC02',4,400
  UNION ALL
    SELECT 'SloDWGroupC03',8,800
  UNION ALL
    SELECT 'SloDWGroupC04',16,1600
  UNION ALL
    SELECT 'SloDWGroupC05',32,3200
  UNION ALL
    SELECT 'SloDWGroupC06',64,6400
  UNION ALL
    SELECT 'SloDWGroupC07',128,12800
)
-- Creating ref based on current / asked DWU.
, ref
AS
(
  SELECT  a1.*
  ,       m1.wg_name          AS wg_name_smallrc
  ,       m1.tgt_mem_grant_MB AS tgt_mem_grant_MB_smallrc
  ,       m2.wg_name          AS wg_name_mediumrc
  ,       m2.tgt_mem_grant_MB AS tgt_mem_grant_MB_mediumrc
  ,       m3.wg_name          AS wg_name_largerc
  ,       m3.tgt_mem_grant_MB AS tgt_mem_grant_MB_largerc
  ,       m4.wg_name          AS wg_name_xlargerc
  ,       m4.tgt_mem_grant_MB AS tgt_mem_grant_MB_xlargerc
  ,       m5.wg_name          AS wg_name_staticrc10
  ,       m5.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc10
  ,       m6.wg_name          AS wg_name_staticrc20
  ,       m6.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc20
  ,       m7.wg_name          AS wg_name_staticrc30
  ,       m7.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc30
  ,       m8.wg_name          AS wg_name_staticrc40
  ,       m8.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc40
  ,       m9.wg_name          AS wg_name_staticrc50
  ,       m9.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc50
  ,       m10.wg_name          AS wg_name_staticrc60
  ,       m10.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc60
  ,       m11.wg_name          AS wg_name_staticrc70
  ,       m11.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc70
  ,       m12.wg_name          AS wg_name_staticrc80
  ,       m12.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc80
  FROM alloc a1
  JOIN map   m1  ON a1.slots_used_smallrc     = m1.slots_used
  JOIN map   m2  ON a1.slots_used_mediumrc    = m2.slots_used
  JOIN map   m3  ON a1.slots_used_largerc     = m3.slots_used
  JOIN map   m4  ON a1.slots_used_xlargerc    = m4.slots_used
  JOIN map   m5  ON a1.slots_used_staticrc10    = m5.slots_used
  JOIN map   m6  ON a1.slots_used_staticrc20    = m6.slots_used
  JOIN map   m7  ON a1.slots_used_staticrc30    = m7.slots_used
  JOIN map   m8  ON a1.slots_used_staticrc40    = m8.slots_used
  JOIN map   m9  ON a1.slots_used_staticrc50    = m9.slots_used
  JOIN map   m10  ON a1.slots_used_staticrc60    = m10.slots_used
  JOIN map   m11  ON a1.slots_used_staticrc70    = m11.slots_used
  JOIN map   m12  ON a1.slots_used_staticrc80    = m12.slots_used
-- WHERE   a1.DWU = @DWU
  WHERE   a1.DWU = UPPER(@DWU)
)
SELECT  DWU
,       max_queries
,       max_slots
,       slots_used
,       wg_name
,       tgt_mem_grant_MB
,       up1 as rc
,       (ROW_NUMBER() OVER(PARTITION BY DWU ORDER BY DWU)) as rc_id
FROM
(
    SELECT  DWU
    ,       max_queries
    ,       max_slots
    ,       slots_used
    ,       wg_name
    ,       tgt_mem_grant_MB
    ,       REVERSE(SUBSTRING(REVERSE(wg_names),1,CHARINDEX('_',REVERSE(wg_names),1)-1)) as up1
    ,       REVERSE(SUBSTRING(REVERSE(tgt_mem_grant_MBs),1,CHARINDEX('_',REVERSE(tgt_mem_grant_MBs),1)-1)) as up2
    ,       REVERSE(SUBSTRING(REVERSE(slots_used_all),1,CHARINDEX('_',REVERSE(slots_used_all),1)-1)) as up3
    FROM    ref AS r1
    UNPIVOT
    (
        wg_name FOR wg_names IN (wg_name_smallrc,wg_name_mediumrc,wg_name_largerc,wg_name_xlargerc,
        wg_name_staticrc10, wg_name_staticrc20, wg_name_staticrc30, wg_name_staticrc40, wg_name_staticrc50,
        wg_name_staticrc60, wg_name_staticrc70, wg_name_staticrc80)
    ) AS r2
    UNPIVOT
    (
        tgt_mem_grant_MB FOR tgt_mem_grant_MBs IN (tgt_mem_grant_MB_smallrc,tgt_mem_grant_MB_mediumrc,
        tgt_mem_grant_MB_largerc,tgt_mem_grant_MB_xlargerc, tgt_mem_grant_MB_staticrc10, tgt_mem_grant_MB_staticrc20,
        tgt_mem_grant_MB_staticrc30, tgt_mem_grant_MB_staticrc40, tgt_mem_grant_MB_staticrc50,
        tgt_mem_grant_MB_staticrc60, tgt_mem_grant_MB_staticrc70, tgt_mem_grant_MB_staticrc80)
    ) AS r3
    UNPIVOT
    (
        slots_used FOR slots_used_all IN (slots_used_smallrc,slots_used_mediumrc,slots_used_largerc,
        slots_used_xlargerc, slots_used_staticrc10, slots_used_staticrc20, slots_used_staticrc30,
        slots_used_staticrc40, slots_used_staticrc50, slots_used_staticrc60, slots_used_staticrc70,
        slots_used_staticrc80)
    ) AS r4
) a
WHERE   up1 = up2
AND     up1 = up3
;
-- Getting current info about workload groups.
WITH  
dmv  
AS  
(
  SELECT
          rp.name                                           AS rp_name
  ,       rp.max_memory_kb*1.0/1048576                      AS rp_max_mem_GB
  ,       (rp.max_memory_kb*1.0/1024)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_MB
  ,       (rp.max_memory_kb*1.0/1048576)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_GB
  ,       wg.name                                           AS wg_name
  ,       wg.importance                                     AS importance
  ,       wg.request_max_memory_grant_percent               AS request_max_memory_grant_percent
  FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
  JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    ON  wg.pdw_node_id  = rp.pdw_node_id
                                                                  AND wg.pool_id      = rp.pool_id
  WHERE   rp.name = 'SloDWPool'
  GROUP BY
          rp.name
  ,       rp.max_memory_kb
  ,       wg.name
  ,       wg.importance
  ,       wg.request_max_memory_grant_percent
)
-- Creating resource class name mapping.
,names
AS
(
  SELECT 'smallrc' as resource_class, 1 as rc_id
  UNION ALL
    SELECT 'mediumrc', 2
  UNION ALL
    SELECT 'largerc', 3
  UNION ALL
    SELECT 'xlargerc', 4
  UNION ALL
    SELECT 'staticrc10', 5
  UNION ALL
    SELECT 'staticrc20', 6
  UNION ALL
    SELECT 'staticrc30', 7
  UNION ALL
    SELECT 'staticrc40', 8
  UNION ALL
    SELECT 'staticrc50', 9
  UNION ALL
    SELECT 'staticrc60', 10
  UNION ALL
    SELECT 'staticrc70', 11
  UNION ALL
    SELECT 'staticrc80', 12
)
,base AS
(   SELECT  schema_name
    ,       table_name
    ,       SUM(column_count)                   AS column_count
    ,       ISNULL(SUM(short_string_column_count),0)   AS short_string_column_count
    ,       ISNULL(SUM(long_string_column_count),0)    AS long_string_column_count
    FROM    (   SELECT  sm.name                                             AS schema_name
                ,       tb.name                                             AS table_name
                ,       COUNT(co.column_id)                                 AS column_count
                           ,       CASE    WHEN co.system_type_id IN (36,43,106,108,165,167,173,175,231,239) 
                                AND  co.max_length <= 32 
                                THEN COUNT(co.column_id) 
                        END                                                 AS short_string_column_count
                ,       CASE    WHEN co.system_type_id IN (165,167,173,175,231,239) 
                                AND  co.max_length > 32 and co.max_length <=8000
                                THEN COUNT(co.column_id) 
                        END                                                 AS long_string_column_count
                FROM    sys.schemas AS sm
                JOIN    sys.tables  AS tb   on sm.[schema_id] = tb.[schema_id]
                JOIN    sys.columns AS co   ON tb.[object_id] = co.[object_id]
                           WHERE tb.name = @TABLE_NAME AND sm.name = @SCHEMA_NAME
                GROUP BY sm.name
                ,        tb.name
                ,        co.system_type_id
                ,        co.max_length            ) a
GROUP BY schema_name
,        table_name
)
, size AS
(
SELECT  schema_name
,       table_name
,       75497472                                            AS table_overhead

,       column_count*1048576*8                              AS column_size
,       short_string_column_count*1048576*32                       AS short_string_size,       (long_string_column_count*16777216) AS long_string_size
FROM    base
UNION
SELECT CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as schema_name
         ,CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as table_name
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as table_overhead
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as column_size
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as short_string_size

,CASE WHEN COUNT(*) = 0 THEN 0 END as long_string_size
FROM   base
)
, load_multiplier as 
(
SELECT  CASE 
                     WHEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) > 0 THEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) 
                     ELSE 1 
              END AS multipliplication_factor
) 
       SELECT  r1.DWU
       , schema_name
       , table_name
       , rc.resource_class as closest_rc_in_increasing_order
       , max_queries_at_this_rc = CASE
             WHEN (r1.max_slots / r1.slots_used > r1.max_queries)
                  THEN r1.max_queries
             ELSE r1.max_slots / r1.slots_used
                  END
       , r1.max_slots as max_concurrency_slots
       , r1.slots_used as required_slots_for_the_rc
       , r1.tgt_mem_grant_MB  as rc_mem_grant_MB
       , CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) AS est_mem_grant_required_for_cci_operation_MB       
       FROM    size, load_multiplier, #ref r1, names  rc
       WHERE r1.rc_id=rc.rc_id
                     AND CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) < r1.tgt_mem_grant_MB
       ORDER BY ABS(CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) - r1.tgt_mem_grant_MB)
GO
```

## <a name="query-importance"></a><span data-ttu-id="a5115-757">Importância da consulta</span><span class="sxs-lookup"><span data-stu-id="a5115-757">Query importance</span></span>
<span data-ttu-id="a5115-758">O SQL Data Warehouse implementa classes de recursos usando grupos de carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="a5115-758">SQL Data Warehouse implements resource classes by using workload groups.</span></span> <span data-ttu-id="a5115-759">Há um total de oito grupos de cargas de trabalho que controlam o comportamento de Olá Olá de classes de recurso entre Olá vários tamanhos DWU.</span><span class="sxs-lookup"><span data-stu-id="a5115-759">There are a total of eight workload groups that control hello behavior of hello resource classes across hello various DWU sizes.</span></span> <span data-ttu-id="a5115-760">Para qualquer DWU SQL Data Warehouse usa apenas quatro das oito grupos de cargas de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="a5115-760">For any DWU, SQL Data Warehouse uses only four of hello eight workload groups.</span></span> <span data-ttu-id="a5115-761">Isso faz sentido porque é atribuída a cada grupo de carga de trabalho tooone de quatro classes de recursos: smallrc, mediumrc, largerc, ou xlargerc.</span><span class="sxs-lookup"><span data-stu-id="a5115-761">This makes sense because each workload group is assigned tooone of four resource classes: smallrc, mediumrc, largerc, or xlargerc.</span></span> <span data-ttu-id="a5115-762">Olá importância de Noções básicas sobre grupos de carga de trabalho de saudação é que alguns desses grupos de carga de trabalho estão definidos toohigher *importância*.</span><span class="sxs-lookup"><span data-stu-id="a5115-762">hello importance of understanding hello workload groups is that some of these workload groups are set toohigher *importance*.</span></span> <span data-ttu-id="a5115-763">A importância é usada para agendamento de CPU.</span><span class="sxs-lookup"><span data-stu-id="a5115-763">Importance is used for CPU scheduling.</span></span> <span data-ttu-id="a5115-764">As consultas executadas com importância alta obterão três vezes mais ciclos de CPU do que aquelas com importância média.</span><span class="sxs-lookup"><span data-stu-id="a5115-764">Queries run with high importance will get three times more CPU cycles than those with medium importance.</span></span> <span data-ttu-id="a5115-765">Portanto, os mapeamentos de slot de simultaneidade também determinam a prioridade da CPU.</span><span class="sxs-lookup"><span data-stu-id="a5115-765">Therefore, concurrency slot mappings also determine CPU priority.</span></span> <span data-ttu-id="a5115-766">Quando uma consulta consome 16 ou mais slots, ela é executada com alta importância.</span><span class="sxs-lookup"><span data-stu-id="a5115-766">When a query consumes 16 or more slots, it runs as high importance.</span></span>

<span data-ttu-id="a5115-767">Olá, tabela a seguir mostra Olá mapeamentos de importância para cada grupo de carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="a5115-767">hello following table shows hello importance mappings for each workload group.</span></span>

### <a name="workload-group-mappings-tooconcurrency-slots-and-importance"></a><span data-ttu-id="a5115-768">Importância e slots de tooconcurrency de mapeamentos de grupo de carga de trabalho</span><span class="sxs-lookup"><span data-stu-id="a5115-768">Workload group mappings tooconcurrency slots and importance</span></span>
| <span data-ttu-id="a5115-769">Grupos de carga de trabalho</span><span class="sxs-lookup"><span data-stu-id="a5115-769">Workload groups</span></span> | <span data-ttu-id="a5115-770">Mapeamento do slot de simultaneidade</span><span class="sxs-lookup"><span data-stu-id="a5115-770">Concurrency slot mapping</span></span> | <span data-ttu-id="a5115-771">MB / Distribuição</span><span class="sxs-lookup"><span data-stu-id="a5115-771">MB / Distribution</span></span> | <span data-ttu-id="a5115-772">Mapeamento de importância</span><span class="sxs-lookup"><span data-stu-id="a5115-772">Importance mapping</span></span> |
|:--- |:---:|:---:|:--- |
| <span data-ttu-id="a5115-773">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="a5115-773">SloDWGroupC00</span></span> |<span data-ttu-id="a5115-774">1</span><span class="sxs-lookup"><span data-stu-id="a5115-774">1</span></span> |<span data-ttu-id="a5115-775">100</span><span class="sxs-lookup"><span data-stu-id="a5115-775">100</span></span> |<span data-ttu-id="a5115-776">Média</span><span class="sxs-lookup"><span data-stu-id="a5115-776">Medium</span></span> |
| <span data-ttu-id="a5115-777">SloDWGroupC01</span><span class="sxs-lookup"><span data-stu-id="a5115-777">SloDWGroupC01</span></span> |<span data-ttu-id="a5115-778">2</span><span class="sxs-lookup"><span data-stu-id="a5115-778">2</span></span> |<span data-ttu-id="a5115-779">200</span><span class="sxs-lookup"><span data-stu-id="a5115-779">200</span></span> |<span data-ttu-id="a5115-780">Média</span><span class="sxs-lookup"><span data-stu-id="a5115-780">Medium</span></span> |
| <span data-ttu-id="a5115-781">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="a5115-781">SloDWGroupC02</span></span> |<span data-ttu-id="a5115-782">4</span><span class="sxs-lookup"><span data-stu-id="a5115-782">4</span></span> |<span data-ttu-id="a5115-783">400</span><span class="sxs-lookup"><span data-stu-id="a5115-783">400</span></span> |<span data-ttu-id="a5115-784">Média</span><span class="sxs-lookup"><span data-stu-id="a5115-784">Medium</span></span> |
| <span data-ttu-id="a5115-785">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="a5115-785">SloDWGroupC03</span></span> |<span data-ttu-id="a5115-786">8</span><span class="sxs-lookup"><span data-stu-id="a5115-786">8</span></span> |<span data-ttu-id="a5115-787">800</span><span class="sxs-lookup"><span data-stu-id="a5115-787">800</span></span> |<span data-ttu-id="a5115-788">Média</span><span class="sxs-lookup"><span data-stu-id="a5115-788">Medium</span></span> |
| <span data-ttu-id="a5115-789">SloDWGroupC04</span><span class="sxs-lookup"><span data-stu-id="a5115-789">SloDWGroupC04</span></span> |<span data-ttu-id="a5115-790">16</span><span class="sxs-lookup"><span data-stu-id="a5115-790">16</span></span> |<span data-ttu-id="a5115-791">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-791">1,600</span></span> |<span data-ttu-id="a5115-792">Alto</span><span class="sxs-lookup"><span data-stu-id="a5115-792">High</span></span> |
| <span data-ttu-id="a5115-793">SloDWGroupC05</span><span class="sxs-lookup"><span data-stu-id="a5115-793">SloDWGroupC05</span></span> |<span data-ttu-id="a5115-794">32</span><span class="sxs-lookup"><span data-stu-id="a5115-794">32</span></span> |<span data-ttu-id="a5115-795">3.200</span><span class="sxs-lookup"><span data-stu-id="a5115-795">3,200</span></span> |<span data-ttu-id="a5115-796">Alto</span><span class="sxs-lookup"><span data-stu-id="a5115-796">High</span></span> |
| <span data-ttu-id="a5115-797">SloDWGroupC06</span><span class="sxs-lookup"><span data-stu-id="a5115-797">SloDWGroupC06</span></span> |<span data-ttu-id="a5115-798">64</span><span class="sxs-lookup"><span data-stu-id="a5115-798">64</span></span> |<span data-ttu-id="a5115-799">6.400</span><span class="sxs-lookup"><span data-stu-id="a5115-799">6,400</span></span> |<span data-ttu-id="a5115-800">Alto</span><span class="sxs-lookup"><span data-stu-id="a5115-800">High</span></span> |
| <span data-ttu-id="a5115-801">SloDWGroupC07</span><span class="sxs-lookup"><span data-stu-id="a5115-801">SloDWGroupC07</span></span> |<span data-ttu-id="a5115-802">128</span><span class="sxs-lookup"><span data-stu-id="a5115-802">128</span></span> |<span data-ttu-id="a5115-803">12.800</span><span class="sxs-lookup"><span data-stu-id="a5115-803">12,800</span></span> |<span data-ttu-id="a5115-804">Alto</span><span class="sxs-lookup"><span data-stu-id="a5115-804">High</span></span> |

<span data-ttu-id="a5115-805">De saudação **alocação e o consumo de slots de simultaneidade** gráfico, você pode ver que uma DW500 usa 1, 4, 8 ou slots de simultaneidade 16 para smallrc, mediumrc, largerc e xlargerc, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="a5115-805">From hello **Allocation and consumption of concurrency slots** chart, you can see that a DW500 uses 1, 4, 8 or 16 concurrency slots for smallrc, mediumrc, largerc, and xlargerc, respectively.</span></span> <span data-ttu-id="a5115-806">Você pode procurar esses valores em Olá anterior a importância de saudação toofind gráfico para cada classe de recurso.</span><span class="sxs-lookup"><span data-stu-id="a5115-806">You can look those values up in hello preceding chart toofind hello importance for each resource class.</span></span>

### <a name="dw500-mapping-of-resource-classes-tooimportance"></a><span data-ttu-id="a5115-807">Mapeamento de DW500 de tooimportance de classes de recursos</span><span class="sxs-lookup"><span data-stu-id="a5115-807">DW500 mapping of resource classes tooimportance</span></span>
| <span data-ttu-id="a5115-808">classe de recurso</span><span class="sxs-lookup"><span data-stu-id="a5115-808">Resource class</span></span> | <span data-ttu-id="a5115-809">Grupo de carga de trabalho</span><span class="sxs-lookup"><span data-stu-id="a5115-809">Workload group</span></span> | <span data-ttu-id="a5115-810">Slots de simultaneidade usados</span><span class="sxs-lookup"><span data-stu-id="a5115-810">Concurrency slots used</span></span> | <span data-ttu-id="a5115-811">MB / Distribuição</span><span class="sxs-lookup"><span data-stu-id="a5115-811">MB / Distribution</span></span> | <span data-ttu-id="a5115-812">importância</span><span class="sxs-lookup"><span data-stu-id="a5115-812">Importance</span></span> |
|:--- |:--- |:---:|:---:|:--- |
| <span data-ttu-id="a5115-813">smallrc</span><span class="sxs-lookup"><span data-stu-id="a5115-813">smallrc</span></span> |<span data-ttu-id="a5115-814">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="a5115-814">SloDWGroupC00</span></span> |<span data-ttu-id="a5115-815">1</span><span class="sxs-lookup"><span data-stu-id="a5115-815">1</span></span> |<span data-ttu-id="a5115-816">100</span><span class="sxs-lookup"><span data-stu-id="a5115-816">100</span></span> |<span data-ttu-id="a5115-817">Média</span><span class="sxs-lookup"><span data-stu-id="a5115-817">Medium</span></span> |
| <span data-ttu-id="a5115-818">mediumrc</span><span class="sxs-lookup"><span data-stu-id="a5115-818">mediumrc</span></span> |<span data-ttu-id="a5115-819">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="a5115-819">SloDWGroupC02</span></span> |<span data-ttu-id="a5115-820">4</span><span class="sxs-lookup"><span data-stu-id="a5115-820">4</span></span> |<span data-ttu-id="a5115-821">400</span><span class="sxs-lookup"><span data-stu-id="a5115-821">400</span></span> |<span data-ttu-id="a5115-822">Média</span><span class="sxs-lookup"><span data-stu-id="a5115-822">Medium</span></span> |
| <span data-ttu-id="a5115-823">largerc</span><span class="sxs-lookup"><span data-stu-id="a5115-823">largerc</span></span> |<span data-ttu-id="a5115-824">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="a5115-824">SloDWGroupC03</span></span> |<span data-ttu-id="a5115-825">8</span><span class="sxs-lookup"><span data-stu-id="a5115-825">8</span></span> |<span data-ttu-id="a5115-826">800</span><span class="sxs-lookup"><span data-stu-id="a5115-826">800</span></span> |<span data-ttu-id="a5115-827">Média</span><span class="sxs-lookup"><span data-stu-id="a5115-827">Medium</span></span> |
| <span data-ttu-id="a5115-828">xlargerc</span><span class="sxs-lookup"><span data-stu-id="a5115-828">xlargerc</span></span> |<span data-ttu-id="a5115-829">SloDWGroupC04</span><span class="sxs-lookup"><span data-stu-id="a5115-829">SloDWGroupC04</span></span> |<span data-ttu-id="a5115-830">16</span><span class="sxs-lookup"><span data-stu-id="a5115-830">16</span></span> |<span data-ttu-id="a5115-831">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-831">1,600</span></span> |<span data-ttu-id="a5115-832">Alto</span><span class="sxs-lookup"><span data-stu-id="a5115-832">High</span></span> |
| <span data-ttu-id="a5115-833">staticrc10</span><span class="sxs-lookup"><span data-stu-id="a5115-833">staticrc10</span></span> |<span data-ttu-id="a5115-834">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="a5115-834">SloDWGroupC00</span></span> |<span data-ttu-id="a5115-835">1</span><span class="sxs-lookup"><span data-stu-id="a5115-835">1</span></span> |<span data-ttu-id="a5115-836">100</span><span class="sxs-lookup"><span data-stu-id="a5115-836">100</span></span> |<span data-ttu-id="a5115-837">Média</span><span class="sxs-lookup"><span data-stu-id="a5115-837">Medium</span></span> |
| <span data-ttu-id="a5115-838">staticrc20</span><span class="sxs-lookup"><span data-stu-id="a5115-838">staticrc20</span></span> |<span data-ttu-id="a5115-839">SloDWGroupC01</span><span class="sxs-lookup"><span data-stu-id="a5115-839">SloDWGroupC01</span></span> |<span data-ttu-id="a5115-840">2</span><span class="sxs-lookup"><span data-stu-id="a5115-840">2</span></span> |<span data-ttu-id="a5115-841">200</span><span class="sxs-lookup"><span data-stu-id="a5115-841">200</span></span> |<span data-ttu-id="a5115-842">Média</span><span class="sxs-lookup"><span data-stu-id="a5115-842">Medium</span></span> |
| <span data-ttu-id="a5115-843">staticrc30</span><span class="sxs-lookup"><span data-stu-id="a5115-843">staticrc30</span></span> |<span data-ttu-id="a5115-844">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="a5115-844">SloDWGroupC02</span></span> |<span data-ttu-id="a5115-845">4</span><span class="sxs-lookup"><span data-stu-id="a5115-845">4</span></span> |<span data-ttu-id="a5115-846">400</span><span class="sxs-lookup"><span data-stu-id="a5115-846">400</span></span> |<span data-ttu-id="a5115-847">Média</span><span class="sxs-lookup"><span data-stu-id="a5115-847">Medium</span></span> |
| <span data-ttu-id="a5115-848">staticrc40</span><span class="sxs-lookup"><span data-stu-id="a5115-848">staticrc40</span></span> |<span data-ttu-id="a5115-849">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="a5115-849">SloDWGroupC03</span></span> |<span data-ttu-id="a5115-850">8</span><span class="sxs-lookup"><span data-stu-id="a5115-850">8</span></span> |<span data-ttu-id="a5115-851">800</span><span class="sxs-lookup"><span data-stu-id="a5115-851">800</span></span> |<span data-ttu-id="a5115-852">Média</span><span class="sxs-lookup"><span data-stu-id="a5115-852">Medium</span></span> |
| <span data-ttu-id="a5115-853">staticrc50</span><span class="sxs-lookup"><span data-stu-id="a5115-853">staticrc50</span></span> |<span data-ttu-id="a5115-854">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="a5115-854">SloDWGroupC03</span></span> |<span data-ttu-id="a5115-855">16</span><span class="sxs-lookup"><span data-stu-id="a5115-855">16</span></span> |<span data-ttu-id="a5115-856">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-856">1,600</span></span> |<span data-ttu-id="a5115-857">Alto</span><span class="sxs-lookup"><span data-stu-id="a5115-857">High</span></span> |
| <span data-ttu-id="a5115-858">staticrc60</span><span class="sxs-lookup"><span data-stu-id="a5115-858">staticrc60</span></span> |<span data-ttu-id="a5115-859">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="a5115-859">SloDWGroupC03</span></span> |<span data-ttu-id="a5115-860">16</span><span class="sxs-lookup"><span data-stu-id="a5115-860">16</span></span> |<span data-ttu-id="a5115-861">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-861">1,600</span></span> |<span data-ttu-id="a5115-862">Alto</span><span class="sxs-lookup"><span data-stu-id="a5115-862">High</span></span> |
| <span data-ttu-id="a5115-863">staticrc70</span><span class="sxs-lookup"><span data-stu-id="a5115-863">staticrc70</span></span> |<span data-ttu-id="a5115-864">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="a5115-864">SloDWGroupC03</span></span> |<span data-ttu-id="a5115-865">16</span><span class="sxs-lookup"><span data-stu-id="a5115-865">16</span></span> |<span data-ttu-id="a5115-866">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-866">1,600</span></span> |<span data-ttu-id="a5115-867">Alto</span><span class="sxs-lookup"><span data-stu-id="a5115-867">High</span></span> |
| <span data-ttu-id="a5115-868">staticrc80</span><span class="sxs-lookup"><span data-stu-id="a5115-868">staticrc80</span></span> |<span data-ttu-id="a5115-869">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="a5115-869">SloDWGroupC03</span></span> |<span data-ttu-id="a5115-870">16</span><span class="sxs-lookup"><span data-stu-id="a5115-870">16</span></span> |<span data-ttu-id="a5115-871">1.600</span><span class="sxs-lookup"><span data-stu-id="a5115-871">1,600</span></span> |<span data-ttu-id="a5115-872">Alto</span><span class="sxs-lookup"><span data-stu-id="a5115-872">High</span></span> |

<span data-ttu-id="a5115-873">Você pode usar o hello toolook de consulta DMV em diferenças Olá na alocação de recursos de memória em detalhes da perspectiva de saudação do administrador de recursos de saudação ou tooanalyze ativo e históricos o uso de grupos de cargas de trabalho Olá a seguir ao solucionar o problema.</span><span class="sxs-lookup"><span data-stu-id="a5115-873">You can use hello following DMV query toolook at hello differences in memory resource allocation in detail from hello perspective of hello resource governor, or tooanalyze active and historic usage of hello workload groups when troubleshooting.</span></span>

```sql
WITH rg
AS
(   SELECT  
     pn.name                        AS node_name
    ,pn.[type]                        AS node_type
    ,pn.pdw_node_id                    AS node_id
    ,rp.name                        AS pool_name
    ,rp.max_memory_kb*1.0/1024                AS pool_max_mem_MB
    ,wg.name                        AS group_name
    ,wg.importance                    AS group_importance
    ,wg.request_max_memory_grant_percent        AS group_request_max_memory_grant_pcnt
    ,wg.max_dop                        AS group_max_dop
    ,wg.effective_max_dop                AS group_effective_max_dop
    ,wg.total_request_count                AS group_total_request_count
    ,wg.total_queued_request_count            AS group_total_queued_request_count
    ,wg.active_request_count                AS group_active_request_count
    ,wg.queued_request_count                AS group_queued_request_count
    FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
    JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    
            ON  wg.pdw_node_id  = rp.pdw_node_id
            AND wg.pool_id      = rp.pool_id
    JOIN    sys.dm_pdw_nodes pn
            ON    wg.pdw_node_id    = pn.pdw_node_id
    WHERE   wg.name like 'SloDWGroup%'
        AND     rp.name = 'SloDWPool'
)
SELECT    pool_name
,        pool_max_mem_MB
,        group_name
,        group_importance
,        (pool_max_mem_MB/100)*group_request_max_memory_grant_pcnt AS max_memory_grant_MB
,        node_name
,        node_type
,       group_total_request_count
,       group_total_queued_request_count
,       group_active_request_count
,       group_queued_request_count
FROM    rg
ORDER BY
    node_name
,    group_request_max_memory_grant_pcnt
,    group_importance
;
```

## <a name="queries-that-honor-concurrency-limits"></a><span data-ttu-id="a5115-874">Consultas que respeitam os limites de simultaneidade</span><span class="sxs-lookup"><span data-stu-id="a5115-874">Queries that honor concurrency limits</span></span>
<span data-ttu-id="a5115-875">A maioria das consultas é governada pelas classes de recurso.</span><span class="sxs-lookup"><span data-stu-id="a5115-875">Most queries are governed by resource classes.</span></span> <span data-ttu-id="a5115-876">Essas consultas devem se ajustar dentro de consultas simultâneas hello e limites de slot de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="a5115-876">These queries must fit inside both hello concurrent query and concurrency slot thresholds.</span></span> <span data-ttu-id="a5115-877">Um usuário não pode escolher tooexclude uma consulta de modelo de slot Olá simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="a5115-877">A user cannot choose tooexclude a query from hello concurrency slot model.</span></span>

<span data-ttu-id="a5115-878">tooreiterate, hello instruções a seguir consideram classes de recursos:</span><span class="sxs-lookup"><span data-stu-id="a5115-878">tooreiterate, hello following statements honor resource classes:</span></span>

* <span data-ttu-id="a5115-879">INSERT-SELECT</span><span class="sxs-lookup"><span data-stu-id="a5115-879">INSERT-SELECT</span></span>
* <span data-ttu-id="a5115-880">UPDATE</span><span class="sxs-lookup"><span data-stu-id="a5115-880">UPDATE</span></span>
* <span data-ttu-id="a5115-881">EXCLUIR</span><span class="sxs-lookup"><span data-stu-id="a5115-881">DELETE</span></span>
* <span data-ttu-id="a5115-882">SELECT (ao consultar tabelas de usuário)</span><span class="sxs-lookup"><span data-stu-id="a5115-882">SELECT (when querying user tables)</span></span>
* <span data-ttu-id="a5115-883">ALTER INDEX REBUILD</span><span class="sxs-lookup"><span data-stu-id="a5115-883">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="a5115-884">ALTER INDEX REORGANIZE</span><span class="sxs-lookup"><span data-stu-id="a5115-884">ALTER INDEX REORGANIZE</span></span>
* <span data-ttu-id="a5115-885">ALTER TABLE REBUILD</span><span class="sxs-lookup"><span data-stu-id="a5115-885">ALTER TABLE REBUILD</span></span>
* <span data-ttu-id="a5115-886">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="a5115-886">CREATE INDEX</span></span>
* <span data-ttu-id="a5115-887">CREATE CLUSTERED COLUMNSTORE INDEX</span><span class="sxs-lookup"><span data-stu-id="a5115-887">CREATE CLUSTERED COLUMNSTORE INDEX</span></span>
* <span data-ttu-id="a5115-888">CREATE TABLE AS SELECT (CTAS)</span><span class="sxs-lookup"><span data-stu-id="a5115-888">CREATE TABLE AS SELECT (CTAS)</span></span>
* <span data-ttu-id="a5115-889">Carregamento de dados</span><span class="sxs-lookup"><span data-stu-id="a5115-889">Data loading</span></span>
* <span data-ttu-id="a5115-890">Operações de movimentação de dados realizadas por Olá serviço de movimentação de dados (DMS)</span><span class="sxs-lookup"><span data-stu-id="a5115-890">Data movement operations conducted by hello Data Movement Service (DMS)</span></span>

## <a name="query-exceptions-tooconcurrency-limits"></a><span data-ttu-id="a5115-891">Limites de tooconcurrency de exceções de consulta</span><span class="sxs-lookup"><span data-stu-id="a5115-891">Query exceptions tooconcurrency limits</span></span>
<span data-ttu-id="a5115-892">Algumas consultas não consideram recurso Olá classe toowhich Olá usuário é atribuído.</span><span class="sxs-lookup"><span data-stu-id="a5115-892">Some queries do not honor hello resource class toowhich hello user is assigned.</span></span> <span data-ttu-id="a5115-893">Esses limites de simultaneidade toohello exceções são feitas quando recursos de memória de saudação necessários para um determinado comando estão baixos, geralmente porque o comando Olá é uma operação de metadados.</span><span class="sxs-lookup"><span data-stu-id="a5115-893">These exceptions toohello concurrency limits are made when hello memory resources needed for a particular command are low, often because hello command is a metadata operation.</span></span> <span data-ttu-id="a5115-894">Olá objetivo essas exceções é tooavoid alocações de memória maior para consultas que nunca precisam delas.</span><span class="sxs-lookup"><span data-stu-id="a5115-894">hello goal of these exceptions is tooavoid larger memory allocations for queries that will never need them.</span></span> <span data-ttu-id="a5115-895">Nesses casos, o padrão de saudação classe do recurso pequeno (smallrc) é sempre usado, independentemente da classe de recurso real Olá atribuído toohello usuário.</span><span class="sxs-lookup"><span data-stu-id="a5115-895">In these cases, hello default small resource class (smallrc) is always used regardless of hello actual resource class assigned toohello user.</span></span> <span data-ttu-id="a5115-896">Por exemplo, `CREATE LOGIN` sempre será executado em smallrc.</span><span class="sxs-lookup"><span data-stu-id="a5115-896">For example, `CREATE LOGIN` will always run in smallrc.</span></span> <span data-ttu-id="a5115-897">Olá recursos necessários toofulfill essa operação são muito baixo, portanto, não faz consultas de saudação tooinclude sentido no modelo de slot de simultaneidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="a5115-897">hello resources required toofulfill this operation are very low, so it does not make sense tooinclude hello query in hello concurrency slot model.</span></span>  <span data-ttu-id="a5115-898">Essas consultas também não são limitadas por limite de simultaneidade de usuário Olá 32, um número ilimitado dessas consultas pode executar o limite de sessão toohello de 1.024 sessões.</span><span class="sxs-lookup"><span data-stu-id="a5115-898">These queries are also not limited by hello 32 user concurrency limit, an unlimited number of these queries can run up toohello session limit of 1,024 sessions.</span></span>

<span data-ttu-id="a5115-899">Olá instruções a seguir não consideram classes de recursos:</span><span class="sxs-lookup"><span data-stu-id="a5115-899">hello following statements do not honor resource classes:</span></span>

* <span data-ttu-id="a5115-900">CREATE ou DROP TABLE</span><span class="sxs-lookup"><span data-stu-id="a5115-900">CREATE or DROP TABLE</span></span>
* <span data-ttu-id="a5115-901">ALTER TABLE ... SWITCH, SPLIT ou MERGE PARTITION</span><span class="sxs-lookup"><span data-stu-id="a5115-901">ALTER TABLE ... SWITCH, SPLIT, or MERGE PARTITION</span></span>
* <span data-ttu-id="a5115-902">ALTER INDEX DISABLE</span><span class="sxs-lookup"><span data-stu-id="a5115-902">ALTER INDEX DISABLE</span></span>
* <span data-ttu-id="a5115-903">DROP INDEX</span><span class="sxs-lookup"><span data-stu-id="a5115-903">DROP INDEX</span></span>
* <span data-ttu-id="a5115-904">CREATE, UPDATE ou DROP STATISTICS</span><span class="sxs-lookup"><span data-stu-id="a5115-904">CREATE, UPDATE, or DROP STATISTICS</span></span>
* <span data-ttu-id="a5115-905">TRUNCATE TABLE</span><span class="sxs-lookup"><span data-stu-id="a5115-905">TRUNCATE TABLE</span></span>
* <span data-ttu-id="a5115-906">ALTER AUTHORIZATION</span><span class="sxs-lookup"><span data-stu-id="a5115-906">ALTER AUTHORIZATION</span></span>
* <span data-ttu-id="a5115-907">CREATE LOGIN</span><span class="sxs-lookup"><span data-stu-id="a5115-907">CREATE LOGIN</span></span>
* <span data-ttu-id="a5115-908">CREATE, ALTER ou DROP USER</span><span class="sxs-lookup"><span data-stu-id="a5115-908">CREATE, ALTER or DROP USER</span></span>
* <span data-ttu-id="a5115-909">CREATE, ALTER ou DROP PROCEDURE</span><span class="sxs-lookup"><span data-stu-id="a5115-909">CREATE, ALTER or DROP PROCEDURE</span></span>
* <span data-ttu-id="a5115-910">CREATE ou DROP VIEW</span><span class="sxs-lookup"><span data-stu-id="a5115-910">CREATE or DROP VIEW</span></span>
* <span data-ttu-id="a5115-911">INSERT VALUES</span><span class="sxs-lookup"><span data-stu-id="a5115-911">INSERT VALUES</span></span>
* <span data-ttu-id="a5115-912">SELECT de exibições do sistema e DMVs</span><span class="sxs-lookup"><span data-stu-id="a5115-912">SELECT from system views and DMVs</span></span>
* <span data-ttu-id="a5115-913">EXPLAIN</span><span class="sxs-lookup"><span data-stu-id="a5115-913">EXPLAIN</span></span>
* <span data-ttu-id="a5115-914">DBCC</span><span class="sxs-lookup"><span data-stu-id="a5115-914">DBCC</span></span>

<!--
Removed as these two are not confirmed / supported under SQLDW
- CREATE REMOTE TABLE AS SELECT
- CREATE EXTERNAL TABLE AS SELECT
- REDISTRIBUTE
-->

##  <span data-ttu-id="a5115-915"><a name="changing-user-resource-class-example"></a> Alterar um exemplo de classe de recursos de usuário</span><span class="sxs-lookup"><span data-stu-id="a5115-915"><a name="changing-user-resource-class-example"></a> Change a user resource class example</span></span>
1. <span data-ttu-id="a5115-916">**Criar logon:** abrir uma conexão tooyour **mestre** banco de dados SQL server Olá que hospeda seu banco de dados do SQL Data Warehouse e executar Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="a5115-916">**Create login:** Open a connection tooyour **master** database on hello SQL server hosting your SQL Data Warehouse database and execute hello following commands.</span></span>
   
    ```sql
    CREATE LOGIN newperson WITH PASSWORD = 'mypassword';
    CREATE USER newperson for LOGIN newperson;
    ```
   
   > [!NOTE]
   > <span data-ttu-id="a5115-917">É uma boa ideia toocreate um usuário no banco de dados mestre para usuários do Azure SQL Data Warehouse hello.</span><span class="sxs-lookup"><span data-stu-id="a5115-917">It is a good idea toocreate a user in hello master database for Azure SQL Data Warehouse users.</span></span> <span data-ttu-id="a5115-918">Criando um usuário em mestre permite que um toologin de usuário usando ferramentas como o SSMS sem especificar um nome de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a5115-918">Creating a user in master allows a user toologin using tools like SSMS without specifying a database name.</span></span>  <span data-ttu-id="a5115-919">Ele também permite que toouse Olá objeto explorer tooview todos os bancos de dados em um SQL server.</span><span class="sxs-lookup"><span data-stu-id="a5115-919">It also allows them toouse hello object explorer tooview all databases on a SQL server.</span></span>  <span data-ttu-id="a5115-920">Para obter mais detalhes sobre como criar e gerenciar usuários, consulte [Proteger um banco de dados no SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="a5115-920">For more details about creating and managing users, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>
   > 
   > 
2. <span data-ttu-id="a5115-921">**Criar usuário do SQL Data Warehouse:** abrir uma conexão toohello **SQL Data Warehouse** banco de dados e executar Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="a5115-921">**Create SQL Data Warehouse user:** Open a connection toohello **SQL Data Warehouse** database and execute hello following command.</span></span>
   
    ```sql
    CREATE USER newperson FOR LOGIN newperson;
    ```
3. <span data-ttu-id="a5115-922">**Conceder permissões:** Olá seguinte exemplo concede `CONTROL` em Olá **SQL Data Warehouse** banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a5115-922">**Grant permissions:** hello following example grants `CONTROL` on hello **SQL Data Warehouse** database.</span></span> <span data-ttu-id="a5115-923">`CONTROL`em Olá nível de banco de dados é Olá equivalente de db_owner no SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a5115-923">`CONTROL` at hello database level is hello equivalent of db_owner in SQL Server.</span></span>
   
    ```sql
    GRANT CONTROL ON DATABASE::MySQLDW toonewperson;
    ```
4. <span data-ttu-id="a5115-924">**Aumentar a classe de recurso:** tooadd de consulta a seguir de saudação Use uma função de gerenciamento de carga de trabalho mais alto do usuário tooa.</span><span class="sxs-lookup"><span data-stu-id="a5115-924">**Increase resource class:** Use hello following query tooadd a user tooa higher workload management role.</span></span>
   
    ```sql
    EXEC sp_addrolemember 'largerc', 'newperson'
    ```
5. <span data-ttu-id="a5115-925">**Diminuir a classe de recurso:** consulta a seguir do uso Olá tooremove um usuário de uma função de gerenciamento de carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="a5115-925">**Decrease resource class:** Use hello following query tooremove a user from a workload management role.</span></span>
   
    ```sql
    EXEC sp_droprolemember 'largerc', 'newperson';
    ```
   
   > [!NOTE]
   > <span data-ttu-id="a5115-926">Não é possível tooremove de smallrc um usuário.</span><span class="sxs-lookup"><span data-stu-id="a5115-926">It is not possible tooremove a user from smallrc.</span></span>
   > 
   > 

## <a name="queued-query-detection-and-other-dmvs"></a><span data-ttu-id="a5115-927">Detecção de consulta enfileirada e outros DMVs</span><span class="sxs-lookup"><span data-stu-id="a5115-927">Queued query detection and other DMVs</span></span>
<span data-ttu-id="a5115-928">Você pode usar o hello `sys.dm_pdw_exec_requests` as consultas DMV tooidentify que estão aguardando na fila de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="a5115-928">You can use hello `sys.dm_pdw_exec_requests` DMV tooidentify queries that are waiting in a concurrency queue.</span></span> <span data-ttu-id="a5115-929">As consultas que estão aguardando um slot de simultaneidade terão um status de **suspensas**.</span><span class="sxs-lookup"><span data-stu-id="a5115-929">Queries waiting for a concurrency slot will have a status of **suspended**.</span></span>

```sql
SELECT      r.[request_id]                 AS Request_ID
        ,r.[status]                 AS Request_Status
        ,r.[submit_time]             AS Request_SubmitTime
        ,r.[start_time]                 AS Request_StartTime
        ,DATEDIFF(ms,[submit_time],[start_time]) AS Request_InitiateDuration_ms
        ,r.resource_class                         AS Request_resource_class
FROM    sys.dm_pdw_exec_requests r;
```

<span data-ttu-id="a5115-930">As funções de gerenciamento de carga de trabalho podem ser exibidas com `sys.database_principals`.</span><span class="sxs-lookup"><span data-stu-id="a5115-930">Workload management roles can be viewed with `sys.database_principals`.</span></span>

```sql
SELECT  ro.[name]           AS [db_role_name]
FROM    sys.database_principals ro
WHERE   ro.[type_desc]      = 'DATABASE_ROLE'
AND     ro.[is_fixed_role]  = 0;
```

<span data-ttu-id="a5115-931">saudação de consulta a seguir mostra qual função de cada usuário é atribuído.</span><span class="sxs-lookup"><span data-stu-id="a5115-931">hello following query shows which role each user is assigned to.</span></span>

```sql
SELECT     r.name AS role_principal_name
        ,m.name AS member_principal_name
FROM    sys.database_role_members rm
JOIN    sys.database_principals AS r            ON rm.role_principal_id        = r.principal_id
JOIN    sys.database_principals AS m            ON rm.member_principal_id    = m.principal_id
WHERE    r.name IN ('mediumrc','largerc', 'xlargerc');
```

<span data-ttu-id="a5115-932">SQL Data Warehouse tem Olá seguintes tipos de espera:</span><span class="sxs-lookup"><span data-stu-id="a5115-932">SQL Data Warehouse has hello following wait types:</span></span>

* <span data-ttu-id="a5115-933">**LocalQueriesConcurrencyResourceType**: consultas que ficam fora do framework de slot de simultaneidade hello.</span><span class="sxs-lookup"><span data-stu-id="a5115-933">**LocalQueriesConcurrencyResourceType**: Queries that sit outside of hello concurrency slot framework.</span></span> <span data-ttu-id="a5115-934">Consultas DMV e funções de sistema, como `SELECT @@VERSION` , são exemplos de consultas de locais.</span><span class="sxs-lookup"><span data-stu-id="a5115-934">DMV queries and system functions such as `SELECT @@VERSION` are examples of local queries.</span></span>
* <span data-ttu-id="a5115-935">**UserConcurrencyResourceType**: consultas que ficam dentro do framework de slot de simultaneidade hello.</span><span class="sxs-lookup"><span data-stu-id="a5115-935">**UserConcurrencyResourceType**: Queries that sit inside hello concurrency slot framework.</span></span> <span data-ttu-id="a5115-936">Consultas em tabelas do usuário final representam exemplos que usariam esse tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="a5115-936">Queries against end-user tables represent examples that would use this resource type.</span></span>
* <span data-ttu-id="a5115-937">**DmsConcurrencyResourceType**: esperas resultantes de operações de movimentação de dados.</span><span class="sxs-lookup"><span data-stu-id="a5115-937">**DmsConcurrencyResourceType**: Waits resulting from data movement operations.</span></span>
* <span data-ttu-id="a5115-938">**BackupConcurrencyResourceType**: essa espera indica que está sendo feito backup de um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a5115-938">**BackupConcurrencyResourceType**: This wait indicates that a database is being backed up.</span></span> <span data-ttu-id="a5115-939">saudação de valor máximo para esse tipo de recurso é 1.</span><span class="sxs-lookup"><span data-stu-id="a5115-939">hello maximum value for this resource type is 1.</span></span> <span data-ttu-id="a5115-940">Se vários backups foram solicitados em Olá simultaneamente, Olá outros colocará em fila.</span><span class="sxs-lookup"><span data-stu-id="a5115-940">If multiple backups have been requested at hello same time, hello others will queue.</span></span>

<span data-ttu-id="a5115-941">Olá `sys.dm_pdw_waits` DMV pode ser usado toosee os recursos que uma solicitação está aguardando.</span><span class="sxs-lookup"><span data-stu-id="a5115-941">hello `sys.dm_pdw_waits` DMV can be used toosee which resources a request is waiting for.</span></span>

```sql
SELECT  w.[wait_id]
,       w.[session_id]
,       w.[type]            AS Wait_type
,       w.[object_type]
,       w.[object_name]
,       w.[request_id]
,       w.[request_time]
,       w.[acquire_time]
,       w.[state]
,       w.[priority]
,    SESSION_ID()            AS Current_session
,    s.[status]            AS Session_status
,    s.[login_name]
,    s.[query_count]
,    s.[client_id]
,    s.[sql_spid]
,    r.[command]            AS Request_command
,    r.[label]
,    r.[status]            AS Request_status
,    r.[submit_time]
,    r.[start_time]
,    r.[end_compile_time]
,    r.[end_time]
,    DATEDIFF(ms,r.[submit_time],r.[start_time])        AS Request_queue_time_ms
,    DATEDIFF(ms,r.[start_time],r.[end_compile_time])    AS Request_compile_time_ms
,    DATEDIFF(ms,r.[end_compile_time],r.[end_time])        AS Request_execution_time_ms
,    r.[total_elapsed_time]
FROM    sys.dm_pdw_waits w
JOIN    sys.dm_pdw_exec_sessions s  ON w.[session_id] = s.[session_id]
JOIN    sys.dm_pdw_exec_requests r  ON w.[request_id] = r.[request_id]
WHERE    w.[session_id] <> SESSION_ID();
```

<span data-ttu-id="a5115-942">Olá `sys.dm_pdw_resource_waits` DMV mostra apenas Olá esperas de recurso consumidas por uma determinada consulta.</span><span class="sxs-lookup"><span data-stu-id="a5115-942">hello `sys.dm_pdw_resource_waits` DMV shows only hello resource waits consumed by a given query.</span></span> <span data-ttu-id="a5115-943">Tempo de espera de recursos só mede o tempo de saudação aguardando toobe de recursos fornecido, conforme toosignal contrário aguardar o tempo, o que é o tempo de saudação que leva para Olá base SQL servidores tooschedule Olá consulta para CPU hello.</span><span class="sxs-lookup"><span data-stu-id="a5115-943">Resource wait time only measures hello time waiting for resources toobe provided, as opposed toosignal wait time, which is hello time it takes for hello underlying SQL servers tooschedule hello query onto hello CPU.</span></span>

```sql
SELECT  [session_id]
,       [type]
,       [object_type]
,       [object_name]
,       [request_id]
,       [request_time]
,       [acquire_time]
,       DATEDIFF(ms,[request_time],[acquire_time])  AS acquire_duration_ms
,       [concurrency_slots_used]                    AS concurrency_slots_reserved
,       [resource_class]
,       [wait_id]                                   AS queue_position
FROM    sys.dm_pdw_resource_waits
WHERE    [session_id] <> SESSION_ID();
```

<span data-ttu-id="a5115-944">Olá `sys.dm_pdw_wait_stats` DMV pode ser usada para análise de tendências históricas de esperas.</span><span class="sxs-lookup"><span data-stu-id="a5115-944">hello `sys.dm_pdw_wait_stats` DMV can be used for historic trend analysis of waits.</span></span>

```sql
SELECT    w.[pdw_node_id]
,        w.[wait_name]
,        w.[max_wait_time]
,        w.[request_count]
,        w.[signal_time]
,        w.[completed_count]
,        w.[wait_time]
FROM    sys.dm_pdw_wait_stats w;
```

## <a name="next-steps"></a><span data-ttu-id="a5115-945">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a5115-945">Next steps</span></span>
<span data-ttu-id="a5115-946">Para obter mais informações sobre como gerenciar usuários de banco de dados e segurança, confira [Proteger um banco de dados no SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="a5115-946">For more information about managing database users and security, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span> <span data-ttu-id="a5115-947">Para obter mais informações sobre classes de recursos como maiores podem melhorar a qualidade do índice columnstore clusterizado, consulte [recriação de qualidade de segmento tooimprove índices].</span><span class="sxs-lookup"><span data-stu-id="a5115-947">For more information about how larger resource classes can improve clustered columnstore index quality, see [Rebuilding indexes tooimprove segment quality].</span></span>

<!--Image references-->

<!--Article references-->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[recriação de qualidade de segmento tooimprove índices]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md

<!--MSDN references-->
[Managing Databases and Logins in Azure SQL Database]:https://msdn.microsoft.com/library/azure/ee336235.aspx

<!--Other Web references-->
