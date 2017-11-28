---
title: "Transações no SQL Data Warehouse | Microsoft Docs"
description: "Dicas para implementar transações no Azure SQL Data Warehouse para o desenvolvimento de soluções."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: ae621788-e575-41f5-8bfe-fa04dc4b0b53
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 29d53e18539f2c24dd64090b2ac6f9dd4c783961
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="transactions-in-sql-data-warehouse"></a><span data-ttu-id="5171d-103">Transações no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="5171d-103">Transactions in SQL Data Warehouse</span></span>
<span data-ttu-id="5171d-104">Como era esperado, o SQL Data Warehouse oferece suporte a transações como parte da carga de trabalho do data warehouse.</span><span class="sxs-lookup"><span data-stu-id="5171d-104">As you would expect, SQL Data Warehouse supports transactions as part of the data warehouse workload.</span></span> <span data-ttu-id="5171d-105">No entanto, para garantir que o desempenho do SQL Data Warehouse seja mantido em grande escala, alguns recursos serão limitados em comparação com o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5171d-105">However, to ensure the performance of SQL Data Warehouse is maintained at scale some features are limited when compared to SQL Server.</span></span> <span data-ttu-id="5171d-106">Este artigo realça as diferenças e lista as outras.</span><span class="sxs-lookup"><span data-stu-id="5171d-106">This article highlights the differences and lists the others.</span></span> 

## <a name="transaction-isolation-levels"></a><span data-ttu-id="5171d-107">Níveis de isolamento da transação</span><span class="sxs-lookup"><span data-stu-id="5171d-107">Transaction isolation levels</span></span>
<span data-ttu-id="5171d-108">O SQL Data Warehouse implementa transações ACID.</span><span class="sxs-lookup"><span data-stu-id="5171d-108">SQL Data Warehouse implements ACID transactions.</span></span> <span data-ttu-id="5171d-109">No entanto, o isolamento do suporte transacional é limitado a `READ UNCOMMITTED` e isso não pode ser alterado.</span><span class="sxs-lookup"><span data-stu-id="5171d-109">However, the Isolation of the transactional support is limited to `READ UNCOMMITTED` and this cannot be changed.</span></span> <span data-ttu-id="5171d-110">Você pode implementar diversos métodos de codificação para impedir leituras sujas de dados, se isso for importante para você.</span><span class="sxs-lookup"><span data-stu-id="5171d-110">You can implement a number of coding methods to prevent dirty reads of data if this is a concern for you.</span></span> <span data-ttu-id="5171d-111">Os métodos mais populares utilizam CTAS e a alternância de partição de tabela (normalmente conhecida como padrão de janela deslizante) para impedir que os usuários consultem dados que ainda estejam sendo preparados.</span><span class="sxs-lookup"><span data-stu-id="5171d-111">The most popular methods leverage both CTAS and table partition switching (often known as the sliding window pattern) to prevent users from querying data that is still being prepared.</span></span> <span data-ttu-id="5171d-112">Modos de exibição que filtram previamente os dados também são uma abordagem popular.</span><span class="sxs-lookup"><span data-stu-id="5171d-112">Views that pre-filter the data is also a popular approach.</span></span>  

## <a name="transaction-size"></a><span data-ttu-id="5171d-113">Tamanho da transação</span><span class="sxs-lookup"><span data-stu-id="5171d-113">Transaction size</span></span>
<span data-ttu-id="5171d-114">Uma única transação de modificação de dados é limitada em tamanho.</span><span class="sxs-lookup"><span data-stu-id="5171d-114">A single data modification transaction is limited in size.</span></span> <span data-ttu-id="5171d-115">Hoje, o limite é aplicado “por distribuição”.</span><span class="sxs-lookup"><span data-stu-id="5171d-115">The limit today is applied "per distribution".</span></span> <span data-ttu-id="5171d-116">Portanto, a alocação total pode ser calculada multiplicando o limite pela contagem de distribuição.</span><span class="sxs-lookup"><span data-stu-id="5171d-116">Therefore, the total allocation can be calculated by multiplying the limit by the distribution count.</span></span> <span data-ttu-id="5171d-117">Para chegar a uma aproximação do número máximo de linhas na transação, divida o limite de distribuição pelo tamanho total de cada linha.</span><span class="sxs-lookup"><span data-stu-id="5171d-117">To approximate the maximum number of rows in the transaction divide the distribution cap by the total size of each row.</span></span> <span data-ttu-id="5171d-118">Para colunas de tamanho variável, considere o uso de um tamanho médio de coluna em vez do tamanho máximo.</span><span class="sxs-lookup"><span data-stu-id="5171d-118">For variable length columns consider taking an average column length rather than using the maximum size.</span></span>

<span data-ttu-id="5171d-119">Na tabela abaixo, foram feitas as seguintes suposições:</span><span class="sxs-lookup"><span data-stu-id="5171d-119">In the table below the following assumptions have been made:</span></span>

* <span data-ttu-id="5171d-120">Ocorreu uma distribuição uniforme dos dados</span><span class="sxs-lookup"><span data-stu-id="5171d-120">An even distribution of data has occurred</span></span> 
* <span data-ttu-id="5171d-121">O tamanho médio da linha é de 250 bytes</span><span class="sxs-lookup"><span data-stu-id="5171d-121">The average row length is 250 bytes</span></span>

| <span data-ttu-id="5171d-122">[DWU][DWU]</span><span class="sxs-lookup"><span data-stu-id="5171d-122">[DWU][DWU]</span></span> | <span data-ttu-id="5171d-123">Limite por distribuição (GiB)</span><span class="sxs-lookup"><span data-stu-id="5171d-123">Cap per distribution (GiB)</span></span> | <span data-ttu-id="5171d-124">Número de distribuições</span><span class="sxs-lookup"><span data-stu-id="5171d-124">Number of Distributions</span></span> | <span data-ttu-id="5171d-125">Tamanho máximo de transações (GiB)</span><span class="sxs-lookup"><span data-stu-id="5171d-125">MAX transaction size (GiB)</span></span> | <span data-ttu-id="5171d-126"># Linhas por distribuição</span><span class="sxs-lookup"><span data-stu-id="5171d-126"># Rows per distribution</span></span> | <span data-ttu-id="5171d-127">Máximo de linhas por transação</span><span class="sxs-lookup"><span data-stu-id="5171d-127">Max Rows per transaction</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="5171d-128">DW100</span><span class="sxs-lookup"><span data-stu-id="5171d-128">DW100</span></span> |<span data-ttu-id="5171d-129">1</span><span class="sxs-lookup"><span data-stu-id="5171d-129">1</span></span> |<span data-ttu-id="5171d-130">60</span><span class="sxs-lookup"><span data-stu-id="5171d-130">60</span></span> |<span data-ttu-id="5171d-131">60</span><span class="sxs-lookup"><span data-stu-id="5171d-131">60</span></span> |<span data-ttu-id="5171d-132">4.000.000</span><span class="sxs-lookup"><span data-stu-id="5171d-132">4,000,000</span></span> |<span data-ttu-id="5171d-133">240.000.000</span><span class="sxs-lookup"><span data-stu-id="5171d-133">240,000,000</span></span> |
| <span data-ttu-id="5171d-134">DW200</span><span class="sxs-lookup"><span data-stu-id="5171d-134">DW200</span></span> |<span data-ttu-id="5171d-135">1.5</span><span class="sxs-lookup"><span data-stu-id="5171d-135">1.5</span></span> |<span data-ttu-id="5171d-136">60</span><span class="sxs-lookup"><span data-stu-id="5171d-136">60</span></span> |<span data-ttu-id="5171d-137">90</span><span class="sxs-lookup"><span data-stu-id="5171d-137">90</span></span> |<span data-ttu-id="5171d-138">6.000.000</span><span class="sxs-lookup"><span data-stu-id="5171d-138">6,000,000</span></span> |<span data-ttu-id="5171d-139">360.000.000</span><span class="sxs-lookup"><span data-stu-id="5171d-139">360,000,000</span></span> |
| <span data-ttu-id="5171d-140">DW300</span><span class="sxs-lookup"><span data-stu-id="5171d-140">DW300</span></span> |<span data-ttu-id="5171d-141">2.25</span><span class="sxs-lookup"><span data-stu-id="5171d-141">2.25</span></span> |<span data-ttu-id="5171d-142">60</span><span class="sxs-lookup"><span data-stu-id="5171d-142">60</span></span> |<span data-ttu-id="5171d-143">135</span><span class="sxs-lookup"><span data-stu-id="5171d-143">135</span></span> |<span data-ttu-id="5171d-144">9.000.000</span><span class="sxs-lookup"><span data-stu-id="5171d-144">9,000,000</span></span> |<span data-ttu-id="5171d-145">540.000.000</span><span class="sxs-lookup"><span data-stu-id="5171d-145">540,000,000</span></span> |
| <span data-ttu-id="5171d-146">DW400</span><span class="sxs-lookup"><span data-stu-id="5171d-146">DW400</span></span> |<span data-ttu-id="5171d-147">3</span><span class="sxs-lookup"><span data-stu-id="5171d-147">3</span></span> |<span data-ttu-id="5171d-148">60</span><span class="sxs-lookup"><span data-stu-id="5171d-148">60</span></span> |<span data-ttu-id="5171d-149">180</span><span class="sxs-lookup"><span data-stu-id="5171d-149">180</span></span> |<span data-ttu-id="5171d-150">12.000.000</span><span class="sxs-lookup"><span data-stu-id="5171d-150">12,000,000</span></span> |<span data-ttu-id="5171d-151">720.000.000</span><span class="sxs-lookup"><span data-stu-id="5171d-151">720,000,000</span></span> |
| <span data-ttu-id="5171d-152">DW500</span><span class="sxs-lookup"><span data-stu-id="5171d-152">DW500</span></span> |<span data-ttu-id="5171d-153">3,75</span><span class="sxs-lookup"><span data-stu-id="5171d-153">3.75</span></span> |<span data-ttu-id="5171d-154">60</span><span class="sxs-lookup"><span data-stu-id="5171d-154">60</span></span> |<span data-ttu-id="5171d-155">225</span><span class="sxs-lookup"><span data-stu-id="5171d-155">225</span></span> |<span data-ttu-id="5171d-156">15.000.000</span><span class="sxs-lookup"><span data-stu-id="5171d-156">15,000,000</span></span> |<span data-ttu-id="5171d-157">900.000.000</span><span class="sxs-lookup"><span data-stu-id="5171d-157">900,000,000</span></span> |
| <span data-ttu-id="5171d-158">DW600</span><span class="sxs-lookup"><span data-stu-id="5171d-158">DW600</span></span> |<span data-ttu-id="5171d-159">4.5</span><span class="sxs-lookup"><span data-stu-id="5171d-159">4.5</span></span> |<span data-ttu-id="5171d-160">60</span><span class="sxs-lookup"><span data-stu-id="5171d-160">60</span></span> |<span data-ttu-id="5171d-161">270</span><span class="sxs-lookup"><span data-stu-id="5171d-161">270</span></span> |<span data-ttu-id="5171d-162">18.000.000</span><span class="sxs-lookup"><span data-stu-id="5171d-162">18,000,000</span></span> |<span data-ttu-id="5171d-163">1.080.000.000</span><span class="sxs-lookup"><span data-stu-id="5171d-163">1,080,000,000</span></span> |
| <span data-ttu-id="5171d-164">DW1000</span><span class="sxs-lookup"><span data-stu-id="5171d-164">DW1000</span></span> |<span data-ttu-id="5171d-165">7.5</span><span class="sxs-lookup"><span data-stu-id="5171d-165">7.5</span></span> |<span data-ttu-id="5171d-166">60</span><span class="sxs-lookup"><span data-stu-id="5171d-166">60</span></span> |<span data-ttu-id="5171d-167">450</span><span class="sxs-lookup"><span data-stu-id="5171d-167">450</span></span> |<span data-ttu-id="5171d-168">30.000.000</span><span class="sxs-lookup"><span data-stu-id="5171d-168">30,000,000</span></span> |<span data-ttu-id="5171d-169">1.800.000.000</span><span class="sxs-lookup"><span data-stu-id="5171d-169">1,800,000,000</span></span> |
| <span data-ttu-id="5171d-170">DW1200</span><span class="sxs-lookup"><span data-stu-id="5171d-170">DW1200</span></span> |<span data-ttu-id="5171d-171">9</span><span class="sxs-lookup"><span data-stu-id="5171d-171">9</span></span> |<span data-ttu-id="5171d-172">60</span><span class="sxs-lookup"><span data-stu-id="5171d-172">60</span></span> |<span data-ttu-id="5171d-173">540</span><span class="sxs-lookup"><span data-stu-id="5171d-173">540</span></span> |<span data-ttu-id="5171d-174">36.000.000</span><span class="sxs-lookup"><span data-stu-id="5171d-174">36,000,000</span></span> |<span data-ttu-id="5171d-175">2.160.000.000</span><span class="sxs-lookup"><span data-stu-id="5171d-175">2,160,000,000</span></span> |
| <span data-ttu-id="5171d-176">DW1500</span><span class="sxs-lookup"><span data-stu-id="5171d-176">DW1500</span></span> |<span data-ttu-id="5171d-177">11,25</span><span class="sxs-lookup"><span data-stu-id="5171d-177">11.25</span></span> |<span data-ttu-id="5171d-178">60</span><span class="sxs-lookup"><span data-stu-id="5171d-178">60</span></span> |<span data-ttu-id="5171d-179">675</span><span class="sxs-lookup"><span data-stu-id="5171d-179">675</span></span> |<span data-ttu-id="5171d-180">45.000.000</span><span class="sxs-lookup"><span data-stu-id="5171d-180">45,000,000</span></span> |<span data-ttu-id="5171d-181">2.700.000.000</span><span class="sxs-lookup"><span data-stu-id="5171d-181">2,700,000,000</span></span> |
| <span data-ttu-id="5171d-182">DW2000</span><span class="sxs-lookup"><span data-stu-id="5171d-182">DW2000</span></span> |<span data-ttu-id="5171d-183">15</span><span class="sxs-lookup"><span data-stu-id="5171d-183">15</span></span> |<span data-ttu-id="5171d-184">60</span><span class="sxs-lookup"><span data-stu-id="5171d-184">60</span></span> |<span data-ttu-id="5171d-185">900</span><span class="sxs-lookup"><span data-stu-id="5171d-185">900</span></span> |<span data-ttu-id="5171d-186">60.000.000</span><span class="sxs-lookup"><span data-stu-id="5171d-186">60,000,000</span></span> |<span data-ttu-id="5171d-187">3.600.000.000</span><span class="sxs-lookup"><span data-stu-id="5171d-187">3,600,000,000</span></span> |
| <span data-ttu-id="5171d-188">DW3000</span><span class="sxs-lookup"><span data-stu-id="5171d-188">DW3000</span></span> |<span data-ttu-id="5171d-189">22,5</span><span class="sxs-lookup"><span data-stu-id="5171d-189">22.5</span></span> |<span data-ttu-id="5171d-190">60</span><span class="sxs-lookup"><span data-stu-id="5171d-190">60</span></span> |<span data-ttu-id="5171d-191">1.350</span><span class="sxs-lookup"><span data-stu-id="5171d-191">1,350</span></span> |<span data-ttu-id="5171d-192">90.000.000</span><span class="sxs-lookup"><span data-stu-id="5171d-192">90,000,000</span></span> |<span data-ttu-id="5171d-193">5.400.000.000</span><span class="sxs-lookup"><span data-stu-id="5171d-193">5,400,000,000</span></span> |
| <span data-ttu-id="5171d-194">DW6000</span><span class="sxs-lookup"><span data-stu-id="5171d-194">DW6000</span></span> |<span data-ttu-id="5171d-195">45</span><span class="sxs-lookup"><span data-stu-id="5171d-195">45</span></span> |<span data-ttu-id="5171d-196">60</span><span class="sxs-lookup"><span data-stu-id="5171d-196">60</span></span> |<span data-ttu-id="5171d-197">2.700</span><span class="sxs-lookup"><span data-stu-id="5171d-197">2,700</span></span> |<span data-ttu-id="5171d-198">180.000.000</span><span class="sxs-lookup"><span data-stu-id="5171d-198">180,000,000</span></span> |<span data-ttu-id="5171d-199">10.800.000.000</span><span class="sxs-lookup"><span data-stu-id="5171d-199">10,800,000,000</span></span> |

<span data-ttu-id="5171d-200">O limite de tamanho de transação é aplicado por transação ou operação.</span><span class="sxs-lookup"><span data-stu-id="5171d-200">The transaction size limit is applied per transaction or operation.</span></span> <span data-ttu-id="5171d-201">Ele não é aplicado em todas as transações simultâneas.</span><span class="sxs-lookup"><span data-stu-id="5171d-201">It is not applied across all concurrent transactions.</span></span> <span data-ttu-id="5171d-202">Portanto, cada transação tem permissão para gravar essa quantidade de dados no log.</span><span class="sxs-lookup"><span data-stu-id="5171d-202">Therefore each transaction is permitted to write this amount of data to the log.</span></span> 

<span data-ttu-id="5171d-203">Para otimizar e minimizar a quantidade de dados gravados no log, confira o artigo [Práticas recomendadas das transações][Transactions best practices].</span><span class="sxs-lookup"><span data-stu-id="5171d-203">To optimize and minimize the amount of data written to the log please refer to the [Transactions best practices][Transactions best practices] article.</span></span>

> [!WARNING]
> <span data-ttu-id="5171d-204">O tamanho máximo de transações só pode ser obtido para tabelas distribuídas HASH ou ROUND_ROBIN nas quais o espalhamento de dados é uniforme.</span><span class="sxs-lookup"><span data-stu-id="5171d-204">The maximum transaction size can only be achieved for HASH or ROUND_ROBIN distributed tables where the spread of the data is even.</span></span> <span data-ttu-id="5171d-205">Se a transação estiver gravando dados de maneira distorcida nas distribuições, provavelmente, o limite será alcançado antes do tamanho máximo de transações.</span><span class="sxs-lookup"><span data-stu-id="5171d-205">If the transaction is writing data in a skewed fashion to the distributions then the limit is likely to be reached prior to the maximum transaction size.</span></span>
> <!--REPLICATED_TABLE-->
> 
> 

## <a name="transaction-state"></a><span data-ttu-id="5171d-206">Estado da transação</span><span class="sxs-lookup"><span data-stu-id="5171d-206">Transaction state</span></span>
<span data-ttu-id="5171d-207">O SQL Data Warehouse usa a função XACT_STATE() para relatar uma transação com falha usando o valor -2.</span><span class="sxs-lookup"><span data-stu-id="5171d-207">SQL Data Warehouse uses the XACT_STATE() function to report a failed transaction using the value -2.</span></span> <span data-ttu-id="5171d-208">Isso significa que a transação falhou e está marcada para reversão somente</span><span class="sxs-lookup"><span data-stu-id="5171d-208">This means that the transaction has failed and is marked for rollback only</span></span>

> [!NOTE]
> <span data-ttu-id="5171d-209">O uso de -2 pela função XACT_STATE para denotar uma transação com falha representa um comportamento diferente para o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5171d-209">The use of -2 by the XACT_STATE function to denote a failed transaction represents different behavior to SQL Server.</span></span> <span data-ttu-id="5171d-210">O SQL Server usa o valor -1 para representar uma transação não confirmável.</span><span class="sxs-lookup"><span data-stu-id="5171d-210">SQL Server uses the value -1 to represent an un-committable transaction.</span></span> <span data-ttu-id="5171d-211">O SQL Server consegue tolerar alguns erros dentro de uma transação sem precisar ser marcado como não confirmável.</span><span class="sxs-lookup"><span data-stu-id="5171d-211">SQL Server can tolerate some errors inside a transaction without it having to be marked as un-committable.</span></span> <span data-ttu-id="5171d-212">Por exemplo, `SELECT 1/0` poderia causar um erro, mas não forçar uma transação em um estado não confirmável.</span><span class="sxs-lookup"><span data-stu-id="5171d-212">For example `SELECT 1/0` would cause an error but not force a transaction into an un-committable state.</span></span> <span data-ttu-id="5171d-213">O SQL Server também permite leituras na transação não confirmável.</span><span class="sxs-lookup"><span data-stu-id="5171d-213">SQL Server also permits reads in the un-committable transaction.</span></span> <span data-ttu-id="5171d-214">No entanto, o SQL Data Warehouse não permite que você faça isso.</span><span class="sxs-lookup"><span data-stu-id="5171d-214">However, SQL Data Warehouse does not let you do this.</span></span> <span data-ttu-id="5171d-215">Se um erro ocorrer dentro de uma transação do SQL Data Warehouse, ele entrará automaticamente no estado -2 e você não poderá mais dar instruções do tipo select até que a instrução seja revertida.</span><span class="sxs-lookup"><span data-stu-id="5171d-215">If an error occurs inside a SQL Data Warehouse transaction it will automatically enter the -2 state and you will not be able to make any further select statements until the statement has been rolled back.</span></span> <span data-ttu-id="5171d-216">Portanto, é importante verificar o código do aplicativo para ver se ele usa XACT_STATE(), pois você poderá precisar modificar o código.</span><span class="sxs-lookup"><span data-stu-id="5171d-216">It is therefore important to check that your application code to see if it uses  XACT_STATE() as you may need to make code modifications.</span></span>
> 
> 

<span data-ttu-id="5171d-217">Por exemplo, no SQL Server, você verá uma transação com esta aparência:</span><span class="sxs-lookup"><span data-stu-id="5171d-217">For example, in SQL Server you might see a transaction that looks like this:</span></span>

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

<span data-ttu-id="5171d-218">Se deixar o código como está acima, você receberá a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="5171d-218">If you leave your code as it is above then you will get the following error message:</span></span>

<span data-ttu-id="5171d-219">Mensagem 111233, Nível 16, Estado 1, Linha 1 111233; A transação atual foi anulada e todas as alterações pendentes foram revertidas.</span><span class="sxs-lookup"><span data-stu-id="5171d-219">Msg 111233, Level 16, State 1, Line 1 111233;The current transaction has aborted, and any pending changes have been rolled back.</span></span> <span data-ttu-id="5171d-220">Causa: uma transação no estado somente reversão não foi revertida explicitamente antes de uma instrução DDL, DML ou SELECT.</span><span class="sxs-lookup"><span data-stu-id="5171d-220">Cause: A transaction in a rollback-only state was not explicitly rolled back before a DDL, DML or SELECT statement.</span></span>

<span data-ttu-id="5171d-221">Você também não receberá a saída das funções ERROR_*.</span><span class="sxs-lookup"><span data-stu-id="5171d-221">You will also not get the output of the ERROR_* functions.</span></span>

<span data-ttu-id="5171d-222">No SQL Data Warehouse, o código precisa ser ligeiramente alterado:</span><span class="sxs-lookup"><span data-stu-id="5171d-222">In SQL Data Warehouse the code needs to be slightly altered:</span></span>

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;
    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

<span data-ttu-id="5171d-223">O comportamento esperado é observado agora.</span><span class="sxs-lookup"><span data-stu-id="5171d-223">The expected behavior is now observed.</span></span> <span data-ttu-id="5171d-224">O erro na transação é gerenciado e as funções ERROR_* fornecem valores conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="5171d-224">The error in the transaction is managed and the ERROR_* functions provide values as expected.</span></span>

<span data-ttu-id="5171d-225">Tudo o que mudou é que a `ROLLBACK` da transação deve ocorrer antes da leitura das informações de erro no bloco `CATCH`.</span><span class="sxs-lookup"><span data-stu-id="5171d-225">All that has changed is that the `ROLLBACK` of the transaction had to happen before the read of the error information in the `CATCH` block.</span></span>

## <a name="errorline-function"></a><span data-ttu-id="5171d-226">Função Error_line()</span><span class="sxs-lookup"><span data-stu-id="5171d-226">Error_Line() function</span></span>
<span data-ttu-id="5171d-227">Também vale a pena observar que o SQL Data Warehouse não implementa ou aceita a função ERROR_LINE().</span><span class="sxs-lookup"><span data-stu-id="5171d-227">It is also worth noting that SQL Data Warehouse does not implement or support the ERROR_LINE() function.</span></span> <span data-ttu-id="5171d-228">Se você tiver isso em seu código, você precisará removê-lo para que seja compatível com o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="5171d-228">If you have this in your code you will need to remove it to be compliant with SQL Data Warehouse.</span></span> <span data-ttu-id="5171d-229">Em vez disso, use rótulos de consulta em seu código para implementar a funcionalidade equivalente.</span><span class="sxs-lookup"><span data-stu-id="5171d-229">Use query labels in your code instead to implement equivalent functionality.</span></span> <span data-ttu-id="5171d-230">Confira o artigo [LABEL][LABEL] para obter mais detalhes sobre este recurso.</span><span class="sxs-lookup"><span data-stu-id="5171d-230">Please refer to the [LABEL][LABEL] article for more details on this feature.</span></span>

## <a name="using-throw-and-raiserror"></a><span data-ttu-id="5171d-231">Uso de THROW e RAISERROR</span><span class="sxs-lookup"><span data-stu-id="5171d-231">Using THROW and RAISERROR</span></span>
<span data-ttu-id="5171d-232">THROW é a implementação mais moderna para lançar exceções no SQL Data Warehouse, mas também há suporte para RAISERROR.</span><span class="sxs-lookup"><span data-stu-id="5171d-232">THROW is the more modern implementation for raising exceptions in SQL Data Warehouse but RAISERROR is also supported.</span></span> <span data-ttu-id="5171d-233">No entanto, existem algumas diferenças que valem a pena prestar atenção.</span><span class="sxs-lookup"><span data-stu-id="5171d-233">There are a few differences that are worth paying attention to however.</span></span>

* <span data-ttu-id="5171d-234">Os números das mensagens de erro definidas pelo usuário não podem estar no intervalo de 100.000 a 150.000 para THROW </span><span class="sxs-lookup"><span data-stu-id="5171d-234">User defined error messages numbers cannot be in the 100,000 - 150,000 range for THROW</span></span>
* <span data-ttu-id="5171d-235">As mensagens de erro do RAISERROR são fixadas em 50.000</span><span class="sxs-lookup"><span data-stu-id="5171d-235">RAISERROR error messages are fixed at 50,000</span></span>
* <span data-ttu-id="5171d-236">Não há suporte para o uso de sys.messages</span><span class="sxs-lookup"><span data-stu-id="5171d-236">Use of sys.messages is not supported</span></span>

## <a name="limitiations"></a><span data-ttu-id="5171d-237">Limitações</span><span class="sxs-lookup"><span data-stu-id="5171d-237">Limitiations</span></span>
<span data-ttu-id="5171d-238">O SQL Data Warehouse tem algumas outras restrições relacionadas a transações.</span><span class="sxs-lookup"><span data-stu-id="5171d-238">SQL Data Warehouse does have a few other restrictions that relate to transactions.</span></span>

<span data-ttu-id="5171d-239">Elas são as seguintes:</span><span class="sxs-lookup"><span data-stu-id="5171d-239">They are as follows:</span></span>

* <span data-ttu-id="5171d-240">Sem transações distribuídas</span><span class="sxs-lookup"><span data-stu-id="5171d-240">No distributed transactions</span></span>
* <span data-ttu-id="5171d-241">Não há transações aninhadas permitidas</span><span class="sxs-lookup"><span data-stu-id="5171d-241">No nested transactions permitted</span></span>
* <span data-ttu-id="5171d-242">Não são permitidos pontos de salvamento</span><span class="sxs-lookup"><span data-stu-id="5171d-242">No save points allowed</span></span>
* <span data-ttu-id="5171d-243">Nenhuma transação nomeada</span><span class="sxs-lookup"><span data-stu-id="5171d-243">No named transactions</span></span>
* <span data-ttu-id="5171d-244">Nenhuma transação marcada</span><span class="sxs-lookup"><span data-stu-id="5171d-244">No marked transactions</span></span>
* <span data-ttu-id="5171d-245">Não há suporte para DDL, como `CREATE TABLE` , em uma transação definida pelo usuário</span><span class="sxs-lookup"><span data-stu-id="5171d-245">No support for DDL such as `CREATE TABLE` inside a user defined transaction</span></span>

## <a name="next-steps"></a><span data-ttu-id="5171d-246">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5171d-246">Next steps</span></span>
<span data-ttu-id="5171d-247">Para saber mais sobre a otimização das transações, confira [Práticas recomendadas das transações][Transactions best practices].</span><span class="sxs-lookup"><span data-stu-id="5171d-247">To learn more about optimizing transactions, see [Transactions best practices][Transactions best practices].</span></span>  <span data-ttu-id="5171d-248">Para saber mais sobre outras práticas recomendadas do SQL Data Warehouse, confira [Práticas recomendadas do SQL Data Warehouse][SQL Data Warehouse best practices].</span><span class="sxs-lookup"><span data-stu-id="5171d-248">To learn about other SQL Data Warehouse best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse best practices].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Transactions best practices]: ./sql-data-warehouse-develop-best-practices-transactions.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->

<!--Other Web references-->
