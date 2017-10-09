---
title: aaaTransactions no SQL Data Warehouse | Microsoft Docs
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
ms.openlocfilehash: 7c541648553238443b407666612561918096eb61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="transactions-in-sql-data-warehouse"></a><span data-ttu-id="adee7-103">Transações no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="adee7-103">Transactions in SQL Data Warehouse</span></span>
<span data-ttu-id="adee7-104">Como esperado, o SQL Data Warehouse oferece suporte a transações como parte da carga de trabalho do hello data warehouse.</span><span class="sxs-lookup"><span data-stu-id="adee7-104">As you would expect, SQL Data Warehouse supports transactions as part of hello data warehouse workload.</span></span> <span data-ttu-id="adee7-105">No entanto, tooensure Olá desempenho do SQL Data Warehouse é mantido em escala de que alguns recursos estão limitados quando tooSQL em comparação com o servidor.</span><span class="sxs-lookup"><span data-stu-id="adee7-105">However, tooensure hello performance of SQL Data Warehouse is maintained at scale some features are limited when compared tooSQL Server.</span></span> <span data-ttu-id="adee7-106">Este artigo destaca as diferenças de saudação e listas Olá outras pessoas.</span><span class="sxs-lookup"><span data-stu-id="adee7-106">This article highlights hello differences and lists hello others.</span></span> 

## <a name="transaction-isolation-levels"></a><span data-ttu-id="adee7-107">Níveis de isolamento da transação</span><span class="sxs-lookup"><span data-stu-id="adee7-107">Transaction isolation levels</span></span>
<span data-ttu-id="adee7-108">O SQL Data Warehouse implementa transações ACID.</span><span class="sxs-lookup"><span data-stu-id="adee7-108">SQL Data Warehouse implements ACID transactions.</span></span> <span data-ttu-id="adee7-109">No entanto, Olá isolamento de suporte transacional Olá é limitado muito`READ UNCOMMITTED` e isso não pode ser alterado.</span><span class="sxs-lookup"><span data-stu-id="adee7-109">However, hello Isolation of hello transactional support is limited too`READ UNCOMMITTED` and this cannot be changed.</span></span> <span data-ttu-id="adee7-110">Você pode implementar vários métodos de codificação tooprevent suja leituras de dados se isso for uma preocupação para você.</span><span class="sxs-lookup"><span data-stu-id="adee7-110">You can implement a number of coding methods tooprevent dirty reads of data if this is a concern for you.</span></span> <span data-ttu-id="adee7-111">Olá métodos mais comuns aproveitam CTAS e a alternância de partição de tabela (geralmente conhecido como Olá padrão de janela deslizante) tooprevent usuários consultando os dados que ainda está sendo preparados.</span><span class="sxs-lookup"><span data-stu-id="adee7-111">hello most popular methods leverage both CTAS and table partition switching (often known as hello sliding window pattern) tooprevent users from querying data that is still being prepared.</span></span> <span data-ttu-id="adee7-112">Exibições de dados pré-filtragem saudação também são um método popular.</span><span class="sxs-lookup"><span data-stu-id="adee7-112">Views that pre-filter hello data is also a popular approach.</span></span>  

## <a name="transaction-size"></a><span data-ttu-id="adee7-113">Tamanho da transação</span><span class="sxs-lookup"><span data-stu-id="adee7-113">Transaction size</span></span>
<span data-ttu-id="adee7-114">Uma única transação de modificação de dados é limitada em tamanho.</span><span class="sxs-lookup"><span data-stu-id="adee7-114">A single data modification transaction is limited in size.</span></span> <span data-ttu-id="adee7-115">limite de saudação hoje é aplicado "por distribuição de".</span><span class="sxs-lookup"><span data-stu-id="adee7-115">hello limit today is applied "per distribution".</span></span> <span data-ttu-id="adee7-116">Portanto, alocação total Olá pode ser calculada pela multiplicação de limite de saudação por contagem de distribuição de saudação.</span><span class="sxs-lookup"><span data-stu-id="adee7-116">Therefore, hello total allocation can be calculated by multiplying hello limit by hello distribution count.</span></span> <span data-ttu-id="adee7-117">número máximo de saudação de tooapproximate de linhas em transação Olá divide cap de distribuição de saudação pelo tamanho total de saudação de cada linha.</span><span class="sxs-lookup"><span data-stu-id="adee7-117">tooapproximate hello maximum number of rows in hello transaction divide hello distribution cap by hello total size of each row.</span></span> <span data-ttu-id="adee7-118">Para colunas de comprimento variável, considere colocar um comprimento médio de coluna em vez de usar o tamanho máximo de saudação.</span><span class="sxs-lookup"><span data-stu-id="adee7-118">For variable length columns consider taking an average column length rather than using hello maximum size.</span></span>

<span data-ttu-id="adee7-119">Na tabela de saudação abaixo Olá foram feitas seguintes suposições:</span><span class="sxs-lookup"><span data-stu-id="adee7-119">In hello table below hello following assumptions have been made:</span></span>

* <span data-ttu-id="adee7-120">Ocorreu uma distribuição uniforme dos dados</span><span class="sxs-lookup"><span data-stu-id="adee7-120">An even distribution of data has occurred</span></span> 
* <span data-ttu-id="adee7-121">Comprimento médio da linha de saudação é de 250 bytes</span><span class="sxs-lookup"><span data-stu-id="adee7-121">hello average row length is 250 bytes</span></span>

| <span data-ttu-id="adee7-122">[DWU][DWU]</span><span class="sxs-lookup"><span data-stu-id="adee7-122">[DWU][DWU]</span></span> | <span data-ttu-id="adee7-123">Limite por distribuição (GiB)</span><span class="sxs-lookup"><span data-stu-id="adee7-123">Cap per distribution (GiB)</span></span> | <span data-ttu-id="adee7-124">Número de distribuições</span><span class="sxs-lookup"><span data-stu-id="adee7-124">Number of Distributions</span></span> | <span data-ttu-id="adee7-125">Tamanho máximo de transações (GiB)</span><span class="sxs-lookup"><span data-stu-id="adee7-125">MAX transaction size (GiB)</span></span> | <span data-ttu-id="adee7-126"># Linhas por distribuição</span><span class="sxs-lookup"><span data-stu-id="adee7-126"># Rows per distribution</span></span> | <span data-ttu-id="adee7-127">Máximo de linhas por transação</span><span class="sxs-lookup"><span data-stu-id="adee7-127">Max Rows per transaction</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="adee7-128">DW100</span><span class="sxs-lookup"><span data-stu-id="adee7-128">DW100</span></span> |<span data-ttu-id="adee7-129">1</span><span class="sxs-lookup"><span data-stu-id="adee7-129">1</span></span> |<span data-ttu-id="adee7-130">60</span><span class="sxs-lookup"><span data-stu-id="adee7-130">60</span></span> |<span data-ttu-id="adee7-131">60</span><span class="sxs-lookup"><span data-stu-id="adee7-131">60</span></span> |<span data-ttu-id="adee7-132">4.000.000</span><span class="sxs-lookup"><span data-stu-id="adee7-132">4,000,000</span></span> |<span data-ttu-id="adee7-133">240.000.000</span><span class="sxs-lookup"><span data-stu-id="adee7-133">240,000,000</span></span> |
| <span data-ttu-id="adee7-134">DW200</span><span class="sxs-lookup"><span data-stu-id="adee7-134">DW200</span></span> |<span data-ttu-id="adee7-135">1.5</span><span class="sxs-lookup"><span data-stu-id="adee7-135">1.5</span></span> |<span data-ttu-id="adee7-136">60</span><span class="sxs-lookup"><span data-stu-id="adee7-136">60</span></span> |<span data-ttu-id="adee7-137">90</span><span class="sxs-lookup"><span data-stu-id="adee7-137">90</span></span> |<span data-ttu-id="adee7-138">6.000.000</span><span class="sxs-lookup"><span data-stu-id="adee7-138">6,000,000</span></span> |<span data-ttu-id="adee7-139">360.000.000</span><span class="sxs-lookup"><span data-stu-id="adee7-139">360,000,000</span></span> |
| <span data-ttu-id="adee7-140">DW300</span><span class="sxs-lookup"><span data-stu-id="adee7-140">DW300</span></span> |<span data-ttu-id="adee7-141">2.25</span><span class="sxs-lookup"><span data-stu-id="adee7-141">2.25</span></span> |<span data-ttu-id="adee7-142">60</span><span class="sxs-lookup"><span data-stu-id="adee7-142">60</span></span> |<span data-ttu-id="adee7-143">135</span><span class="sxs-lookup"><span data-stu-id="adee7-143">135</span></span> |<span data-ttu-id="adee7-144">9.000.000</span><span class="sxs-lookup"><span data-stu-id="adee7-144">9,000,000</span></span> |<span data-ttu-id="adee7-145">540.000.000</span><span class="sxs-lookup"><span data-stu-id="adee7-145">540,000,000</span></span> |
| <span data-ttu-id="adee7-146">DW400</span><span class="sxs-lookup"><span data-stu-id="adee7-146">DW400</span></span> |<span data-ttu-id="adee7-147">3</span><span class="sxs-lookup"><span data-stu-id="adee7-147">3</span></span> |<span data-ttu-id="adee7-148">60</span><span class="sxs-lookup"><span data-stu-id="adee7-148">60</span></span> |<span data-ttu-id="adee7-149">180</span><span class="sxs-lookup"><span data-stu-id="adee7-149">180</span></span> |<span data-ttu-id="adee7-150">12.000.000</span><span class="sxs-lookup"><span data-stu-id="adee7-150">12,000,000</span></span> |<span data-ttu-id="adee7-151">720.000.000</span><span class="sxs-lookup"><span data-stu-id="adee7-151">720,000,000</span></span> |
| <span data-ttu-id="adee7-152">DW500</span><span class="sxs-lookup"><span data-stu-id="adee7-152">DW500</span></span> |<span data-ttu-id="adee7-153">3,75</span><span class="sxs-lookup"><span data-stu-id="adee7-153">3.75</span></span> |<span data-ttu-id="adee7-154">60</span><span class="sxs-lookup"><span data-stu-id="adee7-154">60</span></span> |<span data-ttu-id="adee7-155">225</span><span class="sxs-lookup"><span data-stu-id="adee7-155">225</span></span> |<span data-ttu-id="adee7-156">15.000.000</span><span class="sxs-lookup"><span data-stu-id="adee7-156">15,000,000</span></span> |<span data-ttu-id="adee7-157">900.000.000</span><span class="sxs-lookup"><span data-stu-id="adee7-157">900,000,000</span></span> |
| <span data-ttu-id="adee7-158">DW600</span><span class="sxs-lookup"><span data-stu-id="adee7-158">DW600</span></span> |<span data-ttu-id="adee7-159">4.5</span><span class="sxs-lookup"><span data-stu-id="adee7-159">4.5</span></span> |<span data-ttu-id="adee7-160">60</span><span class="sxs-lookup"><span data-stu-id="adee7-160">60</span></span> |<span data-ttu-id="adee7-161">270</span><span class="sxs-lookup"><span data-stu-id="adee7-161">270</span></span> |<span data-ttu-id="adee7-162">18.000.000</span><span class="sxs-lookup"><span data-stu-id="adee7-162">18,000,000</span></span> |<span data-ttu-id="adee7-163">1.080.000.000</span><span class="sxs-lookup"><span data-stu-id="adee7-163">1,080,000,000</span></span> |
| <span data-ttu-id="adee7-164">DW1000</span><span class="sxs-lookup"><span data-stu-id="adee7-164">DW1000</span></span> |<span data-ttu-id="adee7-165">7.5</span><span class="sxs-lookup"><span data-stu-id="adee7-165">7.5</span></span> |<span data-ttu-id="adee7-166">60</span><span class="sxs-lookup"><span data-stu-id="adee7-166">60</span></span> |<span data-ttu-id="adee7-167">450</span><span class="sxs-lookup"><span data-stu-id="adee7-167">450</span></span> |<span data-ttu-id="adee7-168">30.000.000</span><span class="sxs-lookup"><span data-stu-id="adee7-168">30,000,000</span></span> |<span data-ttu-id="adee7-169">1.800.000.000</span><span class="sxs-lookup"><span data-stu-id="adee7-169">1,800,000,000</span></span> |
| <span data-ttu-id="adee7-170">DW1200</span><span class="sxs-lookup"><span data-stu-id="adee7-170">DW1200</span></span> |<span data-ttu-id="adee7-171">9</span><span class="sxs-lookup"><span data-stu-id="adee7-171">9</span></span> |<span data-ttu-id="adee7-172">60</span><span class="sxs-lookup"><span data-stu-id="adee7-172">60</span></span> |<span data-ttu-id="adee7-173">540</span><span class="sxs-lookup"><span data-stu-id="adee7-173">540</span></span> |<span data-ttu-id="adee7-174">36.000.000</span><span class="sxs-lookup"><span data-stu-id="adee7-174">36,000,000</span></span> |<span data-ttu-id="adee7-175">2.160.000.000</span><span class="sxs-lookup"><span data-stu-id="adee7-175">2,160,000,000</span></span> |
| <span data-ttu-id="adee7-176">DW1500</span><span class="sxs-lookup"><span data-stu-id="adee7-176">DW1500</span></span> |<span data-ttu-id="adee7-177">11,25</span><span class="sxs-lookup"><span data-stu-id="adee7-177">11.25</span></span> |<span data-ttu-id="adee7-178">60</span><span class="sxs-lookup"><span data-stu-id="adee7-178">60</span></span> |<span data-ttu-id="adee7-179">675</span><span class="sxs-lookup"><span data-stu-id="adee7-179">675</span></span> |<span data-ttu-id="adee7-180">45.000.000</span><span class="sxs-lookup"><span data-stu-id="adee7-180">45,000,000</span></span> |<span data-ttu-id="adee7-181">2.700.000.000</span><span class="sxs-lookup"><span data-stu-id="adee7-181">2,700,000,000</span></span> |
| <span data-ttu-id="adee7-182">DW2000</span><span class="sxs-lookup"><span data-stu-id="adee7-182">DW2000</span></span> |<span data-ttu-id="adee7-183">15</span><span class="sxs-lookup"><span data-stu-id="adee7-183">15</span></span> |<span data-ttu-id="adee7-184">60</span><span class="sxs-lookup"><span data-stu-id="adee7-184">60</span></span> |<span data-ttu-id="adee7-185">900</span><span class="sxs-lookup"><span data-stu-id="adee7-185">900</span></span> |<span data-ttu-id="adee7-186">60.000.000</span><span class="sxs-lookup"><span data-stu-id="adee7-186">60,000,000</span></span> |<span data-ttu-id="adee7-187">3.600.000.000</span><span class="sxs-lookup"><span data-stu-id="adee7-187">3,600,000,000</span></span> |
| <span data-ttu-id="adee7-188">DW3000</span><span class="sxs-lookup"><span data-stu-id="adee7-188">DW3000</span></span> |<span data-ttu-id="adee7-189">22,5</span><span class="sxs-lookup"><span data-stu-id="adee7-189">22.5</span></span> |<span data-ttu-id="adee7-190">60</span><span class="sxs-lookup"><span data-stu-id="adee7-190">60</span></span> |<span data-ttu-id="adee7-191">1.350</span><span class="sxs-lookup"><span data-stu-id="adee7-191">1,350</span></span> |<span data-ttu-id="adee7-192">90.000.000</span><span class="sxs-lookup"><span data-stu-id="adee7-192">90,000,000</span></span> |<span data-ttu-id="adee7-193">5.400.000.000</span><span class="sxs-lookup"><span data-stu-id="adee7-193">5,400,000,000</span></span> |
| <span data-ttu-id="adee7-194">DW6000</span><span class="sxs-lookup"><span data-stu-id="adee7-194">DW6000</span></span> |<span data-ttu-id="adee7-195">45</span><span class="sxs-lookup"><span data-stu-id="adee7-195">45</span></span> |<span data-ttu-id="adee7-196">60</span><span class="sxs-lookup"><span data-stu-id="adee7-196">60</span></span> |<span data-ttu-id="adee7-197">2.700</span><span class="sxs-lookup"><span data-stu-id="adee7-197">2,700</span></span> |<span data-ttu-id="adee7-198">180.000.000</span><span class="sxs-lookup"><span data-stu-id="adee7-198">180,000,000</span></span> |<span data-ttu-id="adee7-199">10.800.000.000</span><span class="sxs-lookup"><span data-stu-id="adee7-199">10,800,000,000</span></span> |

<span data-ttu-id="adee7-200">limite de tamanho de transação Olá é aplicado por transação ou a operação.</span><span class="sxs-lookup"><span data-stu-id="adee7-200">hello transaction size limit is applied per transaction or operation.</span></span> <span data-ttu-id="adee7-201">Ele não é aplicado em todas as transações simultâneas.</span><span class="sxs-lookup"><span data-stu-id="adee7-201">It is not applied across all concurrent transactions.</span></span> <span data-ttu-id="adee7-202">Portanto, cada transação é permitida toowrite essa quantidade de dados toohello log.</span><span class="sxs-lookup"><span data-stu-id="adee7-202">Therefore each transaction is permitted toowrite this amount of data toohello log.</span></span> 

<span data-ttu-id="adee7-203">toooptimize e minimizar Olá toohello log de gravação de dados, consulte toohello [transações práticas recomendadas] [ Transactions best practices] artigo.</span><span class="sxs-lookup"><span data-stu-id="adee7-203">toooptimize and minimize hello amount of data written toohello log please refer toohello [Transactions best practices][Transactions best practices] article.</span></span>

> [!WARNING]
> <span data-ttu-id="adee7-204">Olá máximo de tamanho de transação só pode ser obtido para HASH ou tabelas ROUND_ROBIN distribuídas onde espalhar Olá Olá dados é par.</span><span class="sxs-lookup"><span data-stu-id="adee7-204">hello maximum transaction size can only be achieved for HASH or ROUND_ROBIN distributed tables where hello spread of hello data is even.</span></span> <span data-ttu-id="adee7-205">Se transação hello está gravando os dados de maneira distorcida toohello distribuições, em seguida, hello limite é provavelmente toobe atingida o tamanho de máximo de transações de toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="adee7-205">If hello transaction is writing data in a skewed fashion toohello distributions then hello limit is likely toobe reached prior toohello maximum transaction size.</span></span>
> <!--REPLICATED_TABLE-->
> 
> 

## <a name="transaction-state"></a><span data-ttu-id="adee7-206">Estado da transação</span><span class="sxs-lookup"><span data-stu-id="adee7-206">Transaction state</span></span>
<span data-ttu-id="adee7-207">SQL Data Warehouse usa Olá xact_state função tooreport uma transação com falha usando o valor de saudação -2.</span><span class="sxs-lookup"><span data-stu-id="adee7-207">SQL Data Warehouse uses hello XACT_STATE() function tooreport a failed transaction using hello value -2.</span></span> <span data-ttu-id="adee7-208">Isso significa que a transação Olá falhou e está marcada para reversão apenas</span><span class="sxs-lookup"><span data-stu-id="adee7-208">This means that hello transaction has failed and is marked for rollback only</span></span>

> [!NOTE]
> <span data-ttu-id="adee7-209">Olá usá -2 Olá XACT_STATE função toodenote tooSQL de um comportamento diferente de representa uma transação com falha Server.</span><span class="sxs-lookup"><span data-stu-id="adee7-209">hello use of -2 by hello XACT_STATE function toodenote a failed transaction represents different behavior tooSQL Server.</span></span> <span data-ttu-id="adee7-210">O SQL Server usa Olá valor -1 toorepresent uma transação não confirmável.</span><span class="sxs-lookup"><span data-stu-id="adee7-210">SQL Server uses hello value -1 toorepresent an un-committable transaction.</span></span> <span data-ttu-id="adee7-211">SQL Server pode tolerar alguns erros dentro de uma transação sem que ele tenha toobe marcado como não confirmável.</span><span class="sxs-lookup"><span data-stu-id="adee7-211">SQL Server can tolerate some errors inside a transaction without it having toobe marked as un-committable.</span></span> <span data-ttu-id="adee7-212">Por exemplo, `SELECT 1/0` poderia causar um erro, mas não forçar uma transação em um estado não confirmável.</span><span class="sxs-lookup"><span data-stu-id="adee7-212">For example `SELECT 1/0` would cause an error but not force a transaction into an un-committable state.</span></span> <span data-ttu-id="adee7-213">SQL Server também permite leituras de transação não confirmável hello.</span><span class="sxs-lookup"><span data-stu-id="adee7-213">SQL Server also permits reads in hello un-committable transaction.</span></span> <span data-ttu-id="adee7-214">No entanto, o SQL Data Warehouse não permite que você faça isso.</span><span class="sxs-lookup"><span data-stu-id="adee7-214">However, SQL Data Warehouse does not let you do this.</span></span> <span data-ttu-id="adee7-215">Se ocorrer um erro dentro de uma transação do SQL Data Warehouse, ele inserirá automaticamente o estado da saudação -2 e não será capaz de toomake qualquer mais instruções select até que a instrução de saudação foi revertida.</span><span class="sxs-lookup"><span data-stu-id="adee7-215">If an error occurs inside a SQL Data Warehouse transaction it will automatically enter hello -2 state and you will not be able toomake any further select statements until hello statement has been rolled back.</span></span> <span data-ttu-id="adee7-216">Portanto, é importante toocheck que sua toosee de código do aplicativo se ele usa xact_state como você pode precisar de modificações no código toomake.</span><span class="sxs-lookup"><span data-stu-id="adee7-216">It is therefore important toocheck that your application code toosee if it uses  XACT_STATE() as you may need toomake code modifications.</span></span>
> 
> 

<span data-ttu-id="adee7-217">Por exemplo, no SQL Server, você verá uma transação com esta aparência:</span><span class="sxs-lookup"><span data-stu-id="adee7-217">For example, in SQL Server you might see a transaction that looks like this:</span></span>

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

<span data-ttu-id="adee7-218">Se você deixar seu código, pois ele está acima, em seguida, você obterá Olá a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="adee7-218">If you leave your code as it is above then you will get hello following error message:</span></span>

<span data-ttu-id="adee7-219">Msg 111233, nível 16, estado 1, linha 1 111233; Olá atual transação foi anulada, e todas as alterações pendentes foram revertidas.</span><span class="sxs-lookup"><span data-stu-id="adee7-219">Msg 111233, Level 16, State 1, Line 1 111233;hello current transaction has aborted, and any pending changes have been rolled back.</span></span> <span data-ttu-id="adee7-220">Causa: uma transação no estado somente reversão não foi revertida explicitamente antes de uma instrução DDL, DML ou SELECT.</span><span class="sxs-lookup"><span data-stu-id="adee7-220">Cause: A transaction in a rollback-only state was not explicitly rolled back before a DDL, DML or SELECT statement.</span></span>

<span data-ttu-id="adee7-221">Você também não terá saída de saudação do erro. * funções de saudação.</span><span class="sxs-lookup"><span data-stu-id="adee7-221">You will also not get hello output of hello ERROR_* functions.</span></span>

<span data-ttu-id="adee7-222">No SQL Data Warehouse código Olá precisa toobe ligeiramente alterado:</span><span class="sxs-lookup"><span data-stu-id="adee7-222">In SQL Data Warehouse hello code needs toobe slightly altered:</span></span>

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

<span data-ttu-id="adee7-223">Olá esperado comportamento observado agora.</span><span class="sxs-lookup"><span data-stu-id="adee7-223">hello expected behavior is now observed.</span></span> <span data-ttu-id="adee7-224">Erro de saudação na transação de saudação é gerenciado e Olá erro. * funções fornecem valores conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="adee7-224">hello error in hello transaction is managed and hello ERROR_* functions provide values as expected.</span></span>

<span data-ttu-id="adee7-225">Tudo o que mudou é que hello `ROLLBACK` de saudação transação tinha toohappen antes de ler Olá Olá informações de erro em Olá `CATCH` bloco.</span><span class="sxs-lookup"><span data-stu-id="adee7-225">All that has changed is that hello `ROLLBACK` of hello transaction had toohappen before hello read of hello error information in hello `CATCH` block.</span></span>

## <a name="errorline-function"></a><span data-ttu-id="adee7-226">Função Error_line()</span><span class="sxs-lookup"><span data-stu-id="adee7-226">Error_Line() function</span></span>
<span data-ttu-id="adee7-227">Também vale a pena observar que SQL Data Warehouse não implementar ou oferecer suporte a função do hello error_line ().</span><span class="sxs-lookup"><span data-stu-id="adee7-227">It is also worth noting that SQL Data Warehouse does not implement or support hello ERROR_LINE() function.</span></span> <span data-ttu-id="adee7-228">Se você tiver isso em seu código, você precisará tooremove-toobe compatível com o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="adee7-228">If you have this in your code you will need tooremove it toobe compliant with SQL Data Warehouse.</span></span> <span data-ttu-id="adee7-229">Use rótulos de consulta em seu código em vez disso, tooimplement uma funcionalidade equivalente.</span><span class="sxs-lookup"><span data-stu-id="adee7-229">Use query labels in your code instead tooimplement equivalent functionality.</span></span> <span data-ttu-id="adee7-230">Consulte toohello [rótulo] [ LABEL] artigo para obter mais detalhes sobre esse recurso.</span><span class="sxs-lookup"><span data-stu-id="adee7-230">Please refer toohello [LABEL][LABEL] article for more details on this feature.</span></span>

## <a name="using-throw-and-raiserror"></a><span data-ttu-id="adee7-231">Uso de THROW e RAISERROR</span><span class="sxs-lookup"><span data-stu-id="adee7-231">Using THROW and RAISERROR</span></span>
<span data-ttu-id="adee7-232">THROW é Olá implementação mais moderna para gerar exceções no SQL Data Warehouse, mas também há suporte para RAISERROR.</span><span class="sxs-lookup"><span data-stu-id="adee7-232">THROW is hello more modern implementation for raising exceptions in SQL Data Warehouse but RAISERROR is also supported.</span></span> <span data-ttu-id="adee7-233">Há algumas diferenças que vale a pena prestando atenção toohowever.</span><span class="sxs-lookup"><span data-stu-id="adee7-233">There are a few differences that are worth paying attention toohowever.</span></span>

* <span data-ttu-id="adee7-234">Números não podem estar em Olá intervalo 100.000 150.000 THROW de mensagens de erro definidas pelo usuário</span><span class="sxs-lookup"><span data-stu-id="adee7-234">User defined error messages numbers cannot be in hello 100,000 - 150,000 range for THROW</span></span>
* <span data-ttu-id="adee7-235">As mensagens de erro do RAISERROR são fixadas em 50.000</span><span class="sxs-lookup"><span data-stu-id="adee7-235">RAISERROR error messages are fixed at 50,000</span></span>
* <span data-ttu-id="adee7-236">Não há suporte para o uso de sys.messages</span><span class="sxs-lookup"><span data-stu-id="adee7-236">Use of sys.messages is not supported</span></span>

## <a name="limitiations"></a><span data-ttu-id="adee7-237">Limitações</span><span class="sxs-lookup"><span data-stu-id="adee7-237">Limitiations</span></span>
<span data-ttu-id="adee7-238">SQL Data Warehouse tem algumas outras restrições que se relacionam tootransactions.</span><span class="sxs-lookup"><span data-stu-id="adee7-238">SQL Data Warehouse does have a few other restrictions that relate tootransactions.</span></span>

<span data-ttu-id="adee7-239">Elas são as seguintes:</span><span class="sxs-lookup"><span data-stu-id="adee7-239">They are as follows:</span></span>

* <span data-ttu-id="adee7-240">Sem transações distribuídas</span><span class="sxs-lookup"><span data-stu-id="adee7-240">No distributed transactions</span></span>
* <span data-ttu-id="adee7-241">Não há transações aninhadas permitidas</span><span class="sxs-lookup"><span data-stu-id="adee7-241">No nested transactions permitted</span></span>
* <span data-ttu-id="adee7-242">Não são permitidos pontos de salvamento</span><span class="sxs-lookup"><span data-stu-id="adee7-242">No save points allowed</span></span>
* <span data-ttu-id="adee7-243">Nenhuma transação nomeada</span><span class="sxs-lookup"><span data-stu-id="adee7-243">No named transactions</span></span>
* <span data-ttu-id="adee7-244">Nenhuma transação marcada</span><span class="sxs-lookup"><span data-stu-id="adee7-244">No marked transactions</span></span>
* <span data-ttu-id="adee7-245">Não há suporte para DDL, como `CREATE TABLE` , em uma transação definida pelo usuário</span><span class="sxs-lookup"><span data-stu-id="adee7-245">No support for DDL such as `CREATE TABLE` inside a user defined transaction</span></span>

## <a name="next-steps"></a><span data-ttu-id="adee7-246">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="adee7-246">Next steps</span></span>
<span data-ttu-id="adee7-247">toolearn mais informações sobre a otimização de transações, consulte [transações práticas recomendadas][Transactions best practices].</span><span class="sxs-lookup"><span data-stu-id="adee7-247">toolearn more about optimizing transactions, see [Transactions best practices][Transactions best practices].</span></span>  <span data-ttu-id="adee7-248">toolearn sobre outras práticas recomendadas do SQL Data Warehouse, consulte [práticas recomendadas do SQL Data Warehouse][SQL Data Warehouse best practices].</span><span class="sxs-lookup"><span data-stu-id="adee7-248">toolearn about other SQL Data Warehouse best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse best practices].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Transactions best practices]: ./sql-data-warehouse-develop-best-practices-transactions.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->

<!--Other Web references-->
