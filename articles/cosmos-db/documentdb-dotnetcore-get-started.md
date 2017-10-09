---
title: "Azure Cosmos DB: tutorial de introdução à API do DocumentDB em .NET Core | Microsoft Docs"
description: Um tutorial que cria um banco de dados online e um aplicativo de console c# usando hello Azure Cosmos DB documentos API .NET Core SDK.
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
ms.openlocfilehash: 5e7efb327252e9e73e9b2a340820eeecc6937fa5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-getting-started-with-hello-documentdb-api-and-net-core"></a><span data-ttu-id="b5ea9-103">Cosmos do Azure DB: Introdução ao hello API DocumentDB e .NET Core</span><span class="sxs-lookup"><span data-stu-id="b5ea9-103">Azure Cosmos DB: Getting started with hello DocumentDB API and .NET Core</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b5ea9-104">.NET</span><span class="sxs-lookup"><span data-stu-id="b5ea9-104">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="b5ea9-105">.NET Core</span><span class="sxs-lookup"><span data-stu-id="b5ea9-105">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="b5ea9-106">Node.js para MongoDB</span><span class="sxs-lookup"><span data-stu-id="b5ea9-106">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="b5ea9-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="b5ea9-107">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="b5ea9-108">Java</span><span class="sxs-lookup"><span data-stu-id="b5ea9-108">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="b5ea9-109">C++</span><span class="sxs-lookup"><span data-stu-id="b5ea9-109">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="b5ea9-110">Bem-vindo toohello API DocumentDB do Azure Cosmos DB Introdução ao tutorial do .NET Core!</span><span class="sxs-lookup"><span data-stu-id="b5ea9-110">Welcome toohello DocumentDB API for Azure Cosmos DB getting started with .NET Core tutorial!</span></span> <span data-ttu-id="b5ea9-111">Após seguir este tutorial, você terá um aplicativo de console que cria e consulta recursos do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-111">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="b5ea9-112">Abordaremos:</span><span class="sxs-lookup"><span data-stu-id="b5ea9-112">We'll cover:</span></span>

* <span data-ttu-id="b5ea9-113">Criar e conectar-se a conta de banco de dados do Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="b5ea9-113">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="b5ea9-114">Configurar a sua Solução do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b5ea9-114">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="b5ea9-115">Criando um banco de dados online</span><span class="sxs-lookup"><span data-stu-id="b5ea9-115">Creating an online database</span></span>
* <span data-ttu-id="b5ea9-116">Criar uma coleção</span><span class="sxs-lookup"><span data-stu-id="b5ea9-116">Creating a collection</span></span>
* <span data-ttu-id="b5ea9-117">Criando documentos JSON</span><span class="sxs-lookup"><span data-stu-id="b5ea9-117">Creating JSON documents</span></span>
* <span data-ttu-id="b5ea9-118">Consultando Olá coleção</span><span class="sxs-lookup"><span data-stu-id="b5ea9-118">Querying hello collection</span></span>
* <span data-ttu-id="b5ea9-119">Substituição de um documento</span><span class="sxs-lookup"><span data-stu-id="b5ea9-119">Replacing a document</span></span>
* <span data-ttu-id="b5ea9-120">Exclusão de um documento</span><span class="sxs-lookup"><span data-stu-id="b5ea9-120">Deleting a document</span></span>
* <span data-ttu-id="b5ea9-121">Excluir banco de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="b5ea9-121">Deleting hello database</span></span>

<span data-ttu-id="b5ea9-122">Você não tem tempo?</span><span class="sxs-lookup"><span data-stu-id="b5ea9-122">Don't have time?</span></span> <span data-ttu-id="b5ea9-123">Não se preocupe!</span><span class="sxs-lookup"><span data-stu-id="b5ea9-123">Don't worry!</span></span> <span data-ttu-id="b5ea9-124">solução completa de saudação está disponível em [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span><span class="sxs-lookup"><span data-stu-id="b5ea9-124">hello complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span> <span data-ttu-id="b5ea9-125">Saltar toohello [obter a seção de solução completa de saudação](#GetSolution) para instruções rápidas.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-125">Jump toohello [Get hello complete solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="b5ea9-126">Deseja toobuild um Xamarin do iOS, Android ou formulários usando o aplicativo hello API DocumentDB e SDK do .NET Core?</span><span class="sxs-lookup"><span data-stu-id="b5ea9-126">Want toobuild a Xamarin iOS, Android, or Forms application using hello DocumentDB API and .NET Core SDK?</span></span> <span data-ttu-id="b5ea9-127">Confira [Criar aplicativos móveis com o Xamarin e o Azure Cosmos DB](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="b5ea9-127">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b5ea9-128">Olá SDK do Azure Cosmos DB .NET Core usados neste tutorial ainda não é compatível com aplicativos do Windows UWP (plataforma Universal).</span><span class="sxs-lookup"><span data-stu-id="b5ea9-128">hello Azure Cosmos DB .NET Core SDK used in this tutorial is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="b5ea9-129">Para uma versão de visualização do hello .NET Core SDK que dá suporte a aplicativos UWP, enviar email muito[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="b5ea9-129">For a preview version of hello .NET Core SDK that does support UWP apps, send email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

<span data-ttu-id="b5ea9-130">Agora vamos começar!</span><span class="sxs-lookup"><span data-stu-id="b5ea9-130">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5ea9-131">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b5ea9-131">Prerequisites</span></span>
<span data-ttu-id="b5ea9-132">Verifique se que você tem o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="b5ea9-132">Please make sure you have hello following:</span></span>

* <span data-ttu-id="b5ea9-133">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-133">An active Azure account.</span></span> <span data-ttu-id="b5ea9-134">Se não tiver uma, você poderá se inscrever em uma [conta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="b5ea9-134">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="b5ea9-135">Como alternativa, você pode usar o hello [emulador de banco de dados do Azure Cosmos](local-emulator.md) para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-135">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="b5ea9-136">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="b5ea9-136">Visual Studio 2017</span></span>](https://www.visualstudio.com/vs/) 
    * <span data-ttu-id="b5ea9-137">Se você estiver trabalhando em MacOS ou Linux, você pode desenvolver aplicativos .NET Core Olá de linha de comando instalando Olá [.NET Core SDK](https://www.microsoft.com/net/core#macos) para plataforma de saudação de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-137">If you're working on MacOS or Linux, you can develop .NET Core apps from hello command-line by installing hello [.NET Core SDK](https://www.microsoft.com/net/core#macos) for hello platform of your choice.</span></span> 
    * <span data-ttu-id="b5ea9-138">Se você estiver trabalhando no Windows, você pode desenvolver aplicativos .NET Core Olá de linha de comando instalando Olá [.NET Core SDK](https://www.microsoft.com/net/core#windows).</span><span class="sxs-lookup"><span data-stu-id="b5ea9-138">If you're working on Windows, you can develop .NET Core apps from hello command-line by installing hello [.NET Core SDK](https://www.microsoft.com/net/core#windows).</span></span> 
    * <span data-ttu-id="b5ea9-139">Você pode usar seu próprio editor ou baixar o [Visual Studio Code](https://code.visualstudio.com/), que é gratuito e funciona no Windows, Linux e MacOS.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-139">You can use your own editor, or download [Visual Studio Code](https://code.visualstudio.com/) which is free and works on Windows, Linux, and MacOS.</span></span> 

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="b5ea9-140">Etapa 1: Criar uma conta de banco de dados do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b5ea9-140">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="b5ea9-141">Vamos criar uma conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-141">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="b5ea9-142">Se você já tiver uma conta que você deseja toouse, poderá pular muito[configurar sua solução do Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="b5ea9-142">If you already have an account you want toouse, you can skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="b5ea9-143">Se você estiver usando hello Azure Cosmos DB emulador, siga as etapas de saudação em [emulador de banco de dados do Azure Cosmos](local-emulator.md) toosetup Olá emulador e pular muito[configurar sua solução do Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="b5ea9-143">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="b5ea9-144"><a id="SetupVS"></a>Etapa 2: configurar a sua solução do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b5ea9-144"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="b5ea9-145">Abra o **Visual Studio 2017** em seu computador.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-145">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="b5ea9-146">Em Olá **arquivo** menu, selecione **novo**e, em seguida, escolha **projeto**.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-146">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="b5ea9-147">Em Olá **novo projeto** caixa de diálogo, selecione **modelos** / **Visual C#** / **.NET Core** / **Aplicativo de console (.NET Core)**, nomeie o projeto **DocumentDBGettingStarted**e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-147">In hello **New Project** dialog, select **Templates** / **Visual C#** / **.NET Core**/**Console Application (.NET Core)**, name your project **DocumentDBGettingStarted**, and then click **OK**.</span></span>

   ![Captura de tela da janela do novo projeto de saudação](./media/documentdb-dotnetcore-get-started/nosql-tutorial-new-project-2.png)
4. <span data-ttu-id="b5ea9-149">Em Olá **Solution Explorer**, clique com o botão direito em **DocumentDBGettingStarted**.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-149">In hello **Solution Explorer**, right click on **DocumentDBGettingStarted**.</span></span>
5. <span data-ttu-id="b5ea9-150">Sem sair do menu de saudação, clique em **gerenciar pacotes NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="b5ea9-150">Then without leaving hello menu, click on **Manage NuGet Packages...**.</span></span>

   ![Captura de tela de saudação à direita Menu clicado para Olá projeto](./media/documentdb-dotnetcore-get-started/nosql-tutorial-manage-nuget-pacakges.png)
6. <span data-ttu-id="b5ea9-152">Em Olá **NuGet** , clique em **procurar** na parte superior de saudação da janela hello e tipo **documentdb do azure** na caixa de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-152">In hello **NuGet** tab, click **Browse** at hello top of hello window, and type **azure documentdb** in hello search box.</span></span>
7. <span data-ttu-id="b5ea9-153">Nos resultados de saudação localizar **Microsoft.Azure.DocumentDB.Core** e clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-153">Within hello results, find **Microsoft.Azure.DocumentDB.Core** and click **Install**.</span></span>
   <span data-ttu-id="b5ea9-154">ID do pacote Olá Olá DocumentDB biblioteca de cliente para .NET Core é [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span><span class="sxs-lookup"><span data-stu-id="b5ea9-154">hello package ID for hello DocumentDB Client Library for .NET Core is [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span></span> <span data-ttu-id="b5ea9-155">Se você estiver visando uma versão do .NET Framework (como net461) que não tem suporte deste pacote do NuGet do .NET Core, use [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB), que dá suporte a todas as versões do .NET Framework, a partir do .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-155">If you are targeting a .NET Framework version (like net461) that is not supported by this .NET Core NuGet package, then use [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) that supports all .NET Framework versions starting .NET Framework 4.5.</span></span>
8. <span data-ttu-id="b5ea9-156">No hello prompts, aceite contrato de licença de saudação e instalações de pacote do NuGet hello.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-156">At hello prompts, accept hello NuGet package installations and hello license agreement.</span></span>

<span data-ttu-id="b5ea9-157">Ótimo!</span><span class="sxs-lookup"><span data-stu-id="b5ea9-157">Great!</span></span> <span data-ttu-id="b5ea9-158">Concluída a instalação Olá, vamos começar a escrever um código.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-158">Now that we finished hello setup, let's start writing some code.</span></span> <span data-ttu-id="b5ea9-159">Você pode encontrar um projeto de código completo deste tutorial no [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span><span class="sxs-lookup"><span data-stu-id="b5ea9-159">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span>

## <span data-ttu-id="b5ea9-160"><a id="Connect"></a>Etapa 3: Conectar-se a conta de banco de dados do Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="b5ea9-160"><a id="Connect"></a>Step 3: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="b5ea9-161">Primeiro, adicione estas referências toohello a partir de seu aplicativo c#, no arquivo Program.cs de saudação:</span><span class="sxs-lookup"><span data-stu-id="b5ea9-161">First, add these references toohello beginning of your C# application, in hello Program.cs file:</span></span>

```csharp
using System;

// ADD THIS PART tooYOUR CODE
using System.Linq;
using System.Threading.Tasks;
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

> [!IMPORTANT]
> <span data-ttu-id="b5ea9-162">Em ordem toocomplete neste tutorial, certifique-se de que adicionar dependências de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-162">In order toocomplete this tutorial, make sure you add hello dependencies above.</span></span>

<span data-ttu-id="b5ea9-163">Agora, adicione essas duas constantes e sua variável *client* sob sua classe pública *Program*.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-163">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

```csharp
class Program
{
    // ADD THIS PART tooYOUR CODE
    private const string EndpointUri = "<your endpoint URI>";
    private const string PrimaryKey = "<your key>";
    private DocumentClient client;
```

<span data-ttu-id="b5ea9-164">Em seguida, head toohello [Portal do Azure](https://portal.azure.com) tooretrieve seu URI e a chave primária.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-164">Next, head toohello [Azure Portal](https://portal.azure.com) tooretrieve your URI and primary key.</span></span> <span data-ttu-id="b5ea9-165">Hello Azure Cosmos DB URI e a chave primária são necessárias para seu aplicativo toounderstand onde tooconnect e para o banco de dados do Azure Cosmos tootrust conexão do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-165">hello Azure Cosmos DB URI and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="b5ea9-166">Olá Portal do Azure, navegue conta de banco de dados do Azure Cosmos tooyour e, em seguida, clique no **chaves**.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-166">In hello Azure Portal, navigate tooyour Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="b5ea9-167">Copie Olá URI do portal hello e cole-o na `<your endpoint URI>` no arquivo program.cs de saudação.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-167">Copy hello URI from hello portal and paste it into `<your endpoint URI>` in hello program.cs file.</span></span> <span data-ttu-id="b5ea9-168">Cópia Olá chave primária do portal hello e cole-o na `<your key>`.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-168">Then copy hello PRIMARY KEY from hello portal and paste it into `<your key>`.</span></span> <span data-ttu-id="b5ea9-169">Se você estiver usando hello Azure Cosmos DB emulador, use `https://localhost:8081` como ponto de extremidade hello e chave de autorização bem definido de saudação do [como toodevelop usando hello Azure Cosmos DB emulador](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="b5ea9-169">If you are using hello Azure Cosmos DB Emulator, use `https://localhost:8081` as hello endpoint, and hello well-defined authorization key from [How toodevelop using hello Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="b5ea9-170">Verifique se Olá de tooremove < e >, mas deixar Olá aspas duplas em torno de seu ponto de extremidade e a chave.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-170">Make sure tooremove hello < and > but leave hello double quotes around your endpoint and key.</span></span>

![Captura de tela de saudação Portal do Azure usado pelo Olá NoSQL tutorial toocreate um aplicativo de console c#.][keys]

<span data-ttu-id="b5ea9-173">Vamos começar o aplicativo de Introdução ao obter hello, criando uma nova instância da saudação **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-173">We'll start hello getting started application by creating a new instance of hello **DocumentClient**.</span></span>

<span data-ttu-id="b5ea9-174">Abaixo Olá **principal** método, adicione essa nova tarefa assíncrona chamada **GetStartedDemo**, qual instanciará nosso novo **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-174">Below hello **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

```csharp
static void Main(string[] args)
{
}

// ADD THIS PART tooYOUR CODE
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);
}
```

<span data-ttu-id="b5ea9-175">Adicione o código a seguir Olá toorun sua tarefa assíncrona de seu **principal** método.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-175">Add hello following code toorun your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="b5ea9-176">Olá **principal** método capturar exceções e os grava toohello console.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-176">hello **Main** method will catch exceptions and write them toohello console.</span></span>

```csharp
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
```

<span data-ttu-id="b5ea9-177">Olá pressione **DocumentDBGettingStarted** botão toobuild e execute o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-177">Press hello **DocumentDBGettingStarted** button toobuild and run hello application.</span></span>

<span data-ttu-id="b5ea9-178">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="b5ea9-178">Congratulations!</span></span> <span data-ttu-id="b5ea9-179">Você se conectou com êxito a conta de banco de dados do Azure Cosmos tooan, agora, vamos examinar trabalhando com recursos de banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-179">You have successfully connected tooan Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="b5ea9-180">Etapa 4: criar um banco de dados</span><span class="sxs-lookup"><span data-stu-id="b5ea9-180">Step 4: Create a database</span></span>
<span data-ttu-id="b5ea9-181">Antes de adicionar o código de saudação para a criação de um banco de dados, adicione um método auxiliar para gravar toohello console.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-181">Before you add hello code for creating a database, add a helper method for writing toohello console.</span></span>

<span data-ttu-id="b5ea9-182">Copie e cole Olá **WriteToConsoleAndPromptToContinue** método sob Olá **GetStartedDemo** método.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-182">Copy and paste hello **WriteToConsoleAndPromptToContinue** method underneath hello **GetStartedDemo** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
}
```

<span data-ttu-id="b5ea9-183">O banco de dados do Azure Cosmos [banco de dados](documentdb-resources.md#databases) podem ser criados usando Olá [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) método hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-183">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="b5ea9-184">Um banco de dados é um contêiner lógico de saudação do armazenamento de documentos JSON particionado em coleções.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-184">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="b5ea9-185">Copiar e colar a seguir Olá código tooyour **GetStartedDemo** método sob a criação de saudação do cliente.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-185">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello client creation.</span></span> <span data-ttu-id="b5ea9-186">Isso criará um banco de dados denominado *FamilyDB*.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-186">This will create a database named *FamilyDB*.</span></span>

```csharp
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB_oa" });
```

<span data-ttu-id="b5ea9-187">Olá pressione **DocumentDBGettingStarted** botão toorun seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-187">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="b5ea9-188">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="b5ea9-188">Congratulations!</span></span> <span data-ttu-id="b5ea9-189">Você criou um banco de dados do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-189">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="b5ea9-190"><a id="CreateColl"></a>Etapa 5: Criar uma coleção</span><span class="sxs-lookup"><span data-stu-id="b5ea9-190"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="b5ea9-191">**CreateDocumentCollectionAsync** criará uma nova coleção com uma taxa de transferência reservada, que tem implicações de preço.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-191">**CreateDocumentCollectionAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="b5ea9-192">Para obter mais detalhes, visite a nossa [página de preços](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="b5ea9-192">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>

<span data-ttu-id="b5ea9-193">Um [coleção](documentdb-resources.md#collections) podem ser criados usando Olá [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) método hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-193">A [collection](documentdb-resources.md#collections) can be created by using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="b5ea9-194">Uma coleção é um contêiner de documentos JSON e uma lógica de aplicativo JavaScript associada.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-194">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="b5ea9-195">Copiar e colar a seguir Olá código tooyour **GetStartedDemo** método sob a criação do banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-195">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello database creation.</span></span> <span data-ttu-id="b5ea9-196">Isso criará uma coleção de documentos denominada *FamilyCollection_oa*.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-196">This will create a document collection named *FamilyCollection_oa*.</span></span>

```csharp
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    await this.client.CreateDatabaseIfNotExists("FamilyDB_oa");

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"), new DocumentCollection { Id = "FamilyCollection_oa" });
```

<span data-ttu-id="b5ea9-197">Olá pressione **DocumentDBGettingStarted** botão toorun seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-197">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="b5ea9-198">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="b5ea9-198">Congratulations!</span></span> <span data-ttu-id="b5ea9-199">Você criou uma coleção de documentos do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-199">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="b5ea9-200"><a id="CreateDoc"></a>Etapa 6: Criar documentos JSON</span><span class="sxs-lookup"><span data-stu-id="b5ea9-200"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="b5ea9-201">Um [documento](documentdb-resources.md#documents) podem ser criados usando Olá [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) método hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-201">A [document](documentdb-resources.md#documents) can be created by using hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="b5ea9-202">Os documentos são conteúdo JSON (arbitrário) definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-202">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="b5ea9-203">Agora podemos inserir um ou mais documentos.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-203">We can now insert one or more documents.</span></span> <span data-ttu-id="b5ea9-204">Se você já tiver dados você gostaria que toostore no banco de dados, você pode usar o Azure Cosmos DB [ferramenta de migração de dados](import-data.md).</span><span class="sxs-lookup"><span data-stu-id="b5ea9-204">If you already have data you'd like toostore in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md).</span></span>

<span data-ttu-id="b5ea9-205">Primeiro, precisamos toocreate um **família** classe que representa os objetos armazenados no banco de dados do Azure Cosmos neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-205">First, we need toocreate a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="b5ea9-206">Também criaremos as subclasses **Parent**, **Child**, **Pet** e **Address** que são usadas em **Family**.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-206">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="b5ea9-207">Observe que os documentos devem ter uma propriedade **Id** serializada como **id** em JSON.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-207">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="b5ea9-208">Criar essas classes adicionando Olá classes sub internas a seguir após Olá **GetStartedDemo** método.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-208">Create these classes by adding hello following internal sub-classes after hello **GetStartedDemo** method.</span></span>

<span data-ttu-id="b5ea9-209">Copie e cole Olá **família**, **pai**, **filho**, **animal de estimação**, e **endereço** classes abaixo Olá **WriteToConsoleAndPromptToContinue** método.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-209">Copy and paste hello **Family**, **Parent**, **Child**, **Pet**, and **Address** classes underneath hello **WriteToConsoleAndPromptToContinue** method.</span></span>

```csharp
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
```

<span data-ttu-id="b5ea9-210">Copie e cole Olá **CreateFamilyDocumentIfNotExists** método sob sua **CreateDocumentCollectionIfNotExists** método.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-210">Copy and paste hello **CreateFamilyDocumentIfNotExists** method underneath your **CreateDocumentCollectionIfNotExists** method.</span></span>

```csharp
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
```

<span data-ttu-id="b5ea9-211">E inserir dois documentos, um para Olá Andersen família e hello Wakefield família.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-211">And insert two documents, one each for hello Andersen Family and hello Wakefield Family.</span></span>

<span data-ttu-id="b5ea9-212">Copie e cole o código de saudação que segue `// ADD THIS PART tooYOUR CODE` tooyour **GetStartedDemo** método sob a criação do conjunto de documento hello.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-212">Copy and paste hello code that follows `// ADD THIS PART tooYOUR CODE` tooyour **GetStartedDemo** method underneath hello document collection creation.</span></span>

```csharp
await this.CreateDatabaseIfNotExists("FamilyDB_oa");

await this.CreateDocumentCollectionIfNotExists("FamilyDB_oa", "FamilyCollection_oa");

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

<span data-ttu-id="b5ea9-213">Olá pressione **DocumentDBGettingStarted** botão toorun seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-213">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="b5ea9-214">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="b5ea9-214">Congratulations!</span></span> <span data-ttu-id="b5ea9-215">Você criou dois documentos do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-215">You have successfully created two Azure Cosmos DB documents.</span></span>  

![Diagrama ilustrando uma relação hierárquica Olá entre conta hello, banco de dados online hello, coleção hello e documentos Olá usados pelo Olá NoSQL tutorial toocreate um aplicativo de console c#](./media/documentdb-dotnetcore-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="b5ea9-217"><a id="Query"></a>Etapa 7: Consultar recursos do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b5ea9-217"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="b5ea9-218">O Azure Cosmos DB tem suporte para [consultas](documentdb-sql-query.md) avançadas de documentos JSON armazenados em cada coleção.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-218">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="b5ea9-219">Olá, código de exemplo seguinte mostra várias consultas - usando ambos os SQL de banco de dados do Azure Cosmos sintaxe, bem como LINQ - que podem ser executados em relação a Olá documentos que são inseridos na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-219">hello following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against hello documents we inserted in hello previous step.</span></span>

<span data-ttu-id="b5ea9-220">Copie e cole Olá **ExecuteSimpleQuery** método sob sua **CreateFamilyDocumentIfNotExists** método.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-220">Copy and paste hello **ExecuteSimpleQuery** method underneath your **CreateFamilyDocumentIfNotExists** method.</span></span>

```csharp
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
```

<span data-ttu-id="b5ea9-221">Copiar e colar a seguir Olá código tooyour **GetStartedDemo** método sob a criação de documento segundo hello.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-221">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello second document creation.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

// ADD THIS PART tooYOUR CODE
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="b5ea9-222">Olá pressione **DocumentDBGettingStarted** botão toorun seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-222">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="b5ea9-223">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="b5ea9-223">Congratulations!</span></span> <span data-ttu-id="b5ea9-224">Você consultou uma coleção do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-224">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="b5ea9-225">Olá diagrama a seguir ilustra como consultas de banco de dados SQL do Azure Cosmos Olá sintaxe é chamada na coleção de saudação que você criou e hello mesma lógica se aplica também a consulta LINQ em toohello.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-225">hello following diagram illustrates how hello Azure Cosmos DB SQL query syntax is called against hello collection you created, and hello same logic applies toohello LINQ query as well.</span></span>

![Diagrama ilustrando escopo hello e o significado da consulta Olá usado pelo Olá NoSQL tutorial toocreate um aplicativo de console c#](./media/documentdb-dotnetcore-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="b5ea9-227">Olá [FROM](documentdb-sql-query.md#FromClause) palavra-chave é opcional em consulta Olá porque as consultas de banco de dados do Azure Cosmos já estão no escopo tooa única coleção.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-227">hello [FROM](documentdb-sql-query.md#FromClause) keyword is optional in hello query because Azure Cosmos DB queries are already scoped tooa single collection.</span></span> <span data-ttu-id="b5ea9-228">Portanto, "FROM Families f" pode ser trocado por "FROM root r" ou qualquer outra variável de nome que você escolher.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-228">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="b5ea9-229">Documentos deduzirá que famílias, raiz ou o nome da variável Olá você escolheu, coleção atual de saudação de referência por padrão.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-229">DocumentDB will infer that Families, root, or hello variable name you chose, reference hello current collection by default.</span></span>

## <span data-ttu-id="b5ea9-230"><a id="ReplaceDocument"></a>Etapa 8: substituir o documento JSON</span><span class="sxs-lookup"><span data-stu-id="b5ea9-230"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="b5ea9-231">O Azure Cosmos DB dá suporte à substituição de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-231">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="b5ea9-232">Copie e cole Olá **ReplaceFamilyDocument** método sob sua **ExecuteSimpleQuery** método.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-232">Copy and paste hello **ReplaceFamilyDocument** method underneath your **ExecuteSimpleQuery** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
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

<span data-ttu-id="b5ea9-233">Copiar e colar a seguir Olá código tooyour **GetStartedDemo** método sob a execução da consulta hello.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-233">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello query execution.</span></span> <span data-ttu-id="b5ea9-234">Depois de substituir o documento hello, isso será executado Olá mesmo novamente consultar tooview Olá alterado documento.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-234">After replacing hello document, this will run hello same query again tooview hello changed document.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooYOUR CODE
// Update hello Grade of hello Andersen Family child
andersenFamily.Children[0].Grade = 6;

await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="b5ea9-235">Olá pressione **DocumentDBGettingStarted** botão toorun seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-235">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="b5ea9-236">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="b5ea9-236">Congratulations!</span></span> <span data-ttu-id="b5ea9-237">Você substituiu um documento do Azure Cosmos DB com sucesso.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-237">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="b5ea9-238"><a id="DeleteDocument"></a>Etapa 9: excluir o documento JSON</span><span class="sxs-lookup"><span data-stu-id="b5ea9-238"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="b5ea9-239">O Azure Cosmos DB dá suporte à exclusão de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-239">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="b5ea9-240">Copie e cole Olá **DeleteFamilyDocument** método sob sua **ReplaceFamilyDocument** método.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-240">Copy and paste hello **DeleteFamilyDocument** method underneath your **ReplaceFamilyDocument** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
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

<span data-ttu-id="b5ea9-241">Copiar e colar a seguir Olá código tooyour **GetStartedDemo** método sob a segunda execução da consulta hello.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-241">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello second query execution.</span></span>

```csharp
await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooCODE
await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");
```

<span data-ttu-id="b5ea9-242">Olá pressione **DocumentDBGettingStarted** botão toorun seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-242">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="b5ea9-243">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="b5ea9-243">Congratulations!</span></span> <span data-ttu-id="b5ea9-244">Você excluiu um documento do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-244">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="b5ea9-245"><a id="DeleteDatabase"></a>Etapa 10: Excluir o banco de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="b5ea9-245"><a id="DeleteDatabase"></a>Step 10: Delete hello database</span></span>
<span data-ttu-id="b5ea9-246">Excluindo Olá criado o banco de dados removerá o banco de dados de saudação e todos os recursos de filhos (coleções, documentos, etc.).</span><span class="sxs-lookup"><span data-stu-id="b5ea9-246">Deleting hello created database will remove hello database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="b5ea9-247">Copiar e colar a seguir Olá código tooyour **GetStartedDemo** método sob documento hello excluir banco de dados inteiro toodelete hello e todos os recursos de filhos.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-247">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello document delete toodelete hello entire database and all children resources.</span></span>

```csharp
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

// ADD THIS PART tooCODE
// Clean up/delete hello database
await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"));
```

<span data-ttu-id="b5ea9-248">Olá pressione **DocumentDBGettingStarted** botão toorun seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-248">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="b5ea9-249">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="b5ea9-249">Congratulations!</span></span> <span data-ttu-id="b5ea9-250">Você excluiu um banco de dados do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-250">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="b5ea9-251"><a id="Run"></a>Etapa 11: executar o aplicativo de console C# inteiro!</span><span class="sxs-lookup"><span data-stu-id="b5ea9-251"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="b5ea9-252">Olá pressione **DocumentDBGettingStarted** botão no aplicativo do Visual Studio toobuild hello no modo de depuração.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-252">Press hello **DocumentDBGettingStarted** button in Visual Studio toobuild hello application in debug mode.</span></span>

<span data-ttu-id="b5ea9-253">Você deve ver a saída de saudação do aplicativo iniciado get na janela de console hello.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-253">You should see hello output of your get started app in hello console window.</span></span> <span data-ttu-id="b5ea9-254">saída de Hello mostrará os resultados de saudação do hello consultas adicionamos e deve coincidir com o texto de exemplo hello abaixo.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-254">hello output will show hello results of hello queries we added and should match hello example text below.</span></span>

```
Created FamilyDB_oa
Press any key toocontinue ...
Created FamilyCollection_oa
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
```

<span data-ttu-id="b5ea9-255">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="b5ea9-255">Congratulations!</span></span> <span data-ttu-id="b5ea9-256">Você concluiu o tutorial hello e ter um aplicativo de console funcional c#!</span><span class="sxs-lookup"><span data-stu-id="b5ea9-256">You've completed hello tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="b5ea9-257"><a id="GetSolution"></a>Obter a solução completa de tutorial Olá</span><span class="sxs-lookup"><span data-stu-id="b5ea9-257"><a id="GetSolution"></a> Get hello complete tutorial solution</span></span>
<span data-ttu-id="b5ea9-258">toobuild Olá GetStarted solução que contém todos os exemplos de saudação neste artigo, você precisará seguir hello:</span><span class="sxs-lookup"><span data-stu-id="b5ea9-258">toobuild hello GetStarted solution that contains all hello samples in this article, you will need hello following:</span></span>

* <span data-ttu-id="b5ea9-259">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-259">An active Azure account.</span></span> <span data-ttu-id="b5ea9-260">Se não tiver uma, você poderá se inscrever em uma [conta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="b5ea9-260">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="b5ea9-261">Uma [conta do Azure Cosmos DB][create-documentdb-dotnet.md#create-account].</span><span class="sxs-lookup"><span data-stu-id="b5ea9-261">An [Azure Cosmos DB account][create-documentdb-dotnet.md#create-account].</span></span>
* <span data-ttu-id="b5ea9-262">Olá [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) solução disponível no GitHub.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-262">hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="b5ea9-263">toorestore Olá referências toohello DocumentDB API do SDK do Azure Cosmos DB .NET Core no Visual Studio, clique com botão direito Olá **GetStarted** solução no Gerenciador de soluções e clique **restauração de pacotes do NuGetHabilitar**.</span><span class="sxs-lookup"><span data-stu-id="b5ea9-263">toorestore hello references toohello DocumentDB API for Azure Cosmos DB .NET Core SDK in Visual Studio, right-click hello **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="b5ea9-264">Em seguida, no arquivo Program.cs Olá atualizar Olá EndpointUrl e AuthorizationKey valores conforme descrito em [conectar-se a conta de banco de dados do Azure Cosmos tooan](#Connect).</span><span class="sxs-lookup"><span data-stu-id="b5ea9-264">Next, in hello Program.cs file, update hello EndpointUrl and AuthorizationKey values as described in [Connect tooan Azure Cosmos DB account](#Connect).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5ea9-265">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b5ea9-265">Next steps</span></span>
* <span data-ttu-id="b5ea9-266">Quer um tutorial mais complexo do ASP.NET MVC?</span><span class="sxs-lookup"><span data-stu-id="b5ea9-266">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="b5ea9-267">Confira [Tutorial do ASP.NET MVC: desenvolvimento de aplicativo Web com o Azure Cosmos DB](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="b5ea9-267">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="b5ea9-268">Deseja toodevelop um Xamarin do iOS, Android ou formulários usando o aplicativo hello DocumentDB API do SDK do Azure Cosmos DB .NET Core?</span><span class="sxs-lookup"><span data-stu-id="b5ea9-268">Want toodevelop a Xamarin iOS, Android, or Forms application using hello DocumentDB API for Azure Cosmos DB .NET Core SDK?</span></span> <span data-ttu-id="b5ea9-269">Confira [Criar aplicativos móveis com o Xamarin e o Azure Cosmos DB](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="b5ea9-269">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>
* <span data-ttu-id="b5ea9-270">Deseja tooperform escala e testes de desempenho com o banco de dados do Azure Cosmos?</span><span class="sxs-lookup"><span data-stu-id="b5ea9-270">Want tooperform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="b5ea9-271">Confira [Teste de desempenho e escala com o Azure Cosmos DB](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="b5ea9-271">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="b5ea9-272">Saiba como muito[solicitações, uso e armazenamento do banco de dados do Monitor do Azure Cosmos](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="b5ea9-272">Learn how too[Monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="b5ea9-273">Executar consultas em nosso conjunto de dados de exemplo hello [parque de consulta](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="b5ea9-273">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="b5ea9-274">toolearn mais sobre o modelo de programação hello, consulte [o banco de dados do Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="b5ea9-274">toolearn more about hello programming model, see [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

[create-documentdb-dotnet.md#create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-dotnetcore-get-started/nosql-tutorial-keys.png
