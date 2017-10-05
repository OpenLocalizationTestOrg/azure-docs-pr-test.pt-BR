---
title: 'Tutorial do ASP.NET MVC para Azure Cosmos DB: desenvolvimento de aplicativo Web | Microsoft Docs'
description: "Tutorial do ASP.NET MVC para criar um aplicativo Web MVC usando o Azure Cosmos DB. Você armazenará o JSON e acessará dados de um aplicativo de lista de tarefas pendentes hospedado em sites do Azure ‒ tutorial passo a passo do ASP NET MVC."
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
ms.openlocfilehash: 3f2950fe25feb8f3ee81cc0a79bf624f0ee33bd5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <span data-ttu-id="fd251-105"><a name="_Toc395809351"></a>Tutorial do ASP.NET MVC: desenvolvimento de aplicativo Web com o Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fd251-105"><a name="_Toc395809351"></a>ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fd251-106">.NET</span><span class="sxs-lookup"><span data-stu-id="fd251-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="fd251-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="fd251-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="fd251-108">Java</span><span class="sxs-lookup"><span data-stu-id="fd251-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="fd251-109">Python</span><span class="sxs-lookup"><span data-stu-id="fd251-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="fd251-110">Para destacar como você pode aproveitar com eficiência o Azure Cosmos DB para armazenar e consultar documentos JSON, este artigo fornece um passo a passo completo que mostra como compilar um aplicativo de lista de tarefas pendentes usando o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fd251-110">To highlight how you can efficiently leverage Azure Cosmos DB to store and query JSON documents, this article provides an end-to-end walk-through showing you how to build a todo app using Azure Cosmos DB.</span></span> <span data-ttu-id="fd251-111">As tarefas serão armazenadas como documentos JSON no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fd251-111">The tasks will be stored as JSON documents in Azure Cosmos DB.</span></span>

![Captura de tela do aplicativo Web de lista de tarefas pendentes criado por este tutorial - passo a passo do tutorial do ASP.NET MVC](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-image01.png)

<span data-ttu-id="fd251-113">Este passo a passo mostra como usar o serviço Azure Cosmos DB para armazenar e acessar dados por meio de um aplicativo Web ASP .NET MVC hospedado no Azure.</span><span class="sxs-lookup"><span data-stu-id="fd251-113">This walk-through shows you how to use the Azure Cosmos DB service to store and access data from an ASP.NET MVC web application hosted on Azure.</span></span> <span data-ttu-id="fd251-114">Se você estiver procurando um tutorial que se concentra somente no Azure Cosmos DB, e não nos componentes do ASP.NET MVC, confira [Criar um aplicativo de console em C# do Azure Cosmos DB](documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fd251-114">If you're looking for a tutorial that focuses only on Azure Cosmos DB, and not the ASP.NET MVC components, see [Build an Azure Cosmos DB C# console application](documentdb-get-started.md).</span></span>

> [!TIP]
> <span data-ttu-id="fd251-115">Este tutorial pressupõe que você tem experiência anterior com o ASP.NET MVC e com os Sites do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd251-115">This tutorial assumes that you have prior experience using ASP.NET MVC and Azure Websites.</span></span> <span data-ttu-id="fd251-116">Se estiver começando a usar o ASP.NET ou as [ferramentas que são pré-requisitos](#_Toc395637760), recomendamos baixar o projeto de exemplo completo do [GitHub][GitHub] e seguir as instruções nesse exemplo.</span><span class="sxs-lookup"><span data-stu-id="fd251-116">If you are new to ASP.NET or the [prerequisite tools](#_Toc395637760), we recommend downloading the complete sample project from [GitHub][GitHub] and following the instructions in this sample.</span></span> <span data-ttu-id="fd251-117">Depois de compilá-lo, você poderá consultar esse artigo para obter informações sobre o código no contexto do projeto.</span><span class="sxs-lookup"><span data-stu-id="fd251-117">Once you have it built, you can review this article to gain insight on the code in the context of the project.</span></span>
> 
> 

## <span data-ttu-id="fd251-118"><a name="_Toc395637760"></a>Pré-requisitos para este tutorial de banco de dados</span><span class="sxs-lookup"><span data-stu-id="fd251-118"><a name="_Toc395637760"></a>Prerequisites for this database tutorial</span></span>
<span data-ttu-id="fd251-119">Antes de seguir as instruções deste artigo, verifique se você possui o seguinte:</span><span class="sxs-lookup"><span data-stu-id="fd251-119">Before following the instructions in this article, you should ensure that you have the following:</span></span>

* <span data-ttu-id="fd251-120">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd251-120">An active Azure account.</span></span> <span data-ttu-id="fd251-121">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="fd251-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="fd251-122">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fd251-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

    <span data-ttu-id="fd251-123">OU</span><span class="sxs-lookup"><span data-stu-id="fd251-123">OR</span></span>

    <span data-ttu-id="fd251-124">Uma instalação local do [Emulador do Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="fd251-124">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="fd251-125">[Visual Studio 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="fd251-125">[Visual Studio 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="fd251-126">SDK do Microsoft Azure para .NET para Visual Studio 2017, disponível por meio do Instalador do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fd251-126">Microsoft Azure SDK for .NET for Visual Studio 2017, available through the Visual Studio Installer.</span></span>

<span data-ttu-id="fd251-127">As capturas de tela neste artigo foram feitas usando o Microsoft Visual Studio Community 2017.</span><span class="sxs-lookup"><span data-stu-id="fd251-127">All the screen shots in this article have been taken using Microsoft Visual Studio Community 2017.</span></span> <span data-ttu-id="fd251-128">Se o seu sistema estiver configurado com uma versão diferente, será possível que suas telas e opções não correspondam totalmente, mas se você cumprir os pré-requisitos acima, esta solução deverá funcionar.</span><span class="sxs-lookup"><span data-stu-id="fd251-128">If your system is configured with a different version it is possible that your screens and options won't match entirely, but if you meet the above prerequisites this solution should work.</span></span>

## <span data-ttu-id="fd251-129"><a name="_Toc395637761"></a>Etapa 1: Criar uma conta de banco de dados do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fd251-129"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="fd251-130">Vamos começar criando uma conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fd251-130">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="fd251-131">Se você já tiver uma conta do SQL (DocumentDB) para Azure Cosmos DB ou se estiver usando o Emulador do Azure Cosmos DB para este tutorial, pule para [Criar um novo aplicativo ASP .NET MVC](#_Toc395637762).</span><span class="sxs-lookup"><span data-stu-id="fd251-131">If you already have a SQL (DocumentDB) account for Azure Cosmos DB or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Create a new ASP.NET MVC application](#_Toc395637762).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

<br/>
<span data-ttu-id="fd251-132">Agora vamos abordar como criar um novo aplicativo ASP.NET MVC desde o início.</span><span class="sxs-lookup"><span data-stu-id="fd251-132">We will now walk through how to create a new ASP.NET MVC application from the ground-up.</span></span> 

## <span data-ttu-id="fd251-133"><a name="_Toc395637762"></a>Etapa 2: criar um novo aplicativo ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="fd251-133"><a name="_Toc395637762"></a>Step 2: Create a new ASP.NET MVC application</span></span>

1. <span data-ttu-id="fd251-134">No Visual Studio, no menu **Arquivo**, aponte para **Novo** e clique em **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="fd251-134">In Visual Studio, on the **File** menu, point to **New**, and then click **Project**.</span></span> <span data-ttu-id="fd251-135">A caixa de diálogo **Novo Projeto** aparecerá.</span><span class="sxs-lookup"><span data-stu-id="fd251-135">The **New Project** dialog box appears.</span></span>

2. <span data-ttu-id="fd251-136">No painel **Tipos de projeto**, expanda **Modelos**, **Visual C#**, **Web** e selecione **Aplicativo Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="fd251-136">In the **Project types** pane, expand **Templates**, **Visual C#**, **Web**, and then select **ASP.NET Web Application**.</span></span>

      ![Captura de tela da caixa de diálogo Novo Projeto com o tipo de projeto Aplicativo Web ASP.NET realçado](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-project-dialog.png)

3. <span data-ttu-id="fd251-138">Na caixa **Nome** , digite o nome do projeto.</span><span class="sxs-lookup"><span data-stu-id="fd251-138">In the **Name** box, type the name of the project.</span></span> <span data-ttu-id="fd251-139">Este tutorial usará o nome "todo".</span><span class="sxs-lookup"><span data-stu-id="fd251-139">This tutorial uses the name "todo".</span></span> <span data-ttu-id="fd251-140">Se você optar por usar algum outro nome, sempre que este tutorial falar do namespace todo, será preciso ajustar os exemplos de código fornecidos para usar o nome de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fd251-140">If you choose to use something other than this, then wherever this tutorial talks about the todo namespace, you need to adjust the provided code samples to use whatever you named your application.</span></span> 
4. <span data-ttu-id="fd251-141">Clique em **Procurar** para navegar até a pasta na qual você deseja criar o projeto e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="fd251-141">Click **Browse** to navigate to the folder where you would like to create the project, and then click **OK**.</span></span>
   
      <span data-ttu-id="fd251-142">A caixa de diálogo **Novo Aplicativo Web ASP .NET** aparece.</span><span class="sxs-lookup"><span data-stu-id="fd251-142">The **New ASP.NET Web Application** dialog box appears.</span></span>
   
    ![Captura de tela da caixa de diálogo Novo Aplicativo Web ASP .NET com o modelo de aplicativo MVC realçado](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-MVC.png)
5. <span data-ttu-id="fd251-144">No painel de modelos, selecione **MVC**.</span><span class="sxs-lookup"><span data-stu-id="fd251-144">In the templates pane, select **MVC**.</span></span>

6. <span data-ttu-id="fd251-145">Clique em **OK** e deixe o Visual Studio fazer isso realizando scaffolding do modelo ASP.NET MVC vazio.</span><span class="sxs-lookup"><span data-stu-id="fd251-145">Click **OK** and let Visual Studio do its thing around scaffolding the empty ASP.NET MVC template.</span></span> 

          
7. <span data-ttu-id="fd251-146">Depois que o Visual Studio concluir a criação do aplicativo MVC de texto clichê, você terá um aplicativo ASP.NET vazio que poderá ser executado localmente.</span><span class="sxs-lookup"><span data-stu-id="fd251-146">Once Visual Studio has finished creating the boilerplate MVC application you have an empty ASP.NET application that you can run locally.</span></span>
   
    <span data-ttu-id="fd251-147">Vamos ignorar a execução local do projeto porque tenho certeza de que vimos o aplicativo "Hello World" do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="fd251-147">We'll skip running the project locally because I'm sure we've all seen the ASP.NET "Hello World" application.</span></span> <span data-ttu-id="fd251-148">Vamos direto para a adição do Azure Cosmos DB a este projeto e para a compilação de nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fd251-148">Let's go straight to adding Azure Cosmos DB to this project and building our application.</span></span>

## <span data-ttu-id="fd251-149"><a name="_Toc395637767"></a>Etapa 3: Adicionar o Azure Cosmos DB ao seu projeto de aplicativo Web MVC</span><span class="sxs-lookup"><span data-stu-id="fd251-149"><a name="_Toc395637767"></a>Step 3: Add Azure Cosmos DB to your MVC web application project</span></span>
<span data-ttu-id="fd251-150">Agora que cuidamos da maioria dos detalhes técnicos do ASP.NET MVC necessários para esta solução, vamos para o verdadeiro propósito deste tutorial, que é adicionar o Azure Cosmos DB ao nosso aplicativo Web MVC.</span><span class="sxs-lookup"><span data-stu-id="fd251-150">Now that we have most of the ASP.NET MVC plumbing that we need for this solution, let's get to the real purpose of this tutorial, adding Azure Cosmos DB to our MVC web application.</span></span>

1. <span data-ttu-id="fd251-151">O SDK .NET do Azure Cosmos DB é empacotado e distribuído como um pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="fd251-151">The Azure Cosmos DB .NET SDK is packaged and distributed as a NuGet package.</span></span> <span data-ttu-id="fd251-152">Para obter o pacote NuGet no Visual Studio, use o gerenciador de pacotes NuGet no Visual Studio clicando com o botão direito do mouse no projeto no **Gerenciador de Soluções** e clicando em **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="fd251-152">To get the NuGet package in Visual Studio, use the NuGet package manager in Visual Studio by right-clicking on the project in **Solution Explorer** and then clicking **Manage NuGet Packages**.</span></span>
   
    ![Captura de tela das opções do botão direito do mouse para o projeto de aplicativo Web no Gerenciador de Soluções, com Gerenciar Pacotes NuGet realçado.](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-manage-nuget.png)
   
    <span data-ttu-id="fd251-154">A caixa de diálogo **Gerenciar Pacotes NuGet** será exibida.</span><span class="sxs-lookup"><span data-stu-id="fd251-154">The **Manage NuGet Packages** dialog box appears.</span></span>
2. <span data-ttu-id="fd251-155">Na caixa **Procurar** do NuGet, digite ***DocumentDB do Azure***.</span><span class="sxs-lookup"><span data-stu-id="fd251-155">In the NuGet **Browse** box, type ***Azure DocumentDB***.</span></span> <span data-ttu-id="fd251-156">(O nome do pacote não foi atualizado para o Azure Cosmos DB.)</span><span class="sxs-lookup"><span data-stu-id="fd251-156">(The package name has not been updated to Azure Cosmos DB.)</span></span>
   
    <span data-ttu-id="fd251-157">Com base nos resultados, instale o pacote da **Microsoft.Azure.DocumentDB da Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="fd251-157">From the results, install the **Microsoft.Azure.DocumentDB by Microsoft** package.</span></span> <span data-ttu-id="fd251-158">Essa ação baixará e instalará o pacote do Azure Cosmos DB, bem como todas as dependências, como Newtonsoft.Json.</span><span class="sxs-lookup"><span data-stu-id="fd251-158">This will download and install the Azure Cosmos DB package as well as all dependencies, such as Newtonsoft.Json.</span></span> <span data-ttu-id="fd251-159">Clique em **OK** na janela **Visualização** e em **Aceito** na janela **Aceitação da Licença** para concluir a instalação.</span><span class="sxs-lookup"><span data-stu-id="fd251-159">Click **OK** in the **Preview** window, and **I Accept** in the **License Acceptance** window to complete the install.</span></span>
   
    ![Captura de tela da janela Gerenciar Pacotes NuGet com a Biblioteca de Clientes do Microsoft Azure DocumentDB realçada](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-install-nuget.png)
   
      <span data-ttu-id="fd251-161">Como alternativa, você pode usar o Console do Gerenciador de Pacotes para instalar o pacote.</span><span class="sxs-lookup"><span data-stu-id="fd251-161">Alternatively you can use the Package Manager Console to install the package.</span></span> <span data-ttu-id="fd251-162">Para fazer isso, no menu **Ferramentas**, clique em **Gerenciador de Pacotes NuGet** e em **Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="fd251-162">To do so, on the **Tools** menu, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span> <span data-ttu-id="fd251-163">No prompt, digite o seguinte.</span><span class="sxs-lookup"><span data-stu-id="fd251-163">At the prompt, type the following.</span></span>
   
        Install-Package Microsoft.Azure.DocumentDB
        
3. <span data-ttu-id="fd251-164">Após o pacote ser instalado, sua solução do Visual Studio deverá se parecer com a seguinte, com duas novas referências adicionadas, Microsoft.Azure.Documents.Client e Newtonsoft.Json.</span><span class="sxs-lookup"><span data-stu-id="fd251-164">Once the package is installed, your Visual Studio solution should resemble the following with two new references added, Microsoft.Azure.Documents.Client and Newtonsoft.Json.</span></span>
   
    ![Captura de tela das duas referências adicionadas ao projeto de dados JSON no Gerenciador de Soluções](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-added-references.png)

## <span data-ttu-id="fd251-166"><a name="_Toc395637763"></a>Etapa 4: configurar o aplicativo ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="fd251-166"><a name="_Toc395637763"></a>Step 4: Set up the ASP.NET MVC application</span></span>
<span data-ttu-id="fd251-167">Agora vamos adicionar os modelos, as exibições e os controladores a este aplicativo MVC:</span><span class="sxs-lookup"><span data-stu-id="fd251-167">Now let's add the models, views, and controllers to this MVC application:</span></span>

* <span data-ttu-id="fd251-168">[Adicionar um modelo](#_Toc395637764).</span><span class="sxs-lookup"><span data-stu-id="fd251-168">[Add a model](#_Toc395637764).</span></span>
* <span data-ttu-id="fd251-169">[Adicionar um controlador](#_Toc395637765).</span><span class="sxs-lookup"><span data-stu-id="fd251-169">[Add a controller](#_Toc395637765).</span></span>
* <span data-ttu-id="fd251-170">[Adicionar exibições](#_Toc395637766).</span><span class="sxs-lookup"><span data-stu-id="fd251-170">[Add views](#_Toc395637766).</span></span>

### <span data-ttu-id="fd251-171"><a name="_Toc395637764"></a>Adicionar um modelo de dados JSON</span><span class="sxs-lookup"><span data-stu-id="fd251-171"><a name="_Toc395637764"></a>Add a JSON data model</span></span>
<span data-ttu-id="fd251-172">Vamos começar criando o **M** no MVC, o modelo.</span><span class="sxs-lookup"><span data-stu-id="fd251-172">Let's begin by creating the **M** in MVC, the model.</span></span> 

1. <span data-ttu-id="fd251-173">No **Gerenciador de Soluções**, clique com o botão direito do mouse na pasta **Modelos**, clique em **Adicionar** e em **Classe**.</span><span class="sxs-lookup"><span data-stu-id="fd251-173">In **Solution Explorer**, right-click the **Models** folder, click **Add**, and then click **Class**.</span></span>
   
      <span data-ttu-id="fd251-174">A caixa de diálogo **Adicionar Novo Item** aparecerá.</span><span class="sxs-lookup"><span data-stu-id="fd251-174">The **Add New Item** dialog box appears.</span></span>
2. <span data-ttu-id="fd251-175">Nomeie a nova classe **Item.cs** e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="fd251-175">Name your new class **Item.cs** and click **Add**.</span></span> 
3. <span data-ttu-id="fd251-176">Nesse novo arquivo **Item.cs** , adicione o seguinte depois da última *instrução using*.</span><span class="sxs-lookup"><span data-stu-id="fd251-176">In this new **Item.cs** file, add the following after the last *using statement*.</span></span>
   
        using Newtonsoft.Json;
4. <span data-ttu-id="fd251-177">Agora substitua este código</span><span class="sxs-lookup"><span data-stu-id="fd251-177">Now replace this code</span></span> 
   
        public class Item
        {
        }
   
    <span data-ttu-id="fd251-178">pelo código a seguir.</span><span class="sxs-lookup"><span data-stu-id="fd251-178">with the following code.</span></span>
   
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
   
    <span data-ttu-id="fd251-179">Todos os dados no Azure Cosmos DB são transferidos e armazenados como JSON.</span><span class="sxs-lookup"><span data-stu-id="fd251-179">All data in Azure Cosmos DB is passed over the wire and stored as JSON.</span></span> <span data-ttu-id="fd251-180">Para controlar a forma como seus objetos são serializados/desserializados pelo JSON.NET, você pode usar o atributo **JsonProperty**, como demonstrado na classe **Item** criada há pouco.</span><span class="sxs-lookup"><span data-stu-id="fd251-180">To control the way your objects are serialized/deserialized by JSON.NET you can use the **JsonProperty** attribute as demonstrated in the **Item** class we just created.</span></span> <span data-ttu-id="fd251-181">Você não é **obrigado** a fazer isso, mas quero garantir que minhas propriedades sigam as convenções de nomenclatura camelCase de JSON.</span><span class="sxs-lookup"><span data-stu-id="fd251-181">You don't **have** to do this but I want to ensure that my properties follow the JSON camelCase naming conventions.</span></span> 
   
    <span data-ttu-id="fd251-182">Além de poder controlar o formato do nome da propriedade quando ele entra no JSON, você também pode renomear totalmente as propriedades .NET, como fiz com a propriedade **Descrição** .</span><span class="sxs-lookup"><span data-stu-id="fd251-182">Not only can you control the format of the property name when it goes into JSON, but you can entirely rename your .NET properties like I did with the **Description** property.</span></span> 

### <span data-ttu-id="fd251-183"><a name="_Toc395637765"></a>Adicionar um controlador</span><span class="sxs-lookup"><span data-stu-id="fd251-183"><a name="_Toc395637765"></a>Add a controller</span></span>
<span data-ttu-id="fd251-184">Isso cuida do **M**. Agora vamos criar o **C** no MVC, uma classe de controlador.</span><span class="sxs-lookup"><span data-stu-id="fd251-184">That takes care of the **M**, now let's create the **C** in MVC, a controller class.</span></span>

1. <span data-ttu-id="fd251-185">No **Gerenciador de Soluções**, clique com o botão direito do mouse na pasta **Controladores**, clique em **Adicionar** e em **Controlador**.</span><span class="sxs-lookup"><span data-stu-id="fd251-185">In **Solution Explorer**, right-click the **Controllers** folder, click **Add**, and then click **Controller**.</span></span>
   
    <span data-ttu-id="fd251-186">A caixa de diálogo **Adicionar Scaffold** aparecerá.</span><span class="sxs-lookup"><span data-stu-id="fd251-186">The **Add Scaffold** dialog box appears.</span></span>
2. <span data-ttu-id="fd251-187">Selecione **Controlador MVC 5 - Vazio** e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="fd251-187">Select **MVC 5 Controller - Empty** and then click **Add**.</span></span>
   
    ![Captura de tela da caixa de diálogo Adicionar Scaffold com a opção Controlador MVC 5 - Vazio realçada](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-controller-add-scaffold.png)
3. <span data-ttu-id="fd251-189">Nomeie o novo Controlador, **ItemController.**</span><span class="sxs-lookup"><span data-stu-id="fd251-189">Name your new Controller, **ItemController.**</span></span>
   
    ![Captura de tela da caixa de diálogo Adicionar Controlador](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-controller.png)
   
    <span data-ttu-id="fd251-191">Após o arquivo ser criado, sua solução do Visual Studio deverá se parecer com a seguinte, com o novo arquivo ItemController.cs no **Gerenciador de Soluções**.</span><span class="sxs-lookup"><span data-stu-id="fd251-191">Once the file is created, your Visual Studio solution should resemble the following with the new ItemController.cs file in **Solution Explorer**.</span></span> <span data-ttu-id="fd251-192">O novo arquivo Item.cs criado anteriormente também é mostrado.</span><span class="sxs-lookup"><span data-stu-id="fd251-192">The new Item.cs file created earlier is also shown.</span></span>
   
    ![Captura de tela da solução do Visual Studio — Gerenciador de Soluções com o novo arquivo ItemController.cs e o arquivo Item.cs realçados](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-item-solution-explorer.png)
   
    <span data-ttu-id="fd251-194">Você pode fechar ItemController.cs, pois voltaremos a ele mais tarde.</span><span class="sxs-lookup"><span data-stu-id="fd251-194">You can close ItemController.cs, we'll come back to it later.</span></span> 

### <span data-ttu-id="fd251-195"><a name="_Toc395637766"></a>Adicionar exibições</span><span class="sxs-lookup"><span data-stu-id="fd251-195"><a name="_Toc395637766"></a>Add views</span></span>
<span data-ttu-id="fd251-196">Agora vamos criar o **V** no MVC, as exibições:</span><span class="sxs-lookup"><span data-stu-id="fd251-196">Now, let's create the **V** in MVC, the views:</span></span>

* <span data-ttu-id="fd251-197">[Adicionar uma exibição Índice de Itens](#AddItemIndexView).</span><span class="sxs-lookup"><span data-stu-id="fd251-197">[Add an Item Index view](#AddItemIndexView).</span></span>
* <span data-ttu-id="fd251-198">[Adicionar uma exibição Novo Item](#AddNewIndexView).</span><span class="sxs-lookup"><span data-stu-id="fd251-198">[Add a New Item view](#AddNewIndexView).</span></span>
* <span data-ttu-id="fd251-199">[Adicionar uma exibição Editar Item](#_Toc395888515).</span><span class="sxs-lookup"><span data-stu-id="fd251-199">[Add an Edit Item view](#_Toc395888515).</span></span>

#### <span data-ttu-id="fd251-200"><a name="AddItemIndexView"></a>Adicionar uma exibição Índice de Itens</span><span class="sxs-lookup"><span data-stu-id="fd251-200"><a name="AddItemIndexView"></a>Add an Item Index view</span></span>
1. <span data-ttu-id="fd251-201">No **Gerenciador de Soluções**, expanda a pasta **Exibições**, clique com o botão direito do mouse na pasta vazia **Item** que o Visual criou quando você adicionou **ItemController** anteriormente, clique em **Adicionar** e em **Exibição**.</span><span class="sxs-lookup"><span data-stu-id="fd251-201">In **Solution Explorer**, expand the **Views**  folder, right-click the empty **Item** folder that Visual Studio created for you when you added the **ItemController** earlier, click **Add**, and then click **View**.</span></span>
   
    ![Captura de tela do Gerenciador de Soluções mostrando a pasta Item que o Visual Studio criou com os comandos Adicionar Exibição realçados](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view.png)
2. <span data-ttu-id="fd251-203">Na caixa de diálogo **Adicionar Exibição** , faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="fd251-203">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="fd251-204">Na caixa **Nome da exibição**, digite ***Índice***.</span><span class="sxs-lookup"><span data-stu-id="fd251-204">In the **View name** box, type ***Index***.</span></span>
   * <span data-ttu-id="fd251-205">Na caixa **Modelo**, selecione ***Lista***.</span><span class="sxs-lookup"><span data-stu-id="fd251-205">In the **Template** box, select ***List***.</span></span>
   * <span data-ttu-id="fd251-206">Na caixa **Classe de modelo**, selecione ***Item (todo.Models)***.</span><span class="sxs-lookup"><span data-stu-id="fd251-206">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="fd251-207">Na caixa da página de layout, digite ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="fd251-207">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
     
   ![Captura de tela mostrando a caixa de diálogo Adicionar Exibição](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view-dialog.png)
3. <span data-ttu-id="fd251-209">Depois de definir todos esses valores, clique em **Adicionar** e deixe o Visual Studio criar uma nova exibição de modelo.</span><span class="sxs-lookup"><span data-stu-id="fd251-209">Once all these values are set, click **Add** and let Visual Studio create a new template view.</span></span> <span data-ttu-id="fd251-210">Feito isso, o arquivo cshtml criado será aberto.</span><span class="sxs-lookup"><span data-stu-id="fd251-210">Once it is done, it will open the cshtml file  that was created.</span></span> <span data-ttu-id="fd251-211">Podemos fechar esse arquivo no Visual Studio, pois voltaremos a ele mais tarde.</span><span class="sxs-lookup"><span data-stu-id="fd251-211">We can close that file in Visual Studio as we will come back to it later.</span></span>

#### <span data-ttu-id="fd251-212"><a name="AddNewIndexView"></a>Adicionar uma exibição Novo Item</span><span class="sxs-lookup"><span data-stu-id="fd251-212"><a name="AddNewIndexView"></a>Add a New Item view</span></span>
<span data-ttu-id="fd251-213">De forma semelhante à criação de uma exibição **Índice de Itens**, criaremos agora uma nova exibição para criar novos **Itens**.</span><span class="sxs-lookup"><span data-stu-id="fd251-213">Similar to how we created an **Item Index** view, we will now create a new view for creating new **Items**.</span></span>

1. <span data-ttu-id="fd251-214">No **Gerenciador de Soluções**, clique com o botão direito do mouse novamente na pasta **Item**, clique em **Adicionar** e em **Exibir**.</span><span class="sxs-lookup"><span data-stu-id="fd251-214">In **Solution Explorer**, right-click the **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="fd251-215">Na caixa de diálogo **Adicionar Exibição** , faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="fd251-215">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="fd251-216">Na caixa **Nome da exibição**, digite ***Criar***.</span><span class="sxs-lookup"><span data-stu-id="fd251-216">In the **View name** box, type ***Create***.</span></span>
   * <span data-ttu-id="fd251-217">Na caixa **Modelo**, selecione ***Criar***.</span><span class="sxs-lookup"><span data-stu-id="fd251-217">In the **Template** box, select ***Create***.</span></span>
   * <span data-ttu-id="fd251-218">Na caixa **Classe de modelo**, selecione ***Item (todo.Models)***.</span><span class="sxs-lookup"><span data-stu-id="fd251-218">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="fd251-219">Na caixa da página de layout, digite ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="fd251-219">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="fd251-220">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="fd251-220">Click **Add**.</span></span>
   
#### <span data-ttu-id="fd251-221"><a name="_Toc395888515"></a>Adicionar uma exibição Editar Item</span><span class="sxs-lookup"><span data-stu-id="fd251-221"><a name="_Toc395888515"></a>Add an Edit Item view</span></span>
<span data-ttu-id="fd251-222">E, por fim, adicione uma última exibição para editar um **Item** da mesma maneira que foi feita antes.</span><span class="sxs-lookup"><span data-stu-id="fd251-222">And finally, add one last view for editing an **Item** in the same way as before.</span></span>

1. <span data-ttu-id="fd251-223">No **Gerenciador de Soluções**, clique com o botão direito do mouse novamente na pasta **Item**, clique em **Adicionar** e em **Exibir**.</span><span class="sxs-lookup"><span data-stu-id="fd251-223">In **Solution Explorer**, right-click the **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="fd251-224">Na caixa de diálogo **Adicionar Exibição** , faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="fd251-224">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="fd251-225">Na caixa **Nome da exibição**, digite ***Editar***.</span><span class="sxs-lookup"><span data-stu-id="fd251-225">In the **View name** box, type ***Edit***.</span></span>
   * <span data-ttu-id="fd251-226">Na caixa **Modelo**, selecione ***Editar***.</span><span class="sxs-lookup"><span data-stu-id="fd251-226">In the **Template** box, select ***Edit***.</span></span>
   * <span data-ttu-id="fd251-227">Na caixa **Classe de modelo**, selecione ***Item (todo.Models)***.</span><span class="sxs-lookup"><span data-stu-id="fd251-227">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="fd251-228">Na caixa da página de layout, digite ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="fd251-228">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="fd251-229">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="fd251-229">Click **Add**.</span></span>

<span data-ttu-id="fd251-230">Feito isso, feche todos os documentos cshtml no Visual Studio, pois voltaremos a essas exibições mais tarde.</span><span class="sxs-lookup"><span data-stu-id="fd251-230">Once this is done, close all the cshtml documents in Visual Studio as we will return to these views later.</span></span>

## <span data-ttu-id="fd251-231"><a name="_Toc395637769"></a>Etapa 5: Conectar o Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fd251-231"><a name="_Toc395637769"></a>Step 5: Wiring up Azure Cosmos DB</span></span>
<span data-ttu-id="fd251-232">Agora que cuidamos das questões padrão do MVC, vamos adicionar o código do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fd251-232">Now that the standard MVC stuff is taken care of, let's turn to adding the code for Azure Cosmos DB.</span></span> 

<span data-ttu-id="fd251-233">Nesta seção, vamos adicionar código para tratar do seguinte:</span><span class="sxs-lookup"><span data-stu-id="fd251-233">In this section, we'll add code to handle the following:</span></span>

* <span data-ttu-id="fd251-234">[Listando itens incompletos](#_Toc395637770).</span><span class="sxs-lookup"><span data-stu-id="fd251-234">[Listing incomplete Items](#_Toc395637770).</span></span>
* <span data-ttu-id="fd251-235">[Adicionando itens](#_Toc395637771).</span><span class="sxs-lookup"><span data-stu-id="fd251-235">[Adding Items](#_Toc395637771).</span></span>
* <span data-ttu-id="fd251-236">[Editando itens](#_Toc395637772).</span><span class="sxs-lookup"><span data-stu-id="fd251-236">[Editing Items](#_Toc395637772).</span></span>

### <span data-ttu-id="fd251-237"><a name="_Toc395637770"></a>Listando itens incompletos no seu aplicativo Web MVC</span><span class="sxs-lookup"><span data-stu-id="fd251-237"><a name="_Toc395637770"></a>Listing incomplete Items in your MVC web application</span></span>
<span data-ttu-id="fd251-238">A primeira coisa a fazer aqui é adicionar uma classe que contenha toda a lógica para conectar e usar o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fd251-238">The first thing to do here is add a class that contains all the logic to connect to and use Azure Cosmos DB.</span></span> <span data-ttu-id="fd251-239">Para este tutorial, vamos encapsular toda essa lógica em uma classe de repositório chamada DocumentDBRepository.</span><span class="sxs-lookup"><span data-stu-id="fd251-239">For this tutorial we'll encapsulate all this logic in to a repository class called DocumentDBRepository.</span></span> 

1. <span data-ttu-id="fd251-240">No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto, clique em **Adicionar** e em **Classe**.</span><span class="sxs-lookup"><span data-stu-id="fd251-240">In **Solution Explorer**, right-click on the project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="fd251-241">Nomeie a nova classe **DocumentDBRepository** e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="fd251-241">Name the new class **DocumentDBRepository** and click **Add**.</span></span>
2. <span data-ttu-id="fd251-242">Na classe **DocumentDBRepository** recém-criada, adicione as seguintes *instruções using* acima da declaração de *namespace*</span><span class="sxs-lookup"><span data-stu-id="fd251-242">In the newly created **DocumentDBRepository** class and add the following *using statements* above the *namespace* declaration</span></span>
   
        using Microsoft.Azure.Documents; 
        using Microsoft.Azure.Documents.Client; 
        using Microsoft.Azure.Documents.Linq; 
        using System.Configuration;
        using System.Linq.Expressions;
        using System.Threading.Tasks;
        using System.Net
        
    <span data-ttu-id="fd251-243">Agora substitua este código</span><span class="sxs-lookup"><span data-stu-id="fd251-243">Now replace this code</span></span> 
   
        public class DocumentDBRepository
        {
        }
   
    <span data-ttu-id="fd251-244">pelo código a seguir.</span><span class="sxs-lookup"><span data-stu-id="fd251-244">with the following code.</span></span>
   
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
   
    
3. <span data-ttu-id="fd251-245">Estamos lendo alguns valores da configuração, por isso, abra o arquivo **Web.config** de seu aplicativo e adicione as linhas a seguir sob a seção `<AppSettings>`.</span><span class="sxs-lookup"><span data-stu-id="fd251-245">We're reading some values from configuration, so open the **Web.config** file of your application and add the following lines under the `<AppSettings>` section.</span></span>
   
        <add key="endpoint" value="enter the URI from the Keys blade of the Azure Portal"/>
        <add key="authKey" value="enter the PRIMARY KEY, or the SECONDARY KEY, from the Keys blade of the Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. <span data-ttu-id="fd251-246">Agora atualize os valores de *endpoint* e *authKey* usando a folha Chaves do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd251-246">Now, update the values for *endpoint* and *authKey* using the Keys blade of the Azure Portal.</span></span> <span data-ttu-id="fd251-247">Use o **URI** da folha Chaves como o valor da configuração endpoint e use a **CHAVE PRIMÁRIA** ou a **CHAVE SECUNDÁRIA** da folha Chaves como o valor da configuração authKey.</span><span class="sxs-lookup"><span data-stu-id="fd251-247">Use the **URI** from the Keys blade as the value of the endpoint setting, and use the **PRIMARY KEY**, or **SECONDARY KEY** from the Keys blade as the value of the authKey setting.</span></span>

    <span data-ttu-id="fd251-248">Isso trata de conectar o repositório do Azure Cosmos DB. Agora, vamos adicionar nossa lógica do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fd251-248">That takes care of wiring up the Azure Cosmos DB repository, now let's add our application logic.</span></span>

1. <span data-ttu-id="fd251-249">A primeira coisa que desejamos fazer com um aplicativo de lista de tarefas é exibir os itens incompletos.</span><span class="sxs-lookup"><span data-stu-id="fd251-249">The first thing we want to be able to do with a todo list application is to display the incomplete items.</span></span>  <span data-ttu-id="fd251-250">Copie e cole o seguinte trecho de código em qualquer lugar na classe **DocumentDBRepository** .</span><span class="sxs-lookup"><span data-stu-id="fd251-250">Copy and paste the following code snippet anywhere within the **DocumentDBRepository** class.</span></span>
   
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
2. <span data-ttu-id="fd251-251">Abra o **ItemController** que adicionamos anteriormente e adicione as seguintes *instruções using* acima a declaração de namespace.</span><span class="sxs-lookup"><span data-stu-id="fd251-251">Open the **ItemController** we added earlier and add the following *using statements* above the namespace declaration.</span></span>
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    <span data-ttu-id="fd251-252">Se o nome de seu projeto não for "todo", você precisará atualizar usando "todo.Models" de modo a refletir o nome do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="fd251-252">If your project is not named "todo", then you need to update using "todo.Models"; to reflect the name of your project.</span></span>
   
    <span data-ttu-id="fd251-253">Agora substitua este código</span><span class="sxs-lookup"><span data-stu-id="fd251-253">Now replace this code</span></span>
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    <span data-ttu-id="fd251-254">pelo código a seguir.</span><span class="sxs-lookup"><span data-stu-id="fd251-254">with the following code.</span></span>
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. <span data-ttu-id="fd251-255">Abra **Global.asax.cs** e adicione a seguinte linha ao método **Application_Start**</span><span class="sxs-lookup"><span data-stu-id="fd251-255">Open **Global.asax.cs** and add the following line to the **Application_Start** method</span></span> 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

<span data-ttu-id="fd251-256">Neste ponto, sua solução deve ser capaz de compilar sem erros.</span><span class="sxs-lookup"><span data-stu-id="fd251-256">At this point your solution should be able to build without any errors.</span></span>

<span data-ttu-id="fd251-257">Se você executou o aplicativo agora, deverá ir para o **HomeController** e para a exibição **Índice** desse controlador.</span><span class="sxs-lookup"><span data-stu-id="fd251-257">If you ran the application now, you would go to the **HomeController** and the **Index** view of that controller.</span></span> <span data-ttu-id="fd251-258">Esse é o comportamento padrão para o projeto do modelo MVC que escolhemos no início, mas não queremos isso!</span><span class="sxs-lookup"><span data-stu-id="fd251-258">This is the default behavior for the MVC template project we chose at the start but we don't want that!</span></span> <span data-ttu-id="fd251-259">Vamos alterar o roteamento neste aplicativo MVC para alterar seu comportamento.</span><span class="sxs-lookup"><span data-stu-id="fd251-259">Let's change the routing on this MVC application to alter this behavior.</span></span>

<span data-ttu-id="fd251-260">Abra ***App\_Start\RouteConfig.cs***, encontre a linha que começa com "defaults:" e altere-a para que se pareça com o seguinte.</span><span class="sxs-lookup"><span data-stu-id="fd251-260">Open ***App\_Start\RouteConfig.cs*** and locate the line starting with "defaults:" and change it to resemble the following.</span></span>

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

<span data-ttu-id="fd251-261">Agora isso informa ao ASP.NET MVC que se você não especificou um valor na URL para controlar o comportamento de roteamento que, em vez de **Home**, usa **Item** como controlador e o usuário **Índice** como exibição.</span><span class="sxs-lookup"><span data-stu-id="fd251-261">This now tells ASP.NET MVC that if you have not specified a value in the URL to control the routing behavior that instead of **Home**, use **Item** as the controller and user **Index** as the view.</span></span>

<span data-ttu-id="fd251-262">Agora, se você executar o aplicativo, ele chamará o **ItemController** que chamará a classe de repositório e usará o método GetItems para retornar todos os itens incompletos para a exibição **Exibições**\\**Item**\\**Índice**.</span><span class="sxs-lookup"><span data-stu-id="fd251-262">Now if you run the application, it will call into your **ItemController** which will call in to the repository class and use the GetItems method to return all the incomplete items to the **Views**\\**Item**\\**Index** view.</span></span> 

<span data-ttu-id="fd251-263">Se você compilar e executar esse projeto agora, deverá ver algo parecido com isto.</span><span class="sxs-lookup"><span data-stu-id="fd251-263">If you build and run this project now, you should now see something that looks this.</span></span>    

![Captura de tela do aplicativo Web de lista de tarefas pendentes criado por este tutorial de banco de dados](./media/documentdb-dotnet-application/build-and-run-the-project-now.png)

### <span data-ttu-id="fd251-265"><a name="_Toc395637771"></a>Adicionando itens</span><span class="sxs-lookup"><span data-stu-id="fd251-265"><a name="_Toc395637771"></a>Adding Items</span></span>
<span data-ttu-id="fd251-266">Vamos colocar alguns itens em nosso banco de dados; assim, temos alguma coisa além de uma grade vazia para observar.</span><span class="sxs-lookup"><span data-stu-id="fd251-266">Let's put some items into our database so we have something more than an empty grid to look at.</span></span>

<span data-ttu-id="fd251-267">Vamos adicionar um código a DBRepository e ItemController do Cosmos do Azure para persistir o registro no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fd251-267">Let's add some code to  Azure Cosmos DBRepository and ItemController to persist the record in Azure Cosmos DB.</span></span>

1. <span data-ttu-id="fd251-268">Adicione o seguinte método à classe **DocumentDBRepository** .</span><span class="sxs-lookup"><span data-stu-id="fd251-268">Add the following method to your **DocumentDBRepository** class.</span></span>
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   <span data-ttu-id="fd251-269">Este método simplesmente pega algum objeto passado para ele e persiste-o no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fd251-269">This method simply takes an object passed to it and persists it in Azure Cosmos DB.</span></span>
2. <span data-ttu-id="fd251-270">Abra o arquivo ItemController.cs e adicione o seguinte trecho de código à classe.</span><span class="sxs-lookup"><span data-stu-id="fd251-270">Open the ItemController.cs file and add the following code snippet within the class.</span></span> <span data-ttu-id="fd251-271">É assim que o ASP.NET MVC passa a saber o que fazer para a ação **Criar** .</span><span class="sxs-lookup"><span data-stu-id="fd251-271">This is how ASP.NET MVC knows what to do for the **Create** action.</span></span> <span data-ttu-id="fd251-272">Nesse caso, basta renderizar a exibição de Create.cshtml associada criada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fd251-272">In this case just render the associated Create.cshtml view created earlier.</span></span>
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    <span data-ttu-id="fd251-273">Agora precisamos colocar mais alguns códigos neste controlador, os quais aceitarão o envio pela exibição **Criar** .</span><span class="sxs-lookup"><span data-stu-id="fd251-273">We now need some more code in this controller that will accept the submission from the **Create** view.</span></span>
3. <span data-ttu-id="fd251-274">Adicione o próximo bloco de código à classe ItemController.cs que diz ao ASP.NET MVC o que fazer com um formulário POST para esse controlador.</span><span class="sxs-lookup"><span data-stu-id="fd251-274">Add the next block of code to the ItemController.cs class that tells ASP.NET MVC what to do with a form POST for this controller.</span></span>
   
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
   
    <span data-ttu-id="fd251-275">Esse código chama o DocumentDBRepository e usa o método CreateItemAsync para manter o novo item de todo no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="fd251-275">This code calls in to the DocumentDBRepository and uses the CreateItemAsync method to persist the new todo item to the database.</span></span> 
   
    <span data-ttu-id="fd251-276">**Observação de segurança**: o atributo **ValidateAntiForgeryToken** é usado aqui para ajudar a proteger esse aplicativo contra ataques de solicitação entre sites forjada.</span><span class="sxs-lookup"><span data-stu-id="fd251-276">**Security Note**: The **ValidateAntiForgeryToken** attribute is used here to help protect this application against cross-site request forgery attacks.</span></span> <span data-ttu-id="fd251-277">Há mais do que apenas adicionar esse atributo, as exibições precisam trabalhar com esse token antifalsificação também.</span><span class="sxs-lookup"><span data-stu-id="fd251-277">There is more to it than just adding this attribute, your views need to work with this anti-forgery token as well.</span></span> <span data-ttu-id="fd251-278">Para saber mais sobre o assunto e ver exemplos de como implementar isso corretamente, veja [Preventing Cross-Site Request Forgery (Prevenindo solicitação intersite forjada)][Preventing Cross-Site Request Forgery].</span><span class="sxs-lookup"><span data-stu-id="fd251-278">For more on the subject, and examples of how to implement this correctly, please see [Preventing Cross-Site Request Forgery][Preventing Cross-Site Request Forgery].</span></span> <span data-ttu-id="fd251-279">O código-fonte fornecido no [GitHub][GitHub] tem a implementação completa estabelecida.</span><span class="sxs-lookup"><span data-stu-id="fd251-279">The source code provided on [GitHub][GitHub] has the full implementation in place.</span></span>
   
    <span data-ttu-id="fd251-280">**Observação de segurança**: também usamos o atributo **Bind** no parâmetro de método para ajudar na proteção contra ataques de overposting.</span><span class="sxs-lookup"><span data-stu-id="fd251-280">**Security Note**: We also use the **Bind** attribute on the method parameter to help protect against over-posting attacks.</span></span> <span data-ttu-id="fd251-281">Para obter mais detalhes, consulte [Basic CRUD Operations in ASP.NET MVC (Operações CRUD básicas no ASP.NET MVC)][Basic CRUD Operations in ASP.NET MVC].</span><span class="sxs-lookup"><span data-stu-id="fd251-281">For more details please see [Basic CRUD Operations in ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].</span></span>

<span data-ttu-id="fd251-282">Isso conclui o código exigido para adicionar novos itens ao nosso banco de dados.</span><span class="sxs-lookup"><span data-stu-id="fd251-282">This concludes the code required to add new Items to our database.</span></span>

### <span data-ttu-id="fd251-283"><a name="_Toc395637772"></a>Editando itens</span><span class="sxs-lookup"><span data-stu-id="fd251-283"><a name="_Toc395637772"></a>Editing Items</span></span>
<span data-ttu-id="fd251-284">Existe uma última ação para realizarmos, que é adicionar a capacidade de editar **Itens** no banco de dados e marcá-los como concluídos.</span><span class="sxs-lookup"><span data-stu-id="fd251-284">There is one last thing for us to do, and that is to add the ability to edit **Items** in the database and to mark them as complete.</span></span> <span data-ttu-id="fd251-285">A exibição para edição já foi adicionada ao projeto, desse modo, basta adicionar algum código ao nosso Controlador e à classe **DocumentDBRepository** novamente.</span><span class="sxs-lookup"><span data-stu-id="fd251-285">The view for editing was already added to the project, so we just need to add some code to our controller and to the **DocumentDBRepository** class again.</span></span>

1. <span data-ttu-id="fd251-286">Adicione o seguinte à classe **DocumentDBRepository** .</span><span class="sxs-lookup"><span data-stu-id="fd251-286">Add the following to the **DocumentDBRepository** class.</span></span>
   
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
   
    <span data-ttu-id="fd251-287">O primeiro desses métodos, **GetItem**, busca um Item do Azure Cosmos DB que é transferido de volta para o **ItemController** e, depois, para a exibição **Editar**.</span><span class="sxs-lookup"><span data-stu-id="fd251-287">The first of these methods, **GetItem** fetches an Item from Azure Cosmos DB which is passed back to the **ItemController** and then on to the **Edit** view.</span></span>
   
    <span data-ttu-id="fd251-288">O segundo método que acabamos de adicionar substitui o **Documento** no Azure Cosmos DB pela versão do **Documento** transferida do **ItemController**.</span><span class="sxs-lookup"><span data-stu-id="fd251-288">The second of the methods we just added replaces the **Document** in Azure Cosmos DB with the version of the **Document** passed in from the **ItemController**.</span></span>
2. <span data-ttu-id="fd251-289">Adicione o seguinte à classe **ItemController** .</span><span class="sxs-lookup"><span data-stu-id="fd251-289">Add the following to the **ItemController** class.</span></span>
   
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
   
    <span data-ttu-id="fd251-290">O primeiro método lida com o Http GET que ocorrerá quando o usuário clicar no link **Editar** na exibição **Índice**.</span><span class="sxs-lookup"><span data-stu-id="fd251-290">The first method handles the Http GET that happens when the user clicks on the **Edit** link from the **Index** view.</span></span> <span data-ttu-id="fd251-291">Esse método busca um [**Documento**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) do Azure Cosmos DB e o transfere para a exibição **Editar**.</span><span class="sxs-lookup"><span data-stu-id="fd251-291">This method fetches a [**Document**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) from Azure Cosmos DB and passes it to the **Edit** view.</span></span>
   
    <span data-ttu-id="fd251-292">Em seguida, a exibição **Editar** fará um Http POST para o **IndexController**.</span><span class="sxs-lookup"><span data-stu-id="fd251-292">The **Edit** view will then do an Http POST to the **IndexController**.</span></span> 
   
    <span data-ttu-id="fd251-293">O segundo método que adicionamos lida com isso transferindo objeto atualizado por meio do Azure Cosmos DB para que seja persistido no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="fd251-293">The second method we added handles passing the updated object to Azure Cosmos DB to be persisted in the database.</span></span>

<span data-ttu-id="fd251-294">Ou seja, isso é tudo que precisamos para executar nosso aplicativo, listar **Itens** incompletos, adicionar novos **Itens** e editar **Itens**.</span><span class="sxs-lookup"><span data-stu-id="fd251-294">That's it, that is everything we need to run our application, list incomplete **Items**, add new **Items**, and edit **Items**.</span></span>

## <span data-ttu-id="fd251-295"><a name="_Toc395637773"></a>Etapa 6: executar o aplicativo localmente</span><span class="sxs-lookup"><span data-stu-id="fd251-295"><a name="_Toc395637773"></a>Step 6: Run the application locally</span></span>
<span data-ttu-id="fd251-296">Para testar o aplicativo em seu computador local, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="fd251-296">To test the application on your local machine, do the following:</span></span>

1. <span data-ttu-id="fd251-297">Pressione F5 no Visual Studio para compilar o aplicativo no modo de depuração.</span><span class="sxs-lookup"><span data-stu-id="fd251-297">Hit F5 in Visual Studio to build the application in debug mode.</span></span> <span data-ttu-id="fd251-298">Ele deve compilar o aplicativo e iniciar um navegador com a página de grade vazia que vimos anteriormente:</span><span class="sxs-lookup"><span data-stu-id="fd251-298">It should build the application and launch a browser with the empty grid page we saw before:</span></span>
   
    ![Captura de tela do aplicativo Web de lista de tarefas pendentes criado por este tutorial de banco de dados](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item-a.png)
   
     
2. <span data-ttu-id="fd251-300">Clique no link **Criar Novo** e adicione valores ao campos **Nome** e **Descrição**.</span><span class="sxs-lookup"><span data-stu-id="fd251-300">Click the **Create New** link and add values to the **Name** and **Description** fields.</span></span> <span data-ttu-id="fd251-301">Deixe a caixa de seleção **Concluído** desmarcada, caso contrário, o novo **Item** será adicionado em um estado concluído e não aparecerá na lista inicial.</span><span class="sxs-lookup"><span data-stu-id="fd251-301">Leave the **Completed** check box unselected otherwise the new **Item** will be added in a completed state and will not appear on the initial list.</span></span>
   
    ![Captura de tela da exibição Criar](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-new-item.png)
3. <span data-ttu-id="fd251-303">Clique em **Criar** e você será redirecionado de volta à exibição **Índice** e seu **Item** aparecerá na lista.</span><span class="sxs-lookup"><span data-stu-id="fd251-303">Click **Create** and you are redirected back to the **Index** view and your **Item** appears in the list.</span></span>
   
    ![Captura de tela da exibição Índice](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item.png)
   
    <span data-ttu-id="fd251-305">Fique à vontade para adicionar mais alguns **Itens** à sua lista de tarefas pendentes.</span><span class="sxs-lookup"><span data-stu-id="fd251-305">Feel free to add a few more **Items** to your todo list.</span></span>
    
4. <span data-ttu-id="fd251-306">Clique em **Editar** perto de um **Item** na lista e você será levado para a exibição **Editar**, na qual poderá atualizar qualquer propriedade do objeto, incluindo o sinalizador **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="fd251-306">Click **Edit** next to an **Item** on the list and you are taken to the **Edit** view where you can update any property of your object, including the **Completed** flag.</span></span> <span data-ttu-id="fd251-307">Se você marcar o sinalizador **Concluir** e clicar em **Salvar**, o **Item** será removido da lista de tarefas incompletas.</span><span class="sxs-lookup"><span data-stu-id="fd251-307">If you mark the **Complete** flag and click **Save**, the **Item** is removed from the list of incomplete tasks.</span></span>
   
    ![Captura de tela da exibição Índice com a caixa Concluído marcada](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-completed-item.png)
5. <span data-ttu-id="fd251-309">Depois de testar o aplicativo, pressione Ctrl + F5 para parar a depuração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fd251-309">Once you've tested the app, press Ctrl+F5 to stop debugging the app.</span></span> <span data-ttu-id="fd251-310">Você está pronto para implantar!</span><span class="sxs-lookup"><span data-stu-id="fd251-310">You're ready to deploy!</span></span>

## <span data-ttu-id="fd251-311"><a name="_Toc395637774"></a>Etapa 7: implantar o aplicativo no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="fd251-311"><a name="_Toc395637774"></a>Step 7: Deploy the application to Azure App Service</span></span> 
<span data-ttu-id="fd251-312">Agora que você tem o aplicativo completo funcionando corretamente no Azure Cosmos DB, vamos implantar esse aplicativo Web no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd251-312">Now that you have the complete application working correctly with Azure Cosmos DB we're going to deploy this web app to Azure App Service.</span></span>  

1. <span data-ttu-id="fd251-313">Para publicar esse aplicativo, basta clicar com o botão direito do mouse no projeto no **Gerenciador de Soluções** e clicar em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="fd251-313">To publish this application all you need to do is right-click on the project in **Solution Explorer** and click **Publish**.</span></span>
   
    ![Captura de tela da opção Publicar no Gerenciador de Soluções](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish.png)

2. <span data-ttu-id="fd251-315">Na caixa de diálogo **Publicar**, clique em **Serviço de Aplicativo do Microsoft Azure**, em seguida, selecione **Criar Novo** para criar um perfil de Serviço de Aplicativo ou clique em **Selecionar Existente** para usar um perfil existente.</span><span class="sxs-lookup"><span data-stu-id="fd251-315">In the **Publish** dialog box, click **Microsoft Azure App Service**, then select **Create New** to create an App Service profile, or click **Select Existing** to use an existing profile.</span></span>

    ![Caixa de diálogo Publicar no Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish-to-existing.png)

3. <span data-ttu-id="fd251-317">Se você tiver um perfil do Serviço de Aplicativo do Azure existente, digite o nome da assinatura.</span><span class="sxs-lookup"><span data-stu-id="fd251-317">If you have an existing Azure App Service profile, enter your subscription name.</span></span> <span data-ttu-id="fd251-318">Use o filtro **Exibição** para classificar por tipo de recurso ou grupo de recursos, depois selecione o Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd251-318">Use the **View** filter to sort by resource group or resource type, then select your Azure App Service.</span></span> 
   
    ![Caixa de diálogo Serviço de Aplicativo no Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-app-service.png)

4. <span data-ttu-id="fd251-320">Para criar um novo perfil do Serviço de Aplicativo do Azure, clique em **Criar Novo** na caixa de diálogo **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="fd251-320">To create a new Azure App Service profile, click **Create New** in the **Publish** dialog box.</span></span> <span data-ttu-id="fd251-321">Na caixa de diálogo **Criar Serviço de Aplicativo**, digite seu nome do aplicativo Web e a assinatura apropriada, o grupo de recursos e o plano de Serviço de Aplicativo e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="fd251-321">In the **Create App Service** dialog, enter your Web App name and appropriate subscription, resource group, and App Service plan, then click **Create**.</span></span>

    ![Caixa de diálogo Criar Serviço de Aplicativo no Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-app-service.png)

<span data-ttu-id="fd251-323">Em poucos segundos, o Visual Studio terminará de publicar seu aplicativo Web e iniciará um navegador no qual você poderá ver seu trabalho sendo executado no Azure!</span><span class="sxs-lookup"><span data-stu-id="fd251-323">In a few seconds, Visual Studio will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>



## <span data-ttu-id="fd251-324"><a name="_Toc395637775"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fd251-324"><a name="_Toc395637775"></a>Next steps</span></span>
<span data-ttu-id="fd251-325">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="fd251-325">Congratulations!</span></span> <span data-ttu-id="fd251-326">Você acabou de compilar seu primeiro aplicativo Web ASP .NET MVC usando o Azure Cosmos DB e o publicou no Azure.</span><span class="sxs-lookup"><span data-stu-id="fd251-326">You just built your first ASP.NET MVC web application using Azure Cosmos DB and published it to Azure.</span></span> <span data-ttu-id="fd251-327">O código-fonte do aplicativo completo, incluindo as funcionalidades de detalhes e de exclusão que não foram incluídas neste tutorial, pode ser baixado ou clonado do [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="fd251-327">The source code for the complete application, including the detail and delete functionality that were not included in this tutorial can be downloaded or cloned from [GitHub][GitHub].</span></span> <span data-ttu-id="fd251-328">Portanto, se você estiver interessado em adicioná-las ao seu aplicativo, obtenha o código e adicione-o a esse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fd251-328">So if you're interested in adding that to your app, grab the code and add it to this app.</span></span>

<span data-ttu-id="fd251-329">Para adicionar outras funcionalidades a seu aplicativo, examine as APIs disponíveis na [Biblioteca .NET do Azure Cosmos DB](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) e fique à vontade para contribuir com essa biblioteca no [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="fd251-329">To add additional functionality to your application, review the APIs available in the [Azure Cosmos DB .NET Library](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) and feel free to contribute to the Azure Cosmos DB .NET Library on [GitHub][GitHub].</span></span> 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app
