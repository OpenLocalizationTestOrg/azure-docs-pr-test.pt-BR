---
title: "programação JavaScript aaaServer para o banco de dados do Azure Cosmos | Microsoft Docs"
description: "Saiba como toowrite de banco de dados do Azure Cosmos toouse procedimentos armazenados, gatilhos de banco de dados e funções definidas pelo usuário (UDFs) em JavaScript. Obtenha dicas de programação de banco de dados e muito mais."
keywords: Gatilhos de banco de dados, procedimento armazenado, programa de banco de dados, sproc, banco de dados de documentos, azure, Microsoft azure
services: cosmos-db
documentationcenter: 
author: aliuy
manager: jhubbard
editor: mimig
ms.assetid: 0fba7ebd-a4fc-4253-a786-97f1354fbf17
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: andrl
ms.openlocfilehash: 5a011d1c4b0b5908d5de73607a1bc328ed1711d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-server-side-programming-stored-procedures-database-triggers-and-udfs"></a><span data-ttu-id="e816c-105">Programação do lado do servidor do Azure Cosmos DB: procedimentos armazenados, gatilhos de banco de dados e UDFs</span><span class="sxs-lookup"><span data-stu-id="e816c-105">Azure Cosmos DB server-side programming: Stored procedures, database triggers, and UDFs</span></span>
<span data-ttu-id="e816c-106">Saiba como a execução transacional e integrada de linguagem do JavaScript pelo Azure Cosmos DB permite que desenvolvedores escrevam **procedimentos armazenados**, **gatilhos** e **UDFs (funções definidas pelo usuário)** nativamente em um JavaScript [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/).</span><span class="sxs-lookup"><span data-stu-id="e816c-106">Learn how Azure Cosmos DB’s language integrated, transactional execution of JavaScript lets developers write **stored procedures**, **triggers** and **user defined functions (UDFs)** natively in an [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript.</span></span> <span data-ttu-id="e816c-107">Isso permite que você toowrite banco de dados programa lógica do aplicativo que pode ser enviada e executada diretamente em partições de armazenamento do banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e816c-107">This allows you toowrite database program application logic that can be shipped and executed directly on hello database storage partitions.</span></span> 

<span data-ttu-id="e816c-108">É recomendável obter iniciado por Olá assistindo a seguir vídeo, onde Andrew Liu fornece tooCosmos uma breve introdução do banco de dados modelo de programação de banco de dados do servidor.</span><span class="sxs-lookup"><span data-stu-id="e816c-108">We recommend getting started by watching hello following video, where Andrew Liu provides a brief introduction tooCosmos DB's server-side database programming model.</span></span> 

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Demo-A-Quick-Intro-to-Azure-DocumentDBs-Server-Side-Javascript/player]
> 
> 

<span data-ttu-id="e816c-109">Em seguida, retorne toothis artigo, onde você aprenderá Olá respostas toohello perguntas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e816c-109">Then, return toothis article, where you'll learn hello answers toohello following questions:</span></span>  

* <span data-ttu-id="e816c-110">Como eu escrevo um procedimento armazenado, gatilho ou UDF usando JavaScript?</span><span class="sxs-lookup"><span data-stu-id="e816c-110">How do I write a a stored procedure, trigger, or UDF using JavaScript?</span></span>
* <span data-ttu-id="e816c-111">Como o Cosmos DB garante o ACID?</span><span class="sxs-lookup"><span data-stu-id="e816c-111">How does Cosmos DB guarantee ACID?</span></span>
* <span data-ttu-id="e816c-112">Como funcionam as transações no Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="e816c-112">How do transactions work in Cosmos DB?</span></span>
* <span data-ttu-id="e816c-113">O que são pré-gatilhos e pós-gatilhos e como eu escrevo um?</span><span class="sxs-lookup"><span data-stu-id="e816c-113">What are pre-triggers and post-triggers and how do I write one?</span></span>
* <span data-ttu-id="e816c-114">Como eu registro e executo um procedimento armazenado, gatilho ou UDF de modo RESTful usando HTTP?</span><span class="sxs-lookup"><span data-stu-id="e816c-114">How do I register and execute a stored procedure, trigger, or UDF in a RESTful manner by using HTTP?</span></span>
* <span data-ttu-id="e816c-115">Quais Cosmos DB SDKs são toocreate disponível e execute procedimentos armazenados, gatilhos e UDFs?</span><span class="sxs-lookup"><span data-stu-id="e816c-115">What Cosmos DB SDKs are available toocreate and execute stored procedures, triggers, and UDFs?</span></span>

## <a name="introduction-toostored-procedure-and-udf-programming"></a><span data-ttu-id="e816c-116">Introdução tooStored procedimento e programação de UDF</span><span class="sxs-lookup"><span data-stu-id="e816c-116">Introduction tooStored Procedure and UDF Programming</span></span>
<span data-ttu-id="e816c-117">Essa abordagem de *"JavaScript como dia moderno T-SQL"* libera os desenvolvedores de aplicativos das complexidades Olá de incompatibilidade do tipo de sistema e as tecnologias de mapeamento relacional de objeto.</span><span class="sxs-lookup"><span data-stu-id="e816c-117">This approach of *“JavaScript as a modern day T-SQL”* frees application developers from hello complexities of type system mismatches and object-relational mapping technologies.</span></span> <span data-ttu-id="e816c-118">Ele também tem uma série de vantagens intrínsecas que podem ser utilizadas toobuild excelentes aplicativos:</span><span class="sxs-lookup"><span data-stu-id="e816c-118">It also has a number of intrinsic advantages that can be utilized toobuild rich applications:</span></span>  

* <span data-ttu-id="e816c-119">**Lógica de procedimento:** JavaScript como uma linguagem de programação de alto nível, fornece uma interface familiar e avançado tooexpress lógica de negócios.</span><span class="sxs-lookup"><span data-stu-id="e816c-119">**Procedural Logic:** JavaScript as a high level programming language, provides a rich and familiar interface tooexpress business logic.</span></span> <span data-ttu-id="e816c-120">Você pode executar sequências complexas dos dados toohello mais próximos de operações.</span><span class="sxs-lookup"><span data-stu-id="e816c-120">You can perform complex sequences of operations closer toohello data.</span></span>
* <span data-ttu-id="e816c-121">**Transações atômicas:** o Cosmos DB garante que as operações de banco de dados realizadas em um único procedimento armazenado ou gatilho são atômicas.</span><span class="sxs-lookup"><span data-stu-id="e816c-121">**Atomic Transactions:** Cosmos DB guarantees that database operations performed inside a single stored procedure or trigger are atomic.</span></span> <span data-ttu-id="e816c-122">Isso permite que um aplicativo combine operações relacionadas em um único lote para que todas ou nenhuma delas seja bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="e816c-122">This lets an application combine related operations in a single batch so that either all of them succeed or none of them succeed.</span></span> 
* <span data-ttu-id="e816c-123">**Desempenho:** documentos de fato Olá JSON é o sistema de tipo de linguagem de Javascript toohello intrinsecamente mapeadas e também é a unidade básica Olá de armazenamento no banco de dados do Cosmos permite um número de otimizações como lenta materialização de JSON no buffer de saudação pool e tornando-os disponível toohello sob demanda executando o código.</span><span class="sxs-lookup"><span data-stu-id="e816c-123">**Performance:** hello fact that JSON is intrinsically mapped toohello Javascript language type system and is also hello basic unit of storage in Cosmos DB allows for a number of optimizations like lazy materialization of JSON documents in hello buffer pool and making them available on-demand toohello executing code.</span></span> <span data-ttu-id="e816c-124">Há mais benefícios de desempenho associados com o banco de dados toohello lógica de envio comercial:</span><span class="sxs-lookup"><span data-stu-id="e816c-124">There are more performance benefits associated with shipping business logic toohello database:</span></span>
  
  * <span data-ttu-id="e816c-125">Envio em lote – Os desenvolvedores podem agrupar operações como inserções e enviá-las em massa.</span><span class="sxs-lookup"><span data-stu-id="e816c-125">Batching – Developers can group operations like inserts and submit them in bulk.</span></span> <span data-ttu-id="e816c-126">custo de latência de tráfego de rede Hello e transações separadas do hello repositório toocreate sobrecarga são reduzidas significativamente.</span><span class="sxs-lookup"><span data-stu-id="e816c-126">hello network traffic latency cost and hello store overhead toocreate separate transactions are reduced significantly.</span></span> 
  * <span data-ttu-id="e816c-127">Pré-compilação – Cosmos DB pré-compila procedimentos armazenados, disparadores e definidos pelo usuário UDFs (funções) tooavoid custo de compilação de JavaScript para cada invocação.</span><span class="sxs-lookup"><span data-stu-id="e816c-127">Pre-compilation – Cosmos DB precompiles stored procedures, triggers and user defined functions (UDFs) tooavoid JavaScript compilation cost for each invocation.</span></span> <span data-ttu-id="e816c-128">Olá, sobrecarga de compilação de código de bytes de saudação para lógica de procedimento Olá é amortizado tooa o valor mínimo.</span><span class="sxs-lookup"><span data-stu-id="e816c-128">hello overhead of building hello byte code for hello procedural logic is amortized tooa minimal value.</span></span>
  * <span data-ttu-id="e816c-129">Sequenciamento – Várias operações precisam de um efeito colateral (“gatilho”) que possivelmente envolve realizar uma ou mais operações de armazenamento secundárias.</span><span class="sxs-lookup"><span data-stu-id="e816c-129">Sequencing – Many operations need a side-effect (“trigger”) that potentially involves doing one or many secondary store operations.</span></span> <span data-ttu-id="e816c-130">Além de atomicidade, isso é mais eficaz quando movidos toohello server.</span><span class="sxs-lookup"><span data-stu-id="e816c-130">Aside from atomicity, this is more performant when moved toohello server.</span></span> 
* <span data-ttu-id="e816c-131">**Encapsulamento:** procedimentos armazenados podem ser usados toogroup lógica de negócios em um local.</span><span class="sxs-lookup"><span data-stu-id="e816c-131">**Encapsulation:** Stored procedures can be used toogroup business logic in one place.</span></span> <span data-ttu-id="e816c-132">Isso apresenta duas vantagens:</span><span class="sxs-lookup"><span data-stu-id="e816c-132">This has two advantages:</span></span>
  * <span data-ttu-id="e816c-133">Ele adiciona uma camada de abstração sobre dados brutos hello, que permite que dados arquitetos tooevolve seus aplicativos independentemente do dados saudação.</span><span class="sxs-lookup"><span data-stu-id="e816c-133">It adds an abstraction layer on top of hello raw data, which enables data architects tooevolve their applications independently from hello data.</span></span> <span data-ttu-id="e816c-134">Isso é particularmente vantajoso quando Olá dados sem esquema, devido a toohello suposições frágil que talvez seja necessário toobe implantada na aplicativo hello se eles tiverem toodeal com dados diretamente.</span><span class="sxs-lookup"><span data-stu-id="e816c-134">This is particularly advantageous when hello data is schema-less, due toohello brittle assumptions that may need toobe baked into hello application if they have toodeal with data directly.</span></span>  
  * <span data-ttu-id="e816c-135">Essa abstração permite que as empresas proteger seus dados simplificando o acesso de saudação de scripts de saudação.</span><span class="sxs-lookup"><span data-stu-id="e816c-135">This abstraction lets enterprises keep their data secure by streamlining hello access from hello scripts.</span></span>  

<span data-ttu-id="e816c-136">Olá criação e execução de gatilhos de banco de dados, o procedimento armazenado e operadores de consulta personalizada é suportado por meio de saudação [API REST](/rest/api/documentdb/), [Studio do Azure DocumentDB](https://github.com/mingaliu/DocumentDBStudio/releases), e [cliente SDKs](documentdb-sdk-dotnet.md) em muitas plataformas, incluindo .NET, Node.js e JavaScript.</span><span class="sxs-lookup"><span data-stu-id="e816c-136">hello creation and execution of database triggers, stored procedure and custom query operators is supported through hello [REST API](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), and [client SDKs](documentdb-sdk-dotnet.md) in many platforms including .NET, Node.js and JavaScript.</span></span>

<span data-ttu-id="e816c-137">Este tutorial usa Olá [Node. js SDK com p promessas](http://azure.github.io/azure-documentdb-node-q/) tooillustrate sintaxe e uso de procedimentos armazenados, gatilhos e UDFs.</span><span class="sxs-lookup"><span data-stu-id="e816c-137">This tutorial uses hello [Node.js SDK with Q Promises](http://azure.github.io/azure-documentdb-node-q/) tooillustrate syntax and usage of stored procedures, triggers, and UDFs.</span></span>   

## <a name="stored-procedures"></a><span data-ttu-id="e816c-138">Procedimentos armazenados</span><span class="sxs-lookup"><span data-stu-id="e816c-138">Stored procedures</span></span>
### <a name="example-write-a-simple-stored-procedure"></a><span data-ttu-id="e816c-139">Exemplo: escrever um procedimento armazenado simples</span><span class="sxs-lookup"><span data-stu-id="e816c-139">Example: Write a simple stored procedure</span></span>
<span data-ttu-id="e816c-140">Vamos começar com um procedimento armazenado simples que retorna uma resposta “Hello World”.</span><span class="sxs-lookup"><span data-stu-id="e816c-140">Let’s start with a simple stored procedure that returns a “Hello World” response.</span></span>

    var helloWorldStoredProc = {
        id: "helloWorld",
        serverScript: function () {
            var context = getContext();
            var response = context.getResponse();

            response.setBody("Hello, World");
        }
    }


<span data-ttu-id="e816c-141">Os procedimentos armazenados são registrados por coleção e podem operar em qualquer documento e anexo presente na coleção.</span><span class="sxs-lookup"><span data-stu-id="e816c-141">Stored procedures are registered per collection, and can operate on any document and attachment present in that collection.</span></span> <span data-ttu-id="e816c-142">Olá trecho a seguir mostra como tooregister Olá helloWorld armazenado procedimento com uma coleção.</span><span class="sxs-lookup"><span data-stu-id="e816c-142">hello following snippet shows how tooregister hello helloWorld stored procedure with a collection.</span></span> 

    // register hello stored procedure
    var createdStoredProcedure;
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', helloWorldStoredProc)
        .then(function (response) {
            createdStoredProcedure = response.resource;
            console.log("Successfully created stored procedure");
        }, function (error) {
            console.log("Error", error);
        });


<span data-ttu-id="e816c-143">Depois que o procedimento armazenado de saudação for registrado, podemos executá-lo em coleção hello e ler Olá resultados no cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="e816c-143">Once hello stored procedure is registered, we can execute it against hello collection, and read hello results back at hello client.</span></span> 

    // execute hello stored procedure
    client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/helloWorld')
        .then(function (response) {
            console.log(response.result); // "Hello, World"
        }, function (err) {
            console.log("Error", error);
        });


<span data-ttu-id="e816c-144">objeto de contexto Olá fornece acesso a operações de tooall que podem ser executadas no armazenamento de banco de dados do Cosmos, bem como acessarem objetos de solicitação e resposta toohello.</span><span class="sxs-lookup"><span data-stu-id="e816c-144">hello context object provides access tooall operations that can be performed on Cosmos DB storage, as well as access toohello request and response objects.</span></span> <span data-ttu-id="e816c-145">Nesse caso, usamos o corpo da saudação Olá resposta objeto tooset de resposta de saudação enviada toohello back cliente.</span><span class="sxs-lookup"><span data-stu-id="e816c-145">In this case, we used hello response object tooset hello body of hello response that was sent back toohello client.</span></span> <span data-ttu-id="e816c-146">Para obter mais detalhes, consulte toohello [server Azure Cosmos DB JavaScript documentação do SDK](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="e816c-146">For more details, refer toohello [Azure Cosmos DB JavaScript server SDK documentation](http://azure.github.io/azure-documentdb-js-server/).</span></span>  

<span data-ttu-id="e816c-147">Vamos ampliar esse exemplo e adicionar mais funcionalidades relacionadas do banco de dados toohello procedimento de armazenado.</span><span class="sxs-lookup"><span data-stu-id="e816c-147">Let us expand on this example and add more database related functionality toohello stored procedure.</span></span> <span data-ttu-id="e816c-148">Procedimentos armazenados podem criar, atualizar, ler, consultar e excluir documentos e anexos de coleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="e816c-148">Stored procedures can create, update, read, query and delete documents and attachments inside hello collection.</span></span>    

### <a name="example-write-a-stored-procedure-toocreate-a-document"></a><span data-ttu-id="e816c-149">Exemplo: Gravar um procedimento armazenado toocreate um documento</span><span class="sxs-lookup"><span data-stu-id="e816c-149">Example: Write a stored procedure toocreate a document</span></span>
<span data-ttu-id="e816c-150">trecho Avançar Olá mostra como toouse Olá toointeract de objeto de contexto com recursos de banco de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="e816c-150">hello next snippet shows how toouse hello context object toointeract with Cosmos DB resources.</span></span>

    var createDocumentStoredProc = {
        id: "createMyDocument",
        serverScript: function createMyDocument(documentToCreate) {
            var context = getContext();
            var collection = context.getCollection();

            var accepted = collection.createDocument(collection.getSelfLink(),
                  documentToCreate,
                  function (err, documentCreated) {
                      if (err) throw new Error('Error' + err.message);
                      context.getResponse().setBody(documentCreated.id)
                  });
            if (!accepted) return;
        }
    }


<span data-ttu-id="e816c-151">Esse procedimento armazenado usa como entrada documentToCreate, corpo de saudação de um toobe documento criado no conjunto atual de saudação.</span><span class="sxs-lookup"><span data-stu-id="e816c-151">This stored procedure takes as input documentToCreate, hello body of a document toobe created in hello current collection.</span></span> <span data-ttu-id="e816c-152">Todas essas operações são assíncronas e dependem de retornos de chamada de função do JavaScript.</span><span class="sxs-lookup"><span data-stu-id="e816c-152">All such operations are asynchronous and depend on JavaScript function callbacks.</span></span> <span data-ttu-id="e816c-153">função de retorno de chamada Hello tem dois parâmetros, um objeto de erro Olá caso Olá operação falhar e outra para Olá criou o objeto.</span><span class="sxs-lookup"><span data-stu-id="e816c-153">hello callback function has two parameters, one for hello error object in case hello operation fails, and one for hello created object.</span></span> <span data-ttu-id="e816c-154">No retorno de chamada hello, os usuários podem lidar com exceção de saudação ou gerar um erro.</span><span class="sxs-lookup"><span data-stu-id="e816c-154">Inside hello callback, users can either handle hello exception or throw an error.</span></span> <span data-ttu-id="e816c-155">No caso de um retorno de chamada não for fornecido e há um erro, o tempo de execução de banco de dados do Azure Cosmos hello gera um erro.</span><span class="sxs-lookup"><span data-stu-id="e816c-155">In case a callback is not provided and there is an error, hello Azure Cosmos DB runtime throws an error.</span></span>   

<span data-ttu-id="e816c-156">No exemplo hello acima, o retorno de chamada hello gera um erro se a falha na operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e816c-156">In hello example above, hello callback throws an error if hello operation failed.</span></span> <span data-ttu-id="e816c-157">Caso contrário, ele define id de saudação do hello criada o documento como corpo de saudação do cliente de toohello de resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="e816c-157">Otherwise, it sets hello id of hello created document as hello body of hello response toohello client.</span></span> <span data-ttu-id="e816c-158">A seguir, mostramos como esse procedimento armazenado é executado com parâmetros de entrada.</span><span class="sxs-lookup"><span data-stu-id="e816c-158">Here is how this stored procedure is executed with input parameters.</span></span>

    // register hello stored procedure
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', createDocumentStoredProc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;

            // run stored procedure toocreate a document
            var docToCreate = {
                id: "DocFromSproc",
                book: "hello Hitchhiker’s Guide toohello Galaxy",
                author: "Douglas Adams"
            };

            return client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/createMyDocument',
                  docToCreate);
        }, function (error) {
            console.log("Error", error);
        })
    .then(function (response) {
        console.log(response); // "DocFromSproc"
    }, function (error) {
        console.log("Error", error);
    });


<span data-ttu-id="e816c-159">Observe que este procedimento armazenado pode ser modificado tootake uma matriz de corpos de documento como entrada e criá-los em Olá mesmo armazenado execução do procedimento em vez de rede de várias solicitações toocreate cada um deles individualmente.</span><span class="sxs-lookup"><span data-stu-id="e816c-159">Note that this stored procedure can be modified tootake an array of document bodies as input and create them all in hello same stored procedure execution instead of multiple network requests toocreate each of them individually.</span></span> <span data-ttu-id="e816c-160">Isso pode ser usado tooimplement um importador em massa eficiente para o banco de dados do Cosmos (discutidas posteriormente neste tutorial).</span><span class="sxs-lookup"><span data-stu-id="e816c-160">This can be used tooimplement an efficient bulk importer for Cosmos DB (discussed later in this tutorial).</span></span>   

<span data-ttu-id="e816c-161">exemplo Hello descrito demonstrou como toouse de procedimentos armazenados.</span><span class="sxs-lookup"><span data-stu-id="e816c-161">hello example described demonstrated how toouse stored procedures.</span></span> <span data-ttu-id="e816c-162">Abordaremos gatilhos e funções definidas pelo usuário (UDFs) mais tarde no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="e816c-162">We will cover triggers and user defined functions (UDFs) later in hello tutorial.</span></span>

## <a name="database-program-transactions"></a><span data-ttu-id="e816c-163">Transações do programa de banco de dados</span><span class="sxs-lookup"><span data-stu-id="e816c-163">Database program transactions</span></span>
<span data-ttu-id="e816c-164">A transação em um banco de dados típico pode ser definida como uma sequência de operações realizadas como uma única unidade lógica de trabalho.</span><span class="sxs-lookup"><span data-stu-id="e816c-164">Transaction in a typical database can be defined as a sequence of operations performed as a single logical unit of work.</span></span> <span data-ttu-id="e816c-165">Cada transação oferece **garantias ACID**.</span><span class="sxs-lookup"><span data-stu-id="e816c-165">Each transaction provides **ACID guarantees**.</span></span> <span data-ttu-id="e816c-166">ACID é um acrônimo bastante conhecido que indica quatro propriedades: Atomicidade, Consistência, Isolamento e Durabilidade.</span><span class="sxs-lookup"><span data-stu-id="e816c-166">ACID is a well-known acronym that stands for four properties -  Atomicity, Consistency, Isolation and Durability.</span></span>  

<span data-ttu-id="e816c-167">Em resumo, a atomicidade garante que todo o trabalho Olá feito dentro de uma transação é tratado como uma única unidade onde o tudo é confirmada ou nenhum.</span><span class="sxs-lookup"><span data-stu-id="e816c-167">Briefly, atomicity guarantees that all hello work done inside a transaction is treated as a single unit where either all of it is committed or none.</span></span> <span data-ttu-id="e816c-168">Consistência assegura que Olá dados sempre estejam em bom estado interno em transações.</span><span class="sxs-lookup"><span data-stu-id="e816c-168">Consistency makes sure that hello data is always in a good internal state across transactions.</span></span> <span data-ttu-id="e816c-169">Isolamento garante que nenhuma das duas transações interfere uns aos outros – em geral, os sistemas comerciais mais fornecem vários níveis de isolamento que podem ser usados com base nas necessidades do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="e816c-169">Isolation guarantees that no two transactions interfere with each other – generally, most commercial systems provide multiple isolation levels that can be used based on hello application needs.</span></span> <span data-ttu-id="e816c-170">Durabilidade garante que qualquer alteração que está confirmada no banco de dados de saudação sempre estarão presente.</span><span class="sxs-lookup"><span data-stu-id="e816c-170">Durability ensures that any change that’s committed in hello database will always be present.</span></span>   

<span data-ttu-id="e816c-171">No banco de dados do Cosmos, JavaScript é hospedado no hello mesmo espaço de memória como banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e816c-171">In Cosmos DB, JavaScript is hosted in hello same memory space as hello database.</span></span> <span data-ttu-id="e816c-172">Portanto, solicitações feitas em procedimentos armazenados e gatilhos executar no hello mesmo escopo de uma sessão de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e816c-172">Hence, requests made within stored procedures and triggers execute in hello same scope of a database session.</span></span> <span data-ttu-id="e816c-173">Isso permite que tooguarantee Cosmos DB ACID para todas as operações que fazem parte de um único armazenado procedimento/disparador.</span><span class="sxs-lookup"><span data-stu-id="e816c-173">This enables Cosmos DB tooguarantee ACID for all operations that are part of a single stored procedure/trigger.</span></span> <span data-ttu-id="e816c-174">Considere o seguinte Olá armazenados definição do procedimento:</span><span class="sxs-lookup"><span data-stu-id="e816c-174">Consider hello following stored procedure definition:</span></span>

    // JavaScript source code
    var exchangeItemsSproc = {
        id: "exchangeItems",
        serverScript: function (playerId1, playerId2) {
            var context = getContext();
            var collection = context.getCollection();
            var response = context.getResponse();

            var player1Document, player2Document;

            // query for players
            var filterQuery = 'SELECT * FROM Players p where p.id  = "' + playerId1 + '"';
            var accept = collection.queryDocuments(collection.getSelfLink(), filterQuery, {},
                function (err, documents, responseOptions) {
                    if (err) throw new Error("Error" + err.message);

                    if (documents.length != 1) throw "Unable toofind both names";
                    player1Document = documents[0];

                    var filterQuery2 = 'SELECT * FROM Players p where p.id = "' + playerId2 + '"';
                    var accept2 = collection.queryDocuments(collection.getSelfLink(), filterQuery2, {},
                        function (err2, documents2, responseOptions2) {
                            if (err2) throw new Error("Error" + err2.message);
                            if (documents2.length != 1) throw "Unable toofind both names";
                            player2Document = documents2[0];
                            swapItems(player1Document, player2Document);
                            return;
                        });
                    if (!accept2) throw "Unable tooread player details, abort ";
                });

            if (!accept) throw "Unable tooread player details, abort ";

            // swap hello two players’ items
            function swapItems(player1, player2) {
                var player1ItemSave = player1.item;
                player1.item = player2.item;
                player2.item = player1ItemSave;

                var accept = collection.replaceDocument(player1._self, player1,
                    function (err, docReplaced) {
                        if (err) throw "Unable tooupdate player 1, abort ";

                        var accept2 = collection.replaceDocument(player2._self, player2,
                            function (err2, docReplaced2) {
                                if (err) throw "Unable tooupdate player 2, abort"
                            });

                        if (!accept2) throw "Unable tooupdate player 2, abort";
                    });

                if (!accept) throw "Unable tooupdate player 1, abort";
            }
        }
    }

    // register hello stored procedure in Node.js client
    client.createStoredProcedureAsync(collection._self, exchangeItemsSproc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;
        }
    );

<span data-ttu-id="e816c-175">Esse procedimento armazenado usa transações em itens jogos aplicativo tootrade entre os dois participantes em uma única operação.</span><span class="sxs-lookup"><span data-stu-id="e816c-175">This stored procedure uses transactions within a gaming app tootrade items between two players in a single operation.</span></span> <span data-ttu-id="e816c-176">Olá armazenados procedimento tentativas tooread dois documentos que cada player de toohello IDs correspondentes passado como um argumento.</span><span class="sxs-lookup"><span data-stu-id="e816c-176">hello stored procedure attempts tooread two documents each corresponding toohello player IDs passed in as an argument.</span></span> <span data-ttu-id="e816c-177">Se ambos os documentos de player for encontrados, o procedimento de Olá armazenado atualiza documentos Olá trocando seus itens.</span><span class="sxs-lookup"><span data-stu-id="e816c-177">If both player documents are found, then hello stored procedure updates hello documents by swapping their items.</span></span> <span data-ttu-id="e816c-178">Se houver erros ao longo de maneira hello, ele lança uma exceção de JavaScript que implicitamente anula a transação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e816c-178">If any errors are encountered along hello way, it throws a JavaScript exception that implicitly aborts hello transaction.</span></span>

<span data-ttu-id="e816c-179">Se hello coleção Olá armazenado procedimento é registrado em relação é uma coleção de partição única, transação hello está no escopo tooall Olá documentos na coleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="e816c-179">If hello collection hello stored procedure is registered against is a single-partition collection, then hello transaction is scoped tooall hello documents within hello collection.</span></span> <span data-ttu-id="e816c-180">Se a coleção Olá estiver particionada, procedimentos armazenados são executados no escopo de transação de saudação de uma chave de partição única.</span><span class="sxs-lookup"><span data-stu-id="e816c-180">If hello collection is partitioned, then stored procedures are executed in hello transaction scope of a single partition key.</span></span> <span data-ttu-id="e816c-181">Cada armazenado execução do procedimento deve incluir um valor de chave de partição deve ser executados na transação de saudação do escopo toohello correspondente.</span><span class="sxs-lookup"><span data-stu-id="e816c-181">Each stored procedure execution must then include a partition key value corresponding toohello scope hello transaction must run under.</span></span> <span data-ttu-id="e816c-182">Para obter mais detalhes, consulte [Particionamento do Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="e816c-182">For more details, see [Azure Cosmos DB Partitioning](partition-data.md).</span></span>

### <a name="commit-and-rollback"></a><span data-ttu-id="e816c-183">Confirmação e reversão</span><span class="sxs-lookup"><span data-stu-id="e816c-183">Commit and rollback</span></span>
<span data-ttu-id="e816c-184">As transações são profunda e nativamente integradas ao modelo de programação do JavaScript do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e816c-184">Transactions are deeply and natively integrated into Cosmos DB’s JavaScript programming model.</span></span> <span data-ttu-id="e816c-185">Dentro de uma função de JavaScript, todas as operações são automaticamente encapsuladas em uma única transação.</span><span class="sxs-lookup"><span data-stu-id="e816c-185">Inside a JavaScript function, all operations are automatically wrapped under a single transaction.</span></span> <span data-ttu-id="e816c-186">Se hello JavaScript é concluído sem qualquer exceção, o banco de dados do toohello Olá operações serão confirmadas.</span><span class="sxs-lookup"><span data-stu-id="e816c-186">If hello JavaScript completes without any exception, hello operations toohello database are committed.</span></span> <span data-ttu-id="e816c-187">Na verdade, instruções de "BEGIN TRANSACTION" e "COMMIT TRANSACTION" hello em bancos de dados relacionais são implícitas no banco de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="e816c-187">In effect, hello “BEGIN TRANSACTION” and “COMMIT TRANSACTION” statements in relational databases are implicit in Cosmos DB.</span></span>  

<span data-ttu-id="e816c-188">Se houver qualquer exceção que é propagada de script hello, tempo de execução de JavaScript do Cosmos DB reverterá toda a transação hello.</span><span class="sxs-lookup"><span data-stu-id="e816c-188">If there is any exception that’s propagated from hello script, Cosmos DB’s JavaScript runtime will roll back hello whole transaction.</span></span> <span data-ttu-id="e816c-189">Conforme mostrado no hello anteriormente exemplo, gerar uma exceção é efetivamente equivalente tooa "ROLLBACK TRANSACTION" no banco de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="e816c-189">As shown in hello earlier example, throwing an exception is effectively equivalent tooa “ROLLBACK TRANSACTION” in Cosmos DB.</span></span>

### <a name="data-consistency"></a><span data-ttu-id="e816c-190">Consistência de dados</span><span class="sxs-lookup"><span data-stu-id="e816c-190">Data consistency</span></span>
<span data-ttu-id="e816c-191">Procedimentos armazenados e gatilhos são sempre executados na réplica primária de saudação do contêiner de banco de dados do Azure Cosmos hello.</span><span class="sxs-lookup"><span data-stu-id="e816c-191">Stored procedures and triggers are always executed on hello primary replica of hello Azure Cosmos DB container.</span></span> <span data-ttu-id="e816c-192">Isso assegura que as leituras de dentro de procedimentos armazenados ofereçam uma forte consistência.</span><span class="sxs-lookup"><span data-stu-id="e816c-192">This ensures that reads from inside stored procedures offer strong consistency.</span></span> <span data-ttu-id="e816c-193">Consultas que usam funções definidas pelo usuário podem ser executadas no hello primário ou de qualquer réplica secundária, mas podemos garantir toomeet Olá solicitado nível de consistência escolhendo réplica apropriado hello.</span><span class="sxs-lookup"><span data-stu-id="e816c-193">Queries using user defined functions can be executed on hello primary or any secondary replica, but we ensure toomeet hello requested consistency level by choosing hello appropriate replica.</span></span>

## <a name="bounded-execution"></a><span data-ttu-id="e816c-194">Execução vinculada</span><span class="sxs-lookup"><span data-stu-id="e816c-194">Bounded execution</span></span>
<span data-ttu-id="e816c-195">Todas as operações de banco de dados do Cosmos devem ser concluído no servidor de saudação especificado duração de tempo limite da solicitação.</span><span class="sxs-lookup"><span data-stu-id="e816c-195">All Cosmos DB operations must complete within hello server specified request timeout duration.</span></span> <span data-ttu-id="e816c-196">Essa restrição também se aplica a funções tooJavaScript (procedimentos armazenados, gatilhos e funções definidas pelo usuário).</span><span class="sxs-lookup"><span data-stu-id="e816c-196">This constraint also applies tooJavaScript functions (stored procedures, triggers and user-defined functions).</span></span> <span data-ttu-id="e816c-197">Se uma operação não for concluída com limite de tempo, as transações de saudação é revertida.</span><span class="sxs-lookup"><span data-stu-id="e816c-197">If an operation does not complete with that time limit, hello transaction is rolled back.</span></span> <span data-ttu-id="e816c-198">Funções JavaScript devem ser concluída dentro do limite de tempo de saudação ou implementar uma execução de toobatch/retomar continuação com base em modelo.</span><span class="sxs-lookup"><span data-stu-id="e816c-198">JavaScript functions must finish within hello time limit or implement a continuation based model toobatch/resume execution.</span></span>  

<span data-ttu-id="e816c-199">No desenvolvimento de toosimplify ordem armazenado procedimentos e gatilhos toohandle limites de tempo, todas as funções no objeto de coleção de saudação (para criar, ler, substituir e exclusão de documentos e anexos) retornam um valor booleano que representa se que a operação será concluída.</span><span class="sxs-lookup"><span data-stu-id="e816c-199">In order toosimplify development of stored procedures and triggers toohandle time limits, all functions under hello collection object (for create, read, replace, and delete of documents and attachments) return a Boolean value that represents whether that operation will complete.</span></span> <span data-ttu-id="e816c-200">Se esse valor for false, é uma indicação de que limite de tempo de saudação é sobre tooexpire e procedimento Olá deve encapsular a execução.</span><span class="sxs-lookup"><span data-stu-id="e816c-200">If this value is false, it is an indication that hello time limit is about tooexpire and that hello procedure must wrap up execution.</span></span>  <span data-ttu-id="e816c-201">Operações em fila toohello anterior primeira operação de repositório inaceitável têm a garantia toocomplete se o procedimento de Olá armazenado é concluída no tempo e não enfileirar mais solicitações.</span><span class="sxs-lookup"><span data-stu-id="e816c-201">Operations queued prior toohello first unaccepted store operation are guaranteed toocomplete if hello stored procedure completes in time and does not queue any more requests.</span></span>  

<span data-ttu-id="e816c-202">Funções de JavaScript também são vinculadas quanto ao consumo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e816c-202">JavaScript functions are also bounded on resource consumption.</span></span> <span data-ttu-id="e816c-203">Cosmos DB reserva a taxa de transferência por coleção com base no tamanho de saudação provisionado de uma conta de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e816c-203">Cosmos DB reserves throughput per collection based on hello provisioned size of a database account.</span></span> <span data-ttu-id="e816c-204">A produtividade é expressa em termos de uma unidade normalizada de consumo de CPU, memória e E/S chamada unidade de solicitação ou RU.</span><span class="sxs-lookup"><span data-stu-id="e816c-204">Throughput is expressed in terms of a normalized unit of CPU, memory and IO consumption called request units or RUs.</span></span> <span data-ttu-id="e816c-205">Funções JavaScript podem potencialmente usar um número grande de RUs dentro de um curto período de tempo e podem obter a taxa limitada se limite da coleção Olá for atingido.</span><span class="sxs-lookup"><span data-stu-id="e816c-205">JavaScript functions can potentially use up a large number of RUs within a short time, and might get rate-limited if hello collection’s limit is reached.</span></span> <span data-ttu-id="e816c-206">Procedimentos armazenados uso intensivo de recursos também podem estar em quarentena tooensure disponibilidade das operações de banco de dados primitivo.</span><span class="sxs-lookup"><span data-stu-id="e816c-206">Resource intensive stored procedures might also be quarantined tooensure availability of primitive database operations.</span></span>  

### <a name="example-bulk-importing-data-into-a-database-program"></a><span data-ttu-id="e816c-207">Exemplo: importação de dados em massa em um programa de banco de dados</span><span class="sxs-lookup"><span data-stu-id="e816c-207">Example: Bulk importing data into a database program</span></span>
<span data-ttu-id="e816c-208">Abaixo está um exemplo de um procedimento armazenado que é gravado toobulk importar documentos em uma coleção.</span><span class="sxs-lookup"><span data-stu-id="e816c-208">Below is an example of a stored procedure that is written toobulk-import documents into a collection.</span></span> <span data-ttu-id="e816c-209">Observe como Olá armazenadas a execução do procedimento identificadores limitados verificando Olá booliano retornar o valor de createDocument e, em seguida, usa Olá contagem de documentos inseridos em cada invocação Olá armazenado procedimento tootrack e retomar o progresso em lotes.</span><span class="sxs-lookup"><span data-stu-id="e816c-209">Note how hello stored procedure handles bounded execution by checking hello Boolean return value from createDocument, and then uses hello count of documents inserted in each invocation of hello stored procedure tootrack and resume progress across batches.</span></span>

    function bulkImport(docs) {
        var collection = getContext().getCollection();
        var collectionLink = collection.getSelfLink();

        // hello count of imported docs, also used as current doc index.
        var count = 0;

        // Validate input.
        if (!docs) throw new Error("hello array is undefined or null.");

        var docsLength = docs.length;
        if (docsLength == 0) {
            getContext().getResponse().setBody(0);
        }

        // Call hello create API toocreate a document.
        tryCreate(docs[count], callback);

        // Note that there are 2 exit conditions:
        // 1) hello createDocument request was not accepted. 
        //    In this case hello callback will not be called, we just call setBody and we are done.
        // 2) hello callback was called docs.length times.
        //    In this case all documents were created and we don’t need toocall tryCreate anymore. Just call setBody and we are done.
        function tryCreate(doc, callback) {
            var isAccepted = collection.createDocument(collectionLink, doc, callback);

            // If hello request was accepted, callback will be called.
            // Otherwise report current count back toohello client, 
            // which will call hello script again with remaining set of docs.
            if (!isAccepted) getContext().getResponse().setBody(count);
        }

        // This is called when collection.createDocument is done in order tooprocess hello result.
        function callback(err, doc, options) {
            if (err) throw err;

            // One more document has been inserted, increment hello count.
            count++;

            if (count >= docsLength) {
                // If we created all documents, we are done. Just set hello response.
                getContext().getResponse().setBody(count);
            } else {
                // Create next document.
                tryCreate(docs[count], callback);
            }
        }
    }

## <span data-ttu-id="e816c-210"><a id="trigger"></a> Gatilhos de banco de dados</span><span class="sxs-lookup"><span data-stu-id="e816c-210"><a id="trigger"></a> Database triggers</span></span>
### <a name="database-pre-triggers"></a><span data-ttu-id="e816c-211">Pré-gatilhos de banco de dados</span><span class="sxs-lookup"><span data-stu-id="e816c-211">Database pre-triggers</span></span>
<span data-ttu-id="e816c-212">O Cosmos DB oferece gatilhos que são executados ou disparados por uma operação em um documento.</span><span class="sxs-lookup"><span data-stu-id="e816c-212">Cosmos DB provides triggers that are executed or triggered by an operation on a document.</span></span> <span data-ttu-id="e816c-213">Por exemplo, você pode especificar um pré-gatilho de quando você estiver criando um documento – esse pré-gatilho será executado antes que o documento hello é criado.</span><span class="sxs-lookup"><span data-stu-id="e816c-213">For example, you can specify a pre-trigger when you are creating a document – this pre-trigger will run before hello document is created.</span></span> <span data-ttu-id="e816c-214">a seguir Olá é um exemplo de como pré-gatilhos podem ser usado toovalidate Olá propriedades de um documento que está sendo criado:</span><span class="sxs-lookup"><span data-stu-id="e816c-214">hello following is an example of how pre-triggers can be used toovalidate hello properties of a document that is being created:</span></span>

    var validateDocumentContentsTrigger = {
        id: "validateDocumentContents",
        serverScript: function validate() {
            var context = getContext();
            var request = context.getRequest();

            // document toobe created in hello current operation
            var documentToCreate = request.getBody();

            // validate properties
            if (!("timestamp" in documentToCreate)) {
                var ts = new Date();
                documentToCreate["my timestamp"] = ts.getTime();
            }

            // update hello document that will be created
            request.setBody(documentToCreate);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.Create
    }


<span data-ttu-id="e816c-215">E Olá código de registro de cliente Node. js correspondente para o disparador hello:</span><span class="sxs-lookup"><span data-stu-id="e816c-215">And hello corresponding Node.js client-side registration code for hello trigger:</span></span>

    // register pre-trigger
    client.createTriggerAsync(collection.self, validateDocumentContentsTrigger)
        .then(function (response) {
            console.log("Created", response.resource);
            var docToCreate = {
                id: "DocWithTrigger",
                event: "Error",
                source: "Network outage"
            };

            // run trigger while creating above document 
            var options = { preTriggerInclude: "validateDocumentContents" };

            return client.createDocumentAsync(collection.self,
                  docToCreate, options);
        }, function (error) {
            console.log("Error", error);
        })
    .then(function (response) {
        console.log(response.resource); // document with timestamp property added
    }, function (error) {
        console.log("Error", error);
    });


<span data-ttu-id="e816c-216">Pré-gatilhos não podem ter parâmetros de entrada.</span><span class="sxs-lookup"><span data-stu-id="e816c-216">Pre-triggers cannot have any input parameters.</span></span> <span data-ttu-id="e816c-217">o objeto de solicitação Olá pode ser usado toomanipulate mensagem de solicitação de Olá associada à operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e816c-217">hello request object can be used toomanipulate hello request message associated with hello operation.</span></span> <span data-ttu-id="e816c-218">Aqui, pré-gatilho hello está sendo executado com a criação de um documento hello e corpo de mensagem de solicitação de saudação contém Olá documento toobe criado no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="e816c-218">Here, hello pre-trigger is being run with hello creation of a document, and hello request message body contains hello document toobe created in JSON format.</span></span>   

<span data-ttu-id="e816c-219">Quando os gatilhos são registrados, os usuários podem especificar operações Olá que podem ser executados com.</span><span class="sxs-lookup"><span data-stu-id="e816c-219">When triggers are registered, users can specify hello operations that it can run with.</span></span> <span data-ttu-id="e816c-220">Esse gatilho foi criado com TriggerOperation.Create, o que significa o seguinte Olá não é permitido.</span><span class="sxs-lookup"><span data-stu-id="e816c-220">This trigger was created with TriggerOperation.Create, which means hello following is not permitted.</span></span>

    var options = { preTriggerInclude: "validateDocumentContents" };

    client.replaceDocumentAsync(docToReplace.self,
                  newDocBody, options)
    .then(function (response) {
        console.log(response.resource);
    }, function (error) {
        console.log("Error", error);
    });

    // Fails, can’t use a create trigger in a replace operation

### <a name="database-post-triggers"></a><span data-ttu-id="e816c-221">Pós-gatilhos de banco de dados</span><span class="sxs-lookup"><span data-stu-id="e816c-221">Database post-triggers</span></span>
<span data-ttu-id="e816c-222">Pós-gatilhos, assim como pré-gatilhos, são associados a uma operação em um documento e não assumem parâmetros de entrada.</span><span class="sxs-lookup"><span data-stu-id="e816c-222">Post-triggers, like pre-triggers, are associated with an operation on a document and don’t take any input parameters.</span></span> <span data-ttu-id="e816c-223">Eles são executados **depois** Olá operação foi concluída e ter acesso toohello resposta mensagem enviada toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="e816c-223">They run **after** hello operation has completed, and have access toohello response message that is sent toohello client.</span></span>   

<span data-ttu-id="e816c-224">saudação de exemplo a seguir mostra pós-gatilhos em ação:</span><span class="sxs-lookup"><span data-stu-id="e816c-224">hello following example shows post-triggers in action:</span></span>

    var updateMetadataTrigger = {
        id: "updateMetadata",
        serverScript: function updateMetadata() {
            var context = getContext();
            var collection = context.getCollection();
            var response = context.getResponse();

            // document that was created
            var createdDocument = response.getBody();

            // query for metadata document
            var filterQuery = 'SELECT * FROM root r WHERE r.id = "_metadata"';
            var accept = collection.queryDocuments(collection.getSelfLink(), filterQuery,
                updateMetadataCallback);
            if(!accept) throw "Unable tooupdate metadata, abort";

            function updateMetadataCallback(err, documents, responseOptions) {
                if(err) throw new Error("Error" + err.message);
                         if(documents.length != 1) throw 'Unable toofind metadata document';

                         var metadataDocument = documents[0];

                         // update metadata
                         metadataDocument.createdDocuments += 1;
                         metadataDocument.createdNames += " " + createdDocument.id;
                         var accept = collection.replaceDocument(metadataDocument._self,
                               metadataDocument, function(err, docReplaced) {
                                      if(err) throw "Unable tooupdate metadata, abort";
                               });
                         if(!accept) throw "Unable tooupdate metadata, abort";
                         return;                    
            }                                                                                            
        },
        triggerType: TriggerType.Post,
        triggerOperation: TriggerOperation.All
    }


<span data-ttu-id="e816c-225">gatilho Olá pode ser registrado como mostrado na saudação de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="e816c-225">hello trigger can be registered as shown in hello following sample.</span></span>

    // register post-trigger
    client.createTriggerAsync('dbs/testdb/colls/testColl', updateMetadataTrigger)
        .then(function(createdTrigger) { 
            var docToCreate = { 
                name: "artist_profile_1023",
                artist: "hello Band",
                albums: ["Hellujah", "Rotators", "Spinning Top"]
            };

            // run trigger while creating above document 
            var options = { postTriggerInclude: "updateMetadata" };

            return client.createDocumentAsync(collection.self,
                  docToCreate, options);
        }, function(error) {
            console.log("Error" , error);
        })
    .then(function(response) {
        console.log(response.resource); 
    }, function(error) {
        console.log("Error" , error);
    });


<span data-ttu-id="e816c-226">Esse gatilho consultas para o documento de metadados hello e atualiza com detalhes sobre documento hello recém-criado.</span><span class="sxs-lookup"><span data-stu-id="e816c-226">This trigger queries for hello metadata document and updates it with details about hello newly created document.</span></span>  

<span data-ttu-id="e816c-227">Uma coisa importante toonote é hello **transacional** execução de gatilhos no banco de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="e816c-227">One thing that is important toonote is hello **transactional** execution of triggers in Cosmos DB.</span></span> <span data-ttu-id="e816c-228">Esse pós-gatilho executado como parte da saudação mesma transação como a criação de saudação do documento original hello.</span><span class="sxs-lookup"><span data-stu-id="e816c-228">This post-trigger runs as part of hello same transaction as hello creation of hello original document.</span></span> <span data-ttu-id="e816c-229">Portanto, se podemos lançar uma exceção de pós-gatilho de Olá (digamos se estamos documento de metadados não é possível tooupdate Olá), toda a transação Olá falhará e ser revertida.</span><span class="sxs-lookup"><span data-stu-id="e816c-229">Therefore, if we throw an exception from hello post-trigger (say if we are unable tooupdate hello metadata document), hello whole transaction will fail and be rolled back.</span></span> <span data-ttu-id="e816c-230">Nenhum documento será criado e uma exceção será retornada.</span><span class="sxs-lookup"><span data-stu-id="e816c-230">No document will be created, and an exception will be returned.</span></span>  

## <span data-ttu-id="e816c-231"><a id="udf"></a>Funções definidas pelo usuário</span><span class="sxs-lookup"><span data-stu-id="e816c-231"><a id="udf"></a>User-defined functions</span></span>
<span data-ttu-id="e816c-232">Funções definidas pelo usuário (UDFs) são gramática da linguagem de consulta SQL do DocumentDB API tooextend usado hello e implementam a lógica de negócios personalizada.</span><span class="sxs-lookup"><span data-stu-id="e816c-232">User-defined functions (UDFs) are used tooextend hello DocumentDB API SQL query language grammar and implement custom business logic.</span></span> <span data-ttu-id="e816c-233">Elas podem ser invocadas somente de dentro das consultas.</span><span class="sxs-lookup"><span data-stu-id="e816c-233">They can only be called from inside queries.</span></span> <span data-ttu-id="e816c-234">Eles não possuem o objeto de contexto de toohello de acesso e destinam-se toobe usado como o JavaScript somente computação.</span><span class="sxs-lookup"><span data-stu-id="e816c-234">They do not have access toohello context object and are meant toobe used as compute-only JavaScript.</span></span> <span data-ttu-id="e816c-235">Portanto, UDFs podem ser executadas em réplicas secundárias de saudação serviço de banco de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="e816c-235">Therefore, UDFs can be run on secondary replicas of hello Cosmos DB service.</span></span>  

<span data-ttu-id="e816c-236">Hello exemplo a seguir cria um imposto de renda UDF toocalculate com base em taxas de vários colchetes de renda e, em seguida, usa-lo dentro de uma consulta toofind todas as pessoas que paga mais de US $20.000 impostos.</span><span class="sxs-lookup"><span data-stu-id="e816c-236">hello following sample creates a UDF toocalculate income tax based on rates for various income brackets, and then uses it inside a query toofind all people who paid more than $20,000 in taxes.</span></span>

    var taxUdf = {
        id: "tax",
        serverScript: function tax(income) {

            if(income == undefined) 
                throw 'no input';

            if (income < 1000) 
                return income * 0.1;
            else if (income < 10000) 
                return income * 0.2;
            else
                return income * 0.4;
        }
    }


<span data-ttu-id="e816c-237">Olá UDF subsequentemente pode ser usado em consultas como Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="e816c-237">hello UDF can subsequently be used in queries like in hello following sample:</span></span>

    // register UDF
    client.createUserDefinedFunctionAsync('dbs/testdb/colls/testColl', taxUdf)
        .then(function(response) { 
            console.log("Created", response.resource);

            var query = 'SELECT * FROM TaxPayers t WHERE udf.tax(t.income) > 20000'; 
            return client.queryDocuments('dbs/testdb/colls/testColl',
                   query).toArrayAsync();
        }, function(error) {
            console.log("Error" , error);
        })
    .then(function(response) {
        var documents = response.feed;
        console.log(response.resource); 
    }, function(error) {
        console.log("Error" , error);
    });

## <a name="javascript-language-integrated-query-api"></a><span data-ttu-id="e816c-238">API de consulta integrada da linguagem JavaScript</span><span class="sxs-lookup"><span data-stu-id="e816c-238">JavaScript language-integrated query API</span></span>
<span data-ttu-id="e816c-239">Além disso tooissuing consultas usando a gramática SQL do DocumentDB, hello SDK do lado do servidor permitem que você tooperform otimizada de consultas usando uma interface JavaScript fluente sem qualquer conhecimento de SQL.</span><span class="sxs-lookup"><span data-stu-id="e816c-239">In addition tooissuing queries using DocumentDB’s SQL grammar, hello server-side SDK allows you tooperform optimized queries using a fluent JavaScript interface without any knowledge of SQL.</span></span> <span data-ttu-id="e816c-240">consulta de JavaScript Olá que API permite consultas de compilação tooprogrammatically passando funções de predicado em função encadeável chama com do tooECMAScript5 familiar uma sintaxe internos de matriz e bibliotecas JavaScript populares como lodash.</span><span class="sxs-lookup"><span data-stu-id="e816c-240">hello JavaScript query API allows you tooprogrammatically build queries by passing predicate functions into chainable function calls, with a syntax familiar tooECMAScript5's Array built-ins and popular JavaScript libraries like lodash.</span></span> <span data-ttu-id="e816c-241">Consultas são analisadas pelo Olá toobe de tempo de execução de JavaScript executado com eficiência usando índices do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e816c-241">Queries are parsed by hello JavaScript runtime toobe executed efficiently using Azure Cosmos DB’s indices.</span></span>

> [!NOTE]
> <span data-ttu-id="e816c-242">`__`(sublinhado duplo) é um alias muito`getContext().getCollection()`.</span><span class="sxs-lookup"><span data-stu-id="e816c-242">`__` (double-underscore) is an alias too`getContext().getCollection()`.</span></span>
> <br/>
> <span data-ttu-id="e816c-243">Em outras palavras, você pode usar `__` ou `getContext().getCollection()` tooaccess Olá API de consulta do JavaScript.</span><span class="sxs-lookup"><span data-stu-id="e816c-243">In other words, you can use `__` or `getContext().getCollection()` tooaccess hello JavaScript query API.</span></span>
> 
> 

<span data-ttu-id="e816c-244">As funções permitidas incluem:</span><span class="sxs-lookup"><span data-stu-id="e816c-244">Supported functions include:</span></span>

<ul>
<li><span data-ttu-id="e816c-245">
<b>chain() ... .value([callback] [, opções])</b>
</span><span class="sxs-lookup"><span data-stu-id="e816c-245">
<b>chain() ... .value([callback] [, options])</b>
</span></span><ul>
<li>
<span data-ttu-id="e816c-246">Inicia uma chamada encadeada que deve ser terminada com value().</span><span class="sxs-lookup"><span data-stu-id="e816c-246">Starts a chained call which must be terminated with value().</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="e816c-247">
<b>filter(predicateFunction [, opções] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="e816c-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="e816c-248">Filtra hello usando uma função de predicado que retorna true/false na ordem toofilter in/out de documentos de entrada no conjunto resultante da saudação de entrada.</span><span class="sxs-lookup"><span data-stu-id="e816c-248">Filters hello input using a predicate function which returns true/false in order toofilter in/out input documents into hello resulting set.</span></span> <span data-ttu-id="e816c-249">Isso se comporta semelhante tooa cláusula WHERE no SQL.</span><span class="sxs-lookup"><span data-stu-id="e816c-249">This behaves similar tooa WHERE clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="e816c-250">
<b>map(transformationFunction [, opções] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="e816c-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="e816c-251">Aplica uma projeção recebe uma função de transformação que mapeia cada valor ou objeto do item de entrada tooa JavaScript.</span><span class="sxs-lookup"><span data-stu-id="e816c-251">Applies a projection given a transformation function which maps each input item tooa JavaScript object or value.</span></span> <span data-ttu-id="e816c-252">Isso se comporta semelhante cláusula SELECT de tooa em SQL.</span><span class="sxs-lookup"><span data-stu-id="e816c-252">This behaves similar tooa SELECT clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="e816c-253">
<b>pluck([propertyName] [, opções] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="e816c-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="e816c-254">Esse é um atalho para um mapa que extrai o valor de saudação de uma única propriedade de cada item de entrada.</span><span class="sxs-lookup"><span data-stu-id="e816c-254">This is a shortcut for a map which extracts hello value of a single property from each input item.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="e816c-255">
<b>flatten([isShallow] [, opções] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="e816c-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="e816c-256">Combina e mescla as matrizes de cada item na matriz de tooa única de entrada.</span><span class="sxs-lookup"><span data-stu-id="e816c-256">Combines and flattens arrays from each input item in tooa single array.</span></span> <span data-ttu-id="e816c-257">Isso se comporta semelhante tooSelectMany em LINQ.</span><span class="sxs-lookup"><span data-stu-id="e816c-257">This behaves similar tooSelectMany in LINQ.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="e816c-258">
<b>sortBy([predicate] [, opções] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="e816c-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="e816c-259">Gerar um novo conjunto de documentos classificando documentos Olá no fluxo de documento de entrada hello em ordem crescente utilizando Olá fornecido predicado.</span><span class="sxs-lookup"><span data-stu-id="e816c-259">Produce a new set of documents by sorting hello documents in hello input document stream in ascending order using hello given predicate.</span></span> <span data-ttu-id="e816c-260">Isso se comporta semelhante tooa cláusula ORDER BY em SQL.</span><span class="sxs-lookup"><span data-stu-id="e816c-260">This behaves similar tooa ORDER BY clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="e816c-261">
<b>sortByDescending([predicate] [, opções] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="e816c-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="e816c-262">Gerar um novo conjunto de documentos classificando documentos Olá no fluxo de documento de entrada hello em ordem decrescente usando Olá fornecido predicado.</span><span class="sxs-lookup"><span data-stu-id="e816c-262">Produce a new set of documents by sorting hello documents in hello input document stream in descending order using hello given predicate.</span></span> <span data-ttu-id="e816c-263">Isso se comporta semelhante cláusula de ORDER BY x DESC tooa no SQL.</span><span class="sxs-lookup"><span data-stu-id="e816c-263">This behaves similar tooa ORDER BY x DESC clause in SQL.</span></span>
</li>
</ul>
</li>
</ul>


<span data-ttu-id="e816c-264">Quando incluído dentro de funções de predicado e/ou seletor, hello seguintes construções de JavaScript obtém automaticamente otimizada toorun diretamente no banco de dados do Azure Cosmos índices:</span><span class="sxs-lookup"><span data-stu-id="e816c-264">When included inside predicate and/or selector functions, hello following JavaScript constructs get automatically optimized toorun directly on Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="e816c-265">Operadores simples: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span><span class="sxs-lookup"><span data-stu-id="e816c-265">Simple operators: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span></span> ~
* <span data-ttu-id="e816c-266">Literais, incluindo o literal de objeto Olá: {}</span><span class="sxs-lookup"><span data-stu-id="e816c-266">Literals, including hello object literal: {}</span></span>
* <span data-ttu-id="e816c-267">var, return</span><span class="sxs-lookup"><span data-stu-id="e816c-267">var, return</span></span>

<span data-ttu-id="e816c-268">Olá JavaScript seguinte construções não obter otimizado para índices de banco de dados do Azure Cosmos:</span><span class="sxs-lookup"><span data-stu-id="e816c-268">hello following JavaScript constructs do not get optimized for Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="e816c-269">Fluxo de controle (por exemplo,. if, for, while)</span><span class="sxs-lookup"><span data-stu-id="e816c-269">Control flow (e.g. if, for, while)</span></span>
* <span data-ttu-id="e816c-270">Chamadas de função</span><span class="sxs-lookup"><span data-stu-id="e816c-270">Function calls</span></span>

<span data-ttu-id="e816c-271">Para saber mais, consulte nossos [JSDocs no servidor](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="e816c-271">For more information, please see our [Server-Side JSDocs](http://azure.github.io/azure-documentdb-js-server/).</span></span>

### <a name="example-write-a-stored-procedure-using-hello-javascript-query-api"></a><span data-ttu-id="e816c-272">Exemplo: Gravar um procedimento armazenado usando a API de consulta Olá JavaScript</span><span class="sxs-lookup"><span data-stu-id="e816c-272">Example: Write a stored procedure using hello JavaScript query API</span></span>
<span data-ttu-id="e816c-273">saudação de exemplo de código a seguir é um exemplo de como Olá JavaScript consulta API pode ser usada no contexto de saudação de um procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="e816c-273">hello following code sample is an example of how hello JavaScript Query API can be used in hello context of a stored procedure.</span></span> <span data-ttu-id="e816c-274">Olá procedimento armazenado insere um documento, fornecido por um parâmetro de entrada e atualiza um documento de metadados usando Olá `__.filter()` método com minSize, maxSize e totalSize com base na propriedade de tamanho do documento hello entrada.</span><span class="sxs-lookup"><span data-stu-id="e816c-274">hello stored procedure inserts a document, given by an input parameter, and updates a metadata document, using hello `__.filter()` method, with minSize, maxSize, and totalSize based upon hello input document's size property.</span></span>

    /**
     * Insert actual doc and update metadata doc: minSize, maxSize, totalSize based on doc.size.
     */
    function insertDocumentAndUpdateMetadata(doc) {
      // HTTP error codes sent tooour callback funciton by DocDB server.
      var ErrorCode = {
        RETRY_WITH: 449,
      }

      var isAccepted = __.createDocument(__.getSelfLink(), doc, {}, function(err, doc, options) {
        if (err) throw err;

        // Check hello doc (ignore docs with invalid/zero size and metaDoc itself) and call updateMetadata.
        if (!doc.isMetadata && doc.size > 0) {
          // Get hello meta document. We keep it in hello same collection. it's hello only doc that has .isMetadata = true.
          var result = __.filter(function(x) {
            return x.isMetadata === true
          }, function(err, feed, options) {
            if (err) throw err;

            // We assume that metadata doc was pre-created and must exist when this script is called.
            if (!feed || !feed.length) throw new Error("Failed toofind hello metadata document.");

            // hello metadata document.
            var metaDoc = feed[0];

            // Update metaDoc.minSize:
            // for 1st document use doc.Size, for all hello rest see if it's less than last min.
            if (metaDoc.minSize == 0) metaDoc.minSize = doc.size;
            else metaDoc.minSize = Math.min(metaDoc.minSize, doc.size);

            // Update metaDoc.maxSize.
            metaDoc.maxSize = Math.max(metaDoc.maxSize, doc.size);

            // Update metaDoc.totalSize.
            metaDoc.totalSize += doc.size;

            // Update/replace hello metadata document in hello store.
            var isAccepted = __.replaceDocument(metaDoc._self, metaDoc, function(err) {
              if (err) throw err;
              // Note: in case concurrent updates causes conflict with ErrorCode.RETRY_WITH, we can't read hello meta again 
              //       and update again because due tooSnapshot isolation we will read same exact version (we are in same transaction).
              //       We have tootake care of that on hello client side.
            });
            if (!isAccepted) throw new Error("replaceDocument(metaDoc) returned false.");
          });
          if (!result.isAccepted) throw new Error("filter for metaDoc returned false.");
        }
      });
      if (!isAccepted) throw new Error("createDocument(actual doc) returned false.");
    }

## <a name="sql-toojavascript-cheat-sheet"></a><span data-ttu-id="e816c-275">Roteiro de tooJavascript SQL</span><span class="sxs-lookup"><span data-stu-id="e816c-275">SQL tooJavascript cheat sheet</span></span>
<span data-ttu-id="e816c-276">Olá tabela a seguir apresenta várias consultas SQL e consultas de JavaScript correspondentes hello.</span><span class="sxs-lookup"><span data-stu-id="e816c-276">hello following table presents various SQL queries and hello corresponding JavaScript queries.</span></span>

<span data-ttu-id="e816c-277">Assim como acontece com consultas SQL, as chaves de propriedade do documento (por exemplo, `doc.id`) diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="e816c-277">As with SQL queries, document property keys (e.g. `doc.id`) are case-sensitive.</span></span>

|<span data-ttu-id="e816c-278">SQL</span><span class="sxs-lookup"><span data-stu-id="e816c-278">SQL</span></span>| <span data-ttu-id="e816c-279">API de consulta do JavaScript</span><span class="sxs-lookup"><span data-stu-id="e816c-279">JavaScript Query API</span></span>|<span data-ttu-id="e816c-280">Descrição abaixo</span><span class="sxs-lookup"><span data-stu-id="e816c-280">Description below</span></span>|
|---|---|---|
|<span data-ttu-id="e816c-281">SELECIONAR *</span><span class="sxs-lookup"><span data-stu-id="e816c-281">SELECT *</span></span><br><span data-ttu-id="e816c-282">FROM docs</span><span class="sxs-lookup"><span data-stu-id="e816c-282">FROM docs</span></span>| <span data-ttu-id="e816c-283">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="e816c-283">__.map(function(doc) {</span></span> <br><span data-ttu-id="e816c-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span><span class="sxs-lookup"><span data-stu-id="e816c-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span></span><br><span data-ttu-id="e816c-285">});</span><span class="sxs-lookup"><span data-stu-id="e816c-285">});</span></span>|<span data-ttu-id="e816c-286">1</span><span class="sxs-lookup"><span data-stu-id="e816c-286">1</span></span>|
|<span data-ttu-id="e816c-287">SELECT docs.id, docs.message AS msg, docs.actions</span><span class="sxs-lookup"><span data-stu-id="e816c-287">SELECT docs.id, docs.message AS msg, docs.actions</span></span> <br><span data-ttu-id="e816c-288">FROM docs</span><span class="sxs-lookup"><span data-stu-id="e816c-288">FROM docs</span></span>|<span data-ttu-id="e816c-289">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="e816c-289">__.map(function(doc) {</span></span><br><span data-ttu-id="e816c-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="e816c-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="e816c-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="e816c-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="e816c-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span><span class="sxs-lookup"><span data-stu-id="e816c-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span></span><br><span data-ttu-id="e816c-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span><span class="sxs-lookup"><span data-stu-id="e816c-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span></span><br><span data-ttu-id="e816c-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="e816c-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="e816c-295">});</span><span class="sxs-lookup"><span data-stu-id="e816c-295">});</span></span>|<span data-ttu-id="e816c-296">2</span><span class="sxs-lookup"><span data-stu-id="e816c-296">2</span></span>|
|<span data-ttu-id="e816c-297">SELECIONAR *</span><span class="sxs-lookup"><span data-stu-id="e816c-297">SELECT *</span></span><br><span data-ttu-id="e816c-298">FROM docs</span><span class="sxs-lookup"><span data-stu-id="e816c-298">FROM docs</span></span><br><span data-ttu-id="e816c-299">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="e816c-299">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="e816c-300">__.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="e816c-300">__.filter(function(doc) {</span></span><br><span data-ttu-id="e816c-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="e816c-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="e816c-302">});</span><span class="sxs-lookup"><span data-stu-id="e816c-302">});</span></span>|<span data-ttu-id="e816c-303">3</span><span class="sxs-lookup"><span data-stu-id="e816c-303">3</span></span>|
|<span data-ttu-id="e816c-304">SELECIONAR *</span><span class="sxs-lookup"><span data-stu-id="e816c-304">SELECT *</span></span><br><span data-ttu-id="e816c-305">FROM docs</span><span class="sxs-lookup"><span data-stu-id="e816c-305">FROM docs</span></span><br><span data-ttu-id="e816c-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span><span class="sxs-lookup"><span data-stu-id="e816c-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span></span>|<span data-ttu-id="e816c-307">__.filter(function(x) {</span><span class="sxs-lookup"><span data-stu-id="e816c-307">__.filter(function(x) {</span></span><br><span data-ttu-id="e816c-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span><span class="sxs-lookup"><span data-stu-id="e816c-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span></span><br><span data-ttu-id="e816c-309">});</span><span class="sxs-lookup"><span data-stu-id="e816c-309">});</span></span>|<span data-ttu-id="e816c-310">4</span><span class="sxs-lookup"><span data-stu-id="e816c-310">4</span></span>|
|<span data-ttu-id="e816c-311">SELECT docs.id, docs.message AS msg</span><span class="sxs-lookup"><span data-stu-id="e816c-311">SELECT docs.id, docs.message AS msg</span></span><br><span data-ttu-id="e816c-312">FROM docs</span><span class="sxs-lookup"><span data-stu-id="e816c-312">FROM docs</span></span><br><span data-ttu-id="e816c-313">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="e816c-313">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="e816c-314">__.chain()</span><span class="sxs-lookup"><span data-stu-id="e816c-314">__.chain()</span></span><br><span data-ttu-id="e816c-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="e816c-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="e816c-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="e816c-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="e816c-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="e816c-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="e816c-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="e816c-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span></span><br><span data-ttu-id="e816c-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="e816c-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="e816c-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="e816c-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="e816c-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span><span class="sxs-lookup"><span data-stu-id="e816c-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span></span><br><span data-ttu-id="e816c-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="e816c-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="e816c-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="e816c-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="e816c-324">.value();</span><span class="sxs-lookup"><span data-stu-id="e816c-324">.value();</span></span>|<span data-ttu-id="e816c-325">5</span><span class="sxs-lookup"><span data-stu-id="e816c-325">5</span></span>|
|<span data-ttu-id="e816c-326">SELECT VALUE tag</span><span class="sxs-lookup"><span data-stu-id="e816c-326">SELECT VALUE tag</span></span><br><span data-ttu-id="e816c-327">FROM docs</span><span class="sxs-lookup"><span data-stu-id="e816c-327">FROM docs</span></span><br><span data-ttu-id="e816c-328">JOIN tag IN docs.Tags</span><span class="sxs-lookup"><span data-stu-id="e816c-328">JOIN tag IN docs.Tags</span></span><br><span data-ttu-id="e816c-329">ORDER BY docs._ts</span><span class="sxs-lookup"><span data-stu-id="e816c-329">ORDER BY docs._ts</span></span>|<span data-ttu-id="e816c-330">__.chain()</span><span class="sxs-lookup"><span data-stu-id="e816c-330">__.chain()</span></span><br><span data-ttu-id="e816c-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="e816c-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="e816c-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span><span class="sxs-lookup"><span data-stu-id="e816c-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span></span><br><span data-ttu-id="e816c-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="e816c-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="e816c-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="e816c-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span></span><br><span data-ttu-id="e816c-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span><span class="sxs-lookup"><span data-stu-id="e816c-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span></span><br><span data-ttu-id="e816c-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="e816c-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="e816c-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span><span class="sxs-lookup"><span data-stu-id="e816c-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span></span><br><span data-ttu-id="e816c-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span><span class="sxs-lookup"><span data-stu-id="e816c-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span></span><br><span data-ttu-id="e816c-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span><span class="sxs-lookup"><span data-stu-id="e816c-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span></span>|<span data-ttu-id="e816c-340">6</span><span class="sxs-lookup"><span data-stu-id="e816c-340">6</span></span>|

<span data-ttu-id="e816c-341">Olá, descrições a seguir explicam cada consulta na tabela de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="e816c-341">hello following descriptions explain each query in hello table above.</span></span>
1. <span data-ttu-id="e816c-342">Resulta em todos os documentos (paginados com token de continuação) no estado em que se encontram.</span><span class="sxs-lookup"><span data-stu-id="e816c-342">Results in all documents (paginated with continuation token) as is.</span></span>
2. <span data-ttu-id="e816c-343">Projetos Olá id, a mensagem (alias toomsg) e a ação de todos os documentos.</span><span class="sxs-lookup"><span data-stu-id="e816c-343">Projects hello id, message (aliased toomsg), and action from all documents.</span></span>
3. <span data-ttu-id="e816c-344">Consultas em documentos com predicado de saudação: id = "X998_Y998".</span><span class="sxs-lookup"><span data-stu-id="e816c-344">Queries for documents with hello predicate: id = "X998_Y998".</span></span>
4. <span data-ttu-id="e816c-345">Consultas para documentos que têm uma propriedade de marcas e marcas é uma matriz que contém o valor de saudação 123.</span><span class="sxs-lookup"><span data-stu-id="e816c-345">Queries for documents that have a Tags property and Tags is an array containing hello value 123.</span></span>
5. <span data-ttu-id="e816c-346">Consultas em documentos com um predicado, id = "X998_Y998" e, em seguida, id de saudação de projetos e (alias toomsg) da mensagem.</span><span class="sxs-lookup"><span data-stu-id="e816c-346">Queries for documents with a predicate, id = "X998_Y998", and then projects hello id and message (aliased toomsg).</span></span>
6. <span data-ttu-id="e816c-347">Filtros para documentos que têm uma propriedade de matriz, marcas, e classifica documentos resultantes Olá pela propriedade de sistema de carimbo de hora de TS Olá e, em seguida, projetos + mescla a matriz de marcas de saudação.</span><span class="sxs-lookup"><span data-stu-id="e816c-347">Filters for documents which have an array property, Tags, and sorts hello resulting documents by hello _ts timestamp system property, and then projects + flattens hello Tags array.</span></span>


## <a name="runtime-support"></a><span data-ttu-id="e816c-348">Suporte de tempo de execução</span><span class="sxs-lookup"><span data-stu-id="e816c-348">Runtime support</span></span>
<span data-ttu-id="e816c-349">[API de servidor JavaScript do DocumentDB](http://azure.github.io/azure-documentdb-js-server/) fornece suporte para Olá a maioria das Olá principais recursos de linguagem JavaScript como padronizado pelo [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span><span class="sxs-lookup"><span data-stu-id="e816c-349">[DocumentDB JavaScript server side API](http://azure.github.io/azure-documentdb-js-server/) provides support for hello most of hello mainstream JavaScript language features as standardized by [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span></span>

### <a name="security"></a><span data-ttu-id="e816c-350">Segurança</span><span class="sxs-lookup"><span data-stu-id="e816c-350">Security</span></span>
<span data-ttu-id="e816c-351">JavaScript de procedimentos armazenados e gatilhos são em modo seguro para que os efeitos de saudação de um script não apresentam vazamento toohello outros sem passar pelo isolamento de transação de instantâneo Olá no nível de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e816c-351">JavaScript stored procedures and triggers are sandboxed so that hello effects of one script do not leak toohello other without going through hello snapshot transaction isolation at hello database level.</span></span> <span data-ttu-id="e816c-352">ambientes de tempo de execução de saudação são reunidos mas limpo do contexto de saudação após cada execução.</span><span class="sxs-lookup"><span data-stu-id="e816c-352">hello runtime environments are pooled but cleaned of hello context after each run.</span></span> <span data-ttu-id="e816c-353">Portanto, eles não têm garantia toobe seguro de efeitos colaterais não intencionais uns dos outros.</span><span class="sxs-lookup"><span data-stu-id="e816c-353">Hence they are guaranteed toobe safe of any unintended side effects from each other.</span></span>

### <a name="pre-compilation"></a><span data-ttu-id="e816c-354">Pré-compilação</span><span class="sxs-lookup"><span data-stu-id="e816c-354">Pre-compilation</span></span>
<span data-ttu-id="e816c-355">Procedimentos armazenados, gatilhos e UDFs são implicitamente pré-compilado toohello formato de código de bytes no custo da compilação ordem tooavoid na hora Olá cada invocação do script.</span><span class="sxs-lookup"><span data-stu-id="e816c-355">Stored procedures, triggers and UDFs are implicitly precompiled toohello byte code format in order tooavoid compilation cost at hello time of each script invocation.</span></span> <span data-ttu-id="e816c-356">Isso assegura que as invocações dos procedimentos armazenados sejam rápidas e possuam baixa pegada.</span><span class="sxs-lookup"><span data-stu-id="e816c-356">This ensures invocations of stored procedures are fast and have a low footprint.</span></span>

## <a name="client-sdk-support"></a><span data-ttu-id="e816c-357">Suporte de SDK de cliente</span><span class="sxs-lookup"><span data-stu-id="e816c-357">Client SDK support</span></span>
<span data-ttu-id="e816c-358">Em adição toohello API DocumentDB para [Node.js](documentdb-sdk-node.md) tem de cliente, o banco de dados do Azure Cosmos [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [ JavaScript](http://azure.github.io/azure-documentdb-js/), e [Python SDKs](documentdb-sdk-python.md) para Olá API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="e816c-358">In addition toohello DocumentDB API for [Node.js](documentdb-sdk-node.md) client, Azure Cosmos DB has [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [JavaScript](http://azure.github.io/azure-documentdb-js/), and [Python SDKs](documentdb-sdk-python.md) for hello DocumentDB API.</span></span> <span data-ttu-id="e816c-359">Os procedimentos armazenados, gatilhos e UDFs também podem ser criados e executados usando qualquer um desses SDKs.</span><span class="sxs-lookup"><span data-stu-id="e816c-359">Stored procedures, triggers and UDFs can be created and executed using any of these SDKs as well.</span></span> <span data-ttu-id="e816c-360">Olá mostrado no exemplo a seguir como toocreate e executar um procedimento armazenado usando o cliente do .NET hello.</span><span class="sxs-lookup"><span data-stu-id="e816c-360">hello following example shows how toocreate and execute a stored procedure using hello .NET client.</span></span> <span data-ttu-id="e816c-361">Observe como tipos de .NET Olá são passados em Olá procedimento armazenado como JSON e leia novamente.</span><span class="sxs-lookup"><span data-stu-id="e816c-361">Note how hello .NET types are passed into hello stored procedure as JSON and read back.</span></span>

    var markAntiquesSproc = new StoredProcedure
    {
        Id = "ValidateDocumentAge",
        Body = @"
                function(docToCreate, antiqueYear) {
                    var collection = getContext().getCollection();    
                    var response = getContext().getResponse();    

                    if(docToCreate.Year != undefined && docToCreate.Year < antiqueYear){
                        docToCreate.antique = true;
                    }

                    collection.createDocument(collection.getSelfLink(), docToCreate, {}, 
                        function(err, docCreated, options) { 
                            if(err) throw new Error('Error while creating document: ' + err.message);                              
                            if(options.maxCollectionSizeInMb == 0) throw 'max collection size not found'; 
                            response.setBody(docCreated);
                    });
             }"
    };

    // register stored procedure
    StoredProcedure createdStoredProcedure = await client.CreateStoredProcedureAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), markAntiquesSproc);
    dynamic document = new Document() { Id = "Borges_112" };
    document.Title = "Aleph";
    document.Year = 1949;

    // execute stored procedure
    Document createdDocument = await client.ExecuteStoredProcedureAsync<Document>(UriFactory.CreateStoredProcedureUri("db", "coll", "sproc"), document, 1920);


<span data-ttu-id="e816c-362">Este exemplo mostra como Olá toouse [API .NET do DocumentDB](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) toocreate um gatilho de pré-lançamento e criar um documento com hello gatilho habilitado.</span><span class="sxs-lookup"><span data-stu-id="e816c-362">This sample shows how toouse hello [DocumentDB .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) toocreate a pre-trigger and create a document with hello trigger enabled.</span></span> 

    Trigger preTrigger = new Trigger()
    {
        Id = "CapitalizeName",
        Body = @"function() {
            var item = getContext().getRequest().getBody();
            item.id = item.id.toUpperCase();
            getContext().getRequest().setBody(item);
        }",
        TriggerOperation = TriggerOperation.Create,
        TriggerType = TriggerType.Pre
    };

    Document createdItem = await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), new Document { Id = "documentdb" },
        new RequestOptions
        {
            PreTriggerInclude = new List<string> { "CapitalizeName" },
        });


<span data-ttu-id="e816c-363">E hello exemplo a seguir mostra como toocreate um usuário definido UDF (função) e usá-lo em uma [consulta SQL do DocumentDB API](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="e816c-363">And hello following example shows how toocreate a user defined function (UDF) and use it in a [DocumentDB API SQL query](documentdb-sql-query.md).</span></span>

    UserDefinedFunction function = new UserDefinedFunction()
    {
        Id = "LOWER",
        Body = @"function(input) 
        {
            return input.toLowerCase();
        }"
    };

    foreach (Book book in client.CreateDocumentQuery(UriFactory.CreateDocumentCollectionUri("db", "coll"),
        "SELECT * FROM Books b WHERE udf.LOWER(b.Title) = 'war and peace'"))
    {
        Console.WriteLine("Read {0} from query", book);
    }

## <a name="rest-api"></a><span data-ttu-id="e816c-364">API REST</span><span class="sxs-lookup"><span data-stu-id="e816c-364">REST API</span></span>
<span data-ttu-id="e816c-365">Todas as operações do Azure Cosmos DB podem ser realizadas de maneira RESTful.</span><span class="sxs-lookup"><span data-stu-id="e816c-365">All Azure Cosmos DB operations can be performed in a RESTful manner.</span></span> <span data-ttu-id="e816c-366">Procedimentos armazenados, gatilhos e funções definidas pelo usuário podem ser registrados em uma coleção usando HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="e816c-366">Stored procedures, triggers and user-defined functions can be registered under a collection by using HTTP POST.</span></span> <span data-ttu-id="e816c-367">Olá, a seguir está um exemplo de como tooregister um procedimento armazenado:</span><span class="sxs-lookup"><span data-stu-id="e816c-367">hello following is an example of how tooregister a stored procedure:</span></span>

    POST https://<url>/sprocs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT


    var x = {
      "name": "createAndAddProperty",
      "body": function (docToCreate, addedPropertyName, addedPropertyValue) {
                var collectionManager = getContext().getCollection();
                collectionManager.createDocument(
                    collectionManager.getSelfLink(),
                    docToCreate,
                    function(err, docCreated) {
                      if(err) throw new Error('Error:  ' + err.message);
                      docCreated[addedPropertyName] = addedPropertyValue;
                      getContext().getResponse().setBody(docCreated);
                    });
            }
    }


<span data-ttu-id="e816c-368">Olá procedimento armazenado está registrado executando uma solicitação POST em relação a saudação URI bancos de dados/testdb/colls/testColl/sprocs Olá corpo contendo Olá toocreate do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="e816c-368">hello stored procedure is registered by executing a POST request against hello URI dbs/testdb/colls/testColl/sprocs with hello body containing hello stored procedure toocreate.</span></span> <span data-ttu-id="e816c-369">Disparadores e UDFs podem ser registrados da mesma forma, emitindo um POST para /triggers e /udfs respectivamente.</span><span class="sxs-lookup"><span data-stu-id="e816c-369">Triggers and UDFs can be registered similarly by issuing a POST against /triggers and /udfs respectively.</span></span>
<span data-ttu-id="e816c-370">Este procedimento armazenado pode, então, ser executado emitindo uma solicitação POST ao link de recursos:</span><span class="sxs-lookup"><span data-stu-id="e816c-370">This stored procedure can then be executed by issuing a POST request against its resource link:</span></span>

    POST https://<url>/sprocs/<sproc> HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:20 GMT


    [ { "name": "TestDocument", "book": "Autumn of hello Patriarch"}, "Price", 200 ]


<span data-ttu-id="e816c-371">Aqui, o procedimento de entrada toohello armazenado Olá é passado no corpo de solicitação de hello.</span><span class="sxs-lookup"><span data-stu-id="e816c-371">Here, hello input toohello stored procedure is passed in hello request body.</span></span> <span data-ttu-id="e816c-372">Observe que a entrada hello é passada como uma matriz JSON dos parâmetros de entrada.</span><span class="sxs-lookup"><span data-stu-id="e816c-372">Note that hello input is passed as a JSON array of input parameters.</span></span> <span data-ttu-id="e816c-373">Olá armazenados procedimento leva Olá primeira entrada como um documento que é um corpo de resposta.</span><span class="sxs-lookup"><span data-stu-id="e816c-373">hello stored procedure takes hello first input as a document that is a response body.</span></span> <span data-ttu-id="e816c-374">resposta de saudação que recebemos é a seguinte:</span><span class="sxs-lookup"><span data-stu-id="e816c-374">hello response we receive is as follows:</span></span>

    HTTP/1.1 200 OK

    { 
      name: 'TestDocument',
      book: ‘Autumn of hello Patriarch’,
      id: ‘V7tQANV3rAkDAAAAAAAAAA==‘,
      ts: 1407830727,
      self: ‘dbs/V7tQAA==/colls/V7tQANV3rAk=/docs/V7tQANV3rAkDAAAAAAAAAA==/’,
      etag: ‘6c006596-0000-0000-0000-53e9cac70000’,
      attachments: ‘attachments/’,
      Price: 200
    }


<span data-ttu-id="e816c-375">Gatilhos, diferentemente dos procedimentos armazenados, não podem ser executados diretamente.</span><span class="sxs-lookup"><span data-stu-id="e816c-375">Triggers, unlike stored procedures, cannot be executed directly.</span></span> <span data-ttu-id="e816c-376">Ao invés disso, eles são executados como parte de uma operação em um documento.</span><span class="sxs-lookup"><span data-stu-id="e816c-376">Instead they are executed as part of an operation on a document.</span></span> <span data-ttu-id="e816c-377">Podemos especificar Olá gatilhos toorun com uma solicitação usando cabeçalhos HTTP.</span><span class="sxs-lookup"><span data-stu-id="e816c-377">We can specify hello triggers toorun with a request using HTTP headers.</span></span> <span data-ttu-id="e816c-378">a seguir Olá é solicitação toocreate um documento.</span><span class="sxs-lookup"><span data-stu-id="e816c-378">hello following is request toocreate a document.</span></span>

    POST https://<url>/docs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT
    x-ms-documentdb-pre-trigger-include: validateDocumentContents 
    x-ms-documentdb-post-trigger-include: bookCreationPostTrigger


    {
       "name": "newDocument",
       “title”: “hello Wizard of Oz”,
       “author”: “Frank Baum”,
       “pages”: 92
    }


<span data-ttu-id="e816c-379">Aqui Olá pré-gatilho toobe executar com a solicitação de saudação especificado no cabeçalho x-ms-documentdb-pre-trigger-include hello.</span><span class="sxs-lookup"><span data-stu-id="e816c-379">Here hello pre-trigger toobe run with hello request is specified in hello x-ms-documentdb-pre-trigger-include header.</span></span> <span data-ttu-id="e816c-380">De maneira correspondente, os pós-disparadores de recebem no cabeçalho x-ms-documentdb-post-trigger-include Olá.</span><span class="sxs-lookup"><span data-stu-id="e816c-380">Correspondingly, any post-triggers are given in hello x-ms-documentdb-post-trigger-include header.</span></span> <span data-ttu-id="e816c-381">Observe que pré e pós-gatilhos podem ser especificados para uma determinada solicitação.</span><span class="sxs-lookup"><span data-stu-id="e816c-381">Note that both pre- and post-triggers can be specified for a given request.</span></span>

## <a name="sample-code"></a><span data-ttu-id="e816c-382">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="e816c-382">Sample code</span></span>
<span data-ttu-id="e816c-383">Você pode encontrar mais exemplos de código do lado do servidor (incluindo [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js) e [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) em nosso [repositório GitHub](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span><span class="sxs-lookup"><span data-stu-id="e816c-383">You can find more server-side code examples (including [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js), and [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) on our [GitHub repository](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span></span>

<span data-ttu-id="e816c-384">Deseja tooshare o incrível procedimento armazenado?</span><span class="sxs-lookup"><span data-stu-id="e816c-384">Want tooshare your awesome stored procedure?</span></span> <span data-ttu-id="e816c-385">Por favor, envie uma solicitação pull!</span><span class="sxs-lookup"><span data-stu-id="e816c-385">Please, send us a pull-request!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e816c-386">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e816c-386">Next steps</span></span>
<span data-ttu-id="e816c-387">Uma vez que um ou mais procedimentos armazenados, gatilhos e funções definidas pelo usuário criadas, você pode carregá-los e exibi-los no hello portal do Azure usando o Gerenciador de dados.</span><span class="sxs-lookup"><span data-stu-id="e816c-387">Once you have one or more stored procedures, triggers, and user-defined functions created, you can load them and view them in hello Azure portal using Data Explorer.</span></span>

<span data-ttu-id="e816c-388">Você também pode encontrar o seguinte Olá referências e recursos úteis no seu toolearn de caminho mais sobre a programação do Azure Cosmos banco de dados do servidor:</span><span class="sxs-lookup"><span data-stu-id="e816c-388">You may also find hello following references and resources useful in your path toolearn more about Azure Cosmos dB server-side programming:</span></span>

* [<span data-ttu-id="e816c-389">SDKs do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e816c-389">Azure Cosmos DB SDKs</span></span>](documentdb-sdk-dotnet.md)
* [<span data-ttu-id="e816c-390">Estudo do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="e816c-390">DocumentDB Studio</span></span>](https://github.com/mingaliu/DocumentDBStudio/releases)
* [<span data-ttu-id="e816c-391">JSON</span><span class="sxs-lookup"><span data-stu-id="e816c-391">JSON</span></span>](http://www.json.org/) 
* [<span data-ttu-id="e816c-392">JavaScript ECMA-262</span><span class="sxs-lookup"><span data-stu-id="e816c-392">JavaScript ECMA-262</span></span>](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
* [<span data-ttu-id="e816c-393">Extensibilidade de banco de dados seguro e portátil</span><span class="sxs-lookup"><span data-stu-id="e816c-393">Secure and Portable Database Extensibility</span></span>](http://dl.acm.org/citation.cfm?id=276339) 
* [<span data-ttu-id="e816c-394">Arquitetura de banco de dados orientada a serviços</span><span class="sxs-lookup"><span data-stu-id="e816c-394">Service Oriented Database Architecture</span></span>](http://dl.acm.org/citation.cfm?id=1066267&coll=Portal&dl=GUIDE) 
* [<span data-ttu-id="e816c-395">Olá hospedagem .NET Runtime no Microsoft SQL server</span><span class="sxs-lookup"><span data-stu-id="e816c-395">Hosting hello .NET Runtime in Microsoft SQL server</span></span>](http://dl.acm.org/citation.cfm?id=1007669)

