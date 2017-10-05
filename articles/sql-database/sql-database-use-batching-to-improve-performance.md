---
title: Como usar o envio em lote para melhorar o desempenho do aplicativo Banco de Dados SQL do Azure
description: "O tópico fornece provas de que as operações de banco de dados de envio em lote melhorar consideravelmente a velocidade e a escalabilidade de seus aplicativos de Banco de Dados SQL do Azure. Embora essas técnicas de envio em lote funcionem para qualquer banco de dados do SQL Server, o foco do artigo é no Azure."
services: sql-database
documentationcenter: na
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 563862ca-c65a-46f6-975d-10df7ff6aa9c
ms.service: sql-database
ms.custom: develop apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2016
ms.author: sstein
ms.openlocfilehash: 22cff47444306e599325ba3035d83a0266d69c72
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-batching-to-improve-sql-database-application-performance"></a><span data-ttu-id="cbba4-104">Como usar o envio em lote para melhorar o desempenho do aplicativo Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="cbba4-104">How to use batching to improve SQL Database application performance</span></span>
<span data-ttu-id="cbba4-105">O envio de operações em lote para o Banco de Dados SQL do Azure melhora consideravelmente o desempenho e a escalabilidade dos aplicativos.</span><span class="sxs-lookup"><span data-stu-id="cbba4-105">Batching operations to Azure SQL Database significantly improves the performance and scalability of your applications.</span></span> <span data-ttu-id="cbba4-106">Para compreender os benefícios, a primeira parte deste artigo aborda alguns exemplos de resultados de teste que comparam solicitações sequenciais e em lote para um Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="cbba4-106">In order to understand the benefits, the first part of this article covers some sample test results that compare sequential and batched requests to a SQL Database.</span></span> <span data-ttu-id="cbba4-107">O restante do artigo mostra as técnicas, os cenários e considerações para ajudar você a usar o envio em lote com sucesso em seus aplicativos do Azure.</span><span class="sxs-lookup"><span data-stu-id="cbba4-107">The remainder of the article shows the techniques, scenarios, and considerations to help you to use batching successfully in your Azure applications.</span></span>

## <a name="why-is-batching-important-for-sql-database"></a><span data-ttu-id="cbba4-108">Por que o envio em lote é importante para o Banco de Dados SQL?</span><span class="sxs-lookup"><span data-stu-id="cbba4-108">Why is batching important for SQL Database?</span></span>
<span data-ttu-id="cbba4-109">Envio de chamadas em lote para um serviço remoto é uma estratégia conhecida para aumentar o desempenho e a escalabilidade.</span><span class="sxs-lookup"><span data-stu-id="cbba4-109">Batching calls to a remote service is a well-known strategy for increasing performance and scalability.</span></span> <span data-ttu-id="cbba4-110">Há custos de processamento fixos para todas as interações com um serviço remoto, como a serialização, a transferência de rede e a desserialização.</span><span class="sxs-lookup"><span data-stu-id="cbba4-110">There are fixed processing costs to any interactions with a remote service, such as serialization, network transfer, and deserialization.</span></span> <span data-ttu-id="cbba4-111">O empacotamento de muitas transações separadas em um único lote minimiza esses custos.</span><span class="sxs-lookup"><span data-stu-id="cbba4-111">Packaging many separate transactions into a single batch minimizes these costs.</span></span>

<span data-ttu-id="cbba4-112">Neste documento, queremos examinar as vária estratégias e cenários de envio em lote do Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="cbba4-112">In this paper, we want to examine various SQL Database batching strategies and scenarios.</span></span> <span data-ttu-id="cbba4-113">Embora essas estratégias também sejam importantes para aplicativos locais que usam o SQL Server, há vários motivos para destacar o uso do envio em lote para o Banco de Dados SQL:</span><span class="sxs-lookup"><span data-stu-id="cbba4-113">Although these strategies are also important for on-premises applications that use SQL Server, there are several reasons for highlighting the use of batching for SQL Database:</span></span>

* <span data-ttu-id="cbba4-114">Há potencialmente maior latência de rede no acesso ao Banco de Dados SQL, especialmente se você estiver acessando o Banco de Dados SQL fora do mesmo datacenter do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cbba4-114">There is potentially greater network latency in accessing SQL Database, especially if you are accessing SQL Database from outside the same Microsoft Azure datacenter.</span></span>
* <span data-ttu-id="cbba4-115">As características multilocatário do Banco de Dados SQL significam que a eficiência da camada de acesso a dados correlaciona com a escalabilidade geral do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="cbba4-115">The multitenant characteristics of SQL Database means that the efficiency of the data access layer correlates to the overall scalability of the database.</span></span> <span data-ttu-id="cbba4-116">O Banco de Dados SQL deve impedir que qualquer locatário/usuário monopolize os recursos do banco de dados em detrimento de outros locatários.</span><span class="sxs-lookup"><span data-stu-id="cbba4-116">SQL Database must prevent any single tenant/user from monopolizing database resources to the detriment of other tenants.</span></span> <span data-ttu-id="cbba4-117">Em resposta ao uso em excesso das cotas predefinidas, o Banco de Dados SQL pode reduzir a produtividade ou responder com exceções de limitação.</span><span class="sxs-lookup"><span data-stu-id="cbba4-117">In response to usage in excess of predefined quotas, SQL Database can reduce throughput or respond with throttling exceptions.</span></span> <span data-ttu-id="cbba4-118">As eficiências, como o envio em lote, permitem que você execute mais trabalhos no Banco de Dados SQL antes de alcançar esses limites.</span><span class="sxs-lookup"><span data-stu-id="cbba4-118">Efficiencies, such as batching, enable you to do more work on SQL Database before reaching these limits.</span></span> 
* <span data-ttu-id="cbba4-119">O envio em lote também é eficaz para arquiteturas que usam vários bancos de dados (fragmentação).</span><span class="sxs-lookup"><span data-stu-id="cbba4-119">Batching is also effective for architectures that use multiple databases (sharding).</span></span> <span data-ttu-id="cbba4-120">A eficiência da sua interação com cada unidade de banco de dados ainda é um fator fundamental em sua escalabilidade total.</span><span class="sxs-lookup"><span data-stu-id="cbba4-120">The efficiency of your interaction with each database unit is still a key factor in your overall scalability.</span></span> 

<span data-ttu-id="cbba4-121">Um dos benefícios de usar o Banco de Dados SQL é que você não precisa gerenciar os servidores que hospedam o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="cbba4-121">One of the benefits of using SQL Database is that you don’t have to manage the servers that host the database.</span></span> <span data-ttu-id="cbba4-122">No entanto, essa infraestrutura gerenciada também significa que você precisa pensar de forma diferente sobre a otimizações do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="cbba4-122">However, this managed infrastructure also means that you have to think differently about database optimizations.</span></span> <span data-ttu-id="cbba4-123">Você não pode mais procurar melhorar a infraestrutura de hardware ou de rede do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="cbba4-123">You can no longer look to improve the database hardware or network infrastructure.</span></span> <span data-ttu-id="cbba4-124">O Microsoft Azure controla esses ambientes.</span><span class="sxs-lookup"><span data-stu-id="cbba4-124">Microsoft Azure controls those environments.</span></span> <span data-ttu-id="cbba4-125">A principal área que você pode controlar é como seu aplicativo interage com o Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="cbba4-125">The main area that you can control is how your application interacts with SQL Database.</span></span> <span data-ttu-id="cbba4-126">O envio em lote é uma dessas otimizações.</span><span class="sxs-lookup"><span data-stu-id="cbba4-126">Batching is one of these optimizations.</span></span> 

<span data-ttu-id="cbba4-127">A primeira parte do documento examina várias técnicas de envio em lote para aplicativos .NET que usam o Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="cbba4-127">The first part of the paper examines various batching techniques for .NET applications that use SQL Database.</span></span> <span data-ttu-id="cbba4-128">As duas últimas seções abordam diretrizes e cenários de envio em lote.</span><span class="sxs-lookup"><span data-stu-id="cbba4-128">The last two sections cover batching guidelines and scenarios.</span></span>

## <a name="batching-strategies"></a><span data-ttu-id="cbba4-129">Estratégias de envio em lote</span><span class="sxs-lookup"><span data-stu-id="cbba4-129">Batching strategies</span></span>
### <a name="note-about-timing-results-in-this-topic"></a><span data-ttu-id="cbba4-130">Observação sobre os resultados de tempo neste tópico</span><span class="sxs-lookup"><span data-stu-id="cbba4-130">Note about timing results in this topic</span></span>
> [!NOTE]
> <span data-ttu-id="cbba4-131">Os resultados não são parâmetros de comparação, mas têm como finalidade mostrar o **desempenho relativo**.</span><span class="sxs-lookup"><span data-stu-id="cbba4-131">Results are not benchmarks but are meant to show **relative performance**.</span></span> <span data-ttu-id="cbba4-132">Os intervalos se baseiam em uma média de pelo menos 10 execuções de teste.</span><span class="sxs-lookup"><span data-stu-id="cbba4-132">Timings are based on an average of at least 10 test runs.</span></span> <span data-ttu-id="cbba4-133">As operações são inserções em uma tabela vazia.</span><span class="sxs-lookup"><span data-stu-id="cbba4-133">Operations are inserts into an empty table.</span></span> <span data-ttu-id="cbba4-134">Esses testes foram medidos antes do V12 e não correspondem necessariamente à produtividade que você pode obter em um banco de dados V12 usando as novas [camadas de serviço](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="cbba4-134">These tests were measured pre-V12, and they do not necessarily correspond to throughput that you might experience in a V12 database using the new [service tiers](sql-database-service-tiers.md).</span></span> <span data-ttu-id="cbba4-135">O benefício relativo da técnica de envio em lote deve ser semelhante.</span><span class="sxs-lookup"><span data-stu-id="cbba4-135">The relative benefit of the batching technique should be similar.</span></span>
> 
> 

### <a name="transactions"></a><span data-ttu-id="cbba4-136">Transações</span><span class="sxs-lookup"><span data-stu-id="cbba4-136">Transactions</span></span>
<span data-ttu-id="cbba4-137">Parece estranho iniciar uma análise do envio em lote discutindo transações.</span><span class="sxs-lookup"><span data-stu-id="cbba4-137">It seems strange to begin a review of batching by discussing transactions.</span></span> <span data-ttu-id="cbba4-138">Mas o uso de transações no lado do cliente tem um efeito sutil no envio em lote do lado do servidor que melhora o desempenho.</span><span class="sxs-lookup"><span data-stu-id="cbba4-138">But the use of client-side transactions has a subtle server-side batching effect that improves performance.</span></span> <span data-ttu-id="cbba4-139">E é possível adicionar transações com apenas algumas linhas de código, portanto elas fornecem uma maneira rápida de melhorar o desempenho de operações sequenciais.</span><span class="sxs-lookup"><span data-stu-id="cbba4-139">And transactions can be added with only a few lines of code, so they provide a fast way to improve performance of sequential operations.</span></span>

<span data-ttu-id="cbba4-140">Considere o seguinte código C# que contém uma sequência de operações de inserção e de atualização em uma tabela simples.</span><span class="sxs-lookup"><span data-stu-id="cbba4-140">Consider the following C# code that contains a sequence of insert and update operations on a simple table.</span></span>

    List<string> dbOperations = new List<string>();
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 1");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 2");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 3");
    dbOperations.Add("insert MyTable values ('new value',1)");
    dbOperations.Add("insert MyTable values ('new value',2)");
    dbOperations.Add("insert MyTable values ('new value',3)");

<span data-ttu-id="cbba4-141">O seguinte código ADO.NET executa sequencialmente essas operações.</span><span class="sxs-lookup"><span data-stu-id="cbba4-141">The following ADO.NET code sequentially performs these operations.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();

        foreach(string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn);
            cmd.ExecuteNonQuery();                   
        }
    }

<span data-ttu-id="cbba4-142">A melhor maneira de otimizar esse código é implementar alguma forma de envio em lote do lado do cliente dessas chamadas.</span><span class="sxs-lookup"><span data-stu-id="cbba4-142">The best way to optimize this code is to implement some form of client-side batching of these calls.</span></span> <span data-ttu-id="cbba4-143">Mas há uma maneira simples de aumentar o desempenho do código simplesmente encapsulando a sequência de chamadas em uma transação.</span><span class="sxs-lookup"><span data-stu-id="cbba4-143">But there is a simple way to increase the performance of this code by simply wrapping the sequence of calls in a transaction.</span></span> <span data-ttu-id="cbba4-144">Este é o mesmo código que usa uma transação.</span><span class="sxs-lookup"><span data-stu-id="cbba4-144">Here is the same code that uses a transaction.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();
        SqlTransaction transaction = conn.BeginTransaction();

        foreach (string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn, transaction);
            cmd.ExecuteNonQuery();
        }

        transaction.Commit();
    }

<span data-ttu-id="cbba4-145">Na verdade, as transações estão sendo usadas nos dois exemplos.</span><span class="sxs-lookup"><span data-stu-id="cbba4-145">Transactions are actually being used in both of these examples.</span></span> <span data-ttu-id="cbba4-146">No primeiro exemplo, cada chamada individual é uma transação implícita.</span><span class="sxs-lookup"><span data-stu-id="cbba4-146">In the first example, each individual call is an implicit transaction.</span></span> <span data-ttu-id="cbba4-147">No segundo exemplo, uma transação explícita encapsula todas as chamadas.</span><span class="sxs-lookup"><span data-stu-id="cbba4-147">In the second example, an explicit transaction wraps all of the calls.</span></span> <span data-ttu-id="cbba4-148">Conforme a documentação do [log de transações write-ahead](https://msdn.microsoft.com/library/ms186259.aspx), registros de log são liberados no disco quando a transação é confirmada.</span><span class="sxs-lookup"><span data-stu-id="cbba4-148">Per the documentation for the [write-ahead transaction log](https://msdn.microsoft.com/library/ms186259.aspx), log records are flushed to the disk when the transaction commits.</span></span> <span data-ttu-id="cbba4-149">Então, incluindo mais chamadas em uma transação, a gravação no log de transações pode atrasar até que a transação seja confirmada.</span><span class="sxs-lookup"><span data-stu-id="cbba4-149">So by including more calls in a transaction, the write to the transaction log can delay until the transaction is committed.</span></span> <span data-ttu-id="cbba4-150">Na verdade, você está habilitando o envio em lote das gravações no log de transações do servidor.</span><span class="sxs-lookup"><span data-stu-id="cbba4-150">In effect, you are enabling batching for the writes to the server’s transaction log.</span></span>

<span data-ttu-id="cbba4-151">A tabela a seguir mostra alguns resultados de teste ad hoc.</span><span class="sxs-lookup"><span data-stu-id="cbba4-151">The following table shows some ad-hoc testing results.</span></span> <span data-ttu-id="cbba4-152">Os testes executaram as mesmas inserções sequenciais, com e sem transações.</span><span class="sxs-lookup"><span data-stu-id="cbba4-152">The tests performed the same sequential inserts with and without transactions.</span></span> <span data-ttu-id="cbba4-153">Para obter uma perspectiva maior, o primeiro conjunto de testes foi executado remotamente de um laptop para o banco de dados no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cbba4-153">For more perspective, the first set of tests ran remotely from a laptop to the database in Microsoft Azure.</span></span> <span data-ttu-id="cbba4-154">O segundo conjunto de testes foi executado de um serviço de nuvem e de um banco de dados localizados no mesmo datacenter do Microsoft Azure (Oeste dos Estados Unidos).</span><span class="sxs-lookup"><span data-stu-id="cbba4-154">The second set of tests ran from a cloud service and database that both resided within the same Microsoft Azure datacenter (West US).</span></span> <span data-ttu-id="cbba4-155">A tabela a seguir mostra a duração em milissegundos de inserções sequenciais, com e sem transações.</span><span class="sxs-lookup"><span data-stu-id="cbba4-155">The following table shows the duration in milliseconds of sequential inserts with and without transactions.</span></span>

<span data-ttu-id="cbba4-156">**Local para o Azure**:</span><span class="sxs-lookup"><span data-stu-id="cbba4-156">**On-Premises to Azure**:</span></span>

| <span data-ttu-id="cbba4-157">Operações</span><span class="sxs-lookup"><span data-stu-id="cbba4-157">Operations</span></span> | <span data-ttu-id="cbba4-158">Sem transação (ms)</span><span class="sxs-lookup"><span data-stu-id="cbba4-158">No Transaction (ms)</span></span> | <span data-ttu-id="cbba4-159">Com transação (ms)</span><span class="sxs-lookup"><span data-stu-id="cbba4-159">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cbba4-160">1</span><span class="sxs-lookup"><span data-stu-id="cbba4-160">1</span></span> |<span data-ttu-id="cbba4-161">130</span><span class="sxs-lookup"><span data-stu-id="cbba4-161">130</span></span> |<span data-ttu-id="cbba4-162">402</span><span class="sxs-lookup"><span data-stu-id="cbba4-162">402</span></span> |
| <span data-ttu-id="cbba4-163">10</span><span class="sxs-lookup"><span data-stu-id="cbba4-163">10</span></span> |<span data-ttu-id="cbba4-164">1208</span><span class="sxs-lookup"><span data-stu-id="cbba4-164">1208</span></span> |<span data-ttu-id="cbba4-165">1226</span><span class="sxs-lookup"><span data-stu-id="cbba4-165">1226</span></span> |
| <span data-ttu-id="cbba4-166">100</span><span class="sxs-lookup"><span data-stu-id="cbba4-166">100</span></span> |<span data-ttu-id="cbba4-167">12662</span><span class="sxs-lookup"><span data-stu-id="cbba4-167">12662</span></span> |<span data-ttu-id="cbba4-168">10395</span><span class="sxs-lookup"><span data-stu-id="cbba4-168">10395</span></span> |
| <span data-ttu-id="cbba4-169">1000</span><span class="sxs-lookup"><span data-stu-id="cbba4-169">1000</span></span> |<span data-ttu-id="cbba4-170">128852</span><span class="sxs-lookup"><span data-stu-id="cbba4-170">128852</span></span> |<span data-ttu-id="cbba4-171">102917</span><span class="sxs-lookup"><span data-stu-id="cbba4-171">102917</span></span> |

<span data-ttu-id="cbba4-172">**Do Azure para o Azure (mesmo datacenter)**:</span><span class="sxs-lookup"><span data-stu-id="cbba4-172">**Azure to Azure (same datacenter)**:</span></span>

| <span data-ttu-id="cbba4-173">Operações</span><span class="sxs-lookup"><span data-stu-id="cbba4-173">Operations</span></span> | <span data-ttu-id="cbba4-174">Sem transação (ms)</span><span class="sxs-lookup"><span data-stu-id="cbba4-174">No Transaction (ms)</span></span> | <span data-ttu-id="cbba4-175">Com transação (ms)</span><span class="sxs-lookup"><span data-stu-id="cbba4-175">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cbba4-176">1</span><span class="sxs-lookup"><span data-stu-id="cbba4-176">1</span></span> |<span data-ttu-id="cbba4-177">21</span><span class="sxs-lookup"><span data-stu-id="cbba4-177">21</span></span> |<span data-ttu-id="cbba4-178">26</span><span class="sxs-lookup"><span data-stu-id="cbba4-178">26</span></span> |
| <span data-ttu-id="cbba4-179">10</span><span class="sxs-lookup"><span data-stu-id="cbba4-179">10</span></span> |<span data-ttu-id="cbba4-180">220</span><span class="sxs-lookup"><span data-stu-id="cbba4-180">220</span></span> |<span data-ttu-id="cbba4-181">56</span><span class="sxs-lookup"><span data-stu-id="cbba4-181">56</span></span> |
| <span data-ttu-id="cbba4-182">100</span><span class="sxs-lookup"><span data-stu-id="cbba4-182">100</span></span> |<span data-ttu-id="cbba4-183">2145</span><span class="sxs-lookup"><span data-stu-id="cbba4-183">2145</span></span> |<span data-ttu-id="cbba4-184">341</span><span class="sxs-lookup"><span data-stu-id="cbba4-184">341</span></span> |
| <span data-ttu-id="cbba4-185">1000</span><span class="sxs-lookup"><span data-stu-id="cbba4-185">1000</span></span> |<span data-ttu-id="cbba4-186">21479</span><span class="sxs-lookup"><span data-stu-id="cbba4-186">21479</span></span> |<span data-ttu-id="cbba4-187">2756</span><span class="sxs-lookup"><span data-stu-id="cbba4-187">2756</span></span> |

> [!NOTE]
> <span data-ttu-id="cbba4-188">Os resultados não são parâmetros de comparação.</span><span class="sxs-lookup"><span data-stu-id="cbba4-188">Results are not benchmarks.</span></span> <span data-ttu-id="cbba4-189">Consulte a [Observação sobre os resultados de tempo neste tópico](#note-about-timing-results-in-this-topic)</span><span class="sxs-lookup"><span data-stu-id="cbba4-189">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="cbba4-190">Com base nos resultados do teste anterior, a disposição de uma única operação em uma transação reduz o desempenho.</span><span class="sxs-lookup"><span data-stu-id="cbba4-190">Based on the previous test results, wrapping a single operation in a transaction actually decreases performance.</span></span> <span data-ttu-id="cbba4-191">Mas, à medida que você aumenta o número de operações em uma única transação, o aprimoramento do desempenho fica mais evidente.</span><span class="sxs-lookup"><span data-stu-id="cbba4-191">But as you increase the number of operations within a single transaction, the performance improvement becomes more marked.</span></span> <span data-ttu-id="cbba4-192">A diferença de desempenho também é mais perceptível quando todas as operações ocorrem dentro do datacenter do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cbba4-192">The performance difference is also more noticeable when all operations occur within the Microsoft Azure datacenter.</span></span> <span data-ttu-id="cbba4-193">O aumento da latência devido ao uso do Banco de Dados SQL fora do datacenter do Microsoft Azure ofusca o ganho de desempenho do uso das transações.</span><span class="sxs-lookup"><span data-stu-id="cbba4-193">The increased latency of using SQL Database from outside the Microsoft Azure datacenter overshadows the performance gain of using transactions.</span></span>

<span data-ttu-id="cbba4-194">Embora o uso das transações possa aumentar o desempenho, continue a [seguir as práticas recomendadas para transações e conexões](https://msdn.microsoft.com/library/ms187484.aspx).</span><span class="sxs-lookup"><span data-stu-id="cbba4-194">Although the use of transactions can increase performance, continue to [observe best practices for transactions and connections](https://msdn.microsoft.com/library/ms187484.aspx).</span></span> <span data-ttu-id="cbba4-195">Mantenha a transação a mais curta possível, e feche a conexão do banco de dados após a conclusão do trabalho.</span><span class="sxs-lookup"><span data-stu-id="cbba4-195">Keep the transaction as short as possible, and close the database connection after the work completes.</span></span> <span data-ttu-id="cbba4-196">A instrução using no exemplo anterior garante o fechamento da conexão após a conclusão do bloco de códigos subsequente.</span><span class="sxs-lookup"><span data-stu-id="cbba4-196">The using statement in the previous example assures that the connection is closed when the subsequent code block completes.</span></span>

<span data-ttu-id="cbba4-197">O exemplo anterior demonstra que você pode adicionar uma transação local a qualquer código ADO.NET com duas linhas.</span><span class="sxs-lookup"><span data-stu-id="cbba4-197">The previous example demonstrates that you can add a local transaction to any ADO.NET code with two lines.</span></span> <span data-ttu-id="cbba4-198">As transações oferecem uma maneira rápida de melhorar o desempenho do código que faz as operações de inserção sequencial, atualização e de exclusão.</span><span class="sxs-lookup"><span data-stu-id="cbba4-198">Transactions offer a quick way to improve the performance of code that makes sequential insert, update, and delete operations.</span></span> <span data-ttu-id="cbba4-199">No entanto, para obter o melhor desempenho, considere alterar o código ainda mais para aproveitar o envio em lote no lado do cliente, por exemplo, com os parâmetros com valor de tabela.</span><span class="sxs-lookup"><span data-stu-id="cbba4-199">However, for the fastest performance, consider changing the code further to take advantage of client-side batching, such as table-valued parameters.</span></span>

<span data-ttu-id="cbba4-200">Para saber mais sobre transações no ADO.NET, consulte [Transações locais no ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).</span><span class="sxs-lookup"><span data-stu-id="cbba4-200">For more information about transactions in ADO.NET, see [Local Transactions in ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).</span></span>

### <a name="table-valued-parameters"></a><span data-ttu-id="cbba4-201">Parâmetros com valor de tabela</span><span class="sxs-lookup"><span data-stu-id="cbba4-201">Table-valued parameters</span></span>
<span data-ttu-id="cbba4-202">Os parâmetros com valor de tabela oferecem suporte a tipos de tabela definidos pelo usuário como parâmetros em instruções Transact-SQL, procedimentos armazenados e funções.</span><span class="sxs-lookup"><span data-stu-id="cbba4-202">Table-valued parameters support user-defined table types as parameters in Transact-SQL statements, stored procedures, and functions.</span></span> <span data-ttu-id="cbba4-203">Essa técnica de envio em lote no lado do cliente permite o envio de várias linhas de dados dentro do parâmetro com valor de tabela.</span><span class="sxs-lookup"><span data-stu-id="cbba4-203">This client-side batching technique allows you to send multiple rows of data within the table-valued parameter.</span></span> <span data-ttu-id="cbba4-204">Para usar os parâmetros com valor de tabela, primeiro defina um tipo de tabela.</span><span class="sxs-lookup"><span data-stu-id="cbba4-204">To use table-valued parameters, first define a table type.</span></span> <span data-ttu-id="cbba4-205">A instrução Transact-SQL a seguir cria um tipo de tabela denominado **MyTableType**.</span><span class="sxs-lookup"><span data-stu-id="cbba4-205">The following Transact-SQL statement creates a table type named **MyTableType**.</span></span>

    CREATE TYPE MyTableType AS TABLE 
    ( mytext TEXT,
      num INT );


<span data-ttu-id="cbba4-206">No código, você cria uma **DataTable** com exatamente os mesmos nomes e tipos do tipo de tabela.</span><span class="sxs-lookup"><span data-stu-id="cbba4-206">In code, you create a **DataTable** with the exact same names and types of the table type.</span></span> <span data-ttu-id="cbba4-207">Passe essa **DataTable** em um parâmetro em uma consulta de texto ou em uma chamada de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="cbba4-207">Pass this **DataTable** in a parameter in a text query or stored procedure call.</span></span> <span data-ttu-id="cbba4-208">O exemplo a seguir mostra detalhes desta técnica:</span><span class="sxs-lookup"><span data-stu-id="cbba4-208">The following example shows this technique:</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        DataTable table = new DataTable();
        // Add columns and rows. The following is a simple example.
        table.Columns.Add("mytext", typeof(string));
        table.Columns.Add("num", typeof(int));    
        for (var i = 0; i < 10; i++)
        {
            table.Rows.Add(DateTime.Now.ToString(), DateTime.Now.Millisecond);
        }

        SqlCommand cmd = new SqlCommand(
            "INSERT INTO MyTable(mytext, num) SELECT mytext, num FROM @TestTvp",
            connection);

        cmd.Parameters.Add(
            new SqlParameter()
            {
                ParameterName = "@TestTvp",
                SqlDbType = SqlDbType.Structured,
                TypeName = "MyTableType",
                Value = table,
            });

        cmd.ExecuteNonQuery();
    }

<span data-ttu-id="cbba4-209">No exemplo anterior, o objeto **SqlCommand** insere linhas de um parâmetro com valor de tabela, **@TestTvp**.</span><span class="sxs-lookup"><span data-stu-id="cbba4-209">In the previous example, the **SqlCommand** object inserts rows from a table-valued parameter, **@TestTvp**.</span></span> <span data-ttu-id="cbba4-210">O objeto **DataTable** criado anteriormente é atribuído a esse parâmetro com o método **SqlCommand.Parameters.Add**.</span><span class="sxs-lookup"><span data-stu-id="cbba4-210">The previously created **DataTable** object is assigned to this parameter with the **SqlCommand.Parameters.Add** method.</span></span> <span data-ttu-id="cbba4-211">O envio em lote de inserções em uma chamada aumenta consideravelmente o desempenho com inserções sequenciais.</span><span class="sxs-lookup"><span data-stu-id="cbba4-211">Batching the inserts in one call significantly increases the performance over sequential inserts.</span></span>

<span data-ttu-id="cbba4-212">Para melhorar ainda mais o exemplo anterior, use um procedimento armazenado e não um comando baseado em texto.</span><span class="sxs-lookup"><span data-stu-id="cbba4-212">To improve the previous example further, use a stored procedure instead of a text-based command.</span></span> <span data-ttu-id="cbba4-213">O comando Transact-SQL a seguir cria um procedimento armazenado que utiliza o parâmetro com valor de tabela **SimpleTestTableType** .</span><span class="sxs-lookup"><span data-stu-id="cbba4-213">The following Transact-SQL command creates a stored procedure that takes the **SimpleTestTableType** table-valued parameter.</span></span>

    CREATE PROCEDURE [dbo].[sp_InsertRows] 
    @TestTvp as MyTableType READONLY
    AS
    BEGIN
    INSERT INTO MyTable(mytext, num) 
    SELECT mytext, num FROM @TestTvp
    END
    GO

<span data-ttu-id="cbba4-214">Em seguida, altere a declaração do objeto **SqlCommand** no exemplo de código anterior para o seguinte.</span><span class="sxs-lookup"><span data-stu-id="cbba4-214">Then change the **SqlCommand** object declaration in the previous code example to the following.</span></span>

    SqlCommand cmd = new SqlCommand("sp_InsertRows", connection);
    cmd.CommandType = CommandType.StoredProcedure;

<span data-ttu-id="cbba4-215">Na maioria dos casos, os parâmetros com valor de tabela têm um desempenho equivalente ou superior às outras técnicas de envio em lote.</span><span class="sxs-lookup"><span data-stu-id="cbba4-215">In most cases, table-valued parameters have equivalent or better performance than other batching techniques.</span></span> <span data-ttu-id="cbba4-216">Normalmente, a preferência fica com os parâmetros com valor de tabela, pois são mais flexíveis do que as outras opções.</span><span class="sxs-lookup"><span data-stu-id="cbba4-216">Table-valued parameters are often preferable, because they are more flexible than other options.</span></span> <span data-ttu-id="cbba4-217">Por exemplo, outras técnicas, como cópia em massa do SQL, só permitem a inserção de novas linhas.</span><span class="sxs-lookup"><span data-stu-id="cbba4-217">For example, other techniques, such as SQL bulk copy, only permit the insertion of new rows.</span></span> <span data-ttu-id="cbba4-218">Porém, com os parâmetros com valor de tabela, você pode usar lógica no procedimento armazenado para determinar quais linhas serão atualizações e quais serão inserções.</span><span class="sxs-lookup"><span data-stu-id="cbba4-218">But with table-valued parameters, you can use logic in the stored procedure to determine which rows are updates and which are inserts.</span></span> <span data-ttu-id="cbba4-219">O tipo de tabela também pode ser modificado para conter uma coluna "Operação" que indica se a linha especificada deve ser inserida, atualizada ou excluída.</span><span class="sxs-lookup"><span data-stu-id="cbba4-219">The table type can also be modified to contain an “Operation” column that indicates whether the specified row should be inserted, updated, or deleted.</span></span>

<span data-ttu-id="cbba4-220">A tabela a seguir mostra os resultados do teste ad hoc do uso de parâmetros com valor de tabela em milissegundos.</span><span class="sxs-lookup"><span data-stu-id="cbba4-220">The following table shows ad-hoc test results for the use of table-valued parameters in milliseconds.</span></span>

| <span data-ttu-id="cbba4-221">Operações</span><span class="sxs-lookup"><span data-stu-id="cbba4-221">Operations</span></span> | <span data-ttu-id="cbba4-222">Local para o Azure (ms)</span><span class="sxs-lookup"><span data-stu-id="cbba4-222">On-Premises to Azure (ms)</span></span> | <span data-ttu-id="cbba4-223">Mesmo datacenter do Azure (ms)</span><span class="sxs-lookup"><span data-stu-id="cbba4-223">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cbba4-224">1</span><span class="sxs-lookup"><span data-stu-id="cbba4-224">1</span></span> |<span data-ttu-id="cbba4-225">124</span><span class="sxs-lookup"><span data-stu-id="cbba4-225">124</span></span> |<span data-ttu-id="cbba4-226">32</span><span class="sxs-lookup"><span data-stu-id="cbba4-226">32</span></span> |
| <span data-ttu-id="cbba4-227">10</span><span class="sxs-lookup"><span data-stu-id="cbba4-227">10</span></span> |<span data-ttu-id="cbba4-228">131</span><span class="sxs-lookup"><span data-stu-id="cbba4-228">131</span></span> |<span data-ttu-id="cbba4-229">25</span><span class="sxs-lookup"><span data-stu-id="cbba4-229">25</span></span> |
| <span data-ttu-id="cbba4-230">100</span><span class="sxs-lookup"><span data-stu-id="cbba4-230">100</span></span> |<span data-ttu-id="cbba4-231">338</span><span class="sxs-lookup"><span data-stu-id="cbba4-231">338</span></span> |<span data-ttu-id="cbba4-232">51</span><span class="sxs-lookup"><span data-stu-id="cbba4-232">51</span></span> |
| <span data-ttu-id="cbba4-233">1000</span><span class="sxs-lookup"><span data-stu-id="cbba4-233">1000</span></span> |<span data-ttu-id="cbba4-234">2615</span><span class="sxs-lookup"><span data-stu-id="cbba4-234">2615</span></span> |<span data-ttu-id="cbba4-235">382</span><span class="sxs-lookup"><span data-stu-id="cbba4-235">382</span></span> |
| <span data-ttu-id="cbba4-236">10000</span><span class="sxs-lookup"><span data-stu-id="cbba4-236">10000</span></span> |<span data-ttu-id="cbba4-237">23830</span><span class="sxs-lookup"><span data-stu-id="cbba4-237">23830</span></span> |<span data-ttu-id="cbba4-238">3586</span><span class="sxs-lookup"><span data-stu-id="cbba4-238">3586</span></span> |

> [!NOTE]
> <span data-ttu-id="cbba4-239">Os resultados não são parâmetros de comparação.</span><span class="sxs-lookup"><span data-stu-id="cbba4-239">Results are not benchmarks.</span></span> <span data-ttu-id="cbba4-240">Consulte a [Observação sobre os resultados de tempo neste tópico](#note-about-timing-results-in-this-topic)</span><span class="sxs-lookup"><span data-stu-id="cbba4-240">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="cbba4-241">O ganho de desempenho com o envio em lote fica imediatamente aparente.</span><span class="sxs-lookup"><span data-stu-id="cbba4-241">The performance gain from batching is immediately apparent.</span></span> <span data-ttu-id="cbba4-242">No teste sequencial anterior, 1000 operações levaram 129 segundos fora do datacenter e 21 segundos dentro do datacenter.</span><span class="sxs-lookup"><span data-stu-id="cbba4-242">In the previous sequential test, 1000 operations took 129 seconds outside the datacenter and 21 seconds from within the datacenter.</span></span> <span data-ttu-id="cbba4-243">Mas, com os parâmetros com valor de tabela, 1000 operações levam somente 2,6 segundos fora do datacenter e 0,4 segundos dentro do datacenter.</span><span class="sxs-lookup"><span data-stu-id="cbba4-243">But with table-valued parameters, 1000 operations take only 2.6 seconds outside the datacenter and 0.4 seconds within the datacenter.</span></span>

<span data-ttu-id="cbba4-244">Para saber mais sobre parâmetros com valor de tabela, consulte [Parâmetros com valor de tabela](https://msdn.microsoft.com/library/bb510489.aspx).</span><span class="sxs-lookup"><span data-stu-id="cbba4-244">For more information on table-valued parameters, see [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

### <a name="sql-bulk-copy"></a><span data-ttu-id="cbba4-245">Cópia em massa do SQL</span><span class="sxs-lookup"><span data-stu-id="cbba4-245">SQL bulk copy</span></span>
<span data-ttu-id="cbba4-246">Cópia em massa do SQL é outra maneira de inserir grandes quantidades de dados em um banco de dados de destino.</span><span class="sxs-lookup"><span data-stu-id="cbba4-246">SQL bulk copy is another way to insert large amounts of data into a target database.</span></span> <span data-ttu-id="cbba4-247">Aplicativos .NET podem usar a classe **SqlBulkCopy** para executar operações de inserção em massa.</span><span class="sxs-lookup"><span data-stu-id="cbba4-247">.NET applications can use the **SqlBulkCopy** class to perform bulk insert operations.</span></span> <span data-ttu-id="cbba4-248">**SqlBulkCopy** tem uma função semelhante à ferramenta de linha de comando, **Bcp.exe**, ou à instrução Transact-SQL, **BULK INSERT**.</span><span class="sxs-lookup"><span data-stu-id="cbba4-248">**SqlBulkCopy** is similar in function to the command-line tool, **Bcp.exe**, or the Transact-SQL statement, **BULK INSERT**.</span></span> <span data-ttu-id="cbba4-249">O exemplo de código a seguir mostra como copiar em massa as linhas na tabela de origem **DataTable**, para a tabela de destino no SQL Server, MyTable.</span><span class="sxs-lookup"><span data-stu-id="cbba4-249">The following code example shows how to bulk copy the rows in the source **DataTable**, table, to the destination table in SQL Server, MyTable.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        using (SqlBulkCopy bulkCopy = new SqlBulkCopy(connection))
        {
            bulkCopy.DestinationTableName = "MyTable";
            bulkCopy.ColumnMappings.Add("mytext", "mytext");
            bulkCopy.ColumnMappings.Add("num", "num");
            bulkCopy.WriteToServer(table);
        }
    }

<span data-ttu-id="cbba4-250">Há alguns casos nos quais é preferível usar a cópia em massa do que os parâmetros com valor de tabela.</span><span class="sxs-lookup"><span data-stu-id="cbba4-250">There are some cases where bulk copy is preferred over table-valued parameters.</span></span> <span data-ttu-id="cbba4-251">Consulte a tabela de comparação de Parâmetros com valor de tabela versus operações BULK INSERT no tópico [Parâmetros com valor de tabela](https://msdn.microsoft.com/library/bb510489.aspx).</span><span class="sxs-lookup"><span data-stu-id="cbba4-251">See the comparison table of Table-Valued parameters versus BULK INSERT operations in the topic [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

<span data-ttu-id="cbba4-252">Os seguintes resultados do teste ad hoc mostram o desempenho do envio em lote com **SqlBulkCopy** em milissegundos.</span><span class="sxs-lookup"><span data-stu-id="cbba4-252">The following ad-hoc test results show the performance of batching with **SqlBulkCopy** in milliseconds.</span></span>

| <span data-ttu-id="cbba4-253">Operações</span><span class="sxs-lookup"><span data-stu-id="cbba4-253">Operations</span></span> | <span data-ttu-id="cbba4-254">Local para o Azure (ms)</span><span class="sxs-lookup"><span data-stu-id="cbba4-254">On-Premises to Azure (ms)</span></span> | <span data-ttu-id="cbba4-255">Mesmo datacenter do Azure (ms)</span><span class="sxs-lookup"><span data-stu-id="cbba4-255">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cbba4-256">1</span><span class="sxs-lookup"><span data-stu-id="cbba4-256">1</span></span> |<span data-ttu-id="cbba4-257">433</span><span class="sxs-lookup"><span data-stu-id="cbba4-257">433</span></span> |<span data-ttu-id="cbba4-258">57</span><span class="sxs-lookup"><span data-stu-id="cbba4-258">57</span></span> |
| <span data-ttu-id="cbba4-259">10</span><span class="sxs-lookup"><span data-stu-id="cbba4-259">10</span></span> |<span data-ttu-id="cbba4-260">441</span><span class="sxs-lookup"><span data-stu-id="cbba4-260">441</span></span> |<span data-ttu-id="cbba4-261">32</span><span class="sxs-lookup"><span data-stu-id="cbba4-261">32</span></span> |
| <span data-ttu-id="cbba4-262">100</span><span class="sxs-lookup"><span data-stu-id="cbba4-262">100</span></span> |<span data-ttu-id="cbba4-263">636</span><span class="sxs-lookup"><span data-stu-id="cbba4-263">636</span></span> |<span data-ttu-id="cbba4-264">53</span><span class="sxs-lookup"><span data-stu-id="cbba4-264">53</span></span> |
| <span data-ttu-id="cbba4-265">1000</span><span class="sxs-lookup"><span data-stu-id="cbba4-265">1000</span></span> |<span data-ttu-id="cbba4-266">2535</span><span class="sxs-lookup"><span data-stu-id="cbba4-266">2535</span></span> |<span data-ttu-id="cbba4-267">341</span><span class="sxs-lookup"><span data-stu-id="cbba4-267">341</span></span> |
| <span data-ttu-id="cbba4-268">10000</span><span class="sxs-lookup"><span data-stu-id="cbba4-268">10000</span></span> |<span data-ttu-id="cbba4-269">21605</span><span class="sxs-lookup"><span data-stu-id="cbba4-269">21605</span></span> |<span data-ttu-id="cbba4-270">2737</span><span class="sxs-lookup"><span data-stu-id="cbba4-270">2737</span></span> |

> [!NOTE]
> <span data-ttu-id="cbba4-271">Os resultados não são parâmetros de comparação.</span><span class="sxs-lookup"><span data-stu-id="cbba4-271">Results are not benchmarks.</span></span> <span data-ttu-id="cbba4-272">Consulte a [Observação sobre os resultados de tempo neste tópico](#note-about-timing-results-in-this-topic)</span><span class="sxs-lookup"><span data-stu-id="cbba4-272">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="cbba4-273">Em lotes menores, o uso dos parâmetros com valor de tabela superaram a classe **SqlBulkCopy** .</span><span class="sxs-lookup"><span data-stu-id="cbba4-273">In smaller batch sizes, the use table-valued parameters outperformed the **SqlBulkCopy** class.</span></span> <span data-ttu-id="cbba4-274">No entanto, **SqlBulkCopy** teve um desempenho de 12 a 31% mais rápido do que os parâmetros com valor de tabela nos testes de 1.000 e 10.000 linhas.</span><span class="sxs-lookup"><span data-stu-id="cbba4-274">However, **SqlBulkCopy** performed 12-31% faster than table-valued parameters for the tests of 1,000 and 10,000 rows.</span></span> <span data-ttu-id="cbba4-275">Assim como os parâmetros com valor de tabela, **SqlBulkCopy** é uma boa opção para inserções em lotes, especialmente quando comparado ao desempenho de operações que não são feitas em lotes.</span><span class="sxs-lookup"><span data-stu-id="cbba4-275">Like table-valued parameters, **SqlBulkCopy** is a good option for batched inserts, especially when compared to the performance of non-batched operations.</span></span>

<span data-ttu-id="cbba4-276">Para saber mais sobre a cópia em massa no ADO.NET, consulte [Operações de cópia em massa no SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).</span><span class="sxs-lookup"><span data-stu-id="cbba4-276">For more information on bulk copy in ADO.NET, see [Bulk Copy Operations in SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).</span></span>

### <a name="multiple-row-parameterized-insert-statements"></a><span data-ttu-id="cbba4-277">Instruções INSERT com parâmetros de várias linhas</span><span class="sxs-lookup"><span data-stu-id="cbba4-277">Multiple-row Parameterized INSERT statements</span></span>
<span data-ttu-id="cbba4-278">Uma alternativa para lotes pequenos é a construção de uma grande instrução INSERT com parâmetros que insira várias linhas.</span><span class="sxs-lookup"><span data-stu-id="cbba4-278">One alternative for small batches is to construct a large parameterized INSERT statement that inserts multiple rows.</span></span> <span data-ttu-id="cbba4-279">O exemplo de código a seguir demonstra esta técnica.</span><span class="sxs-lookup"><span data-stu-id="cbba4-279">The following code example demonstrates this technique.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        string insertCommand = "INSERT INTO [MyTable] ( mytext, num ) " +
            "VALUES (@p1, @p2), (@p3, @p4), (@p5, @p6), (@p7, @p8), (@p9, @p10)";

        SqlCommand cmd = new SqlCommand(insertCommand, connection);

        for (int i = 1; i <= 10; i += 2)
        {
            cmd.Parameters.Add(new SqlParameter("@p" + i.ToString(), "test"));
            cmd.Parameters.Add(new SqlParameter("@p" + (i+1).ToString(), i));
        }

        cmd.ExecuteNonQuery();
    }


<span data-ttu-id="cbba4-280">Esse exemplo tem como objetivo mostrar o conceito básico.</span><span class="sxs-lookup"><span data-stu-id="cbba4-280">This example is meant to show the basic concept.</span></span> <span data-ttu-id="cbba4-281">Um cenário mais realista percorreria as entidades necessárias a fim de construir simultaneamente a cadeia de caracteres de consulta e os parâmetros de comando.</span><span class="sxs-lookup"><span data-stu-id="cbba4-281">A more realistic scenario would loop through the required entities to construct the query string and the command parameters simultaneously.</span></span> <span data-ttu-id="cbba4-282">Você está limitado a um total de 2100 parâmetros de consulta, e isso limita o número total de linhas que podem ser processadas dessa maneira.</span><span class="sxs-lookup"><span data-stu-id="cbba4-282">You are limited to a total of 2100 query parameters, so this limits the total number of rows that can be processed in this manner.</span></span>

<span data-ttu-id="cbba4-283">Os seguintes resultados do teste ad hoc mostram o desempenho desse tipo de instrução insert em milissegundos.</span><span class="sxs-lookup"><span data-stu-id="cbba4-283">The following ad-hoc test results show the performance of this type of insert statement in milliseconds.</span></span>

| <span data-ttu-id="cbba4-284">Operações</span><span class="sxs-lookup"><span data-stu-id="cbba4-284">Operations</span></span> | <span data-ttu-id="cbba4-285">Parâmetros com valor de tabela (ms)</span><span class="sxs-lookup"><span data-stu-id="cbba4-285">Table-valued parameters (ms)</span></span> | <span data-ttu-id="cbba4-286">Instrução INSERT única (ms)</span><span class="sxs-lookup"><span data-stu-id="cbba4-286">Single-statement INSERT (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cbba4-287">1</span><span class="sxs-lookup"><span data-stu-id="cbba4-287">1</span></span> |<span data-ttu-id="cbba4-288">32</span><span class="sxs-lookup"><span data-stu-id="cbba4-288">32</span></span> |<span data-ttu-id="cbba4-289">20</span><span class="sxs-lookup"><span data-stu-id="cbba4-289">20</span></span> |
| <span data-ttu-id="cbba4-290">10</span><span class="sxs-lookup"><span data-stu-id="cbba4-290">10</span></span> |<span data-ttu-id="cbba4-291">30</span><span class="sxs-lookup"><span data-stu-id="cbba4-291">30</span></span> |<span data-ttu-id="cbba4-292">25</span><span class="sxs-lookup"><span data-stu-id="cbba4-292">25</span></span> |
| <span data-ttu-id="cbba4-293">100</span><span class="sxs-lookup"><span data-stu-id="cbba4-293">100</span></span> |<span data-ttu-id="cbba4-294">33</span><span class="sxs-lookup"><span data-stu-id="cbba4-294">33</span></span> |<span data-ttu-id="cbba4-295">51</span><span class="sxs-lookup"><span data-stu-id="cbba4-295">51</span></span> |

> [!NOTE]
> <span data-ttu-id="cbba4-296">Os resultados não são parâmetros de comparação.</span><span class="sxs-lookup"><span data-stu-id="cbba4-296">Results are not benchmarks.</span></span> <span data-ttu-id="cbba4-297">Consulte a [Observação sobre os resultados de tempo neste tópico](#note-about-timing-results-in-this-topic)</span><span class="sxs-lookup"><span data-stu-id="cbba4-297">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="cbba4-298">Essa abordagem pode ser ligeiramente mais rápida para lotes com menos de 100 linhas.</span><span class="sxs-lookup"><span data-stu-id="cbba4-298">This approach can be slightly faster for batches that are less than 100 rows.</span></span> <span data-ttu-id="cbba4-299">Embora o aprimoramento seja pequeno, essa técnica é outra opção que pode funcionar bem em seu cenário de aplicativo específico.</span><span class="sxs-lookup"><span data-stu-id="cbba4-299">Although the improvement is small, this technique is another option that might work well in your specific application scenario.</span></span>

### <a name="dataadapter"></a><span data-ttu-id="cbba4-300">DataAdapter</span><span class="sxs-lookup"><span data-stu-id="cbba4-300">DataAdapter</span></span>
<span data-ttu-id="cbba4-301">A classe **DataAdapter** permite que você modifique um objeto **DataSet** e envie as alterações como operações INSERT, UPDATE e DELETE.</span><span class="sxs-lookup"><span data-stu-id="cbba4-301">The **DataAdapter** class allows you to modify a **DataSet** object and then submit the changes as INSERT, UPDATE, and DELETE operations.</span></span> <span data-ttu-id="cbba4-302">Se você estiver usando o **DataAdapter** dessa maneira, é importante observar são realizadas chamadas separadas para cada operação distinta.</span><span class="sxs-lookup"><span data-stu-id="cbba4-302">If you are using the **DataAdapter** in this manner, it is important to note that separate calls are made for each distinct operation.</span></span> <span data-ttu-id="cbba4-303">Para melhorar o desempenho, use a propriedade **UpdateBatchSize** de acordo com o número de operações que devem ser enviadas em lote por vez.</span><span class="sxs-lookup"><span data-stu-id="cbba4-303">To improve performance, use the **UpdateBatchSize** property to the number of operations that should be batched at a time.</span></span> <span data-ttu-id="cbba4-304">Para saber mais, consulte [Executando operações em lote usando DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).</span><span class="sxs-lookup"><span data-stu-id="cbba4-304">For more information, see [Performing Batch Operations Using DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).</span></span>

### <a name="entity-framework"></a><span data-ttu-id="cbba4-305">Entity Framework</span><span class="sxs-lookup"><span data-stu-id="cbba4-305">Entity framework</span></span>
<span data-ttu-id="cbba4-306">No momento, o Entity Framework não oferece suporte para o envio em lote.</span><span class="sxs-lookup"><span data-stu-id="cbba4-306">Entity Framework does not currently support batching.</span></span> <span data-ttu-id="cbba4-307">Vários desenvolvedores da comunidade tentaram demonstrar soluções alternativas, como a substituição do método **SaveChanges** .</span><span class="sxs-lookup"><span data-stu-id="cbba4-307">Different developers in the community have attempted to demonstrate workarounds, such as override the **SaveChanges** method.</span></span> <span data-ttu-id="cbba4-308">Mas normalmente as soluções são complexas e personalizadas para o aplicativo e o modelo de dados.</span><span class="sxs-lookup"><span data-stu-id="cbba4-308">But the solutions are typically complex and customized to the application and data model.</span></span> <span data-ttu-id="cbba4-309">Atualmente, o projeto codeplex do Entity Framework tem uma página de discussão sobre essa solicitação de recurso.</span><span class="sxs-lookup"><span data-stu-id="cbba4-309">The Entity Framework codeplex project currently has a discussion page on this feature request.</span></span> <span data-ttu-id="cbba4-310">Para exibir esta discussão, confira [Anotações da reunião de design – 2 de agosto de 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).</span><span class="sxs-lookup"><span data-stu-id="cbba4-310">To view this discussion, see [Design Meeting Notes - August 2, 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).</span></span>

### <a name="xml"></a><span data-ttu-id="cbba4-311">XML</span><span class="sxs-lookup"><span data-stu-id="cbba4-311">XML</span></span>
<span data-ttu-id="cbba4-312">Para abordarmos tudo, achamos que é importante falar sobre XML como uma estratégia de envio em lote.</span><span class="sxs-lookup"><span data-stu-id="cbba4-312">For completeness, we feel that it is important to talk about XML as a batching strategy.</span></span> <span data-ttu-id="cbba4-313">No entanto, o uso de XML não apresenta vantagens sobre outros métodos e impõe várias desvantagens.</span><span class="sxs-lookup"><span data-stu-id="cbba4-313">However, the use of XML has no advantages over other methods and several disadvantages.</span></span> <span data-ttu-id="cbba4-314">A abordagem é semelhante aos parâmetros com valor de tabela, mas um arquivo ou cadeia de caracteres XML é passado para um procedimento armazenado, em vez de uma tabela definida pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="cbba4-314">The approach is similar to table-valued parameters, but an XML file or string is passed to a stored procedure instead of a user-defined table.</span></span> <span data-ttu-id="cbba4-315">O procedimento armazenado analisa os comandos no procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="cbba4-315">The stored procedure parses the commands in the stored procedure.</span></span>

<span data-ttu-id="cbba4-316">Há várias desvantagens nessa abordagem:</span><span class="sxs-lookup"><span data-stu-id="cbba4-316">There are several disadvantages to this approach:</span></span>

* <span data-ttu-id="cbba4-317">Trabalhar com XML pode ser complicado e pode apresentar muitos erros.</span><span class="sxs-lookup"><span data-stu-id="cbba4-317">Working with XML can be cumbersome and error prone.</span></span>
* <span data-ttu-id="cbba4-318">Analisar o XML no banco de dados pode causar a utilização de muita CPU.</span><span class="sxs-lookup"><span data-stu-id="cbba4-318">Parsing the XML on the database can be CPU-intensive.</span></span>
* <span data-ttu-id="cbba4-319">Na maioria dos casos, esse método é mais lento se comparado ao uso de parâmetros com valor de tabela.</span><span class="sxs-lookup"><span data-stu-id="cbba4-319">In most cases, this method is slower than table-valued parameters.</span></span>

<span data-ttu-id="cbba4-320">Por esses motivos, o uso de XML para consultas em lote não é recomendado.</span><span class="sxs-lookup"><span data-stu-id="cbba4-320">For these reasons, the use of XML for batch queries is not recommended.</span></span>

## <a name="batching-considerations"></a><span data-ttu-id="cbba4-321">Considerações sobre o envio em lote</span><span class="sxs-lookup"><span data-stu-id="cbba4-321">Batching considerations</span></span>
<span data-ttu-id="cbba4-322">As seções a seguir fornecem mais orientações sobre o uso do envio em lote em aplicativos do Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="cbba4-322">The following sections provide more guidance for the use of batching in SQL Database applications.</span></span>

### <a name="tradeoffs"></a><span data-ttu-id="cbba4-323">Compensações</span><span class="sxs-lookup"><span data-stu-id="cbba4-323">Tradeoffs</span></span>
<span data-ttu-id="cbba4-324">Dependendo de sua arquitetura, o envio em lote pode envolver uma compensação entre desempenho e resiliência.</span><span class="sxs-lookup"><span data-stu-id="cbba4-324">Depending on your architecture, batching can involve a tradeoff between performance and resiliency.</span></span> <span data-ttu-id="cbba4-325">Por exemplo, considere o cenário no qual sua função fica inesperadamente inativa.</span><span class="sxs-lookup"><span data-stu-id="cbba4-325">For example, consider the scenario where your role unexpectedly goes down.</span></span> <span data-ttu-id="cbba4-326">Se você perder uma linha de dados, o impacto é menor do que o impacto de perder um lote grande de linhas não enviadas.</span><span class="sxs-lookup"><span data-stu-id="cbba4-326">If you lose one row of data, the impact is smaller than the impact of losing a large batch of unsubmitted rows.</span></span> <span data-ttu-id="cbba4-327">Há um risco maior quando você armazena em buffer as linhas antes de enviá-las ao banco de dados em um período especificado.</span><span class="sxs-lookup"><span data-stu-id="cbba4-327">There is a greater risk when you buffer rows before sending them to the database in a specified time window.</span></span>

<span data-ttu-id="cbba4-328">Devido a essa compensação, avalie o tipo das operações que você envia em lote.</span><span class="sxs-lookup"><span data-stu-id="cbba4-328">Because of this tradeoff, evaluate the type of operations that you batch.</span></span> <span data-ttu-id="cbba4-329">Utilize o envio em lote de forma mais agressiva (lotes maiores e períodos maiores) com dados menos críticos.</span><span class="sxs-lookup"><span data-stu-id="cbba4-329">Batch more aggressively (larger batches and longer time windows) with data that is less critical.</span></span>

### <a name="batch-size"></a><span data-ttu-id="cbba4-330">Tamanho do lote</span><span class="sxs-lookup"><span data-stu-id="cbba4-330">Batch size</span></span>
<span data-ttu-id="cbba4-331">Em nossos testes, geralmente não houve vantagem em dividir lotes grandes em partes menores.</span><span class="sxs-lookup"><span data-stu-id="cbba4-331">In our tests, there was typically no advantage to breaking large batches into smaller chunks.</span></span> <span data-ttu-id="cbba4-332">Na verdade, frequentemente essa subdivisão resultou em um desempenho mais lento do que enviar um único lote grande.</span><span class="sxs-lookup"><span data-stu-id="cbba4-332">In fact, this subdivision often resulted in slower performance than submitting a single large batch.</span></span> <span data-ttu-id="cbba4-333">Por exemplo, considere um cenário no qual você deseja inserir 1000 linhas.</span><span class="sxs-lookup"><span data-stu-id="cbba4-333">For example, consider a scenario where you want to insert 1000 rows.</span></span> <span data-ttu-id="cbba4-334">A tabela a seguir mostra quanto tempo leva para usar parâmetros com valor de tabela para inserir 1000 linhas divididas em lotes menores.</span><span class="sxs-lookup"><span data-stu-id="cbba4-334">The following table shows how long it takes to use table-valued parameters to insert 1000 rows when divided into smaller batches.</span></span>

| <span data-ttu-id="cbba4-335">Tamanho do lote</span><span class="sxs-lookup"><span data-stu-id="cbba4-335">Batch size</span></span> | <span data-ttu-id="cbba4-336">Iterações</span><span class="sxs-lookup"><span data-stu-id="cbba4-336">Iterations</span></span> | <span data-ttu-id="cbba4-337">Parâmetros com valor de tabela (ms)</span><span class="sxs-lookup"><span data-stu-id="cbba4-337">Table-valued parameters (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cbba4-338">1000</span><span class="sxs-lookup"><span data-stu-id="cbba4-338">1000</span></span> |<span data-ttu-id="cbba4-339">1</span><span class="sxs-lookup"><span data-stu-id="cbba4-339">1</span></span> |<span data-ttu-id="cbba4-340">347</span><span class="sxs-lookup"><span data-stu-id="cbba4-340">347</span></span> |
| <span data-ttu-id="cbba4-341">500</span><span class="sxs-lookup"><span data-stu-id="cbba4-341">500</span></span> |<span data-ttu-id="cbba4-342">2</span><span class="sxs-lookup"><span data-stu-id="cbba4-342">2</span></span> |<span data-ttu-id="cbba4-343">355</span><span class="sxs-lookup"><span data-stu-id="cbba4-343">355</span></span> |
| <span data-ttu-id="cbba4-344">100</span><span class="sxs-lookup"><span data-stu-id="cbba4-344">100</span></span> |<span data-ttu-id="cbba4-345">10</span><span class="sxs-lookup"><span data-stu-id="cbba4-345">10</span></span> |<span data-ttu-id="cbba4-346">465</span><span class="sxs-lookup"><span data-stu-id="cbba4-346">465</span></span> |
| <span data-ttu-id="cbba4-347">50</span><span class="sxs-lookup"><span data-stu-id="cbba4-347">50</span></span> |<span data-ttu-id="cbba4-348">20</span><span class="sxs-lookup"><span data-stu-id="cbba4-348">20</span></span> |<span data-ttu-id="cbba4-349">630</span><span class="sxs-lookup"><span data-stu-id="cbba4-349">630</span></span> |

> [!NOTE]
> <span data-ttu-id="cbba4-350">Os resultados não são parâmetros de comparação.</span><span class="sxs-lookup"><span data-stu-id="cbba4-350">Results are not benchmarks.</span></span> <span data-ttu-id="cbba4-351">Consulte a [Observação sobre os resultados de tempo neste tópico](#note-about-timing-results-in-this-topic)</span><span class="sxs-lookup"><span data-stu-id="cbba4-351">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="cbba4-352">Veja que o melhor desempenho para 1000 linhas é enviá-las ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="cbba4-352">You can see that the best performance for 1000 rows is to submit them all at once.</span></span> <span data-ttu-id="cbba4-353">Em outros testes (não mostrados aqui), houve um pequeno ganho de desempenho ao dividir um lote de 10000 linhas em dois lotes de 5000.</span><span class="sxs-lookup"><span data-stu-id="cbba4-353">In other tests (not shown here) there was a small performance gain to break a 10000 row batch into two batches of 5000.</span></span> <span data-ttu-id="cbba4-354">Como o esquema da tabela para esses testes é relativamente simples, você pode executar testes em seus dados e tamanhos de lote específicos a fim de verificar essas conclusões.</span><span class="sxs-lookup"><span data-stu-id="cbba4-354">But the table schema for these tests is relatively simple, so you should perform tests on your specific data and batch sizes to verify these findings.</span></span>

<span data-ttu-id="cbba4-355">Outro fator a ser considerado é que, se o lote total ficar muito grande, o Banco de Dados SQL poderá aplicar uma limitação e recusar-se a confirmar o lote.</span><span class="sxs-lookup"><span data-stu-id="cbba4-355">Another factor to consider is that if the total batch becomes too large, SQL Database might throttle and refuse to commit the batch.</span></span> <span data-ttu-id="cbba4-356">Para obter melhores resultados, teste seu cenário específico para determinar se há um tamanho de lote ideal.</span><span class="sxs-lookup"><span data-stu-id="cbba4-356">For the best results, test your specific scenario to determine if there is an ideal batch size.</span></span> <span data-ttu-id="cbba4-357">Torne o tamanho do lote configurável no tempo de execução para permitir ajustes rápidos com base no desempenho ou em erros.</span><span class="sxs-lookup"><span data-stu-id="cbba4-357">Make the batch size configurable at runtime to enable quick adjustments based on performance or errors.</span></span>

<span data-ttu-id="cbba4-358">Por fim, equilibre o tamanho do lote com os riscos associados ao envio em lote.</span><span class="sxs-lookup"><span data-stu-id="cbba4-358">Finally, balance the size of the batch with the risks associated with batching.</span></span> <span data-ttu-id="cbba4-359">Se houver erros transitórios ou a função falhar, considere as consequências da repetição da operação ou da perda dos dados no lote.</span><span class="sxs-lookup"><span data-stu-id="cbba4-359">If there are transient errors or the role fails, consider the consequences of retrying the operation or of losing the data in the batch.</span></span>

### <a name="parallel-processing"></a><span data-ttu-id="cbba4-360">Processamento paralelo</span><span class="sxs-lookup"><span data-stu-id="cbba4-360">Parallel processing</span></span>
<span data-ttu-id="cbba4-361">E se você adotasse a abordagem de redução do tamanho de lote, mas usasse vários threads para executar o trabalho?</span><span class="sxs-lookup"><span data-stu-id="cbba4-361">What if you took the approach of reducing the batch size but used multiple threads to execute the work?</span></span> <span data-ttu-id="cbba4-362">Novamente, nossos testes mostraram que vários lotes menores multithreaded geralmente apresentaram um desempenho pior do que um único lote maior.</span><span class="sxs-lookup"><span data-stu-id="cbba4-362">Again, our tests showed that several smaller multithreaded batches typically performed worse than a single larger batch.</span></span> <span data-ttu-id="cbba4-363">O teste a seguir tenta inserir 1000 linhas em um ou mais lotes paralelos.</span><span class="sxs-lookup"><span data-stu-id="cbba4-363">The following test attempts to insert 1000 rows in one or more parallel batches.</span></span> <span data-ttu-id="cbba4-364">Este teste mostra como uma quantidade maior de lotes simultâneos na verdade diminuiu o desempenho.</span><span class="sxs-lookup"><span data-stu-id="cbba4-364">This test shows how more simultaneous batches actually decreased performance.</span></span>

| <span data-ttu-id="cbba4-365">Tamanho do lote [Iterações]</span><span class="sxs-lookup"><span data-stu-id="cbba4-365">Batch size [Iterations]</span></span> | <span data-ttu-id="cbba4-366">Dois threads (ms)</span><span class="sxs-lookup"><span data-stu-id="cbba4-366">Two threads (ms)</span></span> | <span data-ttu-id="cbba4-367">Quatro threads (ms)</span><span class="sxs-lookup"><span data-stu-id="cbba4-367">Four threads (ms)</span></span> | <span data-ttu-id="cbba4-368">Seis threads (ms)</span><span class="sxs-lookup"><span data-stu-id="cbba4-368">Six threads (ms)</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cbba4-369">1000 [1]</span><span class="sxs-lookup"><span data-stu-id="cbba4-369">1000 [1]</span></span> |<span data-ttu-id="cbba4-370">277</span><span class="sxs-lookup"><span data-stu-id="cbba4-370">277</span></span> |<span data-ttu-id="cbba4-371">315</span><span class="sxs-lookup"><span data-stu-id="cbba4-371">315</span></span> |<span data-ttu-id="cbba4-372">266</span><span class="sxs-lookup"><span data-stu-id="cbba4-372">266</span></span> |
| <span data-ttu-id="cbba4-373">500 [2]</span><span class="sxs-lookup"><span data-stu-id="cbba4-373">500 [2]</span></span> |<span data-ttu-id="cbba4-374">548</span><span class="sxs-lookup"><span data-stu-id="cbba4-374">548</span></span> |<span data-ttu-id="cbba4-375">278</span><span class="sxs-lookup"><span data-stu-id="cbba4-375">278</span></span> |<span data-ttu-id="cbba4-376">256</span><span class="sxs-lookup"><span data-stu-id="cbba4-376">256</span></span> |
| <span data-ttu-id="cbba4-377">250 [4]</span><span class="sxs-lookup"><span data-stu-id="cbba4-377">250 [4]</span></span> |<span data-ttu-id="cbba4-378">405</span><span class="sxs-lookup"><span data-stu-id="cbba4-378">405</span></span> |<span data-ttu-id="cbba4-379">329</span><span class="sxs-lookup"><span data-stu-id="cbba4-379">329</span></span> |<span data-ttu-id="cbba4-380">265</span><span class="sxs-lookup"><span data-stu-id="cbba4-380">265</span></span> |
| <span data-ttu-id="cbba4-381">100 [10]</span><span class="sxs-lookup"><span data-stu-id="cbba4-381">100 [10]</span></span> |<span data-ttu-id="cbba4-382">488</span><span class="sxs-lookup"><span data-stu-id="cbba4-382">488</span></span> |<span data-ttu-id="cbba4-383">439</span><span class="sxs-lookup"><span data-stu-id="cbba4-383">439</span></span> |<span data-ttu-id="cbba4-384">391</span><span class="sxs-lookup"><span data-stu-id="cbba4-384">391</span></span> |

> [!NOTE]
> <span data-ttu-id="cbba4-385">Os resultados não são parâmetros de comparação.</span><span class="sxs-lookup"><span data-stu-id="cbba4-385">Results are not benchmarks.</span></span> <span data-ttu-id="cbba4-386">Consulte a [Observação sobre os resultados de tempo neste tópico](#note-about-timing-results-in-this-topic)</span><span class="sxs-lookup"><span data-stu-id="cbba4-386">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="cbba4-387">Há várias razões possíveis para a degradação do desempenho devido ao paralelismo:</span><span class="sxs-lookup"><span data-stu-id="cbba4-387">There are several potential reasons for the degradation in performance due to parallelism:</span></span>

* <span data-ttu-id="cbba4-388">Há várias chamadas simultâneas de rede em vez de uma.</span><span class="sxs-lookup"><span data-stu-id="cbba4-388">There are multiple simultaneous network calls instead of one.</span></span>
* <span data-ttu-id="cbba4-389">Várias operações em uma única tabela podem resultar em contenção e bloqueio.</span><span class="sxs-lookup"><span data-stu-id="cbba4-389">Multiple operations against a single table can result in contention and blocking.</span></span>
* <span data-ttu-id="cbba4-390">Há sobrecargas associadas ao multithreading.</span><span class="sxs-lookup"><span data-stu-id="cbba4-390">There are overheads associated with multithreading.</span></span>
* <span data-ttu-id="cbba4-391">O fardo de abrir várias conexões supera o benefício do processamento paralelo.</span><span class="sxs-lookup"><span data-stu-id="cbba4-391">The expense of opening multiple connections outweighs the benefit of parallel processing.</span></span>

<span data-ttu-id="cbba4-392">Se você selecionar tabelas ou bancos de dados diferentes, poderá perceber algum ganho de desempenho com essa estratégia.</span><span class="sxs-lookup"><span data-stu-id="cbba4-392">If you target different tables or databases, it is possible to see some performance gain with this strategy.</span></span> <span data-ttu-id="cbba4-393">A fragmentação ou federações do banco de dados seria um cenário para essa abordagem.</span><span class="sxs-lookup"><span data-stu-id="cbba4-393">Database sharding or federations would be a scenario for this approach.</span></span> <span data-ttu-id="cbba4-394">A fragmentação usa vários bancos de dados e encaminha dados diferentes para cada banco de dados.</span><span class="sxs-lookup"><span data-stu-id="cbba4-394">Sharding uses multiple databases and routes different data to each database.</span></span> <span data-ttu-id="cbba4-395">Se cada lote pequeno for encaminhada para um banco de dados diferente, então a execução das operações em paralelo pode ser mais eficiente.</span><span class="sxs-lookup"><span data-stu-id="cbba4-395">If each small batch is going to a different database, then performing the operations in parallel can be more efficient.</span></span> <span data-ttu-id="cbba4-396">No entanto, o ganho de desempenho não é considerável o suficiente para usá-lo como base para uma decisão de uso da fragmentação de banco de dados em sua solução.</span><span class="sxs-lookup"><span data-stu-id="cbba4-396">However, the performance gain is not significant enough to use as the basis for a decision to use database sharding in your solution.</span></span>

<span data-ttu-id="cbba4-397">Em alguns designs, a execução paralela de lotes menores pode resultar em uma produtividade maior das solicitações em um sistema sob carga.</span><span class="sxs-lookup"><span data-stu-id="cbba4-397">In some designs, parallel execution of smaller batches can result in improved throughput of requests in a system under load.</span></span> <span data-ttu-id="cbba4-398">Nesse caso, embora seja mais rápido processar um único lote maior, o processamento de vários lotes em paralelo pode ser mais eficiente.</span><span class="sxs-lookup"><span data-stu-id="cbba4-398">In this case, even though it is quicker to process a single larger batch, processing multiple batches in parallel might be more efficient.</span></span>

<span data-ttu-id="cbba4-399">Se você usar a execução paralela, considere a possibilidade de controlar o número máximo de threads de trabalho.</span><span class="sxs-lookup"><span data-stu-id="cbba4-399">If you do use parallel execution, consider controlling the maximum number of worker threads.</span></span> <span data-ttu-id="cbba4-400">Uma quantidade menor poderia resultar em menos contenção e um tempo de execução mais rápido.</span><span class="sxs-lookup"><span data-stu-id="cbba4-400">A smaller number might result in less contention and a faster execution time.</span></span> <span data-ttu-id="cbba4-401">Além disso, considere a carga adicional que isso impõe sobre o banco de dados de destino, tanto nas conexões quanto nas transações.</span><span class="sxs-lookup"><span data-stu-id="cbba4-401">Also, consider the additional load that this places on the target database both in connections and transactions.</span></span>

### <a name="related-performance-factors"></a><span data-ttu-id="cbba4-402">Fatores de desempenho relacionados</span><span class="sxs-lookup"><span data-stu-id="cbba4-402">Related performance factors</span></span>
<span data-ttu-id="cbba4-403">As orientações típicas sobre o desempenho do banco de dados também dizem respeito ao envio em lote.</span><span class="sxs-lookup"><span data-stu-id="cbba4-403">Typical guidance on database performance also affects batching.</span></span> <span data-ttu-id="cbba4-404">Por exemplo, ocorre a redução do desempenho de inserção para tabelas com uma chave primária grande ou vários índices não clusterizados.</span><span class="sxs-lookup"><span data-stu-id="cbba4-404">For example, insert performance is reduced for tables that have a large primary key or many nonclustered indexes.</span></span>

<span data-ttu-id="cbba4-405">Se parâmetros com valor de tabela usarem um procedimento armazenado, você poderá usar o comando **SET NOCOUNT ON** no início do procedimento.</span><span class="sxs-lookup"><span data-stu-id="cbba4-405">If table-valued parameters use a stored procedure, you can use the command **SET NOCOUNT ON** at the beginning of the procedure.</span></span> <span data-ttu-id="cbba4-406">Essa instrução suprime o retorno da contagem de linhas afetadas no procedimento.</span><span class="sxs-lookup"><span data-stu-id="cbba4-406">This statement suppresses the return of the count of the affected rows in the procedure.</span></span> <span data-ttu-id="cbba4-407">No entanto, em nossos testes, o uso de **SET NOCOUNT ON** não teve qualquer efeito ou diminuiu o desempenho.</span><span class="sxs-lookup"><span data-stu-id="cbba4-407">However, in our tests, the use of **SET NOCOUNT ON** either had no effect or decreased performance.</span></span> <span data-ttu-id="cbba4-408">O procedimento armazenado de teste foi simples com um único comando **INSERT** do parâmetro com valor de tabela.</span><span class="sxs-lookup"><span data-stu-id="cbba4-408">The test stored procedure was simple with a single **INSERT** command from the table-valued parameter.</span></span> <span data-ttu-id="cbba4-409">É possível que outros procedimentos armazenados mais complexos possam se beneficiar dessa instrução.</span><span class="sxs-lookup"><span data-stu-id="cbba4-409">It is possible that more complex stored procedures would benefit from this statement.</span></span> <span data-ttu-id="cbba4-410">Mas não suponha que a adição de **SET NOCOUNT ON** ao procedimento armazenado aprimorará automaticamente o desempenho.</span><span class="sxs-lookup"><span data-stu-id="cbba4-410">But don’t assume that adding **SET NOCOUNT ON** to your stored procedure automatically improves performance.</span></span> <span data-ttu-id="cbba4-411">Para entender o efeito, teste o procedimento armazenado com e sem a instrução **SET NOCOUNT ON** instrução.</span><span class="sxs-lookup"><span data-stu-id="cbba4-411">To understand the effect, test your stored procedure with and without the **SET NOCOUNT ON** statement.</span></span>

## <a name="batching-scenarios"></a><span data-ttu-id="cbba4-412">Cenários de envio em lote</span><span class="sxs-lookup"><span data-stu-id="cbba4-412">Batching scenarios</span></span>
<span data-ttu-id="cbba4-413">As seções a seguir descrevem como usar os parâmetros com valor de tabela em três cenários de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cbba4-413">The following sections describe how to use table-valued parameters in three application scenarios.</span></span> <span data-ttu-id="cbba4-414">O primeiro cenário mostra como o armazenamento em buffer e o envio em lote podem trabalhar juntos.</span><span class="sxs-lookup"><span data-stu-id="cbba4-414">The first scenario shows how buffering and batching can work together.</span></span> <span data-ttu-id="cbba4-415">O segundo cenário melhora o desempenho por meio da execução de operações mestre-detalhes em uma chamada com um único procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="cbba4-415">The second scenario improves performance by performing master-detail operations in a single stored procedure call.</span></span> <span data-ttu-id="cbba4-416">O cenário final mostra como usar os parâmetros com valor de tabela em uma operação "UPSERT".</span><span class="sxs-lookup"><span data-stu-id="cbba4-416">The final scenario shows how to use table-valued parameters in an “UPSERT” operation.</span></span>

### <a name="buffering"></a><span data-ttu-id="cbba4-417">Armazenamento em buffer</span><span class="sxs-lookup"><span data-stu-id="cbba4-417">Buffering</span></span>
<span data-ttu-id="cbba4-418">Embora alguns cenários sejam candidatos óbvios ao envio em lote, há muitos cenários que poderiam se beneficiar do envio em lote por meio do processamento atrasado.</span><span class="sxs-lookup"><span data-stu-id="cbba4-418">Although there are some scenarios that are obvious candidate for batching, there are many scenarios that could take advantage of batching by delayed processing.</span></span> <span data-ttu-id="cbba4-419">No entanto, o processamento atrasado também representa um risco maior de que os dados sejam perdidos no caso de uma falha inesperada.</span><span class="sxs-lookup"><span data-stu-id="cbba4-419">However, delayed processing also carries a greater risk that the data is lost in the event of an unexpected failure.</span></span> <span data-ttu-id="cbba4-420">É importante entender esse risco e considerar as consequências.</span><span class="sxs-lookup"><span data-stu-id="cbba4-420">It is important to understand this risk and consider the consequences.</span></span>

<span data-ttu-id="cbba4-421">Por exemplo, considere um aplicativo Web que controla o histórico de navegação de cada usuário.</span><span class="sxs-lookup"><span data-stu-id="cbba4-421">For example, consider a web application that tracks the navigation history of each user.</span></span> <span data-ttu-id="cbba4-422">Em cada solicitação de página, o aplicativo pode fazer uma chamada de banco de dados para registrar o modo de exibição de página do usuário.</span><span class="sxs-lookup"><span data-stu-id="cbba4-422">On each page request, the application could make a database call to record the user’s page view.</span></span> <span data-ttu-id="cbba4-423">Mas é possível obter mais desempenho e escalabilidade por meio do armazenamento em buffer das atividades de navegação dos usuários e enviar esses dados para o banco de dados em lotes.</span><span class="sxs-lookup"><span data-stu-id="cbba4-423">But higher performance and scalability can be achieved by buffering the users’ navigation activities and then sending this data to the database in batches.</span></span> <span data-ttu-id="cbba4-424">Você pode disparar a atualização do banco de dados por tempo decorrido e/ou tamanho do buffer.</span><span class="sxs-lookup"><span data-stu-id="cbba4-424">You can trigger the database update by elapsed time and/or buffer size.</span></span> <span data-ttu-id="cbba4-425">Por exemplo, uma regra poderia especificar que o lote deve ser processado após 20 segundos, ou quando o buffer atingir 1000 itens.</span><span class="sxs-lookup"><span data-stu-id="cbba4-425">For example, a rule could specify that the batch should be processed after 20 seconds or when the buffer reaches 1000 items.</span></span>

<span data-ttu-id="cbba4-426">O exemplo de código a seguir usa [Extensões Reativas - Rx](https://msdn.microsoft.com/data/gg577609) para processar eventos em buffer gerados por uma classe de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="cbba4-426">The following code example uses [Reactive Extensions - Rx](https://msdn.microsoft.com/data/gg577609) to process buffered events raised by a monitoring class.</span></span> <span data-ttu-id="cbba4-427">Quando o buffer é preenchido ou um tempo limite é atingido, o lote de dados do usuário é enviado ao banco de dados com um parâmetro com valor de tabela.</span><span class="sxs-lookup"><span data-stu-id="cbba4-427">When the buffer fills or a timeout is reached, the batch of user data is sent to the database with a table-valued parameter.</span></span>

<span data-ttu-id="cbba4-428">A classe NavHistoryData a seguir modela os detalhes de navegação do usuário.</span><span class="sxs-lookup"><span data-stu-id="cbba4-428">The following NavHistoryData class models the user navigation details.</span></span> <span data-ttu-id="cbba4-429">Ela contém informações básicas, como o identificador do usuário, a URL acessada e o tempo de acesso.</span><span class="sxs-lookup"><span data-stu-id="cbba4-429">It contains basic information such as the user identifier, the URL accessed, and the access time.</span></span>

    public class NavHistoryData
    {
        public NavHistoryData(int userId, string url, DateTime accessTime)
        { UserId = userId; URL = url; AccessTime = accessTime; }
        public int UserId { get; set; }
        public string URL { get; set; }
        public DateTime AccessTime { get; set; }
    }

<span data-ttu-id="cbba4-430">A classe NavHistoryDataMonitor é responsável pelo armazenamento em buffer dos dados de navegação do usuário no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="cbba4-430">The NavHistoryDataMonitor class is responsible for buffering the user navigation data to the database.</span></span> <span data-ttu-id="cbba4-431">Ela contém um método, RecordUserNavigationEntry, que responde gerando um evento **OnAdded** .</span><span class="sxs-lookup"><span data-stu-id="cbba4-431">It contains a method, RecordUserNavigationEntry, which responds by raising an **OnAdded** event.</span></span> <span data-ttu-id="cbba4-432">O código a seguir mostra a lógica do construtor que usa Rx para criar uma coleção observável com base no evento.</span><span class="sxs-lookup"><span data-stu-id="cbba4-432">The following code shows the constructor logic that uses Rx to create an observable collection based on the event.</span></span> <span data-ttu-id="cbba4-433">Em seguida, ele assina essa coleção observável com o método de Buffer.</span><span class="sxs-lookup"><span data-stu-id="cbba4-433">It then subscribes to this observable collection with the Buffer method.</span></span> <span data-ttu-id="cbba4-434">A sobrecarga especifica que o buffer deve ser enviado a cada 20 segundos ou 1000 entradas.</span><span class="sxs-lookup"><span data-stu-id="cbba4-434">The overload specifies that the buffer should be sent every 20 seconds or 1000 entries.</span></span>

    public NavHistoryDataMonitor()
    {
        var observableData =
            Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

        observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
    }

<span data-ttu-id="cbba4-435">O manipulador converte todos os itens armazenados em buffer em um tipo com valor de tabela e passa esse tipo para um procedimento armazenado que processa o lote.</span><span class="sxs-lookup"><span data-stu-id="cbba4-435">The handler converts all of the buffered items into a table-valued type and then passes this type to a stored procedure that processes the batch.</span></span> <span data-ttu-id="cbba4-436">O código a seguir mostra a definição completa para as classes NavHistoryDataEventArgs e NavHistoryDataMonitor.</span><span class="sxs-lookup"><span data-stu-id="cbba4-436">The following code shows the complete definition for both the NavHistoryDataEventArgs and the NavHistoryDataMonitor classes.</span></span>

    public class NavHistoryDataEventArgs : System.EventArgs
    {
        public NavHistoryDataEventArgs(NavHistoryData data) { Data = data; }
        public NavHistoryData Data { get; set; }
    }

    public class NavHistoryDataMonitor
    {
        public event EventHandler<NavHistoryDataEventArgs> OnAdded;

        public NavHistoryDataMonitor()
        {
            var observableData =
                Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

            observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
        }

        public void RecordUserNavigationEntry(NavHistoryData data)
        {    
            if (OnAdded != null)
                OnAdded(this, new NavHistoryDataEventArgs(data));
        }

        protected void Handler(IList<EventPattern<NavHistoryDataEventArgs>> items)
        {
            DataTable navHistoryBatch = new DataTable("NavigationHistoryBatch");
            navHistoryBatch.Columns.Add("UserId", typeof(int));
            navHistoryBatch.Columns.Add("URL", typeof(string));
            navHistoryBatch.Columns.Add("AccessTime", typeof(DateTime));
            foreach (EventPattern<NavHistoryDataEventArgs> item in items)
            {
                NavHistoryData data = item.EventArgs.Data;
                navHistoryBatch.Rows.Add(data.UserId, data.URL, data.AccessTime);
            }

            using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
            {
                connection.Open();

                SqlCommand cmd = new SqlCommand("sp_RecordUserNavigation", connection);
                cmd.CommandType = CommandType.StoredProcedure;

                cmd.Parameters.Add(
                    new SqlParameter()
                    {
                        ParameterName = "@NavHistoryBatch",
                        SqlDbType = SqlDbType.Structured,
                        TypeName = "NavigationHistoryTableType",
                        Value = navHistoryBatch,
                    });

                cmd.ExecuteNonQuery();
            }
        }
    }

<span data-ttu-id="cbba4-437">Para usar essa classe de armazenamento em buffer, o aplicativo cria um objeto NavHistoryDataMonitor estático.</span><span class="sxs-lookup"><span data-stu-id="cbba4-437">To use this buffering class, the application creates a static NavHistoryDataMonitor object.</span></span> <span data-ttu-id="cbba4-438">Sempre que um usuário acessa uma página, o aplicativo chama o método NavHistoryDataMonitor.RecordUserNavigationEntry.</span><span class="sxs-lookup"><span data-stu-id="cbba4-438">Each time a user accesses a page, the application calls the NavHistoryDataMonitor.RecordUserNavigationEntry method.</span></span> <span data-ttu-id="cbba4-439">A lógica do buffer continua a fim de enviar em lotes essas entradas ao banco de dados.</span><span class="sxs-lookup"><span data-stu-id="cbba4-439">The buffering logic proceeds to take care of sending these entries to the database in batches.</span></span>

### <a name="master-detail"></a><span data-ttu-id="cbba4-440">Detalhes da tabela mestra</span><span class="sxs-lookup"><span data-stu-id="cbba4-440">Master detail</span></span>
<span data-ttu-id="cbba4-441">Parâmetros com valor de tabela são úteis para cenários INSERT simples.</span><span class="sxs-lookup"><span data-stu-id="cbba4-441">Table-valued parameters are useful for simple INSERT scenarios.</span></span> <span data-ttu-id="cbba4-442">No entanto, pode ser mais desafiador executar inserções em lotes que envolvem mais de uma tabela.</span><span class="sxs-lookup"><span data-stu-id="cbba4-442">However, it can be more challenging to batch inserts that involve more than one table.</span></span> <span data-ttu-id="cbba4-443">O cenário "mestre/detalhes" é um bom exemplo.</span><span class="sxs-lookup"><span data-stu-id="cbba4-443">The “master/detail” scenario is a good example.</span></span> <span data-ttu-id="cbba4-444">A tabela mestra identifica a entidade principal.</span><span class="sxs-lookup"><span data-stu-id="cbba4-444">The master table identifies the primary entity.</span></span> <span data-ttu-id="cbba4-445">Uma ou mais tabelas de detalhes armazenam mais dados sobre a entidade.</span><span class="sxs-lookup"><span data-stu-id="cbba4-445">One or more detail tables store more data about the entity.</span></span> <span data-ttu-id="cbba4-446">Nesse cenário, as relações de chave estrangeiras impõem a relação de detalhes a uma entidade mestre exclusiva.</span><span class="sxs-lookup"><span data-stu-id="cbba4-446">In this scenario, foreign key relationships enforce the relationship of details to a unique master entity.</span></span> <span data-ttu-id="cbba4-447">Considere uma versão simplificada de uma tabela PurchaseOrder e sua tabela associada OrderDetail.</span><span class="sxs-lookup"><span data-stu-id="cbba4-447">Consider a simplified version of a PurchaseOrder table and its associated OrderDetail table.</span></span> <span data-ttu-id="cbba4-448">O Transact-SQL a seguir cria a tabela PurchaseOrder com quatro colunas: OrderID, OrderDate, CustomerID e Status.</span><span class="sxs-lookup"><span data-stu-id="cbba4-448">The following Transact-SQL creates the PurchaseOrder table with four columns: OrderID, OrderDate, CustomerID, and Status.</span></span>

    CREATE TABLE [dbo].[PurchaseOrder](
    [OrderID] [int] IDENTITY(1,1) NOT NULL,
    [OrderDate] [datetime] NOT NULL,
    [CustomerID] [int] NOT NULL,
    [Status] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrder] 
    PRIMARY KEY CLUSTERED ( [OrderID] ASC ))

<span data-ttu-id="cbba4-449">Cada pedido contém uma ou mais compras de produtos.</span><span class="sxs-lookup"><span data-stu-id="cbba4-449">Each order contains one or more product purchases.</span></span> <span data-ttu-id="cbba4-450">Essas informações são capturadas na tabela PurchaseOrderDetail.</span><span class="sxs-lookup"><span data-stu-id="cbba4-450">This information is captured in the PurchaseOrderDetail table.</span></span> <span data-ttu-id="cbba4-451">O Transact-SQL a seguir cria a tabela PurchaseOrderDetail com cinco colunas: OrderID, OrderDetailID, ProductID, UnitPrice e OrderQty.</span><span class="sxs-lookup"><span data-stu-id="cbba4-451">The following Transact-SQL creates the PurchaseOrderDetail table with five columns: OrderID, OrderDetailID, ProductID, UnitPrice, and OrderQty.</span></span>

    CREATE TABLE [dbo].[PurchaseOrderDetail](
    [OrderID] [int] NOT NULL,
    [OrderDetailID] [int] IDENTITY(1,1) NOT NULL,
    [ProductID] [int] NOT NULL,
    [UnitPrice] [money] NULL,
    [OrderQty] [smallint] NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrderDetail] PRIMARY KEY CLUSTERED 
    ( [OrderID] ASC, [OrderDetailID] ASC ))

<span data-ttu-id="cbba4-452">A coluna OrderID na tabela PurchaseOrderDetail deve fazer referência a um pedido da tabela PurchaseOrder.</span><span class="sxs-lookup"><span data-stu-id="cbba4-452">The OrderID column in the PurchaseOrderDetail table must reference an order from the PurchaseOrder table.</span></span> <span data-ttu-id="cbba4-453">A seguinte definição de uma chave estrangeira impõe essa restrição.</span><span class="sxs-lookup"><span data-stu-id="cbba4-453">The following definition of a foreign key enforces this constraint.</span></span>

    ALTER TABLE [dbo].[PurchaseOrderDetail]  WITH CHECK ADD 
    CONSTRAINT [FK_OrderID_PurchaseOrder] FOREIGN KEY([OrderID])
    REFERENCES [dbo].[PurchaseOrder] ([OrderID])

<span data-ttu-id="cbba4-454">Para usar parâmetros com valor de tabela, você deve ter um tipo de tabela definido pelo usuário para cada tabela de destino.</span><span class="sxs-lookup"><span data-stu-id="cbba4-454">In order to use table-valued parameters, you must have one user-defined table type for each target table.</span></span>

    CREATE TYPE PurchaseOrderTableType AS TABLE 
    ( OrderID INT,
      OrderDate DATETIME,
      CustomerID INT,
      Status NVARCHAR(50) );
    GO

    CREATE TYPE PurchaseOrderDetailTableType AS TABLE 
    ( OrderID INT,
      ProductID INT,
      UnitPrice MONEY,
      OrderQty SMALLINT );
    GO

<span data-ttu-id="cbba4-455">Em seguida, defina um procedimento armazenado que aceite tabelas desses tipos.</span><span class="sxs-lookup"><span data-stu-id="cbba4-455">Then define a stored procedure that accepts tables of these types.</span></span> <span data-ttu-id="cbba4-456">Esse procedimento permite que um aplicativo envie em lote localmente um conjunto de pedidos e detalhes do pedido em uma única chamada.</span><span class="sxs-lookup"><span data-stu-id="cbba4-456">This procedure allows an application to locally batch a set of orders and order details in a single call.</span></span> <span data-ttu-id="cbba4-457">O seguinte Transact-SQL fornece a declaração completa do procedimento armazenado para esse exemplo de ordem de compra.</span><span class="sxs-lookup"><span data-stu-id="cbba4-457">The following Transact-SQL provides the complete stored procedure declaration for this purchase order example.</span></span>

    CREATE PROCEDURE sp_InsertOrdersBatch (
    @orders as PurchaseOrderTableType READONLY,
    @details as PurchaseOrderDetailTableType READONLY )
    AS
    SET NOCOUNT ON;

    -- Table that connects the order identifiers in the @orders
    -- table with the actual order identifiers in the PurchaseOrder table
    DECLARE @IdentityLink AS TABLE ( 
    SubmittedKey int, 
    ActualKey int, 
    RowNumber int identity(1,1)
    );

          -- Add new orders to the PurchaseOrder table, storing the actual
    -- order identifiers in the @IdentityLink table   
    INSERT INTO PurchaseOrder ([OrderDate], [CustomerID], [Status])
    OUTPUT inserted.OrderID INTO @IdentityLink (ActualKey)
    SELECT [OrderDate], [CustomerID], [Status] FROM @orders ORDER BY OrderID;

    -- Match the passed-in order identifiers with the actual identifiers
    -- and complete the @IdentityLink table for use with inserting the details
    WITH OrderedRows As (
    SELECT OrderID, ROW_NUMBER () OVER (ORDER BY OrderID) As RowNumber 
    FROM @orders
    )
    UPDATE @IdentityLink SET SubmittedKey = M.OrderID
    FROM @IdentityLink L JOIN OrderedRows M ON L.RowNumber = M.RowNumber;

    -- Insert the order details into the PurchaseOrderDetail table, 
          -- using the actual order identifiers of the master table, PurchaseOrder
    INSERT INTO PurchaseOrderDetail (
    [OrderID],
    [ProductID],
    [UnitPrice],
    [OrderQty] )
    SELECT L.ActualKey, D.ProductID, D.UnitPrice, D.OrderQty
    FROM @details D
    JOIN @IdentityLink L ON L.SubmittedKey = D.OrderID;
    GO

<span data-ttu-id="cbba4-458">Nesse exemplo, a tabela @IdentityLink definida localmente armazena os valores reais de OrderID das linhas recentemente inseridas.</span><span class="sxs-lookup"><span data-stu-id="cbba4-458">In this example, the locally defined @IdentityLink table stores the actual OrderID values from the newly inserted rows.</span></span> <span data-ttu-id="cbba4-459">Esses identificadores de pedido são diferentes dos valores temporários de OrderID nos parâmetros com valor de tabela @orders e @details.</span><span class="sxs-lookup"><span data-stu-id="cbba4-459">These order identifiers are different from the temporary OrderID values in the @orders and @details table-valued parameters.</span></span> <span data-ttu-id="cbba4-460">Por esse motivo, a tabela @IdentityLink conecta os valores de OrderID do parâmetro @orders com os valores reais de OrderID para as novas linhas na tabela PurchaseOrder.</span><span class="sxs-lookup"><span data-stu-id="cbba4-460">For this reason, the @IdentityLink table then connects the OrderID values from the @orders parameter to the real OrderID values for the new rows in the PurchaseOrder table.</span></span> <span data-ttu-id="cbba4-461">Após esta etapa, a tabela @IdentityLink pode facilitar a inserção dos detalhes do pedido com o OrderID, o que atende à restrição de chave estrangeira.</span><span class="sxs-lookup"><span data-stu-id="cbba4-461">After this step, the @IdentityLink table can facilitate inserting the order details with the actual OrderID that satisfies the foreign key constraint.</span></span>

<span data-ttu-id="cbba4-462">Esse procedimento armazenado pode ser usado do código ou de outras chamadas Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="cbba4-462">This stored procedure can be used from code or from other Transact-SQL calls.</span></span> <span data-ttu-id="cbba4-463">Consulte a seção de parâmetros com valor de tabela deste documento para obter um exemplo de código.</span><span class="sxs-lookup"><span data-stu-id="cbba4-463">See the table-valued parameters section of this paper for a code example.</span></span> <span data-ttu-id="cbba4-464">O Transact-SQL a seguir mostra como chamar o sp_InsertOrdersBatch.</span><span class="sxs-lookup"><span data-stu-id="cbba4-464">The following Transact-SQL shows how to call the sp_InsertOrdersBatch.</span></span>

    declare @orders as PurchaseOrderTableType
    declare @details as PurchaseOrderDetailTableType

    INSERT @orders 
    ([OrderID], [OrderDate], [CustomerID], [Status])
    VALUES(1, '1/1/2013', 1125, 'Complete'),
    (2, '1/13/2013', 348, 'Processing'),
    (3, '1/12/2013', 2504, 'Shipped')

    INSERT @details
    ([OrderID], [ProductID], [UnitPrice], [OrderQty])
    VALUES(1, 10, $11.50, 1),
    (1, 12, $1.58, 1),
    (2, 23, $2.57, 2),
    (3, 4, $10.00, 1)

    exec sp_InsertOrdersBatch @orders, @details

<span data-ttu-id="cbba4-465">Essa solução permite que cada lote use um conjunto de valores de OrderID que começam com 1.</span><span class="sxs-lookup"><span data-stu-id="cbba4-465">This solution allows each batch to use a set of OrderID values that begin at 1.</span></span> <span data-ttu-id="cbba4-466">Os valores temporários de OrderID descrevem as relações no lote, mas os valores reais de OrderID são determinados no momento da operação de inserção.</span><span class="sxs-lookup"><span data-stu-id="cbba4-466">These temporary OrderID values describe the relationships in the batch, but the actual OrderID values are determined at the time of the insert operation.</span></span> <span data-ttu-id="cbba4-467">Você pode executar as mesmas instruções do exemplo anterior repetidamente e gerar pedidos exclusivos no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="cbba4-467">You can run the same statements in the previous example repeatedly and generate unique orders in the database.</span></span> <span data-ttu-id="cbba4-468">Por esse motivo, considere a adição de mais código ou lógica de banco de dados que impeça os pedidos duplicados ao usar esta técnica de envio em lote.</span><span class="sxs-lookup"><span data-stu-id="cbba4-468">For this reason, consider adding more code or database logic that prevents duplicate orders when using this batching technique.</span></span>

<span data-ttu-id="cbba4-469">Este exemplo demonstra que até mesmo as operações de banco de dados mais complexas, como operações de mestre-detalhes, podem ser enviadas em lote usando parâmetros com valor de tabela.</span><span class="sxs-lookup"><span data-stu-id="cbba4-469">This example demonstrates that even more complex database operations, such as master-detail operations, can be batched using table-valued parameters.</span></span>

### <a name="upsert"></a><span data-ttu-id="cbba4-470">UPSERT</span><span class="sxs-lookup"><span data-stu-id="cbba4-470">UPSERT</span></span>
<span data-ttu-id="cbba4-471">Outro cenário de envio em lote envolve a atualização simultânea de linhas existentes e a inserção de novas linhas.</span><span class="sxs-lookup"><span data-stu-id="cbba4-471">Another batching scenario involves simultaneously updating existing rows and inserting new rows.</span></span> <span data-ttu-id="cbba4-472">Essa operação é chamada às vezes de operação "UPSERT" (atualização + inserção).</span><span class="sxs-lookup"><span data-stu-id="cbba4-472">This operation is sometimes referred to as an “UPSERT” (update + insert) operation.</span></span> <span data-ttu-id="cbba4-473">Em vez de fazer chamadas separadas para INSERT e UPDATE, a instrução MERGE é mais adequada para essa tarefa.</span><span class="sxs-lookup"><span data-stu-id="cbba4-473">Rather than making separate calls to INSERT and UPDATE, the MERGE statement is best suited to this task.</span></span> <span data-ttu-id="cbba4-474">A instrução MERGE pode executar as duas operações, inserção e atualização, em uma única chamada.</span><span class="sxs-lookup"><span data-stu-id="cbba4-474">The MERGE statement can perform both insert and update operations in a single call.</span></span>

<span data-ttu-id="cbba4-475">Parâmetros com valor de tabela podem ser usados com a instrução MERGE para executar atualizações e inserções.</span><span class="sxs-lookup"><span data-stu-id="cbba4-475">Table-valued parameters can be used with the MERGE statement to perform updates and inserts.</span></span> <span data-ttu-id="cbba4-476">Por exemplo, considere uma tabela simplificada de funcionários que contém as seguintes colunas: EmployeeID, FirstName, LastName, SocialSecurityNumber:</span><span class="sxs-lookup"><span data-stu-id="cbba4-476">For example, consider a simplified Employee table that contains the following columns: EmployeeID, FirstName, LastName, SocialSecurityNumber:</span></span>

    CREATE TABLE [dbo].[Employee](
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [SocialSecurityNumber] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_Employee] PRIMARY KEY CLUSTERED 
    ([EmployeeID] ASC ))

<span data-ttu-id="cbba4-477">Neste exemplo, você pode usar o fato de que o SocialSecurityNumber é exclusivo para a execução de uma instrução MERGE de vários funcionários.</span><span class="sxs-lookup"><span data-stu-id="cbba4-477">In this example, you can use the fact that the SocialSecurityNumber is unique to perform a MERGE of multiple employees.</span></span> <span data-ttu-id="cbba4-478">Primeiro, crie o tipo de tabela definido pelo usuário:</span><span class="sxs-lookup"><span data-stu-id="cbba4-478">First, create the user-defined table type:</span></span>

    CREATE TYPE EmployeeTableType AS TABLE 
    ( Employee_ID INT,
      FirstName NVARCHAR(50),
      LastName NVARCHAR(50),
      SocialSecurityNumber NVARCHAR(50) );
    GO

<span data-ttu-id="cbba4-479">Em seguida, crie um procedimento armazenado ou escreva um código que use a instrução MERGE para executar a atualização e a inserção.</span><span class="sxs-lookup"><span data-stu-id="cbba4-479">Next, create a stored procedure or write code that uses the MERGE statement to perform the update and insert.</span></span> <span data-ttu-id="cbba4-480">O exemplo a seguir usa a instrução MERGE em um parâmetro com valor de tabela, @employees, do tipo EmployeeTableType.</span><span class="sxs-lookup"><span data-stu-id="cbba4-480">The following example uses the MERGE statement on a table-valued parameter, @employees, of type EmployeeTableType.</span></span> <span data-ttu-id="cbba4-481">O conteúdo da tabela @employees não é mostrado aqui.</span><span class="sxs-lookup"><span data-stu-id="cbba4-481">The contents of the @employees table are not shown here.</span></span>

    MERGE Employee AS target
    USING (SELECT [FirstName], [LastName], [SocialSecurityNumber] FROM @employees) 
    AS source ([FirstName], [LastName], [SocialSecurityNumber])
    ON (target.[SocialSecurityNumber] = source.[SocialSecurityNumber])
    WHEN MATCHED THEN 
    UPDATE SET
    target.FirstName = source.FirstName, 
    target.LastName = source.LastName
    WHEN NOT MATCHED THEN
       INSERT ([FirstName], [LastName], [SocialSecurityNumber])
       VALUES (source.[FirstName], source.[LastName], source.[SocialSecurityNumber]);

<span data-ttu-id="cbba4-482">Para saber mais, consulte a documentação e exemplos da instrução MERGE.</span><span class="sxs-lookup"><span data-stu-id="cbba4-482">For more information, see the documentation and examples for the MERGE statement.</span></span> <span data-ttu-id="cbba4-483">Embora o mesmo trabalho possa ser executado em uma chamada de procedimento armazenado com várias etapas, com operações INSERT e UPDATE separadas, a instrução MERGE é mais eficiente.</span><span class="sxs-lookup"><span data-stu-id="cbba4-483">Although the same work could be performed in a multiple-step stored procedure call with separate INSERT and UPDATE operations, the MERGE statement is more efficient.</span></span> <span data-ttu-id="cbba4-484">O código do banco de dados também pode construir chamadas Transact-SQL que usam a instrução MERGE diretamente sem exigir duas chamadas de banco de dados para INSERT e UPDATE.</span><span class="sxs-lookup"><span data-stu-id="cbba4-484">Database code can also construct Transact-SQL calls that use the MERGE statement directly without requiring two database calls for INSERT and UPDATE.</span></span>

## <a name="recommendation-summary"></a><span data-ttu-id="cbba4-485">Resumo de recomendações</span><span class="sxs-lookup"><span data-stu-id="cbba4-485">Recommendation summary</span></span>
<span data-ttu-id="cbba4-486">A lista a seguir fornece um resumo das recomendações de envio em lote discutidas neste tópico:</span><span class="sxs-lookup"><span data-stu-id="cbba4-486">The following list provides a summary of the batching recommendations discussed in this topic:</span></span>

* <span data-ttu-id="cbba4-487">Use o armazenamento em buffer e o envio em lote para aumentar o desempenho e a escalabilidade de aplicativos do Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="cbba4-487">Use buffering and batching to increase the performance and scalability of SQL Database applications.</span></span>
* <span data-ttu-id="cbba4-488">Entenda as compensações entre o envio em lote/armazenamento em buffer e resiliência.</span><span class="sxs-lookup"><span data-stu-id="cbba4-488">Understand the tradeoffs between batching/buffering and resiliency.</span></span> <span data-ttu-id="cbba4-489">Durante uma falha de função, o risco de perder um lote não processado de dados críticos para os negócios pode superar o benefício do desempenho do envio em lote.</span><span class="sxs-lookup"><span data-stu-id="cbba4-489">During a role failure, the risk of losing an unprocessed batch of business-critical data might outweigh the performance benefit of batching.</span></span>
* <span data-ttu-id="cbba4-490">Tente manter todas as chamadas para o banco de dados em um único datacenter para reduzir a latência.</span><span class="sxs-lookup"><span data-stu-id="cbba4-490">Attempt to keep all calls to the database within a single datacenter to reduce latency.</span></span>
* <span data-ttu-id="cbba4-491">Se você escolher uma única técnica de envio em lote, os parâmetros com valor de tabela oferecem o melhor desempenho e flexibilidade.</span><span class="sxs-lookup"><span data-stu-id="cbba4-491">If you choose a single batching technique, table-valued parameters offer the best performance and flexibility.</span></span>
* <span data-ttu-id="cbba4-492">Para obter o desempenho mais rápido de inserção, siga estas diretrizes gerais, mas teste seu cenário:</span><span class="sxs-lookup"><span data-stu-id="cbba4-492">For the fastest insert performance, follow these general guidelines but test your scenario:</span></span>
  * <span data-ttu-id="cbba4-493">Para menos de 100 linhas, use um único comando INSERT com parâmetros.</span><span class="sxs-lookup"><span data-stu-id="cbba4-493">For < 100 rows, use a single parameterized INSERT command.</span></span>
  * <span data-ttu-id="cbba4-494">Para menos de 1000 linhas, use parâmetros com valor de tabela.</span><span class="sxs-lookup"><span data-stu-id="cbba4-494">For < 1000 rows, use table-valued parameters.</span></span>
  * <span data-ttu-id="cbba4-495">Para 1000 linhas ou mais, use SqlBulkCopy.</span><span class="sxs-lookup"><span data-stu-id="cbba4-495">For >= 1000 rows, use SqlBulkCopy.</span></span>
* <span data-ttu-id="cbba4-496">Para operações de atualização e exclusão, use parâmetros com valor de tabela com a lógica de procedimento armazenado que determina a operação correta em cada linha no parâmetro de tabela.</span><span class="sxs-lookup"><span data-stu-id="cbba4-496">For update and delete operations, use table-valued parameters with stored procedure logic that determines the correct operation on each row in the table parameter.</span></span>
* <span data-ttu-id="cbba4-497">Diretrizes para o tamanho do lote:</span><span class="sxs-lookup"><span data-stu-id="cbba4-497">Batch size guidelines:</span></span>
  * <span data-ttu-id="cbba4-498">Use os maiores tamanhos de lote adequados aos seus requisitos de aplicativo e de negócios.</span><span class="sxs-lookup"><span data-stu-id="cbba4-498">Use the largest batch sizes that make sense for your application and business requirements.</span></span>
  * <span data-ttu-id="cbba4-499">Equilibre o ganho de desempenho de lotes grandes com os riscos de falhas catastróficas ou temporárias.</span><span class="sxs-lookup"><span data-stu-id="cbba4-499">Balance the performance gain of large batches with the risks of temporary or catastrophic failures.</span></span> <span data-ttu-id="cbba4-500">Qual é a consequência de repetições ou perda de dados no lote?</span><span class="sxs-lookup"><span data-stu-id="cbba4-500">What is the consequence of retries or loss of the data in the batch?</span></span> 
  * <span data-ttu-id="cbba4-501">Teste o maior lote para verificar se o Banco de Dados SQL não irá rejeitá-lo.</span><span class="sxs-lookup"><span data-stu-id="cbba4-501">Test the largest batch size to verify that SQL Database does not reject it.</span></span>
  * <span data-ttu-id="cbba4-502">Crie definições de configuração que controlam o envio em lote, como o tamanho do lote ou o período de armazenamento em buffer.</span><span class="sxs-lookup"><span data-stu-id="cbba4-502">Create configuration settings that control batching, such as the batch size or the buffering time window.</span></span> <span data-ttu-id="cbba4-503">Essas configurações fornecem flexibilidade.</span><span class="sxs-lookup"><span data-stu-id="cbba4-503">These settings provide flexibility.</span></span> <span data-ttu-id="cbba4-504">Você pode alterar o comportamento do lote em produção sem reimplantar o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="cbba4-504">You can change the batching behavior in production without redeploying the cloud service.</span></span>
* <span data-ttu-id="cbba4-505">Evite a execução paralela de lotes que operam em uma única tabela em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="cbba4-505">Avoid parallel execution of batches that operate on a single table in one database.</span></span> <span data-ttu-id="cbba4-506">Se você optar por dividir um único lote entre vários threads de trabalho, execute testes para determinar o número ideal de threads.</span><span class="sxs-lookup"><span data-stu-id="cbba4-506">If you do choose to divide a single batch across multiple worker threads, run tests to determine the ideal number of threads.</span></span> <span data-ttu-id="cbba4-507">Após um limite não especificado, uma quantidade maior de threads diminuirá o desempenho em vez de aumentá-lo.</span><span class="sxs-lookup"><span data-stu-id="cbba4-507">After an unspecified threshold, more threads will decrease performance rather than increase it.</span></span>
* <span data-ttu-id="cbba4-508">Considere o armazenamento em buffer de acordo com o tamanho e o tempo como uma maneira de implementar o envio em lote para mais cenários.</span><span class="sxs-lookup"><span data-stu-id="cbba4-508">Consider buffering on size and time as a way of implementing batching for more scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cbba4-509">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cbba4-509">Next steps</span></span>
<span data-ttu-id="cbba4-510">Este artigo se concentrou em como o design do banco de dados e as técnicas de codificação relacionadas ao envio em lote podem melhorar o desempenho e a escalabilidade do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cbba4-510">This article focused on how database design and coding techniques related to batching can improve your application performance and scalability.</span></span> <span data-ttu-id="cbba4-511">Mas isso é apenas um fator em sua estratégia geral.</span><span class="sxs-lookup"><span data-stu-id="cbba4-511">But this is just one factor in your overall strategy.</span></span> <span data-ttu-id="cbba4-512">Para conhecer outras maneiras de melhorar o desempenho e a escalabilidade, consulte [Diretrizes de desempenho do Banco de Dados SQL do Azure para bancos de dados individuais](sql-database-performance-guidance.md) e [Considerações de preço e desempenho para um pool elástico](sql-database-elastic-pool-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="cbba4-512">For more ways to improve performance and scalability, see [Azure SQL Database performance guidance for single databases](sql-database-performance-guidance.md) and [Price and performance considerations for an elastic pool](sql-database-elastic-pool-guidance.md).</span></span>

