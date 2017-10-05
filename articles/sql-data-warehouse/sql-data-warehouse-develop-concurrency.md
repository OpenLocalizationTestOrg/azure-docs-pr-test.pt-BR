---
title: Gerenciamento de simultaneidade e carga de trabalho no SQL Data Warehouse | Microsoft Docs
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
ms.openlocfilehash: eaf2d43286dbaa52ada1430fbb7ce1e37f41c0d4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="concurrency-and-workload-management-in-sql-data-warehouse"></a><span data-ttu-id="a8730-103">Gerenciamento de simultaneidade e carga de trabalho no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a8730-103">Concurrency and workload management in SQL Data Warehouse</span></span>
<span data-ttu-id="a8730-104">Para oferecer um desempenho previsível em escala, o SQL Data Warehouse do Microsoft Azure ajuda a controlar os níveis de simultaneidade e as alocações de recursos como priorização de CPU e memória.</span><span class="sxs-lookup"><span data-stu-id="a8730-104">To deliver predictable performance at scale, Microsoft Azure SQL Data Warehouse helps you control concurrency levels and resource allocations like memory and CPU prioritization.</span></span> <span data-ttu-id="a8730-105">Este artigo apresenta os conceitos de gerenciamento de simultaneidade e carga de trabalho, explicando como os dois recursos foram implementados e como controlá-los no data warehouse.</span><span class="sxs-lookup"><span data-stu-id="a8730-105">This article introduces you to the concepts of concurrency and workload management, explaining how both features have been implemented and how you can control them in your data warehouse.</span></span> <span data-ttu-id="a8730-106">O gerenciamento de carga de trabalho do SQL Data Warehouse destina-se a ajudá-lo a dar suporte a ambientes com vários usuários.</span><span class="sxs-lookup"><span data-stu-id="a8730-106">SQL Data Warehouse workload management is intended to help you support multi-user environments.</span></span> <span data-ttu-id="a8730-107">Ele não se destina a cargas de trabalho com vários locatários.</span><span class="sxs-lookup"><span data-stu-id="a8730-107">It is not intended for multi-tenant workloads.</span></span>

## <a name="concurrency-limits"></a><span data-ttu-id="a8730-108">Limites de simultaneidade</span><span class="sxs-lookup"><span data-stu-id="a8730-108">Concurrency limits</span></span>
<span data-ttu-id="a8730-109">O SQL Data Warehouse permite até 1.024 conexões simultâneas.</span><span class="sxs-lookup"><span data-stu-id="a8730-109">SQL Data Warehouse allows up to 1,024 concurrent connections.</span></span> <span data-ttu-id="a8730-110">Todas as 1.024 conexões podem enviar consultas ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="a8730-110">All 1,024 connections can submit queries concurrently.</span></span> <span data-ttu-id="a8730-111">No entanto, para otimizar a taxa de transferência, o SQL Data Warehouse pode enfileirar algumas consultas para garantir que cada consulta receba uma concessão de memória mínima.</span><span class="sxs-lookup"><span data-stu-id="a8730-111">However, to optimize throughput, SQL Data Warehouse may queue some queries to ensure that each query receives a minimal memory grant.</span></span> <span data-ttu-id="a8730-112">O enfileiramento ocorre no tempo de execução de consulta.</span><span class="sxs-lookup"><span data-stu-id="a8730-112">Queuing occurs at query execution time.</span></span> <span data-ttu-id="a8730-113">Ao enfileirar consultas quando os limites de simultaneidade são atingidos, o SQL Data Warehouse pode aumentar a taxa de transferência total, garantindo que as consultas ativas obtenham acesso aos recursos de memória muito necessários.</span><span class="sxs-lookup"><span data-stu-id="a8730-113">By queuing queries when concurrency limits are reached, SQL Data Warehouse can increase total throughput by ensuring that active queries get access to critically needed memory resources.</span></span>  

<span data-ttu-id="a8730-114">Os limites de simultaneidade são regidos por dois conceitos: *consultas simultâneas* e *slots de simultaneidade*.</span><span class="sxs-lookup"><span data-stu-id="a8730-114">Concurrency limits are governed by two concepts: *concurrent queries* and *concurrency slots*.</span></span> <span data-ttu-id="a8730-115">Para a execução de uma consulta, ela deve ser executada tanto no limite de simultaneidade de consulta quanto na alocação de slot de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="a8730-115">For a query to execute, it must execute within both the query concurrency limit and the concurrency slot allocation.</span></span>

* <span data-ttu-id="a8730-116">As consultas simultâneas são as consultas em execução ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="a8730-116">Concurrent queries are the queries executing at the same time.</span></span> <span data-ttu-id="a8730-117">O SQL Data Warehouse dá suporte a até 32 consultas simultâneas em tamanhos maiores de DWU.</span><span class="sxs-lookup"><span data-stu-id="a8730-117">SQL Data Warehouse supports up to 32 concurrent queries on the larger DWU sizes.</span></span>
* <span data-ttu-id="a8730-118">Os slots de simultaneidade são alocados com base em DWU.</span><span class="sxs-lookup"><span data-stu-id="a8730-118">Concurrency slots are allocated based on DWU.</span></span> <span data-ttu-id="a8730-119">Cada DWU 100 fornece quatro slots de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="a8730-119">Each 100 DWU provides 4 concurrency slots.</span></span> <span data-ttu-id="a8730-120">Por exemplo, um DW100 aloca quatro slots de simultaneidade e um DW1000 aloca 40.</span><span class="sxs-lookup"><span data-stu-id="a8730-120">For example, a DW100 allocates 4 concurrency slots and DW1000 allocates 40.</span></span> <span data-ttu-id="a8730-121">Cada consulta consome um ou mais slots de simultaneidade, dependendo da [classe de recurso](#resource-classes) da consulta.</span><span class="sxs-lookup"><span data-stu-id="a8730-121">Each query consumes one or more concurrency slots, dependent on the [resource class](#resource-classes) of the query.</span></span> <span data-ttu-id="a8730-122">As consultas em execução na classe de recurso smallrc consomem um slot de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="a8730-122">Queries running in the smallrc resource class consume one concurrency slot.</span></span> <span data-ttu-id="a8730-123">As consultas em execução em uma classe de recurso superior consomem mais slots de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="a8730-123">Queries running in a higher resource class consume more concurrency slots.</span></span>

<span data-ttu-id="a8730-124">A tabela a seguir descreve os limites das consultas simultâneas e dos slots de simultaneidade em vários tamanhos de DWU.</span><span class="sxs-lookup"><span data-stu-id="a8730-124">The following table describes the limits for both concurrent queries and concurrency slots at the various DWU sizes.</span></span>

### <a name="concurrency-limits"></a><span data-ttu-id="a8730-125">Limites de simultaneidade</span><span class="sxs-lookup"><span data-stu-id="a8730-125">Concurrency limits</span></span>
| <span data-ttu-id="a8730-126">DWU</span><span class="sxs-lookup"><span data-stu-id="a8730-126">DWU</span></span> | <span data-ttu-id="a8730-127">Máximo de consultas simultâneas</span><span class="sxs-lookup"><span data-stu-id="a8730-127">Max concurrent queries</span></span> | <span data-ttu-id="a8730-128">Slots de simultaneidade alocados</span><span class="sxs-lookup"><span data-stu-id="a8730-128">Concurrency slots allocated</span></span> |
|:--- |:---:|:---:|
| <span data-ttu-id="a8730-129">DW100</span><span class="sxs-lookup"><span data-stu-id="a8730-129">DW100</span></span> |<span data-ttu-id="a8730-130">4</span><span class="sxs-lookup"><span data-stu-id="a8730-130">4</span></span> |<span data-ttu-id="a8730-131">4</span><span class="sxs-lookup"><span data-stu-id="a8730-131">4</span></span> |
| <span data-ttu-id="a8730-132">DW200</span><span class="sxs-lookup"><span data-stu-id="a8730-132">DW200</span></span> |<span data-ttu-id="a8730-133">8</span><span class="sxs-lookup"><span data-stu-id="a8730-133">8</span></span> |<span data-ttu-id="a8730-134">8</span><span class="sxs-lookup"><span data-stu-id="a8730-134">8</span></span> |
| <span data-ttu-id="a8730-135">DW300</span><span class="sxs-lookup"><span data-stu-id="a8730-135">DW300</span></span> |<span data-ttu-id="a8730-136">12</span><span class="sxs-lookup"><span data-stu-id="a8730-136">12</span></span> |<span data-ttu-id="a8730-137">12</span><span class="sxs-lookup"><span data-stu-id="a8730-137">12</span></span> |
| <span data-ttu-id="a8730-138">DW400</span><span class="sxs-lookup"><span data-stu-id="a8730-138">DW400</span></span> |<span data-ttu-id="a8730-139">16</span><span class="sxs-lookup"><span data-stu-id="a8730-139">16</span></span> |<span data-ttu-id="a8730-140">16</span><span class="sxs-lookup"><span data-stu-id="a8730-140">16</span></span> |
| <span data-ttu-id="a8730-141">DW500</span><span class="sxs-lookup"><span data-stu-id="a8730-141">DW500</span></span> |<span data-ttu-id="a8730-142">20</span><span class="sxs-lookup"><span data-stu-id="a8730-142">20</span></span> |<span data-ttu-id="a8730-143">20</span><span class="sxs-lookup"><span data-stu-id="a8730-143">20</span></span> |
| <span data-ttu-id="a8730-144">DW600</span><span class="sxs-lookup"><span data-stu-id="a8730-144">DW600</span></span> |<span data-ttu-id="a8730-145">24</span><span class="sxs-lookup"><span data-stu-id="a8730-145">24</span></span> |<span data-ttu-id="a8730-146">24</span><span class="sxs-lookup"><span data-stu-id="a8730-146">24</span></span> |
| <span data-ttu-id="a8730-147">DW1000</span><span class="sxs-lookup"><span data-stu-id="a8730-147">DW1000</span></span> |<span data-ttu-id="a8730-148">32</span><span class="sxs-lookup"><span data-stu-id="a8730-148">32</span></span> |<span data-ttu-id="a8730-149">40</span><span class="sxs-lookup"><span data-stu-id="a8730-149">40</span></span> |
| <span data-ttu-id="a8730-150">DW1200</span><span class="sxs-lookup"><span data-stu-id="a8730-150">DW1200</span></span> |<span data-ttu-id="a8730-151">32</span><span class="sxs-lookup"><span data-stu-id="a8730-151">32</span></span> |<span data-ttu-id="a8730-152">48</span><span class="sxs-lookup"><span data-stu-id="a8730-152">48</span></span> |
| <span data-ttu-id="a8730-153">DW1500</span><span class="sxs-lookup"><span data-stu-id="a8730-153">DW1500</span></span> |<span data-ttu-id="a8730-154">32</span><span class="sxs-lookup"><span data-stu-id="a8730-154">32</span></span> |<span data-ttu-id="a8730-155">60</span><span class="sxs-lookup"><span data-stu-id="a8730-155">60</span></span> |
| <span data-ttu-id="a8730-156">DW2000</span><span class="sxs-lookup"><span data-stu-id="a8730-156">DW2000</span></span> |<span data-ttu-id="a8730-157">32</span><span class="sxs-lookup"><span data-stu-id="a8730-157">32</span></span> |<span data-ttu-id="a8730-158">80</span><span class="sxs-lookup"><span data-stu-id="a8730-158">80</span></span> |
| <span data-ttu-id="a8730-159">DW3000</span><span class="sxs-lookup"><span data-stu-id="a8730-159">DW3000</span></span> |<span data-ttu-id="a8730-160">32</span><span class="sxs-lookup"><span data-stu-id="a8730-160">32</span></span> |<span data-ttu-id="a8730-161">120</span><span class="sxs-lookup"><span data-stu-id="a8730-161">120</span></span> |
| <span data-ttu-id="a8730-162">DW6000</span><span class="sxs-lookup"><span data-stu-id="a8730-162">DW6000</span></span> |<span data-ttu-id="a8730-163">32</span><span class="sxs-lookup"><span data-stu-id="a8730-163">32</span></span> |<span data-ttu-id="a8730-164">240</span><span class="sxs-lookup"><span data-stu-id="a8730-164">240</span></span> |

<span data-ttu-id="a8730-165">Quando um desses limites for atingido, novas consultas serão enfileiradas e executadas em uma base de primeira a entrar, primeira a sair.</span><span class="sxs-lookup"><span data-stu-id="a8730-165">When one of these thresholds is met, new queries are queued and executed on a first-in, first-out basis.</span></span>  <span data-ttu-id="a8730-166">Conforme uma consulta for concluída e o número de consultas e slots ficar abaixo dos limites, as consultas em fila serão lançadas.</span><span class="sxs-lookup"><span data-stu-id="a8730-166">As a queries finishes and the number of queries and slots falls below the limits, queued queries are released.</span></span> 

> [!NOTE]  
> <span data-ttu-id="a8730-167">*Select* em execução exclusivamente nas DMVs (exibições de gerenciamento dinâmico) ou nas exibições de catálogo não são regidas por nenhum dos limites de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="a8730-167">*Select* queries executing exclusively on dynamic management views (DMVs) or catalog views are not governed by any of the concurrency limits.</span></span> <span data-ttu-id="a8730-168">Você pode monitorar o sistema independentemente do número de consultas em execução nele.</span><span class="sxs-lookup"><span data-stu-id="a8730-168">You can monitor the system regardless of the number of queries executing on it.</span></span>
> 
> 

## <a name="resource-classes"></a><span data-ttu-id="a8730-169">Classes de recursos</span><span class="sxs-lookup"><span data-stu-id="a8730-169">Resource classes</span></span>
<span data-ttu-id="a8730-170">As classes de recurso ajudam a controlar a alocação de memória e os ciclos de CPU fornecidos para uma consulta.</span><span class="sxs-lookup"><span data-stu-id="a8730-170">Resource classes help you control memory allocation and CPU cycles given to a query.</span></span> <span data-ttu-id="a8730-171">Você pode atribuir dois tipos de classes de recurso para um usuário na forma de funções de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a8730-171">You can assign two types of resource classes to a user in the form of database roles.</span></span> <span data-ttu-id="a8730-172">Os dois tipos de classes de recurso são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="a8730-172">The two types of resource classes are as follows:</span></span>
1. <span data-ttu-id="a8730-173">Classes de recursos dinâmicos (**smallrc, mediumrc, largerc, xlargerc**) alocam uma quantidade variável de memória dependendo da DWU.</span><span class="sxs-lookup"><span data-stu-id="a8730-173">Dynamic Resource Classes (**smallrc, mediumrc, largerc, xlargerc**) allocate a variable amount of memory depending on the current DWU.</span></span> <span data-ttu-id="a8730-174">Isso significa que quando você escala verticalmente para uma maior DWU, as consultas automaticamente recebem mais memória.</span><span class="sxs-lookup"><span data-stu-id="a8730-174">This means that when you scale up to a larger DWU, your queries automatically get more memory.</span></span> 
2. <span data-ttu-id="a8730-175">Classes de recursos estáticos (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) alocam a mesma quantidade de memória, independentemente da DWU atual (desde que o DWU em si tenha memória suficiente).</span><span class="sxs-lookup"><span data-stu-id="a8730-175">Static Resource Classes (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) allocate the same amount of memory regardless of the current DWU (provided that the DWU itself has enough memory).</span></span> <span data-ttu-id="a8730-176">Isso significa que em DWUs maiores, você pode executar mais consultas em cada classe de recursos simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="a8730-176">This means that on larger DWUs, you can run more queries in each resource class concurrently.</span></span>

<span data-ttu-id="a8730-177">Os usuários em **smallrc** e **staticrc10** recebem uma quantidade menor de memória e podem tirar proveito da simultaneidade superior.</span><span class="sxs-lookup"><span data-stu-id="a8730-177">Users in **smallrc** and **staticrc10** are given a smaller amount of memory and can take advantage of higher concurrency.</span></span> <span data-ttu-id="a8730-178">Por outro lado, os usuários atribuídos a **xlargerc** ou **staticrc80** recebem grandes quantidades de memória e, assim, um número menor dessas consultas pode ser executado simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="a8730-178">In contrast, users assigned to **xlargerc** or **staticrc80** are given large amounts of memory, and therefore fewer of their queries can run concurrently.</span></span>

<span data-ttu-id="a8730-179">Por padrão, cada usuário é um membro da pequena classe de recursos, **smallrc**.</span><span class="sxs-lookup"><span data-stu-id="a8730-179">By default, each user is a member of the small resource class, **smallrc**.</span></span> <span data-ttu-id="a8730-180">O procedimento `sp_addrolemember` é usado para aumentar a classe de recurso e `sp_droprolemember` é usado para diminuir a classe de recurso.</span><span class="sxs-lookup"><span data-stu-id="a8730-180">The procedure `sp_addrolemember` is used to increase the resource class, and `sp_droprolemember` is used to decrease the resource class.</span></span> <span data-ttu-id="a8730-181">Por exemplo, este comando aumentaria a classe de recursos de loaduser para **largerc**:</span><span class="sxs-lookup"><span data-stu-id="a8730-181">For example, this command would increase the resource class of loaduser to **largerc**:</span></span>

```sql
EXEC sp_addrolemember 'largerc', 'loaduser'
```


### <a name="queries-that-do-not-honor-resource-classes"></a><span data-ttu-id="a8730-182">Consultas que não consideram classes de recursos</span><span class="sxs-lookup"><span data-stu-id="a8730-182">Queries that do not honor resource classes</span></span>

<span data-ttu-id="a8730-183">Existem alguns tipos de consultas que não se beneficiam de uma alocação de memória maior.</span><span class="sxs-lookup"><span data-stu-id="a8730-183">There are a few types of queries that do not benefit from a larger memory allocation.</span></span> <span data-ttu-id="a8730-184">O sistema ignora a alocação de classe de recurso e sempre executa essas consultas na classe de recurso pequena.</span><span class="sxs-lookup"><span data-stu-id="a8730-184">The system ignores their resource class allocation and always run these queries in the small resource class instead.</span></span> <span data-ttu-id="a8730-185">Se essas consultas são sempre executadas na classe de recurso pequena, elas podem ser executadas quando os slots de simultaneidade estão sob pressão e não consomem mais slots do que o necessário.</span><span class="sxs-lookup"><span data-stu-id="a8730-185">If these queries always run in the small resource class, they can run when concurrency slots are under pressure and they won't consume more slots than needed.</span></span> <span data-ttu-id="a8730-186">Consulte as [exceções de classe de recurso](#query-exceptions-to-concurrency-limits) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="a8730-186">See [Resource class exceptions](#query-exceptions-to-concurrency-limits) for more information.</span></span>

## <a name="details-on-resource-class-assignment"></a><span data-ttu-id="a8730-187">Detalhes sobre a atribuição de classe de recursos</span><span class="sxs-lookup"><span data-stu-id="a8730-187">Details on resource class assignment</span></span>


<span data-ttu-id="a8730-188">Mais alguns detalhes sobre classes de recurso:</span><span class="sxs-lookup"><span data-stu-id="a8730-188">A few more details on resource class:</span></span>

* <span data-ttu-id="a8730-189">*Alter role* é necessária para alterar a classe de recurso de um usuário.</span><span class="sxs-lookup"><span data-stu-id="a8730-189">*Alter role* permission is required to change the resource class of a user.</span></span>
* <span data-ttu-id="a8730-190">Embora seja possível adicionar um usuário a uma ou mais das classes de recursos mais altas, as classes de recursos dinâmicos têm prioridade sobre as classes de recursos estáticos.</span><span class="sxs-lookup"><span data-stu-id="a8730-190">Although you can add a user to one or more of the higher resource classes, dynamic resource classes take precedence over static resource classes.</span></span> <span data-ttu-id="a8730-191">Ou seja, se um usuário for atribuído a **mediumrc** (dinâmico) e **staticrc80** (estático), **mediumrc** é a classe de recursos que será respeitada.</span><span class="sxs-lookup"><span data-stu-id="a8730-191">That is, if a user is assigned to both **mediumrc**(dynamic) and **staticrc80**(static), **mediumrc** is the resource class that is honored.</span></span>
 * <span data-ttu-id="a8730-192">Quando um usuário é atribuído a mais de uma classe de recursos em um tipo de classe de recursos específico (mais de uma classe de recursos dinâmicos ou mais de uma classe de recursos estáticos), a classe de recursos mais alta é respeitada.</span><span class="sxs-lookup"><span data-stu-id="a8730-192">When a user is assigned to more than one resource class in a specific resource class type (more than one dynamic resource class or more than one static resource class), the highest resource class is honored.</span></span> <span data-ttu-id="a8730-193">Ou seja, se um usuário for atribuído a mediumrc e largerc, a classe de recurso mais elevada (largerc) será respeitada.</span><span class="sxs-lookup"><span data-stu-id="a8730-193">That is, if a user is assigned to both mediumrc and largerc, the higher resource class (largerc) is honored.</span></span> <span data-ttu-id="a8730-194">E se um usuário for atribuído a **staticrc20** e **statirc80**, **staticrc80** será respeitada.</span><span class="sxs-lookup"><span data-stu-id="a8730-194">And if a user is assigned to both **staticrc20** and **statirc80**, **staticrc80** is honored.</span></span>
* <span data-ttu-id="a8730-195">A classe de recurso do usuário administrativo do sistema não pode ser alterada.</span><span class="sxs-lookup"><span data-stu-id="a8730-195">The resource class of the system administrative user cannot be changed.</span></span>

<span data-ttu-id="a8730-196">Para obter um exemplo detalhado, consulte [Alterando o exemplo de classe de recurso de usuário](#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="a8730-196">For a detailed example, see [Changing user resource class example](#changing-user-resource-class-example).</span></span>

## <a name="memory-allocation"></a><span data-ttu-id="a8730-197">Alocação de memória</span><span class="sxs-lookup"><span data-stu-id="a8730-197">Memory allocation</span></span>
<span data-ttu-id="a8730-198">Há prós e contras quanto ao aumento da classe de recurso do usuário.</span><span class="sxs-lookup"><span data-stu-id="a8730-198">There are pros and cons to increasing a user's resource class.</span></span> <span data-ttu-id="a8730-199">O aumento de uma classe de recurso para um usuário concede às suas consultas acesso a mais memória, o que pode significar que as consultas serão executadas mais rapidamente.</span><span class="sxs-lookup"><span data-stu-id="a8730-199">Increasing a resource class for a user, gives their queries access to more memory, which may mean queries execute faster.</span></span>  <span data-ttu-id="a8730-200">No entanto, classes de recursos superiores também reduzem o número de consultas simultâneas que podem ser executadas.</span><span class="sxs-lookup"><span data-stu-id="a8730-200">However, higher resource classes also reduce the number of concurrent queries that can run.</span></span> <span data-ttu-id="a8730-201">Essa é a compensação entre alocar grandes quantidades de memória para uma única consulta ou permitir que outras consultas, que também precisam de alocações de memória, sejam executadas simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="a8730-201">This is the trade-off between allocating large amounts of memory to a single query or allowing other queries, which also need memory allocations, to run concurrently.</span></span> <span data-ttu-id="a8730-202">Se um usuário receber alocações de memória altas para uma consulta, outros usuários não terão acesso a essa mesma memória para executar uma consulta.</span><span class="sxs-lookup"><span data-stu-id="a8730-202">If one user is given high allocations of memory for a query, other users will not have access to that same memory to run a query.</span></span>

<span data-ttu-id="a8730-203">A tabela a seguir mapeia a memória alocada para cada distribuição por DWU e classe de recurso.</span><span class="sxs-lookup"><span data-stu-id="a8730-203">The following table maps the memory allocated to each distribution by DWU and resource class.</span></span>

### <a name="memory-allocations-per-distribution-for-dynamic-resource-classes-mb"></a><span data-ttu-id="a8730-204">Alocações de memória por distribuição de classes de recursos dinâmicos (MB)</span><span class="sxs-lookup"><span data-stu-id="a8730-204">Memory allocations per distribution for dynamic resource classes (MB)</span></span>
| <span data-ttu-id="a8730-205">DWU</span><span class="sxs-lookup"><span data-stu-id="a8730-205">DWU</span></span> | <span data-ttu-id="a8730-206">smallrc</span><span class="sxs-lookup"><span data-stu-id="a8730-206">smallrc</span></span> | <span data-ttu-id="a8730-207">mediumrc</span><span class="sxs-lookup"><span data-stu-id="a8730-207">mediumrc</span></span> | <span data-ttu-id="a8730-208">largerc</span><span class="sxs-lookup"><span data-stu-id="a8730-208">largerc</span></span> | <span data-ttu-id="a8730-209">xlargerc</span><span class="sxs-lookup"><span data-stu-id="a8730-209">xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="a8730-210">DW100</span><span class="sxs-lookup"><span data-stu-id="a8730-210">DW100</span></span> |<span data-ttu-id="a8730-211">100</span><span class="sxs-lookup"><span data-stu-id="a8730-211">100</span></span> |<span data-ttu-id="a8730-212">100</span><span class="sxs-lookup"><span data-stu-id="a8730-212">100</span></span> |<span data-ttu-id="a8730-213">200</span><span class="sxs-lookup"><span data-stu-id="a8730-213">200</span></span> |<span data-ttu-id="a8730-214">400</span><span class="sxs-lookup"><span data-stu-id="a8730-214">400</span></span> |
| <span data-ttu-id="a8730-215">DW200</span><span class="sxs-lookup"><span data-stu-id="a8730-215">DW200</span></span> |<span data-ttu-id="a8730-216">100</span><span class="sxs-lookup"><span data-stu-id="a8730-216">100</span></span> |<span data-ttu-id="a8730-217">200</span><span class="sxs-lookup"><span data-stu-id="a8730-217">200</span></span> |<span data-ttu-id="a8730-218">400</span><span class="sxs-lookup"><span data-stu-id="a8730-218">400</span></span> |<span data-ttu-id="a8730-219">800</span><span class="sxs-lookup"><span data-stu-id="a8730-219">800</span></span> |
| <span data-ttu-id="a8730-220">DW300</span><span class="sxs-lookup"><span data-stu-id="a8730-220">DW300</span></span> |<span data-ttu-id="a8730-221">100</span><span class="sxs-lookup"><span data-stu-id="a8730-221">100</span></span> |<span data-ttu-id="a8730-222">200</span><span class="sxs-lookup"><span data-stu-id="a8730-222">200</span></span> |<span data-ttu-id="a8730-223">400</span><span class="sxs-lookup"><span data-stu-id="a8730-223">400</span></span> |<span data-ttu-id="a8730-224">800</span><span class="sxs-lookup"><span data-stu-id="a8730-224">800</span></span> |
| <span data-ttu-id="a8730-225">DW400</span><span class="sxs-lookup"><span data-stu-id="a8730-225">DW400</span></span> |<span data-ttu-id="a8730-226">100</span><span class="sxs-lookup"><span data-stu-id="a8730-226">100</span></span> |<span data-ttu-id="a8730-227">400</span><span class="sxs-lookup"><span data-stu-id="a8730-227">400</span></span> |<span data-ttu-id="a8730-228">800</span><span class="sxs-lookup"><span data-stu-id="a8730-228">800</span></span> |<span data-ttu-id="a8730-229">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-229">1,600</span></span> |
| <span data-ttu-id="a8730-230">DW500</span><span class="sxs-lookup"><span data-stu-id="a8730-230">DW500</span></span> |<span data-ttu-id="a8730-231">100</span><span class="sxs-lookup"><span data-stu-id="a8730-231">100</span></span> |<span data-ttu-id="a8730-232">400</span><span class="sxs-lookup"><span data-stu-id="a8730-232">400</span></span> |<span data-ttu-id="a8730-233">800</span><span class="sxs-lookup"><span data-stu-id="a8730-233">800</span></span> |<span data-ttu-id="a8730-234">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-234">1,600</span></span> |
| <span data-ttu-id="a8730-235">DW600</span><span class="sxs-lookup"><span data-stu-id="a8730-235">DW600</span></span> |<span data-ttu-id="a8730-236">100</span><span class="sxs-lookup"><span data-stu-id="a8730-236">100</span></span> |<span data-ttu-id="a8730-237">400</span><span class="sxs-lookup"><span data-stu-id="a8730-237">400</span></span> |<span data-ttu-id="a8730-238">800</span><span class="sxs-lookup"><span data-stu-id="a8730-238">800</span></span> |<span data-ttu-id="a8730-239">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-239">1,600</span></span> |
| <span data-ttu-id="a8730-240">DW1000</span><span class="sxs-lookup"><span data-stu-id="a8730-240">DW1000</span></span> |<span data-ttu-id="a8730-241">100</span><span class="sxs-lookup"><span data-stu-id="a8730-241">100</span></span> |<span data-ttu-id="a8730-242">800</span><span class="sxs-lookup"><span data-stu-id="a8730-242">800</span></span> |<span data-ttu-id="a8730-243">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-243">1,600</span></span> |<span data-ttu-id="a8730-244">3.200</span><span class="sxs-lookup"><span data-stu-id="a8730-244">3,200</span></span> |
| <span data-ttu-id="a8730-245">DW1200</span><span class="sxs-lookup"><span data-stu-id="a8730-245">DW1200</span></span> |<span data-ttu-id="a8730-246">100</span><span class="sxs-lookup"><span data-stu-id="a8730-246">100</span></span> |<span data-ttu-id="a8730-247">800</span><span class="sxs-lookup"><span data-stu-id="a8730-247">800</span></span> |<span data-ttu-id="a8730-248">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-248">1,600</span></span> |<span data-ttu-id="a8730-249">3.200</span><span class="sxs-lookup"><span data-stu-id="a8730-249">3,200</span></span> |
| <span data-ttu-id="a8730-250">DW1500</span><span class="sxs-lookup"><span data-stu-id="a8730-250">DW1500</span></span> |<span data-ttu-id="a8730-251">100</span><span class="sxs-lookup"><span data-stu-id="a8730-251">100</span></span> |<span data-ttu-id="a8730-252">800</span><span class="sxs-lookup"><span data-stu-id="a8730-252">800</span></span> |<span data-ttu-id="a8730-253">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-253">1,600</span></span> |<span data-ttu-id="a8730-254">3.200</span><span class="sxs-lookup"><span data-stu-id="a8730-254">3,200</span></span> |
| <span data-ttu-id="a8730-255">DW2000</span><span class="sxs-lookup"><span data-stu-id="a8730-255">DW2000</span></span> |<span data-ttu-id="a8730-256">100</span><span class="sxs-lookup"><span data-stu-id="a8730-256">100</span></span> |<span data-ttu-id="a8730-257">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-257">1,600</span></span> |<span data-ttu-id="a8730-258">3.200</span><span class="sxs-lookup"><span data-stu-id="a8730-258">3,200</span></span> |<span data-ttu-id="a8730-259">6.400</span><span class="sxs-lookup"><span data-stu-id="a8730-259">6,400</span></span> |
| <span data-ttu-id="a8730-260">DW3000</span><span class="sxs-lookup"><span data-stu-id="a8730-260">DW3000</span></span> |<span data-ttu-id="a8730-261">100</span><span class="sxs-lookup"><span data-stu-id="a8730-261">100</span></span> |<span data-ttu-id="a8730-262">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-262">1,600</span></span> |<span data-ttu-id="a8730-263">3.200</span><span class="sxs-lookup"><span data-stu-id="a8730-263">3,200</span></span> |<span data-ttu-id="a8730-264">6.400</span><span class="sxs-lookup"><span data-stu-id="a8730-264">6,400</span></span> |
| <span data-ttu-id="a8730-265">DW6000</span><span class="sxs-lookup"><span data-stu-id="a8730-265">DW6000</span></span> |<span data-ttu-id="a8730-266">100</span><span class="sxs-lookup"><span data-stu-id="a8730-266">100</span></span> |<span data-ttu-id="a8730-267">3.200</span><span class="sxs-lookup"><span data-stu-id="a8730-267">3,200</span></span> |<span data-ttu-id="a8730-268">6.400</span><span class="sxs-lookup"><span data-stu-id="a8730-268">6,400</span></span> |<span data-ttu-id="a8730-269">12.800</span><span class="sxs-lookup"><span data-stu-id="a8730-269">12,800</span></span> |

<span data-ttu-id="a8730-270">A tabela a seguir mapeia a memória alocada para cada distribuição por DWU e classe de recursos estáticos.</span><span class="sxs-lookup"><span data-stu-id="a8730-270">The following table maps the memory allocated to each distribution by DWU and static resource class.</span></span> <span data-ttu-id="a8730-271">Observe que as classes de recursos superiores têm sua memória reduzida para atender os limites de DWU globais.</span><span class="sxs-lookup"><span data-stu-id="a8730-271">Note that the higher resource classes have their memory reduced to honor the global DWU limits.</span></span>

### <a name="memory-allocations-per-distribution-for-static-resource-classes-mb"></a><span data-ttu-id="a8730-272">Alocações de memória por distribuição de classes de recursos estáticos (MB)</span><span class="sxs-lookup"><span data-stu-id="a8730-272">Memory allocations per distribution for static resource classes (MB)</span></span>
| <span data-ttu-id="a8730-273">DWU</span><span class="sxs-lookup"><span data-stu-id="a8730-273">DWU</span></span> | <span data-ttu-id="a8730-274">staticrc10</span><span class="sxs-lookup"><span data-stu-id="a8730-274">staticrc10</span></span> | <span data-ttu-id="a8730-275">staticrc20</span><span class="sxs-lookup"><span data-stu-id="a8730-275">staticrc20</span></span> | <span data-ttu-id="a8730-276">staticrc30</span><span class="sxs-lookup"><span data-stu-id="a8730-276">staticrc30</span></span> | <span data-ttu-id="a8730-277">staticrc40</span><span class="sxs-lookup"><span data-stu-id="a8730-277">staticrc40</span></span> | <span data-ttu-id="a8730-278">staticrc50</span><span class="sxs-lookup"><span data-stu-id="a8730-278">staticrc50</span></span> | <span data-ttu-id="a8730-279">staticrc60</span><span class="sxs-lookup"><span data-stu-id="a8730-279">staticrc60</span></span> | <span data-ttu-id="a8730-280">staticrc70</span><span class="sxs-lookup"><span data-stu-id="a8730-280">staticrc70</span></span> | <span data-ttu-id="a8730-281">staticrc80</span><span class="sxs-lookup"><span data-stu-id="a8730-281">staticrc80</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="a8730-282">DW100</span><span class="sxs-lookup"><span data-stu-id="a8730-282">DW100</span></span> |<span data-ttu-id="a8730-283">100</span><span class="sxs-lookup"><span data-stu-id="a8730-283">100</span></span> |<span data-ttu-id="a8730-284">200</span><span class="sxs-lookup"><span data-stu-id="a8730-284">200</span></span> |<span data-ttu-id="a8730-285">400</span><span class="sxs-lookup"><span data-stu-id="a8730-285">400</span></span> |<span data-ttu-id="a8730-286">400</span><span class="sxs-lookup"><span data-stu-id="a8730-286">400</span></span> |<span data-ttu-id="a8730-287">400</span><span class="sxs-lookup"><span data-stu-id="a8730-287">400</span></span> |<span data-ttu-id="a8730-288">400</span><span class="sxs-lookup"><span data-stu-id="a8730-288">400</span></span> |<span data-ttu-id="a8730-289">400</span><span class="sxs-lookup"><span data-stu-id="a8730-289">400</span></span> |<span data-ttu-id="a8730-290">400</span><span class="sxs-lookup"><span data-stu-id="a8730-290">400</span></span> |
| <span data-ttu-id="a8730-291">DW200</span><span class="sxs-lookup"><span data-stu-id="a8730-291">DW200</span></span> |<span data-ttu-id="a8730-292">100</span><span class="sxs-lookup"><span data-stu-id="a8730-292">100</span></span> |<span data-ttu-id="a8730-293">200</span><span class="sxs-lookup"><span data-stu-id="a8730-293">200</span></span> |<span data-ttu-id="a8730-294">400</span><span class="sxs-lookup"><span data-stu-id="a8730-294">400</span></span> |<span data-ttu-id="a8730-295">800</span><span class="sxs-lookup"><span data-stu-id="a8730-295">800</span></span> |<span data-ttu-id="a8730-296">800</span><span class="sxs-lookup"><span data-stu-id="a8730-296">800</span></span> |<span data-ttu-id="a8730-297">800</span><span class="sxs-lookup"><span data-stu-id="a8730-297">800</span></span> |<span data-ttu-id="a8730-298">800</span><span class="sxs-lookup"><span data-stu-id="a8730-298">800</span></span> |<span data-ttu-id="a8730-299">800</span><span class="sxs-lookup"><span data-stu-id="a8730-299">800</span></span> |
| <span data-ttu-id="a8730-300">DW300</span><span class="sxs-lookup"><span data-stu-id="a8730-300">DW300</span></span> |<span data-ttu-id="a8730-301">100</span><span class="sxs-lookup"><span data-stu-id="a8730-301">100</span></span> |<span data-ttu-id="a8730-302">200</span><span class="sxs-lookup"><span data-stu-id="a8730-302">200</span></span> |<span data-ttu-id="a8730-303">400</span><span class="sxs-lookup"><span data-stu-id="a8730-303">400</span></span> |<span data-ttu-id="a8730-304">800</span><span class="sxs-lookup"><span data-stu-id="a8730-304">800</span></span> |<span data-ttu-id="a8730-305">800</span><span class="sxs-lookup"><span data-stu-id="a8730-305">800</span></span> |<span data-ttu-id="a8730-306">800</span><span class="sxs-lookup"><span data-stu-id="a8730-306">800</span></span> |<span data-ttu-id="a8730-307">800</span><span class="sxs-lookup"><span data-stu-id="a8730-307">800</span></span> |<span data-ttu-id="a8730-308">800</span><span class="sxs-lookup"><span data-stu-id="a8730-308">800</span></span> |
| <span data-ttu-id="a8730-309">DW400</span><span class="sxs-lookup"><span data-stu-id="a8730-309">DW400</span></span> |<span data-ttu-id="a8730-310">100</span><span class="sxs-lookup"><span data-stu-id="a8730-310">100</span></span> |<span data-ttu-id="a8730-311">200</span><span class="sxs-lookup"><span data-stu-id="a8730-311">200</span></span> |<span data-ttu-id="a8730-312">400</span><span class="sxs-lookup"><span data-stu-id="a8730-312">400</span></span> |<span data-ttu-id="a8730-313">800</span><span class="sxs-lookup"><span data-stu-id="a8730-313">800</span></span> |<span data-ttu-id="a8730-314">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-314">1,600</span></span> |<span data-ttu-id="a8730-315">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-315">1,600</span></span> |<span data-ttu-id="a8730-316">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-316">1,600</span></span> |<span data-ttu-id="a8730-317">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-317">1,600</span></span> |
| <span data-ttu-id="a8730-318">DW500</span><span class="sxs-lookup"><span data-stu-id="a8730-318">DW500</span></span> |<span data-ttu-id="a8730-319">100</span><span class="sxs-lookup"><span data-stu-id="a8730-319">100</span></span> |<span data-ttu-id="a8730-320">200</span><span class="sxs-lookup"><span data-stu-id="a8730-320">200</span></span> |<span data-ttu-id="a8730-321">400</span><span class="sxs-lookup"><span data-stu-id="a8730-321">400</span></span> |<span data-ttu-id="a8730-322">800</span><span class="sxs-lookup"><span data-stu-id="a8730-322">800</span></span> |<span data-ttu-id="a8730-323">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-323">1,600</span></span> |<span data-ttu-id="a8730-324">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-324">1,600</span></span> |<span data-ttu-id="a8730-325">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-325">1,600</span></span> |<span data-ttu-id="a8730-326">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-326">1,600</span></span> |
| <span data-ttu-id="a8730-327">DW600</span><span class="sxs-lookup"><span data-stu-id="a8730-327">DW600</span></span> |<span data-ttu-id="a8730-328">100</span><span class="sxs-lookup"><span data-stu-id="a8730-328">100</span></span> |<span data-ttu-id="a8730-329">200</span><span class="sxs-lookup"><span data-stu-id="a8730-329">200</span></span> |<span data-ttu-id="a8730-330">400</span><span class="sxs-lookup"><span data-stu-id="a8730-330">400</span></span> |<span data-ttu-id="a8730-331">800</span><span class="sxs-lookup"><span data-stu-id="a8730-331">800</span></span> |<span data-ttu-id="a8730-332">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-332">1,600</span></span> |<span data-ttu-id="a8730-333">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-333">1,600</span></span> |<span data-ttu-id="a8730-334">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-334">1,600</span></span> |<span data-ttu-id="a8730-335">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-335">1,600</span></span> |
| <span data-ttu-id="a8730-336">DW1000</span><span class="sxs-lookup"><span data-stu-id="a8730-336">DW1000</span></span> |<span data-ttu-id="a8730-337">100</span><span class="sxs-lookup"><span data-stu-id="a8730-337">100</span></span> |<span data-ttu-id="a8730-338">200</span><span class="sxs-lookup"><span data-stu-id="a8730-338">200</span></span> |<span data-ttu-id="a8730-339">400</span><span class="sxs-lookup"><span data-stu-id="a8730-339">400</span></span> |<span data-ttu-id="a8730-340">800</span><span class="sxs-lookup"><span data-stu-id="a8730-340">800</span></span> |<span data-ttu-id="a8730-341">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-341">1,600</span></span> |<span data-ttu-id="a8730-342">3.200</span><span class="sxs-lookup"><span data-stu-id="a8730-342">3,200</span></span> |<span data-ttu-id="a8730-343">3.200</span><span class="sxs-lookup"><span data-stu-id="a8730-343">3,200</span></span> |<span data-ttu-id="a8730-344">3.200</span><span class="sxs-lookup"><span data-stu-id="a8730-344">3,200</span></span> |
| <span data-ttu-id="a8730-345">DW1200</span><span class="sxs-lookup"><span data-stu-id="a8730-345">DW1200</span></span> |<span data-ttu-id="a8730-346">100</span><span class="sxs-lookup"><span data-stu-id="a8730-346">100</span></span> |<span data-ttu-id="a8730-347">200</span><span class="sxs-lookup"><span data-stu-id="a8730-347">200</span></span> |<span data-ttu-id="a8730-348">400</span><span class="sxs-lookup"><span data-stu-id="a8730-348">400</span></span> |<span data-ttu-id="a8730-349">800</span><span class="sxs-lookup"><span data-stu-id="a8730-349">800</span></span> |<span data-ttu-id="a8730-350">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-350">1,600</span></span> |<span data-ttu-id="a8730-351">3.200</span><span class="sxs-lookup"><span data-stu-id="a8730-351">3,200</span></span> |<span data-ttu-id="a8730-352">3.200</span><span class="sxs-lookup"><span data-stu-id="a8730-352">3,200</span></span> |<span data-ttu-id="a8730-353">3.200</span><span class="sxs-lookup"><span data-stu-id="a8730-353">3,200</span></span> |
| <span data-ttu-id="a8730-354">DW1500</span><span class="sxs-lookup"><span data-stu-id="a8730-354">DW1500</span></span> |<span data-ttu-id="a8730-355">100</span><span class="sxs-lookup"><span data-stu-id="a8730-355">100</span></span> |<span data-ttu-id="a8730-356">200</span><span class="sxs-lookup"><span data-stu-id="a8730-356">200</span></span> |<span data-ttu-id="a8730-357">400</span><span class="sxs-lookup"><span data-stu-id="a8730-357">400</span></span> |<span data-ttu-id="a8730-358">800</span><span class="sxs-lookup"><span data-stu-id="a8730-358">800</span></span> |<span data-ttu-id="a8730-359">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-359">1,600</span></span> |<span data-ttu-id="a8730-360">3.200</span><span class="sxs-lookup"><span data-stu-id="a8730-360">3,200</span></span> |<span data-ttu-id="a8730-361">3.200</span><span class="sxs-lookup"><span data-stu-id="a8730-361">3,200</span></span> |<span data-ttu-id="a8730-362">3.200</span><span class="sxs-lookup"><span data-stu-id="a8730-362">3,200</span></span> |
| <span data-ttu-id="a8730-363">DW2000</span><span class="sxs-lookup"><span data-stu-id="a8730-363">DW2000</span></span> |<span data-ttu-id="a8730-364">100</span><span class="sxs-lookup"><span data-stu-id="a8730-364">100</span></span> |<span data-ttu-id="a8730-365">200</span><span class="sxs-lookup"><span data-stu-id="a8730-365">200</span></span> |<span data-ttu-id="a8730-366">400</span><span class="sxs-lookup"><span data-stu-id="a8730-366">400</span></span> |<span data-ttu-id="a8730-367">800</span><span class="sxs-lookup"><span data-stu-id="a8730-367">800</span></span> |<span data-ttu-id="a8730-368">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-368">1,600</span></span> |<span data-ttu-id="a8730-369">3.200</span><span class="sxs-lookup"><span data-stu-id="a8730-369">3,200</span></span> |<span data-ttu-id="a8730-370">6.400</span><span class="sxs-lookup"><span data-stu-id="a8730-370">6,400</span></span> |<span data-ttu-id="a8730-371">6.400</span><span class="sxs-lookup"><span data-stu-id="a8730-371">6,400</span></span> |
| <span data-ttu-id="a8730-372">DW3000</span><span class="sxs-lookup"><span data-stu-id="a8730-372">DW3000</span></span> |<span data-ttu-id="a8730-373">100</span><span class="sxs-lookup"><span data-stu-id="a8730-373">100</span></span> |<span data-ttu-id="a8730-374">200</span><span class="sxs-lookup"><span data-stu-id="a8730-374">200</span></span> |<span data-ttu-id="a8730-375">400</span><span class="sxs-lookup"><span data-stu-id="a8730-375">400</span></span> |<span data-ttu-id="a8730-376">800</span><span class="sxs-lookup"><span data-stu-id="a8730-376">800</span></span> |<span data-ttu-id="a8730-377">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-377">1,600</span></span> |<span data-ttu-id="a8730-378">3.200</span><span class="sxs-lookup"><span data-stu-id="a8730-378">3,200</span></span> |<span data-ttu-id="a8730-379">6.400</span><span class="sxs-lookup"><span data-stu-id="a8730-379">6,400</span></span> |<span data-ttu-id="a8730-380">6.400</span><span class="sxs-lookup"><span data-stu-id="a8730-380">6,400</span></span> |
| <span data-ttu-id="a8730-381">DW6000</span><span class="sxs-lookup"><span data-stu-id="a8730-381">DW6000</span></span> |<span data-ttu-id="a8730-382">100</span><span class="sxs-lookup"><span data-stu-id="a8730-382">100</span></span> |<span data-ttu-id="a8730-383">200</span><span class="sxs-lookup"><span data-stu-id="a8730-383">200</span></span> |<span data-ttu-id="a8730-384">400</span><span class="sxs-lookup"><span data-stu-id="a8730-384">400</span></span> |<span data-ttu-id="a8730-385">800</span><span class="sxs-lookup"><span data-stu-id="a8730-385">800</span></span> |<span data-ttu-id="a8730-386">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-386">1,600</span></span> |<span data-ttu-id="a8730-387">3.200</span><span class="sxs-lookup"><span data-stu-id="a8730-387">3,200</span></span> |<span data-ttu-id="a8730-388">6.400</span><span class="sxs-lookup"><span data-stu-id="a8730-388">6,400</span></span> |<span data-ttu-id="a8730-389">12.800</span><span class="sxs-lookup"><span data-stu-id="a8730-389">12,800</span></span> |

<span data-ttu-id="a8730-390">Na tabela anterior, você pode ver que uma consulta em execução em um DW2000 na classe de recursos **xlargerc** teria acesso a 6.400 MB de memória dentro de cada um dos 60 bancos de dados distribuídos.</span><span class="sxs-lookup"><span data-stu-id="a8730-390">From the preceding table, you can see that a query running on a DW2000 in the **xlargerc** resource class would have access to 6,400 MB of memory within each of the 60 distributed databases.</span></span>  <span data-ttu-id="a8730-391">Há 60 distribuições no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a8730-391">In SQL Data Warehouse, there are 60 distributions.</span></span> <span data-ttu-id="a8730-392">Portanto, para calcular a alocação de memória total para uma consulta em uma determinada classe de recurso, os valores acima devem ser multiplicados por 60.</span><span class="sxs-lookup"><span data-stu-id="a8730-392">Therefore, to calculate the total memory allocation for a query in a given resource class, the above values should be multiplied by 60.</span></span>

### <a name="memory-allocations-system-wide-gb"></a><span data-ttu-id="a8730-393">Alocações de memória em todo o sistema (GB)</span><span class="sxs-lookup"><span data-stu-id="a8730-393">Memory allocations system-wide (GB)</span></span>
| <span data-ttu-id="a8730-394">DWU</span><span class="sxs-lookup"><span data-stu-id="a8730-394">DWU</span></span> | <span data-ttu-id="a8730-395">smallrc</span><span class="sxs-lookup"><span data-stu-id="a8730-395">smallrc</span></span> | <span data-ttu-id="a8730-396">mediumrc</span><span class="sxs-lookup"><span data-stu-id="a8730-396">mediumrc</span></span> | <span data-ttu-id="a8730-397">largerc</span><span class="sxs-lookup"><span data-stu-id="a8730-397">largerc</span></span> | <span data-ttu-id="a8730-398">xlargerc</span><span class="sxs-lookup"><span data-stu-id="a8730-398">xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="a8730-399">DW100</span><span class="sxs-lookup"><span data-stu-id="a8730-399">DW100</span></span> |<span data-ttu-id="a8730-400">6</span><span class="sxs-lookup"><span data-stu-id="a8730-400">6</span></span> |<span data-ttu-id="a8730-401">6</span><span class="sxs-lookup"><span data-stu-id="a8730-401">6</span></span> |<span data-ttu-id="a8730-402">12</span><span class="sxs-lookup"><span data-stu-id="a8730-402">12</span></span> |<span data-ttu-id="a8730-403">23</span><span class="sxs-lookup"><span data-stu-id="a8730-403">23</span></span> |
| <span data-ttu-id="a8730-404">DW200</span><span class="sxs-lookup"><span data-stu-id="a8730-404">DW200</span></span> |<span data-ttu-id="a8730-405">6</span><span class="sxs-lookup"><span data-stu-id="a8730-405">6</span></span> |<span data-ttu-id="a8730-406">12</span><span class="sxs-lookup"><span data-stu-id="a8730-406">12</span></span> |<span data-ttu-id="a8730-407">23</span><span class="sxs-lookup"><span data-stu-id="a8730-407">23</span></span> |<span data-ttu-id="a8730-408">47</span><span class="sxs-lookup"><span data-stu-id="a8730-408">47</span></span> |
| <span data-ttu-id="a8730-409">DW300</span><span class="sxs-lookup"><span data-stu-id="a8730-409">DW300</span></span> |<span data-ttu-id="a8730-410">6</span><span class="sxs-lookup"><span data-stu-id="a8730-410">6</span></span> |<span data-ttu-id="a8730-411">12</span><span class="sxs-lookup"><span data-stu-id="a8730-411">12</span></span> |<span data-ttu-id="a8730-412">23</span><span class="sxs-lookup"><span data-stu-id="a8730-412">23</span></span> |<span data-ttu-id="a8730-413">47</span><span class="sxs-lookup"><span data-stu-id="a8730-413">47</span></span> |
| <span data-ttu-id="a8730-414">DW400</span><span class="sxs-lookup"><span data-stu-id="a8730-414">DW400</span></span> |<span data-ttu-id="a8730-415">6</span><span class="sxs-lookup"><span data-stu-id="a8730-415">6</span></span> |<span data-ttu-id="a8730-416">23</span><span class="sxs-lookup"><span data-stu-id="a8730-416">23</span></span> |<span data-ttu-id="a8730-417">47</span><span class="sxs-lookup"><span data-stu-id="a8730-417">47</span></span> |<span data-ttu-id="a8730-418">94</span><span class="sxs-lookup"><span data-stu-id="a8730-418">94</span></span> |
| <span data-ttu-id="a8730-419">DW500</span><span class="sxs-lookup"><span data-stu-id="a8730-419">DW500</span></span> |<span data-ttu-id="a8730-420">6</span><span class="sxs-lookup"><span data-stu-id="a8730-420">6</span></span> |<span data-ttu-id="a8730-421">23</span><span class="sxs-lookup"><span data-stu-id="a8730-421">23</span></span> |<span data-ttu-id="a8730-422">47</span><span class="sxs-lookup"><span data-stu-id="a8730-422">47</span></span> |<span data-ttu-id="a8730-423">94</span><span class="sxs-lookup"><span data-stu-id="a8730-423">94</span></span> |
| <span data-ttu-id="a8730-424">DW600</span><span class="sxs-lookup"><span data-stu-id="a8730-424">DW600</span></span> |<span data-ttu-id="a8730-425">6</span><span class="sxs-lookup"><span data-stu-id="a8730-425">6</span></span> |<span data-ttu-id="a8730-426">23</span><span class="sxs-lookup"><span data-stu-id="a8730-426">23</span></span> |<span data-ttu-id="a8730-427">47</span><span class="sxs-lookup"><span data-stu-id="a8730-427">47</span></span> |<span data-ttu-id="a8730-428">94</span><span class="sxs-lookup"><span data-stu-id="a8730-428">94</span></span> |
| <span data-ttu-id="a8730-429">DW1000</span><span class="sxs-lookup"><span data-stu-id="a8730-429">DW1000</span></span> |<span data-ttu-id="a8730-430">6</span><span class="sxs-lookup"><span data-stu-id="a8730-430">6</span></span> |<span data-ttu-id="a8730-431">47</span><span class="sxs-lookup"><span data-stu-id="a8730-431">47</span></span> |<span data-ttu-id="a8730-432">94</span><span class="sxs-lookup"><span data-stu-id="a8730-432">94</span></span> |<span data-ttu-id="a8730-433">188</span><span class="sxs-lookup"><span data-stu-id="a8730-433">188</span></span> |
| <span data-ttu-id="a8730-434">DW1200</span><span class="sxs-lookup"><span data-stu-id="a8730-434">DW1200</span></span> |<span data-ttu-id="a8730-435">6</span><span class="sxs-lookup"><span data-stu-id="a8730-435">6</span></span> |<span data-ttu-id="a8730-436">47</span><span class="sxs-lookup"><span data-stu-id="a8730-436">47</span></span> |<span data-ttu-id="a8730-437">94</span><span class="sxs-lookup"><span data-stu-id="a8730-437">94</span></span> |<span data-ttu-id="a8730-438">188</span><span class="sxs-lookup"><span data-stu-id="a8730-438">188</span></span> |
| <span data-ttu-id="a8730-439">DW1500</span><span class="sxs-lookup"><span data-stu-id="a8730-439">DW1500</span></span> |<span data-ttu-id="a8730-440">6</span><span class="sxs-lookup"><span data-stu-id="a8730-440">6</span></span> |<span data-ttu-id="a8730-441">47</span><span class="sxs-lookup"><span data-stu-id="a8730-441">47</span></span> |<span data-ttu-id="a8730-442">94</span><span class="sxs-lookup"><span data-stu-id="a8730-442">94</span></span> |<span data-ttu-id="a8730-443">188</span><span class="sxs-lookup"><span data-stu-id="a8730-443">188</span></span> |
| <span data-ttu-id="a8730-444">DW2000</span><span class="sxs-lookup"><span data-stu-id="a8730-444">DW2000</span></span> |<span data-ttu-id="a8730-445">6</span><span class="sxs-lookup"><span data-stu-id="a8730-445">6</span></span> |<span data-ttu-id="a8730-446">94</span><span class="sxs-lookup"><span data-stu-id="a8730-446">94</span></span> |<span data-ttu-id="a8730-447">188</span><span class="sxs-lookup"><span data-stu-id="a8730-447">188</span></span> |<span data-ttu-id="a8730-448">375</span><span class="sxs-lookup"><span data-stu-id="a8730-448">375</span></span> |
| <span data-ttu-id="a8730-449">DW3000</span><span class="sxs-lookup"><span data-stu-id="a8730-449">DW3000</span></span> |<span data-ttu-id="a8730-450">6</span><span class="sxs-lookup"><span data-stu-id="a8730-450">6</span></span> |<span data-ttu-id="a8730-451">94</span><span class="sxs-lookup"><span data-stu-id="a8730-451">94</span></span> |<span data-ttu-id="a8730-452">188</span><span class="sxs-lookup"><span data-stu-id="a8730-452">188</span></span> |<span data-ttu-id="a8730-453">375</span><span class="sxs-lookup"><span data-stu-id="a8730-453">375</span></span> |
| <span data-ttu-id="a8730-454">DW6000</span><span class="sxs-lookup"><span data-stu-id="a8730-454">DW6000</span></span> |<span data-ttu-id="a8730-455">6</span><span class="sxs-lookup"><span data-stu-id="a8730-455">6</span></span> |<span data-ttu-id="a8730-456">188</span><span class="sxs-lookup"><span data-stu-id="a8730-456">188</span></span> |<span data-ttu-id="a8730-457">375</span><span class="sxs-lookup"><span data-stu-id="a8730-457">375</span></span> |<span data-ttu-id="a8730-458">750</span><span class="sxs-lookup"><span data-stu-id="a8730-458">750</span></span> |

<span data-ttu-id="a8730-459">Nesta tabela com as alocações de memória de todo o sistema, você pode ver que uma consulta em execução em um DW2000 na classe de recurso xlargerc recebe a alocação de um total de 375 GB de memória (6.400 MB * 60 distribuições / 1.024 para converter em GB) por todo o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a8730-459">From this table of system-wide memory allocations, you can see that a query running on a DW2000 in the xlargerc resource class is allocated a total of 375 GB of memory (6,400 MB * 60 distributions / 1,024 to convert to GB) over the entirety of your SQL Data Warehouse.</span></span>

<span data-ttu-id="a8730-460">O mesmo cálculo se aplica a classes de recursos estáticos.</span><span class="sxs-lookup"><span data-stu-id="a8730-460">The same calculation applies to static resource classes.</span></span>
 
## <a name="concurrency-slot-consumption"></a><span data-ttu-id="a8730-461">Consumo de slot de simultaneidade</span><span class="sxs-lookup"><span data-stu-id="a8730-461">Concurrency slot consumption</span></span>  
<span data-ttu-id="a8730-462">O SQL Data Warehouse concede mais memória para consultas em execução em classes de recursos mais elevadas.</span><span class="sxs-lookup"><span data-stu-id="a8730-462">SQL Data Warehouse grants more memory to queries running in higher resource classes.</span></span> <span data-ttu-id="a8730-463">A memória é um recurso fixo.</span><span class="sxs-lookup"><span data-stu-id="a8730-463">Memory is a fixed resource.</span></span>  <span data-ttu-id="a8730-464">Portanto, quanto mais memória for alocada por consulta, menos consultas simultâneas poderão ser executadas.</span><span class="sxs-lookup"><span data-stu-id="a8730-464">Therefore, the more memory allocated per query, the fewer concurrent queries can execute.</span></span> <span data-ttu-id="a8730-465">A tabela a seguir reitera todos os conceitos anteriores em uma única exibição que mostra o número de slots de simultaneidade disponíveis por DWU, bem como os slots consumidos por cada classe de recurso.</span><span class="sxs-lookup"><span data-stu-id="a8730-465">The following table reiterates all of the previous concepts in a single view that shows the number of concurrency slots available by DWU and the slots consumed by each resource class.</span></span>  

### <a name="allocation-and-consumption-of-concurrency-slots-for-dynamic-resource-classes"></a><span data-ttu-id="a8730-466">Alocação e consumo de slots de simultaneidade para classes de recursos dinâmicos</span><span class="sxs-lookup"><span data-stu-id="a8730-466">Allocation and consumption of concurrency slots for dynamic resource classes</span></span>  
| <span data-ttu-id="a8730-467">DWU</span><span class="sxs-lookup"><span data-stu-id="a8730-467">DWU</span></span> | <span data-ttu-id="a8730-468">Máximo de consultas simultâneas</span><span class="sxs-lookup"><span data-stu-id="a8730-468">Maximum concurrent queries</span></span> | <span data-ttu-id="a8730-469">Slots de simultaneidade alocados</span><span class="sxs-lookup"><span data-stu-id="a8730-469">Concurrency slots allocated</span></span> | <span data-ttu-id="a8730-470">Slots usados pelo smallrc</span><span class="sxs-lookup"><span data-stu-id="a8730-470">Slots used by smallrc</span></span> | <span data-ttu-id="a8730-471">Slots usados pelo mediumrc</span><span class="sxs-lookup"><span data-stu-id="a8730-471">Slots used by mediumrc</span></span> | <span data-ttu-id="a8730-472">Slots usados pelo largerc</span><span class="sxs-lookup"><span data-stu-id="a8730-472">Slots used by largerc</span></span> | <span data-ttu-id="a8730-473">Slots usados pelo xlargerc</span><span class="sxs-lookup"><span data-stu-id="a8730-473">Slots used by xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="a8730-474">DW100</span><span class="sxs-lookup"><span data-stu-id="a8730-474">DW100</span></span> |<span data-ttu-id="a8730-475">4</span><span class="sxs-lookup"><span data-stu-id="a8730-475">4</span></span> |<span data-ttu-id="a8730-476">4</span><span class="sxs-lookup"><span data-stu-id="a8730-476">4</span></span> |<span data-ttu-id="a8730-477">1</span><span class="sxs-lookup"><span data-stu-id="a8730-477">1</span></span> |<span data-ttu-id="a8730-478">1</span><span class="sxs-lookup"><span data-stu-id="a8730-478">1</span></span> |<span data-ttu-id="a8730-479">2</span><span class="sxs-lookup"><span data-stu-id="a8730-479">2</span></span> |<span data-ttu-id="a8730-480">4</span><span class="sxs-lookup"><span data-stu-id="a8730-480">4</span></span> |
| <span data-ttu-id="a8730-481">DW200</span><span class="sxs-lookup"><span data-stu-id="a8730-481">DW200</span></span> |<span data-ttu-id="a8730-482">8</span><span class="sxs-lookup"><span data-stu-id="a8730-482">8</span></span> |<span data-ttu-id="a8730-483">8</span><span class="sxs-lookup"><span data-stu-id="a8730-483">8</span></span> |<span data-ttu-id="a8730-484">1</span><span class="sxs-lookup"><span data-stu-id="a8730-484">1</span></span> |<span data-ttu-id="a8730-485">2</span><span class="sxs-lookup"><span data-stu-id="a8730-485">2</span></span> |<span data-ttu-id="a8730-486">4</span><span class="sxs-lookup"><span data-stu-id="a8730-486">4</span></span> |<span data-ttu-id="a8730-487">8</span><span class="sxs-lookup"><span data-stu-id="a8730-487">8</span></span> |
| <span data-ttu-id="a8730-488">DW300</span><span class="sxs-lookup"><span data-stu-id="a8730-488">DW300</span></span> |<span data-ttu-id="a8730-489">12</span><span class="sxs-lookup"><span data-stu-id="a8730-489">12</span></span> |<span data-ttu-id="a8730-490">12</span><span class="sxs-lookup"><span data-stu-id="a8730-490">12</span></span> |<span data-ttu-id="a8730-491">1</span><span class="sxs-lookup"><span data-stu-id="a8730-491">1</span></span> |<span data-ttu-id="a8730-492">2</span><span class="sxs-lookup"><span data-stu-id="a8730-492">2</span></span> |<span data-ttu-id="a8730-493">4</span><span class="sxs-lookup"><span data-stu-id="a8730-493">4</span></span> |<span data-ttu-id="a8730-494">8</span><span class="sxs-lookup"><span data-stu-id="a8730-494">8</span></span> |
| <span data-ttu-id="a8730-495">DW400</span><span class="sxs-lookup"><span data-stu-id="a8730-495">DW400</span></span> |<span data-ttu-id="a8730-496">16</span><span class="sxs-lookup"><span data-stu-id="a8730-496">16</span></span> |<span data-ttu-id="a8730-497">16</span><span class="sxs-lookup"><span data-stu-id="a8730-497">16</span></span> |<span data-ttu-id="a8730-498">1</span><span class="sxs-lookup"><span data-stu-id="a8730-498">1</span></span> |<span data-ttu-id="a8730-499">4</span><span class="sxs-lookup"><span data-stu-id="a8730-499">4</span></span> |<span data-ttu-id="a8730-500">8</span><span class="sxs-lookup"><span data-stu-id="a8730-500">8</span></span> |<span data-ttu-id="a8730-501">16</span><span class="sxs-lookup"><span data-stu-id="a8730-501">16</span></span> |
| <span data-ttu-id="a8730-502">DW500</span><span class="sxs-lookup"><span data-stu-id="a8730-502">DW500</span></span> |<span data-ttu-id="a8730-503">20</span><span class="sxs-lookup"><span data-stu-id="a8730-503">20</span></span> |<span data-ttu-id="a8730-504">20</span><span class="sxs-lookup"><span data-stu-id="a8730-504">20</span></span> |<span data-ttu-id="a8730-505">1</span><span class="sxs-lookup"><span data-stu-id="a8730-505">1</span></span> |<span data-ttu-id="a8730-506">4</span><span class="sxs-lookup"><span data-stu-id="a8730-506">4</span></span> |<span data-ttu-id="a8730-507">8</span><span class="sxs-lookup"><span data-stu-id="a8730-507">8</span></span> |<span data-ttu-id="a8730-508">16</span><span class="sxs-lookup"><span data-stu-id="a8730-508">16</span></span> |
| <span data-ttu-id="a8730-509">DW600</span><span class="sxs-lookup"><span data-stu-id="a8730-509">DW600</span></span> |<span data-ttu-id="a8730-510">24</span><span class="sxs-lookup"><span data-stu-id="a8730-510">24</span></span> |<span data-ttu-id="a8730-511">24</span><span class="sxs-lookup"><span data-stu-id="a8730-511">24</span></span> |<span data-ttu-id="a8730-512">1</span><span class="sxs-lookup"><span data-stu-id="a8730-512">1</span></span> |<span data-ttu-id="a8730-513">4</span><span class="sxs-lookup"><span data-stu-id="a8730-513">4</span></span> |<span data-ttu-id="a8730-514">8</span><span class="sxs-lookup"><span data-stu-id="a8730-514">8</span></span> |<span data-ttu-id="a8730-515">16</span><span class="sxs-lookup"><span data-stu-id="a8730-515">16</span></span> |
| <span data-ttu-id="a8730-516">DW1000</span><span class="sxs-lookup"><span data-stu-id="a8730-516">DW1000</span></span> |<span data-ttu-id="a8730-517">32</span><span class="sxs-lookup"><span data-stu-id="a8730-517">32</span></span> |<span data-ttu-id="a8730-518">40</span><span class="sxs-lookup"><span data-stu-id="a8730-518">40</span></span> |<span data-ttu-id="a8730-519">1</span><span class="sxs-lookup"><span data-stu-id="a8730-519">1</span></span> |<span data-ttu-id="a8730-520">8</span><span class="sxs-lookup"><span data-stu-id="a8730-520">8</span></span> |<span data-ttu-id="a8730-521">16</span><span class="sxs-lookup"><span data-stu-id="a8730-521">16</span></span> |<span data-ttu-id="a8730-522">32</span><span class="sxs-lookup"><span data-stu-id="a8730-522">32</span></span> |
| <span data-ttu-id="a8730-523">DW1200</span><span class="sxs-lookup"><span data-stu-id="a8730-523">DW1200</span></span> |<span data-ttu-id="a8730-524">32</span><span class="sxs-lookup"><span data-stu-id="a8730-524">32</span></span> |<span data-ttu-id="a8730-525">48</span><span class="sxs-lookup"><span data-stu-id="a8730-525">48</span></span> |<span data-ttu-id="a8730-526">1</span><span class="sxs-lookup"><span data-stu-id="a8730-526">1</span></span> |<span data-ttu-id="a8730-527">8</span><span class="sxs-lookup"><span data-stu-id="a8730-527">8</span></span> |<span data-ttu-id="a8730-528">16</span><span class="sxs-lookup"><span data-stu-id="a8730-528">16</span></span> |<span data-ttu-id="a8730-529">32</span><span class="sxs-lookup"><span data-stu-id="a8730-529">32</span></span> |
| <span data-ttu-id="a8730-530">DW1500</span><span class="sxs-lookup"><span data-stu-id="a8730-530">DW1500</span></span> |<span data-ttu-id="a8730-531">32</span><span class="sxs-lookup"><span data-stu-id="a8730-531">32</span></span> |<span data-ttu-id="a8730-532">60</span><span class="sxs-lookup"><span data-stu-id="a8730-532">60</span></span> |<span data-ttu-id="a8730-533">1</span><span class="sxs-lookup"><span data-stu-id="a8730-533">1</span></span> |<span data-ttu-id="a8730-534">8</span><span class="sxs-lookup"><span data-stu-id="a8730-534">8</span></span> |<span data-ttu-id="a8730-535">16</span><span class="sxs-lookup"><span data-stu-id="a8730-535">16</span></span> |<span data-ttu-id="a8730-536">32</span><span class="sxs-lookup"><span data-stu-id="a8730-536">32</span></span> |
| <span data-ttu-id="a8730-537">DW2000</span><span class="sxs-lookup"><span data-stu-id="a8730-537">DW2000</span></span> |<span data-ttu-id="a8730-538">32</span><span class="sxs-lookup"><span data-stu-id="a8730-538">32</span></span> |<span data-ttu-id="a8730-539">80</span><span class="sxs-lookup"><span data-stu-id="a8730-539">80</span></span> |<span data-ttu-id="a8730-540">1</span><span class="sxs-lookup"><span data-stu-id="a8730-540">1</span></span> |<span data-ttu-id="a8730-541">16</span><span class="sxs-lookup"><span data-stu-id="a8730-541">16</span></span> |<span data-ttu-id="a8730-542">32</span><span class="sxs-lookup"><span data-stu-id="a8730-542">32</span></span> |<span data-ttu-id="a8730-543">64</span><span class="sxs-lookup"><span data-stu-id="a8730-543">64</span></span> |
| <span data-ttu-id="a8730-544">DW3000</span><span class="sxs-lookup"><span data-stu-id="a8730-544">DW3000</span></span> |<span data-ttu-id="a8730-545">32</span><span class="sxs-lookup"><span data-stu-id="a8730-545">32</span></span> |<span data-ttu-id="a8730-546">120</span><span class="sxs-lookup"><span data-stu-id="a8730-546">120</span></span> |<span data-ttu-id="a8730-547">1</span><span class="sxs-lookup"><span data-stu-id="a8730-547">1</span></span> |<span data-ttu-id="a8730-548">16</span><span class="sxs-lookup"><span data-stu-id="a8730-548">16</span></span> |<span data-ttu-id="a8730-549">32</span><span class="sxs-lookup"><span data-stu-id="a8730-549">32</span></span> |<span data-ttu-id="a8730-550">64</span><span class="sxs-lookup"><span data-stu-id="a8730-550">64</span></span> |
| <span data-ttu-id="a8730-551">DW6000</span><span class="sxs-lookup"><span data-stu-id="a8730-551">DW6000</span></span> |<span data-ttu-id="a8730-552">32</span><span class="sxs-lookup"><span data-stu-id="a8730-552">32</span></span> |<span data-ttu-id="a8730-553">240</span><span class="sxs-lookup"><span data-stu-id="a8730-553">240</span></span> |<span data-ttu-id="a8730-554">1</span><span class="sxs-lookup"><span data-stu-id="a8730-554">1</span></span> |<span data-ttu-id="a8730-555">32</span><span class="sxs-lookup"><span data-stu-id="a8730-555">32</span></span> |<span data-ttu-id="a8730-556">64</span><span class="sxs-lookup"><span data-stu-id="a8730-556">64</span></span> |<span data-ttu-id="a8730-557">128</span><span class="sxs-lookup"><span data-stu-id="a8730-557">128</span></span> |

### <a name="allocation-and-consumption-of-concurrency-slots-for-static-resource-classes"></a><span data-ttu-id="a8730-558">Alocação e consumo de slots de simultaneidade para classes de recursos estáticos</span><span class="sxs-lookup"><span data-stu-id="a8730-558">Allocation and consumption of concurrency slots for static resource classes</span></span>  
| <span data-ttu-id="a8730-559">DWU</span><span class="sxs-lookup"><span data-stu-id="a8730-559">DWU</span></span> | <span data-ttu-id="a8730-560">Máximo de consultas simultâneas</span><span class="sxs-lookup"><span data-stu-id="a8730-560">Maximum concurrent queries</span></span> | <span data-ttu-id="a8730-561">Slots de simultaneidade alocados</span><span class="sxs-lookup"><span data-stu-id="a8730-561">Concurrency slots allocated</span></span> |<span data-ttu-id="a8730-562">staticrc10</span><span class="sxs-lookup"><span data-stu-id="a8730-562">staticrc10</span></span> | <span data-ttu-id="a8730-563">staticrc20</span><span class="sxs-lookup"><span data-stu-id="a8730-563">staticrc20</span></span> | <span data-ttu-id="a8730-564">staticrc30</span><span class="sxs-lookup"><span data-stu-id="a8730-564">staticrc30</span></span> | <span data-ttu-id="a8730-565">staticrc40</span><span class="sxs-lookup"><span data-stu-id="a8730-565">staticrc40</span></span> | <span data-ttu-id="a8730-566">staticrc50</span><span class="sxs-lookup"><span data-stu-id="a8730-566">staticrc50</span></span> | <span data-ttu-id="a8730-567">staticrc60</span><span class="sxs-lookup"><span data-stu-id="a8730-567">staticrc60</span></span> | <span data-ttu-id="a8730-568">staticrc70</span><span class="sxs-lookup"><span data-stu-id="a8730-568">staticrc70</span></span> | <span data-ttu-id="a8730-569">staticrc80</span><span class="sxs-lookup"><span data-stu-id="a8730-569">staticrc80</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="a8730-570">DW100</span><span class="sxs-lookup"><span data-stu-id="a8730-570">DW100</span></span> |<span data-ttu-id="a8730-571">4</span><span class="sxs-lookup"><span data-stu-id="a8730-571">4</span></span> |<span data-ttu-id="a8730-572">4</span><span class="sxs-lookup"><span data-stu-id="a8730-572">4</span></span> |<span data-ttu-id="a8730-573">1</span><span class="sxs-lookup"><span data-stu-id="a8730-573">1</span></span> |<span data-ttu-id="a8730-574">2</span><span class="sxs-lookup"><span data-stu-id="a8730-574">2</span></span> |<span data-ttu-id="a8730-575">4</span><span class="sxs-lookup"><span data-stu-id="a8730-575">4</span></span> |<span data-ttu-id="a8730-576">4</span><span class="sxs-lookup"><span data-stu-id="a8730-576">4</span></span> |<span data-ttu-id="a8730-577">4</span><span class="sxs-lookup"><span data-stu-id="a8730-577">4</span></span> |<span data-ttu-id="a8730-578">4</span><span class="sxs-lookup"><span data-stu-id="a8730-578">4</span></span> |<span data-ttu-id="a8730-579">4</span><span class="sxs-lookup"><span data-stu-id="a8730-579">4</span></span> |<span data-ttu-id="a8730-580">4</span><span class="sxs-lookup"><span data-stu-id="a8730-580">4</span></span> |
| <span data-ttu-id="a8730-581">DW200</span><span class="sxs-lookup"><span data-stu-id="a8730-581">DW200</span></span> |<span data-ttu-id="a8730-582">8</span><span class="sxs-lookup"><span data-stu-id="a8730-582">8</span></span> |<span data-ttu-id="a8730-583">8</span><span class="sxs-lookup"><span data-stu-id="a8730-583">8</span></span> |<span data-ttu-id="a8730-584">1</span><span class="sxs-lookup"><span data-stu-id="a8730-584">1</span></span> |<span data-ttu-id="a8730-585">2</span><span class="sxs-lookup"><span data-stu-id="a8730-585">2</span></span> |<span data-ttu-id="a8730-586">4</span><span class="sxs-lookup"><span data-stu-id="a8730-586">4</span></span> |<span data-ttu-id="a8730-587">8</span><span class="sxs-lookup"><span data-stu-id="a8730-587">8</span></span> |<span data-ttu-id="a8730-588">8</span><span class="sxs-lookup"><span data-stu-id="a8730-588">8</span></span> |<span data-ttu-id="a8730-589">8</span><span class="sxs-lookup"><span data-stu-id="a8730-589">8</span></span> |<span data-ttu-id="a8730-590">8</span><span class="sxs-lookup"><span data-stu-id="a8730-590">8</span></span> |<span data-ttu-id="a8730-591">8</span><span class="sxs-lookup"><span data-stu-id="a8730-591">8</span></span> |
| <span data-ttu-id="a8730-592">DW300</span><span class="sxs-lookup"><span data-stu-id="a8730-592">DW300</span></span> |<span data-ttu-id="a8730-593">12</span><span class="sxs-lookup"><span data-stu-id="a8730-593">12</span></span> |<span data-ttu-id="a8730-594">12</span><span class="sxs-lookup"><span data-stu-id="a8730-594">12</span></span> |<span data-ttu-id="a8730-595">1</span><span class="sxs-lookup"><span data-stu-id="a8730-595">1</span></span> |<span data-ttu-id="a8730-596">2</span><span class="sxs-lookup"><span data-stu-id="a8730-596">2</span></span> |<span data-ttu-id="a8730-597">4</span><span class="sxs-lookup"><span data-stu-id="a8730-597">4</span></span> |<span data-ttu-id="a8730-598">8</span><span class="sxs-lookup"><span data-stu-id="a8730-598">8</span></span> |<span data-ttu-id="a8730-599">8</span><span class="sxs-lookup"><span data-stu-id="a8730-599">8</span></span> |<span data-ttu-id="a8730-600">8</span><span class="sxs-lookup"><span data-stu-id="a8730-600">8</span></span> |<span data-ttu-id="a8730-601">8</span><span class="sxs-lookup"><span data-stu-id="a8730-601">8</span></span> |<span data-ttu-id="a8730-602">8</span><span class="sxs-lookup"><span data-stu-id="a8730-602">8</span></span> |
| <span data-ttu-id="a8730-603">DW400</span><span class="sxs-lookup"><span data-stu-id="a8730-603">DW400</span></span> |<span data-ttu-id="a8730-604">16</span><span class="sxs-lookup"><span data-stu-id="a8730-604">16</span></span> |<span data-ttu-id="a8730-605">16</span><span class="sxs-lookup"><span data-stu-id="a8730-605">16</span></span> |<span data-ttu-id="a8730-606">1</span><span class="sxs-lookup"><span data-stu-id="a8730-606">1</span></span> |<span data-ttu-id="a8730-607">2</span><span class="sxs-lookup"><span data-stu-id="a8730-607">2</span></span> |<span data-ttu-id="a8730-608">4</span><span class="sxs-lookup"><span data-stu-id="a8730-608">4</span></span> |<span data-ttu-id="a8730-609">8</span><span class="sxs-lookup"><span data-stu-id="a8730-609">8</span></span> |<span data-ttu-id="a8730-610">16</span><span class="sxs-lookup"><span data-stu-id="a8730-610">16</span></span> |<span data-ttu-id="a8730-611">16</span><span class="sxs-lookup"><span data-stu-id="a8730-611">16</span></span> |<span data-ttu-id="a8730-612">16</span><span class="sxs-lookup"><span data-stu-id="a8730-612">16</span></span> |<span data-ttu-id="a8730-613">16</span><span class="sxs-lookup"><span data-stu-id="a8730-613">16</span></span> |
| <span data-ttu-id="a8730-614">DW500</span><span class="sxs-lookup"><span data-stu-id="a8730-614">DW500</span></span> | <span data-ttu-id="a8730-615">20</span><span class="sxs-lookup"><span data-stu-id="a8730-615">20</span></span>| <span data-ttu-id="a8730-616">20</span><span class="sxs-lookup"><span data-stu-id="a8730-616">20</span></span>| <span data-ttu-id="a8730-617">1</span><span class="sxs-lookup"><span data-stu-id="a8730-617">1</span></span>| <span data-ttu-id="a8730-618">2</span><span class="sxs-lookup"><span data-stu-id="a8730-618">2</span></span>| <span data-ttu-id="a8730-619">4</span><span class="sxs-lookup"><span data-stu-id="a8730-619">4</span></span>| <span data-ttu-id="a8730-620">8</span><span class="sxs-lookup"><span data-stu-id="a8730-620">8</span></span>| <span data-ttu-id="a8730-621">16</span><span class="sxs-lookup"><span data-stu-id="a8730-621">16</span></span>| <span data-ttu-id="a8730-622">16</span><span class="sxs-lookup"><span data-stu-id="a8730-622">16</span></span>| <span data-ttu-id="a8730-623">16</span><span class="sxs-lookup"><span data-stu-id="a8730-623">16</span></span>| <span data-ttu-id="a8730-624">16</span><span class="sxs-lookup"><span data-stu-id="a8730-624">16</span></span>|
| <span data-ttu-id="a8730-625">DW600</span><span class="sxs-lookup"><span data-stu-id="a8730-625">DW600</span></span> | <span data-ttu-id="a8730-626">24</span><span class="sxs-lookup"><span data-stu-id="a8730-626">24</span></span>| <span data-ttu-id="a8730-627">24</span><span class="sxs-lookup"><span data-stu-id="a8730-627">24</span></span>| <span data-ttu-id="a8730-628">1</span><span class="sxs-lookup"><span data-stu-id="a8730-628">1</span></span>| <span data-ttu-id="a8730-629">2</span><span class="sxs-lookup"><span data-stu-id="a8730-629">2</span></span>| <span data-ttu-id="a8730-630">4</span><span class="sxs-lookup"><span data-stu-id="a8730-630">4</span></span>| <span data-ttu-id="a8730-631">8</span><span class="sxs-lookup"><span data-stu-id="a8730-631">8</span></span>| <span data-ttu-id="a8730-632">16</span><span class="sxs-lookup"><span data-stu-id="a8730-632">16</span></span>| <span data-ttu-id="a8730-633">16</span><span class="sxs-lookup"><span data-stu-id="a8730-633">16</span></span>| <span data-ttu-id="a8730-634">16</span><span class="sxs-lookup"><span data-stu-id="a8730-634">16</span></span>| <span data-ttu-id="a8730-635">16</span><span class="sxs-lookup"><span data-stu-id="a8730-635">16</span></span>|
| <span data-ttu-id="a8730-636">DW1000</span><span class="sxs-lookup"><span data-stu-id="a8730-636">DW1000</span></span> | <span data-ttu-id="a8730-637">32</span><span class="sxs-lookup"><span data-stu-id="a8730-637">32</span></span>| <span data-ttu-id="a8730-638">40</span><span class="sxs-lookup"><span data-stu-id="a8730-638">40</span></span>| <span data-ttu-id="a8730-639">1</span><span class="sxs-lookup"><span data-stu-id="a8730-639">1</span></span>| <span data-ttu-id="a8730-640">2</span><span class="sxs-lookup"><span data-stu-id="a8730-640">2</span></span>| <span data-ttu-id="a8730-641">4</span><span class="sxs-lookup"><span data-stu-id="a8730-641">4</span></span>| <span data-ttu-id="a8730-642">8</span><span class="sxs-lookup"><span data-stu-id="a8730-642">8</span></span>| <span data-ttu-id="a8730-643">16</span><span class="sxs-lookup"><span data-stu-id="a8730-643">16</span></span>| <span data-ttu-id="a8730-644">32</span><span class="sxs-lookup"><span data-stu-id="a8730-644">32</span></span>| <span data-ttu-id="a8730-645">32</span><span class="sxs-lookup"><span data-stu-id="a8730-645">32</span></span>| <span data-ttu-id="a8730-646">32</span><span class="sxs-lookup"><span data-stu-id="a8730-646">32</span></span>|
| <span data-ttu-id="a8730-647">DW1200</span><span class="sxs-lookup"><span data-stu-id="a8730-647">DW1200</span></span> | <span data-ttu-id="a8730-648">32</span><span class="sxs-lookup"><span data-stu-id="a8730-648">32</span></span>| <span data-ttu-id="a8730-649">48</span><span class="sxs-lookup"><span data-stu-id="a8730-649">48</span></span>| <span data-ttu-id="a8730-650">1</span><span class="sxs-lookup"><span data-stu-id="a8730-650">1</span></span>| <span data-ttu-id="a8730-651">2</span><span class="sxs-lookup"><span data-stu-id="a8730-651">2</span></span>| <span data-ttu-id="a8730-652">4</span><span class="sxs-lookup"><span data-stu-id="a8730-652">4</span></span>| <span data-ttu-id="a8730-653">8</span><span class="sxs-lookup"><span data-stu-id="a8730-653">8</span></span>| <span data-ttu-id="a8730-654">16</span><span class="sxs-lookup"><span data-stu-id="a8730-654">16</span></span>| <span data-ttu-id="a8730-655">32</span><span class="sxs-lookup"><span data-stu-id="a8730-655">32</span></span>| <span data-ttu-id="a8730-656">32</span><span class="sxs-lookup"><span data-stu-id="a8730-656">32</span></span>| <span data-ttu-id="a8730-657">32</span><span class="sxs-lookup"><span data-stu-id="a8730-657">32</span></span>|
| <span data-ttu-id="a8730-658">DW1500</span><span class="sxs-lookup"><span data-stu-id="a8730-658">DW1500</span></span> | <span data-ttu-id="a8730-659">32</span><span class="sxs-lookup"><span data-stu-id="a8730-659">32</span></span>| <span data-ttu-id="a8730-660">60</span><span class="sxs-lookup"><span data-stu-id="a8730-660">60</span></span>| <span data-ttu-id="a8730-661">1</span><span class="sxs-lookup"><span data-stu-id="a8730-661">1</span></span>| <span data-ttu-id="a8730-662">2</span><span class="sxs-lookup"><span data-stu-id="a8730-662">2</span></span>| <span data-ttu-id="a8730-663">4</span><span class="sxs-lookup"><span data-stu-id="a8730-663">4</span></span>| <span data-ttu-id="a8730-664">8</span><span class="sxs-lookup"><span data-stu-id="a8730-664">8</span></span>| <span data-ttu-id="a8730-665">16</span><span class="sxs-lookup"><span data-stu-id="a8730-665">16</span></span>| <span data-ttu-id="a8730-666">32</span><span class="sxs-lookup"><span data-stu-id="a8730-666">32</span></span>| <span data-ttu-id="a8730-667">32</span><span class="sxs-lookup"><span data-stu-id="a8730-667">32</span></span>| <span data-ttu-id="a8730-668">32</span><span class="sxs-lookup"><span data-stu-id="a8730-668">32</span></span>|
| <span data-ttu-id="a8730-669">DW2000</span><span class="sxs-lookup"><span data-stu-id="a8730-669">DW2000</span></span> | <span data-ttu-id="a8730-670">32</span><span class="sxs-lookup"><span data-stu-id="a8730-670">32</span></span>| <span data-ttu-id="a8730-671">80</span><span class="sxs-lookup"><span data-stu-id="a8730-671">80</span></span>| <span data-ttu-id="a8730-672">1</span><span class="sxs-lookup"><span data-stu-id="a8730-672">1</span></span>| <span data-ttu-id="a8730-673">2</span><span class="sxs-lookup"><span data-stu-id="a8730-673">2</span></span>| <span data-ttu-id="a8730-674">4</span><span class="sxs-lookup"><span data-stu-id="a8730-674">4</span></span>| <span data-ttu-id="a8730-675">8</span><span class="sxs-lookup"><span data-stu-id="a8730-675">8</span></span>| <span data-ttu-id="a8730-676">16</span><span class="sxs-lookup"><span data-stu-id="a8730-676">16</span></span>| <span data-ttu-id="a8730-677">32</span><span class="sxs-lookup"><span data-stu-id="a8730-677">32</span></span>| <span data-ttu-id="a8730-678">64</span><span class="sxs-lookup"><span data-stu-id="a8730-678">64</span></span>| <span data-ttu-id="a8730-679">64</span><span class="sxs-lookup"><span data-stu-id="a8730-679">64</span></span>|
| <span data-ttu-id="a8730-680">DW3000</span><span class="sxs-lookup"><span data-stu-id="a8730-680">DW3000</span></span> | <span data-ttu-id="a8730-681">32</span><span class="sxs-lookup"><span data-stu-id="a8730-681">32</span></span>| <span data-ttu-id="a8730-682">120</span><span class="sxs-lookup"><span data-stu-id="a8730-682">120</span></span>| <span data-ttu-id="a8730-683">1</span><span class="sxs-lookup"><span data-stu-id="a8730-683">1</span></span>| <span data-ttu-id="a8730-684">2</span><span class="sxs-lookup"><span data-stu-id="a8730-684">2</span></span>| <span data-ttu-id="a8730-685">4</span><span class="sxs-lookup"><span data-stu-id="a8730-685">4</span></span>| <span data-ttu-id="a8730-686">8</span><span class="sxs-lookup"><span data-stu-id="a8730-686">8</span></span>| <span data-ttu-id="a8730-687">16</span><span class="sxs-lookup"><span data-stu-id="a8730-687">16</span></span>| <span data-ttu-id="a8730-688">32</span><span class="sxs-lookup"><span data-stu-id="a8730-688">32</span></span>| <span data-ttu-id="a8730-689">64</span><span class="sxs-lookup"><span data-stu-id="a8730-689">64</span></span>| <span data-ttu-id="a8730-690">64</span><span class="sxs-lookup"><span data-stu-id="a8730-690">64</span></span>|
| <span data-ttu-id="a8730-691">DW6000</span><span class="sxs-lookup"><span data-stu-id="a8730-691">DW6000</span></span> | <span data-ttu-id="a8730-692">32</span><span class="sxs-lookup"><span data-stu-id="a8730-692">32</span></span>| <span data-ttu-id="a8730-693">240</span><span class="sxs-lookup"><span data-stu-id="a8730-693">240</span></span>| <span data-ttu-id="a8730-694">1</span><span class="sxs-lookup"><span data-stu-id="a8730-694">1</span></span>| <span data-ttu-id="a8730-695">2</span><span class="sxs-lookup"><span data-stu-id="a8730-695">2</span></span>| <span data-ttu-id="a8730-696">4</span><span class="sxs-lookup"><span data-stu-id="a8730-696">4</span></span>| <span data-ttu-id="a8730-697">8</span><span class="sxs-lookup"><span data-stu-id="a8730-697">8</span></span>| <span data-ttu-id="a8730-698">16</span><span class="sxs-lookup"><span data-stu-id="a8730-698">16</span></span>| <span data-ttu-id="a8730-699">32</span><span class="sxs-lookup"><span data-stu-id="a8730-699">32</span></span>| <span data-ttu-id="a8730-700">64</span><span class="sxs-lookup"><span data-stu-id="a8730-700">64</span></span>| <span data-ttu-id="a8730-701">128</span><span class="sxs-lookup"><span data-stu-id="a8730-701">128</span></span>|

<span data-ttu-id="a8730-702">Nestas tabelas, você pode ver que um SQL Data Warehouse em execução como DW1000 aloca uma quantidade máxima de 32 consultas simultâneas e um total de 40 slots de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="a8730-702">From these tables, you can see that SQL Data Warehouse running as DW1000 allocates a maximum of 32 concurrent queries and a total of 40 concurrency slots.</span></span> <span data-ttu-id="a8730-703">Se todos os usuários estivessem em execução no smallrc, seriam permitidas 32 consultas simultâneas, pois cada consulta consumiria um slot de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="a8730-703">If all users are running in smallrc, 32 concurrent queries would be allowed because each query would consume 1 concurrency slot.</span></span> <span data-ttu-id="a8730-704">Se todos os usuários em um DW1000 estivessem em execução na mediumrc, cada consulta receberia a alocação de 800 MB por distribuição de uma alocação de memória total de 47 GB por consulta e a simultaneidade seria limitada a cinco usuários (40 slots de simultaneidade/oito slots por usuário mediumrc).</span><span class="sxs-lookup"><span data-stu-id="a8730-704">If all users on a DW1000 were running in mediumrc, each query would be allocated 800 MB per distribution for a total memory allocation of 47 GB per query, and concurrency would be limited to 5 users (40 concurrency slots / 8 slots per mediumrc user).</span></span>

## <a name="selecting-proper-resource-class"></a><span data-ttu-id="a8730-705">Selecionando a classe de recursos apropriada</span><span class="sxs-lookup"><span data-stu-id="a8730-705">Selecting proper resource class</span></span>  
<span data-ttu-id="a8730-706">Uma prática recomendada é atribuir usuários permanentemente a uma classe de recurso em vez de alterar suas classes de recurso.</span><span class="sxs-lookup"><span data-stu-id="a8730-706">A good practice is to permanently assign users to a resource class rather than changing their resource classes.</span></span> <span data-ttu-id="a8730-707">Por exemplo, cargas para tabelas columnstore clusterizadas cria índices de qualidade superiores quando mais memória é alocada.</span><span class="sxs-lookup"><span data-stu-id="a8730-707">For example, loads to clustered columnstore tables create higher-quality indexes when allocated more memory.</span></span> <span data-ttu-id="a8730-708">Para garantir que as cargas tenham acesso a mais memória, crie um usuário especificamente para o carregamento de dados e atribua esse usuário permanentemente a uma classe de recurso mais elevada.</span><span class="sxs-lookup"><span data-stu-id="a8730-708">To ensure that loads have access to higher memory, create a user specifically for loading data and permanently assign this user to a higher resource class.</span></span>
<span data-ttu-id="a8730-709">Há algumas melhores práticas a serem seguidas aqui.</span><span class="sxs-lookup"><span data-stu-id="a8730-709">There are a couple of best practices to follow here.</span></span> <span data-ttu-id="a8730-710">Como mencionado acima, o SQL DW dá suporte a dois tipos de classes de recursos: classes de recursos estáticos e classes de recursos dinâmicos.</span><span class="sxs-lookup"><span data-stu-id="a8730-710">As mentioned above, SQL DW supports two kinds of resource class types: static resource classes and dynamic resource classes.</span></span>
### <a name="loading-best-practices"></a><span data-ttu-id="a8730-711">Melhores práticas de carregamento</span><span class="sxs-lookup"><span data-stu-id="a8730-711">Loading best practices</span></span>
1.  <span data-ttu-id="a8730-712">Se as expectativas forem de carregamentos com uma quantidade de dados regular, uma classe de recursos estáticos é uma boa opção.</span><span class="sxs-lookup"><span data-stu-id="a8730-712">If the expectations are loads with regular amount of data, a static resource class is a good choice.</span></span> <span data-ttu-id="a8730-713">Posteriormente, ao escalar verticalmente para obter mais capacidade de computação, o data warehouse poderá executar consultas mais simultâneas de imediato, uma vez que o usuário do carregamento não consome mais memória.</span><span class="sxs-lookup"><span data-stu-id="a8730-713">Later, when scaling up to get more computational power, the data warehouse will be able to run more concurrent queries out-of-the-box, as the load user does not consume more memory.</span></span>
2.  <span data-ttu-id="a8730-714">Se as expectativas forem de carregamentos maiores em algumas ocasiões, uma classe de recursos dinâmicos será uma boa opção.</span><span class="sxs-lookup"><span data-stu-id="a8730-714">If the expectations are bigger loads in some occasions, a dynamic resource class is a good choice.</span></span> <span data-ttu-id="a8730-715">Posteriormente, ao escalar verticalmente para obter mais capacidade de computação, o usuário do carregamento obterá mais memória de pronto, permitindo assim que o carregamento seja realizado mais rápido.</span><span class="sxs-lookup"><span data-stu-id="a8730-715">Later, when scaling up to get more computational power, the load user will get more memory out-of-the-box, hence allowing the load to perform faster.</span></span>

<span data-ttu-id="a8730-716">A memória necessária para processar cargas com eficiência depende da natureza da tabela carregada e da quantidade de dados processada.</span><span class="sxs-lookup"><span data-stu-id="a8730-716">The memory needed to process loads efficiently depends on the nature of the table loaded and the amount of data processed.</span></span> <span data-ttu-id="a8730-717">Por exemplo, carregar dados em tabelas CCI requer memória para permitir que os rowgroups CCI atinjam o nível ideal.</span><span class="sxs-lookup"><span data-stu-id="a8730-717">For instance, loading data into CCI tables requires some memory to let CCI rowgroups reach optimality.</span></span> <span data-ttu-id="a8730-718">Para obter mais detalhes, consulte os Índices columnstore – diretrizes de carregamento de dados.</span><span class="sxs-lookup"><span data-stu-id="a8730-718">For more details, see the Columnstore indexes - data loading guidance.</span></span>

<span data-ttu-id="a8730-719">Como uma melhor prática, é recomendável usar pelo menos 200 MB de memória para os carregamentos.</span><span class="sxs-lookup"><span data-stu-id="a8730-719">As a best practice, we advise you to use at least 200MB of memory for loads.</span></span>

### <a name="querying-best-practices"></a><span data-ttu-id="a8730-720">Melhores práticas de consulta</span><span class="sxs-lookup"><span data-stu-id="a8730-720">Querying best practices</span></span>
<span data-ttu-id="a8730-721">As consultas têm requisitos diferentes dependendo de sua complexidade.</span><span class="sxs-lookup"><span data-stu-id="a8730-721">Queries have different requirements depending on their complexity.</span></span> <span data-ttu-id="a8730-722">Aumentar a memória por consulta ou aumentar a simultaneidade são duas formas válidas para aumentar a produtividade geral dependendo das necessidades da consulta.</span><span class="sxs-lookup"><span data-stu-id="a8730-722">Increasing memory per query or increasing the concurrency are both valid ways to augment overall throughput depending on the query needs.</span></span>
1.  <span data-ttu-id="a8730-723">Se as expectativas forem consultas complexas e regulares (por exemplo, para gerar relatórios diários e semanais) e não precisarem aproveitar a simultaneidade, uma classe de recursos dinâmicos será uma boa opção.</span><span class="sxs-lookup"><span data-stu-id="a8730-723">If the expectations are regular, complex queries (for instance, to generate daily and weekly reports) and do not need to take advantage of concurrency, a dynamic resource class is a good choice.</span></span> <span data-ttu-id="a8730-724">Se o sistema tiver mais dados a serem processados, escalar verticalmente o data warehouse fornecerá automaticamente mais memória para o usuário executando a consulta.</span><span class="sxs-lookup"><span data-stu-id="a8730-724">If the system has more data to process, scaling up the data warehouse will therefore automatically provide more memory to the user running the query.</span></span>
2.  <span data-ttu-id="a8730-725">Se as expectativas forem padrões de simultaneidade variáveis ou cotidianas (por exemplo, se o banco de dados for consultado por meio de uma interface do usuário Web amplamente acessível), uma classe de recursos estáticos será uma boa opção.</span><span class="sxs-lookup"><span data-stu-id="a8730-725">If the expectations are variable or diurnal concurrency patterns (for instance if the database is queried through a web UI broadly accessible), a static resource class is a good choice.</span></span> <span data-ttu-id="a8730-726">Posteriormente, ao escalar verticalmente para o data warehouse, o usuário associado à classe de recursos estáticos automaticamente poderá executar mais consultas simultâneas.</span><span class="sxs-lookup"><span data-stu-id="a8730-726">Later, when scaling up to data warehouse, the user associated with the static resource class will automatically be able to run more concurrent queries.</span></span>

<span data-ttu-id="a8730-727">Selecionar a concessão de memória apropriada dependendo da necessidade de sua consulta não é simples, uma vez que depende de muitos fatores, como a quantidade de dados consultada, a natureza dos esquemas de tabela e vários predicados de união, seleção e agrupamento.</span><span class="sxs-lookup"><span data-stu-id="a8730-727">Selecting proper memory grant depending on the need of your query is non-trivial, as it depends on many factors, such as the amount of data queried, the nature of the table schemas, and various join, selection, and group predicates.</span></span> <span data-ttu-id="a8730-728">Do ponto de vista geral, alocar mais memória permitirá que consultas sejam concluídas mais rapidamente, mas reduzirá a simultaneidade geral.</span><span class="sxs-lookup"><span data-stu-id="a8730-728">From a general standpoint, allocating more memory will allow queries to complete faster, but would reduce the overall concurrency.</span></span> <span data-ttu-id="a8730-729">Se a simultaneidade não for um problema, a alocação excessiva de memória não será prejudicial.</span><span class="sxs-lookup"><span data-stu-id="a8730-729">If concurrency is not an issue, over-allocating memory does not harm.</span></span> <span data-ttu-id="a8730-730">Para ajustar a taxa de transferência, a tentativa de vários tipos de classes de recursos pode ser necessária.</span><span class="sxs-lookup"><span data-stu-id="a8730-730">To fine-tune throughput, trying various flavors of resource classes may be required.</span></span>

<span data-ttu-id="a8730-731">Você pode usar o procedimento armazenado a seguir para descobrir a concessão de memória e a simultaneidade por classe de recursos em um determinado SLO e a melhor classe de recursos mais próxima para operações de CCI de uso intenso da memória em uma tabela CCI não particionada em uma determinada classe de recursos:</span><span class="sxs-lookup"><span data-stu-id="a8730-731">You can use the following stored procedure to figure out concurrency and memory grant per resource class at a given SLO and the closest best resource class for memory intensive CCI operations on non-partitioned CCI table at a given resource class:</span></span>

#### <a name="description"></a><span data-ttu-id="a8730-732">Descrição:</span><span class="sxs-lookup"><span data-stu-id="a8730-732">Description:</span></span>  
<span data-ttu-id="a8730-733">Aqui está a finalidade deste procedimento armazenado:</span><span class="sxs-lookup"><span data-stu-id="a8730-733">Here's the purpose of this stored procedure:</span></span>  
1. <span data-ttu-id="a8730-734">Ajudar o usuário a descobrir a simultaneidade e a concessão de memória por classe de recursos em um determinado SLO.</span><span class="sxs-lookup"><span data-stu-id="a8730-734">To help user figure out concurrency and memory grant per resource class at a given SLO.</span></span> <span data-ttu-id="a8730-735">O usuário precisa fornecer NULL para o esquema e tablename para isso, conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="a8730-735">User needs to provide NULL for both schema and tablename for this as shown in the example below.</span></span>  
2. <span data-ttu-id="a8730-736">Ajudar o usuário a descobrir a melhor classe de recursos mais próxima para operações de CCI de uso intenso de memória (carregar, copiar tabela, recompilar índice etc.) na tabela CCI não particionada em uma determinada classe de recursos.</span><span class="sxs-lookup"><span data-stu-id="a8730-736">To help user figure out the closest best resource class for the memory intensed CCI operations (load, copy table, rebuild index, etc.) on non partitioned CCI table at a given resource class.</span></span> <span data-ttu-id="a8730-737">O procedimento armazenado usa o esquema da tabela para descobrir a concessão de memória necessária para isso.</span><span class="sxs-lookup"><span data-stu-id="a8730-737">The stored proc uses table schema to find out the required memory grant for this.</span></span>

#### <a name="dependencies--restrictions"></a><span data-ttu-id="a8730-738">Dependências e restrições:</span><span class="sxs-lookup"><span data-stu-id="a8730-738">Dependencies & Restrictions:</span></span>
- <span data-ttu-id="a8730-739">Esse procedimento armazenado não foi projetado para calcular os requisitos de memória para a tabela CCI particionada.</span><span class="sxs-lookup"><span data-stu-id="a8730-739">This stored proc is not designed to calculate memory requirement for partitioned-cci table.</span></span>    
- <span data-ttu-id="a8730-740">Esse procedimento armazenado não considera os requisitos de memória para a parte SELECT de CTAS/INSERT-SELECT e pressupõe que sejam um simples SELECT.</span><span class="sxs-lookup"><span data-stu-id="a8730-740">This stored proc doesn't take memory requirement into account for the SELECT part of CTAS/INSERT-SELECT and assumes it to be a simple SELECT.</span></span>
- <span data-ttu-id="a8730-741">Esse procedimento armazenado usa uma tabela temporária para que possa ser usada na sessão em que esse procedimento armazenado foi criado.</span><span class="sxs-lookup"><span data-stu-id="a8730-741">This stored proc uses a temp table so this can be used in the session where this stored proc was created.</span></span>    
- <span data-ttu-id="a8730-742">Esse procedimento armazenado depende das ofertas atuais (por exemplo, a configuração de hardware, a configuração DMS) e se qualquer uma delas for alterada, esse procedimento armazenado não funcionará corretamente.</span><span class="sxs-lookup"><span data-stu-id="a8730-742">This stored proc depends on the current offerings (e.g. hardware configuration, DMS config) and if any of that changes then this stored proc would not work correctly.</span></span>  
- <span data-ttu-id="a8730-743">Esse procedimento armazenado depende do limite de simultaneidade oferecidos existente e se isso mudar, o procedimento armazenado não funcionará corretamente.</span><span class="sxs-lookup"><span data-stu-id="a8730-743">This stored proc depends on existing offered concurrency limit and if that changes then this stored proc would not work correctly.</span></span>  
- <span data-ttu-id="a8730-744">Esse procedimento armazenado depende das ofertas de classe de recursos existentes e se isso mudar, o procedimento armazenado não funcionará corretamente.</span><span class="sxs-lookup"><span data-stu-id="a8730-744">This stored proc depends on existing resource class offerings and if that changes then this stored proc wuold not work correctly.</span></span>  

>  [!NOTE]  
>  <span data-ttu-id="a8730-745">Se nenhuma saída aparecer após a execução do procedimento armazenado com parâmetros fornecidos, isso poderá ser consequência de dois problemas.</span><span class="sxs-lookup"><span data-stu-id="a8730-745">If you are not getting output after executing stored procedure with parameters provided then there could be two cases.</span></span> <br /><span data-ttu-id="a8730-746">1. Um parâmetro de DW contém o valor inválido de SLO</span><span class="sxs-lookup"><span data-stu-id="a8730-746">1. Either DW Parameter contains invalid SLO value</span></span> <br /><span data-ttu-id="a8730-747">2. OU não há nenhuma classe de recurso correspondente para a operação CCI se o nome de tabela tiver sido fornecido.</span><span class="sxs-lookup"><span data-stu-id="a8730-747">2. OR there are no matching resource class for CCI operation if table name was provided.</span></span> <br /><span data-ttu-id="a8730-748">Por exemplo, no DW100, a concessão de memória mais alta disponível é 400 MB e se o esquema de tabela for grande o suficiente para atravessar o requisito de 400 MB.</span><span class="sxs-lookup"><span data-stu-id="a8730-748">For example, at DW100, highest memory grant available is 400MB and if table schema is wide enough to cross the requirement of 400MB.</span></span>
      
#### <a name="usage-example"></a><span data-ttu-id="a8730-749">Exemplo de uso:</span><span class="sxs-lookup"><span data-stu-id="a8730-749">Usage example:</span></span>
<span data-ttu-id="a8730-750">Sintaxe:</span><span class="sxs-lookup"><span data-stu-id="a8730-750">Syntax:</span></span>  
`EXEC dbo.prc_workload_management_by_DWU @DWU VARCHAR(7), @SCHEMA_NAME VARCHAR(128), @TABLE_NAME VARCHAR(128)`  
1. <span data-ttu-id="a8730-751">@DWU: Forneça um parâmetro NULL para extrair a DWU atual do BD do DW ou forneça uma DWU compatível na forma de 'DW100'</span><span class="sxs-lookup"><span data-stu-id="a8730-751">@DWU: Either provide a NULL parameter to extract the current DWU from the DW DB or provide any supported DWU in the form of 'DW100'</span></span>
2. <span data-ttu-id="a8730-752">@SCHEMA_NAME: Forneça um nome de esquema da tabela</span><span class="sxs-lookup"><span data-stu-id="a8730-752">@SCHEMA_NAME: Provide a schema name of the table</span></span>
3. <span data-ttu-id="a8730-753">@TABLE_NAME: Forneça um nome de tabela dos juros</span><span class="sxs-lookup"><span data-stu-id="a8730-753">@TABLE_NAME: Provide a table name of the interest</span></span>

<span data-ttu-id="a8730-754">Exemplos executando esse procedimento armazenado:</span><span class="sxs-lookup"><span data-stu-id="a8730-754">Examples executing this stored proc:</span></span>  
```sql  
EXEC dbo.prc_workload_management_by_DWU 'DW2000', 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU NULL, 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU 'DW6000', NULL, NULL;  
EXEC dbo.prc_workload_management_by_DWU NULL, NULL, NULL;  
```

<span data-ttu-id="a8730-755">A Table1 usada nos exemplos acima pode ser criado como abaixo:</span><span class="sxs-lookup"><span data-stu-id="a8730-755">Table1 used in the above examples could be created as below:</span></span>  
`CREATE TABLE Table1 (a int, b varchar(50), c decimal (18,10), d char(10), e varbinary(15), f float, g datetime, h date);`

#### <a name="heres-the-stored-procedure-definition"></a><span data-ttu-id="a8730-756">Aqui está a definição do procedimento armazenado:</span><span class="sxs-lookup"><span data-stu-id="a8730-756">Here's the stored procedure definition:</span></span>
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
-- Selecting proper DWU for the current DB if not specified.
SET @DWU = (
  SELECT 'DW'+CAST(COUNT(*)*100 AS VARCHAR(10))
  FROM sys.dm_pdw_nodes
  WHERE type = 'COMPUTE')
END

DECLARE @DWU_NUM INT
SET @DWU_NUM = CAST (SUBSTRING(@DWU, 3, LEN(@DWU)-2) AS INT)

-- Raise error if either schema name or table name is supplied but not both them supplied
--IF ((@SCHEMA_NAME IS NOT NULL AND @TABLE_NAME IS NULL) OR (@TABLE_NAME IS NULL AND @SCHEMA_NAME IS NOT NULL))
--     RAISEERROR('User need to supply either both Schema Name and Table Name or none of them')
       
-- Dropping temp table if exists.
IF OBJECT_ID('tempdb..#ref') IS NOT NULL
BEGIN
  DROP TABLE #ref;
END

-- Creating ref. temptable (CTAS) to hold mapping info.
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
-- Creating workload mapping to their corresponding slot consumption and default memory grant.
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

## <a name="query-importance"></a><span data-ttu-id="a8730-757">Importância da consulta</span><span class="sxs-lookup"><span data-stu-id="a8730-757">Query importance</span></span>
<span data-ttu-id="a8730-758">O SQL Data Warehouse implementa classes de recursos usando grupos de carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="a8730-758">SQL Data Warehouse implements resource classes by using workload groups.</span></span> <span data-ttu-id="a8730-759">Há um total de oito grupos de carga de trabalho que controlam o comportamento das classes de recurso entre os vários tamanhos de DWU.</span><span class="sxs-lookup"><span data-stu-id="a8730-759">There are a total of eight workload groups that control the behavior of the resource classes across the various DWU sizes.</span></span> <span data-ttu-id="a8730-760">Para qualquer DWU, o SQL Data Warehouse usa somente quatro dos oito grupos de carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="a8730-760">For any DWU, SQL Data Warehouse uses only four of the eight workload groups.</span></span> <span data-ttu-id="a8730-761">Isso faz sentido, pois cada grupo de carga de trabalho é atribuído a uma das quatro classes de recurso: smallrc, mediumrc, largerc ou xlargerc.</span><span class="sxs-lookup"><span data-stu-id="a8730-761">This makes sense because each workload group is assigned to one of four resource classes: smallrc, mediumrc, largerc, or xlargerc.</span></span> <span data-ttu-id="a8730-762">A importância de entender esses grupos de carga de trabalho é que alguns deles são definidos com *importância*maior.</span><span class="sxs-lookup"><span data-stu-id="a8730-762">The importance of understanding the workload groups is that some of these workload groups are set to higher *importance*.</span></span> <span data-ttu-id="a8730-763">A importância é usada para agendamento de CPU.</span><span class="sxs-lookup"><span data-stu-id="a8730-763">Importance is used for CPU scheduling.</span></span> <span data-ttu-id="a8730-764">As consultas executadas com importância alta obterão três vezes mais ciclos de CPU do que aquelas com importância média.</span><span class="sxs-lookup"><span data-stu-id="a8730-764">Queries run with high importance will get three times more CPU cycles than those with medium importance.</span></span> <span data-ttu-id="a8730-765">Portanto, os mapeamentos de slot de simultaneidade também determinam a prioridade da CPU.</span><span class="sxs-lookup"><span data-stu-id="a8730-765">Therefore, concurrency slot mappings also determine CPU priority.</span></span> <span data-ttu-id="a8730-766">Quando uma consulta consome 16 ou mais slots, ela é executada com alta importância.</span><span class="sxs-lookup"><span data-stu-id="a8730-766">When a query consumes 16 or more slots, it runs as high importance.</span></span>

<span data-ttu-id="a8730-767">A tabela a seguir mostra os mapeamentos de importância para cada grupo de carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="a8730-767">The following table shows the importance mappings for each workload group.</span></span>

### <a name="workload-group-mappings-to-concurrency-slots-and-importance"></a><span data-ttu-id="a8730-768">Mapeamentos de grupo de carga de trabalho para slots de simultaneidade e importância</span><span class="sxs-lookup"><span data-stu-id="a8730-768">Workload group mappings to concurrency slots and importance</span></span>
| <span data-ttu-id="a8730-769">Grupos de carga de trabalho</span><span class="sxs-lookup"><span data-stu-id="a8730-769">Workload groups</span></span> | <span data-ttu-id="a8730-770">Mapeamento do slot de simultaneidade</span><span class="sxs-lookup"><span data-stu-id="a8730-770">Concurrency slot mapping</span></span> | <span data-ttu-id="a8730-771">MB / Distribuição</span><span class="sxs-lookup"><span data-stu-id="a8730-771">MB / Distribution</span></span> | <span data-ttu-id="a8730-772">Mapeamento de importância</span><span class="sxs-lookup"><span data-stu-id="a8730-772">Importance mapping</span></span> |
|:--- |:---:|:---:|:--- |
| <span data-ttu-id="a8730-773">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="a8730-773">SloDWGroupC00</span></span> |<span data-ttu-id="a8730-774">1</span><span class="sxs-lookup"><span data-stu-id="a8730-774">1</span></span> |<span data-ttu-id="a8730-775">100</span><span class="sxs-lookup"><span data-stu-id="a8730-775">100</span></span> |<span data-ttu-id="a8730-776">Média</span><span class="sxs-lookup"><span data-stu-id="a8730-776">Medium</span></span> |
| <span data-ttu-id="a8730-777">SloDWGroupC01</span><span class="sxs-lookup"><span data-stu-id="a8730-777">SloDWGroupC01</span></span> |<span data-ttu-id="a8730-778">2</span><span class="sxs-lookup"><span data-stu-id="a8730-778">2</span></span> |<span data-ttu-id="a8730-779">200</span><span class="sxs-lookup"><span data-stu-id="a8730-779">200</span></span> |<span data-ttu-id="a8730-780">Média</span><span class="sxs-lookup"><span data-stu-id="a8730-780">Medium</span></span> |
| <span data-ttu-id="a8730-781">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="a8730-781">SloDWGroupC02</span></span> |<span data-ttu-id="a8730-782">4</span><span class="sxs-lookup"><span data-stu-id="a8730-782">4</span></span> |<span data-ttu-id="a8730-783">400</span><span class="sxs-lookup"><span data-stu-id="a8730-783">400</span></span> |<span data-ttu-id="a8730-784">Média</span><span class="sxs-lookup"><span data-stu-id="a8730-784">Medium</span></span> |
| <span data-ttu-id="a8730-785">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="a8730-785">SloDWGroupC03</span></span> |<span data-ttu-id="a8730-786">8</span><span class="sxs-lookup"><span data-stu-id="a8730-786">8</span></span> |<span data-ttu-id="a8730-787">800</span><span class="sxs-lookup"><span data-stu-id="a8730-787">800</span></span> |<span data-ttu-id="a8730-788">Média</span><span class="sxs-lookup"><span data-stu-id="a8730-788">Medium</span></span> |
| <span data-ttu-id="a8730-789">SloDWGroupC04</span><span class="sxs-lookup"><span data-stu-id="a8730-789">SloDWGroupC04</span></span> |<span data-ttu-id="a8730-790">16</span><span class="sxs-lookup"><span data-stu-id="a8730-790">16</span></span> |<span data-ttu-id="a8730-791">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-791">1,600</span></span> |<span data-ttu-id="a8730-792">Alto</span><span class="sxs-lookup"><span data-stu-id="a8730-792">High</span></span> |
| <span data-ttu-id="a8730-793">SloDWGroupC05</span><span class="sxs-lookup"><span data-stu-id="a8730-793">SloDWGroupC05</span></span> |<span data-ttu-id="a8730-794">32</span><span class="sxs-lookup"><span data-stu-id="a8730-794">32</span></span> |<span data-ttu-id="a8730-795">3.200</span><span class="sxs-lookup"><span data-stu-id="a8730-795">3,200</span></span> |<span data-ttu-id="a8730-796">Alto</span><span class="sxs-lookup"><span data-stu-id="a8730-796">High</span></span> |
| <span data-ttu-id="a8730-797">SloDWGroupC06</span><span class="sxs-lookup"><span data-stu-id="a8730-797">SloDWGroupC06</span></span> |<span data-ttu-id="a8730-798">64</span><span class="sxs-lookup"><span data-stu-id="a8730-798">64</span></span> |<span data-ttu-id="a8730-799">6.400</span><span class="sxs-lookup"><span data-stu-id="a8730-799">6,400</span></span> |<span data-ttu-id="a8730-800">Alto</span><span class="sxs-lookup"><span data-stu-id="a8730-800">High</span></span> |
| <span data-ttu-id="a8730-801">SloDWGroupC07</span><span class="sxs-lookup"><span data-stu-id="a8730-801">SloDWGroupC07</span></span> |<span data-ttu-id="a8730-802">128</span><span class="sxs-lookup"><span data-stu-id="a8730-802">128</span></span> |<span data-ttu-id="a8730-803">12.800</span><span class="sxs-lookup"><span data-stu-id="a8730-803">12,800</span></span> |<span data-ttu-id="a8730-804">Alto</span><span class="sxs-lookup"><span data-stu-id="a8730-804">High</span></span> |

<span data-ttu-id="a8730-805">Da tabela **Alocação e consumo de slots de simultaneidade** , podemos ver que um DW500 usa um, quatro, oito ou 16 slots de simultaneidade para smallrc, mediumrc, largerc e xlargerc, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="a8730-805">From the **Allocation and consumption of concurrency slots** chart, you can see that a DW500 uses 1, 4, 8 or 16 concurrency slots for smallrc, mediumrc, largerc, and xlargerc, respectively.</span></span> <span data-ttu-id="a8730-806">Você pode procurar esses valores na tabela anterior para localizar a importância de cada classe de recurso.</span><span class="sxs-lookup"><span data-stu-id="a8730-806">You can look those values up in the preceding chart to find the importance for each resource class.</span></span>

### <a name="dw500-mapping-of-resource-classes-to-importance"></a><span data-ttu-id="a8730-807">Mapeamento do DW500 para obter a importância das classes de recurso</span><span class="sxs-lookup"><span data-stu-id="a8730-807">DW500 mapping of resource classes to importance</span></span>
| <span data-ttu-id="a8730-808">classe de recurso</span><span class="sxs-lookup"><span data-stu-id="a8730-808">Resource class</span></span> | <span data-ttu-id="a8730-809">Grupo de carga de trabalho</span><span class="sxs-lookup"><span data-stu-id="a8730-809">Workload group</span></span> | <span data-ttu-id="a8730-810">Slots de simultaneidade usados</span><span class="sxs-lookup"><span data-stu-id="a8730-810">Concurrency slots used</span></span> | <span data-ttu-id="a8730-811">MB / Distribuição</span><span class="sxs-lookup"><span data-stu-id="a8730-811">MB / Distribution</span></span> | <span data-ttu-id="a8730-812">importância</span><span class="sxs-lookup"><span data-stu-id="a8730-812">Importance</span></span> |
|:--- |:--- |:---:|:---:|:--- |
| <span data-ttu-id="a8730-813">smallrc</span><span class="sxs-lookup"><span data-stu-id="a8730-813">smallrc</span></span> |<span data-ttu-id="a8730-814">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="a8730-814">SloDWGroupC00</span></span> |<span data-ttu-id="a8730-815">1</span><span class="sxs-lookup"><span data-stu-id="a8730-815">1</span></span> |<span data-ttu-id="a8730-816">100</span><span class="sxs-lookup"><span data-stu-id="a8730-816">100</span></span> |<span data-ttu-id="a8730-817">Média</span><span class="sxs-lookup"><span data-stu-id="a8730-817">Medium</span></span> |
| <span data-ttu-id="a8730-818">mediumrc</span><span class="sxs-lookup"><span data-stu-id="a8730-818">mediumrc</span></span> |<span data-ttu-id="a8730-819">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="a8730-819">SloDWGroupC02</span></span> |<span data-ttu-id="a8730-820">4</span><span class="sxs-lookup"><span data-stu-id="a8730-820">4</span></span> |<span data-ttu-id="a8730-821">400</span><span class="sxs-lookup"><span data-stu-id="a8730-821">400</span></span> |<span data-ttu-id="a8730-822">Média</span><span class="sxs-lookup"><span data-stu-id="a8730-822">Medium</span></span> |
| <span data-ttu-id="a8730-823">largerc</span><span class="sxs-lookup"><span data-stu-id="a8730-823">largerc</span></span> |<span data-ttu-id="a8730-824">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="a8730-824">SloDWGroupC03</span></span> |<span data-ttu-id="a8730-825">8</span><span class="sxs-lookup"><span data-stu-id="a8730-825">8</span></span> |<span data-ttu-id="a8730-826">800</span><span class="sxs-lookup"><span data-stu-id="a8730-826">800</span></span> |<span data-ttu-id="a8730-827">Média</span><span class="sxs-lookup"><span data-stu-id="a8730-827">Medium</span></span> |
| <span data-ttu-id="a8730-828">xlargerc</span><span class="sxs-lookup"><span data-stu-id="a8730-828">xlargerc</span></span> |<span data-ttu-id="a8730-829">SloDWGroupC04</span><span class="sxs-lookup"><span data-stu-id="a8730-829">SloDWGroupC04</span></span> |<span data-ttu-id="a8730-830">16</span><span class="sxs-lookup"><span data-stu-id="a8730-830">16</span></span> |<span data-ttu-id="a8730-831">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-831">1,600</span></span> |<span data-ttu-id="a8730-832">Alto</span><span class="sxs-lookup"><span data-stu-id="a8730-832">High</span></span> |
| <span data-ttu-id="a8730-833">staticrc10</span><span class="sxs-lookup"><span data-stu-id="a8730-833">staticrc10</span></span> |<span data-ttu-id="a8730-834">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="a8730-834">SloDWGroupC00</span></span> |<span data-ttu-id="a8730-835">1</span><span class="sxs-lookup"><span data-stu-id="a8730-835">1</span></span> |<span data-ttu-id="a8730-836">100</span><span class="sxs-lookup"><span data-stu-id="a8730-836">100</span></span> |<span data-ttu-id="a8730-837">Média</span><span class="sxs-lookup"><span data-stu-id="a8730-837">Medium</span></span> |
| <span data-ttu-id="a8730-838">staticrc20</span><span class="sxs-lookup"><span data-stu-id="a8730-838">staticrc20</span></span> |<span data-ttu-id="a8730-839">SloDWGroupC01</span><span class="sxs-lookup"><span data-stu-id="a8730-839">SloDWGroupC01</span></span> |<span data-ttu-id="a8730-840">2</span><span class="sxs-lookup"><span data-stu-id="a8730-840">2</span></span> |<span data-ttu-id="a8730-841">200</span><span class="sxs-lookup"><span data-stu-id="a8730-841">200</span></span> |<span data-ttu-id="a8730-842">Média</span><span class="sxs-lookup"><span data-stu-id="a8730-842">Medium</span></span> |
| <span data-ttu-id="a8730-843">staticrc30</span><span class="sxs-lookup"><span data-stu-id="a8730-843">staticrc30</span></span> |<span data-ttu-id="a8730-844">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="a8730-844">SloDWGroupC02</span></span> |<span data-ttu-id="a8730-845">4</span><span class="sxs-lookup"><span data-stu-id="a8730-845">4</span></span> |<span data-ttu-id="a8730-846">400</span><span class="sxs-lookup"><span data-stu-id="a8730-846">400</span></span> |<span data-ttu-id="a8730-847">Média</span><span class="sxs-lookup"><span data-stu-id="a8730-847">Medium</span></span> |
| <span data-ttu-id="a8730-848">staticrc40</span><span class="sxs-lookup"><span data-stu-id="a8730-848">staticrc40</span></span> |<span data-ttu-id="a8730-849">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="a8730-849">SloDWGroupC03</span></span> |<span data-ttu-id="a8730-850">8</span><span class="sxs-lookup"><span data-stu-id="a8730-850">8</span></span> |<span data-ttu-id="a8730-851">800</span><span class="sxs-lookup"><span data-stu-id="a8730-851">800</span></span> |<span data-ttu-id="a8730-852">Média</span><span class="sxs-lookup"><span data-stu-id="a8730-852">Medium</span></span> |
| <span data-ttu-id="a8730-853">staticrc50</span><span class="sxs-lookup"><span data-stu-id="a8730-853">staticrc50</span></span> |<span data-ttu-id="a8730-854">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="a8730-854">SloDWGroupC03</span></span> |<span data-ttu-id="a8730-855">16</span><span class="sxs-lookup"><span data-stu-id="a8730-855">16</span></span> |<span data-ttu-id="a8730-856">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-856">1,600</span></span> |<span data-ttu-id="a8730-857">Alto</span><span class="sxs-lookup"><span data-stu-id="a8730-857">High</span></span> |
| <span data-ttu-id="a8730-858">staticrc60</span><span class="sxs-lookup"><span data-stu-id="a8730-858">staticrc60</span></span> |<span data-ttu-id="a8730-859">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="a8730-859">SloDWGroupC03</span></span> |<span data-ttu-id="a8730-860">16</span><span class="sxs-lookup"><span data-stu-id="a8730-860">16</span></span> |<span data-ttu-id="a8730-861">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-861">1,600</span></span> |<span data-ttu-id="a8730-862">Alto</span><span class="sxs-lookup"><span data-stu-id="a8730-862">High</span></span> |
| <span data-ttu-id="a8730-863">staticrc70</span><span class="sxs-lookup"><span data-stu-id="a8730-863">staticrc70</span></span> |<span data-ttu-id="a8730-864">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="a8730-864">SloDWGroupC03</span></span> |<span data-ttu-id="a8730-865">16</span><span class="sxs-lookup"><span data-stu-id="a8730-865">16</span></span> |<span data-ttu-id="a8730-866">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-866">1,600</span></span> |<span data-ttu-id="a8730-867">Alto</span><span class="sxs-lookup"><span data-stu-id="a8730-867">High</span></span> |
| <span data-ttu-id="a8730-868">staticrc80</span><span class="sxs-lookup"><span data-stu-id="a8730-868">staticrc80</span></span> |<span data-ttu-id="a8730-869">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="a8730-869">SloDWGroupC03</span></span> |<span data-ttu-id="a8730-870">16</span><span class="sxs-lookup"><span data-stu-id="a8730-870">16</span></span> |<span data-ttu-id="a8730-871">1.600</span><span class="sxs-lookup"><span data-stu-id="a8730-871">1,600</span></span> |<span data-ttu-id="a8730-872">Alto</span><span class="sxs-lookup"><span data-stu-id="a8730-872">High</span></span> |

<span data-ttu-id="a8730-873">Você pode usar a seguinte consulta DMV para examinar as diferenças na alocação de recurso de memória em detalhes da perspectiva do administrador de recursos ou para analisar o uso ativo e histórico dos grupos de carga de trabalho ao solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="a8730-873">You can use the following DMV query to look at the differences in memory resource allocation in detail from the perspective of the resource governor, or to analyze active and historic usage of the workload groups when troubleshooting.</span></span>

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

## <a name="queries-that-honor-concurrency-limits"></a><span data-ttu-id="a8730-874">Consultas que respeitam os limites de simultaneidade</span><span class="sxs-lookup"><span data-stu-id="a8730-874">Queries that honor concurrency limits</span></span>
<span data-ttu-id="a8730-875">A maioria das consultas é governada pelas classes de recurso.</span><span class="sxs-lookup"><span data-stu-id="a8730-875">Most queries are governed by resource classes.</span></span> <span data-ttu-id="a8730-876">Essas consultas devem se ajustar tanto aos limites de consultas de simultaneidade quanto aos de slots de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="a8730-876">These queries must fit inside both the concurrent query and concurrency slot thresholds.</span></span> <span data-ttu-id="a8730-877">Um usuário não pode optar por excluir uma consulta do modelo de slot de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="a8730-877">A user cannot choose to exclude a query from the concurrency slot model.</span></span>

<span data-ttu-id="a8730-878">Para reiterar, as instruções a seguir respeitam as classes de recurso:</span><span class="sxs-lookup"><span data-stu-id="a8730-878">To reiterate, the following statements honor resource classes:</span></span>

* <span data-ttu-id="a8730-879">INSERT-SELECT</span><span class="sxs-lookup"><span data-stu-id="a8730-879">INSERT-SELECT</span></span>
* <span data-ttu-id="a8730-880">UPDATE</span><span class="sxs-lookup"><span data-stu-id="a8730-880">UPDATE</span></span>
* <span data-ttu-id="a8730-881">EXCLUIR</span><span class="sxs-lookup"><span data-stu-id="a8730-881">DELETE</span></span>
* <span data-ttu-id="a8730-882">SELECT (ao consultar tabelas de usuário)</span><span class="sxs-lookup"><span data-stu-id="a8730-882">SELECT (when querying user tables)</span></span>
* <span data-ttu-id="a8730-883">ALTER INDEX REBUILD</span><span class="sxs-lookup"><span data-stu-id="a8730-883">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="a8730-884">ALTER INDEX REORGANIZE</span><span class="sxs-lookup"><span data-stu-id="a8730-884">ALTER INDEX REORGANIZE</span></span>
* <span data-ttu-id="a8730-885">ALTER TABLE REBUILD</span><span class="sxs-lookup"><span data-stu-id="a8730-885">ALTER TABLE REBUILD</span></span>
* <span data-ttu-id="a8730-886">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="a8730-886">CREATE INDEX</span></span>
* <span data-ttu-id="a8730-887">CREATE CLUSTERED COLUMNSTORE INDEX</span><span class="sxs-lookup"><span data-stu-id="a8730-887">CREATE CLUSTERED COLUMNSTORE INDEX</span></span>
* <span data-ttu-id="a8730-888">CREATE TABLE AS SELECT (CTAS)</span><span class="sxs-lookup"><span data-stu-id="a8730-888">CREATE TABLE AS SELECT (CTAS)</span></span>
* <span data-ttu-id="a8730-889">Carregamento de dados</span><span class="sxs-lookup"><span data-stu-id="a8730-889">Data loading</span></span>
* <span data-ttu-id="a8730-890">Operações de movimentação de dados realizadas pelo Serviço de Movimentação de Dados (DMS)</span><span class="sxs-lookup"><span data-stu-id="a8730-890">Data movement operations conducted by the Data Movement Service (DMS)</span></span>

## <a name="query-exceptions-to-concurrency-limits"></a><span data-ttu-id="a8730-891">Exceções de consulta para limites de simultaneidade</span><span class="sxs-lookup"><span data-stu-id="a8730-891">Query exceptions to concurrency limits</span></span>
<span data-ttu-id="a8730-892">Algumas consultas não respeitam a classe de recurso à qual o usuário é atribuído.</span><span class="sxs-lookup"><span data-stu-id="a8730-892">Some queries do not honor the resource class to which the user is assigned.</span></span> <span data-ttu-id="a8730-893">Essas exceções para os limites de simultaneidade são feitas quando os recursos de memória necessários para um determinado comando estão baixos, geralmente porque o comando é uma operação de metadados.</span><span class="sxs-lookup"><span data-stu-id="a8730-893">These exceptions to the concurrency limits are made when the memory resources needed for a particular command are low, often because the command is a metadata operation.</span></span> <span data-ttu-id="a8730-894">O objetivo dessas exceções é evitar alocações de memória maiores para consultas que jamais precisarão delas.</span><span class="sxs-lookup"><span data-stu-id="a8730-894">The goal of these exceptions is to avoid larger memory allocations for queries that will never need them.</span></span> <span data-ttu-id="a8730-895">Nesses casos, a classe de recurso padrão pequena (smallrc) sempre é usada, independentemente da classe de recurso real atribuída ao usuário.</span><span class="sxs-lookup"><span data-stu-id="a8730-895">In these cases, the default small resource class (smallrc) is always used regardless of the actual resource class assigned to the user.</span></span> <span data-ttu-id="a8730-896">Por exemplo, `CREATE LOGIN` sempre será executado em smallrc.</span><span class="sxs-lookup"><span data-stu-id="a8730-896">For example, `CREATE LOGIN` will always run in smallrc.</span></span> <span data-ttu-id="a8730-897">Os recursos necessários para atender essa operação são muito baixos, portanto, não faz sentido incluir a consulta no modelo de slot de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="a8730-897">The resources required to fulfill this operation are very low, so it does not make sense to include the query in the concurrency slot model.</span></span>  <span data-ttu-id="a8730-898">Essas consultas também não são limitadas pelo limite de simultaneidade de 32 usuários, um número ilimitado dessas consultas pode ser executado até o limite de sessão de 1.024 sessões.</span><span class="sxs-lookup"><span data-stu-id="a8730-898">These queries are also not limited by the 32 user concurrency limit, an unlimited number of these queries can run up to the session limit of 1,024 sessions.</span></span>

<span data-ttu-id="a8730-899">As instruções a seguir não respeitam classes de recursos:</span><span class="sxs-lookup"><span data-stu-id="a8730-899">The following statements do not honor resource classes:</span></span>

* <span data-ttu-id="a8730-900">CREATE ou DROP TABLE</span><span class="sxs-lookup"><span data-stu-id="a8730-900">CREATE or DROP TABLE</span></span>
* <span data-ttu-id="a8730-901">ALTER TABLE ... SWITCH, SPLIT ou MERGE PARTITION</span><span class="sxs-lookup"><span data-stu-id="a8730-901">ALTER TABLE ... SWITCH, SPLIT, or MERGE PARTITION</span></span>
* <span data-ttu-id="a8730-902">ALTER INDEX DISABLE</span><span class="sxs-lookup"><span data-stu-id="a8730-902">ALTER INDEX DISABLE</span></span>
* <span data-ttu-id="a8730-903">DROP INDEX</span><span class="sxs-lookup"><span data-stu-id="a8730-903">DROP INDEX</span></span>
* <span data-ttu-id="a8730-904">CREATE, UPDATE ou DROP STATISTICS</span><span class="sxs-lookup"><span data-stu-id="a8730-904">CREATE, UPDATE, or DROP STATISTICS</span></span>
* <span data-ttu-id="a8730-905">TRUNCATE TABLE</span><span class="sxs-lookup"><span data-stu-id="a8730-905">TRUNCATE TABLE</span></span>
* <span data-ttu-id="a8730-906">ALTER AUTHORIZATION</span><span class="sxs-lookup"><span data-stu-id="a8730-906">ALTER AUTHORIZATION</span></span>
* <span data-ttu-id="a8730-907">CREATE LOGIN</span><span class="sxs-lookup"><span data-stu-id="a8730-907">CREATE LOGIN</span></span>
* <span data-ttu-id="a8730-908">CREATE, ALTER ou DROP USER</span><span class="sxs-lookup"><span data-stu-id="a8730-908">CREATE, ALTER or DROP USER</span></span>
* <span data-ttu-id="a8730-909">CREATE, ALTER ou DROP PROCEDURE</span><span class="sxs-lookup"><span data-stu-id="a8730-909">CREATE, ALTER or DROP PROCEDURE</span></span>
* <span data-ttu-id="a8730-910">CREATE ou DROP VIEW</span><span class="sxs-lookup"><span data-stu-id="a8730-910">CREATE or DROP VIEW</span></span>
* <span data-ttu-id="a8730-911">INSERT VALUES</span><span class="sxs-lookup"><span data-stu-id="a8730-911">INSERT VALUES</span></span>
* <span data-ttu-id="a8730-912">SELECT de exibições do sistema e DMVs</span><span class="sxs-lookup"><span data-stu-id="a8730-912">SELECT from system views and DMVs</span></span>
* <span data-ttu-id="a8730-913">EXPLAIN</span><span class="sxs-lookup"><span data-stu-id="a8730-913">EXPLAIN</span></span>
* <span data-ttu-id="a8730-914">DBCC</span><span class="sxs-lookup"><span data-stu-id="a8730-914">DBCC</span></span>

<!--
Removed as these two are not confirmed / supported under SQLDW
- CREATE REMOTE TABLE AS SELECT
- CREATE EXTERNAL TABLE AS SELECT
- REDISTRIBUTE
-->

##  <span data-ttu-id="a8730-915"><a name="changing-user-resource-class-example"></a> Alterar um exemplo de classe de recursos de usuário</span><span class="sxs-lookup"><span data-stu-id="a8730-915"><a name="changing-user-resource-class-example"></a> Change a user resource class example</span></span>
1. <span data-ttu-id="a8730-916">**Criar logon:** abra uma conexão com o banco de dados **mestre** no SQL Server hospedando seu banco de dados do SQL Data Warehouse e execute os comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="a8730-916">**Create login:** Open a connection to your **master** database on the SQL server hosting your SQL Data Warehouse database and execute the following commands.</span></span>
   
    ```sql
    CREATE LOGIN newperson WITH PASSWORD = 'mypassword';
    CREATE USER newperson for LOGIN newperson;
    ```
   
   > [!NOTE]
   > <span data-ttu-id="a8730-917">É uma boa ideia criar um usuário no banco de dados mestre para os usuários do Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a8730-917">It is a good idea to create a user in the master database for Azure SQL Data Warehouse users.</span></span> <span data-ttu-id="a8730-918">A criação de um usuário mestre permite que um usuário faça logon usando ferramentas, como o SSMS, sem especificar um nome de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a8730-918">Creating a user in master allows a user to login using tools like SSMS without specifying a database name.</span></span>  <span data-ttu-id="a8730-919">Ela também permite que o usuário utilize o pesquisador de objetos para exibir todos os bancos de dados em um SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a8730-919">It also allows them to use the object explorer to view all databases on a SQL server.</span></span>  <span data-ttu-id="a8730-920">Para obter mais detalhes sobre como criar e gerenciar usuários, consulte [Proteger um banco de dados no SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="a8730-920">For more details about creating and managing users, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>
   > 
   > 
2. <span data-ttu-id="a8730-921">**Criar um usuário do SQL Data Warehouse:** abra uma conexão com o banco de dados **SQL Data Warehouse** e execute o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="a8730-921">**Create SQL Data Warehouse user:** Open a connection to the **SQL Data Warehouse** database and execute the following command.</span></span>
   
    ```sql
    CREATE USER newperson FOR LOGIN newperson;
    ```
3. <span data-ttu-id="a8730-922">**Conceder permissões:** o exemplo a seguir concede `CONTROL` no banco de dados **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="a8730-922">**Grant permissions:** The following example grants `CONTROL` on the **SQL Data Warehouse** database.</span></span> <span data-ttu-id="a8730-923">`CONTROL` no nível do banco de dados é o equivalente de db_owner no SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a8730-923">`CONTROL` at the database level is the equivalent of db_owner in SQL Server.</span></span>
   
    ```sql
    GRANT CONTROL ON DATABASE::MySQLDW to newperson;
    ```
4. <span data-ttu-id="a8730-924">**Aumentar a classe do recurso:** use a consulta a seguir para adicionar um usuário a uma função de gerenciamento de carga de trabalho maior.</span><span class="sxs-lookup"><span data-stu-id="a8730-924">**Increase resource class:** Use the following query to add a user to a higher workload management role.</span></span>
   
    ```sql
    EXEC sp_addrolemember 'largerc', 'newperson'
    ```
5. <span data-ttu-id="a8730-925">**Diminuir a classe de recurso:** use a consulta a seguir para remover um usuário de uma função de gerenciamento de carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="a8730-925">**Decrease resource class:** Use the following query to remove a user from a workload management role.</span></span>
   
    ```sql
    EXEC sp_droprolemember 'largerc', 'newperson';
    ```
   
   > [!NOTE]
   > <span data-ttu-id="a8730-926">Não é possível remover um usuário de smallrc.</span><span class="sxs-lookup"><span data-stu-id="a8730-926">It is not possible to remove a user from smallrc.</span></span>
   > 
   > 

## <a name="queued-query-detection-and-other-dmvs"></a><span data-ttu-id="a8730-927">Detecção de consulta enfileirada e outros DMVs</span><span class="sxs-lookup"><span data-stu-id="a8730-927">Queued query detection and other DMVs</span></span>
<span data-ttu-id="a8730-928">Você pode usar o DMV `sys.dm_pdw_exec_requests` para identificar consultas que estão aguardando em uma fila de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="a8730-928">You can use the `sys.dm_pdw_exec_requests` DMV to identify queries that are waiting in a concurrency queue.</span></span> <span data-ttu-id="a8730-929">As consultas que estão aguardando um slot de simultaneidade terão um status de **suspensas**.</span><span class="sxs-lookup"><span data-stu-id="a8730-929">Queries waiting for a concurrency slot will have a status of **suspended**.</span></span>

```sql
SELECT      r.[request_id]                 AS Request_ID
        ,r.[status]                 AS Request_Status
        ,r.[submit_time]             AS Request_SubmitTime
        ,r.[start_time]                 AS Request_StartTime
        ,DATEDIFF(ms,[submit_time],[start_time]) AS Request_InitiateDuration_ms
        ,r.resource_class                         AS Request_resource_class
FROM    sys.dm_pdw_exec_requests r;
```

<span data-ttu-id="a8730-930">As funções de gerenciamento de carga de trabalho podem ser exibidas com `sys.database_principals`.</span><span class="sxs-lookup"><span data-stu-id="a8730-930">Workload management roles can be viewed with `sys.database_principals`.</span></span>

```sql
SELECT  ro.[name]           AS [db_role_name]
FROM    sys.database_principals ro
WHERE   ro.[type_desc]      = 'DATABASE_ROLE'
AND     ro.[is_fixed_role]  = 0;
```

<span data-ttu-id="a8730-931">A consulta a seguir mostra a qual função cada usuário está atribuído.</span><span class="sxs-lookup"><span data-stu-id="a8730-931">The following query shows which role each user is assigned to.</span></span>

```sql
SELECT     r.name AS role_principal_name
        ,m.name AS member_principal_name
FROM    sys.database_role_members rm
JOIN    sys.database_principals AS r            ON rm.role_principal_id        = r.principal_id
JOIN    sys.database_principals AS m            ON rm.member_principal_id    = m.principal_id
WHERE    r.name IN ('mediumrc','largerc', 'xlargerc');
```

<span data-ttu-id="a8730-932">O SQL Data Warehouse tem os seguintes tipos de espera:</span><span class="sxs-lookup"><span data-stu-id="a8730-932">SQL Data Warehouse has the following wait types:</span></span>

* <span data-ttu-id="a8730-933">**LocalQueriesConcurrencyResourceType**: consultas que ficam fora da estrutura de slot de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="a8730-933">**LocalQueriesConcurrencyResourceType**: Queries that sit outside of the concurrency slot framework.</span></span> <span data-ttu-id="a8730-934">Consultas DMV e funções de sistema, como `SELECT @@VERSION` , são exemplos de consultas de locais.</span><span class="sxs-lookup"><span data-stu-id="a8730-934">DMV queries and system functions such as `SELECT @@VERSION` are examples of local queries.</span></span>
* <span data-ttu-id="a8730-935">**UserConcurrencyResourceType**: consultas que ficam dentro da estrutura de slot de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="a8730-935">**UserConcurrencyResourceType**: Queries that sit inside the concurrency slot framework.</span></span> <span data-ttu-id="a8730-936">Consultas em tabelas do usuário final representam exemplos que usariam esse tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="a8730-936">Queries against end-user tables represent examples that would use this resource type.</span></span>
* <span data-ttu-id="a8730-937">**DmsConcurrencyResourceType**: esperas resultantes de operações de movimentação de dados.</span><span class="sxs-lookup"><span data-stu-id="a8730-937">**DmsConcurrencyResourceType**: Waits resulting from data movement operations.</span></span>
* <span data-ttu-id="a8730-938">**BackupConcurrencyResourceType**: essa espera indica que está sendo feito backup de um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a8730-938">**BackupConcurrencyResourceType**: This wait indicates that a database is being backed up.</span></span> <span data-ttu-id="a8730-939">O valor máximo para esse tipo de recurso é 1.</span><span class="sxs-lookup"><span data-stu-id="a8730-939">The maximum value for this resource type is 1.</span></span> <span data-ttu-id="a8730-940">Se vários backups foram solicitados ao mesmo tempo, os outros serão colocados em fila.</span><span class="sxs-lookup"><span data-stu-id="a8730-940">If multiple backups have been requested at the same time, the others will queue.</span></span>

<span data-ttu-id="a8730-941">O DMV `sys.dm_pdw_waits` pode ser usado para ver quais recursos uma solicitação está aguardando.</span><span class="sxs-lookup"><span data-stu-id="a8730-941">The `sys.dm_pdw_waits` DMV can be used to see which resources a request is waiting for.</span></span>

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

<span data-ttu-id="a8730-942">O DMV `sys.dm_pdw_resource_waits` mostra apenas as esperas de recursos consumidas por determinada consulta.</span><span class="sxs-lookup"><span data-stu-id="a8730-942">The `sys.dm_pdw_resource_waits` DMV shows only the resource waits consumed by a given query.</span></span> <span data-ttu-id="a8730-943">O tempo de espera do recurso mede apenas o tempo de espera dos recursos a serem fornecidos, não o tempo de espera do sinal, que é o tempo necessário para o SQL Server subjacente agendar a consulta para a CPU.</span><span class="sxs-lookup"><span data-stu-id="a8730-943">Resource wait time only measures the time waiting for resources to be provided, as opposed to signal wait time, which is the time it takes for the underlying SQL servers to schedule the query onto the CPU.</span></span>

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

<span data-ttu-id="a8730-944">O DMV `sys.dm_pdw_wait_stats` pode ser usado para análise de tendências históricas de espera.</span><span class="sxs-lookup"><span data-stu-id="a8730-944">The `sys.dm_pdw_wait_stats` DMV can be used for historic trend analysis of waits.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a8730-945">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a8730-945">Next steps</span></span>
<span data-ttu-id="a8730-946">Para obter mais informações sobre como gerenciar usuários de banco de dados e segurança, confira [Proteger um banco de dados no SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="a8730-946">For more information about managing database users and security, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span> <span data-ttu-id="a8730-947">Para obter mais informações sobre como classes de recurso maiores podem melhorar a qualidade do índice columnstore clusterizado, consulte [Recriando índices para melhorar a qualidade de segmento].</span><span class="sxs-lookup"><span data-stu-id="a8730-947">For more information about how larger resource classes can improve clustered columnstore index quality, see [Rebuilding indexes to improve segment quality].</span></span>

<!--Image references-->

<!--Article references-->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Recriando índices para melhorar a qualidade de segmento]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md

<!--MSDN references-->
[Managing Databases and Logins in Azure SQL Database]:https://msdn.microsoft.com/library/azure/ee336235.aspx

<!--Other Web references-->
