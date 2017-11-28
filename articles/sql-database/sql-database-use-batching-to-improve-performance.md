---
title: toouse aaaHow envio em lote tooimprove desempenho de aplicativos de banco de dados SQL
description: "tópico Hello fornece evidência que envio em lote do banco de dados operações muito imroves Olá velocidade e a escalabilidade de seus aplicativos de banco de dados SQL. Embora essas técnicas de envio em lote funcionam para qualquer banco de dados do SQL Server, o foco Olá artigo Olá é no Azure."
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
ms.openlocfilehash: 124b203ee69c595f0813852ff09ef9ec6841233a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-batching-tooimprove-sql-database-application-performance"></a><span data-ttu-id="f86a0-104">Como toouse envio em lote tooimprove desempenho de aplicativos de banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="f86a0-104">How toouse batching tooimprove SQL Database application performance</span></span>
<span data-ttu-id="f86a0-105">Processamento em lotes de operações tooAzure banco de dados SQL significativamente melhora o desempenho de saudação e escalabilidade de seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="f86a0-105">Batching operations tooAzure SQL Database significantly improves hello performance and scalability of your applications.</span></span> <span data-ttu-id="f86a0-106">Benefícios de saudação do toounderstand de ordem, a primeira parte Olá deste artigo abrange alguns resultados do teste de exemplo que comparam solicitações em lote e não sequenciais tooa banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="f86a0-106">In order toounderstand hello benefits, hello first part of this article covers some sample test results that compare sequential and batched requests tooa SQL Database.</span></span> <span data-ttu-id="f86a0-107">Olá restante do artigo Olá mostra técnicas hello, cenários e considerações toohelp toouse envio em lote com êxito em seus aplicativos do Azure.</span><span class="sxs-lookup"><span data-stu-id="f86a0-107">hello remainder of hello article shows hello techniques, scenarios, and considerations toohelp you toouse batching successfully in your Azure applications.</span></span>

## <a name="why-is-batching-important-for-sql-database"></a><span data-ttu-id="f86a0-108">Por que o envio em lote é importante para o Banco de Dados SQL?</span><span class="sxs-lookup"><span data-stu-id="f86a0-108">Why is batching important for SQL Database?</span></span>
<span data-ttu-id="f86a0-109">O serviço remoto tooa chamadas de envio em lote é uma estratégia conhecida para aumentar o desempenho e escalabilidade.</span><span class="sxs-lookup"><span data-stu-id="f86a0-109">Batching calls tooa remote service is a well-known strategy for increasing performance and scalability.</span></span> <span data-ttu-id="f86a0-110">Há corrigidos processar custos tooany interações com um serviço remoto, como a transferência de rede, serialização e desserialização.</span><span class="sxs-lookup"><span data-stu-id="f86a0-110">There are fixed processing costs tooany interactions with a remote service, such as serialization, network transfer, and deserialization.</span></span> <span data-ttu-id="f86a0-111">O empacotamento de muitas transações separadas em um único lote minimiza esses custos.</span><span class="sxs-lookup"><span data-stu-id="f86a0-111">Packaging many separate transactions into a single batch minimizes these costs.</span></span>

<span data-ttu-id="f86a0-112">Neste documento, queremos tooexamine vários cenários e estratégias de envio em lote do banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="f86a0-112">In this paper, we want tooexamine various SQL Database batching strategies and scenarios.</span></span> <span data-ttu-id="f86a0-113">Embora essas estratégias também são importantes para aplicativos locais que usam o SQL Server, há vários motivos para realçar o uso de saudação do envio em lote para o banco de dados SQL:</span><span class="sxs-lookup"><span data-stu-id="f86a0-113">Although these strategies are also important for on-premises applications that use SQL Server, there are several reasons for highlighting hello use of batching for SQL Database:</span></span>

* <span data-ttu-id="f86a0-114">Há potencialmente maior latência de rede ao acessar o banco de dados SQL, especialmente se você estiver acessando o banco de dados SQL de saudação externa mesmo datacenter do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f86a0-114">There is potentially greater network latency in accessing SQL Database, especially if you are accessing SQL Database from outside hello same Microsoft Azure datacenter.</span></span>
* <span data-ttu-id="f86a0-115">características de multilocatário Olá significa de banco de dados SQL que Olá eficiência dos dados Olá acessar camada correlaciona toohello escalabilidade total do banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="f86a0-115">hello multitenant characteristics of SQL Database means that hello efficiency of hello data access layer correlates toohello overall scalability of hello database.</span></span> <span data-ttu-id="f86a0-116">Banco de dados SQL deve impedir que qualquer locatário/usuário monopolize detrimento de toohello de recursos de banco de dados de outros locatários.</span><span class="sxs-lookup"><span data-stu-id="f86a0-116">SQL Database must prevent any single tenant/user from monopolizing database resources toohello detriment of other tenants.</span></span> <span data-ttu-id="f86a0-117">Na resposta toousage além das cotas predefinidas, o banco de dados SQL pode reduzir a taxa de transferência ou responder com exceções de limitação.</span><span class="sxs-lookup"><span data-stu-id="f86a0-117">In response toousage in excess of predefined quotas, SQL Database can reduce throughput or respond with throttling exceptions.</span></span> <span data-ttu-id="f86a0-118">As eficiências, como envio em lote, permitem que você toodo mais trabalho no banco de dados SQL antes de alcançar esses limites.</span><span class="sxs-lookup"><span data-stu-id="f86a0-118">Efficiencies, such as batching, enable you toodo more work on SQL Database before reaching these limits.</span></span> 
* <span data-ttu-id="f86a0-119">O envio em lote também é eficaz para arquiteturas que usam vários bancos de dados (fragmentação).</span><span class="sxs-lookup"><span data-stu-id="f86a0-119">Batching is also effective for architectures that use multiple databases (sharding).</span></span> <span data-ttu-id="f86a0-120">eficiência de saudação de sua interação com cada unidade de banco de dados ainda é um fator essencial em sua escalabilidade total.</span><span class="sxs-lookup"><span data-stu-id="f86a0-120">hello efficiency of your interaction with each database unit is still a key factor in your overall scalability.</span></span> 

<span data-ttu-id="f86a0-121">Um dos benefícios de saudação do uso de banco de dados SQL é que você não tem servidores de saudação toomanage esse banco de dados de saudação do host.</span><span class="sxs-lookup"><span data-stu-id="f86a0-121">One of hello benefits of using SQL Database is that you don’t have toomanage hello servers that host hello database.</span></span> <span data-ttu-id="f86a0-122">No entanto, essa infraestrutura gerenciada também significa que você tenha toothink diferente sobre otimizações de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f86a0-122">However, this managed infrastructure also means that you have toothink differently about database optimizations.</span></span> <span data-ttu-id="f86a0-123">Não é possível examinar infraestrutura de hardware ou de rede de banco de dados de saudação do tooimprove.</span><span class="sxs-lookup"><span data-stu-id="f86a0-123">You can no longer look tooimprove hello database hardware or network infrastructure.</span></span> <span data-ttu-id="f86a0-124">O Microsoft Azure controla esses ambientes.</span><span class="sxs-lookup"><span data-stu-id="f86a0-124">Microsoft Azure controls those environments.</span></span> <span data-ttu-id="f86a0-125">Olá principal área que você pode controlar é como seu aplicativo interage com o banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="f86a0-125">hello main area that you can control is how your application interacts with SQL Database.</span></span> <span data-ttu-id="f86a0-126">O envio em lote é uma dessas otimizações.</span><span class="sxs-lookup"><span data-stu-id="f86a0-126">Batching is one of these optimizations.</span></span> 

<span data-ttu-id="f86a0-127">a primeira parte saudação do papel Olá examina várias técnicas de envio em lote para aplicativos .NET que usam o banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="f86a0-127">hello first part of hello paper examines various batching techniques for .NET applications that use SQL Database.</span></span> <span data-ttu-id="f86a0-128">Olá duas últimas seções abordam diretrizes e cenários de envio em lote.</span><span class="sxs-lookup"><span data-stu-id="f86a0-128">hello last two sections cover batching guidelines and scenarios.</span></span>

## <a name="batching-strategies"></a><span data-ttu-id="f86a0-129">Estratégias de envio em lote</span><span class="sxs-lookup"><span data-stu-id="f86a0-129">Batching strategies</span></span>
### <a name="note-about-timing-results-in-this-topic"></a><span data-ttu-id="f86a0-130">Observação sobre os resultados de tempo neste tópico</span><span class="sxs-lookup"><span data-stu-id="f86a0-130">Note about timing results in this topic</span></span>
> [!NOTE]
> <span data-ttu-id="f86a0-131">Resultados não são parâmetros de comparação, mas devem tooshow **desempenho relativo**.</span><span class="sxs-lookup"><span data-stu-id="f86a0-131">Results are not benchmarks but are meant tooshow **relative performance**.</span></span> <span data-ttu-id="f86a0-132">Os intervalos se baseiam em uma média de pelo menos 10 execuções de teste.</span><span class="sxs-lookup"><span data-stu-id="f86a0-132">Timings are based on an average of at least 10 test runs.</span></span> <span data-ttu-id="f86a0-133">As operações são inserções em uma tabela vazia.</span><span class="sxs-lookup"><span data-stu-id="f86a0-133">Operations are inserts into an empty table.</span></span> <span data-ttu-id="f86a0-134">Esses testes foram medidos pre-V12 e não necessariamente correspondem toothroughput que podem ocorrer no banco de dados V12 usando Olá novo [camadas de serviço](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="f86a0-134">These tests were measured pre-V12, and they do not necessarily correspond toothroughput that you might experience in a V12 database using hello new [service tiers](sql-database-service-tiers.md).</span></span> <span data-ttu-id="f86a0-135">benefício relativo Olá Olá técnica de envio em lote deve ser semelhante.</span><span class="sxs-lookup"><span data-stu-id="f86a0-135">hello relative benefit of hello batching technique should be similar.</span></span>
> 
> 

### <a name="transactions"></a><span data-ttu-id="f86a0-136">Transações</span><span class="sxs-lookup"><span data-stu-id="f86a0-136">Transactions</span></span>
<span data-ttu-id="f86a0-137">Parece estranho toobegin uma revisão do envio em lote discutindo transações.</span><span class="sxs-lookup"><span data-stu-id="f86a0-137">It seems strange toobegin a review of batching by discussing transactions.</span></span> <span data-ttu-id="f86a0-138">Mas o uso de saudação de transações do lado do cliente tem um efeito sutil envio em lote do lado do servidor que melhora o desempenho.</span><span class="sxs-lookup"><span data-stu-id="f86a0-138">But hello use of client-side transactions has a subtle server-side batching effect that improves performance.</span></span> <span data-ttu-id="f86a0-139">E transações podem ser adicionadas com apenas algumas linhas de código, para que eles fornecem um desempenho de tooimprove de maneira rápida de operações sequenciais.</span><span class="sxs-lookup"><span data-stu-id="f86a0-139">And transactions can be added with only a few lines of code, so they provide a fast way tooimprove performance of sequential operations.</span></span>

<span data-ttu-id="f86a0-140">Considere Olá código em c# que contém uma sequência de inserção a seguir e operações de atualização em uma tabela simples.</span><span class="sxs-lookup"><span data-stu-id="f86a0-140">Consider hello following C# code that contains a sequence of insert and update operations on a simple table.</span></span>

    List<string> dbOperations = new List<string>();
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 1");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 2");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 3");
    dbOperations.Add("insert MyTable values ('new value',1)");
    dbOperations.Add("insert MyTable values ('new value',2)");
    dbOperations.Add("insert MyTable values ('new value',3)");

<span data-ttu-id="f86a0-141">Olá código ADO.NET a seguir sequencialmente executa essas operações.</span><span class="sxs-lookup"><span data-stu-id="f86a0-141">hello following ADO.NET code sequentially performs these operations.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();

        foreach(string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn);
            cmd.ExecuteNonQuery();                   
        }
    }

<span data-ttu-id="f86a0-142">Olá toooptimize de maneira melhor esse código é tooimplement alguma forma de envio em lote do lado do cliente dessas chamadas.</span><span class="sxs-lookup"><span data-stu-id="f86a0-142">hello best way toooptimize this code is tooimplement some form of client-side batching of these calls.</span></span> <span data-ttu-id="f86a0-143">Mas há um modo simples tooincrease Olá de desempenho do código simplesmente encapsulando sequência Olá de chamadas em uma transação.</span><span class="sxs-lookup"><span data-stu-id="f86a0-143">But there is a simple way tooincrease hello performance of this code by simply wrapping hello sequence of calls in a transaction.</span></span> <span data-ttu-id="f86a0-144">Eis Olá mesmo código que usa uma transação.</span><span class="sxs-lookup"><span data-stu-id="f86a0-144">Here is hello same code that uses a transaction.</span></span>

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

<span data-ttu-id="f86a0-145">Na verdade, as transações estão sendo usadas nos dois exemplos.</span><span class="sxs-lookup"><span data-stu-id="f86a0-145">Transactions are actually being used in both of these examples.</span></span> <span data-ttu-id="f86a0-146">No primeiro exemplo de hello, cada chamada individual é uma transação implícita.</span><span class="sxs-lookup"><span data-stu-id="f86a0-146">In hello first example, each individual call is an implicit transaction.</span></span> <span data-ttu-id="f86a0-147">No segundo exemplo de hello, uma transação explícita encapsula todas as chamadas de saudação.</span><span class="sxs-lookup"><span data-stu-id="f86a0-147">In hello second example, an explicit transaction wraps all of hello calls.</span></span> <span data-ttu-id="f86a0-148">Por documentação Olá Olá [log de transações write-ahead](https://msdn.microsoft.com/library/ms186259.aspx), registros de log são liberados toohello disco quando Olá transação confirmada.</span><span class="sxs-lookup"><span data-stu-id="f86a0-148">Per hello documentation for hello [write-ahead transaction log](https://msdn.microsoft.com/library/ms186259.aspx), log records are flushed toohello disk when hello transaction commits.</span></span> <span data-ttu-id="f86a0-149">Portanto, incluindo mais chamadas em uma transação, hello grava toohello o log de transações pode atrasar até que Olá a transação é confirmada.</span><span class="sxs-lookup"><span data-stu-id="f86a0-149">So by including more calls in a transaction, hello write toohello transaction log can delay until hello transaction is committed.</span></span> <span data-ttu-id="f86a0-150">Na verdade, você habilitará o envio em lote para o log de transações do servidor do toohello Olá gravações.</span><span class="sxs-lookup"><span data-stu-id="f86a0-150">In effect, you are enabling batching for hello writes toohello server’s transaction log.</span></span>

<span data-ttu-id="f86a0-151">Olá, a tabela a seguir mostra alguns resultados de teste ad-hoc.</span><span class="sxs-lookup"><span data-stu-id="f86a0-151">hello following table shows some ad-hoc testing results.</span></span> <span data-ttu-id="f86a0-152">testes de saudação executada Olá que mesmo sequencial insere com e sem transações.</span><span class="sxs-lookup"><span data-stu-id="f86a0-152">hello tests performed hello same sequential inserts with and without transactions.</span></span> <span data-ttu-id="f86a0-153">Para obter mais perspectiva, primeiro o conjunto de testes Olá foi executado remotamente de um banco de dados de toohello laptop no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f86a0-153">For more perspective, hello first set of tests ran remotely from a laptop toohello database in Microsoft Azure.</span></span> <span data-ttu-id="f86a0-154">Hello segundo conjunto de testes foi executado de um serviço de nuvem e o banco de dados que residiam no hello mesmo datacenter do Microsoft Azure (Oeste dos Estados Unidos).</span><span class="sxs-lookup"><span data-stu-id="f86a0-154">hello second set of tests ran from a cloud service and database that both resided within hello same Microsoft Azure datacenter (West US).</span></span> <span data-ttu-id="f86a0-155">Olá tabela a seguir mostra Olá duração em milissegundos de inserções sequenciais com e sem transações.</span><span class="sxs-lookup"><span data-stu-id="f86a0-155">hello following table shows hello duration in milliseconds of sequential inserts with and without transactions.</span></span>

<span data-ttu-id="f86a0-156">**TooAzure local**:</span><span class="sxs-lookup"><span data-stu-id="f86a0-156">**On-Premises tooAzure**:</span></span>

| <span data-ttu-id="f86a0-157">Operações</span><span class="sxs-lookup"><span data-stu-id="f86a0-157">Operations</span></span> | <span data-ttu-id="f86a0-158">Sem transação (ms)</span><span class="sxs-lookup"><span data-stu-id="f86a0-158">No Transaction (ms)</span></span> | <span data-ttu-id="f86a0-159">Com transação (ms)</span><span class="sxs-lookup"><span data-stu-id="f86a0-159">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f86a0-160">1</span><span class="sxs-lookup"><span data-stu-id="f86a0-160">1</span></span> |<span data-ttu-id="f86a0-161">130</span><span class="sxs-lookup"><span data-stu-id="f86a0-161">130</span></span> |<span data-ttu-id="f86a0-162">402</span><span class="sxs-lookup"><span data-stu-id="f86a0-162">402</span></span> |
| <span data-ttu-id="f86a0-163">10</span><span class="sxs-lookup"><span data-stu-id="f86a0-163">10</span></span> |<span data-ttu-id="f86a0-164">1208</span><span class="sxs-lookup"><span data-stu-id="f86a0-164">1208</span></span> |<span data-ttu-id="f86a0-165">1226</span><span class="sxs-lookup"><span data-stu-id="f86a0-165">1226</span></span> |
| <span data-ttu-id="f86a0-166">100</span><span class="sxs-lookup"><span data-stu-id="f86a0-166">100</span></span> |<span data-ttu-id="f86a0-167">12662</span><span class="sxs-lookup"><span data-stu-id="f86a0-167">12662</span></span> |<span data-ttu-id="f86a0-168">10395</span><span class="sxs-lookup"><span data-stu-id="f86a0-168">10395</span></span> |
| <span data-ttu-id="f86a0-169">1000</span><span class="sxs-lookup"><span data-stu-id="f86a0-169">1000</span></span> |<span data-ttu-id="f86a0-170">128852</span><span class="sxs-lookup"><span data-stu-id="f86a0-170">128852</span></span> |<span data-ttu-id="f86a0-171">102917</span><span class="sxs-lookup"><span data-stu-id="f86a0-171">102917</span></span> |

<span data-ttu-id="f86a0-172">**TooAzure do Azure (mesmo datacenter)**:</span><span class="sxs-lookup"><span data-stu-id="f86a0-172">**Azure tooAzure (same datacenter)**:</span></span>

| <span data-ttu-id="f86a0-173">Operações</span><span class="sxs-lookup"><span data-stu-id="f86a0-173">Operations</span></span> | <span data-ttu-id="f86a0-174">Sem transação (ms)</span><span class="sxs-lookup"><span data-stu-id="f86a0-174">No Transaction (ms)</span></span> | <span data-ttu-id="f86a0-175">Com transação (ms)</span><span class="sxs-lookup"><span data-stu-id="f86a0-175">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f86a0-176">1</span><span class="sxs-lookup"><span data-stu-id="f86a0-176">1</span></span> |<span data-ttu-id="f86a0-177">21</span><span class="sxs-lookup"><span data-stu-id="f86a0-177">21</span></span> |<span data-ttu-id="f86a0-178">26</span><span class="sxs-lookup"><span data-stu-id="f86a0-178">26</span></span> |
| <span data-ttu-id="f86a0-179">10</span><span class="sxs-lookup"><span data-stu-id="f86a0-179">10</span></span> |<span data-ttu-id="f86a0-180">220</span><span class="sxs-lookup"><span data-stu-id="f86a0-180">220</span></span> |<span data-ttu-id="f86a0-181">56</span><span class="sxs-lookup"><span data-stu-id="f86a0-181">56</span></span> |
| <span data-ttu-id="f86a0-182">100</span><span class="sxs-lookup"><span data-stu-id="f86a0-182">100</span></span> |<span data-ttu-id="f86a0-183">2145</span><span class="sxs-lookup"><span data-stu-id="f86a0-183">2145</span></span> |<span data-ttu-id="f86a0-184">341</span><span class="sxs-lookup"><span data-stu-id="f86a0-184">341</span></span> |
| <span data-ttu-id="f86a0-185">1000</span><span class="sxs-lookup"><span data-stu-id="f86a0-185">1000</span></span> |<span data-ttu-id="f86a0-186">21479</span><span class="sxs-lookup"><span data-stu-id="f86a0-186">21479</span></span> |<span data-ttu-id="f86a0-187">2756</span><span class="sxs-lookup"><span data-stu-id="f86a0-187">2756</span></span> |

> [!NOTE]
> <span data-ttu-id="f86a0-188">Os resultados não são parâmetros de comparação.</span><span class="sxs-lookup"><span data-stu-id="f86a0-188">Results are not benchmarks.</span></span> <span data-ttu-id="f86a0-189">Consulte Olá [Observação sobre resultados neste tópico](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="f86a0-189">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="f86a0-190">Com base nos resultados de teste anteriores hello, quebra automática de uma única operação em uma transação, na verdade, reduz o desempenho.</span><span class="sxs-lookup"><span data-stu-id="f86a0-190">Based on hello previous test results, wrapping a single operation in a transaction actually decreases performance.</span></span> <span data-ttu-id="f86a0-191">Mas, conforme você aumenta o número de saudação de operações em uma única transação, a melhoria de desempenho Olá fica mais evidente.</span><span class="sxs-lookup"><span data-stu-id="f86a0-191">But as you increase hello number of operations within a single transaction, hello performance improvement becomes more marked.</span></span> <span data-ttu-id="f86a0-192">diferença de desempenho Olá também é mais perceptível quando todas as operações ocorrem no datacenter do Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f86a0-192">hello performance difference is also more noticeable when all operations occur within hello Microsoft Azure datacenter.</span></span> <span data-ttu-id="f86a0-193">Olá, latência aumentada do uso do banco de dados SQL do data center do Microsoft Azure Olá fora ofusca ganho de desempenho de saudação do uso de transações.</span><span class="sxs-lookup"><span data-stu-id="f86a0-193">hello increased latency of using SQL Database from outside hello Microsoft Azure datacenter overshadows hello performance gain of using transactions.</span></span>

<span data-ttu-id="f86a0-194">Embora o uso de saudação de transações pode aumentar o desempenho, continuar muito[seguindo as práticas recomendadas para transações e conexões](https://msdn.microsoft.com/library/ms187484.aspx).</span><span class="sxs-lookup"><span data-stu-id="f86a0-194">Although hello use of transactions can increase performance, continue too[observe best practices for transactions and connections](https://msdn.microsoft.com/library/ms187484.aspx).</span></span> <span data-ttu-id="f86a0-195">Mantenha a transação de saudação tão curta quanto a conexão de banco de dados de saudação possíveis e de fechamento após a conclusão do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="f86a0-195">Keep hello transaction as short as possible, and close hello database connection after hello work completes.</span></span> <span data-ttu-id="f86a0-196">Olá usando a instrução no exemplo anterior Olá garante que conexão Olá é fechada quando o bloco de código subsequente Olá for concluída.</span><span class="sxs-lookup"><span data-stu-id="f86a0-196">hello using statement in hello previous example assures that hello connection is closed when hello subsequent code block completes.</span></span>

<span data-ttu-id="f86a0-197">Olá anterior demonstra que você pode adicionar um código do ADO.NET do tooany de transação local com duas linhas.</span><span class="sxs-lookup"><span data-stu-id="f86a0-197">hello previous example demonstrates that you can add a local transaction tooany ADO.NET code with two lines.</span></span> <span data-ttu-id="f86a0-198">As transações oferecem uma maneira rápida tooimprove desempenho de saudação do código que faz sequencial inserir, atualizar e excluir operações.</span><span class="sxs-lookup"><span data-stu-id="f86a0-198">Transactions offer a quick way tooimprove hello performance of code that makes sequential insert, update, and delete operations.</span></span> <span data-ttu-id="f86a0-199">No entanto, para um desempenho mais rápido hello, considere alterar Olá código adicional tootake vantagem de lote no lado do cliente, como parâmetros com valor de tabela.</span><span class="sxs-lookup"><span data-stu-id="f86a0-199">However, for hello fastest performance, consider changing hello code further tootake advantage of client-side batching, such as table-valued parameters.</span></span>

<span data-ttu-id="f86a0-200">Para saber mais sobre transações no ADO.NET, consulte [Transações locais no ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).</span><span class="sxs-lookup"><span data-stu-id="f86a0-200">For more information about transactions in ADO.NET, see [Local Transactions in ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).</span></span>

### <a name="table-valued-parameters"></a><span data-ttu-id="f86a0-201">Parâmetros com valor de tabela</span><span class="sxs-lookup"><span data-stu-id="f86a0-201">Table-valued parameters</span></span>
<span data-ttu-id="f86a0-202">Os parâmetros com valor de tabela oferecem suporte a tipos de tabela definidos pelo usuário como parâmetros em instruções Transact-SQL, procedimentos armazenados e funções.</span><span class="sxs-lookup"><span data-stu-id="f86a0-202">Table-valued parameters support user-defined table types as parameters in Transact-SQL statements, stored procedures, and functions.</span></span> <span data-ttu-id="f86a0-203">Essa técnica de envio em lote do lado do cliente permite que você toosend várias linhas de dados no parâmetro com valor de tabela do hello.</span><span class="sxs-lookup"><span data-stu-id="f86a0-203">This client-side batching technique allows you toosend multiple rows of data within hello table-valued parameter.</span></span> <span data-ttu-id="f86a0-204">parâmetros com valor de tabela toouse, primeiro defina um tipo de tabela.</span><span class="sxs-lookup"><span data-stu-id="f86a0-204">toouse table-valued parameters, first define a table type.</span></span> <span data-ttu-id="f86a0-205">Olá instrução Transact-SQL a seguir cria um tipo de tabela denominada **MyTableType**.</span><span class="sxs-lookup"><span data-stu-id="f86a0-205">hello following Transact-SQL statement creates a table type named **MyTableType**.</span></span>

    CREATE TYPE MyTableType AS TABLE 
    ( mytext TEXT,
      num INT );


<span data-ttu-id="f86a0-206">No código, você cria um **DataTable** com hello exato mesmos nomes e tipos de saudação do tipo de tabela.</span><span class="sxs-lookup"><span data-stu-id="f86a0-206">In code, you create a **DataTable** with hello exact same names and types of hello table type.</span></span> <span data-ttu-id="f86a0-207">Passe essa **DataTable** em um parâmetro em uma consulta de texto ou em uma chamada de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="f86a0-207">Pass this **DataTable** in a parameter in a text query or stored procedure call.</span></span> <span data-ttu-id="f86a0-208">Olá, exemplo a seguir mostra essa técnica:</span><span class="sxs-lookup"><span data-stu-id="f86a0-208">hello following example shows this technique:</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        DataTable table = new DataTable();
        // Add columns and rows. hello following is a simple example.
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

<span data-ttu-id="f86a0-209">No exemplo anterior de saudação, Olá **SqlCommand** objeto insere linhas de um parâmetro com valor de tabela,  **@TestTvp** .</span><span class="sxs-lookup"><span data-stu-id="f86a0-209">In hello previous example, hello **SqlCommand** object inserts rows from a table-valued parameter, **@TestTvp**.</span></span> <span data-ttu-id="f86a0-210">Olá criado anteriormente **DataTable** objeto será atribuído o parâmetro hello toothis **SqlCommand.Parameters.Add** método.</span><span class="sxs-lookup"><span data-stu-id="f86a0-210">hello previously created **DataTable** object is assigned toothis parameter with hello **SqlCommand.Parameters.Add** method.</span></span> <span data-ttu-id="f86a0-211">Inserções de saudação envio em lote em uma chamada significativamente aumenta desempenho Olá sobre inserções sequenciais.</span><span class="sxs-lookup"><span data-stu-id="f86a0-211">Batching hello inserts in one call significantly increases hello performance over sequential inserts.</span></span>

<span data-ttu-id="f86a0-212">tooimprove anterior exemplo hello Além disso, use um procedimento armazenado, em vez de um comando baseado em texto.</span><span class="sxs-lookup"><span data-stu-id="f86a0-212">tooimprove hello previous example further, use a stored procedure instead of a text-based command.</span></span> <span data-ttu-id="f86a0-213">Olá comando Transact-SQL a seguir cria um procedimento armazenado que entra Olá **SimpleTestTableType** parâmetro com valor de tabela.</span><span class="sxs-lookup"><span data-stu-id="f86a0-213">hello following Transact-SQL command creates a stored procedure that takes hello **SimpleTestTableType** table-valued parameter.</span></span>

    CREATE PROCEDURE [dbo].[sp_InsertRows] 
    @TestTvp as MyTableType READONLY
    AS
    BEGIN
    INSERT INTO MyTable(mytext, num) 
    SELECT mytext, num FROM @TestTvp
    END
    GO

<span data-ttu-id="f86a0-214">Em seguida, altere Olá **SqlCommand** declaração a seguir do hello anterior código exemplo toohello do objeto.</span><span class="sxs-lookup"><span data-stu-id="f86a0-214">Then change hello **SqlCommand** object declaration in hello previous code example toohello following.</span></span>

    SqlCommand cmd = new SqlCommand("sp_InsertRows", connection);
    cmd.CommandType = CommandType.StoredProcedure;

<span data-ttu-id="f86a0-215">Na maioria dos casos, os parâmetros com valor de tabela têm um desempenho equivalente ou superior às outras técnicas de envio em lote.</span><span class="sxs-lookup"><span data-stu-id="f86a0-215">In most cases, table-valued parameters have equivalent or better performance than other batching techniques.</span></span> <span data-ttu-id="f86a0-216">Normalmente, a preferência fica com os parâmetros com valor de tabela, pois são mais flexíveis do que as outras opções.</span><span class="sxs-lookup"><span data-stu-id="f86a0-216">Table-valued parameters are often preferable, because they are more flexible than other options.</span></span> <span data-ttu-id="f86a0-217">Por exemplo, outras técnicas, como cópia em massa SQL, só permitem a inserção de saudação de novas linhas.</span><span class="sxs-lookup"><span data-stu-id="f86a0-217">For example, other techniques, such as SQL bulk copy, only permit hello insertion of new rows.</span></span> <span data-ttu-id="f86a0-218">Mas com parâmetros com valor de tabela, você pode usar lógica toodetermine de procedimento armazenada de saudação quais linhas são atualizações e quais são inserções.</span><span class="sxs-lookup"><span data-stu-id="f86a0-218">But with table-valued parameters, you can use logic in hello stored procedure toodetermine which rows are updates and which are inserts.</span></span> <span data-ttu-id="f86a0-219">tipo de tabela Olá também pode ser modificado toocontain uma coluna "Operação" que indica se Olá especificada linha deve ser inserida, atualizada ou excluída.</span><span class="sxs-lookup"><span data-stu-id="f86a0-219">hello table type can also be modified toocontain an “Operation” column that indicates whether hello specified row should be inserted, updated, or deleted.</span></span>

<span data-ttu-id="f86a0-220">Olá, a tabela a seguir mostra os resultados do teste ad-hoc para uso de saudação de parâmetros com valor de tabela em milissegundos.</span><span class="sxs-lookup"><span data-stu-id="f86a0-220">hello following table shows ad-hoc test results for hello use of table-valued parameters in milliseconds.</span></span>

| <span data-ttu-id="f86a0-221">Operações</span><span class="sxs-lookup"><span data-stu-id="f86a0-221">Operations</span></span> | <span data-ttu-id="f86a0-222">Local tooAzure (ms)</span><span class="sxs-lookup"><span data-stu-id="f86a0-222">On-Premises tooAzure (ms)</span></span> | <span data-ttu-id="f86a0-223">Mesmo datacenter do Azure (ms)</span><span class="sxs-lookup"><span data-stu-id="f86a0-223">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f86a0-224">1</span><span class="sxs-lookup"><span data-stu-id="f86a0-224">1</span></span> |<span data-ttu-id="f86a0-225">124</span><span class="sxs-lookup"><span data-stu-id="f86a0-225">124</span></span> |<span data-ttu-id="f86a0-226">32</span><span class="sxs-lookup"><span data-stu-id="f86a0-226">32</span></span> |
| <span data-ttu-id="f86a0-227">10</span><span class="sxs-lookup"><span data-stu-id="f86a0-227">10</span></span> |<span data-ttu-id="f86a0-228">131</span><span class="sxs-lookup"><span data-stu-id="f86a0-228">131</span></span> |<span data-ttu-id="f86a0-229">25</span><span class="sxs-lookup"><span data-stu-id="f86a0-229">25</span></span> |
| <span data-ttu-id="f86a0-230">100</span><span class="sxs-lookup"><span data-stu-id="f86a0-230">100</span></span> |<span data-ttu-id="f86a0-231">338</span><span class="sxs-lookup"><span data-stu-id="f86a0-231">338</span></span> |<span data-ttu-id="f86a0-232">51</span><span class="sxs-lookup"><span data-stu-id="f86a0-232">51</span></span> |
| <span data-ttu-id="f86a0-233">1000</span><span class="sxs-lookup"><span data-stu-id="f86a0-233">1000</span></span> |<span data-ttu-id="f86a0-234">2615</span><span class="sxs-lookup"><span data-stu-id="f86a0-234">2615</span></span> |<span data-ttu-id="f86a0-235">382</span><span class="sxs-lookup"><span data-stu-id="f86a0-235">382</span></span> |
| <span data-ttu-id="f86a0-236">10000</span><span class="sxs-lookup"><span data-stu-id="f86a0-236">10000</span></span> |<span data-ttu-id="f86a0-237">23830</span><span class="sxs-lookup"><span data-stu-id="f86a0-237">23830</span></span> |<span data-ttu-id="f86a0-238">3586</span><span class="sxs-lookup"><span data-stu-id="f86a0-238">3586</span></span> |

> [!NOTE]
> <span data-ttu-id="f86a0-239">Os resultados não são parâmetros de comparação.</span><span class="sxs-lookup"><span data-stu-id="f86a0-239">Results are not benchmarks.</span></span> <span data-ttu-id="f86a0-240">Consulte Olá [Observação sobre resultados neste tópico](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="f86a0-240">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="f86a0-241">ganho de desempenho de saudação do envio em lote é imediatamente evidente.</span><span class="sxs-lookup"><span data-stu-id="f86a0-241">hello performance gain from batching is immediately apparent.</span></span> <span data-ttu-id="f86a0-242">No teste sequencial anterior de saudação, 1000 operações levaram 129 segundos fora Olá datacenter e 21 segundos dentro do datacenter hello.</span><span class="sxs-lookup"><span data-stu-id="f86a0-242">In hello previous sequential test, 1000 operations took 129 seconds outside hello datacenter and 21 seconds from within hello datacenter.</span></span> <span data-ttu-id="f86a0-243">Mas, com parâmetros com valor de tabela, 1000 operações levam somente 2,6 segundos fora Olá datacenter e 0,4 segundos no datacenter hello.</span><span class="sxs-lookup"><span data-stu-id="f86a0-243">But with table-valued parameters, 1000 operations take only 2.6 seconds outside hello datacenter and 0.4 seconds within hello datacenter.</span></span>

<span data-ttu-id="f86a0-244">Para saber mais sobre parâmetros com valor de tabela, consulte [Parâmetros com valor de tabela](https://msdn.microsoft.com/library/bb510489.aspx).</span><span class="sxs-lookup"><span data-stu-id="f86a0-244">For more information on table-valued parameters, see [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

### <a name="sql-bulk-copy"></a><span data-ttu-id="f86a0-245">Cópia em massa do SQL</span><span class="sxs-lookup"><span data-stu-id="f86a0-245">SQL bulk copy</span></span>
<span data-ttu-id="f86a0-246">Cópia em massa SQL é outra maneira tooinsert grandes quantidades de dados em um banco de dados de destino.</span><span class="sxs-lookup"><span data-stu-id="f86a0-246">SQL bulk copy is another way tooinsert large amounts of data into a target database.</span></span> <span data-ttu-id="f86a0-247">Aplicativos .NET podem usar Olá **SqlBulkCopy** operações de inserção em massa tooperform de classe.</span><span class="sxs-lookup"><span data-stu-id="f86a0-247">.NET applications can use hello **SqlBulkCopy** class tooperform bulk insert operations.</span></span> <span data-ttu-id="f86a0-248">**SqlBulkCopy** é semelhante na ferramenta de linha de comando de função toohello, **Bcp.exe**, ou hello instrução Transact-SQL, **BULK INSERT**.</span><span class="sxs-lookup"><span data-stu-id="f86a0-248">**SqlBulkCopy** is similar in function toohello command-line tool, **Bcp.exe**, or hello Transact-SQL statement, **BULK INSERT**.</span></span> <span data-ttu-id="f86a0-249">Olá exemplo de código a seguir mostra como saudação de cópia toobulk linhas na fonte de saudação **DataTable**, tabela, a tabela de destino toohello no SQL Server, MyTable.</span><span class="sxs-lookup"><span data-stu-id="f86a0-249">hello following code example shows how toobulk copy hello rows in hello source **DataTable**, table, toohello destination table in SQL Server, MyTable.</span></span>

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

<span data-ttu-id="f86a0-250">Há alguns casos nos quais é preferível usar a cópia em massa do que os parâmetros com valor de tabela.</span><span class="sxs-lookup"><span data-stu-id="f86a0-250">There are some cases where bulk copy is preferred over table-valued parameters.</span></span> <span data-ttu-id="f86a0-251">Consulte Olá a tabela de comparação de parâmetros com valor de tabela versus operações BULK INSERT no tópico Olá [parâmetros com valor de tabela](https://msdn.microsoft.com/library/bb510489.aspx).</span><span class="sxs-lookup"><span data-stu-id="f86a0-251">See hello comparison table of Table-Valued parameters versus BULK INSERT operations in hello topic [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

<span data-ttu-id="f86a0-252">Olá, seguintes resultados do teste ad hoc mostram Olá desempenho do envio em lote com **SqlBulkCopy** em milissegundos.</span><span class="sxs-lookup"><span data-stu-id="f86a0-252">hello following ad-hoc test results show hello performance of batching with **SqlBulkCopy** in milliseconds.</span></span>

| <span data-ttu-id="f86a0-253">Operações</span><span class="sxs-lookup"><span data-stu-id="f86a0-253">Operations</span></span> | <span data-ttu-id="f86a0-254">Local tooAzure (ms)</span><span class="sxs-lookup"><span data-stu-id="f86a0-254">On-Premises tooAzure (ms)</span></span> | <span data-ttu-id="f86a0-255">Mesmo datacenter do Azure (ms)</span><span class="sxs-lookup"><span data-stu-id="f86a0-255">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f86a0-256">1</span><span class="sxs-lookup"><span data-stu-id="f86a0-256">1</span></span> |<span data-ttu-id="f86a0-257">433</span><span class="sxs-lookup"><span data-stu-id="f86a0-257">433</span></span> |<span data-ttu-id="f86a0-258">57</span><span class="sxs-lookup"><span data-stu-id="f86a0-258">57</span></span> |
| <span data-ttu-id="f86a0-259">10</span><span class="sxs-lookup"><span data-stu-id="f86a0-259">10</span></span> |<span data-ttu-id="f86a0-260">441</span><span class="sxs-lookup"><span data-stu-id="f86a0-260">441</span></span> |<span data-ttu-id="f86a0-261">32</span><span class="sxs-lookup"><span data-stu-id="f86a0-261">32</span></span> |
| <span data-ttu-id="f86a0-262">100</span><span class="sxs-lookup"><span data-stu-id="f86a0-262">100</span></span> |<span data-ttu-id="f86a0-263">636</span><span class="sxs-lookup"><span data-stu-id="f86a0-263">636</span></span> |<span data-ttu-id="f86a0-264">53</span><span class="sxs-lookup"><span data-stu-id="f86a0-264">53</span></span> |
| <span data-ttu-id="f86a0-265">1000</span><span class="sxs-lookup"><span data-stu-id="f86a0-265">1000</span></span> |<span data-ttu-id="f86a0-266">2535</span><span class="sxs-lookup"><span data-stu-id="f86a0-266">2535</span></span> |<span data-ttu-id="f86a0-267">341</span><span class="sxs-lookup"><span data-stu-id="f86a0-267">341</span></span> |
| <span data-ttu-id="f86a0-268">10000</span><span class="sxs-lookup"><span data-stu-id="f86a0-268">10000</span></span> |<span data-ttu-id="f86a0-269">21605</span><span class="sxs-lookup"><span data-stu-id="f86a0-269">21605</span></span> |<span data-ttu-id="f86a0-270">2737</span><span class="sxs-lookup"><span data-stu-id="f86a0-270">2737</span></span> |

> [!NOTE]
> <span data-ttu-id="f86a0-271">Os resultados não são parâmetros de comparação.</span><span class="sxs-lookup"><span data-stu-id="f86a0-271">Results are not benchmarks.</span></span> <span data-ttu-id="f86a0-272">Consulte Olá [Observação sobre resultados neste tópico](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="f86a0-272">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="f86a0-273">Em tamanhos de lote menores, os parâmetros com valor de tabela de uso Olá superaram Olá **SqlBulkCopy** classe.</span><span class="sxs-lookup"><span data-stu-id="f86a0-273">In smaller batch sizes, hello use table-valued parameters outperformed hello **SqlBulkCopy** class.</span></span> <span data-ttu-id="f86a0-274">No entanto, **SqlBulkCopy** executada 12-31% mais rápido do que parâmetros com valor de tabela para testes de saudação de 1.000 e 10.000 linhas.</span><span class="sxs-lookup"><span data-stu-id="f86a0-274">However, **SqlBulkCopy** performed 12-31% faster than table-valued parameters for hello tests of 1,000 and 10,000 rows.</span></span> <span data-ttu-id="f86a0-275">Como parâmetros com valor de tabela, **SqlBulkCopy** é uma boa opção para inserções em lotes, especialmente quando comparado toohello desempenho de operações não em lotes.</span><span class="sxs-lookup"><span data-stu-id="f86a0-275">Like table-valued parameters, **SqlBulkCopy** is a good option for batched inserts, especially when compared toohello performance of non-batched operations.</span></span>

<span data-ttu-id="f86a0-276">Para saber mais sobre a cópia em massa no ADO.NET, consulte [Operações de cópia em massa no SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).</span><span class="sxs-lookup"><span data-stu-id="f86a0-276">For more information on bulk copy in ADO.NET, see [Bulk Copy Operations in SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).</span></span>

### <a name="multiple-row-parameterized-insert-statements"></a><span data-ttu-id="f86a0-277">Instruções INSERT com parâmetros de várias linhas</span><span class="sxs-lookup"><span data-stu-id="f86a0-277">Multiple-row Parameterized INSERT statements</span></span>
<span data-ttu-id="f86a0-278">Uma alternativa para lotes pequenos é parametrizada de tooconstruct uma grande instrução INSERT que insere várias linhas.</span><span class="sxs-lookup"><span data-stu-id="f86a0-278">One alternative for small batches is tooconstruct a large parameterized INSERT statement that inserts multiple rows.</span></span> <span data-ttu-id="f86a0-279">saudação de exemplo de código a seguir demonstra essa técnica.</span><span class="sxs-lookup"><span data-stu-id="f86a0-279">hello following code example demonstrates this technique.</span></span>

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


<span data-ttu-id="f86a0-280">Este exemplo visa conceito básico de saudação tooshow.</span><span class="sxs-lookup"><span data-stu-id="f86a0-280">This example is meant tooshow hello basic concept.</span></span> <span data-ttu-id="f86a0-281">Um cenário mais realista seria loop por meio de cadeia de consulta Olá necessário entidades tooconstruct hello e parâmetros de comando Olá simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="f86a0-281">A more realistic scenario would loop through hello required entities tooconstruct hello query string and hello command parameters simultaneously.</span></span> <span data-ttu-id="f86a0-282">Você está limitado tooa total de 2100 parâmetros de consulta, e isso limita o número total de saudação de linhas que podem ser processadas dessa maneira.</span><span class="sxs-lookup"><span data-stu-id="f86a0-282">You are limited tooa total of 2100 query parameters, so this limits hello total number of rows that can be processed in this manner.</span></span>

<span data-ttu-id="f86a0-283">Olá ad-hoc teste resultados Mostrar Olá desempenho desse tipo de instrução de inserção em milissegundos a seguir.</span><span class="sxs-lookup"><span data-stu-id="f86a0-283">hello following ad-hoc test results show hello performance of this type of insert statement in milliseconds.</span></span>

| <span data-ttu-id="f86a0-284">Operações</span><span class="sxs-lookup"><span data-stu-id="f86a0-284">Operations</span></span> | <span data-ttu-id="f86a0-285">Parâmetros com valor de tabela (ms)</span><span class="sxs-lookup"><span data-stu-id="f86a0-285">Table-valued parameters (ms)</span></span> | <span data-ttu-id="f86a0-286">Instrução INSERT única (ms)</span><span class="sxs-lookup"><span data-stu-id="f86a0-286">Single-statement INSERT (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f86a0-287">1</span><span class="sxs-lookup"><span data-stu-id="f86a0-287">1</span></span> |<span data-ttu-id="f86a0-288">32</span><span class="sxs-lookup"><span data-stu-id="f86a0-288">32</span></span> |<span data-ttu-id="f86a0-289">20</span><span class="sxs-lookup"><span data-stu-id="f86a0-289">20</span></span> |
| <span data-ttu-id="f86a0-290">10</span><span class="sxs-lookup"><span data-stu-id="f86a0-290">10</span></span> |<span data-ttu-id="f86a0-291">30</span><span class="sxs-lookup"><span data-stu-id="f86a0-291">30</span></span> |<span data-ttu-id="f86a0-292">25</span><span class="sxs-lookup"><span data-stu-id="f86a0-292">25</span></span> |
| <span data-ttu-id="f86a0-293">100</span><span class="sxs-lookup"><span data-stu-id="f86a0-293">100</span></span> |<span data-ttu-id="f86a0-294">33</span><span class="sxs-lookup"><span data-stu-id="f86a0-294">33</span></span> |<span data-ttu-id="f86a0-295">51</span><span class="sxs-lookup"><span data-stu-id="f86a0-295">51</span></span> |

> [!NOTE]
> <span data-ttu-id="f86a0-296">Os resultados não são parâmetros de comparação.</span><span class="sxs-lookup"><span data-stu-id="f86a0-296">Results are not benchmarks.</span></span> <span data-ttu-id="f86a0-297">Consulte Olá [Observação sobre resultados neste tópico](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="f86a0-297">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="f86a0-298">Essa abordagem pode ser ligeiramente mais rápida para lotes com menos de 100 linhas.</span><span class="sxs-lookup"><span data-stu-id="f86a0-298">This approach can be slightly faster for batches that are less than 100 rows.</span></span> <span data-ttu-id="f86a0-299">Embora Olá melhoria seja pequena, essa técnica é outra opção que pode funcionar bem em seu cenário de aplicativo específico.</span><span class="sxs-lookup"><span data-stu-id="f86a0-299">Although hello improvement is small, this technique is another option that might work well in your specific application scenario.</span></span>

### <a name="dataadapter"></a><span data-ttu-id="f86a0-300">DataAdapter</span><span class="sxs-lookup"><span data-stu-id="f86a0-300">DataAdapter</span></span>
<span data-ttu-id="f86a0-301">Olá **DataAdapter** classe permite que você toomodify uma **DataSet** do objeto e, em seguida, enviar alterações hello como operações INSERT, UPDATE e DELETE.</span><span class="sxs-lookup"><span data-stu-id="f86a0-301">hello **DataAdapter** class allows you toomodify a **DataSet** object and then submit hello changes as INSERT, UPDATE, and DELETE operations.</span></span> <span data-ttu-id="f86a0-302">Se você estiver usando Olá **DataAdapter** dessa maneira, é importante toonote que separam as chamadas são feitas para cada operação distinta.</span><span class="sxs-lookup"><span data-stu-id="f86a0-302">If you are using hello **DataAdapter** in this manner, it is important toonote that separate calls are made for each distinct operation.</span></span> <span data-ttu-id="f86a0-303">tooimprove desempenho, use Olá **UpdateBatchSize** número de toohello de propriedade de operações que deve ser colocado em lote por vez.</span><span class="sxs-lookup"><span data-stu-id="f86a0-303">tooimprove performance, use hello **UpdateBatchSize** property toohello number of operations that should be batched at a time.</span></span> <span data-ttu-id="f86a0-304">Para saber mais, consulte [Executando operações em lote usando DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).</span><span class="sxs-lookup"><span data-stu-id="f86a0-304">For more information, see [Performing Batch Operations Using DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).</span></span>

### <a name="entity-framework"></a><span data-ttu-id="f86a0-305">Entity Framework</span><span class="sxs-lookup"><span data-stu-id="f86a0-305">Entity framework</span></span>
<span data-ttu-id="f86a0-306">No momento, o Entity Framework não oferece suporte para o envio em lote.</span><span class="sxs-lookup"><span data-stu-id="f86a0-306">Entity Framework does not currently support batching.</span></span> <span data-ttu-id="f86a0-307">Os desenvolvedores diferentes na comunidade de saudação tentaram toodemonstrate alternativas, como substituição Olá **SaveChanges** método.</span><span class="sxs-lookup"><span data-stu-id="f86a0-307">Different developers in hello community have attempted toodemonstrate workarounds, such as override hello **SaveChanges** method.</span></span> <span data-ttu-id="f86a0-308">Mas soluções Olá geralmente são complexas e personalizadas toohello aplicativo e o modelo de dados.</span><span class="sxs-lookup"><span data-stu-id="f86a0-308">But hello solutions are typically complex and customized toohello application and data model.</span></span> <span data-ttu-id="f86a0-309">projeto do codeplex Entity Framework Olá atualmente tem uma página de discussão sobre essa solicitação de recurso.</span><span class="sxs-lookup"><span data-stu-id="f86a0-309">hello Entity Framework codeplex project currently has a discussion page on this feature request.</span></span> <span data-ttu-id="f86a0-310">tooview esta discussão, consulte [Design Meeting Notes - 2 de agosto de 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).</span><span class="sxs-lookup"><span data-stu-id="f86a0-310">tooview this discussion, see [Design Meeting Notes - August 2, 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).</span></span>

### <a name="xml"></a><span data-ttu-id="f86a0-311">XML</span><span class="sxs-lookup"><span data-stu-id="f86a0-311">XML</span></span>
<span data-ttu-id="f86a0-312">Para fins de integridade, achamos que é importante tootalk sobre XML como uma estratégia de envio em lote.</span><span class="sxs-lookup"><span data-stu-id="f86a0-312">For completeness, we feel that it is important tootalk about XML as a batching strategy.</span></span> <span data-ttu-id="f86a0-313">No entanto, o uso de saudação do XML tem nenhuma vantagem sobre outros métodos e várias desvantagens.</span><span class="sxs-lookup"><span data-stu-id="f86a0-313">However, hello use of XML has no advantages over other methods and several disadvantages.</span></span> <span data-ttu-id="f86a0-314">abordagem de saudação é parâmetros com valor tootable semelhantes, mas um arquivo XML ou uma cadeia de caracteres é passada procedimento tooa armazenado em vez de uma tabela definida pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="f86a0-314">hello approach is similar tootable-valued parameters, but an XML file or string is passed tooa stored procedure instead of a user-defined table.</span></span> <span data-ttu-id="f86a0-315">procedimento armazenado de saudação analisa os comandos de saudação no procedimento armazenado de saudação.</span><span class="sxs-lookup"><span data-stu-id="f86a0-315">hello stored procedure parses hello commands in hello stored procedure.</span></span>

<span data-ttu-id="f86a0-316">Há várias desvantagens toothis abordagem:</span><span class="sxs-lookup"><span data-stu-id="f86a0-316">There are several disadvantages toothis approach:</span></span>

* <span data-ttu-id="f86a0-317">Trabalhar com XML pode ser complicado e pode apresentar muitos erros.</span><span class="sxs-lookup"><span data-stu-id="f86a0-317">Working with XML can be cumbersome and error prone.</span></span>
* <span data-ttu-id="f86a0-318">Olá análise XML no banco de dados de saudação pode ser com uso intensivo de CPU.</span><span class="sxs-lookup"><span data-stu-id="f86a0-318">Parsing hello XML on hello database can be CPU-intensive.</span></span>
* <span data-ttu-id="f86a0-319">Na maioria dos casos, esse método é mais lento se comparado ao uso de parâmetros com valor de tabela.</span><span class="sxs-lookup"><span data-stu-id="f86a0-319">In most cases, this method is slower than table-valued parameters.</span></span>

<span data-ttu-id="f86a0-320">Por esses motivos, o uso de saudação do XML para consultas de lote não é recomendado.</span><span class="sxs-lookup"><span data-stu-id="f86a0-320">For these reasons, hello use of XML for batch queries is not recommended.</span></span>

## <a name="batching-considerations"></a><span data-ttu-id="f86a0-321">Considerações sobre o envio em lote</span><span class="sxs-lookup"><span data-stu-id="f86a0-321">Batching considerations</span></span>
<span data-ttu-id="f86a0-322">Olá seções a seguir fornece mais diretrizes sobre o uso de saudação do envio em lote em aplicativos de banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="f86a0-322">hello following sections provide more guidance for hello use of batching in SQL Database applications.</span></span>

### <a name="tradeoffs"></a><span data-ttu-id="f86a0-323">Compensações</span><span class="sxs-lookup"><span data-stu-id="f86a0-323">Tradeoffs</span></span>
<span data-ttu-id="f86a0-324">Dependendo de sua arquitetura, o envio em lote pode envolver uma compensação entre desempenho e resiliência.</span><span class="sxs-lookup"><span data-stu-id="f86a0-324">Depending on your architecture, batching can involve a tradeoff between performance and resiliency.</span></span> <span data-ttu-id="f86a0-325">Por exemplo, considere o cenário de saudação onde sua função fica ativa inesperadamente.</span><span class="sxs-lookup"><span data-stu-id="f86a0-325">For example, consider hello scenario where your role unexpectedly goes down.</span></span> <span data-ttu-id="f86a0-326">Se você perder uma linha de dados, o impacto de saudação é menor do que o impacto de saudação de perder um lote grande de linhas não enviadas.</span><span class="sxs-lookup"><span data-stu-id="f86a0-326">If you lose one row of data, hello impact is smaller than hello impact of losing a large batch of unsubmitted rows.</span></span> <span data-ttu-id="f86a0-327">Há um risco maior ao buffer de linhas antes de enviá-los toohello banco de dados em uma janela de tempo especificado.</span><span class="sxs-lookup"><span data-stu-id="f86a0-327">There is a greater risk when you buffer rows before sending them toohello database in a specified time window.</span></span>

<span data-ttu-id="f86a0-328">Devido a essa compensação, avalie o tipo de Olá das operações que você envia em lote.</span><span class="sxs-lookup"><span data-stu-id="f86a0-328">Because of this tradeoff, evaluate hello type of operations that you batch.</span></span> <span data-ttu-id="f86a0-329">Utilize o envio em lote de forma mais agressiva (lotes maiores e períodos maiores) com dados menos críticos.</span><span class="sxs-lookup"><span data-stu-id="f86a0-329">Batch more aggressively (larger batches and longer time windows) with data that is less critical.</span></span>

### <a name="batch-size"></a><span data-ttu-id="f86a0-330">Tamanho do lote</span><span class="sxs-lookup"><span data-stu-id="f86a0-330">Batch size</span></span>
<span data-ttu-id="f86a0-331">Em nossos testes, geralmente não houve nenhuma vantagem toobreaking grandes lotes em partes menores.</span><span class="sxs-lookup"><span data-stu-id="f86a0-331">In our tests, there was typically no advantage toobreaking large batches into smaller chunks.</span></span> <span data-ttu-id="f86a0-332">Na verdade, frequentemente essa subdivisão resultou em um desempenho mais lento do que enviar um único lote grande.</span><span class="sxs-lookup"><span data-stu-id="f86a0-332">In fact, this subdivision often resulted in slower performance than submitting a single large batch.</span></span> <span data-ttu-id="f86a0-333">Por exemplo, considere um cenário onde você deseja tooinsert 1000 linhas.</span><span class="sxs-lookup"><span data-stu-id="f86a0-333">For example, consider a scenario where you want tooinsert 1000 rows.</span></span> <span data-ttu-id="f86a0-334">Olá tabela a seguir mostra o tempo de parâmetros com valor de tabela de toouse tooinsert 1000 linhas quando divididas em lotes menores.</span><span class="sxs-lookup"><span data-stu-id="f86a0-334">hello following table shows how long it takes toouse table-valued parameters tooinsert 1000 rows when divided into smaller batches.</span></span>

| <span data-ttu-id="f86a0-335">Tamanho do lote</span><span class="sxs-lookup"><span data-stu-id="f86a0-335">Batch size</span></span> | <span data-ttu-id="f86a0-336">Iterações</span><span class="sxs-lookup"><span data-stu-id="f86a0-336">Iterations</span></span> | <span data-ttu-id="f86a0-337">Parâmetros com valor de tabela (ms)</span><span class="sxs-lookup"><span data-stu-id="f86a0-337">Table-valued parameters (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f86a0-338">1000</span><span class="sxs-lookup"><span data-stu-id="f86a0-338">1000</span></span> |<span data-ttu-id="f86a0-339">1</span><span class="sxs-lookup"><span data-stu-id="f86a0-339">1</span></span> |<span data-ttu-id="f86a0-340">347</span><span class="sxs-lookup"><span data-stu-id="f86a0-340">347</span></span> |
| <span data-ttu-id="f86a0-341">500</span><span class="sxs-lookup"><span data-stu-id="f86a0-341">500</span></span> |<span data-ttu-id="f86a0-342">2</span><span class="sxs-lookup"><span data-stu-id="f86a0-342">2</span></span> |<span data-ttu-id="f86a0-343">355</span><span class="sxs-lookup"><span data-stu-id="f86a0-343">355</span></span> |
| <span data-ttu-id="f86a0-344">100</span><span class="sxs-lookup"><span data-stu-id="f86a0-344">100</span></span> |<span data-ttu-id="f86a0-345">10</span><span class="sxs-lookup"><span data-stu-id="f86a0-345">10</span></span> |<span data-ttu-id="f86a0-346">465</span><span class="sxs-lookup"><span data-stu-id="f86a0-346">465</span></span> |
| <span data-ttu-id="f86a0-347">50</span><span class="sxs-lookup"><span data-stu-id="f86a0-347">50</span></span> |<span data-ttu-id="f86a0-348">20</span><span class="sxs-lookup"><span data-stu-id="f86a0-348">20</span></span> |<span data-ttu-id="f86a0-349">630</span><span class="sxs-lookup"><span data-stu-id="f86a0-349">630</span></span> |

> [!NOTE]
> <span data-ttu-id="f86a0-350">Os resultados não são parâmetros de comparação.</span><span class="sxs-lookup"><span data-stu-id="f86a0-350">Results are not benchmarks.</span></span> <span data-ttu-id="f86a0-351">Consulte Olá [Observação sobre resultados neste tópico](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="f86a0-351">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="f86a0-352">Você pode ver que o melhor desempenho de saudação de 1000 linhas é toosubmit-los todos de uma vez.</span><span class="sxs-lookup"><span data-stu-id="f86a0-352">You can see that hello best performance for 1000 rows is toosubmit them all at once.</span></span> <span data-ttu-id="f86a0-353">Em outros testes (não mostrados aqui) Houve um toobreak de ganho de desempenho pequeno um lote de 10000 linhas em dois lotes de 5000.</span><span class="sxs-lookup"><span data-stu-id="f86a0-353">In other tests (not shown here) there was a small performance gain toobreak a 10000 row batch into two batches of 5000.</span></span> <span data-ttu-id="f86a0-354">Mas o esquema da tabela Olá para esses testes é relativamente simple, portanto, você deve executar testes em seus dados específicos e tooverify de tamanhos de lote essas descobertas.</span><span class="sxs-lookup"><span data-stu-id="f86a0-354">But hello table schema for these tests is relatively simple, so you should perform tests on your specific data and batch sizes tooverify these findings.</span></span>

<span data-ttu-id="f86a0-355">Tooconsider de outro fator é que, se o lote total Olá ficar muito grande, banco de dados SQL poderá limitar e recusar o lote de saudação toocommit.</span><span class="sxs-lookup"><span data-stu-id="f86a0-355">Another factor tooconsider is that if hello total batch becomes too large, SQL Database might throttle and refuse toocommit hello batch.</span></span> <span data-ttu-id="f86a0-356">Para obter melhores resultados de hello, teste toodetermine seu cenário específico se não houver um tamanho de lote ideal.</span><span class="sxs-lookup"><span data-stu-id="f86a0-356">For hello best results, test your specific scenario toodetermine if there is an ideal batch size.</span></span> <span data-ttu-id="f86a0-357">Tornar o tamanho do lote Olá configurável em tempo de execução tooenable ajustes rápidos com base no desempenho ou erros.</span><span class="sxs-lookup"><span data-stu-id="f86a0-357">Make hello batch size configurable at runtime tooenable quick adjustments based on performance or errors.</span></span>

<span data-ttu-id="f86a0-358">Finalmente, equilibre o tamanho de saudação do lote de saudação com hello riscos associados ao envio em lote.</span><span class="sxs-lookup"><span data-stu-id="f86a0-358">Finally, balance hello size of hello batch with hello risks associated with batching.</span></span> <span data-ttu-id="f86a0-359">Se houver erros transitórios ou função hello falhar, considere as consequências de saudação de repetir a operação de saudação ou de perda de dados de saudação do lote hello.</span><span class="sxs-lookup"><span data-stu-id="f86a0-359">If there are transient errors or hello role fails, consider hello consequences of retrying hello operation or of losing hello data in hello batch.</span></span>

### <a name="parallel-processing"></a><span data-ttu-id="f86a0-360">Processamento paralelo</span><span class="sxs-lookup"><span data-stu-id="f86a0-360">Parallel processing</span></span>
<span data-ttu-id="f86a0-361">E se você Olá abordagem de reduzir o tamanho do lote Olá mas usados vários threads tooexecute Olá trabalho?</span><span class="sxs-lookup"><span data-stu-id="f86a0-361">What if you took hello approach of reducing hello batch size but used multiple threads tooexecute hello work?</span></span> <span data-ttu-id="f86a0-362">Novamente, nossos testes mostraram que vários lotes menores multithreaded geralmente apresentaram um desempenho pior do que um único lote maior.</span><span class="sxs-lookup"><span data-stu-id="f86a0-362">Again, our tests showed that several smaller multithreaded batches typically performed worse than a single larger batch.</span></span> <span data-ttu-id="f86a0-363">Olá, teste a seguir tenta tooinsert 1000 linhas em um ou mais lotes paralelos.</span><span class="sxs-lookup"><span data-stu-id="f86a0-363">hello following test attempts tooinsert 1000 rows in one or more parallel batches.</span></span> <span data-ttu-id="f86a0-364">Este teste mostra como uma quantidade maior de lotes simultâneos na verdade diminuiu o desempenho.</span><span class="sxs-lookup"><span data-stu-id="f86a0-364">This test shows how more simultaneous batches actually decreased performance.</span></span>

| <span data-ttu-id="f86a0-365">Tamanho do lote [Iterações]</span><span class="sxs-lookup"><span data-stu-id="f86a0-365">Batch size [Iterations]</span></span> | <span data-ttu-id="f86a0-366">Dois threads (ms)</span><span class="sxs-lookup"><span data-stu-id="f86a0-366">Two threads (ms)</span></span> | <span data-ttu-id="f86a0-367">Quatro threads (ms)</span><span class="sxs-lookup"><span data-stu-id="f86a0-367">Four threads (ms)</span></span> | <span data-ttu-id="f86a0-368">Seis threads (ms)</span><span class="sxs-lookup"><span data-stu-id="f86a0-368">Six threads (ms)</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f86a0-369">1000 [1]</span><span class="sxs-lookup"><span data-stu-id="f86a0-369">1000 [1]</span></span> |<span data-ttu-id="f86a0-370">277</span><span class="sxs-lookup"><span data-stu-id="f86a0-370">277</span></span> |<span data-ttu-id="f86a0-371">315</span><span class="sxs-lookup"><span data-stu-id="f86a0-371">315</span></span> |<span data-ttu-id="f86a0-372">266</span><span class="sxs-lookup"><span data-stu-id="f86a0-372">266</span></span> |
| <span data-ttu-id="f86a0-373">500 [2]</span><span class="sxs-lookup"><span data-stu-id="f86a0-373">500 [2]</span></span> |<span data-ttu-id="f86a0-374">548</span><span class="sxs-lookup"><span data-stu-id="f86a0-374">548</span></span> |<span data-ttu-id="f86a0-375">278</span><span class="sxs-lookup"><span data-stu-id="f86a0-375">278</span></span> |<span data-ttu-id="f86a0-376">256</span><span class="sxs-lookup"><span data-stu-id="f86a0-376">256</span></span> |
| <span data-ttu-id="f86a0-377">250 [4]</span><span class="sxs-lookup"><span data-stu-id="f86a0-377">250 [4]</span></span> |<span data-ttu-id="f86a0-378">405</span><span class="sxs-lookup"><span data-stu-id="f86a0-378">405</span></span> |<span data-ttu-id="f86a0-379">329</span><span class="sxs-lookup"><span data-stu-id="f86a0-379">329</span></span> |<span data-ttu-id="f86a0-380">265</span><span class="sxs-lookup"><span data-stu-id="f86a0-380">265</span></span> |
| <span data-ttu-id="f86a0-381">100 [10]</span><span class="sxs-lookup"><span data-stu-id="f86a0-381">100 [10]</span></span> |<span data-ttu-id="f86a0-382">488</span><span class="sxs-lookup"><span data-stu-id="f86a0-382">488</span></span> |<span data-ttu-id="f86a0-383">439</span><span class="sxs-lookup"><span data-stu-id="f86a0-383">439</span></span> |<span data-ttu-id="f86a0-384">391</span><span class="sxs-lookup"><span data-stu-id="f86a0-384">391</span></span> |

> [!NOTE]
> <span data-ttu-id="f86a0-385">Os resultados não são parâmetros de comparação.</span><span class="sxs-lookup"><span data-stu-id="f86a0-385">Results are not benchmarks.</span></span> <span data-ttu-id="f86a0-386">Consulte Olá [Observação sobre resultados neste tópico](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="f86a0-386">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="f86a0-387">Há várias razões possíveis para a diminuição do desempenho de saudação tooparallelism vencimento:</span><span class="sxs-lookup"><span data-stu-id="f86a0-387">There are several potential reasons for hello degradation in performance due tooparallelism:</span></span>

* <span data-ttu-id="f86a0-388">Há várias chamadas simultâneas de rede em vez de uma.</span><span class="sxs-lookup"><span data-stu-id="f86a0-388">There are multiple simultaneous network calls instead of one.</span></span>
* <span data-ttu-id="f86a0-389">Várias operações em uma única tabela podem resultar em contenção e bloqueio.</span><span class="sxs-lookup"><span data-stu-id="f86a0-389">Multiple operations against a single table can result in contention and blocking.</span></span>
* <span data-ttu-id="f86a0-390">Há sobrecargas associadas ao multithreading.</span><span class="sxs-lookup"><span data-stu-id="f86a0-390">There are overheads associated with multithreading.</span></span>
* <span data-ttu-id="f86a0-391">despesa de saudação de abrir várias conexões supera o benefício de saudação do processamento paralelo.</span><span class="sxs-lookup"><span data-stu-id="f86a0-391">hello expense of opening multiple connections outweighs hello benefit of parallel processing.</span></span>

<span data-ttu-id="f86a0-392">Se você selecionar bancos de dados ou tabelas diferentes, é possível toosee ganho de alguns desempenho com essa estratégia.</span><span class="sxs-lookup"><span data-stu-id="f86a0-392">If you target different tables or databases, it is possible toosee some performance gain with this strategy.</span></span> <span data-ttu-id="f86a0-393">A fragmentação ou federações do banco de dados seria um cenário para essa abordagem.</span><span class="sxs-lookup"><span data-stu-id="f86a0-393">Database sharding or federations would be a scenario for this approach.</span></span> <span data-ttu-id="f86a0-394">Fragmentação usa vários bancos de dados e rotas diferentes dados tooeach banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f86a0-394">Sharding uses multiple databases and routes different data tooeach database.</span></span> <span data-ttu-id="f86a0-395">Se cada lote pequeno for tooa banco de dados diferente, pode ser mais eficiente, em seguida, executar operações de saudação em paralelo.</span><span class="sxs-lookup"><span data-stu-id="f86a0-395">If each small batch is going tooa different database, then performing hello operations in parallel can be more efficient.</span></span> <span data-ttu-id="f86a0-396">No entanto, Olá ganho de desempenho não é toouse significativo o suficiente como base de saudação de fragmentação de banco de dados de toouse uma decisão em sua solução.</span><span class="sxs-lookup"><span data-stu-id="f86a0-396">However, hello performance gain is not significant enough toouse as hello basis for a decision toouse database sharding in your solution.</span></span>

<span data-ttu-id="f86a0-397">Em alguns designs, a execução paralela de lotes menores pode resultar em uma produtividade maior das solicitações em um sistema sob carga.</span><span class="sxs-lookup"><span data-stu-id="f86a0-397">In some designs, parallel execution of smaller batches can result in improved throughput of requests in a system under load.</span></span> <span data-ttu-id="f86a0-398">Nesse caso, mesmo que seja mais rápido tooprocess um único lote maior, processar vários lotes em paralelo poderá ser mais eficiente.</span><span class="sxs-lookup"><span data-stu-id="f86a0-398">In this case, even though it is quicker tooprocess a single larger batch, processing multiple batches in parallel might be more efficient.</span></span>

<span data-ttu-id="f86a0-399">Se você usar a execução paralela, considere o número de máximo de saudação controladora de threads de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f86a0-399">If you do use parallel execution, consider controlling hello maximum number of worker threads.</span></span> <span data-ttu-id="f86a0-400">Uma quantidade menor poderia resultar em menos contenção e um tempo de execução mais rápido.</span><span class="sxs-lookup"><span data-stu-id="f86a0-400">A smaller number might result in less contention and a faster execution time.</span></span> <span data-ttu-id="f86a0-401">Além disso, considere Olá uma carga adicional que isso coloca nos dados de destino Olá nas conexões e transações.</span><span class="sxs-lookup"><span data-stu-id="f86a0-401">Also, consider hello additional load that this places on hello target database both in connections and transactions.</span></span>

### <a name="related-performance-factors"></a><span data-ttu-id="f86a0-402">Fatores de desempenho relacionados</span><span class="sxs-lookup"><span data-stu-id="f86a0-402">Related performance factors</span></span>
<span data-ttu-id="f86a0-403">As orientações típicas sobre o desempenho do banco de dados também dizem respeito ao envio em lote.</span><span class="sxs-lookup"><span data-stu-id="f86a0-403">Typical guidance on database performance also affects batching.</span></span> <span data-ttu-id="f86a0-404">Por exemplo, ocorre a redução do desempenho de inserção para tabelas com uma chave primária grande ou vários índices não clusterizados.</span><span class="sxs-lookup"><span data-stu-id="f86a0-404">For example, insert performance is reduced for tables that have a large primary key or many nonclustered indexes.</span></span>

<span data-ttu-id="f86a0-405">Se os parâmetros com valor de tabela usam um procedimento armazenado, você pode usar o comando Olá **SET NOCOUNT ON** no início de saudação do procedimento de saudação.</span><span class="sxs-lookup"><span data-stu-id="f86a0-405">If table-valued parameters use a stored procedure, you can use hello command **SET NOCOUNT ON** at hello beginning of hello procedure.</span></span> <span data-ttu-id="f86a0-406">Essa instrução suprime o retorno de saudação da contagem de saudação de linhas de saudação afetada no procedimento hello.</span><span class="sxs-lookup"><span data-stu-id="f86a0-406">This statement suppresses hello return of hello count of hello affected rows in hello procedure.</span></span> <span data-ttu-id="f86a0-407">No entanto, em nossos testes, Olá uso de **SET NOCOUNT ON** não teve nenhum efeito ou diminuiu o desempenho.</span><span class="sxs-lookup"><span data-stu-id="f86a0-407">However, in our tests, hello use of **SET NOCOUNT ON** either had no effect or decreased performance.</span></span> <span data-ttu-id="f86a0-408">Olá procedimento armazenado de teste foi simple com um único **inserir** comando de parâmetro com valor de tabela do hello.</span><span class="sxs-lookup"><span data-stu-id="f86a0-408">hello test stored procedure was simple with a single **INSERT** command from hello table-valued parameter.</span></span> <span data-ttu-id="f86a0-409">É possível que outros procedimentos armazenados mais complexos possam se beneficiar dessa instrução.</span><span class="sxs-lookup"><span data-stu-id="f86a0-409">It is possible that more complex stored procedures would benefit from this statement.</span></span> <span data-ttu-id="f86a0-410">Mas não suponha que a adição **SET NOCOUNT ON** procedimento tooyour armazenado automaticamente melhora o desempenho.</span><span class="sxs-lookup"><span data-stu-id="f86a0-410">But don’t assume that adding **SET NOCOUNT ON** tooyour stored procedure automatically improves performance.</span></span> <span data-ttu-id="f86a0-411">toounderstand Olá efeito, teste o procedimento armazenado com e sem Olá **SET NOCOUNT ON** instrução.</span><span class="sxs-lookup"><span data-stu-id="f86a0-411">toounderstand hello effect, test your stored procedure with and without hello **SET NOCOUNT ON** statement.</span></span>

## <a name="batching-scenarios"></a><span data-ttu-id="f86a0-412">Cenários de envio em lote</span><span class="sxs-lookup"><span data-stu-id="f86a0-412">Batching scenarios</span></span>
<span data-ttu-id="f86a0-413">Olá seções a seguir descrevem como parâmetros com valor de tabela de toouse em três cenários de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f86a0-413">hello following sections describe how toouse table-valued parameters in three application scenarios.</span></span> <span data-ttu-id="f86a0-414">Olá primeiro cenário mostra como o buffer e envio em lote podem trabalhar juntos.</span><span class="sxs-lookup"><span data-stu-id="f86a0-414">hello first scenario shows how buffering and batching can work together.</span></span> <span data-ttu-id="f86a0-415">Olá segundo cenário melhora o desempenho executando operações mestre-detalhes em uma chamada de procedimento armazenado único.</span><span class="sxs-lookup"><span data-stu-id="f86a0-415">hello second scenario improves performance by performing master-detail operations in a single stored procedure call.</span></span> <span data-ttu-id="f86a0-416">Olá cenário final mostra como parâmetros com valor de tabela de toouse em uma operação "UPSERT".</span><span class="sxs-lookup"><span data-stu-id="f86a0-416">hello final scenario shows how toouse table-valued parameters in an “UPSERT” operation.</span></span>

### <a name="buffering"></a><span data-ttu-id="f86a0-417">Armazenamento em buffer</span><span class="sxs-lookup"><span data-stu-id="f86a0-417">Buffering</span></span>
<span data-ttu-id="f86a0-418">Embora alguns cenários sejam candidatos óbvios ao envio em lote, há muitos cenários que poderiam se beneficiar do envio em lote por meio do processamento atrasado.</span><span class="sxs-lookup"><span data-stu-id="f86a0-418">Although there are some scenarios that are obvious candidate for batching, there are many scenarios that could take advantage of batching by delayed processing.</span></span> <span data-ttu-id="f86a0-419">No entanto, o processamento atrasado também apresenta um risco maior que dados hello serão perdidos em caso de saudação de uma falha inesperada.</span><span class="sxs-lookup"><span data-stu-id="f86a0-419">However, delayed processing also carries a greater risk that hello data is lost in hello event of an unexpected failure.</span></span> <span data-ttu-id="f86a0-420">É importante toounderstand esse risco e considerar as consequências de saudação.</span><span class="sxs-lookup"><span data-stu-id="f86a0-420">It is important toounderstand this risk and consider hello consequences.</span></span>

<span data-ttu-id="f86a0-421">Por exemplo, considere um aplicativo web que controla o histórico de navegação de saudação de cada usuário.</span><span class="sxs-lookup"><span data-stu-id="f86a0-421">For example, consider a web application that tracks hello navigation history of each user.</span></span> <span data-ttu-id="f86a0-422">Em cada solicitação de página, aplicativo hello pode fazer a exibição de página do banco de dados chamada toorecord saudação do usuário.</span><span class="sxs-lookup"><span data-stu-id="f86a0-422">On each page request, hello application could make a database call toorecord hello user’s page view.</span></span> <span data-ttu-id="f86a0-423">Mas o melhor desempenho e escalabilidade podem ser obtidos com atividades de navegação dos usuários da saudação de buffer e, em seguida, enviar esse banco de dados de toohello de dados em lotes.</span><span class="sxs-lookup"><span data-stu-id="f86a0-423">But higher performance and scalability can be achieved by buffering hello users’ navigation activities and then sending this data toohello database in batches.</span></span> <span data-ttu-id="f86a0-424">Você pode disparar a atualização do banco de dados de saudação pelo tempo decorrido e/ou o tamanho do buffer.</span><span class="sxs-lookup"><span data-stu-id="f86a0-424">You can trigger hello database update by elapsed time and/or buffer size.</span></span> <span data-ttu-id="f86a0-425">Por exemplo, uma regra pode especificar que esse lote Olá deve ser processado depois de 20 segundos ou quando o buffer de saudação atingir 1000 itens.</span><span class="sxs-lookup"><span data-stu-id="f86a0-425">For example, a rule could specify that hello batch should be processed after 20 seconds or when hello buffer reaches 1000 items.</span></span>

<span data-ttu-id="f86a0-426">usos de exemplo de código a seguir Olá [extensões reativas - Rx](https://msdn.microsoft.com/data/gg577609) tooprocess em buffer os eventos gerados por uma classe de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="f86a0-426">hello following code example uses [Reactive Extensions - Rx](https://msdn.microsoft.com/data/gg577609) tooprocess buffered events raised by a monitoring class.</span></span> <span data-ttu-id="f86a0-427">Olá quando preenchimentos de buffer ou um tempo limite é atingido, lote Olá dos dados do usuário é enviado toohello banco de dados com um parâmetro com valor de tabela.</span><span class="sxs-lookup"><span data-stu-id="f86a0-427">When hello buffer fills or a timeout is reached, hello batch of user data is sent toohello database with a table-valued parameter.</span></span>

<span data-ttu-id="f86a0-428">Olá NavHistoryData classe modelos Olá usuário navegação detalhes a seguir.</span><span class="sxs-lookup"><span data-stu-id="f86a0-428">hello following NavHistoryData class models hello user navigation details.</span></span> <span data-ttu-id="f86a0-429">Contém informações básicas, como o identificador de usuário hello, Olá URL acessada e Olá tempo de acesso.</span><span class="sxs-lookup"><span data-stu-id="f86a0-429">It contains basic information such as hello user identifier, hello URL accessed, and hello access time.</span></span>

    public class NavHistoryData
    {
        public NavHistoryData(int userId, string url, DateTime accessTime)
        { UserId = userId; URL = url; AccessTime = accessTime; }
        public int UserId { get; set; }
        public string URL { get; set; }
        public DateTime AccessTime { get; set; }
    }

<span data-ttu-id="f86a0-430">Olá classe NavHistoryDataMonitor é responsável por buffer Olá usuário navegação dados toohello banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f86a0-430">hello NavHistoryDataMonitor class is responsible for buffering hello user navigation data toohello database.</span></span> <span data-ttu-id="f86a0-431">Ela contém um método, RecordUserNavigationEntry, que responde gerando um evento **OnAdded** .</span><span class="sxs-lookup"><span data-stu-id="f86a0-431">It contains a method, RecordUserNavigationEntry, which responds by raising an **OnAdded** event.</span></span> <span data-ttu-id="f86a0-432">Olá código a seguir mostra a lógica do construtor Olá que usa Rx toocreate uma coleção observável com base em evento hello.</span><span class="sxs-lookup"><span data-stu-id="f86a0-432">hello following code shows hello constructor logic that uses Rx toocreate an observable collection based on hello event.</span></span> <span data-ttu-id="f86a0-433">Ele, em seguida, assina coleção observável toothis com método de Buffer hello.</span><span class="sxs-lookup"><span data-stu-id="f86a0-433">It then subscribes toothis observable collection with hello Buffer method.</span></span> <span data-ttu-id="f86a0-434">sobrecarga de saudação especifica que buffer Olá deve ser enviado a cada 20 segundos ou 1000 entradas.</span><span class="sxs-lookup"><span data-stu-id="f86a0-434">hello overload specifies that hello buffer should be sent every 20 seconds or 1000 entries.</span></span>

    public NavHistoryDataMonitor()
    {
        var observableData =
            Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

        observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
    }

<span data-ttu-id="f86a0-435">manipulador de saudação converte todos os itens de saudação em buffer em um tipo com valor de tabela e passa esse procedimento de tooa armazenado tipo daquele lote de saudação de processos.</span><span class="sxs-lookup"><span data-stu-id="f86a0-435">hello handler converts all of hello buffered items into a table-valued type and then passes this type tooa stored procedure that processes hello batch.</span></span> <span data-ttu-id="f86a0-436">Olá código a seguir mostra a definição completa Olá Olá NavHistoryDataEventArgs e classes de NavHistoryDataMonitor hello.</span><span class="sxs-lookup"><span data-stu-id="f86a0-436">hello following code shows hello complete definition for both hello NavHistoryDataEventArgs and hello NavHistoryDataMonitor classes.</span></span>

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

<span data-ttu-id="f86a0-437">toouse essa classe de buffer, o aplicativo hello cria um objeto NavHistoryDataMonitor estático.</span><span class="sxs-lookup"><span data-stu-id="f86a0-437">toouse this buffering class, hello application creates a static NavHistoryDataMonitor object.</span></span> <span data-ttu-id="f86a0-438">Cada vez que um usuário acessa uma página, aplicativo hello chama o método de NavHistoryDataMonitor.RecordUserNavigationEntry hello.</span><span class="sxs-lookup"><span data-stu-id="f86a0-438">Each time a user accesses a page, hello application calls hello NavHistoryDataMonitor.RecordUserNavigationEntry method.</span></span> <span data-ttu-id="f86a0-439">Olá buffer lógica continua tootake respeito enviar esses bancos de dados de toohello entradas em lotes.</span><span class="sxs-lookup"><span data-stu-id="f86a0-439">hello buffering logic proceeds tootake care of sending these entries toohello database in batches.</span></span>

### <a name="master-detail"></a><span data-ttu-id="f86a0-440">Detalhes da tabela mestra</span><span class="sxs-lookup"><span data-stu-id="f86a0-440">Master detail</span></span>
<span data-ttu-id="f86a0-441">Parâmetros com valor de tabela são úteis para cenários INSERT simples.</span><span class="sxs-lookup"><span data-stu-id="f86a0-441">Table-valued parameters are useful for simple INSERT scenarios.</span></span> <span data-ttu-id="f86a0-442">No entanto, pode ser mais difícil inserções toobatch que envolvem mais de uma tabela.</span><span class="sxs-lookup"><span data-stu-id="f86a0-442">However, it can be more challenging toobatch inserts that involve more than one table.</span></span> <span data-ttu-id="f86a0-443">cenário de "mestre/detalhes" Hello é um bom exemplo.</span><span class="sxs-lookup"><span data-stu-id="f86a0-443">hello “master/detail” scenario is a good example.</span></span> <span data-ttu-id="f86a0-444">tabela mestre Olá identifica a entidade principal hello.</span><span class="sxs-lookup"><span data-stu-id="f86a0-444">hello master table identifies hello primary entity.</span></span> <span data-ttu-id="f86a0-445">Uma ou mais tabelas de detalhes armazenam mais dados sobre a entidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="f86a0-445">One or more detail tables store more data about hello entity.</span></span> <span data-ttu-id="f86a0-446">Nesse cenário, relações de chave estrangeira impõem relação Olá de entidade mestra exclusiva de tooa detalhes.</span><span class="sxs-lookup"><span data-stu-id="f86a0-446">In this scenario, foreign key relationships enforce hello relationship of details tooa unique master entity.</span></span> <span data-ttu-id="f86a0-447">Considere uma versão simplificada de uma tabela PurchaseOrder e sua tabela associada OrderDetail.</span><span class="sxs-lookup"><span data-stu-id="f86a0-447">Consider a simplified version of a PurchaseOrder table and its associated OrderDetail table.</span></span> <span data-ttu-id="f86a0-448">Olá Transact-SQL a seguir cria a tabela de PurchaseOrder de saudação com quatro colunas: Status, OrderDate, CustomerID e OrderID.</span><span class="sxs-lookup"><span data-stu-id="f86a0-448">hello following Transact-SQL creates hello PurchaseOrder table with four columns: OrderID, OrderDate, CustomerID, and Status.</span></span>

    CREATE TABLE [dbo].[PurchaseOrder](
    [OrderID] [int] IDENTITY(1,1) NOT NULL,
    [OrderDate] [datetime] NOT NULL,
    [CustomerID] [int] NOT NULL,
    [Status] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrder] 
    PRIMARY KEY CLUSTERED ( [OrderID] ASC ))

<span data-ttu-id="f86a0-449">Cada pedido contém uma ou mais compras de produtos.</span><span class="sxs-lookup"><span data-stu-id="f86a0-449">Each order contains one or more product purchases.</span></span> <span data-ttu-id="f86a0-450">Essas informações são capturadas na tabela de PurchaseOrderDetail hello.</span><span class="sxs-lookup"><span data-stu-id="f86a0-450">This information is captured in hello PurchaseOrderDetail table.</span></span> <span data-ttu-id="f86a0-451">Olá Transact-SQL a seguir cria a tabela PurchaseOrderDetail de saudação com cinco colunas: OrderID, OrderDetailID, ProductID, UnitPrice e OrderQty.</span><span class="sxs-lookup"><span data-stu-id="f86a0-451">hello following Transact-SQL creates hello PurchaseOrderDetail table with five columns: OrderID, OrderDetailID, ProductID, UnitPrice, and OrderQty.</span></span>

    CREATE TABLE [dbo].[PurchaseOrderDetail](
    [OrderID] [int] NOT NULL,
    [OrderDetailID] [int] IDENTITY(1,1) NOT NULL,
    [ProductID] [int] NOT NULL,
    [UnitPrice] [money] NULL,
    [OrderQty] [smallint] NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrderDetail] PRIMARY KEY CLUSTERED 
    ( [OrderID] ASC, [OrderDetailID] ASC ))

<span data-ttu-id="f86a0-452">coluna de OrderID Olá na tabela de PurchaseOrderDetail Olá deve fazer referência a uma ordem da tabela de PurchaseOrder hello.</span><span class="sxs-lookup"><span data-stu-id="f86a0-452">hello OrderID column in hello PurchaseOrderDetail table must reference an order from hello PurchaseOrder table.</span></span> <span data-ttu-id="f86a0-453">Olá após a definição de uma chave estrangeira impõe essa restrição.</span><span class="sxs-lookup"><span data-stu-id="f86a0-453">hello following definition of a foreign key enforces this constraint.</span></span>

    ALTER TABLE [dbo].[PurchaseOrderDetail]  WITH CHECK ADD 
    CONSTRAINT [FK_OrderID_PurchaseOrder] FOREIGN KEY([OrderID])
    REFERENCES [dbo].[PurchaseOrder] ([OrderID])

<span data-ttu-id="f86a0-454">Ordem toouse com valor de tabela parâmetros in, você deve ter um tipo de tabela definido pelo usuário para cada tabela de destino.</span><span class="sxs-lookup"><span data-stu-id="f86a0-454">In order toouse table-valued parameters, you must have one user-defined table type for each target table.</span></span>

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

<span data-ttu-id="f86a0-455">Em seguida, defina um procedimento armazenado que aceite tabelas desses tipos.</span><span class="sxs-lookup"><span data-stu-id="f86a0-455">Then define a stored procedure that accepts tables of these types.</span></span> <span data-ttu-id="f86a0-456">Esse procedimento permite que um aplicativo toolocally lote um conjunto de pedidos e detalhes do pedido em uma única chamada.</span><span class="sxs-lookup"><span data-stu-id="f86a0-456">This procedure allows an application toolocally batch a set of orders and order details in a single call.</span></span> <span data-ttu-id="f86a0-457">Olá Transact-SQL a seguir fornece Olá declaração de procedimento armazenado completa para este exemplo de ordem de compra.</span><span class="sxs-lookup"><span data-stu-id="f86a0-457">hello following Transact-SQL provides hello complete stored procedure declaration for this purchase order example.</span></span>

    CREATE PROCEDURE sp_InsertOrdersBatch (
    @orders as PurchaseOrderTableType READONLY,
    @details as PurchaseOrderDetailTableType READONLY )
    AS
    SET NOCOUNT ON;

    -- Table that connects hello order identifiers in hello @orders
    -- table with hello actual order identifiers in hello PurchaseOrder table
    DECLARE @IdentityLink AS TABLE ( 
    SubmittedKey int, 
    ActualKey int, 
    RowNumber int identity(1,1)
    );

          -- Add new orders toohello PurchaseOrder table, storing hello actual
    -- order identifiers in hello @IdentityLink table   
    INSERT INTO PurchaseOrder ([OrderDate], [CustomerID], [Status])
    OUTPUT inserted.OrderID INTO @IdentityLink (ActualKey)
    SELECT [OrderDate], [CustomerID], [Status] FROM @orders ORDER BY OrderID;

    -- Match hello passed-in order identifiers with hello actual identifiers
    -- and complete hello @IdentityLink table for use with inserting hello details
    WITH OrderedRows As (
    SELECT OrderID, ROW_NUMBER () OVER (ORDER BY OrderID) As RowNumber 
    FROM @orders
    )
    UPDATE @IdentityLink SET SubmittedKey = M.OrderID
    FROM @IdentityLink L JOIN OrderedRows M ON L.RowNumber = M.RowNumber;

    -- Insert hello order details into hello PurchaseOrderDetail table, 
          -- using hello actual order identifiers of hello master table, PurchaseOrder
    INSERT INTO PurchaseOrderDetail (
    [OrderID],
    [ProductID],
    [UnitPrice],
    [OrderQty] )
    SELECT L.ActualKey, D.ProductID, D.UnitPrice, D.OrderQty
    FROM @details D
    JOIN @IdentityLink L ON L.SubmittedKey = D.OrderID;
    GO

<span data-ttu-id="f86a0-458">Neste exemplo, Olá definidos localmente @IdentityLink tabela armazena valores reais de OrderID Olá das linhas recentemente inserida de saudação.</span><span class="sxs-lookup"><span data-stu-id="f86a0-458">In this example, hello locally defined @IdentityLink table stores hello actual OrderID values from hello newly inserted rows.</span></span> <span data-ttu-id="f86a0-459">Esses identificadores de ordem sejam diferentes dos valores de OrderID temporários Olá no hello @orders e @details parâmetros com valor de tabela.</span><span class="sxs-lookup"><span data-stu-id="f86a0-459">These order identifiers are different from hello temporary OrderID values in hello @orders and @details table-valued parameters.</span></span> <span data-ttu-id="f86a0-460">Por esse motivo, Olá @IdentityLink tabela, em seguida, conecta-se valores de OrderID Olá em Olá @orders toohello real OrderID valores de parâmetro para novas linhas Olá na tabela de PurchaseOrder hello.</span><span class="sxs-lookup"><span data-stu-id="f86a0-460">For this reason, hello @IdentityLink table then connects hello OrderID values from hello @orders parameter toohello real OrderID values for hello new rows in hello PurchaseOrder table.</span></span> <span data-ttu-id="f86a0-461">Após essa etapa, Olá @IdentityLink pode facilitar a tabela Detalhes do pedido Olá inserindo com hello OrderID real que satisfaz a restrição de chave estrangeira hello.</span><span class="sxs-lookup"><span data-stu-id="f86a0-461">After this step, hello @IdentityLink table can facilitate inserting hello order details with hello actual OrderID that satisfies hello foreign key constraint.</span></span>

<span data-ttu-id="f86a0-462">Esse procedimento armazenado pode ser usado do código ou de outras chamadas Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="f86a0-462">This stored procedure can be used from code or from other Transact-SQL calls.</span></span> <span data-ttu-id="f86a0-463">Consulte a seção de parâmetros com valor de tabela de saudação deste documento para obter um exemplo de código.</span><span class="sxs-lookup"><span data-stu-id="f86a0-463">See hello table-valued parameters section of this paper for a code example.</span></span> <span data-ttu-id="f86a0-464">Olá Transact-SQL a seguir mostra como toocall Olá sp_InsertOrdersBatch.</span><span class="sxs-lookup"><span data-stu-id="f86a0-464">hello following Transact-SQL shows how toocall hello sp_InsertOrdersBatch.</span></span>

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

<span data-ttu-id="f86a0-465">Esta solução permite que cada lote toouse um conjunto de valores de OrderID que começam com 1.</span><span class="sxs-lookup"><span data-stu-id="f86a0-465">This solution allows each batch toouse a set of OrderID values that begin at 1.</span></span> <span data-ttu-id="f86a0-466">Os valores de OrderID temporários descrevem relações Olá em lote hello, mas valores reais de OrderID Olá são determinados no tempo de saudação da operação de inserção de saudação.</span><span class="sxs-lookup"><span data-stu-id="f86a0-466">These temporary OrderID values describe hello relationships in hello batch, but hello actual OrderID values are determined at hello time of hello insert operation.</span></span> <span data-ttu-id="f86a0-467">Você pode executar Olá mesmas instruções no exemplo anterior Olá repetidamente e gerar pedidos exclusivos no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="f86a0-467">You can run hello same statements in hello previous example repeatedly and generate unique orders in hello database.</span></span> <span data-ttu-id="f86a0-468">Por esse motivo, considere a adição de mais código ou lógica de banco de dados que impeça os pedidos duplicados ao usar esta técnica de envio em lote.</span><span class="sxs-lookup"><span data-stu-id="f86a0-468">For this reason, consider adding more code or database logic that prevents duplicate orders when using this batching technique.</span></span>

<span data-ttu-id="f86a0-469">Este exemplo demonstra que até mesmo as operações de banco de dados mais complexas, como operações de mestre-detalhes, podem ser enviadas em lote usando parâmetros com valor de tabela.</span><span class="sxs-lookup"><span data-stu-id="f86a0-469">This example demonstrates that even more complex database operations, such as master-detail operations, can be batched using table-valued parameters.</span></span>

### <a name="upsert"></a><span data-ttu-id="f86a0-470">UPSERT</span><span class="sxs-lookup"><span data-stu-id="f86a0-470">UPSERT</span></span>
<span data-ttu-id="f86a0-471">Outro cenário de envio em lote envolve a atualização simultânea de linhas existentes e a inserção de novas linhas.</span><span class="sxs-lookup"><span data-stu-id="f86a0-471">Another batching scenario involves simultaneously updating existing rows and inserting new rows.</span></span> <span data-ttu-id="f86a0-472">Esta operação é às vezes chamado tooas uma operação "UPSERT" (atualização + inserção).</span><span class="sxs-lookup"><span data-stu-id="f86a0-472">This operation is sometimes referred tooas an “UPSERT” (update + insert) operation.</span></span> <span data-ttu-id="f86a0-473">Em vez de fazer chamadas separadas tooINSERT e atualização, instrução de mesclagem Olá é melhor adequada toothis tarefa.</span><span class="sxs-lookup"><span data-stu-id="f86a0-473">Rather than making separate calls tooINSERT and UPDATE, hello MERGE statement is best suited toothis task.</span></span> <span data-ttu-id="f86a0-474">Olá instrução MERGE pode executar os dois insert e operações em uma única chamada de atualização.</span><span class="sxs-lookup"><span data-stu-id="f86a0-474">hello MERGE statement can perform both insert and update operations in a single call.</span></span>

<span data-ttu-id="f86a0-475">Parâmetros com valor de tabela podem ser usados com hello mesclagem instrução tooperform atualizações e inserções.</span><span class="sxs-lookup"><span data-stu-id="f86a0-475">Table-valued parameters can be used with hello MERGE statement tooperform updates and inserts.</span></span> <span data-ttu-id="f86a0-476">Por exemplo, considere uma tabela funcionário simplificada que contém Olá colunas a seguir: EmployeeID, FirstName, LastName, NúmeroDoINPS:</span><span class="sxs-lookup"><span data-stu-id="f86a0-476">For example, consider a simplified Employee table that contains hello following columns: EmployeeID, FirstName, LastName, SocialSecurityNumber:</span></span>

    CREATE TABLE [dbo].[Employee](
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [SocialSecurityNumber] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_Employee] PRIMARY KEY CLUSTERED 
    ([EmployeeID] ASC ))

<span data-ttu-id="f86a0-477">Neste exemplo, você pode usar o fato de saudação que Olá NúmeroDoINPS é exclusivo tooperform uma mesclagem de vários funcionários.</span><span class="sxs-lookup"><span data-stu-id="f86a0-477">In this example, you can use hello fact that hello SocialSecurityNumber is unique tooperform a MERGE of multiple employees.</span></span> <span data-ttu-id="f86a0-478">Primeiro, crie o tipo de tabela definido pelo usuário de saudação:</span><span class="sxs-lookup"><span data-stu-id="f86a0-478">First, create hello user-defined table type:</span></span>

    CREATE TYPE EmployeeTableType AS TABLE 
    ( Employee_ID INT,
      FirstName NVARCHAR(50),
      LastName NVARCHAR(50),
      SocialSecurityNumber NVARCHAR(50) );
    GO

<span data-ttu-id="f86a0-479">Em seguida, criar um procedimento armazenado ou escreva código que usa Olá atualização de saudação de tooperform de instrução direta e insert.</span><span class="sxs-lookup"><span data-stu-id="f86a0-479">Next, create a stored procedure or write code that uses hello MERGE statement tooperform hello update and insert.</span></span> <span data-ttu-id="f86a0-480">Olá exemplo a seguir usa Olá instrução MERGE em um parâmetro com valor de tabela, @employees, do tipo EmployeeTableType.</span><span class="sxs-lookup"><span data-stu-id="f86a0-480">hello following example uses hello MERGE statement on a table-valued parameter, @employees, of type EmployeeTableType.</span></span> <span data-ttu-id="f86a0-481">Olá conteúdo da saudação @employees tabela não são mostradas aqui.</span><span class="sxs-lookup"><span data-stu-id="f86a0-481">hello contents of hello @employees table are not shown here.</span></span>

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

<span data-ttu-id="f86a0-482">Para obter mais informações, consulte documentação hello e exemplos Olá instrução de mesclagem.</span><span class="sxs-lookup"><span data-stu-id="f86a0-482">For more information, see hello documentation and examples for hello MERGE statement.</span></span> <span data-ttu-id="f86a0-483">Embora Olá mesmo trabalho possa ser executado em várias etapas armazenados chamada de procedimento com operações INSERT e UPDATE separadas, Olá instrução MERGE é mais eficiente.</span><span class="sxs-lookup"><span data-stu-id="f86a0-483">Although hello same work could be performed in a multiple-step stored procedure call with separate INSERT and UPDATE operations, hello MERGE statement is more efficient.</span></span> <span data-ttu-id="f86a0-484">Código do banco de dados também pode criar as chamadas Transact-SQL que usam a instrução de mesclagem Olá diretamente sem exigir duas chamadas de banco de dados para INSERT e UPDATE.</span><span class="sxs-lookup"><span data-stu-id="f86a0-484">Database code can also construct Transact-SQL calls that use hello MERGE statement directly without requiring two database calls for INSERT and UPDATE.</span></span>

## <a name="recommendation-summary"></a><span data-ttu-id="f86a0-485">Resumo de recomendações</span><span class="sxs-lookup"><span data-stu-id="f86a0-485">Recommendation summary</span></span>
<span data-ttu-id="f86a0-486">Olá lista a seguir fornece um resumo da saudação envio em lote recomendações discutidas neste tópico:</span><span class="sxs-lookup"><span data-stu-id="f86a0-486">hello following list provides a summary of hello batching recommendations discussed in this topic:</span></span>

* <span data-ttu-id="f86a0-487">Use buffer e envio em lote de desempenho de saudação tooincrease e escalabilidade de aplicativos de banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="f86a0-487">Use buffering and batching tooincrease hello performance and scalability of SQL Database applications.</span></span>
* <span data-ttu-id="f86a0-488">Entenda as compensações de saudação entre o envio em lote/buffer e a resiliência.</span><span class="sxs-lookup"><span data-stu-id="f86a0-488">Understand hello tradeoffs between batching/buffering and resiliency.</span></span> <span data-ttu-id="f86a0-489">Durante uma falha de função, o risco de saudação de perder um lote não processado de dados essenciais aos negócios pode compensar benefício de desempenho de saudação do envio em lote.</span><span class="sxs-lookup"><span data-stu-id="f86a0-489">During a role failure, hello risk of losing an unprocessed batch of business-critical data might outweigh hello performance benefit of batching.</span></span>
* <span data-ttu-id="f86a0-490">Tentativa de tookeep todas as chamadas toohello banco de dados de latência de tooreduce um único datacenter.</span><span class="sxs-lookup"><span data-stu-id="f86a0-490">Attempt tookeep all calls toohello database within a single datacenter tooreduce latency.</span></span>
* <span data-ttu-id="f86a0-491">Se você escolher uma única técnica de envio em lote, parâmetros com valor de tabela oferecem flexibilidade e Olá melhor desempenho.</span><span class="sxs-lookup"><span data-stu-id="f86a0-491">If you choose a single batching technique, table-valued parameters offer hello best performance and flexibility.</span></span>
* <span data-ttu-id="f86a0-492">Para hello mais rápido desempenho de inserção, siga estas diretrizes gerais mas testar seu cenário:</span><span class="sxs-lookup"><span data-stu-id="f86a0-492">For hello fastest insert performance, follow these general guidelines but test your scenario:</span></span>
  * <span data-ttu-id="f86a0-493">Para menos de 100 linhas, use um único comando INSERT com parâmetros.</span><span class="sxs-lookup"><span data-stu-id="f86a0-493">For < 100 rows, use a single parameterized INSERT command.</span></span>
  * <span data-ttu-id="f86a0-494">Para menos de 1000 linhas, use parâmetros com valor de tabela.</span><span class="sxs-lookup"><span data-stu-id="f86a0-494">For < 1000 rows, use table-valued parameters.</span></span>
  * <span data-ttu-id="f86a0-495">Para 1000 linhas ou mais, use SqlBulkCopy.</span><span class="sxs-lookup"><span data-stu-id="f86a0-495">For >= 1000 rows, use SqlBulkCopy.</span></span>
* <span data-ttu-id="f86a0-496">Para atualizar e excluir operações, use parâmetros com valor de tabela com a lógica de procedimento armazenado que determina a operação correta de saudação em cada linha no parâmetro de tabela hello.</span><span class="sxs-lookup"><span data-stu-id="f86a0-496">For update and delete operations, use table-valued parameters with stored procedure logic that determines hello correct operation on each row in hello table parameter.</span></span>
* <span data-ttu-id="f86a0-497">Diretrizes para o tamanho do lote:</span><span class="sxs-lookup"><span data-stu-id="f86a0-497">Batch size guidelines:</span></span>
  * <span data-ttu-id="f86a0-498">Use Olá tamanhos de lote maiores que fazem sentido para o aplicativo e os requisitos de negócios.</span><span class="sxs-lookup"><span data-stu-id="f86a0-498">Use hello largest batch sizes that make sense for your application and business requirements.</span></span>
  * <span data-ttu-id="f86a0-499">Ganho de desempenho de saudação do saldo de lotes grandes com riscos de saudação de falhas catastróficas ou temporárias.</span><span class="sxs-lookup"><span data-stu-id="f86a0-499">Balance hello performance gain of large batches with hello risks of temporary or catastrophic failures.</span></span> <span data-ttu-id="f86a0-500">O que é a consequência de saudação de repetições ou perda de dados de saudação em lote Olá?</span><span class="sxs-lookup"><span data-stu-id="f86a0-500">What is hello consequence of retries or loss of hello data in hello batch?</span></span> 
  * <span data-ttu-id="f86a0-501">Teste Olá maior lote tamanho tooverify que banco de dados SQL não rejeitá-la.</span><span class="sxs-lookup"><span data-stu-id="f86a0-501">Test hello largest batch size tooverify that SQL Database does not reject it.</span></span>
  * <span data-ttu-id="f86a0-502">Crie definições de configuração que controle envio em lote, como tamanho de lote de saudação ou janela de tempo de buffer de saudação.</span><span class="sxs-lookup"><span data-stu-id="f86a0-502">Create configuration settings that control batching, such as hello batch size or hello buffering time window.</span></span> <span data-ttu-id="f86a0-503">Essas configurações fornecem flexibilidade.</span><span class="sxs-lookup"><span data-stu-id="f86a0-503">These settings provide flexibility.</span></span> <span data-ttu-id="f86a0-504">Você pode alterar Olá envio em lote comportamento na produção sem reimplantar o serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="f86a0-504">You can change hello batching behavior in production without redeploying hello cloud service.</span></span>
* <span data-ttu-id="f86a0-505">Evite a execução paralela de lotes que operam em uma única tabela em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f86a0-505">Avoid parallel execution of batches that operate on a single table in one database.</span></span> <span data-ttu-id="f86a0-506">Se você escolher toodivide um único lote em vários threads de trabalho, execute testes toodetermine Olá número ideal de threads.</span><span class="sxs-lookup"><span data-stu-id="f86a0-506">If you do choose toodivide a single batch across multiple worker threads, run tests toodetermine hello ideal number of threads.</span></span> <span data-ttu-id="f86a0-507">Após um limite não especificado, uma quantidade maior de threads diminuirá o desempenho em vez de aumentá-lo.</span><span class="sxs-lookup"><span data-stu-id="f86a0-507">After an unspecified threshold, more threads will decrease performance rather than increase it.</span></span>
* <span data-ttu-id="f86a0-508">Considere o armazenamento em buffer de acordo com o tamanho e o tempo como uma maneira de implementar o envio em lote para mais cenários.</span><span class="sxs-lookup"><span data-stu-id="f86a0-508">Consider buffering on size and time as a way of implementing batching for more scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f86a0-509">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f86a0-509">Next steps</span></span>
<span data-ttu-id="f86a0-510">Este artigo se concentra em como o design de banco de dados e técnicas de codificação relacionam toobatching pode melhorar o desempenho do aplicativo e a escalabilidade.</span><span class="sxs-lookup"><span data-stu-id="f86a0-510">This article focused on how database design and coding techniques related toobatching can improve your application performance and scalability.</span></span> <span data-ttu-id="f86a0-511">Mas isso é apenas um fator em sua estratégia geral.</span><span class="sxs-lookup"><span data-stu-id="f86a0-511">But this is just one factor in your overall strategy.</span></span> <span data-ttu-id="f86a0-512">Para obter escalabilidade e desempenho de tooimprove maneiras, consulte [diretrizes de desempenho de banco de dados SQL para bancos de dados único](sql-database-performance-guidance.md) e [considerações de preço e desempenho para um pool Elástico](sql-database-elastic-pool-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="f86a0-512">For more ways tooimprove performance and scalability, see [Azure SQL Database performance guidance for single databases](sql-database-performance-guidance.md) and [Price and performance considerations for an elastic pool](sql-database-elastic-pool-guidance.md).</span></span>

