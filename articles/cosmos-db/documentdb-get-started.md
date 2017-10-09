---
title: "Azure Cosmos DB: tutorial de introdução da API do DocumentDB | Microsoft Docs"
description: "Um tutorial que cria um banco de dados online e um aplicativo de console c# usando Olá API DocumentDB."
keywords: tutorial do nosql, banco de dados online, aplicativo de console c#
services: cosmos-db
documentationcenter: .net
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: bf08e031-718a-4a2a-89d6-91e12ff8797d
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2017
ms.author: anhoh
ms.openlocfilehash: 65a181f715a670987492ad7815ef2ec94498e84d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-api-getting-started-tutorial"></a>Azure Cosmos DB: tutorial de introdução da API do DocumentDB
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js para MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Bem-vindo toohello API DocumentDB do Azure Cosmos DB tutorial de Introdução! Após seguir este tutorial, você terá um aplicativo de console que cria e consulta recursos do Azure Cosmos DB.

Abordaremos:

* Criar e conectar-se a conta de banco de dados do Azure Cosmos tooan
* Configurar a sua Solução do Visual Studio
* Criando um banco de dados online
* Criar uma coleção
* Criando documentos JSON
* Consultando Olá coleção
* Substituição de um documento
* Exclusão de um documento
* Excluir banco de dados de saudação

Você não tem tempo? Não se preocupe! solução completa de saudação está disponível em [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started). Saltar toohello [obter seção de solução tutorial NoSQL completa Olá](#GetSolution) para instruções rápidas.

Posteriormente,. use Olá votação botões na parte superior da saudação ou inferior de toogive esta página nos comentários. Se você deseja toocontact você diretamente, sinta-se livre tooinclude endereço do seu email em seus comentários.

Agora vamos começar!

## <a name="prerequisites"></a>Pré-requisitos
Verifique se que você tem o seguinte hello:

* Uma conta ativa do Azure. Se não tiver uma, você poderá se inscrever em uma [conta gratuita](https://azure.microsoft.com/free/). 
    * Como alternativa, você pode usar o hello [emulador de banco de dados do Azure Cosmos](local-emulator.md) para este tutorial.
* [Visual Studio Community 2017](http://www.visualstudio.com/).

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Etapa 1: Criar uma conta de banco de dados do Azure Cosmos DB
Vamos criar uma conta do Azure Cosmos DB. Se você já tiver uma conta que você deseja toouse, poderá pular muito[configurar sua solução do Visual Studio](#SetupVS). Se você estiver usando hello Azure Cosmos DB emulador, siga as etapas de saudação em [emulador de banco de dados do Azure Cosmos](local-emulator.md) toosetup Olá emulador e pular muito[configurar sua solução do Visual Studio](#SetupVS).

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupVS"></a>Etapa 2: configurar a sua solução do Visual Studio
1. Abra o **Visual Studio 2017** em seu computador.
2. Em Olá **arquivo** menu, selecione **novo**e, em seguida, escolha **projeto**.
3. Em Olá **novo projeto** caixa de diálogo, selecione **modelos** / **Visual C#** / **aplicativo de Console**, nome seu projeto e clique **Okey**.
   ![Captura de tela da janela do novo projeto de saudação](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)
4. Em Olá **Solution Explorer**, clique com o botão direito no seu novo aplicativo de console, que está em sua solução do Visual Studio, e, em seguida, clique em **gerenciar pacotes NuGet...**
    
    ![Captura de tela de saudação à direita Menu clicado para Olá projeto](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)
5. Em Olá **Nuget** , clique em **procurar**e o tipo **documentdb do azure** na caixa de pesquisa de saudação.
6. Nos resultados de saudação localizar **Microsoft.Azure.DocumentDB** e clique em **instalar**.
   ID do pacote Olá Olá biblioteca de cliente de API do Azure Cosmos DB DocumentDB é [biblioteca de cliente do Microsoft Azure DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).
   ![Captura de tela de saudação Menu do Nuget para localizar o SDK de cliente de banco de dados do Azure Cosmos](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)

    Se você receber uma mensagem sobre a revisar as alterações toohello solução, clique em **Okey**. Se receber uma mensagem sobre a aceitação da licença, clique em **Aceito**.

Ótimo! Concluída a instalação Olá, vamos começar a escrever um código. Você pode encontrar um projeto de código completo deste tutorial no [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).

## <a id="Connect"></a>Etapa 3: Conectar-se a conta de banco de dados do Azure Cosmos tooan
Primeiro, adicione estas referências toohello a partir de seu aplicativo c#, no arquivo Program.cs de saudação:

    using System;
    using System.Linq;
    using System.Threading.Tasks;

    // ADD THIS PART tooYOUR CODE
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;

> [!IMPORTANT]
> Tutorial de saudação do toocomplete ordem, certifique-se de que adicionar dependências de saudação acima.
> 
> 

Agora, adicione essas duas constantes e sua variável *client* sob sua classe pública *Program*.

    public class Program
    {
        // ADD THIS PART tooYOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;

Em seguida, head fazer toohello [Portal do Azure](https://portal.azure.com) tooretrieve sua URL de ponto de extremidade e a chave primária. URL de ponto de extremidade de saudação e a chave primária são necessárias para seu aplicativo toounderstand onde tooconnect e para o banco de dados do Azure Cosmos tootrust conexão do seu aplicativo.

Olá Portal do Azure, navegue conta de banco de dados do Azure Cosmos tooyour e, em seguida, clique no **chaves**.

Copie Olá URI do portal hello e cole-o na `<your endpoint URL>` no arquivo program.cs de saudação. Cópia Olá chave primária do portal hello e cole-o na `<your primary key>`.

![Captura de tela de saudação Portal do Azure usado pelo Olá NoSQL tutorial toocreate um aplicativo de console c#. Mostra um banco de dados do Azure Cosmos conta, com o hub ACTIVE Olá realçado, Olá realçado na folha de conta do banco de dados do Azure Cosmos Olá de botão de chaves e valores URI, chave primária e SECUNDÁRIA Olá realçados em Olá folha de chaves][keys]

Em seguida, vamos começar aplicativo hello, criando uma nova instância da saudação **DocumentClient**.

Abaixo Olá **principal** método, adicione essa nova tarefa assíncrona chamada **GetStartedDemo**, qual instanciará nosso novo **DocumentClient**.

    static void Main(string[] args)
    {
    }

    // ADD THIS PART tooYOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);
    }

Adicione o código a seguir Olá toorun sua tarefa assíncrona de seu **principal** método. Olá **principal** método capturar exceções e os grava toohello console.

    static void Main(string[] args)
    {
            // ADD THIS PART tooYOUR CODE
            try
            {
                    Program p = new Program();
                    p.GetStartedDemo().Wait();
            }
            catch (DocumentClientException de)
            {
                    Exception baseException = de.GetBaseException();
                    Console.WriteLine("{0} error occurred: {1}, Message: {2}", de.StatusCode, de.Message, baseException.Message);
            }
            catch (Exception e)
            {
                    Exception baseException = e.GetBaseException();
                    Console.WriteLine("Error: {0}, Message: {1}", e.Message, baseException.Message);
            }
            finally
            {
                    Console.WriteLine("End of demo, press any key tooexit.");
                    Console.ReadKey();
            }

Pressione **F5** toorun seu aplicativo. saída da janela de console Olá exibe a mensagem de saudação `End of demo, press any key tooexit.` confirmando que a conexão de saudação foi feita.  Você pode então fechar a janela do console hello. 

Parabéns! Você se conectou com êxito a conta de banco de dados do Azure Cosmos tooan, agora, vamos examinar trabalhando com recursos de banco de dados do Azure Cosmos.  

## <a name="step-4-create-a-database"></a>Etapa 4: criar um banco de dados
Antes de adicionar o código de saudação para a criação de um banco de dados, adicione um método auxiliar para gravar toohello console.

Copie e cole Olá **WriteToConsoleAndPromptToContinue** método após Olá **GetStartedDemo** método.

    // ADD THIS PART tooYOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key toocontinue ...");
            Console.ReadKey();
    }

O banco de dados do Azure Cosmos [banco de dados](documentdb-resources.md#databases) podem ser criados usando Olá [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) método hello **DocumentClient** classe. Um banco de dados é um contêiner lógico de saudação do armazenamento de documentos JSON particionado em coleções.

Copiar e colar a seguir Olá código tooyour **GetStartedDemo** método após a criação de saudação do cliente. Isso criará um banco de dados denominado *FamilyDB*.

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        // ADD THIS PART tooYOUR CODE
        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

Pressione **F5** toorun seu aplicativo.

Parabéns! Você criou um banco de dados do Azure Cosmos DB com êxito.  

## <a id="CreateColl"></a>Etapa 5: Criar uma coleção
> [!WARNING]
> **CreateDocumentCollectionIfNotExistsAsync** criará uma nova coleção com taxa de transferência reservada, com implicações de preço. Para obter mais detalhes, visite a nossa [página de preços](https://azure.microsoft.com/pricing/details/cosmos-db/).
> 
> 

Um [coleção](documentdb-resources.md#collections) podem ser criados usando Olá [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) método hello **DocumentClient** classe. Uma coleção é um contêiner de documentos JSON e uma lógica de aplicativo JavaScript associada.

Copiar e colar a seguir Olá código tooyour **GetStartedDemo** método após a criação do banco de dados de saudação. Essa ação criará uma coleção de documentos denominada *FamilyCollection*.

        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

        // ADD THIS PART tooYOUR CODE
         await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });

Pressione **F5** toorun seu aplicativo.

Parabéns! Você criou uma coleção de documentos do Azure Cosmos DB com êxito.  

## <a id="CreateDoc"></a>Etapa 6: Criar documentos JSON
Um [documento](documentdb-resources.md#documents) podem ser criados usando Olá [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) método hello **DocumentClient** classe. Os documentos são conteúdo JSON (arbitrário) definido pelo usuário. Agora podemos inserir um ou mais documentos. Se você já tiver dados você gostaria que toostore no banco de dados, você pode usar o hello Azure Cosmos DB [ferramenta de migração de dados](import-data.md) tooimport dados de saudação em um banco de dados.

Primeiro, precisamos toocreate um **família** classe que representa os objetos armazenados no banco de dados do Azure Cosmos neste exemplo. Também criaremos as subclasses **Parent**, **Child**, **Pet** e **Address** que são usadas em **Family**. Observe que os documentos devem ter uma propriedade **Id** serializada como **id** em JSON. Criar essas classes adicionando Olá classes sub internas a seguir após Olá **GetStartedDemo** método.

Copie e cole Olá **família**, **pai**, **filho**, **animal de estimação**, e **endereço** classes após Olá **WriteToConsoleAndPromptToContinue** método.

    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
    }

    // ADD THIS PART tooYOUR CODE
    public class Family
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        public string LastName { get; set; }
        public Parent[] Parents { get; set; }
        public Child[] Children { get; set; }
        public Address Address { get; set; }
        public bool IsRegistered { get; set; }
        public override string ToString()
        {
            return JsonConvert.SerializeObject(this);
        }
    }

    public class Parent
    {
        public string FamilyName { get; set; }
        public string FirstName { get; set; }
    }

    public class Child
    {
        public string FamilyName { get; set; }
        public string FirstName { get; set; }
        public string Gender { get; set; }
        public int Grade { get; set; }
        public Pet[] Pets { get; set; }
    }

    public class Pet
    {
        public string GivenName { get; set; }
    }

    public class Address
    {
        public string State { get; set; }
        public string County { get; set; }
        public string City { get; set; }
    }

Copie e cole Olá **CreateFamilyDocumentIfNotExists** método sob sua **endereço** classe.

    // ADD THIS PART tooYOUR CODE
    private async Task CreateFamilyDocumentIfNotExists(string databaseName, string collectionName, Family family)
    {
        try
        {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, family.Id));
            this.WriteToConsoleAndPromptToContinue("Found {0}", family.Id);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                await this.client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), family);
                this.WriteToConsoleAndPromptToContinue("Created Family {0}", family.Id);
            }
            else
            {
                throw;
            }
        }
    }

E inserir dois documentos, um para Olá Andersen família e hello Wakefield família.

Copiar e colar a seguir Olá código tooyour **GetStartedDemo** método após a criação de coleção do documento hello.

    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });
    
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });


    // ADD THIS PART tooYOUR CODE
    Family andersenFamily = new Family
    {
            Id = "Andersen.1",
            LastName = "Andersen",
            Parents = new Parent[]
            {
                    new Parent { FirstName = "Thomas" },
                    new Parent { FirstName = "Mary Kay" }
            },
            Children = new Child[]
            {
                    new Child
                    {
                            FirstName = "Henriette Thaulow",
                            Gender = "female",
                            Grade = 5,
                            Pets = new Pet[]
                            {
                                    new Pet { GivenName = "Fluffy" }
                            }
                    }
            },
            Address = new Address { State = "WA", County = "King", City = "Seattle" },
            IsRegistered = true
    };

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", andersenFamily);

    Family wakefieldFamily = new Family
    {
            Id = "Wakefield.7",
            LastName = "Wakefield",
            Parents = new Parent[]
            {
                    new Parent { FamilyName = "Wakefield", FirstName = "Robin" },
                    new Parent { FamilyName = "Miller", FirstName = "Ben" }
            },
            Children = new Child[]
            {
                    new Child
                    {
                            FamilyName = "Merriam",
                            FirstName = "Jesse",
                            Gender = "female",
                            Grade = 8,
                            Pets = new Pet[]
                            {
                                    new Pet { GivenName = "Goofy" },
                                    new Pet { GivenName = "Shadow" }
                            }
                    },
                    new Child
                    {
                            FamilyName = "Miller",
                            FirstName = "Lisa",
                            Gender = "female",
                            Grade = 1
                    }
            },
            Address = new Address { State = "NY", County = "Manhattan", City = "NY" },
            IsRegistered = false
    };

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

Pressione **F5** toorun seu aplicativo.

Parabéns! Você criou dois documentos do Azure Cosmos DB com êxito.  

![Diagrama ilustrando uma relação hierárquica Olá entre conta hello, banco de dados online hello, coleção hello e documentos Olá usados pelo Olá NoSQL tutorial toocreate um aplicativo de console c#](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <a id="Query"></a>Etapa 7: Consultar recursos do Azure Cosmos DB
O Azure Cosmos DB tem suporte para [consultas](documentdb-sql-query.md) avançadas de documentos JSON armazenados em cada coleção.  Olá, código de exemplo seguinte mostra várias consultas - usando ambos os SQL de banco de dados do Azure Cosmos sintaxe, bem como LINQ - que podem ser executados em relação a Olá documentos que são inseridos na etapa anterior hello.

Copie e cole Olá **ExecuteSimpleQuery** método após o **CreateFamilyDocumentIfNotExists** método.

    // ADD THIS PART tooYOUR CODE
    private void ExecuteSimpleQuery(string databaseName, string collectionName)
    {
        // Set some common query options
        FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };

            // Here we find hello Andersen family via its LastName
            IQueryable<Family> familyQuery = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                    .Where(f => f.LastName == "Andersen");

            // hello query is executed synchronously here, but can also be executed asynchronously via hello IDocumentQuery<T> interface
            Console.WriteLine("Running LINQ query...");
            foreach (Family family in familyQuery)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            // Now execute hello same query via direct SQL
            IQueryable<Family> familyQueryInSql = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                    "SELECT * FROM Family WHERE Family.LastName = 'Andersen'",
                    queryOptions);

            Console.WriteLine("Running direct SQL query...");
            foreach (Family family in familyQueryInSql)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            Console.WriteLine("Press any key toocontinue ...");
            Console.ReadKey();
    }

Copiar e colar a seguir Olá código tooyour **GetStartedDemo** método após a criação de documento segundo hello.

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    // ADD THIS PART tooYOUR CODE
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

Pressione **F5** toorun seu aplicativo.

Parabéns! Você consultou uma coleção do Azure Cosmos DB com êxito.

Olá diagrama a seguir ilustra como consultas de banco de dados SQL do Azure Cosmos Olá sintaxe é chamada na coleção de saudação que você criou e hello mesma lógica se aplica também a consulta LINQ em toohello.

![Diagrama ilustrando escopo hello e o significado da consulta Olá usado pelo Olá NoSQL tutorial toocreate um aplicativo de console c#](./media/documentdb-get-started/nosql-tutorial-collection-documents.png)

Olá [FROM](documentdb-sql-query.md#FromClause) palavra-chave é opcional em consulta Olá porque as consultas de banco de dados do Azure Cosmos já estão no escopo tooa única coleção. Portanto, "FROM Families f" pode ser trocado por "FROM root r" ou qualquer outra variável de nome que você escolher. Banco de dados do Azure Cosmos deduzirá que famílias, raiz ou o nome da variável Olá você escolheu, coleção atual de saudação de referência por padrão.

## <a id="ReplaceDocument"></a>Etapa 8: substituir o documento JSON
O Azure Cosmos DB dá suporte à substituição de documentos JSON.  

Copie e cole Olá **ReplaceFamilyDocument** método após o **ExecuteSimpleQuery** método.

    // ADD THIS PART tooYOUR CODE
    private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
    {
         await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
         this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }

Copiar e colar a seguir Olá código tooyour **GetStartedDemo** método após a execução de consulta hello, no final de saudação do método hello. Depois de substituir o documento hello, isso será executado Olá mesmo novamente consultar tooview Olá alterado documento.

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    // ADD THIS PART tooYOUR CODE
    // Update hello Grade of hello Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

Pressione **F5** toorun seu aplicativo.

Parabéns! Você substituiu um documento do Azure Cosmos DB com sucesso.

## <a id="DeleteDocument"></a>Etapa 9: excluir o documento JSON
O Azure Cosmos DB dá suporte à exclusão de documentos JSON.  

Copie e cole Olá **DeleteFamilyDocument** método após o **ReplaceFamilyDocument** método.

    // ADD THIS PART tooYOUR CODE
    private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
    {
         await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
         Console.WriteLine("Deleted Family {0}", documentName);
    }

Copiar e colar a seguir Olá código tooyour **GetStartedDemo** método após a execução da consulta de saudação segundo, no final de saudação do método hello.

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);
    
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");
    
    // ADD THIS PART tooCODE
    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

Pressione **F5** toorun seu aplicativo.

Parabéns! Você excluiu um documento do Azure Cosmos DB com êxito.

## <a id="DeleteDatabase"></a>Etapa 10: Excluir o banco de dados de saudação
Excluindo Olá criado o banco de dados removerá o banco de dados de saudação e todos os recursos de filhos (coleções, documentos, etc.).

Copiar e colar a seguir Olá código tooyour **GetStartedDemo** método após documento hello excluir banco de dados inteiro toodelete hello e todos os recursos de filhos.

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

    // ADD THIS PART tooCODE
    // Clean up/delete hello database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB"));

Pressione **F5** toorun seu aplicativo.

Parabéns! Você excluiu um banco de dados do Azure Cosmos DB com êxito.

## <a id="Run"></a>Etapa 11: executar o aplicativo de console C# inteiro!
Pressione F5 no aplicativo do Visual Studio toobuild hello no modo de depuração.

Você deve ver a saída de saudação do aplicativo iniciado get em uma janela de console. saída de Hello mostrará os resultados de saudação do hello consultas adicionamos e deve coincidir com o texto de exemplo hello abaixo.

    Created FamilyDB
    Press any key toocontinue ...
    Created FamilyCollection
    Press any key toocontinue ...
    Created Family Andersen.1
    Press any key toocontinue ...
    Created Family Wakefield.7
    Press any key toocontinue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Replaced Family Andersen.1
    Press any key toocontinue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Deleted Family Andersen.1
    End of demo, press any key tooexit.

Parabéns! Você concluiu o tutorial hello e ter um aplicativo de console funcional c#!

## <a id="GetSolution"></a>Obter a solução completa de tutorial Olá
Se você não tem tempo Olá toocomplete as etapas neste tutorial, ou apenas deseja toodownload Olá exemplos de código, você poderá obtê-lo de [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started). 

toobuild solução de GetStarted hello, você precisará seguir hello:

* Uma conta ativa do Azure. Se não tiver uma, você poderá se inscrever em uma [conta gratuita](https://azure.microsoft.com/free/).
* Uma [conta do Azure Cosmos DB][cosmos-db-create-account].
* Olá [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) solução disponível no GitHub.

toorestore Olá referências toohello SDK .NET do Azure Cosmos banco de dados no Visual Studio, clique com botão direito Olá **GetStarted** solução no Gerenciador de soluções e clique **habilite a restauração do pacote de NuGet**. Em seguida, no arquivo App. config de hello, atualizar Olá EndpointUrl e AuthorizationKey valores conforme descrito em [conectar-se a conta de banco de dados do Azure Cosmos tooan](#Connect).

Pronto, compile-o e você pode continuar!


## <a name="next-steps"></a>Próximas etapas
* Quer um tutorial mais complexo do ASP.NET MVC? Confira [Tutorial do ASP.NET MVC: desenvolvimento de aplicativo Web com o Azure Cosmos DB](documentdb-dotnet-application.md).
* Deseja tooperform escala e testes de desempenho com o banco de dados do Azure Cosmos? Confira [Teste de desempenho e escala com o Azure Cosmos DB](performance-testing.md)
* Saiba como muito[monitorar solicitações, uso e armazenamento do banco de dados do Azure Cosmos](monitor-accounts.md).
* Executar consultas em nosso conjunto de dados de exemplo hello [parque de consulta](https://www.documentdb.com/sql/demo).
* toolearn mais sobre Azure Cosmos DB, consulte [tooAzure Cosmos DB de boas-vindas](https://docs.microsoft.com/azure/cosmos-db/introduction).

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
[cosmos-db-create-account]: create-documentdb-dotnet.md#create-account
