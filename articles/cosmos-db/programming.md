---
title: "Programação de JavaScript do lado do servidor para o Azure Cosmos DB | Microsoft Docs"
description: "Saiba como usar o Azure Cosmos DB para escrever procedimentos armazenados, gatilhos de banco de dados e UDFs (funções definidas pelo usuário) em JavaScript. Obtenha dicas de programação de banco de dados e muito mais."
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
ms.openlocfilehash: 8cddc7a8c9aa677b9c93bee3a7e05c226cc1f655
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-server-side-programming-stored-procedures-database-triggers-and-udfs"></a><span data-ttu-id="e3df5-105">Programação do lado do servidor do Azure Cosmos DB: procedimentos armazenados, gatilhos de banco de dados e UDFs</span><span class="sxs-lookup"><span data-stu-id="e3df5-105">Azure Cosmos DB server-side programming: Stored procedures, database triggers, and UDFs</span></span>
<span data-ttu-id="e3df5-106">Saiba como a execução transacional e integrada de linguagem do JavaScript pelo Azure Cosmos DB permite que desenvolvedores escrevam **procedimentos armazenados**, **gatilhos** e **UDFs (funções definidas pelo usuário)** nativamente em um JavaScript [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/).</span><span class="sxs-lookup"><span data-stu-id="e3df5-106">Learn how Azure Cosmos DB’s language integrated, transactional execution of JavaScript lets developers write **stored procedures**, **triggers** and **user defined functions (UDFs)** natively in an [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript.</span></span> <span data-ttu-id="e3df5-107">Isso permite que você escreva uma lógica de aplicativo de programa de banco de dados que pode ser enviada e executada diretamente nas partições de armazenamento do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e3df5-107">This allows you to write database program application logic that can be shipped and executed directly on the database storage partitions.</span></span> 

<span data-ttu-id="e3df5-108">Recomendamos que você comece assistindo ao vídeo a seguir, em que Andrew Liu fornece uma breve introdução ao modelo de programação de banco de dados do lado do servidor do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e3df5-108">We recommend getting started by watching the following video, where Andrew Liu provides a brief introduction to Cosmos DB's server-side database programming model.</span></span> 

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Demo-A-Quick-Intro-to-Azure-DocumentDBs-Server-Side-Javascript/player]
> 
> 

<span data-ttu-id="e3df5-109">Em seguida, volte a este artigo, onde você aprenderá as respostas para as seguintes perguntas:</span><span class="sxs-lookup"><span data-stu-id="e3df5-109">Then, return to this article, where you'll learn the answers to the following questions:</span></span>  

* <span data-ttu-id="e3df5-110">Como eu escrevo um procedimento armazenado, gatilho ou UDF usando JavaScript?</span><span class="sxs-lookup"><span data-stu-id="e3df5-110">How do I write a a stored procedure, trigger, or UDF using JavaScript?</span></span>
* <span data-ttu-id="e3df5-111">Como o Cosmos DB garante o ACID?</span><span class="sxs-lookup"><span data-stu-id="e3df5-111">How does Cosmos DB guarantee ACID?</span></span>
* <span data-ttu-id="e3df5-112">Como funcionam as transações no Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="e3df5-112">How do transactions work in Cosmos DB?</span></span>
* <span data-ttu-id="e3df5-113">O que são pré-gatilhos e pós-gatilhos e como eu escrevo um?</span><span class="sxs-lookup"><span data-stu-id="e3df5-113">What are pre-triggers and post-triggers and how do I write one?</span></span>
* <span data-ttu-id="e3df5-114">Como eu registro e executo um procedimento armazenado, gatilho ou UDF de modo RESTful usando HTTP?</span><span class="sxs-lookup"><span data-stu-id="e3df5-114">How do I register and execute a stored procedure, trigger, or UDF in a RESTful manner by using HTTP?</span></span>
* <span data-ttu-id="e3df5-115">Quais SDKs do Cosmos DB estão disponíveis para criar e executar procedimentos armazenados, gatilhos e UDFs?</span><span class="sxs-lookup"><span data-stu-id="e3df5-115">What Cosmos DB SDKs are available to create and execute stored procedures, triggers, and UDFs?</span></span>

## <a name="introduction-to-stored-procedure-and-udf-programming"></a><span data-ttu-id="e3df5-116">Introdução ao procedimento armazenado e à programação UDF</span><span class="sxs-lookup"><span data-stu-id="e3df5-116">Introduction to Stored Procedure and UDF Programming</span></span>
<span data-ttu-id="e3df5-117">Essa abordagem de *"JavaScript como um T-SQL moderno"* libera os desenvolvedores de aplicativos das complexidades das incompatibilidades do sistema de tipos e tecnologias de mapeamento relacionais do objeto.</span><span class="sxs-lookup"><span data-stu-id="e3df5-117">This approach of *“JavaScript as a modern day T-SQL”* frees application developers from the complexities of type system mismatches and object-relational mapping technologies.</span></span> <span data-ttu-id="e3df5-118">Também possui uma série de vantagens intrínsecas que podem ser utilizadas para criar aplicativos ricos:</span><span class="sxs-lookup"><span data-stu-id="e3df5-118">It also has a number of intrinsic advantages that can be utilized to build rich applications:</span></span>  

* <span data-ttu-id="e3df5-119">**Lógica de procedimento:** o JavaScript, enquanto uma linguagem de programação de alto nível, oferece uma interface rica e familiar para expressar a lógica de negócios.</span><span class="sxs-lookup"><span data-stu-id="e3df5-119">**Procedural Logic:** JavaScript as a high level programming language, provides a rich and familiar interface to express business logic.</span></span> <span data-ttu-id="e3df5-120">Você pode realizar sequências complexas de operações de maneira mais próxima aos dados.</span><span class="sxs-lookup"><span data-stu-id="e3df5-120">You can perform complex sequences of operations closer to the data.</span></span>
* <span data-ttu-id="e3df5-121">**Transações atômicas:** o Cosmos DB garante que as operações de banco de dados realizadas em um único procedimento armazenado ou gatilho são atômicas.</span><span class="sxs-lookup"><span data-stu-id="e3df5-121">**Atomic Transactions:** Cosmos DB guarantees that database operations performed inside a single stored procedure or trigger are atomic.</span></span> <span data-ttu-id="e3df5-122">Isso permite que um aplicativo combine operações relacionadas em um único lote para que todas ou nenhuma delas seja bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="e3df5-122">This lets an application combine related operations in a single batch so that either all of them succeed or none of them succeed.</span></span> 
* <span data-ttu-id="e3df5-123">**Desempenho:** o fato de o JSON ser intrinsecamente mapeado para o sistema de tipos de linguagem JavaScript e também ser a unidade básica de armazenamento no Cosmos DB permite uma série de otimizações, como a materialização lenta de documentos JSON no pool de buffers e sua disponibilização sob demanda ao código de execução.</span><span class="sxs-lookup"><span data-stu-id="e3df5-123">**Performance:** The fact that JSON is intrinsically mapped to the Javascript language type system and is also the basic unit of storage in Cosmos DB allows for a number of optimizations like lazy materialization of JSON documents in the buffer pool and making them available on-demand to the executing code.</span></span> <span data-ttu-id="e3df5-124">Há mais benefícios de desempenho associados ao envio da lógica de negócios ao banco de dados:</span><span class="sxs-lookup"><span data-stu-id="e3df5-124">There are more performance benefits associated with shipping business logic to the database:</span></span>
  
  * <span data-ttu-id="e3df5-125">Envio em lote – Os desenvolvedores podem agrupar operações como inserções e enviá-las em massa.</span><span class="sxs-lookup"><span data-stu-id="e3df5-125">Batching – Developers can group operations like inserts and submit them in bulk.</span></span> <span data-ttu-id="e3df5-126">O custo de latência de tráfego de rede e a sobrecarga de armazenamento para criar transações separadas são reduzidos significativamente.</span><span class="sxs-lookup"><span data-stu-id="e3df5-126">The network traffic latency cost and the store overhead to create separate transactions are reduced significantly.</span></span> 
  * <span data-ttu-id="e3df5-127">Pré-compilação – o Cosmos DB pré-compila procedimentos armazenados, gatilhos e UDFs (funções definidas pelo usuário) a fim de evitar custos de compilação de JavaScript para cada invocação.</span><span class="sxs-lookup"><span data-stu-id="e3df5-127">Pre-compilation – Cosmos DB precompiles stored procedures, triggers and user defined functions (UDFs) to avoid JavaScript compilation cost for each invocation.</span></span> <span data-ttu-id="e3df5-128">A sobrecarga de construir o código de bytes para a lógica de procedimento é amortizada a um valor mínimo.</span><span class="sxs-lookup"><span data-stu-id="e3df5-128">The overhead of building the byte code for the procedural logic is amortized to a minimal value.</span></span>
  * <span data-ttu-id="e3df5-129">Sequenciamento – Várias operações precisam de um efeito colateral (“gatilho”) que possivelmente envolve realizar uma ou mais operações de armazenamento secundárias.</span><span class="sxs-lookup"><span data-stu-id="e3df5-129">Sequencing – Many operations need a side-effect (“trigger”) that potentially involves doing one or many secondary store operations.</span></span> <span data-ttu-id="e3df5-130">Além da atomicidade, o desempenho é melhor quando movido ao servidor.</span><span class="sxs-lookup"><span data-stu-id="e3df5-130">Aside from atomicity, this is more performant when moved to the server.</span></span> 
* <span data-ttu-id="e3df5-131">**Encapsulamento:** procedimentos armazenados podem ser usados para agrupar lógica de negócios em um único lugar.</span><span class="sxs-lookup"><span data-stu-id="e3df5-131">**Encapsulation:** Stored procedures can be used to group business logic in one place.</span></span> <span data-ttu-id="e3df5-132">Isso apresenta duas vantagens:</span><span class="sxs-lookup"><span data-stu-id="e3df5-132">This has two advantages:</span></span>
  * <span data-ttu-id="e3df5-133">Adiciona uma camada de abstração sobre os dados brutos, o que permite que os arquitetos de dados desenvolvam seus aplicativos de maneira independente dos dados.</span><span class="sxs-lookup"><span data-stu-id="e3df5-133">It adds an abstraction layer on top of the raw data, which enables data architects to evolve their applications independently from the data.</span></span> <span data-ttu-id="e3df5-134">Isso é ainda mais vantajoso quando os dados não possuem esquema, devido às suposições que precisam ser integradas ao aplicativo se precisarem lidar diretamente com os dados.</span><span class="sxs-lookup"><span data-stu-id="e3df5-134">This is particularly advantageous when the data is schema-less, due to the brittle assumptions that may need to be baked into the application if they have to deal with data directly.</span></span>  
  * <span data-ttu-id="e3df5-135">Essa abstração permite que as empresas protejam seus dados simplificando o acesso pelos scripts.</span><span class="sxs-lookup"><span data-stu-id="e3df5-135">This abstraction lets enterprises keep their data secure by streamlining the access from the scripts.</span></span>  

<span data-ttu-id="e3df5-136">Há suporte para a criação e execução de gatilhos de banco de dados, procedimentos armazenados e operadores de consulta personalizada por meio da [API REST](/rest/api/documentdb/), do [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases) e dos [SDKs do cliente](documentdb-sdk-dotnet.md) em diversas plataformas, incluindo .NET, Node.js e JavaScript.</span><span class="sxs-lookup"><span data-stu-id="e3df5-136">The creation and execution of database triggers, stored procedure and custom query operators is supported through the [REST API](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), and [client SDKs](documentdb-sdk-dotnet.md) in many platforms including .NET, Node.js and JavaScript.</span></span>

<span data-ttu-id="e3df5-137">Esse tutorial utiliza o [SDK do Node.js com Q Promises](http://azure.github.io/azure-documentdb-node-q/) para ilustrar a sintaxe e o uso de procedimentos armazenados, gatilhos e UDFs.</span><span class="sxs-lookup"><span data-stu-id="e3df5-137">This tutorial uses the [Node.js SDK with Q Promises](http://azure.github.io/azure-documentdb-node-q/) to illustrate syntax and usage of stored procedures, triggers, and UDFs.</span></span>   

## <a name="stored-procedures"></a><span data-ttu-id="e3df5-138">Procedimentos armazenados</span><span class="sxs-lookup"><span data-stu-id="e3df5-138">Stored procedures</span></span>
### <a name="example-write-a-simple-stored-procedure"></a><span data-ttu-id="e3df5-139">Exemplo: escrever um procedimento armazenado simples</span><span class="sxs-lookup"><span data-stu-id="e3df5-139">Example: Write a simple stored procedure</span></span>
<span data-ttu-id="e3df5-140">Vamos começar com um procedimento armazenado simples que retorna uma resposta “Hello World”.</span><span class="sxs-lookup"><span data-stu-id="e3df5-140">Let’s start with a simple stored procedure that returns a “Hello World” response.</span></span>

    var helloWorldStoredProc = {
        id: "helloWorld",
        serverScript: function () {
            var context = getContext();
            var response = context.getResponse();

            response.setBody("Hello, World");
        }
    }


<span data-ttu-id="e3df5-141">Os procedimentos armazenados são registrados por coleção e podem operar em qualquer documento e anexo presente na coleção.</span><span class="sxs-lookup"><span data-stu-id="e3df5-141">Stored procedures are registered per collection, and can operate on any document and attachment present in that collection.</span></span> <span data-ttu-id="e3df5-142">O trecho a seguir mostra como registrar o procedimento armazenado helloWorld com uma coleção.</span><span class="sxs-lookup"><span data-stu-id="e3df5-142">The following snippet shows how to register the helloWorld stored procedure with a collection.</span></span> 

    // register the stored procedure
    var createdStoredProcedure;
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', helloWorldStoredProc)
        .then(function (response) {
            createdStoredProcedure = response.resource;
            console.log("Successfully created stored procedure");
        }, function (error) {
            console.log("Error", error);
        });


<span data-ttu-id="e3df5-143">Uma vez que o procedimento armazenado é registrado, podemos executá-lo em relação à coleção e ler os resultados no cliente.</span><span class="sxs-lookup"><span data-stu-id="e3df5-143">Once the stored procedure is registered, we can execute it against the collection, and read the results back at the client.</span></span> 

    // execute the stored procedure
    client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/helloWorld')
        .then(function (response) {
            console.log(response.result); // "Hello, World"
        }, function (err) {
            console.log("Error", error);
        });


<span data-ttu-id="e3df5-144">O objeto de contexto fornece acesso a todas as operações que podem ser realizadas no armazenamento do Cosmos DB, bem como o acesso aos objetos de solicitação e resposta.</span><span class="sxs-lookup"><span data-stu-id="e3df5-144">The context object provides access to all operations that can be performed on Cosmos DB storage, as well as access to the request and response objects.</span></span> <span data-ttu-id="e3df5-145">Nesse caso, usamos o objeto de resposta para definir o corpo da resposta que foi enviada ao cliente.</span><span class="sxs-lookup"><span data-stu-id="e3df5-145">In this case, we used the response object to set the body of the response that was sent back to the client.</span></span> <span data-ttu-id="e3df5-146">Para obter mais detalhes, consulte a [documentação do SDK do servidor do JavaScript do Azure Cosmos DB](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="e3df5-146">For more details, refer to the [Azure Cosmos DB JavaScript server SDK documentation](http://azure.github.io/azure-documentdb-js-server/).</span></span>  

<span data-ttu-id="e3df5-147">Vamos ampliar esse exemplo e adicionar mais funcionalidades relativas ao banco de dados ao procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="e3df5-147">Let us expand on this example and add more database related functionality to the stored procedure.</span></span> <span data-ttu-id="e3df5-148">Procedimentos armazenados podem criar, atualizar, ler, consultar e excluir documentos e anexos dentro da coleção.</span><span class="sxs-lookup"><span data-stu-id="e3df5-148">Stored procedures can create, update, read, query and delete documents and attachments inside the collection.</span></span>    

### <a name="example-write-a-stored-procedure-to-create-a-document"></a><span data-ttu-id="e3df5-149">Exemplo: escrever um procedimento armazenado para criar um documento</span><span class="sxs-lookup"><span data-stu-id="e3df5-149">Example: Write a stored procedure to create a document</span></span>
<span data-ttu-id="e3df5-150">O próximo trecho mostra como usar o objeto de contexto para interagir com recursos do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e3df5-150">The next snippet shows how to use the context object to interact with Cosmos DB resources.</span></span>

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


<span data-ttu-id="e3df5-151">Esse procedimento armazenado assume como entrada documentToCreate, o corpo de um documento a ser criado na coleção atual.</span><span class="sxs-lookup"><span data-stu-id="e3df5-151">This stored procedure takes as input documentToCreate, the body of a document to be created in the current collection.</span></span> <span data-ttu-id="e3df5-152">Todas essas operações são assíncronas e dependem de retornos de chamada de função do JavaScript.</span><span class="sxs-lookup"><span data-stu-id="e3df5-152">All such operations are asynchronous and depend on JavaScript function callbacks.</span></span> <span data-ttu-id="e3df5-153">A função de retorno de chamada possui dois parâmetros, um para o objeto de erro no caso de falhas na operação e um para o objeto criado.</span><span class="sxs-lookup"><span data-stu-id="e3df5-153">The callback function has two parameters, one for the error object in case the operation fails, and one for the created object.</span></span> <span data-ttu-id="e3df5-154">Dentro da chamada de retorno, os usuários podem lidar com a exceção ou lançar um erro.</span><span class="sxs-lookup"><span data-stu-id="e3df5-154">Inside the callback, users can either handle the exception or throw an error.</span></span> <span data-ttu-id="e3df5-155">Caso uma chamada de retorno não seja fornecida e haja um erro, o tempo de execução do Azure Cosmos DB gerará um erro.</span><span class="sxs-lookup"><span data-stu-id="e3df5-155">In case a callback is not provided and there is an error, the Azure Cosmos DB runtime throws an error.</span></span>   

<span data-ttu-id="e3df5-156">No exemplo acima, a chamada de torno lançará um erro se a operação falhar.</span><span class="sxs-lookup"><span data-stu-id="e3df5-156">In the example above, the callback throws an error if the operation failed.</span></span> <span data-ttu-id="e3df5-157">Caso contrário, ela definirá a ID do documento criada como o corpo da resposta ao cliente.</span><span class="sxs-lookup"><span data-stu-id="e3df5-157">Otherwise, it sets the id of the created document as the body of the response to the client.</span></span> <span data-ttu-id="e3df5-158">A seguir, mostramos como esse procedimento armazenado é executado com parâmetros de entrada.</span><span class="sxs-lookup"><span data-stu-id="e3df5-158">Here is how this stored procedure is executed with input parameters.</span></span>

    // register the stored procedure
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', createDocumentStoredProc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;

            // run stored procedure to create a document
            var docToCreate = {
                id: "DocFromSproc",
                book: "The Hitchhiker’s Guide to the Galaxy",
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


<span data-ttu-id="e3df5-159">Observe que esse procedimento armazenado pode ser modificado para assumir uma matriz de corpos de documentos como entrada e criá-los todos na mesma execução do procedimento armazenado ao invés de em várias solicitações de rede para criar cada um deles individualmente.</span><span class="sxs-lookup"><span data-stu-id="e3df5-159">Note that this stored procedure can be modified to take an array of document bodies as input and create them all in the same stored procedure execution instead of multiple network requests to create each of them individually.</span></span> <span data-ttu-id="e3df5-160">Isso pode ser usado para implementar um importador em massa eficiente para o Cosmos DB (abordado posteriormente neste tutorial).</span><span class="sxs-lookup"><span data-stu-id="e3df5-160">This can be used to implement an efficient bulk importer for Cosmos DB (discussed later in this tutorial).</span></span>   

<span data-ttu-id="e3df5-161">O exemplo descrito demonstra como usar procedimentos armazenados.</span><span class="sxs-lookup"><span data-stu-id="e3df5-161">The example described demonstrated how to use stored procedures.</span></span> <span data-ttu-id="e3df5-162">Iremos discutir os gatilhos e funções definidas pelo usuário (UDFs) posteriormente no tutorial.</span><span class="sxs-lookup"><span data-stu-id="e3df5-162">We will cover triggers and user defined functions (UDFs) later in the tutorial.</span></span>

## <a name="database-program-transactions"></a><span data-ttu-id="e3df5-163">Transações do programa de banco de dados</span><span class="sxs-lookup"><span data-stu-id="e3df5-163">Database program transactions</span></span>
<span data-ttu-id="e3df5-164">A transação em um banco de dados típico pode ser definida como uma sequência de operações realizadas como uma única unidade lógica de trabalho.</span><span class="sxs-lookup"><span data-stu-id="e3df5-164">Transaction in a typical database can be defined as a sequence of operations performed as a single logical unit of work.</span></span> <span data-ttu-id="e3df5-165">Cada transação oferece **garantias ACID**.</span><span class="sxs-lookup"><span data-stu-id="e3df5-165">Each transaction provides **ACID guarantees**.</span></span> <span data-ttu-id="e3df5-166">ACID é um acrônimo bastante conhecido que indica quatro propriedades: Atomicidade, Consistência, Isolamento e Durabilidade.</span><span class="sxs-lookup"><span data-stu-id="e3df5-166">ACID is a well-known acronym that stands for four properties -  Atomicity, Consistency, Isolation and Durability.</span></span>  

<span data-ttu-id="e3df5-167">Em resumo, a atomicidade garante que todo o trabalho realizado dentro de uma transação seja tratado como uma única unidade em que tudo é confirmado ou não.</span><span class="sxs-lookup"><span data-stu-id="e3df5-167">Briefly, atomicity guarantees that all the work done inside a transaction is treated as a single unit where either all of it is committed or none.</span></span> <span data-ttu-id="e3df5-168">A consistência garante que os dados estejam sempre em uma boa condição interna entre as transações.</span><span class="sxs-lookup"><span data-stu-id="e3df5-168">Consistency makes sure that the data is always in a good internal state across transactions.</span></span> <span data-ttu-id="e3df5-169">O isolamento garante que duas transações não interfiram uma com a outra; geralmente, a maioria dos sistemas comerciais oferece vários níveis de isolamento que podem ser usados com base nas necessidades do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e3df5-169">Isolation guarantees that no two transactions interfere with each other – generally, most commercial systems provide multiple isolation levels that can be used based on the application needs.</span></span> <span data-ttu-id="e3df5-170">A durabilidade garante que qualquer alteração confirmada no banco de dados esteja sempre presente.</span><span class="sxs-lookup"><span data-stu-id="e3df5-170">Durability ensures that any change that’s committed in the database will always be present.</span></span>   

<span data-ttu-id="e3df5-171">No Cosmos DB, o JavaScript é hospedado no mesmo espaço de memória do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e3df5-171">In Cosmos DB, JavaScript is hosted in the same memory space as the database.</span></span> <span data-ttu-id="e3df5-172">Portanto, as solicitações realizadas dentro de procedimentos armazenados e gatilhos são executadas no mesmo escopo de uma sessão do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e3df5-172">Hence, requests made within stored procedures and triggers execute in the same scope of a database session.</span></span> <span data-ttu-id="e3df5-173">Isso permite que o Cosmos DB garanta ACID para todas as operações que fazem parte de um único procedimento armazenado/gatilho.</span><span class="sxs-lookup"><span data-stu-id="e3df5-173">This enables Cosmos DB to guarantee ACID for all operations that are part of a single stored procedure/trigger.</span></span> <span data-ttu-id="e3df5-174">Considere a seguinte definição de um procedimento armazenado:</span><span class="sxs-lookup"><span data-stu-id="e3df5-174">Consider the following stored procedure definition:</span></span>

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

                    if (documents.length != 1) throw "Unable to find both names";
                    player1Document = documents[0];

                    var filterQuery2 = 'SELECT * FROM Players p where p.id = "' + playerId2 + '"';
                    var accept2 = collection.queryDocuments(collection.getSelfLink(), filterQuery2, {},
                        function (err2, documents2, responseOptions2) {
                            if (err2) throw new Error("Error" + err2.message);
                            if (documents2.length != 1) throw "Unable to find both names";
                            player2Document = documents2[0];
                            swapItems(player1Document, player2Document);
                            return;
                        });
                    if (!accept2) throw "Unable to read player details, abort ";
                });

            if (!accept) throw "Unable to read player details, abort ";

            // swap the two players’ items
            function swapItems(player1, player2) {
                var player1ItemSave = player1.item;
                player1.item = player2.item;
                player2.item = player1ItemSave;

                var accept = collection.replaceDocument(player1._self, player1,
                    function (err, docReplaced) {
                        if (err) throw "Unable to update player 1, abort ";

                        var accept2 = collection.replaceDocument(player2._self, player2,
                            function (err2, docReplaced2) {
                                if (err) throw "Unable to update player 2, abort"
                            });

                        if (!accept2) throw "Unable to update player 2, abort";
                    });

                if (!accept) throw "Unable to update player 1, abort";
            }
        }
    }

    // register the stored procedure in Node.js client
    client.createStoredProcedureAsync(collection._self, exchangeItemsSproc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;
        }
    );

<span data-ttu-id="e3df5-175">Esse procedimento armazenado utiliza transações dentro de um aplicativo de jogos para negociar itens entre dois jogadores em uma única operação.</span><span class="sxs-lookup"><span data-stu-id="e3df5-175">This stored procedure uses transactions within a gaming app to trade items between two players in a single operation.</span></span> <span data-ttu-id="e3df5-176">O procedimento armazenado tenta ler dois ou mais documentos, cada um correspondente às IDs dos jogadores transmitidos como um argumento.</span><span class="sxs-lookup"><span data-stu-id="e3df5-176">The stored procedure attempts to read two documents each corresponding to the player IDs passed in as an argument.</span></span> <span data-ttu-id="e3df5-177">Se os documentos de ambos os jogadores forem encontrados, então, o procedimento armazenado atualizará os documentos trocando seus itens.</span><span class="sxs-lookup"><span data-stu-id="e3df5-177">If both player documents are found, then the stored procedure updates the documents by swapping their items.</span></span> <span data-ttu-id="e3df5-178">Se forem encontrados erros pelo caminho, uma exceção JavaScript será lançada, o que aborta implicitamente a transação.</span><span class="sxs-lookup"><span data-stu-id="e3df5-178">If any errors are encountered along the way, it throws a JavaScript exception that implicitly aborts the transaction.</span></span>

<span data-ttu-id="e3df5-179">Se a coleção na qual o procedimento armazenado está registrado for uma coleção de única partição, o escopo da transação será todos os documentos dentro da coleção.</span><span class="sxs-lookup"><span data-stu-id="e3df5-179">If the collection the stored procedure is registered against is a single-partition collection, then the transaction is scoped to all the documents within the collection.</span></span> <span data-ttu-id="e3df5-180">Se a coleção for particionada, os procedimentos armazenados serão executados no escopo da transação de uma única chave de partição.</span><span class="sxs-lookup"><span data-stu-id="e3df5-180">If the collection is partitioned, then stored procedures are executed in the transaction scope of a single partition key.</span></span> <span data-ttu-id="e3df5-181">A execução de cada procedimento armazenado deve incluir um valor de chave de partição correspondente ao escopo sob o qual a transação deve ser executada.</span><span class="sxs-lookup"><span data-stu-id="e3df5-181">Each stored procedure execution must then include a partition key value corresponding to the scope the transaction must run under.</span></span> <span data-ttu-id="e3df5-182">Para obter mais detalhes, consulte [Particionamento do Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="e3df5-182">For more details, see [Azure Cosmos DB Partitioning](partition-data.md).</span></span>

### <a name="commit-and-rollback"></a><span data-ttu-id="e3df5-183">Confirmação e reversão</span><span class="sxs-lookup"><span data-stu-id="e3df5-183">Commit and rollback</span></span>
<span data-ttu-id="e3df5-184">As transações são profunda e nativamente integradas ao modelo de programação do JavaScript do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e3df5-184">Transactions are deeply and natively integrated into Cosmos DB’s JavaScript programming model.</span></span> <span data-ttu-id="e3df5-185">Dentro de uma função de JavaScript, todas as operações são automaticamente encapsuladas em uma única transação.</span><span class="sxs-lookup"><span data-stu-id="e3df5-185">Inside a JavaScript function, all operations are automatically wrapped under a single transaction.</span></span> <span data-ttu-id="e3df5-186">Se o JavaScript for concluído sem nenhuma exceção, as operações de banco de dados serão confirmadas.</span><span class="sxs-lookup"><span data-stu-id="e3df5-186">If the JavaScript completes without any exception, the operations to the database are committed.</span></span> <span data-ttu-id="e3df5-187">De fato, as instruções “BEGIN TRANSACTION” e “COMMIT TRANSACTION” em bancos de dados relacionais são implícitas no Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e3df5-187">In effect, the “BEGIN TRANSACTION” and “COMMIT TRANSACTION” statements in relational databases are implicit in Cosmos DB.</span></span>  

<span data-ttu-id="e3df5-188">Se houver uma exceção propagada no script, o tempo de execução do JavaScript do Cosmos DB reverterá toda a transação.</span><span class="sxs-lookup"><span data-stu-id="e3df5-188">If there is any exception that’s propagated from the script, Cosmos DB’s JavaScript runtime will roll back the whole transaction.</span></span> <span data-ttu-id="e3df5-189">Como mostrado no exemplo anterior, gerar uma exceção é efetivamente equivalente a uma instrução “ROLLBACK TRANSACTION” no Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e3df5-189">As shown in the earlier example, throwing an exception is effectively equivalent to a “ROLLBACK TRANSACTION” in Cosmos DB.</span></span>

### <a name="data-consistency"></a><span data-ttu-id="e3df5-190">Consistência de dados</span><span class="sxs-lookup"><span data-stu-id="e3df5-190">Data consistency</span></span>
<span data-ttu-id="e3df5-191">Procedimentos armazenados e gatilhos são sempre executados na réplica primária do contêiner do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e3df5-191">Stored procedures and triggers are always executed on the primary replica of the Azure Cosmos DB container.</span></span> <span data-ttu-id="e3df5-192">Isso assegura que as leituras de dentro de procedimentos armazenados ofereçam uma forte consistência.</span><span class="sxs-lookup"><span data-stu-id="e3df5-192">This ensures that reads from inside stored procedures offer strong consistency.</span></span> <span data-ttu-id="e3df5-193">As consultas que utilizam funções definidas pelo usuário podem ser executadas na réplica primária ou em qualquer réplica secundária, porém, garantimos que o nível de consistência solicitado seja atendido ao escolher a réplica adequada.</span><span class="sxs-lookup"><span data-stu-id="e3df5-193">Queries using user defined functions can be executed on the primary or any secondary replica, but we ensure to meet the requested consistency level by choosing the appropriate replica.</span></span>

## <a name="bounded-execution"></a><span data-ttu-id="e3df5-194">Execução vinculada</span><span class="sxs-lookup"><span data-stu-id="e3df5-194">Bounded execution</span></span>
<span data-ttu-id="e3df5-195">Todas as operações do Cosmos DB devem ser concluídas dentro da duração de tempo limite da solicitação especificada pelo servidor.</span><span class="sxs-lookup"><span data-stu-id="e3df5-195">All Cosmos DB operations must complete within the server specified request timeout duration.</span></span> <span data-ttu-id="e3df5-196">Essa restrição também se aplica à função de JavaScript (procedimentos armazenados, gatilhos e funções definidas pelo usuário).</span><span class="sxs-lookup"><span data-stu-id="e3df5-196">This constraint also applies to JavaScript functions (stored procedures, triggers and user-defined functions).</span></span> <span data-ttu-id="e3df5-197">Se uma operação não for concluída com esse limite de tempo, a transação será retrocedida.</span><span class="sxs-lookup"><span data-stu-id="e3df5-197">If an operation does not complete with that time limit, the transaction is rolled back.</span></span> <span data-ttu-id="e3df5-198">Funções JavaScript devem ser concluídas dentro do limite de tempo ou implementar um modelo com base em uma continuação para criar um lote/retomar a execução.</span><span class="sxs-lookup"><span data-stu-id="e3df5-198">JavaScript functions must finish within the time limit or implement a continuation based model to batch/resume execution.</span></span>  

<span data-ttu-id="e3df5-199">A fim de simplificar o desenvolvimento de procedimentos armazenados e gatilhos para lidar com limites de tempo, todas as funções no objeto de coleção (para a criação, leitura, substituição e exclusão de documentos e anexos) retornam um valor booliano que representa se a operação será concluída.</span><span class="sxs-lookup"><span data-stu-id="e3df5-199">In order to simplify development of stored procedures and triggers to handle time limits, all functions under the collection object (for create, read, replace, and delete of documents and attachments) return a Boolean value that represents whether that operation will complete.</span></span> <span data-ttu-id="e3df5-200">Se esse valor for falso, isso indica que o limite de tempo está prestes a expirar e que o procedimento deve encerrar a execução.</span><span class="sxs-lookup"><span data-stu-id="e3df5-200">If this value is false, it is an indication that the time limit is about to expire and that the procedure must wrap up execution.</span></span>  <span data-ttu-id="e3df5-201">Operações colocadas em fila antes da primeira operação de armazenamento não aceita serão concluídas com certeza se o procedimento armazenado for concluído dentro do tempo e não colocar nenhuma outra solicitação em fila.</span><span class="sxs-lookup"><span data-stu-id="e3df5-201">Operations queued prior to the first unaccepted store operation are guaranteed to complete if the stored procedure completes in time and does not queue any more requests.</span></span>  

<span data-ttu-id="e3df5-202">Funções de JavaScript também são vinculadas quanto ao consumo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e3df5-202">JavaScript functions are also bounded on resource consumption.</span></span> <span data-ttu-id="e3df5-203">O Cosmos DB reserva a produtividade por coleção com base no tamanho provisionado de uma conta de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e3df5-203">Cosmos DB reserves throughput per collection based on the provisioned size of a database account.</span></span> <span data-ttu-id="e3df5-204">A produtividade é expressa em termos de uma unidade normalizada de consumo de CPU, memória e E/S chamada unidade de solicitação ou RU.</span><span class="sxs-lookup"><span data-stu-id="e3df5-204">Throughput is expressed in terms of a normalized unit of CPU, memory and IO consumption called request units or RUs.</span></span> <span data-ttu-id="e3df5-205">Funções de JavaScript podem usar um grande número de RUs dentro de um curto período, e podem ter sua taxa limitada se o limite da coleção for atingido.</span><span class="sxs-lookup"><span data-stu-id="e3df5-205">JavaScript functions can potentially use up a large number of RUs within a short time, and might get rate-limited if the collection’s limit is reached.</span></span> <span data-ttu-id="e3df5-206">Procedimentos armazenados ricos em recursos também podem ser postos em quarentena para garantir a disponibilidade das operações primitivas do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e3df5-206">Resource intensive stored procedures might also be quarantined to ensure availability of primitive database operations.</span></span>  

### <a name="example-bulk-importing-data-into-a-database-program"></a><span data-ttu-id="e3df5-207">Exemplo: importação de dados em massa em um programa de banco de dados</span><span class="sxs-lookup"><span data-stu-id="e3df5-207">Example: Bulk importing data into a database program</span></span>
<span data-ttu-id="e3df5-208">Abaixo está um exemplo de um procedimento armazenado gravado para documentos de importação em massa em uma coleção.</span><span class="sxs-lookup"><span data-stu-id="e3df5-208">Below is an example of a stored procedure that is written to bulk-import documents into a collection.</span></span> <span data-ttu-id="e3df5-209">Observe como o procedimento armazenado lida com a execução vinculada verificando o valor de retorno booliano em createDocument, e depois utiliza a contagem de documentos inserida em cada invocação do procedimento armazenado para rastrear e retomar o progresso nos lotes.</span><span class="sxs-lookup"><span data-stu-id="e3df5-209">Note how the stored procedure handles bounded execution by checking the Boolean return value from createDocument, and then uses the count of documents inserted in each invocation of the stored procedure to track and resume progress across batches.</span></span>

    function bulkImport(docs) {
        var collection = getContext().getCollection();
        var collectionLink = collection.getSelfLink();

        // The count of imported docs, also used as current doc index.
        var count = 0;

        // Validate input.
        if (!docs) throw new Error("The array is undefined or null.");

        var docsLength = docs.length;
        if (docsLength == 0) {
            getContext().getResponse().setBody(0);
        }

        // Call the create API to create a document.
        tryCreate(docs[count], callback);

        // Note that there are 2 exit conditions:
        // 1) The createDocument request was not accepted. 
        //    In this case the callback will not be called, we just call setBody and we are done.
        // 2) The callback was called docs.length times.
        //    In this case all documents were created and we don’t need to call tryCreate anymore. Just call setBody and we are done.
        function tryCreate(doc, callback) {
            var isAccepted = collection.createDocument(collectionLink, doc, callback);

            // If the request was accepted, callback will be called.
            // Otherwise report current count back to the client, 
            // which will call the script again with remaining set of docs.
            if (!isAccepted) getContext().getResponse().setBody(count);
        }

        // This is called when collection.createDocument is done in order to process the result.
        function callback(err, doc, options) {
            if (err) throw err;

            // One more document has been inserted, increment the count.
            count++;

            if (count >= docsLength) {
                // If we created all documents, we are done. Just set the response.
                getContext().getResponse().setBody(count);
            } else {
                // Create next document.
                tryCreate(docs[count], callback);
            }
        }
    }

## <span data-ttu-id="e3df5-210"><a id="trigger"></a> Gatilhos de banco de dados</span><span class="sxs-lookup"><span data-stu-id="e3df5-210"><a id="trigger"></a> Database triggers</span></span>
### <a name="database-pre-triggers"></a><span data-ttu-id="e3df5-211">Pré-gatilhos de banco de dados</span><span class="sxs-lookup"><span data-stu-id="e3df5-211">Database pre-triggers</span></span>
<span data-ttu-id="e3df5-212">O Cosmos DB oferece gatilhos que são executados ou disparados por uma operação em um documento.</span><span class="sxs-lookup"><span data-stu-id="e3df5-212">Cosmos DB provides triggers that are executed or triggered by an operation on a document.</span></span> <span data-ttu-id="e3df5-213">Por exemplo, você pode especificar um pré-gatilho ao criar um documento; esse pré-gatilho será executado antes que o documento seja criado.</span><span class="sxs-lookup"><span data-stu-id="e3df5-213">For example, you can specify a pre-trigger when you are creating a document – this pre-trigger will run before the document is created.</span></span> <span data-ttu-id="e3df5-214">A seguir está um exemplo de como os pré-gatilhos podem ser usados para validar as propriedades de um documento que está sendo criado:</span><span class="sxs-lookup"><span data-stu-id="e3df5-214">The following is an example of how pre-triggers can be used to validate the properties of a document that is being created:</span></span>

    var validateDocumentContentsTrigger = {
        id: "validateDocumentContents",
        serverScript: function validate() {
            var context = getContext();
            var request = context.getRequest();

            // document to be created in the current operation
            var documentToCreate = request.getBody();

            // validate properties
            if (!("timestamp" in documentToCreate)) {
                var ts = new Date();
                documentToCreate["my timestamp"] = ts.getTime();
            }

            // update the document that will be created
            request.setBody(documentToCreate);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.Create
    }


<span data-ttu-id="e3df5-215">E o código de registro do lado do cliente do Node.js para o gatilho:</span><span class="sxs-lookup"><span data-stu-id="e3df5-215">And the corresponding Node.js client-side registration code for the trigger:</span></span>

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


<span data-ttu-id="e3df5-216">Pré-gatilhos não podem ter parâmetros de entrada.</span><span class="sxs-lookup"><span data-stu-id="e3df5-216">Pre-triggers cannot have any input parameters.</span></span> <span data-ttu-id="e3df5-217">O objeto de solicitação pode ser usado para manipular a mensagem de solicitação associada à operação.</span><span class="sxs-lookup"><span data-stu-id="e3df5-217">The request object can be used to manipulate the request message associated with the operation.</span></span> <span data-ttu-id="e3df5-218">Aqui, o pré-gatilho está sendo executado com a criação de um documento, e o corpo da mensagem de solicitação contém o documento a ser criado no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="e3df5-218">Here, the pre-trigger is being run with the creation of a document, and the request message body contains the document to be created in JSON format.</span></span>   

<span data-ttu-id="e3df5-219">Quando os gatilhos são registrados, os usuários podem especificar as operações com as quais eles podem ser executados.</span><span class="sxs-lookup"><span data-stu-id="e3df5-219">When triggers are registered, users can specify the operations that it can run with.</span></span> <span data-ttu-id="e3df5-220">Este gatilho foi criado com TriggerOperation.Create, o que significa que a situação a seguir não é permitida.</span><span class="sxs-lookup"><span data-stu-id="e3df5-220">This trigger was created with TriggerOperation.Create, which means the following is not permitted.</span></span>

    var options = { preTriggerInclude: "validateDocumentContents" };

    client.replaceDocumentAsync(docToReplace.self,
                  newDocBody, options)
    .then(function (response) {
        console.log(response.resource);
    }, function (error) {
        console.log("Error", error);
    });

    // Fails, can’t use a create trigger in a replace operation

### <a name="database-post-triggers"></a><span data-ttu-id="e3df5-221">Pós-gatilhos de banco de dados</span><span class="sxs-lookup"><span data-stu-id="e3df5-221">Database post-triggers</span></span>
<span data-ttu-id="e3df5-222">Pós-gatilhos, assim como pré-gatilhos, são associados a uma operação em um documento e não assumem parâmetros de entrada.</span><span class="sxs-lookup"><span data-stu-id="e3df5-222">Post-triggers, like pre-triggers, are associated with an operation on a document and don’t take any input parameters.</span></span> <span data-ttu-id="e3df5-223">Eles são executados **após** a operação ter sido concluída, e possuem acesso à mensagem de resposta que é enviada ao cliente.</span><span class="sxs-lookup"><span data-stu-id="e3df5-223">They run **after** the operation has completed, and have access to the response message that is sent to the client.</span></span>   

<span data-ttu-id="e3df5-224">O exemplo a seguir mostra pós-gatilhos em ação:</span><span class="sxs-lookup"><span data-stu-id="e3df5-224">The following example shows post-triggers in action:</span></span>

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
            if(!accept) throw "Unable to update metadata, abort";

            function updateMetadataCallback(err, documents, responseOptions) {
                if(err) throw new Error("Error" + err.message);
                         if(documents.length != 1) throw 'Unable to find metadata document';

                         var metadataDocument = documents[0];

                         // update metadata
                         metadataDocument.createdDocuments += 1;
                         metadataDocument.createdNames += " " + createdDocument.id;
                         var accept = collection.replaceDocument(metadataDocument._self,
                               metadataDocument, function(err, docReplaced) {
                                      if(err) throw "Unable to update metadata, abort";
                               });
                         if(!accept) throw "Unable to update metadata, abort";
                         return;                    
            }                                                                                            
        },
        triggerType: TriggerType.Post,
        triggerOperation: TriggerOperation.All
    }


<span data-ttu-id="e3df5-225">O gatilho pode ser registrado como mostrado na amostra a seguir.</span><span class="sxs-lookup"><span data-stu-id="e3df5-225">The trigger can be registered as shown in the following sample.</span></span>

    // register post-trigger
    client.createTriggerAsync('dbs/testdb/colls/testColl', updateMetadataTrigger)
        .then(function(createdTrigger) { 
            var docToCreate = { 
                name: "artist_profile_1023",
                artist: "The Band",
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


<span data-ttu-id="e3df5-226">Esse gatilho consulta o documento de metadados e o atualiza com detalhes sobre o documento recém-criado.</span><span class="sxs-lookup"><span data-stu-id="e3df5-226">This trigger queries for the metadata document and updates it with details about the newly created document.</span></span>  

<span data-ttu-id="e3df5-227">É importante observar a execução **transacional** de gatilhos no Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e3df5-227">One thing that is important to note is the **transactional** execution of triggers in Cosmos DB.</span></span> <span data-ttu-id="e3df5-228">Esse pós-gatilho é executado como parte da mesma transação como a criação do documento original.</span><span class="sxs-lookup"><span data-stu-id="e3df5-228">This post-trigger runs as part of the same transaction as the creation of the original document.</span></span> <span data-ttu-id="e3df5-229">Portanto, se lançarmos uma exceção a partir do pós-gatilho (digamos, se não for possível atualizar o documento de metadados), toda a transação falhará e será retrocedida.</span><span class="sxs-lookup"><span data-stu-id="e3df5-229">Therefore, if we throw an exception from the post-trigger (say if we are unable to update the metadata document), the whole transaction will fail and be rolled back.</span></span> <span data-ttu-id="e3df5-230">Nenhum documento será criado e uma exceção será retornada.</span><span class="sxs-lookup"><span data-stu-id="e3df5-230">No document will be created, and an exception will be returned.</span></span>  

## <span data-ttu-id="e3df5-231"><a id="udf"></a>Funções definidas pelo usuário</span><span class="sxs-lookup"><span data-stu-id="e3df5-231"><a id="udf"></a>User-defined functions</span></span>
<span data-ttu-id="e3df5-232">As UDFs (funções definidas pelo usuário) são usadas para estender a gramática da linguagem de consulta SQL da API do DocumentDB e implementar uma lógica de negócios personalizada.</span><span class="sxs-lookup"><span data-stu-id="e3df5-232">User-defined functions (UDFs) are used to extend the DocumentDB API SQL query language grammar and implement custom business logic.</span></span> <span data-ttu-id="e3df5-233">Elas podem ser invocadas somente de dentro das consultas.</span><span class="sxs-lookup"><span data-stu-id="e3df5-233">They can only be called from inside queries.</span></span> <span data-ttu-id="e3df5-234">Elas não possuem acesso ao objeto de contexto e devem ser usadas como JavaScript somente para cálculo.</span><span class="sxs-lookup"><span data-stu-id="e3df5-234">They do not have access to the context object and are meant to be used as compute-only JavaScript.</span></span> <span data-ttu-id="e3df5-235">Portanto, as UDFs podem ser executadas em réplicas secundárias do serviço Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e3df5-235">Therefore, UDFs can be run on secondary replicas of the Cosmos DB service.</span></span>  

<span data-ttu-id="e3df5-236">A amostra a seguir cria uma UDF para calcular o imposto de renda com base nas taxas para diversos intervalos de renda, e depois a utiliza dentro de uma consulta para descobrir todas as pessoas que pagaram mais de $20.000 em impostos.</span><span class="sxs-lookup"><span data-stu-id="e3df5-236">The following sample creates a UDF to calculate income tax based on rates for various income brackets, and then uses it inside a query to find all people who paid more than $20,000 in taxes.</span></span>

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


<span data-ttu-id="e3df5-237">A UDF pode, subsequentemente, ser usada em consultas como na amostra a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3df5-237">The UDF can subsequently be used in queries like in the following sample:</span></span>

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

## <a name="javascript-language-integrated-query-api"></a><span data-ttu-id="e3df5-238">API de consulta integrada da linguagem JavaScript</span><span class="sxs-lookup"><span data-stu-id="e3df5-238">JavaScript language-integrated query API</span></span>
<span data-ttu-id="e3df5-239">Além de emitir consultas usando a gramática SQL do DocumentDB, o SDK do servidor permite que você execute consultas otimizadas usando uma interface fluente do JavaScript sem qualquer conhecimento de SQL.</span><span class="sxs-lookup"><span data-stu-id="e3df5-239">In addition to issuing queries using DocumentDB’s SQL grammar, the server-side SDK allows you to perform optimized queries using a fluent JavaScript interface without any knowledge of SQL.</span></span> <span data-ttu-id="e3df5-240">A API de consulta JavaScript permite que você crie consultas programaticamente ao passar funções de predicado em chamadas a função encadeáveis, com uma sintaxe semelhantes a bibliotecas JavaScript internas e conhecidas da Matriz ECMAScript5, como lodash.</span><span class="sxs-lookup"><span data-stu-id="e3df5-240">The JavaScript query API allows you to programmatically build queries by passing predicate functions into chainable function calls, with a syntax familiar to ECMAScript5's Array built-ins and popular JavaScript libraries like lodash.</span></span> <span data-ttu-id="e3df5-241">As consultas são analisadas no tempo de execução do JavaScript para serem executadas com eficiência usando índices do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e3df5-241">Queries are parsed by the JavaScript runtime to be executed efficiently using Azure Cosmos DB’s indices.</span></span>

> [!NOTE]
> <span data-ttu-id="e3df5-242">`__` (double-underscore) é um alias para `getContext().getCollection()`.</span><span class="sxs-lookup"><span data-stu-id="e3df5-242">`__` (double-underscore) is an alias to `getContext().getCollection()`.</span></span>
> <br/>
> <span data-ttu-id="e3df5-243">Em outras palavras, você pode usar `__` ou `getContext().getCollection()` para acessar a API de consulta JavaScript.</span><span class="sxs-lookup"><span data-stu-id="e3df5-243">In other words, you can use `__` or `getContext().getCollection()` to access the JavaScript query API.</span></span>
> 
> 

<span data-ttu-id="e3df5-244">As funções permitidas incluem:</span><span class="sxs-lookup"><span data-stu-id="e3df5-244">Supported functions include:</span></span>

<ul>
<li><span data-ttu-id="e3df5-245">
<b>chain() ... .value([callback] [, opções])</b>
</span><span class="sxs-lookup"><span data-stu-id="e3df5-245">
<b>chain() ... .value([callback] [, options])</b>
</span></span><ul>
<li>
<span data-ttu-id="e3df5-246">Inicia uma chamada encadeada que deve ser terminada com value().</span><span class="sxs-lookup"><span data-stu-id="e3df5-246">Starts a chained call which must be terminated with value().</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="e3df5-247">
<b>filter(predicateFunction [, opções] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="e3df5-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="e3df5-248">Filtra a entrada usando uma função de predicado que retorna true/false para filtrar documentos de entrada no conjunto resultante.</span><span class="sxs-lookup"><span data-stu-id="e3df5-248">Filters the input using a predicate function which returns true/false in order to filter in/out input documents into the resulting set.</span></span> <span data-ttu-id="e3df5-249">Esse comportamento é semelhante ao de uma cláusula WHERE no SQL.</span><span class="sxs-lookup"><span data-stu-id="e3df5-249">This behaves similar to a WHERE clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="e3df5-250">
<b>map(transformationFunction [, opções] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="e3df5-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="e3df5-251">Aplica uma projeção dada uma função de transformação que mapeia cada item de entrada para um objeto ou valor JavaScript.</span><span class="sxs-lookup"><span data-stu-id="e3df5-251">Applies a projection given a transformation function which maps each input item to a JavaScript object or value.</span></span> <span data-ttu-id="e3df5-252">Esse comportamento é semelhante ao de uma cláusula SELECT no SQL.</span><span class="sxs-lookup"><span data-stu-id="e3df5-252">This behaves similar to a SELECT clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="e3df5-253">
<b>pluck([propertyName] [, opções] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="e3df5-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="e3df5-254">Esse é um atalho para um mapa que extrai o valor de uma única propriedade de cada item de entrada.</span><span class="sxs-lookup"><span data-stu-id="e3df5-254">This is a shortcut for a map which extracts the value of a single property from each input item.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="e3df5-255">
<b>flatten([isShallow] [, opções] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="e3df5-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="e3df5-256">Combina e nivela as matrizes de cada item de entrada em uma única matriz.</span><span class="sxs-lookup"><span data-stu-id="e3df5-256">Combines and flattens arrays from each input item in to a single array.</span></span> <span data-ttu-id="e3df5-257">Esse comportamento é semelhante ao de SelectMany no LINQ.</span><span class="sxs-lookup"><span data-stu-id="e3df5-257">This behaves similar to SelectMany in LINQ.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="e3df5-258">
<b>sortBy([predicate] [, opções] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="e3df5-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="e3df5-259">Produz um novo conjunto de documentos classificando os documentos no fluxo de documentos de entrada em ordem crescente usando o predicado em questão.</span><span class="sxs-lookup"><span data-stu-id="e3df5-259">Produce a new set of documents by sorting the documents in the input document stream in ascending order using the given predicate.</span></span> <span data-ttu-id="e3df5-260">Esse comportamento é semelhante ao da cláusula ORDER BY no SQL.</span><span class="sxs-lookup"><span data-stu-id="e3df5-260">This behaves similar to a ORDER BY clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="e3df5-261">
<b>sortByDescending([predicate] [, opções] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="e3df5-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="e3df5-262">Produz um novo conjunto de documentos classificando os documentos no fluxo de documentos de entrada em ordem decrescente usando o predicado em questão.</span><span class="sxs-lookup"><span data-stu-id="e3df5-262">Produce a new set of documents by sorting the documents in the input document stream in descending order using the given predicate.</span></span> <span data-ttu-id="e3df5-263">Esse comportamento é semelhante ao da cláusula ORDER BY x DESC no SQL.</span><span class="sxs-lookup"><span data-stu-id="e3df5-263">This behaves similar to a ORDER BY x DESC clause in SQL.</span></span>
</li>
</ul>
</li>
</ul>


<span data-ttu-id="e3df5-264">Quando incluídas em funções de predicado e/ou do seletor, os constructos do JavaScript a seguir são automaticamente otimizados para serem executados diretamente nos índices do Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="e3df5-264">When included inside predicate and/or selector functions, the following JavaScript constructs get automatically optimized to run directly on Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="e3df5-265">Operadores simples: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span><span class="sxs-lookup"><span data-stu-id="e3df5-265">Simple operators: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span></span> ~
* <span data-ttu-id="e3df5-266">Literais, incluindo o literal de objeto: {}</span><span class="sxs-lookup"><span data-stu-id="e3df5-266">Literals, including the object literal: {}</span></span>
* <span data-ttu-id="e3df5-267">var, return</span><span class="sxs-lookup"><span data-stu-id="e3df5-267">var, return</span></span>

<span data-ttu-id="e3df5-268">Os seguintes constructos do JavaScript não são otimizados pelos índices do Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="e3df5-268">The following JavaScript constructs do not get optimized for Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="e3df5-269">Fluxo de controle (por exemplo,. if, for, while)</span><span class="sxs-lookup"><span data-stu-id="e3df5-269">Control flow (e.g. if, for, while)</span></span>
* <span data-ttu-id="e3df5-270">Chamadas de função</span><span class="sxs-lookup"><span data-stu-id="e3df5-270">Function calls</span></span>

<span data-ttu-id="e3df5-271">Para saber mais, consulte nossos [JSDocs no servidor](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="e3df5-271">For more information, please see our [Server-Side JSDocs](http://azure.github.io/azure-documentdb-js-server/).</span></span>

### <a name="example-write-a-stored-procedure-using-the-javascript-query-api"></a><span data-ttu-id="e3df5-272">Exemplo: Escrever um procedimento armazenado usando a API de consulta JavaScript</span><span class="sxs-lookup"><span data-stu-id="e3df5-272">Example: Write a stored procedure using the JavaScript query API</span></span>
<span data-ttu-id="e3df5-273">O exemplo de código a seguir mostra como a API de Consulta JavaScript pode ser usada no contexto de um procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="e3df5-273">The following code sample is an example of how the JavaScript Query API can be used in the context of a stored procedure.</span></span> <span data-ttu-id="e3df5-274">O procedimento armazenado insere um documento, fornecido por um parâmetro de entrada e atualiza um documento de metadados usando o método `__.filter()` com minSize, maxSize e totalSize baseados na propriedade de tamanho do documento de entrada.</span><span class="sxs-lookup"><span data-stu-id="e3df5-274">The stored procedure inserts a document, given by an input parameter, and updates a metadata document, using the `__.filter()` method, with minSize, maxSize, and totalSize based upon the input document's size property.</span></span>

    /**
     * Insert actual doc and update metadata doc: minSize, maxSize, totalSize based on doc.size.
     */
    function insertDocumentAndUpdateMetadata(doc) {
      // HTTP error codes sent to our callback funciton by DocDB server.
      var ErrorCode = {
        RETRY_WITH: 449,
      }

      var isAccepted = __.createDocument(__.getSelfLink(), doc, {}, function(err, doc, options) {
        if (err) throw err;

        // Check the doc (ignore docs with invalid/zero size and metaDoc itself) and call updateMetadata.
        if (!doc.isMetadata && doc.size > 0) {
          // Get the meta document. We keep it in the same collection. it's the only doc that has .isMetadata = true.
          var result = __.filter(function(x) {
            return x.isMetadata === true
          }, function(err, feed, options) {
            if (err) throw err;

            // We assume that metadata doc was pre-created and must exist when this script is called.
            if (!feed || !feed.length) throw new Error("Failed to find the metadata document.");

            // The metadata document.
            var metaDoc = feed[0];

            // Update metaDoc.minSize:
            // for 1st document use doc.Size, for all the rest see if it's less than last min.
            if (metaDoc.minSize == 0) metaDoc.minSize = doc.size;
            else metaDoc.minSize = Math.min(metaDoc.minSize, doc.size);

            // Update metaDoc.maxSize.
            metaDoc.maxSize = Math.max(metaDoc.maxSize, doc.size);

            // Update metaDoc.totalSize.
            metaDoc.totalSize += doc.size;

            // Update/replace the metadata document in the store.
            var isAccepted = __.replaceDocument(metaDoc._self, metaDoc, function(err) {
              if (err) throw err;
              // Note: in case concurrent updates causes conflict with ErrorCode.RETRY_WITH, we can't read the meta again 
              //       and update again because due to Snapshot isolation we will read same exact version (we are in same transaction).
              //       We have to take care of that on the client side.
            });
            if (!isAccepted) throw new Error("replaceDocument(metaDoc) returned false.");
          });
          if (!result.isAccepted) throw new Error("filter for metaDoc returned false.");
        }
      });
      if (!isAccepted) throw new Error("createDocument(actual doc) returned false.");
    }

## <a name="sql-to-javascript-cheat-sheet"></a><span data-ttu-id="e3df5-275">Folha de respostas rápidas do SQL para Javascript</span><span class="sxs-lookup"><span data-stu-id="e3df5-275">SQL to Javascript cheat sheet</span></span>
<span data-ttu-id="e3df5-276">A tabela a seguir apresenta várias consultas SQL e as consultas JavaScript correspondentes.</span><span class="sxs-lookup"><span data-stu-id="e3df5-276">The following table presents various SQL queries and the corresponding JavaScript queries.</span></span>

<span data-ttu-id="e3df5-277">Assim como acontece com consultas SQL, as chaves de propriedade do documento (por exemplo, `doc.id`) diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="e3df5-277">As with SQL queries, document property keys (e.g. `doc.id`) are case-sensitive.</span></span>

|<span data-ttu-id="e3df5-278">SQL</span><span class="sxs-lookup"><span data-stu-id="e3df5-278">SQL</span></span>| <span data-ttu-id="e3df5-279">API de consulta do JavaScript</span><span class="sxs-lookup"><span data-stu-id="e3df5-279">JavaScript Query API</span></span>|<span data-ttu-id="e3df5-280">Descrição abaixo</span><span class="sxs-lookup"><span data-stu-id="e3df5-280">Description below</span></span>|
|---|---|---|
|<span data-ttu-id="e3df5-281">SELECIONAR *</span><span class="sxs-lookup"><span data-stu-id="e3df5-281">SELECT *</span></span><br><span data-ttu-id="e3df5-282">FROM docs</span><span class="sxs-lookup"><span data-stu-id="e3df5-282">FROM docs</span></span>| <span data-ttu-id="e3df5-283">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="e3df5-283">__.map(function(doc) {</span></span> <br><span data-ttu-id="e3df5-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span><span class="sxs-lookup"><span data-stu-id="e3df5-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span></span><br><span data-ttu-id="e3df5-285">});</span><span class="sxs-lookup"><span data-stu-id="e3df5-285">});</span></span>|<span data-ttu-id="e3df5-286">1</span><span class="sxs-lookup"><span data-stu-id="e3df5-286">1</span></span>|
|<span data-ttu-id="e3df5-287">SELECT docs.id, docs.message AS msg, docs.actions</span><span class="sxs-lookup"><span data-stu-id="e3df5-287">SELECT docs.id, docs.message AS msg, docs.actions</span></span> <br><span data-ttu-id="e3df5-288">FROM docs</span><span class="sxs-lookup"><span data-stu-id="e3df5-288">FROM docs</span></span>|<span data-ttu-id="e3df5-289">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="e3df5-289">__.map(function(doc) {</span></span><br><span data-ttu-id="e3df5-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="e3df5-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="e3df5-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="e3df5-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="e3df5-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span><span class="sxs-lookup"><span data-stu-id="e3df5-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span></span><br><span data-ttu-id="e3df5-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span><span class="sxs-lookup"><span data-stu-id="e3df5-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span></span><br><span data-ttu-id="e3df5-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="e3df5-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="e3df5-295">});</span><span class="sxs-lookup"><span data-stu-id="e3df5-295">});</span></span>|<span data-ttu-id="e3df5-296">2</span><span class="sxs-lookup"><span data-stu-id="e3df5-296">2</span></span>|
|<span data-ttu-id="e3df5-297">SELECIONAR *</span><span class="sxs-lookup"><span data-stu-id="e3df5-297">SELECT *</span></span><br><span data-ttu-id="e3df5-298">FROM docs</span><span class="sxs-lookup"><span data-stu-id="e3df5-298">FROM docs</span></span><br><span data-ttu-id="e3df5-299">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="e3df5-299">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="e3df5-300">__.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="e3df5-300">__.filter(function(doc) {</span></span><br><span data-ttu-id="e3df5-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="e3df5-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="e3df5-302">});</span><span class="sxs-lookup"><span data-stu-id="e3df5-302">});</span></span>|<span data-ttu-id="e3df5-303">3</span><span class="sxs-lookup"><span data-stu-id="e3df5-303">3</span></span>|
|<span data-ttu-id="e3df5-304">SELECIONAR *</span><span class="sxs-lookup"><span data-stu-id="e3df5-304">SELECT *</span></span><br><span data-ttu-id="e3df5-305">FROM docs</span><span class="sxs-lookup"><span data-stu-id="e3df5-305">FROM docs</span></span><br><span data-ttu-id="e3df5-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span><span class="sxs-lookup"><span data-stu-id="e3df5-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span></span>|<span data-ttu-id="e3df5-307">__.filter(function(x) {</span><span class="sxs-lookup"><span data-stu-id="e3df5-307">__.filter(function(x) {</span></span><br><span data-ttu-id="e3df5-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span><span class="sxs-lookup"><span data-stu-id="e3df5-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span></span><br><span data-ttu-id="e3df5-309">});</span><span class="sxs-lookup"><span data-stu-id="e3df5-309">});</span></span>|<span data-ttu-id="e3df5-310">4</span><span class="sxs-lookup"><span data-stu-id="e3df5-310">4</span></span>|
|<span data-ttu-id="e3df5-311">SELECT docs.id, docs.message AS msg</span><span class="sxs-lookup"><span data-stu-id="e3df5-311">SELECT docs.id, docs.message AS msg</span></span><br><span data-ttu-id="e3df5-312">FROM docs</span><span class="sxs-lookup"><span data-stu-id="e3df5-312">FROM docs</span></span><br><span data-ttu-id="e3df5-313">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="e3df5-313">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="e3df5-314">__.chain()</span><span class="sxs-lookup"><span data-stu-id="e3df5-314">__.chain()</span></span><br><span data-ttu-id="e3df5-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="e3df5-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="e3df5-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="e3df5-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="e3df5-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="e3df5-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="e3df5-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="e3df5-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span></span><br><span data-ttu-id="e3df5-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="e3df5-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="e3df5-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="e3df5-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="e3df5-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span><span class="sxs-lookup"><span data-stu-id="e3df5-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span></span><br><span data-ttu-id="e3df5-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="e3df5-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="e3df5-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="e3df5-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="e3df5-324">.value();</span><span class="sxs-lookup"><span data-stu-id="e3df5-324">.value();</span></span>|<span data-ttu-id="e3df5-325">5</span><span class="sxs-lookup"><span data-stu-id="e3df5-325">5</span></span>|
|<span data-ttu-id="e3df5-326">SELECT VALUE tag</span><span class="sxs-lookup"><span data-stu-id="e3df5-326">SELECT VALUE tag</span></span><br><span data-ttu-id="e3df5-327">FROM docs</span><span class="sxs-lookup"><span data-stu-id="e3df5-327">FROM docs</span></span><br><span data-ttu-id="e3df5-328">JOIN tag IN docs.Tags</span><span class="sxs-lookup"><span data-stu-id="e3df5-328">JOIN tag IN docs.Tags</span></span><br><span data-ttu-id="e3df5-329">ORDER BY docs._ts</span><span class="sxs-lookup"><span data-stu-id="e3df5-329">ORDER BY docs._ts</span></span>|<span data-ttu-id="e3df5-330">__.chain()</span><span class="sxs-lookup"><span data-stu-id="e3df5-330">__.chain()</span></span><br><span data-ttu-id="e3df5-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="e3df5-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="e3df5-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span><span class="sxs-lookup"><span data-stu-id="e3df5-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span></span><br><span data-ttu-id="e3df5-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="e3df5-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="e3df5-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="e3df5-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span></span><br><span data-ttu-id="e3df5-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span><span class="sxs-lookup"><span data-stu-id="e3df5-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span></span><br><span data-ttu-id="e3df5-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="e3df5-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="e3df5-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span><span class="sxs-lookup"><span data-stu-id="e3df5-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span></span><br><span data-ttu-id="e3df5-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span><span class="sxs-lookup"><span data-stu-id="e3df5-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span></span><br><span data-ttu-id="e3df5-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span><span class="sxs-lookup"><span data-stu-id="e3df5-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span></span>|<span data-ttu-id="e3df5-340">6</span><span class="sxs-lookup"><span data-stu-id="e3df5-340">6</span></span>|

<span data-ttu-id="e3df5-341">As descrições a seguir explicam cada consulta na tabela acima.</span><span class="sxs-lookup"><span data-stu-id="e3df5-341">The following descriptions explain each query in the table above.</span></span>
1. <span data-ttu-id="e3df5-342">Resulta em todos os documentos (paginados com token de continuação) no estado em que se encontram.</span><span class="sxs-lookup"><span data-stu-id="e3df5-342">Results in all documents (paginated with continuation token) as is.</span></span>
2. <span data-ttu-id="e3df5-343">Projeta a ID, a mensagem (com o alias msg) e a ação de todos os documentos.</span><span class="sxs-lookup"><span data-stu-id="e3df5-343">Projects the id, message (aliased to msg), and action from all documents.</span></span>
3. <span data-ttu-id="e3df5-344">Consulta documentos com o predicado : id = "X998_Y998".</span><span class="sxs-lookup"><span data-stu-id="e3df5-344">Queries for documents with the predicate: id = "X998_Y998".</span></span>
4. <span data-ttu-id="e3df5-345">Consulta documentos com uma propriedade Tags e Tags é uma matriz que contém o valor 123.</span><span class="sxs-lookup"><span data-stu-id="e3df5-345">Queries for documents that have a Tags property and Tags is an array containing the value 123.</span></span>
5. <span data-ttu-id="e3df5-346">Consulta documentos com um predicado, id = "X998_Y998" e projeta a ID e a mensagem (com alias para msg).</span><span class="sxs-lookup"><span data-stu-id="e3df5-346">Queries for documents with a predicate, id = "X998_Y998", and then projects the id and message (aliased to msg).</span></span>
6. <span data-ttu-id="e3df5-347">Filtra documentos que têm uma propriedade de matriz, Tags, e classifica os documentos resultantes pela propriedade do sistema do carimbo de data/hora _ts e projeta + mescla a matriz Tags.</span><span class="sxs-lookup"><span data-stu-id="e3df5-347">Filters for documents which have an array property, Tags, and sorts the resulting documents by the _ts timestamp system property, and then projects + flattens the Tags array.</span></span>


## <a name="runtime-support"></a><span data-ttu-id="e3df5-348">Suporte de tempo de execução</span><span class="sxs-lookup"><span data-stu-id="e3df5-348">Runtime support</span></span>
<span data-ttu-id="e3df5-349">A [API do lado do servidor de JavaScript do DocumentDB](http://azure.github.io/azure-documentdb-js-server/) dá suporte para a maioria dos principais recursos de linguagem JavaScript conforme padronizado pelo [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span><span class="sxs-lookup"><span data-stu-id="e3df5-349">[DocumentDB JavaScript server side API](http://azure.github.io/azure-documentdb-js-server/) provides support for the most of the mainstream JavaScript language features as standardized by [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span></span>

### <a name="security"></a><span data-ttu-id="e3df5-350">Segurança</span><span class="sxs-lookup"><span data-stu-id="e3df5-350">Security</span></span>
<span data-ttu-id="e3df5-351">Procedimentos armazenados e gatilhos de JavaScript são colocados em uma área restrita para que os efeitos de um script não vazem para o outro sem passar pelo isolamento da transação de captura instantânea no nível do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e3df5-351">JavaScript stored procedures and triggers are sandboxed so that the effects of one script do not leak to the other without going through the snapshot transaction isolation at the database level.</span></span> <span data-ttu-id="e3df5-352">Os ambientes de tempo de execução são colocados em pools, porém, seu contexto é limpo após cada execução.</span><span class="sxs-lookup"><span data-stu-id="e3df5-352">The runtime environments are pooled but cleaned of the context after each run.</span></span> <span data-ttu-id="e3df5-353">Portanto, sua segurança é garantida e cada um deles está livre de qualquer efeito colateral inesperado advindo do outro.</span><span class="sxs-lookup"><span data-stu-id="e3df5-353">Hence they are guaranteed to be safe of any unintended side effects from each other.</span></span>

### <a name="pre-compilation"></a><span data-ttu-id="e3df5-354">Pré-compilação</span><span class="sxs-lookup"><span data-stu-id="e3df5-354">Pre-compilation</span></span>
<span data-ttu-id="e3df5-355">Os procedimentos armazenados, gatilhos e UDFs são pré-compilados implicitamente para o formato de código de bytes a fim de evitar o custo de compilação no momento da invocação de cada script.</span><span class="sxs-lookup"><span data-stu-id="e3df5-355">Stored procedures, triggers and UDFs are implicitly precompiled to the byte code format in order to avoid compilation cost at the time of each script invocation.</span></span> <span data-ttu-id="e3df5-356">Isso assegura que as invocações dos procedimentos armazenados sejam rápidas e possuam baixa pegada.</span><span class="sxs-lookup"><span data-stu-id="e3df5-356">This ensures invocations of stored procedures are fast and have a low footprint.</span></span>

## <a name="client-sdk-support"></a><span data-ttu-id="e3df5-357">Suporte de SDK de cliente</span><span class="sxs-lookup"><span data-stu-id="e3df5-357">Client SDK support</span></span>
<span data-ttu-id="e3df5-358">Além da API do DocumentDB para o cliente [Node.js](documentdb-sdk-node.md), o Azure Cosmos DB tem SDKs do [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [JavaScript](http://azure.github.io/azure-documentdb-js/) e [Python](documentdb-sdk-python.md) para a API do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="e3df5-358">In addition to the DocumentDB API for [Node.js](documentdb-sdk-node.md) client, Azure Cosmos DB has [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [JavaScript](http://azure.github.io/azure-documentdb-js/), and [Python SDKs](documentdb-sdk-python.md) for the DocumentDB API.</span></span> <span data-ttu-id="e3df5-359">Os procedimentos armazenados, gatilhos e UDFs também podem ser criados e executados usando qualquer um desses SDKs.</span><span class="sxs-lookup"><span data-stu-id="e3df5-359">Stored procedures, triggers and UDFs can be created and executed using any of these SDKs as well.</span></span> <span data-ttu-id="e3df5-360">O exemplo a seguir mostra como criar e executar um procedimento armazenado usando o cliente .NET.</span><span class="sxs-lookup"><span data-stu-id="e3df5-360">The following example shows how to create and execute a stored procedure using the .NET client.</span></span> <span data-ttu-id="e3df5-361">Observe como os tipos .NET são transferidos para o procedimento armazenado como JSON e lidos novamente.</span><span class="sxs-lookup"><span data-stu-id="e3df5-361">Note how the .NET types are passed into the stored procedure as JSON and read back.</span></span>

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


<span data-ttu-id="e3df5-362">Esse exemplo mostra como usar a [API do .NET do DocumentDB](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) para criar um pré-gatilho e criar um documento com o gatilho habilitado.</span><span class="sxs-lookup"><span data-stu-id="e3df5-362">This sample shows how to use the [DocumentDB .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) to create a pre-trigger and create a document with the trigger enabled.</span></span> 

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


<span data-ttu-id="e3df5-363">E o exemplo a seguir mostra como criar uma UDF (função definida pelo usuário) e usá-la em uma [consulta SQL da API do DocumentDB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="e3df5-363">And the following example shows how to create a user defined function (UDF) and use it in a [DocumentDB API SQL query](documentdb-sql-query.md).</span></span>

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

## <a name="rest-api"></a><span data-ttu-id="e3df5-364">API REST</span><span class="sxs-lookup"><span data-stu-id="e3df5-364">REST API</span></span>
<span data-ttu-id="e3df5-365">Todas as operações do Azure Cosmos DB podem ser realizadas de maneira RESTful.</span><span class="sxs-lookup"><span data-stu-id="e3df5-365">All Azure Cosmos DB operations can be performed in a RESTful manner.</span></span> <span data-ttu-id="e3df5-366">Procedimentos armazenados, gatilhos e funções definidas pelo usuário podem ser registrados em uma coleção usando HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="e3df5-366">Stored procedures, triggers and user-defined functions can be registered under a collection by using HTTP POST.</span></span> <span data-ttu-id="e3df5-367">A seguir está um exemplo sobre como registrar um procedimento armazenado:</span><span class="sxs-lookup"><span data-stu-id="e3df5-367">The following is an example of how to register a stored procedure:</span></span>

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


<span data-ttu-id="e3df5-368">O procedimento armazenado é registrado pela execução de uma solicitação POST em relação ao URI dbs/testdb/colls/testColl/sprocs com o corpo contendo o procedimento armazenado a ser criado.</span><span class="sxs-lookup"><span data-stu-id="e3df5-368">The stored procedure is registered by executing a POST request against the URI dbs/testdb/colls/testColl/sprocs with the body containing the stored procedure to create.</span></span> <span data-ttu-id="e3df5-369">Disparadores e UDFs podem ser registrados da mesma forma, emitindo um POST para /triggers e /udfs respectivamente.</span><span class="sxs-lookup"><span data-stu-id="e3df5-369">Triggers and UDFs can be registered similarly by issuing a POST against /triggers and /udfs respectively.</span></span>
<span data-ttu-id="e3df5-370">Este procedimento armazenado pode, então, ser executado emitindo uma solicitação POST ao link de recursos:</span><span class="sxs-lookup"><span data-stu-id="e3df5-370">This stored procedure can then be executed by issuing a POST request against its resource link:</span></span>

    POST https://<url>/sprocs/<sproc> HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:20 GMT


    [ { "name": "TestDocument", "book": "Autumn of the Patriarch"}, "Price", 200 ]


<span data-ttu-id="e3df5-371">Aqui, a entrada para o procedimento armazenado é transmitida no corpo de solicitação.</span><span class="sxs-lookup"><span data-stu-id="e3df5-371">Here, the input to the stored procedure is passed in the request body.</span></span> <span data-ttu-id="e3df5-372">Observe que a entrada é transmitida como uma matriz JSON de parâmetros de entrada.</span><span class="sxs-lookup"><span data-stu-id="e3df5-372">Note that the input is passed as a JSON array of input parameters.</span></span> <span data-ttu-id="e3df5-373">O procedimento armazenado assume a primeira entrada como um documento que é um corpo de resposta.</span><span class="sxs-lookup"><span data-stu-id="e3df5-373">The stored procedure takes the first input as a document that is a response body.</span></span> <span data-ttu-id="e3df5-374">A resposta recebida é a seguinte:</span><span class="sxs-lookup"><span data-stu-id="e3df5-374">The response we receive is as follows:</span></span>

    HTTP/1.1 200 OK

    { 
      name: 'TestDocument',
      book: ‘Autumn of the Patriarch’,
      id: ‘V7tQANV3rAkDAAAAAAAAAA==‘,
      ts: 1407830727,
      self: ‘dbs/V7tQAA==/colls/V7tQANV3rAk=/docs/V7tQANV3rAkDAAAAAAAAAA==/’,
      etag: ‘6c006596-0000-0000-0000-53e9cac70000’,
      attachments: ‘attachments/’,
      Price: 200
    }


<span data-ttu-id="e3df5-375">Gatilhos, diferentemente dos procedimentos armazenados, não podem ser executados diretamente.</span><span class="sxs-lookup"><span data-stu-id="e3df5-375">Triggers, unlike stored procedures, cannot be executed directly.</span></span> <span data-ttu-id="e3df5-376">Ao invés disso, eles são executados como parte de uma operação em um documento.</span><span class="sxs-lookup"><span data-stu-id="e3df5-376">Instead they are executed as part of an operation on a document.</span></span> <span data-ttu-id="e3df5-377">Podemos especificar os gatilhos a serem executados com uma solicitação usando cabeçalhos HTTP.</span><span class="sxs-lookup"><span data-stu-id="e3df5-377">We can specify the triggers to run with a request using HTTP headers.</span></span> <span data-ttu-id="e3df5-378">A seguir está uma solicitação para criar um documento.</span><span class="sxs-lookup"><span data-stu-id="e3df5-378">The following is request to create a document.</span></span>

    POST https://<url>/docs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT
    x-ms-documentdb-pre-trigger-include: validateDocumentContents 
    x-ms-documentdb-post-trigger-include: bookCreationPostTrigger


    {
       "name": "newDocument",
       “title”: “The Wizard of Oz”,
       “author”: “Frank Baum”,
       “pages”: 92
    }


<span data-ttu-id="e3df5-379">Aqui, o pré-gatilho a ser executado com a solicitação é especificado no cabeçalho x-ms-documentdb-pre-trigger-include.</span><span class="sxs-lookup"><span data-stu-id="e3df5-379">Here the pre-trigger to be run with the request is specified in the x-ms-documentdb-pre-trigger-include header.</span></span> <span data-ttu-id="e3df5-380">Da mesma forma, qualquer pós-gatilho é fornecido no cabeçalho x-ms-documentdb-post-trigger-include.</span><span class="sxs-lookup"><span data-stu-id="e3df5-380">Correspondingly, any post-triggers are given in the x-ms-documentdb-post-trigger-include header.</span></span> <span data-ttu-id="e3df5-381">Observe que pré e pós-gatilhos podem ser especificados para uma determinada solicitação.</span><span class="sxs-lookup"><span data-stu-id="e3df5-381">Note that both pre- and post-triggers can be specified for a given request.</span></span>

## <a name="sample-code"></a><span data-ttu-id="e3df5-382">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="e3df5-382">Sample code</span></span>
<span data-ttu-id="e3df5-383">Você pode encontrar mais exemplos de código do lado do servidor (incluindo [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js) e [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) em nosso [repositório GitHub](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span><span class="sxs-lookup"><span data-stu-id="e3df5-383">You can find more server-side code examples (including [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js), and [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) on our [GitHub repository](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span></span>

<span data-ttu-id="e3df5-384">Deseja compartilhar seu procedimento armazenado incrível?</span><span class="sxs-lookup"><span data-stu-id="e3df5-384">Want to share your awesome stored procedure?</span></span> <span data-ttu-id="e3df5-385">Por favor, envie uma solicitação pull!</span><span class="sxs-lookup"><span data-stu-id="e3df5-385">Please, send us a pull-request!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e3df5-386">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e3df5-386">Next steps</span></span>
<span data-ttu-id="e3df5-387">Depois de criar um ou mais procedimentos armazenados, gatilhos e funções definidas pelo usuário, você pode carregá-los e exibi-los no Portal do Azure usando o Data Explorer.</span><span class="sxs-lookup"><span data-stu-id="e3df5-387">Once you have one or more stored procedures, triggers, and user-defined functions created, you can load them and view them in the Azure portal using Data Explorer.</span></span>

<span data-ttu-id="e3df5-388">Você também pode achar as seguintes referências e recursos úteis em seu caminho para saber mais sobre a programação no servidor do Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="e3df5-388">You may also find the following references and resources useful in your path to learn more about Azure Cosmos dB server-side programming:</span></span>

* [<span data-ttu-id="e3df5-389">SDKs do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e3df5-389">Azure Cosmos DB SDKs</span></span>](documentdb-sdk-dotnet.md)
* [<span data-ttu-id="e3df5-390">Estudo do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="e3df5-390">DocumentDB Studio</span></span>](https://github.com/mingaliu/DocumentDBStudio/releases)
* [<span data-ttu-id="e3df5-391">JSON</span><span class="sxs-lookup"><span data-stu-id="e3df5-391">JSON</span></span>](http://www.json.org/) 
* [<span data-ttu-id="e3df5-392">JavaScript ECMA-262</span><span class="sxs-lookup"><span data-stu-id="e3df5-392">JavaScript ECMA-262</span></span>](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
* [<span data-ttu-id="e3df5-393">Extensibilidade de banco de dados seguro e portátil</span><span class="sxs-lookup"><span data-stu-id="e3df5-393">Secure and Portable Database Extensibility</span></span>](http://dl.acm.org/citation.cfm?id=276339) 
* [<span data-ttu-id="e3df5-394">Arquitetura de banco de dados orientada a serviços</span><span class="sxs-lookup"><span data-stu-id="e3df5-394">Service Oriented Database Architecture</span></span>](http://dl.acm.org/citation.cfm?id=1066267&coll=Portal&dl=GUIDE) 
* [<span data-ttu-id="e3df5-395">Hospedando o Runtime do .NET no Microsoft SQL Server</span><span class="sxs-lookup"><span data-stu-id="e3df5-395">Hosting the .NET Runtime in Microsoft SQL server</span></span>](http://dl.acm.org/citation.cfm?id=1007669)

