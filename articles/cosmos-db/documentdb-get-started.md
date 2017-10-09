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
# <a name="azure-cosmos-db-documentdb-api-getting-started-tutorial"></a><span data-ttu-id="9fa34-104">Azure Cosmos DB: tutorial de introdução da API do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="9fa34-104">Azure Cosmos DB: DocumentDB API getting started tutorial</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9fa34-105">.NET</span><span class="sxs-lookup"><span data-stu-id="9fa34-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="9fa34-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="9fa34-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="9fa34-107">Node.js para MongoDB</span><span class="sxs-lookup"><span data-stu-id="9fa34-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="9fa34-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="9fa34-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="9fa34-109">Java</span><span class="sxs-lookup"><span data-stu-id="9fa34-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="9fa34-110">C++</span><span class="sxs-lookup"><span data-stu-id="9fa34-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="9fa34-111">Bem-vindo toohello API DocumentDB do Azure Cosmos DB tutorial de Introdução!</span><span class="sxs-lookup"><span data-stu-id="9fa34-111">Welcome toohello Azure Cosmos DB DocumentDB API getting started tutorial!</span></span> <span data-ttu-id="9fa34-112">Após seguir este tutorial, você terá um aplicativo de console que cria e consulta recursos do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9fa34-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="9fa34-113">Abordaremos:</span><span class="sxs-lookup"><span data-stu-id="9fa34-113">We'll cover:</span></span>

* <span data-ttu-id="9fa34-114">Criar e conectar-se a conta de banco de dados do Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="9fa34-114">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="9fa34-115">Configurar a sua Solução do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9fa34-115">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="9fa34-116">Criando um banco de dados online</span><span class="sxs-lookup"><span data-stu-id="9fa34-116">Creating an online database</span></span>
* <span data-ttu-id="9fa34-117">Criar uma coleção</span><span class="sxs-lookup"><span data-stu-id="9fa34-117">Creating a collection</span></span>
* <span data-ttu-id="9fa34-118">Criando documentos JSON</span><span class="sxs-lookup"><span data-stu-id="9fa34-118">Creating JSON documents</span></span>
* <span data-ttu-id="9fa34-119">Consultando Olá coleção</span><span class="sxs-lookup"><span data-stu-id="9fa34-119">Querying hello collection</span></span>
* <span data-ttu-id="9fa34-120">Substituição de um documento</span><span class="sxs-lookup"><span data-stu-id="9fa34-120">Replacing a document</span></span>
* <span data-ttu-id="9fa34-121">Exclusão de um documento</span><span class="sxs-lookup"><span data-stu-id="9fa34-121">Deleting a document</span></span>
* <span data-ttu-id="9fa34-122">Excluir banco de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="9fa34-122">Deleting hello database</span></span>

<span data-ttu-id="9fa34-123">Você não tem tempo?</span><span class="sxs-lookup"><span data-stu-id="9fa34-123">Don't have time?</span></span> <span data-ttu-id="9fa34-124">Não se preocupe!</span><span class="sxs-lookup"><span data-stu-id="9fa34-124">Don't worry!</span></span> <span data-ttu-id="9fa34-125">solução completa de saudação está disponível em [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="9fa34-125">hello complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> <span data-ttu-id="9fa34-126">Saltar toohello [obter seção de solução tutorial NoSQL completa Olá](#GetSolution) para instruções rápidas.</span><span class="sxs-lookup"><span data-stu-id="9fa34-126">Jump toohello [Get hello complete NoSQL tutorial solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="9fa34-127">Posteriormente,. use Olá votação botões na parte superior da saudação ou inferior de toogive esta página nos comentários.</span><span class="sxs-lookup"><span data-stu-id="9fa34-127">Afterwards, please use hello voting buttons at hello top or bottom of this page toogive us feedback.</span></span> <span data-ttu-id="9fa34-128">Se você deseja toocontact você diretamente, sinta-se livre tooinclude endereço do seu email em seus comentários.</span><span class="sxs-lookup"><span data-stu-id="9fa34-128">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments.</span></span>

<span data-ttu-id="9fa34-129">Agora vamos começar!</span><span class="sxs-lookup"><span data-stu-id="9fa34-129">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9fa34-130">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9fa34-130">Prerequisites</span></span>
<span data-ttu-id="9fa34-131">Verifique se que você tem o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="9fa34-131">Please make sure you have hello following:</span></span>

* <span data-ttu-id="9fa34-132">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="9fa34-132">An active Azure account.</span></span> <span data-ttu-id="9fa34-133">Se não tiver uma, você poderá se inscrever em uma [conta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="9fa34-133">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="9fa34-134">Como alternativa, você pode usar o hello [emulador de banco de dados do Azure Cosmos](local-emulator.md) para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="9fa34-134">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="9fa34-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="9fa34-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="9fa34-136">Etapa 1: Criar uma conta de banco de dados do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9fa34-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="9fa34-137">Vamos criar uma conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9fa34-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="9fa34-138">Se você já tiver uma conta que você deseja toouse, poderá pular muito[configurar sua solução do Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="9fa34-138">If you already have an account you want toouse, you can skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="9fa34-139">Se você estiver usando hello Azure Cosmos DB emulador, siga as etapas de saudação em [emulador de banco de dados do Azure Cosmos](local-emulator.md) toosetup Olá emulador e pular muito[configurar sua solução do Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="9fa34-139">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="9fa34-140"><a id="SetupVS"></a>Etapa 2: configurar a sua solução do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9fa34-140"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="9fa34-141">Abra o **Visual Studio 2017** em seu computador.</span><span class="sxs-lookup"><span data-stu-id="9fa34-141">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="9fa34-142">Em Olá **arquivo** menu, selecione **novo**e, em seguida, escolha **projeto**.</span><span class="sxs-lookup"><span data-stu-id="9fa34-142">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="9fa34-143">Em Olá **novo projeto** caixa de diálogo, selecione **modelos** / **Visual C#** / **aplicativo de Console**, nome seu projeto e clique **Okey**.</span><span class="sxs-lookup"><span data-stu-id="9fa34-143">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console Application**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="9fa34-144">![Captura de tela da janela do novo projeto de saudação](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="9fa34-144">![Screen shot of hello New Project window](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span></span>
4. <span data-ttu-id="9fa34-145">Em Olá **Solution Explorer**, clique com o botão direito no seu novo aplicativo de console, que está em sua solução do Visual Studio, e, em seguida, clique em **gerenciar pacotes NuGet...**</span><span class="sxs-lookup"><span data-stu-id="9fa34-145">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Captura de tela de saudação à direita Menu clicado para Olá projeto](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="9fa34-147">Em Olá **Nuget** , clique em **procurar**e o tipo **documentdb do azure** na caixa de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="9fa34-147">In hello **Nuget** tab, click **Browse**, and type **azure documentdb** in hello search box.</span></span>
6. <span data-ttu-id="9fa34-148">Nos resultados de saudação localizar **Microsoft.Azure.DocumentDB** e clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="9fa34-148">Within hello results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="9fa34-149">ID do pacote Olá Olá biblioteca de cliente de API do Azure Cosmos DB DocumentDB é [biblioteca de cliente do Microsoft Azure DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span><span class="sxs-lookup"><span data-stu-id="9fa34-149">hello package ID for hello Azure Cosmos DB DocumentDB API Client Library is [Microsoft Azure DocumentDB Client Library](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span></span>
   <span data-ttu-id="9fa34-150">![Captura de tela de saudação Menu do Nuget para localizar o SDK de cliente de banco de dados do Azure Cosmos](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="9fa34-150">![Screen shot of hello Nuget Menu for finding Azure Cosmos DB Client SDK](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="9fa34-151">Se você receber uma mensagem sobre a revisar as alterações toohello solução, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="9fa34-151">If you get a messages about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="9fa34-152">Se receber uma mensagem sobre a aceitação da licença, clique em **Aceito**.</span><span class="sxs-lookup"><span data-stu-id="9fa34-152">If you get a message about license acceptance, click **I accept**.</span></span>

<span data-ttu-id="9fa34-153">Ótimo!</span><span class="sxs-lookup"><span data-stu-id="9fa34-153">Great!</span></span> <span data-ttu-id="9fa34-154">Concluída a instalação Olá, vamos começar a escrever um código.</span><span class="sxs-lookup"><span data-stu-id="9fa34-154">Now that we finished hello setup, let's start writing some code.</span></span> <span data-ttu-id="9fa34-155">Você pode encontrar um projeto de código completo deste tutorial no [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="9fa34-155">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span></span>

## <span data-ttu-id="9fa34-156"><a id="Connect"></a>Etapa 3: Conectar-se a conta de banco de dados do Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="9fa34-156"><a id="Connect"></a>Step 3: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="9fa34-157">Primeiro, adicione estas referências toohello a partir de seu aplicativo c#, no arquivo Program.cs de saudação:</span><span class="sxs-lookup"><span data-stu-id="9fa34-157">First, add these references toohello beginning of your C# application, in hello Program.cs file:</span></span>

    using System;
    using System.Linq;
    using System.Threading.Tasks;

    // ADD THIS PART tooYOUR CODE
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;

> [!IMPORTANT]
> <span data-ttu-id="9fa34-158">Tutorial de saudação do toocomplete ordem, certifique-se de que adicionar dependências de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="9fa34-158">In order toocomplete hello tutorial, make sure you add hello dependencies above.</span></span>
> 
> 

<span data-ttu-id="9fa34-159">Agora, adicione essas duas constantes e sua variável *client* sob sua classe pública *Program*.</span><span class="sxs-lookup"><span data-stu-id="9fa34-159">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

    public class Program
    {
        // ADD THIS PART tooYOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;

<span data-ttu-id="9fa34-160">Em seguida, head fazer toohello [Portal do Azure](https://portal.azure.com) tooretrieve sua URL de ponto de extremidade e a chave primária.</span><span class="sxs-lookup"><span data-stu-id="9fa34-160">Next, head back toohello [Azure Portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="9fa34-161">URL de ponto de extremidade de saudação e a chave primária são necessárias para seu aplicativo toounderstand onde tooconnect e para o banco de dados do Azure Cosmos tootrust conexão do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9fa34-161">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="9fa34-162">Olá Portal do Azure, navegue conta de banco de dados do Azure Cosmos tooyour e, em seguida, clique no **chaves**.</span><span class="sxs-lookup"><span data-stu-id="9fa34-162">In hello Azure Portal, navigate tooyour Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="9fa34-163">Copie Olá URI do portal hello e cole-o na `<your endpoint URL>` no arquivo program.cs de saudação.</span><span class="sxs-lookup"><span data-stu-id="9fa34-163">Copy hello URI from hello portal and paste it into `<your endpoint URL>` in hello program.cs file.</span></span> <span data-ttu-id="9fa34-164">Cópia Olá chave primária do portal hello e cole-o na `<your primary key>`.</span><span class="sxs-lookup"><span data-stu-id="9fa34-164">Then copy hello PRIMARY KEY from hello portal and paste it into `<your primary key>`.</span></span>

![Captura de tela de saudação Portal do Azure usado pelo Olá NoSQL tutorial toocreate um aplicativo de console c#.][keys]

<span data-ttu-id="9fa34-167">Em seguida, vamos começar aplicativo hello, criando uma nova instância da saudação **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="9fa34-167">Next, we'll start hello application by creating a new instance of hello **DocumentClient**.</span></span>

<span data-ttu-id="9fa34-168">Abaixo Olá **principal** método, adicione essa nova tarefa assíncrona chamada **GetStartedDemo**, qual instanciará nosso novo **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="9fa34-168">Below hello **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

    static void Main(string[] args)
    {
    }

    // ADD THIS PART tooYOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);
    }

<span data-ttu-id="9fa34-169">Adicione o código a seguir Olá toorun sua tarefa assíncrona de seu **principal** método.</span><span class="sxs-lookup"><span data-stu-id="9fa34-169">Add hello following code toorun your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="9fa34-170">Olá **principal** método capturar exceções e os grava toohello console.</span><span class="sxs-lookup"><span data-stu-id="9fa34-170">hello **Main** method will catch exceptions and write them toohello console.</span></span>

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

<span data-ttu-id="9fa34-171">Pressione **F5** toorun seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9fa34-171">Press **F5** toorun your application.</span></span> <span data-ttu-id="9fa34-172">saída da janela de console Olá exibe a mensagem de saudação `End of demo, press any key tooexit.` confirmando que a conexão de saudação foi feita.</span><span class="sxs-lookup"><span data-stu-id="9fa34-172">hello console window output displays hello message `End of demo, press any key tooexit.` confirming that hello connection was made.</span></span>  <span data-ttu-id="9fa34-173">Você pode então fechar a janela do console hello.</span><span class="sxs-lookup"><span data-stu-id="9fa34-173">You can then close hello console window.</span></span> 

<span data-ttu-id="9fa34-174">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="9fa34-174">Congratulations!</span></span> <span data-ttu-id="9fa34-175">Você se conectou com êxito a conta de banco de dados do Azure Cosmos tooan, agora, vamos examinar trabalhando com recursos de banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="9fa34-175">You have successfully connected tooan Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="9fa34-176">Etapa 4: criar um banco de dados</span><span class="sxs-lookup"><span data-stu-id="9fa34-176">Step 4: Create a database</span></span>
<span data-ttu-id="9fa34-177">Antes de adicionar o código de saudação para a criação de um banco de dados, adicione um método auxiliar para gravar toohello console.</span><span class="sxs-lookup"><span data-stu-id="9fa34-177">Before you add hello code for creating a database, add a helper method for writing toohello console.</span></span>

<span data-ttu-id="9fa34-178">Copie e cole Olá **WriteToConsoleAndPromptToContinue** método após Olá **GetStartedDemo** método.</span><span class="sxs-lookup"><span data-stu-id="9fa34-178">Copy and paste hello **WriteToConsoleAndPromptToContinue** method after hello **GetStartedDemo** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key toocontinue ...");
            Console.ReadKey();
    }

<span data-ttu-id="9fa34-179">O banco de dados do Azure Cosmos [banco de dados](documentdb-resources.md#databases) podem ser criados usando Olá [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) método hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="9fa34-179">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using hello [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="9fa34-180">Um banco de dados é um contêiner lógico de saudação do armazenamento de documentos JSON particionado em coleções.</span><span class="sxs-lookup"><span data-stu-id="9fa34-180">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="9fa34-181">Copiar e colar a seguir Olá código tooyour **GetStartedDemo** método após a criação de saudação do cliente.</span><span class="sxs-lookup"><span data-stu-id="9fa34-181">Copy and paste hello following code tooyour **GetStartedDemo** method after hello client creation.</span></span> <span data-ttu-id="9fa34-182">Isso criará um banco de dados denominado *FamilyDB*.</span><span class="sxs-lookup"><span data-stu-id="9fa34-182">This will create a database named *FamilyDB*.</span></span>

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        // ADD THIS PART tooYOUR CODE
        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

<span data-ttu-id="9fa34-183">Pressione **F5** toorun seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9fa34-183">Press **F5** toorun your application.</span></span>

<span data-ttu-id="9fa34-184">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="9fa34-184">Congratulations!</span></span> <span data-ttu-id="9fa34-185">Você criou um banco de dados do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="9fa34-185">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="9fa34-186"><a id="CreateColl"></a>Etapa 5: Criar uma coleção</span><span class="sxs-lookup"><span data-stu-id="9fa34-186"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="9fa34-187">**CreateDocumentCollectionIfNotExistsAsync** criará uma nova coleção com taxa de transferência reservada, com implicações de preço.</span><span class="sxs-lookup"><span data-stu-id="9fa34-187">**CreateDocumentCollectionIfNotExistsAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="9fa34-188">Para obter mais detalhes, visite a nossa [página de preços](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="9fa34-188">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="9fa34-189">Um [coleção](documentdb-resources.md#collections) podem ser criados usando Olá [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) método hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="9fa34-189">A [collection](documentdb-resources.md#collections) can be created by using hello [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="9fa34-190">Uma coleção é um contêiner de documentos JSON e uma lógica de aplicativo JavaScript associada.</span><span class="sxs-lookup"><span data-stu-id="9fa34-190">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="9fa34-191">Copiar e colar a seguir Olá código tooyour **GetStartedDemo** método após a criação do banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="9fa34-191">Copy and paste hello following code tooyour **GetStartedDemo** method after hello database creation.</span></span> <span data-ttu-id="9fa34-192">Essa ação criará uma coleção de documentos denominada *FamilyCollection*.</span><span class="sxs-lookup"><span data-stu-id="9fa34-192">This will create a document collection named *FamilyCollection*.</span></span>

        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

        // ADD THIS PART tooYOUR CODE
         await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });

<span data-ttu-id="9fa34-193">Pressione **F5** toorun seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9fa34-193">Press **F5** toorun your application.</span></span>

<span data-ttu-id="9fa34-194">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="9fa34-194">Congratulations!</span></span> <span data-ttu-id="9fa34-195">Você criou uma coleção de documentos do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="9fa34-195">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="9fa34-196"><a id="CreateDoc"></a>Etapa 6: Criar documentos JSON</span><span class="sxs-lookup"><span data-stu-id="9fa34-196"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="9fa34-197">Um [documento](documentdb-resources.md#documents) podem ser criados usando Olá [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) método hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="9fa34-197">A [document](documentdb-resources.md#documents) can be created by using hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="9fa34-198">Os documentos são conteúdo JSON (arbitrário) definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="9fa34-198">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="9fa34-199">Agora podemos inserir um ou mais documentos.</span><span class="sxs-lookup"><span data-stu-id="9fa34-199">We can now insert one or more documents.</span></span> <span data-ttu-id="9fa34-200">Se você já tiver dados você gostaria que toostore no banco de dados, você pode usar o hello Azure Cosmos DB [ferramenta de migração de dados](import-data.md) tooimport dados de saudação em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="9fa34-200">If you already have data you'd like toostore in your database, you can use hello Azure Cosmos DB [Data Migration tool](import-data.md) tooimport hello data into a database.</span></span>

<span data-ttu-id="9fa34-201">Primeiro, precisamos toocreate um **família** classe que representa os objetos armazenados no banco de dados do Azure Cosmos neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="9fa34-201">First, we need toocreate a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="9fa34-202">Também criaremos as subclasses **Parent**, **Child**, **Pet** e **Address** que são usadas em **Family**.</span><span class="sxs-lookup"><span data-stu-id="9fa34-202">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="9fa34-203">Observe que os documentos devem ter uma propriedade **Id** serializada como **id** em JSON.</span><span class="sxs-lookup"><span data-stu-id="9fa34-203">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="9fa34-204">Criar essas classes adicionando Olá classes sub internas a seguir após Olá **GetStartedDemo** método.</span><span class="sxs-lookup"><span data-stu-id="9fa34-204">Create these classes by adding hello following internal sub-classes after hello **GetStartedDemo** method.</span></span>

<span data-ttu-id="9fa34-205">Copie e cole Olá **família**, **pai**, **filho**, **animal de estimação**, e **endereço** classes após Olá **WriteToConsoleAndPromptToContinue** método.</span><span class="sxs-lookup"><span data-stu-id="9fa34-205">Copy and paste hello **Family**, **Parent**, **Child**, **Pet**, and **Address** classes after hello **WriteToConsoleAndPromptToContinue** method.</span></span>

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

<span data-ttu-id="9fa34-206">Copie e cole Olá **CreateFamilyDocumentIfNotExists** método sob sua **endereço** classe.</span><span class="sxs-lookup"><span data-stu-id="9fa34-206">Copy and paste hello **CreateFamilyDocumentIfNotExists** method underneath your **Address** class.</span></span>

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

<span data-ttu-id="9fa34-207">E inserir dois documentos, um para Olá Andersen família e hello Wakefield família.</span><span class="sxs-lookup"><span data-stu-id="9fa34-207">And insert two documents, one each for hello Andersen Family and hello Wakefield Family.</span></span>

<span data-ttu-id="9fa34-208">Copiar e colar a seguir Olá código tooyour **GetStartedDemo** método após a criação de coleção do documento hello.</span><span class="sxs-lookup"><span data-stu-id="9fa34-208">Copy and paste hello following code tooyour **GetStartedDemo** method after hello document collection creation.</span></span>

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

<span data-ttu-id="9fa34-209">Pressione **F5** toorun seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9fa34-209">Press **F5** toorun your application.</span></span>

<span data-ttu-id="9fa34-210">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="9fa34-210">Congratulations!</span></span> <span data-ttu-id="9fa34-211">Você criou dois documentos do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="9fa34-211">You have successfully created two Azure Cosmos DB documents.</span></span>  

![Diagrama ilustrando uma relação hierárquica Olá entre conta hello, banco de dados online hello, coleção hello e documentos Olá usados pelo Olá NoSQL tutorial toocreate um aplicativo de console c#](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="9fa34-213"><a id="Query"></a>Etapa 7: Consultar recursos do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9fa34-213"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="9fa34-214">O Azure Cosmos DB tem suporte para [consultas](documentdb-sql-query.md) avançadas de documentos JSON armazenados em cada coleção.</span><span class="sxs-lookup"><span data-stu-id="9fa34-214">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="9fa34-215">Olá, código de exemplo seguinte mostra várias consultas - usando ambos os SQL de banco de dados do Azure Cosmos sintaxe, bem como LINQ - que podem ser executados em relação a Olá documentos que são inseridos na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="9fa34-215">hello following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against hello documents we inserted in hello previous step.</span></span>

<span data-ttu-id="9fa34-216">Copie e cole Olá **ExecuteSimpleQuery** método após o **CreateFamilyDocumentIfNotExists** método.</span><span class="sxs-lookup"><span data-stu-id="9fa34-216">Copy and paste hello **ExecuteSimpleQuery** method after your **CreateFamilyDocumentIfNotExists** method.</span></span>

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

<span data-ttu-id="9fa34-217">Copiar e colar a seguir Olá código tooyour **GetStartedDemo** método após a criação de documento segundo hello.</span><span class="sxs-lookup"><span data-stu-id="9fa34-217">Copy and paste hello following code tooyour **GetStartedDemo** method after hello second document creation.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    // ADD THIS PART tooYOUR CODE
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="9fa34-218">Pressione **F5** toorun seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9fa34-218">Press **F5** toorun your application.</span></span>

<span data-ttu-id="9fa34-219">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="9fa34-219">Congratulations!</span></span> <span data-ttu-id="9fa34-220">Você consultou uma coleção do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="9fa34-220">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="9fa34-221">Olá diagrama a seguir ilustra como consultas de banco de dados SQL do Azure Cosmos Olá sintaxe é chamada na coleção de saudação que você criou e hello mesma lógica se aplica também a consulta LINQ em toohello.</span><span class="sxs-lookup"><span data-stu-id="9fa34-221">hello following diagram illustrates how hello Azure Cosmos DB SQL query syntax is called against hello collection you created, and hello same logic applies toohello LINQ query as well.</span></span>

![Diagrama ilustrando escopo hello e o significado da consulta Olá usado pelo Olá NoSQL tutorial toocreate um aplicativo de console c#](./media/documentdb-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="9fa34-223">Olá [FROM](documentdb-sql-query.md#FromClause) palavra-chave é opcional em consulta Olá porque as consultas de banco de dados do Azure Cosmos já estão no escopo tooa única coleção.</span><span class="sxs-lookup"><span data-stu-id="9fa34-223">hello [FROM](documentdb-sql-query.md#FromClause) keyword is optional in hello query because Azure Cosmos DB queries are already scoped tooa single collection.</span></span> <span data-ttu-id="9fa34-224">Portanto, "FROM Families f" pode ser trocado por "FROM root r" ou qualquer outra variável de nome que você escolher.</span><span class="sxs-lookup"><span data-stu-id="9fa34-224">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="9fa34-225">Banco de dados do Azure Cosmos deduzirá que famílias, raiz ou o nome da variável Olá você escolheu, coleção atual de saudação de referência por padrão.</span><span class="sxs-lookup"><span data-stu-id="9fa34-225">Azure Cosmos DB will infer that Families, root, or hello variable name you chose, reference hello current collection by default.</span></span>

## <span data-ttu-id="9fa34-226"><a id="ReplaceDocument"></a>Etapa 8: substituir o documento JSON</span><span class="sxs-lookup"><span data-stu-id="9fa34-226"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="9fa34-227">O Azure Cosmos DB dá suporte à substituição de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="9fa34-227">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="9fa34-228">Copie e cole Olá **ReplaceFamilyDocument** método após o **ExecuteSimpleQuery** método.</span><span class="sxs-lookup"><span data-stu-id="9fa34-228">Copy and paste hello **ReplaceFamilyDocument** method after your **ExecuteSimpleQuery** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
    {
         await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
         this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }

<span data-ttu-id="9fa34-229">Copiar e colar a seguir Olá código tooyour **GetStartedDemo** método após a execução de consulta hello, no final de saudação do método hello.</span><span class="sxs-lookup"><span data-stu-id="9fa34-229">Copy and paste hello following code tooyour **GetStartedDemo** method after hello query execution, at hello end of hello method.</span></span> <span data-ttu-id="9fa34-230">Depois de substituir o documento hello, isso será executado Olá mesmo novamente consultar tooview Olá alterado documento.</span><span class="sxs-lookup"><span data-stu-id="9fa34-230">After replacing hello document, this will run hello same query again tooview hello changed document.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    // ADD THIS PART tooYOUR CODE
    // Update hello Grade of hello Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="9fa34-231">Pressione **F5** toorun seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9fa34-231">Press **F5** toorun your application.</span></span>

<span data-ttu-id="9fa34-232">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="9fa34-232">Congratulations!</span></span> <span data-ttu-id="9fa34-233">Você substituiu um documento do Azure Cosmos DB com sucesso.</span><span class="sxs-lookup"><span data-stu-id="9fa34-233">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="9fa34-234"><a id="DeleteDocument"></a>Etapa 9: excluir o documento JSON</span><span class="sxs-lookup"><span data-stu-id="9fa34-234"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="9fa34-235">O Azure Cosmos DB dá suporte à exclusão de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="9fa34-235">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="9fa34-236">Copie e cole Olá **DeleteFamilyDocument** método após o **ReplaceFamilyDocument** método.</span><span class="sxs-lookup"><span data-stu-id="9fa34-236">Copy and paste hello **DeleteFamilyDocument** method after your **ReplaceFamilyDocument** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
    {
         await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
         Console.WriteLine("Deleted Family {0}", documentName);
    }

<span data-ttu-id="9fa34-237">Copiar e colar a seguir Olá código tooyour **GetStartedDemo** método após a execução da consulta de saudação segundo, no final de saudação do método hello.</span><span class="sxs-lookup"><span data-stu-id="9fa34-237">Copy and paste hello following code tooyour **GetStartedDemo** method after hello second query execution, at hello end of hello method.</span></span>

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);
    
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");
    
    // ADD THIS PART tooCODE
    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

<span data-ttu-id="9fa34-238">Pressione **F5** toorun seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9fa34-238">Press **F5** toorun your application.</span></span>

<span data-ttu-id="9fa34-239">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="9fa34-239">Congratulations!</span></span> <span data-ttu-id="9fa34-240">Você excluiu um documento do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="9fa34-240">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="9fa34-241"><a id="DeleteDatabase"></a>Etapa 10: Excluir o banco de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="9fa34-241"><a id="DeleteDatabase"></a>Step 10: Delete hello database</span></span>
<span data-ttu-id="9fa34-242">Excluindo Olá criado o banco de dados removerá o banco de dados de saudação e todos os recursos de filhos (coleções, documentos, etc.).</span><span class="sxs-lookup"><span data-stu-id="9fa34-242">Deleting hello created database will remove hello database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="9fa34-243">Copiar e colar a seguir Olá código tooyour **GetStartedDemo** método após documento hello excluir banco de dados inteiro toodelete hello e todos os recursos de filhos.</span><span class="sxs-lookup"><span data-stu-id="9fa34-243">Copy and paste hello following code tooyour **GetStartedDemo** method after hello document delete toodelete hello entire database and all children resources.</span></span>

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

    // ADD THIS PART tooCODE
    // Clean up/delete hello database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB"));

<span data-ttu-id="9fa34-244">Pressione **F5** toorun seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9fa34-244">Press **F5** toorun your application.</span></span>

<span data-ttu-id="9fa34-245">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="9fa34-245">Congratulations!</span></span> <span data-ttu-id="9fa34-246">Você excluiu um banco de dados do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="9fa34-246">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="9fa34-247"><a id="Run"></a>Etapa 11: executar o aplicativo de console C# inteiro!</span><span class="sxs-lookup"><span data-stu-id="9fa34-247"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="9fa34-248">Pressione F5 no aplicativo do Visual Studio toobuild hello no modo de depuração.</span><span class="sxs-lookup"><span data-stu-id="9fa34-248">Hit F5 in Visual Studio toobuild hello application in debug mode.</span></span>

<span data-ttu-id="9fa34-249">Você deve ver a saída de saudação do aplicativo iniciado get em uma janela de console.</span><span class="sxs-lookup"><span data-stu-id="9fa34-249">You should see hello output of your get started app in a console window.</span></span> <span data-ttu-id="9fa34-250">saída de Hello mostrará os resultados de saudação do hello consultas adicionamos e deve coincidir com o texto de exemplo hello abaixo.</span><span class="sxs-lookup"><span data-stu-id="9fa34-250">hello output will show hello results of hello queries we added and should match hello example text below.</span></span>

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

<span data-ttu-id="9fa34-251">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="9fa34-251">Congratulations!</span></span> <span data-ttu-id="9fa34-252">Você concluiu o tutorial hello e ter um aplicativo de console funcional c#!</span><span class="sxs-lookup"><span data-stu-id="9fa34-252">You've completed hello tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="9fa34-253"><a id="GetSolution"></a>Obter a solução completa de tutorial Olá</span><span class="sxs-lookup"><span data-stu-id="9fa34-253"><a id="GetSolution"></a> Get hello complete tutorial solution</span></span>
<span data-ttu-id="9fa34-254">Se você não tem tempo Olá toocomplete as etapas neste tutorial, ou apenas deseja toodownload Olá exemplos de código, você poderá obtê-lo de [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="9fa34-254">If you didn't have time toocomplete hello steps in this tutorial, or just want toodownload hello code samples, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> 

<span data-ttu-id="9fa34-255">toobuild solução de GetStarted hello, você precisará seguir hello:</span><span class="sxs-lookup"><span data-stu-id="9fa34-255">toobuild hello GetStarted solution, you will need hello following:</span></span>

* <span data-ttu-id="9fa34-256">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="9fa34-256">An active Azure account.</span></span> <span data-ttu-id="9fa34-257">Se não tiver uma, você poderá se inscrever em uma [conta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="9fa34-257">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="9fa34-258">Uma [conta do Azure Cosmos DB][cosmos-db-create-account].</span><span class="sxs-lookup"><span data-stu-id="9fa34-258">An [Azure Cosmos DB account][cosmos-db-create-account].</span></span>
* <span data-ttu-id="9fa34-259">Olá [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) solução disponível no GitHub.</span><span class="sxs-lookup"><span data-stu-id="9fa34-259">hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="9fa34-260">toorestore Olá referências toohello SDK .NET do Azure Cosmos banco de dados no Visual Studio, clique com botão direito Olá **GetStarted** solução no Gerenciador de soluções e clique **habilite a restauração do pacote de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="9fa34-260">toorestore hello references toohello Azure Cosmos DB .NET SDK in Visual Studio, right-click hello **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="9fa34-261">Em seguida, no arquivo App. config de hello, atualizar Olá EndpointUrl e AuthorizationKey valores conforme descrito em [conectar-se a conta de banco de dados do Azure Cosmos tooan](#Connect).</span><span class="sxs-lookup"><span data-stu-id="9fa34-261">Next, in hello App.config file, update hello EndpointUrl and AuthorizationKey values as described in [Connect tooan Azure Cosmos DB account](#Connect).</span></span>

<span data-ttu-id="9fa34-262">Pronto, compile-o e você pode continuar!</span><span class="sxs-lookup"><span data-stu-id="9fa34-262">That's it, build it and you're on your way!</span></span>


## <a name="next-steps"></a><span data-ttu-id="9fa34-263">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9fa34-263">Next steps</span></span>
* <span data-ttu-id="9fa34-264">Quer um tutorial mais complexo do ASP.NET MVC?</span><span class="sxs-lookup"><span data-stu-id="9fa34-264">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="9fa34-265">Confira [Tutorial do ASP.NET MVC: desenvolvimento de aplicativo Web com o Azure Cosmos DB](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="9fa34-265">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="9fa34-266">Deseja tooperform escala e testes de desempenho com o banco de dados do Azure Cosmos?</span><span class="sxs-lookup"><span data-stu-id="9fa34-266">Want tooperform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="9fa34-267">Confira [Teste de desempenho e escala com o Azure Cosmos DB](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="9fa34-267">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="9fa34-268">Saiba como muito[monitorar solicitações, uso e armazenamento do banco de dados do Azure Cosmos](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="9fa34-268">Learn how too[monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="9fa34-269">Executar consultas em nosso conjunto de dados de exemplo hello [parque de consulta](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="9fa34-269">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="9fa34-270">toolearn mais sobre Azure Cosmos DB, consulte [tooAzure Cosmos DB de boas-vindas](https://docs.microsoft.com/azure/cosmos-db/introduction).</span><span class="sxs-lookup"><span data-stu-id="9fa34-270">toolearn more about Azure Cosmos DB, see [Welcome tooAzure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
[cosmos-db-create-account]: create-documentdb-dotnet.md#create-account
