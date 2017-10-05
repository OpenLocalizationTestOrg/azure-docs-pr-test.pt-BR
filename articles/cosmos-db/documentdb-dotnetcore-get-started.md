---
title: "Azure Cosmos DB: tutorial de introdução à API do DocumentDB em .NET Core | Microsoft Docs"
description: Um tutorial que cria um banco de dados online e um aplicativo de console C# usando o SDK do .NET Core da API do DocumentDB do Azure Cosmos DB.
services: cosmos-db
documentationcenter: .net
author: arramac
manager: jhubbard
editor: 
ms.assetid: 9f93e276-9936-4efb-a534-a9889fa7c7d2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 7536978bbb1e41b6484b66fd1b51c900fc3e545d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-getting-started-with-the-documentdb-api-and-net-core"></a><span data-ttu-id="59a57-103">Azure Cosmos DB: Introdução à API do DocumentDB e ao .NET Core</span><span class="sxs-lookup"><span data-stu-id="59a57-103">Azure Cosmos DB: Getting started with the DocumentDB API and .NET Core</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="59a57-104">.NET</span><span class="sxs-lookup"><span data-stu-id="59a57-104">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="59a57-105">.NET Core</span><span class="sxs-lookup"><span data-stu-id="59a57-105">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="59a57-106">Node.js para MongoDB</span><span class="sxs-lookup"><span data-stu-id="59a57-106">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="59a57-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="59a57-107">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="59a57-108">Java</span><span class="sxs-lookup"><span data-stu-id="59a57-108">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="59a57-109">C++</span><span class="sxs-lookup"><span data-stu-id="59a57-109">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="59a57-110">Bem-vindo ao tutorial de introdução à API do DocumentDB para Azure Cosmos DB com .NET Core!</span><span class="sxs-lookup"><span data-stu-id="59a57-110">Welcome to the DocumentDB API for Azure Cosmos DB getting started with .NET Core tutorial!</span></span> <span data-ttu-id="59a57-111">Após seguir este tutorial, você terá um aplicativo de console que cria e consulta recursos do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="59a57-111">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="59a57-112">Abordaremos:</span><span class="sxs-lookup"><span data-stu-id="59a57-112">We'll cover:</span></span>

* <span data-ttu-id="59a57-113">Criar e conectar-se a uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="59a57-113">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="59a57-114">Configurar a sua Solução do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="59a57-114">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="59a57-115">Criando um banco de dados online</span><span class="sxs-lookup"><span data-stu-id="59a57-115">Creating an online database</span></span>
* <span data-ttu-id="59a57-116">Criar uma coleção</span><span class="sxs-lookup"><span data-stu-id="59a57-116">Creating a collection</span></span>
* <span data-ttu-id="59a57-117">Criando documentos JSON</span><span class="sxs-lookup"><span data-stu-id="59a57-117">Creating JSON documents</span></span>
* <span data-ttu-id="59a57-118">Consultar a coleção</span><span class="sxs-lookup"><span data-stu-id="59a57-118">Querying the collection</span></span>
* <span data-ttu-id="59a57-119">Substituição de um documento</span><span class="sxs-lookup"><span data-stu-id="59a57-119">Replacing a document</span></span>
* <span data-ttu-id="59a57-120">Exclusão de um documento</span><span class="sxs-lookup"><span data-stu-id="59a57-120">Deleting a document</span></span>
* <span data-ttu-id="59a57-121">Excluir o banco de dados</span><span class="sxs-lookup"><span data-stu-id="59a57-121">Deleting the database</span></span>

<span data-ttu-id="59a57-122">Você não tem tempo?</span><span class="sxs-lookup"><span data-stu-id="59a57-122">Don't have time?</span></span> <span data-ttu-id="59a57-123">Não se preocupe!</span><span class="sxs-lookup"><span data-stu-id="59a57-123">Don't worry!</span></span> <span data-ttu-id="59a57-124">A solução completa está disponível em [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span><span class="sxs-lookup"><span data-stu-id="59a57-124">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span> <span data-ttu-id="59a57-125">Vá para a [seção Obter a solução completa](#GetSolution) a fim de ver as instruções rápidas.</span><span class="sxs-lookup"><span data-stu-id="59a57-125">Jump to the [Get the complete solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="59a57-126">Deseja criar um aplicativo Xamarin iOS, Android ou Forms usando o SDK do .NET Core e a API do DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="59a57-126">Want to build a Xamarin iOS, Android, or Forms application using the DocumentDB API and .NET Core SDK?</span></span> <span data-ttu-id="59a57-127">Confira [Criar aplicativos móveis com o Xamarin e o Azure Cosmos DB](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="59a57-127">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>

> [!NOTE]
> <span data-ttu-id="59a57-128">O SDK do .NET Core do Azure Cosmos DB usado neste tutorial ainda não é compatível com aplicativos da UWP (Plataforma Universal do Windows).</span><span class="sxs-lookup"><span data-stu-id="59a57-128">The Azure Cosmos DB .NET Core SDK used in this tutorial is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="59a57-129">Para obter uma versão de visualização do SDK do .NET Core que dê suporte a aplicativos UWP, envie um email para [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="59a57-129">For a preview version of the .NET Core SDK that does support UWP apps, send email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

<span data-ttu-id="59a57-130">Agora vamos começar!</span><span class="sxs-lookup"><span data-stu-id="59a57-130">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59a57-131">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="59a57-131">Prerequisites</span></span>
<span data-ttu-id="59a57-132">Certifique-se que você tem o seguinte:</span><span class="sxs-lookup"><span data-stu-id="59a57-132">Please make sure you have the following:</span></span>

* <span data-ttu-id="59a57-133">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="59a57-133">An active Azure account.</span></span> <span data-ttu-id="59a57-134">Se não tiver uma, você poderá se inscrever em uma [conta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="59a57-134">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="59a57-135">Como alternativa, você pode usar o [Emulador do Azure Cosmos DB](local-emulator.md) neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="59a57-135">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="59a57-136">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="59a57-136">Visual Studio 2017</span></span>](https://www.visualstudio.com/vs/) 
    * <span data-ttu-id="59a57-137">Se estiver trabalhando no MacOS ou Linux, você poderá desenvolver aplicativos .NET Core na linha de comando instalando o [SDK .NET Core](https://www.microsoft.com/net/core#macos) para a plataforma de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="59a57-137">If you're working on MacOS or Linux, you can develop .NET Core apps from the command-line by installing the [.NET Core SDK](https://www.microsoft.com/net/core#macos) for the platform of your choice.</span></span> 
    * <span data-ttu-id="59a57-138">Se estiver trabalhando no Windows, você poderá desenvolver aplicativos .NET Core na linha de comando instalando o [SDK .NET Core](https://www.microsoft.com/net/core#windows).</span><span class="sxs-lookup"><span data-stu-id="59a57-138">If you're working on Windows, you can develop .NET Core apps from the command-line by installing the [.NET Core SDK](https://www.microsoft.com/net/core#windows).</span></span> 
    * <span data-ttu-id="59a57-139">Você pode usar seu próprio editor ou baixar o [Visual Studio Code](https://code.visualstudio.com/), que é gratuito e funciona no Windows, Linux e MacOS.</span><span class="sxs-lookup"><span data-stu-id="59a57-139">You can use your own editor, or download [Visual Studio Code](https://code.visualstudio.com/) which is free and works on Windows, Linux, and MacOS.</span></span> 

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="59a57-140">Etapa 1: Criar uma conta de banco de dados do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="59a57-140">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="59a57-141">Vamos criar uma conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="59a57-141">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="59a57-142">Se você já tem uma conta que deseja usar, você pode pular para [Configurar sua solução do Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="59a57-142">If you already have an account you want to use, you can skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="59a57-143">Se estiver usando o Emulador do Azure Cosmos DB, execute as etapas em [Emulador do Azure Cosmos DB](local-emulator.md) para configurar o emulador e pule para [Configurar sua solução do Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="59a57-143">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="59a57-144"><a id="SetupVS"></a>Etapa 2: configurar a sua solução do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="59a57-144"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="59a57-145">Abra o **Visual Studio 2017** em seu computador.</span><span class="sxs-lookup"><span data-stu-id="59a57-145">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="59a57-146">No menu **Arquivo**, selecione **Novo** e depois **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="59a57-146">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="59a57-147">Na caixa de diálogo **Novo Projeto**, selecione **Modelos** / **Visual C#** / **.NET Core**/**Aplicativo de Console (.NET Core)**, nomeie o projeto **DocumentDBGettingStarted** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="59a57-147">In the **New Project** dialog, select **Templates** / **Visual C#** / **.NET Core**/**Console Application (.NET Core)**, name your project **DocumentDBGettingStarted**, and then click **OK**.</span></span>

   ![Captura de tela da janela Novo Projeto](./media/documentdb-dotnetcore-get-started/nosql-tutorial-new-project-2.png)
4. <span data-ttu-id="59a57-149">No **Gerenciador de Solução**, clique com o botão direito em **DocumentDBGettingStarted**.</span><span class="sxs-lookup"><span data-stu-id="59a57-149">In the **Solution Explorer**, right click on **DocumentDBGettingStarted**.</span></span>
5. <span data-ttu-id="59a57-150">Sem sair do menu, clique em **Gerenciar Pacotes NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="59a57-150">Then without leaving the menu, click on **Manage NuGet Packages...**.</span></span>

   ![Captura de tela do menu exibido pelo clique com o botão direito do mouse para o projeto](./media/documentdb-dotnetcore-get-started/nosql-tutorial-manage-nuget-pacakges.png)
6. <span data-ttu-id="59a57-152">Na guia **Nuget**, clique em **Procurar** na parte superior da janela e digite **azure documentdb** na caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="59a57-152">In the **NuGet** tab, click **Browse** at the top of the window, and type **azure documentdb** in the search box.</span></span>
7. <span data-ttu-id="59a57-153">Nos resultados, encontre **Microsoft.Azure.DocumentDB.Core** e clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="59a57-153">Within the results, find **Microsoft.Azure.DocumentDB.Core** and click **Install**.</span></span>
   <span data-ttu-id="59a57-154">A ID do pacote para a Biblioteca de Cliente do DocumentDB para .NET Core é [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span><span class="sxs-lookup"><span data-stu-id="59a57-154">The package ID for the DocumentDB Client Library for .NET Core is [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span></span> <span data-ttu-id="59a57-155">Se você estiver visando uma versão do .NET Framework (como net461) que não tem suporte deste pacote do NuGet do .NET Core, use [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB), que dá suporte a todas as versões do .NET Framework, a partir do .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="59a57-155">If you are targeting a .NET Framework version (like net461) that is not supported by this .NET Core NuGet package, then use [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) that supports all .NET Framework versions starting .NET Framework 4.5.</span></span>
8. <span data-ttu-id="59a57-156">Nos prompts, aceite as instalações de pacote do NuGet e o contrato de licença.</span><span class="sxs-lookup"><span data-stu-id="59a57-156">At the prompts, accept the NuGet package installations and the license agreement.</span></span>

<span data-ttu-id="59a57-157">Ótimo!</span><span class="sxs-lookup"><span data-stu-id="59a57-157">Great!</span></span> <span data-ttu-id="59a57-158">Agora que a instalação está concluída, vamos começar a escrever algum código.</span><span class="sxs-lookup"><span data-stu-id="59a57-158">Now that we finished the setup, let's start writing some code.</span></span> <span data-ttu-id="59a57-159">Você pode encontrar um projeto de código completo deste tutorial no [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span><span class="sxs-lookup"><span data-stu-id="59a57-159">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span>

## <span data-ttu-id="59a57-160"><a id="Connect"></a>Etapa 3: Conectar-se a uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="59a57-160"><a id="Connect"></a>Step 3: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="59a57-161">Primeiro, adicione essas referências para o início de seu aplicativo C#, no arquivo Program.cs:</span><span class="sxs-lookup"><span data-stu-id="59a57-161">First, add these references to the beginning of your C# application, in the Program.cs file:</span></span>

```csharp
using System;

// ADD THIS PART TO YOUR CODE
using System.Linq;
using System.Threading.Tasks;
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

> [!IMPORTANT]
> <span data-ttu-id="59a57-162">Para concluir este tutorial, adicione as dependências acima.</span><span class="sxs-lookup"><span data-stu-id="59a57-162">In order to complete this tutorial, make sure you add the dependencies above.</span></span>

<span data-ttu-id="59a57-163">Agora, adicione essas duas constantes e sua variável *client* sob sua classe pública *Program*.</span><span class="sxs-lookup"><span data-stu-id="59a57-163">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

```csharp
class Program
{
    // ADD THIS PART TO YOUR CODE
    private const string EndpointUri = "<your endpoint URI>";
    private const string PrimaryKey = "<your key>";
    private DocumentClient client;
```

<span data-ttu-id="59a57-164">Em seguida, vá para o [Portal do Azure](https://portal.azure.com) para recuperar o URI e a chave primária.</span><span class="sxs-lookup"><span data-stu-id="59a57-164">Next, head to the [Azure Portal](https://portal.azure.com) to retrieve your URI and primary key.</span></span> <span data-ttu-id="59a57-165">O URI e a chave primária do Azure Cosmos DB são necessários para que seu aplicativo reconheça onde deve se conectar e para que o Azure Cosmos DB confie na conexão do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="59a57-165">The Azure Cosmos DB URI and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="59a57-166">No Portal do Azure, navegue até sua conta do Azure Cosmos DB e clique em **Chaves**.</span><span class="sxs-lookup"><span data-stu-id="59a57-166">In the Azure Portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="59a57-167">Copie o URI do portal e cole-o em `<your endpoint URI>` no arquivo program.cs.</span><span class="sxs-lookup"><span data-stu-id="59a57-167">Copy the URI from the portal and paste it into `<your endpoint URI>` in the program.cs file.</span></span> <span data-ttu-id="59a57-168">Em seguida, copie a CHAVE PRIMÁRIA do portal e cole-a em `<your key>`.</span><span class="sxs-lookup"><span data-stu-id="59a57-168">Then copy the PRIMARY KEY from the portal and paste it into `<your key>`.</span></span> <span data-ttu-id="59a57-169">Se estiver usando o Emulador do Azure Cosmos DB, use `https://localhost:8081` como o ponto de extremidade e a chave de autorização bem definida de [Como desenvolver usando o Emulador do Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="59a57-169">If you are using the Azure Cosmos DB Emulator, use `https://localhost:8081` as the endpoint, and the well-defined authorization key from [How to develop using the Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="59a57-170">Lembre-se de remover o < e > , mas deixe as aspas duplas ao redor do ponto de extremidade e da chave.</span><span class="sxs-lookup"><span data-stu-id="59a57-170">Make sure to remove the < and > but leave the double quotes around your endpoint and key.</span></span>

![Captura de tela do Portal do Azure usado pelo tutorial do NoSQL para criar um aplicativo de console em C#.][keys]

<span data-ttu-id="59a57-173">Iniciaremos o aplicativo de introdução criando uma nova instância de **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="59a57-173">We'll start the getting started application by creating a new instance of the **DocumentClient**.</span></span>

<span data-ttu-id="59a57-174">Abaixo do método **Main**, adicione esta nova tarefa assíncrona denominada **GetStartedDemo**, que criará uma instância do nosso novo **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="59a57-174">Below the **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

```csharp
static void Main(string[] args)
{
}

// ADD THIS PART TO YOUR CODE
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);
}
```

<span data-ttu-id="59a57-175">Adicione o código a seguir para executar a tarefa assíncrona a partir do seu método **Main** .</span><span class="sxs-lookup"><span data-stu-id="59a57-175">Add the following code to run your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="59a57-176">O método **Main** capturará as exceções e as gravará no console.</span><span class="sxs-lookup"><span data-stu-id="59a57-176">The **Main** method will catch exceptions and write them to the console.</span></span>

```csharp
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
```

<span data-ttu-id="59a57-177">Pressione o botão **DocumentDBGettingStarted** para compilar e executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="59a57-177">Press the **DocumentDBGettingStarted** button to build and run the application.</span></span>

<span data-ttu-id="59a57-178">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="59a57-178">Congratulations!</span></span> <span data-ttu-id="59a57-179">Você se conectou a uma conta do Azure Cosmos DB. Agora, vamos conferir como trabalhar com recursos do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="59a57-179">You have successfully connected to an Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="59a57-180">Etapa 4: criar um banco de dados</span><span class="sxs-lookup"><span data-stu-id="59a57-180">Step 4: Create a database</span></span>
<span data-ttu-id="59a57-181">Antes de adicionar o código para criar um banco de dados, adicione um método auxiliar para gravar no console.</span><span class="sxs-lookup"><span data-stu-id="59a57-181">Before you add the code for creating a database, add a helper method for writing to the console.</span></span>

<span data-ttu-id="59a57-182">Copie e cole o método **WriteToConsoleAndPromptToContinue** sob o método **GetStartedDemo**.</span><span class="sxs-lookup"><span data-stu-id="59a57-182">Copy and paste the **WriteToConsoleAndPromptToContinue** method underneath the **GetStartedDemo** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
}
```

<span data-ttu-id="59a57-183">Seu [banco de dados](documentdb-resources.md#databases) do Azure Cosmos DB pode ser criado usando o método [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) da classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="59a57-183">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using the [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="59a57-184">Um banco de dados é o contêiner lógico de armazenamento de documentos JSON particionado em coleções.</span><span class="sxs-lookup"><span data-stu-id="59a57-184">A database is the logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="59a57-185">Copie e cole o código a seguir no seu método **GetStartedDemo** embaixo da criação do cliente.</span><span class="sxs-lookup"><span data-stu-id="59a57-185">Copy and paste the following code to your **GetStartedDemo** method underneath the client creation.</span></span> <span data-ttu-id="59a57-186">Isso criará um banco de dados denominado *FamilyDB*.</span><span class="sxs-lookup"><span data-stu-id="59a57-186">This will create a database named *FamilyDB*.</span></span>

```csharp
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    // ADD THIS PART TO YOUR CODE
    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB_oa" });
```

<span data-ttu-id="59a57-187">Pressione o botão **DocumentDBGettingStarted** para executar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="59a57-187">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="59a57-188">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="59a57-188">Congratulations!</span></span> <span data-ttu-id="59a57-189">Você criou um banco de dados do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="59a57-189">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="59a57-190"><a id="CreateColl"></a>Etapa 5: Criar uma coleção</span><span class="sxs-lookup"><span data-stu-id="59a57-190"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="59a57-191">**CreateDocumentCollectionAsync** criará uma nova coleção com uma taxa de transferência reservada, que tem implicações de preço.</span><span class="sxs-lookup"><span data-stu-id="59a57-191">**CreateDocumentCollectionAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="59a57-192">Para obter mais detalhes, visite a nossa [página de preços](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="59a57-192">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>

<span data-ttu-id="59a57-193">É possível criar uma [coleção](documentdb-resources.md#collections) usando o método [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) da classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="59a57-193">A [collection](documentdb-resources.md#collections) can be created by using the [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="59a57-194">Uma coleção é um contêiner de documentos JSON e uma lógica de aplicativo JavaScript associada.</span><span class="sxs-lookup"><span data-stu-id="59a57-194">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="59a57-195">Copie e cole o código a seguir no seu método **GetStartedDemo** sob a criação do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="59a57-195">Copy and paste the following code to your **GetStartedDemo** method underneath the database creation.</span></span> <span data-ttu-id="59a57-196">Isso criará uma coleção de documentos denominada *FamilyCollection_oa*.</span><span class="sxs-lookup"><span data-stu-id="59a57-196">This will create a document collection named *FamilyCollection_oa*.</span></span>

```csharp
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    await this.client.CreateDatabaseIfNotExists("FamilyDB_oa");

    // ADD THIS PART TO YOUR CODE
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"), new DocumentCollection { Id = "FamilyCollection_oa" });
```

<span data-ttu-id="59a57-197">Pressione o botão **DocumentDBGettingStarted** para executar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="59a57-197">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="59a57-198">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="59a57-198">Congratulations!</span></span> <span data-ttu-id="59a57-199">Você criou uma coleção de documentos do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="59a57-199">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="59a57-200"><a id="CreateDoc"></a>Etapa 6: Criar documentos JSON</span><span class="sxs-lookup"><span data-stu-id="59a57-200"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="59a57-201">Um [documento](documentdb-resources.md#documents) pode ser criado usando o método [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) da classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="59a57-201">A [document](documentdb-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="59a57-202">Os documentos são conteúdo JSON (arbitrário) definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="59a57-202">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="59a57-203">Agora podemos inserir um ou mais documentos.</span><span class="sxs-lookup"><span data-stu-id="59a57-203">We can now insert one or more documents.</span></span> <span data-ttu-id="59a57-204">Se já tiver dados que gostaria de armazenar em seu banco de dados, você poderá usar a [ferramenta de Migração de Dados](import-data.md) do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="59a57-204">If you already have data you'd like to store in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md).</span></span>

<span data-ttu-id="59a57-205">Primeiro, precisamos criar uma classe **Family** que representará os objetos armazenados no Azure Cosmos DB neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="59a57-205">First, we need to create a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="59a57-206">Também criaremos as subclasses **Parent**, **Child**, **Pet** e **Address** que são usadas em **Family**.</span><span class="sxs-lookup"><span data-stu-id="59a57-206">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="59a57-207">Observe que os documentos devem ter uma propriedade **Id** serializada como **id** em JSON.</span><span class="sxs-lookup"><span data-stu-id="59a57-207">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="59a57-208">Crie essas classes, adicionando as seguintes subclasses internas após o método **GetStartedDemo** .</span><span class="sxs-lookup"><span data-stu-id="59a57-208">Create these classes by adding the following internal sub-classes after the **GetStartedDemo** method.</span></span>

<span data-ttu-id="59a57-209">Copie e cole as classes **Family**, **Parent**, **Child**, **Pet** e **Address** sob o método **WriteToConsoleAndPromptToContinue**.</span><span class="sxs-lookup"><span data-stu-id="59a57-209">Copy and paste the **Family**, **Parent**, **Child**, **Pet**, and **Address** classes underneath the **WriteToConsoleAndPromptToContinue** method.</span></span>

```csharp
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
```

<span data-ttu-id="59a57-210">Copie e cole o método **CreateFamilyDocumentIfNotExists** sob o método **CreateDocumentCollectionIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="59a57-210">Copy and paste the **CreateFamilyDocumentIfNotExists** method underneath your **CreateDocumentCollectionIfNotExists** method.</span></span>

```csharp
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
```

<span data-ttu-id="59a57-211">Insira dois documentos, um para a Família Martins e um para a Família Barros.</span><span class="sxs-lookup"><span data-stu-id="59a57-211">And insert two documents, one each for the Andersen Family and the Wakefield Family.</span></span>

<span data-ttu-id="59a57-212">Copie e cole o código a seguir `// ADD THIS PART TO YOUR CODE` em seu método **GetStartedDemo** embaixo da criação da coleção de documentos.</span><span class="sxs-lookup"><span data-stu-id="59a57-212">Copy and paste the code that follows `// ADD THIS PART TO YOUR CODE` to your **GetStartedDemo** method underneath the document collection creation.</span></span>

```csharp
await this.CreateDatabaseIfNotExists("FamilyDB_oa");

await this.CreateDocumentCollectionIfNotExists("FamilyDB_oa", "FamilyCollection_oa");

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

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", andersenFamily);

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

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);
```

<span data-ttu-id="59a57-213">Pressione o botão **DocumentDBGettingStarted** para executar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="59a57-213">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="59a57-214">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="59a57-214">Congratulations!</span></span> <span data-ttu-id="59a57-215">Você criou dois documentos do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="59a57-215">You have successfully created two Azure Cosmos DB documents.</span></span>  

![Diagrama que ilustra a relação hierárquica entre a conta, o banco de dados online, a coleção e os documentos usados pelo tutorial do NoSQL para criar um aplicativo de console em C#](./media/documentdb-dotnetcore-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="59a57-217"><a id="Query"></a>Etapa 7: Consultar recursos do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="59a57-217"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="59a57-218">O Azure Cosmos DB tem suporte para [consultas](documentdb-sql-query.md) avançadas de documentos JSON armazenados em cada coleção.</span><span class="sxs-lookup"><span data-stu-id="59a57-218">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="59a57-219">O exemplo de código a seguir mostra diversas consultas - usando a sintaxe SQL do Azure Cosmos DB bem como o LINQ - que podem ser realizadas nos documentos que inserimos na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="59a57-219">The following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against the documents we inserted in the previous step.</span></span>

<span data-ttu-id="59a57-220">Copie e cole o método **ExecuteSimpleQuery** sob seu método **CreateFamilyDocumentIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="59a57-220">Copy and paste the **ExecuteSimpleQuery** method underneath your **CreateFamilyDocumentIfNotExists** method.</span></span>

```csharp
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
```

<span data-ttu-id="59a57-221">Copie e cole o código a seguir no seu método **GetStartedDemo** embaixo da segunda criação de documento.</span><span class="sxs-lookup"><span data-stu-id="59a57-221">Copy and paste the following code to your **GetStartedDemo** method underneath the second document creation.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

// ADD THIS PART TO YOUR CODE
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="59a57-222">Pressione o botão **DocumentDBGettingStarted** para executar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="59a57-222">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="59a57-223">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="59a57-223">Congratulations!</span></span> <span data-ttu-id="59a57-224">Você consultou uma coleção do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="59a57-224">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="59a57-225">O diagrama a seguir ilustra como a sintaxe da consulta SQL do Azure Cosmos DB é chamada em relação à coleção que você criou, e a mesma lógica se aplica à consulta LINQ.</span><span class="sxs-lookup"><span data-stu-id="59a57-225">The following diagram illustrates how the Azure Cosmos DB SQL query syntax is called against the collection you created, and the same logic applies to the LINQ query as well.</span></span>

![Diagrama que ilustra o escopo e o significado da consulta usada pelo tutorial do NoSQL para criar um aplicativo de console em C#](./media/documentdb-dotnetcore-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="59a57-227">A palavra-chave [FROM](documentdb-sql-query.md#FromClause) é opcional na consulta, pois as consultas do Azure Cosmos DB já têm o escopo para uma única coleção.</span><span class="sxs-lookup"><span data-stu-id="59a57-227">The [FROM](documentdb-sql-query.md#FromClause) keyword is optional in the query because Azure Cosmos DB queries are already scoped to a single collection.</span></span> <span data-ttu-id="59a57-228">Portanto, "FROM Families f" pode ser trocado por "FROM root r" ou qualquer outra variável de nome que você escolher.</span><span class="sxs-lookup"><span data-stu-id="59a57-228">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="59a57-229">O DocumentDB fará com que Families, root ou o nome de variável escolhido por você faça referência à coleção atual, por padrão.</span><span class="sxs-lookup"><span data-stu-id="59a57-229">DocumentDB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span></span>

## <span data-ttu-id="59a57-230"><a id="ReplaceDocument"></a>Etapa 8: substituir o documento JSON</span><span class="sxs-lookup"><span data-stu-id="59a57-230"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="59a57-231">O Azure Cosmos DB dá suporte à substituição de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="59a57-231">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="59a57-232">Copie e cole o método **ReplaceFamilyDocument** sob seu método **ExecuteSimpleQuery**.</span><span class="sxs-lookup"><span data-stu-id="59a57-232">Copy and paste the **ReplaceFamilyDocument** method underneath your **ExecuteSimpleQuery** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
{
    try
    {
        await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
        this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

<span data-ttu-id="59a57-233">Copie e cole o código a seguir de seu método **GetStartedDemo** embaixo da execução da consulta.</span><span class="sxs-lookup"><span data-stu-id="59a57-233">Copy and paste the following code to your **GetStartedDemo** method underneath the query execution.</span></span> <span data-ttu-id="59a57-234">Depois de substituir o documento, isso executará a mesma consulta novamente para exibir o documento alterado.</span><span class="sxs-lookup"><span data-stu-id="59a57-234">After replacing the document, this will run the same query again to view the changed document.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART TO YOUR CODE
// Update the Grade of the Andersen Family child
andersenFamily.Children[0].Grade = 6;

await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="59a57-235">Pressione o botão **DocumentDBGettingStarted** para executar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="59a57-235">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="59a57-236">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="59a57-236">Congratulations!</span></span> <span data-ttu-id="59a57-237">Você substituiu um documento do Azure Cosmos DB com sucesso.</span><span class="sxs-lookup"><span data-stu-id="59a57-237">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="59a57-238"><a id="DeleteDocument"></a>Etapa 9: excluir o documento JSON</span><span class="sxs-lookup"><span data-stu-id="59a57-238"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="59a57-239">O Azure Cosmos DB dá suporte à exclusão de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="59a57-239">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="59a57-240">Copie e cole o método **DeleteFamilyDocument** sob seu método **ReplaceFamilyDocument**.</span><span class="sxs-lookup"><span data-stu-id="59a57-240">Copy and paste the **DeleteFamilyDocument** method underneath your **ReplaceFamilyDocument** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
{
    try
    {
        await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
        Console.WriteLine("Deleted Family {0}", documentName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

<span data-ttu-id="59a57-241">Copie e cole o código a seguir de seu método **GetStartedDemo** embaixo da segunda execução da consulta.</span><span class="sxs-lookup"><span data-stu-id="59a57-241">Copy and paste the following code to your **GetStartedDemo** method underneath the second query execution.</span></span>

```csharp
await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART TO CODE
await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");
```

<span data-ttu-id="59a57-242">Pressione o botão **DocumentDBGettingStarted** para executar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="59a57-242">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="59a57-243">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="59a57-243">Congratulations!</span></span> <span data-ttu-id="59a57-244">Você excluiu um documento do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="59a57-244">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="59a57-245"><a id="DeleteDatabase"></a>Etapa 10: excluir o banco de dados</span><span class="sxs-lookup"><span data-stu-id="59a57-245"><a id="DeleteDatabase"></a>Step 10: Delete the database</span></span>
<span data-ttu-id="59a57-246">Excluir o banco de dados criado removerá o banco de dados e todos os recursos filhos (coleções, documentos, etc.).</span><span class="sxs-lookup"><span data-stu-id="59a57-246">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="59a57-247">Copie e cole o código a seguir de seu método **GetStartedDemo** embaixo da exclusão de documento para excluir o banco de dados inteiro e todos os recursos-filhos.</span><span class="sxs-lookup"><span data-stu-id="59a57-247">Copy and paste the following code to your **GetStartedDemo** method underneath the document delete to delete the entire database and all children resources.</span></span>

```csharp
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

// ADD THIS PART TO CODE
// Clean up/delete the database
await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"));
```

<span data-ttu-id="59a57-248">Pressione o botão **DocumentDBGettingStarted** para executar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="59a57-248">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="59a57-249">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="59a57-249">Congratulations!</span></span> <span data-ttu-id="59a57-250">Você excluiu um banco de dados do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="59a57-250">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="59a57-251"><a id="Run"></a>Etapa 11: executar o aplicativo de console C# inteiro!</span><span class="sxs-lookup"><span data-stu-id="59a57-251"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="59a57-252">Pressione o botão **DocumentDBGettingStarted** no Visual Studio para compilar o aplicativo no modo de depuração.</span><span class="sxs-lookup"><span data-stu-id="59a57-252">Press the **DocumentDBGettingStarted** button in Visual Studio to build the application in debug mode.</span></span>

<span data-ttu-id="59a57-253">Você deverá ver a saída do aplicativo iniciado na janela do console.</span><span class="sxs-lookup"><span data-stu-id="59a57-253">You should see the output of your get started app in the console window.</span></span> <span data-ttu-id="59a57-254">A saída mostrará os resultados das consultas que adicionamos e deverá coincidir com o texto de exemplo abaixo.</span><span class="sxs-lookup"><span data-stu-id="59a57-254">The output will show the results of the queries we added and should match the example text below.</span></span>

```
Created FamilyDB_oa
Press any key to continue ...
Created FamilyCollection_oa
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
```

<span data-ttu-id="59a57-255">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="59a57-255">Congratulations!</span></span> <span data-ttu-id="59a57-256">Você concluiu este tutorial e tem um aplicativo de console em C# funcional!</span><span class="sxs-lookup"><span data-stu-id="59a57-256">You've completed the tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="59a57-257"><a id="GetSolution"></a> Obter a solução completa do tutorial</span><span class="sxs-lookup"><span data-stu-id="59a57-257"><a id="GetSolution"></a> Get the complete tutorial solution</span></span>
<span data-ttu-id="59a57-258">Para criar a solução de Introdução que contém todos os exemplos neste artigo, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="59a57-258">To build the GetStarted solution that contains all the samples in this article, you will need the following:</span></span>

* <span data-ttu-id="59a57-259">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="59a57-259">An active Azure account.</span></span> <span data-ttu-id="59a57-260">Se não tiver uma, você poderá se inscrever em uma [conta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="59a57-260">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="59a57-261">Uma [conta do Azure Cosmos DB][create-documentdb-dotnet.md#create-account].</span><span class="sxs-lookup"><span data-stu-id="59a57-261">An [Azure Cosmos DB account][create-documentdb-dotnet.md#create-account].</span></span>
* <span data-ttu-id="59a57-262">A solução [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) disponível no GitHub.</span><span class="sxs-lookup"><span data-stu-id="59a57-262">The [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="59a57-263">Para restaurar as referências da API do DocumentDB do SDK do .NET Core do Azure Cosmos DB no Visual Studio, clique com o botão direito do mouse na solução **GetStarted** no Gerenciador de Soluções e clique em **Habilitar Pacote de Restauração NuGet**.</span><span class="sxs-lookup"><span data-stu-id="59a57-263">To restore the references to the DocumentDB API for Azure Cosmos DB .NET Core SDK in Visual Studio, right-click the **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="59a57-264">Em seguida, no arquivo Program.cs, atualize os valores EndpointUrl e AuthorizationKey conforme descrito em [Conectar-se a uma conta do Azure Cosmos DB](#Connect).</span><span class="sxs-lookup"><span data-stu-id="59a57-264">Next, in the Program.cs file, update the EndpointUrl and AuthorizationKey values as described in [Connect to an Azure Cosmos DB account](#Connect).</span></span>

## <a name="next-steps"></a><span data-ttu-id="59a57-265">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="59a57-265">Next steps</span></span>
* <span data-ttu-id="59a57-266">Quer um tutorial mais complexo do ASP.NET MVC?</span><span class="sxs-lookup"><span data-stu-id="59a57-266">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="59a57-267">Confira [Tutorial do ASP.NET MVC: desenvolvimento de aplicativo Web com o Azure Cosmos DB](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="59a57-267">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="59a57-268">Deseja desenvolver um aplicativo Xamarin iOS, Android ou Forms usando a API do DocumentDB para SDK do .NET Core do Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="59a57-268">Want to develop a Xamarin iOS, Android, or Forms application using the DocumentDB API for Azure Cosmos DB .NET Core SDK?</span></span> <span data-ttu-id="59a57-269">Confira [Criar aplicativos móveis com o Xamarin e o Azure Cosmos DB](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="59a57-269">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>
* <span data-ttu-id="59a57-270">Quer executar testes de desempenho e escala com o Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="59a57-270">Want to perform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="59a57-271">Confira [Teste de desempenho e escala com o Azure Cosmos DB](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="59a57-271">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="59a57-272">Saiba como [Monitorar solicitações, o uso e o armazenamento do Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="59a57-272">Learn how to [Monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="59a57-273">Executar consultas em nosso conjunto de dados de exemplo no [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="59a57-273">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="59a57-274">Para saber mais sobre o modelo de programação, confira [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="59a57-274">To learn more about the programming model, see [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

[create-documentdb-dotnet.md#create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-dotnetcore-get-started/nosql-tutorial-keys.png
