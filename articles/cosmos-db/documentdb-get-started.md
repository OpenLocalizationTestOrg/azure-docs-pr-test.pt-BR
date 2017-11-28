---
title: "Azure Cosmos DB: tutorial de introdução da API do DocumentDB | Microsoft Docs"
description: Um tutorial que cria um banco de dados online e um aplicativo de console C# usando a API do DocumentDB.
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
ms.openlocfilehash: 72f66081a6409f980ec6bca5188f585489245a36
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-documentdb-api-getting-started-tutorial"></a><span data-ttu-id="d6722-104">Azure Cosmos DB: tutorial de introdução da API do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="d6722-104">Azure Cosmos DB: DocumentDB API getting started tutorial</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d6722-105">.NET</span><span class="sxs-lookup"><span data-stu-id="d6722-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="d6722-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="d6722-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="d6722-107">Node.js para MongoDB</span><span class="sxs-lookup"><span data-stu-id="d6722-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="d6722-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="d6722-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="d6722-109">Java</span><span class="sxs-lookup"><span data-stu-id="d6722-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="d6722-110">C++</span><span class="sxs-lookup"><span data-stu-id="d6722-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="d6722-111">Bem-vindo(a) ao tutorial de introdução da API do DocumentDB do Azure Cosmos DB!</span><span class="sxs-lookup"><span data-stu-id="d6722-111">Welcome to the Azure Cosmos DB DocumentDB API getting started tutorial!</span></span> <span data-ttu-id="d6722-112">Após seguir este tutorial, você terá um aplicativo de console que cria e consulta recursos do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d6722-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="d6722-113">Abordaremos:</span><span class="sxs-lookup"><span data-stu-id="d6722-113">We'll cover:</span></span>

* <span data-ttu-id="d6722-114">Criar e conectar-se a uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d6722-114">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="d6722-115">Configurar a sua Solução do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d6722-115">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="d6722-116">Criando um banco de dados online</span><span class="sxs-lookup"><span data-stu-id="d6722-116">Creating an online database</span></span>
* <span data-ttu-id="d6722-117">Criar uma coleção</span><span class="sxs-lookup"><span data-stu-id="d6722-117">Creating a collection</span></span>
* <span data-ttu-id="d6722-118">Criando documentos JSON</span><span class="sxs-lookup"><span data-stu-id="d6722-118">Creating JSON documents</span></span>
* <span data-ttu-id="d6722-119">Consultar a coleção</span><span class="sxs-lookup"><span data-stu-id="d6722-119">Querying the collection</span></span>
* <span data-ttu-id="d6722-120">Substituição de um documento</span><span class="sxs-lookup"><span data-stu-id="d6722-120">Replacing a document</span></span>
* <span data-ttu-id="d6722-121">Exclusão de um documento</span><span class="sxs-lookup"><span data-stu-id="d6722-121">Deleting a document</span></span>
* <span data-ttu-id="d6722-122">Excluir o banco de dados</span><span class="sxs-lookup"><span data-stu-id="d6722-122">Deleting the database</span></span>

<span data-ttu-id="d6722-123">Você não tem tempo?</span><span class="sxs-lookup"><span data-stu-id="d6722-123">Don't have time?</span></span> <span data-ttu-id="d6722-124">Não se preocupe!</span><span class="sxs-lookup"><span data-stu-id="d6722-124">Don't worry!</span></span> <span data-ttu-id="d6722-125">A solução completa está disponível em [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="d6722-125">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> <span data-ttu-id="d6722-126">Vá para a [seção Obter a solução do tutorial do NoSQL completo](#GetSolution) para obter instruções rápidas.</span><span class="sxs-lookup"><span data-stu-id="d6722-126">Jump to the [Get the complete NoSQL tutorial solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="d6722-127">Em seguida, use os botões de votação na parte superior ou inferior desta página para nos enviar comentários.</span><span class="sxs-lookup"><span data-stu-id="d6722-127">Afterwards, please use the voting buttons at the top or bottom of this page to give us feedback.</span></span> <span data-ttu-id="d6722-128">Se quiser que entremos em contato com você diretamente, inclua seu endereço de email em seu comentário.</span><span class="sxs-lookup"><span data-stu-id="d6722-128">If you'd like us to contact you directly, feel free to include your email address in your comments.</span></span>

<span data-ttu-id="d6722-129">Agora vamos começar!</span><span class="sxs-lookup"><span data-stu-id="d6722-129">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6722-130">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d6722-130">Prerequisites</span></span>
<span data-ttu-id="d6722-131">Certifique-se que você tem o seguinte:</span><span class="sxs-lookup"><span data-stu-id="d6722-131">Please make sure you have the following:</span></span>

* <span data-ttu-id="d6722-132">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6722-132">An active Azure account.</span></span> <span data-ttu-id="d6722-133">Se não tiver uma, você poderá se inscrever em uma [conta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="d6722-133">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="d6722-134">Como alternativa, você pode usar o [Emulador do Azure Cosmos DB](local-emulator.md) neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="d6722-134">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="d6722-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="d6722-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="d6722-136">Etapa 1: Criar uma conta de banco de dados do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d6722-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="d6722-137">Vamos criar uma conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d6722-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="d6722-138">Se você já tem uma conta que deseja usar, você pode pular para [Configurar sua solução do Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="d6722-138">If you already have an account you want to use, you can skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="d6722-139">Se estiver usando o Emulador do Azure Cosmos DB, execute as etapas em [Emulador do Azure Cosmos DB](local-emulator.md) para configurar o emulador e pule para [Configurar sua solução do Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="d6722-139">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="d6722-140"><a id="SetupVS"></a>Etapa 2: configurar a sua solução do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d6722-140"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="d6722-141">Abra o **Visual Studio 2017** em seu computador.</span><span class="sxs-lookup"><span data-stu-id="d6722-141">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="d6722-142">No menu **Arquivo**, selecione **Novo** e depois **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="d6722-142">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="d6722-143">Na caixa de diálogo **Novo Projeto**, selecione **Modelos** / **Visual C#** / **Aplicativo de Console**, nomeie o projeto e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d6722-143">In the **New Project** dialog, select **Templates** / **Visual C#** / **Console Application**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="d6722-144">![Captura de tela da janela Novo Projeto](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="d6722-144">![Screen shot of the New Project window](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span></span>
4. <span data-ttu-id="d6722-145">No **Gerenciador de Soluções**, clique com o botão direito do mouse no seu novo aplicativo de console, que está em sua solução do Visual Studio e clique em **gerenciar pacotes NuGet...**</span><span class="sxs-lookup"><span data-stu-id="d6722-145">In the **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Captura de tela do menu exibido pelo clique com o botão direito do mouse para o projeto](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="d6722-147">Na guia **Nuget**, clique em **Procurar** e digite **azure documentdb** na caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6722-147">In the **Nuget** tab, click **Browse**, and type **azure documentdb** in the search box.</span></span>
6. <span data-ttu-id="d6722-148">Nos resultados, encontre **Microsoft.Azure.DocumentDB** e clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="d6722-148">Within the results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="d6722-149">A ID do pacote para a Biblioteca de Clientes de API do DocumentDB no Azure Cosmos DB é [ Biblioteca de Clientes do Microsoft Azure DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span><span class="sxs-lookup"><span data-stu-id="d6722-149">The package ID for the Azure Cosmos DB DocumentDB API Client Library is [Microsoft Azure DocumentDB Client Library](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span></span>
   <span data-ttu-id="d6722-150">![Captura de tela do menu NuGet para localizar documentos do SDK do cliente do Azure Cosmos DB](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="d6722-150">![Screen shot of the Nuget Menu for finding Azure Cosmos DB Client SDK](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="d6722-151">Se receber uma mensagem sobre a análise das alterações para a solução, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d6722-151">If you get a messages about reviewing changes to the solution, click **OK**.</span></span> <span data-ttu-id="d6722-152">Se receber uma mensagem sobre a aceitação da licença, clique em **Aceito**.</span><span class="sxs-lookup"><span data-stu-id="d6722-152">If you get a message about license acceptance, click **I accept**.</span></span>

<span data-ttu-id="d6722-153">Ótimo!</span><span class="sxs-lookup"><span data-stu-id="d6722-153">Great!</span></span> <span data-ttu-id="d6722-154">Agora que a instalação está concluída, vamos começar a escrever algum código.</span><span class="sxs-lookup"><span data-stu-id="d6722-154">Now that we finished the setup, let's start writing some code.</span></span> <span data-ttu-id="d6722-155">Você pode encontrar um projeto de código completo deste tutorial no [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="d6722-155">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span></span>

## <span data-ttu-id="d6722-156"><a id="Connect"></a>Etapa 3: Conectar-se a uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d6722-156"><a id="Connect"></a>Step 3: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="d6722-157">Primeiro, adicione essas referências para o início de seu aplicativo C#, no arquivo Program.cs:</span><span class="sxs-lookup"><span data-stu-id="d6722-157">First, add these references to the beginning of your C# application, in the Program.cs file:</span></span>

    using System;
    using System.Linq;
    using System.Threading.Tasks;

    // ADD THIS PART TO YOUR CODE
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;

> [!IMPORTANT]
> <span data-ttu-id="d6722-158">Para concluir este tutorial, adicione as dependências acima.</span><span class="sxs-lookup"><span data-stu-id="d6722-158">In order to complete the tutorial, make sure you add the dependencies above.</span></span>
> 
> 

<span data-ttu-id="d6722-159">Agora, adicione essas duas constantes e sua variável *client* sob sua classe pública *Program*.</span><span class="sxs-lookup"><span data-stu-id="d6722-159">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

    public class Program
    {
        // ADD THIS PART TO YOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;

<span data-ttu-id="d6722-160">Em seguida, volte ao [Portal do Azure](https://portal.azure.com) para recuperar a URL do ponto de extremidade e a chave primária.</span><span class="sxs-lookup"><span data-stu-id="d6722-160">Next, head back to the [Azure Portal](https://portal.azure.com) to retrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="d6722-161">A URL do ponto de extremidade e a chave primária são necessárias para que seu aplicativo reconheça onde deve se conectar e para que o Azure Cosmos DB confie na conexão do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d6722-161">The endpoint URL and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="d6722-162">No Portal do Azure, navegue até sua conta do Azure Cosmos DB e clique em **Chaves**.</span><span class="sxs-lookup"><span data-stu-id="d6722-162">In the Azure Portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="d6722-163">Copie o URI do portal e cole-o em `<your endpoint URL>` no arquivo program.cs.</span><span class="sxs-lookup"><span data-stu-id="d6722-163">Copy the URI from the portal and paste it into `<your endpoint URL>` in the program.cs file.</span></span> <span data-ttu-id="d6722-164">Em seguida, copie a CHAVE PRIMÁRIA do portal e cole-a em `<your primary key>`.</span><span class="sxs-lookup"><span data-stu-id="d6722-164">Then copy the PRIMARY KEY from the portal and paste it into `<your primary key>`.</span></span>

![Captura de tela do Portal do Azure usado pelo tutorial do NoSQL para criar um aplicativo de console em C#.][keys]

<span data-ttu-id="d6722-167">Em seguida, vamos iniciar o aplicativo criando uma nova instância de **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="d6722-167">Next, we'll start the application by creating a new instance of the **DocumentClient**.</span></span>

<span data-ttu-id="d6722-168">Abaixo do método **Main**, adicione esta nova tarefa assíncrona denominada **GetStartedDemo**, que criará uma instância do nosso novo **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="d6722-168">Below the **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

    static void Main(string[] args)
    {
    }

    // ADD THIS PART TO YOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);
    }

<span data-ttu-id="d6722-169">Adicione o código a seguir para executar a tarefa assíncrona a partir do seu método **Main** .</span><span class="sxs-lookup"><span data-stu-id="d6722-169">Add the following code to run your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="d6722-170">O método **Main** capturará as exceções e as gravará no console.</span><span class="sxs-lookup"><span data-stu-id="d6722-170">The **Main** method will catch exceptions and write them to the console.</span></span>

    static void Main(string[] args)
    {
            // ADD THIS PART TO YOUR CODE
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
                    Console.WriteLine("End of demo, press any key to exit.");
                    Console.ReadKey();
            }

<span data-ttu-id="d6722-171">Pressione **F5** para executar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d6722-171">Press **F5** to run your application.</span></span> <span data-ttu-id="d6722-172">A saída da janela console exibe a mensagem `End of demo, press any key to exit.`, confirmando que a conexão foi feita.</span><span class="sxs-lookup"><span data-stu-id="d6722-172">The console window output displays the message `End of demo, press any key to exit.` confirming that the connection was made.</span></span>  <span data-ttu-id="d6722-173">Em seguida, você pode fechar a janela do console.</span><span class="sxs-lookup"><span data-stu-id="d6722-173">You can then close the console window.</span></span> 

<span data-ttu-id="d6722-174">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="d6722-174">Congratulations!</span></span> <span data-ttu-id="d6722-175">Você se conectou a uma conta do Azure Cosmos DB. Agora, vamos conferir como trabalhar com recursos do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d6722-175">You have successfully connected to an Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="d6722-176">Etapa 4: criar um banco de dados</span><span class="sxs-lookup"><span data-stu-id="d6722-176">Step 4: Create a database</span></span>
<span data-ttu-id="d6722-177">Antes de adicionar o código para criar um banco de dados, adicione um método auxiliar para gravar no console.</span><span class="sxs-lookup"><span data-stu-id="d6722-177">Before you add the code for creating a database, add a helper method for writing to the console.</span></span>

<span data-ttu-id="d6722-178">Copie e cole o método **WriteToConsoleAndPromptToContinue** após o método **GetStartedDemo**.</span><span class="sxs-lookup"><span data-stu-id="d6722-178">Copy and paste the **WriteToConsoleAndPromptToContinue** method after the **GetStartedDemo** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }

<span data-ttu-id="d6722-179">Seu [banco de dados](documentdb-resources.md#databases) do Azure Cosmos DB pode ser criado com o método [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) da classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="d6722-179">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using the [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="d6722-180">Um banco de dados é o contêiner lógico de armazenamento de documentos JSON particionado em coleções.</span><span class="sxs-lookup"><span data-stu-id="d6722-180">A database is the logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="d6722-181">Copie e cole o código a seguir no seu método **GetStartedDemo** após a criação do cliente.</span><span class="sxs-lookup"><span data-stu-id="d6722-181">Copy and paste the following code to your **GetStartedDemo** method after the client creation.</span></span> <span data-ttu-id="d6722-182">Isso criará um banco de dados denominado *FamilyDB*.</span><span class="sxs-lookup"><span data-stu-id="d6722-182">This will create a database named *FamilyDB*.</span></span>

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        // ADD THIS PART TO YOUR CODE
        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

<span data-ttu-id="d6722-183">Pressione **F5** para executar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d6722-183">Press **F5** to run your application.</span></span>

<span data-ttu-id="d6722-184">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="d6722-184">Congratulations!</span></span> <span data-ttu-id="d6722-185">Você criou um banco de dados do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="d6722-185">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="d6722-186"><a id="CreateColl"></a>Etapa 5: Criar uma coleção</span><span class="sxs-lookup"><span data-stu-id="d6722-186"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="d6722-187">**CreateDocumentCollectionIfNotExistsAsync** criará uma nova coleção com taxa de transferência reservada, com implicações de preço.</span><span class="sxs-lookup"><span data-stu-id="d6722-187">**CreateDocumentCollectionIfNotExistsAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="d6722-188">Para obter mais detalhes, visite a nossa [página de preços](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="d6722-188">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="d6722-189">É possível criar uma [coleção](documentdb-resources.md#collections) com o método [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) da classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="d6722-189">A [collection](documentdb-resources.md#collections) can be created by using the [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="d6722-190">Uma coleção é um contêiner de documentos JSON e uma lógica de aplicativo JavaScript associada.</span><span class="sxs-lookup"><span data-stu-id="d6722-190">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="d6722-191">Copie e cole o código a seguir no método **GetStartedDemo** após a criação do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="d6722-191">Copy and paste the following code to your **GetStartedDemo** method after the database creation.</span></span> <span data-ttu-id="d6722-192">Essa ação criará uma coleção de documentos denominada *FamilyCollection*.</span><span class="sxs-lookup"><span data-stu-id="d6722-192">This will create a document collection named *FamilyCollection*.</span></span>

        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

        // ADD THIS PART TO YOUR CODE
         await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });

<span data-ttu-id="d6722-193">Pressione **F5** para executar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d6722-193">Press **F5** to run your application.</span></span>

<span data-ttu-id="d6722-194">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="d6722-194">Congratulations!</span></span> <span data-ttu-id="d6722-195">Você criou uma coleção de documentos do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="d6722-195">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="d6722-196"><a id="CreateDoc"></a>Etapa 6: Criar documentos JSON</span><span class="sxs-lookup"><span data-stu-id="d6722-196"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="d6722-197">Um [documento](documentdb-resources.md#documents) pode ser criado usando o método [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) da classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="d6722-197">A [document](documentdb-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="d6722-198">Os documentos são conteúdo JSON (arbitrário) definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="d6722-198">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="d6722-199">Agora podemos inserir um ou mais documentos.</span><span class="sxs-lookup"><span data-stu-id="d6722-199">We can now insert one or more documents.</span></span> <span data-ttu-id="d6722-200">Se já tiver dados que deseja armazenar no banco de dados, você poderá usar a [ferramenta de migração de dados](import-data.md) do Azure Cosmos DB para importar os dados para um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="d6722-200">If you already have data you'd like to store in your database, you can use the Azure Cosmos DB [Data Migration tool](import-data.md) to import the data into a database.</span></span>

<span data-ttu-id="d6722-201">Primeiro, precisamos criar uma classe **Family** que representará os objetos armazenados no Azure Cosmos DB neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="d6722-201">First, we need to create a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="d6722-202">Também criaremos as subclasses **Parent**, **Child**, **Pet** e **Address** que são usadas em **Family**.</span><span class="sxs-lookup"><span data-stu-id="d6722-202">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="d6722-203">Observe que os documentos devem ter uma propriedade **Id** serializada como **id** em JSON.</span><span class="sxs-lookup"><span data-stu-id="d6722-203">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="d6722-204">Crie essas classes, adicionando as seguintes subclasses internas após o método **GetStartedDemo** .</span><span class="sxs-lookup"><span data-stu-id="d6722-204">Create these classes by adding the following internal sub-classes after the **GetStartedDemo** method.</span></span>

<span data-ttu-id="d6722-205">Copie e cole as classes **Family**, **Parent**, **Child**, **Pet** e **Address** após o método **WriteToConsoleAndPromptToContinue**.</span><span class="sxs-lookup"><span data-stu-id="d6722-205">Copy and paste the **Family**, **Parent**, **Child**, **Pet**, and **Address** classes after the **WriteToConsoleAndPromptToContinue** method.</span></span>

    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
    }

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="d6722-206">Copie e cole o método **CreateFamilyDocumentIfNotExists** sob sua classe **Address**.</span><span class="sxs-lookup"><span data-stu-id="d6722-206">Copy and paste the **CreateFamilyDocumentIfNotExists** method underneath your **Address** class.</span></span>

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="d6722-207">Insira dois documentos, um para a Família Martins e um para a Família Barros.</span><span class="sxs-lookup"><span data-stu-id="d6722-207">And insert two documents, one each for the Andersen Family and the Wakefield Family.</span></span>

<span data-ttu-id="d6722-208">Copie e cole o código a seguir no seu método **GetStartedDemo** após a criação da coleção de documentos.</span><span class="sxs-lookup"><span data-stu-id="d6722-208">Copy and paste the following code to your **GetStartedDemo** method after the document collection creation.</span></span>

    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });
    
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });


    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="d6722-209">Pressione **F5** para executar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d6722-209">Press **F5** to run your application.</span></span>

<span data-ttu-id="d6722-210">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="d6722-210">Congratulations!</span></span> <span data-ttu-id="d6722-211">Você criou dois documentos do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="d6722-211">You have successfully created two Azure Cosmos DB documents.</span></span>  

![Diagrama que ilustra a relação hierárquica entre a conta, o banco de dados online, a coleção e os documentos usados pelo tutorial do NoSQL para criar um aplicativo de console em C#](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="d6722-213"><a id="Query"></a>Etapa 7: Consultar recursos do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d6722-213"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="d6722-214">O Azure Cosmos DB tem suporte para [consultas](documentdb-sql-query.md) avançadas de documentos JSON armazenados em cada coleção.</span><span class="sxs-lookup"><span data-stu-id="d6722-214">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="d6722-215">O exemplo de código a seguir mostra diversas consultas - usando a sintaxe SQL do Azure Cosmos DB bem como o LINQ - que podem ser realizadas nos documentos que inserimos na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="d6722-215">The following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against the documents we inserted in the previous step.</span></span>

<span data-ttu-id="d6722-216">Copie e cole o método **ExecuteSimpleQuery** após o método **CreateFamilyDocumentIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="d6722-216">Copy and paste the **ExecuteSimpleQuery** method after your **CreateFamilyDocumentIfNotExists** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private void ExecuteSimpleQuery(string databaseName, string collectionName)
    {
        // Set some common query options
        FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };

            // Here we find the Andersen family via its LastName
            IQueryable<Family> familyQuery = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                    .Where(f => f.LastName == "Andersen");

            // The query is executed synchronously here, but can also be executed asynchronously via the IDocumentQuery<T> interface
            Console.WriteLine("Running LINQ query...");
            foreach (Family family in familyQuery)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            // Now execute the same query via direct SQL
            IQueryable<Family> familyQueryInSql = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                    "SELECT * FROM Family WHERE Family.LastName = 'Andersen'",
                    queryOptions);

            Console.WriteLine("Running direct SQL query...");
            foreach (Family family in familyQueryInSql)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }

<span data-ttu-id="d6722-217">Copie e cole o código a seguir no seu método **GetStartedDemo** após a criação do segundo documento.</span><span class="sxs-lookup"><span data-stu-id="d6722-217">Copy and paste the following code to your **GetStartedDemo** method after the second document creation.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    // ADD THIS PART TO YOUR CODE
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="d6722-218">Pressione **F5** para executar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d6722-218">Press **F5** to run your application.</span></span>

<span data-ttu-id="d6722-219">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="d6722-219">Congratulations!</span></span> <span data-ttu-id="d6722-220">Você consultou uma coleção do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="d6722-220">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="d6722-221">O diagrama a seguir ilustra como a sintaxe da consulta SQL do Azure Cosmos DB é chamada em relação à coleção que você criou, e a mesma lógica se aplica à consulta LINQ.</span><span class="sxs-lookup"><span data-stu-id="d6722-221">The following diagram illustrates how the Azure Cosmos DB SQL query syntax is called against the collection you created, and the same logic applies to the LINQ query as well.</span></span>

![Diagrama que ilustra o escopo e o significado da consulta usada pelo tutorial do NoSQL para criar um aplicativo de console em C#](./media/documentdb-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="d6722-223">A palavra-chave [FROM](documentdb-sql-query.md#FromClause) é opcional na consulta, pois as consultas do Azure Cosmos DB já têm o escopo para uma única coleção.</span><span class="sxs-lookup"><span data-stu-id="d6722-223">The [FROM](documentdb-sql-query.md#FromClause) keyword is optional in the query because Azure Cosmos DB queries are already scoped to a single collection.</span></span> <span data-ttu-id="d6722-224">Portanto, "FROM Families f" pode ser trocado por "FROM root r" ou qualquer outra variável de nome que você escolher.</span><span class="sxs-lookup"><span data-stu-id="d6722-224">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="d6722-225">O Azure Cosmos DB inferirá que Famílias, raiz ou o nome de variável escolhido faz referência à coleção atual por padrão.</span><span class="sxs-lookup"><span data-stu-id="d6722-225">Azure Cosmos DB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span></span>

## <span data-ttu-id="d6722-226"><a id="ReplaceDocument"></a>Etapa 8: substituir o documento JSON</span><span class="sxs-lookup"><span data-stu-id="d6722-226"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="d6722-227">O Azure Cosmos DB dá suporte à substituição de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="d6722-227">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="d6722-228">Copie e cole o método **ReplaceFamilyDocument** após o método **ExecuteSimpleQuery**.</span><span class="sxs-lookup"><span data-stu-id="d6722-228">Copy and paste the **ReplaceFamilyDocument** method after your **ExecuteSimpleQuery** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
    {
         await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
         this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }

<span data-ttu-id="d6722-229">Copie e cole o seguinte código para o método **GetStartedDemo** após a execução da consulta, no fim do método.</span><span class="sxs-lookup"><span data-stu-id="d6722-229">Copy and paste the following code to your **GetStartedDemo** method after the query execution, at the end of the method.</span></span> <span data-ttu-id="d6722-230">Depois de substituir o documento, isso executará a mesma consulta novamente para exibir o documento alterado.</span><span class="sxs-lookup"><span data-stu-id="d6722-230">After replacing the document, this will run the same query again to view the changed document.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    // ADD THIS PART TO YOUR CODE
    // Update the Grade of the Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="d6722-231">Pressione **F5** para executar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d6722-231">Press **F5** to run your application.</span></span>

<span data-ttu-id="d6722-232">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="d6722-232">Congratulations!</span></span> <span data-ttu-id="d6722-233">Você substituiu um documento do Azure Cosmos DB com sucesso.</span><span class="sxs-lookup"><span data-stu-id="d6722-233">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="d6722-234"><a id="DeleteDocument"></a>Etapa 9: excluir o documento JSON</span><span class="sxs-lookup"><span data-stu-id="d6722-234"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="d6722-235">O Azure Cosmos DB dá suporte à exclusão de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="d6722-235">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="d6722-236">Copie e cole o método **DeleteFamilyDocument** após o método **ReplaceFamilyDocument**.</span><span class="sxs-lookup"><span data-stu-id="d6722-236">Copy and paste the **DeleteFamilyDocument** method after your **ReplaceFamilyDocument** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
    {
         await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
         Console.WriteLine("Deleted Family {0}", documentName);
    }

<span data-ttu-id="d6722-237">Copie e cole o seguinte código para o método **GetStartedDemo** após a execução da segunda consulta, no fim do método.</span><span class="sxs-lookup"><span data-stu-id="d6722-237">Copy and paste the following code to your **GetStartedDemo** method after the second query execution, at the end of the method.</span></span>

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);
    
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");
    
    // ADD THIS PART TO CODE
    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

<span data-ttu-id="d6722-238">Pressione **F5** para executar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d6722-238">Press **F5** to run your application.</span></span>

<span data-ttu-id="d6722-239">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="d6722-239">Congratulations!</span></span> <span data-ttu-id="d6722-240">Você excluiu um documento do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="d6722-240">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="d6722-241"><a id="DeleteDatabase"></a>Etapa 10: excluir o banco de dados</span><span class="sxs-lookup"><span data-stu-id="d6722-241"><a id="DeleteDatabase"></a>Step 10: Delete the database</span></span>
<span data-ttu-id="d6722-242">Excluir o banco de dados criado removerá o banco de dados e todos os recursos filhos (coleções, documentos, etc.).</span><span class="sxs-lookup"><span data-stu-id="d6722-242">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="d6722-243">Copie e cole o código a seguir de seu método **GetStartedDemo** após a exclusão de documento para excluir o banco de dados inteiro e todos os recursos-filhos.</span><span class="sxs-lookup"><span data-stu-id="d6722-243">Copy and paste the following code to your **GetStartedDemo** method after the document delete to delete the entire database and all children resources.</span></span>

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

    // ADD THIS PART TO CODE
    // Clean up/delete the database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB"));

<span data-ttu-id="d6722-244">Pressione **F5** para executar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d6722-244">Press **F5** to run your application.</span></span>

<span data-ttu-id="d6722-245">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="d6722-245">Congratulations!</span></span> <span data-ttu-id="d6722-246">Você excluiu um banco de dados do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="d6722-246">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="d6722-247"><a id="Run"></a>Etapa 11: executar o aplicativo de console C# inteiro!</span><span class="sxs-lookup"><span data-stu-id="d6722-247"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="d6722-248">Pressione F5 no Visual Studio para compilar o aplicativo no modo de depuração.</span><span class="sxs-lookup"><span data-stu-id="d6722-248">Hit F5 in Visual Studio to build the application in debug mode.</span></span>

<span data-ttu-id="d6722-249">Você deverá ver a saída do aplicativo iniciado em uma janela do console.</span><span class="sxs-lookup"><span data-stu-id="d6722-249">You should see the output of your get started app in a console window.</span></span> <span data-ttu-id="d6722-250">A saída mostrará os resultados das consultas que adicionamos e deverá coincidir com o texto de exemplo abaixo.</span><span class="sxs-lookup"><span data-stu-id="d6722-250">The output will show the results of the queries we added and should match the example text below.</span></span>

    Created FamilyDB
    Press any key to continue ...
    Created FamilyCollection
    Press any key to continue ...
    Created Family Andersen.1
    Press any key to continue ...
    Created Family Wakefield.7
    Press any key to continue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Replaced Family Andersen.1
    Press any key to continue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Deleted Family Andersen.1
    End of demo, press any key to exit.

<span data-ttu-id="d6722-251">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="d6722-251">Congratulations!</span></span> <span data-ttu-id="d6722-252">Você concluiu este tutorial e tem um aplicativo de console em C# funcional!</span><span class="sxs-lookup"><span data-stu-id="d6722-252">You've completed the tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="d6722-253"><a id="GetSolution"></a> Obter a solução completa do tutorial</span><span class="sxs-lookup"><span data-stu-id="d6722-253"><a id="GetSolution"></a> Get the complete tutorial solution</span></span>
<span data-ttu-id="d6722-254">Se você não teve tempo para concluir as etapas neste tutorial ou se deseja apenas baixar os exemplos de código, poderá obtê-los no [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="d6722-254">If you didn't have time to complete the steps in this tutorial, or just want to download the code samples, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> 

<span data-ttu-id="d6722-255">Para criar a solução de Introdução, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="d6722-255">To build the GetStarted solution, you will need the following:</span></span>

* <span data-ttu-id="d6722-256">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6722-256">An active Azure account.</span></span> <span data-ttu-id="d6722-257">Se não tiver uma, você poderá se inscrever em uma [conta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="d6722-257">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="d6722-258">Uma [conta do Azure Cosmos DB][cosmos-db-create-account].</span><span class="sxs-lookup"><span data-stu-id="d6722-258">An [Azure Cosmos DB account][cosmos-db-create-account].</span></span>
* <span data-ttu-id="d6722-259">A solução [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) disponível no GitHub.</span><span class="sxs-lookup"><span data-stu-id="d6722-259">The [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="d6722-260">Para restaurar as referências do SDK do .NET do Azure Cosmos DB no Visual Studio, clique com o botão direito do mouse na solução **GetStarted** no Gerenciador de Soluções e clique em **Habilitar Pacote de Restauração NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d6722-260">To restore the references to the Azure Cosmos DB .NET SDK in Visual Studio, right-click the **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="d6722-261">Em seguida, no arquivo App.config, atualize os valores EndpointUrl e AuthorizationKey conforme descrito em [Conectar-se a uma conta do Azure Cosmos DB](#Connect).</span><span class="sxs-lookup"><span data-stu-id="d6722-261">Next, in the App.config file, update the EndpointUrl and AuthorizationKey values as described in [Connect to an Azure Cosmos DB account](#Connect).</span></span>

<span data-ttu-id="d6722-262">Pronto, compile-o e você pode continuar!</span><span class="sxs-lookup"><span data-stu-id="d6722-262">That's it, build it and you're on your way!</span></span>


## <a name="next-steps"></a><span data-ttu-id="d6722-263">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d6722-263">Next steps</span></span>
* <span data-ttu-id="d6722-264">Quer um tutorial mais complexo do ASP.NET MVC?</span><span class="sxs-lookup"><span data-stu-id="d6722-264">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="d6722-265">Confira [Tutorial do ASP.NET MVC: desenvolvimento de aplicativo Web com o Azure Cosmos DB](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="d6722-265">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="d6722-266">Quer executar testes de desempenho e escala com o Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="d6722-266">Want to perform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="d6722-267">Confira [Teste de desempenho e escala com o Azure Cosmos DB](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="d6722-267">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="d6722-268">Saiba como [monitorar solicitações, o uso e o armazenamento do Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="d6722-268">Learn how to [monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="d6722-269">Executar consultas em nosso conjunto de dados de exemplo no [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="d6722-269">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="d6722-270">Para saber mais sobre o Azure Cosmos DB, confira [Bem-vindo ao Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span><span class="sxs-lookup"><span data-stu-id="d6722-270">To learn more about Azure Cosmos DB, see [Welcome to Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
[cosmos-db-create-account]: create-documentdb-dotnet.md#create-account
