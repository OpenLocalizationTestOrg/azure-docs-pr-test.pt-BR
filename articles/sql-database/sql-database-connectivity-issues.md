---
title: "aaaFix um erro de conexão do SQL, erro transitório | Microsoft Docs"
description: "Saiba como tootroubleshoot, diagnosticar e evitar que um erro de conexão do SQL ou transitórias no banco de dados do SQL Azure. "
keywords: "conexão do sql, cadeia de conexão, problemas de conectividade, erro transitório, erro de conexão"
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: efb35451-3fed-4264-bf86-72b350f67d50
ms.service: sql-database
ms.custom: develop apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: d225e610b9e88170ab53ca16d615bd07220603cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-diagnose-and-prevent-sql-connection-errors-and-transient-errors-for-sql-database"></a><span data-ttu-id="b4f5f-104">Solucionar problemas, diagnosticar e evitar erros de conexão SQL e erros transitórios para o Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="b4f5f-104">Troubleshoot, diagnose, and prevent SQL connection errors and transient errors for SQL Database</span></span>
<span data-ttu-id="b4f5f-105">Este artigo descreve como tooprevent, solucionar problemas, diagnosticar e reduzir os erros de conexão e erros transitórios que seu aplicativo cliente encontra quando ele interage com o banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-105">This article describes how tooprevent, troubleshoot, diagnose, and mitigate connection errors and transient errors that your client application encounters when it interacts with Azure SQL Database.</span></span> <span data-ttu-id="b4f5f-106">Saiba como tooconfigure lógica de repetição, criar cadeia de caracteres de conexão hello e ajuste outras configurações de conexão.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-106">Learn how tooconfigure retry logic, build hello connection string, and adjust other connection settings.</span></span>

<a id="i-transient-faults" name="i-transient-faults"></a>

## <a name="transient-errors-transient-faults"></a><span data-ttu-id="b4f5f-107">Erros transitórios (falhas transitórias)</span><span class="sxs-lookup"><span data-stu-id="b4f5f-107">Transient errors (transient faults)</span></span>
<span data-ttu-id="b4f5f-108">Um erro transitório (também chamado de falha transitória) tem uma causa que, em breve, será resolvida.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-108">A transient error - also, transient fault - has an underlying cause that will soon resolve itself.</span></span> <span data-ttu-id="b4f5f-109">Uma causa ocasional erros transitórios é quando Olá sistema Azure rapidamente desloca balanceamento de carga de toobetter de recursos de hardware várias cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-109">An occasional cause of transient errors is when hello Azure system quickly shifts hardware resources toobetter load-balance various workloads.</span></span> <span data-ttu-id="b4f5f-110">A maioria desses eventos de reconfiguração normalmente é concluída em menos de 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-110">Most of these reconfiguration events often complete in less than 60 seconds.</span></span> <span data-ttu-id="b4f5f-111">Durante esse período de tempo de reconfiguração, você pode ter conectividade emite tooAzure banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-111">During this reconfiguration time span, you may have connectivity issues tooAzure SQL Database.</span></span> <span data-ttu-id="b4f5f-112">Aplicativos que se conectam tooAzure banco de dados SQL deve ser compilado tooexpect esses erros transitórios, identificador-los com a implementação de lógica de repetição em seu código em vez de tê-los toousers como erros de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-112">Applications connecting tooAzure SQL Database should be built tooexpect these transient errors, handle them by implementing retry logic in their code instead of surfacing them toousers as application errors.</span></span>

<span data-ttu-id="b4f5f-113">Se seu programa cliente estiver usando ADO.NET, seu programa é informado sobre o erro transitório Olá por throw saudação de um **SqlException**.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-113">If your client program is using ADO.NET, your program is told about hello transient error by hello throw of an **SqlException**.</span></span> <span data-ttu-id="b4f5f-114">Olá **número** propriedade pode ser comparada com a lista de saudação de erros transitórios superior de saudação do tópico Olá: [códigos de erro SQL para aplicativos de cliente do banco de dados SQL](sql-database-develop-error-messages.md).</span><span class="sxs-lookup"><span data-stu-id="b4f5f-114">hello **Number** property can be compared against hello list of transient errors near hello top of hello topic: [SQL error codes for SQL Database client applications](sql-database-develop-error-messages.md).</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="b4f5f-115">Conexão versus comando</span><span class="sxs-lookup"><span data-stu-id="b4f5f-115">Connection versus command</span></span>
<span data-ttu-id="b4f5f-116">Você repetir a conexão de SQL hello ou selecioná-lo novamente, dependendo do seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="b4f5f-116">You'll retry hello SQL connection or establish it again, depending on hello following:</span></span>

* <span data-ttu-id="b4f5f-117">**Um erro transitório ocorre durante uma tentativa de conexão**: conexão Olá deverá ser repetida após o atraso de alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-117">**A transient error occurs during a connection try**: hello connection should be retried after delaying for several seconds.</span></span>
* <span data-ttu-id="b4f5f-118">**Um erro transitório ocorre durante um comando de consulta SQL**: comando Olá não deve ser repetido imediatamente.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-118">**A transient error occurs during a SQL query command**: hello command should not be immediately retried.</span></span> <span data-ttu-id="b4f5f-119">Em vez disso, após um atraso, conexão Olá deve ser recentemente estabelecida.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-119">Instead, after a delay, hello connection should be freshly established.</span></span> <span data-ttu-id="b4f5f-120">Comando Olá pode ser tentada novamente.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-120">Then hello command can be retried.</span></span>

<a id="j-retry-logic-transient-faults" name="j-retry-logic-transient-faults"></a>

### <a name="retry-logic-for-transient-errors"></a><span data-ttu-id="b4f5f-121">Lógica de repetição para erros transitórios</span><span class="sxs-lookup"><span data-stu-id="b4f5f-121">Retry logic for transient errors</span></span>
<span data-ttu-id="b4f5f-122">Os programas cliente que ocasionalmente encontram um erro transitório são mais eficientes quando contêm lógica de repetição.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-122">Client programs that occasionally encounter a transient error are more robust when they contain retry logic.</span></span>

<span data-ttu-id="b4f5f-123">Quando seu programa se comunica com o banco de dados do SQL Azure por meio de um middleware de terceiros 3ª, consulte com o fornecedor de saudação se Olá middleware contém a lógica de repetição para erros transitórios.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-123">When your program communicates with Azure SQL Database through a 3rd party middleware, inquire with hello vendor whether hello middleware contains retry logic for transient errors.</span></span>

<a id="principles-for-retry" name="principles-for-retry"></a>

#### <a name="principles-for-retry"></a><span data-ttu-id="b4f5f-124">Princípios de repetição</span><span class="sxs-lookup"><span data-stu-id="b4f5f-124">Principles for retry</span></span>
* <span data-ttu-id="b4f5f-125">Tooopen uma tentativa de uma conexão deve ser repetida se o erro de saudação é temporário.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-125">An attempt tooopen a connection should be retried if hello error is transient.</span></span>
* <span data-ttu-id="b4f5f-126">Uma instrução SQL SELECT que falhe com um erro transitório não deverá ser repetida diretamente.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-126">A SQL SELECT statement that fails with a transient error should not be retried directly.</span></span>
  
  * <span data-ttu-id="b4f5f-127">Em vez disso, estabelecer uma nova conexão e tente novamente Olá SELECT.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-127">Instead, establish a fresh connection, and then retry hello SELECT.</span></span>
* <span data-ttu-id="b4f5f-128">Quando uma instrução SQL UPDATE falhará com um erro transitório, uma nova conexão deve ser estabelecida antes Olá que nova tentativa de atualização.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-128">When a SQL UPDATE statement fails with a transient error, a fresh connection should be established before hello UPDATE is retried.</span></span>
  
  * <span data-ttu-id="b4f5f-129">lógica de repetição Olá deve garantir que transação de banco de dados inteiro Olá concluída ou transação Olá inteira é revertida.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-129">hello retry logic must ensure that either hello entire database transaction completed, or that hello entire transaction is rolled back.</span></span>

#### <a name="other-considerations-for-retry"></a><span data-ttu-id="b4f5f-130">Outras considerações sobre tentativas de repetição</span><span class="sxs-lookup"><span data-stu-id="b4f5f-130">Other considerations for retry</span></span>
* <span data-ttu-id="b4f5f-131">Um arquivo em lotes que é iniciado automaticamente depois do horário comercial e que será concluída antes da manhã, pode ter toovery paciente com tempo intervalos de tempo entre as tentativas de repetição.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-131">A batch program that is automatically started after work hours, and which will complete before morning, can afford toovery patient with long time intervals between its retry attempts.</span></span>
* <span data-ttu-id="b4f5f-132">Um programa de interface do usuário deve conta para Olá tendência humana toogive após uma espera longa demais.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-132">A user interface program should account for hello human tendency toogive up after too long a wait.</span></span>
  
  * <span data-ttu-id="b4f5f-133">No entanto, solução de saudação não deve ser tooretry em alguns segundos, porque essa política pode sobrecarregar o sistema Olá com solicitações.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-133">However, hello solution must not be tooretry every few seconds, because that policy can flood hello system with requests.</span></span>

#### <a name="interval-increase-between-retries"></a><span data-ttu-id="b4f5f-134">Aumento do intervalo entre tentativas de repetição</span><span class="sxs-lookup"><span data-stu-id="b4f5f-134">Interval increase between retries</span></span>
<span data-ttu-id="b4f5f-135">É recomendável que você aguarde 5 segundos antes de sua primeira tentativa.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-135">We recommend that you delay for 5 seconds before your first retry.</span></span> <span data-ttu-id="b4f5f-136">Repetir após um intervalo menor do que 5 segundos corre o risco de serviço de nuvem Olá imenso.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-136">Retrying after a delay shorter than 5 seconds risks overwhelming hello cloud service.</span></span> <span data-ttu-id="b4f5f-137">Para cada repetição subsequente atraso Olá deve crescer exponencialmente, tooa máximo de 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-137">For each subsequent retry hello delay should grow exponentially, up tooa maximum of 60 seconds.</span></span>

<span data-ttu-id="b4f5f-138">Uma discussão de saudação *período de bloqueio* para clientes que usam o ADO.NET está disponível em [Pooling de Conexão do SQL Server (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4f5f-138">A discussion of hello *blocking period* for clients that use ADO.NET is available in [SQL Server Connection Pooling (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span></span>

<span data-ttu-id="b4f5f-139">Você também poderá tooset um número máximo de tentativas antes de programa hello se encerra.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-139">You might also want tooset a maximum number of retries before hello program self-terminates.</span></span>

#### <a name="code-samples-with-retry-logic"></a><span data-ttu-id="b4f5f-140">Exemplos de código com lógica de repetição</span><span class="sxs-lookup"><span data-stu-id="b4f5f-140">Code samples with retry logic</span></span>
<span data-ttu-id="b4f5f-141">Os exemplos de código com lógica de repetição, em uma variedade de linguagens de programação, estão disponíveis em:</span><span class="sxs-lookup"><span data-stu-id="b4f5f-141">Code samples with retry logic, in a variety of programming languages, are available at:</span></span>

* [<span data-ttu-id="b4f5f-142">Bibliotecas de conexão para Banco de Dados SQL e SQL Server</span><span class="sxs-lookup"><span data-stu-id="b4f5f-142">Connection libraries for SQL Database and SQL Server</span></span>](sql-database-libraries.md)

<a id="k-test-retry-logic" name="k-test-retry-logic"></a>

#### <a name="test-your-retry-logic"></a><span data-ttu-id="b4f5f-143">Testar sua lógica de repetição</span><span class="sxs-lookup"><span data-stu-id="b4f5f-143">Test your retry logic</span></span>
<span data-ttu-id="b4f5f-144">tootest sua lógica de repetição, você deve simular ou causar um erro que pode ser corrigido enquanto seu programa ainda está em execução.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-144">tootest your retry logic, you must simulate or cause an error than can be corrected while your program is still running.</span></span>

##### <a name="test-by-disconnecting-from-hello-network"></a><span data-ttu-id="b4f5f-145">Teste se desconectar da rede Olá</span><span class="sxs-lookup"><span data-stu-id="b4f5f-145">Test by disconnecting from hello network</span></span>
<span data-ttu-id="b4f5f-146">Uma maneira que você pode testar sua lógica de repetição é toodisconnect computador cliente da saudação de rede durante execução do programa de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-146">One way you can test your retry logic is toodisconnect your client computer from hello network while hello program is running.</span></span> <span data-ttu-id="b4f5f-147">Erro de saudação será:</span><span class="sxs-lookup"><span data-stu-id="b4f5f-147">hello error will be:</span></span>

* <span data-ttu-id="b4f5f-148">**SqlException.Number** = 11001</span><span class="sxs-lookup"><span data-stu-id="b4f5f-148">**SqlException.Number** = 11001</span></span>
* <span data-ttu-id="b4f5f-149">Mensagem: "Este host não é conhecido"</span><span class="sxs-lookup"><span data-stu-id="b4f5f-149">Message: "No such host is known"</span></span>

<span data-ttu-id="b4f5f-150">Como parte da saudação primeiro tentativa de repetição, seu programa pode corrigir erros de ortografia hello e, em seguida, tente tooconnect.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-150">As part of hello first retry attempt, your program can correct hello misspelling, and then attempt tooconnect.</span></span>

<span data-ttu-id="b4f5f-151">toomake nesse prático, você desconecte o computador da rede Olá antes de iniciar o programa.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-151">toomake this practical, you unplug your computer from hello network before you start your program.</span></span> <span data-ttu-id="b4f5f-152">Em seguida, seu programa reconhece um parâmetro de tempo de execução que faz com que o programa hello:</span><span class="sxs-lookup"><span data-stu-id="b4f5f-152">Then your program recognizes a run time parameter that causes hello program to:</span></span>

1. <span data-ttu-id="b4f5f-153">Adicione temporariamente 11001 lista tooits de erros tooconsider como transitório.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-153">Temporarily add 11001 tooits list of errors tooconsider as transient.</span></span>
2. <span data-ttu-id="b4f5f-154">Tente fazer sua primeira conexão como de costume.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-154">Attempt its first connection as usual.</span></span>
3. <span data-ttu-id="b4f5f-155">Depois que o erro Olá é capturado, remova 11001 da lista de hello.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-155">After hello error is caught, remove 11001 from hello list.</span></span>
4. <span data-ttu-id="b4f5f-156">Exiba uma mensagem informando Olá usuário tooplug Olá computador em rede hello.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-156">Display a message telling hello user tooplug hello computer into hello network.</span></span>
   * <span data-ttu-id="b4f5f-157">Pausar a execução ainda mais usando o hello **ReadLine** método ou uma caixa de diálogo com um botão Okey.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-157">Pause further execution by using either hello **Console.ReadLine** method or a dialog with an OK button.</span></span> <span data-ttu-id="b4f5f-158">usuário Olá pressiona a tecla de Enter de saudação depois que o computador Olá conectado em rede hello.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-158">hello user presses hello Enter key after hello computer plugged into hello network.</span></span>
5. <span data-ttu-id="b4f5f-159">Tente novamente tooconnect, esperando sucesso.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-159">Attempt again tooconnect, expecting success.</span></span>

##### <a name="test-by-misspelling-hello-database-name-when-connecting"></a><span data-ttu-id="b4f5f-160">Ao conectar-se de teste por nome de banco de dados de saudação do erro de ortografia</span><span class="sxs-lookup"><span data-stu-id="b4f5f-160">Test by misspelling hello database name when connecting</span></span>
<span data-ttu-id="b4f5f-161">Seu programa pode propositadamente errar nome de usuário de saudação antes da primeira tentativa de conexão hello.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-161">Your program can purposely misspell hello user name before hello first connection attempt.</span></span> <span data-ttu-id="b4f5f-162">Erro de saudação será:</span><span class="sxs-lookup"><span data-stu-id="b4f5f-162">hello error will be:</span></span>

* <span data-ttu-id="b4f5f-163">**SqlException.Number** = 18456</span><span class="sxs-lookup"><span data-stu-id="b4f5f-163">**SqlException.Number** = 18456</span></span>
* <span data-ttu-id="b4f5f-164">Mensagem: "Falha de logon para o usuário 'WRONG_MyUserName'."</span><span class="sxs-lookup"><span data-stu-id="b4f5f-164">Message: "Login failed for user 'WRONG_MyUserName'."</span></span>

<span data-ttu-id="b4f5f-165">Como parte da saudação primeiro tentativa de repetição, seu programa pode corrigir erros de ortografia hello e, em seguida, tente tooconnect.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-165">As part of hello first retry attempt, your program can correct hello misspelling, and then attempt tooconnect.</span></span>

<span data-ttu-id="b4f5f-166">toomake nesse prático, seu programa pode reconhecer um parâmetro de tempo de execução que faz com que o programa hello:</span><span class="sxs-lookup"><span data-stu-id="b4f5f-166">toomake this practical, your program could recognize a run time parameter that causes hello program to:</span></span>

1. <span data-ttu-id="b4f5f-167">Adicione temporariamente 18456 lista tooits de erros tooconsider como transitório.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-167">Temporarily add 18456 tooits list of errors tooconsider as transient.</span></span>
2. <span data-ttu-id="b4f5f-168">Propositadamente Adicione nome de usuário toohello 'WRONG_'.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-168">Purposely add 'WRONG_' toohello user name.</span></span>
3. <span data-ttu-id="b4f5f-169">Depois que o erro Olá é capturado, remova 18456 da lista de hello.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-169">After hello error is caught, remove 18456 from hello list.</span></span>
4. <span data-ttu-id="b4f5f-170">Remova 'WRONG_' hello do nome do usuário.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-170">Remove 'WRONG_' from hello user name.</span></span>
5. <span data-ttu-id="b4f5f-171">Tente novamente tooconnect, esperando sucesso.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-171">Attempt again tooconnect, expecting success.</span></span>

<a id="net-sqlconnection-parameters-for-connection-retry" name="net-sqlconnection-parameters-for-connection-retry"></a>

### <a name="net-sqlconnection-parameters-for-connection-retry"></a><span data-ttu-id="b4f5f-172">Parâmetros SqlConnection .NET para repetição de conexão</span><span class="sxs-lookup"><span data-stu-id="b4f5f-172">.NET SqlConnection parameters for connection retry</span></span>
<span data-ttu-id="b4f5f-173">Se seu programa cliente se conecta a tootooAzure banco de dados SQL usando a classe do .NET Framework Olá **SqlConnection**, você deve usar o .NET 4.6.1 ou posterior (ou .NET Core) para que você pode aproveitar o recurso de repetição de conexão.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-173">If your client program connects tootooAzure SQL Database by using hello .NET Framework class **System.Data.SqlClient.SqlConnection**, you should use .NET 4.6.1 or later (or .NET Core) so you can leverage its connection retry feature.</span></span> <span data-ttu-id="b4f5f-174">Detalhes do recurso Olá [aqui](http://go.microsoft.com/fwlink/?linkid=393996).</span><span class="sxs-lookup"><span data-stu-id="b4f5f-174">Details of hello feature are [here](http://go.microsoft.com/fwlink/?linkid=393996).</span></span>

<!--
2015-11-30, FwLink 393996 points toodn632678.aspx, which links tooa downloadable .docx related tooSqlClient and SQL Server 2014.
-->


<span data-ttu-id="b4f5f-175">Quando você cria Olá [cadeia de caracteres de conexão](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) para sua **SqlConnection** do objeto, você deve coordenar valores hello entre Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4f5f-175">When you build hello [connection string](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) for your **SqlConnection** object, you should coordinate hello values among hello following parameters:</span></span>

* <span data-ttu-id="b4f5f-176">ConnectRetryCount &nbsp;&nbsp;*(o Padrão é 1. O intervalo vai de 0 a 255).*</span><span class="sxs-lookup"><span data-stu-id="b4f5f-176">ConnectRetryCount &nbsp;&nbsp;*(Default is 1. Range is 0 through 255.)*</span></span>
* <span data-ttu-id="b4f5f-177">ConnectRetryInterval &nbsp;&nbsp;*(o Padrão é 1 segundo. O intervalo vai de 1 a 60).*</span><span class="sxs-lookup"><span data-stu-id="b4f5f-177">ConnectRetryInterval &nbsp;&nbsp;*(Default is 1 second. Range is 1 through 60.)*</span></span>
* <span data-ttu-id="b4f5f-178">Connection Timeout &nbsp;&nbsp;*(o Padrão é 15 segundos. O intervalo vai de 0 a 2147483647)*</span><span class="sxs-lookup"><span data-stu-id="b4f5f-178">Connection Timeout &nbsp;&nbsp;*(Default is 15 seconds. Range is 0 through 2147483647)*</span></span>

<span data-ttu-id="b4f5f-179">Especificamente, os valores escolhidos devem ter Olá true igualdade a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4f5f-179">Specifically, your chosen values should make hello following equality true:</span></span>

* <span data-ttu-id="b4f5f-180">Connection Timeout = ConnectRetryCount * ConnectionRetryInterval</span><span class="sxs-lookup"><span data-stu-id="b4f5f-180">Connection Timeout = ConnectRetryCount * ConnectionRetryInterval</span></span>

<span data-ttu-id="b4f5f-181">Por exemplo, se hello contar = 3 e intervalo = 10 segundos, um tempo limite de somente 29 segundos não bastante daria sistema Olá tempo suficiente para sua repetição 3º e final na conexão: 29 < 3 * 10.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-181">For example, if hello count = 3, and interval = 10 seconds, a timeout of only 29 seconds would not quite give hello system enough time for its 3rd and final retry at connecting: 29 < 3 * 10.</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="b4f5f-182">Conexão versus comando</span><span class="sxs-lookup"><span data-stu-id="b4f5f-182">Connection versus command</span></span>
<span data-ttu-id="b4f5f-183">Olá **ConnectRetryCount** e **ConnectRetryInterval** parâmetros permitem que seu **SqlConnection** Olá de repetição de objeto a operação de conexão sem informando ou incomodar seu programa, como retornar o programa de controle de tooyour.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-183">hello **ConnectRetryCount** and **ConnectRetryInterval** parameters let your **SqlConnection** object retry hello connect operation without telling or bothering your program, such as returning control tooyour program.</span></span> <span data-ttu-id="b4f5f-184">tentativas de saudação podem ocorrer em Olá situações a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4f5f-184">hello retries can occur in hello following situations:</span></span>

* <span data-ttu-id="b4f5f-185">Chamada ao método mySqlConnection.Open</span><span class="sxs-lookup"><span data-stu-id="b4f5f-185">mySqlConnection.Open method call</span></span>
* <span data-ttu-id="b4f5f-186">Chamada ao método mySqlConnection.Execute</span><span class="sxs-lookup"><span data-stu-id="b4f5f-186">mySqlConnection.Execute method call</span></span>

<span data-ttu-id="b4f5f-187">Mas há uma sutileza aqui.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-187">There is a subtlety.</span></span> <span data-ttu-id="b4f5f-188">Se ocorrer um erro transitório enquanto seu *consulta* está sendo executado, o **SqlConnection** não Olá de repetir a operação de conexão, e ele certamente não repita a consulta do objeto.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-188">If a transient error occurs while your *query* is being executed, your **SqlConnection** object does not retry hello connect operation, and it certainly does not retry your query.</span></span> <span data-ttu-id="b4f5f-189">No entanto, **SqlConnection** rapidamente verificações Olá conexão antes de enviar sua consulta para execução.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-189">However, **SqlConnection** very quickly checks hello connection before sending your query for execution.</span></span> <span data-ttu-id="b4f5f-190">Se a verificação rápida Olá detectar um problema de conexão, **SqlConnection** Olá repetições a operação de conexão.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-190">If hello quick check detects a connection problem, **SqlConnection** retries hello connect operation.</span></span> <span data-ttu-id="b4f5f-191">Se a repetição de saudação for bem-sucedida, você consulta é enviada para execução.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-191">If hello retry succeeds, you query is sent for execution.</span></span>

#### <a name="should-connectretrycount-be-combined-with-application-retry-logic"></a><span data-ttu-id="b4f5f-192">ConnectRetryCount deve ser combinada à lógica de repetição de aplicativo?</span><span class="sxs-lookup"><span data-stu-id="b4f5f-192">Should ConnectRetryCount be combined with application retry logic?</span></span>
<span data-ttu-id="b4f5f-193">Suponha que seu aplicativo tenha lógica de repetição personalizada robusta.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-193">Suppose your application has robust custom retry logic.</span></span> <span data-ttu-id="b4f5f-194">Ele pode repetir Olá 4 vezes a operação de conexão.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-194">It might retry hello connect operation 4 times.</span></span> <span data-ttu-id="b4f5f-195">Se você adicionar **ConnectRetryInterval** e **ConnectRetryCount** = cadeia de caracteres de conexão de tooyour 3, aumenta a too4 de contagem de repetição hello * 3 = 12 tentativas.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-195">If you add **ConnectRetryInterval** and **ConnectRetryCount** =3 tooyour connection string, you will increase hello retry count too4 * 3 = 12 retries.</span></span> <span data-ttu-id="b4f5f-196">Talvez você não queira um número tão alto de repetições.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-196">You might not intend such a high number of retries.</span></span>

<a id="a-connection-connection-string" name="a-connection-connection-string"></a>

## <a name="connections-tooazure-sql-database"></a><span data-ttu-id="b4f5f-197">Conexões tooAzure banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="b4f5f-197">Connections tooAzure SQL Database</span></span>
<a id="c-connection-string" name="c-connection-string"></a>

### <a name="connection-connection-string"></a><span data-ttu-id="b4f5f-198">Conexão: cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="b4f5f-198">Connection: Connection string</span></span>
<span data-ttu-id="b4f5f-199">cadeia de caracteres de conexão do Hello necessária para conectar-se tooAzure banco de dados SQL é ligeiramente diferente da cadeia de caracteres de saudação para conectar-se tooMicrosoft do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-199">hello connection string necessary for connecting tooAzure SQL Database is slightly different from hello string for connecting tooMicrosoft SQL Server.</span></span> <span data-ttu-id="b4f5f-200">Você pode copiar cadeia de caracteres de conexão de saudação do banco de dados de saudação [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b4f5f-200">You can copy hello connection string for your database from hello [Azure portal](https://portal.azure.com/).</span></span>

[!INCLUDE [sql-database-include-connection-string-20-portalshots](../../includes/sql-database-include-connection-string-20-portalshots.md)]

<a id="b-connection-ip-address" name="b-connection-ip-address"></a>

### <a name="connection-ip-address"></a><span data-ttu-id="b4f5f-201">Conexão: endereço IP</span><span class="sxs-lookup"><span data-stu-id="b4f5f-201">Connection: IP address</span></span>
<span data-ttu-id="b4f5f-202">Você deve configurar a saudação banco de dados SQL server tooaccept comunicação do endereço IP de saudação do computador de saudação que hospeda o programa cliente.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-202">You must configure hello SQL Database server tooaccept communication from hello IP address of hello computer that hosts your client program.</span></span> <span data-ttu-id="b4f5f-203">Você pode fazer isso editando as configurações de firewall Olá por meio de saudação [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b4f5f-203">You do this by editing hello firewall settings through hello [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="b4f5f-204">Se você esquecer o endereço IP tooconfigure hello, seu programa falhará com uma mensagem de erro úteis que declara o endereço IP hello necessário.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-204">If you forget tooconfigure hello IP address, your program will fail with a handy error message that states hello necessary IP address.</span></span>

[!INCLUDE [sql-database-include-ip-address-22-portal](../../includes/sql-database-include-ip-address-22-v12portal.md)]

<span data-ttu-id="b4f5f-205">Para saber mais, consulte [Como definir as configurações de firewall no Banco de Dados SQL](sql-database-configure-firewall-settings.md)</span><span class="sxs-lookup"><span data-stu-id="b4f5f-205">For more information, see: [How to: Configure firewall settings on SQL Database](sql-database-configure-firewall-settings.md)</span></span>

<a id="c-connection-ports" name="c-connection-ports"></a>

### <a name="connection-ports"></a><span data-ttu-id="b4f5f-206">Conexão: portas</span><span class="sxs-lookup"><span data-stu-id="b4f5f-206">Connection: Ports</span></span>
<span data-ttu-id="b4f5f-207">Normalmente, você só precisa tooensure que a porta 1433 está aberta para comunicação de saída, no computador de saudação que hospeda a você o programa cliente.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-207">Typically you only need tooensure that port 1433 is open for outbound communication, on hello computer that hosts you client program.</span></span>

<span data-ttu-id="b4f5f-208">Por exemplo, quando o programa cliente está hospedado em um computador com Windows, Olá Firewall do Windows no host Olá permite que você tooopen a porta 1433:</span><span class="sxs-lookup"><span data-stu-id="b4f5f-208">For example, when your client program is hosted on a Windows computer, hello Windows Firewall on hello host enables you tooopen port 1433:</span></span>

1. <span data-ttu-id="b4f5f-209">Abrir o painel de controle de saudação</span><span class="sxs-lookup"><span data-stu-id="b4f5f-209">Open hello Control Panel</span></span>
2. <span data-ttu-id="b4f5f-210">&gt; Todos os Itens do Painel de Controle</span><span class="sxs-lookup"><span data-stu-id="b4f5f-210">&gt; All Control Panel Items</span></span>
3. <span data-ttu-id="b4f5f-211">&gt; Firewall do Windows</span><span class="sxs-lookup"><span data-stu-id="b4f5f-211">&gt; Windows Firewall</span></span>
4. <span data-ttu-id="b4f5f-212">&gt; Configurações Avançadas</span><span class="sxs-lookup"><span data-stu-id="b4f5f-212">&gt; Advanced Settings</span></span>
5. <span data-ttu-id="b4f5f-213">&gt; Regras de Saída</span><span class="sxs-lookup"><span data-stu-id="b4f5f-213">&gt; Outbound Rules</span></span>
6. <span data-ttu-id="b4f5f-214">&gt; Ações</span><span class="sxs-lookup"><span data-stu-id="b4f5f-214">&gt; Actions</span></span>
7. <span data-ttu-id="b4f5f-215">&gt; Nova Regra</span><span class="sxs-lookup"><span data-stu-id="b4f5f-215">&gt; New Rule</span></span>

<span data-ttu-id="b4f5f-216">Se seu programa cliente estiver hospedado em uma máquina virtual do Azure (VM), você deverá ler:</span><span class="sxs-lookup"><span data-stu-id="b4f5f-216">If your client program is hosted on an Azure virtual machine (VM), you should read:</span></span><br/><span data-ttu-id="b4f5f-217">[Portas acima da 1433 para o ADO.NET 4.5 e o Banco de Dados SQL](sql-database-develop-direct-route-ports-adonet-v12.md).</span><span class="sxs-lookup"><span data-stu-id="b4f5f-217">[Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>

<span data-ttu-id="b4f5f-218">Para saber mais sobre a configuração de portas e de endereços IP, consulte: [Firewall do Banco de Dados SQL do Azure](sql-database-firewall-configure.md)</span><span class="sxs-lookup"><span data-stu-id="b4f5f-218">For background information about cofiguration of ports and IP address, see: [Azure SQL Database firewall](sql-database-firewall-configure.md)</span></span>

<a id="d-connection-ado-net-4-5" name="d-connection-ado-net-4-5"></a>

### <a name="connection-adonet-461"></a><span data-ttu-id="b4f5f-219">Conexão: ADO.NET 4.6.1</span><span class="sxs-lookup"><span data-stu-id="b4f5f-219">Connection: ADO.NET 4.6.1</span></span>
<span data-ttu-id="b4f5f-220">Se seu programa usa as classes ADO.NET como **SqlConnection** tooconnect tooAzure banco de dados SQL, é recomendável que você use o .NET Framework versão 4.6.1 ou superior.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-220">If your program uses ADO.NET classes like **System.Data.SqlClient.SqlConnection** tooconnect tooAzure SQL Database, we recommend that you use .NET Framework version 4.6.1 or higher.</span></span>

<span data-ttu-id="b4f5f-221">ADO.NET 4.6.1:</span><span class="sxs-lookup"><span data-stu-id="b4f5f-221">ADO.NET 4.6.1:</span></span>

* <span data-ttu-id="b4f5f-222">Para o banco de dados SQL Azure, há maior confiabilidade quando você abrir uma conexão usando Olá **SqlConnection. Open** método.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-222">For Azure SQL Database, there is improved reliability when you open a connection by using hello **SqlConnection.Open** method.</span></span> <span data-ttu-id="b4f5f-223">Olá **abrir** método agora incorpora melhor esforço repetição mecanismos em falhas de tootransient de resposta, para determinados erros dentro do período de tempo limite de Conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-223">hello **Open** method now incorporates best effort retry mechanisms in response tootransient faults, for certain errors within hello Connection Timeout period.</span></span>
* <span data-ttu-id="b4f5f-224">Dá suporte ao pool de conexões.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-224">Supports connection pooling.</span></span> <span data-ttu-id="b4f5f-225">Isso inclui uma verificação eficiente que Olá conexão objeto assim que o programa está funcionando.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-225">This includes an efficient verification that hello connection object it gives your program is functioning.</span></span>

<span data-ttu-id="b4f5f-226">Quando você usa um objeto de conexão de um pool de conexão, é recomendável que seu programa temporariamente fechar conexão hello quando usá-lo não imediatamente.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-226">When you use a connection object from a connection pool, we recommend that your program temporarily close hello connection when not immediately using it.</span></span> <span data-ttu-id="b4f5f-227">Abrir novamente uma conexão não é caro Olá maneira criando uma nova conexão é.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-227">Re-opening a connection is not expensive hello way creating a new connection is.</span></span>

<span data-ttu-id="b4f5f-228">Se você estiver usando o ADO.NET 4.0 ou anterior, é recomendável que você atualize toohello ADO.NET mais recente.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-228">If you are using ADO.NET 4.0 or earlier, we recommend that you upgrade toohello latest ADO.NET.</span></span>

* <span data-ttu-id="b4f5f-229">Desde novembro de 2015, você pode [baixar o ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4f5f-229">As of November 2015, you can [download ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).</span></span>

<a id="e-diagnostics-test-utilities-connect" name="e-diagnostics-test-utilities-connect"></a>

## <a name="diagnostics"></a><span data-ttu-id="b4f5f-230">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="b4f5f-230">Diagnostics</span></span>
<a id="d-test-whether-utilities-can-connect" name="d-test-whether-utilities-can-connect"></a>

### <a name="diagnostics-test-whether-utilities-can-connect"></a><span data-ttu-id="b4f5f-231">Diagnóstico: testar se os utilitários podem se conectar</span><span class="sxs-lookup"><span data-stu-id="b4f5f-231">Diagnostics: Test whether utilities can connect</span></span>
<span data-ttu-id="b4f5f-232">Se o programa estiver falhando tooconnect tooAzure banco de dados SQL, uma opção de diagnóstica é tooconnect tootry com um programa utilitário.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-232">If your program is failing tooconnect tooAzure SQL Database, one diagnostic option is tootry tooconnect with a utility program.</span></span> <span data-ttu-id="b4f5f-233">Idealmente utilitário Olá conectaria usando Olá mesma biblioteca que usa o programa.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-233">Ideally hello utility would connect by using hello same library that your program uses.</span></span>

<span data-ttu-id="b4f5f-234">Em qualquer computador Windows, você pode experimentar estes utilitários:</span><span class="sxs-lookup"><span data-stu-id="b4f5f-234">On any Windows computer, you can try these utilities:</span></span>

* <span data-ttu-id="b4f5f-235">SQL Server Management Studio (ssms.exe), que se conecta usando ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-235">SQL Server Management Studio (ssms.exe), which connects by using ADO.NET.</span></span>
* <span data-ttu-id="b4f5f-236">sqlcmd.exe, que se conecta usando [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4f5f-236">sqlcmd.exe, which connects by using [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span></span>

<span data-ttu-id="b4f5f-237">Uma vez conectado, teste se uma consulta SQL SELECT curta funciona.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-237">Once connected, test whether a short SQL SELECT query works.</span></span>

<a id="f-diagnostics-check-open-ports" name="f-diagnostics-check-open-ports"></a>

### <a name="diagnostics-check-hello-open-ports"></a><span data-ttu-id="b4f5f-238">Diagnóstico: Portas abertas de saudação seleção</span><span class="sxs-lookup"><span data-stu-id="b4f5f-238">Diagnostics: Check hello open ports</span></span>
<span data-ttu-id="b4f5f-239">Suponha que você suspeita de que as tentativas de conexão estão falhando devido a problemas de tooport.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-239">Suppose you suspect that connection attempts are failing due tooport issues.</span></span> <span data-ttu-id="b4f5f-240">Em seu computador, você pode executar um utilitário que relatórios sobre configurações de porta de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-240">On your computer you can run a utility that reports on hello port configurations.</span></span>

<span data-ttu-id="b4f5f-241">No Linux Olá utilitários a seguir podem ser úteis:</span><span class="sxs-lookup"><span data-stu-id="b4f5f-241">On Linux hello following utilities might be helpful:</span></span>

* `netstat -nap`
* `nmap -sS -O 127.0.0.1`
  * <span data-ttu-id="b4f5f-242">(Alterar toobe de valor do exemplo hello seu endereço IP.)</span><span class="sxs-lookup"><span data-stu-id="b4f5f-242">(Change hello example value toobe your IP address.)</span></span>

<span data-ttu-id="b4f5f-243">No Windows hello [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) utilitário pode ser útil.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-243">On Windows hello [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) utility might be helpful.</span></span> <span data-ttu-id="b4f5f-244">Aqui está uma execução de exemplo que consultados situação de porta de saudação em um servidor de banco de dados SQL, e que foi executado em um computador laptop:</span><span class="sxs-lookup"><span data-stu-id="b4f5f-244">Here is an example execution that queried hello port situation on an Azure SQL Database server, and which was run on a laptop computer:</span></span>

```
[C:\Users\johndoe\]
>> portqry.exe -n johndoesvr9.database.windows.net -p tcp -e 1433

Querying target system called:
 johndoesvr9.database.windows.net

Attempting tooresolve name tooIP address...
Name resolved too23.100.117.95

querying...
TCP port 1433 (ms-sql-s service): LISTENING

[C:\Users\johndoe\]
>>
```


<a id="g-diagnostics-log-your-errors" name="g-diagnostics-log-your-errors"></a>

### <a name="diagnostics-log-your-errors"></a><span data-ttu-id="b4f5f-245">Diagnóstico: registrar seus erros em log</span><span class="sxs-lookup"><span data-stu-id="b4f5f-245">Diagnostics: Log your errors</span></span>
<span data-ttu-id="b4f5f-246">Às vezes, um problema intermitente é mais bem diagnosticado pela detecção de um padrão geral ao longo de dias ou de semanas.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-246">An intermittent problem is sometimes best diagnosed by detection of a general pattern over days or weeks.</span></span>

<span data-ttu-id="b4f5f-247">O cliente pode auxiliar em um diagnóstico ao registrar em log todos os erros encontrados.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-247">Your client can assist in a diagnosis by logging all errors it encounters.</span></span> <span data-ttu-id="b4f5f-248">Pode ser capaz de toocorrelate entradas de log de Olá com dados de erro que o banco de dados do Azure SQL registra próprio internamente.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-248">You might be able toocorrelate hello log entries with error data that Azure SQL Database logs itself internally.</span></span>

<span data-ttu-id="b4f5f-249">Enterprise Library 6 (EntLib60) oferece tooassist de classes .NET gerenciado com o log:</span><span class="sxs-lookup"><span data-stu-id="b4f5f-249">Enterprise Library 6 (EntLib60) offers .NET managed classes tooassist with logging:</span></span>

* [<span data-ttu-id="b4f5f-250">5 - como fácil como cair fora de um Log: usando Olá Logging Application Block</span><span class="sxs-lookup"><span data-stu-id="b4f5f-250">5 - As Easy As Falling Off a Log: Using hello Logging Application Block</span></span>](http://msdn.microsoft.com/library/dn440731.aspx)

<a id="h-diagnostics-examine-logs-errors" name="h-diagnostics-examine-logs-errors"></a>

### <a name="diagnostics-examine-system-logs-for-errors"></a><span data-ttu-id="b4f5f-251">Diagnóstico: examinar logs de erros do sistema</span><span class="sxs-lookup"><span data-stu-id="b4f5f-251">Diagnostics: Examine system logs for errors</span></span>
<span data-ttu-id="b4f5f-252">Aqui estão algumas instruções Transact-SQL SELECT que a consulta registra em log os erros e outras informações.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-252">Here are some Transact-SQL SELECT statements that query logs of error and other information.</span></span>

| <span data-ttu-id="b4f5f-253">Consulta de log</span><span class="sxs-lookup"><span data-stu-id="b4f5f-253">Query of log</span></span> | <span data-ttu-id="b4f5f-254">Descrição</span><span class="sxs-lookup"><span data-stu-id="b4f5f-254">Description</span></span> |
|:--- |:--- |
| `SELECT e.*`<br/>`FROM sys.event_log AS e`<br/>`WHERE e.database_name = 'myDbName'`<br/>`AND e.event_category = 'connectivity'`<br/>`AND 2 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, e.end_time, GetUtcDate())`<br/>`ORDER BY e.event_category,`<br/>&nbsp;&nbsp;`e.event_type, e.end_time;` |<span data-ttu-id="b4f5f-255">Olá [sys. event_log](http://msdn.microsoft.com/library/dn270018.aspx) exibição oferece informações sobre os eventos individuais, incluindo alguns que podem causar erros transitórios ou falhas de conectividade.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-255">hello [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) view offers information about individual events, including some that can cause transient errors or connectivity failures.</span></span><br/><br/><span data-ttu-id="b4f5f-256">Idealmente, você pode correlacionar Olá **start_time** ou **end_time** valores com informações sobre quando o programa cliente apresentar problemas.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-256">Ideally you can correlate hello **start_time** or **end_time** values with information about when your client program experienced problems.</span></span><br/><br/><span data-ttu-id="b4f5f-257">**Dica:** você deve se conectar toohello **mestre** de banco de dados toorun isso.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-257">**TIP:** You must connect toohello **master** database toorun this.</span></span> |
| `SELECT c.*`<br/>`FROM sys.database_connection_stats AS c`<br/>`WHERE c.database_name = 'myDbName'`<br/>`AND 24 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, c.end_time, GetUtcDate())`<br/>`ORDER BY c.end_time;` |<span data-ttu-id="b4f5f-258">Olá [sys. database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) exibição oferece contagens agregadas dos tipos de evento de diagnóstico adicional.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-258">hello [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) view offers aggregated counts of event types, for additional diagnostics.</span></span><br/><br/><span data-ttu-id="b4f5f-259">**Dica:** você deve se conectar toohello **mestre** de banco de dados toorun isso.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-259">**TIP:** You must connect toohello **master** database toorun this.</span></span> |

<a id="d-search-for-problem-events-in-the-sql-database-log" name="d-search-for-problem-events-in-the-sql-database-log"></a>

### <a name="diagnostics-search-for-problem-events-in-hello-sql-database-log"></a><span data-ttu-id="b4f5f-260">Diagnóstico: Pesquisa eventos de problema no log de banco de dados SQL de saudação</span><span class="sxs-lookup"><span data-stu-id="b4f5f-260">Diagnostics: Search for problem events in hello SQL Database log</span></span>
<span data-ttu-id="b4f5f-261">Você pode procurar entradas sobre problema eventos no log de saudação do banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-261">You can search for entries about problem events in hello log of Azure SQL Database.</span></span> <span data-ttu-id="b4f5f-262">Tente Olá após a instrução SELECT Transact-SQL em Olá **mestre** banco de dados:</span><span class="sxs-lookup"><span data-stu-id="b4f5f-262">Try hello following Transact-SQL SELECT statement in hello **master** database:</span></span>

```
SELECT
   object_name
  ,CAST(f.event_data as XML).value
      ('(/event/@timestamp)[1]', 'datetime2')                      AS [timestamp]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="error"]/value)[1]', 'int')             AS [error]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="state"]/value)[1]', 'int')             AS [state]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="is_success"]/value)[1]', 'bit')        AS [is_success]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="database_name"]/value)[1]', 'sysname') AS [database_name]
FROM
  sys.fn_xe_telemetry_blob_target_read_file('el', null, null, null) AS f
WHERE
  object_name != 'login_event'  -- Login events are numerous.
  and
  '2015-06-21' < CAST(f.event_data as XML).value
        ('(/event/@timestamp)[1]', 'datetime2')
ORDER BY
  [timestamp] DESC
;
```


#### <a name="a-few-returned-rows-from-sysfnxetelemetryblobtargetreadfile"></a><span data-ttu-id="b4f5f-263">Algumas linhas retornadas de sys.fn_xe_telemetry_blob_target_read_file</span><span class="sxs-lookup"><span data-stu-id="b4f5f-263">A few returned rows from sys.fn_xe_telemetry_blob_target_read_file</span></span>
<span data-ttu-id="b4f5f-264">A seguir, como seria a aparência de uma linha retornada.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-264">Next is what a returned row might look like.</span></span> <span data-ttu-id="b4f5f-265">valores nulos de saudação mostrados geralmente não são nulos em outras linhas.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-265">hello null values shown are often not null in other rows.</span></span>

```
object_name                   timestamp                    error  state  is_success  database_name

database_xml_deadlock_report  2015-10-16 20:28:01.0090000  NULL   NULL   NULL        AdventureWorks
```


<a id="l-enterprise-library-6" name="l-enterprise-library-6"></a>

## <a name="enterprise-library-6"></a><span data-ttu-id="b4f5f-266">Enterprise Library 6</span><span class="sxs-lookup"><span data-stu-id="b4f5f-266">Enterprise Library 6</span></span>
<span data-ttu-id="b4f5f-267">Enterprise Library 6 (EntLib60) é uma estrutura de classes .NET que ajuda a implementar robustos clientes dos serviços de nuvem, um dos quais é o serviço de banco de dados do Azure SQL hello.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-267">Enterprise Library 6 (EntLib60) is a framework of .NET classes that helps you implement robust clients of cloud services, one of which is hello Azure SQL Database service.</span></span> <span data-ttu-id="b4f5f-268">Você pode localizar a área de tooeach dedicado de tópicos no qual EntLib60 podem ajudá-lo visitando primeiro:</span><span class="sxs-lookup"><span data-stu-id="b4f5f-268">You can locate topics dedicated tooeach area in which EntLib60 can assist by first visiting:</span></span>

* [<span data-ttu-id="b4f5f-269">A Enterprise Library 6 – abril de 2013</span><span class="sxs-lookup"><span data-stu-id="b4f5f-269">Enterprise Library 6 - April 2013</span></span>](http://msdn.microsoft.com/library/dn169621%28v=pandp.60%29.aspx)

<span data-ttu-id="b4f5f-270">A lógica de repetição para tratar erros transitórios é uma área em que EntLib60 pode auxiliar:</span><span class="sxs-lookup"><span data-stu-id="b4f5f-270">Retry logic for handling transient errors is one area in which EntLib60 can assist:</span></span>

* [<span data-ttu-id="b4f5f-271">4 - perseverance, o segredo de todos os Triumphs: usando Olá Transient Fault Handling Application Block</span><span class="sxs-lookup"><span data-stu-id="b4f5f-271">4 - Perseverance, Secret of All Triumphs: Using hello Transient Fault Handling Application Block</span></span>](http://msdn.microsoft.com/library/dn440719%28v=pandp.60%29.aspx)

> [!NOTE]
> <span data-ttu-id="b4f5f-272">Olá código-fonte para a EntLib60 está disponível para o público [baixar](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span><span class="sxs-lookup"><span data-stu-id="b4f5f-272">hello source code for EntLib60 is available for public [download](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span></span> <span data-ttu-id="b4f5f-273">A Microsoft não tem nenhum recurso adicional de toomake planos tooEntLib de atualizações de manutenção ou atualizações.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-273">Microsoft has no plans toomake further feature updates or maintenance updates tooEntLib.</span></span>
> 
> 

<a id="entlib60-classes-for-transient-errors-and-retry" name="entlib60-classes-for-transient-errors-and-retry"></a>

### <a name="entlib60-classes-for-transient-errors-and-retry"></a><span data-ttu-id="b4f5f-274">Classes do EntLib60 para erros transitórios e tentativas de repetição</span><span class="sxs-lookup"><span data-stu-id="b4f5f-274">EntLib60 classes for transient errors and retry</span></span>
<span data-ttu-id="b4f5f-275">Olá EntLib60 classes a seguir é particularmente úteis para lógica de repetição.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-275">hello following EntLib60 classes are particularly useful for retry logic.</span></span> <span data-ttu-id="b4f5f-276">Todos eles estão na ou são posteriormente, Olá namespace **transientfaulthandling**:</span><span class="sxs-lookup"><span data-stu-id="b4f5f-276">All these  are in, or are further under, hello namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span></span>

<span data-ttu-id="b4f5f-277">*Olá namespace **transientfaulthandling**:*</span><span class="sxs-lookup"><span data-stu-id="b4f5f-277">*In hello namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span></span>

* <span data-ttu-id="b4f5f-278">**RetryPolicy** </span><span class="sxs-lookup"><span data-stu-id="b4f5f-278">**RetryPolicy** class</span></span>
  
  * <span data-ttu-id="b4f5f-279">**ExecuteAction** </span><span class="sxs-lookup"><span data-stu-id="b4f5f-279">**ExecuteAction** method</span></span>
* <span data-ttu-id="b4f5f-280">**ExponentialBackoff** </span><span class="sxs-lookup"><span data-stu-id="b4f5f-280">**ExponentialBackoff** class</span></span>
* <span data-ttu-id="b4f5f-281">**SqlDatabaseTransientErrorDetectionStrategy** </span><span class="sxs-lookup"><span data-stu-id="b4f5f-281">**SqlDatabaseTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="b4f5f-282">**ReliableSqlConnection** </span><span class="sxs-lookup"><span data-stu-id="b4f5f-282">**ReliableSqlConnection** class</span></span>
  
  * <span data-ttu-id="b4f5f-283">**ExecuteCommand** </span><span class="sxs-lookup"><span data-stu-id="b4f5f-283">**ExecuteCommand** method</span></span>

<span data-ttu-id="b4f5f-284">Olá namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span><span class="sxs-lookup"><span data-stu-id="b4f5f-284">In hello namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span></span>

* <span data-ttu-id="b4f5f-285">**AlwaysTransientErrorDetectionStrategy** </span><span class="sxs-lookup"><span data-stu-id="b4f5f-285">**AlwaysTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="b4f5f-286">**NeverTransientErrorDetectionStrategy** </span><span class="sxs-lookup"><span data-stu-id="b4f5f-286">**NeverTransientErrorDetectionStrategy** class</span></span>

<span data-ttu-id="b4f5f-287">Aqui estão os links tooinformation sobre o EntLib60:</span><span class="sxs-lookup"><span data-stu-id="b4f5f-287">Here are links tooinformation about EntLib60:</span></span>

* <span data-ttu-id="b4f5f-288">Livre [Download do livro: tooMicrosoft do guia do desenvolvedor Enterprise Library, 2ª edição](http://www.microsoft.com/download/details.aspx?id=41145)</span><span class="sxs-lookup"><span data-stu-id="b4f5f-288">Free [Book Download: Developer's Guide tooMicrosoft Enterprise Library, 2nd Edition](http://www.microsoft.com/download/details.aspx?id=41145)</span></span>
* <span data-ttu-id="b4f5f-289">Práticas recomendadas: [Diretrizes gerais para tentativas de repetição](../best-practices-retry-general.md) tem uma excelente discussão detalhada sobre lógica de repetição.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-289">Best practices: [Retry general guidance](../best-practices-retry-general.md) has an excellent in-depth discussion of retry logic.</span></span>
* <span data-ttu-id="b4f5f-290">Download NuGet de [Enterprise Library - bloqueio de aplicativos de manipulação de falhas transitórias 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span><span class="sxs-lookup"><span data-stu-id="b4f5f-290">NuGet download of [Enterprise Library - Transient Fault Handling application block 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span></span>

<a id="entlib60-the-logging-block" name="entlib60-the-logging-block"></a>

### <a name="entlib60-hello-logging-block"></a><span data-ttu-id="b4f5f-291">EntLib60: bloco de log de saudação</span><span class="sxs-lookup"><span data-stu-id="b4f5f-291">EntLib60: hello logging block</span></span>
* <span data-ttu-id="b4f5f-292">bloco de log Olá é uma solução altamente configurável e flexível que permite que você:</span><span class="sxs-lookup"><span data-stu-id="b4f5f-292">hello Logging block is a highly flexible and configurable solution that allows you to:</span></span>
  
  * <span data-ttu-id="b4f5f-293">Crie e armazene mensagens de log em uma grande variedade de locais.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-293">Create and store log messages in a wide variety of locations.</span></span>
  * <span data-ttu-id="b4f5f-294">Categorize e filtre as mensagens.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-294">Categorize and filter messages.</span></span>
  * <span data-ttu-id="b4f5f-295">Colete informações contextuais que sejam úteis para depuração e rastreamento, bem como para requisitos de auditoria e de log geral.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-295">Collect contextual information that is useful for debugging and tracing, as well as for auditing and general logging requirements.</span></span>
* <span data-ttu-id="b4f5f-296">bloco de log Olá abstrai Olá log funcionalidade do destino de log hello, para que o código do aplicativo hello seja consistente, independentemente do local hello e o tipo de armazenamento de log de destino hello.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-296">hello Logging block abstracts hello logging functionality from hello log destination so that hello application code is consistent, irrespective of hello location and type of hello target logging store.</span></span>

<span data-ttu-id="b4f5f-297">Para obter detalhes, consulte: [5 - como fácil como cair fora de um Log: usando Olá Logging Application Block](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="b4f5f-297">For details see: [5 - As Easy As Falling Off a Log: Using hello Logging Application Block](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span></span>

<a id="entlib60-istransient-method-source-code" name="entlib60-istransient-method-source-code"></a>

### <a name="entlib60-istransient-method-source-code"></a><span data-ttu-id="b4f5f-298">O EntLib60 é o código-fonte do método IsTransient</span><span class="sxs-lookup"><span data-stu-id="b4f5f-298">EntLib60 IsTransient method source code</span></span>
<span data-ttu-id="b4f5f-299">Em seguida, de saudação **SqlDatabaseTransientErrorDetectionStrategy** classe, é o código-fonte para Olá Olá c# **IsTransient** método.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-299">Next, from hello **SqlDatabaseTransientErrorDetectionStrategy** class, is hello C# source code for hello **IsTransient** method.</span></span> <span data-ttu-id="b4f5f-300">código-fonte Olá esclarece que os erros foram considerados toobe transitório e pena repetir, a partir de abril de 2013.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-300">hello source code clarifies which errors were considered toobe transient and worthy of retry, as of April 2013.</span></span>

<span data-ttu-id="b4f5f-301">Vários **//comment** linhas foram removidas da leitura de tooemphasize cópia.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-301">Numerous **//comment** lines have been removed from this copy tooemphasize readability.</span></span>

```
public bool IsTransient(Exception ex)
{
  if (ex != null)
  {
    SqlException sqlException;
    if ((sqlException = ex as SqlException) != null)
    {
      // Enumerate through all errors found in hello exception.
      foreach (SqlError err in sqlException.Errors)
      {
        switch (err.Number)
        {
            // SQL Error Code: 40501
            // hello service is currently busy. Retry hello request after 10 seconds.
            // Code: (reason code toobe decoded).
          case ThrottlingCondition.ThrottlingErrorNumber:
            // Decode hello reason code from hello error message to
            // determine hello grounds for throttling.
            var condition = ThrottlingCondition.FromError(err);

            // Attach hello decoded values as additional attributes to
            // hello original SQL exception.
            sqlException.Data[condition.ThrottlingMode.GetType().Name] =
              condition.ThrottlingMode.ToString();
            sqlException.Data[condition.GetType().Name] = condition;

            return true;

          case 10928:
          case 10929:
          case 10053:
          case 10054:
          case 10060:
          case 40197:
          case 40540:
          case 40613:
          case 40143:
          case 233:
          case 64:
            // DBNETLIB Error Code: 20
            // hello instance of SQL Server you attempted tooconnect to
            // does not support encryption.
          case (int)ProcessNetLibErrorCode.EncryptionNotSupported:
            return true;
        }
      }
    }
    else if (ex is TimeoutException)
    {
      return true;
    }
    else
    {
      EntityException entityException;
      if ((entityException = ex as EntityException) != null)
      {
        return this.IsTransient(entityException.InnerException);
      }
    }
  }

  return false;
}
```


## <a name="next-steps"></a><span data-ttu-id="b4f5f-302">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b4f5f-302">Next steps</span></span>
* <span data-ttu-id="b4f5f-303">Para solucionar outros problemas comuns de conexão de banco de dados de SQL do Azure, visite [tooAzure banco de dados SQL de problemas de solução de problemas conexão](sql-database-troubleshoot-common-connection-issues.md).</span><span class="sxs-lookup"><span data-stu-id="b4f5f-303">For troubleshooting other common Azure SQL Database connection issues, visit [Troubleshoot connection issues tooAzure SQL Database](sql-database-troubleshoot-common-connection-issues.md).</span></span>
* [<span data-ttu-id="b4f5f-304">Pool de conexões do SQL Server (ADO.NET)</span><span class="sxs-lookup"><span data-stu-id="b4f5f-304">SQL Server Connection Pooling (ADO.NET)</span></span>](http://msdn.microsoft.com/library/8xx3tyca.aspx)
* [<span data-ttu-id="b4f5f-305">*Repetindo* é de finalidade geral de repetir a biblioteca, escrita em uma licença do Apache 2.0 **Python**, tarefa de saudação do toosimplify de adicionar toojust de comportamento de repetição sobre qualquer coisa.</span><span class="sxs-lookup"><span data-stu-id="b4f5f-305">*Retrying* is an Apache 2.0 licensed general-purpose retrying library, written in **Python**, toosimplify hello task of adding retry behavior toojust about anything.</span></span>](https://pypi.python.org/pypi/retrying)

