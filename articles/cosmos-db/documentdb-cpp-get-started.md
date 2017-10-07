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
# <a name="azure-cosmos-db-c-console-application-tutorial-for-hello-documentdb-api"></a>Cosmos do Azure DB: Tutorial do aplicativo de console C++ para Olá API DocumentDB
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js para MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 
 

Toohello bem-vindo ao tutorial de C++ para Olá API DocumentDB do Azure Cosmos DB aprovados SDK para C++! Após seguir este tutorial, você terá um aplicativo de console que cria e consulta recursos do Azure Cosmos DB, incluindo um banco de dados em C++.

Abordaremos:

* Criar e conectar-se a conta de banco de dados do Azure Cosmos tooan
* Configurando o aplicativo
* Criar um banco de dados do Azure Cosmos DB em C++
* Criar uma coleção
* Criando documentos JSON
* Consultando Olá coleção
* Substituição de um documento
* Exclusão de um documento
* Excluir banco de dados de banco de dados do C++ Azure Cosmos Olá

Você não tem tempo? Não se preocupe! solução completa de saudação está disponível em [GitHub](https://github.com/stalker314314/DocumentDBCpp). Consulte [obter a solução completa de saudação](#GetSolution) para instruções rápidas.

Depois que você concluiu o tutorial de C++ hello,. use Olá votação botões na parte inferior de saudação do toogive página nos comentários. 

Se você deseja toocontact você diretamente, sinta-se livre tooinclude endereço do seu email em seus comentários ou [chegar aqui toous](https://www.research.net/r/8BKRJ3Z). 

Agora vamos começar!

## <a name="prerequisites-for-hello-c-tutorial"></a>Pré-requisitos para o tutorial Olá C++
Verifique se que você tem o seguinte hello:

* Uma conta ativa do Azure. Se não tiver uma, você poderá se inscrever em uma [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* [O Visual Studio](https://www.visualstudio.com/downloads/), com componentes de linguagem Olá C++ instalados.

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Etapa 1: Criar uma conta de banco de dados do Azure Cosmos DB
Vamos criar uma conta do Azure Cosmos DB. Se você já tiver uma conta que você deseja toouse, poderá pular muito[configurar seu aplicativo C++](#SetupNode).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupC++"></a>Etapa 2: configurar o aplicativo C++
1. Abra o Visual Studio e, em seguida, em Olá **arquivo** menu, clique em **novo**e, em seguida, clique em **projeto**. 
2. Em Olá **novo projeto** janela no hello **instalado** painel, expanda **Visual C++**, clique em **Win32**e, em seguida, clique em  **Aplicativo do Console Win32**. Nome hello hellodocumentdb de projeto e, em seguida, clique em **Okey**. 
   
    ![Captura de tela do Assistente do novo projeto Olá](media/documentdb-cpp-get-started/hello.png)
3. Quando iniciado Olá Win32 Application Wizard, clique em **concluir**.
4. Quando Olá projeto foi criado, abra o Gerenciador de pacotes do NuGet Olá clicando Olá **hellodocumentdb** project no **Solution Explorer** e clicando em **gerenciar pacotes NuGet**. 
   
    ![Captura de tela mostrando a gerenciar pacotes do NuGet no menu do projeto Olá](media/documentdb-cpp-get-started/nuget.png)
5. Em Olá **NuGet: hellodocumentdb** , clique em **procurar**e, em seguida, procure *documentdbcpp*. Nos resultados de saudação, selecione DocumentDbCPP, conforme mostrado no hello captura de tela a seguir. Este pacote instala referências tooC c++ REST SDK, que é uma dependência para Olá DocumentDbCPP.  
   
    ![Pacote de DocumentDbCpp Olá de captura de tela mostrando realçado](media/documentdb-cpp-get-started/cpp.png)
   
    Depois que os pacotes de saudação adicionou tooyour projeto, estamos todos os toostart conjunto gravar qualquer código.   

## <a id="Config"></a>Etapa 3: copiar detalhes da conexão do Portal do Azure para o banco de dados do Azure Cosmos DB
Ativar [portal do Azure](https://portal.azure.com) e percorrer a conta de banco de dados do banco de dados do Azure Cosmos toohello criado por você. Precisaremos Olá URI e a chave primária de saudação do portal do Azure no hello de próxima etapa tooestablish uma conexão de nosso trecho de código C++. 

![Azure Cosmos URI de banco de dados e as chaves no hello portal do Azure](media/documentdb-cpp-get-started/nosql-tutorial-keys.png)

## <a id="Connect"></a>Etapa 4: Conectar-se a conta de banco de dados do Azure Cosmos tooan
1. Olá cabeçalhos e namespaces tooyour código-fonte, a seguir depois de adicionar `#include "stdafx.h"`.
   
        #include <cpprest/json.h>
        #include <documentdbcpp\DocumentClient.h>
        #include <documentdbcpp\exceptions.h>
        #include <documentdbcpp\TriggerOperation.h>
        #include <documentdbcpp\TriggerType.h>
        using namespace documentdb;
        using namespace std;
        using namespace web::json;
2. Em seguida, adicione a seguir Olá código função main tooyour e substitua toomatch de chave primária e a configuração de conta de saudação suas configurações de banco de dados do Azure Cosmos da etapa 3. 
   
        DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
        DocumentClient client (conf);
   
    Agora que você possui o cliente de documentos do hello código tooinitialize Olá, vamos dar uma olhada em trabalhar com recursos de banco de dados do Azure Cosmos.

## <a id="CreateDBColl"></a>Etapa 5: criar um banco de dados em C++ e uma coleção
Antes desta etapa é executada, vamos falar sobre como documentos, coleção e um banco de dados interagem para aqueles que são tooAzure novo banco de dados do Cosmos. Um [banco de dados](documentdb-resources.md#databases) é um contêiner lógico de armazenamento de documentos particionado em coleções. Um [coleção](documentdb-resources.md#collections) é um contêiner de documentos JSON e Olá associados a lógica do aplicativo JavaScript. Você pode aprender mais sobre o modelo de recurso hierárquica hello Azure Cosmos DB e o conceitos em [conceitos e modelo de recurso hierárquica do banco de dados do Azure Cosmos](documentdb-resources.md).

toocreate um banco de dados e uma coleção correspondente adicionam Olá seguindo código toohello final de sua função principal. Isso cria um banco de dados chamado 'FamilyRegistry' e uma coleção chamada 'FamilyCollection' usando a configuração de cliente Olá declarado na etapa anterior hello.

    try {
      shared_ptr<Database> db = client.CreateDatabase(L"FamilyRegistry");
      shared_ptr<Collection> coll = db->CreateCollection(L"FamilyCollection");
    } catch (DocumentDBRuntimeException ex) {
      wcout << ex.message();
    }


## <a id="CreateDoc"></a>Etapa 6: Criar um documento
Os [documentos](documentdb-resources.md#documents) são conteúdo JSON (arbitrário) definido pelo usuário. Agora você pode inserir um documento no Azure Cosmos DB. Você pode criar um documento copiando Olá código a seguir no final de saudação da função principal hello. 

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

toosummarize, esse código cria um banco de dados do banco de dados do Azure Cosmos, coleção e documentos, que podem ser consultados no Gerenciador de documentos no portal do Azure. 

![Tutorial de C++ - diagrama que ilustra uma relação hierárquica entre conta hello, banco de dados de saudação, coleção hello e documentos Olá Olá](media/documentdb-cpp-get-started/docs.png)

## <a id="QueryDB"></a>Etapa 7: Consultar recursos do Azure Cosmos DB
O Azure Cosmos DB tem suporte para [consultas](documentdb-sql-query.md) avançadas de documentos JSON armazenados em cada coleção. Hello, código de exemplo seguinte mostra uma consulta feita usando a sintaxe SQL que pode ser executado em documentos de saudação criada na etapa anterior hello.

função Hello assume como argumentos Olá identificador exclusivo ou id de recurso do banco de dados de saudação e coleção Olá junto com o cliente do documento hello. Adicione esse código antes da função principal.

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

## <a id="Replace"></a>Etapa 8: substituir um documento
Banco de dados do Azure Cosmos dá suporte a documentos JSON substituindo, conforme demonstrado no hello código a seguir. Adicione esse código após a função de executesimplequery hello.

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

## <a id="Delete"></a>Etapa 9: excluir um documento
Azure Cosmos DB dá suporte à exclusão de documentos JSON, você pode fazer isso por copiar e colar Olá código a seguir após a função de replacedocument hello. 

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

## <a id="DeleteDB"></a>Etapa 10: excluir um banco de dados
Banco de dados excluindo Olá criado remove o banco de dados de saudação e todos os recursos filho (coleções, documentos, etc.).

Copie e cole hello (Limpeza de função) do trecho de código a seguir após o banco de dados do hello deletedocument função tooremove hello e todos os recursos filho de saudação.

    void deletedb(const DocumentClient &client, const wstring dbresourceid) {
      try {
        client.DeleteDatabase(dbresourceid);
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <a id="Run"></a>Etapa 11: executar o aplicativo C++ em conjunto!
Nós adicionou toocreate de código, consultar, modificar e excluir recursos de banco de dados do Azure Cosmos diferentes.  Vamos agora conecte isso adicionando chamadas toothese diferentes funções de nossa função principal do hellodocumentdb.cpp juntamente com algumas mensagens de diagnósticas.

Você pode fazer isso, substituindo a função principal saudação do seu aplicativo com hello código a seguir. Este gravações Olá account_configuration_uri e primary_key que você copiou no código Olá na etapa 3, então salvar que valores de linha ou cópia Olá no novamente do portal de saudação. 

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

Agora deve ser capaz de toobuild e executar seu código no Visual Studio pressionando F5 ou como alternativa Olá executável na janela de terminal Olá Localizando aplicativo hello e em execução. 

Você deve ver a saída de saudação do aplicativo iniciado get. saída de Hello deve corresponder a saudação captura de tela a seguir.

![Saída do aplicativo C++ do Azure Cosmos DB](media/documentdb-cpp-get-started/console.png)

Parabéns! Você concluiu o tutorial de C++ hello e ter seu primeiro aplicativo de console de banco de dados do Azure Cosmos!

## <a id="GetSolution"></a>Obter a solução completa de tutorial de C++ Olá
toobuild Olá GetStarted solução que contém todos os exemplos de saudação neste artigo, você precisa seguir hello:

* [Conta do Azure Cosmos DB][create-account].
* Olá [GetStarted](https://github.com/stalker314314/DocumentDBCpp) solução disponível no GitHub.

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[monitorar uma conta de banco de dados do Azure Cosmos](monitor-accounts.md).
* Executar consultas em nosso conjunto de dados de exemplo hello [parque de consulta](https://www.documentdb.com/sql/demo).
* Saiba mais sobre o modelo de programação de Olá Olá seção desenvolver de saudação [página de documentação do banco de dados do Azure Cosmos](https://azure.microsoft.com/documentation/services/documentdb/).

[create-account]: create-documentdb-dotnet.md#create-account


