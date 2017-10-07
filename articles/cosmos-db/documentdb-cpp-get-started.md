---
title: tutorial aaaC + + para o banco de dados do Azure Cosmos | Microsoft Docs
description: "Um tutorial de C++ que cria um aplicativo de banco de dados e console em C++ usando um SDK endossado pelo Azure Cosmos DB para C++. O Azure Cosmos DB é um serviço de banco de dados de escala mundial."
services: cosmos-db
documentationcenter: cpp
author: asthana86
manager: jhubbard
editor: 
ms.assetid: b8756b60-8d41-4231-ba4f-6cfcfe3b4bab
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 12/25/2016
ms.author: aasthan
ms.openlocfilehash: 2d5eeff349b7753e39936b7eb77557ad30c5830a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-c-console-application-tutorial-for-hello-documentdb-api"></a><span data-ttu-id="56af5-104">Cosmos do Azure DB: Tutorial do aplicativo de console C++ para Olá API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="56af5-104">Azure Cosmos DB: C++ console application tutorial for hello DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="56af5-105">.NET</span><span class="sxs-lookup"><span data-stu-id="56af5-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="56af5-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="56af5-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="56af5-107">Node.js para MongoDB</span><span class="sxs-lookup"><span data-stu-id="56af5-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="56af5-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="56af5-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="56af5-109">Java</span><span class="sxs-lookup"><span data-stu-id="56af5-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="56af5-110">C++</span><span class="sxs-lookup"><span data-stu-id="56af5-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 
 

<span data-ttu-id="56af5-111">Toohello bem-vindo ao tutorial de C++ para Olá API DocumentDB do Azure Cosmos DB aprovados SDK para C++!</span><span class="sxs-lookup"><span data-stu-id="56af5-111">Welcome toohello C++ tutorial for hello Azure Cosmos DB DocumentDB API endorsed SDK for C++!</span></span> <span data-ttu-id="56af5-112">Após seguir este tutorial, você terá um aplicativo de console que cria e consulta recursos do Azure Cosmos DB, incluindo um banco de dados em C++.</span><span class="sxs-lookup"><span data-stu-id="56af5-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources, including a C++ database.</span></span>

<span data-ttu-id="56af5-113">Abordaremos:</span><span class="sxs-lookup"><span data-stu-id="56af5-113">We'll cover:</span></span>

* <span data-ttu-id="56af5-114">Criar e conectar-se a conta de banco de dados do Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="56af5-114">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="56af5-115">Configurando o aplicativo</span><span class="sxs-lookup"><span data-stu-id="56af5-115">Setting up your application</span></span>
* <span data-ttu-id="56af5-116">Criar um banco de dados do Azure Cosmos DB em C++</span><span class="sxs-lookup"><span data-stu-id="56af5-116">Creating a C++ Azure Cosmos DB database</span></span>
* <span data-ttu-id="56af5-117">Criar uma coleção</span><span class="sxs-lookup"><span data-stu-id="56af5-117">Creating a collection</span></span>
* <span data-ttu-id="56af5-118">Criando documentos JSON</span><span class="sxs-lookup"><span data-stu-id="56af5-118">Creating JSON documents</span></span>
* <span data-ttu-id="56af5-119">Consultando Olá coleção</span><span class="sxs-lookup"><span data-stu-id="56af5-119">Querying hello collection</span></span>
* <span data-ttu-id="56af5-120">Substituição de um documento</span><span class="sxs-lookup"><span data-stu-id="56af5-120">Replacing a document</span></span>
* <span data-ttu-id="56af5-121">Exclusão de um documento</span><span class="sxs-lookup"><span data-stu-id="56af5-121">Deleting a document</span></span>
* <span data-ttu-id="56af5-122">Excluir banco de dados de banco de dados do C++ Azure Cosmos Olá</span><span class="sxs-lookup"><span data-stu-id="56af5-122">Deleting hello C++ Azure Cosmos DB database</span></span>

<span data-ttu-id="56af5-123">Você não tem tempo?</span><span class="sxs-lookup"><span data-stu-id="56af5-123">Don't have time?</span></span> <span data-ttu-id="56af5-124">Não se preocupe!</span><span class="sxs-lookup"><span data-stu-id="56af5-124">Don't worry!</span></span> <span data-ttu-id="56af5-125">solução completa de saudação está disponível em [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span><span class="sxs-lookup"><span data-stu-id="56af5-125">hello complete solution is available on [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span></span> <span data-ttu-id="56af5-126">Consulte [obter a solução completa de saudação](#GetSolution) para instruções rápidas.</span><span class="sxs-lookup"><span data-stu-id="56af5-126">See [Get hello complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="56af5-127">Depois que você concluiu o tutorial de C++ hello,. use Olá votação botões na parte inferior de saudação do toogive página nos comentários.</span><span class="sxs-lookup"><span data-stu-id="56af5-127">After you've completed hello C++ tutorial, please use hello voting buttons at hello bottom of this page toogive us feedback.</span></span> 

<span data-ttu-id="56af5-128">Se você deseja toocontact você diretamente, sinta-se livre tooinclude endereço do seu email em seus comentários ou [chegar aqui toous](https://www.research.net/r/8BKRJ3Z).</span><span class="sxs-lookup"><span data-stu-id="56af5-128">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments or [reach out toous here](https://www.research.net/r/8BKRJ3Z).</span></span> 

<span data-ttu-id="56af5-129">Agora vamos começar!</span><span class="sxs-lookup"><span data-stu-id="56af5-129">Now let's get started!</span></span>

## <a name="prerequisites-for-hello-c-tutorial"></a><span data-ttu-id="56af5-130">Pré-requisitos para o tutorial Olá C++</span><span class="sxs-lookup"><span data-stu-id="56af5-130">Prerequisites for hello C++ tutorial</span></span>
<span data-ttu-id="56af5-131">Verifique se que você tem o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="56af5-131">Please make sure you have hello following:</span></span>

* <span data-ttu-id="56af5-132">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="56af5-132">An active Azure account.</span></span> <span data-ttu-id="56af5-133">Se não tiver uma, você poderá se inscrever em uma [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="56af5-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="56af5-134">[O Visual Studio](https://www.visualstudio.com/downloads/), com componentes de linguagem Olá C++ instalados.</span><span class="sxs-lookup"><span data-stu-id="56af5-134">[Visual Studio](https://www.visualstudio.com/downloads/), with hello C++ language components installed.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="56af5-135">Etapa 1: Criar uma conta de banco de dados do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="56af5-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="56af5-136">Vamos criar uma conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="56af5-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="56af5-137">Se você já tiver uma conta que você deseja toouse, poderá pular muito[configurar seu aplicativo C++](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="56af5-137">If you already have an account you want toouse, you can skip ahead too[Setup your C++ application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="56af5-138"><a id="SetupC++"></a>Etapa 2: configurar o aplicativo C++</span><span class="sxs-lookup"><span data-stu-id="56af5-138"><a id="SetupC++"></a>Step 2: Set up your C++ application</span></span>
1. <span data-ttu-id="56af5-139">Abra o Visual Studio e, em seguida, em Olá **arquivo** menu, clique em **novo**e, em seguida, clique em **projeto**.</span><span class="sxs-lookup"><span data-stu-id="56af5-139">Open Visual Studio, and then on hello **File** menu, click **New**, and then click **Project**.</span></span> 
2. <span data-ttu-id="56af5-140">Em Olá **novo projeto** janela no hello **instalado** painel, expanda **Visual C++**, clique em **Win32**e, em seguida, clique em  **Aplicativo do Console Win32**.</span><span class="sxs-lookup"><span data-stu-id="56af5-140">In hello **New Project** window, in hello **Installed** pane, expand **Visual C++**, click **Win32**, and then click **Win32 Console Application**.</span></span> <span data-ttu-id="56af5-141">Nome hello hellodocumentdb de projeto e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="56af5-141">Name hello project hellodocumentdb and then click **OK**.</span></span> 
   
    ![Captura de tela do Assistente do novo projeto Olá](media/documentdb-cpp-get-started/hello.png)
3. <span data-ttu-id="56af5-143">Quando iniciado Olá Win32 Application Wizard, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="56af5-143">When hello Win32 Application Wizard starts, click **Finish**.</span></span>
4. <span data-ttu-id="56af5-144">Quando Olá projeto foi criado, abra o Gerenciador de pacotes do NuGet Olá clicando Olá **hellodocumentdb** project no **Solution Explorer** e clicando em **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="56af5-144">Once hello project has been created, open hello NuGet package manager by right-clicking hello **hellodocumentdb** project in **Solution Explorer** and clicking **Manage NuGet Packages**.</span></span> 
   
    ![Captura de tela mostrando a gerenciar pacotes do NuGet no menu do projeto Olá](media/documentdb-cpp-get-started/nuget.png)
5. <span data-ttu-id="56af5-146">Em Olá **NuGet: hellodocumentdb** , clique em **procurar**e, em seguida, procure *documentdbcpp*.</span><span class="sxs-lookup"><span data-stu-id="56af5-146">In hello **NuGet: hellodocumentdb** tab, click **Browse**, and then search for *documentdbcpp*.</span></span> <span data-ttu-id="56af5-147">Nos resultados de saudação, selecione DocumentDbCPP, conforme mostrado no hello captura de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="56af5-147">In hello results, select DocumentDbCPP, as shown in hello following screenshot.</span></span> <span data-ttu-id="56af5-148">Este pacote instala referências tooC c++ REST SDK, que é uma dependência para Olá DocumentDbCPP.</span><span class="sxs-lookup"><span data-stu-id="56af5-148">This package installs references tooC++ REST SDK, which is a dependency for hello DocumentDbCPP.</span></span>  
   
    ![Pacote de DocumentDbCpp Olá de captura de tela mostrando realçado](media/documentdb-cpp-get-started/cpp.png)
   
    <span data-ttu-id="56af5-150">Depois que os pacotes de saudação adicionou tooyour projeto, estamos todos os toostart conjunto gravar qualquer código.</span><span class="sxs-lookup"><span data-stu-id="56af5-150">Once hello packages have been added tooyour project, we are all set toostart writing some code.</span></span>   

## <span data-ttu-id="56af5-151"><a id="Config"></a>Etapa 3: copiar detalhes da conexão do Portal do Azure para o banco de dados do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="56af5-151"><a id="Config"></a>Step 3: Copy connection details from Azure portal for your Azure Cosmos DB database</span></span>
<span data-ttu-id="56af5-152">Ativar [portal do Azure](https://portal.azure.com) e percorrer a conta de banco de dados do banco de dados do Azure Cosmos toohello criado por você.</span><span class="sxs-lookup"><span data-stu-id="56af5-152">Bring up [Azure portal](https://portal.azure.com) and traverse toohello Azure Cosmos DB database account you created.</span></span> <span data-ttu-id="56af5-153">Precisaremos Olá URI e a chave primária de saudação do portal do Azure no hello de próxima etapa tooestablish uma conexão de nosso trecho de código C++.</span><span class="sxs-lookup"><span data-stu-id="56af5-153">We will need hello URI and hello primary key from Azure portal in hello next step tooestablish a connection from our C++ code snippet.</span></span> 

![Azure Cosmos URI de banco de dados e as chaves no hello portal do Azure](media/documentdb-cpp-get-started/nosql-tutorial-keys.png)

## <span data-ttu-id="56af5-155"><a id="Connect"></a>Etapa 4: Conectar-se a conta de banco de dados do Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="56af5-155"><a id="Connect"></a>Step 4: Connect tooan Azure Cosmos DB account</span></span>
1. <span data-ttu-id="56af5-156">Olá cabeçalhos e namespaces tooyour código-fonte, a seguir depois de adicionar `#include "stdafx.h"`.</span><span class="sxs-lookup"><span data-stu-id="56af5-156">Add hello following headers and namespaces tooyour source code, after `#include "stdafx.h"`.</span></span>
   
        #include <cpprest/json.h>
        #include <documentdbcpp\DocumentClient.h>
        #include <documentdbcpp\exceptions.h>
        #include <documentdbcpp\TriggerOperation.h>
        #include <documentdbcpp\TriggerType.h>
        using namespace documentdb;
        using namespace std;
        using namespace web::json;
2. <span data-ttu-id="56af5-157">Em seguida, adicione a seguir Olá código função main tooyour e substitua toomatch de chave primária e a configuração de conta de saudação suas configurações de banco de dados do Azure Cosmos da etapa 3.</span><span class="sxs-lookup"><span data-stu-id="56af5-157">Next add hello following code tooyour main function and replace hello account configuration and primary key toomatch your Azure Cosmos DB settings from step 3.</span></span> 
   
        DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
        DocumentClient client (conf);
   
    <span data-ttu-id="56af5-158">Agora que você possui o cliente de documentos do hello código tooinitialize Olá, vamos dar uma olhada em trabalhar com recursos de banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="56af5-158">Now that you have hello code tooinitialize hello documentdb client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <span data-ttu-id="56af5-159"><a id="CreateDBColl"></a>Etapa 5: criar um banco de dados em C++ e uma coleção</span><span class="sxs-lookup"><span data-stu-id="56af5-159"><a id="CreateDBColl"></a>Step 5: Create a C++ database and collection</span></span>
<span data-ttu-id="56af5-160">Antes desta etapa é executada, vamos falar sobre como documentos, coleção e um banco de dados interagem para aqueles que são tooAzure novo banco de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="56af5-160">Before we perform this step, let's go over how a database, collection and documents interact for those of you who are new tooAzure Cosmos DB.</span></span> <span data-ttu-id="56af5-161">Um [banco de dados](documentdb-resources.md#databases) é um contêiner lógico de armazenamento de documentos particionado em coleções.</span><span class="sxs-lookup"><span data-stu-id="56af5-161">A [database](documentdb-resources.md#databases) is a logical container of document storage portioned across collections.</span></span> <span data-ttu-id="56af5-162">Um [coleção](documentdb-resources.md#collections) é um contêiner de documentos JSON e Olá associados a lógica do aplicativo JavaScript.</span><span class="sxs-lookup"><span data-stu-id="56af5-162">A [collection](documentdb-resources.md#collections) is a container of JSON documents and hello associated JavaScript application logic.</span></span> <span data-ttu-id="56af5-163">Você pode aprender mais sobre o modelo de recurso hierárquica hello Azure Cosmos DB e o conceitos em [conceitos e modelo de recurso hierárquica do banco de dados do Azure Cosmos](documentdb-resources.md).</span><span class="sxs-lookup"><span data-stu-id="56af5-163">You can learn more about hello Azure Cosmos DB hierarchical resource model and concepts in [Azure Cosmos DB hierarchical resource model and concepts](documentdb-resources.md).</span></span>

<span data-ttu-id="56af5-164">toocreate um banco de dados e uma coleção correspondente adicionam Olá seguindo código toohello final de sua função principal.</span><span class="sxs-lookup"><span data-stu-id="56af5-164">toocreate a database and a corresponding collection add hello following code toohello end of your main function.</span></span> <span data-ttu-id="56af5-165">Isso cria um banco de dados chamado 'FamilyRegistry' e uma coleção chamada 'FamilyCollection' usando a configuração de cliente Olá declarado na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="56af5-165">This creates a database called 'FamilyRegistry’ and a collection called ‘FamilyCollection’ using hello client configuration you declared in hello previous step.</span></span>

    try {
      shared_ptr<Database> db = client.CreateDatabase(L"FamilyRegistry");
      shared_ptr<Collection> coll = db->CreateCollection(L"FamilyCollection");
    } catch (DocumentDBRuntimeException ex) {
      wcout << ex.message();
    }


## <span data-ttu-id="56af5-166"><a id="CreateDoc"></a>Etapa 6: Criar um documento</span><span class="sxs-lookup"><span data-stu-id="56af5-166"><a id="CreateDoc"></a>Step 6: Create a document</span></span>
<span data-ttu-id="56af5-167">Os [documentos](documentdb-resources.md#documents) são conteúdo JSON (arbitrário) definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="56af5-167">[Documents](documentdb-resources.md#documents) are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="56af5-168">Agora você pode inserir um documento no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="56af5-168">You can now insert a document into Azure Cosmos DB.</span></span> <span data-ttu-id="56af5-169">Você pode criar um documento copiando Olá código a seguir no final de saudação da função principal hello.</span><span class="sxs-lookup"><span data-stu-id="56af5-169">You can create a document by copying hello following code into hello end of hello main function.</span></span> 

    try {
      value document_family;
      document_family[L"id"] = value::string(L"AndersenFamily");
      document_family[L"FirstName"] = value::string(L"Thomas");
      document_family[L"LastName"] = value::string(L"Andersen");
      shared_ptr<Document> doc = coll->CreateDocumentAsync(document_family).get();

      document_family[L"id"] = value::string(L"WakefieldFamily");
      document_family[L"FirstName"] = value::string(L"Lucy");
      document_family[L"LastName"] = value::string(L"Wakefield");
      doc = coll->CreateDocumentAsync(document_family).get();
    } catch (ResourceAlreadyExistsException ex) {
      wcout << ex.message();
    }

<span data-ttu-id="56af5-170">toosummarize, esse código cria um banco de dados do banco de dados do Azure Cosmos, coleção e documentos, que podem ser consultados no Gerenciador de documentos no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="56af5-170">toosummarize, this code creates an Azure Cosmos DB database, collection, and documents, which you can query in Document Explorer in Azure portal.</span></span> 

![Tutorial de C++ - diagrama que ilustra uma relação hierárquica entre conta hello, banco de dados de saudação, coleção hello e documentos Olá Olá](media/documentdb-cpp-get-started/docs.png)

## <span data-ttu-id="56af5-172"><a id="QueryDB"></a>Etapa 7: Consultar recursos do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="56af5-172"><a id="QueryDB"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="56af5-173">O Azure Cosmos DB tem suporte para [consultas](documentdb-sql-query.md) avançadas de documentos JSON armazenados em cada coleção.</span><span class="sxs-lookup"><span data-stu-id="56af5-173">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="56af5-174">Hello, código de exemplo seguinte mostra uma consulta feita usando a sintaxe SQL que pode ser executado em documentos de saudação criada na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="56af5-174">hello following sample code shows a query made using SQL syntax that you can run against hello documents we created in hello previous step.</span></span>

<span data-ttu-id="56af5-175">função Hello assume como argumentos Olá identificador exclusivo ou id de recurso do banco de dados de saudação e coleção Olá junto com o cliente do documento hello.</span><span class="sxs-lookup"><span data-stu-id="56af5-175">hello function takes in as arguments hello unique identifier or resource id for hello database and hello collection along with hello document client.</span></span> <span data-ttu-id="56af5-176">Adicione esse código antes da função principal.</span><span class="sxs-lookup"><span data-stu-id="56af5-176">Add this code before main function.</span></span>

    void executesimplequery(const DocumentClient &client,
                            const wstring dbresourceid,
                            const wstring collresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        wstring coll_name = coll->id();
        shared_ptr<DocumentIterator> iter =
            coll->QueryDocumentsAsync(wstring(L"SELECT * FROM " + coll_name)).get();
        wcout << "\n\nQuerying collection:";
        while (iter->HasMore()) {
          shared_ptr<Document> doc = iter->Next();
          wstring doc_name = doc->id();
          wcout << "\n\t" << doc_name << "\n";
          wcout << "\t"
                << "[{\"FirstName\":"
                << doc->payload().at(U("FirstName")).as_string()
                << ",\"LastName\":" << doc->payload().at(U("LastName")).as_string()
                << "}]";
        }
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="56af5-177"><a id="Replace"></a>Etapa 8: substituir um documento</span><span class="sxs-lookup"><span data-stu-id="56af5-177"><a id="Replace"></a>Step 8: Replace a document</span></span>
<span data-ttu-id="56af5-178">Banco de dados do Azure Cosmos dá suporte a documentos JSON substituindo, conforme demonstrado no hello código a seguir.</span><span class="sxs-lookup"><span data-stu-id="56af5-178">Azure Cosmos DB supports replacing JSON documents, as demonstrated in hello following code.</span></span> <span data-ttu-id="56af5-179">Adicione esse código após a função de executesimplequery hello.</span><span class="sxs-lookup"><span data-stu-id="56af5-179">Add this code after hello executesimplequery function.</span></span>

    void replacedocument(const DocumentClient &client, const wstring dbresourceid,
                         const wstring collresourceid,
                         const wstring docresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        value newdoc;
        newdoc[L"id"] = value::string(L"WakefieldFamily");
        newdoc[L"FirstName"] = value::string(L"Lucy");
        newdoc[L"LastName"] = value::string(L"Smith Wakefield");
        coll->ReplaceDocument(docresourceid, newdoc);
      } catch (DocumentDBRuntimeException ex) {
        throw;
      }
    }

## <span data-ttu-id="56af5-180"><a id="Delete"></a>Etapa 9: excluir um documento</span><span class="sxs-lookup"><span data-stu-id="56af5-180"><a id="Delete"></a>Step 9: Delete a document</span></span>
<span data-ttu-id="56af5-181">Azure Cosmos DB dá suporte à exclusão de documentos JSON, você pode fazer isso por copiar e colar Olá código a seguir após a função de replacedocument hello.</span><span class="sxs-lookup"><span data-stu-id="56af5-181">Azure Cosmos DB supports deleting JSON documents, you can do so by copy and pasting hello following code after hello replacedocument function.</span></span> 

    void deletedocument(const DocumentClient &client, const wstring dbresourceid,
                        const wstring collresourceid, const wstring docresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        coll->DeleteDocumentAsync(docresourceid).get();
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="56af5-182"><a id="DeleteDB"></a>Etapa 10: excluir um banco de dados</span><span class="sxs-lookup"><span data-stu-id="56af5-182"><a id="DeleteDB"></a>Step 10: Delete a database</span></span>
<span data-ttu-id="56af5-183">Banco de dados excluindo Olá criado remove o banco de dados de saudação e todos os recursos filho (coleções, documentos, etc.).</span><span class="sxs-lookup"><span data-stu-id="56af5-183">Deleting hello created database removes hello database and all child resources (collections, documents, etc.).</span></span>

<span data-ttu-id="56af5-184">Copie e cole hello (Limpeza de função) do trecho de código a seguir após o banco de dados do hello deletedocument função tooremove hello e todos os recursos filho de saudação.</span><span class="sxs-lookup"><span data-stu-id="56af5-184">Copy and paste hello following code snippet (function cleanup) after hello deletedocument function tooremove hello database and all hello child resources.</span></span>

    void deletedb(const DocumentClient &client, const wstring dbresourceid) {
      try {
        client.DeleteDatabase(dbresourceid);
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="56af5-185"><a id="Run"></a>Etapa 11: executar o aplicativo C++ em conjunto!</span><span class="sxs-lookup"><span data-stu-id="56af5-185"><a id="Run"></a>Step 11: Run your C++ application all together!</span></span>
<span data-ttu-id="56af5-186">Nós adicionou toocreate de código, consultar, modificar e excluir recursos de banco de dados do Azure Cosmos diferentes.</span><span class="sxs-lookup"><span data-stu-id="56af5-186">We have now added code toocreate, query, modify, and delete different Azure Cosmos DB resources.</span></span>  <span data-ttu-id="56af5-187">Vamos agora conecte isso adicionando chamadas toothese diferentes funções de nossa função principal do hellodocumentdb.cpp juntamente com algumas mensagens de diagnósticas.</span><span class="sxs-lookup"><span data-stu-id="56af5-187">Let us now wire this up by adding calls toothese different functions from our main function in hellodocumentdb.cpp along with some diagnostic messages.</span></span>

<span data-ttu-id="56af5-188">Você pode fazer isso, substituindo a função principal saudação do seu aplicativo com hello código a seguir.</span><span class="sxs-lookup"><span data-stu-id="56af5-188">You can do so by replacing hello main function of your application with hello following code.</span></span> <span data-ttu-id="56af5-189">Este gravações Olá account_configuration_uri e primary_key que você copiou no código Olá na etapa 3, então salvar que valores de linha ou cópia Olá no novamente do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="56af5-189">This writes over hello account_configuration_uri and primary_key you copied into hello code in Step 3, so save that line or copy hello values in again from hello portal.</span></span> 

    int main() {
        try {
            // Start by defining your account's configuration
            DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
            // Create your client
            DocumentClient client(conf);
            // Create a new database
            try {
                shared_ptr<Database> db = client.CreateDatabase(L"FamilyDB");
                wcout << "\nCreating database:\n" << db->id();
                // Create a collection inside database
                shared_ptr<Collection> coll = db->CreateCollection(L"FamilyColl");
                wcout << "\n\nCreating collection:\n" << coll->id();
                value document_family;
                document_family[L"id"] = value::string(L"AndersenFamily");
                document_family[L"FirstName"] = value::string(L"Thomas");
                document_family[L"LastName"] = value::string(L"Andersen");
                shared_ptr<Document> doc =
                    coll->CreateDocumentAsync(document_family).get();
                wcout << "\n\nCreating document:\n" << doc->id();
                document_family[L"id"] = value::string(L"WakefieldFamily");
                document_family[L"FirstName"] = value::string(L"Lucy");
                document_family[L"LastName"] = value::string(L"Wakefield");
                doc = coll->CreateDocumentAsync(document_family).get();
                wcout << "\n\nCreating document:\n" << doc->id();
                executesimplequery(client, db->resource_id(), coll->resource_id());
                replacedocument(client, db->resource_id(), coll->resource_id(),
                    doc->resource_id());
                wcout << "\n\nReplaced document:\n" << doc->id();
                executesimplequery(client, db->resource_id(), coll->resource_id());
                deletedocument(client, db->resource_id(), coll->resource_id(),
                    doc->resource_id());
                wcout << "\n\nDeleted document:\n" << doc->id();
                deletedb(client, db->resource_id());
                wcout << "\n\nDeleted db:\n" << db->id();
                cin.get();
            }
            catch (ResourceAlreadyExistsException ex) {
                wcout << ex.message();
            }
        }
        catch (DocumentDBRuntimeException ex) {
            wcout << ex.message();
        }
        cin.get();
    }

<span data-ttu-id="56af5-190">Agora deve ser capaz de toobuild e executar seu código no Visual Studio pressionando F5 ou como alternativa Olá executável na janela de terminal Olá Localizando aplicativo hello e em execução.</span><span class="sxs-lookup"><span data-stu-id="56af5-190">You should now be able toobuild and run your code in Visual Studio by pressing F5 or alternatively in hello terminal window by locating hello application and running hello executable.</span></span> 

<span data-ttu-id="56af5-191">Você deve ver a saída de saudação do aplicativo iniciado get.</span><span class="sxs-lookup"><span data-stu-id="56af5-191">You should see hello output of your get started app.</span></span> <span data-ttu-id="56af5-192">saída de Hello deve corresponder a saudação captura de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="56af5-192">hello output should match hello following screenshot.</span></span>

![Saída do aplicativo C++ do Azure Cosmos DB](media/documentdb-cpp-get-started/console.png)

<span data-ttu-id="56af5-194">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="56af5-194">Congratulations!</span></span> <span data-ttu-id="56af5-195">Você concluiu o tutorial de C++ hello e ter seu primeiro aplicativo de console de banco de dados do Azure Cosmos!</span><span class="sxs-lookup"><span data-stu-id="56af5-195">You've completed hello C++ tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="56af5-196"><a id="GetSolution"></a>Obter a solução completa de tutorial de C++ Olá</span><span class="sxs-lookup"><span data-stu-id="56af5-196"><a id="GetSolution"></a>Get hello complete C++ tutorial solution</span></span>
<span data-ttu-id="56af5-197">toobuild Olá GetStarted solução que contém todos os exemplos de saudação neste artigo, você precisa seguir hello:</span><span class="sxs-lookup"><span data-stu-id="56af5-197">toobuild hello GetStarted solution that contains all hello samples in this article, you need hello following:</span></span>

* <span data-ttu-id="56af5-198">[Conta do Azure Cosmos DB][create-account].</span><span class="sxs-lookup"><span data-stu-id="56af5-198">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="56af5-199">Olá [GetStarted](https://github.com/stalker314314/DocumentDBCpp) solução disponível no GitHub.</span><span class="sxs-lookup"><span data-stu-id="56af5-199">hello [GetStarted](https://github.com/stalker314314/DocumentDBCpp) solution available on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56af5-200">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="56af5-200">Next steps</span></span>
* <span data-ttu-id="56af5-201">Saiba como muito[monitorar uma conta de banco de dados do Azure Cosmos](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="56af5-201">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="56af5-202">Executar consultas em nosso conjunto de dados de exemplo hello [parque de consulta](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="56af5-202">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="56af5-203">Saiba mais sobre o modelo de programação de Olá Olá seção desenvolver de saudação [página de documentação do banco de dados do Azure Cosmos](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="56af5-203">Learn more about hello programming model in hello Develop section of hello [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account


