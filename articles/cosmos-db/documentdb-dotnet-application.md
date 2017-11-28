---
title: 'Tutorial do ASP.NET MVC para Azure Cosmos DB: desenvolvimento de aplicativo Web | Microsoft Docs'
description: "ASP.NET MVC tutorial toocreate um aplicativo web do MVC usando o banco de dados do Azure Cosmos. Você armazenará o JSON e acessará dados de um aplicativo de lista de tarefas pendentes hospedado em sites do Azure ‒ tutorial passo a passo do ASP NET MVC."
keywords: tutorial do asp.net mvc, desenvolvimento de aplicativos web, aplicativo web mvc, passo a passo do tutorial do asp net mvc
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 52532d89-a40e-4fdf-9b38-aadb3a4cccbc
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: mimig
ms.openlocfilehash: dac2a9599b395524533e6fe14983789ff095331f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="104e2-105"><a name="_Toc395809351"></a>Tutorial do ASP.NET MVC: desenvolvimento de aplicativo Web com o Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="104e2-105"><a name="_Toc395809351"></a>ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="104e2-106">.NET</span><span class="sxs-lookup"><span data-stu-id="104e2-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="104e2-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="104e2-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="104e2-108">Java</span><span class="sxs-lookup"><span data-stu-id="104e2-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="104e2-109">Python</span><span class="sxs-lookup"><span data-stu-id="104e2-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="104e2-110">toohighlight como com eficiência, você pode aproveitar o banco de dados do Azure Cosmos toostore e consultar documentos JSON, este artigo fornece uma passo a passo a-ponta mostrando como toobuild um aplicativo todo usando o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="104e2-110">toohighlight how you can efficiently leverage Azure Cosmos DB toostore and query JSON documents, this article provides an end-to-end walk-through showing you how toobuild a todo app using Azure Cosmos DB.</span></span> <span data-ttu-id="104e2-111">tarefas de saudação serão armazenadas como documentos JSON no banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="104e2-111">hello tasks will be stored as JSON documents in Azure Cosmos DB.</span></span>

![Captura de tela da lista de tarefas Olá aplicativo da web MVC criado por este tutorial - tutorial de ASP NET MVC passo a passo](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-image01.png)

<span data-ttu-id="104e2-113">Este passo a passo mostra como toouse hello Azure Cosmos DB serviço toostore e acessar dados de um aplicativo ASP.NET MVC hospedado no Azure.</span><span class="sxs-lookup"><span data-stu-id="104e2-113">This walk-through shows you how toouse hello Azure Cosmos DB service toostore and access data from an ASP.NET MVC web application hosted on Azure.</span></span> <span data-ttu-id="104e2-114">Se você estiver procurando um tutorial que se concentra somente no banco de dados do Azure Cosmos e não hello componentes do ASP.NET MVC, consulte [criar um aplicativo de console do Azure Cosmos DB c#](documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="104e2-114">If you're looking for a tutorial that focuses only on Azure Cosmos DB, and not hello ASP.NET MVC components, see [Build an Azure Cosmos DB C# console application](documentdb-get-started.md).</span></span>

> [!TIP]
> <span data-ttu-id="104e2-115">Este tutorial pressupõe que você tem experiência anterior com o ASP.NET MVC e com os Sites do Azure.</span><span class="sxs-lookup"><span data-stu-id="104e2-115">This tutorial assumes that you have prior experience using ASP.NET MVC and Azure Websites.</span></span> <span data-ttu-id="104e2-116">Se você for novo tooASP.NET ou Olá [ferramentas pré-requisito](#_Toc395637760), recomendamos o download do projeto de exemplo completo de saudação do [GitHub] [ GitHub] e seguindo as instruções de saudação de Este exemplo.</span><span class="sxs-lookup"><span data-stu-id="104e2-116">If you are new tooASP.NET or hello [prerequisite tools](#_Toc395637760), we recommend downloading hello complete sample project from [GitHub][GitHub] and following hello instructions in this sample.</span></span> <span data-ttu-id="104e2-117">Depois de criado, você pode examinar informações de toogain este artigo no código Olá no contexto de saudação do projeto hello.</span><span class="sxs-lookup"><span data-stu-id="104e2-117">Once you have it built, you can review this article toogain insight on hello code in hello context of hello project.</span></span>
> 
> 

## <span data-ttu-id="104e2-118"><a name="_Toc395637760"></a>Pré-requisitos para este tutorial de banco de dados</span><span class="sxs-lookup"><span data-stu-id="104e2-118"><a name="_Toc395637760"></a>Prerequisites for this database tutorial</span></span>
<span data-ttu-id="104e2-119">Antes de seguir as instruções neste artigo hello, você deve garantir que você tenha a seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="104e2-119">Before following hello instructions in this article, you should ensure that you have hello following:</span></span>

* <span data-ttu-id="104e2-120">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="104e2-120">An active Azure account.</span></span> <span data-ttu-id="104e2-121">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="104e2-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="104e2-122">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="104e2-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

    <span data-ttu-id="104e2-123">OU</span><span class="sxs-lookup"><span data-stu-id="104e2-123">OR</span></span>

    <span data-ttu-id="104e2-124">Uma instalação local do hello [emulador de banco de dados do Azure Cosmos](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="104e2-124">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="104e2-125">[Visual Studio 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="104e2-125">[Visual Studio 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="104e2-126">SDK do Microsoft Azure para .NET para Visual Studio de 2017, disponíveis por meio de saudação instalador do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="104e2-126">Microsoft Azure SDK for .NET for Visual Studio 2017, available through hello Visual Studio Installer.</span></span>

<span data-ttu-id="104e2-127">Todas as capturas de tela de saudação neste artigo tem sido feitas usando o Microsoft Visual Studio Community 2017.</span><span class="sxs-lookup"><span data-stu-id="104e2-127">All hello screen shots in this article have been taken using Microsoft Visual Studio Community 2017.</span></span> <span data-ttu-id="104e2-128">Se seu sistema estiver configurado com uma versão diferente, é possível que as opções e telas não correspondem totalmente, mas se você atender a saudação acima pré-requisitos Essa solução deve funcionar.</span><span class="sxs-lookup"><span data-stu-id="104e2-128">If your system is configured with a different version it is possible that your screens and options won't match entirely, but if you meet hello above prerequisites this solution should work.</span></span>

## <span data-ttu-id="104e2-129"><a name="_Toc395637761"></a>Etapa 1: Criar uma conta de banco de dados do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="104e2-129"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="104e2-130">Vamos começar criando uma conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="104e2-130">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="104e2-131">Se você já tem uma conta do SQL (documentos) para o banco de dados do Azure Cosmos ou se você estiver usando hello Azure Cosmos DB emulador para este tutorial, você poderá ignorar muito[criar um novo aplicativo ASP.NET MVC](#_Toc395637762).</span><span class="sxs-lookup"><span data-stu-id="104e2-131">If you already have a SQL (DocumentDB) account for Azure Cosmos DB or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Create a new ASP.NET MVC application](#_Toc395637762).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

<br/>
<span data-ttu-id="104e2-132">Agora vamos percorrer como toocreate um novo aplicativo ASP.NET MVC de saudação Terra-o.</span><span class="sxs-lookup"><span data-stu-id="104e2-132">We will now walk through how toocreate a new ASP.NET MVC application from hello ground-up.</span></span> 

## <span data-ttu-id="104e2-133"><a name="_Toc395637762"></a>Etapa 2: criar um novo aplicativo ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="104e2-133"><a name="_Toc395637762"></a>Step 2: Create a new ASP.NET MVC application</span></span>

1. <span data-ttu-id="104e2-134">No Visual Studio, no hello **arquivo** menus, aponte muito**novo**e, em seguida, clique em **projeto**.</span><span class="sxs-lookup"><span data-stu-id="104e2-134">In Visual Studio, on hello **File** menu, point too**New**, and then click **Project**.</span></span> <span data-ttu-id="104e2-135">Olá **novo projeto** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="104e2-135">hello **New Project** dialog box appears.</span></span>

2. <span data-ttu-id="104e2-136">Em Olá **tipos de projeto** painel, expanda **modelos**, **Visual C#**, **Web**e, em seguida, selecione **aplicativo Web ASP.NET** .</span><span class="sxs-lookup"><span data-stu-id="104e2-136">In hello **Project types** pane, expand **Templates**, **Visual C#**, **Web**, and then select **ASP.NET Web Application**.</span></span>

      ![Captura de tela da caixa de diálogo Novo projeto Olá com tipo de projeto de aplicativo Web ASP.NET Olá realçado](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-project-dialog.png)

3. <span data-ttu-id="104e2-138">Em Olá **nome** caixa, digite o nome de saudação do projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="104e2-138">In hello **Name** box, type hello name of hello project.</span></span> <span data-ttu-id="104e2-139">Este tutorial usa nome hello "todo".</span><span class="sxs-lookup"><span data-stu-id="104e2-139">This tutorial uses hello name "todo".</span></span> <span data-ttu-id="104e2-140">Se você escolher toouse algo diferente de isso, em seguida, sempre que este tutorial aborda Olá todo namespace, você precisa toouse de exemplos de código tooadjust Olá fornecido tudo o que você nomeou seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="104e2-140">If you choose toouse something other than this, then wherever this tutorial talks about hello todo namespace, you need tooadjust hello provided code samples toouse whatever you named your application.</span></span> 
4. <span data-ttu-id="104e2-141">Clique em **procurar** toonavigate toohello pasta onde você deseja como projeto de saudação toocreate e clique **Okey**.</span><span class="sxs-lookup"><span data-stu-id="104e2-141">Click **Browse** toonavigate toohello folder where you would like toocreate hello project, and then click **OK**.</span></span>
   
      <span data-ttu-id="104e2-142">Olá **novo aplicativo Web ASP.NET** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="104e2-142">hello **New ASP.NET Web Application** dialog box appears.</span></span>
   
    ![Captura de tela da caixa de diálogo Novo aplicativo Web ASP.NET Olá com modelo de aplicativo MVC Olá realçado](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-MVC.png)
5. <span data-ttu-id="104e2-144">No painel de modelos hello, selecione **MVC**.</span><span class="sxs-lookup"><span data-stu-id="104e2-144">In hello templates pane, select **MVC**.</span></span>

6. <span data-ttu-id="104e2-145">Clique em **Okey** e deixar o Visual Studio fazer seu trabalho em torno do modelo de ASP.NET MVC scaffolding Olá vazio.</span><span class="sxs-lookup"><span data-stu-id="104e2-145">Click **OK** and let Visual Studio do its thing around scaffolding hello empty ASP.NET MVC template.</span></span> 

          
7. <span data-ttu-id="104e2-146">Depois que o Visual Studio terminar a criação do aplicativo do hello boilerplate MVC, você tem um aplicativo ASP.NET vazio que pode ser executado localmente.</span><span class="sxs-lookup"><span data-stu-id="104e2-146">Once Visual Studio has finished creating hello boilerplate MVC application you have an empty ASP.NET application that you can run locally.</span></span>
   
    <span data-ttu-id="104e2-147">Será ignorada projeto de saudação em execução localmente como sei temos Olá todos vistas ASP.NET "Hello World" aplicativo.</span><span class="sxs-lookup"><span data-stu-id="104e2-147">We'll skip running hello project locally because I'm sure we've all seen hello ASP.NET "Hello World" application.</span></span> <span data-ttu-id="104e2-148">Vamos tooadding reta Azure Cosmos DB toothis projeto e compilar nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="104e2-148">Let's go straight tooadding Azure Cosmos DB toothis project and building our application.</span></span>

## <span data-ttu-id="104e2-149"><a name="_Toc395637767"></a>Etapa 3: Adicionar um projeto de aplicativo web do banco de dados do Azure Cosmos tooyour MVC</span><span class="sxs-lookup"><span data-stu-id="104e2-149"><a name="_Toc395637767"></a>Step 3: Add Azure Cosmos DB tooyour MVC web application project</span></span>
<span data-ttu-id="104e2-150">Agora que temos a maioria dos detalhes técnicos saudação do ASP.NET MVC que precisamos para esta solução, vamos toohello propósito deste tutorial, adicionando o aplicativo web do banco de dados do Azure Cosmos tooour MVC.</span><span class="sxs-lookup"><span data-stu-id="104e2-150">Now that we have most of hello ASP.NET MVC plumbing that we need for this solution, let's get toohello real purpose of this tutorial, adding Azure Cosmos DB tooour MVC web application.</span></span>

1. <span data-ttu-id="104e2-151">Olá SDK .NET do Azure Cosmos DB empacotado e distribuído como um pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="104e2-151">hello Azure Cosmos DB .NET SDK is packaged and distributed as a NuGet package.</span></span> <span data-ttu-id="104e2-152">tooget Olá pacote do NuGet no Visual Studio, use o Gerenciador de pacotes do NuGet Olá no Visual Studio clicando no projeto Olá no **Solution Explorer** e, em seguida, clicando em **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="104e2-152">tooget hello NuGet package in Visual Studio, use hello NuGet package manager in Visual Studio by right-clicking on hello project in **Solution Explorer** and then clicking **Manage NuGet Packages**.</span></span>
   
    ![Captura de tela de saudação com o botão direito em opções para o projeto de aplicativo web Olá no Gerenciador de soluções, com gerenciar pacotes NuGet realçado.](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-manage-nuget.png)
   
    <span data-ttu-id="104e2-154">Olá **gerenciar pacotes NuGet** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="104e2-154">hello **Manage NuGet Packages** dialog box appears.</span></span>
2. <span data-ttu-id="104e2-155">Em Olá NuGet **procurar** , digite ***DocumentDB do Azure***.</span><span class="sxs-lookup"><span data-stu-id="104e2-155">In hello NuGet **Browse** box, type ***Azure DocumentDB***.</span></span> <span data-ttu-id="104e2-156">(nome do pacote de saudação não foi atualizado tooAzure Cosmos DB.)</span><span class="sxs-lookup"><span data-stu-id="104e2-156">(hello package name has not been updated tooAzure Cosmos DB.)</span></span>
   
    <span data-ttu-id="104e2-157">Resultados de hello, instalar Olá **Microsoft.Azure.DocumentDB pela Microsoft** pacote.</span><span class="sxs-lookup"><span data-stu-id="104e2-157">From hello results, install hello **Microsoft.Azure.DocumentDB by Microsoft** package.</span></span> <span data-ttu-id="104e2-158">Isso baixará e instalará o pacote de banco de dados do Azure Cosmos hello, bem como todas as dependências, como newtonsoft. JSON.</span><span class="sxs-lookup"><span data-stu-id="104e2-158">This will download and install hello Azure Cosmos DB package as well as all dependencies, such as Newtonsoft.Json.</span></span> <span data-ttu-id="104e2-159">Clique em **Okey** em Olá **visualização** janela, e **aceito** em Olá **a aceitação da licença** janela toocomplete Olá instalar.</span><span class="sxs-lookup"><span data-stu-id="104e2-159">Click **OK** in hello **Preview** window, and **I Accept** in hello **License Acceptance** window toocomplete hello install.</span></span>
   
    ![Captura de tela da janela Gerenciar pacotes NuGet Olá com hello biblioteca de cliente do Microsoft Azure DocumentDB realçado](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-install-nuget.png)
   
      <span data-ttu-id="104e2-161">Como alternativa, você pode usar Olá pacote de saudação tooinstall Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="104e2-161">Alternatively you can use hello Package Manager Console tooinstall hello package.</span></span> <span data-ttu-id="104e2-162">toodo caso, em Olá **ferramentas** menu, clique em **NuGet Package Manager**e, em seguida, clique em **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="104e2-162">toodo so, on hello **Tools** menu, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span> <span data-ttu-id="104e2-163">No prompt de hello, digite o seguinte hello.</span><span class="sxs-lookup"><span data-stu-id="104e2-163">At hello prompt, type hello following.</span></span>
   
        Install-Package Microsoft.Azure.DocumentDB
        
3. <span data-ttu-id="104e2-164">Depois de instalar o pacote de saudação, sua solução do Visual Studio deve se parecer com o seguinte Olá com duas novas referências adicionadas, Microsoft.Azure.Documents.Client e newtonsoft. JSON.</span><span class="sxs-lookup"><span data-stu-id="104e2-164">Once hello package is installed, your Visual Studio solution should resemble hello following with two new references added, Microsoft.Azure.Documents.Client and Newtonsoft.Json.</span></span>
   
    ![Captura de tela de duas referências de saudação adicionado o projeto de dados JSON toohello no Gerenciador de soluções](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-added-references.png)

## <span data-ttu-id="104e2-166"><a name="_Toc395637763"></a>Etapa 4: Configurar Olá aplicativo ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="104e2-166"><a name="_Toc395637763"></a>Step 4: Set up hello ASP.NET MVC application</span></span>
<span data-ttu-id="104e2-167">Agora vamos adicionar Olá modelos, exibições e controladores toothis MVC de aplicativos:</span><span class="sxs-lookup"><span data-stu-id="104e2-167">Now let's add hello models, views, and controllers toothis MVC application:</span></span>

* <span data-ttu-id="104e2-168">[Adicionar um modelo](#_Toc395637764).</span><span class="sxs-lookup"><span data-stu-id="104e2-168">[Add a model](#_Toc395637764).</span></span>
* <span data-ttu-id="104e2-169">[Adicionar um controlador](#_Toc395637765).</span><span class="sxs-lookup"><span data-stu-id="104e2-169">[Add a controller](#_Toc395637765).</span></span>
* <span data-ttu-id="104e2-170">[Adicionar exibições](#_Toc395637766).</span><span class="sxs-lookup"><span data-stu-id="104e2-170">[Add views](#_Toc395637766).</span></span>

### <span data-ttu-id="104e2-171"><a name="_Toc395637764"></a>Adicionar um modelo de dados JSON</span><span class="sxs-lookup"><span data-stu-id="104e2-171"><a name="_Toc395637764"></a>Add a JSON data model</span></span>
<span data-ttu-id="104e2-172">Vamos começar criando Olá **M** no MVC, Olá modelo.</span><span class="sxs-lookup"><span data-stu-id="104e2-172">Let's begin by creating hello **M** in MVC, hello model.</span></span> 

1. <span data-ttu-id="104e2-173">Em **Gerenciador de soluções**, Olá atalho **modelos** pasta, clique em **adicionar**e, em seguida, clique em **classe**.</span><span class="sxs-lookup"><span data-stu-id="104e2-173">In **Solution Explorer**, right-click hello **Models** folder, click **Add**, and then click **Class**.</span></span>
   
      <span data-ttu-id="104e2-174">Olá **Adicionar Novo Item** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="104e2-174">hello **Add New Item** dialog box appears.</span></span>
2. <span data-ttu-id="104e2-175">Nomeie a nova classe **Item.cs** e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="104e2-175">Name your new class **Item.cs** and click **Add**.</span></span> 
3. <span data-ttu-id="104e2-176">Neste novo **Item.cs** de arquivo, adicione o seguinte de saudação após Olá última *usando a instrução*.</span><span class="sxs-lookup"><span data-stu-id="104e2-176">In this new **Item.cs** file, add hello following after hello last *using statement*.</span></span>
   
        using Newtonsoft.Json;
4. <span data-ttu-id="104e2-177">Agora substitua este código</span><span class="sxs-lookup"><span data-stu-id="104e2-177">Now replace this code</span></span> 
   
        public class Item
        {
        }
   
    <span data-ttu-id="104e2-178">com hello código a seguir.</span><span class="sxs-lookup"><span data-stu-id="104e2-178">with hello following code.</span></span>
   
        public class Item
        {
            [JsonProperty(PropertyName = "id")]
            public string Id { get; set; }
   
            [JsonProperty(PropertyName = "name")]
            public string Name { get; set; }
   
            [JsonProperty(PropertyName = "description")]
            public string Description { get; set; }
   
            [JsonProperty(PropertyName = "isComplete")]
            public bool Completed { get; set; }
        }
   
    <span data-ttu-id="104e2-179">Todos os dados no banco de dados do Azure Cosmos é passada pela transmissão hello e armazenados como JSON.</span><span class="sxs-lookup"><span data-stu-id="104e2-179">All data in Azure Cosmos DB is passed over hello wire and stored as JSON.</span></span> <span data-ttu-id="104e2-180">forma de saudação toocontrol os objetos são serializados/desserializados por JSON.NET, você pode usar Olá **JsonProperty** atributo conforme demonstrado no hello **Item** classe que acabamos de criar.</span><span class="sxs-lookup"><span data-stu-id="104e2-180">toocontrol hello way your objects are serialized/deserialized by JSON.NET you can use hello **JsonProperty** attribute as demonstrated in hello **Item** class we just created.</span></span> <span data-ttu-id="104e2-181">Você não **ter** toodo isso mas deseja tooensure Minhas propriedades sigam Olá JSON camelCase convenções de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="104e2-181">You don't **have** toodo this but I want tooensure that my properties follow hello JSON camelCase naming conventions.</span></span> 
   
    <span data-ttu-id="104e2-182">Não só você pode controlar formato Olá Olá do nome da propriedade quando entra em JSON, mas é totalmente possível renomear suas propriedades .NET como fiz com hello **descrição** propriedade.</span><span class="sxs-lookup"><span data-stu-id="104e2-182">Not only can you control hello format of hello property name when it goes into JSON, but you can entirely rename your .NET properties like I did with hello **Description** property.</span></span> 

### <span data-ttu-id="104e2-183"><a name="_Toc395637765"></a>Adicionar um controlador</span><span class="sxs-lookup"><span data-stu-id="104e2-183"><a name="_Toc395637765"></a>Add a controller</span></span>
<span data-ttu-id="104e2-184">Que cuida da saudação **M**, agora vamos criar hello **C** no MVC, uma classe de controlador.</span><span class="sxs-lookup"><span data-stu-id="104e2-184">That takes care of hello **M**, now let's create hello **C** in MVC, a controller class.</span></span>

1. <span data-ttu-id="104e2-185">Em **Solution Explorer**, Olá do botão direito do mouse **controladores** pasta, clique em **adicionar**e, em seguida, clique em **controlador**.</span><span class="sxs-lookup"><span data-stu-id="104e2-185">In **Solution Explorer**, right-click hello **Controllers** folder, click **Add**, and then click **Controller**.</span></span>
   
    <span data-ttu-id="104e2-186">Olá **adicionar Scaffold** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="104e2-186">hello **Add Scaffold** dialog box appears.</span></span>
2. <span data-ttu-id="104e2-187">Selecione **Controlador MVC 5 - Vazio** e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="104e2-187">Select **MVC 5 Controller - Empty** and then click **Add**.</span></span>
   
    ![Captura de tela da caixa de diálogo Adicionar Scaffold Olá com hello controlador MVC 5 - opção vazia realçado](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-controller-add-scaffold.png)
3. <span data-ttu-id="104e2-189">Nomeie o novo Controlador, **ItemController.**</span><span class="sxs-lookup"><span data-stu-id="104e2-189">Name your new Controller, **ItemController.**</span></span>
   
    ![Captura de tela da caixa de diálogo Adicionar controlador Olá](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-controller.png)
   
    <span data-ttu-id="104e2-191">Depois de criar o arquivo hello, sua solução do Visual Studio deve ser semelhante a seguinte Olá com novo ItemController.cs arquivo hello em **Gerenciador de soluções**.</span><span class="sxs-lookup"><span data-stu-id="104e2-191">Once hello file is created, your Visual Studio solution should resemble hello following with hello new ItemController.cs file in **Solution Explorer**.</span></span> <span data-ttu-id="104e2-192">Olá Novo Item.cs arquivo criado anteriormente também é mostrado.</span><span class="sxs-lookup"><span data-stu-id="104e2-192">hello new Item.cs file created earlier is also shown.</span></span>
   
    ![Captura de tela de saudação solução do Visual Studio - Gerenciador de soluções com o novo arquivo. ItemController.cs hello e arquivo Item.cs realçado](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-item-solution-explorer.png)
   
    <span data-ttu-id="104e2-194">Você pode fechar ItemController.cs, voltaremos tooit mais tarde.</span><span class="sxs-lookup"><span data-stu-id="104e2-194">You can close ItemController.cs, we'll come back tooit later.</span></span> 

### <span data-ttu-id="104e2-195"><a name="_Toc395637766"></a>Adicionar exibições</span><span class="sxs-lookup"><span data-stu-id="104e2-195"><a name="_Toc395637766"></a>Add views</span></span>
<span data-ttu-id="104e2-196">Agora, vamos criar hello **V** no MVC, Olá modos de exibição:</span><span class="sxs-lookup"><span data-stu-id="104e2-196">Now, let's create hello **V** in MVC, hello views:</span></span>

* <span data-ttu-id="104e2-197">[Adicionar uma exibição Índice de Itens](#AddItemIndexView).</span><span class="sxs-lookup"><span data-stu-id="104e2-197">[Add an Item Index view](#AddItemIndexView).</span></span>
* <span data-ttu-id="104e2-198">[Adicionar uma exibição Novo Item](#AddNewIndexView).</span><span class="sxs-lookup"><span data-stu-id="104e2-198">[Add a New Item view](#AddNewIndexView).</span></span>
* <span data-ttu-id="104e2-199">[Adicionar uma exibição Editar Item](#_Toc395888515).</span><span class="sxs-lookup"><span data-stu-id="104e2-199">[Add an Edit Item view](#_Toc395888515).</span></span>

#### <span data-ttu-id="104e2-200"><a name="AddItemIndexView"></a>Adicionar uma exibição Índice de Itens</span><span class="sxs-lookup"><span data-stu-id="104e2-200"><a name="AddItemIndexView"></a>Add an Item Index view</span></span>
1. <span data-ttu-id="104e2-201">Em **Solution Explorer**, expanda Olá **exibições** pasta, com o botão direito Olá vazio **Item** pasta Visual Studio criado para você quando você adicionou Olá  **ItemController** anteriormente, clique em **adicionar**e, em seguida, clique em **exibição**.</span><span class="sxs-lookup"><span data-stu-id="104e2-201">In **Solution Explorer**, expand hello **Views**  folder, right-click hello empty **Item** folder that Visual Studio created for you when you added hello **ItemController** earlier, click **Add**, and then click **View**.</span></span>
   
    ![Captura de tela do Gerenciador de soluções mostrando a pasta de Item de saudação Visual Studio criado com comandos de exibição adicionar Olá realçados](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view.png)
2. <span data-ttu-id="104e2-203">Em Olá **adicionar exibição** caixa de diálogo caixa, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="104e2-203">In hello **Add View** dialog box, do hello following:</span></span>
   
   * <span data-ttu-id="104e2-204">Em Olá **nome de exibição** , digite ***índice***.</span><span class="sxs-lookup"><span data-stu-id="104e2-204">In hello **View name** box, type ***Index***.</span></span>
   * <span data-ttu-id="104e2-205">Em Olá **modelo** selecione ***lista***.</span><span class="sxs-lookup"><span data-stu-id="104e2-205">In hello **Template** box, select ***List***.</span></span>
   * <span data-ttu-id="104e2-206">Em Olá **classe modelo** selecione ***Item (todo. Modelos)***.</span><span class="sxs-lookup"><span data-stu-id="104e2-206">In hello **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="104e2-207">Na caixa de página de layout hello, digite ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="104e2-207">In hello layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
     
   ![Caixa de diálogo Adicionar modo de exibição do captura de tela mostrando Olá](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view-dialog.png)
3. <span data-ttu-id="104e2-209">Depois de definir todos esses valores, clique em **Adicionar** e deixe o Visual Studio criar uma nova exibição de modelo.</span><span class="sxs-lookup"><span data-stu-id="104e2-209">Once all these values are set, click **Add** and let Visual Studio create a new template view.</span></span> <span data-ttu-id="104e2-210">Quando terminar, ele será aberto Olá cshtml um arquivo criado.</span><span class="sxs-lookup"><span data-stu-id="104e2-210">Once it is done, it will open hello cshtml file  that was created.</span></span> <span data-ttu-id="104e2-211">Podemos pode fechar esse arquivo no Visual Studio como retornaremos tooit mais tarde.</span><span class="sxs-lookup"><span data-stu-id="104e2-211">We can close that file in Visual Studio as we will come back tooit later.</span></span>

#### <span data-ttu-id="104e2-212"><a name="AddNewIndexView"></a>Adicionar uma exibição Novo Item</span><span class="sxs-lookup"><span data-stu-id="104e2-212"><a name="AddNewIndexView"></a>Add a New Item view</span></span>
<span data-ttu-id="104e2-213">Toohow semelhante, criamos um **índice do Item** exibição, agora, vamos criar uma nova exibição para criar um novo **itens**.</span><span class="sxs-lookup"><span data-stu-id="104e2-213">Similar toohow we created an **Item Index** view, we will now create a new view for creating new **Items**.</span></span>

1. <span data-ttu-id="104e2-214">Em **Solution Explorer**, Olá do botão direito do mouse **Item** pasta novamente, clique em **adicionar**e, em seguida, clique em **exibição**.</span><span class="sxs-lookup"><span data-stu-id="104e2-214">In **Solution Explorer**, right-click hello **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="104e2-215">Em Olá **adicionar exibição** caixa de diálogo caixa, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="104e2-215">In hello **Add View** dialog box, do hello following:</span></span>
   
   * <span data-ttu-id="104e2-216">Em Olá **nome de exibição** , digite ***criar***.</span><span class="sxs-lookup"><span data-stu-id="104e2-216">In hello **View name** box, type ***Create***.</span></span>
   * <span data-ttu-id="104e2-217">Em Olá **modelo** selecione ***criar***.</span><span class="sxs-lookup"><span data-stu-id="104e2-217">In hello **Template** box, select ***Create***.</span></span>
   * <span data-ttu-id="104e2-218">Em Olá **classe modelo** selecione ***Item (todo. Modelos)***.</span><span class="sxs-lookup"><span data-stu-id="104e2-218">In hello **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="104e2-219">Na caixa de página de layout hello, digite ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="104e2-219">In hello layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="104e2-220">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="104e2-220">Click **Add**.</span></span>
   
#### <span data-ttu-id="104e2-221"><a name="_Toc395888515"></a>Adicionar uma exibição Editar Item</span><span class="sxs-lookup"><span data-stu-id="104e2-221"><a name="_Toc395888515"></a>Add an Edit Item view</span></span>
<span data-ttu-id="104e2-222">Finalmente, adicione um último modo de exibição para editar um **Item** em Olá mesma forma como antes.</span><span class="sxs-lookup"><span data-stu-id="104e2-222">And finally, add one last view for editing an **Item** in hello same way as before.</span></span>

1. <span data-ttu-id="104e2-223">Em **Solution Explorer**, Olá do botão direito do mouse **Item** pasta novamente, clique em **adicionar**e, em seguida, clique em **exibição**.</span><span class="sxs-lookup"><span data-stu-id="104e2-223">In **Solution Explorer**, right-click hello **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="104e2-224">Em Olá **adicionar exibição** caixa de diálogo caixa, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="104e2-224">In hello **Add View** dialog box, do hello following:</span></span>
   
   * <span data-ttu-id="104e2-225">Em Olá **nome de exibição** , digite ***editar***.</span><span class="sxs-lookup"><span data-stu-id="104e2-225">In hello **View name** box, type ***Edit***.</span></span>
   * <span data-ttu-id="104e2-226">Em Olá **modelo** selecione ***editar***.</span><span class="sxs-lookup"><span data-stu-id="104e2-226">In hello **Template** box, select ***Edit***.</span></span>
   * <span data-ttu-id="104e2-227">Em Olá **classe modelo** selecione ***Item (todo. Modelos)***.</span><span class="sxs-lookup"><span data-stu-id="104e2-227">In hello **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="104e2-228">Na caixa de página de layout hello, digite ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="104e2-228">In hello layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="104e2-229">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="104e2-229">Click **Add**.</span></span>

<span data-ttu-id="104e2-230">Depois que isso for feito, feche todos os documentos de cshtml de Olá no Visual Studio, como podemos retornarão exibições toothese mais tarde.</span><span class="sxs-lookup"><span data-stu-id="104e2-230">Once this is done, close all hello cshtml documents in Visual Studio as we will return toothese views later.</span></span>

## <span data-ttu-id="104e2-231"><a name="_Toc395637769"></a>Etapa 5: Conectar o Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="104e2-231"><a name="_Toc395637769"></a>Step 5: Wiring up Azure Cosmos DB</span></span>
<span data-ttu-id="104e2-232">Agora que é resolvido Olá MVC padronizado, vamos tooadding código de saudação para o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="104e2-232">Now that hello standard MVC stuff is taken care of, let's turn tooadding hello code for Azure Cosmos DB.</span></span> 

<span data-ttu-id="104e2-233">Nesta seção, vamos adicionar código seguinte de saudação do toohandle:</span><span class="sxs-lookup"><span data-stu-id="104e2-233">In this section, we'll add code toohandle hello following:</span></span>

* <span data-ttu-id="104e2-234">[Listando itens incompletos](#_Toc395637770).</span><span class="sxs-lookup"><span data-stu-id="104e2-234">[Listing incomplete Items](#_Toc395637770).</span></span>
* <span data-ttu-id="104e2-235">[Adicionando itens](#_Toc395637771).</span><span class="sxs-lookup"><span data-stu-id="104e2-235">[Adding Items](#_Toc395637771).</span></span>
* <span data-ttu-id="104e2-236">[Editando itens](#_Toc395637772).</span><span class="sxs-lookup"><span data-stu-id="104e2-236">[Editing Items](#_Toc395637772).</span></span>

### <span data-ttu-id="104e2-237"><a name="_Toc395637770"></a>Listando itens incompletos no seu aplicativo Web MVC</span><span class="sxs-lookup"><span data-stu-id="104e2-237"><a name="_Toc395637770"></a>Listing incomplete Items in your MVC web application</span></span>
<span data-ttu-id="104e2-238">Olá toodo coisa primeiro aqui é adicionar uma classe que contém todos os Olá lógica tooconnect tooand uso do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="104e2-238">hello first thing toodo here is add a class that contains all hello logic tooconnect tooand use Azure Cosmos DB.</span></span> <span data-ttu-id="104e2-239">Para este tutorial, será encapsular toda essa lógica na classe de repositório tooa chamado DocumentDBRepository.</span><span class="sxs-lookup"><span data-stu-id="104e2-239">For this tutorial we'll encapsulate all this logic in tooa repository class called DocumentDBRepository.</span></span> 

1. <span data-ttu-id="104e2-240">Em **Solution Explorer**, com o botão direito no projeto hello, clique em **adicionar**e, em seguida, clique em **classe**.</span><span class="sxs-lookup"><span data-stu-id="104e2-240">In **Solution Explorer**, right-click on hello project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="104e2-241">Nomeie a nova classe de saudação **DocumentDBRepository** e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="104e2-241">Name hello new class **DocumentDBRepository** and click **Add**.</span></span>
2. <span data-ttu-id="104e2-242">Em Olá recém-criado **DocumentDBRepository** classe e adicione o seguinte Olá *usando instruções* acima Olá *namespace* declaração</span><span class="sxs-lookup"><span data-stu-id="104e2-242">In hello newly created **DocumentDBRepository** class and add hello following *using statements* above hello *namespace* declaration</span></span>
   
        using Microsoft.Azure.Documents; 
        using Microsoft.Azure.Documents.Client; 
        using Microsoft.Azure.Documents.Linq; 
        using System.Configuration;
        using System.Linq.Expressions;
        using System.Threading.Tasks;
        using System.Net
        
    <span data-ttu-id="104e2-243">Agora substitua este código</span><span class="sxs-lookup"><span data-stu-id="104e2-243">Now replace this code</span></span> 
   
        public class DocumentDBRepository
        {
        }
   
    <span data-ttu-id="104e2-244">com hello código a seguir.</span><span class="sxs-lookup"><span data-stu-id="104e2-244">with hello following code.</span></span>
   
        public static class DocumentDBRepository<T> where T : class
        {
            private static readonly string DatabaseId = ConfigurationManager.AppSettings["database"];
            private static readonly string CollectionId = ConfigurationManager.AppSettings["collection"];
            private static DocumentClient client;
   
            public static void Initialize()
            {
                client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);
                CreateDatabaseIfNotExistsAsync().Wait();
                CreateCollectionIfNotExistsAsync().Wait();
            }
   
            private static async Task CreateDatabaseIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDatabaseAsync(UriFactory.CreateDatabaseUri(DatabaseId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
   
            private static async Task CreateCollectionIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDocumentCollectionAsync(
                            UriFactory.CreateDatabaseUri(DatabaseId),
                            new DocumentCollection { Id = CollectionId },
                            new RequestOptions { OfferThroughput = 1000 });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
        }
   
    
3. <span data-ttu-id="104e2-245">Estamos está lendo alguns valores de configuração, isso abra Olá **Web. config** arquivo do seu aplicativo e adicione Olá linhas em Olá seguintes `<AppSettings>` seção.</span><span class="sxs-lookup"><span data-stu-id="104e2-245">We're reading some values from configuration, so open hello **Web.config** file of your application and add hello following lines under hello `<AppSettings>` section.</span></span>
   
        <add key="endpoint" value="enter hello URI from hello Keys blade of hello Azure Portal"/>
        <add key="authKey" value="enter hello PRIMARY KEY, or hello SECONDARY KEY, from hello Keys blade of hello Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. <span data-ttu-id="104e2-246">Agora, atualize os valores hello para *ponto de extremidade* e *authKey* usando a folha de chaves de saudação do hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="104e2-246">Now, update hello values for *endpoint* and *authKey* using hello Keys blade of hello Azure Portal.</span></span> <span data-ttu-id="104e2-247">Use Olá **URI** da folha de chaves hello como valor de saudação de configuração de ponto de extremidade de saudação e use Olá **chave primária**, ou **chave SECUNDÁRIA** da folha de chaves hello como valor Olá Olá configuração de authKey.</span><span class="sxs-lookup"><span data-stu-id="104e2-247">Use hello **URI** from hello Keys blade as hello value of hello endpoint setting, and use hello **PRIMARY KEY**, or **SECONDARY KEY** from hello Keys blade as hello value of hello authKey setting.</span></span>

    <span data-ttu-id="104e2-248">Que cuida da conectando com o repositório de banco de dados do Azure Cosmos hello, agora vamos adicionar nossa lógica do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="104e2-248">That takes care of wiring up hello Azure Cosmos DB repository, now let's add our application logic.</span></span>

1. <span data-ttu-id="104e2-249">Olá primeiro queremos toodo capaz de toobe com um aplicativo de lista de tarefas é itens do toodisplay Olá incompletos.</span><span class="sxs-lookup"><span data-stu-id="104e2-249">hello first thing we want toobe able toodo with a todo list application is toodisplay hello incomplete items.</span></span>  <span data-ttu-id="104e2-250">Copie e cole Olá seguindo o trecho de código em qualquer lugar na Olá **DocumentDBRepository** classe.</span><span class="sxs-lookup"><span data-stu-id="104e2-250">Copy and paste hello following code snippet anywhere within hello **DocumentDBRepository** class.</span></span>
   
        public static async Task<IEnumerable<T>> GetItemsAsync(Expression<Func<T, bool>> predicate)
        {
            IDocumentQuery<T> query = client.CreateDocumentQuery<T>(
                UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId))
                .Where(predicate)
                .AsDocumentQuery();
   
            List<T> results = new List<T>();
            while (query.HasMoreResults)
            {
                results.AddRange(await query.ExecuteNextAsync<T>());
            }
   
            return results;
        }
2. <span data-ttu-id="104e2-251">Olá abrir **ItemController** é adicionada anteriormente e adicione o seguinte Olá *usando instruções* acima da declaração de namespace hello.</span><span class="sxs-lookup"><span data-stu-id="104e2-251">Open hello **ItemController** we added earlier and add hello following *using statements* above hello namespace declaration.</span></span>
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    <span data-ttu-id="104e2-252">Se seu projeto não é chamado de "todo", em seguida, você precisa tooupdate usando "todo. Modelos"; nome da saudação tooreflect de seu projeto.</span><span class="sxs-lookup"><span data-stu-id="104e2-252">If your project is not named "todo", then you need tooupdate using "todo.Models"; tooreflect hello name of your project.</span></span>
   
    <span data-ttu-id="104e2-253">Agora substitua este código</span><span class="sxs-lookup"><span data-stu-id="104e2-253">Now replace this code</span></span>
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    <span data-ttu-id="104e2-254">com hello código a seguir.</span><span class="sxs-lookup"><span data-stu-id="104e2-254">with hello following code.</span></span>
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. <span data-ttu-id="104e2-255">Abra **Global.asax.cs** e adicione Olá toohello linha a seguir **Application_Start** método</span><span class="sxs-lookup"><span data-stu-id="104e2-255">Open **Global.asax.cs** and add hello following line toohello **Application_Start** method</span></span> 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

<span data-ttu-id="104e2-256">Neste ponto, sua solução deve ser capaz de toobuild sem erros.</span><span class="sxs-lookup"><span data-stu-id="104e2-256">At this point your solution should be able toobuild without any errors.</span></span>

<span data-ttu-id="104e2-257">Se você tiver executado o aplicativo hello agora, você deve ir toohello **HomeController** e hello **índice** desse controlador de modo de exibição.</span><span class="sxs-lookup"><span data-stu-id="104e2-257">If you ran hello application now, you would go toohello **HomeController** and hello **Index** view of that controller.</span></span> <span data-ttu-id="104e2-258">Este é o comportamento padrão de saudação do projeto de modelo MVC Olá que escolhemos no início de saudação, mas não queremos que!</span><span class="sxs-lookup"><span data-stu-id="104e2-258">This is hello default behavior for hello MVC template project we chose at hello start but we don't want that!</span></span> <span data-ttu-id="104e2-259">Vamos alterar Olá roteamento neste tooalter de aplicativo MVC esse comportamento.</span><span class="sxs-lookup"><span data-stu-id="104e2-259">Let's change hello routing on this MVC application tooalter this behavior.</span></span>

<span data-ttu-id="104e2-260">Abra ***aplicativo\_Start\RouteConfig.cs*** e localize a linha hello começando com "padrões:" e alterá-la Olá tooresemble a seguir.</span><span class="sxs-lookup"><span data-stu-id="104e2-260">Open ***App\_Start\RouteConfig.cs*** and locate hello line starting with "defaults:" and change it tooresemble hello following.</span></span>

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

<span data-ttu-id="104e2-261">Agora diz que se você não especificou um valor toocontrol de URL Olá Olá comportamento que, em vez de roteamento ASP.NET MVC **início**, use **Item** como controlador de saudação e usuário **índice** como modo de exibição de saudação.</span><span class="sxs-lookup"><span data-stu-id="104e2-261">This now tells ASP.NET MVC that if you have not specified a value in hello URL toocontrol hello routing behavior that instead of **Home**, use **Item** as hello controller and user **Index** as hello view.</span></span>

<span data-ttu-id="104e2-262">Agora, se você executar o aplicativo hello, ele chamará o **ItemController** que será chamada na classe de repositório toohello e usar Olá GetItems método tooreturn todos os toohello de itens incompletos Olá **modos de exibição** \\ **Item**\\**índice** exibição.</span><span class="sxs-lookup"><span data-stu-id="104e2-262">Now if you run hello application, it will call into your **ItemController** which will call in toohello repository class and use hello GetItems method tooreturn all hello incomplete items toohello **Views**\\**Item**\\**Index** view.</span></span> 

<span data-ttu-id="104e2-263">Se você compilar e executar esse projeto agora, deverá ver algo parecido com isto.</span><span class="sxs-lookup"><span data-stu-id="104e2-263">If you build and run this project now, you should now see something that looks this.</span></span>    

![Captura de tela do aplicativo de web hello todo lista criado por este tutorial do banco de dados](./media/documentdb-dotnet-application/build-and-run-the-project-now.png)

### <span data-ttu-id="104e2-265"><a name="_Toc395637771"></a>Adicionando itens</span><span class="sxs-lookup"><span data-stu-id="104e2-265"><a name="_Toc395637771"></a>Adding Items</span></span>
<span data-ttu-id="104e2-266">Vamos colocar alguns itens no nosso banco de dados para que tenhamos algo mais que um toolook de grade vazia no.</span><span class="sxs-lookup"><span data-stu-id="104e2-266">Let's put some items into our database so we have something more than an empty grid toolook at.</span></span>

<span data-ttu-id="104e2-267">Vamos adicionar alguns códigos muito Azure Cosmos DBRepository e ItemController toopersist Olá o registro no banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="104e2-267">Let's add some code too Azure Cosmos DBRepository and ItemController toopersist hello record in Azure Cosmos DB.</span></span>

1. <span data-ttu-id="104e2-268">Adicionar Olá após o método tooyour **DocumentDBRepository** classe.</span><span class="sxs-lookup"><span data-stu-id="104e2-268">Add hello following method tooyour **DocumentDBRepository** class.</span></span>
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   <span data-ttu-id="104e2-269">Este método simplesmente pega um objeto passado tooit e ele é mantida no banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="104e2-269">This method simply takes an object passed tooit and persists it in Azure Cosmos DB.</span></span>
2. <span data-ttu-id="104e2-270">Abrir o arquivo de ItemController.cs hello e adicione Olá seguindo o trecho de código na classe hello.</span><span class="sxs-lookup"><span data-stu-id="104e2-270">Open hello ItemController.cs file and add hello following code snippet within hello class.</span></span> <span data-ttu-id="104e2-271">Isso é como o ASP.NET MVC sabe quais toodo para Olá **criar** ação.</span><span class="sxs-lookup"><span data-stu-id="104e2-271">This is how ASP.NET MVC knows what toodo for hello **Create** action.</span></span> <span data-ttu-id="104e2-272">Nesse caso renderização apenas Olá associados Create.cshtml exibição criada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="104e2-272">In this case just render hello associated Create.cshtml view created earlier.</span></span>
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    <span data-ttu-id="104e2-273">Agora precisamos de algum código mais neste controlador que aceitará o envio de saudação de saudação **criar** exibição.</span><span class="sxs-lookup"><span data-stu-id="104e2-273">We now need some more code in this controller that will accept hello submission from hello **Create** view.</span></span>
3. <span data-ttu-id="104e2-274">Adicione Olá próximo bloco de código toohello classe ItemController.cs que informa ao ASP.NET MVC que toodo um formulário POST para esse controlador.</span><span class="sxs-lookup"><span data-stu-id="104e2-274">Add hello next block of code toohello ItemController.cs class that tells ASP.NET MVC what toodo with a form POST for this controller.</span></span>
   
        [HttpPost]
        [ActionName("Create")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> CreateAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.CreateItemAsync(item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
    <span data-ttu-id="104e2-275">Esse código chama em toohello DocumentDBRepository e usa Olá CreateItemAsync método toopersist Olá novo todo item toohello banco de dados.</span><span class="sxs-lookup"><span data-stu-id="104e2-275">This code calls in toohello DocumentDBRepository and uses hello CreateItemAsync method toopersist hello new todo item toohello database.</span></span> 
   
    <span data-ttu-id="104e2-276">**Observação de segurança**: Olá **ValidateAntiForgeryToken** atributo é usado aqui toohelp proteger esse aplicativo contra ataques de falsificação de solicitação entre sites.</span><span class="sxs-lookup"><span data-stu-id="104e2-276">**Security Note**: hello **ValidateAntiForgeryToken** attribute is used here toohelp protect this application against cross-site request forgery attacks.</span></span> <span data-ttu-id="104e2-277">Não há mais tooit que apenas adicionar esse atributo, suas exibições necessário toowork com esse token antifalsificação também.</span><span class="sxs-lookup"><span data-stu-id="104e2-277">There is more tooit than just adding this attribute, your views need toowork with this anti-forgery token as well.</span></span> <span data-ttu-id="104e2-278">Para obter mais informações sobre o assunto hello e exemplos de como tooimplement isso corretamente, consulte [impedindo a falsificação de solicitação intersite][Preventing Cross-Site Request Forgery].</span><span class="sxs-lookup"><span data-stu-id="104e2-278">For more on hello subject, and examples of how tooimplement this correctly, please see [Preventing Cross-Site Request Forgery][Preventing Cross-Site Request Forgery].</span></span> <span data-ttu-id="104e2-279">Olá fornecido no código-fonte [GitHub] [ GitHub] tem implementação completa Olá em vigor.</span><span class="sxs-lookup"><span data-stu-id="104e2-279">hello source code provided on [GitHub][GitHub] has hello full implementation in place.</span></span>
   
    <span data-ttu-id="104e2-280">**Observação de segurança**: também usamos Olá **associar** atributo toohelp de parâmetro do método hello proteger contra ataques de lançamento excesso.</span><span class="sxs-lookup"><span data-stu-id="104e2-280">**Security Note**: We also use hello **Bind** attribute on hello method parameter toohelp protect against over-posting attacks.</span></span> <span data-ttu-id="104e2-281">Para obter mais detalhes, consulte [Basic CRUD Operations in ASP.NET MVC (Operações CRUD básicas no ASP.NET MVC)][Basic CRUD Operations in ASP.NET MVC].</span><span class="sxs-lookup"><span data-stu-id="104e2-281">For more details please see [Basic CRUD Operations in ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].</span></span>

<span data-ttu-id="104e2-282">Isso conclui Olá código necessário tooadd novos itens tooour banco de dados.</span><span class="sxs-lookup"><span data-stu-id="104e2-282">This concludes hello code required tooadd new Items tooour database.</span></span>

### <span data-ttu-id="104e2-283"><a name="_Toc395637772"></a>Editando itens</span><span class="sxs-lookup"><span data-stu-id="104e2-283"><a name="_Toc395637772"></a>Editing Items</span></span>
<span data-ttu-id="104e2-284">Há uma última coisa para que possamos toodo e que é tooadd Olá capacidade tooedit **itens** no banco de dados de saudação e toomark-los como concluída.</span><span class="sxs-lookup"><span data-stu-id="104e2-284">There is one last thing for us toodo, and that is tooadd hello ability tooedit **Items** in hello database and toomark them as complete.</span></span> <span data-ttu-id="104e2-285">Olá exibição para edição já foi adicionada toohello projeto, por isso, precisamos apenas tooadd alguns código controlador tooour e toohello **DocumentDBRepository** classe novamente.</span><span class="sxs-lookup"><span data-stu-id="104e2-285">hello view for editing was already added toohello project, so we just need tooadd some code tooour controller and toohello **DocumentDBRepository** class again.</span></span>

1. <span data-ttu-id="104e2-286">Adicionar Olá após toohello **DocumentDBRepository** classe.</span><span class="sxs-lookup"><span data-stu-id="104e2-286">Add hello following toohello **DocumentDBRepository** class.</span></span>
   
        public static async Task<Document> UpdateItemAsync(string id, T item)
        {
            return await client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id), item);
        }
   
        public static async Task<T> GetItemAsync(string id)
        {
            try
            {
                Document document = await client.ReadDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id));
                return (T)(dynamic)document;
            }
            catch (DocumentClientException e)
            {
                if (e.StatusCode == HttpStatusCode.NotFound)
                {
                    return null;
                }
                else
                {
                    throw;
                }
            }
        }
   
    <span data-ttu-id="104e2-287">Olá primeiro desses métodos, **GetItem** busca um Item do Azure Cosmos DB que é passado back toohello **ItemController** e, em seguida, em toohello **editar** exibição.</span><span class="sxs-lookup"><span data-stu-id="104e2-287">hello first of these methods, **GetItem** fetches an Item from Azure Cosmos DB which is passed back toohello **ItemController** and then on toohello **Edit** view.</span></span>
   
    <span data-ttu-id="104e2-288">Olá segundo dos métodos de saudação que acabamos de adicionar substitui Olá **documento** no banco de dados do Azure Cosmos com versão de saudação do hello **documento** passado do hello **ItemController**.</span><span class="sxs-lookup"><span data-stu-id="104e2-288">hello second of hello methods we just added replaces hello **Document** in Azure Cosmos DB with hello version of hello **Document** passed in from hello **ItemController**.</span></span>
2. <span data-ttu-id="104e2-289">Adicionar Olá após toohello **ItemController** classe.</span><span class="sxs-lookup"><span data-stu-id="104e2-289">Add hello following toohello **ItemController** class.</span></span>
   
        [HttpPost]
        [ActionName("Edit")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> EditAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.UpdateItemAsync(item.Id, item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
        [ActionName("Edit")]
        public async Task<ActionResult> EditAsync(string id)
        {
            if (id == null)
            {
                return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
            }
   
            Item item = await DocumentDBRepository<Item>.GetItemAsync(id);
            if (item == null)
            {
                return HttpNotFound();
            }
   
            return View(item);
        }
   
    <span data-ttu-id="104e2-290">Olá primeiro método trata Olá Http GET que acontece quando Olá usuário clica em Olá **editar** link da saudação **índice** exibição.</span><span class="sxs-lookup"><span data-stu-id="104e2-290">hello first method handles hello Http GET that happens when hello user clicks on hello **Edit** link from hello **Index** view.</span></span> <span data-ttu-id="104e2-291">Esse método busca um [ **documento** ](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) do banco de dados do Azure Cosmos e transmite toohello **editar** exibição.</span><span class="sxs-lookup"><span data-stu-id="104e2-291">This method fetches a [**Document**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) from Azure Cosmos DB and passes it toohello **Edit** view.</span></span>
   
    <span data-ttu-id="104e2-292">Olá **editar** exibição, em seguida, fará um Http POST toohello **IndexController**.</span><span class="sxs-lookup"><span data-stu-id="104e2-292">hello **Edit** view will then do an Http POST toohello **IndexController**.</span></span> 
   
    <span data-ttu-id="104e2-293">método segundo Hello, adicionamos identificadores passando Olá atualizado objeto tooAzure Cosmos DB toobe persistentes no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="104e2-293">hello second method we added handles passing hello updated object tooAzure Cosmos DB toobe persisted in hello database.</span></span>

<span data-ttu-id="104e2-294">Isto é, que é tudo que precisamos toorun nosso aplicativo, lista incompleta **itens**, adicionar novos **itens**e editar **itens**.</span><span class="sxs-lookup"><span data-stu-id="104e2-294">That's it, that is everything we need toorun our application, list incomplete **Items**, add new **Items**, and edit **Items**.</span></span>

## <span data-ttu-id="104e2-295"><a name="_Toc395637773"></a>Etapa 6: Executar aplicativo hello localmente</span><span class="sxs-lookup"><span data-stu-id="104e2-295"><a name="_Toc395637773"></a>Step 6: Run hello application locally</span></span>
<span data-ttu-id="104e2-296">aplicativo de hello tootest em seu computador local, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="104e2-296">tootest hello application on your local machine, do hello following:</span></span>

1. <span data-ttu-id="104e2-297">Pressione F5 no aplicativo do Visual Studio toobuild hello no modo de depuração.</span><span class="sxs-lookup"><span data-stu-id="104e2-297">Hit F5 in Visual Studio toobuild hello application in debug mode.</span></span> <span data-ttu-id="104e2-298">Ele deve criar um aplicativo hello e iniciar um navegador com a página de grade vazia Olá que vimos antes:</span><span class="sxs-lookup"><span data-stu-id="104e2-298">It should build hello application and launch a browser with hello empty grid page we saw before:</span></span>
   
    ![Captura de tela do aplicativo de web hello todo lista criado por este tutorial do banco de dados](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item-a.png)
   
     
2. <span data-ttu-id="104e2-300">Clique em Olá **criar novo** link e adicionar valores toohello **nome** e **descrição** campos.</span><span class="sxs-lookup"><span data-stu-id="104e2-300">Click hello **Create New** link and add values toohello **Name** and **Description** fields.</span></span> <span data-ttu-id="104e2-301">Deixe Olá **concluído** caixa de seleção desmarcada caso contrário Olá novo **Item** será adicionado em um estado concluído e não serão exibidos na lista de saudação inicial.</span><span class="sxs-lookup"><span data-stu-id="104e2-301">Leave hello **Completed** check box unselected otherwise hello new **Item** will be added in a completed state and will not appear on hello initial list.</span></span>
   
    ![Captura de tela de saudação Create view](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-new-item.png)
3. <span data-ttu-id="104e2-303">Clique em **criar** e são redirecionada toohello back **índice** exibição e o **Item** aparece na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="104e2-303">Click **Create** and you are redirected back toohello **Index** view and your **Item** appears in hello list.</span></span>
   
    ![Captura de tela de saudação exibição índice](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item.png)
   
    <span data-ttu-id="104e2-305">Sinta-se livre tooadd mais algumas **itens** tooyour lista de tarefas.</span><span class="sxs-lookup"><span data-stu-id="104e2-305">Feel free tooadd a few more **Items** tooyour todo list.</span></span>
    
4. <span data-ttu-id="104e2-306">Clique em **editar** tooan próximo **Item** em lista hello e ficam toohello **editar** exibição onde você pode atualizar qualquer propriedade de seu objeto, incluindo Olá  **Concluída** sinalizador.</span><span class="sxs-lookup"><span data-stu-id="104e2-306">Click **Edit** next tooan **Item** on hello list and you are taken toohello **Edit** view where you can update any property of your object, including hello **Completed** flag.</span></span> <span data-ttu-id="104e2-307">Se você marcar Olá **concluir** sinalizador e clique em **salvar**, Olá **Item** é removido da lista de saudação de tarefas não concluídas.</span><span class="sxs-lookup"><span data-stu-id="104e2-307">If you mark hello **Complete** flag and click **Save**, hello **Item** is removed from hello list of incomplete tasks.</span></span>
   
    ![Captura de tela de saudação visualização de índice com hello concluído caixa marcada](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-completed-item.png)
5. <span data-ttu-id="104e2-309">Depois de testar o aplicativo hello, pressione Ctrl + F5 toostop depurar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="104e2-309">Once you've tested hello app, press Ctrl+F5 toostop debugging hello app.</span></span> <span data-ttu-id="104e2-310">Você está pronto toodeploy!</span><span class="sxs-lookup"><span data-stu-id="104e2-310">You're ready toodeploy!</span></span>

## <span data-ttu-id="104e2-311"><a name="_Toc395637774"></a>Etapa 7: Implantar Olá tooAzure de aplicativo do serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="104e2-311"><a name="_Toc395637774"></a>Step 7: Deploy hello application tooAzure App Service</span></span> 
<span data-ttu-id="104e2-312">Agora que você tem o aplicativo completo Olá funcionando corretamente com o banco de dados do Azure Cosmos, vamos toodeploy este tooAzure do aplicativo web do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="104e2-312">Now that you have hello complete application working correctly with Azure Cosmos DB we're going toodeploy this web app tooAzure App Service.</span></span>  

1. <span data-ttu-id="104e2-313">toopublish esse aplicativo, todos os toodo é com o botão direito no projeto Olá no **Solution Explorer** e clique em **publicar**.</span><span class="sxs-lookup"><span data-stu-id="104e2-313">toopublish this application all you need toodo is right-click on hello project in **Solution Explorer** and click **Publish**.</span></span>
   
    ![Captura de tela de saudação opção Publicar no Gerenciador de soluções](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish.png)

2. <span data-ttu-id="104e2-315">Em Olá **publicar** caixa de diálogo, clique em **serviço de aplicativo do Microsoft Azure**, em seguida, selecione **criar novo** toocreate um aplicativo de serviço de perfil ou clique em **selecionar Existente** toouse um perfil existente.</span><span class="sxs-lookup"><span data-stu-id="104e2-315">In hello **Publish** dialog box, click **Microsoft Azure App Service**, then select **Create New** toocreate an App Service profile, or click **Select Existing** toouse an existing profile.</span></span>

    ![Caixa de diálogo Publicar no Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish-to-existing.png)

3. <span data-ttu-id="104e2-317">Se você tiver um perfil do Serviço de Aplicativo do Azure existente, digite o nome da assinatura.</span><span class="sxs-lookup"><span data-stu-id="104e2-317">If you have an existing Azure App Service profile, enter your subscription name.</span></span> <span data-ttu-id="104e2-318">Saudação de uso **exibição** toosort por grupo de recursos ou o tipo de recurso de filtro, selecione o serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="104e2-318">Use hello **View** filter toosort by resource group or resource type, then select your Azure App Service.</span></span> 
   
    ![Caixa de diálogo Serviço de Aplicativo no Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-app-service.png)

4. <span data-ttu-id="104e2-320">toocreate um novo perfil de serviço de aplicativo do Azure, clique em **criar novo** em Olá **publicar** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="104e2-320">toocreate a new Azure App Service profile, click **Create New** in hello **Publish** dialog box.</span></span> <span data-ttu-id="104e2-321">Em Olá **criar serviço de aplicativo** caixa de diálogo, digite seu nome do aplicativo Web e a assinatura apropriada, o grupo de recursos e o plano de serviço de aplicativo, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="104e2-321">In hello **Create App Service** dialog, enter your Web App name and appropriate subscription, resource group, and App Service plan, then click **Create**.</span></span>

    ![Caixa de diálogo Criar Serviço de Aplicativo no Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-app-service.png)

<span data-ttu-id="104e2-323">Em poucos segundos, o Visual Studio terminará de publicar seu aplicativo Web e iniciará um navegador no qual você poderá ver seu trabalho sendo executado no Azure!</span><span class="sxs-lookup"><span data-stu-id="104e2-323">In a few seconds, Visual Studio will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>



## <span data-ttu-id="104e2-324"><a name="_Toc395637775"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="104e2-324"><a name="_Toc395637775"></a>Next steps</span></span>
<span data-ttu-id="104e2-325">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="104e2-325">Congratulations!</span></span> <span data-ttu-id="104e2-326">Você acabou de criado o ASP.NET MVC primeiro aplicativo web usando o banco de dados do Azure Cosmos e publicá-la tooAzure.</span><span class="sxs-lookup"><span data-stu-id="104e2-326">You just built your first ASP.NET MVC web application using Azure Cosmos DB and published it tooAzure.</span></span> <span data-ttu-id="104e2-327">Olá código-fonte para o aplicativo concluído hello, incluindo detalhes hello e excluir funcionalidade que não foram incluídos neste tutorial pode ser baixado ou clonado de [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="104e2-327">hello source code for hello complete application, including hello detail and delete functionality that were not included in this tutorial can be downloaded or cloned from [GitHub][GitHub].</span></span> <span data-ttu-id="104e2-328">Então se você estiver interessado em Adicionar aplicativo tooyour, pegue código hello e adicioná-lo toothis aplicativo.</span><span class="sxs-lookup"><span data-stu-id="104e2-328">So if you're interested in adding that tooyour app, grab hello code and add it toothis app.</span></span>

<span data-ttu-id="104e2-329">aplicativo de tooyour tooadd funcionalidade adicional, Olá revisão APIs disponíveis no hello [biblioteca .NET do Azure Cosmos DB](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) e se sentir livre toocontribute toohello Azure Cosmos DB-Library do .NET em [GitHub] [GitHub].</span><span class="sxs-lookup"><span data-stu-id="104e2-329">tooadd additional functionality tooyour application, review hello APIs available in hello [Azure Cosmos DB .NET Library](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) and feel free toocontribute toohello Azure Cosmos DB .NET Library on [GitHub][GitHub].</span></span> 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app
