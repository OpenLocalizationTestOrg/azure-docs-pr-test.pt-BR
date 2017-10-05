---
title: "Criar um aplicativo Web do Azure que se conecte ao MongoDB em execução em uma máquina virtual"
description: "Um tutorial que ensina como usar o Git para implantar um aplicativo ASP.NET no Serviço de Aplicativo do Azure, conectado ao MongoDB em uma Máquina Virtual do Azure."
tags: azure-portal
services: app-service\web, virtual-machines
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: adf7a472-ae00-45a8-aec4-06247e21318b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/29/2016
ms.author: cephalin
ms.openlocfilehash: a3f289ed9c764d0859573de4f834e042d0f103c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-in-azure-that-connects-to-mongodb-running-on-a-virtual-machine"></a><span data-ttu-id="2d822-103">Criar um aplicativo Web do Azure que se conecte ao MongoDB em execução em uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="2d822-103">Create a web app in Azure that connects to MongoDB running on a virtual machine</span></span>
<span data-ttu-id="2d822-104">Usando Git, é possível implantar um aplicativo ASP.NET em Aplicativos Web do Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="2d822-104">Using Git, you can deploy an ASP.NET application to Azure App Service Web Apps.</span></span> <span data-ttu-id="2d822-105">Neste tutorial, você compilará um aplicativo de lista de tarefas MVC do ASP.NET de front-end simples que se conecta a um banco de dados MongoDB em execução em uma máquina virtual no Azure.</span><span class="sxs-lookup"><span data-stu-id="2d822-105">In this tutorial, you will build a simple front-end ASP.NET MVC task list application that connects to a MongoDB database running on a virtual machine in Azure.</span></span>  <span data-ttu-id="2d822-106">[O MongoDB][MongoDB] é um popular banco de dados NoSQL de código-fonte aberto e de alto desempenho.</span><span class="sxs-lookup"><span data-stu-id="2d822-106">[MongoDB][MongoDB] is a popular open source, high performance NoSQL database.</span></span> <span data-ttu-id="2d822-107">Depois de executar e testar o aplicativo ASP.NET no computador de desenvolvimento, você carregará o aplicativo nos Aplicativos Web do Serviço de Aplicativo usando Git.</span><span class="sxs-lookup"><span data-stu-id="2d822-107">After running and testing the ASP.NET application on your development computer, you will upload the application to App Service Web Apps using Git.</span></span>

> [!NOTE]
> <span data-ttu-id="2d822-108">Se desejar começar a usar o Serviço de Aplicativo do Azure antes de inscrever-se em uma conta do Azure, vá para [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo Web inicial de curta duração no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2d822-108">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="2d822-109">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="2d822-109">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="background-knowledge"></a><span data-ttu-id="2d822-110">Conhecimento prévio</span><span class="sxs-lookup"><span data-stu-id="2d822-110">Background knowledge</span></span>
<span data-ttu-id="2d822-111">O conhecimento dos seguintes itens é útil para este tutorial, embora não seja obrigatório:</span><span class="sxs-lookup"><span data-stu-id="2d822-111">Knowledge of the following is useful for this tutorial, though not required:</span></span>

* <span data-ttu-id="2d822-112">O driver do C# para MongoDB.</span><span class="sxs-lookup"><span data-stu-id="2d822-112">The C# driver for MongoDB.</span></span> <span data-ttu-id="2d822-113">Para obter mais informações sobre como desenvolver aplicativos do C# para MongoDB, consulte o MongoDB [Central da linguagem CSharp][MongoC#LangCenter].</span><span class="sxs-lookup"><span data-stu-id="2d822-113">For more information on developing C# applications against MongoDB, see the MongoDB [CSharp Language Center][MongoC#LangCenter].</span></span> 
* <span data-ttu-id="2d822-114">A estrutura do aplicativo Web do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="2d822-114">The ASP .NET web application framework.</span></span> <span data-ttu-id="2d822-115">É possível aprender tudo sobre ela no [Site do ASP.NET][ASP.NET].</span><span class="sxs-lookup"><span data-stu-id="2d822-115">You can learn all about it at the [ASP.net website][ASP.NET].</span></span>
* <span data-ttu-id="2d822-116">A estrutura do aplicativo Web MVC do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="2d822-116">The ASP .NET MVC web application framework.</span></span> <span data-ttu-id="2d822-117">É possível aprender tudo sobre ela no [Site do ASP.NET MVC][MVCWebSite].</span><span class="sxs-lookup"><span data-stu-id="2d822-117">You can learn all about it at the [ASP.NET MVC website][MVCWebSite].</span></span>
* <span data-ttu-id="2d822-118">Azure.</span><span class="sxs-lookup"><span data-stu-id="2d822-118">Azure.</span></span> <span data-ttu-id="2d822-119">Você pode começar lendo em [Azure][WindowsAzure].</span><span class="sxs-lookup"><span data-stu-id="2d822-119">You can get started reading at [Azure][WindowsAzure].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d822-120">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2d822-120">Prerequisites</span></span>
* <span data-ttu-id="2d822-121">[Visual Studio Express 2013 para Web][VSEWeb] ou [Visual Studio 2013][VSUlt]</span><span class="sxs-lookup"><span data-stu-id="2d822-121">[Visual Studio Express 2013 for Web][VSEWeb] or [Visual Studio 2013][VSUlt]</span></span>
* [<span data-ttu-id="2d822-122">SDK do Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="2d822-122">Azure SDK for .NET</span></span>](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* <span data-ttu-id="2d822-123">Uma assinatura ativa do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="2d822-123">An active Microsoft Azure subscription</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a><span data-ttu-id="2d822-124">Criar uma máquina virtual e instalar MongoDB</span><span class="sxs-lookup"><span data-stu-id="2d822-124">Create a virtual machine and install MongoDB</span></span>
<span data-ttu-id="2d822-125">Este tutorial supõe que você tenha criado uma máquina virtual no Azure.</span><span class="sxs-lookup"><span data-stu-id="2d822-125">This tutorial assumes you have created a virtual machine in Azure.</span></span> <span data-ttu-id="2d822-126">Depois de criar a máquina virtual, você precisa instalar o MongoDB na máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="2d822-126">After creating the virtual machine you need to install MongoDB on the virtual machine:</span></span>

* <span data-ttu-id="2d822-127">Para criar uma máquina virtual do Windows e instalar MongoDB, consulte [Instalar MongoDB em uma máquina virtual executando o Windows Server no Azure][InstallMongoOnWindowsVM].</span><span class="sxs-lookup"><span data-stu-id="2d822-127">To create a Windows virtual machine and install MongoDB, see [Install MongoDB on a virtual machine running Windows Server in Azure][InstallMongoOnWindowsVM].</span></span>

<span data-ttu-id="2d822-128">Depois de criar a máquina virtual no Azure e instalar MongoDB, não se esqueça do nome DNS da máquina virtual ("testlinuxvm.cloudapp.net", por exemplo) e da porta externa de MongoDB que você especificou no ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="2d822-128">After you have created the virtual machine in Azure and installed MongoDB, be sure to remember the DNS name of the virtual machine ("testlinuxvm.cloudapp.net", for example) and the external port for MongoDB that you specified in the endpoint.</span></span>  <span data-ttu-id="2d822-129">Você precisará dessas informações mais tarde no tutorial.</span><span class="sxs-lookup"><span data-stu-id="2d822-129">You will need this information later in the tutorial.</span></span>

<a id="createapp"></a>

## <a name="create-the-application"></a><span data-ttu-id="2d822-130">Criar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="2d822-130">Create the application</span></span>
<span data-ttu-id="2d822-131">Nesta seção, você criará um aplicativo ASP.NET chamado "Minha Lista de Tarefas" usando o Visual Studio e realizará uma implantação inicial nos Aplicativos Web do Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="2d822-131">In this section you will create an ASP.NET application called "My Task List" by using Visual Studio and perform an initial deployment to Azure App Service Web Apps.</span></span> <span data-ttu-id="2d822-132">Você executará o aplicativo localmente, mas ele se conectará à máquina virtual no Azure e usará a instância de MongoDB que você criou aqui.</span><span class="sxs-lookup"><span data-stu-id="2d822-132">You will run the application locally, but it will connect to your virtual machine on Azure and use the MongoDB instance that you created there.</span></span>

1. <span data-ttu-id="2d822-133">No Visual Studio, clique em **Novo Projeto**.</span><span class="sxs-lookup"><span data-stu-id="2d822-133">In Visual Studio, click **New Project**.</span></span>
   
    ![Iniciar página Novo Projeto][StartPageNewProject]
2. <span data-ttu-id="2d822-135">Na janela **Novo Projeto**, no painel à esquerda, escolha **Visual C#** e, em seguida, **Web**.</span><span class="sxs-lookup"><span data-stu-id="2d822-135">In the **New Project** window, in the left pane, select **Visual C#**, and then select **Web**.</span></span> <span data-ttu-id="2d822-136">No painel do meio, escolha **Aplicativo Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="2d822-136">In the middle pane, select **ASP.NET  Web Application**.</span></span> <span data-ttu-id="2d822-137">Na parte inferior, dê ao projeto o nome de "MyTaskListApp" e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="2d822-137">At the bottom, name your project "MyTaskListApp," and then click **OK**.</span></span>
   
    ![Caixa de diálogo Novo Projeto][NewProjectMyTaskListApp]
3. <span data-ttu-id="2d822-139">Na caixa de diálogo **Novo Projeto ASP.NET**, escolha **MVC** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="2d822-139">In the **New ASP.NET Project** dialog box, select **MVC**, and then click **OK**.</span></span>
   
    ![Selecionar modelo do MVC][VS2013SelectMVCTemplate]
4. <span data-ttu-id="2d822-141">Se você ainda não tiver entrado no Microsoft Azure, será solicitada a sua conexão.</span><span class="sxs-lookup"><span data-stu-id="2d822-141">If you aren't already signed into Microsoft Azure, you will be prompted to sign in.</span></span> <span data-ttu-id="2d822-142">Siga os prompts para entrar no Azure.</span><span class="sxs-lookup"><span data-stu-id="2d822-142">Follow the prompts to sign into Azure.</span></span>
5. <span data-ttu-id="2d822-143">Depois de se conectar, você poderá começar a configurar seu aplicativo Web do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2d822-143">Once you are signed in, you can start configuring your App Service web app.</span></span> <span data-ttu-id="2d822-144">Especifique o **Nome do Aplicativo Web**, o **plano do Serviço de Aplicativo**, o **Grupo de recursos** e a **Região** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2d822-144">Specify the **Web App name**, **App Service plan**, **Resource group**, and **Region**, then click **Create**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. <span data-ttu-id="2d822-145">Após a conclusão da criação do projeto, espere até que o aplicativo Web seja criado no Serviço de Aplicativo do Azure, conforme indicado na janela **Atividade do Serviço de Aplicativo do Azure** .</span><span class="sxs-lookup"><span data-stu-id="2d822-145">After the project creation completes, wait for the web app to be created in Azure App Service as indicated in the **Azure App Service Activity** window.</span></span> <span data-ttu-id="2d822-146">Em seguida, clique em **Publicar MyTaskListApp para este Aplicativo Web agora**.</span><span class="sxs-lookup"><span data-stu-id="2d822-146">Then, click **Publish MyTaskListApp to this Web App now**.</span></span>
7. <span data-ttu-id="2d822-147">Clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="2d822-147">Click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    <span data-ttu-id="2d822-148">Depois que o aplicativo ASP.NET padrão for publicado nos Aplicativos Web do Serviço de Aplicativo do Azure, ele será iniciado no navegador.</span><span class="sxs-lookup"><span data-stu-id="2d822-148">Once your default ASP.NET application is published to Azure App Service Web Apps, it will be launched in the browser.</span></span>

## <a name="install-the-mongodb-c-driver"></a><span data-ttu-id="2d822-149">Instalar o driver do C# para MongoDB</span><span class="sxs-lookup"><span data-stu-id="2d822-149">Install the MongoDB C# driver</span></span>
<span data-ttu-id="2d822-150">O MongoDB dá suporte do lado do cliente para aplicativos do C# por meio de um driver, que você precisa instalar no computador de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="2d822-150">MongoDB offers client-side support for C# applications through a driver, which you need to install on your local development computer.</span></span> <span data-ttu-id="2d822-151">O driver do C# está disponível por meio de NuGet.</span><span class="sxs-lookup"><span data-stu-id="2d822-151">The C# driver is available through NuGet.</span></span>

<span data-ttu-id="2d822-152">Para instalar o driver do C# para MongoDB:</span><span class="sxs-lookup"><span data-stu-id="2d822-152">To install the MongoDB C# driver:</span></span>

1. <span data-ttu-id="2d822-153">No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto **MyTaskListApp** e escolha **Gerenciar NuGetPackages**.</span><span class="sxs-lookup"><span data-stu-id="2d822-153">In **Solution Explorer**, right-click the **MyTaskListApp** project and select **Manage NuGetPackages**.</span></span>
   
    ![Gerenciar Pacotes NuGet][VS2013ManageNuGetPackages]
2. <span data-ttu-id="2d822-155">Na janela **Gerenciar Pacotes NuGet**, no painel à esquerda, clique em **Online**.</span><span class="sxs-lookup"><span data-stu-id="2d822-155">In the **Manage NuGet Packages** window, in the left pane, click **Online**.</span></span> <span data-ttu-id="2d822-156">Na caixa **Pesquisar Online** à direita, digite "mongodb.driver".</span><span class="sxs-lookup"><span data-stu-id="2d822-156">In the **Search Online** box on the right, type "mongodb.driver".</span></span>  <span data-ttu-id="2d822-157">Clique em **Instalar** para instalar o driver.</span><span class="sxs-lookup"><span data-stu-id="2d822-157">Click **Install** to install the driver.</span></span>
   
    ![Procurar o driver do C# para MongoDB][SearchforMongoDBCSharpDriver]
3. <span data-ttu-id="2d822-159">Clique em **Aceito** para aceitar os termos de licença da 10gen, Inc.</span><span class="sxs-lookup"><span data-stu-id="2d822-159">Click **I Accept** to accept the 10gen, Inc. license terms.</span></span>
4. <span data-ttu-id="2d822-160">Clique em **Fechar** depois que o driver for instalado.</span><span class="sxs-lookup"><span data-stu-id="2d822-160">Click **Close** after the driver has installed.</span></span>
    <span data-ttu-id="2d822-161">![Driver do C# para MongoDB instalado][MongoDBCsharpDriverInstalled]</span><span class="sxs-lookup"><span data-stu-id="2d822-161">![MongoDB C# Driver Installed][MongoDBCsharpDriverInstalled]</span></span>

<span data-ttu-id="2d822-162">O driver do C# para MongoDB agora está instalado.</span><span class="sxs-lookup"><span data-stu-id="2d822-162">The MongoDB C# driver is now installed.</span></span>  <span data-ttu-id="2d822-163">Referências às bibliotecas **MongoDB.Bson**, **MongoDB.Driver** e **MongoDB.Driver.Core** foram adicionadas ao projeto.</span><span class="sxs-lookup"><span data-stu-id="2d822-163">References to the **MongoDB.Bson**, **MongoDB.Driver**, and **MongoDB.Driver.Core**  libraries have been added to the project.</span></span>

![Referências do driver do C# para MongoDB][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a><span data-ttu-id="2d822-165">Adicionar um modelo</span><span class="sxs-lookup"><span data-stu-id="2d822-165">Add a model</span></span>
<span data-ttu-id="2d822-166">No **Gerenciador de Soluções**, clique com o botão direito do mouse na pasta *Modelos* e **adicione** uma nova **Classe**, dando a ela o nome de *TaskModel.cs*.</span><span class="sxs-lookup"><span data-stu-id="2d822-166">In **Solution Explorer**, right-click the *Models* folder and **Add** a new **Class** and name it *TaskModel.cs*.</span></span>  <span data-ttu-id="2d822-167">Em *TaskModel.cs*, substitua o código existente pelo seguinte código:</span><span class="sxs-lookup"><span data-stu-id="2d822-167">In *TaskModel.cs*, replace the existing code with the following code:</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MongoDB.Bson.Serialization.Attributes;
    using MongoDB.Bson.Serialization.IdGenerators;
    using MongoDB.Bson;

    namespace MyTaskListApp.Models
    {
        public class MyTask
        {
            [BsonId(IdGenerator = typeof(CombGuidGenerator))]
            public Guid Id { get; set; }

            [BsonElement("Name")]
            public string Name { get; set; }

            [BsonElement("Category")]
            public string Category { get; set; }

            [BsonElement("Date")]
            public DateTime Date { get; set; }

            [BsonElement("CreatedDate")]
            public DateTime CreatedDate { get; set; }

        }
    }

## <a name="add-the-data-access-layer"></a><span data-ttu-id="2d822-168">Adicionar a camada de acesso aos dados</span><span class="sxs-lookup"><span data-stu-id="2d822-168">Add the data access layer</span></span>
<span data-ttu-id="2d822-169">No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto *MyTaskListApp* e **adicione** uma **Nova Pasta** chamada *DAL*.</span><span class="sxs-lookup"><span data-stu-id="2d822-169">In **Solution Explorer**, right-click the *MyTaskListApp* project and **Add** a **New Folder** named *DAL*.</span></span>  <span data-ttu-id="2d822-170">Clique com botão direito do mouse na pasta *DAL* e **adicione** uma nova **Classe**.</span><span class="sxs-lookup"><span data-stu-id="2d822-170">Right-click the *DAL* folder and **Add** a new **Class**.</span></span> <span data-ttu-id="2d822-171">Nomeie o arquivo de classe *Dal.cs*.</span><span class="sxs-lookup"><span data-stu-id="2d822-171">Name the class file *Dal.cs*.</span></span>  <span data-ttu-id="2d822-172">Em *Dal.cs*, substitua o código existente pelo seguinte código:</span><span class="sxs-lookup"><span data-stu-id="2d822-172">In *Dal.cs*, replace the existing code with the following code:</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MyTaskListApp.Models;
    using MongoDB.Driver;
    using MongoDB.Bson;
    using System.Configuration;


    namespace MyTaskListApp
    {
        public class Dal : IDisposable
        {
            private MongoServer mongoServer = null;
            private bool disposed = false;

            // To do: update the connection string with the DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net"
            private string connectionString = "mongodb://mongodbsrv20151211.cloudapp.net";

            // This sample uses a database named "Tasks" and a 
            //collection named "TasksList".  The database and collection 
            //will be automatically created if they don't already exist.
            private string dbName = "Tasks";
            private string collectionName = "TasksList";

            // Default constructor.        
            public Dal()
            {
            }

            // Gets all Task items from the MongoDB server.        
            public List<MyTask> GetAllTasks()
            {
                try
                {
                    var collection = GetTasksCollection();
                    return collection.Find(new BsonDocument()).ToList();
                }
                catch (MongoConnectionException)
                {
                    return new List<MyTask>();
                }
            }

            // Creates a Task and inserts it into the collection in MongoDB.
            public void CreateTask(MyTask task)
            {
                var collection = GetTasksCollectionForEdit();
                try
                {
                    collection.InsertOne(task);
                }
                catch (MongoCommandException ex)
                {
                    string msg = ex.Message;
                }
            }

            private IMongoCollection<MyTask> GetTasksCollection()
            {
                MongoClient client = new MongoClient(connectionString);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }

            private IMongoCollection<MyTask> GetTasksCollectionForEdit()
            {
                MongoClient client = new MongoClient(connectionString);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }

            # region IDisposable

            public void Dispose()
            {
                this.Dispose(true);
                GC.SuppressFinalize(this);
            }

            protected virtual void Dispose(bool disposing)
            {
                if (!this.disposed)
                {
                    if (disposing)
                    {
                        if (mongoServer != null)
                        {
                            this.mongoServer.Disconnect();
                        }
                    }
                }

                this.disposed = true;
            }

            # endregion
        }
    }

## <a name="add-a-controller"></a><span data-ttu-id="2d822-173">Adicionar um controlador</span><span class="sxs-lookup"><span data-stu-id="2d822-173">Add a controller</span></span>
<span data-ttu-id="2d822-174">Abra o arquivo *Controllers\HomeController.cs* no **Gerenciador de Soluções** e substitua o código existente pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="2d822-174">Open the *Controllers\HomeController.cs* file in **Solution Explorer** and replace the existing code with the following:</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.Mvc;
    using MyTaskListApp.Models;
    using System.Configuration;

    namespace MyTaskListApp.Controllers
    {
        public class HomeController : Controller, IDisposable
        {
            private Dal dal = new Dal();
            private bool disposed = false;
            //
            // GET: /MyTask/

            public ActionResult Index()
            {
                return View(dal.GetAllTasks());
            }

            //
            // GET: /MyTask/Create

            public ActionResult Create()
            {
                return View();
            }

            //
            // POST: /MyTask/Create

            [HttpPost]
            public ActionResult Create(MyTask task)
            {
                try
                {
                    dal.CreateTask(task);
                    return RedirectToAction("Index");
                }
                catch
                {
                    return View();
                }
            }

            public ActionResult About()
            {
                return View();
            }

            # region IDisposable

            new protected void Dispose()
            {
                this.Dispose(true);
                GC.SuppressFinalize(this);
            }

            new protected virtual void Dispose(bool disposing)
            {
                if (!this.disposed)
                {
                    if (disposing)
                    {
                        this.dal.Dispose();
                    }
                }

                this.disposed = true;
            }

            # endregion

        }
    }

## <a name="set-up-the-styles"></a><span data-ttu-id="2d822-175">Configurar os estilos</span><span class="sxs-lookup"><span data-stu-id="2d822-175">Set up the styles</span></span>
<span data-ttu-id="2d822-176">Para alterar o título na parte superior da página, abra o arquivo *Views\Shared\\_Layout.cshtml* no **Gerenciador de Soluções** e substitua "Nome do aplicativo" no cabeçalho da barra de navegação por "Aplicativo Minha Lista de Tarefas" para que se pareça com este exemplo:</span><span class="sxs-lookup"><span data-stu-id="2d822-176">To change the title at the top of the page, open the *Views\Shared\\_Layout.cshtml* file in **Solution Explorer** and replace "Application name" in the navbar header with "My Task List Application" so that it looks like this:</span></span>

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

<span data-ttu-id="2d822-177">Para configurar o menu Lista de Tarefas, abra o arquivo *\Views\Home\Index.cshtml* e substitua o código existente pelo seguinte código:</span><span class="sxs-lookup"><span data-stu-id="2d822-177">In order to set up the Task List menu, open the *\Views\Home\Index.cshtml* file and replace the existing code with the following code:</span></span>

    @model IEnumerable<MyTaskListApp.Models.MyTask>

    @{
        ViewBag.Title = "My Task List";
    }

    <h2>My Task List</h2>

    <table border="1">
        <tr>
            <th>Task</th>
            <th>Category</th>
            <th>Date</th>

        </tr>

    @foreach (var item in Model) {
        <tr>
            <td>
                @Html.DisplayFor(modelItem => item.Name)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.Category)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.Date)
            </td>

        </tr>
    }

    </table>
    <div>  @Html.Partial("Create", new MyTaskListApp.Models.MyTask())</div>


<span data-ttu-id="2d822-178">Para adicionar a capacidade de criar uma nova tarefa, clique com botão direito do mouse na pasta *Views\Home\\\* e **adicione** um **Modo de exibição**.</span><span class="sxs-lookup"><span data-stu-id="2d822-178">To add the ability to create a new task, right-click the *Views\Home\\* folder and **Add** a **View**.</span></span>  <span data-ttu-id="2d822-179">Dê ao modo de exibição o nome *Criar*.</span><span class="sxs-lookup"><span data-stu-id="2d822-179">Name the view *Create*.</span></span> <span data-ttu-id="2d822-180">Substitua o código pelo seguinte código:</span><span class="sxs-lookup"><span data-stu-id="2d822-180">Replace the code with the following:</span></span>

    @model MyTaskListApp.Models.MyTask

    <script src="@Url.Content("~/Scripts/jquery-1.10.2.min.js")" type="text/javascript"></script>
    <script src="@Url.Content("~/Scripts/jquery.validate.min.js")" type="text/javascript"></script>
    <script src="@Url.Content("~/Scripts/jquery.validate.unobtrusive.min.js")" type="text/javascript"></script>

    @using (Html.BeginForm("Create", "Home")) {
        @Html.ValidationSummary(true)
        <fieldset>
            <legend>New Task</legend>

            <div class="editor-label">
                @Html.LabelFor(model => model.Name)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Name)
                @Html.ValidationMessageFor(model => model.Name)
            </div>

            <div class="editor-label">
                @Html.LabelFor(model => model.Category)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Category)
                @Html.ValidationMessageFor(model => model.Category)
            </div>

            <div class="editor-label">
                @Html.LabelFor(model => model.Date)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Date)
                @Html.ValidationMessageFor(model => model.Date)
            </div>

            <p>
                <input type="submit" value="Create" />
            </p>
        </fieldset>
    }

<span data-ttu-id="2d822-181">**Gerenciador de soluções** deve ser assim:</span><span class="sxs-lookup"><span data-stu-id="2d822-181">**Solution Explorer** should look like this:</span></span>

![Gerenciador de soluções][SolutionExplorerMyTaskListApp]

## <a name="set-the-mongodb-connection-string"></a><span data-ttu-id="2d822-183">Defina a cadeia de conexão MongoDB.</span><span class="sxs-lookup"><span data-stu-id="2d822-183">Set the MongoDB connection string</span></span>
<span data-ttu-id="2d822-184">No **Gerenciador de soluções**, abra o arquivo *DAL/Dal.cs* .</span><span class="sxs-lookup"><span data-stu-id="2d822-184">In **Solution Explorer**, open the *DAL/Dal.cs* file.</span></span> <span data-ttu-id="2d822-185">Localize a seguinte linha de código:</span><span class="sxs-lookup"><span data-stu-id="2d822-185">Find the following line of code:</span></span>

    private string connectionString = "mongodb://<vm-dns-name>";

<span data-ttu-id="2d822-186">Substitua `<vm-dns-name>` pelo nome DNS da máquina virtual executando MongoDB criado na etapa [Criar uma máquina virtual e instalar o MongoDB][Create a virtual machine and install MongoDB] deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="2d822-186">Replace `<vm-dns-name>` with the DNS name of the virtual machine running MongoDB you created in the [Create a virtual machine and install MongoDB][Create a virtual machine and install MongoDB] step of this tutorial.</span></span>  <span data-ttu-id="2d822-187">Para encontrar o nome DNS da máquina virtual, vá até o portal do Azure, escolha **Máquinas Virtuais** e localize **Nome DNS**.</span><span class="sxs-lookup"><span data-stu-id="2d822-187">To find the DNS name of your virtual machine, go to the Azure Portal, select **Virtual Machines**, and find **DNS Name**.</span></span>

<span data-ttu-id="2d822-188">Se o nome DNS da máquina virtual for "testlinuxvm.cloudapp.net" e MongoDB estiver escutando na porta padrão 27017, a linha da cadeia de conexão do código será assim:</span><span class="sxs-lookup"><span data-stu-id="2d822-188">If the DNS name of the virtual machine is "testlinuxvm.cloudapp.net" and MongoDB is listening on the default port 27017, the connection string line of code will look like:</span></span>

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

<span data-ttu-id="2d822-189">Se o ponto de extremidade da máquina virtual especificar uma porta externa diferente para MongoDB, você poderá especificar a porta na cadeia de conexão:</span><span class="sxs-lookup"><span data-stu-id="2d822-189">If the virtual machine endpoint specifies a different external port for MongoDB, you can specifiy the port in the connection string:</span></span>

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

<span data-ttu-id="2d822-190">Para obter mais informações sobre cadeias de conexão de MongoDB, consulte [Conexões][MongoConnectionStrings].</span><span class="sxs-lookup"><span data-stu-id="2d822-190">For more information on MongoDB connection strings, see [Connections][MongoConnectionStrings].</span></span>

## <a name="test-the-local-deployment"></a><span data-ttu-id="2d822-191">Testar a implantação local</span><span class="sxs-lookup"><span data-stu-id="2d822-191">Test the local deployment</span></span>
<span data-ttu-id="2d822-192">Para executar o aplicativo no computador de desenvolvimento, escolha **Iniciar Depuração** no menu **Depurar** ou pressione **F5**.</span><span class="sxs-lookup"><span data-stu-id="2d822-192">To run your application on your development computer, select **Start Debugging** from the **Debug** menu or hit **F5**.</span></span> <span data-ttu-id="2d822-193">O IIS Express é iniciado, e um navegador abre e inicia a página inicial do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2d822-193">IIS Express starts and a browser opens and launches the application's home page.</span></span>  <span data-ttu-id="2d822-194">É possível adicionar uma nova tarefa, que será adicionada ao banco de dados MongoDB em execução na máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="2d822-194">You can add a new task, which will be added to the MongoDB database running on your virtual machine in Azure.</span></span>

![Aplicativo Minha Lista de Tarefas][TaskListAppBlank]

## <a name="publish-to-azure-app-service-web-apps"></a><span data-ttu-id="2d822-196">Publicar para Aplicativos Web do Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="2d822-196">Publish to Azure App Service Web Apps</span></span>
<span data-ttu-id="2d822-197">Nesta seção, você publicará as alterações feitas nos Aplicativos Web do Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="2d822-197">In this section you will publish your changes to Azure App Service Web Apps.</span></span>

1. <span data-ttu-id="2d822-198">No Gerenciador de Soluções, clique novamente com o botão direito do mouse em **MyTaskListApp** e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="2d822-198">In Solution Explorer, right-click **MyTaskListApp** again and click **Publish**.</span></span>
2. <span data-ttu-id="2d822-199">Clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="2d822-199">Click **Publish**.</span></span>
   
    <span data-ttu-id="2d822-200">Agora você já deve conseguir ver seu aplicativo Web em execução no Serviço de Aplicativo do Azure e acessar o banco de dados do MongoDB em Máquinas Virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="2d822-200">You should now see your web app running in Azure App Service and accessing the MongoDB database in Azure Virtual Machines.</span></span>

## <a name="summary"></a><span data-ttu-id="2d822-201">Resumo</span><span class="sxs-lookup"><span data-stu-id="2d822-201">Summary</span></span>
<span data-ttu-id="2d822-202">Você já implantou o aplicativo ASP.NET com êxito para os Aplicativos Web do Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="2d822-202">You have now successfully deployed your ASP.NET application to Azure App Service Web Apps.</span></span> <span data-ttu-id="2d822-203">Para exibir o aplicativo Web:</span><span class="sxs-lookup"><span data-stu-id="2d822-203">To view the web app:</span></span>

1. <span data-ttu-id="2d822-204">Faça logon no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2d822-204">Log into the Azure Portal.</span></span>
2. <span data-ttu-id="2d822-205">Clique em **Aplicativos Web**.</span><span class="sxs-lookup"><span data-stu-id="2d822-205">Click **Web apps**.</span></span> 
3. <span data-ttu-id="2d822-206">Selecione seu aplicativo Web na lista **Aplicativos Web** .</span><span class="sxs-lookup"><span data-stu-id="2d822-206">Select your web app in the **Web Apps** list.</span></span>

<span data-ttu-id="2d822-207">Para obter mais informações sobre como desenvolver aplicativos do C# para MongoDB, consulte a [Central da linguagem CSharp][MongoC#LangCenter].</span><span class="sxs-lookup"><span data-stu-id="2d822-207">For more information on developing C# applications against MongoDB, see [CSharp Language Center][MongoC#LangCenter].</span></span> 

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

<!-- HYPERLINKS -->

[AzurePortal]: http://manage.windowsazure.com
[WindowsAzure]: http://www.windowsazure.com
[MongoC#LangCenter]: http://docs.mongodb.org/ecosystem/drivers/csharp/
[MVCWebSite]: http://www.asp.net/mvc
[ASP.NET]: http://www.asp.net/
[MongoConnectionStrings]: http://www.mongodb.org/display/DOCS/Connections
[MongoDB]: http://www.mongodb.org
[InstallMongoOnWindowsVM]:../virtual-machines/windows/classic/install-mongodb.md
[VSEWeb]: http://www.microsoft.com/visualstudio/eng/2013-downloads#d-2013-express
[VSUlt]: http://www.microsoft.com/visualstudio/eng/2013-downloads

<!-- IMAGES -->


[StartPageNewProject]: ./media/web-sites-dotnet-store-data-mongodb-vm/NewProject.png
[NewProjectMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/NewProjectMyTaskListApp.png
[VS2013SelectMVCTemplate]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013SelectMVCTemplate.png
[VS2013DefaultMVCApplication]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013DefaultMVCApplication.png
[VS2013ManageNuGetPackages]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013ManageNuGetPackages.png
[SearchforMongoDBCSharpDriver]: ./media/web-sites-dotnet-store-data-mongodb-vm/SearchforMongoDBCSharpDriver.png
[MongoDBCsharpDriverInstalled]: ./media/web-sites-dotnet-store-data-mongodb-vm/MongoDBCsharpDriverInstalled.png
[MongoDBCSharpDriverReferences]: ./media/web-sites-dotnet-store-data-mongodb-vm/MongoDBCSharpDriverReferences.png
[SolutionExplorerMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/SolutionExplorerMyTaskListApp.png
[TaskListAppBlank]: ./media/web-sites-dotnet-store-data-mongodb-vm/TaskListAppBlank.png
[WAWSCreateWebSite]: ./media/web-sites-dotnet-store-data-mongodb-vm/WAWSCreateWebSite.png
[WAWSDashboardMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/WAWSDashboardMyTaskListApp.png
[Image9]: ./media/web-sites-dotnet-store-data-mongodb-vm/RepoReady.png
[Image10]: ./media/web-sites-dotnet-store-data-mongodb-vm/GitInstructions.png
[Image11]: ./media/web-sites-dotnet-store-data-mongodb-vm/GitDeploymentComplete.png

<!-- TOC BOOKMARKS -->
[Create a virtual machine and install MongoDB]: #virtualmachine
[Create and run the My Task List ASP.NET application on your development computer]: #createapp
[Create an Azure web site]: #createwebsite
[Deploy the ASP.NET application to the web site using Git]: #deployapp
